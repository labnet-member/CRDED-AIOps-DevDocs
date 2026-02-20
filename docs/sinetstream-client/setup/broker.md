# SINETStream 用ブローカのセットアップ手順
- 前提: `/opt` 配下に証明書（certs）と broker1 のサンプルファイル（samples）がある
- 以下のポートを空けておく
    - **443**（必須）

## 1. `conf` をコピー
```bash
sudo cp /opt/samples/emqx.conf /etc/emqx/emqx.conf
sudo cp /opt/samples/acl.conf /etc/emqx/acl.conf
```

## 2. PATH の書き全て
- `/etc/emqx/emqx.conf` において，`broker1` となっている箇所をすべて `broker2` に変更
```bash
$ cat /etc/emqx/emqx.conf | grep broker2
                certfile = "/opt/certs/broker1.pem"
                keyfile = "/opt/certs/broker1.key"
        certfile = "/opt/certs/broker1.pem"
        keyfile = "/opt/certs/broker1.key"
```

## 3. `setcap` を使って EMQX に 443 をバインドする権限を与える

```bash
sudo setcap 'cap_net_bind_service=+ep' /usr/lib/emqx/erts-*/bin/beam.smp
sudo setcap 'cap_net_bind_service=+ep' /usr/lib/emqx/bin/emqx
```

## 4. SSL 設定
### 4-0. issuer を確認
```bash
cd /opt/certs/
/opt/certs$ openssl x509 -in broker2.net.hiroshima-u.ac.jp.cer -noout -issuer
issuer=C = JP, O = "SECOM Trust Systems CO.,LTD.", CN = NII Open Domain CA - G7 RSA # G7 RSA
```

### 4-1. 中間 CA 証明書をダウンロード（G7 RSA）
```bash
/opt/certs$ wget https://repo1.secomtrust.net/sppca/nii/odca4/nii-odca4g7rsa.cer
```

### 4-2. サーバ証明書と中間 CA 証明書を一つのファイルに結合
```bash
/opt/certs$ cat broker2.net.hiroshima-u.ac.jp.cer nii-odca4g7rsa.cer | sudo tee broker2.pem > /dev/null
```

### 4-3. パーミッション設定
```bash
# 秘密鍵
sudo chown emqx:emqx /opt/certs/broker2.key
sudo chmod 600 /opt/certs/broker2.key

# サーバ証明書
sudo chown emqx:emqx /opt/certs/broker2.net.hiroshima-u.ac.jp.cer
sudo chmod 644 /opt/certs/broker2.net.hiroshima-u.ac.jp.cer

# 中間 CA（G7）
sudo chown emqx:emqx /opt/certs/nii-odca4g7rsa.cer
sudo chmod 644 /opt/certs/nii-odca4g7rsa.cer

# PEM
sudo chown root:root /opt/certs/broker2.pem
sudo chmod 644 /opt/certs/broker2.pem
```

### 4-4. 最終確認
```bash
/opt/certs$ ls -al
total 36
drwxr-xr-x 2 tkondo tkondo 4096 Nov 19 04:45 .
drwxr-xr-x 4 root   root   4096 Nov 19 02:33 ..
-rw-rw-r-- 1 tkondo tkondo 1041 Nov 14 23:35 broker2.csr
-rw------- 1 emqx   emqx   1704 Nov 14 23:34 broker2.key
-rw------- 1 tkondo tkondo 1874 Nov 14 23:34 broker2.key_pass
-rw-r--r-- 1 emqx   emqx   2573 Nov 17 00:36 broker2.net.hiroshima-u.ac.jp.cer
-rw-r--r-- 1 root   root   4375 Nov 19 04:45 broker2.pem
-rw-r--r-- 1 emqx   emqx   1802 Nov 19 04:44 nii-odca4g7rsa.cer
```

## 5. ブローカ再起動
```bash
$ sudo systemctl restart emqx
$ sudo systemctl status emqx
● emqx.service - emqx daemon
     Loaded: loaded (/usr/lib/systemd/system/emqx.service; enabled; preset: enabled)
     Active: active (running) since Wed 2025-11-19 05:53:23 UTC; 45min ago
   Main PID: 51912 (beam.smp)
      Tasks: 40 (limit: 5240)
     Memory: 394.6M (peak: 410.3M)
        CPU: 1min 40.678s
     CGroup: /system.slice/emqx.service
             ├─51912 emqx -Bd -zdbbl 8192 -spp true -A 4 -IOt 4 -SDio 8 -stbt db -sbwt none -sbwtdcpu none -sbwtdio none -C multi_time_warp -c true -pc unicode -e 262144 -Q 1048576 -P 2097152 >
             ├─52237 erl_child_setup 1048576
             ├─52299 /usr/lib/emqx/lib/os_mon-2.10.1/priv/bin/memsup
             ├─52300 /usr/lib/emqx/lib/os_mon-2.10.1/priv/bin/cpu_sup
             ├─54944 /usr/lib/emqx/erts-15.2.7.1/bin/inet_gethost 4
             └─54945 /usr/lib/emqx/erts-15.2.7.1/bin/inet_gethost 4

Nov 19 05:53:29 broker2 bash[51912]: What Requires a Different License:
Nov 19 05:53:29 broker2 bash[51912]:  - Clustered deployments (more than one node).
Nov 19 05:53:29 broker2 bash[51912]:  - Commercial use in SaaS, hosted services, or embedded/resold products.
Nov 19 05:53:29 broker2 bash[51912]: To enable clustering or use EMQX for external commercial purposes, a commercial license is required.
Nov 19 05:53:29 broker2 bash[51912]: Visit https://emqx.com/apply-licenses/emqx to apply for a license.
Nov 19 05:53:29 broker2 bash[51912]: (Clustering for non-profit or educational purposes may qualify for a free license - please inquire via the link above)
Nov 19 05:53:29 broker2 bash[51912]: =====================================================================
Nov 19 05:53:29 broker2 bash[51912]: Listener http:dashboard on :18083 started.
Nov 19 05:53:29 broker2 bash[51912]: Listener https:dashboard on :18084 started.
Nov 19 05:53:30 broker2 bash[51912]: EMQX Enterprise 6.0.1 is running now!
```

### 5-1. ダッシュボードで起動確認
- 18083 / 18084 のどちらかが必須


![](../../images/broker2.net.hiroshima-u.ac.jp_18084.png)
