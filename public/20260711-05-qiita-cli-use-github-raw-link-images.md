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

QiitaはGitHubリポジトリ内の相対パスを解決できないため、画像を表示するにはインターネット上から直接取得できるURL（`GitHub Raw Link`）が必要になります。



## GitHub Raw Linkとは
GitHub Raw Linkとは、GitHub上のファイルをHTMLページではなく、
ファイルそのものとして取得するためのURLです。

例えば、画像ファイルであれば、
ブラウザでアクセスすると画像だけが表示されるURLになります。

## GitHub Raw Linkを取得する手順

GitHub Raw Linkは下記の手順で手に入れることができます。
1. ブラウザ版のGitHub上で画像を表示させます。
2. 画像を右クリック後`画像アドレスをコピー`を選択します。

取得すると下記のようなリンクが取得できます。
```
https://raw.githubusercontent.com/aaruupaka/qiita-contents/9e5f6c7f88b737ef4a6dfcac740e46fe1a843ac9/articles/20260711-05-qiita-cli-use-github-raw-link-images/images/20260711-05-01.png
```

`https://raw.githubusercontent.com/aaruupaka/qiita-contents/9e5f6c7f88b737ef4a6dfcac740e46fe1a843ac9`
部分までは別画像であっても共通なので、一度自分のGitHub Raw Linkを取得してしまえば、それ以降を書き換えることで表示できます。

また、GitHub Raw Linkは下記の要素で構成されているようです。
```
https://raw.githubusercontent.com/<ユーザー名>/<リポジトリ名>/<ブランチ名>/<画像パス>
```

そのため、極論、ブラウザからGitHub Raw Linkを取得するまでもなく、対応する情報に書き換えれば問題なく取得できます。

# おわりに
今回はGitHub Raw Linkを使用し、Qiita CLIで管理しているQiita記事でGitHub管理下の画像を使用する方法をまとめました。
