---
title: 20260724-01-localwp-wp-cli-wordpress-theme-check
tags:
  - ''
private: true
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: true
posting_campaign_uuid: null
agreed_posting_campaign_term: false
---
# メモ
`wp theme-check run <実行対象のテーマ名>`コマンドを実行しようとしても下記のようになってしまう
```
Error: 'theme-check' is not a registered wp command. See 'wp help' for available commands.
```

GitHub版のREADMEによると、実行できそうではあるのでいまいちわからない
https://github.com/wordpress/theme-check?tab=readme-ov-file

また、WP　CLI　コマンドのリストに`wp theme-check run `に該当しそうなものがないのも気になる

https://developer.wordpress.org/cli/commands/

ひとまず、作業が進まないので下記の順番で対応する
- 管理画面から取得できるプラグインを試し、指摘事項対応
- GitHub版を取得し、指摘事項対応
- WP CLIをLocalWPに標準搭載されているものではなく、ウェブページから取得してみて、`wp theme-check run`コマンドが使えるか調べる

また、Qiitaで質問してみるのもありかもしれない


# 環境情報
- OS: Windows11
- ソフトウェア: LocalWP

# WP CLIの動作確認
- `Local WP`を起動します。

- テストを実行したいサイトの`Site shell`を押下します。

- windows Terminalが起動することを確認します。
  - 起動時出力内容例
    ```bash
    Setting Local environment variables...
    ----
    WP-CLI: WP-CLI 2.12.0
    PHP version 8.3.29 (C:\Users\username\AppData\Roaming\Local\lightning-services\php-8.3.29+1\bin\win64\php.exe)
    Run the "diagnose" command to get more detailed diagnostics output.
    Composer: Composer version 2.8.6 2025-02-25 13:03:50
    PHP: 8.3.29
    MySQL: mysql  Ver 15.1 Distrib 10.6.23-MariaDB, for Win64 (AMD64), source revision fe8047caf26d20e98ea7f6ec1dce3924e696703f
    ----
    Loaded Shell for Local Site: wordpress-theme-dev
    ----
    ```

- WP CLIが動作するか確認します。
  - 実行コマンド
    ```bash
    wp --info
    ```
  - 実行結果例
    ```bash
    OS:     Windows NT 10.0 build 26200 (Windows 11) AMD64
    Shell:  C:\WINDOWS\system32\cmd.exe
    PHP binary:     C:\Users\ks0530\AppData\Roaming\Local\lightning-services\php-8.3.29+1\bin\win64\php.exe
    PHP version:    8.3.29
    php.ini used:   C:\Users\ks0530\AppData\Roaming\Local\run\dvKwOgLxb\conf\php\php.ini
    MySQL binary:
    MySQL version:
    SQL modes:
    WP-CLI root dir:        phar://wp-cli.phar/vendor/wp-cli/wp-cli
    WP-CLI vendor dir:      phar://wp-cli.phar/vendor
    WP_CLI phar path:       phar://C:/Users/ks0530/AppData/Local/Programs/Local/resources/extraResources/bin/wp-cli/wp-cli.phar
    WP-CLI packages dir:
    WP-CLI cache dir:       C:\Users\ks0530/.wp-cli/cache
    WP-CLI global config:
    WP-CLI project config:
    WP-CLI version: 2.12.0
    ```

# `Theme Check`プラグインのインストール
- `Theme Check`プラグインが入っていないことを確認します。
  - 実行コマンド
    ```bash
    wp plugin list
    ```
  - 実行結果例
    ```bash
    +------+--------+--------+---------+----------------+-------------+
    | name | status | update | version | update_version | auto_update |
    +------+--------+--------+---------+----------------+-------------+
    +------+--------+--------+---------+----------------+-------------+
    ```

- `Theme check`プラグインをインストールします。
  - 実行コマンド
    ```bash
    wp plugin install theme-check --activate
    ```
  - 実行結果
    ```bash
    Installing Theme Check (20231220)
    https://downloads.wordpress.org/plugin/theme-check.20231220.zip からインストールパッケージをダウンロード中...
    パッケージを展開しています…
    プラグインをインストールしています…
    プラグインのインストールが完了しました。
    Activating 'theme-check'...
    Plugin 'theme-check' activated.
    Success: Installed 1 of 1 plugins.
    ```

- `Theme check`プラグインがインストールされていることを確認します。
  - 実行コマンド
    ```bash
    wp plugin list
    ```
  - 実行結果例
    ```bash
    +-------------+--------+--------+----------+----------------+-------------+
    | name        | status | update | version  | update_version | auto_update |
    +-------------+--------+--------+----------+----------------+-------------+
    | theme-check | active | none   | 20231220 |                | off         |
    +-------------+--------+--------+----------+----------------+-------------+
    ```

- `Theme check`プラグインが有効になっていることを確認します。
  - 実行コマンド
    ```bash
    wp plugin status theme-check
    ```
  - 実行結果例
    ```bash
    Plugin theme-check details:
        Name: Theme Check
        Status: Active
        Version: 20231220
        Author: Themes Team
        Description: A simple and easy way to test your theme for all the latest WordPress standards and practices. A great theme development tool!
    ```

# `Theme check`プラグインを実行する
- `Theme Check`を実行します。
  - 実行コマンド
    ```bash
    wp theme-check run <実行対象のテーマ名>
    ```
  - 実行コマンド例
    ```bash
    wp theme-check run aaruupaka-prot
    ```
  - 実行結果例
    ```bash
    Error: 'theme-check' is not a registered wp command. See 'wp help' for available commands.
    ```