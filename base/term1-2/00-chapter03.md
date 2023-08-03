# JSON データ取得について学ぼう

![9d2c38e6fe48e61528f6b2d34370768f](https://i.gyazo.com/9d2c38e6fe48e61528f6b2d34370768f.png)

## この章で学ぶこと

JSON データ取得について学びます。

## JSON とは

![63ab2988b4cf0591e5dd408ad473bb4e](https://i.gyazo.com/63ab2988b4cf0591e5dd408ad473bb4e.png)

JSON は JavaScript Object Notation（JSON、ジェイソン）はデータ記述言語の1つです。JSON は JavaScript オブジェクトにとても似ている形式の文字列です。

といっても、みなさんの中には JavaScript を知っているわけではない人も多いと思うので、Unity で使う基本データ型（文字列、数値、配列、論理型やその他のリテラル型）を使うことができて、柔軟にデータを表現することができると覚えておきましょう。

たとえば、このようなデータがあるとします。プロパティ名は Unity でも使われている、オブジェクトのプロパティの名前と同じ役割です。

- プロパティ名は「number」
  - 値は、整数の 1
- プロパティ名は「float」
  - 値は、浮動小数点の 23.4
- プロパティ名は「bool_ok」
  - 値は、真偽値の true
- プロパティ名は「name」
  - 値は、文字列の MyName

こちらは JSON データでは以下で表現できます。

![3484da3d26f272ede691d421f73da1b9](https://i.gyazo.com/3484da3d26f272ede691d421f73da1b9.png)

このようなデータです。これから話すために分かりやすく、少し色を付けます。

![19cea4e2d46d153eb0f9e423e98b41a5](https://i.gyazo.com/19cea4e2d46d153eb0f9e423e98b41a5.png)

```js
{
  "number":1,
  "float":23.4,
  "bool_ok":true,
  "name":"MyName"
}
```

このようなルールでデータが作られています。

![30c03f890ae6f717ab9fd2effb89b3e1](https://i.gyazo.com/30c03f890ae6f717ab9fd2effb89b3e1.png)

Unity で受信したときに扱える JSON は `{` と `}` で囲われたオブジェクト型ではじまっています。

![fae9f572145e6e8efad9b8056551657f](https://i.gyazo.com/fae9f572145e6e8efad9b8056551657f.png)

ここでいう `"number"` ・ `"float"` ・ `"bool_ok"`・ `"name"` が、値の名前（プロパティ名）です。ダブルクォーテーションで囲んだ名称にします。Unity で読み込まれたとき、変数名として扱われます。

![715d8b39d9e5d1ed217095505da4cb91](https://i.gyazo.com/715d8b39d9e5d1ed217095505da4cb91.png)

それぞれの値の名前（プロパティ名）に対応した値は `:` で区切って設定しています。

![666b08142ec856ff892179e2364b35ba](https://i.gyazo.com/666b08142ec856ff892179e2364b35ba.png)

青文字の部分が、各プロパティの実際の値です

以下のような型表現ができます。ひとまず、Unity でも理解しやすい number の整数・浮動小数点, string , 理論値 boolean, 文字列が理解できていれば OK です。

ちょっと array と object は、はじめは難しい。

- number 型
  - 整数を表現。たとえば、整数の 1 は `1` と記述する。
    - 今回の `"number":1`
  - 浮動小数点数。たとえば、浮動小数点数の 23.4は `23.4` と記述する。
    - 今回の `"float":23.4`
  - 10 進法のみですが指数も表現できます。
- string 型
  - 文字列を表現。たとえば、文字列の MyName は `"MyName"` と記述する。
    - 今回の `"name":"MyName"`
- null 型
  - null を表現。小文字で `null` と記述する。
- true 型
  - 理論値 true を表現。小文字で `true` と記述する。
  - 今回の `"bool_ok":true`
- false 型
  - 理論値 false を表現。小文字で `false` と記述する。
- array 型
  - JavaScript でいう配列型を表現。値を `[]` でくくる。たとえば、a と b と c の文字列の入ったの配列は `["a","b","c"]` と記述する。
  - Unity C# でいうと List 型に近いものです
- object 型
  - JavaScript でいうオブジェクト型を表現。値を `{}` でくくる。プロパティ名はダブルクォーテーションで文字列として記述して、値は前述の各型で記述する。
  - JSON データもオブジェクトではじまっているとも言えます。

![6c9cb3ece828fd3ebec43b869a97dbf3](https://i.gyazo.com/6c9cb3ece828fd3ebec43b869a97dbf3.png)

そして、各プロパティはカンマで区切られます。末尾にはカンマは入れません。

✅参考文献
- JSON の操作 - ウェブ開発を学ぶ | MDN
  - https://developer.mozilla.org/ja/docs/Learn/JavaScript/Objects/JSON
- JavaScript Object Notation - Wikipedia
  - https://ja.wikipedia.org/wiki/JavaScript_Object_Notation
- JSON - JavaScript | MDN
  - https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/JSON

✅補足
- `[` と `]` で配列ではじまる JSON も表現できますが Unity で受け取ったときに、ひと手間かかるデータなので、一旦ここでは割愛します。

## JSON データに慣れよう

![25365ec06cac99fdaecaf0d97df14a34](https://i.gyazo.com/25365ec06cac99fdaecaf0d97df14a34.png)

✅参考文献
- JSON - JavaScript | MDN
  - https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/JSON

こちらの文献でも紹介されている JSON Parser https://jsonparser.org/ というツールで、少し JSON データに慣れてみましょう。

### 例題 1

```js
{
  "number":1,
  "float":23.4,
  "bool_ok":true,
  "name":"MyName"
}
```

こちらを左側にコピーペーストして、JSON Parse ボタンをクリックして JSON 構造を体験します。

### 例題 2

「価格が 500 円」

価格を示すプロパティ名は英語 price に置き換えて表現してみましょう。

<details>
<summary>答え（出題中は開かないでくださいね）</summary>
<pre style="position: relative;"><code class="lang-js">{"price":"500"}
</code></pre>
</details>

### 例題 3

「自分の名前」

名前を示すプロパティ名は英語 name に置き換えて表現してみましょう。

<details>
<summary>答え（出題中は開かないでくださいね）</summary>
<pre style="position: relative;"><code class="lang-js">{"name":"たなかせいご"}
</code></pre>
</details>

### 例題 4

「緯度が 35.681236 経度が 139.767125 の場所の名前が東京タワー」

- 緯度を示すプロパティ名は latitude
- 経度を示すプロパティ名は longitude
- 場所を示すプロパティ名は placeName

<details>
<summary>答え（出題中は開かないでくださいね）</summary>
<pre style="position: relative;"><code class="lang-js">{
{
  "latitude":35.681236,
  "longitude":139.767125,
  "placeName":"東京タワー"
}
</code></pre>
</details>


## データ表現例

いくつかのデータ例を元に JSON でのデータ表現を把握します。

JSON データの構造を、人間の生活や IoT のセンサーや住所などを例にして表現してみました。

### 日時・イベント名

```js
{
  "date": "2023-04-08T07:19:56+09:00",
  "eventName": "バースデーパーティー"
}
```

### たまご・ぶどう・肉などの買い物リスト

```js
{
  "shoppingList": [
    {
      "name": "たまご",
      "quantity": 12
    },
    {
      "name": "ぶどう",
      "quantity": 1,
      "unitPrice": 200,
      "currency": "JPY"
    },
    {
      "name": "肉",
      "quantity": 2,
      "unitPrice": 1000,
      "currency": "JPY"
    }
  ]
}
```

### 温度センサーの1回の値（小数点第一位まで）

```js
{
  "temperatureSensorValue": {
    "value": 25.5,
    "unitOfMeasurement": "℃"
  }
}
```

### Windows PC 商品名・メーカー名・型番・価格・消費税

```js
{
  "productDetails": {
    "productName": "Hyper Laptop Z 2930",
    "manufacturerName": "PC Paradise",
    "modelNumber": "HL-Z-2930-BK",
    "priceDetails": {
      "priceAmount": 200000,
      "currencyCode": "JPY",
      "taxDetails": {
        "taxAmount": 20000,
        "taxRatePercentage": 10
      }
    }
  }
}
```

## JSON データの送信や受け取ったデータの JSON 解析は JsonUtility

![305255eea1072f3becd161d1df9a5755](https://i.gyazo.com/305255eea1072f3becd161d1df9a5755.png)

JSON データの送信や受け取ったデータの JSON 解析は、Unity でビルドインされている JsonUtility が便利です。

- JSON 形式にシリアライズ - Unity マニュアル
  - https://docs.unity3d.com/ja/2018.4/Manual/JSONSerialization.html
- JsonUtility-FromJson - Unity スクリプトリファレンス
  - https://docs.unity3d.com/ja/2018.4/ScriptReference/JsonUtility.FromJson.html
  - 受け取った JSON データ「から」Unity での構造体に変換します
- JsonUtility-ToJson - Unity スクリプトリファレンス
  - https://docs.unity3d.com/ja/2018.4/ScriptReference/JsonUtility.ToJson.html
  - Unity での構造体を JSON データ「へ」変換します

この章では、シンプルな JSON データをサーバーから受け取って、Unity の型で使える流れを学んでみましょう。

## Codespace の起動

![0a3a35f3418068b7713ddaa729f2c660](https://i.gyazo.com/0a3a35f3418068b7713ddaa729f2c660.png)

GitHub にログインした状態で https://github.com/codespaces にアクセスします。

![34de49185c6b28fb938519084d5b36fe](https://i.gyazo.com/34de49185c6b28fb938519084d5b36fe.png)

Codespaces のページです。さきほど使っていた Codespace をクリックして起動します。

## サーバの起動

![0a3a35f3418068b7713ddaa729f2c660](https://i.gyazo.com/0a3a35f3418068b7713ddaa729f2c660.png)

- ターミナルで `node term1-2-chapter03.js` をサーバ起動
- ポートタブで今回のサーバ起動を公開
- シークレットウィンドウで今回のサーバが公開されているか確認します

こちらの手順を進めます。

✅ポイント
- 今回は GET リクエストで 1 つの仕組みを作っています
- `/api/get/json` というパスで GET リクエストでアクセスすると `{"name":"Box1","name2":"Box2"}}` という JSON データが取得できます
  - これを Unity 内の name というプロパティで扱ってシーンのテキストに反映します

## 今回の Unity シーンを起動

![6049726527f3133083e8ca07d1e6261c](https://i.gyazo.com/6049726527f3133083e8ca07d1e6261c.png)

Project タブから Assets > Scenes を選択します。Scene-Term1-2-Chapter03 をダブルクリックして起動しましょう。

## Term1_2_Chapter03_CubeEvent.cs 変更

`Assets/Scripts/Term1_2_Chapter03_CubeEvent.cs` をエディタで開きます。

```csharp
using UnityEngine;
using UnityEngine.EventSystems;

using System.Collections;       // IEnumerator のための参照
using UnityEngine.Networking;   // UnityWebRequest のための参照
using System;                   // Serializable のための参照

public class Term1_2_Chapter03_CubeEvent : MonoBehaviour, IPointerClickHandler
{
    // JSON データ化する NameData ベースクラス
    [Serializable]
    public class NameData
    {
        // name というプロパティ名で string 型で変換
        public string name;
        // name2 というプロパティ名で string 型で変換
        public string name2;
    }

    // アクセスする URL
    // サーバーURL + /api/get/json でアクセス
    string urlGitHub = "ここにサーバーURLを入れる";

    public void OnPointerClick(PointerEventData eventData)
    {
        // マウスクリックイベント
        // Debug.Log($"オブジェクト {this.name} がクリックされたよ！");

        // HTTP GET リクエストを非同期処理を待つためコルーチンとして呼び出す
        StartCoroutine("GetGitHubData");
    }

    // GET リクエストする本体
    IEnumerator GetGitHubData()
    {
        // HTTP リクエストする(GET メソッド) UnityWebRequest を呼び出し
        // アクセスする先は変数 urlGitHub で設定
        UnityWebRequest request = UnityWebRequest.Get(urlGitHub);

        // リクエスト開始
        yield return request.SendWebRequest();

        // 結果によって分岐
        switch (request.result)
        {
            case UnityWebRequest.Result.InProgress:
                Debug.Log("リクエスト中");
                break;

            case UnityWebRequest.Result.Success:
                Debug.Log("リクエスト成功");

                // コンソールに表示
                Debug.Log($"responseData: {request.downloadHandler.text}");

                // そのうえで ShibaData クラスで JSON データ化
                NameData nameData = JsonUtility.FromJson<NameData>(request.downloadHandler.text);

                // Title にテキスト割り当て
                GameObject.Find("Title").GetComponent<TextMesh>().text = "Loaded!";

                break;
        }


    }
}
```

以下を修正します。

```csharp
// アクセスする URL
// サーバーURL + /api/get/json でアクセス
string urlGitHub = "ここにサーバーURLを入れる";
```

こちらをサーバー URL に `/api/get/json` というパスを加えて変更して保存します。

解説していきます。

```csharp
// JSON データ化する NameData ベースクラス
[Serializable]
public class NameData
{
    // name というプロパティ名で string 型で変換
    public string name;
    // name2 というプロパティ名で string 型で変換
    public string name2;
}
```

まず、JsonUtility.FromJson が JSON データ化する NameData ベースクラスを用意します。これは、このあと受け取る `{"name":"Box1","name2":"Box2"}}` に合わせたものです。

```csharp
using System;                   // Serializable のための参照
```

また、この対応をするために、こちらの関数群も呼び出しています。

```csharp
// そのうえで ShibaData クラスで JSON データ化
NameData nameData = JsonUtility.FromJson<NameData>(request.downloadHandler.text);
```

そのうえで JsonUtility.FromJson 関数で、このように呼び出します。こうすると、ダウンロードしたテキスト `request.downloadHandler.text` を `<NameData>` のところで、さきほどのクラスをひな形にしながら `nameData` という変数に代入します。

これ以降は、うまくロードできれば nameData は NameData 型として扱われるので、コードヒントもしっかり出ます。

![7841c12d92f8e7c2ffb4b5d743532232](https://i.gyazo.com/7841c12d92f8e7c2ffb4b5d743532232.png)

キューブをクリックすると、現在は

```csharp
// Title にテキスト割り当て
GameObject.Find("Title").GetComponent<TextMesh>().text = "Loaded!";
```

となるので `Loaded!` の固定値ですが、

![080db25e7155c27f64dccd36dd9d2c31](https://i.gyazo.com/080db25e7155c27f64dccd36dd9d2c31.png)

`nameData` のあとに `.` と打ち込んで `name` を打ち込んでみると、今回のクラスの値が呼び出せます。

```csharp
// Title にテキスト割り当て
GameObject.Find("Title").GetComponent<TextMesh>().text = nameData.name;
```

と記述して保存して、

![3039cb6387befa4ab05f998ab307caa3](https://i.gyazo.com/3039cb6387befa4ab05f998ab307caa3.png)

このように Box1 という値を呼び出してみましょう。

## まとめ

- JSON データは、データの構造が作れるので様々なデータがやり取りできるようになります
- Unity では JsonUtility クラスがあるのでこれを使って JSON をあつかうことができます

## 今回の Codespace の終了

![0a8b4cfb807e57ea1382292a757c6899](https://i.gyazo.com/0a8b4cfb807e57ea1382292a757c6899.png)

今回の Codespace 終了しておきましょう。