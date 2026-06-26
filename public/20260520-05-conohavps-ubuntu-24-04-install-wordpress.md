---
title: ConoHa VPSで構築したUbuntuにWordPressをインストールする手順【備忘録】【Ubuntu24.04】
tags:
  - WordPress
  - Ubuntu
  - mariadb
  - ConohaVPS
  - Ubuntu24.04
private: false
updated_at: '2026-06-26T15:44:36+09:00'
id: 20c390cb93d80d6cc06c
organization_url_name: null
slide: false
ignorePublish: false
---
# はじめに

ConoHa VPS上に構築したUbuntu 24.04へWordPressをインストールする手順をまとめます。

本記事では、WordPressの配置から初期設定までを実施し、ブラウザから管理画面へログインできる状態を目指します。

なお、Apache・PHP・MariaDBのインストール手順については別記事で紹介しています。本記事では、それらのセットアップが完了している前提で作業を進めます。

同じ環境でWordPressを構築する際の備忘録として、どなたかの参考になれば幸いです。


# 実行環境
- 利用サービス:`ConohaVPS`
- ディストリビューション:`Ubuntu`
- バージョン: `24.04`
- アーキテクチャ: `x86_64`
- メモリ: `2GB`
- CPU: `3Core`
- SSD: `100GB`

# 前提条件
- apacheのインストールが完了していること
- phpのインストールが完了していること
- MariaDBのインストールが完了していること。

# DBの準備を行う
- DBに接続する
    - 実行コマンド
        ```bash
        sudo mysql
        ```
    - 実行結果
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/96b91016-0adf-4651-bcd1-58811fe52deb.png)
- DBを作成する。
    - 実行コマンド
        ```sql
        CREATE DATABASE wordpress;
        ```
    - 実行結果
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/3212bf4d-ec2e-45cf-9f73-88c3efaf48d8.png)
- DBのユーザーを作成する。
    - 実行コマンド
        ```sql
        CREATE USER 'wp_user'@'localhost' IDENTIFIED BY '任意パスワード';
        ```
    - 実行結果
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/fceecb80-0505-46c7-a5bb-2d2615d38507.png)
- DBのユーザーに権限を付与する。
    - 実行コマンド
        ```sql
        GRANT ALL PRIVILEGES ON wordpress.* TO 'wp_user'@'localhost';
        ```
    - 実行結果
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/f90dea11-9bf1-4098-a790-35087af8140a.png)
- 権限情報の再読み込みを行う
    - 実行コマンド
        ```sql
        FLUSH PRIVILEGES;
        ```
    - 実行結果
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/d8a42101-12e3-48c5-b553-c4992013597f.png)
- DB接続を切断する。
    - 実行コマンド
        ```sql
        exit
        ```
    - 実行結果
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/368e9454-22c6-4584-b87d-0d77c60404cd.png)

# WordPressのダウンロードおよび配置を行う
- 作業ディレクトリに移動する。
    - 実行コマンド
        ```bash
        cd /tmp
        ```

- 本件作業用ディレクトリを作成する。
    - 実行コマンド
        ```bash
        mkdir /tmp/20260507-01-wordpress
        ```
    - 実行結果
    <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/5792b8fb-863b-4354-8e61-006685b11d2e.png)
- 本件作業用ディレクトリに移動する。
    - 実行コマンド
        ```
        cd /tmp/20260507-01-wordpress
        ```
    - 実行結果
    <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/ce86b6c0-bd9c-4c6a-a068-ff8e0af2ea81.png)
- WordPressをダウンロードする。
    - 実行コマンド
        ```bash
        wget https://wordpress.org/latest.tar.gz
        ```
    - 実行結果
    <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/00227b1c-b7d9-4d04-9dce-d054807df859.png)
    - 確認事項
