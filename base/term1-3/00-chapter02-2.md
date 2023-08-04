# 画像を読み込んでみる

## Codespace の起動

![0a3a35f3418068b7713ddaa729f2c660](https://i.gyazo.com/0a3a35f3418068b7713ddaa729f2c660.png)

GitHub にログインした状態で https://github.com/codespaces にアクセスします。

![34de49185c6b28fb938519084d5b36fe](https://i.gyazo.com/34de49185c6b28fb938519084d5b36fe.png)

Codespaces のページです。さきほど使っていた Codespace をクリックして起動します。

## サーバの起動

![0a3a35f3418068b7713ddaa729f2c660](https://i.gyazo.com/0a3a35f3418068b7713ddaa729f2c660.png)

- ターミナルで `node term1-3-chapter02.js` をサーバ起動
  - 実際は public フォルダを読みこむ機能だけなのでどのプログラムでも動きます。
- ポートタブで今回のサーバ起動を公開
- シークレットウィンドウで今回のサーバが公開されているか確認します

こちらの手順を進めます。

✅ポイント
- public フォルダに sample01.png と sample02.png というサンプル画像が入っています。

## 今回の Unity シーンを起動

![6049726527f3133083e8ca07d1e6261c](https://i.gyazo.com/6049726527f3133083e8ca07d1e6261c.png)

Project タブから Assets > Scenes を選択します。Scene-Term1-3-Chapter02-2 をダブルクリックして起動しましょう。

今日は、このプログラムをベースに、送る値や受け取る値を Unity に使っていきます。

- HTTP サーバーからテクスチャを取得 (GET) - Unity マニュアル
  - https://docs.unity3d.com/ja/2019.4/Manual/UnityWebRequest-RetrievingTexture.html


を参考に画像をテクスチャに読み込んでみましょう。

✅ポイント
- 

## Term1_3_Chapter02_GetImage.cs 変更

Cube にコンポーネントとして割り当てられている `Assets/Scripts/Term1_3_Chapter02_GetImage.cs` をエディタで開きます。

```csharp
using UnityEngine;
using UnityEngine.EventSystems;

using System.Collections;       // IEnumerator のための参照
using UnityEngine.Networking;   // UnityWebRequest のための参照

public class Term1_3_Chapter02_GetImage : MonoBehaviour, IPointerClickHandler
{
    void Start()
    {
        
    }

    // アクセスする URL
    // サーバーURL + /sample01.png でアクセス
    string urlGitHub = "ここにサーバーURLを入れる";

    public void OnPointerClick(PointerEventData eventData)
    {
        // マウスクリックイベント

        // HTTP リクエストを非同期処理を待つためコルーチンとして呼び出す
        StartCoroutine("GetTexture");
    }

    IEnumerator GetTexture()
    {
        // テクスチャを GET リクエストで読み込む。ブラウザでも見れる。
        UnityWebRequest request = UnityWebRequestTexture.GetTexture(urlGitHub);

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

                GameObject.Find("Tile01").GetComponent<MeshRenderer>().material.SetTexture("_MainTex", loadedTexture);

                break;
        }
    }
}
```

以下を修正します。

```csharp
// アクセスする URL
// サーバーURL + /sample01.png でアクセス
string urlGitHub = "ここにサーバーURLを入れる";
```

こちらをサーバー URL に `/sample01.png` というパスを加えて変更して保存します。

## 動かしてみる

まずは、サーバーへつなぐ設定ができたので動かしてみましょう。

![ad833d19086696f4841ff7d11828b4fb](https://i.gyazo.com/ad833d19086696f4841ff7d11828b4fb.png)

Play ボタンをクリックします。

![3d81f9d98fd255f2ed1f6c1ca3705555](https://i.gyazo.com/3d81f9d98fd255f2ed1f6c1ca3705555.png)

Cube をクリックするとこのように画像が読み込まれテクスチャに適用されて表示します。

## 今回の Codespace の終了

![0a8b4cfb807e57ea1382292a757c6899](https://i.gyazo.com/0a8b4cfb807e57ea1382292a757c6899.png)

今回の Codespace 終了しておきましょう。