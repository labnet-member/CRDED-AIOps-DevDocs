## 実行環境
- Wi-Fi: なし
- eth0: ZoneC

```bash
tokyo@tokyo-mon01:~/sindan-client/linux $ ip addr show eth0
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 2c:cf:67:e8:b4:73 brd ff:ff:ff:ff:ff:ff
    inet 10.20.22.17/24 brd 10.20.22.255 scope global dynamic noprefixroute eth0
       valid_lft 82823sec preferred_lft 82823sec
    inet6 2001:2f8:1c1:816::ead/128 scope global dynamic noprefixroute 
       valid_lft 85588sec preferred_lft 2188sec
    inet6 fe80::3d1d:fb00:694:d745/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
```

## 実行結果
```bash
tokyo@tokyo-mon01:~/sindan-client/linux $ sudo ./sindan.sh 
Phase 0: Hardware Layer checking...
 hardware information:
  os_info: Debian GNU/Linux 13 (trixie)
  hostname: tokyo-mon01
  hw_info: Raspberry Pi 5 Model B Rev 1.1
  cpu(freq: 1600020224 Hz, volt: 0.7500 V, temp: 50.5 'C)
  clock_state: synchronized=yes
  clock_src: Status: "Contacted time server [2001:df5:f4c0:0:1273:c6ff:fe3e:a07b]:123 (2.debian.pool.ntp.org)."
 done.
Phase 1: Datalink Layer checking...
command failed: Network is down (-100)
 datalink information:
  datalink status: 0
  type: Wi-Fi, ifname: wlan0
  status: down, mtu: 1500 byte
  ssid: , band:  GHz, ch: 36 (80 MHz)
  mode: Wi-Fi , mcs index: , nss: , rate:  Mbps
  bssid: 2c:cf:67:e8:b4:74
  rssi:  dBm, noise:  dBm, quality: 
  environment:
BSSID,SSID,Mode,Band,Channel,Bandwidth,Security,RSSI
 done.
Phase 2: Interface Layer checking...
Error:  - no such connection profile.
 interface information:
  intarface status (IPv4): 1
  IPv4 conf: 
  IPv4 addr: /0.0.0.0
  IPv4 routers: 
  IPv4 namesrv: 133.41.4.2
Error:  - no such connection profile.
  IPv6 conf: 
  IPv6 lladdr: 
Sending ICMPv6 packet: Network is unreachable
  IPv6 routers: 
  IPv6 namesrv: 2001:2f8:1c1:51::8529:402
 done.
Phase 3: Localnet Layer checking...
 ping to IPv6 namesrv: 2001:2f8:1c1:51::8529:402
  status: ok, rtt: 1.945 msec, loss: 0 %
 ping to IPv4 namesrv: 133.41.4.2
  status: ok, rtt: 1.941 msec, loss: 0 %
 done.
Phase 4: Globalnet Layer checking...
 done.
Phase 5: DNS Layer checking...
 done.
Phase 6: Application Layer checking...
 done.
Phase 7: Create campaign log...
 done.
```