---
date: 2026-06-01
description: 學習如何使用 GroupDocs.Editor for .NET 透過詳細的逐步教學，取得頁數並擷取文件中繼資料。
keywords:
- get page count
- extract document metadata
- get document info
- find document extension
- retrieve document size
linktitle: 取得頁數與擷取文件資訊
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
title: 使用 GroupDocs.Editor 取得頁數與擷取文件資訊
type: docs
url: /zh-hant/net/document-processing/extract-document-info/
weight: 10
---

# 取得頁數與提取文件資訊（使用 GroupDocs.Editor）

## 簡介
在本完整教學中，您將學習如何 **get page count** 並使用 GroupDocs.Editor for .NET 提取詳細的文件資訊——包括格式、大小與加密狀態。無論您是構建文件管理系統、報表引擎，或是自動化轉換流程，了解檔案的中繼資料都是可靠處理的第一步。讓我們從載入檔案到安全釋放資源，完整走過整個工作流程。

## 快速解答
- **如何取得文件的頁數？**  
  在使用 `Editor` 載入檔案後，呼叫 `editor.GetDocumentInfo().PageCount`。
- **支援哪些檔案格式的中繼資料提取？**  
  超過 50 種格式，包括 DOCX、XLSX、PPTX、PDF、TXT 與 HTML。
- **我可以從受密碼保護的檔案提取中繼資料嗎？**  
  可以——在建立 `Editor` 實例時提供密碼。
- **我需要手動釋放資源嗎？**  
  當然需要；請始終呼叫 `editor.Dispose()` 或將 editor 包於 `using` 區塊中。
- **需要哪個版本的 GroupDocs.Editor？**  
  最新的穩定版（撰寫時為 v23.12 以上）支援本文展示的全部功能。

## 「get page count」在 GroupDocs.Editor 中是什麼？
`GetDocumentInfo()` 是一個方法，會回傳包含文件頁數、格式、大小以及其他中繼資料的 `DocumentInfo` 物件。只要一次呼叫即可即時取得資訊，無需手動解析檔案。使用此方法可避免將整個文件載入記憶體，提升效能，特別是對於大型檔案，並減少伺服器資源消耗。

## 為何使用 GroupDocs.Editor 提取文件中繼資料？
GroupDocs.Editor 能處理 **50+ 輸入與輸出格式**，並可在不將整個文件載入記憶體的情況下，取得最高 **2 GB** 檔案的中繼資料。此效率相較於完整文件解析可降低伺服器負載最高 **70 %**，非常適合高吞吐量的應用程式。

