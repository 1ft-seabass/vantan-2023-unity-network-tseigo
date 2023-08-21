# サーバから動的なデータの取得してみよう

![9d2c38e6fe48e61528f6b2d34370768f](https://i.gyazo.com/9d2c38e6fe48e61528f6b2d34370768f.png)

## この章で学ぶこと

サーバから動的なデータの取得してみます。

## Codespace の起動

![0a3a35f3418068b7713ddaa729f2c660](https://i.gyazo.com/0a3a35f3418068b7713ddaa729f2c660.png)

GitHub にログインした状態で https://github.com/codespaces にアクセスします。

![34de49185c6b28fb938519084d5b36fe](https://i.gyazo.com/34de49185c6b28fb938519084d5b36fe.png)

Codespaces のページです。さきほど使っていた Codespace をクリックして起動します。

## サーバ側の仕組みの説明

今回起動するプログラム `term2-1-chapter03.js` の仕組みを説明します。

```js
// path ライブラリ
const path = require('path');

// Airtable 設定 /////////////////////////////////////////////////////

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

// サーバー設定 ///////////////////////////////////////////////////////

// Express ライブラリの呼び出し
const express = require('express');
// Express ライブラリからサーバーの仕組みを app 変数として呼び出す
const app = express();

// public フォルダ内にあるファイルはパスが一致していると呼びだせます
// /index.html や / の場合は public フォルダ内の index.html が表示されます
app.use(express.static(__dirname + '/public'));

// POST データを受け取る際に必要な処理
app.use(express.urlencoded({ extended: true }));
// データを JSON データとして受け取る処理
app.use(express.json())

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

// サーバーを 8080 ポートで起動してログを出力
app.listen(process.env.PORT || 8080, () => {
  console.log(`${path.basename(__filename)} start!`);
  console.log(`app listening at http://localhost:${process.env.PORT || 8080}`)
})
```

✅ポイント
- 前回の `term2-1-chapter02.js` と同じ仕組みで `/api/get` でのデータ取得だけにしています。
- Airtable の Base ID や API キーの設定に慣れるようシンプルにしてます

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

- ターミナルで `node term2-1-chapter03.js` をサーバ起動
- ポートタブで今回のサーバ起動を公開
- シークレットウィンドウで今回のサーバが公開されているか確認します

## Unity プロジェクトを削除

![5a66450b5365263705111d3910b4c08b](https://i.gyazo.com/5a66450b5365263705111d3910b4c08b.png)

現在作業しているフォルダを削除します。この場所を覚えておいて再度置けるようにしましょう。

## Unity プロジェクトをダウンロード

![d2e14eaab7e66332b09a2086fa5b767e](https://i.gyazo.com/d2e14eaab7e66332b09a2086fa5b767e.png)

今回の教材の Unity プロジェクトを https://github.com/1ft-seabass/vantan-unity-network-project-01 にブラウザからアクセスします。

![c21bb001f1a904122fa2bd6065f2e437](https://i.gyazo.com/c21bb001f1a904122fa2bd6065f2e437.png)

Code ボタンをクリックして Local タブから Download ZIP をクリックしてダウンロードします。

![acd4f7e6c79f434770632f77b16f34b3](https://i.gyazo.com/acd4f7e6c79f434770632f77b16f34b3.png)

ダウンロードできたら ZIP ファイルを、ダブルクリックして ZIP の中身をエクスプローラで表示します。

![9fd6e42489c174d3aa6b44eb4c196bb8](https://i.gyazo.com/9fd6e42489c174d3aa6b44eb4c196bb8.png)

ZIP ファイル直下に vantan-unity-network-project-01-main というフォルダがあります。

![8bb21ae532d5de43c4dc20cdeb932efc](https://i.gyazo.com/8bb21ae532d5de43c4dc20cdeb932efc.png)

このフォルダを選択して、作業フォルダにドラッグアンドドロップしましょう。

![40f366c8c40c7154f475820f5da0d16f](https://i.gyazo.com/40f366c8c40c7154f475820f5da0d16f.png)

フォルダの中身はには、このように Unity プロジェクトそのものがあり Assets や Packages などのファイルがある状況です。

## Unity プロジェクトを Unity Hub から開く

![204afd35cc70224251ca41321b6c1e31](https://i.gyazo.com/204afd35cc70224251ca41321b6c1e31.png)

Unity Hub を開きます。

![38284ca9eeeb4b4b85b1d4717acc716f](https://i.gyazo.com/38284ca9eeeb4b4b85b1d4717acc716f.png)

Open ボタンをクリックします。

![1e463774b96f38951a39ac5ba5135d2f](https://i.gyazo.com/1e463774b96f38951a39ac5ba5135d2f.png)

フォルダ選択で vantan-unity-network-project-01-main フォルダを選択して Open ボタンをクリックします。

![6085e7572e7f03a32f88c6e49c8792b0](https://i.gyazo.com/6085e7572e7f03a32f88c6e49c8792b0.png)

プロジェクトが読み込まれます。

![2b745e107ff5991957e1a4ad5d86fff4](https://i.gyazo.com/2b745e107ff5991957e1a4ad5d86fff4.png)

プロジェクトが表示されました。現時点で、授業用のシーンではなく Untitled になっているのは問題ないです。

![930d6df890c0e10f92ad28c4fc3e4987](https://i.gyazo.com/930d6df890c0e10f92ad28c4fc3e4987.png)

コンソールでこのようなエラーが出るのも問題ないです。

## 今回の Unity シーンを起動

![6049726527f3133083e8ca07d1e6261c](https://i.gyazo.com/6049726527f3133083e8ca07d1e6261c.png)

Project タブから Assets > Scenes を選択します。Scene-Term2-1-Chapter03 をダブルクリックして起動しましょう。

今日は、このプログラムをベースに、送る値や受け取る値を Unity に使っていきます。

✅ポイント
- Cube に Term2_1_Chapter03_CubeEvent01 が割り当てられているのでこちらでつないでみましょう
- Term2_1_Chapter03_CubeEvent01_OK_Sample に正解が入っていますが、どうしてもうまくいかないときに見てみましょう。

## 久々なのでウォームアップ

![ab0a5d229a906401ca2458c5afb42397](https://i.gyazo.com/ab0a5d229a906401ca2458c5afb42397.png)

授業も久々なのでおさらいもかねて、プログラムを書いていく形でウォームアップしてみましょう。

## まず API につないでみましょう

![02db792fd629a56812a205234a08ae44](https://i.gyazo.com/02db792fd629a56812a205234a08ae44.png)

JSON データは気にせず、まずつないでみましょう。

```csharp
IEnumerator GetData()
{
    // HTTP リクエストする(GET メソッド) UnityWebRequest を呼び出し
    // アクセスする先は変数 urlGitHub で設定
    UnityWebRequest request = UnityWebRequest.Get(urlAPI);
```

今回は サーバーURL + /api/get を読み込みます。urlAPI 変数をうまく変更してつないでみましょう。

## データの内容を見つつ JSON データを取り出せるようにする

![02db792fd629a56812a205234a08ae44](https://i.gyazo.com/02db792fd629a56812a205234a08ae44.png)

うまくつながるとコンソールでデータが見ることができます。

今回は `{"data":["A","B","C","D"]}` という data のオブジェクトの中に配列が入っています。

JSON データでの配列は Unity では List 型で変換できます。

```csharp
// 受信した JSON データを Unity で扱うデータにする ResponseData ベースクラス
// 今回は {"data":["A","B","C","D"]} という data のオブジェクトの中に配列が入っています
[Serializable]
public class ResponseData
{
    
}
```

こちらの内容を変更してみましょう。

## データをリストアップしてみる

![02db792fd629a56812a205234a08ae44](https://i.gyazo.com/02db792fd629a56812a205234a08ae44.png)

```csharp
// ResponseData クラスで Unity で扱えるデータ化
ResponseData response = JsonUtility.FromJson<ResponseData>(request.downloadHandler.text);

// データを一つずつログに出す
```

`// データを一つずつログに出す` の部分で、JSON データを List で取り出せた内容をログで表示してみましょう。

## Unity だけでもアクセスできるが、悩ましい点がある

![40ee748630dfef0b75f3f18414363382](https://i.gyazo.com/40ee748630dfef0b75f3f18414363382.png)

✅ポイント
- URL で直接アクセスできる手法はある
- ただしこの場合だと API キーが Unity に残ってしまい漏洩の可能性がある
- 今回のようにサーバー側で直接の接続を行って中継してやることでリスクを避ける狙いもある
- Airtable のライブラリが JavaScript で対応しやすいのでサーバーを JavaScript で行うという意図もある
- 非公式の有志でつくられている Unity から直接扱える https://github.com/lipemon1/airtableunity みたいな仕組みもある模様