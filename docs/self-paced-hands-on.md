# セルフペース ハンズオン

このハンズオン資料は、Microsoft Ignite Spotlight on Japan の現地会場ハンズオンで利用するためにまとめられたものです。

ただし、事前準備の条件をクリアできる方は実施できる内容になっていますので、ご参考になれば幸いです。


## 事前準備

- GitHub アカウントを用意する
  - 個人アカウントの場合、GitHub Codespaces ベータ版の申請が受理されていること
  - もしくは、GitHub Codespaces が有効になっている（Spent limit が 0 より大きく設定されている）Organization に属していて、リポジトリを用意できること
- Microsoft Azure のアカウントを用意する


## 手順＆解説

### GitHub Codespaces を立ち上げる

このリポジトリのメインブランチには `devcontainer.json`（Development Containers の設定ファイル）がないので、GitHub Codespaces の default image で環境が立ち上がります。default image の詳細は、[vscode-dev-containers/containers/codespaces-linux](https://aka.ms/ghcs-default-image) をご参照ください。

default image は Ubuntu で構成されていて、`apt` を利用して追加のパッケージをインストールすることも可能です。また、主要な言語が含まれており、カスタマイズしなくても使える場合も多いです。テキストを書くだけなら、default image で事足ります。

default image は Visual Studio Code の拡張機能はインストールされていませんが、自由にインストールすることができます。

保存したファイルやインストールしたパッケージ、インストールした拡張機能は、その codespace のインスタンスを消すまでは保持されます。

今回は、Azure Functions の開発を行いたいのですが、今ここで必要なパッケージや拡張機能をインストールしていると時間がかかってしまうので、"すでに用意されているイメージ" を使った環境を立ち上げてみましょう。


### Prebuild が設定されたブランチから codespace を立ち上げてみる

GitHub Codespaces は、起動するオプションを選ぶことができます。今回は、事前に用意しておいた `pre-built` ブランチで起動してみましょう。

- ブランチ
- 参照する Dev container の設定ファイル
- codespace を配置するリージョン
- SKU（コア数、メモリ、ストレージ量）

`pre-built` ブランチには、`.devcontainer/devcontainer.json` と `.devcontainer/Dockerfile` が含まれており、このファイルがあると Codespaces はその設定をもとにイメージをビルドした上で環境を起動します。

さて、お気づきでしょうか？即座に立ち上がりましたね？

実は、リポジトリの設定で GitHub Codespaces の Prebuild という機能を設定しておくことで、先にイメージをビルドしておくことができます。利用するリージョンにイメージを保存しておいてくれるので、すぐダウンロードが終わり起動することができるのです。

この Dev container の設定は、とても簡単にベースを作成できます。

メニューから「View」→「Command Palette...」を開き、`Codespaces: Add Dev Container Configuration Files...` を選択してみましょう。

すると、設定の定義一覧が表示されます。`Show All Definitions...` からすべての定義を表示し、`Azure Functions & Node.js` をみつけてみてください。

これが今開いてもらっている `pre-built` ブランチで利用している Dev container の設定のベースです。私はこの設定のうち、Node.js のバージョンだけを `16` に変更して利用しています。

この `Azure Functions & Node.js` イメージには、Azure Functions の開発に必要なパッケージや拡張機能が事前にインストールされています。

ターミナルを開き、`az` や `func` コマンドを確認してみましょう。また、拡張機能の一覧を開き、「CODESPACES - INSTALLED」に「[Azure Account](https://marketplace.visualstudio.com/items?itemName=ms-vscode.azure-account)」や「[Azure Functions](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)」がインストールされていることが確認できます。

> **Note** このハンズオンでは機能説明をしやすいようにデフォルトではないブランチに prebuild を設定していますが、実際に利用するときは、デフォルトブランチ（`main`）に設定する方が直感的で、プロジェクトのメンバーがより早く環境にアクセスできるようになるでしょう。


### Azure Functions のプロジェクトを作成する

それではさっそく Azure Functions の開発に着手しましょう！


まず、今は `pre-built` ブランチが開かれているので、作業用のブランチに切替え、作業用のディレクトリを作成しておきましょう。メニューから「Terminal」→「New Terminal」を開き、下記を実行します。

```
git switch -c add-functions
mkdir functions
```

つぎに、拡張機能を用いて Azure Functions の新規プロジェクトを生成しましょう。Command Palette で、`Azure Functions: Create New Project...` を選択します。

ファイルを配置するディレクトリを問われるので、`Browse...` で先ほど作成した `functions` ディレクトリを選択してください。

言語の選択では、お好きな言語を選択しましょう。（講師は `JavaScript` を選択します。不安のある方は同じものを選択してください。）

つぎに、最初の関数のテンプレートを選択します。ここでは、API を作成したので、`HTTP trigger` を選択しましょう。

HTTP trigger の名前は、そのまま決定（`Enter`キー押下）しておきます。

認証レベルは `Anonymous` を選択しておきましょう。

これで `HttpTrigger1` という HTTP trigger 関数が作成されました。


### GitHub Codespaces 上でローカル実行する
  - ポートフォワーディングにより、手元のマシンの `localhost` で接続できることを確認する


- 拡張機能で Azure にサインインする
  - ブラウザで作業している場合、同じブラウザでサインインが行われる。セッションを避けたい場合は、`Azure: Sign in with Device Code` でサインインするとよい


## Functions のリソースを作成して、デプロイする

