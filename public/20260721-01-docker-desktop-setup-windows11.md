---
title: 20260721-01-docker-desktop-setup-windows11
tags:
  - ''
private: true
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: true
posting_campaign_uuid: null
agreed_posting_campaign_term: false
---
# 環境情報
- OS: `Windows 11`
- WSL: WSL2
- WSL2 Linuxディストリビューション: Ubuntu

# 前提条件
- WSL2がインストールされていること
- WSL2でubuntuがインストールされていること

::: note info
WSL2で利用するディストリビューションはUbuntuである必要はないと思いますが、私の環境はUbuntuであるため、指定しています。
任意のディストリビューションで問題ありません。
:::

# WSLの状態確認
- Windows Terminal（PowerShell）を起動します。

- WSLのステータスを確認します。
  - 実行コマンド
    ```bash
    wsl --status
    ```
  - 実行結果例
    ```bash
    既定のディストリビューション: Ubuntu
    既定のバージョン: 2
    WSL1 は、現在のマシン構成ではサポートされていません。
    WSL1 を使用するには、"Linux 用 Windows サブシステム" オプション コンポーネントを有効にしてください。
    ```
  - 確認事項
    - WSL2が使用可能な状態であること。

- インストール済みのLinuxの状態を確認します。
  - 実行コマンド
    ```bash
    wsl -l -v
    ```
  - 実行結果例
    ```bash
      NAME      STATE           VERSION
    * Ubuntu    Stopped         2
    ```
  - 確認事項
    - `Ubuntu`がインストールされていること

## WSLの更新
- WSLの更新をします。
  - 実行コマンド
    ```bash
    wsl --update
    ```
  - 実行結果例
    ```bash
    更新プログラムを確認しています。
    Linux 用 Windows サブシステムの最新バージョンは既にインストールされています。
    ```
- WSLのバージョンを確認します。
  - 実行コマンド
    ```bash
    WSL バージョン: 2.7.10.0
    カーネル バージョン: 6.18.33.2-2
    WSLg バージョン: 1.0.73.2
    MSRDC バージョン: 1.2.6676
    Direct3D バージョン: 1.611.1-81528511
    DXCore バージョン: 10.0.26100.1-240331-1435.ge-release
    Windows バージョン: 10.0.26200.8894
    ```

