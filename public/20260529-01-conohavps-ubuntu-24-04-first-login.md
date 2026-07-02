---
title: ConoHa VPSで構築したUbuntuへの初回ログイン【備忘録】【Ubuntu24.04】
tags:
  - Ubuntu
  - vps
  - 備忘録
  - ConohaVPS
  - Ubuntu24.04
private: false
updated_at: '2026-07-02T20:42:11+09:00'
id: a81b54d400b74a89f9de
organization_url_name: null
slide: false
ignorePublish: false
posting_campaign_uuid: null
agreed_posting_campaign_term: false
---
# はじめに
本記事では、ConoHaVPSで作成したUbuntuへの初回ログインを行います。

今回はConoHa VPSのコンソール機能を利用してログインします。

SSHクライアント（Tera Term等）から接続することも可能ですが、
初回は接続設定が不要なコンソールを利用すると簡単です。

# 実行環境
- 利用サービス:`ConoHa VPS`
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
  ![20260520-01-01-conohavps-adm.png](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260520-01-conohavps-ubuntu-24-04-first-login-and-initial-setup/images/20260520-01-01-conohavps-adm.png)

- 契約したサーバーの`コンソール`リンクを押下します。
  ![20260520-01-02-conohavps-console-link.png](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260520-01-conohavps-ubuntu-24-04-first-login-and-initial-setup/images/20260520-01-02-conohavps-console-link.png)

- コンソールが開くことを確認します。
  ![](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260520-01-conohavps-ubuntu-24-04-first-login-and-initial-setup/images/20260520-01-03.png)

- `login: `では、`root`と入力し、`Enter`を押下します。
  - `root`はConoHa VPSでの契約時にパスワードを設定したアカウントです。
  ![](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260520-01-conohavps-ubuntu-24-04-first-login-and-initial-setup/images/20260520-01-04.png)

- `Password: `では、契約時に設定したrootアカウントのパスワードを入力し、`Enter`を押下します。
  ![](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260520-01-conohavps-ubuntu-24-04-first-login-and-initial-setup/images/20260520-01-05.png)

- ログインできたことを確認します。
  - ログイン後出力内容
    ![alt text](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260529-01-conohavps-ubuntu-24-04-first-login/images/20260529-01-01.png)
    - `root@sv-xxxxx:~#`のような表示が出ていれば成功です。

# 関連資料。
私が公開しているWordPress構築手順をまとめたページを作成しています。
もしよければ、閲覧いただけると嬉しいです。

https://qiita.com/aaruupaka/items/ed1fa439da66510d38b9

同じ環境を構築する際の参考になれば幸いです。