- `latest.tar.gz`がダウンロードされていることを確認する。
    - 実行コマンド
        ```bash
        ls -lts
        ```
    - 実行結果
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/2f1461e9-9230-4eff-86df-e73558f0eb25.png)
    - 確認事項
        - `latest.tar.gz`が出力されること。
- `latest.tar.gz`を解凍する。
    - 実行コマンド
        ```bash
        tar -xvzf latest.tar.gz
        ```
    - 実行結果
      <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/bc8b1798-398b-4b63-bf40-b445a14b29a3.png)
    - 確認事項
        - `wordpress`ディレクトリが出力されること。
            - 実行コマンド
                ```bash
                ls -lts
                ```
            - 実行結果
                <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/43cd65db-65fc-4a21-b335-1c77086dee01.png)
- Apacheのデフォルトページがあるか確認し、存在する場合は削除する。
    - 実行コマンド
        ```bash
        ls -lts /var/www/html/
        ```
    - 実行結果
    <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/549cac95-83eb-4226-9297-6830866546fe.png)
    - 確認事項
        - index.htmlがあるかを確認する。
            - 存在する場合、apache2のデフォルトページであるかを確認する。
                - 実行コマンド
                    ```bash
                    less /var/www/html/index.html
                    ```
                - 実行結果
                <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/b2b602aa-df8b-4dbe-8c8e-ebbabf6692bb.png)
                - 確認事項
                    - `Apache2 Default Page`という文言があることを確認する。
            - lessコマンドを終了する
              - 実行コマンド
                  ```bash
                  q
                  ```
          - `index.html`を削除する。
              - 実行コマンド
                  ```bash
                  sudo rm -i /var/www/html/index.html
                  ```
              - 実行結果
                  <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/33e82b13-3010-45c4-be72-772d764974d6.png)
              - 確認事項
                  - `index.html`が存在しないことを確認する
                      - 実行コマンド
                          ```
                          ls -lts /var/www/html/
                          ```
                      - 実行結果
                          <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/7cc4310b-49aa-4b8d-9ded-4c7ff952845a.png)
- WordPressを配置する。
    - 実行コマンド
        ```bash
        sudo cp -R wordpress/* /var/www/html/
        ```
    - 実行結果
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/80f82959-0776-41e0-a160-1508985ff9ef.png)
    - 確認事項
        - `wordpress`配下のフォルダが`/var/www/html/`配下に配置されていることを確認する。
            - 実行コマンド
                ```bash
                ls -lts /var/www/html
                ```
            - 実行結果
                <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/49f59245-6aa5-47ba-bac3-ba30707ba053.png)
- `/var/www/html/`配下の所有者を変更する。
    - 実行コマンド
        ```bash
        sudo chown -R www-data:www-data /var/www/html/
        ```
    - 実行結果
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/2644baf6-4545-4db1-8d64-3d496698d459.png)
    - 確認事項
        - 所有者および、所属グループが`www-data`になっていることを確認する。
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/b02276a8-9e5a-4ffc-81a1-cf87e8e6f52c.png)

  :::note info
  - apacheは下記の情報を用い動いています。
      - ユーザー：www-data
      - グループ：www-data
  - ここでは、apacheが問題なく`/var/www/html/`配下にアクセスできるよう、所有者および、グループを`www-data:www-data`に変更しています。
  :::
