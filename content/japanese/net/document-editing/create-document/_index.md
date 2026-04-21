---
date: 2026-03-14
description: .NET 用の GroupDocs.Editor を使用して PowerPoint プレゼンテーションやその他のドキュメントタイプを編集する方法を学びます。このガイドでは、編集したドキュメントの保存方法や
  Word ドキュメントの編集方法もカバーしています。
linktitle: Create Document
second_title: GroupDocs.Editor .NET API
title: GroupDocs.Editor for .NET で PowerPoint プレゼンテーションを編集
type: docs
url: /ja/net/document-editing/create-document/
weight: 10
---

latest release)" translate maybe keep as is? The label "Tested With:" translate? Probably translate label but keep content. Keep bold formatting.

"**Author:** GroupDocs" translate label.

Now produce final content.

Let's craft translation.

Be careful with bullet list formatting.

Proceed.

# Edit PowerPoint Presentation with GroupDocs.Editor for .NET

## はじめに
プログラムから **edit PowerPoint presentation** ファイルを確実に編集したい場合は、GroupDocs.Editor for .NET が最適です。このライブラリは Word、Excel、PowerPoint、Ebook、Email 形式をすべて単一の使いやすい API で扱うことができます。本チュートリアルでは、サポートされている各ドキュメントタイプの作成と編集手順を解説し、**save edited document** ストリームの取得方法を示し、実際のプロジェクトで活用できる実用的なヒントを提供します。

## クイック回答
- **.NET で PowerPoint ファイルを編集できるライブラリは何ですか？** GroupDocs.Editor for .NET.  
- **同じ API で Word、Excel、Epub ファイルも編集できますか？** はい、同じ `Editor` クラスがすべてのフォーマットをサポートしています。  
- **編集されたファイルはどうやって取得しますか？** 結果ストリームを受け取るコールバック関数（例: `SaveNewDocument`）を提供します。  
- **本番環境で使用するためにライセンスは必要ですか？** はい—ライセンスを購入するか、期間限定のトライアルライセンスを使用してください。  
- **サポートされている .NET バージョンはどれですか？** .NET Framework 4.0+、.NET Core、.NET 5/6。

## GroupDocs.Editor での “edit PowerPoint presentation” とは？
PowerPoint プレゼンテーションの編集とは、`.pptx` ファイルを読み込み、スライドやテキスト、非表示要素などの変更を加え、更新されたファイルを取得することを指します。Microsoft Office がインストールされている必要はありません。

## なぜ GroupDocs.Editor for .NET を使うのか？
- **多数のフォーマットに対応した単一 API** – Word、Excel、Epub 用に別々のライブラリを用意する必要がありません。  
- **Office 依存なし** – サーバー、コンテナ、CI パイプライン上でも動作します。  
- **細かな制御が可能** – ページング、言語情報、フォント抽出などをカスタマイズできます。  
- **ストリームベースの処理** – 物理ファイルではなくメモリストリームで操作できるため、クラウドサービスに最適です。

## 前提条件
- Visual Studio（最新版のいずれか）。  
- .NET Framework 4.0 以上（または .NET Core/.NET 5+）。  
- GroupDocs.Editor for .NET ライブラリ – [こちら](https://releases.groupdocs.com/editor/net/) からダウンロード。  
- 基本的な C# の知識。

## 名前空間のインポート
まず、使用するコアクラスが含まれる名前空間をインポートします。

```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using System.IO;
```

## Step 1: ストリームの設定
ドキュメント内容のプレースホルダーとしてメモリストリームを使用します。

```csharp
Stream memoryStream = Stream.Null;
```

## Step 2: **save edited document** 用コールバック関数
編集されたストリームを受け取り、`memoryStream` に保存するコールバックを定義します。

```csharp
void SaveNewDocument(Stream resultStream)
{
    memoryStream = resultStream;
}
```

## Step 3: WordProcessing ドキュメントの作成と編集  
(Here we **edit word document .net**.)

### デフォルトオプションで作成・編集
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    EditableDocument defaultWordProcessingDoc = editor.Edit();
}
```

### カスタムオプションで作成・編集
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

## Step 4: Spreadsheet ドキュメントの作成と編集  
(Use this to **edit excel file .net**.)

### デフォルトオプションで作成・編集
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    EditableDocument defaultEditableSpreadsheetDocument = editor.Edit();
}
```

### カスタムオプションで作成・編集
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

## Step 5: **Edit PowerPoint Presentation** – プレゼンテーションドキュメントの作成と編集
本キーワードの中心となるセクションです。

### デフォルトオプションで作成・編集
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    EditableDocument defaultEditablePresentationDocument = editor.Edit();
}
```

### カスタムオプションで作成・編集
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

## Step 6: Ebook ドキュメントの作成と編集  
(Here we **edit epub file**.)

### デフォルトオプションで作成・編集
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EditableDocument defaultEditableEbookDocument = editor.Edit();
}
```

### カスタムオプションで作成・編集
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

## Step 7: Email ドキュメントの作成と編集
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EditableDocument defaultEditableEmailDocument = editor.Edit();
}
```

### カスタムオプションで作成・編集
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

## Step 8: プロセスの完了
作業が終わったらストリームを破棄してリソースを解放します。

```csharp
memoryStream.Dispose();
System.Console.WriteLine("CreateDocument routine has successfully finished");
```

## よくある落とし穴とヒント
- **ストリームの破棄を忘れない** – 開いたままにすると長時間稼働するサービスでメモリリークが発生します。  
- **PowerPoint を編集する際は `SlideNumber` を正しく設定** – 設定ミスだと最初のスライドが重複します。  
- **元のファイル名を保持したい場合** – コールバック前に名前を保存し、編集後に出力ストリームの名前を変更します。  
- **大容量ドキュメントの場合** – チャンク処理や一時ファイルを使用した `Editor` の利用を検討し、メモリ使用量を抑えます。

## FAQ

**Q: GroupDocs.Editor for .NET で編集できるドキュメントの種類は何ですか？**  
A: WordProcessing、スプレッドシート、プレゼンテーション、Ebook、メールの各形式を編集できます。**edit PowerPoint presentation** のユースケースも含まれます。

**Q: 編集オプションはカスタマイズできますか？**  
A: はい。各フォーマットには独自のオプションクラス（例: `WordProcessingEditOptions`、`SpreadsheetEditOptions`、`PresentationEditOptions`）があり、ページングや非表示スライド、シート選択などを細かく調整できます。

**Q: 編集後のドキュメントはどう扱えばよいですか？**  
A: コールバック関数（`SaveNewDocument`）で編集ストリームを取得し、ディスク、データベース、または Web API のレスポンスとして保存できます。

**Q: GroupDocs.Editor for .NET の使用にライセンスは必要ですか？**  
A: はい、本番環境ではライセンスが必須です。[こちら](https://purchase.groupdocs.com/buy) から購入できます。期間限定のトライアルライセンスも利用可能です。

**Q: 詳細なドキュメントはどこで確認できますか？**  
A: 詳細なドキュメントは [GroupDocs.Editor for .NET documentation page](https://tutorials.groupdocs.com/editor/net/) にあります。

## 結論
GroupDocs.Editor for .NET を使用すれば、**edit PowerPoint presentation** ファイルはもちろん、さまざまなドキュメントタイプをコードだけで簡単に作成・変更・**save edited document** ストリームとして保存できます。Office のインストールに依存せず、ビジネスニーズに合わせた高度なオプションで編集体験をカスタマイズしてください。

---

**Last Updated:** 2026-03-14  
**Tested With:** GroupDocs.Editor for .NET (latest release)  
**Author:** GroupDocs