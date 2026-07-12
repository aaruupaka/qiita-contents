---
title: 20260711-06-qiita-cli-import-qiita-articles
tags:
  - QiitaCLI
  - 備忘録
private: true
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: true
posting_campaign_uuid: null
agreed_posting_campaign_term: false
---
---
# はじめに
Qiita CLIの導入したので、すでに公開済みの記事の取り込みを行います。

なお、下書き状態の記事は取り込めないようなので、それについては手動で行う必要があります。

# 作業環境
- OS:Windows 11 Home
- バージョン:22h2
- Node.js管理ツール:Nodist
- Nodeバージョン:v22.4.0
- npmバージョン:10.2.3
- npxバージョン:10.2.3
- CLIツール:terminal

# 前提
- Qiita CLIのインストールが完了していること
- Qiitaの記事管理用のリポジトリが作成されていること
- Qiita CLI と　GitHubリポジトリの連携が完了していること
- terminal上でQiitaにログインしていること

# 事前準備
- terminalを起動します。
- `cd`コマンドでローカルリポジトリのルートディレクトリに移動します。
    - 実行コマンド
        ```bash
        cd C:\git\ルートディレクトリ\
        ```
    - 実行コマンド例
        ```bash
        cd C:\git\qiita-contents\
        ```
- GitHubリポジトリ(remote)の内容をローカルに取り込みます。
    - 実行コマンド
        ```bash
        git pull
        ```
    - 実行結果
        ```
        Already up to date.
        ```
    - 確認事項
        - `Already up to date.`と出力されるか、変更が取り込まれること。

# すでに作成済みの記事の取り込み
- `pwd`コマンドを実行し、ローカルリポジトリのルートディレクトリにいることを確認します。
    - 実行コマンド
        ```bash
        pwd
        ```
- Qiita CLIの記事取り込みコマンドを実行します。
    - 実行コマンド
        ```
        npx qiita pull
        ```
    - 実行結果
        ```
        ◇ injected env (0) from .env // tip: ⌘ enable debugging { debug: true }
        Sync local articles from Qiita
        Successful!
        ```
    - 確認事項
        - `Successful!`が出力されていることを確認します。
