# いろいろとデータを調整する

![9d2c38e6fe48e61528f6b2d34370768f](https://i.gyazo.com/9d2c38e6fe48e61528f6b2d34370768f.png)

## この章で学ぶこと

いろいろとデータを調整する

- シンプルに動かしてみる
- 受け取ったデータをあいさつ文テキストに反映してみる（ResponseData.title）
- 自分の名前を送っていてサーバーであいさつ文を作っていることを確認（RequestData.name）
- 受け取ったデータをポイント加算に反映してみる（ResponseData.add_point）
- 実は term1-2 chapter02 のデータを JSON でまとめたことを確認
- ゲームポイントの記録を確認（RequestData.point）
- ゲームポイントの記録が成功すると記録ポイントが返ってくるのでテキストに反映してみる（ResponseData.recordPoint）
- 初期起動時の API で記録ポイントが表示されていることを確認
- 実はサーバーが起動している間、記録ポイントは保持されていることを確認
- 初期起動時に受け取った記録ポイントを反映すれば再開できることを確認
- 再起動して記録ポイントが初期化されることも確認

## Codespace の起動

![0a3a35f3418068b7713ddaa729f2c660](https://i.gyazo.com/0a3a35f3418068b7713ddaa729f2c660.png)

GitHub にログインした状態で https://github.com/codespaces にアクセスします。

![34de49185c6b28fb938519084d5b36fe](https://i.gyazo.com/34de49185c6b28fb938519084d5b36fe.png)

Codespaces のページです。さきほど使っていた Codespace をクリックして起動します。

## サーバの起動

![0a3a35f3418068b7713ddaa729f2c660](https://i.gyazo.com/0a3a35f3418068b7713ddaa729f2c660.png)

- ターミナルで `node term1-3-chapter02.js` をサーバ起動
- ポートタブで今回のサーバ起動を公開
- シークレットウィンドウで今回のサーバが公開されているか確認します

こちらの手順を進めます。

✅ポイント
- 今回は POST リクエストで 2 つの仕組みを作っています
- `/api/post/result` というパスでは、現在のポイント受信して記録。さらに今記録したものを返答。
- `/api/post/init` というパスでは、初回ロード時にいろいろな情報をもらいます。
- `recordPoint` という現在のポイントを記録する変数もあります。
  - サーバープログラム内の変数なのでメモリで動いています
  - これはサーバを再起動すると初期化されますが起動している間は記録してくれています
- 受信した現在のポイントを記録にも注目
- あいさつ文の値の流れにも注目

## 今回の Unity シーンを起動

![6049726527f3133083e8ca07d1e6261c](https://i.gyazo.com/6049726527f3133083e8ca07d1e6261c.png)

Project タブから Assets > Scenes を選択します。Scene-Term1-3-Chapter02 をダブルクリックして起動しましょう。

今日は、このプログラムをベースに、送る値や受け取る値を Unity に使っていきます。

✅ポイント
- ClickPart が Term1-2 Chapter02 に近い仕組みでクリックしたらポイントが加算されたり、初回ロード時にいろいろな情報をサーバの `/api/post/init` から受け取っています。
- SendButton が Term1-3 Chapter01 とほぼ同じ仕組みで ClickPart の得たポイントをサーバの `/api/post/result` に送っています。

## Term1_3_Chapter02_ClickPart.cs 変更

`Assets/Scripts/Term1_3_Chapter02_ClickPart.cs` をエディタで開きます。

```csharp
using UnityEngine;
using UnityEngine.EventSystems;

using System.Collections;       // IEnumerator のための参照
using UnityEngine.Networking;   // UnityWebRequest のための参照
using System.Text;              // Encoding のための参照
using System;                   // Serializable のための参照

public class Term1_3_Chapter02_ClickPart : MonoBehaviour, IPointerClickHandler
{
    // 受信した JSON データを Unity で扱うデータにする ResponseData ベースクラス
    [Serializable]
    public class ResponseData
    {
        // result というプロパティ名で string 型で変換
        public string result;
    }

    // 送信する Unity データを JSON データ化する RequestData ベースクラス
    [Serializable]
    public class RequestData
    {   
        // 自分の名前
        // name というプロパティ名で string 型で変換
        public string name;
    }

    // アクセスする URL
    // サーバー URL + /api/post/init
    string urlGitHub = "ここにサーバーURLを入れる";

    // ポイント加算設定
    int addPoint = 1;

    // 蓄積ポイント
    public int currentPoint = 0;

    void Start()
    {
        // 起動時にデータを読み込む

        // HTTP リクエストを非同期処理を待つためコルーチンとして呼び出す
        StartCoroutine("RequestInit");

        // 蓄積ポイントのリセット
        currentPoint = 0;
    }

    public void OnPointerClick(PointerEventData eventData)
    {
        // マウスクリックイベント
        // Debug.Log($"オブジェクト {this.name} がクリックされたよ！");

        // ポイント加算
        currentPoint += addPoint;

        // テキストに反映
        string infomation = currentPoint + "pt";
        GameObject.Find("CurrentPointMessage").GetComponent<TextMesh>().text = infomation;
    }

    // リクエストする本体
    IEnumerator RequestInit()
    {
        // HTTP リクエストする(POST メソッド) UnityWebRequest を呼び出し
        // アクセスする先は変数 urlGitHub で設定
        UnityWebRequest request = new UnityWebRequest(urlGitHub, "POST");

        // ResponseData ベースクラスを器として呼び出す
        RequestData requestData = new RequestData();
        // データを設定
        // requestData.name = "まいねーむ"; // 自分の名前

        // 送信データを JsonUtility.ToJson で JSON 文字列を作成
        // pointRequestData の構造に基づいて変換してくれる
        string strJSON = JsonUtility.ToJson(requestData);
        Debug.Log($"strJSON : {strJSON}");
        // 送信データを Encoding.UTF8.GetBytes で byte データ化
        byte[] bodyRaw = Encoding.UTF8.GetBytes(strJSON);

        // アップロード（Unity→サーバ）のハンドラを作成
        request.uploadHandler = new UploadHandlerRaw(bodyRaw);
        // ダウンロード（サーバ→Unity）のハンドラを作成
        request.downloadHandler = new DownloadHandlerBuffer();

        // JSON で送ると HTTP ヘッダーで宣言する
        request.SetRequestHeader("Content-Type", "application/json");

        // リクエスト開始
        Debug.Log("リクエスト開始");
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

                // ResponseData クラスで Unity で扱えるデータ化
                ResponseData responseData = JsonUtility.FromJson<ResponseData>(request.downloadHandler.text);

                // MessageText に結果テキスト割り当て
                GameObject.Find("StatusMessage").GetComponent<TextMesh>().text = responseData.result;

                break;
        }


    }

    // Update is called once per frame
    void Update()
    {

    }
}
```

以下を修正します。

```csharp
// アクセスする URL
// サーバー URL + /api/post/init
string urlGitHub = "ここにサーバーURLを入れる";
```

こちらをサーバー URL に `/api/post/init` というパスを加えて変更して保存します。

解説します。

今回は Term1-2 Chapter02 に近い仕組みで作られています。

```csharp
// 受信した JSON データを Unity で扱うデータにする ResponseData ベースクラス
[Serializable]
public class ResponseData
{
    // result というプロパティ名で string 型で変換
    public string result;
}
```

受信した JSON データを Unity で扱うデータにする ResponseData ベースクラスを用意して、「ひとまず」result 値だけ Unity の値として扱えるようにしています。「ひとまず」としたのは、

```js
{
    "result":"OK",
    "title":"こんにちは！ようこそ！",  // あいさつ文
    "add_point":1,  // 加算ポイント
    "recordPoint":0 // 記録している現在のポイント
};
```

他のデータも受け取れるため、あとで拡張するためです。JsonUtility はクラスで準備した以外のデータを受け取っても、無視されるので、このようなことができます。

```csharp
// 送信する Unity データを JSON データ化する RequestData ベースクラス
[Serializable]
public class RequestData
{   
    // 自分の名前
    // name というプロパティ名で string 型で変換
    public string name;
}
```

送信する Unity データを JSON データ化する RequestData ベースクラスでは、サーバに自分の名前を name という値で送れるよう準備しています。

```csharp
// ResponseData ベースクラスを器として呼び出す
RequestData requestData = new RequestData();
// データを設定
// requestData.name = "まいねーむ"; // 自分の名前
```

最初に動かすときは name 未設定なので `{"name":""}` と空の文字列で動作します。コメントアウトすると `requestData.name = "まいねーむ";` の部分が動作するので、サーバが出来る title の値が `こんにちは！ようこそ！` から `こんにちは！まいねーむさん、ようこそ！` と動作します。

あとは、POST リクエストを行っています。

## Term1_3_Chapter02_SendButton.cs 変更

`Assets/Scripts/Term1_3_Chapter02_SendButton.cs` をエディタで開きます。

```csharp
using UnityEngine;
using UnityEngine.EventSystems;

using System.Collections;       // IEnumerator のための参照
using UnityEngine.Networking;   // UnityWebRequest のための参照
using System;                   // Serializable のための参照
using System.Text;              // Encoding のための参照

public class Term1_3_Chapter02_SendButton : MonoBehaviour, IPointerClickHandler
{
    // Term1_3_Chapter01_CubeEvent とほぼ同じ

    // 受信した JSON データを Unity で扱うデータにする ResultResponseData ベースクラス
    [Serializable]
    public class ResultResponseData
    {
        // result というプロパティ名で string 型で変換
        public string result;
    }

    // 送信する Unity データを JSON データ化する PointRequestData ベースクラス
    [Serializable]
    public class PointRequestData
    {
        // point というプロパティ名で int 型で変換
        public int point;
    }

    // アクセスする URL
    // サーバーURL + /api/post/result でアクセス
    string urlGitHub = "ここにサーバーURLを入れる";

    public void OnPointerClick(PointerEventData eventData)
    {
        // マウスクリックイベント
        // Debug.Log($"オブジェクト {this.name} がクリックされたよ！");

        // HTTP リクエストを非同期処理を待つためコルーチンとして呼び出す
        StartCoroutine("PostPointData");
    }

    // POST リクエストする本体
    IEnumerator PostPointData()
    {
        // HTTP リクエストする(POST メソッド) UnityWebRequest を呼び出し
        // アクセスする先は変数 urlGitHub で設定
        UnityWebRequest request = new UnityWebRequest(urlGitHub, "POST");


        // PointRequestData ベースクラスを器として呼び出す
        PointRequestData pointRequestData = new PointRequestData();
        // データを設定
        pointRequestData.point = 1000; // ダミーで 1000 pt のゲーム結果を送る
        pointRequestData.point = GameObject.Find("ClickPart").GetComponent<Term1_3_Chapter02_ClickPart>().currentPoint;

        // 送信データを JsonUtility.ToJson で JSON 文字列を作成
        // pointRequestData の構造に基づいて変換してくれる
        string strJSON = JsonUtility.ToJson(pointRequestData);
        Debug.Log($"strJSON : {strJSON}");
        // 送信データを Encoding.UTF8.GetBytes で byte データ化
        byte[] bodyRaw = Encoding.UTF8.GetBytes(strJSON);

        // アップロード（Unity→サーバ）のハンドラを作成
        request.uploadHandler = new UploadHandlerRaw(bodyRaw);
        // ダウンロード（サーバ→Unity）のハンドラを作成
        request.downloadHandler = new DownloadHandlerBuffer();

        // JSON で送ると HTTP ヘッダーで宣言する
        request.SetRequestHeader("Content-Type", "application/json");

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

                // ResultResponseData クラスで Unity で扱えるデータ化
                ResultResponseData resultResponse = JsonUtility.FromJson<ResultResponseData>(request.downloadHandler.text);

                // MessageText に結果テキスト割り当て
                GameObject.Find("StatusMessage").GetComponent<TextMesh>().text = resultResponse.result;

                break;
        }

    }
}
```

以下を修正します。

```csharp
// アクセスする URL
// サーバーURL + /api/post/result でアクセス
string urlGitHub = "ここにサーバーURLを入れる";
```

こちらをサーバー URL に `/api/post/result` というパスを加えて変更して保存します。

解説します。

今回はTerm1_3_Chapter01_CubeEvent とほぼ同じプログラムです。SendButton をクリックすると現在のポイントを ClickPart から取得してデータ送信します。

```csharp
// データを設定
pointRequestData.point = GameObject.Find("ClickPart").GetComponent<Term1_3_Chapter02_ClickPart>().currentPoint;
```

このように値を取得しています。あとは同じです。

## シンプルに動かしてみる

まずは、サーバーへつなぐ設定ができたので動かしてみましょう。

![ad833d19086696f4841ff7d11828b4fb](https://i.gyazo.com/ad833d19086696f4841ff7d11828b4fb.png)

Play ボタンをクリックします。

![7d4dad403a48608db49b89293e8d58ec](https://i.gyazo.com/7d4dad403a48608db49b89293e8d58ec.png)

ClickPart の上の StatusMessage にサーバからデータを受け取って JSON データを Unity で扱えるデータにしてから result 値の OK を表示できていれば、うまくつながっています。

![d687f574cde14e7f191c84470ce760a1](https://i.gyazo.com/d687f574cde14e7f191c84470ce760a1.png)

コンソールでもやり取りの様子が確認できます。

```
/api/post/init 受信
{ name: '' }
```

Codespace 側でもターミナルで字受信できたことが確認できます。

![2d930e83bef28594da9fd7c29ea512f5](https://i.gyazo.com/2d930e83bef28594da9fd7c29ea512f5.png)

続いて、ClickPart を何度かクリックしたあとに、結果送信ボタンをクリックします。

```
/api/post/result 受信
{ point: 8 }
8 pt 記録
```

Codespace 側でもターミナルで字受信できたことが確認できます。

![99365fca16458a0ad1e75e9a731efaba](https://i.gyazo.com/99365fca16458a0ad1e75e9a731efaba.png)

コンソールでもやり取りの様子が確認できます。またこの値は、サーバで受信した時点でサーバに recordPoint という値で記録されています。サーバーが起動している間、記録ポイントは保持されています。

![c8e76c52116732bee393f9e0128beb3c](https://i.gyazo.com/c8e76c52116732bee393f9e0128beb3c.png)

また、こちらは初期起動時のデータ取得でも、記録ポイントが返ってきています。（再度つないでみた様子）

## 受け取ったデータをあいさつ文テキストに反映してみる（ResponseData.title）

![02db792fd629a56812a205234a08ae44](https://i.gyazo.com/02db792fd629a56812a205234a08ae44.png)

Term1_3_Chapter02_ClickPart の対応です。

<details>
<summary>📋答え（出題中は開かないでくださいね）</summary>
<pre style="position: relative;"><code class="lang-csharp">    // 受信した JSON データを Unity で扱うデータにする ResponseData ベースクラス
    [Serializable]
    public class ResponseData
    {
        // result というプロパティ名で string 型で変換
        public string result;
        // title というプロパティ名で string 型で変換
        public string title;
    }
</code></pre>

ResponseData に title の読み込みを加えます。

<pre style="position: relative;"><code class="lang-csharp">// StatusMessage に結果テキスト割り当て
GameObject.Find("StatusMessage").GetComponent<TextMesh>().text = responseData.title;
</code></pre>

StatusMessage のテキスト割り当てを responseData.title に変更します。

</details>

## 自分の名前を送っていてサーバーであいさつ文を作っていることを確認してから反映（RequestData.name）

![02db792fd629a56812a205234a08ae44](https://i.gyazo.com/02db792fd629a56812a205234a08ae44.png)

Term1_3_Chapter02_ClickPart の対応です。


```csharp
// 初回ロード時にいろいろな情報をもらう
// /api/post/init というパスで POST リクエストでアクセスするとデータが取得できます
app.post('/api/post/init', (req, res) => {
  console.log('/api/post/init 受信');
  // 受信したデータ
  console.log(req.body);
  // あいさつ文の値
  let title = "";
  // 受信した name 値の有無で文言が変わる
  if(req.body.name){
    title = `こんにちは！${req.body.name}さん、ようこそ！`;
  } else {
    title = "こんにちは！ようこそ！";
  }
  // 送るデータを JavaScript のオブジェクトで作る
  const responseData = {
    "result":"OK",
    "title":title,  // あいさつ文
    "add_point":1,  // 加算ポイント
    "recordPoint":recordPoint // 記録している現在のポイント
  };
  // res.json はオブジェクトを JSON 形式で返答します
  res.json(responseData)
});
```

このようにサーバ側では実は name 値を待っています。では name 値を反映してみましょう。

<details>
<summary>📋答え（出題中は開かないでくださいね）</summary>

<pre style="position: relative;"><code class="lang-csharp">// ResponseData ベースクラスを器として呼び出す
RequestData requestData = new RequestData();
// データを設定
requestData.name = "まいねーむ"; // 自分の名前
</code></pre>

このように新たな値を加えます。

</details>

## 受け取ったデータをポイント加算に反映してみる（ResponseData.add_point）

![02db792fd629a56812a205234a08ae44](https://i.gyazo.com/02db792fd629a56812a205234a08ae44.png)

## ポイント送信時に実は記録ほやほやの値が返ってくるので、それをOK と表示されてる StatusMessage に表示してみる（ResultResponseData.recordPoint）

![02db792fd629a56812a205234a08ae44](https://i.gyazo.com/02db792fd629a56812a205234a08ae44.png)

Term1_3_Chapter02_SendButton の対応です。

<details>
<summary>📋答え（出題中は開かないでくださいね）</summary>
<pre style="position: relative;"><code class="lang-csharp">
    // 受信した JSON データを Unity で扱うデータにする ResultResponseData ベースクラス
    [Serializable]
    public class ResultResponseData
    {
        // result というプロパティ名で string 型で変換
        public string result;
        // recordPoint というプロパティ名で int 型で変換
        public int recordPoint;
    }
</code></pre>

PointRequestData に recordPoint の読み込みを加えます。

<pre style="position: relative;"><code class="lang-csharp">
// MessageText に結果テキスト割り当て
GameObject.Find("StatusMessage").GetComponent<TextMesh>().text = resultResponse.recordPoint.ToString();
</code></pre>

StatusMessage のテキスト割り当てを responseData.recordPoint に文字列変換して変更します。

</details>

## ダミーでなく加点したポイントをちゃんと送る

![02db792fd629a56812a205234a08ae44](https://i.gyazo.com/02db792fd629a56812a205234a08ae44.png)

## 再起動して記録ポイントが初期化されることも確認

![02db792fd629a56812a205234a08ae44](https://i.gyazo.com/02db792fd629a56812a205234a08ae44.png)

## 今回の Codespace の終了

![0a8b4cfb807e57ea1382292a757c6899](https://i.gyazo.com/0a8b4cfb807e57ea1382292a757c6899.png)

今回の Codespace 終了しておきましょう。