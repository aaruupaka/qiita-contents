---
title: ConoHa VPSで構築したUbuntuにMariaDBをインストールする手順【備忘録】【Ubuntu24.04】
tags:
  - Ubuntu
  - mariadb
  - ConohaVPS
  - Ubuntu24.04
  - MariaDB10.11
private: false
updated_at: '2026-07-02T20:42:11+09:00'
id: 7b8976fd3bff4fde8f4f
organization_url_name: null
slide: false
ignorePublish: false
posting_campaign_uuid: null
agreed_posting_campaign_term: false
---
## はじめに

前回の記事では、ConoHa VPS上に構築したUbuntu 24.04へPHPをインストールしました。

今回は、WordPressのデータ保存先として利用するMariaDBをインストールし、初期設定を行います。

MariaDBはMySQL互換のデータベースであり、WordPressでも広く利用されています。

本記事では、MariaDBのインストールからセキュリティ設定、ログイン確認までの手順を備忘録としてまとめます。

# 実行環境
- 利用サービス:`ConohaVPS`
- ディストリビューション:`Ubuntu`
- バージョン: `24.04`
- アーキテクチャ: `x86_64`
- メモリ: `2GB`
- CPU: `3Core`
- SSD: `100GB`

# MariaDBのインストール手順
- MariaDBをインストールします。
    - 実行コマンド
        ```bash
        sudo apt install mariadb-server -y
        ```
    - 実行結果
        ![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/80512f43-6efb-4c86-b877-4d584b139a3e.png)

- MariaDBのセキュリティ初期設定を行います。
    - 実行コマンド
        ```bash
        sudo mysql_secure_installation
        ```
    - 選択内容
        - Enter current password for root (enter for none):
            - `Enter`を押下
        - Switch to unix_socket authentication?
            - `Y`を入力し、`Enter`を押下
        - Change the root password?
            - `n`を入力し、`Enter`を押下
        - Remove anonymous users?
            - `Y`を入力し、`Enter`を押下
        - Disallow root login remotely?
            - `Y`を入力し、`Enter`を押下
        - Remove test database?
            - `Y`を入力し、`Enter`を押下
        - Reload privilege tables?
            - `Y`を入力し、`Enter`を押下

- ログイン確認を行います。
    - 実行コマンド
        ```bash
        sudo mysql
        ```
    - 実行結果
        ![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/307bdb83-36ee-4414-86f3-ad8ce4a99bc3.png)

- DBからログアウトします。
    - 実行コマンド
        ```sql
        exit
        ```
    - 実行結果
        ![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/44dda5ab-f09c-4920-a649-fbab8deafffd.png)

- バージョン確認を行います。
    - 実行コマンド
        ```bash
        mariadb --version
        ```
    - 実行結果
        ```
        mariadb  Ver 15.1 Distrib 10.11.14-MariaDB, for debian-linux-gnu (x86_64) using  EditLine wrapper
        ```
    - 確認事項
        - バージョン情報が出力されることを確認します。

## おわりに

今回は、ConoHa VPS上のUbuntu 24.04へMariaDBをインストールし、基本的なセキュリティ設定とログイン確認を行いました。

MariaDBの導入が完了したことで、WordPressを動作させるためのデータベース環境が整いました。

次回は、WordPressで利用するデータベースとユーザーの作成手順をまとめる予定です。

また、WordPress構築手順をまとめた記事も公開していますので、あわせてご覧いただけると幸いです。


# 関連資料
私が公開しているWordPress構築手順をまとめたページを作成しています。
もしよければ、閲覧いただけると嬉しいです。

https://qiita.com/aaruupaka/items/ed1fa439da66510d38b9

同じ環境を構築する際の参考になれば幸いです。
