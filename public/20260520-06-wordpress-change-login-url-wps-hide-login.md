---
title: 【WordPress】WordPressのログインURLの変更手順【WPS Hide Login】
tags:
  - WordPress
  - Apache
  - Ubuntu
  - ConohaVPS
  - WPSHideLogin
private: false
updated_at: '2026-07-04T17:40:14+09:00'
id: 1976bfaa6485dc5f871b
organization_url_name: null
slide: false
ignorePublish: false
posting_campaign_uuid: 783b7a849caf11eefd91
agreed_posting_campaign_term: true
---
# はじめに
今回は、ログインURLの変更を行います。

Apacheのアクセスログをみてみたところ、知らないIPアドレスがWordpressのログインURLにアクセスしていたことが判明しました。

いつか不正アクセスを試みられるだろうと思っていましたが、ここまで速いのは想定外でした。

WordPressは世界中で利用されているCMSであるため、wp-login.phpへのアクセスを自動で試みるボットも非常に多く存在します。

今回は、WPS Hide Loginプラグインを利用してログインURLを変更する手順を紹介します。

# 作業環境
- ConohaVPS
- WordPress バージョン:6.9.4

# ログインURLの変更手順
- ダッシュボードにアクセスします。
    <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/0c0e0d8a-26b5-4ad7-b840-cedfb6b9a37c.png)

- `プラグイン`タブの`プラグインを追加`リンクを押下します。
    <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/8635b712-a0b0-465d-903b-9bd908a7cea8.png)

- `プラグインの検索`に`WPS Hide Login`と入力し、`今すぐインストール`ボタンを押下します。
    <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/a6734067-3d50-4ebd-8253-b4f758d4fafb.png)
    
  :::note info
  私は作者が`Remy Perona`さんのものをインストールしました。
  :::

- `有効化`ボタンを押下します。
    <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/02243626-427b-4dd8-8799-3429e2596f39.png)

- `設定`タブの`WPS Hide Login`リンクを押下します。
    <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/1cbe5d31-6693-4082-a8c9-adb9b96a8715.png)

- `ログインURL`の値を任意のものに変更し、`変更を保存`ボタンを押下します。
    <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/17b52a09-1b7c-429d-ae76-906493938f40.png)
    
  :::note info
    ログインURLには、`login` や `admin` のような推測されやすい単語だけを使用することは避けましょう。

    第三者が推測しにくい、十分にランダムな文字列を含むURLや、自分だけが分かる言葉を組み合わせたURLを設定することをおすすめします。
  :::

- 変更後のログインURLにアクセスします。
    - ログイン画面か、ダッシュボードに遷移することを確認します。
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/dbd227ff-c785-4a6b-8c2f-443c0c867084.png)

# Not Foundが出た場合の対処法
<br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/dfcccc5b-62c7-49df-80a2-4f784df73594.png)

ログインURL変更後、初回ログインURLアクセス時、`Not Found`ページに出てしまいました。

今回の環境では、Apacheのrewriteモジュールが無効かつ、、
AllowOverrideがNoneとなっていたために、
WPS Hide Loginが正常に動作しませんでした。

以下はその復旧手順です。

- WPS Hide Loginを無効化する。
    - SSH接続または、ConohaVPSのコンソールを起動し、ログインします。
    - cdコマンドを実行し、wordpressのプラグインのディレクトリに移動します。
        - 実行コマンド
            ```
            cd /var/www/html/wp-content/plugins/
            ```
    - lsコマンドを実行し、`wps-hide-login`が存在していることを確認します。
        - 実行コマンド
            ```
            ls -lts
            ```
        - 実行結果
            <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/d2d162e5-d623-4f18-a30e-883dd04fa8ce.png)
    - mvコマンドを実行し、`wps-hide-login`を`wps-hide-login-disabled`に変更します。
        - 実行コマンド
            ```
            sudo mv wps-hide-login wps-hide-login-disabled
            ```
    - 再度lsコマンドを実行し、ディレクトリ名が変更されていることを確認します。
        - 実行コマンド
            ```
            ls -lts
            ```
        - 実行結果
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/6fab7f74-f3ad-47c1-ad47-0c69e09adf36.png)
    - 初期ログインURLにアクセスし、ログイン画面に遷移することを確認します。
    <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/21cc7dc1-e8f0-4009-8d26-f3b1c169e13e.png)
    - ログインし、ダッシュボードにアクセスできれば、復旧作業は完了です。
    <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/91cfd75b-8f76-4052-971c-2a50f8af2040.png)
- Apacheのrewriteモジュールが有効か確認します。
    - 実行コマンド
        ```
        apache2ctl -M | grep rewrite
        ```
    - 実行結果
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/d6758016-01d5-4a5a-a791-89e26933ee43.png)
    - 確認事項
        - 何も出力されない場合は、有効化されていません。
        - `rewrite_module (shared)`が出力された場合、有効化されています。
        - 今回は、何も出力されなかったので、**有効化されていなかった**ようです。
- Apacheのrewriteモジュールを有効化します。
    - 実行コマンド
        ```
        sudo a2enmod rewrite
        ```
    - 実行結果
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/209b2f6d-3fda-4d08-94c8-99174b617bdf.png)
    - 確認事項
        - `Enabling module rewrite.`と出力されることを確認します。
- Apacheを再起動します。
    - 実行コマンド
        ```
        sudo systemctl restart apache2
        ```
    - 実行結果
