---
title: CakePHP Migrationsプラグインで指定可能なデータ型まとめ【Migrations 5.2.6】
tags:
  - CakePHP
  - Cakephp5
  - Migrations
  - CakePHP-Migrations-Plugin
  - PHP
private: true
updated_at: '2026-09-29T20:27:32+09:00'
id: d5f9759d623f8c6588dc
organization_url_name: null
slide: false
ignorePublish: false
posting_campaign_uuid: null
agreed_posting_campaign_term: false
---
## はじめに

CakePHPのMigrationsプラグインでは、マイグレーションファイルで`string`や`integer`などのデータ型を指定して、テーブルのカラムを定義できます。

例えば、MariaDBでは`string`を指定した場合、データベース上では`VARCHAR`型のカラムが作成されます。

本記事では、CakePHP Migrations 5.2.6の公式リファレンスをもとに、Migrationsプラグインで指定可能なデータ型を日本語で確認しやすいようにまとめます。

また、MySQL、PostgreSQLなど、データベース固有で指定可能なデータ型についてもあわせて記載します。

なお、本記事の内容は公式リファレンスをもとに整理したものであり、記載しているすべてのデータ型について、実際にマイグレーションを実行して動作確認を行ったものではありません。

# バージョン
- CakePHP: `5.4.2`
- Migrations: `5.2.6`

# CakePHP Migrationsプラグインで指定可能なデータ型

## 指定可能な基本データ型

2026年9月現在、指定可能なデータ型の一覧はこちらです。

- binary
- boolean
- char
- date
- datetime
- decimal
- float
- double
- smallinteger
- integer
- biginteger
- string
  - MariaDBでは`VARCHAR`が設定されます。
- text
- time
- timestamp
- uuid
  - MariaDBでは`CHAR(36)`が設定されます。
- binaryuuid
- nativeuuid
  - 多くのデータベースでは`uuid`のエイリアスです。
  - MariaDBではネイティブの`UUID`型が設定されます。

## MySQL

**MySQL**では、以下のデータ型も指定できます。

- enum
- set
- blob
- tinyblob
- mediumblob
- longblob
- bit
- json
  - MySQL 5.7以降で利用可能。

## PostgreSQL

**PostgreSQL 9.3**以降では、以下のデータ型も指定できます。

- interval
- json
- jsonb
- uuid
- cidr
- inet
- macaddr
- citext
  - 使用するには、データベースで`citext`拡張機能を有効にする必要があります。

# CakePHP Migrationsプラグインで指定可能なカラムオプション

2026年9月現在、すべてのデータ型で指定可能なカラムオプションの一覧はこちらです。

- limit
- length
  - `limit`のエイリアスです。
- default
- null
  - `NULL`を許可するか指定します。デフォルトは`true`です。
- after
  - 新しいカラムをどのカラムの後ろに追加するか指定します。
  - MySQLでのみ利用可能です。
- comment

## decimalおよびfloat

**decimal**および**float**では、以下のカラムオプションも指定できます。

- precision
  - 桁数の合計。
- scale
  - 小数点以下の桁数。
- signed
  - `unsigned`オプションを有効または無効にします。
  - MySQLでのみ利用可能。

## enumおよびset

**enum**および**set**では、以下のカラムオプションも指定できます。

- values
  - カンマ区切りのリストまたは値の配列。

## smallinteger、integerおよびbiginteger

**smallinteger**、**integer**および**biginteger**では、以下のカラムオプションも指定できます。

- identity
  - 自動インクリメントを有効または無効にします。
- signed
  - `unsigned`オプションを有効または無効にします。
  - MySQLでのみ利用可能。

## その他

`date`、`time`、`datetime`、`timestamp`では、使用するDBアダプターに応じて`default`、`timezone`、`update`オプションを指定できます。

また、MySQLでは`string`、`text`に`collation`、`encoding`オプションを指定できます。

# 公式リファレンス
[CakePHP book - Migrations](https://book.cakephp.org/migrations/5/)

[CakePHP book - Migrations 指定可能なデータ型](https://book.cakephp.org/migrations/5/guides/writing-migrations/columns-and-table-operations.html#adding-columns)
