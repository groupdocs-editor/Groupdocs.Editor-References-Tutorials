---
date: 2026-09-21
description: 了解如何使用 GroupDocs.Editor for .NET 在無需 Office 的情況下編輯 PowerPoint，並編輯 Word、Excel、EPUB
  以及擷取編輯後的文件串流。
keywords:
- edit powerpoint without office
- GroupDocs.Editor .NET
- document editing .NET
- edit presentation programmatically
lastmod: 2026-09-21
linktitle: 建立文件
og_description: 使用 GroupDocs.Editor for .NET 在無需 Office 的情況下編輯 PowerPoint。本指南說明如何修改簡報、Word、Excel、EPUB，並儲存編輯後的文件串流。
og_image_alt: Guide showing code to edit PowerPoint presentations without Microsoft
  Office using GroupDocs.Editor for .NET
og_title: 使用 GroupDocs.Editor for .NET 編輯 PowerPoint（無需 Office）
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
title: 使用 GroupDocs.Editor for .NET 編輯 PowerPoint（無需 Office）
type: docs
url: /zh-hant/net/document-editing/create-document/
weight: 10
---

# 使用 GroupDocs.Editor for .NET 編輯 PowerPoint（無需 Office）

## 簡介
如果您正在尋找一種可靠的方式以程式方式 **編輯 PowerPoint（無需 Office）**，GroupDocs.Editor for .NET 就是答案。此函式庫讓您透過單一、易於使用的 API 處理 Word、Excel、PowerPoint、Ebook 以及 Email 格式。於本教學中，我們將示範如何建立與編輯每種支援的文件類型，說明如何 **儲存已編輯的文件** 串流，並提供可在實際專案中應用的實用技巧。

## 快速解答
- **什麼函式庫可以讓我在 .NET 中編輯 PowerPoint 檔案？** GroupDocs.Editor for .NET.  
- **我可以使用相同的 API 編輯 Word、Excel 與 Epub 檔案嗎？** 可以，相同的 `Editor` 類別支援所有這些格式。  
- **我要如何取得已編輯的檔案？** 提供一個回呼函式（例如 `SaveNewDocument`），它會接收結果串流。  
- **在正式環境使用是否需要授權？** 需要 — 可購買授權或使用臨時試用授權。  
- **支援哪些 .NET 版本？** .NET Framework 4.0+、.NET Core 與 .NET 5/6。

## 何謂無需 Office 編輯 PowerPoint？
在無需 Office 的情況下編輯 PowerPoint 簡報，指的是載入 `.pptx` 檔案、套用變更（例如修改投影片、文字或隱藏元素），然後取得更新後的檔案——整個過程不需要在伺服器上安裝 Microsoft PowerPoint。

## 為何使用 GroupDocs.Editor for .NET？
GroupDocs.Editor 支援 **5 種以上的主要文件類型**（Word、Excel、PowerPoint、EPUB、Email），且可處理高達 **500 MB** 的檔案，同時因為採用串流架構，使記憶體使用量維持在 **100 MB** 以下。此函式庫可在 **Windows、Linux 與 macOS** 上執行，十分適合雲端原生服務、CI 流程以及容器化工作負載。

