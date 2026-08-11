---
date: '2026-04-11'
description: 學習如何使用 GroupDocs.Editor for .NET 建立可編輯文件，並高效地將文件另存為 HTML。
keywords:
- create editable document
- extract images from document
- save document as html
title: 使用 GroupDocs.Editor .NET 建立可編輯文件
type: docs
url: /zh-hant/net/document-editing/groupdocs-editor-net-edit-manage-documents-guide/
weight: 1
---

# 使用 GroupDocs.Editor .NET 建立可編輯文件

在當今的數位時代，**建立可編輯文件**是任何現代工作流程的核心需求。無論您是構建協作編輯器、內容管理系統，或是自動化報告工具，程式化編輯與儲存 HTML 檔案的能力都能節省大量時間。本教學將示範如何使用 GroupDocs.Editor for .NET **建立可編輯文件**實例、抽取資源，以及 **將文件儲存為 HTML**。

## 快速解答
- **什麼是「create editable document」？** 這表示將來源檔案載入至 GroupDocs.Editor 的 `EditableDocument` 物件，您可以以程式方式修改它。  
- **哪些格式可以轉換為 HTML？** 支援 Word、Excel、PowerPoint 以及其他多種 Office 格式。  
- **如何從文件中抽取圖片？** 使用 `EditableDocument.Images` 集合。  
- **我可以產生包含所有資源的單一 HTML 字串嗎？** 可以——呼叫 `GetEmbeddedHtml()`。  
- **正式環境需要授權嗎？** 試用版可用於評估；商業使用需購買永久授權。

## 「create editable document」是什麼？
建立可編輯文件表示將來源檔案（例如 .docx）載入至 GroupDocs.Editor，並回傳一個 `EditableDocument` 物件。此物件會公開文件的 HTML 標記、圖片、字型與 CSS，讓您能編輯內容、取代資源，或將整個文件嵌入網頁中。

## 為何在此任務使用 GroupDocs.Editor .NET？
- **功能完整的 API** – 支援 Word、Excel、PowerPoint 等多種格式。  
- **資源抽取** – 透過簡單屬性取得圖片、字型與樣式表。  
- **嵌入式 HTML 產生** – 產生包含所有資源的單一 HTML 字串，適合用於電子郵件或單頁應用程式。  
- **效能導向** – 及時釋放物件，必要時使用非同步模式。

## 前置條件
在實作 GroupDocs.Editor .NET 功能之前，請確保：
- **.NET 環境**：為 .NET 應用程式設定開發環境。  
- **函式庫與相依性**：
  - 使用以下任一方式安裝 GroupDocs.Editor：
    - **.NET CLI**
      ```bash
      dotnet add package GroupDocs.Editor
      ```
    - **Package Manager**
      ```powershell
      Install-Package GroupDocs.Editor
      ```
    - **NuGet 套件管理員 UI**：搜尋並安裝最新版本。  
- **知識前提**：建議熟悉 C# 程式設計與基本文件處理概念。

## 設定 GroupDocs.Editor for .NET
### 安裝說明
首先，在您的專案中設定 GroupDocs.Editor：
1. **透過 .NET CLI 安裝**：
   ```bash
   dotnet add package GroupDocs.Editor
   ```
2. **使用套件管理員**：
   - 開啟套件管理員主控台並執行：
     ```powershell
     Install-Package GroupDocs.Editor
     ```
3. **NuGet 套件管理員 UI**： 
   - 前往 NuGet，搜尋「GroupDocs.Editor」並安裝。

