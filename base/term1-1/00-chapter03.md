# 基礎となるゲームサンプルの共有と動作確認

![9d2c38e6fe48e61528f6b2d34370768f](https://i.gyazo.com/9d2c38e6fe48e61528f6b2d34370768f.png)

## この章で学ぶこと

基礎となるゲームサンプルの共有と動作確認を行います。

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

## シーンを開く

![6049726527f3133083e8ca07d1e6261c](https://i.gyazo.com/6049726527f3133083e8ca07d1e6261c.png)

Project タブから Assets > Scenes を選択します。Scene-Term1-1-Chapter03 をダブルクリックして起動しましょう。

![d9b23dbbd1c785f79b1fb51278755eba](https://i.gyazo.com/d9b23dbbd1c785f79b1fb51278755eba.png)

Cube が一つ配置されているシーンが表示されます。

## 動作確認をする

![2fbea7338e0832c54e0b977c39f5dedd](https://i.gyazo.com/2fbea7338e0832c54e0b977c39f5dedd.png)

Play ボタンをクリックします。

![6044c7e49cf4a9d7af2d62b94476d854](https://i.gyazo.com/6044c7e49cf4a9d7af2d62b94476d854.png)

Cube をマウスでクリックしてみましょう。

![cfe7587c4bb92695695695e3a2f291d4](https://i.gyazo.com/cfe7587c4bb92695695695e3a2f291d4.png)

Console でこのようなログが出てくれば成功です！

まずはマウスクリックが動きました。

## シーンの仕組みの解説

![ae6172228f962578c4c19763b03360d2](https://i.gyazo.com/ae6172228f962578c4c19763b03360d2.png)

（時間があれば）シーンの仕組みを解説します。

✅ポイント
- Cube には CubeEvent というスクリプトが関連づけられシンプルなクリックイベントが書かれています
- イベントまわりは Main Camera の Pyshics Raycaster と EventSystem の設置で対応しています

## Codespace の再起動

- codespace の停止と開始 - GitHub Docs
  - https://docs.github.com/ja/codespaces/developing-in-codespaces/stopping-and-starting-a-codespace

こちらを参考に再起動します。

GitHub にログインした状態で https://github.com/codespaces にアクセスします。

![34de49185c6b28fb938519084d5b36fe](https://i.gyazo.com/34de49185c6b28fb938519084d5b36fe.png)

Codespaces のページです。

![6be56b218c122cfa36b4518208104104](https://i.gyazo.com/6be56b218c122cfa36b4518208104104.png)

さきほど使っていた Codespace をクリックして起動します。

## サーバーの起動

```
node server01.js
```

ターミナルで以下のコマンドを入力して Enter キーを押して実行します。

```
server01 start!
app listening at http://localhost:8080
```

というメッセージが次の行に出てくれば起動成功です。これで無事サーバーが起動できました。

## 自分の GitHub アカウントのみで見えることを確認

![ad43d16f32933e425e9818fafd1ee031](https://i.gyazo.com/ad43d16f32933e425e9818fafd1ee031.png)

現在この Codespace でサーバー起動している状況はポートタブから確認できます。ターミナルタブのポートをクリックしてポートタブを表示します。

![55758bc0dc28422bc1dc42bd8c6ac725](https://i.gyazo.com/55758bc0dc28422bc1dc42bd8c6ac725.png)

このように 8080 ポートで起動していることがわかり、表示範囲がまだ Private になっていることを確認します。

![5119ac8b2b9bc81ee2dc1a5a12d479e6](https://i.gyazo.com/5119ac8b2b9bc81ee2dc1a5a12d479e6.png)

こちらの地球儀マークをクリックすると、現在のブラウザで新しいタブが開いてサーバーが確認できます。

![75ef12af4b9fa57857d6a5cc1e04e6bb](https://i.gyazo.com/75ef12af4b9fa57857d6a5cc1e04e6bb.png)

Index というページが表示されます。

これは server01.js の

```js
// public フォルダ内にあるファイルはパスが一致していると呼びだせます
// /index.html や / の場合は public フォルダ内の index.html が表示されます
app.use(express.static(__dirname + '/public'));
```

の、仕組みで public フォルダ内の index.html が表示されています。

この Private 状態でも見える理由は、いまのブラウザで GitHub アカウントにログインしているので自分の GitHub アカウントのみで見える状況です。

![cec370c19d64e05d74af2bd84cab7aa1](https://i.gyazo.com/cec370c19d64e05d74af2bd84cab7aa1.png)

今のままだと、Unity からはアクセスできません。

## シークレットウィンドウで自分の GitHub アカウント以外で見れないことを把握

![364a7b4d7e0db1811b34739e6ecc50d4](https://i.gyazo.com/364a7b4d7e0db1811b34739e6ecc50d4.png)

手軽にアカウントをログインしていない状態で見るなら Chrome のシークレットウィンドウ機能は便利です。

右上のメニューから新しいシークレットウィンドウをクリックしてシークレットウィンドウを起動します。

![fb0b95a3e4ae0ba4e207e5c6813b9772](https://i.gyazo.com/fb0b95a3e4ae0ba4e207e5c6813b9772.png)

新しいシークレットウィンドウが表示されました。

![09b0473d51bd8a7227a41b6c08b3c32a](https://i.gyazo.com/09b0473d51bd8a7227a41b6c08b3c32a.png)

今回のサーバーの行のクリップボードマークをクリックして今回の URL をコピーしましょう。

今回のシークレットウィンドウのアドレスバーに URL をコピーしてペーストしてアクセスしてみましょう。

![3a24e8de9f75efbab253cc776f46d4da](https://i.gyazo.com/3a24e8de9f75efbab253cc776f46d4da.png)

このように GitHub のログインページになりアクセスできないことが分かります。なお、別の GitHub アカウントでログインして、今回の URL を見ようとしても 404 エラーになり、外部や別ユーザーから見れないことが分かります。

なお、このシークレットウィンドウは、このあとの公開後に公開チェックをするので、閉じずにそのままにしておいてください。

## サーバーの使っているポートを公開する

![55758bc0dc28422bc1dc42bd8c6ac725](https://i.gyazo.com/55758bc0dc28422bc1dc42bd8c6ac725.png)

ポートタブに戻ります。

![d531dea56766a4a10b71457abf505531](https://i.gyazo.com/d531dea56766a4a10b71457abf505531.png)

今回のサーバーが動いている 8080 の行を右クリックして、ポートの表示範囲 > Private となっているところを Public に変更します。

![01482cb73eb19684ff0e0e564ccee505](https://i.gyazo.com/01482cb73eb19684ff0e0e564ccee505.png)

公開範囲が Private から Public になります。これで公開は完了です。

![09b0473d51bd8a7227a41b6c08b3c32a](https://i.gyazo.com/09b0473d51bd8a7227a41b6c08b3c32a.png)

今回のサーバーの行のクリップボードマークをクリックして今回の URL をコピーしましょう。

今回のシークレットウィンドウのアドレスバーに URL をコピーしてペーストしてアクセスしてみましょう。公開ができていて Index が表示されるか確認しましょう。

![864f04a4ab4903aa57d39a7f41dc8b8b](https://i.gyazo.com/864f04a4ab4903aa57d39a7f41dc8b8b.png)

これで Unity ともやり取りできるようになります。

## 今回の Codespace の終了

![0a8b4cfb807e57ea1382292a757c6899](https://i.gyazo.com/0a8b4cfb807e57ea1382292a757c6899.png)

今回の Codespace 終了しておきましょう。

Unity は起動しっぱなしで OK です。