# 前提
- サイトヘルスの内容<br>
    ![alt text](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260524-01-wordpress-site-health-improvements/images/20260524-01-02.png)

# 作業前準備
- rootアカウントの作業ディレクトリに移動する
    - 実行コマンド
        ```sh
        cd /root
        ```
    - 確認事項
        - `/root`に移動できたことを確認する。
            - 実行コマンド
                ```sh
                pwd
                ```

- 作業ディレクトリを作成する。
    - 実行コマンド
        ```sh
        mkdir 20260527-01-wordpress-site-health-improvements-php-module
        ```
    - 実行結果
    - 確認事項
        - `/root`配下に`20260527-01-wordpress-site-health-improvements-php-module`が作成されていること
            - 実行コマンド
                ```sh
                ls -la /root/
                ```

- 本件作業ディレクトリに移動する。
    - 実行コマンド
        ```sh
        cd /root/20260527-01-wordpress-site-health-improvements-php-module
        ```
    - 確認事項
        - `/root/20260527-01-wordpress-site-health-improvements-php-module`に移動できていることを確認する。
            - 実行コマンド
                ```sh
                pwd
                ```

- php.iniの配置場所を探す
    - 実行コマンド
        ```sh
        php -i | grep "Loaded Configuration File"
        ```
    - 実行結果<br>
        ![](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260524-01-wordpress-site-health-improvements/images/20260524-01-01.png)
    - 所感
        - どうも、php.iniはエクステンションインストール時に自動で更新されることがあるようなので、<br>自分で編集する必要はないみたい。

- PHPのエクステンションのインストールの前に、ubuntuのアップデートを行う。
    - アップデートの取得を行う
        - 実行コマンド
            ```sh
            sudo apt update
            ```
        - 実行結果
    - アップデート対象があるか確認する
        - 実行コマンド
            ```sh
            apt list --upgradable
            ```
        - 実行結果
    - アップデート対象がある場合、アップデートを行う
        - 実行コマンド
            ```sh
            sudo apt upgrade -y
            ```
        - 実行結果
    - OSの再起動が必要なら再起動する。
        - 実行コマンド
            ```sh
            sudo reboot
            ```
        - 実行結果

- PHPのエクステンションが入っているか確認する。
    - 実行コマンド
        ```sh
        php -m | grep -E 'curl|dom|imagick|mbstring|zip|intl|gd'
        ```
    - 実行結果
    ![alt text](images/20260524-01-05.png)

# バックアップ
- php.iniをバックアップする。
    - 実行コマンド
        ```sh
        sudo cp /etc/php/8.3/apache2/php.ini /etc/php/8.3/apache2/php.ini.bak_$(date +%Y%m%d)
        ```
    - 実行結果
        ![alt text](images/20260524-01-07.png)
    - 確認事項
        - `php.ini.bak_yyyymmdd`という名前のファイルが作成されていること
            - yyyymmdd部分は、実行日
            - 2026年5月28日に実行した場合は`php.ini.bak_20260528`となる。
        - 確認結果<br>
            ![alt text](images/20260524-01-06.png)

- エクステンションインストール前の`/etc/php/8.3/mods-available/`のファイル構成をバックアップする
    - 実行コマンド
        ```sh
        ls -la /etc/php/8.3/mods-available/ > before_mods_available.txt
        ```
    - 確認事項
        - `root/20260527-01-wordpress-site-health-improvements-php-module`配下に、`before_mods_available.txt`が作成されていることを確認する。
            - 実行コマンド
                ```sh
                ls -la /root/20260527-01-wordpress-site-health-improvements-php-module
                ```
            - 実行結果<br>
                ![alt text](images/20260524-01-08.png)
        - `before_mods_available.txt`に中身があることを確認する。
            - 実行コマンド
                ```sh
                less /root/20260527-01-wordpress-site-health-improvements-php-module/before_mods_available.txt
                ```
            - 実行結果<br>
                ![alt text](images/20260524-01-09.png)

- エクステンションインストール前の`/etc/php/8.3/apache2/conf.d/`のファイル構成をバックアップする
    - 実行コマンド
        ```sh
        ls -la /etc/php/8.3/apache2/conf.d/ > before_apache2_conf.d.txt
        ```
    - 確認事項
        - `root/20260527-01-wordpress-site-health-improvements-php-module`配下に、`before_apache2_conf.d.txt`が作成されていることを確認する。
            - 実行コマンド
                ```sh
                ls -la /root/20260527-01-wordpress-site-health-improvements-php-module
                ```
            - 実行結果<br>
                ![alt text](images/20260524-01-10.png)
        - `before_apache2_conf.d.txt`に中身があることを確認する。
            - 実行コマンド
                ```sh
                less /root/20260527-01-wordpress-site-health-improvements-php-module/before_apache2_conf.d.txt
                ```
            - 実行結果<br>
                ![alt text](images/20260524-01-11.png)

# PHPのエクステンションのインストール
- PHPのエクステンションをインストールする
    - 実行コマンド
        ```sh
        sudo apt install php-curl php-xml php-mbstring php-zip php-intl php-imagick php-gd -y
        ```
    - 実行結果
        ![alt text](images/20260524-01-12.png)

