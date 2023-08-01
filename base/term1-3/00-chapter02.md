# いろいろとデータを調整する

![9d2c38e6fe48e61528f6b2d34370768f](https://i.gyazo.com/9d2c38e6fe48e61528f6b2d34370768f.png)

## この章で学ぶこと

いろいろとデータを調整する

- シンプルに動かしてみる
- 受け取ったデータをあいさつ文テキストに反映してみる（ResponseData.title）
- 自分の名前を送っていてサーバーであいさつ文を作っていることを確認（RequestData.name）
- 受け取ったデータをポイント加算に反映してみる（ResponseData.add_point）
- 実は term1-2 chapter02 のデータを JSON でまとめたことを確認
- ゲームポイントの記録を確認（RequestData.point）
- ゲームポイントの記録が成功すると記録ポイントが返ってくるのでテキストに反映してみる（ResponseData.recordPoint）
- 実はサーバーが起動している間、記録ポイントは保持されていることを確認
- 再起動してなくなることも確認


## Codespace の起動

![0a3a35f3418068b7713ddaa729f2c660](https://i.gyazo.com/0a3a35f3418068b7713ddaa729f2c660.png)

GitHub にログインした状態で https://github.com/codespaces にアクセスします。

![34de49185c6b28fb938519084d5b36fe](https://i.gyazo.com/34de49185c6b28fb938519084d5b36fe.png)

Codespaces のページです。さきほど使っていた Codespace をクリックして起動します。

## サーバの起動

![0a3a35f3418068b7713ddaa729f2c660](https://i.gyazo.com/0a3a35f3418068b7713ddaa729f2c660.png)

- ターミナルで `node term1-3-chapter02.js` をサーバ起動
- ポートタブで今回のサーバ起動を公開
- シークレットウィンドウで今回のサーバが公開されているか確認します

こちらの手順を進めます。

✅ポイント
- 今回は POST リクエストで 2 つの仕組みを作っています

## 今回の Unity シーンを起動

![6049726527f3133083e8ca07d1e6261c](https://i.gyazo.com/6049726527f3133083e8ca07d1e6261c.png)

Project タブから Assets > Scenes を選択します。Scene-Term1-3-Chapter02 をダブルクリックして起動しましょう。