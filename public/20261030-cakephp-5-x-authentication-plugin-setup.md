---
title: 【CakePHP5.x】認証プラグインのセットアップ
tags:
  - CakePHP
  - CakePHP5
  - 認証プラグイン
  - Authentication
  - 備忘録
private: ture
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
posting_campaign_uuid: null
agreed_posting_campaign_term: false
---
# はじめに
CakePHP5系において、ログイン機能を実装しようとした際、認証機能の実装の前に、認証プラグインのセットアップが必要であることが分かりました。

今回は、認証プラグインのセットアップ手順、
後述するCakePHPの認証プラグインの公式リファレンス内、
「Quick Start」の最初に実行するコマンドについてまとめています。

# 公式リファレンス

[CakePHP 認証プラグイン　公式リファレンス](https://book.cakephp.org/authentication/4/)

CakePHPの公式リファレンスは上記のリンクです。

# 環境
- OS: Windows 11
- コマンドライン: Powershell
- ソース管理: Git, GitHub

# 認証プラグインのセットアップ

## 認証プラグインのインストール状況の確認

CakePHPプロジェクトを新規作成時、デフォルトではインストールされていないはずです。

しかし、プロジェクト作成から時間が経過したことなどにより、認証プラグインをインストールしたかわからない場合や、念のため確認したい場合などは、インストール状況の確認を行いましょう。

- Powershellを起動します。

- CakePHPプロジェクトのルートディレクトリに移動します。

- showコマンドを実行します。
  - 実行コマンド
    ```powershell
    composer show cakephp/authentication
    ```
  - 実行結果例
    ```powershell    
      In ShowCommand.php line 321:

      Package "cakephp/authentication" not found, try using --available (-a) to show all available pack
      ages.


      show [--all] [--locked] [-i|--installed] [-p|--platform] [-a|--available] [-s|--self] [-N|--name-only] [-P|--path] [-t|--tree] [-l|--latest] [-o|--outdated] [--ignore IGNORE] [-M|--major-only] [-m|--minor-only] [--patch-only] [-A|--sort-by-age] [-D|--direct] [--strict] [-f|--format FORMAT] [--no-dev] [--ignore-platform-req IGNORE-PLATFORM-REQ] [--ignore-platform-reqs] [--] [<package> [<version>]]


      What's next:
          Debug this Compose error with Gordon → docker ai "help me fix this compose error"
    ```
  - 確認事項
    - `Package "cakephp/authentication" not found`と出力されていることを確認します。
  - 補足
    - インストールされている場合、下記のように出力されます。
      - 出力結果例
        ```powershell
        name     : cakephp/authentication
        descrip. : Authentication plugin for CakePHP
        keywords : Authentication, auth, cakephp, middleware
        versions : * 4.2.1
        released : 2026-07-08, 2 months ago
        type     : cakephp-plugin
        license  : MIT License (MIT) (OSI approved) https://spdx.org/licenses/MIT.html#licenseText
        homepage : https://cakephp.org
        source   : [git] https://github.com/cakephp/authentication.git ad018852ebc0c2594894c5d820d4296e5357097c
        dist     : [zip] https://api.github.com/repos/cakephp/authentication/zipball/ad018852ebc0c2594894c5d820d4296e5357097c ad018852ebc0c2594894c5d820d4296e5357097c
        path     : /var/www/html/your-cakephp-project-name/vendor/cakephp/authentication
        names    : cakephp/authentication

        support
        docs : https://book.cakephp.org/authentication/4/en/
        forum : https://discourse.cakephp.org/
        issues : https://github.com/cakephp/authentication/issues
        source : https://github.com/cakephp/authentication

        autoload
        psr-4
        Authentication\ => src/

        requires
        cakephp/http ^5.0
        cakephp/utility ^5.0
        laminas/laminas-diactoros ^3.0
        php >=8.1
        psr/http-client ^1.0
        psr/http-message ^1.1 || ^2.0
        psr/http-server-handler ^1.0
        psr/http-server-middleware ^1.0

        requires (dev)
        cakephp/cakephp ^5.1.0
        cakephp/cakephp-codesniffer ^5.0
        firebase/php-jwt ^7.0
        phpunit/phpunit ^10.5.58 || ^11.5.3 || ^12.4 || ^13.0

        suggests
        cakephp/cakephp Install full core to use "CookieAuthenticator".
        cakephp/orm To use "OrmResolver" (Not needed separately if using full CakePHP framework).
        cakephp/utility Provides CakePHP security methods. Required for the JWT adapter and Legacy password hasher.
        ext-ldap Make sure this php extension is installed and enabled on your system if you want to use the built-in LDAP adapter for "LdapIdentifier".
        firebase/php-jwt If you want to use the JWT adapter add this dependency
        ```
  
## 認証プラグインのインストール

認証プラグインのインストールを行います。
まず、依存関係を問題なく解決できるかを確認後、インストールを行います。

- CakePHPプロジェクトのルートディレクトリにいることを確認します。

- 依存関係を解決できるか確認します。※本コマンド実行時にはインストールされません。
    - 実行コマンド
        ```powershell
        composer require cakephp/authentication --dry-run
        ```
    - 実行結果
        ```powershell
        Cannot create cache directory /var/www/.composer/cache/repo/https---repo.packagist.org/, or directory is not writable. Proceeding without cache. See also cache-read-only config if your filesystem is read-only.
        ./composer.json has been updated
        Running composer update cakephp/authentication
        Loading composer repositories with package information
        Cannot create cache directory /var/www/.composer/cache/repo/https---repo.packagist.org/, or directory is not writable. Proceeding without cache. See also cache-read-only config if your filesystem is read-only.
        Updating dependencies
        Lock file operations: 1 install, 0 updates, 0 removals
        - Locking cakephp/authentication (4.2.1)
        Installing dependencies from lock file (including require-dev)
        Package operations: 1 install, 0 updates, 0 removals
        - Installing cakephp/authentication (4.2.1)
        2 package suggestions were added by new dependencies, use `composer suggest` to see details.
        61 packages you are using are looking for funding.
        Use the `composer fund` command to find out more!
        No security vulnerability advisories found.
        Using version ^4.2 for cakephp/authentication
        ```
    - 確認事項
        - 依存関係に問題のないことを確認します。
        - 今回、キャッシュ関連の警告が出ていますが、今回は対応しません。

- ファイルの変更状況を確認します。
    - 実行コマンド
        ```powershell
        git status
        ```
    - 実行結果
        ```powershell
        Your branch is ahead of 'origin/feature/setup-authentication-plugin' by 2 commits.
        (use "git push" to publish your local commits)
        ```
    - 確認事項
        - 追加ファイルがないことを確認しました。

- プラグインのインストールを行います。
    - 実行コマンド
        ```powershell
        composer require cakephp/authentication
        ```
    - 実行結果
        ```powershell
        Cannot create cache directory /var/www/.composer/cache/repo/https---repo.packagist.org/, or directory is not writable. Proceeding without cache. See also cache-read-only config if your filesystem is read-only.
        ./composer.json has been updated
        Running composer update cakephp/authentication
        Loading composer repositories with package information
        Cannot create cache directory /var/www/.composer/cache/repo/https---repo.packagist.org/, or directory is not writable. Proceeding without cache. See also cache-read-only config if your filesystem is read-only.
        Updating dependencies
        Lock file operations: 1 install, 0 updates, 0 removals
        - Locking cakephp/authentication (4.2.1)
        Writing lock file
        Installing dependencies from lock file (including require-dev)
        Package operations: 1 install, 0 updates, 0 removals
        Cannot create cache directory /var/www/.composer/cache/files/, or directory is not writable. Proceeding without cache. See also cache-read-only config if your filesystem is read-only.
        - Downloading cakephp/authentication (4.2.1)
        - Installing cakephp/authentication (4.2.1): Extracting archive
        2 package suggestions were added by new dependencies, use `composer suggest` to see details.
        Generating autoload files
        61 packages you are using are looking for funding.
        Use the `composer fund` command to find out more!
        No security vulnerability advisories found.
        Using version ^4.2 for cakephp/authentication
        ```
    - 確認事項
        - 依存関係に問題のないことを確認します。
        - また、依存関係の解決の確認時と同様に、キャッシュに関する警告が出ていますが、今回は対応しません。

- ファイルの変更状況を確認します。
    - 実行コマンド
        ```powershell
        git status
        ```
    - 実行結果
        ```powershell
        On branch feature/setup-authentication-plugin
        Your branch is ahead of 'origin/feature/setup-authentication-plugin' by 2 commits.
        (use "git push" to publish your local commits)

        Changes not staged for commit:
        (use "git add <file>..." to update what will be committed)
        (use "git restore <file>..." to discard changes in working directory)
                modified:   your-cakephp-project-name/composer.json
                modified:   your-cakephp-project-name/composer.lock
        ```
    - 確認事項
        - 追加ファイルがないことを確認しました。

- 認証プラグインのインストールを確認を行います。
    - 実行コマンド
        ```powershell
        composer show cakephp/authentication
        ```
    - 実行結果
        ```powershell
        name     : cakephp/authentication
        descrip. : Authentication plugin for CakePHP
        keywords : Authentication, auth, cakephp, middleware
        versions : * 4.2.1
        released : 2026-07-08, 2 months ago
        type     : cakephp-plugin
        license  : MIT License (MIT) (OSI approved) https://spdx.org/licenses/MIT.html#licenseText
        homepage : https://cakephp.org
        source   : [git] https://github.com/cakephp/authentication.git ad018852ebc0c2594894c5d820d4296e5357097c
        dist     : [zip] https://api.github.com/repos/cakephp/authentication/zipball/ad018852ebc0c2594894c5d820d4296e5357097c ad018852ebc0c2594894c5d820d4296e5357097c
        path     : /var/www/html/your-cakephp-project-name/vendor/cakephp/authentication
        names    : cakephp/authentication

        support
        docs : https://book.cakephp.org/authentication/4/en/
        forum : https://discourse.cakephp.org/
        issues : https://github.com/cakephp/authentication/issues
        source : https://github.com/cakephp/authentication

        autoload
        psr-4
        Authentication\ => src/

        requires
        cakephp/http ^5.0
        cakephp/utility ^5.0
        laminas/laminas-diactoros ^3.0
        php >=8.1
        psr/http-client ^1.0
        psr/http-message ^1.1 || ^2.0
        psr/http-server-handler ^1.0
        psr/http-server-middleware ^1.0

        requires (dev)
        cakephp/cakephp ^5.1.0
        cakephp/cakephp-codesniffer ^5.0
        firebase/php-jwt ^7.0
        phpunit/phpunit ^10.5.58 || ^11.5.3 || ^12.4 || ^13.0

        suggests
        cakephp/cakephp Install full core to use "CookieAuthenticator".
        cakephp/orm To use "OrmResolver" (Not needed separately if using full CakePHP framework).
        cakephp/utility Provides CakePHP security methods. Required for the JWT adapter and Legacy password hasher.
        ext-ldap Make sure this php extension is installed and enabled on your system if you want to use the built-in LDAP adapter for "LdapIdentifier".
        firebase/php-jwt If you want to use the JWT adapter add this dependency
        ```
    - 確認事項
        - プラグイン情報が問題なく表示されることを確認します。

## 認証プラグインのロード
- 認証プラグインのロードを行います。
    - 実行コマンド
        ```powershell
        bin/cake plugin load Authentication
        ```
    - 実行結果
        ```powershell
        Plugin added successfully to `CONFIG/plugins.php`
        ```
    - 確認事項
        - プラグインの追加に成功した旨の内容を確認します。

- 変更のあったファイルを確認します。
    - 実行コマンド
        ```powershell
        git status
        ```
    - 実行結果
        ```powershell
        On branch feature/setup-authentication-plugin
        Your branch is up to date with 'origin/feature/setup-authentication-plugin'.

        Changes not staged for commit:
        (use "git add <file>..." to update what will be committed)
        (use "git restore <file>..." to discard changes in working directory)
                modified:   your-cakephp-project-name/config/plugins.php

        ```

- `your-cakephp-project-name/config/plugins.php`をステージングします。
    - 実行コマンド
        ```powershell
        git add your-cakephp-project-name/config/plugins.php
        ```
    - 実行結果
        ```powershell
        # 出力なし
        ```

- 変更内容を確認します。
    - 実行コマンド
        ```powershell
        git diff --staged
        ```
    - 実行結果
        ```powershell
        diff --git a/your-cakephp-project-name/config/plugins.php b/your-cakephp-project-name/config/plugins.php
        index 6be3095..779627e 100644
        --- a/your-cakephp-project-name/config/plugins.php
        +++ b/your-cakephp-project-name/config/plugins.php
        @@ -1,36 +1,15 @@
        <?php
        -/**
        - * Plugin configuration.
        - *
        - * In this file, you configure which plugins are loaded in the different states your app can be.
        - * It's loaded via the `parent::bootstrap();` call inside your `Application::bootstrap()` method.
        - * For more information see https://book.cakephp.org/5/en/plugins.html#loading-plugins-via-configuration-array
        - *
        - * CakePHP(tm) : Rapid Development Framework (https://cakephp.org)
        - * Copyright (c) Cake Software Foundation, Inc. (https://cakefoundation.org)
        - *
        - * Licensed under The MIT License
        - * For full copyright and license information, please see the LICENSE.txt
        - * Redistributions of files must retain the above copyright notice.
        - *
        - * @copyright     Copyright (c) Cake Software Foundation, Inc. (https://cakefoundation.org)
        - * @link          https://cakephp.org CakePHP(tm) Project
        - * @since         5.0.0
        - * @license       https://opensource.org/licenses/mit-license.php MIT License
        - */

        - /*
        -  * List of plugins to load in the form `PluginName` => `[configuration options]`.
        -  *
        -  * Available options:
        -  * - onlyDebug: Load the plugin only in debug mode. Default false.
        -  * - onlyCli: Load the plugin only in CLI mode. Default false.
        -  * - optional: Do not throw an exception if the plugin is not found. Default false.
        -  */
        return [
        -    'DebugKit' => ['onlyDebug' => true],
        -    'Bake' => ['onlyCli' => true, 'optional' => true],
        -    'Migrations' => ['onlyCli' => true],
        -
        -    // Additional plugins here
        +    'DebugKit' => [
        +        'onlyDebug' => true,
        +    ],
        +    'Bake' => [
        +        'onlyCli' => true,
        +        'optional' => true,
        +    ],
        +    'Migrations' => [
        +        'onlyCli' => true,
        +    ],
        +    'Authentication' => [],
        ];
        ```
    - 確認事項
        - `Authentication`が追加されたことを確認します。
        - 既存設定内容の設定項目が変更されていないことを確認します。
            - `DebugKit`
            - `Bake`
            - `Migrations`
    - 補足
      - 下記の変更内容は問題なしと判断しています。
          - コメントが削除されていること
          - 既存設定内容の設定項目が展開されていること



