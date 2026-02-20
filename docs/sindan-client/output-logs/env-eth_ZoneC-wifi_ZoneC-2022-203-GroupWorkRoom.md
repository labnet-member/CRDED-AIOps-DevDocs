## 実行環境
- Wi-Fi: ZoneC-2022-203-GroupWorkRoom
- eth0: ZoneC

```bash
tokyo@tokyo-mon01:~/sindan-client/linux $ ip addr show eth0
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 2c:cf:67:e8:b4:73 brd ff:ff:ff:ff:ff:ff
    inet 10.20.22.17/24 brd 10.20.22.255 scope global dynamic noprefixroute eth0
       valid_lft 86045sec preferred_lft 86045sec
    inet6 2001:2f8:1c1:816::ead/128 scope global dynamic noprefixroute 
       valid_lft 86048sec preferred_lft 2648sec
    inet6 fe80::3d1d:fb00:694:d745/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
```

```bash
tokyo@tokyo-mon01:~ $ sudo iw dev wlan0 link
Connected to 04:ab:18:2c:7f:05 (on wlan0)
        SSID: ZoneC-2022-203-GroupWorkRoom
        freq: 5180.0
        RX: 189534 bytes (1487 packets)
        TX: 36624 bytes (318 packets)
        signal: -58 dBm
        rx bitrate: 263.2 MBit/s
        tx bitrate: 433.3 MBit/s
        bss flags: short-slot-time
        dtim period: 1
        beacon int: 100
```

