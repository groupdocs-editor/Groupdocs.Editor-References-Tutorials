---
date: 2026-06-01
description: GroupDocs.Editor for .NET を使用して、page count を取得し、document metadata を抽出する方法を、詳細な
  step‑by‑step tutorial で学びましょう。
keywords:
- get page count
- extract document metadata
- get document info
- find document extension
- retrieve document size
linktitle: Page Count の取得と Document Info の抽出
schemas:
- author: GroupDocs
  dateModified: '2026-06-01'
  description: Learn how to get page count and extract document metadata using GroupDocs.Editor
    for .NET in a detailed step‑by‑step tutorial.
  headline: Get Page Count & Extract Document Info with GroupDocs.Editor
  type: TechArticle
- questions:
  - answer: GroupDocs.Editor supports Word processing, spreadsheet, presentation,
      PDF, and plain‑text files—over 50 formats in total.
    question: What document types can I extract metadata from?
  - answer: Access `DocumentInfo.Extension` after calling `GetDocumentInfo()`; it
      returns the extension without the leading dot.
    question: How do I retrieve the file extension?
  - answer: Yes—`DocumentInfo.Size` returns the size in bytes; divide by 1,048,576
      to convert to megabytes.
    question: Can I get the size of a document in megabytes?
  - answer: Absolutely—GroupDocs.Editor never writes the password to disk and disposes
      of all cryptographic objects after use.
    question: Is it safe to process password‑protected files on a server?
  - answer: You can get support from the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).
    question: Where can I find additional help if I run into issues?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: GroupDocs.Editorで Page Count の取得と Document Info の抽出
type: docs
url: /ja/net/document-processing/extract-document-info/
weight: 10
---

# ページ数の取得と GroupDocs.Editor を使用したドキュメント情報の抽出

## はじめに
この包括的なチュートリアルでは、**get page count** を取得し、フォーマット、サイズ、暗号化ステータスを含む詳細なドキュメント情報を GroupDocs.Editor for .NET を使用して抽出する方法を学びます。ドキュメント管理システム、レポートエンジン、または自動変換パイプラインを構築する場合でも、ファイルのメタデータを理解することは、信頼できる処理への第一歩です。ファイルの読み込みからリソースの安全な解放まで、全体のワークフローを順に見ていきましょう。

## クイック回答
- **ドキュメントのページ数を取得するにはどうすればよいですか？**  
  `Editor` でファイルをロードした後、`editor.GetDocumentInfo().PageCount` を呼び出します。
- **メタデータ抽出に対応しているファイル形式はどれですか？**  
  DOCX、XLSX、PPTX、PDF、TXT、HTML など、50 以上の形式に対応しています。
- **パスワードで保護されたファイルからメタデータを抽出できますか？**  
  はい—`Editor` インスタンスを作成する際にパスワードを指定します。
- **リソースを手動で解放する必要がありますか？**  
  もちろんです。必ず `editor.Dispose()` を呼び出すか、`using` ブロックでエディタをラップしてください。
- **どのバージョンの GroupDocs.Editor が必要ですか？**  
  執筆時点での最新の安定版 (v23.12 以上) が、ここで示したすべての機能をサポートしています。

## GroupDocs.Editor の “get page count” とは何ですか？
`GetDocumentInfo()` は、ドキュメントのページ数、フォーマット、サイズ、その他のメタデータを含む `DocumentInfo` オブジェクトを返すメソッドです。この単一の呼び出しで、ファイルを手動で解析することなく即座に情報を取得できます。このメソッドを使用すると、ドキュメント全体をメモリにロードする必要がなくなるため、特に大きなファイルでのパフォーマンスが向上し、サーバーリソースの消費を削減できます。

## なぜ GroupDocs.Editor でドキュメントメタデータを抽出するのか？
GroupDocs.Editor は **50 以上の入力および出力フォーマット** を処理でき、**2 GB** までのファイルのメタデータをドキュメント全体をメモリにロードせずに取得できます。この効率性により、フルドキュメントの解析に比べてサーバー負荷が最大 **70 %** 減少し、高スループットなアプリケーションに最適です。

