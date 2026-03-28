# Grafana ダッシュボード

- テンプレートとして [sindan-docker/grafana/dashboards/sindan_new.json](https://github.com/SINDAN/sindan-docker/blob/master/grafana/dashboards/sindan_new.json) を利用
- 元は MySQL を前提としていたため，データソースを InfluxDB に変更し，それに対応するようクエリを書き換えてデータを取得

<img src="/docs/images/dashboard1.png">

<img src="/docs/images/dashboard2.png">

- 上部のプルダウンを切り替えることで該当のデータを表示
- IPv6 が利用できない場合や，外部サーバへの到達ができない場合などは No data と表示される

## （引継ぎ用）未対応の項目
- `Alert`: スピードテストの結果をもとにアラートを表示するためのパネル？
- `Latest Campaign`: 指定期間内のログキャンペーンから，最新の順で30件，時刻と MAC アドレスを取得する
    - Phase 7 のデータもパブリッシュする必要あり（現状 Phase 6 まで）