# データ活用例の体験

![9d2c38e6fe48e61528f6b2d34370768f](https://i.gyazo.com/9d2c38e6fe48e61528f6b2d34370768f.png)

## この章で学ぶこと

- データ活用例の体験として、データをみんなでシェアします。
- OpenAI 社の ChatGPT API を試してみます

## データ活用例の体験として、データをみんなでシェアします

![02db792fd629a56812a205234a08ae44](https://i.gyazo.com/02db792fd629a56812a205234a08ae44.png)

[前章の chapter03 のサンプル](../term2-2/00-chapter03.md) を動かしてみて、サーバーを講師の起動した URL でみんな設定してみて「みんなでデータをシェア」を体験します。

## 今回の Unity シーンを起動

![6049726527f3133083e8ca07d1e6261c](https://i.gyazo.com/6049726527f3133083e8ca07d1e6261c.png)

Project タブから Assets > Scenes を選択します。Scene-Term2-3-Chapter01 をダブルクリックして起動しましょう。

## ChatGPT の API キーを設定

```csharp
// ChatGPT の API キーを入力
public string tokenCHatGPT = "tokenCHatGPT";
```

こちらで自分の取得した ChatGPT の API キーを設定 を入力して保存しましょう。

## 動かしてみる

![fb6deee20969f2b1e41528b8276d1be2](https://i.gyazo.com/fb6deee20969f2b1e41528b8276d1be2.png)

クリックして動かしてみましょう！

## ざっくり解説

![image](https://i.gyazo.com/aba8ccd625e7320883851b71ebd0caf2.png)

時間の許す限り、ソースコードや API 仕様を解説します。