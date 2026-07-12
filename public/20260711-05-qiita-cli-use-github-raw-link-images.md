---
title: Qiita CLIでGitHub管理下の画像を使用する方法【GitHub Raw Link】
tags:
  - QiitaCLI
  - GitHub
  - GitHubRawLink
  - 備忘録
private: true
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: true
posting_campaign_uuid: null
agreed_posting_campaign_term: false
---
# はじめに
Qiita CLIを利用してGitHubで管理している記事を公開した際、画像が正しく表示されないという問題に遭遇しました。

原因を調べたところ、相対パスでの画像パスの指定では表示できず、GitHub Raw Linkを指定する必要があることが分かりました。

本記事では、GitHub Raw Linkの取得方法と、Qiita CLIで画像を表示する方法を紹介します。

