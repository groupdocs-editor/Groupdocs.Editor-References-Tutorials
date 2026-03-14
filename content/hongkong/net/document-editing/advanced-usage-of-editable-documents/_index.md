---
date: 2026-03-14
description: 了解如何使用 GroupDocs.Editor for .NET 從 DOCX 提取圖片、將 DOCX 轉換為 HTML，並將文件另存為
  HTML。
linktitle: Extract Images from DOCX – Advanced Editable Document Usage
second_title: GroupDocs.Editor .NET API
title: 從 DOCX 提取圖像 – 高級可編輯文件使用
type: docs
url: /zh-hant/net/document-editing/advanced-usage-of-editable-documents/
weight: 11
---

# 從 DOCX 提取圖片 – 進階可編輯文件使用

如果您是 .NET 開發人員，想要 **從 DOCX 提取圖片** 並提升文件編輯功能，GroupDocs.Editor for .NET 提供了一套強大的工具。本完整指南將帶您深入了解使用 GroupDocs.Editor 的可編輯文件進階用法，逐步說明每個步驟，讓您充分發揮其潛力。

## 快速解答
- **如何從 DOCX 檔案提取圖片？** 載入文件後使用 `EditableDocument.Images`（透過 `Editor`）。
- **我可以將 DOCX 轉換為內嵌資源的 HTML 嗎？** 可以——呼叫 `EditableDocument.GetEmbeddedHtml()` 或 `GetContent()` 取得 HTML 標記。
- **哪個方法可將編輯後的文件儲存為 HTML？** 使用 `EditableDocument.Save(htmlFilePath)` 會產生包含資源資料夾的 HTML 檔案。
- **能否從 Word 文件提取字型？** 使用 `EditableDocument.Fonts` 取得所有字型資源。
- **正式環境需要授權嗎？** 必須擁有有效的 GroupDocs.Editor 授權；亦提供免費試用。

## 什麼是 **extract images from docx**？
從 DOCX 檔案提取圖片是指以程式方式取得 Word 文件中嵌入的每張圖片，以便重新使用、修改或單獨儲存。GroupDocs.Editor 在 `EditableDocument` 實例上提供 `Images` 集合，使此工作變得簡單直觀。

## 為何在此工作流程中使用 GroupDocs.Editor？
- **完整控制** 文件資源（圖片、字型、CSS），無需手動處理 ZIP。  
- **無縫轉換** 從 DOCX 至 HTML，保持版面配置與樣式。  
- **輕鬆提取資源**，可用於自訂圖片處理、字型嵌入或 CDN 發佈。  
- **穩健的釋放模式**，確保長時間服務不會發生記憶體洩漏。

