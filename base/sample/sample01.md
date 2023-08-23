# Airtable 画像サンプル

![5f751c5902104b2364bf23166c27250e](https://i.gyazo.com/5f751c5902104b2364bf23166c27250e.png)

このように動きます。

## Table の準備

![ec21fe00664163a70c2e06d95fe56295](https://i.gyazo.com/ec21fe00664163a70c2e06d95fe56295.png)

- `+ Add or import` ボタンをクリックして Create blank table ボタンをクリックします。
- テーブル名を聞かれるので `ImageList` として Save ボタンをクリックします。
- Table ができあがったら、最初に作られているフィールド Notes, Assignee, Status を削除します。
- Name はそのまま使います
  - フィールド名 `Name`
  - フィールドタイプ `Single line text`
- 新しく列を追加します
  - フィールド名 `Image`
  - フィールドタイプ `Attachment`
- 新しく列を追加します
  - フィールド名 `CreatedTime`
  - フィールドタイプ `Created time`

## Table の入力

![d72adfe0ef58885eb67dff628cac3a16](https://i.gyazo.com/d72adfe0ef58885eb67dff628cac3a16.png)

3 行ぶん以下のように設定します。

- Name
  - 適当な文字列
- Image
  - ＋ボタンを押して JPEG 画像か PNG 画像をアップロード
  - 手はじめに https://icooon-mono.com/ で 512 x 512 画像を選ぶのがおススメ

## 今回のサーバプログラム

`sample01.js` です。

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

- ターミナルで `node sample01.js` をサーバ起動
- ポートタブで今回のサーバ起動を公開
- シークレットウィンドウで今回のサーバが公開されているか確認します

## 今回の Unity シーンを起動

![6049726527f3133083e8ca07d1e6261c](https://i.gyazo.com/6049726527f3133083e8ca07d1e6261c.png)

Project タブから Assets > Scenes を選択します。Sample01 をダブルクリックして起動しましょう。

- GetAPI にある Sample01_GetAPI スクリプトを開きます。
- urlAPI 変数を `サーバーURL + /api/get` に変更します。

## Unity を動かしてみる

このようになります。

![5f751c5902104b2364bf23166c27250e](https://i.gyazo.com/5f751c5902104b2364bf23166c27250e.png)