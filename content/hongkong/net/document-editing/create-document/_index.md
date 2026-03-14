---
date: 2026-03-14
description: 了解如何使用 GroupDocs.Editor for .NET 編輯 PowerPoint 簡報及其他文件類型。指南亦說明如何儲存已編輯的文件以及在
  .NET 中編輯 Word 文件。
linktitle: Create Document
second_title: GroupDocs.Editor .NET API
title: 使用 GroupDocs.Editor for .NET 編輯 PowerPoint 簡報
type: docs
url: /zh-hant/net/document-editing/create-document/
weight: 10
---

 block placeholders unchanged.

Also note the note about "For Traditional Chinese (Hong Kong), ensure proper RTL formatting if needed" but Chinese is LTR, not needed.

Now produce final content.# 使用 GroupDocs.Editor for .NET 編輯 PowerPoint 簡報

## 簡介
如果您正在尋找一種可靠的方式以程式方式 **編輯 PowerPoint 簡報** 檔案，GroupDocs.Editor for .NET 就是答案。此函式庫讓您能夠使用單一、易於使用的 API 處理 Word、Excel、PowerPoint、電子書與 Email 格式。於本教學中，我們將逐步示範如何建立與編輯每種支援的文件類型，說明如何 **儲存已編輯的文件** 串流，並提供可在實際專案中套用的實用技巧。

## 快速解答
- **哪個函式庫可以在 .NET 中編輯 PowerPoint 檔案？** GroupDocs.Editor for .NET.  
- **我可以使用相同的 API 編輯 Word、Excel 與 Epub 檔案嗎？** 可以，相同的 `Editor` 類別支援所有這些格式。  
- **如何取得已編輯的檔案？** 提供一個回呼函式（例如 `SaveNewDocument`），它會接收結果串流。  
- **正式環境使用是否需要授權？** 需要——購買授權或使用臨時試用授權。  
- **支援哪些 .NET 版本？** .NET Framework 4.0 以上、.NET Core 以及 .NET 5/6.

## 什麼是使用 GroupDocs.Editor 進行 “編輯 PowerPoint 簡報”？
編輯 PowerPoint 簡報即是載入 `.pptx` 檔案，套用變更（例如修改投影片、文字或隱藏元素），然後取得更新後的檔案——全部不需要安裝 Microsoft Office。

## 為什麼要使用 GroupDocs.Editor for .NET？
- **單一 API 支援多種格式** – 無需為 Word、Excel 或 Epub 切換不同函式庫。  
- **無 Office 依賴** – 可在伺服器、容器及 CI 流程中運作。  
- **細緻的控制** – 可自訂分頁、語言資訊、字型抽取等。  
- **基於串流的處理** – 適用於雲端服務，您可使用記憶體串流而非實體檔案。

## 先決條件
- Visual Studio（任何近期版本）。  
- .NET Framework 4.0 或以上（或 .NET Core/.NET 5+）。  
- GroupDocs.Editor for .NET 函式庫 – 從 [here](https://releases.groupdocs.com/editor/net/) 下載。  
- 基本的 C# 知識。

## 匯入命名空間
首先，匯入包含我們將使用的核心類別的命名空間。

```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using System.IO;
```

## 步驟 1：設定串流
我們將使用記憶體串流作為文件內容的佔位符。

```csharp
Stream memoryStream = Stream.Null;
```

## 步驟 2：回呼函式以 **儲存已編輯的文件**
定義一個回呼函式，接收已編輯的串流並將其儲存至 `memoryStream`。

```csharp
void SaveNewDocument(Stream resultStream)
{
    memoryStream = resultStream;
}
```

## 步驟 3：建立與編輯 WordProcessing 文件  
（此處我們 **編輯 word document .net**。）

### 使用預設選項建立與編輯
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    EditableDocument defaultWordProcessingDoc = editor.Edit();
}
```

### 使用自訂選項建立與編輯
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

## 步驟 4：建立與編輯 Spreadsheet 文件  
（使用此方式 **編輯 excel file .net**。）

### 使用預設選項建立與編輯
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    EditableDocument defaultEditableSpreadsheetDocument = editor.Edit();
}
```

### 使用自訂選項建立與編輯
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

## 步驟 5：**編輯 PowerPoint 簡報** – 建立與編輯 Presentation 文件
這是我們主要關鍵字焦點的核心。

### 使用預設選項建立與編輯
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    EditableDocument defaultEditablePresentationDocument = editor.Edit();
}
```

### 使用自訂選項建立與編輯
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

## 步驟 6：建立與編輯 Ebook 文件  
（此處我們 **編輯 epub file**。）

### 使用預設選項建立與編輯
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EditableDocument defaultEditableEbookDocument = editor.Edit();
}
```

### 使用自訂選項建立與編輯
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
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EditableDocument defaultEditableEmailDocument = editor.Edit();
}
```

### 使用自訂選項建立與編輯
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
完成後釋放串流以釋放資源。

```csharp
memoryStream.Dispose();
System.Console.WriteLine("CreateDocument routine has successfully finished");
```

## 常見陷阱與技巧
- **千萬別忘記釋放串流** – 若保持開啟會導致長時間服務的記憶體泄漏。  
- **編輯 PowerPoint 時，請確保正確設定 `SlideNumber`**；否則第一張投影片可能會被重複。  
- **如果需要保留原始檔名**，請在回呼之前儲存，編輯完成後再重新命名輸出串流。  
- **針對大型文件**，建議分塊處理或使用帶暫存檔的 `Editor`，以避免高記憶體使用量。

## 常見問答

**Q: 使用 GroupDocs.Editor for .NET 可以編輯哪些類型的文件？**  
A: 您可以編輯 WordProcessing、試算表、簡報、電子書與 Email——包括用於 **編輯 PowerPoint 簡報** 的 PowerPoint 檔案。

**Q: 可以自訂編輯選項嗎？**  
A: 可以，每種格式都有自己的選項類別（例如 `WordProcessingEditOptions`、`SpreadsheetEditOptions`、`PresentationEditOptions`），讓您細部調整分頁、隱藏投影片、工作表選取等。

**Q: 如何處理已編輯文件的輸出？**  
A: 使用回呼函式（`SaveNewDocument`）取得已編輯的串流，之後您可以寫入磁碟、資料庫，或從 Web API 回傳。

**Q: 使用 GroupDocs.Editor for .NET 是否需要授權？**  
A: 是，正式環境必須取得授權。您可從 [here](https://purchase.groupdocs.com/buy) 取得授權，也提供臨時試用授權。

**Q: 在哪裡可以找到更詳細的文件說明？**  
A: 詳細文件說明可於 [GroupDocs.Editor for .NET documentation page](https://tutorials.groupdocs.com/editor/net/) 取得。

## 結論
GroupDocs.Editor for .NET 讓 **編輯 PowerPoint 簡報** 檔案以及各種其他文件類型變得簡單。依照上述步驟，您即可在程式碼中完整建立、修改與 **儲存已編輯的文件** 串流，無需依賴 Office 安裝。探索函式庫的進階選項，以符合您的特定業務需求。

---

**最後更新：** 2026-03-14  
**測試環境：** GroupDocs.Editor for .NET（最新版本）  
**作者：** GroupDocs