---
title: Qiita CLI導入後に最初にやること【公開済み記事の取り込み】
tags:
  - QiitaCLI
  - 備忘録
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: true
posting_campaign_uuid: 783b7a849caf11eefd91
agreed_posting_campaign_term: true
---
---
# はじめに
Qiita CLIを導入しました。

Qiita CLIでは、公開済みの記事をローカルで管理できます。しかし、既にQiita上で公開している記事は自動では取得されません。そのため、最初に記事を取り込んでローカルと同期しておくことをおすすめします。

今回は、すでに公開済みの記事を取り込む方法をまとめます。

なお、下書き状態の記事は取り込めないようなので、それについては手動で行う必要がある点には注意が必要です。

# 作業環境
- OS: Windows 11 Home
- バージョン: 22h2
- Node.js管理ツール: Nodist
- Nodeバージョン: v22.4.0
- npmバージョン: 10.2.3
- npxバージョン: 10.2.3
- CLIツール: Windows Terminal

# 前提
- Qiita CLIのインストールが完了していること
- Qiitaの記事管理用のリポジトリが作成されていること
- `Qiita CLI`と`GitHubリポジトリ`の連携が完了していること
- Windows Terminal上でQiitaにログインしていること

# 事前準備
- Windows Terminalを起動します。

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

# すでに公開済みの記事の取り込み
- `pwd`コマンドを実行し、ローカルリポジトリのルートディレクトリにいることを確認します。
    - 実行コマンド
        ```bash
        pwd
        ```
    - 確認事項
        - ローカルリポジトリのルートディレクトリにいることを確認します。

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

- `public`フォルダ配下にファイルが追加されていることを確認します。
  - 実行コマンド
    ```bash
    ls C:\git\ルートディレクトリ\public
    ```
  - 実行コマンド例
    ```bash
    ls C:\git\qiita-contents\public
    ```
  - 確認事項
    - 現在公開済みの記事数と、publicフォルダ配下のファイル数が一致していること。

# おわりに
今回は、Qiita CLIの導入後、一番最初にやることと題し、
公開済みの記事の取り込み手順をまとめました。

下書きの記事や、限定公開の記事が取り込まれないので、そちらについては別途対応する必要はある点には注意が必要です。

Qiita CLIを導入された他の方のお役に立てましたら幸いです。