# 初めに
本、mdファイルでは、
Qiitaの限定公開の記事の取り込みを行う。

# 限定公開記事の移行
- ローカルリポジトリに移動する
    ```bash
    cd D:\a_pjs\2026051401_aaruupaka_qiita-contents\qiita-contents\
    ```
- 移行先の記事を、ローカルリポジトリ内で作成する。
    - 実行コマンド
        ```bash
        npx qiita new 20260427-01-conohavps-server-spec-selection
        ```
    - 実行結果
        ```bash
        ◇ injected env (0) from .env // tip: ◈ encrypted .env [www.dotenvx.com]
        created: 20260427-01-conohavps-server-spec-selection.md
        ```
- ファイルが作成されたことを確認する。
    - 実行コマンド
        ```bash
        ls .\public\
        ```
    - 実行結果
        ```bash    
        Directory: D:\a_pjs\2026051401_aaruupaka_qiita-contents\qiita-contents\public

        Mode                 LastWriteTime         Length Name
        ----                 -------------         ------ ----
        d----          2026/05/15    16:08                .remote
        -a---          2026/05/18    17:15            192 20260427-01-conohavps-server-spec-selection.md
        -a---          2026/05/15    14:43           7259 ad29b1589f55a521942f.md
        ```

- ファイルの内容を確認する
    - ファイル内容例
        ```md
        ---
        title: 20260427-01-conohavps-server-spec-selection
        tags:
        - ''
        private: false
        updated_at: ''
        id: null
        organization_url_name: null
        slide: false
        ignorePublish: false
        ---
        # new article body
        ```
- 記事の情報を更新する。
    - 更新対象
        - title
            - タイトルを限定公開時の記事に変更
        - private
            - `ture`に変更
                - `true`にすることにより、限定公開になる
    - 更新例
        ```md
        ---
        title: ConohaVPS　契約サーバーのスペック検討
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
        # new article body

        ```
- 限定定公開記事の内容を張り付ける。


# githubのリモートリポジトリに反映する。
- gitのローカルリポジトリのステータスを確認する。
    - 実行コマンド
        ```bash
        git status
        ```
    - 実行結果
        ```bash
        On branch main
        Your branch is up to date with 'origin/main'.

        Untracked files:
        (use "git add <file>..." to include in what will be committed)
                public/20260427-01-conohavps-server-spec-selection.md
                worklogs/20260518-01-import-private-article/

        nothing added to commit but untracked files present (use "git add" to track)
        ```
- 今回追加した記事のみ、ステージングする。
    - 実行コマンド
        ```bash
        git add public/20260427-01-conohavps-server-spec-selection.md
        ```
- gitのローカルリポジトリのステータスを確認する。
    - 実行コマンド
        ```bash
        git status
        ```
    - 実行結果
        ```bash
        On branch main
        Your branch is up to date with 'origin/main'.

        Changes to be committed:
        (use "git restore --staged <file>..." to unstage)
                new file:   public/20260427-01-conohavps-server-spec-selection.md

        Untracked files:
        (use "git add <file>..." to include in what will be committed)
                worklogs/20260518-01-import-private-article/

        ```
- コミットする
    - 実行コマンド
        ```
        git commit -m "20260518-import-private-articles"
        ```
- リモートリポジトリにプッシュする
    - 実行コマンド
        ```
        git push origin main
        ```
    - 実行結果
        ```
        Enumerating objects: 6, done.
        Counting objects: 100% (6/6), done.
        Delta compression using up to 8 threads
        Compressing objects: 100% (4/4), done.
        Writing objects: 100% (4/4), 1.37 KiB | 1.37 MiB/s, done.
        Total 4 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
        remote: Resolving deltas: 100% (1/1), completed with 1 local object.
        To github.com:aaruupaka/qiita-contents.git
        7bf22b9..0f45b14  main -> main
        ```