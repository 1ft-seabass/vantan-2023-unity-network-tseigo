# 静的なデータを取得してみよう

![9d2c38e6fe48e61528f6b2d34370768f](https://i.gyazo.com/9d2c38e6fe48e61528f6b2d34370768f.png)

## この章で学ぶこと

サーバからデータを取得してみます。

## Codespace の起動

![0a3a35f3418068b7713ddaa729f2c660](https://i.gyazo.com/0a3a35f3418068b7713ddaa729f2c660.png)

GitHub にログインした状態で https://github.com/codespaces にアクセスします。

![34de49185c6b28fb938519084d5b36fe](https://i.gyazo.com/34de49185c6b28fb938519084d5b36fe.png)

Codespaces のページです。さきほど使っていた Codespace をクリックして起動します。

## サーバの起動

![0a3a35f3418068b7713ddaa729f2c660](https://i.gyazo.com/0a3a35f3418068b7713ddaa729f2c660.png)

- ターミナルで `node term1-2-chapter01.js` をサーバ起動
- ポートタブで今回のサーバ起動を公開
- シークレットウィンドウで今回のサーバが公開されているか確認します

こちらの手順を進めます。

✅ポイント
- 前回は public フォルダの中身を取ってくる仕組みだったが、今回は明確に特定のパスにアクセスすると特定の文言が返ってくる仕組みになっています。
- サーバー URL に `/api/get/sample` というパスを加わったときに、ブラウザや GET リクエストをすると `GET OK!` というテキストが取得できる
- サーバー URL に `/api/post/sample` というパスを加わったときに、POST リクエストをすると `POST OK!` というテキストが取得できる

## 今回の Unity シーンを起動

![6049726527f3133083e8ca07d1e6261c](https://i.gyazo.com/6049726527f3133083e8ca07d1e6261c.png)

Project タブから Assets > Scenes を選択します。Scene-Term1-2-Chapter01 をダブルクリックして起動しましょう。

## シーンの仕組みの解説

![ae6172228f962578c4c19763b03360d2](https://i.gyazo.com/ae6172228f962578c4c19763b03360d2.png)

シーンの仕組みを解説します。

✅ポイント
- GET リクエストと POST リクエストを試すものです
- GET リクエストは CubeGet オブジェクトに CubeEvent03_01.cs スクリプトがコンポーネントとして加わっています
- POST リクエストは CubePost オブジェクトに CubeEvent03_02.cs スクリプトがコンポーネントとして加わっています

## サーバーの起動をチェック

![60a04c04a43b5dbd23e17176d0da05db](https://i.gyazo.com/60a04c04a43b5dbd23e17176d0da05db.png)

今回のサーバーの行のクリップボードマークをクリックして今回の URL をコピーしてブラウザで表示されるか確認しましょう。

このサーバー URL を覚えておきましょう。

## ブラウザで GET リクエストでパスつきのアクセスを体験

今回は、サーバー側の以下のコードによって、先ほどアクセスしたサーバー URL に `/api/get/sample` というパスを加わったときに `GET OK!` というテキストが取得できる仕組みになっています。

また、この仕組みが動作すると、サーバーが返答すると同時に `console.log('GET Response!');` というコードによってサーバー側のターミナルで `GET Response!` というログが残るのでアクセスしたことが分かりやすいです。

```js
// /api/get/sample というパスで GET リクエストでアクセスすると GET OK! が取得できます
// GET リクエストなのでブラウザから見れます
app.get('/api/get/sample', (req, res) => {
  console.log('GET Response!');
  res.send('GET OK!')
});
```

ブラウザで、さきほどアクセスできた、サーバー URL に `/api/get/sample` というパスを加えてアクセスしてみましょう。

![de284f0eda8aef20c7605bb86ca8f84e](https://i.gyazo.com/de284f0eda8aef20c7605bb86ca8f84e.png)

このように `GET OK!` とブラウザで表示されたら、正しくサーバーが動いています。

## サーバー側でも GET リクエストが反応していることを体験

![c12bdf2a9458ddde8b630fa939b0128e](https://i.gyazo.com/c12bdf2a9458ddde8b630fa939b0128e.png)

この仕組みが動作したのでサーバー側のターミナルで `GET Response!` というログが残ることも確認しましょう。

## Unity で GET リクエストでパスつきのアクセスを体験

Unity シーンでは GET リクエストは CubeGet オブジェクトに Term1_2_Chapter01_CubeEvent01.cs スクリプトがコンポーネントとして加わっています。

`Assets/Scripts/Term1_2_Chapter01_CubeEvent01.cs` をエディタで開きます。

```csharp
using UnityEngine;
using UnityEngine.EventSystems;

using System.Collections;       // IEnumerator のための参照
using UnityEngine.Networking;   // UnityWebRequest のための参照

public class Term1_2_Chapter01_CubeEvent01 : MonoBehaviour, IPointerClickHandler
{
    // アクセスする URL
    // サーバー URL + /api/get/sample
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

                break;
        }


    }
}
```

前章で習った仕組みと同じものです。

```csharp
    // アクセスする URL
    // サーバー URL + /api/get/sample
    string urlGitHub = "ここにサーバーURLを入れる";
```

こちらを「ブラウザで GET リクエストでパスつきのリクエストを体験」でアクセスできた URL に変更して保存します。

## Unity で GET リクエストを動かしてみる

![ad833d19086696f4841ff7d11828b4fb](https://i.gyazo.com/ad833d19086696f4841ff7d11828b4fb.png)

Play ボタンをクリックします。

![0a32f4ca5b5aec5a5660d3354ce63c3a](https://i.gyazo.com/0a32f4ca5b5aec5a5660d3354ce63c3a.png)

CubeGet をマウスでクリックしてみましょう。先ほど設定した URL にアクセスします。

![22173618d1266819141729e1417e5e95](https://i.gyazo.com/22173618d1266819141729e1417e5e95.png)

Console で `GET OK!` というログが出てくれば成功です！

## サーバー側の POST リクエストの仕組み

今回は、サーバー側の以下のコードによって、先ほどアクセスしたサーバー URL に `/api/post/sample` というパスを加わったときに `POST OK!` というテキストが取得できる仕組みになっています。

また、この仕組みが動作すると、サーバーが返答すると同時に `console.log('POST Response!');` というコードによってサーバー側のターミナルで `POST Response!` というログが残るのでアクセスしたことが分かりやすいです。

```js
// /api/post/sample というパスで POST リクエストでアクセスすると POST OK! が取得できます
app.post('/api/post/sample', (req, res) => {
  console.log('POST Response!');
  res.send('POST OK!')
});
```

## ブラウザで POST リクエストでパスつきのアクセスができないことを体験

ブラウザでアクセスできるのは GET リクエストです。サーバー URL に `/api/post/sample` というパスを加えてアクセスしてみましょう。

![2748abd2644bed6899752f29c110d029](https://i.gyazo.com/2748abd2644bed6899752f29c110d029.png)

このようにエラーになります。ただこれは「GET リクエストをブラウザでしてみたけど GET リクエストで返答できなかった」という意味で、正確には POST リクエストが失敗したわけではないです。

POST リクエストはこのようにブラウザでアクセスして簡単に見ることができない点で、セキュリティ的には少し安全です。

さらに、POST は GET とくらべてより多くのデータを仕込むこともできるので、ユーザーに紐づいたログインのやりとりなどを仕込めば、よりセキュリティを高めたやり取りができます。

## Unity で POST リクエストでパスつきのアクセスを体験

ブラウザでは直接アクセスできませんでしたが、Unity では UnityWebRequest で POST リクエストを行うことができます。

Unity シーンでは POST リクエストは CubePost オブジェクトに Term1_2_Chapter01_CubeEvent02.cs スクリプトがコンポーネントとして加わっています。

`Assets/Scripts/Term1_2_Chapter01_CubeEvent02.cs` をエディタで開きます。

```csharp
using UnityEngine;
using UnityEngine.EventSystems;

using System.Collections;       // IEnumerator のための参照
using UnityEngine.Networking;   // UnityWebRequest のための参照
using System.Text;              // Encoding のための参照

public class Term1_2_Chapter01_CubeEvent02 : MonoBehaviour, IPointerClickHandler
{
    // アクセスする URL
    // サーバー URL + /api/post/sample
    string urlGitHub = "ここにサーバーURLを入れる";

    public void OnPointerClick(PointerEventData eventData)
    {
        // マウスクリックイベント
        // Debug.Log($"オブジェクト {this.name} がクリックされたよ！");

        // HTTP リクエストを非同期処理を待つためコルーチンとして呼び出す
        StartCoroutine("PostGitHubData");
    }

    // リクエストする本体
    IEnumerator PostGitHubData()
    {
        // HTTP リクエストする(POST メソッド) UnityWebRequest を呼び出し
        // アクセスする先は変数 urlGitHub で設定
        UnityWebRequest request = new UnityWebRequest(urlGitHub, "POST");
        // 空ではやりとりできないので、今回は仮の dummy 文字を用意
        byte[] bodyRaw = Encoding.UTF8.GetBytes("dummy");
        // アップロード（Unity→サーバ）のハンドラを作成
        request.uploadHandler = new UploadHandlerRaw(bodyRaw);
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
}
```

このようなコードです。

✅ポイント
- `using System.Text;`
  - 今回の Encoding のための参照のために追加されています。
- `UnityWebRequest request = new UnityWebRequest(urlGitHub, "POST");`
  - HTTP リクエストする(POST メソッド) UnityWebRequest を呼び出し
  - アクセスする URL は変数 urlGitHub で設定
- `byte[] bodyRaw = Encoding.UTF8.GetBytes("dummy");`
  - 空ではやりとりできないので、今回は仮の dummy 文字を用意
- `request.uploadHandler = new UploadHandlerRaw(bodyRaw);`
  - アップロード（Unity→サーバ）のハンドラを作成
- `request.downloadHandler = new DownloadHandlerBuffer();`
  - ダウンロード（サーバ→Unity）のハンドラを作成
- リクエスト後の結果待ちの処理は GET リクエストの時と同じ

```csharp
    // アクセスする URL
    // サーバー URL + /api/post/sample
    string urlGitHub = "ここにサーバーURLを入れる";
```

こちらをサーバー URL に `/api/post/sample` というパスを加えてアクセスしてみます。

わたしの仕事でも POST リクエストでアクセスするケースは多いのですが GET リクエストと違いブラウザで一旦確認できず、Unity 側で試すことになるところが POST リクエストの少しハマりやすいところです。

## Unity で POST リクエストを動かしてみる

![ad833d19086696f4841ff7d11828b4fb](https://i.gyazo.com/ad833d19086696f4841ff7d11828b4fb.png)

Play ボタンをクリックします。

![026abdb76fafe0c18fabe63e3edaab47](https://i.gyazo.com/026abdb76fafe0c18fabe63e3edaab47.png)

CubePost をマウスでクリックしてみましょう。先ほど設定した URL にアクセスします。

![142cb5a953e095e5a4db36e2c8a53295](https://i.gyazo.com/142cb5a953e095e5a4db36e2c8a53295.png)

Console で `POST OK!` というログが出てくれば成功です！

## サーバー側でも POST リクエストが反応していることを体験

![8f97df0a60843b2b92ae32625eecddc3](https://i.gyazo.com/8f97df0a60843b2b92ae32625eecddc3.png)

この仕組みが動作したのでサーバー側のターミナルで `POST Response!` というログが残ることも確認しましょう。

## 今回の Codespace の終了

![0a8b4cfb807e57ea1382292a757c6899](https://i.gyazo.com/0a8b4cfb807e57ea1382292a757c6899.png)

今回の Codespace 終了しておきましょう。