## 実行結果
```bash
tokyo@tokyo-mon01:~/sindan-client/linux $ sudo ./sindan.sh 
Phase 0: Hardware Layer checking...
 hardware information:
  os_info: Debian GNU/Linux 13 (trixie)
  hostname: tokyo-mon01
  hw_info: Raspberry Pi 5 Model B Rev 1.1
  cpu(freq: 2400033792 Hz, volt: 0.8357 V, temp: 55.4 'C)
  clock_state: synchronized=yes
  clock_src: Status: "Contacted time server [2001:418:3ff::53]:123 (2.debian.pool.ntp.org)."
 done.
Phase 1: Datalink Layer checking...
 datalink information:
  datalink status: 1
  type: Wi-Fi, ifname: wlan0
  status: up, mtu: 1500 byte
  ssid: ZoneC-2022-203-GroupWorkRoom, band: 5 GHz, ch: 36 (80 MHz)
  mode: Wi-Fi 3, mcs index: , nss: , rate: 24.0 Mbps
  bssid: 2c:cf:67:e8:b4:74
  rssi: -54 dBm, noise: -256 dBm, quality: 57
  environment:
BSSID,SSID,Mode,Band,Channel,Bandwidth,Security,RSSI
04:ab:18:2c:7f:05,ZoneC-2022-203-GroupWorkRoom,5,5G,36,80,WPA2-Personal,-51.00
c8:28:e5:21:a9:4f,HU-CUP,6,5G,36,20,Open,-54.00
c8:28:e5:21:a9:4e,eduroam,6,5G,36,20,WPA2-Enterprise,-54.00
c8:28:e5:21:a9:4d,0002softbank,6,5G,36,20,WPA2-Enterprise,-54.00
04:ab:18:a2:d4:53,ZoneC-2022-203-GroupWorkRoom,6,5G,44,80,WPA2-Personal,-54.00
80:cc:9c:47:59:09,ZoneB-304-KondoLab,6,5G,48,80,WPA2-Personal,-74.00
be:02:65:22:3b:5c,s-iPhone,6,2.4G,6,,WPA2-Personal,-44.00
6c:70:9f:e7:10:66,Apple Network e71067,4,2.4G,6,,WPA2-Personal,-52.00
04:ab:18:2c:7f:04,ZoneC-2022-203-GroupWorkRoom-G,4,2.4G,7,,WPA2-Personal,-45.00
c8:28:e5:21:a9:41,eduroam,6,2.4G,6,,WPA2-Enterprise,-53.00
00:90:c7:02:51:4b,TIICE-ZB-AP,4,2.4G,7,,WPA2-Personal,-74.00
04:ab:18:a2:d4:52,ZoneC-2022-203-GroupWorkRoom-G,6,2.4G,10,20,WPA2-Personal,-47.00
88:1f:a1:35:6e:86,ZoneC-2044-w3fStudio-css,4,2.4G,11,,WPA2-Personal,-69.00
f0:d8:05:10:71:e1,eduroam,6,2.4G,11,,WPA2-Enterprise,-60.00
f0:d8:05:10:b6:2d,0002softbank,6,5G,64,20,WPA2-Enterprise,-44.00
f0:d8:05:10:b6:2e,eduroam,6,5G,64,20,WPA2-Enterprise,-44.00
f0:d8:05:10:b6:2f,HU-CUP,6,5G,64,20,Open,-44.00
f0:d8:05:10:71:ed,0002softbank,6,5G,108,20,WPA2-Enterprise,-65.00
f0:d8:05:10:71:ee,eduroam,6,5G,108,20,WPA2-Enterprise,-65.00
f0:d8:05:10:71:ef,HU-CUP,6,5G,108,20,Open,-65.00
6c:70:9f:e7:10:67,Apple Network e71067 5GHz,5,5G,116,80,WPA2-Personal,-76.00
 done.
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
Phase 3: Localnet Layer checking...
 ping to IPv4 namesrv: 133.41.4.2
  status: ok, rtt: 2.005 msec, loss: 0 %
 ping to IPv6 namesrv: 2001:2f8:1c1:51::8529:402
  status: ok, rtt: 2.013 msec, loss: 0 %
 ping to IPv4 router: 10.20.22.1
  status: ok, rtt: 2.701 msec, loss: 0 %
 ping to IPv6 router: fe80::212:e2ff:fe36:7b00%wlan0
  status: ok, rtt: 6.327 msec, loss: 0 %
 done.
Phase 4: Globalnet Layer checking...
 pmtud to IPv4 server: 203.178.139.60, from: 10.20.22.19
  pmtu: unmeasurable
 pmtud to IPv4 server: 8.8.8.8, from: 10.20.22.19
  pmtu: unmeasurable
 pmtud to IPv4 server: 1.1.1.1, from: 10.20.22.19
  pmtu: unmeasurable
 ping to IPv6 srv: 2001:4860:4860::8888
  status: ok, rtt: 8.074 msec, loss: 0 %
 ping to IPv6 srv: 2606:4700:4700::1111
  status: ok, rtt: 7.757 msec, loss: 0 %
 ping to IPv6 srv: 2001:200:0:180c::6
  status: ok, rtt: 15.311 msec, loss: 0 %
 traceroute to IPv6 srv: 2001:4860:4860::8888
  path: -,2001:2f8:1c1:6::2,2001:2f8:1c1:5::1,2001:2f8:1c1:1::1,2001:2f8:1c0:7208::4,2001:2f8:ff00:105::1,2001:2f8:ffd0:9e1::2,2001:7fa:7:2:0:1:5169:2,2001:4860:0:1::86ef,2001:4860:0:1::5ec1,2001:4860:4860::8888
 pmtud to IPv6 server: 2001:4860:4860::8888, from: 2001:2f8:1c1:816::eae
  pmtu: 1500 byte
 pmtud to IPv6 server: 2606:4700:4700::1111, from: 2001:2f8:1c1:816::eae
  pmtu: 1500 byte
 pmtud to IPv6 server: 2001:200:0:180c::6, from: 2001:2f8:1c1:816::eae
  pmtu: 1500 byte
 traceroute to IPv4 srv: 8.8.8.8
  path: 10.20.22.1,10.11.6.2,133.41.11.17,-,-,-,-,-,-,-,-,-,-,-,-,-,-,-,-,-
 traceroute to IPv4 srv: 203.178.139.60
  path: 10.20.22.1,10.11.6.2,133.41.11.17,-,-,-,-,-,-,-,-,-,-,-,-,-,-,-,-,-
 traceroute to IPv4 srv: 1.1.1.1
  path: 10.20.22.1,10.11.6.2,133.41.11.17,-,-,-,-,-,-,-,-,-,-,-,-,-,-,-,-,-
 traceroute to IPv6 srv: 2001:200:0:180c::6
  path: -,2001:2f8:1c1:6::2,-,2001:2f8:1c1:1::1,2001:2f8:1c0:7208::4,2001:2f8:ff00:105::1,2001:2f8:ffd0:9df::2,2001:200:0:6020::1,2001:200:0:20::2,2001:200:0:1841::3,2001:200:0:180c::6
 traceroute to IPv6 srv: 2606:4700:4700::1111
  path: -,2001:2f8:1c1:6::2,-,2001:2f8:1c1:1::1,-,2001:2f8:ff00:105::1,2001:2f8:ffd0:9e1::2,2001:7fa:7:2:0:1:3335:1,2400:cb00:767:3::,2606:4700:4700::1111
 ping to IPv4 srv: 8.8.8.8
  status: ng
 ping to IPv4 srv: 1.1.1.1
  status: ng
 ping to IPv4 srv: 203.178.139.60
  status: ng
 done.
Phase 5: DNS Layer checking...
 dns lookup for AAAA record by IPv4 nameserver: 8.8.8.8
  resolve server: dual.sindan-net.com
   status: ok, result(ttl): 2001:200:0:180c::6(30 s), query time: 24 ms
  resolve server: ipv4.sindan-net.com
   status: ok, result(ttl): ( s), query time: 24 ms
  resolve server: ipv6.sindan-net.com
   status: ok, result(ttl): 2001:200:0:180c::6(24 s), query time: 24 ms
 dns lookup for A record by IPv4 nameserver: 8.8.8.8
  resolve server: dual.sindan-net.com
   status: ok, result(ttl): 203.178.139.60(30 s), query time: 24 ms
  resolve server: ipv4.sindan-net.com
   status: ok, result(ttl): 203.178.139.60(30 s), query time: 24 ms
  resolve server: ipv6.sindan-net.com
   status: ok, result(ttl): ( s), query time: 24 ms
 dns lookup for A record by IPv6 nameserver: 2001:2f8:1c1:51::8529:402
  resolve server: dual.sindan-net.com
   status: ok, result(ttl): 203.178.139.60(30 s), query time: 64 ms
  resolve server: ipv4.sindan-net.com
   status: ok, result(ttl): 203.178.139.60(30 s), query time: 20 ms
  resolve server: ipv6.sindan-net.com
   status: ok, result(ttl): ( s), query time: 16 ms
 dns lookup for AAAA record by IPv4 nameserver: 133.41.4.2
  resolve server: dual.sindan-net.com
   status: ok, result(ttl): 2001:200:0:180c::6(30 s), query time: 56 ms
  resolve server: ipv4.sindan-net.com
   status: ok, result(ttl): ( s), query time: 20 ms
  resolve server: ipv6.sindan-net.com
   status: ok, result(ttl): 2001:200:0:180c::6(30 s), query time: 24 ms
 dns lookup for A record by IPv4 nameserver: 133.41.4.2
  resolve server: dual.sindan-net.com
   status: ok, result(ttl): 203.178.139.60(30 s), query time: 68 ms
  resolve server: ipv4.sindan-net.com
   status: ok, result(ttl): 203.178.139.60(30 s), query time: 20 ms
  resolve server: ipv6.sindan-net.com
   status: ok, result(ttl): ( s), query time: 4 ms
 dns lookup for AAAA record by IPv6 nameserver: 2001:4860:4860::8888
  resolve server: dual.sindan-net.com
   status: ok, result(ttl): 2001:200:0:180c::6(30 s), query time: 24 ms
  resolve server: ipv4.sindan-net.com
   status: ok, result(ttl): ( s), query time: 28 ms
  resolve server: ipv6.sindan-net.com
   status: ok, result(ttl): 2001:200:0:180c::6(30 s), query time: 20 ms
 dns lookup for AAAA record by IPv6 nameserver: 2001:2f8:1c1:51::8529:402
  resolve server: dual.sindan-net.com
   status: ok, result(ttl): 2001:200:0:180c::6(30 s), query time: 56 ms
  resolve server: ipv4.sindan-net.com
   status: ok, result(ttl): ( s), query time: 4 ms
  resolve server: ipv6.sindan-net.com
   status: ok, result(ttl): 2001:200:0:180c::6(30 s), query time: 0 ms
 dns lookup for A record by IPv6 nameserver: 2001:4860:4860::8888
  resolve server: dual.sindan-net.com
   status: ok, result(ttl): 203.178.139.60(30 s), query time: 24 ms
  resolve server: ipv4.sindan-net.com
   status: ok, result(ttl): 203.178.139.60(30 s), query time: 20 ms
  resolve server: ipv6.sindan-net.com
   status: ok, result(ttl): ( s), query time: 24 ms
 dns lookup for AAAA record by IPv4 nameserver: 1.1.1.1
  resolve server: dual.sindan-net.com
   status: ok, result(ttl): 2001:200:0:180c::6(30 s), query time: 100 ms
  resolve server: ipv4.sindan-net.com
   status: ok, result(ttl): ( s), query time: 24 ms
  resolve server: ipv6.sindan-net.com
   status: ok, result(ttl): 2001:200:0:180c::6(30 s), query time: 20 ms
 dns lookup for A record by IPv6 nameserver: 2606:4700:4700::1111
  resolve server: dual.sindan-net.com
   status: ok, result(ttl): 203.178.139.60(30 s), query time: 96 ms
  resolve server: ipv4.sindan-net.com
   status: ok, result(ttl): 203.178.139.60(30 s), query time: 24 ms
  resolve server: ipv6.sindan-net.com
   status: ok, result(ttl): ( s), query time: 24 ms
 dns lookup for A record by IPv4 nameserver: 1.1.1.1
  resolve server: dual.sindan-net.com
   status: ok, result(ttl): 203.178.139.60(30 s), query time: 20 ms
  resolve server: ipv4.sindan-net.com
   status: ok, result(ttl): 203.178.139.60(30 s), query time: 156 ms
  resolve server: ipv6.sindan-net.com
   status: ok, result(ttl): ( s), query time: 108 ms
 dns lookup for AAAA record by IPv6 nameserver: 2606:4700:4700::1111
  resolve server: dual.sindan-net.com
   status: ok, result(ttl): 2001:200:0:180c::6(30 s), query time: 108 ms
  resolve server: ipv4.sindan-net.com
   status: ok, result(ttl): ( s), query time: 108 ms
  resolve server: ipv6.sindan-net.com
   status: ok, result(ttl): 2001:200:0:180c::6(30 s), query time: 24 ms
 done.
Phase 6: Application Layer checking...
 portscan to extarnal server: target.sindan-net.com:22 by IPv4
  status: ok
 portscan to extarnal server: target.sindan-net.com:80 by IPv4
  status: ok
 portscan to extarnal server: target.sindan-net.com:443 by IPv4
  status: ok
 portscan to extarnal server: target.sindan-net.com:443 by IPv6
  status: ok
 portscan to extarnal server: target.sindan-net.com:80 by IPv6
  status: ok
 portscan to extarnal server: target.sindan-net.com:22 by IPv6
  status: ok
 curl to extarnal server: www.yahoo.co.jp by IPv4
  status: ok, http status code: 200
 sshkeyscan to extarnal server: fluentd.sindan-net.com by IPv4
  status: ok
 sshkeyscan to extarnal server: fluentd.sindan-net.com by IPv6
  status: ok
 curl to extarnal server: www.wide.ad.jp by IPv6
  status: ok, http status code: 200
 curl to extarnal server: www.wide.ad.jp by IPv4
  status: ok, http status code: 200
 curl to extarnal server: www.google.co.jp by IPv6
  status: ok, http status code: 200
 speedtest to extarnal server: https://api.inonius.net/ by Dualstack
  status: ok
  IPv4 RTT: 15.45 ms
  IPv4 Jitter: 2.21 ms
  IPv4 Download: 175.05 Mbps
  IPv4 Upload: 622.04 Mbps
  IPv4 Timestamp: 1762927082
  IPv4 IP address: 133.41.74.30
  IPv4 Port number: 39023
  IPv4 ISP: AS2506 NTT WEST CHUGOKU CORPORATION
  IPv4 MSS: 1460
  IPv6 RTT: 14.64 ms
  IPv6 Jitter: 0.19 ms
  IPv6 Download: 518.15 Mbps
  IPv6 Upload: 762.53 Mbps
  IPv6 Timestamp: 1762927082
  IPv6 IP address: 2001:2f8:1c1:816::ead
  IPv6 Port number: 40502
  IPv6 ISP: AS2907 Research Organization of Information and Systems, National Institute of Informatics
  IPv6 MSS: 1440
 done.
Phase 7: Create campaign log...
 done.
```