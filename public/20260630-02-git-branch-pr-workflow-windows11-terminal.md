---
title: 20260630-02-git-branch-pr-workflow-windows11-terminal
tags:
  - ''
private: true
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: true
---
# 環境情報
- OS：Windows11
- ターミナルソフト：terminal
- 利用サービス：GitHub

# 前提条件
- Windows11を使用していること。
- リポジトリが作成済みであること。
- terminalでGitHubリポジトリにSSH接続できる状態であること。
- リポジトリをClone済みであること。

# ブランチ作成

- terminalを起動します。

- ローカルリポジトリのrootディレクトリに移動します。

- mainブランチを最新の状態にします。
  - 実行コマンド
    ```bash
    git pull
    ```

  - 確認事項
    - 下記の二つのどちらかが出力されることを確認します。
      - リモートリポジトリの内容が取り込まれること。
      - `Already up to date.`と出力され、更新内容がないこと。

- ブランチを作成します。
  - 実行コマンド
    ```bash
    git switch -c ブランチ名
    ```

  - 実行コマンド例
    ```bash
    git switch -c feature/post-list-design
    ```

  - 実行結果
    ```bash
    Switched to a new branch 'feature/post-list-design'
    ```

  ::: note info
  `git switch -c ブランチ名`を実行することで下記のことを実施しています。
  - 新しいブランチを作ることと
  - そのブランチに移動する
  :::

- ブランチの作成状況および、現在のブランチを確認します。
  - 実行コマンド
    ```bash
    git branch
    ```
  - 実行結果
    ```bash
    * feature/post-list-design
      main
    ```
  - 確認事項
    - `git switch -c ブランチ名`を実行した際のブランチ名が表示されていること。
    - 作成したブランチ名の前に`*`が付いていること。
