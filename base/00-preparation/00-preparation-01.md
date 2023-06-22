# 事前準備

![e9dd44a207adb9344320ce0f17fabf19](https://i.gyazo.com/e9dd44a207adb9344320ce0f17fabf19.png)
本授業では以下の準備が必要です。

## Unity 2020.3.48f をインストール

![5711e16c5c561b25df44d2bf72063db1](https://i.gyazo.com/5711e16c5c561b25df44d2bf72063db1.png)

最新の Unity Hub がインストールされている前提で進めます。

![9bb813dfb2549bf95d728da1250d402a](https://i.gyazo.com/9bb813dfb2549bf95d728da1250d402a.png)

左メニューから Installs をクリックして、右上の Install Editor ボタンをクリックします。

![f27a7037d9a25e10ac255d445261e141](https://i.gyazo.com/f27a7037d9a25e10ac255d445261e141.png)

Install Unity Editor の画面から Official releases > LONG TERM SUPPORT (LTS) から `2020.3.48f` の Install ボタンをクリックします。

もし　2020.3 台で新しい LTS のバージョンが出ていたら、そちらをクリックします。

![87c286f7c629f8c07ba65ac72e7442ee](https://i.gyazo.com/87c286f7c629f8c07ba65ac72e7442ee.jpg)

Add modules では DEV TOOLS の Microsoft Visual Studio Community 2019 が、インストールされていれば、あとは何もチェックせず Install ボタンをクリックします。

![ff923ad9f642fcf1332a558c92556f6c](https://i.gyazo.com/ff923ad9f642fcf1332a558c92556f6c.png)

ダウンロードを待ちます。

![504c7b73bdc51e80c1bed8bdc09e886d](https://i.gyazo.com/504c7b73bdc51e80c1bed8bdc09e886d.png)

ダウンロードが進むとインストールがはじまります。

ユーザーアカウントの制御ウィンドウが出たら「はい」で許可をして、インストールを進めます。

![4b8e0e322a21477e91310e3ef1c797fc](https://i.gyazo.com/4b8e0e322a21477e91310e3ef1c797fc.png)

しばらく待つとインストールが完了します。

## Airtable アカウント

![image](https://i.gyazo.com/2fa709857524e4f85423675808a883d4.png)

今回、Airtable アカウント が必要です。

![27bc22a09d269759ac5081a3dc31a51f](https://i.gyazo.com/27bc22a09d269759ac5081a3dc31a51f.jpg)

スプレッドシートのような操作感でデータを管理できる <a href="https://www.airtable.com/product" target="_blank">Airtable</a> というサービスがあります。API も使いやすくデータの読み書きもしやすいです。

<a href="https://airtable.com/pricing" target="_blank">Pricing - Airtable</a> で AirTable の価格表をみてみても 2023/6 現在、

![a54430947683d3a47d381d37faadd06e](https://i.gyazo.com/a54430947683d3a47d381d37faadd06e.png)

```
無制限の Base
Base あたり1,200レコード
Base あたり2GBの添付ファイル
```

が、無料枠で含まれるので、とりあえず触ってみても、基本的な機能を体験しやすいものになっています。今回は Airtable を使って、データの記録やデータの管理を行っていきます。

## アカウント作成

![77f11ba87db1888e6953e5deb4408e46](https://i.gyazo.com/77f11ba87db1888e6953e5deb4408e46.png)

<a href="https://airtable.com/signup" target="_blank">サインアップ</a> から自分のメールアドレスでアカウント作成をすすめて準備をします。自分のメールアドレスを Work email に入力して Continue をクリックします。

![7d0e01ea62e400bb2698b57cc8d4f8e0](https://i.gyazo.com/7d0e01ea62e400bb2698b57cc8d4f8e0.png)

Full name と Password を入力します。メールアドレスとパスワードはメモして控えておきましょう。

![02f763f36c7fe6e88eb58f406187835b](https://i.gyazo.com/02f763f36c7fe6e88eb58f406187835b.png)

こちらは Skip ボタンをクリック。

![84664be8aae0fdb1f831c740220ed95b](https://i.gyazo.com/84664be8aae0fdb1f831c740220ed95b.png)

こちらは Skip ボタンをクリック。

![9db04980955f37b065e7f86a9286785f](https://i.gyazo.com/9db04980955f37b065e7f86a9286785f.png)

なにも選択せず Continue ボタンをクリックします。

![d2ad23bd5159f9c96692f1f5ab437312](https://i.gyazo.com/d2ad23bd5159f9c96692f1f5ab437312.png)

I'm currently working on: の欄には my Unity project を入力して Continue をクリックします。

![0df467e4625322d6db656342c3f3456d](https://i.gyazo.com/0df467e4625322d6db656342c3f3456d.png)

こちらは Add your own を選択したあと Continue ボタンをクリックします。

![e05efe706e39d0f8a26dd318c56402d5](https://i.gyazo.com/e05efe706e39d0f8a26dd318c56402d5.png)

こちらは Status を選択したあと Continue ボタンをクリックします。

![482650a11e367daea6169c926f0b9182](https://i.gyazo.com/482650a11e367daea6169c926f0b9182.png)

こちらは Create your own workflow later を選択したあと Continue ボタンをクリックします。

![85663f5a1caf08fbe8899882ceefc31f](https://i.gyazo.com/85663f5a1caf08fbe8899882ceefc31f.png)

こちらは Grid only を選択したあと Continue ボタンをクリックします。

![c5bfb1ab41e036a4d3804a94bd04a315](https://i.gyazo.com/c5bfb1ab41e036a4d3804a94bd04a315.png)

ローディングが進行します。

![bece43ffa56b4f28cd6ffa981fba6b7b](https://i.gyazo.com/bece43ffa56b4f28cd6ffa981fba6b7b.png)

このような画面になれば作成成功です！

### Verify my email もチェックしておきましょう

![91b0725105e7b8d07e273c765b0a5f08](https://i.gyazo.com/91b0725105e7b8d07e273c765b0a5f08.png)

登録したメールアドレスに確認メール（Verify my email）が届くので Verify my email ボタンをクリックして、確認完了しておきましょう。

![bd9ab490b7d8f3bd523ee1dc17d0ed80](https://i.gyazo.com/bd9ab490b7d8f3bd523ee1dc17d0ed80.png)

Workspace に移動して Your email has been verified! と表示されたらチェック対応も OK です。

## GitHub アカウント

## Slack アカウント