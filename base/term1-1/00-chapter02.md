# 環境構築・初動サンプル動作

![9d2c38e6fe48e61528f6b2d34370768f](https://i.gyazo.com/9d2c38e6fe48e61528f6b2d34370768f.png)

## この章で学ぶこと

環境構築や初動のサンプル動作を行います。

## 環境構築

今回事前準備した Unity バージョンを確認しつつ、環境構築をしていきましょう。

![a22ec4c95524c34562414d6efe01f566](https://i.gyazo.com/a22ec4c95524c34562414d6efe01f566.png)

Unity Hub を起動して、New Project ボタンをクリックします。

![ddf49ef780c60063791bf3aabc75d45a](https://i.gyazo.com/ddf49ef780c60063791bf3aabc75d45a.png)

Core > 3D をクリックします。右エリアに PROJECT SETTING が表示されます。

![bc6e6c44a26e7040b70255bedbf9048d](https://i.gyazo.com/bc6e6c44a26e7040b70255bedbf9048d.png)

Project name は `Unity-Network-Sample-01` で Location は、自分の普段の作業フォルダで行います。

作業フォルダのおすすめ
- C ドライブ直下に、今回の授業名 vantan_unity_network で作る。
- ユーザーフォルダに自分の分かりやすいフォルダで作る
- C ドライブ直下に自分の分かりやすいフォルダで作る

デスクトップ直下は、他のファイルも混ざってしまい混乱しやすいので避けましょう。

![195a89c3cb80a9c037b080f96fb8ae7e](https://i.gyazo.com/195a89c3cb80a9c037b080f96fb8ae7e.png)

Project name と Location を設定したら、Create project ボタンをクリックします。

![8693cc6b6be3c66765c28a159a0d5e4a](https://i.gyazo.com/8693cc6b6be3c66765c28a159a0d5e4a.png)

プロジェクトの作成が始まります。

![b7ca8c2686c7f01a7d87fa04a4208499](https://i.gyazo.com/b7ca8c2686c7f01a7d87fa04a4208499.png)

該当バージョンの Unity が開き、プロジェクトが準備されます。

![77b30f4a9da6debd2f94b28c769a5a12](https://i.gyazo.com/77b30f4a9da6debd2f94b28c769a5a12.png)

プロジェクトが開きます。もし Build Setting が開いていたら閉じましょう。

![c35f9a277dc4ca526b241ccf02b88d68](https://i.gyazo.com/c35f9a277dc4ca526b241ccf02b88d68.png)

これで準備完了です。

## 初動のサンプル動作

![c35f9a277dc4ca526b241ccf02b88d68](https://i.gyazo.com/c35f9a277dc4ca526b241ccf02b88d68.png)

ということで、ここからサンプルを作成していきます。

### Build Setting 確認

![1ef230a444b6d94461cc88d14923fb58](https://i.gyazo.com/1ef230a444b6d94461cc88d14923fb58.png)

メニュー > File > Build Setting で Build Setting を開きます。

![c7a4e4da91fc04a649033e6cd165b0b7](https://i.gyazo.com/c7a4e4da91fc04a649033e6cd165b0b7.png)

Platform が PC になっていれば OK です。

## Cube 配置

![9d5f314021661da71ed0128f9da22755](https://i.gyazo.com/9d5f314021661da71ed0128f9da22755.png)

Hierarcy の＋ボタンをクリックして 3D Object > Cube をクリックして Cube を配置します。

## EventSystem 配置

![791062a03a48c41fe156ffddc9f6282c](https://i.gyazo.com/791062a03a48c41fe156ffddc9f6282c.png)

Hierarcy の＋ボタンをクリックして UI > EventSystem で EventSystem を配置します。

## Hierarcy 確認

![e62df939e056f9b2a4c126fa49f6d4be](https://i.gyazo.com/e62df939e056f9b2a4c126fa49f6d4be.png)

このような Hierarcy になります。

## Main Camera にコンポーネント追加

![c190ea2def5824d7c2cd1cad1f342853](https://i.gyazo.com/c190ea2def5824d7c2cd1cad1f342853.png)

Hierarcy で Main Camera を選択して Main Camera の Inspector を見ます。Add Component ボタンをクリックします。

![73874f01b22f9d05427935db4551b8e3](https://i.gyazo.com/73874f01b22f9d05427935db4551b8e3.png)

コンポーネント検索で Physics Raycaster を選択してコンポーネントを加えます。

## Assets に Scripts フォルダ作成

![5d2428e4b832594b8232198419793c2a](https://i.gyazo.com/5d2428e4b832594b8232198419793c2a.png)

Project タブで Assets を選択して、右クリックから Create > Folder を選択して Scripts フォルダを作成します。Scenes フォルダと同じ階層です。

## CubeEvent スクリプト

![ac26279a81eb874c750bc60bfb4dd9f8](https://i.gyazo.com/ac26279a81eb874c750bc60bfb4dd9f8.png)

Scripts フォルダの中に移動して、右クリックから Create > C# Script で選択して CubeEvent というファイルを作成します。

## CubeEvent スクリプト書き換え

CubeEvent をダブルクリックしてエディタで開きます。すべて選択して、以下のプログラムに書き換えます。

```csharp
using UnityEngine;
using UnityEngine.EventSystems;

public class CubeEvent : MonoBehaviour, IPointerClickHandler
{
    public void OnPointerClick(PointerEventData eventData)
    {
        // マウスクリックイベント
        Debug.Log($"オブジェクト {this.name} がクリックされたよ！");
    }
}
```

書き換えたら保存しましょう。

## Cube に CubeEvent スクリプト割り当て

![e37d75b91a946c35519711c87422d6d7](https://i.gyazo.com/e37d75b91a946c35519711c87422d6d7.png)

Hierarcy で Cube を選択して Cube の Inspector を見ます。Add Component ボタンをクリックします。

![2ae59cc631d5e1ea352717468369e5a3](https://i.gyazo.com/2ae59cc631d5e1ea352717468369e5a3.png)

コンポーネント検索で CubeEvent を選択してコンポーネントを加えます。

## シーン保存

![172edf11c047e3cb48db6b6b131b7f40](https://i.gyazo.com/172edf11c047e3cb48db6b6b131b7f40.png)

シーンをいったん保存しましょう。

## 動作確認

![2fbea7338e0832c54e0b977c39f5dedd](https://i.gyazo.com/2fbea7338e0832c54e0b977c39f5dedd.png)

Play ボタンをクリックします。

![6044c7e49cf4a9d7af2d62b94476d854](https://i.gyazo.com/6044c7e49cf4a9d7af2d62b94476d854.png)

Cube をマウスでクリックしてみましょう。

![cfe7587c4bb92695695695e3a2f291d4](https://i.gyazo.com/cfe7587c4bb92695695695e3a2f291d4.png)

Console でこのようなログが出てくれば成功です！まずはマウスクリックが動きました。