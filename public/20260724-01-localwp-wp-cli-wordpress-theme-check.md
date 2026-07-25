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

<2026年7月25日　追記>
GitHub版を取得し、実行したところ下記の結果が得られた。
- 管理画面で取得できるチェック結果は同一の内容
- `wp theme-check run `が実行でき、結果が出た
  - なお、管理画面で出るものとは出力順が異なるため、内容が一致しているかまでは未確認


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
  - 実行結果例（GItHub版（バージョン： 20260508））
    ```bash
    +-------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
    | type        | value                                                                                                                                                                                           |
    +-------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
    | REQUIRED    | Could not find add_theme_support( 'automatic-feed-links' ). See: add_theme_support <?php add_theme_support( $feature ); ?>                                                                      |
    | REQUIRED    | Could not find wp_link_pages. See: wp_link_pages <?php wp_link_pages( $args ); ?>                                                                                                               |
    | RECOMMENDED | No reference to register_block_pattern was found in the theme. Theme authors are encouraged to implement custom block patterns as a transition to block themes.                                 |
    | RECOMMENDED | No reference to register_block_style was found in the theme. Theme authors are encouraged to implement new block styles as a transition to block themes.                                        |
    | RECOMMENDED | The theme doesn't have comment pagination code in it. Use paginate_comments_links() or the_comments_navigation or the_comments_pagination or next_comments_link() and previous_comments_link()  |
    |             | to add comment pagination.                                                                                                                                                                      |
    | RECOMMENDED | Could not find the comment-reply script enqueued.                                                                                                                                               |
    | RECOMMENDED | Could not find comments_template. See: comments_template <?php comments_template( $file, $separate_comments ); ?>                                                                               |
    | RECOMMENDED | Could not find wp_list_comments. See: wp_list_comments <?php wp_list_comments( $args ); ?>                                                                                                      |
    | RECOMMENDED | Could not find comment_form. See: comment_form <?php comment_form(); ?>                                                                                                                         |
    | WARNING     | Could not find a copyright notice for the theme. A copyright notice is needed if your theme is licenced as GPL. Learn how to add a copyright notice (opens in a new window).                    |
    | RECOMMENDED | No reference to add_editor_style() was found in the theme. It is recommended that the theme implement editor styling, so as to make the editor content match the resulting post output in the t |
    |             | heme, for a better user experience.                                                                                                                                                             |
    | REQUIRED    | Could not find the file readme.txt in the theme.                                                                                                                                                |
    | RECOMMENDED | This theme doesn't seem to support the standard avatar functions. Use get_avatar or wp_list_comments to add this support.                                                                       |
    | RECOMMENDED | No reference to nav_menu's was found in the theme. Note that if your theme has a menu bar, it is required to use the WordPress nav_menu functionality for it.                                   |
    | RECOMMENDED | The theme doesn't have post pagination code in it. Use posts_nav_link() or paginate_links() or the_posts_pagination() or the_posts_navigation() or next_posts_link() and previous_posts_link()  |
    |             | to add post pagination.                                                                                                                                                                         |
    | RECOMMENDED | No reference to the_post_thumbnail() was found in the theme. It is recommended that the theme implement this functionality instead of using custom fields for thumbnails.                       |
    | RECOMMENDED | No reference to post-thumbnails was found in the theme. If the theme has a thumbnail like functionality, it should be implemented with add_theme_support( "post-thumbnails" ) in the functions. |
    |             | php file.                                                                                                                                                                                       |
    | REQUIRED    | No screenshot detected! Please include a screenshot.png or screenshot.jpg.                                                                                                                      |
    | REQUIRED    | License: is missing from your style.css header.                                                                                                                                                 |
    | REQUIRED    | License URI: is missing from your style.css header.                                                                                                                                             |
    | REQUIRED    | Text Domain: is missing from your style.css header.                                                                                                                                             |
    | REQUIRED    | Tested up to: is missing from your style.css header. Also, this should be numbers only, so 5.0 and not WP 5.0                                                                                   |
    | REQUIRED    | Requires PHP: is missing from your style.css header.                                                                                                                                            |
    | INFO        | Tags: is either empty or missing in style.css header.                                                                                                                                           |
    | RECOMMENDED | Theme URI: is missing from your style.css header.                                                                                                                                               |
    | RECOMMENDED | Author URI: is missing from your style.css header.                                                                                                                                              |
    | RECOMMENDED | .sticky css class is recommended in your theme css.                                                                                                                                             |
    | RECOMMENDED | .bypostauthor css class is recommended in your theme css.                                                                                                                                       |
    | RECOMMENDED | .alignleft css class is recommended in your theme css.                                                                                                                                          |
    | RECOMMENDED | .alignright css class is recommended in your theme css.                                                                                                                                         |
    | RECOMMENDED | .aligncenter css class is recommended in your theme css.                                                                                                                                        |
    | RECOMMENDED | .wp-caption css class is recommended in your theme css.                                                                                                                                         |
    | RECOMMENDED | .wp-caption-text css class is recommended in your theme css.                                                                                                                                    |
    | RECOMMENDED | .gallery-caption css class is recommended in your theme css.                                                                                                                                    |
    | INFO        | Only one text-domain is being used in this theme. Make sure it matches the theme's slug correctly so that the theme will be compatible with WordPress.org language packs. The domain found is . |
    | RECOMMENDED | No reference to add_theme_support( "custom-header", $args ) was found in the theme. It is recommended that the theme implement this functionality if using an image for the header.             |
    | RECOMMENDED | No reference to add_theme_support( "custom-background", $args ) was found in the theme. If the theme uses background images or solid colors for the background, then it is recommended that the |
    |             |  theme implement this functionality.                                                                                                                                                            |
    | RECOMMENDED | No reference to add_theme_support( "custom-logo", $args ) was found in the theme. It is recommended that the theme implement this functionality.                                                |
    | RECOMMENDED | No reference to add_theme_support( "html5", $args ) was found in the theme. It is strongly recommended that the theme implement this functionality.                                             |
    | RECOMMENDED | No reference to add_theme_support( "responsive-embeds" ) was found in the theme. It is recommended that the theme implement this functionality.                                                 |
    | RECOMMENDED | No reference to add_theme_support( "align-wide" ) was found in the theme. It is recommended that the theme implement this functionality.                                                        |
    | RECOMMENDED | No reference to add_theme_support( "wp-block-styles" ) was found in the theme. It is recommended that the theme implement this functionality.                                                   |
    | REQUIRED    | No reference to add_theme_support( "title-tag" ) was found in the theme.                                                                                                                        |
    | RECOMMENDED | <title> tag was found in the file header.php. Document titles must not be hard coded, use add_theme_support( "title-tag" ) instead. Line 6: <title><?php bloginfo('name'); ?></title>           |
    +-------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
    ```