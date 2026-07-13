---
title: Git管理しているWordPressテーマをLocal WPで利用する方法【シンボリックリンク】
tags:
  - WordPress
  - WordPressテーマ
  - Windows11
  - LocalWP
  - WordPress開発環境
private: false
updated_at: '2026-07-14T03:37:18+09:00'
id: 61ab210d7a3b300785c3
organization_url_name: null
slide: false
ignorePublish: false
posting_campaign_uuid: 783b7a849caf11eefd91
agreed_posting_campaign_term: true
---
# はじめに

Local WPでWordPressテーマを開発する場合、Gitで管理しているテーマを開発環境でもそのまま利用したいことがあります。

しかし、Git管理しているテーマをそのままLocal WPのテーマディレクトリへ配置すると、開発環境やディレクトリ構成によっては管理しづらくなる場合があります。

そこで本記事では、Windowsのシンボリックリンクを利用して、Git管理しているWordPressテーマをLocal WPから利用できるようにする手順を紹介します。

シンボリックリンクの作成だけでなく、Local WPでテーマとして認識されることや、テーマの変更内容が正常に反映されることまで確認します。

# 作業手順
## パスの確認
- パスの確認を行います。下記のパス情報が必要です。
  - Git管理しているテーマ本体のパス
  - LocalWPのテーマディレクトリのパス
    - Git管理しているテーマ本体のパスの例
        ```text
        D:\a_pjs\2026060301_aaruupaka_wordpress-theme-aaruupaka-prot\wordpress-theme-aaruupaka-prot\aaruupaka-prot
        ```
    - LocalWPのテーマディレクトリのパスの例
        ```text
        C:\Users\<Windowsユーザー名>\Local Sites\<サイト名>\app\public\wp-content\themes
        ```

## シンボリックリンクの作成
- 管理者権限でコマンドプロンプトを起動します。
- シンボリックリンクを作成します。
    - 実行コマンド
        ```cmd
        mklink /D "C:\Users\<Windowsユーザー名>\Local Sites\<サイト名>\app\public\wp-content\themes\aaruupaka-prot" "D:\a_pjs\2026060301_aaruupaka_wordpress-theme-aaruupaka-prot\wordpress-theme-aaruupaka-prot\aaruupaka-prot"
        ```
        - 文法
            ```cmd
            mklink /D "LocalWPのテーマディレクトリのパス" "Git管理しているテーマ本体のパス"
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
        - `themes`配下に、`aaruupaka-prot`が表示されていること。
    
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

## テーマ作成用のWordPressサイトにテーマに設定する。
- LocalWPを起動します。

- テーマ作成用のWordPressサイトが起動していることを確認します。
    - 起動していなければ起動します。

- テーマ作成用のWordPressサイトの管理画面に遷移します。

- `テーマ一覧`画面に移動します。

- テーマの一覧に`テーマフォルダ名`が存在していることを確認します。

- `テーマフォルダ名`を有効化します。

- テーマ作成用のWordPressサイトのトップページにアクセスし、テーマが反映されていることを確認します。

## シンボリックリンク経由で変更が反映されるかの確認
- 任意のファイルに任意の変更を加えます。
    - style.cssの背景色を変更するのが一番わかりやすいと思います。
- テーマ作成用のWordPressサイトにアクセスし、変更が反映されていることを確認します。

# おわりに

以上で、Git管理しているWordPressテーマをLocal WPから利用するための設定は完了です。

シンボリックリンクを利用することで、Git管理下のテーマをそのまま開発環境から利用できるようになり、テーマを二重に管理する必要がなくなります。また、Git管理しているファイルを編集するだけでLocal WP側にも変更が反映されるため、開発をスムーズに進められるようになります。

一度設定してしまえば、今後は同じ環境で継続してテーマ開発を行えるため、WordPressテーマをGitで管理している方はぜひ活用してみてください。
