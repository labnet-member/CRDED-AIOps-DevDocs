# SINETStream 送信プログラム実行までのセットアップ手順

## 1. `uv` をインストール
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

## 2. PATH を通す
```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

## 3. sinetstream-client リポジトリをクローン
```
cd ~
git clone https://github.com/labnet-member/sinetstream-client.git
```

## 3. プロジェクトの依存関係を環境と同期
```bash
cd sinetstream-client/
uv sync
```
