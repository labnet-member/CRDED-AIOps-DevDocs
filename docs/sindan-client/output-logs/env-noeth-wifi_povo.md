## 実行環境
- Wi-Fi: povo（スマホでテザリング）
- eth0: なし

```bash
tokyo@tokyo-mon01:~/sindan-client/linux $ sudo iw dev wlan0 link
Connected to be:02:65:22:3b:5c (on wlan0)
        SSID: s-iPhone
        freq: 2437.0
        RX: 147310095 bytes (159459 packets)
        TX: 630095981 bytes (467807 packets)
        signal: -34 dBm
        rx bitrate: 72.2 MBit/s
        tx bitrate: 65.0 MBit/s
        bss flags: short-slot-time
        dtim period: 1
        beacon int: 100
```

## 実行結果
```bash
tokyo@tokyo-mon01:~/sindan-client/linux $ sudo iw phy | grep -A10 'Band 1'
        Band 1:
                Capabilities: 0x1020
                        HT20
                        Static SM Power Save
                        RX HT20 SGI
                        No RX STBC
                        Max AMSDU length: 3839 bytes
                        DSSS/CCK HT40
                Maximum RX AMPDU length 65535 bytes (exponent: 0x003)
                Minimum RX AMPDU time spacing: 16 usec (0x07)
                HT TX/RX MCS rate indexes supported: 0-7
```

