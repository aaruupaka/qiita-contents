---
title: ConoHa VPSで構築したUbuntuにApacheをインストールする手順【備忘録】【Ubuntu24.04】【Apache2】
tags:
  - ConohaVPS
  - Ubuntu
  - Ubuntu24.04
  - Apache
  - Apache2
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

# Webサーバー（Apache）のインストール
1. Apacheのインストール
    - 実行コマンド
        ```bash
        sudo apt install apache2 -y
        ```
    - 実行結果
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/e36c74d4-bb51-417b-9b74-3cfe5bab37fa.png)


1. インストール後のステータスチェック
    - 実行コマンド
        ```bash
        sudo systemctl status apache2
        ```
    - 実行結果
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/c776e291-a6a9-4f22-a424-206766d10991.png)

1. アクセスチェック
    - URLアクセス
        ```URL
        http://IPアドレス
        ```
    - 実行結果
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/ba527b32-82f7-4877-8ecd-c2d44fbc0162.png)
    - 確認事項
        - Apache2 Default Page が出力されることを確認します。