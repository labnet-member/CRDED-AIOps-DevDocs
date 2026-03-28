## ファイアウォール設定
**受信通信はすべて拒否し，送信通信のみ許可**

### インストール
```bash
sudo apt install ufw -y
```

### 設定内容
```bash
sudo ufw enable
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow 22
```

```bash
$ sudo ufw status
Status: active

To                         Action      From
--                         ------      ----
22                         ALLOW       Anywhere
22 (v6)                    ALLOW       Anywhere (v6)
```

## WireGuard 設定
- 各大学のアドレス対応は [ネットワーク情報一覧](https://github.com/labnet-member/CRDED-AIOps-DevDocs/blob/main/docs/environment.md#%E3%83%8D%E3%83%83%E3%83%88%E3%83%AF%E3%83%BC%E3%82%AF%E6%83%85%E5%A0%B1%E4%B8%80%E8%A6%A7) 参照

### インストール
```bash
sudo apt install wireguard -y
```

### 設定内容
```conf
$ sudo cat /etc/wireguard/client0.conf
[Interface]
Address = 10.0.0.X/24
PrivateKey = [client0.keyの内容]

[Peer]
PublicKey = [server.pubの内容]
PresharedKey = [client0-preshared.keyの内容]
AllowedIPs = 10.0.0.0/24
Endpoint = [サーバーのIPアドレス]:51820
PersistentKeepalive = 25
```

### 反映
```bash
sudo wg-quick up client0
sudo systemctl enable wg-quick@client0
```