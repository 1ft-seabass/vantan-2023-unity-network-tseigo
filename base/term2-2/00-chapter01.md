# サーバから動的なデータを表示してみよう

![9d2c38e6fe48e61528f6b2d34370768f](https://i.gyazo.com/9d2c38e6fe48e61528f6b2d34370768f.png)

## この章で学ぶこと

サーバから動的なデータを表示してみます。

- Airtable 変更後のデータ反映をみる

## Airtable に新しい Table を作る

今回は Airtable に色に示す Color という値が並んでいる Table を作って反映します。

以下の手順で新しい　Table を作りましょう。

- `+ Add or import` ボタンをクリックして Create blank table ボタンをクリックします。
- テーブル名を聞かれるので `Sample02` として Save ボタンをクリックします。
- Table ができあがったら、最初に作られているフィールド Notes, Assignee, Status を削除します。

![4ba2126a27e4b998e9a51efbc7eeff18](https://i.gyazo.com/4ba2126a27e4b998e9a51efbc7eeff18.png)

フィールド名を Name から Color に変更します。

![b19a1dd998ce04587a9a31fad161a4cb](https://i.gyazo.com/b19a1dd998ce04587a9a31fad161a4cb.png)

- フィールドの＋ボタンをクリックしてフィールドをひとつ加えます。
- フィールド名は ID 、フィールドタイプは Formula 、式は `RECORD_ID()` を入力します。

![dc4c3a9d34239d38f3c0a75869c76147](https://i.gyazo.com/dc4c3a9d34239d38f3c0a75869c76147.png)

このように Table ができました。

![861ed5323d25a26efd28286fdc149b43](https://i.gyazo.com/861ed5323d25a26efd28286fdc149b43.png)

最後に、このように Red Yellow Blue と値を入力しておきます。

✅ポイント
- もし Airtable 操作を思い出せなかったら [Table を新しく作ってみる](../term2-1/00-chapter01.md) をおさらいしてみましょう。

## Codespace の起動

![0a3a35f3418068b7713ddaa729f2c660](https://i.gyazo.com/0a3a35f3418068b7713ddaa729f2c660.png)

GitHub にログインした状態で https://github.com/codespaces にアクセスします。

![34de49185c6b28fb938519084d5b36fe](https://i.gyazo.com/34de49185c6b28fb938519084d5b36fe.png)

Codespaces のページです。さきほど使っていた Codespace をクリックして起動します。

## サーバ側の仕組みの説明

今回起動するプログラム `term2-2-chapter01.js` の仕組みを説明します。

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
const AIRTABLE_TABLE_NAME = 'Sample02';

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
    responseData.data.push(record.get('Color'));
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
- 前章で作られた仕組みとかなり近いものです
- 今回は `responseData.data.push(record.get('Color'));` となっていて Color の列を読み込むように設定しています

## Base ID や API キーの入力

```js
// Airtable API キー
const AIRTABLE_API_KEY = 'AIRTABLE_API_KEY';
// Airtable BASE ID
const AIRTABLE_BASE_ID = 'AIRTABLE_BASE_ID';
// Airtable Table 名
const AIRTABLE_TABLE_NAME = 'Sample02';
```

こちらに Base ID や API キーの入力をします。AIRTABLE_API_KEY には API キー、AIRTABLE_BASE_ID には Base ID を入力しましょう。Airtable Table 名については、すでに今回アクセスする Table 名 `Sample02` が入っています。

設定ができたらサーバの起動です。

## サーバの起動

![0a3a35f3418068b7713ddaa729f2c660](https://i.gyazo.com/0a3a35f3418068b7713ddaa729f2c660.png)

- ターミナルで `node term2-2-chapter01.js` をサーバ起動
- ポートタブで今回のサーバ起動を公開
- シークレットウィンドウで今回のサーバが公開されているか確認します

## 今回の Unity シーンを起動

![6049726527f3133083e8ca07d1e6261c](https://i.gyazo.com/6049726527f3133083e8ca07d1e6261c.png)

Project タブから Assets > Scenes を選択します。Scene-Term2-2-Chapter01-1 をダブルクリックして起動しましょう。

今日は、このプログラムをベースに、送る値や受け取る値を Unity に使っていきます。

✅ポイント
- GetAPI に Term2_1_Chapter03_GetAPI が割り当てられているのでこちらでつないでみましょう
- Term2_1_Chapter03_GetAPI_OK_Sample に正解が入っていますが、どうしてもうまくいかないときに見てみましょう。

## JSON データを受け取って Unity で使えるようにしましょう

![02db792fd629a56812a205234a08ae44](https://i.gyazo.com/02db792fd629a56812a205234a08ae44.png)

- サーバから `サーバーURL + /api/get` を読み込みます。urlAPI 変数をうまく変更してつないでみましょう。
- 今回は `{"data":["Red","Yello","Blue"]}` という data のオブジェクトの中に配列が入っています。
  - JSON データでの配列は Unity では List 型で変換できます。受信した JSON データを Unity で扱うデータにする ResponseData ベースクラスを調整しましょう。

## 各 Cube にテキストで Color 値を割り振る

![02db792fd629a56812a205234a08ae44](https://i.gyazo.com/02db792fd629a56812a205234a08ae44.png)

```csharp
// データを一つずつ反映する
for (int i = 0; i < 3; i++)
{
    
}
```

JSON データを Unity データで扱えるようになったあと、各 Cube にテキストで Color 値を割り振れるように for 文を用意しています。 Cube 内の MessageText という TextMesh にテキストを反映してみましょう。

## 各 Cube に Color 値によって Cube の色を変更してみましょう

![02db792fd629a56812a205234a08ae44](https://i.gyazo.com/02db792fd629a56812a205234a08ae44.png)


各 Cube に Color 値によって Cube の色を変更してみましょう。

ヒント : https://docs.unity3d.com/ja/2021.2/ScriptReference/Material-color.html

## ややリアルタイム反映を作ってみよう

![02db792fd629a56812a205234a08ae44](https://i.gyazo.com/02db792fd629a56812a205234a08ae44.png)

ここまでできると、Start 関数で GetDataCore を呼び出すことで最初の表示時に動作する流れを、InvokeRepeating 関数を使えば、Airtable で値を変更するとリアルタイムに値が変わるようにできます。

- InvokeRepeating
  - https://docs.unity3d.com/ja/2018.4/ScriptReference/MonoBehaviour.InvokeRepeating.html

とはいえ Airtable の API の制限を超えないようにアクセスしましょう。

![c0d5c21fd21b6037f7cf011905ddef34](https://i.gyazo.com/c0d5c21fd21b6037f7cf011905ddef34.png)

2023 年現在 Airtable API の Rate Limit https://airtable.com/developers/web/api/rate-limits は「Base 1 つあたり 1 秒間 5 回まで」です。かなり太っ腹なので `InvokeRepeating("GetDataCore", 1.0f, 1.0f);` で、第 2 引数は 1 秒後開始を意味していて、第 3 引数は 1 秒ごと実行される指定でやってみましょう。

```csharp
void Start()
{
    // 開始時に読み込み開始
    // GetDataCore();

    InvokeRepeating("GetDataCore", 1.0f, 1.0f);
}
```

このように GetDataCore の直実行をコメントアウトして InvokeRepeating を指定してみましょう。