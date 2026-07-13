---
title: Qiita CLIでGitHubリポジトリで管理している画像を使用する方法【GitHub Raw Link】
tags:
  - GitHub
  - 備忘録
  - QiitaCLI
  - GitHubRawLink
private: false
updated_at: '2026-07-13T23:07:16+09:00'
id: f286952b967af8fc47c0
organization_url_name: null
slide: false
ignorePublish: false
posting_campaign_uuid: 783b7a849caf11eefd91
agreed_posting_campaign_term: true
---
# はじめに
Qiita CLIを利用してGitHubリポジトリで管理している記事を公開した際、画像が正しく表示されないという問題に遭遇しました。

原因を調べたところ、GitHubリポジトリ内の相対パスでは表示できず、GitHub Raw Linkを指定する必要があることが分かりました。

本記事では、GitHub Raw Linkの取得方法と、Qiita CLIで画像を表示する方法を紹介します。

# 発生した事象
GitHubリポジトリで管理している画像をMarkdownに記載して記事を投稿したところ、
Qiita上で画像が表示されませんでした。

例えば、以下のように相対パスで画像リンクを指定していたのですが、うまく表示されませんでした。

```md
![alt text](../articles/20260711-05-qiita-cli-use-github-raw-link-images/images/20260711-05-01.png)
```

# 原因と解決方法
原因は相対パスで画像パスを指定していたことでした。

Qiita CLIを利用してGitHubリポジトリで記事を管理すること自体はできますが、
GitHubリポジトリのコンテンツを相対パスで指定して表示することはできませんでした。

QiitaはGitHubリポジトリ内の相対パスを解決できないため、画像を表示するにはインターネット上から直接取得できるURL（`GitHub Raw Link`）が必要になります。

## GitHub Raw Linkとは
GitHub Raw Linkとは、GitHubリポジトリ上のファイルをGitHubの表示ページではなく、画像やテキストファイルなどの実データを直接取得するためのURLです。

例えば、画像ファイルであれば、
ブラウザでアクセスすると画像だけが表示されるURLになります。

## GitHub Raw Linkを取得する手順

GitHub Raw Linkは下記の手順で手に入れることができます。
1. ブラウザ版のGitHub上で画像を表示させます。
2. 画像を右クリック後`画像アドレスをコピー`など、画像URLをコピーできるメニューをを選択します。

取得すると下記のようなリンクが取得できます。
```
https://raw.githubusercontent.com/aaruupaka/qiita-contents/9e5f6c7f88b737ef4a6dfcac740e46fe1a843ac9/articles/20260711-05-qiita-cli-use-github-raw-link-images/images/20260711-05-01.png
```

`https://raw.githubusercontent.com/aaruupaka/qiita-contents/9e5f6c7f88b737ef4a6dfcac740e46fe1a843ac9`
部分までは別画像であっても共通なので、一度自分のGitHub Raw Linkを取得してしまえば、それ以降を書き換えることで表示できます。

::: note info
上記例のリンクの`9e5f6c7f88b737ef4a6dfcac740e46fe1a843ac9`部分は「コミットハッシュ」であるようです。
:::

また、GitHub Raw Linkは下記の要素でも構築することができます。
```
https://raw.githubusercontent.com/<ユーザー名>/<リポジトリ名>/<ブランチ名>/<画像パス>
```

そのため、URLの構成が分かれば、ブラウザから取得しなくても組み立てることも可能です。

# おわりに
今回はGitHub Raw Linkを使用して、Qiita CLIで管理している記事からGitHub管理下の画像を表示する方法を紹介しました。

同じように「画像が表示されない」という現象に遭遇した場合は、本記事の手順を試してみてください。

他の方のお役に立てましたら幸いです。
