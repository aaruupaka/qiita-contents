---
title: 20260717-01-integration-github-chatgpt
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
# はじめに
GitHubとChatGPTの連携を行ったので、その際の対応手順を備忘録としてまとめています。

::: note info
2026年7月に実施した際の手順です。

実施時期によっては手順が異なる可能性もあります。
:::

# 環境情報
- ChatGPT: ブラウザ版
- ChatGPT契約プラン: Plusプラン
- GitHub: ブラウザ版

# ChatGPTのプラグインをインストールする
- ChatGPT(ブラウザ版)にアクセスします。

- 左下のプロフィールアイコンを押下し、めゆーを展開後、`設定`を押下します。
  <br>![alt text](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260717-01-integration-github-chatgpt/images/20260717-01-01.png)

- 設定画面が開いたら`プラグイン`タブを開き`プラグインを探す`を押下します。
  <br>![alt text](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260717-01-integration-github-chatgpt/images/20260717-01-02.png)

- プラグイン画面が開いたら、`GitHub`を押下します。
  <br>![alt text](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260717-01-integration-github-chatgpt/images/20260717-01-03.png)

- `GitHub`の詳細ページが開いたら`プラグインをインストール`を押下します。
  <br>![alt text](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260717-01-integration-github-chatgpt/images/20260717-01-04.png)

- `GitHubを接続する`ポップアップが出ることを確認します。
  - 今回、多要素認証（MFA）の有効化を求められたので対応します。
  <br>![alt text](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260717-01-integration-github-chatgpt/images/20260717-01-05.png)

- 多要素認証対応後、選択肢が`GitHubに進む`に変わったことを確認し、押下します。
  <br>![alt text](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260717-01-integration-github-chatgpt/images/20260717-01-06.png)

- GitHubのログイン画面に遷移することを確認します。
  <br>![alt text](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260717-01-integration-github-chatgpt/images/20260717-01-13.png)

# GitHub側で認証を行う
- 先ほど開いたGitHubのログイン画面からログインをします。
  <br>![alt text](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260717-01-integration-github-chatgpt/images/20260717-01-13.png)

- 内容を確認し`Authorize`を押下します。
  <br>![alt text](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260717-01-integration-github-chatgpt/images/20260717-01-07.png)

- `GitHub`の詳細ページに再アクセスし、`チャットで試す`や`接続済み`となっていることを確認します。
  <br>![alt text](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260717-01-integration-github-chatgpt/images/20260717-01-08.png)

# GitHubにChatGPT Codex Connectorをインストールする
- 「GitHub を ChatGPT に接続」というページにアクセスします。

```
https://help.openai.com/ja-jp/articles/11145903-connecting-github-to-chatgpt
```

  <br>![alt text](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260717-01-integration-github-chatgpt/images/20260717-01-12.png)

- 「ChatGPT を GitHub に接続した後、一部のリポジトリが表示されないのはなぜですか？」内の`このリンク`を押下します。
  <br>![alt text](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260717-01-integration-github-chatgpt/images/20260717-01-14.png)

- `Install & Authorize ChatGPT Codex Connector`のページに遷移することを確認します。
  <br>![alt text](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260717-01-integration-github-chatgpt/images/20260717-01-15.png)

- 任意の内容を選択し、`Install & Authorize`を押下します。

  ::: note warn
  今回、書き込み権限を求められているので、`Only select repositories`を選択し、最低限のリポジトリを選択することをお勧めします。
  :::

  <br>![alt text](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260717-01-integration-github-chatgpt/images/20260717-01-16.png)

- GitHubの設定画面に遷移します。
  <br>![alt text](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260717-01-integration-github-chatgpt/images/20260717-01-09.png)

- `Applications`を押下し、`Installed GitHub Apps`タブ内に`ChatGPT Codex Connector`があることを確認します。
  <br>![alt text](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260717-01-integration-github-chatgpt/images/20260717-01-17.png)


# ChatGPT側のプラグインの権限を確認する
ChatGPTのGitHubプラグインでは権限がデフォルトの場合、「低リスクのアクションを許可」が選択されています。
使用用途によっては権限が足りなくなる場合もあるので、必要に応じて変更してください。

### ChatGPT側のプラグインの権限の変更手順
- ChatGPTのプラグインを開き、GitHubのプラグインを選択します。
  <br>![alt text](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260717-01-integration-github-chatgpt/images/20260717-01-19.png)
- `権限`を押下します。
  <br>![alt text](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260717-01-integration-github-chatgpt/images/20260717-01-20.png)
- 任意の権限を選択すれば、反映されます。
  <br>![alt text](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260717-01-integration-github-chatgpt/images/20260717-01-21.png)

# 動作確認
- ChatGPTにリポジトリの一覧を取得するよう依頼し、問題なく取得できることを確認します。
  <br>![alt text](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260717-01-integration-github-chatgpt/images/20260717-01-22.png)

# 502エラーが発生した件
動作確認時にChatGPTにリポジトリの一覧の取得を依頼したところ502エラーが発生すると返されました。

調べたところOpenAI側で不具合が発生していたようでした。
執筆時点では解決しています。

https://status.openai.com/incidents/01KXPJ62Z704GE0SRNKQA64X4X

  <br>![alt text](https://raw.githubusercontent.com/aaruupaka/qiita-contents/main/articles/20260717-01-integration-github-chatgpt/images/20260717-01-18.png)

# おわりに
今回はChatGPTとGitHubの連携を行い、その内に実施した手順をまとめました。

この記事がどなたかのお役に立てれば幸いです。