# GitHub Codespaces 体験ハンズオン

## GitHub Codespaces について知る

- [GitHub Codespaces](https://github.co.jp/features/codespaces)

### 特徴

- GitHub プラットフォームに立ち上げられた独立した環境
- 実態はコンテナだが、コンテナについての知識がなくても利用しやすい
- ブラウザまたは Visual Studio Code から利用できる
- GitHub とのシームレスな連携
- ポートフォワーディングにより、あたかも手元の環境で動作してるかのようにアクセスできる（`localhost`）
- [Development Containers](https://containers.dev/) に則ったカスタマイズができる
  - [dev container features](https://containers.dev/features) を利用して簡単に機能追加ができる
  - 拡張機能のプリインストール
  - 任意のイメージ及び Dockerfile で構築できる
- 事前にビルドしておく機構を用いて、素早く環境を立ち上げられる
- 利用量（アクティブな時間と利用しているボリューム量）に従った課金


## Microsoft Azure について知る

- [Microsoft Azure](https://azure.microsoft.com/ja-jp/)


## ハンズオン シナリオ

- GitHub Codespaces を立ち上げる
- 拡張機能を眺める（この時点では何もインストールされていない）
- `pre-built` ブランチから codespace を立ち上げてみる
- 拡張機能がインストールされていることを確認する
- `az` や `func` のコマンドがインストールされていることを確認する
- Azure Functions のプロジェクトを作成する
- GitHub Codespaces 上でローカル実行する
  - ポートフォワーディングにより、手元のマシンの `localhost` で接続できることを確認する
- 拡張機能で Azure にサインインする
  - ブラウザで作業している場合、同じブラウザでサインインが行われる。セッションを避けたい場合は、`Azure: Sign in with Device Code` でサインインするとよい
- Functions のリソースを作成して、デプロイする
