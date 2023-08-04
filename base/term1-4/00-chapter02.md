# 外部の API 連携を体験

![9d2c38e6fe48e61528f6b2d34370768f](https://i.gyazo.com/9d2c38e6fe48e61528f6b2d34370768f.png)

## この章で学ぶこと

外部の API 連携を体験します。

## 今回の Unity シーンを起動

![6049726527f3133083e8ca07d1e6261c](https://i.gyazo.com/6049726527f3133083e8ca07d1e6261c.png)

Project タブから Assets > Scenes を選択します。Scene-Term1-4-Chapter02 をダブルクリックして起動しましょう。

## わんこ画像を持ってくる API をつないでみる

![aae5fcbb30bf9d55b7249a6d6bd44697](https://i.gyazo.com/aae5fcbb30bf9d55b7249a6d6bd44697.png)

https://dog.ceo/dog-api/ というpublic-apis にある API からつないでみます。わんこ画像を表示してみましょう。

簡単にドキュメントを読みながら、実装を想像してみましょう。

✅ポイント
- GET リクエストでつなぐ URL を把握してみましょう
- 実際に受け取る値から画像 URL を取得する JSON 取得クラスの設定を考えてみましょう
- そのうえで、画像を読み込んでテクスチャで貼り付けるところまで考えてみましょう

## Term1_4_Chapter02_CubeEvent01.cs を見てみる

Cube01 オブジェクトの `Assets/Scripts/Term1_4_Chapter02_CubeEvent01.cs` で実際の動作が書かれています。こちらをエディタで開きます。

```csharp
using UnityEngine;
using UnityEngine.EventSystems;

using System.Collections;       // IEnumerator のための参照
using UnityEngine.Networking;   // UnityWebRequest のための参照
using System;                   // Serializable のための参照

public class Term1_4_Chapter02_CubeEvent01 : MonoBehaviour, IPointerClickHandler
{
    // アクセスする API の URL
    // https://dog.ceo/dog-api/
    string urlAPI = "";

    // 受信した JSON データを Unity で扱うデータにする ResponseData ベースクラス
    [Serializable]
    public class ResponseData
    {
        // message というプロパティ名で string 型で変換
        // message だけ取得
        public string message;
    }

    void Start()
    {
        
    }

    public void OnPointerClick(PointerEventData eventData)
    {
        // HTTP リクエストを非同期処理を待つためコルーチンとして呼び出す
        StartCoroutine("GetAPI");
    }

    // API 取得
    IEnumerator GetAPI()
    {
        // HTTP リクエストする(GET メソッド) UnityWebRequest を呼び出し
        // アクセスする先は変数 urlGitHub で設定
        UnityWebRequest request = UnityWebRequest.Get(urlAPI);

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

                // ResponseData クラスで Unity で扱えるデータ化
                ResponseData response = JsonUtility.FromJson<ResponseData>(request.downloadHandler.text);

                // 画像読み込み
                StartCoroutine("GetTexture",response.message);

                break;
        }


    }

    // テクスチャ読み込みb
    IEnumerator GetTexture(string url)
    {
        // テクスチャを GET リクエストで読み込む。ブラウザでも見れる。
        UnityWebRequest request = UnityWebRequestTexture.GetTexture(url);


        // リクエスト開始
        yield return request.SendWebRequest();

        Debug.Log("リクエスト開始");

        // 結果によって分岐
        switch (request.result)
        {
            case UnityWebRequest.Result.InProgress:
                Debug.Log("リクエスト中");
                break;

            case UnityWebRequest.Result.Success:
                Debug.Log("リクエスト成功");

                // テクスチャに割り当て
                Texture loadedTexture = ((DownloadHandlerTexture)request.downloadHandler).texture;

                GameObject.Find("Tile").GetComponent<MeshRenderer>().material.SetTexture("_MainTex", loadedTexture);

                break;
        }
    }


    void Update()
    {
        
    }
}
```

実際に動作が把握できたら、今回は API の URL を入力して保存みましょう。

```csharp
    // アクセスする API の URL
    // https://dog.ceo/dog-api/
    string urlAPI = "";
```

こちらです。

![d0cee31a104f1b4f6d4e6aabb949c468](https://i.gyazo.com/d0cee31a104f1b4f6d4e6aabb949c468.png)

そして Cube01 をクリックして動かしてみましょう！

## LINE Notify につないでみましょう

![0315bfabadc8442391ad415f119e63c3](https://i.gyazo.com/0315bfabadc8442391ad415f119e63c3.png)

[LINE Notifyの API キーの取得](../00-preparation/01-line-notify.md) をして仕様をまず把握しましょう。そして API キーを手元にメモしておきます。

ただ、今回はやや難しいデータなので、ある程度把握できたら実際のソースコードで動かしてみましょう。

## Term1_4_Chapter02_CubeEvent02.cs を見てみる

Cube02 オブジェクトの `Assets/Scripts/Term1_4_Chapter02_CubeEvent02.cs` で実際の動作が書かれています。こちらをエディタで開きます。

```csharp
using UnityEngine;
using UnityEngine.EventSystems;

using System.Collections;       // IEnumerator のための参照
using UnityEngine.Networking;   // UnityWebRequest のための参照
using System.Collections.Generic; // Listのため

public class Term1_4_Chapter02_CubeEvent02 : MonoBehaviour, IPointerClickHandler
{

    // LINE Notify のトークン
    string tokenLINENotify = "token";

    void Start()
    {
        
    }

    public void OnPointerClick(PointerEventData eventData)
    {
        // HTTP リクエストを非同期処理を待つためコルーチンとして呼び出す
        // 第 2 引数で送りたい文言を入れる
        StartCoroutine("PostLINENofify", "Unityからテスト");
    }

    IEnumerator PostLINENofify(string message)
    {
        // IMultipartFormSection で multipart/form-data のデータとして送れます
        // https://docs.unity3d.com/ja/2018.4/Manual/UnityWebRequest-SendingForm.html
        // https://docs.unity3d.com/ja/2019.4/ScriptReference/Networking.IMultipartFormSection.html
        // https://docs.unity3d.com/ja/2020.3/ScriptReference/Networking.MultipartFormDataSection.html
        List<IMultipartFormSection> formData = new List<IMultipartFormSection>();
        formData.Add(new MultipartFormDataSection("message", message));

        // HTTP リクエストする(POST メソッド) UnityWebRequest を呼び出し
        // アクセスする先は変数 urlGitHub で設定
        // 第 2 引数で上記のフォームデータを割り当てて multipart/form-data のデータとして送ります
        UnityWebRequest request = UnityWebRequest.Post("https://notify-api.line.me/api/notify", formData);

        // LINE Notify の認証は Authorization ヘッダーで Bearer のあとに API トークンを入れる
        request.SetRequestHeader("Authorization", $"Bearer {tokenLINENotify}");

        // ダウンロード（サーバ→Unity）のハンドラを作成
        request.downloadHandler = new DownloadHandlerBuffer();

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

                break;
        }


    }


    void Update()
    {
        
    }
}
```

LINE Notify のトークンを入力します。

```csharp
    // LINE Notify のトークン
    string tokenLINENotify = "token";
```

こちらです。

![d0cee31a104f1b4f6d4e6aabb949c468](https://i.gyazo.com/d0cee31a104f1b4f6d4e6aabb949c468.png)

そして Cube02 をクリックして動かしてみましょう！

![381021c8feeb23b82f9271e0b7c5d896](https://i.gyazo.com/381021c8feeb23b82f9271e0b7c5d896.png)

このようにコンソールでログが出ると成功です！

![39080780da95e20e9a32ab13c9ea2df3](https://i.gyazo.com/39080780da95e20e9a32ab13c9ea2df3.jpg)

そして、このように LINE Notify にメッセージがきます。

## 手軽に使えるお天気 API にチャレンジ

![aae5fcbb30bf9d55b7249a6d6bd44697](https://i.gyazo.com/aae5fcbb30bf9d55b7249a6d6bd44697.png)

https://github.com/robertoduessmann/weather-api という public-apis にある手軽に使えるお天気 API にチャレンジしてみましょう。

Cube03 にある GET リクエストベースのソースコードを使ってつないでみましょう。

✅ポイント
- GET リクエストでつなぐ URL を Tokyo の場合で考えてみましょう。
- 実際に受け取る値から temperature , description を取得してみましょう。
- なお、しっかり POST リクエストでより情報を取得したいときは OpenWeatherMap API https://openweathermap.org/api もおススメです

Cube03 オブジェクトの `Assets/Scripts/Term1_4_Chapter02_CubeEvent03.cs` で実際の動作が書かれています。こちらをエディタで開きます。

ソースはこちらです。

```csharp
using UnityEngine;
using UnityEngine.EventSystems;

using System.Collections;       // IEnumerator のための参照
using UnityEngine.Networking;   // UnityWebRequest のための参照
using System;                   // Serializable のための参照

public class Term1_4_Chapter02_CubeEvent03 : MonoBehaviour, IPointerClickHandler
{
    // API の接続先
    string urlAPI = "";

    // 受信した JSON データを Unity で扱うデータにする ResponseData ベースクラス
    [Serializable]
    public class ResponseData
    {
        
    }

    void Start()
    {
        
    }
    
    void Update()
    {
        
    }
    public void OnPointerClick(PointerEventData eventData)
    {
        // マウスクリックイベント

        // HTTP リクエストを非同期処理を待つためコルーチンとして呼び出す
        StartCoroutine("GetData");
    }

    IEnumerator GetData()
    {
        // HTTP リクエストする(GET メソッド) UnityWebRequest を呼び出し
        // アクセスする先は変数 urlGitHub で設定
        UnityWebRequest request = UnityWebRequest.Get(urlAPI);

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

                // ResponseData クラスで Unity で扱えるデータ化
                ResponseData response = JsonUtility.FromJson<ResponseData>(request.downloadHandler.text);

                // MessageText に結果テキスト割り当て
                this.transform.Find("MessageText").GetComponent<TextMesh>().text = "";

                break;
        }


    }
}
```