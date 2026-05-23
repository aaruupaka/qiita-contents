---
title: ConoHa VPSで構築したUbuntuへの初回ログインと初期設定手順【備忘録】【Ubuntu24.04】
tags:
  - ConohaVPS
  - VPS
  - Ubuntu
  - Ubuntu24.04
  - 備忘録
private: true
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
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

# 初回ログイン
- ConoHa VPSの管理画面にログインします。
  ![20260520-01-01-conohavps-adm.png](../articles/20260520-01-conohavps-ubuntu-24-04-first-login-and-initial-setup/images/20260520-01-01-conohavps-adm.png)
- 契約したサーバーの`コンソール`リンクを押下します。
  ![20260520-01-02-conohavps-console-link.png](../articles/20260520-01-conohavps-ubuntu-24-04-first-login-and-initial-setup/images/20260520-01-02-conohavps-console-link.png)
- コンソールが開くことを確認します。
  ![](../articles/20260520-01-conohavps-ubuntu-24-04-first-login-and-initial-setup/images/20260520-01-03.png)
- `login: `では、`root`と入力し、`Enter`を押下します。
  ![](../articles/20260520-01-conohavps-ubuntu-24-04-first-login-and-initial-setup/images/20260520-01-04.png)
- `Password: `では、契約時に設定したrootアカウントのパスワードを入力し、`Enter`を押下します。
  ![](../articles/20260520-01-conohavps-ubuntu-24-04-first-login-and-initial-setup/images/20260520-01-05.png)
- ログインできたことを確認します。
  - ログイン後出力内容
    ![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/25ef129e-9325-48d8-8848-93b05add0915.png)

# OSアップデート
1. OSのアップデート
    - 実行コマンド
      ```bash
      sudo apt update && sudo apt upgrade -y
      ```
    - 実行結果
      ![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/f3530104-cebd-46dc-9fb6-739f42cb23ad.png)

1. Linuxの再起動
    - 実行コマンド
      ```bash
      sudo reboot
      ```
    - 実行結果
      ```bash
      ```
    ![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/878410cd-e705-42ee-a71e-b6c87e7768bf.png)

1. タイムゾーンがJSTになっているか確認する。
    - 確認用のコマンドを実行する。
        - 実行コマンド
        ```
        timedatectl
        ```
        - 実行結果
        ![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/f06cbe3f-5c75-4070-95af-68fa0b4c31fa.png)
        - 確認内容
          - `Time zone`の内容が`Asia/Tokyo (JST, +0900)`になっていれば問題ありません。
          - もし、Asia/Tokyo (JST, +0900)`でない場合は下記のコマンドを実行し、再度`timedatectl`を実行し確認すれば大丈夫です。
          ```
          sudo timedatectl set-timezone Asia/Tokyo
          ```
