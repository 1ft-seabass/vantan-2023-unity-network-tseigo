# データ活用例を体験 : ユーザー情報

![9d2c38e6fe48e61528f6b2d34370768f](https://i.gyazo.com/9d2c38e6fe48e61528f6b2d34370768f.png)

## この章で学ぶこと

データ活用例の体験として、ユーザー情報としてランキング情報を取得してみます。

## Codespace の起動

![0a3a35f3418068b7713ddaa729f2c660](https://i.gyazo.com/0a3a35f3418068b7713ddaa729f2c660.png)

GitHub にログインした状態で https://github.com/codespaces にアクセスします。

![34de49185c6b28fb938519084d5b36fe](https://i.gyazo.com/34de49185c6b28fb938519084d5b36fe.png)

Codespaces のページです。さきほど使っていた Codespace をクリックして起動します。

## サーバ側の仕組みの説明

今回起動するプログラム `term2-2-chapter03.js` の仕組みを説明します。

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

// /api/get/ranking というパスで GET リクエストでアクセスするとランキングデータが取得できます
app.get('/api/get/ranking', async (req, res) => {
  console.log('/api/get/ranking 受信');
  // 受信したデータを表示
  console.log(req.query);

  // Airtable からデータを取得
  let records;
  try {
    records = await base('PointList').select({
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
    // ランキングとして取りやすくする JSON データを整備
    const rankingData = {
      "Name":record.get('Name'),
      "Point":record.get('Point'),
      "CreatedTime":record.get('CreatedTime')
    }
    responseData.data.push(rankingData);
  });

  // res.json はオブジェクトを JSON 形式で返答します
  res.json(responseData)
});

// /api/post/result というパスで POST リクエストでアクセスすると名前とポイントデータが保存できます
app.post('/api/post/result', async (req, res) => {
  console.log('/api/post/result 受信');
  // 受信したデータを表示
  console.log(req.body);

  // Airtable にデータを保存
  const currentName = req.body.name;
  const currentData = req.body.point;

  let result;
  try {
    const fields = [
      {
        "fields": {
          "Name":currentName,
          "Point": currentData
        }
      }
    ];

    result = await base('PointList').create(fields);
  } catch (e) {
    console.log(e);
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
- `/api/get/ranking` というパスで GET リクエストでアクセスするとランキングデータが取得できます
- `/api/post/result` というパスで POST リクエストでアクセスすると名前とポイントデータが保存できます
- テーブル名は `base('PointList').create(fields);` や `await base('PointList').select(～)` に直接書く形で設定しています

## Base ID や API キーの入力

```js
// Airtable API キー
const AIRTABLE_API_KEY = 'AIRTABLE_API_KEY';
// Airtable BASE ID
const AIRTABLE_BASE_ID = 'AIRTABLE_BASE_ID';
```

こちらに Base ID や API キーの入力をします。AIRTABLE_API_KEY には API キー、AIRTABLE_BASE_ID には Base ID を入力しましょう。

## サーバの起動

![0a3a35f3418068b7713ddaa729f2c660](https://i.gyazo.com/0a3a35f3418068b7713ddaa729f2c660.png)

- ターミナルで `node term2-2-chapter03.js` をサーバ起動
- ポートタブで今回のサーバ起動を公開
- シークレットウィンドウで今回のサーバが公開されているか確認します

## 今回の Unity シーンを起動

![6049726527f3133083e8ca07d1e6261c](https://i.gyazo.com/6049726527f3133083e8ca07d1e6261c.png)

Project タブから Assets > Scenes を選択します。Scene-Term2-2-Chapter03 をダブルクリックして起動しましょう。

今日は、このプログラムをベースに、送る値や受け取る値を Unity に設定していきます。

✅ポイント
- ClickPart には、すでに Term2_2_Chapter03_ClickPart が割り当てられてポイントの加算やリセットを担当しています
- RankingMessage は Term2_2_Chapter03_RankingMessage が割り当てられて、これから書いていきます。出来上がったサンプルは Term2_2_Chapter03_RankingMessage_OK_Sample がありますが、どうしてもわからないときに確認しましょう。
- SendButton は Term2_2_Chapter03_SendButton が割り当てられて、これから書いていきます。出来上がったサンプルは Term2_2_Chapter03_SendButton_OK_Sample がありますが、どうしてもわからないときに確認しましょう。
- 今回、新しく InputField が登場してポイント登録時に自分の名前が設定できるようになっています。

## ランキング表示の API の URL を設定する

![02db792fd629a56812a205234a08ae44](https://i.gyazo.com/02db792fd629a56812a205234a08ae44.png)

```csharp
    // アクセスする URL
    // サーバーURL + /api/get/ranking でアクセス
    string urlAPI = "";;
```

今回はランキング表示は GET リクエストをしています。API の URL を設定しましょう。

## ランキング表示のデータを読み込めるように ResponseData と ResponseDataList を設定しよう

![02db792fd629a56812a205234a08ae44](https://i.gyazo.com/02db792fd629a56812a205234a08ae44.png)

```csharp
    // 受信した JSON データを Unity で扱うデータにする ResponseData ベースクラス
    // 今回は data の中身が配列で、さらに Name , Point , CreatedTime のプロパティが入っているので、List の中身を定義する ResponseDataList 型を作成。
    [Serializable]
    public class ResponseData
    {
        public List<ResponseDataList> data;
    }

    // Name , Point , CreatedTime のプロパティが入っているので、List の中身を定義する ResponseDataList 型を作成
    [Serializable]
    public class ResponseDataList
    {
        
    }
```

今回受け取るデータの例です。

```js
{
    data: [
        {
            Name: "Seigo",
            Point: 5,
            CreatedTime: "2023-08-18T02:18:33.000Z"
        },
        {
            Name: "Seigo",
            Point: 254,
            CreatedTime: "2023-08-18T02:25:01.000Z"
        },
        {
            Name: "Seigo",
            Point: 23,
            CreatedTime: "2023-08-18T02:25:10.000Z"
        }
    ]
}
```

今回は data の中身が配列で、さらに Name , Point , CreatedTime のプロパティが入っているので、List の中身を定義する ResponseDataList 型を作成しています。

List の中身を定義する ResponseDataList 型を作成を、Name , Point , CreatedTime のプロパティが入っている形で設定してみましょう。

## ランキングのテキストを表示してみよう

![02db792fd629a56812a205234a08ae44](https://i.gyazo.com/02db792fd629a56812a205234a08ae44.png)

```csharp
string textRankingList = "[Ranking]\n";

Debug.Log(response.data);

// データを一つずつ反映する
for (int i = 0; i < 3; i++)
{
    ResponseDataList currentLine = response.data[i];

    Debug.Log(currentLine);

    // 文字列を連結
    textRankingList += "";
}

// メッセージに反映
this.transform.GetComponent<TextMesh>().text = textRankingList;
```

データがうまく読み込めて ResponseData と ResponseDataList でさばけるようになると、この部分が動作します。

textRankingList の文字列を調整してランキング表示テキストに反映しましょう。currentLine には ResponseDataList で各行のデータが入っているので、

```csharp
    // 文字列を連結
    textRankingList += "";
```

の文字列を調整して `[1] Seigo 256pt` といった表現をしてみましょう。改行は末尾に `\n` を使いましょう。

## ランキング表示を動かしてみましょう

![02db792fd629a56812a205234a08ae44](https://i.gyazo.com/02db792fd629a56812a205234a08ae44.png)

ここまでできたらランキング表示を動かしてみましょう。

## ポイントデータ記録ボタンで自分の名前を反映

![02db792fd629a56812a205234a08ae44](https://i.gyazo.com/02db792fd629a56812a205234a08ae44.png)

ポイントデータ記録ボタンで自分の名前を反映できるようにしましょう。

```csharp
// 自分の名前を登録
// 固定値でなく InputField から取得する
pointRequestData.name = "Seigo";
```

GameObject InputField から `.GetComponent<InputField>().text` という形で入力フィールドから取得できるので実装してみましょう。

## ポイント登録後にランキングの更新を行う

![02db792fd629a56812a205234a08ae44](https://i.gyazo.com/02db792fd629a56812a205234a08ae44.png)

現在の機能だとポイント登録後にランキングの更新が行われません。ランキングを更新しましょう。

```csharp
// RankingMessage で最新データを取得
// GetDataCore を動かす

```

のところで RankingMessage から Term2_2_Chapter03_RankingMessage クラスにある GetDataCore を実行してみましょう。

## 何度か動かしてみましょう

![02db792fd629a56812a205234a08ae44](https://i.gyazo.com/02db792fd629a56812a205234a08ae44.png)

この状態だと、Airtable 側でデータが更新されるのですが、ランキングにはデータの行順で表示されてしまうので、新しいデータが表示されません。調整していきましょう。

## Airtable 側のビューでソート（並び替え）機能で登録順やポイント順にしてみる

![02db792fd629a56812a205234a08ae44](https://i.gyazo.com/02db792fd629a56812a205234a08ae44.png)

Airtable がデータをいろいろな並び順や見せ方をすることができます。今回はデフォルトにある Grid view を調整してみましょう。

![8ab616114bebe1f9c921459eaf86f5d7](https://i.gyazo.com/8ab616114bebe1f9c921459eaf86f5d7.png)

Sort ボタンで CreatedTime を 9→1 （最新順）にしてみて Unity で表示してみましょう。

![c766bbfd25680703d8c1b940569c7b1d](https://i.gyazo.com/c766bbfd25680703d8c1b940569c7b1d.png)

Point を 9→1 （多い順）にしてみて Unity で表示してみましょう。

もし Unity 側でこういった対応をするには繰り返し処理などで手間がかかりますが、Airtable 側でデータはそのままにビューで表現できれば、うまくランキング表示が実装できます。

ビューをどう狙っているかというと、

```js
  // Airtable からデータを取得
  let records;
  try {
    records = await base('PointList').select({
      // ビューはデータの見せ方のこと今回は最初に作られた Grid view で OK
      view: "Grid view"
    }).all();
    // console.log(records);
  } catch (e) {
    console.log(e);
  }
```

サーバ側で select の処理をするときに `view: "Grid view"` といった形でビュー名を読んでいます。もちろん、Airtable で新たなビューを作って呼び出せば、その時に応じたビューが呼び出せます。