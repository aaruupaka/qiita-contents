# Local WP 初回セットアップ

## 初回起動時
- LocalWPが起動します。<br>
    ![alt text](images/20260503-03-01.png)
- `Terms of Service`の内容を確認し、チェックボックスを有効化、`I agree`ボタンを押下します。<br>
    ![alt text](images/20260503-03-02.png)
- `Is it ok to enable error reports?`では、任意のボタンを押下します。
    - 私は`Turn on error reporting`を選択しました。
    - 仮に本番環境DBのコピー等、機密情報をlocalWP上で取り扱う予定がある場合は、`No, thanks`を選択するのが良いと思います。
    ![alt text](images/20260503-03-03.png)
- `IS it ok to enable usage reporting?`では、任意のボタンを押下します。
    - 私は`No, thanks`を選択しました。<br>
    ![alt text](images/20260503-03-04.png)

- LocalWPの`Local sites`タブが表示されることを確認します。<br>
    ![alt text](images/20260503-03-05.png)

## テーマ作成用のローカルWPを作成する。
- `+ Create a new site`ボタンを押下します。<br>
    ![alt text](images/20260503-03-06.png)
- `Create a site`画面で`Create a new site`を選択した状態で、`Contine`ボタンを押下します。<br>
    ![alt text](images/20260503-03-07.png)
- `What's your site's name?`画面では、任意のサイト名を入力し、`Continue`ボタンを押下します。<br>
    ![alt text](images/20260503-03-08.png)
- `Choose your environment`画面では、`Custom`を選択後、自身の環境に最も近しい内容を選択し、`Continue`ボタンを押下します。<br>
    ![alt text](images/20260503-03-09.png)
- `Set up WordPress`画面では、任意の内容を入力し、`Add Site`ボタンを押下します。
    - 私は下記の設定を行いました。
        - WordPress username
            - localwp
        - WordPress password
            - password
        - WordPress e-mail
            - dev-email@wpengine.local
                - デフォルト値<br>
    ![alt text](images/20260503-03-10.png)
- UATが出た場合は、適宜許可します。
- 環境構築が完了したことを確認します。<br>
    ![alt text](images/20260503-03-11.png)
- LocalWPの`Local sites`タブ内の`WP Admin`ボタンを押下し、WordPressのログイン画面に遷移することを確認します。<br>
    ![alt text](images/20260503-03-12.png)
- `Set up WordPress`画面で設定したアカウント情報を入力し。`Log in`ボタンを押下します。<br>
    ![alt text](images/20260503-03-13.png)
- ダッシュボードに遷移することを確認します。<br>
    ![alt text](images/20260503-03-14.png)
- LocalWPの`Local sites`タブ内の`Open Site`ボタンを押下し、WordPresサイトのトップ画面に遷移することを確認します。<br>
    ![alt text](images/20260503-03-15.png)