---
title: Docker Desktopの `Disk image location` の変更手順【Windows 11】
tags:
  - Docker
  - DockerDesktop
  - Windows
  - Windows11
private: true
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
posting_campaign_uuid: null
agreed_posting_campaign_term: false
---
# はじめに
Cドライブの残り容量が13GB程度になってしまったため、
`Disk image location`の保存先をDドライブに変更することにしました。

今回は、Docker Desktopの`Disk image location`の変更した際の手順をまとめています。

::: note info
2026年7月に対応した際の内容です。
:::

# 環境情報
- OS: `Windows 11`
- Docker Desktopバージョン: `v4.83.0`

# `Disk image location`の変更手順
- Docker Desktopを起動します。

  ![alt text](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260723-01-docker-desk-top-change-disk-image-location/images/20260723-01-01.png)

- ⚙マークを押下します。

  ![alt text](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260723-01-docker-desk-top-change-disk-image-location/images/20260723-01-02.png)

- `Resources`を選択します。

  ![alt text](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260723-01-docker-desk-top-change-disk-image-location/images/20260723-01-03.png)

- `Advanced`タブ内の`Disk image location`の`Browse`を押下し、任意のパスを指定します。

  ![alt text](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260723-01-docker-desk-top-change-disk-image-location/images/20260723-01-04.png)

- `Apply & restart`を押下します。

  ![alt text](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260723-01-docker-desk-top-change-disk-image-location/images/20260723-01-05.png)

- 確認画面が出るので`Yes, move it`を押下します。

  ![alt text](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260723-01-docker-desk-top-change-disk-image-location/images/20260723-01-06.png)

- 処理が完了するまで待機します。
  - 私の場合は30秒ぐらいでした。
  - 環境によっては時間がかかることがあるようです。

  ![alt text](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260723-01-docker-desk-top-change-disk-image-location/images/20260723-01-07.png)

- 以上で作業は完了です。

  ![alt text](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260723-01-docker-desk-top-change-disk-image-location/images/20260723-01-08.png)

# おわりに
今回は、Docker Desktopの`Disk image location`の変更手順をまとめました。

この記事がどなたかのお役に立てば幸いです。