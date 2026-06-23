---
title: >-
  ConoHa
  VPSで構築したUbuntuにApacheをインストールした際、「IPアドレスからの応答時間が長すぎます」と表示され、アクセスできなかった話【備忘録】【Ubuntu24.04】【Apache2】
tags:
  - Apache
  - apache2
  - ufw
  - ConohaVPS
  - Ubuntu24.04
private: false
updated_at: '2026-06-22T20:23:35+09:00'
id: 60ddf031b8a7c9f52655
organization_url_name: null
slide: false
ignorePublish: false
---
# はじめに

ConoHa VPSでUbuntu 24.04の環境を用意し、Apacheをインストールした際、ブラウザからIPアドレスへアクセスしても「IPアドレスからの応答時間が長すぎます」と表示され、Apacheのデフォルトページが表示されませんでした。

最初はApacheの起動状態やUbuntu側のファイアウォール設定を疑いましたが、最終的にはConoHa VPS側のセキュリティグループ設定も原因になっていました。

この記事では、同じような状態になった際に確認したことと、実際に解決するまでの流れを備忘録として残します。

# 実行環境
- 利用サービス:`ConohaVPS`
- ディストリビューション:`Ubuntu`
- バージョン: `24.04`
- アーキテクチャ: `x86_64`
- メモリ: `2GB`
- CPU: `3Core`
- SSD: `100GB`

# 発生した事象
## トラブルシューティング:IPアドレスからの応答時間が長すぎます。と出たケース
- 初回URLアクセス時、下記のような表示となってしまいました。<br>解決するために対応したことを記載します。
    <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/13f82e2f-a44f-488d-bdeb-e1550789e1f8.png)

# 原因調査委
- URLアクセスできない理由を特定する。
    ## サーバー内でApacheにアクセスできるか確認
    - サーバー内でApacheにアクセスできるか確認
        - 実行コマンド
            ```bash
            curl http://localhost
            ```
        - 実行結果
            <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/b5de5856-eda6-4902-a738-690f79ccceaf.png)
        - 確認事項
            - HTMLが出力されることを確認します。
            - HTMLが出力されている場合、Apache自体は問題なく動いていると判断できます。

    ## 80番ポートが使用されているかを確認
    - 80番ポートが使用されているかを確認
        - 実行コマンド
            ```bash
            sudo ss -tulpn | grep ':80'
            ```
        - 実行結果
            <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/d27856ee-70d0-4de3-abb1-9266ef15b316.png)
        - 確認事項
            - `LISTEN 0 511 *:80`といったような出力がされれば問題ありません。
            - 80番ポートで待ち受けできていると判断できます。
    
    ##  UFW（外部通信）の設定を確認
    - UFW（外部通信）で通信を遮断していないか確認
        - 実行コマンド
            ```bash
            sudo ufw status
            ```
        - 実行結果
            <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/efac620d-a14f-46ae-93f7-0e746f213b67.png)
        - 確認事項
            - 通信の許可リストにApacheがあることを確認します。
            - 今回、ufwのリスト内にApacheの記載がなかったため、Ubuntu側のファイアウォールで外部からのアクセスが遮断されている可能性があると判断しました。

# 対応1: UFWでApacheへのアクセスを許可
- ufwでApacheのHTTP/HTTPS通信を許可する。
    - 実行コマンド
        ```bash
        sudo ufw allow 'Apache Full'
        ```
    - 実行結果
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/452f3515-e50d-46c3-9049-e608e79742d0.png)

- ufwで80番ポート（apache）へのアクセスが許可されているか確認する。
    - 実行コマンド
        ```bash
        sudo ufw status
        ```
    - 実行結果
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/f2575ea1-9034-4d25-8917-fd6ccd3b97a6.png)
    - 確認事項
        - 通信の許可リストにApache(Apache Full)があることを確認します。

- 再度、URLアクセス
    - URLアクセス
        ```URL
        http://IPアドレス
        ```
    - 実行結果
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/13f82e2f-a44f-488d-bdeb-e1550789e1f8.png)
    - 確認事項
        - HTMLが出力されることを確認します。
        - ...あれ？まだ解決してませんね.... ConohaVPS側の設定かな...?

# 対応2: ConoHa VPSのセキュリティグループを変更
- ConohaVPSで外部接続を遮断していないか確認する。
    - ConohaVPSの管理画面にログインし、サーバーリスト画面にアクセスします。
        - ここで少し驚いたのですが、サーバーリストへのアクセス時、下記のようなポップアップが出ました。セキュリティグループが`default`の場合、外部からの通信はすべて遮断しているらしいです。今回アクセスできなかった原因②であると判断できました。
            <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/bb9922c9-5193-436e-90e2-02bc5ea5a954.png)
    - サーバーリストから、現在使っているサーバーを探し、詳細画面を開き、セキュリティグループが`default`になっていることを確認します。
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/abda7276-609f-49c0-8165-431600daf6e2.png)
    - セキュリティグループの鉛筆アイコンをクリックします。
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/ccec3701-5527-4bc5-986d-0a5e5c749df5.png)
    - セキュリティグループを`default`から`IPv4v6-Web`に変更し`保存`ボタンをクリックします。
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/8b71e8d5-ef04-4a23-b9f3-f3c78a749560.png)
    - セキュリティグループが`IPv4v6-Web`に変更されていることを確認します。
        <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/9b1ae5e9-2cce-4047-997e-e42a2a70d898.png)

# 解決確認
- 再度、URLアクセス
    - URLアクセス
        ```URL
        http://IPアドレス
        ```
    - 実行結果
      <br>![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/ba527b32-82f7-4877-8ecd-c2d44fbc0162.png)
    - 確認事項
        - Apache2 Default Page が出力されることを確認します。

# おわりに

今回のケースでは、Apache自体はサーバー内で正常に動作していましたが、Ubuntu側のUFW設定とConoHa VPS側のセキュリティグループ設定により、外部からアクセスできない状態になっていました。

ブラウザからアクセスできない場合、Apacheの設定だけを確認してしまいがちですが、以下のように順番に切り分けると原因を見つけやすいと感じました。

* サーバー内でApacheにアクセスできるか確認する
* 80番ポートで待ち受けできているか確認する
* Ubuntu側のUFW設定を確認する
* VPS側のセキュリティグループ設定を確認する

同じように「応答時間が長すぎます」と表示されてアクセスできない場合は、Ubuntu側だけでなく、ConoHa VPS側のセキュリティグループも確認すると良さそうです。

# 関連資料。
私が公開しているWordPress構築手順をまとめたページを作成しています。
もしよければ、閲覧いただけると嬉しいです。

https://qiita.com/aaruupaka/items/ed1fa439da66510d38b9

同じ環境を構築する際の参考になれば幸いです。