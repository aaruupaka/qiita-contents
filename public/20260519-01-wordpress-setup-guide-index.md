---
title: ConoHa VPSでWordPressを構築するまでの手順まとめ【備忘録】
tags:
  - WordPress
  - vps
  - 備忘録
  - ConohaVPS
private: false
updated_at: '2026-07-04T17:20:27+09:00'
id: ed1fa439da66510d38b9
organization_url_name: null
slide: false
ignorePublish: false
posting_campaign_uuid: 783b7a849caf11eefd91
agreed_posting_campaign_term: true
---
# はじめに

ConoHa VPS上にWordPress環境を構築した際の手順をまとめるための記事です。

本記事では、ConoHa VPSの契約から、Ubuntu環境の初期設定、Apache / PHP / MariaDBの導入、WordPressの配置、最低限のセキュリティ設定までの流れを整理します。

各作業の詳細は個別記事として作成し、本記事からリンクする予定です。

# 前提

本記事は、以下の環境で作業した際の記録です。

- VPS：ConoHa VPS
- OS：Ubuntu 24.04 LTS
- Webサーバー：Apache 2.4系
- PHP：PHP 8.3系
- DB：MariaDB 10.11系
- CMS：WordPress

2026年4月から6月に作業した際の内容です。
料金、画面表示、各種バージョンは 
今後変更される可能性があります。

# 全体の流れ

大まかな作業の流れは下記のとおりです。

1. ConoHa VPSのアカウント作成・契約
2. 契約するVPSのスペック検討
3. VPSへの初回ログイン
4. Ubuntuの初期設定
5. Apacheのインストールと外部公開確認
6. PHPのインストール
7. MariaDBのインストール
8. WordPressのインストール
  - WordPress用DB・ユーザー作成
  - WordPress本体の配置
  - WordPress初期設定
9. 最低限のセキュリティ設定

# 記事一覧

## 1. ConoHa VPSの契約関連

### ConoHa VPSのアカウント作成〜契約完了まで

ConoHa VPSのアカウント作成から、VPS契約完了までの手順をまとめた記事です。

- 記事リンク：

https://qiita.com/aaruupaka/items/ad29b1589f55a521942f


### 契約サーバーのスペック検討

WordPressブログや今後のポートフォリオ設置を想定し、メモリ1GB / 2GB / 4GBのどれを選ぶか検討した記録です。

- 記事リンク：

https://qiita.com/aaruupaka/items/49c08d393091ce7b82fe

## 2. VPS初期設定

### VPSへの初回ログイン

ConoHa VPSへ初回ログインし、作業を開始するまでの記録です。

- 記事リンク：

https://qiita.com/aaruupaka/items/a81b54d400b74a89f9de

### Ubuntuの初期設定

Ubuntuのアップデート、タイムゾーン設定など、最初に行った設定をまとめる予定です。

- 記事リンク：

https://qiita.com/aaruupaka/items/805405d2a7ae514ee618

## 3. Apache / PHP / MariaDBの導入

### Apacheのインストール

Apacheをインストールした際の記録です。

- 記事リンク：

https://qiita.com/aaruupaka/items/928bfd422cd85d1fafae

### Apacheの外部公開確認

Apacheをインストールした際、ブラウザからIPアドレスへアクセスしても「IPアドレスからの応答時間が長すぎます」と表示され、Apacheのデフォルトページが表示されませんでした。
その際に対処した内容の記録です。

- 記事リンク：

https://qiita.com/aaruupaka/items/60ddf031b8a7c9f52655

### PHPのインストール

WordPressで利用するPHPと、Apache連携用モジュールなどを導入した記録です。

- 記事リンク：

https://qiita.com/aaruupaka/items/1a4ee975af3339843b4a

### MariaDBのインストール

MariaDBをインストールし、初期設定を行った記録です。

- 記事リンク：

https://qiita.com/aaruupaka/items/7b8976fd3bff4fde8f4f

## 4. WordPress構築

### WordPressのインストール

WordPressのインストールを行います。
また下記の内容も実施します。
  - WordPress用DB・ユーザー作成
  - WordPress本体の配置
  - WordPress初期設定

- 記事リンク：

https://qiita.com/aaruupaka/items/20c390cb93d80d6cc06c

## 5. セキュリティ・運用設定

### WPS Hide Loginの導入

WordPressのログインURLを変更するため、WPS Hide Loginを導入した記録です。  
また、Apacheの `mod_rewrite` や `AllowOverride` 設定で詰まった内容も記録する予定です。

- 記事リンク：

https://qiita.com/aaruupaka/items/1976bfaa6485dc5f871b

### Linuxカーネル脆弱性通知への対応

ConoHa VPSから届いたLinuxカーネル脆弱性通知を受け、Ubuntuのアップデート確認を行った記録です。

- 記事リンク：作成予定

# 今後追加予定

今後、以下の記事も追加する予定です。

- 独自ドメイン設定
- HTTPS化
- WordPressテーマ作成
- バックアップ設定
- 不要テーマ・不要プラグイン整理
- PHP拡張機能の追加
- サイトヘルス改善

# おわりに

ConoHa VPS上にWordPressを構築する作業は、レンタルサーバーの簡単インストールと比べると手順が多くなります。

一方で、Apache、PHP、MariaDB、Linuxの権限設定など、Webアプリケーションを動かすための基本的な仕組みを学べる良い機会になりました。

本記事が、ConoHa VPSでWordPressを構築しようとしている方の参考になれば幸いです。
