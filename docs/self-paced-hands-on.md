# セルフペース ハンズオン

このハンズオン資料は、Microsoft Ignite Spotlight on Japan の現地会場ハンズオンで利用するためにまとめられたものです。

ただし、事前準備の条件をクリアできる方は実施できる内容になっていますので、ご参考になれば幸いです。


## 事前準備

- GitHub アカウントを用意する
  - 個人アカウントの場合、GitHub Codespaces ベータ版の申請が受理されていること
  - もしくは、GitHub Codespaces が有効になっている（Spent limit が 0 より大きく設定されている）Organization に属していて、リポジトリを用意できること
- Microsoft Azure のアカウントを用意する


## 手順

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

