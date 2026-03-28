# SINDAN クライアントの出力データまとめ

- [公式ドキュメント](https://github.com/SINDAN/sindan-client/blob/master/docs/metrics.md) にも記載

## Phase 0: Hardware Layer
- ハードウェアに関する基礎情報と時刻同期状態

<details>
<summary>出力例</summary>

```bash
Phase 0: Hardware Layer checking...
 hardware information:
  os_info: Debian GNU/Linux 13 (trixie)
  hostname: tokyo-mon01
  hw_info: Raspberry Pi 5 Model B Rev 1.1
  cpu(freq: 1500016128 Hz, volt: 0.7500 V, temp: 49.9 'C)
  clock_state: synchronized=yes
  clock_src: Status: "Contacted time server [2001:678:8::123]:123 (2.debian.pool.ntp.org)."
 done.
```
</details>


| 項目名 | 小項目 | 内容 | 例 |
|--------|--------|------|----|
| **os_info** |  | インストールされているOSの名称とバージョン | Debian GNU/Linux 13 (trixie) |
| **hostname** |  | ホスト名（ネットワーク識別名） | tokyo-mon01 |
| **hw_info** |  | ハードウェアのモデル情報（ボード名・リビジョン） | Raspberry Pi 5 Model B Rev 1.1 |
| **cpu** | freq | CPUの動作クロック周波数（Hz単位） | 1500016128 Hz（約1.5 GHz） |
|  | volt | CPUコア電圧（V） | 0.7500 V |
|  | temp | CPU温度（摂氏） | 49.9 °C |
| **clock_state** |  | システムクロックの同期状態（NTPサーバと同期しているか） | synchronized = yes |
| **clock_src** |  | 同期に使用しているNTPサーバ情報（IPv4/IPv6, ドメイン） | Contacted time server [2001:678:8::123]:123 (2.debian.pool.ntp.org) |


## Phase 1: Datalink Layer
- 通信インタフェースの状態と周囲の無線環境

<details>
<summary>出力例</summary>

```bash
Phase 1: Datalink Layer checking...
 datalink information:
  datalink status: 1
  type: Wi-Fi, ifname: wlan0
  status: up, mtu: 1500 byte
  ssid: ZoneC-2022-203-GroupWorkRoom, band: 5 GHz, ch: 36 (80 MHz)
  mode: Wi-Fi 3, mcs index: , nss: , rate: 24.0 Mbps
  bssid: 2c:cf:67:e8:b4:74
  rssi: -55 dBm, noise: -256 dBm, quality: 55
  environment:
BSSID,SSID,Mode,Band,Channel,Bandwidth,Security,RSSI
04:ab:18:2c:7f:05,ZoneC-2022-203-GroupWorkRoom,5,5G,36,80,WPA2-Personal,-54.00
c8:28:e5:21:a9:4f,HU-CUP,6,5G,36,20,Open,-59.00
c8:28:e5:21:a9:4e,eduroam,6,5G,36,20,WPA2-Enterprise,-58.00
c8:28:e5:21:a9:4d,0002softbank,6,5G,36,20,WPA2-Enterprise,-59.00
04:ab:18:a2:d4:53,ZoneC-2022-203-GroupWorkRoom,6,5G,44,80,WPA2-Personal,-53.00
58:6c:25:4b:ab:09,Zone-C-2022-203-onboarding,,2.4G,1,,WPA2-Personal,-45.00
6c:70:9f:e7:10:66,Apple Network e71067,4,2.4G,6,,WPA2-Personal,-53.00
c8:28:e5:21:a9:41,eduroam,6,2.4G,6,,WPA2-Enterprise,-59.00
04:ab:18:2c:7f:04,ZoneC-2022-203-GroupWorkRoom-G,4,2.4G,7,,WPA2-Personal,-44.00
00:90:c7:02:51:4b,TIICE-ZB-AP,4,2.4G,7,,WPA2-Personal,-67.00
04:ab:18:a2:d4:52,ZoneC-2022-203-GroupWorkRoom-G,6,2.4G,10,20,WPA2-Personal,-52.00
88:1f:a1:35:6e:86,ZoneC-2044-w3fStudio-css,4,2.4G,11,,WPA2-Personal,-63.00
f0:d8:05:10:71:e1,eduroam,6,2.4G,11,,WPA2-Enterprise,-61.00
f0:d8:05:10:b6:2d,0002softbank,6,5G,64,20,WPA2-Enterprise,-45.00
f0:d8:05:10:b6:2e,eduroam,6,5G,64,20,WPA2-Enterprise,-45.00
f0:d8:05:10:b6:2f,HU-CUP,6,5G,64,20,Open,-45.00
f0:d8:05:10:71:ed,0002softbank,6,5G,108,20,WPA2-Enterprise,-72.00
f0:d8:05:10:71:ee,eduroam,6,5G,108,20,WPA2-Enterprise,-72.00
f0:d8:05:10:71:ef,HU-CUP,6,5G,108,20,Open,-73.00
6c:70:9f:e7:10:67,Apple Network e71067 5GHz,5,5G,116,80,WPA2-Personal,-76.00
 done.
```
</details>


| 項目名 | 内容 | 具体例 |
|--------|------|--------|
| **datalink status** | データリンク層の動作状態（1 = 有効／0 = 無効） | 1 |
| **type** | インタフェース種別（Wi-Fi / Ethernet） | Wi-Fi |
| **ifname** | インタフェース名 | wlan0 |
| **status** | インタフェース状態 | up |
| **mtu** | 最大転送単位（バイト） | 1500 byte |
| **ssid** | 接続中の無線LAN名 | ZoneC-2022-203-GroupWorkRoom |
| **band** | 使用周波数帯（2.4 GHz / 5 GHz） | 5 GHz |
| **ch** | チャンネル番号および帯域幅 | 36 (80 MHz) |
| **mode** | Wi-Fi規格（Wi-Fi 3 = IEEE 802.11g） | Wi-Fi 3 |
| **mcs index** | 変調符号化方式（空欄＝取得不可） | *(空)* |
| **nss** | 空間ストリーム数（空欄＝取得不可） | *(空)* |
| **rate** | 現在のリンク速度 | 24.0 Mbps |
| **bssid** | 接続先アクセスポイントのMACアドレス | 2c:cf:67:e8:b4:74 |
| **rssi** | 受信信号強度（負の値で小さいほど弱い） | -55 dBm |
| **noise** | ノイズレベル（ドライバ依存で -256 は未知値） | -256 dBm |
| **quality** | 信号品質（0–100 スケール） | 55 |
| **environment** | 周辺アクセスポイントのスキャン結果（BSSID,SSID,Mode,Band,Channel,Bandwidth,Security,RSSI） | 04\:ab:18:2c:7f:05,ZoneC-2022-203-GroupWorkRoom,5,5G,36,80,WPA2-Personal,-54.00 |

<details>

<summary>なぜ MCS Index / NSS が空欄になるのか</summary>

### 1. ハードウェア概要
- 内蔵チップ：Broadcom BCM43456 (SDIO)
- 対応規格：Wi-Fi 5 (IEEE 802.11ac) まで
  ※Wi-Fi 6 (802.11ax) 以降は非対応
- 周波数帯：2.4 GHz ／ 5 GHz
- 空間ストリーム数：1 （1×1 MIMO）

### 2. 実際の動作モード確認結果

```bash
tokyo@tokyo-mon01:~/sindan-client $ sudo iw dev wlan0 info
Interface wlan0
        ifindex 3
        wdev 0x1
        addr 2c:cf:67:e8:b4:74
        ssid ZoneC-2022-203-GroupWorkRoom
        type managed
        wiphy 0
        channel 36 (5180 MHz), width: 80 MHz, center1: 5210 MHz
        txpower 31.00 dBm
```
```bash
tokyo@tokyo-mon01:~/sindan-client $ sudo iw phy | grep -A5 'Band 1'
        Band 1:
                Capabilities: 0x1020
                        HT20
                        Static SM Power Save
                        RX HT20 SGI
                        No RX STBC
```
→ この出力では HT (802.11n, Wi-Fi 4) モードで動作中
VHT や HE の表記がなく、MCS Index／NSS 情報が存在しないため，
スクリプトで `get_wlan_mcs` や `get_wlan_nss` を実行しても空欄になる
</details>

## Phase 2: Interface Layer
- ネットワークインタフェースの IP 層設定状況

<details>
<summary>出力例</summary>

```bash
Phase 2: Interface Layer checking...
 interface information:
  intarface status (IPv4): 1
  IPv4 conf: auto
  IPv4 addr: 10.20.22.19/255.255.255.0
  IPv4 routers: 10.20.22.1
  IPv4 namesrv: 133.41.4.2
  IPv6 conf: auto
  IPv6 lladdr: fe80::389a:662:2efb:bbeb
  IPv6 RA src addr: fe80::212:e2ff:fe36:7b00
   IPv6 RA flags: Mh
   IPv6 RA hoplimit: 64
   IPv6 RA lifetime: 1800
   IPv6 RA reachable: unspecified
   IPv6 RA retransmit: unspecified
   IPv6 RA prefix: 2001:2f8:1c1:816::/64
    flags: L
    valid time: infinite
    preferred time: infinite
   IPv6 addr: 2001:2f8:1c1:816::eae/64
   intarface status (IPv6): 0
  IPv6 routers: fe80::212:e2ff:fe36:7b00%wlan0
  IPv6 namesrv: 2001:2f8:1c1:51::8529:402
 done.
```
</details>

| 項目名 | 小項目 | 内容 | 具体例 |
|--------|--------|------|--------|
| **interface status (IPv4)** |  | IPv4 の有効状態（1 = 有効，0 = 無効） | 1 |
| **IPv4 conf** |  | IPv4 設定モード（`auto` = DHCP, `manual` = 静的） | auto |
| **IPv4 addr** |  | IPv4アドレスとサブネットマスク | 10.20.22.19 / 255.255.255.0 |
| **IPv4 routers** |  | IPv4デフォルトゲートウェイ | 10.20.22.1 |
| **IPv4 namesrv** |  | IPv4 DNSサーバアドレス | 133.41.4.2 |
| **IPv6 conf** |  | IPv6設定モード（`auto` = DHCP, `manual` = 静的） | auto |
| **IPv6 lladdr** |  | IPv6リンクローカルアドレス | fe80::389a:662:2efb:bbeb |
| **IPv6 RA src addr** | IPv6 RA flags | RA フラグ情報（`M` = Managed, `O` = OtherConf）| Mh |
|  | IPv6 RA hoplimit | 受信した RA パケットの Hop Limit 値 | 64 |
|  | IPv6 RA lifetime | デフォルトルータ有効時間（秒） | 1800 |
|  | IPv6 RA reachable | 到達可能時間（未指定の場合は `unspecified`） | unspecified |
|  | IPv6 RA retransmit | 再送間隔（未指定の場合は `unspecified`） | unspecified |
|  | IPv6 RA prefix | ルータアドバタイズメントで通知されたプレフィックスとその属性<br>・`flags`: L<br>・`valid time`: infinite<br>・`preferred time`: infinite | 2001:2f8:1c1:816::/64 |
| **IPv6 addr** |  | 割り当てられたグローバルIPv6アドレス | 2001:2f8:1c1:816::eae / 64 |
| **interface status (IPv6)** |  | IPv6到達性状態（1 = OK，0 = NG） | 0 |
| **IPv6 routers** |  | IPv6デフォルトルータアドレス | fe80::212:e2ff:fe36:7b00%wlan0 |
| **IPv6 namesrv** |  | IPv6 DNSサーバアドレス | 2001:2f8:1c1:51::8529:402 |

<details>

<summary>IPv6 RA reachable / IPv6 RA reachable が unspecified になってるか確認</summary>

```bash
tokyo@tokyo-mon01:~/sindan-client $ sudo rdisc6 wlan0
Soliciting ff02::2 (ff02::2) on wlan0...

Hop limit                 :           64 (      0x40)
Stateful address conf.    :          Yes
Stateful other conf.      :           No
Mobile home agent         :           No
Router preference         :         high
Neighbor discovery proxy  :           No
Router lifetime           :         1800 (0x00000708) seconds
Reachable time            :  unspecified (0x00000000) # 未指定
Retransmit time           :  unspecified (0x00000000) # 未指定
 Source link-layer address: 00:12:E2:36:7B:00
 MTU                      :         1500 bytes (valid)
 Prefix                   : 2001:2f8:1c1:816::/64
  On-link                 :          Yes
  Autonomous address conf.:           No
  Valid time              :     infinite (0xffffffff)
  Pref. time              :     infinite (0xffffffff)
 from fe80::212:e2ff:fe36:7b00
```
</details>


## Phase 3: Localnet Layer
- ネットワーク内部での疎通状況
- 計測項目:
  - 通信状態（status）
  - 応答遅延（rtt）
  - パケット損失率（loss）
<details>
<summary>出力例</summary>

```bash
Phase 3: Localnet Layer checking...
 ping to IPv4 namesrv: 133.41.4.2
  status: ok, rtt: 2.575 msec, loss: 0 %
 ping to IPv6 namesrv: 2001:2f8:1c1:51::8529:402
  status: ok, rtt: 1.940 msec, loss: 0 %
 ping to IPv4 router: 10.20.22.1
  status: ok, rtt: 67.016 msec, loss: 10 %
 ping to IPv6 router: fe80::212:e2ff:fe36:7b00%wlan0
  status: ok, rtt: 72.283 msec, loss: 10 %
 done.
```
</details>

| 項目名 | 内容 | 具体例 |
|--------|------|--------|
| **ping to IPv4 namesrv** | IPv4 DNSサーバへの疎通確認 | status: ok／rtt: 2.575 ms／loss: 0 % |
| **ping to IPv6 namesrv** | IPv6 DNSサーバへの疎通確認 | status: ok／rtt: 1.940 ms／loss: 0 % |
| **ping to IPv4 router** | IPv4デフォルトルータへの疎通確認 | status: ok／rtt: 67.016 ms／loss: 10 % |
| **ping to IPv6 router** | IPv6デフォルトルータへの疎通確認 | status: ok／rtt: 72.283 ms／loss: 10 % |



## Phase 4: Globalnet Layer
- ネットワーク外部への疎通状況
- 計測項目:
  - 通信状態（status）
  - 応答遅延（rtt）
  - パケット損失率（loss）

<details>
<summary>出力例</summary>

```bash
Phase 4: Globalnet Layer checking...
 pmtud to IPv4 server: 8.8.8.8, from: 10.20.22.19
  pmtu: unmeasurable
 pmtud to IPv4 server: 203.178.139.60, from: 10.20.22.19
  pmtu: unmeasurable
 pmtud to IPv4 server: 1.1.1.1, from: 10.20.22.19
  pmtu: unmeasurable
 ping to IPv6 srv: 2001:4860:4860::8888
  status: ok, rtt: 7.584 msec, loss: 0 %
 ping to IPv6 srv: 2001:200:0:180c::6
  status: ok, rtt: 15.357 msec, loss: 0 %
 ping to IPv6 srv: 2606:4700:4700::1111
  status: ok, rtt: 7.730 msec, loss: 0 %
 pmtud to IPv6 server: 2001:4860:4860::8888, from: 2001:2f8:1c1:816::eae
  pmtu: 1500 byte
 pmtud to IPv6 server: 2606:4700:4700::1111, from: 2001:2f8:1c1:816::eae
  pmtu: 1500 byte
 pmtud to IPv6 server: 2001:200:0:180c::6, from: 2001:2f8:1c1:816::eae
  pmtu: 1500 byte
 traceroute to IPv4 srv: 203.178.139.60
  path: -,10.11.6.2,-,-,-,-,-,-,-,-,-,-,-,-,-,-,-,-,-,-
 traceroute to IPv4 srv: 8.8.8.8
  path: -,10.11.6.2,-,-,-,-,-,-,-,-,-,-,-,-,-,-,-,-,-,-
 traceroute to IPv4 srv: 1.1.1.1
  path: -,10.11.6.2,-,-,-,-,-,-,-,-,-,-,-,-,-,-,-,-,-,-
 traceroute to IPv6 srv: 2001:4860:4860::8888
  path: -,2001:2f8:1c1:6::2,-,2001:2f8:1c1:1::1,2001:2f8:1c0:7208::4,2001:2f8:ff00:105::1,2001:2f8:ffd0:9e1::2,2001:7fa:7:2:0:1:5169:2,-,2001:4860:0:1::17bb,2001:4860:4860::8888
 traceroute to IPv6 srv: 2606:4700:4700::1111
  path: -,2001:2f8:1c1:6::2,-,2001:2f8:1c1:1::1,-,2001:2f8:ff00:105::1,2001:2f8:ffd0:9e1::2,2001:7fa:7:2:0:1:3335:1,2400:cb00:767:3::,2606:4700:4700::1111
 traceroute to IPv6 srv: 2001:200:0:180c::6
  path: -,2001:2f8:1c1:6::2,-,2001:2f8:1c1:1::1,-,2001:2f8:ff00:105::1,2001:2f8:ffd0:9df::2,2001:200:0:6020::1,2001:200:0:20::2,2001:200:0:1841::3,2001:200:0:180c::6
 ping to IPv4 srv: 203.178.139.60
  status: ng
 ping to IPv4 srv: 8.8.8.8
  status: ng
 ping to IPv4 srv: 1.1.1.1
  status: ng
 done.
```
</details>

| 項目名 | 接続先 | 内容 | 具体例 |
|--------|--------|------|--------|
| **ping to IPv4 srv** | 203.178.139.60<br>8.8.8.8<br>1.1.1.1 | IPv4サーバへの疎通確認 | status: ng |
| **ping to IPv6 srv** | 2001:4860:4860::8888<br>2001:200:0:180c::6<br>2606:4700:4700::1111 | IPv6サーバへの疎通確認 | status: ok／rtt: 7.584 ms／loss: 0 % |
| **traceroute (IPv4)** | 203.178.139.60<br>8.8.8.8<br>1.1.1.1 | IPv4ルーティング経路をトレースし，中継ノードの到達状況を確認<br>`-` は応答なしを示す | path: -,10.11.6.2,-,-,-,-,-,-,-,-,-,-,-,-,-,-,-,-,-,- |
| **traceroute (IPv6)** | 2001:4860:4860::8888<br>2606:4700:4700::1111<br>2001:200:0:180c::6 | IPv6ルーティング経路をトレースし，中継ノードの到達状況を確認 | path: -,2001:2f8:1c1:6::2,-,2001:2f8:1c1:1::1,2001:2f8:1c0:7208::4,2001:2f8:ff00:105::1,2001:2f8:ffd0:9e1::2,2001:7fa:7:2:0:1:5169:2,-,2001:4860:0:1::17bb,2001:4860:4860::8888 |
| **pmtud (IPv4)** | 8.8.8.8<br>203.178.139.60<br>1.1.1.1 | IPv4経路におけるPath MTU Discoveryを実施し最小MTU値を測定 | pmtu: unmeasurable（応答なしまたは測定不可） |
| **pmtud (IPv6)** | 2001:4860:4860::8888<br>2606:4700:4700::1111<br>2001:200:0:180c::6 | IPv6経路におけるPath MTU Discoveryを実施し最小MTU値を測定 | pmtu: 1500 byte |

- IPv4でpingとpmtudが取得できないのは，広島大学のファイアウォール設定のため 


## Phase 5: DNS Layer
- ネットワークの名前解決を確認
- 参照サーバ（resolve server）
  - dual.sindan-net.com
  - ipv4.sindan-net.com
  - ipv6.sindan-net.com
- 測定項目: 各参照サーバに対して以下の項目を測定
  - 応答状態（status）
  - TTL（result(ttl)）
  - クエリ時間（query time）
<details>
<summary>出力例</summary>

```bash
Phase 5: DNS Layer checking...
 dns lookup for A record by IPv4 nameserver: 8.8.8.8
  resolve server: dual.sindan-net.com
   status: ok, result(ttl): 203.178.139.60(30 s), query time: 28 ms
  resolve server: ipv4.sindan-net.com
   status: ok, result(ttl): 203.178.139.60(30 s), query time: 84 ms
  resolve server: ipv6.sindan-net.com
   status: ok, result(ttl): ( s), query time: 20 ms
 dns lookup for A record by IPv6 nameserver: 2001:2f8:1c1:51::8529:402
  resolve server: dual.sindan-net.com
   status: ok, result(ttl): 203.178.139.60(30 s), query time: 76 ms
  resolve server: ipv4.sindan-net.com
   status: ok, result(ttl): 203.178.139.60(30 s), query time: 20 ms
  resolve server: ipv6.sindan-net.com
   status: ok, result(ttl): ( s), query time: 20 ms
 dns lookup for A record by IPv4 nameserver: 1.1.1.1
  resolve server: dual.sindan-net.com
   status: ok, result(ttl): 203.178.139.60(30 s), query time: 20 ms
  resolve server: ipv4.sindan-net.com
   status: ok, result(ttl): 203.178.139.60(30 s), query time: 124 ms
  resolve server: ipv6.sindan-net.com
   status: ok, result(ttl): ( s), query time: 12 ms
 dns lookup for A record by IPv4 nameserver: 133.41.4.2
  resolve server: dual.sindan-net.com
   status: ok, result(ttl): 203.178.139.60(30 s), query time: 96 ms
  resolve server: ipv4.sindan-net.com
   status: ok, result(ttl): 203.178.139.60(30 s), query time: 4 ms
  resolve server: ipv6.sindan-net.com
   status: ok, result(ttl): ( s), query time: 16 ms
 dns lookup for AAAA record by IPv4 nameserver: 133.41.4.2
  resolve server: dual.sindan-net.com
   status: ok, result(ttl): 2001:200:0:180c::6(30 s), query time: 96 ms
  resolve server: ipv4.sindan-net.com
   status: ok, result(ttl): ( s), query time: 20 ms
  resolve server: ipv6.sindan-net.com
   status: ok, result(ttl): 2001:200:0:180c::6(30 s), query time: 20 ms
 dns lookup for AAAA record by IPv4 nameserver: 8.8.8.8
  resolve server: dual.sindan-net.com
   status: ok, result(ttl): 2001:200:0:180c::6(30 s), query time: 28 ms
  resolve server: ipv4.sindan-net.com
   status: ok, result(ttl): ( s), query time: 68 ms
  resolve server: ipv6.sindan-net.com
   status: ok, result(ttl): 2001:200:0:180c::6(30 s), query time: 72 ms
 dns lookup for AAAA record by IPv6 nameserver: 2001:2f8:1c1:51::8529:402
  resolve server: dual.sindan-net.com
   status: ok, result(ttl): 2001:200:0:180c::6(30 s), query time: 76 ms
  resolve server: ipv4.sindan-net.com
   status: ok, result(ttl): ( s), query time: 4 ms
  resolve server: ipv6.sindan-net.com
   status: ok, result(ttl): 2001:200:0:180c::6(30 s), query time: 4 ms
 dns lookup for A record by IPv6 nameserver: 2001:4860:4860::8888
  resolve server: dual.sindan-net.com
   status: ok, result(ttl): 203.178.139.60(30 s), query time: 24 ms
  resolve server: ipv4.sindan-net.com
   status: ok, result(ttl): 203.178.139.60(30 s), query time: 28 ms
  resolve server: ipv6.sindan-net.com
   status: ok, result(ttl): ( s), query time: 56 ms
 dns lookup for AAAA record by IPv4 nameserver: 1.1.1.1
  resolve server: dual.sindan-net.com
   status: ok, result(ttl): 2001:200:0:180c::6(30 s), query time: 108 ms
  resolve server: ipv4.sindan-net.com
   status: ok, result(ttl): ( s), query time: 20 ms
  resolve server: ipv6.sindan-net.com
   status: ok, result(ttl): 2001:200:0:180c::6(30 s), query time: 24 ms
 dns lookup for AAAA record by IPv6 nameserver: 2001:4860:4860::8888
  resolve server: dual.sindan-net.com
   status: ok, result(ttl): 2001:200:0:180c::6(30 s), query time: 24 ms
  resolve server: ipv4.sindan-net.com
   status: ok, result(ttl): ( s), query time: 28 ms
  resolve server: ipv6.sindan-net.com
   status: ok, result(ttl): 2001:200:0:180c::6(30 s), query time: 64 ms
 dns lookup for AAAA record by IPv6 nameserver: 2606:4700:4700::1111
  resolve server: dual.sindan-net.com
   status: ok, result(ttl): 2001:200:0:180c::6(30 s), query time: 112 ms
  resolve server: ipv4.sindan-net.com
   status: ok, result(ttl): ( s), query time: 8 ms
  resolve server: ipv6.sindan-net.com
   status: ok, result(ttl): 2001:200:0:180c::6(30 s), query time: 12 ms
 dns lookup for A record by IPv6 nameserver: 2606:4700:4700::1111
  resolve server: dual.sindan-net.com
   status: ok, result(ttl): 203.178.139.60(30 s), query time: 120 ms
  resolve server: ipv4.sindan-net.com
   status: ok, result(ttl): 203.178.139.60(30 s), query time: 96 ms
  resolve server: ipv6.sindan-net.com
   status: ok, result(ttl): ( s), query time: 24 ms
 done.
```
</details>

| 項目名 | 使用DNS | 内容 | 具体例 |
|--------|----------|------|--------|
| **dns lookup for A record by IPv4 nameserver** | 8.8.8.8<br>1.1.1.1<br>133.41.4.2 | IPv4 DNSサーバによるAレコード解決 | status: ok, result(ttl): 203.178.139.60(30 s), query time: 28 ms |
| **dns lookup for A record by IPv6 nameserver** | 2001:2f8:1c1:51::8529:402<br>2001:4860:4860::8888<br>2606:4700:4700::1111 | IPv6 DNSサーバによるAレコード解決 | status: ok, result(ttl): 203.178.139.60(30 s), query time: 76 ms |
| **dns lookup for AAAA record by IPv4 nameserver** | 8.8.8.8<br>1.1.1.1<br>133.41.4.2 | IPv4 DNSサーバによるAAAAレコード解決 | status: ok, result(ttl): 2001:200:0:180c::6(30 s), query time: 108 ms |
| **dns lookup for AAAA record by IPv6 nameserver** | 2001:2f8:1c1:51::8529:402<br>2001:4860:4860::8888<br>2606:4700:4700::1111 | IPv6 DNSサーバによるAAAAレコード解決 | status: ok, result(ttl): 2001:200:0:180c::6(30 s), query time: 76 ms |


## Phase 6: Application Layer
- アプリケーション通信（HTTP, SSH, Speedtest）レベルでの 外部接続性能と信頼性の最終確認

<details>
<summary>出力例</summary>

```bash
Phase 6: Application Layer checking...
 portscan to extarnal server: target.sindan-net.com:80 by IPv4
  status: ok
 portscan to extarnal server: target.sindan-net.com:443 by IPv4
  status: ok
 portscan to extarnal server: target.sindan-net.com:22 by IPv4
  status: ok
 portscan to extarnal server: target.sindan-net.com:80 by IPv6
  status: ok
 portscan to extarnal server: target.sindan-net.com:22 by IPv6
  status: ok
 portscan to extarnal server: target.sindan-net.com:443 by IPv6
  status: ok
 curl to extarnal server: www.wide.ad.jp by IPv4
  status: ok, http status code: 200
 curl to extarnal server: www.yahoo.co.jp by IPv4
  status: ok, http status code: 200
 sshkeyscan to extarnal server: fluentd.sindan-net.com by IPv4
  status: ok
 curl to extarnal server: www.wide.ad.jp by IPv6
  status: ok, http status code: 200
 sshkeyscan to extarnal server: fluentd.sindan-net.com by IPv6
  status: ok
 curl to extarnal server: www.google.co.jp by IPv6
  status: ok, http status code: 200
 speedtest to extarnal server: https://api.inonius.net/ by Dualstack
  status: ok
  IPv4 RTT: 19.73 ms
  IPv4 Jitter: 6.5 ms
  IPv4 Download: 160.5 Mbps
  IPv4 Upload: 652.04 Mbps
  IPv4 Timestamp: 1762835577
  IPv4 IP address: 133.41.74.30
  IPv4 Port number: 9417
  IPv4 ISP: AS2506 NTT WEST CHUGOKU CORPORATION
  IPv4 MSS: 1460
  IPv6 RTT: 15 ms
  IPv6 Jitter: 0 ms
  IPv6 Download: 505.91 Mbps
  IPv6 Upload: 593.02 Mbps
  IPv6 Timestamp: 1762835577
  IPv6 IP address: 2001:2f8:1c1:816::ead
  IPv6 Port number: 60614
  IPv6 ISP: AS2907 Research Organization of Information and Systems, National Institute of Informatics
  IPv6 MSS: 1440
 done.
```
</details>


| 項目名 | 接続先 | 内容 | 具体例 |
|--------|--------|------|--------|
| **portscan by IPv4** | target.sindan-net.com:80<br>target.sindan-net.com:443<br>target.sindan-net.com:22 | IPv4経由で外部サーバのポートスキャンを実施し，各ポートの応答可否を確認 | status: ok |
| **portscan by IPv6** | target.sindan-net.com:80<br>target.sindan-net.com:443<br>target.sindan-net.com:22 | IPv6経由で外部サーバのポートスキャンを実施し，各ポートの応答可否を確認 | status: ok |
| **curl by IPv4** | www.wide.ad.jp<br>www.yahoo.co.jp | IPv4経由でHTTP/HTTPS通信を実施し，応答状態とHTTPステータスコードを確認 | status: ok／http status code: 200 |
| **curl by IPv6** | www.wide.ad.jp<br>www.google.co.jp | IPv6経由でHTTP/HTTPS通信を実施し，応答状態とHTTPステータスコードを確認 | status: ok／http status code: 200 |
| **sshkeyscan by IPv4** | fluentd.sindan-net.com | IPv4経由でSSH鍵スキャンを実行し，サーバ応答を確認 | status: ok |
| **sshkeyscan by IPv6** | fluentd.sindan-net.com | IPv6経由でSSH鍵スキャンを実行し，サーバ応答を確認 | status: ok |
| **speedtest by Dualstack** | https://api.inonius.net/ | IPv4およびIPv6経路でスループット測定を実施し，RTT・Jitter・上下速度・ISP情報などを取得 | IPv4: RTT 19.73 ms／Jitter 6.5 ms／Down 160.5 Mbps／Up 652.04 Mbps<br>IPv6: RTT 15 ms／Jitter 0 ms／Down 505.91 Mbps／Up 593.02 Mbps |
| **speedtest by Dualstack** | https://api.inonius.net/ | IPv4およびIPv6経路でスループット測定を実施し，以下を計測<br>・status<br>・IPv4 RTT<br>・IPv4 Jitter<br>・IPv4 Download<br>・IPv4 Upload<br>・IPv4 Timestamp<br>・IPv4 IP address<br>・IPv4 Port number<br>・IPv4 ISP<br>・IPv4 MSS<br>・IPv6 RTT<br>・IPv6 Jitter<br>・IPv6 Download<br>・IPv6 Upload<br>・IPv6 Timestamp<br>・IPv6 IP address<br>・IPv6 Port number<br>・IPv6 ISP<br>・IPv6 MSS | ・status: ok<br>・IPv4 RTT: 19.73 ms<br>・IPv4 Jitter: 6.5 ms<br>・IPv4 Download: 160.5 Mbps<br>・IPv4 Upload: 652.04 Mbps<br>・IPv4 Timestamp: 1762835577<br>・IPv4 IP address: 133.41.74.30<br>・IPv4 Port number: 9417<br>・IPv4 ISP: AS2506 NTT WEST CHUGOKU CORPORATION<br>・IPv4 MSS: 1460<br>・IPv6 RTT: 15 ms<br>・IPv6 Jitter: 0 ms<br>・IPv6 Download: 505.91 Mbps<br>・IPv6 Upload: 593.02 Mbps<br>・IPv6 Timestamp: 1762835577<br>・IPv6 IP address: 2001:2f8:1c1:816::ead<br>・IPv6 Port number: 60614<br>・IPv6 ISP: AS2907 Research Organization of Information and Systems, National Institute of Informatics<br>・IPv6 MSS: 1440 |


## Phase 7: Log Generation
- これまでの診断結果をまとめて1つのログ（キャンペーンログ）として出力する
- キャンペーンログの例
```json
{
    "log_campaign_uuid": "4f4c854b-a2ae-4cd3-8da7-140c94b6e321",
    "mac_addr": "2c:cf:67:e8:b4:74",
    "os": "Debian GNU/Linux 13 (trixie)",
    "network_type": "Wi-Fi",
    "ssid": "ZoneC-2022-203-GroupWorkRoom",
    "hostname": "tokyo-mon01",
    "version": "6.0.1",
    "occurred_at": "2025-11-11 04:34:04"
}

```

