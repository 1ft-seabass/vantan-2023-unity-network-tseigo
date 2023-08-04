# さまざまな API サービスの把握

![9d2c38e6fe48e61528f6b2d34370768f](https://i.gyazo.com/9d2c38e6fe48e61528f6b2d34370768f.png)

## この章で学ぶこと

さまざまな API サービスの把握をします。

## API とは（再確認）

さて、あらためて API とはこういうものです。

![image](https://i.gyazo.com/3edbe1e460cdd4d53d5880f071a47d30.png)

参考資料 : http://e-words.jp/w/API.html

![image](https://i.gyazo.com/25273e2cadab797efc93ec8610253ea4.png)

API とは、 Application Programming Interface の頭文字です。データを提供したり、何かしらの機能を提供するソフトウェアの一部を、私たちのような外部の人間が扱えるように公開されている窓口です。HTTP プロトコルでやり取りしていることが多いです。

たとえば、Web アプリケーションなどインターネットの様々な仕組みを構築するとき、 API からデータを取得して加工して表示することが多いです。データや機能を借り受けるということですね。

✅ポイント
- 

## API とクリエイティブ（再確認）

![image](https://i.gyazo.com/0d0557a56626670b5768cc533f90b737.png)

みなさんの「つくる」視点からも API は大事な役割あります。それは「API は技術同士をつなげる良き接着剤」というポイントです。

自分が API へつなげることで、自分だけでは用意できなかったデータや仕組みで制作物を面白くできたり、何かの API を存在を知ることで、自分の企画に新しい視点が生まれます。

<img src="https://i.gyazo.com/6ff6923d6ae5dee49fdf1bf1816b68ca.png" width="200" />

- アイデアのつくり方
  - 著 ジェームス W.ヤング
  - https://www.amazon.co.jp/gp/product/4484881047
- アイデアのつくり方 - Wikipedia
  - https://ja.wikipedia.org/wiki/%E3%82%A2%E3%82%A4%E3%83%87%E3%82%A2%E3%81%AE%E3%81%A4%E3%81%8F%E3%82%8A%E6%96%B9

何かをつくっていく上で、とても勉強になるクリエイティブの古典で「アイデアのつくり方」というジェームス W.ヤング氏の書かれた本があります。

![image](https://i.gyazo.com/50eea765175a7d9a4d4c4a38636a8195.png)

この中で「アイデアは既存の要素の新しい組み合わせである」とあります。様々な技術とつながって新しい世界（データ）をみせてくれる API は、カジュアルに発想の組み合わせをしていく助けになります。

![image](https://i.gyazo.com/ca62ef1b64e4d0b133bfe8491b36d000.png)

さて、こちらの図は、私が使ったことのある API や、まだ使ったことはないが知っている API をまとめてみたものです。

みなさんもイチから仕組みを構築してシステムをつくることももちろん大事ですが、このように API を知ることで、データを用意出来たり、ひとりでは難しい仕組みを導入出来たり、API を通じて新しい技術に触れることができます。

✅ポイント
- 

## そしてなにより API は HTTP

![96b1357e0be36546141716fa6d6aa5f0](https://i.gyazo.com/96b1357e0be36546141716fa6d6aa5f0.png)

## API をながめてみよう

![image](https://i.gyazo.com/ca62ef1b64e4d0b133bfe8491b36d000.png)

私がまとめたこの図のように API にはこのような広がりがあります。

![image](https://i.gyazo.com/b3c1f4c2b1625cba88d3e862fcb7570e.png)

フリーのAPIのリストコレクション [public\-apis](https://github.com/public-apis/public-apis) をご紹介します。

- public-apis
  - https://github.com/public-apis/public-apis

英語ですが、実に 100 以上の API があり見ているだけで楽しいです。しかも定期的にメンテナンスされています。実は柴犬画像 API もこの中で紹介されているもののひとつです。

![image](https://i.gyazo.com/9605a51706aeac4dfbe3143a13397207.png)

各 API では

- Auth
  - 使うために認証が必要か
  - ないものは特別のユーザー登録が必要なく柴犬画像 API のような使いやすいリクエスト GET リクエストでアクセスできたりする
- HTTPS
  - セキュアな通信でつながるか
- CORS
  - クロスドメイン制約（ドメインの違うところからのアクセスに関する制約）がないか

という項目で、使い方がザっと把握できます。

以下の点を注目しておくと使いやすいものを探せるでしょう。

- Auth
  - No のものは特別のユーザー登録が必要なく柴犬画像 API のような使いやすいリクエスト GET リクエストでアクセスできたりする
- CORS
  - ブラウザでのクロスドメイン制約（ドメインの違うところからのアクセスに関する制約）がないか
  - ないとアクセスしやすい。Unity 単体でのアクセスであれば気にしなくてよい。

ということで、

![image](https://i.gyazo.com/72e0eee127c60dc5d51544f642d70b7b.png)

いろいろな API を紹介していきます！

今回紹介した API たちのように、すぐに作れるツールやアプローチを知っていることで、よりつくるためのアイデアが増えていくので、手を動かしつつ技術に触れつつ、鍛えていきましょう。

✅ポイント
- ひとまず試すなら Auth なしで GET リクエストだとデータが取り出しやすかったりします

## 今回は CodeSpaces は起動しません

![13de54927bc6437f8b51d6a60e676a6a](https://i.gyazo.com/13de54927bc6437f8b51d6a60e676a6a.png)

外部の API にいよいよつなげるので、起動しません。もちろん、後半のほうで、また学ぶために使います。

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

## ひま API (Bored API) につなげてみましょう

![aae5fcbb30bf9d55b7249a6d6bd44697](https://i.gyazo.com/aae5fcbb30bf9d55b7249a6d6bd44697.png)

https://www.boredapi.com/ という「ひまなときに、何かしてみようという」ものを英語ですがテキストを返してくれる面白い API です。

ドキュメント https://www.boredapi.com/ を見てみると GET リクエストで `https://www.boredapi.com/api/activity?participants=1` でアクセスすると、

```js
{
  "activity": "Learn about a distributed version control system such as Git",
  "type": "education",
  "participants": 1,
  "price": 0,
  "link": "https://en.wikipedia.org/wiki/Distributed_version_control",
  "key": "9303608",
  "accessibility": 0
}
```

といった値が返ってくることがわかります。今回は、実際に暇のつぶし方のテキストである activity 値だけを読み込んでみましょう。

## 今回の Unity シーンを起動

![6049726527f3133083e8ca07d1e6261c](https://i.gyazo.com/6049726527f3133083e8ca07d1e6261c.png)

Project タブから Assets > Scenes を選択します。Scene-Term1-4-Chapter01 をダブルクリックして起動しましょう。

## Term1_4_Chapter01_CubeEvent01.cs を見てみる

Cube オブジェクトの `Assets/Scripts/Term1_4_Chapter01_CubeEvent01.cs` で実際の動作が書かれています。こちらをエディタで開きます。

```csharp
using UnityEngine;
using UnityEngine.EventSystems;

using System.Collections;       // IEnumerator のための参照
using UnityEngine.Networking;   // UnityWebRequest のための参照
using System;                   // Serializable のための参照

public class Term1_4_Chapter01_CubeEvent01 : MonoBehaviour, IPointerClickHandler
{
    // アクセスする API の URL
    // https://www.boredapi.com/
    string urlAPI = "https://www.boredapi.com/api/activity?participants=1";

    // 受信した JSON データを Unity で扱うデータにする ResponseData ベースクラス
    [Serializable]
    public class ResponseData
    {
        // activity というプロパティ名で string 型で変換
        // activity だけ取得
        public string activity;
    }

    void Start()
    {
        
    }

    public void OnPointerClick(PointerEventData eventData)
    {
        // マウスクリックイベント

        // HTTP リクエストを非同期処理を待つためコルーチンとして呼び出す
        StartCoroutine("GetData");
    }

    // GET リクエストする本体
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
                this.transform.Find("MessageText").GetComponent<TextMesh>().text = response.activity;

                break;
        }


    }

    void Update()
    {
        
    }
}
```

## 質疑応答

![image](https://i.gyazo.com/aba8ccd625e7320883851b71ebd0caf2.png)

ここまでで質問があればどうぞ！