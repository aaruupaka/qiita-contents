---
title: ConohaVPS 契約サーバーのスペック検討
tags:
  - ConohaVPS
  - 備忘録
  - 検討資料 
private: true
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
# 概要
- ConohaVPSで契約するサーバーのスペック検討内容の記録

# 検討プラン
1. メモリ1GB 
      - スペック
        - メモリ:1GB
        - CPU:2コア
        - SSD:100GB
      - 料金
        - 1カ月：589円
        - 1年　：7068円

1. メモリ2GB 
    - スペック
      - メモリ:2GB
      - CPU:3コア
      - SSD:100GB
    - 料金
      - 1カ月：981円
      - 1年　：11772円

3. メモリ4GB
    - スペック
      - メモリ:4GB
      - CPU:4コア
      - SSD:100GB
    - 料金
      - 1カ月：1970円
      - 1年　：23640円

- 参考資料
  - URL : https://vps.conoha.jp/pricing/?btn_id=top--header_pricing

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4376858/26b7d91a-2e48-4ece-8e5a-3560abd27c1e.png)

#使用用途
- Blog（wordpress）
- 家計管理システム
- 日記システム
- タスク管理システム
- ウェブコンテンツ管理システム

おもにBlogを運用し、状況に合わせほかシステムを開発、リリースする予定。

なお、blog以外は、認証機能ありかつ、個人利用を目的とする。
但し、ドメインは、ブログとブログ以外で2つ運用する想定。

# その他・所感
- メモリ4GBは、金銭的にきつい
- 運用する覚悟を決めるため、1年プランで契約（あと、割引も効く）
- 1GBはいろいろリリースしたらスペック不足しそう。ブログが伸びればサーバーは分離するが、いったん一緒にしたい。

# 結論
**メモリ2GB**を契約する。





