---
title: ConoHa VPSで構築したUbuntuにMariaDBをインストールする手順【備忘録】【Ubuntu24.04】
tags:
  - mariaDB
  - ConohaVPS
  - Ubuntu
  - Ubuntu24.04
  - MariaDB10.11
private: true
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: true
---
# 実行環境
- 利用サービス:`ConohaVPS`
- ディストリビューション:`Ubuntu`
- バージョン: `24.04`
- アーキテクチャ: `x86_64`
- メモリ: `2GB`
- CPU: `3Core`
- SSD: `100GB`

# MariaDBのインストール手順
- MariaDBをインストールする。
    - 実行コマンド
        ```bash
        sudo apt install mariadb-server -y
        ```
    - 実行結果
        ![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/80512f43-6efb-4c86-b877-4d584b139a3e.png)

- MariaDBのセキュリティ初期設定を行う
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
- ログイン確認を行う
    - 実行コマンド
        ```bash
        sudo mysql
        ```
    - 実行結果
        ![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/307bdb83-36ee-4414-86f3-ad8ce4a99bc3.png)
- DBからログアウトする。
    - 実行コマンド
        ```sql
        /q
        ```
    - 実行結果
        ![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/44dda5ab-f09c-4920-a649-fbab8deafffd.png)


