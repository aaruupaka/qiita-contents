---
title: Git(GitHub)のブランチの作成からプルリクエストの作成、マージまでの手順【初学者向け】
tags:
  - Git
  - GitHub
  - 初学者向け
  - 初心者向け
  - 備忘録
private: true
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: true
---
# はじめに
今回は、Gitでブランチを作成してから、変更をコミットし、GitHubでプルリクエスト（PR）を作成・マージするまでの一連の流れを紹介します。

Gitを使い始めたばかりの頃は、「ブランチは作れたけど、その後は何をすればいいの？」と迷うことも少なくありません。

この記事では、Windows 11のWindows Terminalを使用し、初学者向けに実際のコマンドと画面を交えながら、ブランチ作成からマージ後の後片付けまで順番に解説します。

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

# コミットを行う
- 任意のファイルを編集します。


- 変更をステージングします。
  - 実行コマンド
    ```bash
    git add .
    ```
- ステージング内容が認識と相違ないか確認します。
  - 実行コマンド
    ```bash
    git diff --staged
    ```
  - 確認事項
    - ステージングした内容に問題がないか確認します。

    ::: note info
    - 実行結果が表示しきれない場合、`↓`を押すことで内容を確認できます。
    - 実行結果の確認を終えたい場合は`q`を押下することで終了できます。
    :::

    ::: note info
    ステージングした内容に意図しない内容が含まれている場合は下記のコマンドでステージングをリセットできます。
    ```bash
    git reset
    ```
    :::

- 変更をローカルリポジトリにコミットします。
  - 実行コマンド
    ```bash
    git commit -m "コミットメッセージ"
    ```
  - 実行コマンド例
    ```bash
    git commit -m "Update 投稿一覧のページタイトルをサイトタイトルの位置と合わせる refs #63"
    ```
  - 実行結果例
    ```bash
     3 files changed, 8 insertions(+), 3 deletions(-)
    ```
  - 確認事項
    - 今回の変更内容の概要が出力されることを確認します。

# 初回プッシュを行う
- 初回プッシュを行います。
  - 実行コマンド
    ```bash
    git push -u origin feature/post-list-design
    ```
  - 実行結果例
    ```bash
    Enumerating objects: 16, done.
    Counting objects: 100% (16/16), done.
    Delta compression using up to 8 threads
    Compressing objects: 100% (11/11), done.
    Writing objects: 100% (11/11), 1.04 KiB | 1.04 MiB/s, done.
    Total 11 (delta 9), reused 0 (delta 0), pack-reused 0 (from 0)
    remote: Resolving deltas: 100% (9/9), completed with 5 local objects.
    remote:
    remote: Create a pull request for 'feature/post-list-design' on GitHub by visiting:
    remote:      https://github.com/aaruupaka/wordpress-theme-aaruupaka-prot/pull/new/feature/post-list-design
    remote:
    To github.com:aaruupaka/wordpress-theme-aaruupaka-prot.git
    * [new branch]      feature/post-list-design -> feature/post-list-design
    branch 'feature/post-list-design' set up to track 'origin/feature/post-list-design'.
    ```
  
  ::: note info
  次回以降は下記のコマンドで問題なく実行できます。
  - 実行コマンド
    ```bash
    git push
    ```
  :::

# PR(プルリクエスト)を作成する
- リポジトリのトップページにアクセスします。
  <br>![alt text](../articles/20260630-02-git-branch-pr-workflow-windows11-terminal/images/20260630-02-01.png)

- `Pull requests`タブを開きます。
  <br>![alt text](../articles/20260630-02-git-branch-pr-workflow-windows11-terminal/images/20260630-02-02.png)

- `New pull request`ボタンを押下し、`Compare changes`画面を開きます。
  <br>![alt text](../articles/20260630-02-git-branch-pr-workflow-windows11-terminal/images/20260630-02-03.png)

- 比較するブランチを選択し、差分を確認します。
  <br>![alt text](../articles/20260630-02-git-branch-pr-workflow-windows11-terminal/images/20260630-02-04.png)