- `/var/www/html/`配下のディレクトリの権限を変更する。
    - 実行コマンド
        ```bash
        sudo find /var/www/html/ -type d -exec chmod 755 {} \;
        ```
      :::note info
      - `-type d` はディレクトリのみを対象とするオプションです。
      :::
      :::note info
      ## `-exec chmod 644 {} \;` について
      - `-exec`
          - 見つかった対象に対してコマンドを実行します。
      - `{}`
          - 対象フォルダ/ディレクトリのパスが入ります。
      - `\;`
          - コマンドの終了を意味します。（;はシェルの区切り文字のためエスケープが必要）
      - `-exec ... {} \;` 
          - 「1件ずつ処理する」ようにします。
      - `-exec ... {} + `
          - 「まとめて処理」ようにします。（高速）
      :::

    - 実行結果
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/6f3353c5-e1fd-4a63-9bbf-9df69d9e28df.png)
    - 確認事項
        - ディレクトリの権限が`rwxr-xr-x`になっていることを確認する。
            <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/17662910-c113-482b-80fe-bc9e6e81fb35.png)

  :::note info
  - ディレクトリには「実行権限(x)」が必要です。
    - 755 = rwxr-xr-x
      - 所有者：読み書き実行可能
      - 所属グループ：読み取り・実行のみ
      - 上記以外のその他：読み取り・実行のみ
    - 実行権限がないとディレクトリ内にアクセスできない（403エラーの原因になる）
  :::

- `/var/www/html/`配下のフォルダの権限を変更する。
    - 実行コマンド
        ```bash
        sudo find /var/www/html/ -type f -exec chmod 644 {} \;
        ```
      :::note info
      - `-type f` はフォルダのみを対象とするオプションです。
      :::
    - 実行結果
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/1c49e9de-85b1-45cf-872e-c427844754b3.png)
    - 確認事項
        - フォルダの権限が`rw-r--r--`になっていることを確認する。
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/fc97be53-efb6-4916-8356-86c75b307245.png)
  :::note info
  - フォルダの場合「実行権限(x)」は不要です。
    - 644 = rw-r--r--
      - 所有者：読み書き可能
      - 所属グループ：読み取りのみ
      - 上記以外のその他：読み取りのみ
  - HTMLや、PHPはApacheがフォルダを読み取り処理を行うので、実行権限は必要ありません。
  - 今回は関係ないですが`.sh`フォルダなど、OSが直接実行するバッチフォルダ等であれば「実行権限(x)」が必要になります。
  :::
- ブラウザでアクセスチェックを行う。
    - URL
        ```
        http://IPアドレス
        ```
    - 実行結果
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/e57fba15-4097-4d6f-9fba-a86b3f33d590.png)
    - 確認事項
        - 言語選択画面が出ることを確認する。

# WordPressの初期設定を行う。
- ブラウザでwordpressのトップページにアクセスする。
    - URL
        ```
        http://IPアドレス
        ```
    - 実行結果
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/e57fba15-4097-4d6f-9fba-a86b3f33d590.png)
    - 確認事項
        - 言語選択画面が出ることを確認する。
- 言語選択を行い、`次へ`ボタンを押下します。
    <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/cb061e9a-b441-4bec-86e3-ba91d2d21bea.png)

- 設定項目に関する説明が出るので、内容を確認して、`さあ、始めましょう！`ボタンを押下します。
  <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/59f13fc0-3cd2-4853-92a5-bcdb58bd3496.png)

- 下記のDB接続情報および、設定項目を入力後、`送信ボタン`を押下します。
  - データベース名
  - ユーザー名
  - パスワード
  - データベースのホスト名
  - テーブル接頭辞
      <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/6c823543-71a0-4352-be9f-651a9b8ec272.png)

- DBと通信できる状態であることを確認し、`インストール実行`ボタンを押下します。
    <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/d6870394-a7a3-4373-a5de-fb6d11438412.png)
- 下記の設定項目を入力し、`Wordpressをインストール`ボタンを押下します。
  - サイトのタイトル
  - ユーザー名
  - パスワード
  - メールアドレス
  :::note warn
  ユーザー名はadmin等推測されやすい名称にするのは避けましょう
  :::
  :::note info
  ユーザーなどは後から追加削除することができます。
  :::
    <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/1e5fb1cb-80a9-4f9a-ba29-e31730def687.png)
- WordPressがインストールされたことを確認し、`ログイン`リンクをクリックします。
    <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/36d81083-9103-4610-8892-4756ac1c7b7d.png)
- 下記項目を入力し、`ログイン`ボタンを押下します。
<br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/9eeb39fb-bf5c-4826-a7e8-4015103060b9.png)

