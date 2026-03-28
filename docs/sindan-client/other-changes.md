# その他の変更

[SINDAN クライアント実行・デバッグ記録（ZoneC 環境）](https://github.com/labnet-member/CRDED-AIOps-DevDocs/blob/main/docs/sindan-client/debug.md) の他に元のコードを変更した箇所の記録

---

## ログ関連
### 保存場所
- 変更前: `/home/{username}/sindan-client/linux/log`にまとめて保存される
- 変更後: `/home/{username}/log/tmp/タイムスタンプ` フォルダごとに分けて保存

[#3644ef1](https://github.com/labnet-member/sindan-client/commit/3644ef16499d1e52f190c66c45ebbe249ead1909)

> [!NOTE]
> `sudo ./sindan.sh` で実行しても
ログが root のホームではなく 元ユーザのホームに保存されるように変更

### ログに記録される時刻（`occurred_at`）
- 変更前: UTC
- 変更後: JST

[#301229b](https://github.com/labnet-member/sindan-client/commit/301229b432eb18e99f4e4c91c319c7dbc547fed5)

---



