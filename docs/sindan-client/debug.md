# SINDAN クライアント実行・デバッグ記録（ZoneC 環境）

> [!WARNING]
> （2026年2月16日追記）元コードが本ドキュメント記載の不具合に対応したため修正は不要（[#13a1b84](https://github.com/SINDAN/sindan-client/commit/13a1b848edd9917f50dd9b1515e2ec772d8b2f99)）

## 実行環境
- Wi-Fi: ZoneC-2022-203-GroupWorkRoom
- eth0: ZoneC

## 実行ログ・デバッグ記録
1. `sindan.sh`をそのまま実行してみる

<details>
<summary>出力結果(途中までになってしまったのであとで貼り直す)</summary>

```bash
tokyo@tokyo-mon01:~/sindan-client/linux $ ./sindan.sh
Phase 0: Hardware Layer checking...
 hardware information:
  os_info: Debian GNU/Linux 13 (trixie)
  hostname: tokyo-mon01
  hw_info: Raspberry Pi 5 Model B Rev 1.1
  cpu(freq: 1700017792 Hz, volt: 0.7500 V, temp: 54.9 'C)
  clock_state: synchronized=yes
  clock_src: Status: "Contacted time server [2400:8902::2000:52ff:fee4:69d9]:123 (2.debi
an.pool.ntp.org)."
 done.
Phase 1: Datalink Layer checking...
command failed: Operation not permitted (-1)
 datalink information:
  datalink status: 1
  type: Wi-Fi, ifname: wlan0
  status: up, mtu: 1500 byte
  ssid: HU-CUP, band: 5 GHz, ch: 64 (20 MHz)
  mode: Wi-Fi 3, mcs index: , nss: , rate: 24.0 Mbps
  bssid: 2c:cf:67:e8:b4:74
  rssi: -44 dBm, noise: -256 dBm, quality: 66
  environment:
  environment:
BSSID,SSID,Mode,Band,Channel,Bandwidth,Security,RSSI
 done.
 done.
Phase 2: Interface Layer checking...
dhcpcd is not running
Phase 2: Interface Layer checking...
dhcpcd is not running
dhcpcd is not running
dhcpcd is not running
dhcpcd is not running
dhcpcd is not running
dhcpcd is not running
dhcpcd is not running
dhcpcd is not running
dhcpcd is not running
dhcpcd is not running
dhcpcd is not running
dhcpcd is not running
dhcpcd is not running
dhcpcd is not running
 interface information:
  intarface status (IPv4): 0
  IPv4 conf: auto
  IPv4 addr: 133.41.189.100/255.255.240.0
  IPv4 routers: 133.41.176.1
  IPv4 namesrv: 133.41.4.2
  IPv6 conf: auto
  IPv6 lladdr: fe80::8da7:4266:5b67:2cd6
  IPv6 RA src addr: fe80::212:e2ff:fe36:7b00
   IPv6 RA flags: Mh
   IPv6 RA hoplimit: 64
   IPv6 RA lifetime: 1800
   IPv6 RA reachable: unspecified
   IPv6 RA retransmit: unspecified
   IPv6 RA prefix: 2001:2f8:1c1:40::/64
    flags: L
    valid time: infinite
    preferred time: infinite
dhcpcd is not running
dhcpcd is not running
dhcpcd is not running
dhcpcd is not running
dhcpcd is not running
dhcpcd is not running
dhcpcd is not running
```
</details>


2. Phase 1・Phase 2・Phase 4・Phase 6 で正常に動かなかったため原因調査

---

> [!WARNING]
> `command failed: Operation not permitted (-1)`
> 
> これは Wi-Fi 情報取得 (`iw` コマンド) に root 権限が必要な処理があるために出ている
> 
> → `sindan.sh` は root で動かすことが前提になっているとのこと

---

> [!CAUTION]
> `dhcpcd is not running`
> 
> これは Raspberry Pi OS Bookworm/Trixie 以降は `NetworkManager` が標準で DHCP を管理しており，古い `dhcpcd` デーモンは停止されている

Raspberry Pi OS最新版(Debian GNU/Linux 13 (trixie))で `dhcpcd`と `NetworkManager` どちらが標準か確認
```bash
tokyo@tokyo-mon01:~/sindan-client $ systemctl status dhcpcd
Unit dhcpcd.service could not be found.

tokyo@tokyo-mon01:~/sindan-client $ systemctl status NetworkManager
● NetworkManager.service - Network Manager
     Loaded: loaded (/usr/lib/systemd/system/NetworkManager.service; enabled>
     Active: active (running) since Fri 2025-11-07 14:36:46 JST; 2h 15min ago
 Invocation: 1797756ebfc94eb98496c282d6d5acbb
       Docs: man:NetworkManager(8)
   Main PID: 749 (NetworkManager)
      Tasks: 4 (limit: 9578)
        CPU: 3.273s
     CGroup: /system.slice/NetworkManager.service
             └─749 /usr/sbin/NetworkManager --no-daemon

Nov 07 15:39:37 tokyo-mon01 NetworkManager[749]: <info>  [1762497577.9647] d>
Nov 07 15:49:49 tokyo-mon01 NetworkManager[749]: <info>  [1762498189.0163] d>
Nov 07 15:54:14 tokyo-mon01 NetworkManager[749]: <info>  [1762498454.9277] d>
Nov 07 16:04:09 tokyo-mon01 NetworkManager[749]: <info>  [1762499049.8158] d>
Nov 07 16:10:03 tokyo-mon01 NetworkManager[749]: <info>  [1762499403.5117] d>
Nov 07 16:19:14 tokyo-mon01 NetworkManager[749]: <info>  [1762499954.4438] d>
Nov 07 16:25:07 tokyo-mon01 NetworkManager[749]: <info>  [1762500307.3192] d>
Nov 07 16:34:13 tokyo-mon01 NetworkManager[749]: <info>  [1762500853.3175] d>
Nov 07 16:40:39 tokyo-mon01 NetworkManager[749]: <info>  [1762501239.7730] d>
Nov 07 16:49:08 tokyo-mon01 NetworkManager[749]: <info>  [1762501748.8473] d>
```

このように `dhcpcd` デーモンは起動していないのに，[sindan_func2.sh](https://github.com/SINDAN/sindan-client/blob/master/linux/sindan_func2.sh#L79-L89) では単にバイナリの有無で情報取得を行おうとしていた

```bash
tokyo@tokyo-mon01:~/sindan-client $ which dhcpcd
/usr/sbin/dhcpcd # dhcpcd のバイナリはある
tokyo@tokyo-mon01:~/sindan-client $ which nmcli
/usr/bin/nmcli # nmcli のバイナリもある
```

該当箇所: [79-89行目](https://github.com/SINDAN/sindan-client/blob/master/linux/sindan_func2.sh#L79-L89)
```shell
if which dhcpcd > /dev/null 2>&1; then
    dhcp_data=$(dhcpcd -4 -U "$1" | sed "s/'//g") # ここで dhcpcd is not running が発生
elif [ -f /var/lib/dhcp/dhclient."$1".leases ]; then
    dhcp_data=$(sed 's/"//g' /var/lib/dhcp/dhclient."$1".leases)
elif which nmcli > /dev/null 2>&1 &&
        [ "$(nmcli networking)" = "enabled" ]; then
    conpath=$(nmcli -g general.con-path device show $1)
    dhcp_data=$(nmcli -g dhcp4 connection show $conpath)
else
    dhcp_data='TBD'
fi
```

そのため，`if` 文の条件式に `systemctl is-active --quiet` を使用し，サービスが起動中かどうかによって使用する DHCP 管理デーモンを選択するように変更([#bbede2a](https://github.com/labnet-member/sindan-client/commit/bbede2a5fc7076e0c75be117daf8042019e4ba15))

---

> [!WARNING]
> - `timeout: failed to run command ‘traceroute’: No such file or directory`
> - `./sindan_func6.sh: line 147: ./bin/inonius_v3cli: No such file or directory`
> 
> これは `traceroute`，`inonius_v3cli` コマンドがインストールされていないために出ている
> 
> そのため，`install.sh` を実行
> 
> ```
> tokyo@tokyo-mon01:~/sindan-client/linux $ ./install.sh
> ```

---

3. 修正後の動作確認


[実行ログ](https://github.com/labnet-member/CRDED-AIOps-DevDocs/blob/main/docs/sindan-client/output-logs/env-eth_ZoneC-wifi_ZoneC-2022-203-GroupWorkRoom.md)を参照


