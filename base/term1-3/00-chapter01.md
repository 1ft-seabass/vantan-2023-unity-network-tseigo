# ゲーム結果のデータを送ってみよう

![9d2c38e6fe48e61528f6b2d34370768f](https://i.gyazo.com/9d2c38e6fe48e61528f6b2d34370768f.png)

## この章で学ぶこと

ゲーム結果のデータを送ってみよう

この章では、Unity からシンプルなゲーム結果ポイント 1000 pt をJsonUtility を使って JSON データを作成してサーバに送ってみます。

## Codespace の起動

![0a3a35f3418068b7713ddaa729f2c660](https://i.gyazo.com/0a3a35f3418068b7713ddaa729f2c660.png)

GitHub にログインした状態で https://github.com/codespaces にアクセスします。

![34de49185c6b28fb938519084d5b36fe](https://i.gyazo.com/34de49185c6b28fb938519084d5b36fe.png)

Codespaces のページです。さきほど使っていた Codespace をクリックして起動します。

## サーバの起動

![0a3a35f3418068b7713ddaa729f2c660](https://i.gyazo.com/0a3a35f3418068b7713ddaa729f2c660.png)

- ターミナルで `node term1-3-chapter01.js` をサーバ起動
- ポートタブで今回のサーバ起動を公開
- シークレットウィンドウで今回のサーバが公開されているか確認します

こちらの手順を進めます。

✅ポイント
- 今回は POST リクエストで 1 つの仕組みを作っています
- `/api/post/result` というパスで POST リクエストでアクセスすると `{"result":"OK"}` という JSON データが取得できます
  - こちらに POST リクエストするとき Unity 側から `{"point":1000}` というダミーのゲーム結果ポイントをサーバに送ります
  - 取得した `{"result":"OK"}` を Unity 内の result というプロパティで扱ってシーンのテキストに反映します

## 今回の Unity シーンを起動

![6049726527f3133083e8ca07d1e6261c](https://i.gyazo.com/6049726527f3133083e8ca07d1e6261c.png)

Project タブから Assets > Scenes を選択します。Scene-Term1-3-Chapter01 をダブルクリックして起動しましょう。

## Term1_3_Chapter01_CubeEvent.cs 変更

`Assets/Scripts/Term1_3_Chapter01_CubeEvent.cs` をエディタで開きます。

```csharp
using UnityEngine;
using UnityEngine.EventSystems;

using System.Collections;       // IEnumerator のための参照
using UnityEngine.Networking;   // UnityWebRequest のための参照
using System;                   // Serializable のための参照
using System.Text;              // Encoding のための参照

public class Term1_3_Chapter01_CubeEvent : MonoBehaviour, IPointerClickHandler
{
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
                GameObject.Find("MessageText").GetComponent<TextMesh>().text = resultResponse.result;

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

解説していきます。

```csharp
// 受信した JSON データを Unity で扱うデータにする ResultResponseData ベースクラス
[Serializable]
public class ResultResponseData
{
    // result というプロパティ名で string 型で変換
    public string result;
}
```

受信した JSON データを Unity で扱うデータにする ResultResponseData ベースクラスです。今回は `{"result":"OK"}` というデータを受け取るので、それに対応しています。

```csharp
// 送信する Unity データを JSON データ化する PointRequestData ベースクラス
[Serializable]
public class PointRequestData
{
    // point というプロパティ名で int 型で変換
    public int point;
}
```

送信する Unity データを JSON データ化する PointRequestData ベースクラスです。今回は仮のゲーム点数 1000 を送る `{"point":1000}` というデータを受け取るので、それに対応しています。

```csharp
// PointRequestData ベースクラスを器として呼び出す
PointRequestData pointRequestData = new PointRequestData();
// データを設定
pointRequestData.point = 1000; // ダミーで 1000 pt のゲーム結果を送る
```

JSON データに変換するために Unity でのデータの器を作ります。PointRequestData ベースクラスを器として用意します。

そして、pointRequestData に pointRequestData.point という形で、 1000 pt のゲーム結果を設定しています。

```csharp
// 送信データを JsonUtility.ToJson で JSON 文字列を作成
// pointRequestData の構造に基づいて変換してくれる
string strJSON = JsonUtility.ToJson(pointRequestData);
Debug.Log($"strJSON : {strJSON}");
// 送信データを Encoding.UTF8.GetBytes で byte データ化
byte[] bodyRaw = Encoding.UTF8.GetBytes(strJSON);
```

送信データを JsonUtility.ToJson で JSON 文字列を作成します。ToJson は、分かりやすくクラスの構造に合わせて変換してくれます。

今回は PointRequestData の内容に合わせて、point という int 型の値があるので `{"point":1000}` と変換し strJSON の変数に入れます。

そして、実際にデータを送るときは byte 列にする必要があるので strJSON を `byte[] bodyRaw = Encoding.UTF8.GetBytes(strJSON);` で Raw データ（生のデータ）として bodyRaw に格納して送信前の準備をします。

```csharp
// アップロード（Unity→サーバ）のハンドラを作成
request.uploadHandler = new UploadHandlerRaw(bodyRaw);
// ダウンロード（サーバ→Unity）のハンドラを作成
request.downloadHandler = new DownloadHandlerBuffer();

// JSON で送ると HTTP ヘッダーで宣言する
request.SetRequestHeader("Content-Type", "application/json");
```

UploadHandlerRaw、DownloadHandlerBuffer でデータの送受信（アップロードとダウンロード）を用意していますが、今回は JSON データで送るので `request.SetRequestHeader` で送る前に「これは JSON で送りますよ」と HTTP ヘッダーで宣言しています。

これで POST リクエストが JSON で送られます。

```csharp
// ResultResponseData クラスで Unity で扱えるデータ化
ResultResponseData resultResponse = JsonUtility.FromJson<ResultResponseData>(request.downloadHandler.text);

// MessageText に結果テキスト割り当て
GameObject.Find("MessageText").GetComponent<TextMesh>().text = resultResponse.result;
```

JSON データを受信する仕組みは、以前学んだとおりです。

受け取った `{"result":"OK"}` JSON データを ResultResponseData クラスで Unity で扱えるデータ化を行って、MessageText に結果テキスト割り当てています。

## 動かしてみる

![ad833d19086696f4841ff7d11828b4fb](https://i.gyazo.com/ad833d19086696f4841ff7d11828b4fb.png)

Play ボタンをクリックします。

![172e77202148148d63c107761e7680fa](https://i.gyazo.com/172e77202148148d63c107761e7680fa.png)

再生されたあと、Cube をクリックするとサーバとデータのやり取りが行われて `{"point":1000}` がサーバーに送信されて、サーバーから取得した JSON データ `{"result":"OK"}` を JSONUtility で解析します。

そして result 結果「OK」を Message テキストに割り当てました。

![b1f7fe83c56dbb6f17cb04dd9b7bf1e3](https://i.gyazo.com/b1f7fe83c56dbb6f17cb04dd9b7bf1e3.png)

```text
/api/post/result 受信
{ point: 1000 }
```

サーバー側でも受信が行われていることも確認してみましょう！

## 今回の Codespace の終了

![0a8b4cfb807e57ea1382292a757c6899](https://i.gyazo.com/0a8b4cfb807e57ea1382292a757c6899.png)

今回の Codespace 終了しておきましょう。