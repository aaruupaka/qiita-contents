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

# 発生した事象
GitHubで管理している画像をMarkdownに記載して記事を投稿したところ、
Qiita上で画像が表示されませんでした。

例えば、以下のように相対パスで画像リンクを指定していたのですが、うまく表示されませんでした。

```md
![alt text](../articles/20260711-05-qiita-cli-use-github-raw-link-images/images/20260711-05-01.png)
```

# 原因と解決方法
原因は相対パスで画像パスを指定していたことでした。

Qiita CLIを利用してGitHubで記事を管理すること自体はできますが、
GitHubリポジトリのコンテンツを相対パスで指定して表示することはできませんでした。

GitHub管理下の画像ファイルをQiitaの記事上で表示させたい場合、
画像そのものへ直接アクセスできるURLである、
`GitHub Raw Link`を使用する必要がありました。

