---
title: Docker Desktopの導入手順【Windows11】【2026年7月】
tags:
  - Docker
  - DockerDesktop
  - Windows11
  - Ubuntu
  - WSL2
private: true
updated_at: '2026-08-01T17:22:43+09:00'
id: b78ef1d60902ce78412a
organization_url_name: null
slide: false
ignorePublish: false
posting_campaign_uuid: null
agreed_posting_campaign_term: false
---
# はじめに
本記事では、Windows11にWindows 11にDocker Desktopを導入した際の手順を記録しています。

Windows11に導入する予定の方のお役に立てましたら幸いです。

::: note info
2026年7月に対応した際の手順です。
:::

# 環境情報
- OS: `Windows 11`
- WSL: `WSL2`
- WSL2 Linuxディストリビューション: `Ubuntu`
- Docker Desktop バージョン: `v4.83.0`

# 前提条件
- Docker Desktopのシステム要件を満たしていること
  [Install Docker Desktop on Windows #System requirements - docker docs](https://docs.docker.com/desktop/setup/install/windows-install/#system-requirements)
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

::: note info
WSLの更新作業は、任意作業です。
必要に応じて実施してください。
:::

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
    wsl --version
    ```
  - 実行結果
    ```bash
    WSL バージョン: 2.7.10.0
    カーネル バージョン: 6.18.33.2-2
    WSLg バージョン: 1.0.73.2
    MSRDC バージョン: 1.2.6676
    Direct3D バージョン: 1.611.1-81528511
    DXCore バージョン: 10.0.26100.1-240331-1435.ge-release
    Windows バージョン: 10.0.26200.8894
    ```

## Ubuntuの更新

::: note info
Ubuntuの更新作業は、任意作業です。
必要に応じて実施してください。
:::

- Ubuntuを起動します。
  - 実行コマンド
    ```bash
    wsl
    ```
  - 実行結果例
    ```bash
    To run a command as administrator (user "root"), use "sudo <command>".
    See "man sudo_root" for details.

    test@testpc:/mnt/c/Users/test$
    ```

- Ubuntuの更新内容を取得します。
  - 実行コマンド
    ```bash
    sudo apt update
    ```
  - 実行結果例
    ```bash
    ...(一部省略)
    Fetched 35.8 MB in 8s (4516 kB/s)
    Reading package lists... Done
    Building dependency tree... Done
    Reading state information... Done
    238 packages can be upgraded. Run 'apt list --upgradable' to see them.
    ```

- Ubuntuの更新を行います。
  - 実行コマンド
    ```bash
    sudo apt upgrade
    ```
  - 実行結果例
    ```
    ...(一部省略)
    Setting up ubuntu-wsl (1.539.2) ...
    Processing triggers for ca-certificates (20260601~24.04.1) ...
    Updating certificates in /etc/ssl/certs...
    0 added, 0 removed; done.
    Running hooks in /etc/ca-certificates/update.d...
    done.
    ```

# Docker Desktopの導入手順

## Docker Desktopをダウンロード
- 下記のURL、Dockerのトップページにアクセスします。
  [Docker Desktop](https://www.docker.com/ja-jp/products/docker-desktop/)

- `Docker Desktopをダウンロードする`にカーソルを合わせたのち、自身の環境にあった選択肢を選択します。
  ![alt text](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260721-01-docker-desktop-setup-windows11/images/20260721-01-01.png)
  - 私は`Windows 版のダウンロード – AMD64`を選択しました。
  - OSおよびCPUにより、ダウンロードするものが異なります。
    - Windowsの場合、下記コマンドを実行することで、どちらをダウンロードすべきか確認できます。
      - 実行コマンド
        ```bash
        echo $env:PROCESSOR_ARCHITECTURE
        ```
      - 実行結果例
        ```bash
        AMD64
        ```

- `Docker Desktop Installer.exe`がダウンロードされたことを確認します。

## Docker Desktopのインストール
- `Docker Desktop Installer.exe`を起動します。

- `Configuration`画面で任意の項目を選択し`OK`を押下します。
  - 私は`Per-user installation(Recommended)`を選択しました。

    ::: note info
    本記事では、実際に使用したPer-user installationでの導入手順を記載しています。

    インストール方式による機能や権限の違いについては検証していないため、本記事では説明を省略します。
    利用目的に応じたインストール方式の選択については、Docker公式ドキュメントをご確認ください
    :::

    ![alt text](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260721-01-docker-desktop-setup-windows11/images/20260721-01-02.png)

- インストールが始まるので待機します。
  ![alt text](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260721-01-docker-desktop-setup-windows11/images/20260721-01-03.png)

- インストールが完了すると`Installation succeeded`と出るので`Close`を押下します。
  ![alt text](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260721-01-docker-desktop-setup-windows11/images/20260721-01-04.png)

- スタートメニューで`Docker Desktop`検索し、表示されることを確認します。
  ![alt text](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260721-01-docker-desktop-setup-windows11/images/20260721-01-05.png)

## Docker Desktopの初回起動時対応
- `Docker Desktop`を起動します。

- 規約等を確認して`Accept`を押下します。

  ::: note warn
  Docker Desktopは、個人利用・教育・非商用OSS・一定規模未満の小規模企業では無料で利用できます。
  
  一方、大規模組織での業務利用などでは有料サブスクリプションが必要になる場合があります。利用前に最新のライセンス条件を公式ページで確認してください。
  :::

  ![alt text](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260721-01-docker-desktop-setup-windows11/images/20260721-01-06.png)

- ログイン画面が出るのでログインか、アカウントの作成を行います。
  ![alt text](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260721-01-docker-desktop-setup-windows11/images/20260721-01-07.png)

  ::: note info
  ログインせずに利用する場合は、スキップして先に進みます。
  :::

- Docker Desktopが起動できたことを確認します。
  ![alt text](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260721-01-docker-desktop-setup-windows11/images/20260721-01-08.png)

# Dockerの動作確認

## Docker CLIの動作確認
- Windows Terminal(PowerShell)を起動します。

- Dockerのバージョンチェックコマンドを実行します。
  - 実行コマンド
    ```bash
    docker --version
    ```
  - 実行結果例
    ```bash
    Docker version 29.6.2, build dfc4efb
    ```
- Docker composeのバージョンチェックコマンドを実行します。
  - 実行コマンド
    ```bash
    docker compose version
    ```
  - 実行結果例
    ```bash
    Docker Compose version v5.3.1
    ```

## Dockerの動作確認
今回は、`hello-world`というイメージを使用し、実際にコンテナを起動してみます。
- `hello-world`を実行します。
  - 実行コマンド
    ```bash
    docker run hello-world
    ```
  - 実行結果例
    ```bash
    Unable to find image 'hello-world:latest' locally
    latest: Pulling from library/hello-world
    4f55086f7dd0: Pull complete
    d5e71e642bf5: Download complete
    Digest: sha256:c3cbe1cc1aa588a64951ac6286e0df7b27fe2e6324b1001c619bb358770c0178
    Status: Downloaded newer image for hello-world:latest

    Hello from Docker!
    This message shows that your installation appears to be working correctly.

    To generate this message, Docker took the following steps:
    1. The Docker client contacted the Docker daemon.
    2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
        (amd64)
    3. The Docker daemon created a new container from that image which runs the
        executable that produces the output you are currently reading.
    4. The Docker daemon streamed that output to the Docker client, which sent it
        to your terminal.

    To try something more ambitious, you can run an Ubuntu container with:
    $ docker run -it ubuntu bash

    Share images, automate workflows, and more with a free Docker ID:
    https://hub.docker.com/

    For more examples and ideas, visit:
    https://docs.docker.com/get-started/
    ```
  - 確認事項
    - `Hello from Docker!`と出力されていることを確認します。

- imageが取得できたか確認します。
  - 実行コマンド
    ```bash
    docker images
    ```
  - 実行結果例
    ```bash
    IMAGE                ID             DISK USAGE   CONTENT SIZE   EXTRA
    hello-world:latest   c3cbe1cc1aa5       25.9kB         9.49kB    U
    ```

- コンテナを確認します。
  - 実行コマンド
    ```bash
    docker ps -a
    ```
  - 実行結果例
    ```bash
    CONTAINER ID   IMAGE         COMMAND    CREATED         STATUS                     PORTS     NAMES
    40f94a50244f   hello-world   "/hello"   3 minutes ago   Exited (0) 3 minutes ago             gifted_mcclintock
    ```
  - 確認事項
    - `hello-world`のレコードが出力されること

## 動作確認の後処理

### 動作確認用のコンテナを削除
- コンテナを削除します。
  - 実行コマンド
    ```bash
    docker rm <hello-worldのコンテナのID>
    ```
  - 実行コマンド例
    ```bash
    docker rm 40f94a50244f
    ```
  - 実行結果例
    ```bash
    40f94a50244f
    ```

- コンテナが削除されたか確認します。
  - 実行コマンド
    ```bash
    docker ps -a
    ```
  - 実行結果例
    ```bash
    CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
    ```
  - 確認事項
    - `hello-world`が存在していないことを確認します。

### 動作検証用のイメージを削除
- イメージを削除します。
  - 実行コマンド
    ```bash
    docker image rm hello-world
    ```
  - 実行結果例
    ```bash
    Untagged: hello-world:latest
    Deleted: sha256:c3cbe1cc1aa588a64951ac6286e0df7b27fe2e6324b1001c619bb358770c0178
    ```

- イメージが削除されたか確認します。
  - 実行コマンド
    ```bash
    docker images
    ```
  - 実行結果例
    ```bash
    IMAGE   ID             DISK USAGE   CONTENT SIZE   EXTRA
    ```

# おわりに
本記事では、Windows11にWindows 11にDocker Desktopを導入した際の手順を記録しました。
今回は、ダウンロードから動作確認まで対応しました。

Windows11に導入する予定の方のお役に立てましたら幸いです。