- 表示された差分で問題なければ、`Create pull request`ボタンを押下します。
  <br>![alt text](../articles/20260630-02-git-branch-pr-workflow-windows11-terminal/images/20260630-02-05.png)

- `Open a pull request`画面で、下記の内容を入力後、`Create pull request`ボタンを押下します。
  - 設定内容
    - Add a title *
        - 必須項目です。
    - Add a description
        - 任意項目ですが、変更内容をざっと入力することを推奨します。

  <br>![alt text](../articles/20260630-02-git-branch-pr-workflow-windows11-terminal/images/20260630-02-06.png)

- プルリクエストが作成されたことを確認します。
  <br>![alt text](../articles/20260630-02-git-branch-pr-workflow-windows11-terminal/images/20260630-02-07.png)

# PRをマージする
- `Merge pull request`ボタンの右側`▽`をクリックし、Margeの種類を`Squash and merge`に変更します。
  <br>![alt text](../articles/20260630-02-git-branch-pr-workflow-windows11-terminal/images/20260630-02-08.png)

::: note info
今回、自分自身でPRを作成、マージしようとしているため、レビューは省略しています。
:::

- `Squash and merge`ボタンを押下します。
  <br>![alt text](../articles/20260630-02-git-branch-pr-workflow-windows11-terminal/images/20260630-02-09.png)

- 自動生成された下記項目を確認し、問題がなければ`Confirm squash and merge`ボタンを押下します。
  - Commit message
  - Extended description
  <br>![alt text](../articles/20260630-02-git-branch-pr-workflow-windows11-terminal/images/20260630-02-10.png)

- `Pull request successfully merged and closed`と出力されたことを確認します。
  <br>![alt text](../articles/20260630-02-git-branch-pr-workflow-windows11-terminal/images/20260630-02-11.png)

- ブランチを削除する場合は、`Delete branch`ボタンを押下します。
  <br>![alt text](../articles/20260630-02-git-branch-pr-workflow-windows11-terminal/images/20260630-02-12.png)

# ローカルリポジトリを最新の状態に更新する
- terminalに戻ります。

- mainブランチに切り替えます。
  - 実行コマンド
    ```bash
    git switch main
    ```
  - 実行結果例
    ```bash
    Switched to branch 'main'
    Your branch is behind 'origin/main' by 1 commit, and can be fast-forwarded.
      (use "git pull" to update your local branch)
    ```

- mainブランチに切り替わっていることを確認します。
  - 実行コマンド
    ```bash
    git branch
    ```
  - 実行結果例
    ```bash
      feature/post-list-design
      * main
    ```
  - 確認事項
    - `main`の前に`*`が付いていることを確認します。

- mainブランチを最新の状態にします。
  - 実行コマンド
    ```bash
    git pull
    ```
  - 実行結果例
    ```bash
    Updating 72a453e..601a966
    Fast-forward
    aaruupaka-prot/functions.php | 2 +-
    aaruupaka-prot/index.php     | 2 +-
    aaruupaka-prot/style.css     | 7 ++++++-
    3 files changed, 8 insertions(+), 3 deletions(-)
    ```

# ローカルリポジトリのブランチを削除する。
- ブランチを削除したい場合、下記のコマンドを実行します。
  - 実行コマンド
    ```bash
    git branch -d ブランチ名
    ```
  - 実行コマンド例
    ```bash
    git branch -d feature/post-list-design
    ```
  - 実行結果例
    ```bash
    warning: deleting branch 'feature/post-list-design' that has been merged to
             'refs/remotes/origin/feature/post-list-design', but not yet merged to HEAD
    Deleted branch feature/post-list-design (was c02a163).
    ```
  
  ::: note info
  今回、警告が出てしまっています。

  上記のような警告が出る場合、ローカルリポジトリ内に古いリモート追跡ブランチ情報が残っている可能性があります。

  古いリモートブランチが残っているかの確認は下記のコマンドで確認できます。
  - 実行コマンド
    ```bash
    git branch -r
    ```
  
  古いリモートブランチが残っているかつ、削除したい場合は下記のコマンドを実行します。
  - 実行コマンド
    ```bash
    git fetch --prune
    ``` 
  :::