- Apache2を再起動する。
    - 実行コマンド
        ```sh
        sudo systemctl restart apache2
        ```

# インストール後チェック
- PHPのエクステンションがインストールされていることを確認する
    - 実行コマンド
        ```sh
        php -m | grep -E 'curl|dom|imagick|mbstring|zip|intl|gd'
        ```
    - 実行結果
        ![alt text](images/20260524-01-13.png)
    - 確認事項
        - 下記のエクステンションがインストールされていること
            - curl
            - dom
            - imagick
            - mbstring
            - zip
            - intl
            - gd

- php.iniに更新内容があるか確認する
    - 実行コマンド
        ```sh
        sudo diff -u /etc/php/8.3/apache2/php.ini.bak_20260527 /etc/php/8.3/apache2/php.ini
        ```
    - 実行結果
        ![alt text](images/20260524-01-14.png)
    - 確認事項
        - 変更がある場合は、下記のエクステンションに関する事項であることを確認する。
            - curl
            - dom
            - imagick
            - mbstring
            - zip
            - intl
            - gd
        - もし、差異が出ない場合は、php.iniを編集する形ではなく下記の内容が更新されている可能性がある
            - `/etc/php/8.3/mods-available/`<br>
                ![alt text](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260524-01-wordpress-site-health-improvements/images/20260524-01-03.png)
            - `/etc/php/8.3/apache2/conf.d/`<br>
                ![alt text](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260524-01-wordpress-site-health-improvements/images/20260524-01-04.png)

- エクステンションインストール後の`/etc/php/8.3/mods-available/`のファイル構成をバックアップする
    - 実行コマンド
        ```sh
        ls -la /etc/php/8.3/mods-available/ > after_mods_available.txt
        ```
    - 確認事項
        - `root/20260527-01-wordpress-site-health-improvements-php-module`配下に、`after_mods_available.txt`が作成されていることを確認する。
            - 実行コマンド
                ```sh
                ls -la /root/20260527-01-wordpress-site-health-improvements-php-module
                ```
            - 実行結果
                ![alt text](images/20260524-01-15.png)
        - `after_mods_available.txt`に中身があることを確認する。
            - 実行コマンド
                ```sh
                less /root/20260527-01-wordpress-site-health-improvements-php-module/after_mods_available.txt
                ```
            - 実行結果
                ![alt text](images/20260524-01-16.png)

- インストール前後の`/etc/php/8.3/mods-available/`のファイル構成を比較する。
    - 実行コマンド
        ```sh
        sudo diff -u /root/20260527-01-wordpress-site-health-improvements-php-module/before_mods_available.txt /root/20260527-01-wordpress-site-health-improvements-php-module/after_mods_available.txt
        ```
    - 実行結果
        ![alt text](images/20260524-01-17.png)
    - 確認事項
        - 下記のエクステンションに関するiniファイルが増えていること。
            - curl
            - dom
            - imagick
            - mbstring
            - zip
            - intl
            - gd

- エクステンションインストール後の`/etc/php/8.3/apache2/conf.d/`のファイル構成をバックアップする
    - 実行コマンド
        ```sh
        ls -la /etc/php/8.3/apache2/conf.d/ > after_apache2_conf.d.txt
        ```
    - 確認事項
        - `root/20260527-01-wordpress-site-health-improvements-php-module`配下に、`after_apache2_conf.d.txt`が作成されていることを確認する。
            - 実行コマンド
                ```sh
                ls -la /root/20260527-01-wordpress-site-health-improvements-php-module
                ```
            - 実行結果
                ![alt text](images/20260524-01-18.png)
        - `after_apache2_conf.d.txt`に中身があることを確認する。
            - 実行コマンド
                ```sh
                less /root/20260527-01-wordpress-site-health-improvements-php-module/after_apache2_conf.d.txt
                ```
            - 実行結果
                ![alt text](images/20260524-01-19.png)

- インストール前後の`/etc/php/8.3/apache2/conf.d/`のファイル構成を比較する。
    - 実行コマンド
        ```sh
        sudo diff -u /root/20260527-01-wordpress-site-health-improvements-php-module/before_apache2_conf.d.txt /root/20260527-01-wordpress-site-health-improvements-php-module/after_apache2_conf.d.txt
        ```
    - 実行結果
        ![alt text](images/20260524-01-20.png)
    - 確認事項
        - 下記のエクステンションに関するiniファイルへのリンクが増えていること。
            - curl
            - dom
            - imagick
            - mbstring
            - zip
            - intl
            - gd

# WordPress管理画面の確認
- WordPressのダッシュボードにアクセスする。
    ![alt text](images/20260524-01-22.png)
- サイトヘルスを開き、モジュールに関する`1件の致命的な問題`が改善されていることを確認する。
    ![alt text](images/20260524-01-21.png)

# その他・留意事項
RSSウィジェットには「XML or PCRE extensions not loaded!」が表示されていたが、php -m で xml系および pcre が読み込まれていることを確認した。
また、/etc/php/8.3/apache2/conf.d/ に xml / dom / simplexml / xmlreader / xmlwriter の設定リンクが存在することを確認した。
pcre は conf.d に個別iniが見当たらないが、php -m 上では読み込まれているため、PHPモジュール未導入が原因とは考えにくい。