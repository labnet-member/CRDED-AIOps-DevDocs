# Grafana のセットアップ手順
- 前提: `/opt` 配下に証明書（certs）がある
- 以下のポートを空けておく
    - **443**（必須）

## 1. `Grafana` に 443 をバインドする権限を与える
[参考](https://github.com/grafana/grafana/issues/1694#issuecomment-1359685543)
```bash
sudo nano /lib/systemd/system/grafana-server.service
```

`[Service]` セクションに以下を追加
```bash
CapabilityBoundingSet=CAP_NET_BIND_SERVICE
AmbientCapabilities=CAP_NET_BIND_SERVICE
PrivateUsers=false
```

> [!WARNING]
> [公式ドキュメント](https://grafana.com/docs/grafana/latest/setup-grafana/configure-grafana/#http_port)では以下のコマンドを使用していたが，バインドできなかった
> ```bash
> sudo setcap 'cap_net_bind_service=+ep' /usr/sbin/grafana-server
> ```

## 2. SSL 設定
### 2-0. issuer を確認
```bash
cd /opt/certs/
/opt/certs$ openssl x509 -in aiops-monitoring.net.hiroshima-u.ac.jp.cer -noout -issuer
issuer=C = JP, O = "SECOM Trust Systems CO.,LTD.", CN = NII Open Domain CA - G7 RSA # G7 RSA
```

### 2-1. 中間 CA 証明書をダウンロード（G7 RSA）
```bash
/opt/certs$ wget https://repo1.secomtrust.net/sppca/nii/odca4/nii-odca4g7rsa.cer
```

### 2-2. サーバ証明書と中間 CA 証明書を一つのファイルに結合
```bash
/opt/certs$ cat aiops-monitoring.net.hiroshima-u.ac.jp.cer nii-odca4g7rsa.cer | sudo tee aiops.pem > /dev/null
```

### 2-3. パーミッション設定
```bash
# 秘密鍵
sudo chown root:grafana /opt/certs/aiops-monitoring.key
sudo chmod 640 /opt/certs/aiops-monitoring.key

# サーバ証明書
sudo chown root:grafana /opt/certs/aiops-monitoring.net.hiroshima-u.ac.jp.cer
sudo chmod 644 /opt/certs/aiops-monitoring.net.hiroshima-u.ac.jp.cer

# 中間 CA（G7）
sudo chown root:grafana /opt/certs/nii-odca4g7rsa.cer
sudo chmod 644 /opt/certs/nii-odca4g7rsa.cer

# PEM
sudo chown root:grafana /opt/certs/aiops.pem
sudo chmod 644 /opt/certs/aiops.pem
```

### 2-4. 最終確認
```bash
/opt/certs$ ls -al
total 32
drwxr-xr-x 2 root root    4096 Nov 26 13:15 .
drwxr-xr-x 3 root root    4096 Nov 22 23:31 ..
-rw-r--r-- 1 root root    1054 Nov 26 00:38 aiops-monitoring.csr
-rw-r----- 1 root grafana 1704 Nov 26 00:37 aiops-monitoring.key
-rw------- 1 root root    1874 Nov 26 00:37 aiops-monitoring.key_pass
-rw-r--r-- 1 root grafana 2594 Nov 26 11:56 aiops-monitoring.net.hiroshima-u.ac.jp.cer
-rw-r--r-- 1 root root    3862 Nov 26 13:15 aiops.pem
-rw-r--r-- 1 root grafana 1268 Dec 15  2020 nii-odca4g7rsa.cer
```

## 3. `Grafana` を HTTPS 化
```bash
sudo nano /etc/grafana/grafana.ini
```

```ini
#################################### Server ####################################
[server]
# Protocol (http, https, h2, socket)
protocol = https

# The http port to use
http_port = 443

# https certs & key file
cert_file = /opt/certs/aiops.pem
cert_key  = /opt/certs/aiops-monitoring.key
```

## 4. `Grafana` 再起動
```bash
$ sudo systemctl restart grafana-server
$ sudo systemctl status grafana-server
● grafana-server.service - Grafana instance
     Loaded: loaded (/usr/lib/systemd/system/grafana-server.service; enabled; preset: enabled)
     Active: active (running) since Wed 2025-11-26 13:43:09 JST; 2h 19min ago
       Docs: http://docs.grafana.org
   Main PID: 43102 (grafana)
      Tasks: 15 (limit: 5242)
     Memory: 81.9M (peak: 116.1M)
        CPU: 53.133s
     CGroup: /system.slice/grafana-server.service
             └─43102 /usr/share/grafana/bin/grafana server --config=/etc/grafana/grafana.ini --pidfile=/run/gra>

Nov 26 15:31:28 aiops-monitoring grafana[43102]: logger=context userId=0 orgId=0 uname= t=2025-11-26T15:31:28.6>
Nov 26 15:31:47 aiops-monitoring grafana[43102]: logger=context userId=1 orgId=1 uname=admin t=2025-11-26T15:31>
Nov 26 15:31:48 aiops-monitoring grafana[43102]: logger=context userId=1 orgId=1 uname=admin t=2025-11-26T15:31>
Nov 26 15:33:10 aiops-monitoring grafana[43102]: logger=cleanup t=2025-11-26T15:33:10.369181121+09:00 level=inf>
Nov 26 15:33:10 aiops-monitoring grafana[43102]: logger=plugins.update.checker t=2025-11-26T15:33:10.686383171+>
Nov 26 15:43:10 aiops-monitoring grafana[43102]: logger=cleanup t=2025-11-26T15:43:10.472817143+09:00 level=inf>
Nov 26 15:43:10 aiops-monitoring grafana[43102]: logger=plugins.update.checker t=2025-11-26T15:43:10.693183171+>
Nov 26 15:44:01 aiops-monitoring grafana[43102]: logger=infra.usagestats t=2025-11-26T15:44:01.383520794+09:00 >
Nov 26 15:53:10 aiops-monitoring grafana[43102]: logger=cleanup t=2025-11-26T15:53:10.361209887+09:00 level=inf>
Nov 26 15:53:10 aiops-monitoring grafana[43102]: logger=plugins.update.checker t=2025-11-26T15:53:10.682350226+
```

### 5. ダッシュボードで起動確認
