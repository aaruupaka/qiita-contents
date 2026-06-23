---
title: ConoHa VPSで構築したUbuntuの初期設定手順【備忘録】【Ubuntu24.04】
tags:
  - Ubuntu
  - vps
  - 備忘録
  - ConohaVPS
  - Ubuntu24.04
private: false
updated_at: '2026-06-12T08:59:06+09:00'
id: 805405d2a7ae514ee618
organization_url_name: null
slide: false
ignorePublish: false
---
# はじめに

本記事では、ConoHa VPSで構築したUbuntu 24.04に対して初期設定を行います。

今回は以下を実施します。

- OSアップデート
- Linuxの再起動
- タイムゾーン確認

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

# OSアップデート
- OSのアップデート

  Ubuntuの初期状態では、
  セキュリティ更新や不具合修正が適用されていない場合があります。

  そのため、最初にOSアップデートを実施します。
  - 実行コマンド
    ```bash
    sudo apt update && sudo apt upgrade -y
    ```
  - 実行結果
    <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/f3530104-cebd-46dc-9fb6-739f42cb23ad.png)

- Linuxの再起動

  アップデート内容によっては、
  Linuxカーネルの更新が含まれる場合があります。

  そのため、OSアップデート後は再起動を実施します。
    - 実行コマンド
      ```bash
      sudo reboot
      ```
    - 実行結果
      <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/878410cd-e705-42ee-a71e-b6c87e7768bf.png)

- タイムゾーンがJSTになっているか確認する。
    - 確認用のコマンドを実行する。
        - 実行コマンド
        ```bash
        timedatectl
        ```
        - 実行結果
          <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/f06cbe3f-5c75-4070-95af-68fa0b4c31fa.png)
        - 確認内容
          - `Time zone`の内容が`Asia/Tokyo (JST, +0900)`になっていれば問題ありません。
          - もし、Asia/Tokyo (JST, +0900)`でない場合は下記のコマンドを実行し、再度`timedatectl`を実行し確認すれば大丈夫です。
            ```bash
            sudo timedatectl set-timezone Asia/Tokyo
            ```

# 関連資料。
私が公開しているWordPress構築手順をまとめたページを作成しています。
もしよければ、閲覧いただけると嬉しいです。

https://qiita.com/aaruupaka/items/ed1fa439da66510d38b9

同じ環境を構築する際の参考になれば幸いです。