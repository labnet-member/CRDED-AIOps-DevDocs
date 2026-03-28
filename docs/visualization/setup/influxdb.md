# `InfluxDB` のセットアップ手順
- 前提: `Telegraf` でブローカにからデータを受信してファイルに出力するところまで確認済み

## 0. バージョン確認（1.x 版ではできない）
```bash
~$ influxd version
InfluxDB v2.7.12 (git: ec9dcde5d6) build_date: 2025-05-20T22:48:39Z
```

## 1. セットアップ
### 1-1. 対話式コマンド
```bash
~$ influx setup
> Welcome to InfluxDB 2.0!
? Please type your primary username admin
? Please type your password *********
? Please type your password again *********
? Please type your primary organization name aiops
? Please type your primary bucket name telegraf
? Please type your retention period in hours, or 0 for infinite 0
? Setup with these parameters?
  Username:          admin
  Organization:      aiops
  Bucket:            telegraf
  Retention Period:  infinite
 Yes
User    Organization    Bucket
admin   aiops           telegraf
```

### 1-2. 自動セットアップコマンド
```bash
influx setup \
  --username admin \
  --password 'YOUR_PASSWORD' \
  --org aiops \
  --bucket telegraf \
  --retention 0 \
  --force
```

### 1-3. HTTP UI
`http://<アドレス>:8086` にブラウザでアクセスすることで設定することも可能

## 2. トークンを確認
`YOUR_TOKEN` の箇所

```bash
sdoi@aiops-monitoring:~$ influx auth list --user admin
ID                      Description     Token        User Name        User ID                 Permissions
0fdb8fef8c7a7000        admin's Token   YOUR_TOKEN   admin           0fdb8fef743a7000 [read:/authorizations write:/authorizations read:/buckets write:/buckets read:/dashboards write:/dashboards read:/orgs write:/orgs read:/sources write:/sources read:/tasks write:/tasks read:/telegrafs write:/telegrafs read:/users write:/users read:/variables write:/variables read:/scrapers write:/scrapers read:/secrets write:/secrets read:/labels write:/labels read:/views write:/views read:/documents write:/documents read:/notificationRules write:/notificationRules read:/notificationEndpoints write:/notificationEndpoints read:/checks write:/checks read:/dbrp write:/dbrp read:/notebooks write:/notebooks read:/annotations write:/annotations read:/remotes write:/remotes read:/replications write:/replications]
```
## 3. `Telegraf` → `InfluxDB` 接続設定
```bash
sudo nano /etc/telegraf/telegraf.conf
```

```toml
###############################################################################
#                            OUTPUT PLUGINS                                   #
###############################################################################

# # Configuration for sending metrics to InfluxDB 2.0
[[outputs.influxdb_v2]]
#   ## The URLs of the InfluxDB cluster nodes.
#   ##
#   ## Multiple URLs can be specified for a single cluster, only ONE of the
#   ## urls will be written to each interval.
#   ##   ex: urls = ["https://us-west-2-1.aws.cloud2.influxdata.com"]
  urls = ["http://127.0.0.1:8086"]
#
#   ## Token for authentication.
  token = "YOUR_TOKEN" # 2. で確認したトークンをここに貼る
#
#   ## Organization is the name of the organization you wish to write to.
  organization = "aiops"
#
#   ## Destination bucket to write into.
  bucket = "telegraf"
#
#   ## Timeout for HTTP messages.
  timeout = "10s"
```

## 4. `Telegraf` 再起動
```bash
$ sudo systemctl restart telegraf
$ sudo systemctl status telegraf
● telegraf.service - Telegraf
     Loaded: loaded (/usr/lib/systemd/system/telegraf.service; enabled; preset: e>
     Active: active (running) since Wed 2025-11-26 12:48:36 JST; 3h 5min ago
       Docs: https://github.com/influxdata/telegraf
   Main PID: 41644 (telegraf)
      Tasks: 9 (limit: 5242)
     Memory: 22.6M (peak: 24.0M)
        CPU: 11.619s
     CGroup: /system.slice/telegraf.service
             └─41644 /usr/bin/telegraf -config /etc/telegraf/telegraf.conf -confi

Nov 26 12:48:36 aiops-monitoring telegraf[41644]: 2025-11-26T03:48:36Z I! Loaded >
Nov 26 12:48:36 aiops-monitoring telegraf[41644]: 2025-11-26T03:48:36Z I! Loaded >
```

## 5. `InfluxDB` にデータが入っているか確認
```bash
$ influx query 'from(bucket:"telegraf") |> range(start: -5m)'
Result: _result
Table: keys: [_start, _stop, _field, _measurement, host, topic]
                   _start:time                      _stop:time           _field:string     _measurement:string             host:string               topic:string                      _time:time                  _value:float
------------------------------  ------------------------------  ----------------------  ----------------------  ----------------------  -------------------------  ------------------------------  ----------------------------
2025-11-26T06:50:07.938261056Z  2025-11-26T06:55:07.938261056Z                   phase           mqtt_consumer        aiops-monitoring  sindan/tokyo-mon01/phase0  2025-11-26T06:51:02.199244233Z                             0
2025-11-26T06:50:07.938261056Z  2025-11-26T06:55:07.938261056Z                   phase           mqtt_consumer        aiops-monitoring  sindan/tokyo-mon01/phase0  2025-11-26T06:54:02.083657037Z                             0
Table: keys: [_start, _stop, _field, _measurement, host, topic]
                   _start:time                      _stop:time           _field:string     _measurement:string             host:string               topic:string                      _time:time                  _value:float
------------------------------  ------------------------------  ----------------------  ----------------------  ----------------------  -------------------------  ------------------------------  ----------------------------
（省略）
```