---
title: ドキュメント情報の抽出
linktitle: ドキュメント情報の抽出
second_title: GroupDocs.Editor .NET API
description: 詳細なステップバイステップのチュートリアルで、GroupDocs.Editor for .NET を使用してドキュメント情報を抽出する方法を学びます。さまざまな種類のドキュメントを管理するのに最適です。
weight: 10
url: /ja/net/document-processing/extract-document-info/
---
## 導入
GroupDocs.Editor for .NET を使用してドキュメント情報を抽出する包括的なチュートリアルへようこそ。このガイドでは、プロセスをステップごとに説明し、各部分を明確かつ簡潔に理解できるようにします。熟練した開発者でも、初心者でも、このチュートリアルは、GroupDocs.Editor を .NET プロジェクトにシームレスに統合して、ドキュメントを効率的に管理および操作するのに役立ちます。
## 前提条件
コードに進む前に、必要なものがすべて揃っていることを確認しましょう。
- C# の基礎知識: C# プログラミングの基礎を理解することが不可欠です。
- Visual Studio: Visual Studio がインストールされていることを確認してください。
-  GroupDocs.Editor for .NET: GroupDocs.Editor for .NETライブラリが必要です。ダウンロードは以下から行えます。[ダウンロードページ](https://releases.groupdocs.com/editor/net/).
## 名前空間のインポート
まず、必要な名前空間をインポートする必要があります。これにより、ドキュメントの操作に必要なクラスとメソッドにアクセスできるようになります。
```csharp
using System;
using GroupDocs.Editor.Metadata;
```
## ステップ1: ドキュメントを読み込む
まず、情報を抽出するドキュメントを読み込む必要があります。これは、ドキュメントへのファイル パスを提供することで実行できます。
```csharp
string docxInputFilePath = "YourSampleDocument.docx";
Editor editorDocx = new Editor(docxInputFilePath);
```
## ステップ2: ドキュメント情報を取得する
次に、`GetDocumentInfo`方法。ドキュメントの形式が不明な場合、この方法では特定の読み込みオプションは必要ありません。
```csharp
IDocumentInfo infoDocx = editorDocx.GetDocumentInfo(null);
```
## ステップ3: ドキュメントの種類を決定する
次に、扱っている文書の種類を確認する必要があります。これは、文書の取り扱い方法を決定するため、非常に重要です。
```csharp
bool isSpreadsheet = infoDocx is SpreadsheetDocumentInfo;
bool isText = infoDocx is TextualDocumentInfo;
bool isWordProcessing = infoDocx is WordProcessingDocumentInfo;
Console.WriteLine($"Is '{docxInputFilePath}' a Spreadsheet: {isSpreadsheet}");
Console.WriteLine($"Is '{docxInputFilePath}' a Textual document: {isText}");
Console.WriteLine($"Is '{docxInputFilePath}' a WordProcessing document: {isWordProcessing}");
```
## ステップ4: 詳細情報の抽出
文書がワープロ文書である場合は、形式、拡張子、ページ数、サイズ、暗号化されているかどうかなどの詳細情報を抽出できます。
```csharp
if (isWordProcessing)
{
    WordProcessingDocumentInfo casted = (WordProcessingDocumentInfo)infoDocx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Page count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```
## ステップ5: 異なるドキュメントタイプで繰り返します
スプレッドシートやテキスト文書などの他の文書タイプについても、同じ手順を繰り返します。
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
## ステップ6: パスワードで保護されたドキュメントを処理する
パスワードで保護されたドキュメントを扱うときは、最初にパスワードなしで開いてみて、次に間違ったパスワードで開いてみて、最後に正しいパスワードで開いてみることをお勧めします。
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
## ステップ7: テキストベースのドキュメントを処理する
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
## ステップ8: リソースを破棄する
最後に、メモリ リークを防ぐために、すべてのリソースを破棄するようにしてください。
```csharp
editorDocx.Dispose();
editorXlsx.Dispose();
editorXls.Dispose();
editorXml.Dispose();
Console.WriteLine("ExtractingDocumentInfo routine has successfully finished");
```
## 結論
おめでとうございます。これで、GroupDocs.Editor for .NET を使用してドキュメント情報を抽出する方法を学習しました。この強力なライブラリは、ドキュメントの管理と操作を簡素化し、さまざまな種類のドキュメントをシームレスに処理できるようにします。ワード プロセッサ、スプレッドシート、またはテキスト ベースのドキュメントのいずれを扱う場合でも、GroupDocs.Editor は堅牢なソリューションを提供します。
## よくある質問
### GroupDocs.Editor はどのような種類のドキュメントを処理できますか?
GroupDocs.Editor は、ワードプロセッサ、スプレッドシート、テキストベースのドキュメントなど、さまざまな種類のドキュメントを処理できます。
### GroupDocs.Editor はパスワードで保護されたドキュメントを管理できますか?
はい、GroupDocs.Editor はパスワードで保護されたドキュメントを管理できます。正しいパスワードが与えられれば、これらのドキュメントを識別して開くことができます。
### Editor オブジェクトを破棄する必要がありますか?
はい、リソースを解放し、メモリ リークを防ぐために、Editor オブジェクトを破棄することが重要です。
### ドキュメントの形式やサイズに関する詳細な情報を抽出できますか?
もちろんです! GroupDocs.Editor を使用すると、形式、拡張子、サイズ、ページ数、暗号化ステータスなどの詳細情報を抽出できます。
### 問題が発生した場合、どこでサポートを受けることができますか?
サポートを受けるには[GroupDocs.Editor サポート フォーラム](https://forum.groupdocs.com/c/editor/20).