---
date: 2026-09-21
description: Office を使用せずに GroupDocs.Editor for .NET で PowerPoint を編集する方法を学び、Word、Excel、EPUB
  を編集し、編集されたドキュメントストリームを取得します。
keywords:
- edit powerpoint without office
- GroupDocs.Editor .NET
- document editing .NET
- edit presentation programmatically
lastmod: 2026-09-21
linktitle: ドキュメントを作成
og_description: Office を使用せずに GroupDocs.Editor for .NET で PowerPoint を編集します。このガイドでは、プレゼンテーション、Word、Excel、EPUB
  を変更し、編集されたドキュメントストリームを保存する方法を示します。
og_image_alt: Guide showing code to edit PowerPoint presentations without Microsoft
  Office using GroupDocs.Editor for .NET
og_title: Office を使用せずに GroupDocs.Editor for .NET で PowerPoint を編集
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to edit PowerPoint without Office using GroupDocs.Editor
    for .NET, edit Word, Excel, EPUB and capture the edited document stream.
  headline: Edit powerpoint without office with GroupDocs.Editor for .NET
  type: TechArticle
- questions:
  - answer: You can edit WordProcessing, spreadsheets, presentations, ebooks, and
      emails—including PowerPoint files for the **edit powerpoint without office**
      use case.
    question: What types of documents can I edit with GroupDocs.Editor for .NET?
  - answer: Yes, each format has its own options class (e.g., `WordProcessingEditOptions`,
      `SpreadsheetEditOptions`, `PresentationEditOptions`) that let you fine‑tune
      pagination, hidden slides, worksheet selection, etc.
    question: Is it possible to customize the editing options?
  - answer: Use the callback function (`SaveNewDocument`) to capture the edited stream,
      then you can write it to disk, a database, or return it from a web API.
    question: How do I handle the output of the edited documents?
  - answer: Yes, a license is required for production. You can obtain one from the
      [GroupDocs.Editor purchase page](https://purchase.groupdocs.com/buy). A temporary
      trial license is also available.
    question: Do I need a license to use GroupDocs.Editor for .NET?
  - answer: Detailed documentation is available on the [GroupDocs.Editor for .NET
      documentation page](https://tutorials.groupdocs.com/editor/net/).
    question: Where can I find more detailed documentation?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
tags:
- edit powerpoint
- GroupDocs.Editor
- .NET document processing
title: Office を使用せずに GroupDocs.Editor for .NET で PowerPoint を編集
type: docs
url: /ja/net/document-editing/create-document/
weight: 10
---

# OfficeなしでPowerPointを編集する - GroupDocs.Editor for .NET

## はじめに
プログラムで **OfficeなしでPowerPointを編集** する信頼できる方法を探しているなら、GroupDocs.Editor for .NET が答えです。このライブラリを使用すると、Word、Excel、PowerPoint、Ebook、Email のフォーマットをすべて、単一の使いやすい API で操作できます。このチュートリアルでは、サポートされている各ドキュメントタイプの作成と編集の手順を解説し、**編集したドキュメント** ストリームの保存方法を示し、実際のプロジェクトで活用できる実用的なヒントを提供します。

## クイック回答
- **.NETでPowerPointファイルを編集できるライブラリは何ですか？** GroupDocs.Editor for .NET.  
- **同じ API で Word、Excel、Epub ファイルを編集できますか？** はい、同じ `Editor` クラスがこれらすべてのフォーマットをサポートします。  
- **編集されたファイルはどうやって取得しますか？** 結果ストリームを受け取るコールバック関数（例: `SaveNewDocument`）を提供します。  
- **本番環境で使用するにはライセンスが必要ですか？** はい—ライセンスを購入するか、または一時的なトライアルライセンスを使用してください。  
- **サポートされている .NET バージョンはどれですか？** .NET Framework 4.0 以上、.NET Core、そして .NET 5/6。

## OfficeなしでPowerPointを編集するとは？
Office を使用せずに PowerPoint プレゼンテーションを編集するとは、`.pptx` ファイルを読み込み、スライドやテキスト、非表示要素の変更などを適用し、更新されたファイルを取得することです。サーバーに Microsoft PowerPoint がインストールされている必要はありません。

## なぜ GroupDocs.Editor for .NET を使用するのか？
GroupDocs.Editor は **5 以上の主要なドキュメントタイプ**（Word、Excel、PowerPoint、EPUB、Email）をサポートし、ストリームベースのアーキテクチャにより、サイズが **500 MB** までのファイルを処理しながらメモリ使用量を **100 MB** 未満に抑えることができます。このライブラリは **Windows、Linux、macOS** 上で動作し、クラウドネイティブサービス、CI パイプライン、コンテナ化されたワークロードに最適です。

## 前提条件
- Visual Studio（任意の最新エディション）。  
- .NET Framework 4.0 以上（または .NET Core/.NET 5+）。  
- GroupDocs.Editor for .NET ライブラリ – [download the GroupDocs.Editor for .NET library](https://releases.groupdocs.com/editor/net/)。  
- 基本的な C# の知識。

## 名前空間のインポート
`Editor` クラスは `GroupDocs.Editor` 名前空間にあり、フォーマット固有のオプションクラスはそれぞれのサブ名前空間に配置されています。

`Editor` はドキュメントをロードし、編集可能な表現を提供し、変更されたコンテンツをストリームに書き戻すコアクラスです。  

```csharp
using GroupDocs.Editor;
using GroupDocs.Editor.Options;
using System.IO;
```

```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using System.IO;
```

## 手順 1: ストリームの設定
ストリームを使用すると、ワークフロー全体をメモリ上に保持できるため、Web API やサーバーレス関数に最適です。

`MemoryStream` は軽量で拡張可能なバッファで、ディスク上のファイルを模倣しますが、RAM 上に保持されます。  

```csharp
byte[] fileBytes = File.ReadAllBytes("sample.pptx");
var inputStream = new MemoryStream(fileBytes);
```

```csharp
Stream memoryStream = Stream.Null;
```

## 手順 2: **編集したドキュメントを保存** するコールバック関数
コールバックは `Editor` の処理が完了した後に編集されたストリームを受け取ります。その後、ディスクやデータベースに書き込むか、API エンドポイントから返すことができます。

`SaveNewDocument` は、編集が完了した際に SDK が自動的に呼び出すユーザー定義メソッドです。  

```csharp
void SaveNewDocument(Stream editedStream)
{
    using var file = File.Create("output.pptx");
    editedStream.CopyTo(file);
}
```

```csharp
void SaveNewDocument(Stream resultStream)
{
    memoryStream = resultStream;
}
```

## 手順 3: ワードプロセッシングドキュメントの作成と編集  
(ここでは **.NETでWordドキュメントを編集** します。)

### デフォルトオプションで作成と編集
`WordProcessingEditOptions` クラスは DOCX ファイルに対して適切なデフォルト設定を提供します。

`WordProcessingEditOptions` は、エディタがページング、変更履歴、埋め込みオブジェクトをどのように処理するかを定義します。  

```csharp
var editor = new Editor(inputStream, new WordProcessingEditOptions());
var editable = editor.Edit();
editable.Replace("{Placeholder}", "Actual value");
editor.Save(SaveNewDocument);
```

```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    EditableDocument defaultWordProcessingDoc = editor.Edit();
}
```

### カスタムオプションで作成と編集
スペルチェックや変更履歴など、特定の機能をオンまたはオフにできます。

`WordProcessingEditOptions` では、監査トレイル用に `EnableTrackChanges` を有効にできます。  

```csharp
var options = new WordProcessingEditOptions
{
    EnableTrackChanges = true,
    EnableSpellCheck = false
};
var editor = new Editor(inputStream, options);
```

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

## 手順 4: スプレッドシートドキュメントの作成と編集  
（**.NETでExcelファイルを編集** するために使用します。）

### デフォルトオプションで作成と編集
`SpreadsheetEditOptions` は、ロードするワークシートと数式を評価するかどうかを制御します。

`SpreadsheetEditOptions` はデフォルトで最初のワークシートを選択します。  

```csharp
var editor = new Editor(inputStream, new SpreadsheetEditOptions());
var editable = editor.Edit();
editable.ReplaceCell("A1", "42");
editor.Save(SaveNewDocument);
```

```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    EditableDocument defaultEditableSpreadsheetDocument = editor.Edit();
}
```

### カスタムオプションで作成と編集
パフォーマンス向上のために、別のワークシートインデックスを指定したり、数式評価を無効にしたりできます。

`SpreadsheetEditOptions` では `WorksheetIndex` と `EnableFormulaEvaluation` を設定できます。  

```csharp
var options = new SpreadsheetEditOptions
{
    WorksheetIndex = 2,
    EnableFormulaEvaluation = false
};
var editor = new Editor(inputStream, options);
```

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

## 手順 5: OfficeなしでPowerPointを編集 – プレゼンテーションドキュメントの作成と編集
これは主要キーワードの中心となる部分です。

### デフォルトオプションで作成と編集
`PresentationEditOptions` は、非表示スライドを含めるかどうかと、デフォルトの編集対象スライドを決定します。

`PresentationEditOptions` はデフォルトで非表示スライドを含みますが、切り替えることができます。  

```csharp
var editor = new Editor(inputStream, new PresentationEditOptions());
var editable = editor.Edit();
editable.ReplaceSlideText(0, "{Title}", "Quarterly Report");
editor.Save(SaveNewDocument);
```

```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    EditableDocument defaultEditablePresentationDocument = editor.Edit();
}
```

### カスタムオプションで作成と編集
特定のスライドを編集するために `SlideNumber` を変更したり、ノートページの含めることを無効にしたりできます。

`PresentationEditOptions` では `SlideNumber` と `IncludeNotes` を設定できます。  

```csharp
var options = new PresentationEditOptions
{
    SlideNumber = 2,
    IncludeNotes = false
};
var editor = new Editor(inputStream, options);
```

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

## 手順 6: 電子書籍ドキュメントの作成と編集  
（ここでは **epub ファイルを編集** します。）

### デフォルトオプションで作成と編集
`EbookEditOptions` は EPUB と内部の HTML 表現間の変換を処理します。

`EbookEditOptions` は EPUB コンテンツにデフォルトの HTML レンダラーを使用します。  

```csharp
var editor = new Editor(inputStream, new EbookEditOptions());
var editable = editor.Edit();
editable.Replace("{Author}", "Jane Doe");
editor.Save(SaveNewDocument);
```

```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EditableDocument defaultEditableEbookDocument = editor.Edit();
}
```

### カスタムオプションで作成と編集
元の CSS を保持したり、プレーンテキストレイアウトを強制したりできます。

`EbookEditOptions` は `PreserveCss` と `PlainTextOnly` フラグを提供します。  

```csharp
var options = new EbookEditOptions
{
    PreserveCss = true,
    PlainTextOnly = false
};
var editor = new Editor(inputStream, options);
```

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

## 手順 7: メールドキュメントの作成と編集

### デフォルトオプションで作成と編集
`EmailEditOptions` を使用すると、.eml ファイルの本文、件名、添付ファイルを操作できます。

`EmailEditOptions` はシンプルな置換のためにメール本文をプレーンテキストとしてロードします。  

```csharp
var editor = new Editor(inputStream, new EmailEditOptions());
var editable = editor.Edit();
editable.Replace("{Recipient}", "john@example.com");
editor.Save(SaveNewDocument);
```

```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EditableDocument defaultEditableEmailDocument = editor.Edit();
}
```

### カスタムオプションで作成と編集
元の MIME ヘッダーを保持したり、クリーンなテキストバージョンのために除去したりできます。

`EmailEditOptions` には MIME メタデータを保持または破棄するための `KeepHeaders` が含まれています。  

```csharp
var options = new EmailEditOptions
{
    KeepHeaders = false
};
var editor = new Editor(inputStream, options);
```

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

## 手順 8: プロセスの最終化
作業が完了したらストリームを破棄してリソースを解放します。適切に破棄することで、Web API やバックグラウンドワーカーなどの長時間実行されるサービスでのメモリリークを防止できます。

```csharp
inputStream.Dispose();
```

```csharp
memoryStream.Dispose();
System.Console.WriteLine("CreateDocument routine has successfully finished");
```

## よくある落とし穴とヒント
- **ストリームの破棄を忘れないでください** – 開いたままにすると、長時間実行されるサービスでメモリリークが発生する可能性があります。  
- **PowerPoint を編集する際は `SlideNumber` を正しく設定してください**；設定しないと最初のスライドが重複することがあります。  
- **元のファイル名を保持する必要がある場合**、コールバックの前に保存し、編集後に出力ストリームの名前を変更します。  
- **大きなドキュメントの場合**、チャンク単位で処理するか、`Editor` を一時ファイルと併用してメモリ消費を抑えることを検討してください。  
- **本番環境で予期しない動作をトラブルシュートする必要がある場合**、`EditorOptions` でロギングを有効にしてください。

## よくある質問

**Q: GroupDocs.Editor for .NET で編集できるドキュメントの種類は何ですか？**  
A: WordProcessing、スプレッドシート、プレゼンテーション、電子書籍、メールを編集できます。**OfficeなしでPowerPointを編集** するユースケースの PowerPoint ファイルも含まれます。

**Q: 編集オプションをカスタマイズできますか？**  
A: はい、各フォーマットには独自のオプションクラス（例: `WordProcessingEditOptions`、`SpreadsheetEditOptions`、`PresentationEditOptions`）があり、ページング、非表示スライド、ワークシート選択などを細かく調整できます。

**Q: 編集されたドキュメントの出力はどのように処理すればよいですか？**  
A: コールバック関数（`SaveNewDocument`）を使用して編集されたストリームを取得し、ディスクやデータベースに書き込むか、Web API から返すことができます。

**Q: GroupDocs.Editor for .NET の使用にはライセンスが必要ですか？**  
A: はい、本番環境ではライセンスが必要です。ライセンスは [GroupDocs.Editor purchase page](https://purchase.groupdocs.com/buy) から取得できます。臨時のトライアルライセンスも利用可能です。

**Q: 詳細なドキュメントはどこで見つけられますか？**  
A: 詳細なドキュメントは [GroupDocs.Editor for .NET documentation page](https://tutorials.groupdocs.com/editor/net/) にあります。

## 結論
GroupDocs.Editor for .NET を使用すれば、**OfficeなしでPowerPoint** ファイルやその他多数のドキュメントタイプを簡単に編集できます。上記の手順に従うことで、コードだけでドキュメントを作成・変更し、**編集したドキュメント** ストリームを保存でき、Office のインストールに依存する必要はありません。ライブラリの高度なオプションを活用して、ビジネスニーズに合わせた編集体験を実現してください。

---

**最終更新日:** 2026-09-21  
**テスト環境:** GroupDocs.Editor for .NET（最新リリース）  
**作者:** GroupDocs

## 関連チュートリアル

- [GroupDocs.Editor .NET 用 プレゼンテーションドキュメント編集チュートリアル](/editor/net/presentation-documents/)
- [GroupDocs.Editor .NET で編集可能なドキュメントを作成](/editor/net/document-editing/groupdocs-editor-net-edit-manage-documents-guide/)
- [GroupDocs.Editor を使用した .NET でオプションなしでドキュメントをロードする包括的ガイド](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)