# OpenAI 社のアカウントの取得

この資料は 2023/6 現在のものです、いまは手順が異なる場合があります。

![e87f6ca928239a4f4318995f3000b692](https://i.gyazo.com/e87f6ca928239a4f4318995f3000b692.jpg)

[OpenAI 社のトップページ](https://openai.com/)の右上のメニューから Sign up ボタンをクリックします。

![2fe8702eb8814bf040e8c19f977ef5a8](https://i.gyazo.com/2fe8702eb8814bf040e8c19f977ef5a8.png)

さらにパスワードを設定し、Continueを押すと、メールが送信されます。

![img](https://gyazo.com/bd9dcdba593bcb272dc2d99072520370.png)

下記のようなメールが届きます。

![img](https://gyazo.com/124872c2fc0a7f64a31eee463a7b729a.png)

メールのVerify email addressをクリックするとメールアドレスが認証されました。

![](https://gyazo.com/253a5ae39b635820b1648615670fb480.png)

再度[ログインページ](https://chat.openai.com/auth/login)にアクセスし、先ほどのメールアドレスとパスワードを使用して、ログインしましょう。

初ログインに成功すると、下記のような名前と生年月日の入力ページが表示されます。

![img](https://gyazo.com/fbf6c39afc5a82deaf375edd76630555.png)

名前と生年月日を入力すると次は、電話番号の入力を行います。

![img](https://gyazo.com/30684ec04633bc9c67b276071e1e2a01.png)

Secd codeをクリックするとOpenAIから6桁の認証コードが送られてきます。

※皆さんは596196ではありません。

![img](https://gyazo.com/52916d53b93b0795553808ed65e41473.png)

送られてきた認証コードを下記の画面で入力します。

![img](https://gyazo.com/3caf47b4dcdc0182d2ed8dfa9cf071f7.png)

電話番号の認証に成功すると、ChatGPTの画面に映ります。

![img](https://gyazo.com/49038171a1c26ad93ae3bcd41c0c06fe.png)

次に[OpenAI Platform](https://platform.openai.com/)に移ります。アカウントが作成できているとアプリの選択ページが表示されます。これでOpenAIアカウントの準備は終了です。

![c23a9f0bd362823347f92d420e4ab185](https://i.gyazo.com/c23a9f0bd362823347f92d420e4ab185.png)

このような API ページ https://platform.openai.com/ が表示されます。

# OpenAI 社 ChatGPT API キーの取得

## API キーの取得

![59721bc470b73edf42fe34f4ae88a4e3](https://i.gyazo.com/59721bc470b73edf42fe34f4ae88a4e3.png)

ログインして API ページ https://platform.openai.com/ が表示した状態で、右上のユーザー名の書いてあるところをクリックしてユーザーメニューを出します。View API Keys をクリックします。

![95ab50ffd208cbf94b7dac63817a9552](https://i.gyazo.com/95ab50ffd208cbf94b7dac63817a9552.png)

API keys ページ https://platform.openai.com/account/api-keys に移動します。Create new secret key ボタンをクリックします。

![b547ba48e0b280cc1c7ad9f56aeeb7f8](https://i.gyazo.com/b547ba48e0b280cc1c7ad9f56aeeb7f8.png)

今後分かりやすくするためのキーの名前を決めれるので `Handson key` と入力して、Create secret key ボタンをクリックします。

![96af348f170078f9dbaad47faa33c06d](https://i.gyazo.com/96af348f170078f9dbaad47faa33c06d.png)

Create new secret key のウィンドウになり、キーが表示されます。 `sk-` ではじまるものです。このキーは **この画面一度切り** しか表示されないので、手元のテキストエディタにメモしておきましょう。

ちゃんとメモができたら Done ボタンをクリックします。

## 支払い情報の登録

この状態ですと、API キーは作られましたが、支払い情報がないために課金ができず指標することができません。

支払い情報の登録をしましょう。

![34caadfece28092285cc87d983d56cf8](https://i.gyazo.com/34caadfece28092285cc87d983d56cf8.png)

左メニューから Billing をクリックします。

![a79b300f4769e6d8daaaaa85d927ca2b](https://i.gyazo.com/a79b300f4769e6d8daaaaa85d927ca2b.png)

Billing overview という支払い情報のページが表示されます。

![6d7651d7a393f03773fd72baf1cbe594](https://i.gyazo.com/6d7651d7a393f03773fd72baf1cbe594.png)

Set up paid account ボタンをクリックします。Set up payment method が聞かれるので、今回のハンズオンでは個人利用なので I'm an indivisual をクリックします。

![658ce920bb6dcc1871eec194bf32473a](https://i.gyazo.com/658ce920bb6dcc1871eec194bf32473a.png)

クレジットカード情報を入力して Set up payment method ボタンをクリックして支払い情報の登録を完了します。

## 利用制限 Usage limits を設定

API の利用は使ったら使った分だけ課金される従量課金のため、小さめ金額で制限を設けておきます。

![335882d8f13f4ef022727ee8a7ae3ba4](https://i.gyazo.com/335882d8f13f4ef022727ee8a7ae3ba4.png)

Usage limits をクリックします。

![7f58eac4de0591a3a104183c57502776](https://i.gyazo.com/7f58eac4de0591a3a104183c57502776.png)

Hard limit は「毎月この使用量しきい値に達すると、それ以降のリクエストは拒否されます」。Soft limit は「毎月この使用量のしきい値に達すると、通知メールが送信されます」。ですので、使いすぎを即ブロックしたい場合は Hard limit が重要です。

私の場合は、余裕をもって Hard limit を $24 Soft limit は $12 に設定しましたが。皆さんの状況に合わせて設定しましょう。

- Hard limit
  - $10
- Soft limit
  - $5

くらいだと、1000 円前後でストップするので使いやすいかもしれません。

これで、うっかりたくさん試して使いすぎになりそうなときでも安心です。

📝参考資料
- ChatGPT APIキー取得までの手順 - Qiita
  - https://qiita.com/kotattsu3/items/b936a65d173a5d39dad0