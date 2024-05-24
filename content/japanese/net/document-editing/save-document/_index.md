---
title: ドキュメントを保存
linktitle: ドキュメントを保存
second_title: GroupDocs.Editor .NET API
description: GroupDocs.Editor for .NET を使用すると、ドキュメントを簡単に編集して保存できます。このステップ バイ ステップ ガイドは、開発者のプロセスを簡素化します。
type: docs
weight: 14
url: /ja/net/document-editing/save-document/
---
## 導入
GroupDocs.Editor for .NET を使用して、ドキュメントを簡単に編集および保存したいとお考えですか? まさにうってつけの場所です。このチュートリアルでは、ドキュメントを簡単に管理できるように、プロセスをステップごとに説明します。熟練した開発者でも初心者でも、このガイドには、開始するために必要なすべての情報が記載されています。
## 前提条件
チュートリアルに進む前に、次の前提条件が満たされていることを確認してください。
- 開発環境: マシンに Visual Studio がインストールされていること。
- .NET Framework: .NET Framework 4.6.1 以降がインストールされていることを確認してください。
-  GroupDocs.Editor for .NET: 最新バージョンをダウンロード[ここ](https://releases.groupdocs.com/editor/net/).
- 基本的な C# の知識: C# プログラミングに精通していることが必須です。
## 名前空間のインポート
.NET プロジェクトで GroupDocs.Editor を使用するには、必要な名前空間をインポートする必要があります。手順は次のとおりです。
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
環境が設定され、必要な名前空間がインポートされたので、GroupDocs.Editor for .NET を使用してドキュメントを読み込み、編集し、保存するために必要な手順を詳しく見ていきましょう。
## ステップ1: ドキュメントを読み込む
まず、編集したいドキュメントを読み込む必要があります。GroupDocs.Editor を使用すると、このプロセスが簡単になります。手順は次のとおりです。

```csharp
string inputFilePath = "Your Sample Document";
Editor editor = new Editor(inputFilePath, delegate { return new Options.WordProcessingLoadOptions(); });
EditableDocument defaultWordProcessingDoc = editor.Edit();
```
このステップでは、編集したいドキュメントへのパスを指定し、`Editor`クラス。`Edit`メソッドが呼び出され、ドキュメントが`EditableDocument`物体。
## ステップ2: ドキュメントを変更する
ドキュメントが読み込まれたら、変更を加えます。WYSIWYG エディターが接続されていないため、コードで編集プロセスをシミュレートします。

```csharp
string allEmbeddedInsideString = defaultWordProcessingDoc.GetEmbeddedHtml();
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
EditableDocument editedDoc = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```
ここでは、ドキュメントに埋め込まれたHTMLコンテンツを取得し、単純なテキスト置換を実行して、新しい`EditableDocument`変更された HTML からのインスタンス。
## ステップ3: ドキュメントを保存する
ドキュメントを編集した後、最後のステップはそれを保存することです。GroupDocs.Editor には、さまざまな形式でドキュメントを保存するための複数のオプションが用意されています。
## RTFとして保存
```csharp
string outputRtfPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.rtf");
WordProcessingSaveOptions rtfSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
editor.Save(editedDoc, outputRtfPath, rtfSaveOptions);
```
## DOCMとして保存
```csharp
string outputDocmPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.docm");
WordProcessingSaveOptions docmSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm);
using (FileStream outputStream = File.Create(outputDocmPath))
{
    editor.Save(editedDoc, outputStream, docmSaveOptions);
}
```
## プレーンテキストとして保存
```csharp
string outputTxtPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.txt");
TextSaveOptions textSaveOptions = new TextSaveOptions
{
    Encoding = System.Text.Encoding.UTF8,
    PreserveTableLayout = true
};
editor.Save(editedDoc, outputTxtPath, textSaveOptions);
```
## ステップ4: クリーンアップ
最後に、`EditableDocument`そして`Editor`インスタンスを作成してリソースを解放します。
```csharp
editedDoc.Dispose();
defaultWordProcessingDoc.Dispose();
editor.Dispose();
```
これらの手順に従うことで、GroupDocs.Editor for .NET を使用してドキュメントを効率的に読み込み、編集し、保存できます。この強力なツールは柔軟性と使いやすさを提供し、ドキュメント管理を簡単にします。
## 結論
GroupDocs.Editor for .NET を使用すると、プログラムによるドキュメントの編集と保存がこれまでになく簡単になります。このガイドでは、ドキュメントの読み込みからさまざまな形式での保存まで、プロセス全体を説明しました。GroupDocs.Editor を使用すると、多用途で堅牢なソリューションを簡単に利用でき、ドキュメント編集プロセスを簡素化できます。
## よくある質問
### GroupDocs.Editor はどのようなファイル形式をサポートしていますか?
GroupDocs.Editorは、DOCX、RTF、TXTなど、さまざまなファイル形式をサポートしています。完全なリストについては、[ドキュメンテーション](https://reference.groupdocs.com/editor/net/).
### 購入前に GroupDocs.Editor を試すことはできますか?
はい、[無料トライアル](https://releases.groupdocs.com/) GroupDocs.Editor の機能をテストします。
### 問題が発生した場合、サポートを受けることはできますか?
もちろんです！[サポートフォーラム](https://forum.groupdocs.com/c/editor/20)問題が発生した場合のサポートについては、
### 一時ライセンスを取得するにはどうすればよいですか?
リクエストすることができます[一時ライセンス](https://purchase.groupdocs.com/temporary-license/)評価目的のため。
### GroupDocs.Editor のフルバージョンはどこで購入できますか?
フルバージョンを購入することができます[ここ](https://purchase.groupdocs.com/buy).