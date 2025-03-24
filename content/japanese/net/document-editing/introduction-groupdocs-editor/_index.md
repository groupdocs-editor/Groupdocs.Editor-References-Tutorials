---
title: GroupDocs.Editor for .NET の紹介
linktitle: GroupDocs.Editor for .NET の紹介
second_title: GroupDocs.Editor .NET API
description: この詳細なステップバイステップ ガイドでは、GroupDocs.Editor for .NET を使用してプログラムでドキュメントを編集する方法を学習します。
weight: 12
url: /ja/net/document-editing/introduction-groupdocs-editor/
---
## 導入 
ドキュメント編集機能を .NET アプリケーションにシームレスに統合したいと考えている開発者にとって、GroupDocs.Editor for .NET は検討に値する強力なツールです。この多機能ライブラリを使用すると、さまざまなドキュメント形式をプログラムで読み込み、編集し、保存できます。Word ドキュメント、PDF、HTML ファイルのいずれを処理する必要がある場合でも、GroupDocs.Editor によってプロセスが簡素化され、効率的かつわかりやすくなります。このチュートリアルでは、GroupDocs.Editor for .NET の基本について、実用的な例を段階的に説明しながら説明します。
## 前提条件
実装に進む前に、次の前提条件が満たされていることを確認してください。
- 開発環境: Visual Studio 2017 以降。
- .NET Framework: .NET Framework 4.6.1 以降。
-  GroupDocs.Editor for .NET: 次のようなことができます[ダウンロード](https://releases.groupdocs.com/editor/net/)サイトから入手してください。
- ライセンス: 有効なライセンスまたは[一時ライセンス](https://purchase.groupdocs.com/temporary-license/)GroupDocs より。
## 名前空間のインポート
GroupDocs.Editor for .NET の使用を開始するには、必要な名前空間をインポートする必要があります。これらの名前空間は、ドキュメント編集に必要なクラスとメソッドへのアクセスを提供します。
```csharp
using System;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```

このセクションでは、プロセスを管理しやすいステップに分割し、ワークフローの各部分を理解できるようにします。
## ステップ1: 入力ファイルへのパスを取得する
まず、編集するドキュメントへのパスを指定する必要があります。この例では、「Your Sample Document.docx」という名前の DOCX ファイルがあると仮定します。
```csharp
string inputFilePath = "Your Sample Document.docx";
```
## ステップ2: エディターオブジェクトのインスタンスを作成する
次に、`Editor`入力ファイルをロードしてクラスを作成します。このステップでは、ドキュメントを初期化してさらに処理できるようにします。
```csharp
using (GroupDocs.Editor.Editor editor = new Editor(inputFilePath))
{
    //後続のステップはこのブロック内にネストされます
}
```
## ステップ3: 編集用にドキュメントを開く
文書を編集するには、中間者を取得する`EditableDocument`インスタンス。このオブジェクトを使用すると、ドキュメントのコンテンツと関連リソースを操作できます。
```csharp
EditableDocument beforeEdit = editor.Edit();
```
## ステップ4: ドキュメントコンテンツとリソースを取得する
編集可能なドキュメントからメインコンテンツ、画像、フォント、スタイルシートを抽出します。この情報は、変更を行うために不可欠です。
```csharp
string content = beforeEdit.GetContent();
var images = beforeEdit.Images;
var fonts = beforeEdit.Fonts;
var stylesheets = beforeEdit.Css;
```
### ステップ 4.1: ドキュメントを単一の Base64 エンコードされた文字列として取得する
すべてのリソースを含む、ドキュメント コンテンツ全体を単一の base64 エンコード文字列として取得することもできます。
```csharp
string allEmbeddedInsideString = beforeEdit.GetEmbeddedHtml();
```
### ステップ4.2: コンテンツを編集する
デモンストレーションのために、特定のテキストを置き換えてドキュメントの内容を変更してみましょう。
```csharp
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
```
## ステップ5: 新しいEditableDocumentインスタンスを作成する
コンテンツを編集したら、新しい`EditableDocument`変更されたコンテンツを使用するインスタンス。
```csharp
EditableDocument afterEdit = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```
## ステップ6: 編集したドキュメントを保存する
次に、編集したドキュメントを目的の出力形式で保存します。この例では、RTF ファイルとして保存します。
### ステップ6.1: 出力パスを準備する
出力ドキュメントを保存するパスを指定します。
```csharp
string outputPath = Path.Combine("Output Directory Path", Path.GetFileNameWithoutExtension(inputFilePath) + ".rtf");
```
### ステップ6.2: 保存オプションの準備
ドキュメントを保存する形式を指定して、保存オプションを定義します。
```csharp
Options.WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
```
### ステップ6.3: パスに保存
編集したドキュメントを指定されたパスに保存します。
```csharp
editor.Save(afterEdit, outputPath, saveOptions);
```
### ステップ 6.4: ストリームに保存する
あるいは、出力ドキュメントを任意の書き込み可能なストリームに保存することもできます。
```csharp
using (MemoryStream ms = new MemoryStream())
{
    editor.Save(afterEdit, ms, saveOptions);
}
```
## ステップ 7: Editor および EditableDocument インスタンスを破棄する
最後に、`EditableDocument`インスタンスと`Editor`リソースを解放するためのオブジェクト。
```csharp
beforeEdit.Dispose();
afterEdit.Dispose();
editor.Dispose();
```

## 結論
GroupDocs.Editor for .NET を使用すると、ドキュメント編集機能をアプリケーションに簡単に統合できます。このチュートリアルで説明されている手順に従うと、最小限の労力でプログラムによってドキュメントを読み込み、編集し、保存できます。Word ドキュメント、PDF、その他の形式のいずれを処理する必要がある場合でも、GroupDocs.Editor はドキュメント処理のニーズに応える強力なソリューションを提供します。
## よくある質問
### GroupDocs.Editor for .NET を使用して PDF ファイルを編集できますか?
はい、GroupDocs.Editor for .NET は、PDF ファイルの編集に加えて、DOCX、HTML などの他の多くの形式もサポートしています。
### GroupDocs.Editor for .NET の一時ライセンスを取得するにはどうすればよいですか?
臨時免許証は、[GroupDocsウェブサイト](https://purchase.groupdocs.com/temporary-license/).
### GroupDocs.Editor for .NET ではどのようなファイル形式がサポートされていますか?
GroupDocs.Editor for .NET は、DOCX、PDF、HTML、RTF など、さまざまな形式をサポートしています。
### GroupDocs.Editor をクラウド ストレージと統合することは可能ですか?
はい、GroupDocs.Editor をさまざまなクラウド ストレージ ソリューションと統合してドキュメントを管理できます。
### GroupDocs.Editor for .NET のドキュメントはどこにありますか?
ドキュメントは入手可能です[ここ](https://tutorials.groupdocs.com/editor/net/).