## 前提条件
- **C# 開発の基礎** – Visual Studio と .NET プロジェクト構造に慣れている必要があります。
- **Visual Studio 2022**（または最近のバージョン）をマシンにインストールしてください。
- **GroupDocs.Editor for .NET** – 最新パッケージは [download page](https://releases.groupdocs.com/editor/net/) からダウンロードしてください。

## ドキュメントの読み込み方法は？
`Editor` はドキュメントを表す主要クラスで、ロードや操作のためのメソッドを提供します。`Editor` インスタンスを作成し、ファイルパスを渡すことで対象ファイルをロードします。エディタは自動的にフォーマットを検出するため、ロードオプションを指定する必要はありません。このアプローチはすべてのサポート対象ファイルタイプで機能し、初期設定を簡素化します。

```csharp
using System;
using GroupDocs.Editor.Metadata;
```

## ドキュメント情報の取得方法は？
`GetDocumentInfo()` は、ページ数、フォーマット、サイズ、暗号化ステータスなどのメタデータを含む `DocumentInfo` オブジェクトを返します。ロード後にこのメソッドを呼び出してオブジェクトを取得します。返される `DocumentInfo` はファイルの特性を簡潔に把握できるスナップショットを提供し、追加の処理なしで判断を下すことが可能です。

```csharp
string docxInputFilePath = "YourSampleDocument.docx";
Editor editorDocx = new Editor(docxInputFilePath);
```

## ドキュメントタイプの判定方法は？
`DocumentType` は、ドキュメントが WordProcessing、Spreadsheet、または Text のどれかを示す列挙型です。ファイルがワードプロセッシング文書、スプレッドシート、プレーンテキストのいずれかであるかを把握することで、後続の処理方法が変わります。`DocumentInfo` オブジェクトの `DocumentType` プロパティを使用してこの判断を行い、ロジックを分岐させます。

```csharp
IDocumentInfo infoDocx = editorDocx.GetDocumentInfo(null);
```

## WordProcessing ファイルの詳細情報抽出方法は？
`WordProcessing` は、DOCX、ODT、RTF などのワードプロセッシングファイルとして扱われるドキュメントを指します。ドキュメントタイプが `WordProcessing` の場合、`DocumentInfo` オブジェクトから **format**、**extension**、**page count**、**size**、**encryption flag** などの追加プロパティを直接取得できます。これらの詳細は、特定の変換やセキュリティチェックを適用するなど、処理手順をカスタマイズする際に役立ちます。

```csharp
bool isSpreadsheet = infoDocx is SpreadsheetDocumentInfo;
bool isText = infoDocx is TextualDocumentInfo;
bool isWordProcessing = infoDocx is WordProcessingDocumentInfo;
Console.WriteLine($"Is '{docxInputFilePath}' a Spreadsheet: {isSpreadsheet}");
Console.WriteLine($"Is '{docxInputFilePath}' a Textual document: {isText}");
Console.WriteLine($"Is '{docxInputFilePath}' a WordProcessing document: {isWordProcessing}");
```

## スプレッドシートおよびテキストドキュメントの処理方法は？
`Spreadsheet` は XLSX などのスプレッドシートファイルを示し、`Text` はプレーンテキストドキュメントを表します。スプレッドシート（`Spreadsheet`）やプレーンテキストファイル（`Text`）でも、`DocumentInfo` オブジェクトは拡張子、サイズ、ページ数といった基本的なメタデータを提供します。形式によってはページ数が提供されない場合があり、その場合は値が `0` になります。下流のロジックでは他のメタデータを利用できます。

```csharp
if (isWordProcessing)
{
    WordProcessingDocumentInfo casted = (WordProcessingDocumentInfo)infoDocx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Page count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```

## パスワード保護されたドキュメントの扱い方は？
`Password` は暗号化されたファイルを開くために `Editor` コンストラクタに渡す文字列です。ドキュメントが暗号化されている場合、まずパスワードなしで開くことを試みます。失敗した場合は例外をキャッチし、正しいパスワードで再試行します。`Editor` コンストラクタはこの目的のために `Password` パラメータを受け付け、保護されたファイルをシームレスに処理できるようにします。

```csharp
string xlsxInputFilePath = "YourSampleDocument.xlsx";
Editor editorXlsx = new Editor(xlsxInputFilePath);
IDocumentInfo infoXlsx = editorXlsx.GetDocumentInfo(null);
bool isXlsxSpreadsheet = infoXlsx is SpreadsheetDocumentInfo;
Console.WriteLine($"Is '{xlsxInputFilePath}' a Spreadsheet: {isXlsxSpreadsheet}");
if (isXlsxSpreadsheet)
{
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo)infoXlsx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Tabs count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```

## テキストベースのドキュメントの処理方法は？
`DocumentInfo` はテキストファイルのサイズ、拡張子、エンコーディングといった基本的なメタデータを提供します。テキストファイル（例: `.txt`、`.md`）は単純なストリームとして扱われます。`DocumentInfo` からサイズとエンコーディング情報を取得でき、ファイルの整合性検証や適切な処理パイプラインの決定に役立ちます。

```csharp
string xlsInputFilePath = "YourSampleDocument.xls";
Editor editorXls = new Editor(xlsInputFilePath);
try
{
    IDocumentInfo infoXls = editorXls.GetDocumentInfo(null);
}
catch (PasswordRequiredException)
{
    Console.WriteLine("This document is password-protected.");
}
try
{
    IDocumentInfo infoXls = editorXls.GetDocumentInfo("incorrect_password");
}
catch (IncorrectPasswordException)
{
    Console.WriteLine("The provided password is incorrect.");
}
IDocumentInfo infoXlsValid = editorXls.GetDocumentInfo("correct_password");
bool isXlsSpreadsheet = infoXlsValid is SpreadsheetDocumentInfo;
Console.WriteLine($"Password-protected document is a Spreadsheet: {isXlsSpreadsheet}");
if (isXlsSpreadsheet)
{
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo)infoXlsValid;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Tabs count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```

## リソースを適切に解放する方法は？
`Editor` はアンマネージドリソースを保持する主要クラスで、使用後に必ず解放する必要があります。メモリリークを防ぐため、情報の取得が完了したら必ず `Editor` インスタンスを解放してください。`using` 文は例外が発生した場合でも確実に解放される最も安全なパターンで、クリーンなリソース管理を保証します。

```csharp
string xmlInputFilePath = "YourSampleDocument.xml";
Editor editorXml = new Editor(xmlInputFilePath);
IDocumentInfo infoXml = editorXml.GetDocumentInfo(null);
bool isXmlText = infoXml is TextualDocumentInfo;
Console.WriteLine($"Is '{xmlInputFilePath}' a Textual document: {isXmlText}");
if (isXmlText)
{
    TextualDocumentInfo casted = (TextualDocumentInfo)infoXml;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Encoding: {casted.Encoding}; Size: {casted.Size} bytes");
}
```

## よくある問題と解決策
| 問題 | 原因 | 解決策 |
|------|------|--------|
| **PageCount が 0 を返す** | フォーマットがページングに対応していない (例: プレーンテキスト) | `PageCount` に依存する前に `DocumentInfo.DocumentType` を確認してください。 |
| **サポートされていないファイル形式** | ファイル拡張子が認識されない | ファイルが 50 以上のサポート対象形式のいずれかであることを確認し、GroupDocs.Editor を最新バージョンに更新してください。 |
| **Password 例外** | 提供されたパスワードが間違っている | `PasswordProtectedException` をキャッチし、ユーザーにパスワードの再入力を促してください。 |
| **大きなファイルでメモリ使用量が急増** | ストリーミングせずに非常に大きな PDF をロードしている | `LoadOptions` の `LoadOptions.LoadMode = LoadMode.Stream` を使用してください（新しいリリースで利用可能）。 |

## よくある質問

**Q: どのドキュメントタイプからメタデータを抽出できますか？**  
A: GroupDocs.Editor はワードプロセッシング、スプレッドシート、プレゼンテーション、PDF、プレーンテキストファイルをサポートしており、合計で 50 以上の形式に対応しています。

**Q: ファイル拡張子はどうやって取得しますか？**  
A: `GetDocumentInfo()` を呼び出した後、`DocumentInfo.Extension` にアクセスします。先頭のドットなしで拡張子が返されます。

**Q: ドキュメントのサイズをメガバイトで取得できますか？**  
A: はい—`DocumentInfo.Size` はバイト単位でサイズを返すので、1,048,576 で割るとメガバイトに変換できます。

**Q: サーバー上でパスワード保護されたファイルを処理しても安全ですか？**  
A: 絶対に安全です—GroupDocs.Editor はパスワードをディスクに書き込まず、使用後はすべての暗号オブジェクトを解放します。

**Q: 問題が発生した場合、追加のサポートはどこで得られますか？**  
A: [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20) でサポートを受けられます。

---

**最終更新日:** 2026-06-01  
**テスト環境:** GroupDocs.Editor 23.12 for .NET  
**作者:** GroupDocs

```csharp
editorDocx.Dispose();
editorXlsx.Dispose();
editorXls.Dispose();
editorXml.Dispose();
Console.WriteLine("ExtractingDocumentInfo routine has successfully finished");
```

## 関連チュートリアル

- [GroupDocs.Editor を使用した .NET のメタデータ抽出マスター：包括的ガイド](/editor/net/advanced-features/groupdocs-editor-net-metadata-extraction-guide/)
- [GroupDocs.Editor for .NET のドキュメントロードチュートリアル](/editor/net/document-loading/)
- [GroupDocs.Editor .NET で効率的なドキュメント編集：HTML を編集可能なドキュメントに変換](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)