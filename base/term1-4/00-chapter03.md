# 前半のおさらい

![9d2c38e6fe48e61528f6b2d34370768f](https://i.gyazo.com/9d2c38e6fe48e61528f6b2d34370768f.png)

## この章で学ぶこと

前半のおさらいをしましょう。

## 質疑応答多めで行きたいと思います

![image](https://i.gyazo.com/aba8ccd625e7320883851b71ebd0caf2.png)

よろしくお願いします！

## カジュアルに試すなら GET リクエスト

![147af28193f674986f4e8f00009f1698](https://i.gyazo.com/147af28193f674986f4e8f00009f1698.png)

外部 API をカジュアルに試すなら、なるべく設定の少ない GET リクエストでアクセスできる API が試すのにはおススメです。そのうえで POST リクエストで設定が必要なものにステップアップしていきましょう。

## ひとまず、自分のゲームの仕組みのデータを、外に送ってみよう

![0cb576bcc9cda870c381adb4a43d863a](https://i.gyazo.com/0cb576bcc9cda870c381adb4a43d863a.png)

自分の仕組みに、とりあえず加えていくのを試したいのであれば、ゲームポイントのサンプルのように内部のデータを外部に送ってみることを試してみましょう。

また、ゲームの設定値を外部から取り込むのも、いろいろ用途が広がると思います。もちろん後半でもより深掘りしていきますが、今のうちから企画や開発方針を考えておきましょう。

## ツールの紹介

### 送ったデータを自分に折り返して確認できる httpbin

![fbe6aff58d93a80ec6ce37eff039b828](https://i.gyazo.com/fbe6aff58d93a80ec6ce37eff039b828.png)

外部 API にどういうデータを送ったかを把握しづらい問題は httpbin https://httpbin.org/ という サービスを使ってもよいです。

✅参考資料
- APIクライアント開発時のモックに使えるhttpbinの紹介 - Qiita
  - https://qiita.com/sameyasu/items/adacceb8a1bee893599b

![27ad8b6ffa1c707d8ce8ca6bd3f1e194](https://i.gyazo.com/27ad8b6ffa1c707d8ce8ca6bd3f1e194.png)

GET リクエストの場合は https://httpbin.org/get に送ります。POST リクエストの場合は https://httpbin.org/post に送ります。

### VSCode REST Client 機能拡張

![f717cdc6603a9e727820a55cba00ed31](https://i.gyazo.com/f717cdc6603a9e727820a55cba00ed31.png)

Web ブラウザでは GET リクエストしか試せないとお伝えしましたが VSCode の拡張機能で様々なデータの送り方が試せる REST Client　機能拡張というのがあります。うまくつながるか確かめるには使いやすいツールですので、ぜひ試してみましょう。

✅参考資料
- VS Code上でHTTPリクエストを送信し、VS Code上でレスポンスを確認できる「REST Client」拡張の紹介 - Qiita
  - https://qiita.com/toshi0607/items/c4440d3fbfa72eac840c

## Codespaces 停止後の自動削除の話

![ce561ee73bcbc8a765828b73685cd7a8](https://i.gyazo.com/ce561ee73bcbc8a765828b73685cd7a8.png)

くわしくはこちら。

https://docs.github.com/ja/codespaces/customizing-your-codespace/configuring-automatic-deletion-of-your-codespaces?tool=webui

> 既定では、GitHub Codespaces は、停止して、非アクティブな状態で 30 日間が過ぎると、自動的に削除されます。

ということで、よく使うものは、定期的に起動して保持しておきましょう。

また、Keep codespace でも保持することができます。

> 個人設定で定義されている保持期間よりも長く保持したい codespace がある場合があります。 それを行うには、[Keep codespace] オプションを使います。 このオプションを選択すると、codespace は無期限に、手動で削除するまで保持されます。

