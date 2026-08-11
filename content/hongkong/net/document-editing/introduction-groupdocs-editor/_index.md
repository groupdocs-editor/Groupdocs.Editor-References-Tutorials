---
date: 2026-04-11
description: 學習如何使用 GroupDocs.Editor for .NET 以程式方式編輯 Word 文件，並將 Word 轉換為 RTF，這是一個詳細的逐步指南。
keywords:
- programmatically edit word document
- convert pdf to editable
- replace text in document
- convert word to rtf
- save document to stream
linktitle: 以程式方式使用 GroupDocs.Editor for .NET 編輯 Word 文件
second_title: GroupDocs.Editor .NET API
title: 使用 GroupDocs.Editor for .NET 程式化編輯 Word 文件
type: docs
url: /zh-hant/net/document-editing/introduction-groupdocs-editor/
weight: 12
---

# 以程式方式編輯 Word 文件（使用 GroupDocs.Editor for .NET）

如果你是一位需要 **以程式方式編輯 Word 文件** 的 .NET 開發人員——無論是取代文字、轉換格式，或將結果嵌入串流——GroupDocs.Editor for .NET 是一個功能強大、易於使用的函式庫，能完成這項工作。在本教學中，我們將示範一個實務範例，涵蓋載入 DOCX 檔案、編輯內容、將結果轉換為 RTF，並儲存至磁碟或記憶體串流。

## 快速答覆
- **我可以編輯什麼？** Word、PDF、HTML、RTF 以及其他多種格式。  
- **我可以取代文字嗎？** 是 — 使用簡單的字串取代或更進階的 DOM 操作。  
- **如何將 PDF 轉換為可編輯的？** 使用 `Editor` 載入 PDF，並編輯產生的 HTML。  
- **將檔案儲存至串流的最簡單方法是什麼？** 使用 `editor.Save(editableDoc, stream, options)`。  
- **我需要授權嗎？** 在正式環境中需要臨時或完整授權。

## 什麼是以程式方式編輯 Word 文件？
以程式方式編輯 Word 文件是指使用程式碼—而非使用者介面—來開啟檔案、變更其內容（文字、圖片、樣式），並將修改後的版本寫回儲存空間。此方式可支援自動化報告、大量文件更新以及自訂內容產生。

## 為什麼使用 GroupDocs.Editor for .NET？
- **格式彈性：** 載入 DOCX、PDF、HTML、RTF 等，並儲存為任何支援的格式。  
- **無需 Office 依賴：** 在伺服器上不需安裝 Microsoft Office 即可運作。  
- **支援串流：** 適用於雲端情境，您可以從串流讀寫，而非檔案系統。  
- **功能豐富的 API：** 可存取圖片、字型、CSS 及其他資源，以實現完整功能的編輯。

## 前置條件
在開始實作之前，請確保您已具備以下條件：

