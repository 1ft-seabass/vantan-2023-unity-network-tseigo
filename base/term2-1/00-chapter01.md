# データベース外部サービス Airtable の体験

![9d2c38e6fe48e61528f6b2d34370768f](https://i.gyazo.com/9d2c38e6fe48e61528f6b2d34370768f.png)

## この章で学ぶこと

データベース外部サービス Airtable の体験をします。

## アカウント確認

ログインページ https://airtable.com/login からログインしてみましょう。

![9e781448202ccff0bad8baa78eee2df5](https://i.gyazo.com/9e781448202ccff0bad8baa78eee2df5.png)

ワークスペースページ https://airtable.com/workspaces に移動します。

![4f6e0581a7a80428ac687974e629328c](https://i.gyazo.com/4f6e0581a7a80428ac687974e629328c.png)

もし my Unity project という事前準備で作成できた Base があればそれをそのまま使います。

### もし作成していなければ

![76cdeb2e20951d2bf58401a791dbfbc3](https://i.gyazo.com/76cdeb2e20951d2bf58401a791dbfbc3.png)

今回の Workspace の右上に Create a base というボタンがあるのでクリックします。

![9ee32a264bedfd16034def152bf35822](https://i.gyazo.com/9ee32a264bedfd16034def152bf35822.png)

Untitled Base という Base が作成されます。（今回は青ですがテーマカラーはランダムです）

![68246919d68f4b2b1926e90affd753df](https://i.gyazo.com/68246919d68f4b2b1926e90affd753df.png)

左上のタイトルをクリックします。

![bc72fd35c1608c707e4f39b7a8481e22](https://i.gyazo.com/bc72fd35c1608c707e4f39b7a8481e22.png)

タイトルを my Unity project と変更します。そしてタイトル横の Airtable アイコンをクリックして Workspace ページに戻ります。

![db0671ea6b0f57a055654ddcd88a0e32](https://i.gyazo.com/db0671ea6b0f57a055654ddcd88a0e32.png)

戻りました。

## Base と Table

![db0671ea6b0f57a055654ddcd88a0e32](https://i.gyazo.com/db0671ea6b0f57a055654ddcd88a0e32.png)

Airtable においての Base は、今回でいうと my Unity project というかたまりです。このかたまり（単位）で Airtable API からデータを取得することができます。

![585f1daace67a5feab16826a919e167b](https://i.gyazo.com/585f1daace67a5feab16826a919e167b.png)

Base の中に、複数の Table が格納されています。

![46b7f4c16d2b64d7aea1417451bbe851](https://i.gyazo.com/46b7f4c16d2b64d7aea1417451bbe851.png)

Table は表形式でデータが保管される仕組みです。表とは、行と列で構成されます。

![84cfec06a6690446dd60486cd23b24af](https://i.gyazo.com/84cfec06a6690446dd60486cd23b24af.png)

複数の列でデータの種類が列ごとに決められて格納されます。Airtable の場合、列はフィールドとも呼びます。データの種類は、フィールドタイプと呼びます。

![ed2109772b58243841e7f131ef858b02](https://i.gyazo.com/ed2109772b58243841e7f131ef858b02.png)

行は列で決められたデータの種類に基づいて、データが格納されて 1 行 1 行のかたまりで記録されていきます。

![68d2b7d3e8913d6824129d0f062c9dae](https://i.gyazo.com/68d2b7d3e8913d6824129d0f062c9dae.png)

そして Airtable においての Table は、この Table 1 と書かれた部分です。

さまざまなデータを記録することができます。 1 つの Table ではデータをどういった形式でためていけるかを設定できます。たとえば、この Table は、Airtable の初期設定で作られるものです。

- Name
  - フィールド名
    - Name
  - フィールドタイプ
    - Single line text
    - 単一行という意味
- Notes
  - フィールド名
    - Notes
  - フィールドタイプ
    - Long text
    - 長いテキスト　複数行という意味
- Assignee
  - フィールド名
    - Assignee
  - フィールドタイプ
    - User
- Status
  - フィールド名
    - Status
  - フィールドタイプ
    - Single select
    - あらかじめ決めた選択肢を 1 つ選択できるデータタイプ

フィールドタイプは、いろいろなタイプがあります。

![381f395ceffe89e16237b5496408966c](https://i.gyazo.com/381f395ceffe89e16237b5496408966c.png)

- Supported field types in Airtable overview
  - https://support.airtable.com/docs/supported-field-types-in-airtable-overview

## Table を新しく作ってみる

それでは、今回のためのデータを新しく作ってみましょう。

![21da4fe910a699e692b1ffda35d73f64](https://i.gyazo.com/21da4fe910a699e692b1ffda35d73f64.png)

`+ Add or import` ボタンをクリックして Create blank table ボタンをクリックします。

![6d54b1921708f7be23d8718eccc3c4da](https://i.gyazo.com/6d54b1921708f7be23d8718eccc3c4da.png)

テーブル名を聞かれるので `Sample01` として Save ボタンをクリックします。

![95b4d3c2c8b96dddebf256cbb53761c3](https://i.gyazo.com/95b4d3c2c8b96dddebf256cbb53761c3.png)

最初にフィールドタイプが 4 つ設定された Table が作られました。

## フィールドを設定してみる

Table ができあがったら、フィールドを設定してみましょう。

## フィールドの削除

まず、最初に作られているフィールドを削除しましょう。Notes, Assignee, Status を削除します。

![bd7e8e660e0df560afcc552b86216eba](https://i.gyazo.com/bd7e8e660e0df560afcc552b86216eba.png)

Notes の列のタイトルのこちらのボタンをクリックします。

![115e16e642a5fa2e022acfb0a93c8c09](https://i.gyazo.com/115e16e642a5fa2e022acfb0a93c8c09.png)

フィールドのいろいろな設定ができるメニューが出てくるので Delete field をクリックして列を削除します。

![f23b39ed4665b84c7b6a9726cb8db75f](https://i.gyazo.com/f23b39ed4665b84c7b6a9726cb8db75f.png)

Notes と同じく Assignee, Status も削除します。

### フィールド名の変更

![e321681b77e603e5aa500ee2963728c5](https://i.gyazo.com/e321681b77e603e5aa500ee2963728c5.png)

Name でもメニューを表示させて Edit field をクリックします。

![ce0cb96f5454bdc146e983a05e63d0d9](https://i.gyazo.com/ce0cb96f5454bdc146e983a05e63d0d9.png)

フィールド名を Data にして Save をクリックします。フィールドタイプは Single line text のままでよいです。

## フィールド ID を表示する ID フィールドを追加

![d5dec7b47234fb39f76e65e8cdc0db20](https://i.gyazo.com/d5dec7b47234fb39f76e65e8cdc0db20.png)

つづいて、フィールドの＋ボタンをクリックしてフィールドをひとつ加えます。

![e94141996a302bff89e421bf5f33530e](https://i.gyazo.com/e94141996a302bff89e421bf5f33530e.png)

設定は

- フィールド名
  - ID
- データタイプ
  - Formula
  - Airtable であらかじめ設定された計算式やフィールドの値を「式（Formula）」として扱えるフィールドタイプ

とします。

![3ba57896cf87f903e59f64b53449937b](https://i.gyazo.com/3ba57896cf87f903e59f64b53449937b.png)

実際の Formula の値は `RECORD_ID()` とします。RECORD_ID 関数とは各行で自動で設定されるレコード ID を表示してくれる便利な Airtable 関数です。

レコード ID は API での呼び出しでも名指しで指定の行を読みだすために使えたり、他のデータをあつかうきっかけとしても利用しやすいので、設定しておきます。

設定できたら Create field をクリックします。

![46e36f159c5623ca034ee6e56618ac31](https://i.gyazo.com/46e36f159c5623ca034ee6e56618ac31.png)

このように ID のフィールドも設定されて、各行のレコード ID も表示されました。

### 各行のデータを設定する

![65a1675018a57f09e4b07dc73940296e](https://i.gyazo.com/65a1675018a57f09e4b07dc73940296e.png)

Data の列のデータを、以下のように入力します。

- 1 番目の行
  - A
- 2 番目の行
  - B
- 3 番目の行
  - C

設定できたらこのようになります。

![ea196a0dbcf8d3579c386437dd6ff83e](https://i.gyazo.com/ea196a0dbcf8d3579c386437dd6ff83e.png)

### 1 行データを加える

![18dcadfda5bcc81db22432e2e71834bc](https://i.gyazo.com/18dcadfda5bcc81db22432e2e71834bc.png)

データを加えるのも体験しましょう。

行の最下部の＋ボタンをクリックしてデータを 1 行加えます。

![3f43d3e8024c933c23c66ed87b80608d](https://i.gyazo.com/3f43d3e8024c933c23c66ed87b80608d.png)

ID は `RECORD_ID` 関数によって自動表示されます。Data の列に D と入力します。

![ccd150ca7fc2f08608714fcd75f84c2f](https://i.gyazo.com/ccd150ca7fc2f08608714fcd75f84c2f.png)

これで Airtable で Sample01 の Table の設定が完了です。

## 他にも便利なフィールド紹介

![0315bfabadc8442391ad415f119e63c3](https://i.gyazo.com/0315bfabadc8442391ad415f119e63c3.png)

フィールドタイプは、いろいろなタイプがあります。

![381f395ceffe89e16237b5496408966c](https://i.gyazo.com/381f395ceffe89e16237b5496408966c.png)

- Supported field types in Airtable overview
  - https://support.airtable.com/docs/supported-field-types-in-airtable-overview

こちらをベースにいくつか紹介していきます。

### フィールドタイプ紹介

- Number
  - 数字で揃えられる
- Single select
  - 入力時にデータをそろえられる
- Multi select
  - 複数のデータを決めた値で入力できる（Sta）
- Checkbox
  - チェックされているかいないかの 2 つの値で管理できる
  - Unity の bool に近い
- Date
  - 日付入力がしやすい
  - API 側から入力するときは ISO 8601 フォーマットに合わせる必要がある
    - https://ja.wikipedia.org/wiki/ISO_8601

### 自動入力系フィールドタイプ紹介

- Formula
  - 色々な式が使える
  - https://support.airtable.com/docs/formula-field-reference#introduction
- Created time
  - 行が作られたとき自動で作成日時を作ってくれる
  - 自前で作るときはひと手間必要なので重宝
- Last modified time
  - データが変更されたとき自動で更新日時を更新してくれる
  - 自前で作るときはひと手間必要なので重宝