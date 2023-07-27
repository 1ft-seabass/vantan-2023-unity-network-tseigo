# ゲームサンプルからサーバーの仕組みとの疎通

![9d2c38e6fe48e61528f6b2d34370768f](https://i.gyazo.com/9d2c38e6fe48e61528f6b2d34370768f.png)

## この章で学ぶこと

ゲームサンプルからサーバーの仕組みとの疎通を行います。

## 外部サーバーの多くは HTTP プロトコルでつながる

![771bd9213b5426398ade19423c9a1433](https://i.gyazo.com/771bd9213b5426398ade19423c9a1433.png)

外部サーバーの多くは HTTP プロトコルで構成されています。今回のサーバーもそうです。

ですので、外部サーバーのやりとりを扱うときに読み解くために HTTP の仕組みを覚えておくと、やりとりできるようになるので、みなさんの制作の幅が広がります。

## HTTP について

HTTP プロトコルについて概要を把握します。

HTTP は Hypertext Transfer Protocol という正式名称です。 Web ブラウザが Web サーバと通信する際に主として使用する通信プロトコルです。

よくある例としては、みなさんが Web ブラウザからアドレスバーで URL を入力して HTML などのテキストによって記述された Web ページなどのコンテンツを表示するときのデータの送受信に用いられます。

参考文献
- Hypertext Transfer Protocol - Wikipedia
  - https://ja.wikipedia.org/wiki/Hypertext_Transfer_Protocol
- HTTP の基本 - HTTP | MDN
  - https://developer.mozilla.org/ja/docs/Web/HTTP/Basics_of_HTTP

実際には、このような仕組みになっています。

> HTTPはリクエスト-レスポンス型のプロトコルであり、クライアントがサーバにリクエストメッセージを送信する。 基本的な考え方は非常に単純で、「何を」「どうして」欲しいのかを伝える。URLが「何を」、メソッドが「どうして」に当たる。 サーバはこれにレスポンスメッセージを返し、基本的にこの時点で初期状態に戻る。つまり、サーバはクライアントの状態を保存しない。
>
> Hypertext Transfer Protocol - Wikipedia - https://ja.wikipedia.org/wiki/Hypertext_Transfer_Protocol

この説明は、仕様をちゃんと説明してはいるのですが、ちょっととっつきにくいかもしれません。もう少し、噛み砕いていきましょう。

![image](https://i.gyazo.com/8d8b5bcd165aa9851160c0aeac32169d.png)

こちらの図を見つつ、[典型的な HTTP セッション](https://developer.mozilla.org/ja/docs/Web/HTTP/Session) を追っていきます。

まず、クライアントからサーバーへ URL で「何か」決めて問い合わせます。また、HTTP ヘッダーでクライアントからサーバーが追加情報を渡すことができます。

- HTTP メソッド
  - リソースに対して実行したいアクションを宣言します。いろいろありますが GET と POST を使うことが多いです。
  - https://developer.mozilla.org/ja/docs/Web/HTTP/Headers
- HTTP ヘッダー
  - HTTP リクエストやレスポンスでクライアントやサーバーが追加情報を渡すことができます
  - https://developer.mozilla.org/ja/docs/Web/HTTP/Headers

![image](https://i.gyazo.com/03d1c316f872a525a4bb30e7fffa412a.png)


そして、サーバーが HTTP リクエストから受け取った内容で、今度は HTTP レスポンスという形で応答します。こちらの図を見つつ、[典型的な HTTP セッション](https://developer.mozilla.org/ja/docs/Web/HTTP/Session) を追っていきます。

まず、HTTP ヘッダーでサーバーからクライアントへ追加情報を渡すことができます。そして、HTTP 応答ステータスコードで正常に完了したどうかを伝えます。こちらを、みなさんのブラウザが受信すると Web ページが表示されます。

- HTTP 応答ステータスコード（HTTP レスポンスステータスコード）
  - 特定の HTTP リクエストが正常に完了したどうかを示します。200 が Success で応答成功です。その他に、有名なものとして 404 , 500 , 503 などがあります。
  - 404 Not Found
    - サーバーがリクエストされたリソースを発見できないこと
  - 500 Internal Server Error
    - サーバー側で処理方法がわからない事態が発生したことを示します。
  - 503 Service Unavailable
    - サーバーはリクエストを処理する準備ができていないことを示します。
  - 参考文献（一覧はこちら）
    - https://developer.mozilla.org/ja/docs/Web/HTTP/Status

全体の図としては以下の通りです。

![image](https://i.gyazo.com/6052386b6f5bdf2b17b7692149fd2d92.png)

本来、みなさんのブラウザで URL にアクセスして何かしらが表示されるまでには、このような流れで行われています。いろいろありますね。

ですが、いま、すべて覚える必要はないです。 HTTP プロトコルを扱うために、ざっくりこのような流れになっているんだなと理解できていれば OK です。

雰囲気での理解は、あとで生きてきます！

## Unity における HTTP 

### Unity でつなげる公式ドキュメント

- 共通操作 - HLAPI の使用 - Unity マニュアル
  - https://docs.unity3d.com/ja/2019.4/Manual/UnityWebRequest-HLAPI.html

こちらに文献があります。

### メジャーな GET と POST リクエストの文献

GET リクエスト

- HTTP サーバーからテキストやバイナリデータを取得 (GET) - Unity マニュアル
  - https://docs.unity3d.com/ja/2019.4/Manual/UnityWebRequest-RetrievingTextBinaryData.html

POST リクエスト例

- HTTP サーバーにフォームを送信 (POST) - Unity マニュアル
  - https://docs.unity3d.com/ja/2019.4/Manual/UnityWebRequest-SendingForm.html
  - 参考にはなるが、最近のユースケースでは、必ずしもフォームでデータをやり取りするわけではないです
- 【Unity】UnityWebRequest で JSON を POST 通信するサンプル - コガネブログ
  - https://baba-s.hatenablog.com/entry/2020/11/16/080000_9
  - JSON データを送るところではこちらのほうが参考になります

## 今回は HTTP GET で一点突破します

次の章では、ブラウザで表示して確認もできる GET リクエストの API でサッと試してみます。

![864f04a4ab4903aa57d39a7f41dc8b8b](https://i.gyazo.com/864f04a4ab4903aa57d39a7f41dc8b8b.png)

Codespace で起動したサーバーに Unity からつなぎます。

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

## 今回の Codespace の終了

![0a8b4cfb807e57ea1382292a757c6899](https://i.gyazo.com/0a8b4cfb807e57ea1382292a757c6899.png)

今回の Codespace 終了しておきましょう。