- Visual Studio 2017 或更新版本。  
- .NET Framework 4.6.1 或更新版本。  
- GroupDocs.Editor for .NET – 您可以從網站[下載](https://releases.groupdocs.com/editor/net/)。  
- 有效的授權或來自 GroupDocs 的[臨時授權](https://purchase.groupdocs.com/temporary-license/)。

## 匯入命名空間
要開始使用 GroupDocs.Editor for .NET，請匯入所需的命名空間：

```csharp
using System;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```

在以下各節中，我們會將工作流程拆解成小步驟，讓您輕鬆跟隨。

## 步驟 1：取得輸入檔案的路徑
指定您想編輯的 Word 檔案位置。此範例假設有一個名為 **Your Sample Document.docx** 的 DOCX 檔案。

```csharp
string inputFilePath = "Your Sample Document.docx";
```

## 步驟 2：實例化 Editor 物件
透過傳入輸入路徑建立 `Editor` 實例。此操作會載入文件並為編輯做準備。

```csharp
using (GroupDocs.Editor.Editor editor = new Editor(inputFilePath))
{
    // Subsequent steps will be nested inside this block
}
```

## 步驟 3：開啟文件以供編輯
取得 `EditableDocument`，以取得文件的 HTML 表示形式及其資源。

```csharp
EditableDocument beforeEdit = editor.Edit();
```

## 步驟 4：取得文件內容與資源
您可以提取原始 HTML、圖片、字型與 CSS。當需要直接操作標記時，此功能相當有用。

```csharp
string content = beforeEdit.GetContent();
var images = beforeEdit.Images;
var fonts = beforeEdit.Fonts;
var stylesheets = beforeEdit.Css;
```

### 步驟 4.1：以單一 Base64 編碼字串取得文件
如果您偏好單一字串包含所有嵌入資源，請呼叫 `GetEmbeddedHtml()`。

```csharp
string allEmbeddedInsideString = beforeEdit.GetEmbeddedHtml();
```

### 步驟 4.2：編輯內容
讓我們將 **Subtitle** 替換為 **Edited subtitle**，示範簡單的文字取代。

```csharp
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
```

## 步驟 5：建立新的 EditableDocument 實例
編輯完標記後，將其重新包裝成 `EditableDocument` 物件。

```csharp
EditableDocument afterEdit = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```

## 步驟 6：儲存已編輯的文件
我們將結果儲存為 RTF 檔案，示範檔案系統路徑與記憶體串流兩種方式。

### 步驟 6.1：準備輸出路徑
定義 RTF 應寫入的位置。

```csharp
string outputPath = Path.Combine("Output Directory Path", Path.GetFileNameWithoutExtension(inputFilePath) + ".rtf");
```

### 步驟 6.2：準備儲存選項
透過 `WordProcessingSaveOptions` 選擇 RTF 格式。

```csharp
Options.WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
```

### 步驟 6.3：儲存至路徑
將已編輯的文件寫入檔案系統。

```csharp
editor.Save(afterEdit, outputPath, saveOptions);
```

### 步驟 6.4：儲存至串流
如果需要將結果保留在記憶體中（例如上傳至雲端儲存），請使用 `MemoryStream`。

```csharp
using (MemoryStream ms = new MemoryStream())
{
    editor.Save(afterEdit, ms, saveOptions);
}
```

## 步驟 7：釋放 Editor 與 EditableDocument 實例
及時釋放資源，以避免記憶體洩漏。

```csharp
beforeEdit.Dispose();
afterEdit.Dispose();
editor.Dispose();
```

## 常見使用情境與技巧
- **將 PDF 轉換為可編輯：** 使用 `Editor` 載入 PDF，編輯產生的 HTML，然後儲存回 PDF 或其他格式。  
- **在文件中取代文字：** 在簡單情況下使用 `string.Replace`，在複雜情況下操作 DOM。  
- **將 Word 轉換為 RTF：** 如上所示，在儲存選項中設定 `WordProcessingFormats.Rtf`。  
- **將文件儲存至串流：** 適用於直接將檔案回傳給客戶端的 Web API。  
- **載入文件以供編輯：** 請始終將 `Editor` 包於 `using` 區塊中，以確保正確釋放。

## 常見問題

**問：我可以使用 GroupDocs.Editor for .NET 編輯 PDF 檔案嗎？**  
答：可以，GroupDocs.Editor 透過將 PDF 轉換為中介的 HTML 表示形式來支援編輯。

**問：如何取得 GroupDocs.Editor for .NET 的臨時授權？**  
答：您可從[GroupDocs 網站](https://purchase.groupdocs.com/temporary-license/)取得臨時授權。

**問：GroupDocs.Editor for .NET 支援哪些檔案格式？**  
答：支援 DOCX、PDF、HTML、RTF 以及其他多種格式。

**問：是否可以將 GroupDocs.Editor 與雲端儲存整合？**  
答：當然可以——您可以從 Azure Blob、Amazon S3、Google Cloud Storage 等讀寫串流。

**問：在哪裡可以找到 GroupDocs.Editor for .NET 的文件說明？**  
答：文件說明可在[此處](https://tutorials.groupdocs.com/editor/net/)取得。

---

**最後更新：** 2026-04-11  
**測試環境：** GroupDocs.Editor 23.12 for .NET  
**作者：** GroupDocs