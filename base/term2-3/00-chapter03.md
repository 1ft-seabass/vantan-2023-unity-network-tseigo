# 後半のおさらい

![9d2c38e6fe48e61528f6b2d34370768f](https://i.gyazo.com/9d2c38e6fe48e61528f6b2d34370768f.png)

## この章で学ぶこと

後半のおさらいを行います。

## 質疑応答多めで行きたいと思います

![image](https://i.gyazo.com/aba8ccd625e7320883851b71ebd0caf2.png)

よろしくお願いします！

こんな質問や相談どうぞ！

- 前回の成果発表の説明を受けて聞きたいことがあります！
- こんなアイデアがあるんですけど今回の展示でアリですか？
- 今回のサンプルをこう発展させるのはどうしたらいいでしょう？
- 私のできることってデザイン寄りですがどういうのがいいですかね？
- 先日のこの辺り詳しく教えてほしいです！

## サンプル紹介してみます

![0315bfabadc8442391ad415f119e63c3](https://i.gyazo.com/0315bfabadc8442391ad415f119e63c3.png)

いくつかサンプルを紹介します。サーバの Codespace と Unity プロジェクトを最新にすれば、今回のサンプルが使えます。

## エラー検出は手厚く用意するとつながりやすい

![0315bfabadc8442391ad415f119e63c3](https://i.gyazo.com/0315bfabadc8442391ad415f119e63c3.png)

今回は、シンプルにリクエスト成功とリクエスト中しか検出していませんでしたが API をつなぐときに出てくる様々なエラーを検出して、つなぐための手掛かりにしていきましょう。

```csharp
Debug.Log("リクエスト開始");

// 結果によって分岐
switch (request.result)
{
    case UnityWebRequest.Result.InProgress:
        Debug.Log("リクエスト中");
        break;

    case UnityWebRequest.Result.ProtocolError:
        Debug.Log("ProtocolError");
        Debug.Log(request.responseCode);
        Debug.Log(request.error);
        break;

    case UnityWebRequest.Result.ConnectionError:
        Debug.Log("ConnectionError");
        break;

    case UnityWebRequest.Result.Success:
        Debug.Log("リクエスト成功");

        // コンソールに表示
        Debug.Log($"responseData: {request.downloadHandler.text}");

        break;
}
```