# パブリッシュされるJSONの例

[SINDAN クライアントの出力データまとめ](https://github.com/labnet-member/CRDED-AIOps-DevDocs/blob/main/docs/sindan-client/sindan-output-reference.md) にはあるが，[元々の SINDAN クライアント](https://github.com/SINDAN/sindan-client/blob/master/linux/sindan.sh) がログとして出力する JSON にはない項目は追加実装（[#41d17d3](https://github.com/labnet-member/sindan-client/commit/41d17d300daf6754fc81b291fdd22dbcaa745b78)）


## Topic: `sindan/{hostname}/phase0`
- ハードウェアに関する基礎情報と時刻同期状態
    - `os_info`，`hostname` を追加
```json
{
  "phase": 0,
  "layer": "hardware",
  "campaign_uuid": "0bd99baa-9f4f-481e-b295-d8dc9c78fcb3",
  "timestamp": "2025-11-25 14:40:13",
  "data": {
    "hostname": "tokyo-mon01",
    "cpu_volt": "0.8329",
    "cpu_freq": "1500019456",
    "clock_state": "synchronized=yes",
    "os_info": "Debian GNU/Linux 13 (trixie)",
    "hw_info": "Raspberry Pi 5 Model B Rev 1.1",
    "cpu_temp": "82.9"
  }
}
``` 

## Topic: `sindan/{hostname}/phase1`
- 通信インタフェースの状態と周囲の無線環境
```json
{
  "phase": 1,
  "layer": "datalink",
  "campaign_uuid": "44d240fb-01c8-4d37-a19d-e7e2ead63530",
  "timestamp": "2025-11-25 15:10:14",
  "data": {
    "wlan_chband": "80",
    "wlan_rate": "433.3",
    "wlan_noise": "-256",
    "wlan_channel": "36",
    "wlan_environment": [
      {
        "BSSID": "04:ab:18:2c:7f:05",
        "SSID": "ZoneC-2022-203-GroupWorkRoom",
        "Mode": "5",
        "Band": "5G",
        "Channel": "36",
        "Bandwidth": "80",
        "Security": "WPA2-Personal",
        "RSSI": "-51.00"
      },
      {
        "BSSID": "f0:d8:05:10:b6:2f",
        "SSID": "HU-CUP",
        "Mode": "6",
        "Band": "5G",
        "Channel": "36",
        "Bandwidth": "20",
        "Security": "Open",
        "RSSI": "-42.00"
      },
      (省略)
      {
        "BSSID": "c8:28:e5:21:a9:4f",
        "SSID": "HU-CUP",
        "Mode": "6",
        "Band": "5G",
        "Channel": "140",
        "Bandwidth": "20",
        "Security": "Open",
        "RSSI": "-54.00"
      }
    ],
    "ifstatus": "up",
    "wlan_quality": "56",
    "iftype": "Wi-Fi",
    "wlan_rssi": "-54",
    "wlan_ssid": "ZoneC-2022-203-GroupWorkRoom",
    "wlan_bssid": "2c:cf:67:e8:b4:74",
    "ifmtu": "1500",
    "wlan_band": "5"
  }
}
```

# Topic: `sindan/{hostname}/phase2`
- ネットワークインタフェースの IP 層設定状況
    - `v4ifstatus`，`v6ifstatus` を追加
```json
{
  "phase": 2,
  "layer": "interface",
  "campaign_uuid": "02d7e07b-fafb-46dc-8c42-6177aa65635b",
  "timestamp": "2025-11-25 15:46:49",
  "data": {
    "v4ifconf": "auto",
    "v6lladdr": "fe80::389a:662:2efb:bbeb",
    "v6ifconf": "auto",
    "netmask": "255.255.255.0",
    "ra_flags": "Mh",
    "ra_pref_len": "64",
    "ra_pref_pltime": "infinite",
    "ra_prefs": "2001:2f8:1c1:816::/64",
    "v6addrs": "2001:2f8:1c1:816::ef3",
    "v4addr": "10.20.22.23",
    "ra_pref_vltime": "infinite",
    "ra_reach": "unspecified",
    "v6routers": "fe80::212:e2ff:fe36:7b00%wlan0",
    "ra_pref_flags": "L",
    "ra_hlim": "64",
    "v6nameservers": "2001:2f8:1c1:51::8529:402",
    "ra_addrs": "fe80::212:e2ff:fe36:7b00",
    "v6ifstatus": "0",
    "ra_retrans": "unspecified",
    "v4nameservers": "133.41.4.2",
    "v4ifstatus": "1",
    "ra_ltime": "1800",
    "v4routers": "10.20.22.1"
  }
}
```

# Topic: `sindan/{hostname}/phase3`
- ネットワーク内部での疎通状況
- 以下を追加
    - `v4status_router`: IPv4 ルータへの ping の status
    - `v4status_namesrv`: IPv4 ネームサーバへの ping の status
    - `v6status_router`: IPv6 ルーターへの ping の status
    - `v6status_namesrv`: IPv6 ネームサーバーへの ping の status
```json
{
  "phase": 3,
  "layer": "localnet",
  "campaign_uuid": "42554fac-f497-4a51-b651-dbfdd8ce6854",
  "timestamp": "2025-11-25 15:56:51",
  "data": {
    "v4rtt_namesrv_dev": "2.245",
    "v6rtt_router_dev": "0.951",
    "v6loss_router": "0",
    "v4loss_router": "0",
    "v4rtt_router_max": "1.771",
    "v4status_router": "1",
    "v4rtt_router_min": "1.437",
    "v6rtt_namesrv_max": "9.778",
    "v6rtt_namesrv_dev": "2.338",
    "v4rtt_namesrv_ave": "2.751",
    "v4rtt_namesrv_max": "9.480",
    "v4rtt_namesrv_min": "1.781",
    "v6rtt_router_min": "3.088",
    "v4rtt_router_dev": "0.120",
    "v4rtt_router_ave": "1.694",
    "v6loss_namesrv": "0",
    "v6rtt_router_max": "5.784",
    "v4status_namesrv": "1",
    "v4loss_namesrv": "0",
    "v6rtt_router_ave": "4.778",
    "v6status_router": "1",
    "v6status_namesrv": "1",
    "v6rtt_namesrv_ave": "2.770",
    "v6rtt_namesrv_min": "1.832"
  }
}
```

# Topic: `sindan/{hostname}/phase4`
- ネットワーク外部への疎通状況
- 以下を追加
    - `v4status_srv`: 外部 IPv4 ネームサーバへの ping の status
    - `v6status_nsrv`: 外部 IPv6 ネームサーバーへの ping の status
```json
{
  "phase": 4,
  "layer": "globalnet",
  "campaign_uuid": "ab77a377-292b-4113-b165-149ef4b935c9",
  "timestamp": "2025-11-25 16:07:06",
  "data": {
    "203.178.139.60": {
      "v4path_srv": "10.20.22.1,10.11.6.2,133.41.11.17,-,-,-,-,-,-,-,-,-,-,-,-,-,-,-,-,-",
      "v4pmtu_srv": "unmeasurable,10.20.22.23",
      "v4status_srv": 0
    },
    "1.1.1.1": {
      "v4path_srv": "10.20.22.1,10.11.6.2,133.41.11.17,-,-,-,-,-,-,-,-,-,-,-,-,-,-,-,-,-",
      "v4pmtu_srv": "unmeasurable,10.20.22.23",
      "v4status_srv": 0
    },
    "2001:200:0:180c::6": {
      "v6pmtu_srv": "1500,2001:2f8:1c1:816::ef3",
      "v6rtt_srv_max": 15.714,
      "v6rtt_srv_dev": 0.163,
      "v6rtt_srv_ave": 15.347,
      "v6loss_srv": 0,
      "v6path_srv": "-,2001:2f8:1c1:6::2,-,2001:2f8:1c1:1::1,-,2001:2f8:ff00:105::1,2001:2f8:ffd0:9df::2,2001:200:0:6020::1,2001:200:0:20::2,2001:200:0:1841::3,2001:200:0:180c::6",
      "v6rtt_srv_min": 15.173,
      "v6status_srv": 1
    },
    "2001:4860:4860::8888": {
      "v6pmtu_srv": "1500,2001:2f8:1c1:816::ef3",
      "v6rtt_srv_max": 7.625,
      "v6path_srv": "-,2001:2f8:1c1:6::2,-,2001:2f8:1c1:1::1,2001:2f8:1c0:7208::4,2001:2f8:ff00:105::1,2001:2f8:ffd0:9e1::2,2001:7fa:7:2:0:1:5169:2,2001:4860:0:1::352d,-,2001:4860:4860::8888",
      "v6status_srv": 1,
      "v6rtt_srv_dev": 0.043,
      "v6loss_srv": 0,
      "v6rtt_srv_ave": 7.541,
      "v6rtt_srv_min": 7.476
    },
    "2606:4700:4700::1111": {
      "v6rtt_srv_max": 8.001,
      "v6status_srv": 1,
      "v6loss_srv": 0,
      "v6rtt_srv_dev": 0.09,
      "v6rtt_srv_min": 7.679,
      "v6pmtu_srv": "1500,2001:2f8:1c1:816::ef3",
      "v6rtt_srv_ave": 7.752,
      "v6path_srv": "-,2001:2f8:1c1:6::2,-,2001:2f8:1c1:1::1,-,2001:2f8:ff00:105::1,2001:2f8:ffd0:9e1::2,2001:7fa:7:2:0:1:3335:1,2400:cb00:767:3::,2606:4700:4700::1111"
    },
    "8.8.8.8": {
      "v4pmtu_srv": "unmeasurable,10.20.22.23",
      "v4status_srv": 0,
      "v4path_srv": "10.20.22.1,10.11.6.2,133.41.11.17,-,-,-,-,-,-,-,-,-,-,-,-,-,-,-,-,-"
    }
  }
}
```


# Topic: `sindan/{hostname}/phase5`
- ネットワークの名前解決を確認
- 以下を追加
    - `v4dnsstatus_A_dual.sindan-net.com`: IPv4 nameserver による A レコードの dual.sindan-net.com への DNS lookup の status
    - `v4dnsstatus_AAAA_ipv6.sindan-net.com`: IPv4 nameserver による AAAA レコードの ipv6.sindan-net.com への DNS lookup の status
    - `v6dnsstatus_A_dual.sindan-net.com`: IPv6 nameserver による A レコードの dual.sindan-net.com への DNS lookup の status
    - `v6dnsstatus_AAAA_ipv6.sindan-net.com`: IPv6 nameserver による AAAA レコードの ipv6.sindan-net.com への DNS lookup の status
```json
{
  "phase": 5,
  "layer": "dns",
  "campaign_uuid": "8612cb87-34f6-4a33-9fbe-59f29aab135f",
  "timestamp": "2025-11-25 16:42:08",
  "data": {
    "2606:4700:4700::1111": {
      "v6dnsrtt_A_ipv6.sindan-net.com": 107,
      "v6dnsttl_A_ipv6.sindan-net.com": "",
      "v6dnsstatus_A_ipv6.sindan-net.com": 1,
      "v6dnsttl_AAAA_ipv4.sindan-net.com": "",
      "v6dnsttl_AAAA_dual.sindan-net.com": 30,
      "v6dnsstatus_AAAA_dual.sindan-net.com": 1,
      "v6dnsstatus_AAAA_ipv6.sindan-net.com": 1,
      "v6dnsttl_A_ipv4.sindan-net.com": 30,
      "v6dnsttl_A_dual.sindan-net.com": 30,
      "v6dnsrtt_AAAA_ipv6.sindan-net.com": 107,
      "v6dnsans_A_dual.sindan-net.com": "203.178.139.60",
      "v6dnsrtt_A_ipv4.sindan-net.com": 27,
      "v6dnsans_A_ipv6.sindan-net.com": "",
      "v6dnsstatus_AAAA_ipv4.sindan-net.com": 1,
      "v6dnsstatus_A_dual.sindan-net.com": 1,
      "v6dnsans_AAAA_dual.sindan-net.com": "2001:200:0:180c::6",
      "v6dnsttl_AAAA_ipv6.sindan-net.com": 30,
      "v6dnsans_AAAA_ipv4.sindan-net.com": "",
      "v6dnsrtt_AAAA_dual.sindan-net.com": 19,
      "v6dnsans_AAAA_ipv6.sindan-net.com": "2001:200:0:180c::6",
      "v6dnsrtt_AAAA_ipv4.sindan-net.com": 19,
      "v6dnsrtt_A_dual.sindan-net.com": 11,
      "v6dnsans_A_ipv4.sindan-net.com": "203.178.139.60",
      "v6dnsstatus_A_ipv4.sindan-net.com": 1
    },
    "8.8.8.8": {
      "v4dnsttl_AAAA_ipv4.sindan-net.com": "",
      "v4dnsttl_AAAA_ipv6.sindan-net.com": 30,
      "v4dnsstatus_A_dual.sindan-net.com": 1,
      "v4dnsrtt_A_ipv4.sindan-net.com": 27,
      "v4dnsrtt_A_dual.sindan-net.com": 23,
      "v4dnsstatus_A_ipv6.sindan-net.com": 1,
      "v4dnsrtt_AAAA_ipv6.sindan-net.com": 23,
      "v4dnsttl_A_ipv4.sindan-net.com": 30,
      "v4dnsans_AAAA_dual.sindan-net.com": "2001:200:0:180c::6",
      "v4dnsttl_AAAA_dual.sindan-net.com": 30,
      "v4dnsans_A_ipv4.sindan-net.com": "203.178.139.60",
      "v4dnsttl_A_dual.sindan-net.com": 30,
      "v4dnsstatus_AAAA_dual.sindan-net.com": 1,
      "v4dnsrtt_AAAA_dual.sindan-net.com": 23,
      "v4dnsrtt_AAAA_ipv4.sindan-net.com": 19,
      "v4dnsans_A_dual.sindan-net.com": "203.178.139.60",
      "v4dnsstatus_AAAA_ipv6.sindan-net.com": 1,
      "v4dnsstatus_A_ipv4.sindan-net.com": 1,
      "v4dnsans_AAAA_ipv4.sindan-net.com": "",
      "v4dnsstatus_AAAA_ipv4.sindan-net.com": 1,
      "v4dnsans_AAAA_ipv6.sindan-net.com": "2001:200:0:180c::6"
    },
    "1.1.1.1": {
      "v4dnsttl_A_ipv6.sindan-net.com": "",
      "v4dnsrtt_AAAA_ipv6.sindan-net.com": 71,
      "v4dnsttl_AAAA_ipv6.sindan-net.com": 30,
      "v4dnsrtt_A_ipv4.sindan-net.com": 19,
      "v4dnsttl_A_dual.sindan-net.com": 30,
      "v4dnsrtt_A_ipv6.sindan-net.com": 15,
      "v4dnsans_A_dual.sindan-net.com": "203.178.139.60",
      "v4dnsans_AAAA_ipv6.sindan-net.com": "2001:200:0:180c::6",
      "v4dnsans_A_ipv4.sindan-net.com": "203.178.139.60",
      "v4dnsrtt_A_dual.sindan-net.com": 107,
      "v4dnsttl_AAAA_ipv4.sindan-net.com": "",
      "v4dnsstatus_A_dual.sindan-net.com": 1,
      "v4dnsrtt_AAAA_dual.sindan-net.com": 119,
      "v4dnsstatus_AAAA_dual.sindan-net.com": 1,
      "v4dnsans_AAAA_dual.sindan-net.com": "2001:200:0:180c::6",
      "v4dnsttl_AAAA_dual.sindan-net.com": 30,
      "v4dnsrtt_AAAA_ipv4.sindan-net.com": 11,
      "v4dnsans_AAAA_ipv4.sindan-net.com": "",
      "v4dnsstatus_A_ipv4.sindan-net.com": 1,
      "v4dnsstatus_AAAA_ipv4.sindan-net.com": 1,
      "v4dnsttl_A_ipv4.sindan-net.com": 30,
      "v4dnsstatus_A_ipv6.sindan-net.com": 1,
      "v4dnsstatus_AAAA_ipv6.sindan-net.com": 1,
      "v4dnsans_A_ipv6.sindan-net.com": ""
    },
    "2001:4860:4860::8888": {
      "v6dnsans_AAAA_ipv4.sindan-net.com": "",
      "v6dnsttl_A_dual.sindan-net.com": 30,
      "v6dnsttl_AAAA_ipv6.sindan-net.com": 30,
      "v6dnsrtt_AAAA_ipv4.sindan-net.com": 19,
      "v6dnsans_A_ipv4.sindan-net.com": "203.178.139.60",
      "v6dnsstatus_A_dual.sindan-net.com": 1,
      "v6dnsstatus_AAAA_ipv6.sindan-net.com": 1,
      "v6dnsans_A_ipv6.sindan-net.com": "",
      "v6dnsstatus_A_ipv6.sindan-net.com": 1,
      "v6dnsttl_AAAA_dual.sindan-net.com": 30,
      "v6dnsttl_A_ipv4.sindan-net.com": 30,
      "v6dnsrtt_A_ipv6.sindan-net.com": 23,
      "v6dnsrtt_A_dual.sindan-net.com": 39,
      "v6dnsans_A_dual.sindan-net.com": "203.178.139.60",
      "v6dnsrtt_AAAA_dual.sindan-net.com": 23,
      "v6dnsstatus_A_ipv4.sindan-net.com": 1,
      "v6dnsans_AAAA_dual.sindan-net.com": "2001:200:0:180c::6",
      "v6dnsstatus_AAAA_dual.sindan-net.com": 1,
      "v6dnsrtt_A_ipv4.sindan-net.com": 27,
      "v6dnsttl_A_ipv6.sindan-net.com": "",
      "v6dnsstatus_AAAA_ipv4.sindan-net.com": 1,
      "v6dnsrtt_AAAA_ipv6.sindan-net.com": 91,
      "v6dnsans_AAAA_ipv6.sindan-net.com": "2001:200:0:180c::6"
    },
    "133.41.4.2": {
      "v4dnsans_A_ipv6.sindan-net.com": "",
      "v4dnsrtt_AAAA_dual.sindan-net.com": 19,
      "v4dnsrtt_A_dual.sindan-net.com": 35,
      "v4dnsrtt_A_ipv6.sindan-net.com": 3,
      "v4dnsttl_A_ipv6.sindan-net.com": ""
    },
    "2001:2f8:1c1:51::8529:402": {
      "v6dnsans_A_dual.sindan-net.com": "203.178.139.60",
      "v6dnsstatus_A_dual.sindan-net.com": 1,
      "v6dnsttl_AAAA_ipv4.sindan-net.com": "",
      "v6dnsttl_A_dual.sindan-net.com": 30,
      "v6dnsrtt_A_dual.sindan-net.com": 3,
      "v6dnsans_AAAA_dual.sindan-net.com": "2001:200:0:180c::6"
    }
  }
}
```

# Topic: `sindan/{hostname}/phase6`
- アプリケーション通信（HTTP, SSH, Speedtest）レベルでの 外部接続性能と信頼性の最終確認
- 以下を追加
    - `v${ver}httpstatus_${type}`: HTTP/HTTPS 接続の status
    - `v${ver}sshstatus_${type}`: SSH 接続の status
    - `v${ver}portscanstatus_${port}`: ポートスキャンの status
    - `speedteststatus`: スピードテストの status
```json
{
  "phase": 6,
  "layer": "app",
  "campaign_uuid": "3926a33f-eeaf-4900-8e1a-f05eb145481a",
  "timestamp": "2025-11-25 16:38:13",
  "data": {
    "target.sindan-net.com": {
      "v4portscan_443": "Connection to target.sindan-net.com (210.231.212.50) 443 port [tcp/https] succeeded!",
      "v6portscanstatus_443": 1,
      "v4portscanstatus_80": 1,
      "v6portscan_443": "Connection to target.sindan-net.com (2405:f000:202:2592:210:231:212:50) 443 port [tcp/https] succeeded!",
      "v4portscan_80": "Connection to target.sindan-net.com (210.231.212.50) 80 port [tcp/http] succeeded!",
      "v6portscan_22": "Connection to target.sindan-net.com (2405:f000:202:2592:210:231:212:50) 22 port [tcp/ssh] succeeded!",
      "v6portscanstatus_80": 1,
      "v6portscanstatus_22": 1,
      "v4portscan_22": "Connection to target.sindan-net.com (210.231.212.50) 22 port [tcp/ssh] succeeded!",
      "v4portscanstatus_22": 1,
      "v6portscan_80": "Connection to target.sindan-net.com (2405:f000:202:2592:210:231:212:50) 80 port [tcp/http] succeeded!",
      "v4portscanstatus_443": 1
    },
    "www.wide.ad.jp": {
      "v4http_websrv": 200,
      "v4httpstatus_websrv": 1,
      "v6http_websrv": 200,
      "v6httpstatus_websrv": 1
    },
    "https://api.inonius.net/": {
      "v6speedtest_rtt": 15,
      "v6speedtest_download": 454.47,
      "v6speedtest_jitter": 0.95,
      "v6speedtest_time": 1764056226,
      "v4speedtest_rtt": 16.55,
      "v4speedtest_upload": 487.88,
      "v6speedtest_port": 51818,
      "v6speedtest_ip": "2001:2f8:1c1:816::eef",
      "speedteststatus": 1,
      "v6speedtest_upload": 784.01,
      "v6speedtest_mss": 1440,
      "v4speedtest_org": "AS2506 NTT WEST CHUGOKU CORPORATION",
      "v4speedtest_mss": 1460,
      "v4speedtest_jitter": 1.29,
      "v4speedtest_download": 154.7,
      "v6speedtest_org": "AS2907 Research Organization of Information and Systems, National Institute of Informatics",
      "v4speedtest_ip": "133.41.74.30",
      "v4speedtest_time": 1764056226,
      "v4speedtest_port": 52692
    },
    "fluentd.sindan-net.com": {
      "v4sshstatus_sshsrv": 1,
      "v6sshstatus_sshsrv": 1
    },
    "www.yahoo.co.jp": {
      "v4httpstatus_websrv": 1,
      "v4http_websrv": 200
    },
    "www.google.co.jp": {
      "v6httpstatus_websrv": 1,
      "v6http_websrv": 200
    }
  }
}
```