## 前置條件
- **C# 開發基礎** – 您應該熟悉 Visual Studio 與 .NET 專案結構。
- **Visual Studio 2022**（或任何較新版本）已安裝於您的機器上。
- **GroupDocs.Editor for .NET** – 從 [download page](https://releases.groupdocs.com/editor/net/) 下載最新套件。

## 如何載入文件？
`Editor` 是代表文件的主要類別，提供載入與操作文件的方法。透過建立 `Editor` 實例並傳入檔案路徑，即可載入目標檔案。編輯器會自動偵測格式，無需指定載入選項。此方式適用於所有支援的檔案類型，簡化初始設定。

```csharp
using System;
using GroupDocs.Editor.Metadata;
```

## 如何取得文件資訊？
`GetDocumentInfo()` 會回傳包含頁數、格式、大小與加密狀態等中繼資料的 `DocumentInfo` 物件。載入後呼叫此方法即可取得該物件。回傳的 `DocumentInfo` 為檔案特性的簡要快照，讓您在不進一步處理的情況下即可作出決策。

```csharp
string docxInputFilePath = "YourSampleDocument.docx";
Editor editorDocx = new Editor(docxInputFilePath);
```

## 如何判斷文件類型？
`DocumentType` 是一個列舉，指示文件是 WordProcessing、Spreadsheet 或 Text。了解檔案是文字處理文件、試算表或純文字，會影響後續的處理方式。使用 `DocumentInfo` 物件的 `DocumentType` 屬性來做此判斷，並依此分支您的邏輯。

```csharp
IDocumentInfo infoDocx = editorDocx.GetDocumentInfo(null);
```

## 如何提取 Word 處理文件的詳細資訊？
`WordProcessing` 指的是像 DOCX、ODT、RTF 等作為文字處理文件處理的文件。若文件類型為 `WordProcessing`，您可以直接從 `DocumentInfo` 物件讀取額外屬性，如 **format**、**extension**、**page count**、**size** 與 **encryption flag**。這些細節有助於您自訂處理步驟，例如套用特定轉換或安全檢查。

```csharp
bool isSpreadsheet = infoDocx is SpreadsheetDocumentInfo;
bool isText = infoDocx is TextualDocumentInfo;
bool isWordProcessing = infoDocx is WordProcessingDocumentInfo;
Console.WriteLine($"Is '{docxInputFilePath}' a Spreadsheet: {isSpreadsheet}");
Console.WriteLine($"Is '{docxInputFilePath}' a Textual document: {isText}");
Console.WriteLine($"Is '{docxInputFilePath}' a WordProcessing document: {isWordProcessing}");
```

## 如何處理試算表與文字文件？
`Spreadsheet` 代表試算表檔案，如 XLSX，而 `Text` 代表純文字文件。對於試算表（`Spreadsheet`）與純文字檔（`Text`），`DocumentInfo` 仍提供核心中繼資料（extension、size、page count）。某些格式可能不會顯示頁數，這時其值會是 `0`。您仍可依賴其他中繼資料進行後續邏輯。

```csharp
if (isWordProcessing)
{
    WordProcessingDocumentInfo casted = (WordProcessingDocumentInfo)infoDocx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Page count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```

## 如何處理受密碼保護的文件？
`Password` 是傳遞給 `Editor` 建構函式的字串，用於開啟加密檔案。當文件被加密時，請先嘗試在未提供密碼的情況下開啟；若失敗，捕捉例外後再以正確的密碼重試。`Editor` 建構函式接受 `Password` 參數，以便順暢處理受保護的檔案。

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

## 如何處理文字型文件？
`DocumentInfo` 為文字檔提供基本中繼資料，如 size、extension 與 encoding。文字檔（例如 `.txt`、`.md`）被視為簡單的串流。您仍可從 `DocumentInfo` 取得大小與編碼資訊，這對驗證檔案完整性或決定適當的處理流程很有幫助。

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

## 如何正確釋放資源？
`Editor` 是持有非受控資源的主要類別，使用完畢後必須釋放。為避免記憶體洩漏，請在完成資訊提取後始終釋放 `Editor` 實例。`using` 陳述式是最安全的模式，因為即使發生例外也能保證釋放，確保資源管理乾淨。

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

## 常見問題與解決方案
| 問題 | 原因 | 解決方案 |
|-------|-------|----------|
| **PageCount returns 0** | 格式不支援分頁（例如純文字） | 在依賴 `PageCount` 前，先檢查 `DocumentInfo.DocumentType`。 |
| **Unsupported file format** | 檔案副檔名未被識別 | 確認檔案屬於 50+ 支援的格式之一；將 GroupDocs.Editor 更新至最新版本。 |
| **Password exception** | 提供的密碼錯誤 | 捕捉 `PasswordProtectedException`，並提示使用者重新輸入密碼。 |
| **Memory spike on large files** | 在未使用串流的情況下載入極大 PDF | 使用 `LoadOptions` 並將 `LoadOptions.LoadMode = LoadMode.Stream`（在較新版本中可用）。 |

## 常見問答

**Q: 我可以從哪些文件類型提取中繼資料？**  
A: GroupDocs.Editor 支援文字處理、試算表、簡報、PDF 與純文字檔——總計超過 50 種格式。

**Q: 我如何取得檔案副檔名？**  
A: 在呼叫 `GetDocumentInfo()` 後存取 `DocumentInfo.Extension`；它會回傳不含前置點的副檔名。

**Q: 我能以兆位元組取得文件大小嗎？**  
A: 可以——`DocumentInfo.Size` 以位元組回傳大小；除以 1,048,576 即可換算成 MB。

**Q: 在伺服器上處理受密碼保護的檔案安全嗎？**  
A: 絕對安全——GroupDocs.Editor 從不將密碼寫入磁碟，且在使用後會釋放所有加密物件。

**Q: 若遇到問題，我可以在哪裡取得更多協助？**  
A: 您可以在 [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20) 獲得支援。

---

**最後更新：** 2026-06-01  
**測試環境：** GroupDocs.Editor 23.12 for .NET  
**作者：** GroupDocs

```csharp
editorDocx.Dispose();
editorXlsx.Dispose();
editorXls.Dispose();
editorXml.Dispose();
Console.WriteLine("ExtractingDocumentInfo routine has successfully finished");
```

## 相關教學

- [在 .NET 中使用 GroupDocs.Editor 的完整中繼資料提取指南](/editor/net/advanced-features/groupdocs-editor-net-metadata-extraction-guide/)
- [使用 GroupDocs.Editor for .NET 的文件載入教學](/editor/net/document-loading/)
- [使用 GroupDocs.Editor .NET 高效文件編輯：將 HTML 轉換為可編輯文件](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)