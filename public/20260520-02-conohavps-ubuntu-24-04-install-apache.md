---
title: ConoHa VPSのUbuntu 24.04にApache2をインストールする手順【備忘録】
tags:
  - Apache
  - Ubuntu
  - apache2
  - ConohaVPS
  - Ubuntu24.04
private: false
updated_at: '2026-06-22T20:30:47+09:00'
id: 928bfd422cd85d1fafae
organization_url_name: null
slide: false
ignorePublish: false
---
# はじめに
ConoHa VPS上に構築したUbuntu 24.04環境へ、WebサーバーであるApache2をインストールした際の手順を備忘録としてまとめました。

本記事では、Apache2のインストールから動作確認までを実施します。

# 実行環境
- 利用サービス:`ConohaVPS`
- ディストリビューション:`Ubuntu`
- バージョン: `24.04`
- アーキテクチャ: `x86_64`
- メモリ: `2GB`
- CPU: `3Core`
- SSD: `100GB`

# 前提条件
- ConohaVPSでサーバーの契約が完了していること
- OSはUbuntu24.04を選択していること
- rootアカウントでログインした状態であること
- Ubuntuの初期設定が完了していること

# Webサーバー（Apache）のインストール
1. パッケージ情報の更新
    - 実行コマンド
        ```bash
        sudo apt update
        ```
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
    - 確認事項
        - Active: active (running) と表示されていることを確認します。

1. Apacheのデフォルトページ表示確認
    - URLアクセス
        ```URL
        http://IPアドレス
        ```
    - 実行結果
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/ba527b32-82f7-4877-8ecd-c2d44fbc0162.png)
    - 確認事項
        - Apache2 Default Page が出力されることを確認します。
    - 備考
        - アクセスできない場合は、ファイアウォールやConoHa VPSのセキュリティグループ設定を確認してください。
        - 初回アクセス時、「IPアドレスからの応答時間が長すぎます」と表示され、アクセスすることができませんでした。
            - その際の対処法は下記にまとめています。


https://qiita.com/aaruupaka/items/60ddf031b8a7c9f52655


# おわりに
今回は、Apacheのインストールを行いました。
特にトラブルが起きなければやること自体はシンプルだと思います。
次回はPHPのインストールを行おうと思います。
