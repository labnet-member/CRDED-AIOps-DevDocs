# SINDAN クライアント実行までのセットアップ手順

## 1. [Installation Guide](https://github.com/SINDAN/sindan-client/blob/master/linux/README.md) に従い必要パッケージをインストール

```bash
sudo apt install uuid-runtime wireless-tools ndisc6 dnsutils curl chromium npm
```

<details>

<summary>
以下に示すように，ラズパイで chromium-browser パッケージは現在 apt リポジトリには存在しないため，代わりに大元の chromium パッケージを使用</summary>

```bash
$ sudo apt-get install chromium-browser
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
Package chromium-browser is not available, but is referred to by another package.
This may mean that the package is missing, has been obsoleted, or
is only available from another source

E: Package 'chromium-browser' has no installation candidate
```

</details>

## 2. 改修後の sindan-client リポジトリをクローン
```bash
git clone https://github.com/labnet-member/sindan-client.git
```

## 3. `install.sh` を実行して残りのパッケージをインストール
```bash
~ $ cd sindan-client/linux/
~/sindan-client/linux $ ./install.sh
```

## 4. コンフィグファイルを作成
```bash
~/sindan-client/linux $ cp sindan.conf.example sindan.conf
```

> [!NOTE]
> デフォルトだと無線（Wi-Fi）接続前提の設定になっています．もし有線にする場合は，以下の箇所を `IFTYPE=Ethernet` や `DEVNAME=eth0` のように変更してください．
> ```config
> # target interface
> # IFTYPE: Wi-Fi, WWAN (for Cellular), Ethernet
> readonly IFTYPE=Wi-Fi
> readonly DEVNAME=wlan0
> ```


## 5. スケジューリング
`crontab` で定期実行
3 箇所の `{username}` は自身のものに書き換える
```bash
crontab -e

# sindan.sh と main.py を 5 分ごとに実行
*/5 * * * * cd /home/{username}/sindan-client/linux/ && sudo ./sindan.sh && cd /home/{username}/sinetstream-client && /home/{username}/sinetstream-client/.venv/bin/python main.py


# sindan.sh の実行ログを残したい場合は以下のようにする（main.py はプログラム側でログを残している）
# */5 * * * * cd /home/{username}/sindan-client/linux/ && sudo ./sindan.sh >> /home/{username}/log/sindan-client-cron.log 2>&1 && cd /home/{username}/sinetstream-client && /home/{username}/sinetstream-client/.venv/bin/python main.py > /dev/null 2>&1
```

---

## 参考リンク

- [SINDAN Client: Installation Guide](https://github.com/SINDAN/sindan-client/blob/master/linux/README.md)