## 前置條件
- Visual Studio（任何近期版本）。  
- .NET Framework 4.0 或更新版本（或 .NET Core/.NET 5+）。  
- GroupDocs.Editor for .NET 函式庫 – [download the GroupDocs.Editor for .NET library](https://releases.groupdocs.com/editor/net/)。  
- 基本的 C# 知識。

## 匯入命名空間
`Editor` 類別位於 `GroupDocs.Editor` 命名空間，而特定格式的選項類別則位於各自的子命名空間中。

`Editor` 是核心類別，負責載入文件、提供可編輯的表示，並將修改後的內容寫回串流。  

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

## 步驟 1：設定串流
使用串流可讓整個工作流程保持在記憶體中，非常適合 Web API 或無伺服器函式。

`MemoryStream` 是輕量且可擴充的緩衝區，模擬磁碟上的檔案但實際儲存在 RAM 中。  

```csharp
byte[] fileBytes = File.ReadAllBytes("sample.pptx");
var inputStream = new MemoryStream(fileBytes);
```

```csharp
Stream memoryStream = Stream.Null;
```

## 步驟 2：回呼函式以 **儲存已編輯的文件**
回呼函式會在 `Editor` 完成處理後接收已編輯的串流。之後您可以將其寫入磁碟、資料庫，或從 API 端點回傳。

`SaveNewDocument` 是使用者自訂的方法，SDK 會在編輯完成後自動呼叫它。  

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

## 步驟 3：建立與編輯文字處理文件  
（此處 **編輯 .NET 的 Word 文件**。）

### 使用預設選項建立與編輯
`WordProcessingEditOptions` 類別為 DOCX 檔案提供合理的預設值。

`WordProcessingEditOptions` 定義編輯器如何處理分頁、變更追蹤與嵌入物件。  

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

### 使用自訂選項建立與編輯
您可以開啟或關閉特定功能，例如拼寫檢查或變更追蹤。

`WordProcessingEditOptions` 允許您啟用 `EnableTrackChanges` 以進行稽核追蹤。  

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

## 步驟 4：建立與編輯試算表文件  
（用於 **編輯 .NET 的 Excel 檔案**。）

### 使用預設選項建立與編輯
`SpreadsheetEditOptions` 控制載入哪個工作表以及是否評估公式。

`SpreadsheetEditOptions` 預設選擇第一個工作表。  

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

### 使用自訂選項建立與編輯
您可以指定不同的工作表索引，或為提升效能停用公式評估。

`SpreadsheetEditOptions` 讓您設定 `WorksheetIndex` 與 `EnableFormulaEvaluation`。  

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

## 步驟 5：無需 Office 編輯 PowerPoint – 建立與編輯簡報文件
這是我們主要關鍵字焦點的核心。

### 使用預設選項建立與編輯
`PresentationEditOptions` 決定是否包含隱藏投影片，以及哪一張投影片為預設編輯目標。

`PresentationEditOptions` 預設包含隱藏投影片，您可以切換此設定。  

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

### 使用自訂選項建立與編輯
您可以變更 `SlideNumber` 以編輯特定投影片，或停用包含備註頁面的功能。

`PresentationEditOptions` 讓您設定 `SlideNumber` 與 `IncludeNotes`。  

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

## 步驟 6：建立與編輯電子書文件  
（此處 **編輯 epub 檔案**。）

### 使用預設選項建立與編輯
`EbookEditOptions` 處理 EPUB 與其內部 HTML 表示之間的轉換。

`EbookEditOptions` 使用預設的 HTML 渲染器來呈現 EPUB 內容。  

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

### 使用自訂選項建立與編輯
您可以保留原始 CSS，或強制使用純文字版面配置。

`EbookEditOptions` 提供 `PreserveCss` 與 `PlainTextOnly` 旗標。  

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

## 步驟 7：建立與編輯 Email 文件

### 使用預設選項建立與編輯
`EmailEditOptions` 讓您操作 .eml 檔案的內容、主旨與附件。

`EmailEditOptions` 以純文字載入 Email 內容，以便簡單取代。  

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

### 使用自訂選項建立與編輯
您可以保留原始 MIME 標頭，或將其移除以取得純文字版本。

`EmailEditOptions` 包含 `KeepHeaders`，可保留或捨棄 MIME 中繼資料。  

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

## 步驟 8：完成流程
完成後請釋放串流以釋放資源。正確的釋放可防止長時間執行的服務（如 Web API 或背景工作者）發生記憶體洩漏。  

```csharp
inputStream.Dispose();
```

```csharp
memoryStream.Dispose();
System.Console.WriteLine("CreateDocument routine has successfully finished");
```

## 常見陷阱與技巧
- **千萬別忘記釋放串流** — 若保持開啟狀態，長時間執行的服務可能會發生記憶體洩漏。  
- **編輯 PowerPoint 時，請確保正確設定 `SlideNumber`**；否則第一張投影片可能會被重複。  
- **若需保留原始檔名**，請在回呼之前儲存，編輯完成後再重新命名輸出串流。  
- **針對大型文件**，建議分塊處理或使用 `Editor` 搭配暫存檔，以避免高記憶體消耗。  
- **透過 `EditorOptions` 啟用日誌**，若需在正式環境除錯意外行為。

## 常見問答

**Q: 我可以使用 GroupDocs.Editor for .NET 編輯哪些類型的文件？**  
A: 您可以編輯 WordProcessing、試算表、簡報、電子書與 Email——包括用於 **無需 Office 編輯 PowerPoint** 的情境的 PowerPoint 檔案。

**Q: 是否可以自訂編輯選項？**  
A: 可以，每種格式都有自己的選項類別（例如 `WordProcessingEditOptions`、`SpreadsheetEditOptions`、`PresentationEditOptions`），讓您微調分頁、隱藏投影片、工作表選擇等設定。

**Q: 我該如何處理已編輯文件的輸出？**  
A: 使用回呼函式（`SaveNewDocument`）取得已編輯的串流，之後您可以將其寫入磁碟、資料庫，或從 Web API 回傳。

**Q: 使用 GroupDocs.Editor for .NET 是否需要授權？**  
A: 需要，正式環境必須取得授權。您可從 [GroupDocs.Editor purchase page](https://purchase.groupdocs.com/buy) 取得授權，亦提供臨時試用授權。

**Q: 我在哪裡可以找到更詳細的文件說明？**  
A: 詳細文件說明可於 [GroupDocs.Editor for .NET documentation page](https://tutorials.groupdocs.com/editor/net/) 取得。

## 結論
GroupDocs.Editor for .NET 讓 **無需 Office 編輯 PowerPoint** 檔案以及各種其他文件類型變得相當簡單。依循上述步驟，您即可在程式碼中完整建立、修改並 **儲存已編輯的文件** 串流，而不需依賴 Office 安裝。探索函式庫的進階選項，以符合您的特定業務需求。

---

**最後更新：** 2026-09-21  
**測試環境：** GroupDocs.Editor for .NET (latest release)  
**作者：** GroupDocs

- [GroupDocs.Editor .NET 簡報文件編輯教學](/editor/net/presentation-documents/)
- [使用 GroupDocs.Editor .NET 建立可編輯文件](/editor/net/document-editing/groupdocs-editor-net-edit-manage-documents-guide/)
- [在 .NET 中使用 GroupDocs.Editor 載入文件（無需選項）— 完整指南](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)