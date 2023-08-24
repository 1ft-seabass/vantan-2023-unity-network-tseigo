# Airtable クイズサンプル

（画像）

このように動きます。

## Table の準備

![ec21fe00664163a70c2e06d95fe56295](https://i.gyazo.com/ec21fe00664163a70c2e06d95fe56295.png)

- `+ Add or import` ボタンをクリックして Create blank table ボタンをクリックします。
- テーブル名を聞かれるので `QuizList` として Save ボタンをクリックします。
- Table ができあがったら、最初に作られているフィールド Notes, Assignee, Status を削除します。
- Name は変更します
  - フィールド名 `ID`
  - フィールドタイプ `Single line text`
- 新しく列を追加します
  - フィールド名 `QuizText`
  - フィールドタイプ `Long text`
- 新しく列を追加します
  - フィールド名 `Select1`
  - フィールドタイプ `Single line text`
- 新しく列を追加します
  - フィールド名 `Select2`
  - フィールドタイプ `Single line text`
- 新しく列を追加します
  - フィールド名 `Select3`
  - フィールドタイプ `Single line text`
- 新しく列を追加します
  - フィールド名 `Answer`
  - フィールドタイプ `Number` , `Integer`

## Table の入力

![483bbc63c9504f326e8eec746fde3f36](https://i.gyazo.com/483bbc63c9504f326e8eec746fde3f36.png)

3 行ぶん以下のように設定します。

- ID
  - 1 からの連番
- QuizText
  - 出題テキスト
- Select1
  - 選択肢 1
- Select2
  - 選択肢 2
- Select3
  - 選択肢 3
- Answer
  - 選択肢 1 ～ 3 のうちどれが正解か

## 今回のサーバプログラム

`sample02.js` です。

## Base ID や API キーの入力

```js
// Airtable API キー
const AIRTABLE_API_KEY = 'AIRTABLE_API_KEY';
// Airtable BASE ID
const AIRTABLE_BASE_ID = 'AIRTABLE_BASE_ID';
```

こちらに Base ID や API キーの入力をします。AIRTABLE_API_KEY には API キー、AIRTABLE_BASE_ID には Base ID を入力しましょう。

## サーバの起動

![0a3a35f3418068b7713ddaa729f2c660](https://i.gyazo.com/0a3a35f3418068b7713ddaa729f2c660.png)

- ターミナルで `node sample02.js` をサーバ起動
- ポートタブで今回のサーバ起動を公開
- シークレットウィンドウで今回のサーバが公開されているか確認します

## 今回の Unity シーンを起動

![6049726527f3133083e8ca07d1e6261c](https://i.gyazo.com/6049726527f3133083e8ca07d1e6261c.png)

Project タブから Assets > Scenes を選択します。Sample02 をダブルクリックして起動しましょう。

- GetAPI にある Sample01_GetAPI スクリプトを開きます。
- urlAPI 変数を `サーバーURL + /api/get` に変更します。

## Unity を動かしてみる

このようになります。

（画像）