```bash
tokyo@tokyo-mon01:~/sindan-client/linux $ ./sindan.sh
Phase 0: Hardware Layer checking...
 hardware information:
  os_info: Debian GNU/Linux 13 (trixie)
  hostname: tokyo-mon01
  hw_info: Raspberry Pi 5 Model B Rev 1.1
  cpu(freq: 1500012800 Hz, volt: 0.7500 V, temp: 51.6 'C)
  clock_state: synchronized=yes
  clock_src: Status: "Contacted time server [2001:678:8::123]:123 (2.debian.pool.ntp.org)."
 done.
Phase 1: Datalink Layer checking...
 datalink information:
  datalink status: 1
  type: Wi-Fi, ifname: wlan0
  status: up, mtu: 1500 byte
  ssid: s-iPhone, band: 2.4 GHz, ch: 6 (20 MHz)
  mode: Wi-Fi , mcs index: , nss: , rate: 72.2 Mbps
  bssid: 2c:cf:67:e8:b4:74
  rssi: -37 dBm, noise: -256 dBm, quality: 70
  environment:
BSSID,SSID,Mode,Band,Channel,Bandwidth,Security,RSSI
be:02:65:22:3b:5c,s-iPhone,6,2.4G,6,,WPA2-Personal,-35.00
6c:70:9f:e7:10:66,Apple Network e71067,4,2.4G,6,,WPA2-Personal,-52.00
04:ab:18:2c:7f:04,ZoneC-2022-203-GroupWorkRoom-G,4,2.4G,7,,WPA2-Personal,-44.00
c8:28:e5:21:a9:41,eduroam,6,2.4G,6,,WPA2-Enterprise,-47.00
04:ab:18:a2:d4:52,ZoneC-2022-203-GroupWorkRoom-G,6,2.4G,10,20,WPA2-Personal,-48.00
88:1f:a1:35:6e:86,ZoneC-2044-w3fStudio-css,4,2.4G,11,,WPA2-Personal,-65.00
f0:d8:05:10:b6:21,eduroam,6,2.4G,1,,WPA2-Enterprise,-36.00
04:ab:18:2c:7f:05,ZoneC-2022-203-GroupWorkRoom,5,5G,36,80,WPA2-Personal,-49.00
c8:28:e5:21:a9:4f,HU-CUP,6,5G,36,20,Open,-52.00
c8:28:e5:21:a9:4e,eduroam,6,5G,36,20,WPA2-Enterprise,-52.00
c8:28:e5:21:a9:4d,0002softbank,6,5G,36,20,WPA2-Enterprise,-52.00
04:ab:18:a2:d4:53,ZoneC-2022-203-GroupWorkRoom,6,5G,44,80,WPA2-Personal,-56.00
80:cc:9c:47:59:09,ZoneB-304-KondoLab,6,5G,48,80,WPA2-Personal,-75.00
f0:d8:05:10:b6:2d,0002softbank,6,5G,64,20,WPA2-Enterprise,-42.00
f0:d8:05:10:b6:2e,eduroam,6,5G,64,20,WPA2-Enterprise,-42.00
f0:d8:05:10:b6:2f,HU-CUP,6,5G,64,20,Open,-42.00
c8:28:e5:70:24:0e,eduroam,6,5G,100,20,WPA2-Enterprise,-82.00
c8:28:e5:70:24:0f,HU-CUP,6,5G,100,20,Open,-81.00
f0:d8:05:10:71:ed,0002softbank,6,5G,108,20,WPA2-Enterprise,-65.00
f0:d8:05:10:71:ee,eduroam,6,5G,108,20,WPA2-Enterprise,-65.00
f0:d8:05:10:71:ef,HU-CUP,6,5G,108,20,Open,-65.00
6c:70:9f:e7:10:67,Apple Network e71067 5GHz,5,5G,116,80,WPA2-Personal,-72.00
 done.
Phase 2: Interface Layer checking...
 interface information:
  intarface status (IPv4): 1
  IPv4 conf: auto
  IPv4 addr: 172.20.10.5/255.255.255.240
  IPv4 routers: 172.20.10.1
  IPv4 namesrv: 172.20.10.1
  IPv6 conf: auto
  IPv6 lladdr: fe80::4de3:20be:8c58:1097
  IPv6 RA src addr: fe80::fc66:cfff:fe96:7b64
   IPv6 RA flags: Om
   IPv6 RA hoplimit: 255
   IPv6 RA lifetime: 9000
   IPv6 RA reachable: 19000
   IPv6 RA retransmit: 1000
   IPv6 RA prefix: 2001:268:9bd6:3e10::/64
    flags: LA
    valid time: infinite
    preferred time: infinite
   IPv6 addr: 2001:268:9bd6:3e10:8afa:35bc:c1da:7ad3/64
   intarface status (IPv6): 1
   IPv6 RA rdnss: fe80::fc66:cfff:fe96:7b64
    lifetime: 270
  IPv6 routers: fe80::fc66:cfff:fe96:7b64%wlan0
  IPv6 namesrv:
 done.
Phase 3: Localnet Layer checking...
 ping to IPv4 namesrv: 172.20.10.1
  status: ok, rtt: 10.045 msec, loss: 0 %
 ping to IPv4 router: 172.20.10.1
  status: ok, rtt: 11.516 msec, loss: 0 %
 ping to IPv6 router: fe80::fc66:cfff:fe96:7b64%wlan0
  status: ok, rtt: 8.499 msec, loss: 0 %
 done.
Phase 4: Globalnet Layer checking...
 ping to IPv4 srv: 8.8.8.8
  status: ok, rtt: 56.706 msec, loss: 0 %
 ping to IPv4 srv: 1.1.1.1
  status: ok, rtt: 64.764 msec, loss: 0 %
 ping to IPv6 srv: 2001:4860:4860::8888
  status: ok, rtt: 53.588 msec, loss: 0 %
 ping to IPv6 srv: 2001:200:0:180c::6
  status: ok, rtt: 65.102 msec, loss: 0 %
 ping to IPv6 srv: 2606:4700:4700::1111
  status: ok, rtt: 47.555 msec, loss: 0 %
 ping to IPv4 srv: 203.178.139.60
  status: ok, rtt: 63.727 msec, loss: 0 %
 traceroute to IPv4 srv: 8.8.8.8
  path: 172.20.10.1,-,10.60.196.251,172.25.208.1,172.25.210.254,172.25.65.73,-,27.86.108.189,27.86.108.185,175.129.8.73,27.85.225.1,27.85.134.46,72.14.202.93,192.178.110.59,142.251.48.19,8.8.8.8
 traceroute to IPv4 srv: 1.1.1.1
  path: 172.20.10.1,-,10.60.196.123,172.25.208.1,172.25.210.254,172.25.65.73,-,27.86.108.189,27.86.108.185,175.129.8.65,27.85.225.13,27.85.228.6,103.246.232.134,162.158.4.27,1.1.1.1
 traceroute to IPv4 srv: 203.178.139.60
  path: 172.20.10.1,-,10.60.196.123,172.25.208.1,172.25.210.254,172.25.65.73,-,27.86.108.190,27.86.108.185,175.129.8.65,27.85.132.197,27.80.241.93,27.86.121.178,202.249.2.83,203.178.137.19,203.178.139.60
 pmtud to IPv4 server: 1.1.1.1, from: 172.20.10.5
  pmtu: 1500 byte
 pmtud to IPv4 server: 8.8.8.8, from: 172.20.10.5
  pmtu: 1500 byte
 pmtud to IPv4 server: 203.178.139.60, from: 172.20.10.5
  pmtu: 1500 byte
 pmtud to IPv6 server: 2001:4860:4860::8888, from: 2001:268:9bd6:3e10:8afa:35bc:c1da:7ad3
  pmtu: 1420 byte
 pmtud to IPv6 server: 2606:4700:4700::1111, from: 2001:268:9bd6:3e10:8afa:35bc:c1da:7ad3
  pmtu: 1420 byte
 pmtud to IPv6 server: 2001:200:0:180c::6, from: 2001:268:9bd6:3e10:8afa:35bc:c1da:7ad3
  pmtu: 1420 byte
 traceroute to IPv6 srv: 2001:200:0:180c::6
  path: 2001:268:9bd6:3e10:e0cc:24ba:6c68:5399,2001:268:ea00:c401::fffb,2001:268:ea00:c401::fffb,2001:268:fa71:107a::7,-,2001:268:fa71:107e::1,-,2001:268:f370:d001::e,2001:268:f370:d001::9,-,-,-,-,2001:200:0:fe00::9c4:11,2001:200:0:1841::3,2001:200:0:180c::6
 traceroute to IPv6 srv: 2001:4860:4860::8888
  path: 2001:268:9bd6:3e10:e0cc:24ba:6c68:5399,2001:268:ea00:c401::fffb,2001:268:ea00:c401::fffb,2001:268:fa71:107a::7,-,2001:268:fa71:107e::1,-,2001:268:f370:d001::16,2001:268:f370:d001::11,-,-,-,-,2001:4860:1:1::5ed,2001:4860:0:1::86f1,2001:4860:0:1::17bb,2001:4860:4860::8888
 traceroute to IPv6 srv: 2606:4700:4700::1111
  path: 2001:268:9bd6:3e10:e0cc:24ba:6c68:5399,2001:268:ea00:c401::fffb,2001:268:ea00:c401::fffb,2001:268:fa71:107a::7,-,2001:268:fa71:107e::1,-,2001:268:f370:d001::e,-,-,-,-,-,2001:de8:8:6:0:1:3335:1,2400:cb00:768:3::,2606:4700:4700::1111
 done.
Phase 5: DNS Layer checking...
 dns lookup for A record by IPv4 nameserver: 172.20.10.1
  resolve server: dual.sindan-net.com
   status: ok, result(ttl): 203.178.139.60(39 s), query time: 56 ms
  resolve server: ipv4.sindan-net.com
   status: ok, result(ttl): 203.178.139.60(39 s), query time: 52 ms
  resolve server: ipv6.sindan-net.com
   status: ok, result(ttl): ( s), query time: 4 ms
 dns lookup for AAAA record by IPv4 nameserver: 172.20.10.1
  resolve server: dual.sindan-net.com
   status: ok, result(ttl): 2001:200:0:180c::6(39 s), query time: 52 ms
  resolve server: ipv4.sindan-net.com
   status: ok, result(ttl): ( s), query time: 4 ms
  resolve server: ipv6.sindan-net.com
   status: ok, result(ttl): 2001:200:0:180c::6(39 s), query time: 48 ms
 dns lookup for AAAA record by IPv4 nameserver: 8.8.8.8
  resolve server: dual.sindan-net.com
   status: ok, result(ttl): 2001:200:0:180c::6(30 s), query time: 52 ms
  resolve server: ipv4.sindan-net.com
   status: ok, result(ttl): ( s), query time: 44 ms
  resolve server: ipv6.sindan-net.com
   status: ok, result(ttl): 2001:200:0:180c::6(30 s), query time: 48 ms
 dns lookup for AAAA record by IPv4 nameserver: 1.1.1.1
  resolve server: dual.sindan-net.com
   status: ok, result(ttl): 2001:200:0:180c::6(30 s), query time: 44 ms
  resolve server: ipv4.sindan-net.com
   status: ok, result(ttl): ( s), query time: 40 ms
  resolve server: ipv6.sindan-net.com
   status: ok, result(ttl): 2001:200:0:180c::6(30 s), query time: 48 ms
 dns lookup for AAAA record by IPv6 nameserver: 2606:4700:4700::1111
  resolve server: dual.sindan-net.com
   status: ok, result(ttl): 2001:200:0:180c::6(30 s), query time: 60 ms
  resolve server: ipv4.sindan-net.com
   status: ok, result(ttl): ( s), query time: 40 ms
  resolve server: ipv6.sindan-net.com
   status: ok, result(ttl): 2001:200:0:180c::6(30 s), query time: 48 ms
 dns lookup for AAAA record by IPv6 nameserver: 2001:4860:4860::8888
  resolve server: dual.sindan-net.com
   status: ok, result(ttl): 2001:200:0:180c::6(30 s), query time: 60 ms
  resolve server: ipv4.sindan-net.com
   status: ok, result(ttl): ( s), query time: 52 ms
  resolve server: ipv6.sindan-net.com
   status: ok, result(ttl): 2001:200:0:180c::6(30 s), query time: 52 ms
 dns lookup for A record by IPv4 nameserver: 8.8.8.8
  resolve server: dual.sindan-net.com
   status: ok, result(ttl): 203.178.139.60(30 s), query time: 56 ms
  resolve server: ipv4.sindan-net.com
   status: ok, result(ttl): 203.178.139.60(30 s), query time: 56 ms
  resolve server: ipv6.sindan-net.com
   status: ok, result(ttl): ( s), query time: 48 ms
 dns lookup for A record by IPv6 nameserver: 2001:4860:4860::8888
  resolve server: dual.sindan-net.com
   status: ok, result(ttl): 203.178.139.60(30 s), query time: 64 ms
  resolve server: ipv4.sindan-net.com
   status: ok, result(ttl): 203.178.139.60(30 s), query time: 48 ms
  resolve server: ipv6.sindan-net.com
   status: ok, result(ttl): ( s), query time: 48 ms
 dns lookup for A record by IPv6 nameserver: 2606:4700:4700::1111
  resolve server: dual.sindan-net.com
   status: ok, result(ttl): 203.178.139.60(30 s), query time: 60 ms
  resolve server: ipv4.sindan-net.com
   status: ok, result(ttl): 203.178.139.60(30 s), query time: 136 ms
  resolve server: ipv6.sindan-net.com
   status: ok, result(ttl): ( s), query time: 32 ms
 dns lookup for A record by IPv4 nameserver: 1.1.1.1
  resolve server: dual.sindan-net.com
   status: ok, result(ttl): 203.178.139.60(30 s), query time: 48 ms
  resolve server: ipv4.sindan-net.com
   status: ok, result(ttl): 203.178.139.60(30 s), query time: 148 ms
  resolve server: ipv6.sindan-net.com
   status: ok, result(ttl): ( s), query time: 48 ms
 done.
Phase 6: Application Layer checking...
 portscan to extarnal server: target.sindan-net.com:80 by IPv4
  status: ok
 portscan to extarnal server: target.sindan-net.com:443 by IPv4
  status: ok
 portscan to extarnal server: target.sindan-net.com:22 by IPv4
  status: ok
 curl to extarnal server: www.wide.ad.jp by IPv4
  status: ok, http status code: 200
 curl to extarnal server: www.wide.ad.jp by IPv6
  status: ok, http status code: 200
 portscan to extarnal server: target.sindan-net.com:22 by IPv6
  status: ok
 portscan to extarnal server: target.sindan-net.com:80 by IPv6
  status: ok
 portscan to extarnal server: target.sindan-net.com:443 by IPv6
  status: ok
 curl to extarnal server: www.yahoo.co.jp by IPv4
  status: ok, http status code: 200
 sshkeyscan to extarnal server: fluentd.sindan-net.com by IPv4
  status: ok
 curl to extarnal server: www.google.co.jp by IPv6
  status: ok, http status code: 200
 sshkeyscan to extarnal server: fluentd.sindan-net.com by IPv6
  status: ok
FATA[0072] No server is currently available, please try again later.
 speedtest to extarnal server: https://api.inonius.net/ by Dualstack
  status: ng (1)
 done.
Phase 7: Create campaign log...
 done.
```