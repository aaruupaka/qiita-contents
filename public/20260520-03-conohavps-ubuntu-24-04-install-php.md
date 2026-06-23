---
title: ConoHa VPSで構築したUbuntuにPHPをインストールする手順【備忘録】【Ubuntu24.04】【PHP8.3】
tags:
  - PHP
  - ConohaVPS
  - Ubuntu
  - Ubuntu24.04
  - PHP8.3
private: true
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: true
---
# はじめに

前回までの記事で、Apacheのインストールと動作確認を実施しました。

今回は、Apache上でPHPを実行できるようにするため、PHP 8.3をインストールします。

また、インストール後は `php -v` によるバージョン確認だけでなく、Apache経由でPHPが正しく動作するかも確認します。

前回の記事は下記です。
もしよろしければ読んでいただけると幸いです。

https://qiita.com/aaruupaka/items/60ddf031b8a7c9f52655


ConoHa VPSで構築したUbuntu 24.04環境で実施した内容の備忘録として残します。

# 実行環境
- 利用サービス:`ConohaVPS`
- ディストリビューション:`Ubuntu`
- バージョン: `24.04`
- アーキテクチャ: `x86_64`
- メモリ: `2GB`
- CPU: `3Core`
- SSD: `100GB`

# 前提条件
- Apache(Apache2)がインストールされていること。
- `http://IPアドレス`へアクセス時、`Apache2 Default Page`にアクセスすること。

# PHPをインストールする。
- PHPのインストール
    - 実行コマンド
        ```bash
        sudo apt install php libapache2-mod-php php-mysql -y
        ```
    - 実行結果
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/0e828100-7025-4c01-b2da-5134a4c74d6d.png)

- PHPの動作確認
    - 実行コマンド
        ```bash
        php -v
        ```
    - 実行結果
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/a5b6c3fa-7a87-4e8b-802d-9a6c3279b8da.png)
    - 確認事項
        - `PHP 8.3.6`といったようなバージョン情報が出力されること。
    - 備考

        今回はApache再起動なしでPHPが動作しました。

        環境によってはApache再起動が必要な場合があるため、
        動作しない場合は下記を実行してください。
        - 実行コマンド
            ```bash
            sudo systemctl restart apache2
            ```

- PHPがApache経由で動作するかを確認する。
    - phpinfo確認用のファイルを作成する。
        - 実行コマンド
            ```bash
            sudo nano /var/www/html/info.php
            ```
        - 実行結果
            <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/3fb47ee0-969e-4554-a0d0-551bcd5e498e.png)
        - エディタが開くので、下記の内容を記載する。
            - 記載内容
                ```php
                <?php
                phpinfo();
                ?>
                ```
            <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/4b8941f9-f4d7-4875-a022-3767e04d627b.png)
        - `Ctrl + O`入力後、`Enter`を押し、編集モードを終了する。
        - `Ctrl + X`を押し、エディタを閉じる。
        - 確認事項
            - info.phpが作成されていることを確認する。
                - 実行コマンド
                    ```bash
                    ls /var/www/html/
                    ```
                - 実行結果
                    <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/dc697c0a-97c9-400b-bec6-c2c3f3f6d04e.png)
                - 確認事項
                    - info.phpが出力されること
            - info.phpのファイル内容が意図したものになっていることを確認する。
                - 実行コマンド
                    ```bash
                    less /var/www/html/info.php
                    ```
                - 実行結果
                    <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/8de8f44d-b921-41f9-bd12-e4d30bd3a2d1.png)

                - 確認事項
                    - 下記の内容と出力内容が一致すること。
                        ```php
                        <?php
                        phpinfo();
                        ?>
                        ```
                    - `q`を押し、lessコマンドを終了する

    - ブラウザでinfo.phpにアクセスする。
        - URL
            - `http://IPアドレス/info.php`
        - アクセス結果
            <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/4da8e399-8570-46ef-a8fb-c5a31d14efc7.png)

        - 確認事項
            - PHP Versionが`8.3.x`であること
            - Server APIが`Apache 2.0 Handler`であること
            <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/3ecacb52-7200-4a3f-84d2-1ac99d54d208.png)
            <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/e7f58ed5-48c4-4972-895b-ae02b2e7c583.png)

    - phpinfo確認用ファイルを削除する。
        - 実行コマンド
            ```
            sudo rm -i /var/www/html/info.php
            ```
        - 実行結果
            <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/3879422f-d229-4c6d-b058-1a7f4a527711.png)
        - 対応事項
            - 削除対象が`/var/www/html/info.php`であることを確認し`y`入力し、`Enter`を押す。
        - 確認事項
            - info.phpが削除されていることを確認する。
                - 実行コマンド
                    ```bash
                    ls /var/www/html/
                    ```
                - 実行結果
                    <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/f0895eb3-66c2-4aca-86d5-db95331a64dc.png)
                - 確認事項
                    - info.phpが出力されないこと。
        :::note warn
        phpinfo() はサーバー構成やPHP設定などの情報を表示します。

        第三者に公開し続けることはセキュリティ上好ましくないため、
        動作確認後は削除しておくことを推奨します。
        :::

# おわりに

今回は、Ubuntu 24.04へPHP 8.3をインストールし、Apache経由でPHPが実行できることを確認しました。

次回はMariaDBのインストールやデータベースの初期設定を行い、WordPressを動作させるための環境を整えていく予定です。

WordPress構築手順をまとめた記事一覧は下記です。

https://qiita.com/aaruupaka/items/ed1fa439da66510d38b9

同じ環境を構築する際の参考になれば幸いです。