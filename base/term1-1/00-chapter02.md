# 環境構築・初動サンプル動作

![9d2c38e6fe48e61528f6b2d34370768f](https://i.gyazo.com/9d2c38e6fe48e61528f6b2d34370768f.png)

## この章で学ぶこと

環境構築や初動のサンプル動作を行います。（GitHub CodeSpaces）

## GitHub Codespaces とは

GitHub Codespaces は、クラウド上に開発環境を提供することで環境設定の手間を省き、どこからでも安全に開発を行うことができる便利なツールです。

今回は Unity から外部のサーバーや API にどうつなぐかを中心に伝えるので、サーバー側の仕組みはなるべく手軽に立ち上げられるように GitHub Codespaces を採用しています。

![df3b5938f05d8b487e6c73d496c21dd4](https://i.gyazo.com/df3b5938f05d8b487e6c73d496c21dd4.png)

- GitHub Codespaces の概要
  - https://docs.github.com/ja/codespaces/overview

### 個人アカウントの無料枠や使用量の確認

![8d4412849bd88c209424edd608476ffd](https://i.gyazo.com/8d4412849bd88c209424edd608476ffd.png)

- GitHub Codespaces の使用状況の表示 - GitHub Docs
  - https://docs.github.com/ja/billing/managing-billing-for-github-codespaces/viewing-your-github-codespaces-usage
- GitHub Codespaces の請求について - GitHub Docs
  - https://docs.github.com/ja/billing/managing-billing-for-github-codespaces/about-billing-for-github-codespaces#monthly-included-storage-and-core-hours-for-personal-accounts
  - 2023/7 現在、個人アカウントでは 1 ヵ月 120 時間使えます。
  - 授業で 40-50 時間使うとしても十分残っているはず

## 今回の GitHub Codespaces リポジトリにアクセス

今回の GitHub Codespaces リポジトリに Chrome ブラウザでアクセスします。

![1d4fe9d0e6c86377c17828a2ff26fd0d](https://i.gyazo.com/1d4fe9d0e6c86377c17828a2ff26fd0d.png)

https://github.com/1ft-seabass/vantan-unity-network-server-base に Chrome ブラウザでアクセスします。それ以外のブラウザだと、うまく動作しない可能性があるので Chrome で動かしましょう。

## GitHub Codespaces としてリポジトリを開く

![6ebad95a052d8a2d37d889399e120424](https://i.gyazo.com/6ebad95a052d8a2d37d889399e120424.png)

Code ボタンをクリックします。

![8f6a286108378103ac8d30df6f811ef4](https://i.gyazo.com/8f6a286108378103ac8d30df6f811ef4.png)

Codespaces タブをクリックします。Create codespace on main をクリックします。

![47b24d3be5b687f60383455a75898788](https://i.gyazo.com/47b24d3be5b687f60383455a75898788.png)

Setting up your codespace という画面が出て構築されます。

![28ea2b9aece0957b5bb7292427889a10](https://i.gyazo.com/28ea2b9aece0957b5bb7292427889a10.png)

ブラウザ上で Visual Studio Code が起動し、今回の仕組みを反映した環境が起動しました。

## Visual Studio Code 操作画面の紹介

- 参考 : Visual Studio Code User Interface
  - https://code.visualstudio.com/docs/getstarted/userinterface

> VS Code には、フォルダーまたはプロジェクトの完全なコンテキストを参照してアクセスするための十分なスペースを確保しながら、エディターに提供されるスペースを最大化する、シンプルで直感的なレイアウトが付属しています。UI は 5 つの主要な領域に分かれています。

![15944e01b4a98ec52bc55931cd2cc250](https://i.gyazo.com/15944e01b4a98ec52bc55931cd2cc250.png)

- アクティビティバー
  - 左側の端にあり、ビューを切り替えることができ、Git が有効になっている場合の発信変更の数など、追加のコンテキスト固有のインジケーターが表示されます。

![4bfb8dfed081b246ea705113ae37760a](https://i.gyazo.com/4bfb8dfed081b246ea705113ae37760a.png)

- プライマリ サイド バー
  - プロジェクトでの作業を支援するエクスプローラーなどのさまざまなビューが含まれています。

![d814cce244bfd173feea1a5a16d3384c](https://i.gyazo.com/d814cce244bfd173feea1a5a16d3384c.png)

- エディタ
  - ファイルを編集するためのメイン領域です。エディタは好きなだけ縦横に並べて開くことができます。

![2967ec1e72381c1a16b92dfea6d84f7b](https://i.gyazo.com/2967ec1e72381c1a16b92dfea6d84f7b.png)

- パネル
  - エディター領域の下にあるビュー用の追加スペース。デフォルトでは、出力、デバッグ情報、エラーと警告、および統合ターミナルが格納されます。パネルを左右に移動して、垂直方向のスペースを増やすこともできます。

![6a15e2237c2845012027e49843c613d9](https://i.gyazo.com/6a15e2237c2845012027e49843c613d9.png)

- ステータス バー
  - 開いているプロジェクトと編集するファイルに関する情報。

✅ポイント
- 機能を全部覚える必要はありません。気になる人がいたら、英語ですが https://code.visualstudio.com/docs でいろいろ使い方を調べて試してみましょう
  - テーマをダークにしたい人は多いかもなので https://code.visualstudio.com/docs/getstarted/themes を見てダークテーマに変更してみてもよいでしょう
- 今回は、エクスプローラでファイルを選択し→エディタで編集＆保存→パネルでターミナルから実行という流れで行います

## プログラムは Node.js という仕組みで動いている

エクスプローラを見てみましょう。今回のプログラム群は Node.js で作られています。

![8adc98dbfb57d79abbc6a5be5eefbad8](https://i.gyazo.com/8adc98dbfb57d79abbc6a5be5eefbad8.png)

Node.js は、普段はブラウザで活用されていて、ネット上で文献の多い JavaScript 言語で、Unity でデータのやり取りをするサーバー側、つまりサーバーサイドのプログラムが作成することができます。

- Node.js® とは
  - https://nodejs.org/ja/about

また、Node.js と一緒にインストールされる npm は、Node.jsのパッケージ管理ツールです。npmを使うことで、パッケージの依存関係や競合関係を管理してくれるので、パッケージを追加、更新する際は基本的に npm 経由で行うことになります。

また、npm には、Node.js と一緒に入ってすぐ使える便利なライブラリがたくさん登録されています。今回は Express https://expressjs.com/ という便利なサーバー構築ライブラリがインストールされています。

✅ポイント
- 今回は、Node.js サーバー側のプログラムは、起動とちょっとした設定反映が中心です。
- もし、より知りたくなったら、ネット上でいろいろと調べてみましょう。
  - （余裕があれば、文献の検索実演）

## 今回の環境の準備

この環境はすでに以下の準備が Codespace によって準備済みです。

- GitHub Codespaces 上に今回の環境が用意されている
- Node.js がすぐ動くように構築されている
- package.json をベースにした npm によるライブラリのインストール
  - 今回は Express https://expressjs.com/ という便利なサーバー構築ライブラリがインストールされています。
- 今回のリポジトリにあるコード群がすべて使える
- ブラウザ上の Visual Studio Code で今回のリポジトリにあるコードが編集・実行できる

## サンプルをターミナルから実行

`app01.js` というプログラムを実行してみましょう。

```js
console.log('Hello! app01!');
```

JavaScript で、コンソールログに「Hello! app01!」と表示するプログラムです。

![2967ec1e72381c1a16b92dfea6d84f7b](https://i.gyazo.com/2967ec1e72381c1a16b92dfea6d84f7b.png)

ターミナルでコマンドを実行します。パネルエリアに注目します。

![d1301375d265afe3f21076fad33192a8](https://i.gyazo.com/d1301375d265afe3f21076fad33192a8.png)

ターミナルタブをクリックします。

![f7d059007e4397f355c11a09dce4b387](https://i.gyazo.com/f7d059007e4397f355c11a09dce4b387.png)

このようにカーソルがありコマンドの入力待ちになっています。

```
node app01.js
```

このコマンドを入力して Enter キーを押します。

コマンドの意味は、以下の通りです。

- `node`
  - 「Node.js でファイルを実行する」コマンド
- `app01.js`
  - app01.js というファイルが対象という意味
  - `/workspaces/vantan-unity-network-server-base` というプロジェクト最上部にいるので、詳しくパスを打たなくても `app01.js` だけで名指しできます

すると、次の行に「Hello! app01!」とでてきたら成功です。

![b537857243d0aed0c58a93e7bd0380a7](https://i.gyazo.com/b537857243d0aed0c58a93e7bd0380a7.png)

これでターミナル実行のウォームアップ完了です。

## ターミナルからサーバーを起動

`server01.js` というプログラムを実行してみましょう。

```js
// Express ライブラリの呼び出し
const express = require('express');
// Express ライブラリからサーバーの仕組みを app 変数として呼び出す
const app = express();

// public フォルダ内にあるファイルはパスが一致していると呼びだせます
// /index.html や / の場合は public フォルダ内の index.html が表示されます
app.use(express.static(__dirname + '/public'));

// サーバーを 8080 ポートで起動してログを出力
app.listen(process.env.PORT || 8080, () => {
  console.log("server01 start!");
  console.log(`app listening at http://localhost:${process.env.PORT || 8080}`)
})
```

Express というライブラリでサーバーを構築できるプログラムです。

```
node server01.js
```

ターミナルで以下のコマンドを入力して Enter キーを押して実行します。

```
server01 start!
app listening at http://localhost:8080
```

というメッセージが次の行に出てくれば起動成功です。これで無事サーバーが起動できました。

✅ポイント
- 現在のプログラムは app01.js のように実行したらすぐに終わるプログラムではなく、サーバーとして動き続けています。

## ブラウザからアクセスしてみる

現在は、起動中の GitHub アカウントのみで構築されたサーバーが確認できます。

![2b7eb26ecba22ee6aa0154d986935251](https://i.gyazo.com/2b7eb26ecba22ee6aa0154d986935251.png)

ターミナルで出力された `http://localhost:8080` にマウスを乗せます。

![9fdd7fbc69e3113ed32732845a6cb9d0](https://i.gyazo.com/9fdd7fbc69e3113ed32732845a6cb9d0.png)

リンクにアクセスというメッセージが出てくるのでクリックします。すると、ブラウザの別のタブでアクセスされます。

![6e18a3f970632af493c0815256d34b11](https://i.gyazo.com/6e18a3f970632af493c0815256d34b11.png)

Index というページが表示されます。

![4d336da902c362dbb0bfc5f289d0c7c5](https://i.gyazo.com/4d336da902c362dbb0bfc5f289d0c7c5.png)

アドレスバーに書いてある URL は、今回の Codespace が構築されたサーバアドレスのトップページが表示されています。

✅ポイント
- server01.js の `app.use(express.static(__dirname + '/public'));` によって、public フォルダの中身でトップページを示す `public/index.html` の内容が、今回起動したサーバーのトップページとして表示されています。
- 現在は、起動中の GitHub アカウントのみで構築されたサーバーが確認でき、次の授業では、Unity からもアクセスできるよう、誰でも見れる公開する対応を行います。

## プログラムの終了

現在のプログラムは app01.js のように実行したらすぐに終わるプログラムではなく、サーバーとして動き続けています。プログラムの終了をしてみましょう。

ターミナル上で Ctrl + C を打ってプログラムを終了します。

![93a99bf90eb16a44806b5bc745cdc9ec](https://i.gyazo.com/93a99bf90eb16a44806b5bc745cdc9ec.png)

このように `^C` 入力とともに、ターミナルの入力待ちになれば終了成功です。

![9ea2265a9d054bc697a822b8b0061bee](https://i.gyazo.com/9ea2265a9d054bc697a822b8b0061bee.png)

サーバーが終了したので、さきほどの Index と書かれたページも再読み込みしてもアクセスできなくなります。

## 今回の Codespace の終了

![0a8b4cfb807e57ea1382292a757c6899](https://i.gyazo.com/0a8b4cfb807e57ea1382292a757c6899.png)

今回の Codespace の終了をします。Codespace はブラウザを閉じると自動で閉じることもありますが、確実に閉じたほうが、無料枠の制限時間も無駄に消費せずおススメです。

> コードスペースのライフサイクルを理解する  
> https://docs.github.com/ja/codespaces/getting-started/understanding-the-codespace-lifecycle
> 
> コードスペースを操作せずに実行したままにした場合、またはコードスペースを明示的に停止せずに終了した場合、コードスペースは非アクティブな時間が経過するとタイムアウトになり、実行が停止します。デフォルトでは、コードスペースは非アクティブ状態が 30 分間続くとタイムアウトしますが、作成する新しいコードスペースのタイムアウト期間をカスタマイズできます。

いま起動している Codespace から終了してみましょう。

![270f2ad603d2c7aa6a984689f0ef6003](https://i.gyazo.com/270f2ad603d2c7aa6a984689f0ef6003.png)

左下の `>< Codespaces` をクリックします。

![579e1da05534e8d00cfa81428042c216](https://i.gyazo.com/579e1da05534e8d00cfa81428042c216.png)

上部にコマンドパレットが表示されます。 `Stop Current Codespace` をクリックします。

![6d77c1b267a243d5e43e7c6561bd5339](https://i.gyazo.com/6d77c1b267a243d5e43e7c6561bd5339.png)

右下にステータスが表示されます。

![4e949f3c23eca5b3d6383905f97eed3e](https://i.gyazo.com/4e949f3c23eca5b3d6383905f97eed3e.png)

しばらく待つと画面が切り替わり、このようになれば無事終了できました。

その他に、以下のヘルプで、Codespace 一覧から停止する操作も確認できます。ちゃんと終了されたか確認するときにも役に立つでしょう。

- codespace の停止と開始 - GitHub Docs
  - https://docs.github.com/ja/codespaces/developing-in-codespaces/stopping-and-starting-a-codespace