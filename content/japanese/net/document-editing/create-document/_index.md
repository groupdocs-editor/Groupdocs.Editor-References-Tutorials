---
title: ドキュメントを作成
linktitle: ドキュメントを作成
second_title: GroupDocs.Editor .NET API
description: この包括的なステップバイステップのチュートリアルでは、GroupDocs.Editor for .NET を使用して Word、Excel、PowerPoint、電子ブック、電子メールのドキュメントを編集する方法を学習します。
weight: 10
url: /ja/net/document-editing/create-document/
type: docs
---
# ドキュメントを作成

## 導入
さまざまな種類のドキュメントをプログラムで編集する手間にうんざりしていませんか? GroupDocs.Editor for .NET は、このプロセスを簡素化します。この強力なツールを使用すると、開発者は Word、Excel、PowerPoint、電子書籍、電子メールなどのさまざまなドキュメント形式を簡単に編集できます。このチュートリアルでは、GroupDocs.Editor for .NET を使用してドキュメントを作成および編集する方法について詳しく説明します。プロセスをわかりやすい手順に分解して、初心者でも理解できるようにします。
## 前提条件
始める前に、以下のものを用意してください。
- マシンに Visual Studio がインストールされています。
- .NET Framework (4.0 以上)。
-  GroupDocs.Editor for .NETライブラリ。ここからダウンロードできます。[ここ](https://releases.groupdocs.com/editor/net/).
- C# プログラミングの基礎知識。
## 名前空間のインポート
まず、必要な名前空間をインポートしましょう。これにより、アプリケーションで必要なクラスとメソッドにアクセスできるようになります。
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using System.IO;
```
## ステップ1: ストリームの設定
まず、ドキュメント コンテンツのプレースホルダーとして機能するメモリ ストリームを設定する必要があります。
```csharp
Stream memoryStream = Stream.Null;
```
## ステップ2: ドキュメントを保存するためのコールバック関数
次に、新しいドキュメント ストリームを保存するコールバック関数を定義します。この関数は、ドキュメント編集プロセスの出力を処理するために不可欠です。
```csharp
void SaveNewDocument(Stream resultStream)
{
    memoryStream = resultStream;
}
```
## ステップ3: ワードプロセッサ文書の作成と編集
それでは、Word文書を作成して編集してみましょう。まずは新しい文書を作成します。`Editor` WordProcessing ドキュメントのインスタンスを作成し、デフォルトのオプションで編集します。
### デフォルトオプションで作成および編集する
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    EditableDocument defaultWordProcessingDoc = editor.Edit();
}
```
### カスタムオプションで作成および編集
さらに細かく制御するには、ページ区切りを無効にしたり、埋め込みフォントを抽出したりするオプションを指定できます。
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    WordProcessingEditOptions wordProcessingEditOptions = new WordProcessingEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true,
        FontExtraction = FontExtractionOptions.ExtractAllEmbedded
    };
    EditableDocument editableWordProcessingDocument = editor.Edit(wordProcessingEditOptions);
}
```
## ステップ4: スプレッドシートドキュメントの作成と編集
同様に、Excel ドキュメントを作成および編集することもできます。手順は次のとおりです。
### デフォルトオプションで作成および編集する
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    EditableDocument defaultEditableSpreadsheetDocument = editor.Edit();
}
```
### カスタムオプションで作成および編集
特定のワークシートをターゲットにしたり、非表示のワークシートを除外したりするには、`SpreadsheetEditOptions`.
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    SpreadsheetEditOptions spreadsheetEditOptions = new SpreadsheetEditOptions
    {
        WorksheetIndex = 0,
        ExcludeHiddenWorksheets = true
    };
    EditableDocument editableSpreadsheetDocument = editor.Edit(spreadsheetEditOptions);
}
```
## ステップ5: プレゼンテーションドキュメントの作成と編集
PowerPoint プレゼンテーションもサポートされています。その処理方法を見てみましょう。
### デフォルトオプションで作成および編集する
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    EditableDocument defaultEditablePresentationDocument = editor.Edit();
}
```
### カスタムオプションで作成および編集
表示するスライドや非表示のスライドを含めるかどうかなどのオプションを指定して、編集をカスタマイズできます。
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    PresentationEditOptions presentationEditOptions = new PresentationEditOptions
    {
        ShowHiddenSlides = false,
        SlideNumber = 0
    };
    EditableDocument editablePresentationDocument = editor.Edit(presentationEditOptions);
}
```
## ステップ6: 電子書籍ドキュメントの作成と編集
GroupDocs.Editor では、EPUB などの電子書籍形式の編集も可能です。その方法は次のとおりです。
### デフォルトオプションで作成および編集する
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EditableDocument defaultEditableEbookDocument = editor.Edit();
}
```
### カスタムオプションで作成および編集
ページ区切りと言語情報を有効または無効にして、電子書籍の編集をカスタマイズします。
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EbookEditOptions ebookEditOptions = new EbookEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true
    };
    EditableDocument editableEbookDocument = editor.Edit(ebookEditOptions);
}
```
## ステップ7: 電子メールドキュメントの作成と編集
最後に、電子メール ドキュメントを編集する方法について説明します。これには、EML などの形式が含まれます。
### デフォルトオプションで作成および編集する
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EditableDocument defaultEditableEmailDocument = editor.Edit();
}
```
### カスタムオプションで作成および編集
編集プロセスを制御するためのメール メッセージ出力オプションを指定します。
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EmailEditOptions emailEditOptions = new EmailEditOptions
    {
        MailMessageOutput = MailMessageOutput.All
    };
    EditableDocument editableEmailDocument = editor.Edit(emailEditOptions);
}
```
## ステップ8: プロセスの終了
ドキュメントを編集した後は、メモリ ストリームを適切に破棄してリソースを解放することが重要です。
```csharp
memoryStream.Dispose();
System.Console.WriteLine("CreateDocument routine has successfully finished");
```
## 結論
GroupDocs.Editor for .NET は、さまざまなドキュメント タイプをプログラムで編集する作業を簡素化できる、多機能で強力なツールです。このステップ バイ ステップ ガイドに従うことで、WordProcessing ファイル、スプレッドシート、プレゼンテーション、電子書籍、電子メールなど、ドキュメントを簡単に作成および編集できます。より高度な機能とカスタマイズ オプションについては、GroupDocs.Editor のドキュメントを参照してください。
## よくある質問
### GroupDocs.Editor for .NET で編集できるドキュメントの種類は何ですか?
ワードプロセッサ、スプレッドシート、プレゼンテーション、電子書籍、電子メールなど、幅広いドキュメントを編集できます。
### 編集オプションをカスタマイズすることは可能ですか?
はい、GroupDocs.Editor for .NET では、各ドキュメント タイプに固有のさまざまな編集オプションを通じて、広範囲にわたるカスタマイズが可能です。
### 編集したドキュメントの出力をどのように処理すればよいですか?
コールバック関数を使用して、編集したドキュメント ストリームを目的の場所に保存できます。
### GroupDocs.Editor for .NET を使用するにはライセンスが必要ですか?
はい、ライセンスは以下から取得できます。[ここ](https://purchase.groupdocs.com/buy)一時ライセンスのオプションもあります。
### より詳細なドキュメントはどこで見つかりますか?
詳細なドキュメントは、[GroupDocs.Editor for .NET ドキュメント ページ](https://tutorials.groupdocs.com/editor/net/).