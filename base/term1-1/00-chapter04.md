# ゲームサンプルからサーバーの仕組みとの疎通

![9d2c38e6fe48e61528f6b2d34370768f](https://i.gyazo.com/9d2c38e6fe48e61528f6b2d34370768f.png)

## この章で学ぶこと

ゲームサンプルからサーバーの仕組みとの疎通を行います。

## Codespaced の起動

![0a3a35f3418068b7713ddaa729f2c660](https://i.gyazo.com/0a3a35f3418068b7713ddaa729f2c660.png)

GitHub にログインした状態で https://github.com/codespaces にアクセスします。

![34de49185c6b28fb938519084d5b36fe](https://i.gyazo.com/34de49185c6b28fb938519084d5b36fe.png)

Codespaces のページです。さきほど使っていた Codespace をクリックして起動します。

## サーバの起動

![0a3a35f3418068b7713ddaa729f2c660](https://i.gyazo.com/0a3a35f3418068b7713ddaa729f2c660.png)

- ターミナルで `node server01.js` をサーバ起動
- ポートタブで今回のサーバ起動を公開
- シークレットウィンドウで今回のサーバが公開されているか確認します

こちらの手順を進めます。

## 今回の Unity シーンを起動

![6049726527f3133083e8ca07d1e6261c](https://i.gyazo.com/6049726527f3133083e8ca07d1e6261c.png)

Project タブから Assets > Scenes を選択します。Scene02 をダブルクリックして起動しましょう。

## シーンの仕組みの解説

![ae6172228f962578c4c19763b03360d2](https://i.gyazo.com/ae6172228f962578c4c19763b03360d2.png)

シーンの仕組みを解説します。

✅ポイント
- Scene01 と同じイベントの仕組みです
- Cube には CubeEvent02 というスクリプトがむずびついています
  - Scene01 で使われた CubeEventではないです
- CubeEvent02 に今回の URL にアクセスする

## CubeEvent02.cs の変更

CubeEvent02.cs のスクリプトはブラウザで表示できるデータにアクセスすることができます。

![09b0473d51bd8a7227a41b6c08b3c32a](https://i.gyazo.com/09b0473d51bd8a7227a41b6c08b3c32a.png)

今回のサーバーの行のクリップボードマークをクリックして今回の URL をコピーしましょう。

```csharp
        // HTTP リクエストする(GET メソッド) UnityWebRequest を呼び出し
        // アクセスする先は変数 urlGitHub で設定
        UnityWebRequest request = UnityWebRequest.Get(urlGitHub);
```

こちらの行が Unity で HTTP リクエストしている行です。HTTP リクエストする(GET メソッド) UnityWebRequest を呼び出しています。アクセスする先は変数 urlGitHub で設定しているので、このスクリプトの上部にある変数 urlGitHub に注目します。

```csharp
    // アクセスする URL
    string urlGitHub = "ここにサーバーURLを入れる";
```

変数 urlGitHub は、こちらです。

`ここにサーバーURLを入れる` のところを、今回の GitHub の URL に置き換えてスクリプトを保存します。

## 動かしてみる

![ad833d19086696f4841ff7d11828b4fb](https://i.gyazo.com/ad833d19086696f4841ff7d11828b4fb.png)

Play ボタンをクリックします。

![6044c7e49cf4a9d7af2d62b94476d854](https://i.gyazo.com/6044c7e49cf4a9d7af2d62b94476d854.png)

Cube をマウスでクリックしてみましょう。GitHub の URL にアクセスします。

![593ace4fa0bb0e5c367da426e94e14bf](https://i.gyazo.com/593ace4fa0bb0e5c367da426e94e14bf.png)

Console でこのようなログが出てくれば成功です！ブラウザで見ていた Index の HTML ファイルのデータを見ることができます。

## httpbin も試してみる