# 基礎となるゲームサンプルの共有と動作確認

![9d2c38e6fe48e61528f6b2d34370768f](https://i.gyazo.com/9d2c38e6fe48e61528f6b2d34370768f.png)

## この章で学ぶこと

基礎となるゲームサンプルの共有と動作確認を行います。

## Codespaced の再起動

- codespace の停止と開始 - GitHub Docs
  - https://docs.github.com/ja/codespaces/developing-in-codespaces/stopping-and-starting-a-codespace

こちらを参考に再起動します。

GitHub にログインした状態で https://github.com/codespaces にアクセスします。

![34de49185c6b28fb938519084d5b36fe](https://i.gyazo.com/34de49185c6b28fb938519084d5b36fe.png)

Codespaces のページです。

![6be56b218c122cfa36b4518208104104](https://i.gyazo.com/6be56b218c122cfa36b4518208104104.png)

さきほど使っていた Codespace をクリックして起動します。

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

![9a668436222b881cbfa0f45be98bdf22](https://i.gyazo.com/9a668436222b881cbfa0f45be98bdf22.png)

Project タブから Assets > Scenes を選択します。Scene01 をダブルクリックして起動しましょう。

![d9b23dbbd1c785f79b1fb51278755eba](https://i.gyazo.com/d9b23dbbd1c785f79b1fb51278755eba.png)

Cube が一つ配置されているシーンが表示されます。

## 動作確認をする

![2fbea7338e0832c54e0b977c39f5dedd](https://i.gyazo.com/2fbea7338e0832c54e0b977c39f5dedd.png)

Play ボタンをクリックします。

![6044c7e49cf4a9d7af2d62b94476d854](https://i.gyazo.com/6044c7e49cf4a9d7af2d62b94476d854.png)

Cube をマウスでクリックしてみましょう。

![cfe7587c4bb92695695695e3a2f291d4](https://i.gyazo.com/cfe7587c4bb92695695695e3a2f291d4.png)

Console でこのようなログが出てくれば成功です！まずはマウスクリックが動きました。