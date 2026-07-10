---
title: Local WPでWordPress開発環境を構築する手順【Windows 11】
tags:
  - LocalWP
  - WordPress
  - WordPressテーマ
  - 開発環境構築
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
# はじめに
先日、ConoHa VPS上でWordPressを構築しました。

WordPressテーマに関して、公開されているテーマを使うことも考えましたが、
今回は自作してみようと思い至りました。

本番環境でテーマの開発を行うのはさすがに危険であるため、開発環境を準備します。

今回は最も簡単にWordPressの開発環境を構築できると思われる
`Local WP`を使用します。

他の方のお役に立てましたら幸いです。

# 関連資料
ConoHa VPSでWordPressを構築するまでにいくつか記事を作成しました。
リンク集を作成したので、もしよければ閲覧いただけると嬉しいです。

https://qiita.com/aaruupaka/items/ed1fa439da66510d38b9

# 環境情報
- OS:Windows 11

# localWPのダウンロード

## 公式サイトにアクセス
- 下記URLにアクセスします。
    - URL : `https://localwp.com/`
        <br>![alt text](../articles/20260603-01-windows-11-download-localwp/images/20260603-01-02.png)

## localWPダウンロード
- `DOWNLOAD FOR FREE`ボタンを押下します。
    <br>![alt text](../articles/20260603-01-windows-11-download-localwp/images/20260603-01-01.png)

- 各項目を入力し、`GET IT NOW!`ボタンを押下します。
    <br>![alt text](../articles/20260603-01-windows-11-download-localwp/images/20260603-01-03.png)

- ダウンロードが完了するのを待機します。
    <br>![alt text](../articles/20260603-01-windows-11-download-localwp/images/20260603-01-04.png)

- `local-10.1.0-windows.exe`がダウンロードされたことを確認します。

# localWPのインストール

## インストール
- `local-10.1.0-windows.exe`を起動します。

- `Local セットアップ`ウィンドウが展開されるのを確認します。
    <br>![alt text](../articles/20260603-02-windows-11-install-localwp/images/20260503-02-03.png)

- `インストールオプションの選択`画面で下記の内容を選択し`次へ(N)>`を押下する。
    <br>![alt text](../articles/20260603-02-windows-11-install-localwp/images/20260503-02-01.png) 

- `インストール先を選んでください。`画面で任意のインストール先フォルダを指定し、`インストール`ボタンを押下します。
    <br>![alt text](../articles/20260603-02-windows-11-install-localwp/images/20260503-02-02.png)

- `インストール`画面に遷移することを確認します。
    <br>![alt text](../articles/20260603-02-windows-11-install-localwp/images/20260503-02-04.png)

- `Localセットアップ ウィザードは完了しました。`画面が出たら`完了(F)`ボタンを押下します。
    <br>![alt text](../articles/20260603-02-windows-11-install-localwp/images/20260503-02-05.png)

- LocalWPが起動することを確認します。
    <br>![alt text](../articles/20260603-02-windows-11-install-localwp/images/20260503-02-06.png)

# Local WP 初回セットアップ

## 初回起動時
- LocalWPが起動します。
    <br>![alt text](../articles/20260603-03-local-wp-first-setup/images/20260503-03-01.png)

- `Terms of Service`の内容を確認し、チェックボックスを有効化、`I agree`ボタンを押下します。
    <br>![alt text](../articles/20260603-03-local-wp-first-setup/images/20260503-03-02.png)

- `Is it ok to enable error reports?`では、任意のボタンを押下します。
    - 私は`Turn on error reporting`を選択しました。
    - 仮に本番環境DBのコピー等、機密情報をlocalWP上で取り扱う予定がある場合は、`No, thanks`を選択するのが良いと思います。
    <br>![alt text](../articles/20260603-03-local-wp-first-setup/images/20260503-03-03.png)

- `IS it ok to enable usage reporting?`では、任意のボタンを押下します。
    - 私は`No, thanks`を選択しました。
    <br>![alt text](../articles/20260603-03-local-wp-first-setup/images/20260503-03-04.png)


- LocalWPの`Local sites`タブが表示されることを確認します。
    <br>![alt text](../articles/20260603-03-local-wp-first-setup/images/20260503-03-05.png)


## テーマ作成用のローカルWPを作成する。
- `+ Create a new site`ボタンを押下します。
    <br>![alt text](../articles/20260603-03-local-wp-first-setup/images/20260503-03-06.png)

- `Create a site`画面で`Create a new site`を選択した状態で、`Contine`ボタンを押下します。
    <br>![alt text](../articles/20260603-03-local-wp-first-setup/images/20260503-03-07.png)

- `What's your site's name?`画面では、任意のサイト名を入力し、`Continue`ボタンを押下します。
    <br>![alt text](../articles/20260603-03-local-wp-first-setup/images/20260503-03-08.png)

- `Choose your environment`画面では、`Custom`を選択後、自身の環境に最も近しい内容を選択し、`Continue`ボタンを押下します。
    <br>![alt text](../articles/20260603-03-local-wp-first-setup/images/20260503-03-09.png)

- `Set up WordPress`画面では、任意の内容を入力し、`Add Site`ボタンを押下します。
    - 私は下記の設定を行いました。
        - WordPress username
            - localwp
        - WordPress password
            - password
        - WordPress e-mail
            - dev-email@wpengine.local
                - デフォルト値
    <br>![alt text](../articles/20260603-03-local-wp-first-setup/images/20260503-03-10.png)

- UATが表示された場合は、適宜許可します。

- 環境構築が完了したことを確認します。
    <br>![alt text](../articles/20260603-03-local-wp-first-setup/images/20260503-03-11.png)

- LocalWPの`Local sites`タブ内の`WP Admin`ボタンを押下し、WordPressのログイン画面に遷移することを確認します。
    <br>![alt text](../articles/20260603-03-local-wp-first-setup/images/20260503-03-12.png)

- `Set up WordPress`画面で設定したアカウント情報を入力し。`Log in`ボタンを押下します。
    <br>![alt text](../articles/20260603-03-local-wp-first-setup/images/20260503-03-13.png)

- ダッシュボードに遷移することを確認します。
    <br>![alt text](../articles/20260603-03-local-wp-first-setup/images/20260503-03-14.png)

- LocalWPの`Local sites`タブ内の`Open Site`ボタンを押下し、WordPresサイトのトップ画面に遷移することを確認します。
    <br>![alt text](../articles/20260603-03-local-wp-first-setup/images/20260503-03-15.png)