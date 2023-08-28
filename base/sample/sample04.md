# Airtable に Unity から直接アクセスする

## Table の準備

![ccd150ca7fc2f08608714fcd75f84c2f](https://i.gyazo.com/ccd150ca7fc2f08608714fcd75f84c2f.png)

[こちらで作った Sample01 の Table ](../term2-1/00-chapter01.md) を使います。

## 今回の Unity シーンを起動

![6049726527f3133083e8ca07d1e6261c](https://i.gyazo.com/6049726527f3133083e8ca07d1e6261c.png)

Project タブから Assets > Scenes を選択します。Sample04 をダブルクリックして起動しましょう。

Cube にある Sample04_GetAPI_Direct_Airtable スクリプトを開きます。

```csharp
    // Airtable の Base ID
    string settingAirtableBaseID = "settingAirtableBaseID";

    // Airtable の API キー
    string settingAirtableAPIKey = "settingAirtableAPIKey";
```

settingAirtableBaseID には今回動かしたい Airtable の Base ID を入力します。settingAirtableAPIKey には Airtable の API キー を入力します。

## 動かしてみる

Unity を動かしてみると、以下のように Data と ID の各値が表示されます。

![bfbb107cc2c6694c16afedf0aff9558c](https://i.gyazo.com/bfbb107cc2c6694c16afedf0aff9558c.png)


## 今回の仕組み

### URL 作成

```csharp
// API URL 作成
string urlAirtableAPI = "https://api.airtable.com/v0/" + settingAirtableBaseID + "/" + settingAirtableTable + "?view=" + settingAirtableView;
// API URL を Uri.AbsoluteUri と通して URL パラメータ調整
// 例 ?view=Grid view が ?view=Grid%20view になる
urlAirtableAPI = new Uri(urlAirtableAPI).AbsoluteUri;

// HTTP リクエストする(GET メソッド) UnityWebRequest を呼び出し
UnityWebRequest request = UnityWebRequest.Get(urlAirtableAPI);
```

view の名前 `Grid view` を GET リクエストで送るために `view=Grid view` が `view=Grid%20view` になる必要があるため Uri クラス https://learn.microsoft.com/ja-jp/dotnet/api/system.uri?view=net-7.0 を利用して AbsoluteUri で変換しています。

### API キーはヘッダーに設定

```csharp
// API キーを HTTP ヘッダーに設定
request.SetRequestHeader("Authorization", "Bearer " + settingAirtableAPIKey);
```

API キーはこのように設定しています。

### 受信したデータを

受信したデータは以下のようになっています。各行が records に配列で入っていて、その中に id , createdTime , fields があります。fields の中身が、各列の情報になっています。今回は Data 列と ID 列があります。

```csharp
{
    "records": [
        {
            "id": "recsZHOU2F0hqdD8G",
            "createdTime": "2023-08-21T06:01:47.000Z",
            "fields": {
                "Data": "A",
                "ID": "recsZHOU2F0hqdD8G"
            }
        },
        {
            "id": "recaLn7uEszYsBLPE",
            "createdTime": "2023-08-21T06:01:47.000Z",
            "fields": {
                "Data": "B",
                "ID": "recaLn7uEszYsBLPE"
            }
        },
        {
            "id": "recSn4R2oxR46P6VA",
            "createdTime": "2023-08-21T06:01:47.000Z",
            "fields": {
                "Data": "C",
                "ID": "recSn4R2oxR46P6VA"
            }
        }
    ],
    "offset": "itrfiG2tfH2TjwE5y/recSn4R2oxR46P6VA"
}
```

こちらを踏まえて受信した JSON データを Unity で扱うデータにする ResponseData ベースクラスが以下です。


```csharp
// 受信した JSON データを Unity で扱うデータにする ResponseData ベースクラス
[Serializable]
public class ResponseData
{
    public List<ResponseDataRecord> records;
}

[Serializable]
public class ResponseDataRecord
{
    public string id;
    public string createdTime;
    public ResponseDataRecordField fields;
}

// ResponseDataRecordField は Table の列の内容によって変更します
[Serializable]
public class ResponseDataRecordField
{
    // フィールド名 Data が string 型
    public string Data;
    // フィールド名 Image には画像関連の情報が入っている
    public string ID;
}
```

今回は Sample01 の列ですが、ResponseDataRecordField は Table の列の内容によって変更します。

## 覚えておいてほしいこと

![40ee748630dfef0b75f3f18414363382](https://i.gyazo.com/40ee748630dfef0b75f3f18414363382.png)

プログラムを広く配布する形の場合は Airtable の API キーや Base ID がプログラムに入ったままだと漏洩の可能性はあります。

ですが、今回のように、プログラムを配布せず、個人の制作の範疇で自分の PC や固有の VR 機器で動く形であれば、やや軽減されるので Unity のプログラムから直接 Airtable にアクセスするのもアリです。

という視点を忘れず、組み込んでみてください！

## 以前のプログラムもサンプル用意しました

以前のプログラムでの Airtable 直接アクセスのプログラムを用意しました。

### Scene-Term2-1-Chapter03 シーン

- Cube にある Term2_1_Chapter03_CubeEvent01 のコンポーネントを削除します
- Cube に Term2_1_Chapter03_CubeEvent01_Direct_Airtable をコンポーネントに割り当てます。
- Term2_1_Chapter03_CubeEvent01_Direct_Airtable 内の settingAirtableBaseID には今回動かしたい Airtable の Base ID を入力し settingAirtableAPIKey には Airtable の API キー を入力します。
- 実行して動かしてみましょう

### Scene-Term2-2-Chapter01 シーン

- GetAPI にある Term2_2_Chapter01_GetAPI のコンポーネントを削除します
- GetAPI に Term2_2_Chapter01_GetAPI_Direct_Airtable をコンポーネントに割り当てます。
- Term2_2_Chapter01_GetAPI_Direct_Airtable 内の settingAirtableBaseID には今回動かしたい Airtable の Base ID を入力し settingAirtableAPIKey には Airtable の API キー を入力します。
- 実行して動かしてみましょう

## Scene-Term2-2-Chapter02 シーン

Airtable に書き込むプログラムが確認できるのでおススメです。

- SendButton にある Term2_2_Chapter02_SendButton のコンポーネントを削除します
- SendButton に Term2_2_Chapter02_SendButton_Direct_Airtable をコンポーネントに割り当てます。
- Term2_2_Chapter02_SendButton_Direct_Airtable 内の settingAirtableBaseID には今回動かしたい Airtable の Base ID を入力し settingAirtableAPIKey には Airtable の API キー を入力します。
- 実行して動かしてみましょう

## Scene-Term2-2-Chapter03 シーン

- SendButton にある Term2_2_Chapter03_SendButton のコンポーネントを削除します
- SendButton に Term2_2_Chapter03_SendButton_Direct_Airtable をコンポーネントに割り当てます。
- Term2_2_Chapter03_SendButton_Direct_Airtable 内の settingAirtableBaseID には今回動かしたい Airtable の Base ID を入力し settingAirtableAPIKey には Airtable の API キー を入力します。
- RankingMessage にある Term2_2_Chapter03_RankingMessage のコンポーネントを削除します
- RankingMessage に Term2_2_Chapter03_RankingMessage_Direct_Airtable をコンポーネントに割り当てます。
- Term2_2_Chapter03_RankingMessage_Direct_Airtable 内の settingAirtableBaseID には今回動かしたい Airtable の Base ID を入力し settingAirtableAPIKey には Airtable の API キー を入力します。
- 実行して動かしてみましょう

## Sample01 シーン

- GetAPI にある Sample01_GetAPI のコンポーネントを削除します
- GetAPI に Sample01_GetAPI_Direct_Airtable をコンポーネントに割り当てます。
- Sample01_GetAPI_Direct_Airtable 内の settingAirtableBaseID には今回動かしたい Airtable の Base ID を入力し settingAirtableAPIKey には Airtable の API キー を入力します。
- 実行して動かしてみましょう

## Sample02シーン

- NextButton にある Sample02_NextButton のコンポーネントを削除します
- NextButton に Sample02_NextButton_Direct_Airtable をコンポーネントに割り当てます。
- Sample02_NextButton_Direct_Airtable 内の settingAirtableBaseID には今回動かしたい Airtable の Base ID を入力し settingAirtableAPIKey には Airtable の API キー を入力します。
- 実行して動かしてみましょう
