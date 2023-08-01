# 静的なデータを表示してみよう

![9d2c38e6fe48e61528f6b2d34370768f](https://i.gyazo.com/9d2c38e6fe48e61528f6b2d34370768f.png)

## この章で学ぶこと

サーバから受け取ったデータを表示してみましょう。

## Codespace の起動

![0a3a35f3418068b7713ddaa729f2c660](https://i.gyazo.com/0a3a35f3418068b7713ddaa729f2c660.png)

GitHub にログインした状態で https://github.com/codespaces にアクセスします。

![34de49185c6b28fb938519084d5b36fe](https://i.gyazo.com/34de49185c6b28fb938519084d5b36fe.png)

Codespaces のページです。さきほど使っていた Codespace をクリックして起動します。

## サーバの起動

![0a3a35f3418068b7713ddaa729f2c660](https://i.gyazo.com/0a3a35f3418068b7713ddaa729f2c660.png)

- ターミナルで `node term1-2-chapter02.js` をサーバ起動
- ポートタブで今回のサーバ起動を公開
- シークレットウィンドウで今回のサーバが公開されているか確認します

こちらの手順を進めます。

✅ポイント
- `term1-2-chapter01.js` の仕組みをベースにしています。
- 今回は POST リクエストで 2 つの仕組みを作っています
- `/api/post/title` というパスで POST リクエストでアクセスすると「こんにちは！ようこそ！」というテキストが取得できます
  - これをテキストとして扱ってシーンのテキストに反映します
- `/api/post/add_point` というパスで POST リクエストでアクセスすると 1 というテキストが取得できます。
  - これを数字として扱って、クリック時のポイント加算設定にします

## 今回の Unity シーンを起動

![6049726527f3133083e8ca07d1e6261c](https://i.gyazo.com/6049726527f3133083e8ca07d1e6261c.png)

Project タブから Assets > Scenes を選択します。Scene-Term1-2-Chapter02 をダブルクリックして起動しましょう。

## シーンの仕組みの解説

![ae6172228f962578c4c19763b03360d2](https://i.gyazo.com/ae6172228f962578c4c19763b03360d2.png)

シーンの仕組みを解説します。

✅ポイント
- WelcomeMessage は、再生開始時に、挨拶メッセージを読み込みます
  - `Assets/Scripts/Scene04WelcomeMessage.cs` で動作しています
  - `/api/post/title` のパスでサーバーに POST リクエストでアクセスすると「こんにちは！ようこそ！」というテキストが取得してテキストに反映します
- ClickPart をクリックするとポイントが加算される仕組みです
  - `Assets/Scripts/Scene04ClickPart.cs` で動作しています
  - `/api/post/add_point` のパスでサーバーに POST リクエストでアクセスすると 1 というテキストが取得できるので数値に変換して加算するポイントに使います
  - CurrentPointMessage にクリックした現在のポイントが表示されます
  - AddPointMessage に加算される数値が表示されます

## サーバーの起動をチェック

![60a04c04a43b5dbd23e17176d0da05db](https://i.gyazo.com/60a04c04a43b5dbd23e17176d0da05db.png)

今回のサーバーの行のクリップボードマークをクリックして今回の URL をコピーしてブラウザで表示されるか確認しましょう。

このサーバー URL を覚えておきましょう。

## Term1_2_Chapter02_WelcomeMessage.cs 変更

`Assets/Scripts/Term1_2_Chapter02_WelcomeMessage.cs` をエディタで開きます。

```csharp
using UnityEngine;
using UnityEngine.EventSystems;

using System.Collections;       // IEnumerator のための参照
using UnityEngine.Networking;   // UnityWebRequest のための参照
using System.Text;              // Encoding のための参照

public class Term1_2_Chapter02_WelcomeMessage : MonoBehaviour
{
    // アクセスする URL
    // サーバー URL + /api/post/title
    string urlGitHub = "ここにサーバーURLを入れる";

    void Start()
    {
        // 起動時にデータを読み込む

        // HTTP リクエストを非同期処理を待つためコルーチンとして呼び出す
        StartCoroutine("RequestWelcomeMessage");
    }

    // リクエストする本体
    IEnumerator RequestWelcomeMessage()
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

                // テキストに反映
                string message = request.downloadHandler.text;
                this.gameObject.GetComponent<TextMesh>().text = message;

                break;
        }


    }

}
```

✅ポイント
- Scene03 の POST リクエストの仕組みと同じです。
- Start 関数で動作するので再生開始時にデータを読みに行きます

```csharp
    // アクセスする URL
    // サーバー URL + /api/post/title
    string urlGitHub = "ここにサーバーURLを入れる";
```

こちらをサーバー URL に `/api/post/title` というパスを加えて変更して保存します。

## Term1_2_Chapter02_ClickPart.cs 変更


```csharp
using UnityEngine;
using UnityEngine.EventSystems;

using System.Collections;       // IEnumerator のための参照
using UnityEngine.Networking;   // UnityWebRequest のための参照
using System.Text;              // Encoding のための参照

public class Term1_2_Chapter02_ClickPart : MonoBehaviour, IPointerClickHandler
{
    // アクセスする URL
    // サーバー URL + /api/post/add_point
    string urlGitHub = "ここにサーバーURLを入れる";

    // ポイント加算設定
    int addPoint = 0;

    // 蓄積ポイント
    int currentPoint = 0;

    void Start()
    {
        // 起動時にデータを読み込む

        // HTTP リクエストを非同期処理を待つためコルーチンとして呼び出す
        StartCoroutine("RequestAddPointSetting");

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
    IEnumerator RequestAddPointSetting()
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

                // 受け取った加算ポイント設定を変数に記録
                // 文字列なので int.Parse で変換
                addPoint = int.Parse(request.downloadHandler.text);

                // テキストに反映
                string infomation = "AddPoint +" + request.downloadHandler.text + "pt";
                GameObject.Find("AddPointMessage").GetComponent<TextMesh>().text = infomation;

                break;
        }


    }

    // Update is called once per frame
    void Update()
    {
        
    }
}
```

✅ポイント
- Term1_2_Chapter01_CubeEvent02 の POST リクエストの仕組みと同じです。
- Start 関数で動作するので再生開始時にデータを読みに行きます
- クリック時にポイント加算をしています
- 受け取った加算ポイント設定を変数に記録するとき、文字列なので int.Parse で変換して数字で扱えるようにしています

```csharp
    // アクセスする URL
    // サーバー URL + /api/post/add_point
    string urlGitHub = "ここにサーバーURLを入れる";
```

こちらをサーバー URL に `/api/post/add_point` というパスを加えて変更して保存します。

## 動かしてみる

![ad833d19086696f4841ff7d11828b4fb](https://i.gyazo.com/ad833d19086696f4841ff7d11828b4fb.png)

Play ボタンをクリックします。

![f1e79dfe04b48d7053cc6fc318224dff](https://i.gyazo.com/f1e79dfe04b48d7053cc6fc318224dff.png)

まず、再生開始時にデータがうまく取得できれば、このように表示されます。

![f07aa48409d1a946b4df49246f8bda66](https://i.gyazo.com/f07aa48409d1a946b4df49246f8bda66.png)

クリックすると、ポイントが変化します。

![e70f06c613de324d3e80750bce01dcc1](https://i.gyazo.com/e70f06c613de324d3e80750bce01dcc1.png)

Console で動作も確認しておきましょう。

![7107764174ee0d6d6875d8e87615e7cf](https://i.gyazo.com/7107764174ee0d6d6875d8e87615e7cf.png)

サーバー側のログで動作していることを確認しましょう。

## サーバーで仕組みを変えてみる

現在、サーバーでこのゲームの設定が管理されています。

サーバーのプログラムをちょっとだけ書き換えて、あいさつ文を変更したり、加算ポイントを増加させてたりしてしてみましょう。

![015275ca191cdae0d807906966ffdfe1](https://i.gyazo.com/015275ca191cdae0d807906966ffdfe1.png)

サーバー修正するのでいったん終了します。ターミナルで Ctrl + C をするとプログラムが終了しサーバーが終了します。

### term1-2-chapter02.js をエディタで開く

TODO
term1-2-chapter02.js をダブルクリックしてエディタを開きます。

### あいさつ変更

```js
// /api/post/title というパスで POST リクエストでアクセスすると「こんにちは！ようこそ！」というテキストが取得できます
app.post('/api/post/title', (req, res) => {
  console.log('あいさつメッセージ返答！');
  res.send('こんにちは！ようこそ！')
});
```

こちらの `res.send('こんにちは！ようこそ！')` が、Unity にデータを返答している部分です。このテキストを `res.send('こんばんわ！')` とメッセージを変更して保存しましょう。

### 加算ポイント変更

```js
// /api/post/title というパスで POST リクエストでアクセスすると「こんにちは！ようこそ！」というテキストが取得できます
app.post('/api/post/add_point', (req, res) => {
  console.log('ポイント加算設定返答！');
  res.send('1')
});
```

こちらの `res.send('1')` が、Unity にデータを返答している部分です。このテキストを `res.send('38')` とメッセージを変更して保存しましょう。

### サーバー再起動

ターミナルで再度 `node term1-2-chapter02.js` コマンドでサーバー動かします。

Unity をもう一度 Play ボタンを押して再生してみると、あいさつ文が変わり、クリック時の加算ポイントが 1 から 38 ポイントに変わって、増加量がアップしています。 

![8707ab6e5422a65642d8840893656830](https://i.gyazo.com/8707ab6e5422a65642d8840893656830.png)

このように、サーバーで設定を管理すれば、ゲーム内の変更はせずに、あいさつ文を一律変更できたり、ゲームの設定データを遠隔で一時的に変更しボーナスタイムを演出できたりと、いろいろな仕組みを加えることができます。

## 今回の Codespace の終了

![0a8b4cfb807e57ea1382292a757c6899](https://i.gyazo.com/0a8b4cfb807e57ea1382292a757c6899.png)

今回の Codespace 終了しておきましょう。