## 前置條件
- 開發機上已安裝 Visual Studio。  
- 與 GroupDocs.Editor 相容的 .NET Framework。  
- GroupDocs.Editor for .NET 程式庫。您可於此處[下載](https://releases.groupdocs.com/editor/net/)。  
- 有效的 GroupDocs.Editor 授權。您可取得[免費試用](https://releases.groupdocs.com/)或購買[臨時授權](https://purchase.groupdocs.com/temporary-license/)。

## 匯入命名空間
首先，確保在 .NET 專案中匯入必要的命名空間：

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```

## 步驟 1：建立 EditableDocument 實例
首先，您需要透過載入支援格式的輸入文件，建立 `EditableDocument` 的實例以進行編輯。

```csharp
string inputFilePath = "YourSampleDocument.docx";
Editor editor = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```

在此步驟中，我們載入輸入文件並為編輯做準備。

## 如何 **extract images from DOCX**？
以下我們將深入資源提取功能，從最常見的需求——取得 Word 檔案中所有圖片——開始說明。

## 步驟 2：提取文件資源
`EditableDocument` 包含多種可提取與操作的資源。我們將逐一說明：

### 步驟 2.1：將整個文件提取為 HTML
您可以產生一個字串，內含整個文件及其所有資源，並以 HTML 形式嵌入。

```csharp
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```

此字串會相當龐大，因為它包含以 base64 編碼的樣式表、圖片與字型。

### 步驟 2.2：提取所有圖片 *(primary keyword in action)*
從文件中提取所有圖片——這正是 **extract images from docx** 的核心。

```csharp
List<IImageResource> allImages = beforeEdit.Images;
```

### 步驟 2.3：提取所有字型 *(secondary keyword)*
如果您同時需要 **extract fonts from word**，請使用以下呼叫：

```csharp
List<FontResourceBase> allFonts = beforeEdit.Fonts;
```

### 步驟 2.4：提取所有樣式表
以文字格式提取所有樣式表。

```csharp
List<CssText> allStylesheets = beforeEdit.Css;
```

### 步驟 2.5：收集所有資源
一次呼叫即可收集所有資源。

```csharp
List<IHtmlResource> allResources = beforeEdit.AllResources;
```

包括圖片、字型與樣式表。

### 步驟 2.6：取得 HTML 標記
取得文件的 HTML 標記（不含嵌入資源）。

```csharp
string htmlMarkup = beforeEdit.GetContent();
```

## 如何使用自訂處理 **convert docx to html**？
有時您需要調整外部連結，使其指向自訂的資源處理程式。

## 步驟 3：調整外部連結
### 步驟 3.1：準備自訂前綴
準備將會加在原始外部連結前的前綴字串。

```csharp
string customImagesRequesthandlerUri = "http://example.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://example.com/CssHandler/id=";
string customFontsRequesthandlerUri = "http://example.com/FontsHandler/id=";
```

### 步驟 3.2：產生帶前綴的 HTML 標記
產生已調整連結的 HTML 標記。

```csharp
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```

### 步驟 3.3：取得僅含 Body 的 HTML 內容
某些 WYSIWYG 編輯器僅接受不含標頭的純 HTML 標記。

```csharp
string onlyBodyContent = beforeEdit.GetBodyContent();
```

### 步驟 3.4：帶前綴的僅 Body 內容
產生僅含 Body 且帶有自訂圖片前綴的內容。

```csharp
string prefixedBodyContent = beforeEdit.GetBodyContent(customImagesRequesthandlerUri);
```

### 步驟 3.5：提取樣式表
提取文件中使用的樣式表。

```csharp
List<string> stylesheets = beforeEdit.GetCssContent();
```

### 步驟 3.6：帶前綴的樣式表
以自訂前綴提取樣式表。

```csharp
List<string> prefixedStylesheets = beforeEdit.GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri);
```

## 如何正確 **save document as html**？
## 步驟 4：將文件儲存為 HTML
將編輯後的文件儲存為 HTML 檔案，並包含其資源。

```csharp
string htmlFilePath = Path.Combine("output", Path.GetFileNameWithoutExtension(inputFilePath) + ".html");
beforeEdit.Save(htmlFilePath);
```

此方法會為樣式表、圖片、字型等資源建立獨立目錄。

## 步驟 5：釋放 EditableDocument
`EditableDocument` 實作 `IDisposable`，並提供檢查實例是否已釋放的功能。

```csharp
Console.WriteLine("EditableDocument is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");
```

### 步驟 5.1 處理 Dispose 事件
您也可以訂閱 disposing 事件。

```csharp
EventHandler someMethod = delegate { Console.WriteLine("Disposing event was spotted!"); };
beforeEdit.Disposed += someMethod;
```

## 步驟 6：從 HTML 建立 EditableDocument
從 HTML 文件建立 `EditableDocument` 實例。

### 步驟 6.1：從 HTML 檔案

```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
```

### 步驟 6.2：從 HTML 標記

```csharp
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);
```

這兩個實例（`afterEditFromFile` 與 `afterEditFromMarkup`）與原始實例（`beforeEdit`）相同。

## 步驟 7：手動釋放
手動釋放您的 `EditableDocument` 實例。

```csharp
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```

確保資源得到正確清理。

## 常見問題與解決方案
- **提取後圖片未顯示：** 請確認文件確實包含嵌入圖片，且在呼叫 `Edit` 後存取 `beforeEdit.Images`。  
- **HTML 輸出缺少字型：** 請確保呼叫 `GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri)` 正確嵌入字型 URL。  
- **大型 HTML 字串導致記憶體壓力：** 使用 `GetContent()` 取得不含嵌入資源的標記，並將圖片／CSS 以獨立檔案提供。

## 常見問答

**Q: GroupDocs.Editor 支援哪些格式？**  
A: GroupDocs.Editor 支援 DOCX、XLSX、PPTX 以及許多其他常見的辦公文件格式。

**Q: 可以在沒有授權的情況下使用 GroupDocs.Editor 嗎？**  
A: 可以，您可使用[免費試用](https://releases.groupdocs.com/)或[臨時授權](https://purchase.groupdocs.com/temporary-license/)。

**Q: 如何從文件中提取特定資源？**  
A: 使用 `EditableDocument` 實例上的 `Images`、`Fonts` 與 `Css` 集合。

**Q: 能否調整 HTML 輸出的連結？**  
A: 可以，將自訂的 URI 前綴傳遞給 `GetContent` 或 `GetBodyContent` 以重新寫入圖片、CSS 與字型的連結。

**Q: 如何將編輯後的文件儲存為 HTML 檔案？**  
A: 呼叫 `EditableDocument` 實例的 `Save` 方法，並提供以 `.html` 結尾的檔案路徑。

**最後更新：** 2026-03-14  
**測試環境：** GroupDocs.Editor for .NET（最新版本）  
**作者：** GroupDocs