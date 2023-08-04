# ゲーム結果のデータを送ってみよう

![9d2c38e6fe48e61528f6b2d34370768f](https://i.gyazo.com/9d2c38e6fe48e61528f6b2d34370768f.png)

## この章で学ぶこと

ゲーム結果のデータを送ってみよう

この章では、Unity からシンプルなゲーム結果ポイント 1000 pt をJsonUtility を使って JSON データを作成してサーバに送ってみます。

## 授業をはじめる前に教材の更新

Codespace と Unity プロジェクトを更新します。

- Codespace
  - Codespace 削除の体験
  - 再度リポジトリにアクセスして最新コードで Codespace 起動
- Unity プロジェクト
  - 手元のソースコードフォルダを削除
  - 再度リポジトリにアクセスして最新コードをダウンロード
  - Unity Hub で起動

を行います。

## Codespace 削除

![0a3a35f3418068b7713ddaa729f2c660](https://i.gyazo.com/0a3a35f3418068b7713ddaa729f2c660.png)

GitHub にログインした状態で https://github.com/codespaces にアクセスします。

![016de554e3ab779c598ac69607955af2](https://i.gyazo.com/016de554e3ab779c598ac69607955af2.png)

今回使っている Codespace を探します。

![abd033cda989bfdd5a094d922bb6cfbc](https://i.gyazo.com/abd033cda989bfdd5a094d922bb6cfbc.png)

Delete をクリックして削除します。

## 今回の GitHub Codespaces リポジトリにアクセス

今回の GitHub Codespaces リポジトリに Chrome ブラウザでアクセスします。

![1d4fe9d0e6c86377c17828a2ff26fd0d](https://i.gyazo.com/1d4fe9d0e6c86377c17828a2ff26fd0d.png)

https://github.com/1ft-seabass/vantan-unity-network-server-base にアクセスします。

## GitHub Codespaces としてリポジトリを開く

![6ebad95a052d8a2d37d889399e120424](https://i.gyazo.com/6ebad95a052d8a2d37d889399e120424.png)

Code ボタンをクリックします。

![8f6a286108378103ac8d30df6f811ef4](https://i.gyazo.com/8f6a286108378103ac8d30df6f811ef4.png)

Codespaces タブをクリックします。Create codespace on main をクリックします。

![47b24d3be5b687f60383455a75898788](https://i.gyazo.com/47b24d3be5b687f60383455a75898788.png)

Setting up your codespace という画面が出て構築されます。

![28ea2b9aece0957b5bb7292427889a10](https://i.gyazo.com/28ea2b9aece0957b5bb7292427889a10.png)

ブラウザ上で Visual Studio Code が起動し、今回の仕組みを反映した環境が起動しました。

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