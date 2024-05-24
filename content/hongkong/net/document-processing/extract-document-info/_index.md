---
title: 提取文檔資訊
linktitle: 提取文檔資訊
second_title: GroupDocs.Editor .NET API
description: 透過我們詳細的逐步教學，了解如何使用 GroupDocs.Editor for .NET 擷取文件資訊。非常適合管理各種文件類型。
type: docs
weight: 10
url: /zh-hant/net/document-processing/extract-document-info/
---
## 介紹
歡迎來到這個關於使用 GroupDocs.Editor for .NET 提取文件資訊的綜合教學。在本指南中，我們將逐步引導您完成整個過程，確保您清晰簡潔地理解每個部分。無論您是經驗豐富的開發人員還是剛剛入門，本教學都將幫助您將 GroupDocs.Editor 無縫整合到 .NET 專案中，以有效地管理和操作文件。
## 先決條件
在深入研究程式碼之前，讓我們確保您擁有所需的一切：
- C# 基礎知識：了解 C# 程式設計基礎至關重要。
- Visual Studio：確保您已安裝 Visual Studio。
-  GroupDocs.Editor for .NET：您將需要 GroupDocs.Editor for .NET 程式庫。您可以從[下載頁面](https://releases.groupdocs.com/editor/net/).
## 導入命名空間
首先，您需要匯入必要的命名空間。這允許您存取操作文件所需的類別和方法。
```csharp
using System;
using GroupDocs.Editor.Metadata;
```
## 第 1 步：載入您的文檔
首先，您需要載入要從中提取資訊的文件。這可以透過提供文件的文件路徑來完成。
```csharp
string docxInputFilePath = "YourSampleDocument.docx";
Editor editorDocx = new Editor(docxInputFilePath);
```
## 步驟2：檢索文件資訊
接下來，您將使用以下方法檢索文檔資訊`GetDocumentInfo`方法。如果您不確定文檔格式，此方法不需要任何特定的載入選項。
```csharp
IDocumentInfo infoDocx = editorDocx.GetDocumentInfo(null);
```
## 第 3 步：確定文檔類型
現在，您需要檢查您正在處理的文件類型。這很重要，因為它決定了您將如何處理文件。
```csharp
bool isSpreadsheet = infoDocx is SpreadsheetDocumentInfo;
bool isText = infoDocx is TextualDocumentInfo;
bool isWordProcessing = infoDocx is WordProcessingDocumentInfo;
Console.WriteLine($"Is '{docxInputFilePath}' a Spreadsheet: {isSpreadsheet}");
Console.WriteLine($"Is '{docxInputFilePath}' a Textual document: {isText}");
Console.WriteLine($"Is '{docxInputFilePath}' a WordProcessing document: {isWordProcessing}");
```
## 第四步：提取詳細信息
如果文檔是字處理文檔，您可以提取格式、擴展名、頁數、大小以及是否加密等詳細資訊。
```csharp
if (isWordProcessing)
{
    WordProcessingDocumentInfo casted = (WordProcessingDocumentInfo)infoDocx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Page count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```
## 步驟 5：針對不同文件類型重複此操作
對電子表格和文字文件等其他文件類型重複相同的步驟。
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
## 第 6 步：處理受密碼保護的文檔
處理受密碼保護的文件時，應先嘗試在沒有密碼的情況下開啟它們，然後使用不正確的密碼，最後使用正確的密碼。
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
## 第 7 步：處理基於文字的文檔
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
## 第 8 步：處置資源
最後，確保處置所有資源以防止記憶體洩漏。
```csharp
editorDocx.Dispose();
editorXlsx.Dispose();
editorXls.Dispose();
editorXml.Dispose();
Console.WriteLine("ExtractingDocumentInfo routine has successfully finished");
```
## 結論
恭喜！現在您已經了解如何使用 GroupDocs.Editor for .NET 來擷取文件資訊。這個強大的程式庫簡化了文件管理和操作，使您能夠無縫處理各種文件類型。無論您是處理文字處理、電子表格還是基於文字的文檔，GroupDocs.Editor 都能提供強大的解決方案。
## 常見問題解答
### GroupDocs.Editor 可以處理哪些類型的文件？
GroupDocs.Editor 可以處理各種文件類型，包括文字處理、電子表格和基於文字的文件。
### GroupDocs.Editor 可以管理受密碼保護的文件嗎？
是的，GroupDocs.Editor 可以管理受密碼保護的文件。只要輸入正確的密碼，它就可以識別並開啟這些文件。
### 是否有必要處理Editor物件？
是的，處理 Editor 物件以釋放資源並防止記憶體洩漏至關重要。
### 我可以提取有關文件格式和大小的詳細資訊嗎？
絕對地！ GroupDocs.Editor 可讓您提取詳細信息，包括格式、擴展名、大小、頁數和加密狀態。
### 如果遇到問題，我可以在哪裡獲得支援？
您可以從以下方面獲得支持[GroupDocs.Editor 支援論壇](https://forum.groupdocs.com/c/editor/20).