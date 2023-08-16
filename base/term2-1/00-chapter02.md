# Airtable をサーバに反映して動かす

![9d2c38e6fe48e61528f6b2d34370768f](https://i.gyazo.com/9d2c38e6fe48e61528f6b2d34370768f.png)

## この章で学ぶこと

Airtable をサーバに反映して動かします。

## Base からデータを取得するために必要な設定

Base からデータを取得するためは Airtable API をあつかう必要があります。そして狙った Base から取得する Base ID と API キーが必要になります。

## Base ID の取得

![59e025e8ef9495c56ac93382f684e6f3](https://i.gyazo.com/59e025e8ef9495c56ac93382f684e6f3.png)

https://airtable.com/developers/web/api/introduction をクリックして API のドキュメントに移動します。

![41a222a868c0e8881d73f2b55b6c0fd3](https://i.gyazo.com/41a222a868c0e8881d73f2b55b6c0fd3.png)

API Reference ページが表示されているので、その下部に Base の一覧があるので、今回の Base をクリックします。

![531c6a425920b683528b5963f880aed8](https://i.gyazo.com/531c6a425920b683528b5963f880aed8.png)

今回の Base を取得するために特化した API ドキュメントに移動するので、`The ID of this base is ` ではじまる文章を探します。

![3e6db650699a2898b5f7502dc72cd885](https://i.gyazo.com/3e6db650699a2898b5f7502dc72cd885.png)

appからピリオドの手前までが今回の Base Id です。テキストエディタにコピーしてメモしておきましょう。

### もう一つの Base Id の確認方法

![e83fbbaac0f5dc509f2d16503cea76fe](https://i.gyazo.com/e83fbbaac0f5dc509f2d16503cea76fe.png)

実は Base Id は Base ページの URL でも分かります。今回の Base ページを表示します。

![1f623bf099c2c4ac9857907f030f5998](https://i.gyazo.com/1f623bf099c2c4ac9857907f030f5998.png)

Base ページの URL のは https://airtable.com/ 以降にある次のスラッシュまで app～～～～～～ が Base Id です。

コピーしたものと、こちらが合っているかも確認しておくとより確実です。

Airtable の扱いに慣れてくれば、こちらのやりかたで Base Id を把握するのもよいでしょう。

## API キーの取得

Airtable にログインした状態で、Airtable Developers のトークン管理画面 https://airtable.com/create/tokens にアクセスします。

![48a456f3303bb8273ce07b544a69a1ea](https://i.gyazo.com/48a456f3303bb8273ce07b544a69a1ea.png)

Personal access token ページが表示されます。 Create token ボタンをクリックします。

![474f4398fe432867af92ce329d9f0a1a](https://i.gyazo.com/474f4398fe432867af92ce329d9f0a1a.png)

Create personal access token が表示されます。

![590490ff2f15502a2c4bef7119396da7](https://i.gyazo.com/590490ff2f15502a2c4bef7119396da7.png)

今回、 Name は `unity test` とします。

![7917693b3084603d66f40967a6a52b6b](https://i.gyazo.com/7917693b3084603d66f40967a6a52b6b.png)

Scopes では、この API Key で解放する権限を決めます。 Add a scope をクリックしましょう。

![7b10655e6b5d639d7fca99ceb2b139ba](https://i.gyazo.com/7b10655e6b5d639d7fca99ceb2b139ba.png)

data.records:read と data.records:write を 1 つずつ選択します。結果、Scopes に 2 つの権限が設定されました。

![b9974d0ce91eb08750b6c8755e407aab](https://i.gyazo.com/b9974d0ce91eb08750b6c8755e407aab.png)

Access ではアクセス可能なデータ（Base や Workspace）を設定します。Add a base をクリックしましょう。

![595555c5dc05dd5fa83eaeb02cf0fb65](https://i.gyazo.com/595555c5dc05dd5fa83eaeb02cf0fb65.png)

今回は `All current and future bases in all current and future workspaces` を選択します。

![50d76ae0c0898b71d0df19a477b5dd7e](https://i.gyazo.com/50d76ae0c0898b71d0df19a477b5dd7e.png)

作成できたら Create token ボタンをクリックします。

![925f00ce09b18711bf013f9f8f4128e5](https://i.gyazo.com/925f00ce09b18711bf013f9f8f4128e5.png)

今回の API Key が作成されます。こちらは 1 度かぎりしか出てこないウィンドウです。閉じてしまうと、もう見ることができないので注意しましょう。

これをコピーして保管しておけば新しい Airtable API Key 作成は完了です。

![d203b07aff01ff9ec1b297c335f0dd9f](https://i.gyazo.com/d203b07aff01ff9ec1b297c335f0dd9f.png)

x ボタンをクリックして閉じて、一覧に今回の API Key が出来ているか確認しましょう。

## Codespace 削除

![0a3a35f3418068b7713ddaa729f2c660](https://i.gyazo.com/0a3a35f3418068b7713ddaa729f2c660.png)

GitHub にログインした状態で https://github.com/codespaces にアクセスします。

![016de554e3ab779c598ac69607955af2](https://i.gyazo.com/016de554e3ab779c598ac69607955af2.png)

今回使っている Codespace を探します。

![abd033cda989bfdd5a094d922bb6cfbc](https://i.gyazo.com/abd033cda989bfdd5a094d922bb6cfbc.png)

Delete をクリックして削除します。

## 今回の GitHub Codespaces リポジトリにアクセス

今回の GitHub Codespaces リポジトリに Chrome ブラウザでアクセスします。

![1d4fe9d0e6c86377c17828a2ff26fd0d](https://i.gyazo.com/1d4fe9d0e6c86377c17828a2ff26fd0d.png)

https://github.com/1ft-seabass/vantan-unity-network-server-base にアクセスします。

## GitHub Codespaces としてリポジトリを開く

![6ebad95a052d8a2d37d889399e120424](https://i.gyazo.com/6ebad95a052d8a2d37d889399e120424.png)

Code ボタンをクリックします。

![8f6a286108378103ac8d30df6f811ef4](https://i.gyazo.com/8f6a286108378103ac8d30df6f811ef4.png)

Codespaces タブをクリックします。Create codespace on main をクリックします。

![47b24d3be5b687f60383455a75898788](https://i.gyazo.com/47b24d3be5b687f60383455a75898788.png)

Setting up your codespace という画面が出て構築されます。

![28ea2b9aece0957b5bb7292427889a10](https://i.gyazo.com/28ea2b9aece0957b5bb7292427889a10.png)

ブラウザ上で Visual Studio Code が起動し、今回の仕組みを反映した環境が起動しました。

## サーバの起動

![0a3a35f3418068b7713ddaa729f2c660](https://i.gyazo.com/0a3a35f3418068b7713ddaa729f2c660.png)

- ターミナルで `node term2-1-chapter02.js` をサーバ起動
- ポートタブで今回のサーバ起動を公開
- シークレットウィンドウで今回のサーバが公開されているか確認します

## API キーの入力

## 動かしてみる1（URL アクセスで、データ取得）

## 動かしてみる2（データ変更して確認）

## 動かしてみる2（URL アクセスで、データ変更）

## そのほかのメソッド

JavaScript だけど