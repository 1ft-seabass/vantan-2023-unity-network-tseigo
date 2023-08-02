## LINE アカウント確認

<img src="https://guide.line.me/ja/install_5.png" width="200" />

LINE アカウントとスマホアプリインストールを確認します。

## LINE Notify サイトログイン

LINE Notify サイトにログインしアカウント確認をします。

![image](https://i.gyazo.com/c45ee309aa6793bc12f67c24f3a905ce.png)

https://notify-bot.line.me/ja/ に、まずアクセスします。

![image](https://i.gyazo.com/043d433bfa913e2edaee4bb917e92bb2.png)

右上のログインをクリック。

![image](https://i.gyazo.com/d2a7444465cb56a81eedb3e957403806.png)

下部の QR コードログインをクリックします。（メールアドレス・パスワードは、おそらくみなさん設定していないのと、いまから設定をやるとなると、PCとアプリを行き来して、まあまあ大変になるので今回は避けます。）

![image](https://i.gyazo.com/a6834bc86db3d0f024a0cb5886664883.png)

QR コードが表示されます。 LINE アプリでスキャンするとログインできます。QR コードのスキャン方法は下部のリンクをクリックすると表示されます。

![image](https://i.gyazo.com/e3856b10d3a1b933f284f7f81f3fac64.png)

✅ポイント
- LINE Notify API を使うために必要なアカウントは、LINE アカウントです。
- LINE Notify API を使うためにアクセストークンは、LINE Notify のサイトにアクセスしてアクセストークンを発行します。

## LINE Notify 設定の取得

LINE Notify 設定しトークンの取得を行います。

![image](https://i.gyazo.com/bf26cdcf093a783aee4ff510ec9ddb68.png)

ログインすると、右上にアカウント名が出るのでクリックします。

![image](https://i.gyazo.com/7cdb07c7e588bac278a5fb0b2dbc9d83.png)

マイページをクリック。

![image](https://i.gyazo.com/0c48f49af1be4e5e7c789366c0b838cf.png)

マイページの下の方に「アクセストークンの発行(開発者向け)」というエリアがあるのでスクロールします。

![image](https://i.gyazo.com/bbba9909e0437e487718479953b198ff.png)

トークンを発行するボタンをクリックします。

![image](https://i.gyazo.com/05b98371bcae556f578cdb96505ecb7c.jpg)

トークンを発行するウィンドウが表示されるので、以下のように対応します。

- トークン名を記入してください (通知の際に表示されます)
  - `授業テスト` と入力
- 通知を送信するトークルームを選択してください
  - `1:1でLINE Notifyから通知を受け取る` を選択

こちらを対応すると、発行するボタンが押せるようになるのでクリックします。

![image](https://i.gyazo.com/abee7f38d2db6897c61cdb42fc29a83c.png)

このようにトークンが表示されるのでメモしましょう。

**このページから移動すると、新しく発行されたトークンは二度と表示されないので気をつけましょう**

メモしたらウィンドウを閉じるボタンをクリックして閉じます。

✅ポイント
- LINE Notify API のアクセストークンの発行直後の対応は、アクセストークンは一度しか表示されないので忘れずメモすることです。

## LINE Notify 設定の確認

LINE で LINE Notify 設定されたかメッセージ確認を行います。

![image](https://i.gyazo.com/2fcf2f7f0d039737510759301a619485.png)

リストに追加されたことを確認しておきます。

![image](https://i.gyazo.com/07a33eec5562fc6fd67e52aeaa5c2bc9.png)

今回選択した LINE Notify 先のアカウントにこのようなメッセージが来ていることも確認します。このように、LINE Notify API のアクセストークンの発行されると LINE アプリに Personal Access Token 発行の通知が来ます。

✅ポイント
- LINE Notify API のアクセストークンの発行されると LINE アプリに Personal Access Token 発行の通知が来ます。

## LINE Notify の技術仕様

LINE Notify の技術的な仕様やメッセージデータを確認します。

### 技術的な仕様やドキュメント

LINE Notify API のデータのやり取りは HTTP プロトコルで行います。 

![image](https://i.gyazo.com/279081acd57f3204852561b29cab2aef.png)

ドキュメントは LINE Notify サイトから確認できます。

- https://notify-bot.line.me/ja/

![image](https://i.gyazo.com/6865fb59897f753ac0e2f0eec54e6739.png)

こんな感じです。

✅ポイント
- LINE Notify API のデータのやり取りは HTTP プロトコルで行われます。
- LINE Notify API の公式ドキュメントは LINE Notify サイトで確認できます。

### 通知系を把握していこう

![image](https://i.gyazo.com/8d51aa1bceb0f9b8531a879bc8d11ef8.png)

ドキュメントのつくりとして、はじめに「API 全体の流れと、実装の必要な箇所について」や「認証系」がありますが、今回はメッセージのやり取りを行う「通知系」をみていきます。

いままで勉強した HTTP の知識で一緒に読み解いていきましょう。

![image](https://i.gyazo.com/2717cf9a01715977b1a52f20243d0280.png)

リクエスト方法、必要なヘッダーを把握します。

- LINE への通知のためのAPI
  - メソッド
    - POST
  - URL
    - https://notify-api.line.me/api/notify

![image](https://i.gyazo.com/26199a652d191b61f11b0a747fe3285d.png)

送信できるデータはリクエストパラメータで確認できます。テキスト・画像・スタンプを送ることができます。

![image](https://i.gyazo.com/433127ff3540c8c9aab3ed4e37e934be.png)

各サービスごとに1時間にAPIをcallできる回数の上限 API Rate Limit も注意しましょう。

✅ポイント
- LINE Notify API でアクセストークンに関連付けられたユーザ・またはグループに対して通知を送信する場合、 POST メソッドでリクエストを行います。
- LINE Notify API では各サービスごとに1時間にAPIをcallできる回数の上限は 2022 年 6 月現在 1000 回です。
- LINE Notify API で送信できるデータは、テキスト・画像・スタンプがあります。