### 取得授權
- **免費試用與臨時授權**：  
  先從 [GroupDocs releases](https://releases.groupdocs.com/editor/net/) 下載免費試用版。若需延長測試，可於 [purchase page](https://purchase.groupdocs.com/temporary-license) 申請臨時授權。

### 基本初始化與設定
以下示範如何在應用程式中初始化 GroupDocs.Editor：
```csharp
using System;
using GroupDocs.Editor;

string inputFilePath = "YOUR_DOCUMENT_DIRECTORY"; // Replace with your actual document path
Editor editor = new Editor(inputFilePath, new WordProcessingLoadOptions());
```

## 如何使用 GroupDocs.Editor .NET 建立可編輯文件
### 建立 EditableDocument 實例
**概覽**：透過建立 `EditableDocument` 實例來載入與編輯文件。

#### 載入文件
```csharp
using GroupDocs.Editor.Options;

// Load your document with appropriate options
Editor editor = new Editor(inputFilePath, new WordProcessingLoadOptions());

// Create EditableDocument from the loaded file
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```

## 如何產生嵌入式 HTML
### 從 EditableDocument 產生嵌入式 HTML
**概覽**：將整個文件轉換為包含樣式表與資源的單一嵌入式 HTML 字串。
```csharp
using System.Collections.Generic;
using GroupDocs.Editor.HtmlCss.Resources;

// Generate embedded HTML
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```

## 如何從文件中抽取圖片
### 從 EditableDocument 抽取資源
**概覽**：從文件中取得圖片、字型、CSS 以及其他資源。
```csharp
List<IImageResource> allImages = beforeEdit.Images;
List<FontResourceBase> allFonts = beforeEdit.Fonts;
List<CssText> allStylesheets = beforeEdit.Css;
List<IHtmlResource> allResources = beforeEdit.AllResources;
```

## 如何從文件中抽取字型
*上述相同的程式碼區塊也示範了如何透過 `beforeEdit.Fonts` 取得字型資源。*

## 如何取得純 HTML 內容
### 從 EditableDocument 取得 HTML 內容
**概覽**：抽取不含嵌入資源的純 HTML 內容。
```csharp
string htmlMarkup = beforeEdit.GetContent();
```

## 如何調整 HTML 內容中的外部連結
### 調整 HTML 內容中的外部連結
**概覽**：使用自訂前綴調整圖片、CSS 與字型的外部連結。
```csharp
using System.Collections.Generic;

// Define custom handlers for resource URLs
string customImagesRequesthandlerUri = "http://example.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://example.com/CssHandler/id=";

// Adjust HTML content with prefixed links
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```

## 如何將文件儲存為 HTML
### 將 EditableDocument 儲存為 HTML 檔案
**概覽**：將編輯後的文件以 HTML 格式儲存回磁碟。
```csharp
using System.IO;

string htmlFilePath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "document.html"); // Adjust the output path
beforeEdit.Save(htmlFilePath);
```

## 釋放與事件處理（EditableDocument）
**概覽**：管理資源釋放並處理與文件生命週期相關的事件。
```csharp
Console.WriteLine("beforeEdit variable of EditableDocument type is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");

// Subscribe to the disposing event
EventHandler someMethod = delegate {
    Console.WriteLine("Disposing event was spotted!");
};
beforeEdit.Disposed += someMethod;
```

## 如何從 HTML 內容建立可編輯文件
### 從 HTML 內容建立 EditableDocument
**概覽**：從現有的 HTML 內容重建 `EditableDocument` 實例。
```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);

// Dispose resources once done
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```

## 實務應用
GroupDocs.Editor .NET 可在眾多實務情境中發揮效用：
- **協作編輯**：讓多位使用者無縫編輯文件。  
- **網路發佈**：將文件轉換為適合線上瀏覽與互動的網頁格式。  
- **內容管理系統**：與 CMS 平台整合，實現動態內容更新。  
- **自動化報告產生**：自動從各種資料來源產生與格式化報告。

## 效能考量
為了最佳化 GroupDocs.Editor .NET 的效能：
- 及時釋放物件以有效管理記憶體。  
- 透過優化檔案路徑與 URL 減少資源載入時間。  
- 在適用情況下使用非同步處理，以提升應用程式回應性。

## 常見問題與解決方案
- **大型檔案導致高記憶體使用** – 在完成處理後立即釋放 `EditableDocument` 物件。  
- **轉換後圖片連結失效** – 呼叫 `GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri)` 時，確保使用正確的資源處理程式 URI。  
- **產生的 HTML 缺少字型** – 確認來源文件已嵌入所需字型，或確保伺服器上有相應字型可供使用。

## 常見問答
**Q: GroupDocs.Editor .NET 是否相容所有文件格式？**  
A: GroupDocs.Editor 支援廣泛的格式，包括 Word、Excel、PowerPoint 以及其他許多格式，讓您在不同使用情境中具備彈性。

**Q: 如何有效處理大型檔案？**  
A: 在可用時使用非同步 API，盡可能分塊處理檔案，並始終即時釋放 `EditableDocument` 與 `Editor` 物件以釋放記憶體。

**Q: 能否將 GroupDocs.Editor 與雲端儲存解決方案整合？**  
A: 可以，您只需將檔案串流傳入 `Editor` 建構函式，即可連接 Azure Blob Storage、Amazon S3、Google Cloud Storage 或其他雲端服務提供者。

**Q: GroupDocs.Editor 的授權選項有哪些？**  
A: 您可以先使用免費試用或申請臨時授權進行評估。正式上線則需購買付費授權。

**Q: 若遇到問題，該向何處尋求支援？**  
A: 可前往 [GroupDocs Support Forum](https://forum.groupdocs.com) 取得協助，亦可直接聯絡 GroupDocs 支援團隊。

---

**最後更新：** 2026-04-11  
**測試版本：** GroupDocs.Editor 23.12 for .NET  
**作者：** GroupDocs  

---