- ダッシュボードに遷移すれば、初期設定は完了です。
<br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/ad385905-2053-41ad-9e75-dad9e8931742.png)

- ブラウザでwordpressのトップページにアクセスし、Hello World!が表示されることを確認します。
    - URL
        ```
        http://IPアドレス
        ```
    - 実行結果
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/326c050a-abe5-41d4-9bac-d92fcd89af16.png)

# 初期ページの非公開化
- Hello world!を非公開化する。

  :::note info
  WordPressには初期状態でサンプル記事やサンプルページが登録されています。

  公開したままでも問題ありませんが、
  実運用では不要なため非公開化しておきます。
  :::
    - ダッシュボードにアクセスします。
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/ad385905-2053-41ad-9e75-dad9e8931742.png)
    - `投稿`タブの`投稿一覧`リンクを押下します。
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/5e2c4092-d69f-4d7f-af23-bdc100cbc484.png)
    - `Hello world!`の投稿にカーソルを合わせ、`クイック編集`リンクを押下します。
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/99ab008a-2feb-460c-afac-b2ec66dd4a36.png)
    - `非公開`のチェックボックスを選択し、`更新`ボタンを押下します。
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/07bd4bc2-0aa5-4e17-ac29-2a9be290e9a0.png)
    - トップページにアクセスし、`Hello World!`が表示されていないことを確認します。
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/cb015d7c-e851-4b58-9401-7ecb20383591.png)
- サンプルページを非公開化する。
    - `固定ページ`タブの`固定ページ一覧`リンクを押下します。
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/65cac73c-500e-49bc-be2a-86dbd9fa2f9f.png)
    - `サンプルページ`の投稿にカーソルを合わせ、`クイック編集`リンクを押下します。
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/1c6ab8db-2594-464a-a957-741341af8227.png)
    - `非公開`のチェックボックスを選択し、`更新`ボタンを押下します。
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/e2a0dae2-3c14-4258-865d-bc84009dcf22.png)
    - トップページの`サンプルページ`リンクが消えていることを確認します。
     <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/681f7924-a69f-448e-88f1-cb27d9af82b7.png)

# タイムゾーンを確認する。
- `設定`タブの`一般`リンクを押下します。
    <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/0eda450a-2af1-4045-b2e7-decd6ab998db.png)
- タイムゾーンが`東京`になっていることを確認します。
    <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/d91f462a-2d02-472f-ab75-af088a9de3c1.png)

# プロフィール表示名変更
- ダッシュボードにアクセスします。
- `ユーザー`タブの`プロフィール`リンクを押下します。
    <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/437c9027-3264-41eb-926a-40b3f7e3ba84.png)
- `ニックネーム`および、`ブログ上の表示名`を任意の名前に変更します。
    <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/922c3dce-6cc4-485e-8815-0fd83944c86b.png)
- `プロフィールを更新`ボタンを押下します。
    <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/ecc92a18-6e63-4415-98b7-81da9af898c2.png)
- 画面上部のユーザー名が、`ブログ上の表示名`になっていることを確認します。
    <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/0fb0d386-76f4-4730-a666-21c040a588ee.png)

# おわりに

今回はConoHa VPS上のUbuntu 24.04へWordPressをインストールし、初期設定まで実施しました。

ここまで完了すると、WordPressの管理画面へログインできるようになり、記事の投稿やテーマの変更などを行えるようになります。

次回は、WordPressを運用するうえで実施しておきたい初期設定やセキュリティ設定についてまとめる予定です。

同じ環境でWordPressを構築する際の参考になれば幸いです。

# 関連資料
私が公開しているWordPress構築手順をまとめたページを作成しています。
もしよければ、閲覧いただけると嬉しいです。


https://qiita.com/aaruupaka/items/ed1fa439da66510d38b9


同じ環境を構築する際の参考になれば幸いです。
