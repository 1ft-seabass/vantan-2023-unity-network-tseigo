# 他のデータも色々と記録してみよう

![9d2c38e6fe48e61528f6b2d34370768f](https://i.gyazo.com/9d2c38e6fe48e61528f6b2d34370768f.png)

## この章で学ぶこと

他のデータも色々と記録してみます。

## Airtable に新しい Table を作る

今回はクリックしたポイントを記録する Table を作ります。

以下の手順で新しい　Table を作りましょう。

- `+ Add or import` ボタンをクリックして Create blank table ボタンをクリックします。
- テーブル名を聞かれるので `PointList` として Save ボタンをクリックします。
- Table ができあがったら、最初に作られているフィールド Notes, Assignee, Status を削除します。

![c6e123eceef7d6efb0023be9472f207b](https://i.gyazo.com/c6e123eceef7d6efb0023be9472f207b.png)

フィールド名 Name はそのまま使います。

![e0f5b71d7dd01bcbd7e88c0dae923b5a](https://i.gyazo.com/e0f5b71d7dd01bcbd7e88c0dae923b5a.png)

- フィールドの＋ボタンをクリックしてフィールドをひとつ加えます。
- フィールド名は Point 、フィールドタイプは Number にします。
- Formatting は Integer にします。

![b19a1dd998ce04587a9a31fad161a4cb](https://i.gyazo.com/b19a1dd998ce04587a9a31fad161a4cb.png)

- フィールドの＋ボタンをクリックしてフィールドをひとつ加えます。
- フィールド名は ID 、フィールドタイプは Formula 、式は `RECORD_ID()` を入力します。

![47d008ed4db43c6a297c973a1f50e595](https://i.gyazo.com/47d008ed4db43c6a297c973a1f50e595.png)

- フィールドの＋ボタンをクリックしてフィールドをひとつ加えます。
- フィールド名は CreatedTime 、フィールドタイプは Created time にします。

![9f71fcde11e0a8d46513e481b7288959](https://i.gyazo.com/9f71fcde11e0a8d46513e481b7288959.png)

Date format や Time format はそのままで Create field をクリックします。

![a0e77608c2d441751cd1f9ddabf12d81](https://i.gyazo.com/a0e77608c2d441751cd1f9ddabf12d81.png)

このような Table ができました。

## Codespace の起動

![0a3a35f3418068b7713ddaa729f2c660](https://i.gyazo.com/0a3a35f3418068b7713ddaa729f2c660.png)

GitHub にログインした状態で https://github.com/codespaces にアクセスします。

![34de49185c6b28fb938519084d5b36fe](https://i.gyazo.com/34de49185c6b28fb938519084d5b36fe.png)

Codespaces のページです。さきほど使っていた Codespace をクリックして起動します。

## サーバ側の仕組みの説明

今回起動するプログラム `term2-2-chapter02.js` の仕組みを説明します。

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

// /api/post/result というパスで POST リクエストでアクセスするとポイントデータが保存できます
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

✅ポイント TODO
- 今回は `await base('PointList').create(fields)` の部分で PointList を名指しでデータを呼び出しています。AIRTABLE_TABLE_NAME のような固定値を用意してません。
- `/api/post/result` というパスで POST リクエストでアクセスするとポイントデータが保存できます

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

- ターミナルで `node term2-2-chapter02.js` をサーバ起動
- ポートタブで今回のサーバ起動を公開
- シークレットウィンドウで今回のサーバが公開されているか確認します

## 今回の Unity シーンを起動

![6049726527f3133083e8ca07d1e6261c](https://i.gyazo.com/6049726527f3133083e8ca07d1e6261c.png)

Project タブから Assets > Scenes を選択します。Scene-Term2-2-Chapter02 をダブルクリックして起動しましょう。

今日は、このプログラムをベースに、送る値や受け取る値を Unity に設定していきます。

✅ポイント
- SendButton に Term2_2_Chapter02_SendButton が割り当てられているのでこちらでつないでみましょう
- 今回は POST リクエストで API とやり取りするサンプルです。
- Term2_2_Chapter02_SendButton_OK_Sample に正解が入っていますが、どうしてもうまくいかないときに見てみましょう。

## API の URL を設定する

![02db792fd629a56812a205234a08ae44](https://i.gyazo.com/02db792fd629a56812a205234a08ae44.png)

```csharp
// アクセスする URL
// サーバーURL + /api/post/result でアクセス
string urlGitHub = "";
```

今回は POST 送信をしています。API の URL を設定しましょう。

## 現在のポイントを送れるようにする

PointRequestData に追記して現在のポイントを int 型で point 値に割り当てて送信できるようにしましょう。

![02db792fd629a56812a205234a08ae44](https://i.gyazo.com/02db792fd629a56812a205234a08ae44.png)

```csharp
// 送信する Unity データを JSON データ化する PointRequestData ベースクラス
[Serializable]
public class PointRequestData
{
    
}
```

こちらに準備しつつ

```csharp
// PointRequestData ベースクラスを器として呼び出す
PointRequestData pointRequestData = new PointRequestData();
// データを設定
// 現在のポイントを得る

// 自分の名前を登録

```

に、値の設定をするようにします。

## 自分の名前を送れるようにする

PointRequestData に追記して現在のポイントを string 型で name 値に割り当てて送信できるようにしましょう。今回は固定値で自分の名前にします。

![02db792fd629a56812a205234a08ae44](https://i.gyazo.com/02db792fd629a56812a205234a08ae44.png)


```csharp
// 送信する Unity データを JSON データ化する PointRequestData ベースクラス
[Serializable]
public class PointRequestData
{
    
}
```

こちらに準備しつつ

```csharp
// PointRequestData ベースクラスを器として呼び出す
PointRequestData pointRequestData = new PointRequestData();
// データを設定
// 現在のポイントを得る

// 自分の名前を登録

```

に、値の設定をするようにします。

## 実際に送ってみて確認する

![cdc6617c072b939cb86336decc3fc433](https://i.gyazo.com/cdc6617c072b939cb86336decc3fc433.png)

クリックしてポイントを増やして結果を送信してみましょう。

![e9e40a1928a4f49ef2af153b83268020](https://i.gyazo.com/e9e40a1928a4f49ef2af153b83268020.png)

このようにデータがどんどん記録されていることを確認しましょう。