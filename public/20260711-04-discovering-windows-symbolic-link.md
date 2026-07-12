---
title: Windowsでシンボリックリンクが作れることを最近知った話
tags:
  - Windows11
  - シンボリックリンク
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
最近、Windowsでもシンボリックリンクが作れることを知りました。

一応、約3年、エンジニアとしての業務経験があるのですが、
お恥ずかしながら知りませんでした。

2年ほど前にWindowsでもシンボリックリンクが作れれば便利なのにと思い、
当時も調べた記憶はあるのですが、私の調べ方が悪かったのか、うまく情報を見つけられませんでした。

しかし、先日、WordPressテーマ開発の環境構築中に、ChatGPTから教えてもらい、大変驚きました。

シンボリックリンクを利用すると、Gitリポジトリ側を編集するだけで
Local WP側にも反映されるため、WordPressテーマを最新の状態に更新する作業が不要になります。

備忘録として、今後同じように調べる方の参考になればと思いまとめました。

また、もしよろしければ、Windowsでもシンボリックリンクを作れることを知っているか否かを教えていただけると嬉しいです。
認知率がどのくらいなのかを知りたいです！

# シンボリックリンクとは
シンボリックリンクとは、別の場所にあるファイルやフォルダを、あたかも現在の場所に存在しているかのように扱える仕組みです。

例えば、`C:\Git\my-theme` にあるWordPressテーマを、`Local WP` のテーマディレクトリにシンボリックリンクとして配置すると、実際には同じファイルを参照しているため、Git管理しているテーマを編集するだけで、Local WP側にも変更が反映されます。

そのため、ファイルをコピーし直す手間がなくなり、開発効率を向上させることができます。

# シンボリックリンク作成コマンドの文法
- 文法
```cmd
mklink /D "シンボリックリンク作成先のパス" "シンボリックリンクの参照先のパス"
```

- 実行コマンド例
  ```cmd
  mklink /D "C:\Users\testuser\Local Sites\wordpress-theme-dev\app\public\wp-content\themes\aaruupaka-prot" "D:\a_pjs\2026060301_aaruupaka_wordpress-theme-aaruupaka-prot\wordpress-theme-aaruupaka-prot\aaruupaka-prot"
  ```
