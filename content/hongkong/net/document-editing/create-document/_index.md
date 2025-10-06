---
title: 建立文檔
linktitle: 建立文檔
second_title: GroupDocs.Editor .NET API
description: 透過這個全面的逐步教學，了解如何使用 GroupDocs.Editor for .NET 編輯 Word、Excel、PowerPoint、電子書和電子郵件文件。
weight: 10
url: /zh-hant/net/document-editing/create-document/
type: docs
---
# 建立文檔

## 介紹
您是否厭倦了以程式設計方式編輯不同文件類型帶來的麻煩？ GroupDocs.Editor for .NET 的角色是簡化流程。這個強大的工具允許開發人員輕鬆編輯各種文件格式，例如 Word、Excel、PowerPoint、電子書和電子郵件。在本教學中，我們將深入探討如何使用 GroupDocs.Editor for .NET 建立和編輯文件。我們將把這個過程分解為易於遵循的步驟，即使您是新手也可以輕鬆完成。
## 先決條件
在我們開始之前，請確保您具備以下條件：
- Visual Studio 安裝在您的電腦上。
- .NET Framework（4.0 或更高版本）。
-  .NET 函式庫的 GroupDocs.Editor。您可以從以下位置下載：[這裡](https://releases.groupdocs.com/editor/net/).
- C# 程式設計基礎知識。
## 導入命名空間
首先，讓我們導入必要的名稱空間。這將使我們的應用程式可以存取所需的類別和方法。
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using System.IO;
```
## 第 1 步：設定流
首先，我們需要設定一個記憶體流來充當文件內容的佔位符。
```csharp
Stream memoryStream = Stream.Null;
```
## 步驟2：儲存文件的回調函數
接下來，定義一個回呼函數來儲存新的文檔流。此功能對於處理文件編輯過程的輸出至關重要。
```csharp
void SaveNewDocument(Stream resultStream)
{
    memoryStream = resultStream;
}
```
## 步驟 3：建立和編輯字處理文檔
現在，讓我們建立並編輯一個 Word 文件。我們將從創建一個新的`Editor`WordProcessing 文件的實例並使用預設選項對其進行編輯。
### 使用預設選項建立和編輯
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    EditableDocument defaultWordProcessingDoc = editor.Edit();
}
```
### 使用自訂選項建立和編輯
為了進行更多控制，我們可以指定禁用分頁和提取嵌入字體等選項。
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
## 步驟 4：建立和編輯電子表格文檔
同樣，我們可以建立和編輯Excel文檔。操作方法如下。
### 使用預設選項建立和編輯
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    EditableDocument defaultEditableSpreadsheetDocument = editor.Edit();
}
```
### 使用自訂選項建立和編輯
要定位特定工作表或排除隱藏的工作表，我們使用`SpreadsheetEditOptions`.
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
## 步驟 5：建立和編輯簡報文檔
也支援 PowerPoint 簡報。讓我們看看如何處理它們。
### 使用預設選項建立和編輯
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    EditableDocument defaultEditablePresentationDocument = editor.Edit();
}
```
### 使用自訂選項建立和編輯
您可以透過指定選項（例如顯示哪張投影片以及是否包含隱藏投影片）來自訂編輯。
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
## 步驟 6：建立和編輯電子書文檔
GroupDocs.Editor 也允許編輯 EPUB 等電子書格式。以下是您可以處理的方法。
### 使用預設選項建立和編輯
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EditableDocument defaultEditableEbookDocument = editor.Edit();
}
```
### 使用自訂選項建立和編輯
透過啟用或停用分頁和語言資訊來自訂您的電子書編輯。
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
## 步驟 7：建立和編輯電子郵件文檔
最後，我們將了解如何編輯電子郵件文件。這包括 EML 等格式。
### 使用預設選項建立和編輯
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EditableDocument defaultEditableEmailDocument = editor.Edit();
}
```
### 使用自訂選項建立和編輯
指定郵件訊息輸出選項以控制編輯過程。
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
## 第 8 步：完成流程
編輯文件後，正確處理記憶體流以釋放資源至關重要。
```csharp
memoryStream.Dispose();
System.Console.WriteLine("CreateDocument routine has successfully finished");
```
## 結論
GroupDocs.Editor for .NET 是一個多功能且功能強大的工具，可以簡化以程式設計方式編輯各種文件類型的任務。透過遵循此逐步指南，您可以輕鬆建立和編輯文檔，無論它們是字處理文件、電子表格、簡報、電子書還是電子郵件。深入研究 GroupDocs.Editor 文件以取得更多進階功能和自訂選項。
## 常見問題解答
### 我可以使用 GroupDocs.Editor for .NET 編輯哪些類型的文件？
您可以編輯各種文檔，包括文字處理、電子表格、簡報、電子書和電子郵件。
### 是否可以自訂編輯選項？
是的，GroupDocs.Editor for .NET 允許透過特定於每種文件類型的各種編輯選項進行廣泛的自訂。
### 如何處理編輯文檔的輸出？
您可以使用回呼函數將編輯後的文件流儲存到您所需的位置。
### 我需要許可證才能使用 GroupDocs.Editor for .NET 嗎？
是的，您可以從以下位置取得許可證[這裡](https://purchase.groupdocs.com/buy)。還有一個臨時許可證的選項。
### 在哪裡可以找到更詳細的文件？
詳細文件可在[.NET 文件頁面的 GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/).