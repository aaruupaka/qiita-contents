---
title: Git管理しているWordPressテーマをLocal WPで利用する方法【シンボリックリンク】
tags:
  - LocalWP
  - WordPress
  - WordPressテーマ
  - WordPress開発環境
  - Windows11
private: true
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: true
posting_campaign_uuid: null
agreed_posting_campaign_term: false
---
# 概要
LocalWPのテーマフォルダ配下に、
git管理上のaaruupaka-protのテーマフォルダの
シンボリックリンクを作成します。

# 作業手順
## パスの確認
- パスの確認を行います。
    - Git管理しているテーマ本体のパスの例
        ```text
        D:\a_pjs\2026060301_aaruupaka_wordpress-theme-aaruupaka-prot\wordpress-theme-aaruupaka-prot\aaruupaka-prot
        ```
    - LocalWPのテーマ配置先のパスの例
        ```text
        C:\Users\<Windowsユーザー名>\Local Sites\<サイト名>\app\public\wp-content\themes
        ```

## シンボリックリンクの作成
- 管理者権限でコマンドプロンプトを起動する。
- シンボリックリンクを作成する。
    - 実行コマンド
        ```cmd
        mklink /D "C:\Users\<Windowsユーザー名>\Local Sites\<サイト名>\app\public\wp-content\themes\aaruupaka-prot" "D:\a_pjs\2026060301_aaruupaka_wordpress-theme-aaruupaka-prot\wordpress-theme-aaruupaka-prot\aaruupaka-prot"
        ```
        - 文法
            ```cmd
            mklink /D "LocalWP側に作るリンク" "Git管理しているテーマ本体"
            ```
    - 実行コマンド例
        - ユーザー名：testuser
        - サイト名：wordpress-theme-dev
            ```cmd
            mklink /D "C:\Users\testuser\Local Sites\wordpress-theme-dev\app\public\wp-content\themes\aaruupaka-prot" "D:\a_pjs\2026060301_aaruupaka_wordpress-theme-aaruupaka-prot\wordpress-theme-aaruupaka-prot\aaruupaka-prot"
            ```
    - 実行結果例
        ```
        C:\Users\<ユーザー名>\Local Sites\<サイト名>\app\public\wp-content\themes\aaruupaka-prot <<===>> D:\a_pjs\2026060301_aaruupaka_wordpress-theme-aaruupaka-prot\wordpress-theme-aaruupaka-prot\aaruupaka-prot のシンボリック リンクが作成されました
        ```

## シンボリックリンク作成結果の確認
- シンボリックリンクが作成されているかの確認
    - 実行コマンド
        ```cmd
        dir "C:\Users\<Windowsユーザー名>\Local Sites\<サイト名>\app\public\wp-content\themes"
        ```
    - 実行コマンド例
        - ユーザー名：testuser
        - サイト名：wordpress-theme-dev
            ```cmd
            dir "C:\Users\testuser\Local Sites\wordpress-theme-dev\app\public\wp-content\themes"
            ```
    - 実行結果例
        ```cmd
         ドライブ C のボリューム ラベルは Windows です
         ボリューム シリアル番号は NNNN-NNNN です

         C:\Users\<ユーザー名>\Local Sites\<サイト名>\app\public\wp-content\themes のディレクトリ

        2026/06/05  00:09    <DIR>          .
        2026/06/05  00:03    <DIR>          ..
        2026/06/05  00:09    <SYMLINKD>     aaruupaka-prot [D:\a_pjs\2026060301_aaruupaka_wordpress-theme-aaruupaka-prot\wordpress-theme-aaruupaka-prot\aaruupaka-prot]
        2014/06/06  00:59                28 index.php
        2026/05/19  14:12    <DIR>          twentytwentyfive
        2026/05/19  14:12    <DIR>          twentytwentyfour
        2026/05/19  14:12    <DIR>          twentytwentythree
                    1 個のファイル                  28 バイト
                    6 個のディレクトリ  12,191,125,504 バイトの空き領域
        ```
    - 確認事項
        - `theme`配下に、`aaruupaka-prot`が表示されていること。
    
- シンボリックリンクの中身の確認
    - 実行コマンド
        ```cmd
        dir "C:\Users\<Windowsユーザー名>\Local Sites\<サイト名>\app\public\wp-content\themes\aaruupaka-prot"
        ```
    - 実行コマンド例
        - ユーザー名：testuser
        - サイト名：wordpress-theme-dev
            ```cmd
            dir "C:\Users\testuser\Local Sites\wordpress-theme-dev\app\public\wp-content\themes\aaruupaka-prot"
            ```
    - 実行結果例
        ```cmd
        ドライブ C のボリューム ラベルは Windows です
        ボリューム シリアル番号は NNNN-NNNN です

        C:\Users\<ユーザー名>\Local Sites\<サイト名>\app\public\wp-content\themes\aaruupaka-prot のディレクトリ

        2026/06/03  22:55    <DIR>          .
        2026/06/03  22:55    <DIR>          ..
        2026/06/03  22:58               314 index.php
        2026/06/03  22:56               131 style.css
                    2 個のファイル                 445 バイト
                    2 個のディレクトリ  984,650,559,488 バイトの空き領域
        ```

## `aaruupaka-prot`をテーマに設定する。
- LocalWPを起動する。
- 検証用サイトが起動していることを確認する。
    - 起動していなければ起動する。
- WordPressの管理画面に遷移する。
- `テーマ一覧`画面に移動する。
- テーマの一覧に`aaruupaka-prot`が存在していることを確認する。
- `aaruupaka-prot`を有効化する。

## テーマの反映確認
- WordPressのトップページに遷移します。
- `aaruupaka-prot`が適応されていることを確認します。
    - ver.`0.1.0`では下記の文言が確認できればOK
        ```
        Aaruupaka Prot
        自作テーマが表示されています。
        ```

## シンボリックリンク経由で変更が反映されるかの確認
- VSCodeを起動します。
- git管理下の下記のファイルを開きます。
    ```
    D:\a_pjs\2026060301_aaruupaka_wordpress-theme-aaruupaka-prot\wordpress-theme-aaruupaka-prot\aaruupaka-prot\index.php
    ```
- 開いたファイルに下記の文言を追記します。
    ```php
    <p>シンボリックリンク経由で自作テーマが表示されています。</p>
    ```
- ファイルを保存します。
- WordPressのトップページに遷移します。
- `aaruupaka-prot`の内容が更新されていることを確認します。
    - ver.`0.1.0`では下記の文言が確認できればOK
        ```
        Aaruupaka Prot
        自作テーマが表示されています。
        シンボリックリンク経由で自作テーマが表示されています。
        ```
