# Airtable をサーバに反映して動かす

![9d2c38e6fe48e61528f6b2d34370768f](https://i.gyazo.com/9d2c38e6fe48e61528f6b2d34370768f.png)

## この章で学ぶこと

Airtable をサーバに反映して動かします。

## おさらい

![c2469d996dc803b8a13c286342e01942](https://i.gyazo.com/c2469d996dc803b8a13c286342e01942.png)

サーバのプログラム内で記録すると再起動時になくなってしまいます。データを記録する Airtable サービスを使って、サーバの外にデータを記録して、サーバーが再起動してもデータが保持されるようにしてみましょう。

## Base からデータを取得するために必要な設定

![0d324902d7e79943fcc93826cba1f871](https://i.gyazo.com/0d324902d7e79943fcc93826cba1f871.png)

Base からデータを取得するためは Airtable API をあつかう必要があります。そして狙った Base から取得する Base ID と API キーが必要になります。

その他に、テーブル名も必要ですが、これは、そのままの名前で呼び出せばいいので割愛します。

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

![0315bfabadc8442391ad415f119e63c3](https://i.gyazo.com/0315bfabadc8442391ad415f119e63c3.png)

これをテキストエディタにコピーして保管しておけば新しい Airtable API Key 作成は完了です。

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

## 仕組みの説明

今回起動するプログラム `term2-1-chapter02.js` の仕組みを説明します。

```js
// path ライブラリ
const path = require('path');
// Express ライブラリの呼び出し
const express = require('express');
// Express ライブラリからサーバーの仕組みを app 変数として呼び出す
const app = express();

// Airtable 設定 ///////////////////////////////////////////////////////////////
// Airtable ライブラリ
const Airtable = require('airtable');

// Airtable API キー
const AIRTABLE_API_KEY = 'AIRTABLE_API_KEY';
// Airtable BASE ID
const AIRTABLE_BASE_ID = 'AIRTABLE_BASE_ID';
// Airtable Table 名
const AIRTABLE_TABLE_NAME = 'Sample01';

// 今回 Base を読み込む設定
const base = new Airtable({ apiKey: AIRTABLE_API_KEY }).base(AIRTABLE_BASE_ID);

// public フォルダ内にあるファイルはパスが一致していると呼びだせます
// /index.html や / の場合は public フォルダ内の index.html が表示されます
app.use(express.static(__dirname + '/public'));

// POST データを受け取る際に必要な処理
app.use(express.urlencoded({ extended: true }));
// データを JSON データとして受け取る処理
app.use(express.json())

// 現在のポイントを記録する変数
// サーバープログラム内の変数なのでメモリで動いているので再起動すると初期化されますが起動している間は記録してくれています
let recordPoint = 0;

// /api/get というパスで GET リクエストでアクセスするとデータが取得できます
app.get('/api/get', async (req, res) => {
  console.log('/api/get 受信');
  // 受信したデータを表示
  console.log(req.query);

  // Airtable からデータを取得
  let records;
  try {
    records = await base(AIRTABLE_TABLE_NAME).select({
      // ビューはデータの見せ方のこと今回は最初に作られた Grid view で OK
      view: "Grid view"
    }).all();
    // console.log(records);
  } catch (e) {
    console.log(e);
  }

  // 返答データ作成
  let responseData = { "data": [] };
  records.forEach(function (record) {
    // 今回は Data 列を取得
    responseData.data.push(record.get('Data'));
  });

  // res.json はオブジェクトを JSON 形式で返答します
  res.json(responseData)
});

// /api/create というパスで GET リクエストでアクセスすると data パラメータがある場合、データが保存できます
// /api/create?data=A の場合、A が保存されます
app.get('/api/create', async (req, res) => {
  console.log('/api/create 受信');
  // 受信したデータを表示
  // /api/set?data=1
  console.log('受信したデータを表示');
  console.log(req.query);

  // Airtable にデータを保存
  if(req.query.data){
    console.log('データあり');

    const currentData = req.query.data;

    let result;
    try {
      const fields = [
        {
          "fields": {
            "Data": currentData
          }
        }
      ];

      result = await base(AIRTABLE_TABLE_NAME).create(fields);
    } catch (e) {
      console.log(e);
    }
  } else {
    console.log('データなし');
  }
  
  // res.json はオブジェクトを JSON 形式で返答します
  let responseData = { "result": "OK" };
  res.json(responseData)
});

// サーバーを 8080 ポートで起動してログを出力
app.listen(process.env.PORT || 8080, () => {
  console.log(`${path.basename(__filename)} start!`);
  console.log(`app listening at http://localhost:${process.env.PORT || 8080}`)
})
```

✅ポイント
- `const Airtable = require('airtable');` で Airtable のライブラリを読み込んでいます。
  - このライブラリは Airtable が公式でメンテナンスしているライブラリです
    - https://github.com/Airtable/airtable.js
- `AIRTABLE_API_KEY` や `AIRTABLE_BASE_ID` の変数で Base ID や API キーを準備します。
- `const base = new Airtable({ apiKey: AIRTABLE_API_KEY }).base(AIRTABLE_BASE_ID);` で今回の Base が使えるようになります。
- `/api/create` というパスで GET リクエストでアクセスすると data パラメータがある場合、データが保存できます。
- `/api/get` というパスで GET リクエストでアクセスするとデータが取得できます。

## Base ID や API キーの入力

```js
// Airtable API キー
const AIRTABLE_API_KEY = 'AIRTABLE_API_KEY';
// Airtable BASE ID
const AIRTABLE_BASE_ID = 'AIRTABLE_BASE_ID';
// Airtable Table 名
const AIRTABLE_TABLE_NAME = 'Sample01';
```

こちらに Base ID や API キーの入力をします。AIRTABLE_API_KEY には API キー、AIRTABLE_BASE_ID には Base ID を入力しましょう。Airtable Table 名については、すでに今回アクセスする Table 名 `Sample01` が入っています。

設定ができたらサーバの起動です。

## サーバの起動

![0a3a35f3418068b7713ddaa729f2c660](https://i.gyazo.com/0a3a35f3418068b7713ddaa729f2c660.png)

- ターミナルで `node term2-1-chapter02.js` をサーバ起動
- ポートタブで今回のサーバ起動を公開
- シークレットウィンドウで今回のサーバが公開されているか確認します

## データ取得を体験してみる

`/api/get` というパスで GET リクエストでアクセスするとデータが取得できます。

![3d5acaeddc15f2185ddeb90dc7120345](https://i.gyazo.com/3d5acaeddc15f2185ddeb90dc7120345.png)

実際にブラウザでアクセスしてみましょう。このように `{"data":["A","B","C","D"]}` と data というオブジェクトの中に配列でデータが入っています。

![30a0789ab27846655472da09e4e76489](https://i.gyazo.com/30a0789ab27846655472da09e4e76489.png)

Base に入っている Sample01 の Table 内容が表示されています。

## データ追加を体験してみる

`/api/create` というパスで GET リクエストでアクセスすると data パラメータがある場合、データが保存できます。

![7f83b7aa74438e8a067125defa2f23b9](https://i.gyazo.com/7f83b7aa74438e8a067125defa2f23b9.png)

実際に `/api/create?data=Test` でブラウザからアクセスしてみましょう。このように `{"result":"OK"}` と返答が来ます。

![dab681cc1c59529a2bfd055b9f748d76](https://i.gyazo.com/dab681cc1c59529a2bfd055b9f748d76.png)

Base に入っている Sample01 の Table 内容に新しい行が加わっています。

## データ変更を体験してみる

![a05d5d50f448f135154610177daab9e7](https://i.gyazo.com/a05d5d50f448f135154610177daab9e7.png)

たとえば `A` の部分を `てすと` と変更して Base のデータを変更します。

![f4eae1d1353434b85cb1614445bb8387](https://i.gyazo.com/f4eae1d1353434b85cb1614445bb8387.png)

`/api/get` でアクセスしてみて、サーバ側で変更されることを確認してみましょう。

![e28a698e4680da20b73ff7a6904c28d9](https://i.gyazo.com/e28a698e4680da20b73ff7a6904c28d9.png)

Test の行で右クリックして Delete sample をクリックして削除も体験してみましょう。

## そのほかの使い方

![7b5c8cf2b481d875f5f4c7bdf4c60cda](https://i.gyazo.com/7b5c8cf2b481d875f5f4c7bdf4c60cda.png)

Base ID を取得したときにアクセスした API ページ https://airtable.com/developers/web/api/introduction から、各 Base での JavaScript でのアクセスの仕方を確認できます。

![dee00e7a902116f5c1edee747811ed7f](https://i.gyazo.com/dee00e7a902116f5c1edee747811ed7f.png)

✅ポイント
- 更新 Update や 削除 Delete もできます
- RECORD ID が分かれば、検索しなくても名指しで特定データが呼べます
- List で filterByFormula で検索内容を頑張ると特定のデータが呼べます