- Apacheのrewriteモジュールが有効になったことを確認します。
    - 実行コマンド
        ```
        apache2ctl -M | grep rewrite
        ```
    - 実行結果
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/776c8ce0-1a2f-4ac2-b0da-56b3a4e70c7c.png)
    - 確認事項
        - `rewrite_module (shared)`と出力されることを確認します。
- `.htaccess`が存在しているかを確認する。
    - 実行コマンド
        ```
        ls -la /var/www/html/
        ```
    - 実行結果
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/e5b3bfe2-e392-408b-bebd-95c73cbc8986.png)
    - 確認事項
        - `.htaccess`が存在していることを確認します。
- `.htaccess`が許可されているか確認します。
    - 実行コマンド
        ```
        less /etc/apache2/apache2.conf
        ```
    - 実行結果
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/e9418219-06b5-45d9-84d6-a9504f3eb4a2.png)
    - 確認事項
        - `<Directory /var/www/>`のブロックを探し、`AllowOverride`の値を確認します。
        - `AllowOverride`の値が`None`であれば、無効化されています。
        - `AllowOverride`の値が`All`であれば、有効化されています。
- `AllowOverride`の値が`None`であった場合、`All`に変更します。
    - nanoコマンドでapache2.confを開きます。
        - 実行コマンド
            ```
            sudo nano /etc/apache2/apache2.conf
            ```
        - 実行結果
    - `<Directory /var/www/>`のブロックを探します。
    - `<Directory /var/www/>`ブロックの`AllowOverride`を`All`に書き換えます。
        - 変更前
            ```conf
            <Directory /var/www/>
                Options Indexes FollowSymLinks
                AllowOverride None
                Require all granted
            </Directory>
            ```
        - 変更後
            ```conf
            <Directory /var/www/>
                Options Indexes FollowSymLinks
                AllowOverride All
                Require all granted
            </Directory>
            ```
    - `ctrl + o`を入力後、`Enter`を押下し、変更内容を保存します。
    - `ctrl + x`でnanoコマンドを終了します。
- `.htaccess`が許可されているか確認します。
    - 実行コマンド
        ```
        less /etc/apache2/apache2.conf
        ```
    - 実行結果
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/c06f7dc2-d242-40f4-8b44-0b25167b74bc.png)
    - 確認事項
        - `<Directory /var/www/>`ブロックの`AllowOverride`が`All`になっていることを確認します。
- Apacheを再起動します。
    - 実行コマンド
        ```bash
        sudo systemctl restart apache2
        ```
    - 実行結果
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/11732005-114c-4cf9-9f8d-647354129fe1.png)
- `WPS Hide Login`を再度有効化します。
    - cdコマンドを実行し、wordpressのプラグインのディレクトリに移動します。
        - 実行コマンド
            ```
            cd /var/www/html/wp-content/plugins/
            ```
    - lsコマンドを実行し、`wps-hide-login-disabled`が存在していることを確認します。
        - 実行コマンド
            ```
            ls -lts
            ```
        - 実行結果
            <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/480fda5a-b34f-4c07-ac79-9110019ecfec.png)
    - mvコマンドを実行し、`wps-hide-login-disabled`を`wps-hide-login`に変更します。
        - 実行コマンド
            ```
            sudo mv wps-hide-login-disabled wps-hide-login
            ```
    - 再度lsコマンドを実行し、ディレクトリ名が変更されていることを確認します。
        - 実行コマンド
            ```
            ls -lts
            ```
        - 実行結果
            <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/aed629fc-b099-4694-a2d0-54d00fdf590b.png)
    - WordPressのダッシュボードにアクセスします。
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/9bc4d7c8-ec23-408d-8e71-94071632928f.png)
    - `プラグイン`タブの`インストール済みのプラグイン`リンクを押下します。
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/cc484bb9-492d-46a3-95e3-8e6d30b874d1.png)
    - `WPS Hide Login`の`有効化`リンクを押下します。
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/80bacbc8-b0f3-4aca-a316-6daf95b32106.png)
    - `設定`タブの`WPS Hide Login`リンクを押下します。
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/1cbe5d31-6693-4082-a8c9-adb9b96a8715.png)
    - `ログインURL`の値が任意のものになっていることを確認します。
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/17b52a09-1b7c-429d-ae76-906493938f40.png)

# おわりに

今回は、`WPS Hide Login`を利用してWordPressのログインURLを変更する手順を紹介しました。

ログインURLを変更するだけで不正アクセスを完全に防げるわけではありませんが、既知のログインURLを狙ったアクセスを減らす効果が期待できます。

また、今回のように`Not Found`が表示された場合でも、Apacheの設定や`rewrite`モジュール、`.htaccess`の設定を確認することで復旧できるケースがあります。

同じ環境でWordPressを構築している方の参考になれば幸いです。

# 参考資料
- ワプ活「WordPressのログインURLを変更する方法！プラグインを使ってセキュリティ対策を」

https://www.conoha.jp/lets-wp/wp-loginurl/#wp-loginurl_wps-hide-login

# 関連資料
私が公開しているWordPress構築手順をまとめたページを作成しています。
もしよければ、閲覧いただけると嬉しいです。

https://qiita.com/aaruupaka/items/ed1fa439da66510d38b9

同じ環境を構築する際の参考になれば幸いです。
