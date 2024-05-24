---
title: 可編輯文檔的進階用法
linktitle: 可編輯文檔的進階用法
second_title: GroupDocs.Editor .NET API
description: 了解 GroupDocs.Editor 的高級用法，以便以程式設計方式從文件中建立、編輯和提取資源。
type: docs
weight: 11
url: /zh-hant/net/document-editing/advanced-usage-of-editable-documents/
---
## 介紹
如果您是一位希望增強文件編輯功能的 .NET 開發人員，GroupDocs.Editor for .NET 提供了一套功能強大的工具。本綜合指南將引導您使用 GroupDocs.Editor 進階使用可編輯文檔，詳細分解每個步驟，以確保您可以充分利用其潛力。
## 先決條件
在深入了解進階功能之前，請確保您具備以下條件：
- Visual Studio 安裝在您的開發電腦上。
- .NET Framework 與 GroupDocs.Editor 相容。
- 用於 .NET 函式庫的 GroupDocs.Editor。你可以[在這裡下載](https://releases.groupdocs.com/editor/net/).
- 有效的 GroupDocs.Editor 許可證。您可以獲得[免費試用](https://releases.groupdocs.com/)或購買一個[臨時執照](https://purchase.groupdocs.com/temporary-license/).
## 導入命名空間
首先，請確保在 .NET 專案中匯入必要的命名空間：
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
## 第 1 步：建立 EditableDocument 實例
首先，您需要建立一個實例`EditableDocument`透過載入和編輯支援格式的輸入文件。
```csharp
string inputFilePath = "YourSampleDocument.docx";
Editor editor = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```
在此步驟中，我們載入輸入文件並準備進行編輯。
## 步驟2：提取文檔資源
這`EditableDocument`包含可以提取和操縱的各種資源。讓我們來分解一下：
### 步驟 2.1：將整個文件提取為 HTML
您可以產生一個字串，其中包含整個文件及其以 HTML 形式嵌入的所有資源。
```csharp
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```
該字串將非常大，因為它包含以 base64 編碼的樣式表、圖像和字體。
### 步驟2.2：擷取所有影像
從文件中提取所有圖像。
```csharp
List<IImageResource> allImages = beforeEdit.Images;
```
### 步驟2.3：擷取所有字體
提取文件中使用的所有字體。
```csharp
List<FontResourceBase> allFonts = beforeEdit.Fonts;
```
### 步驟2.4：擷取所有樣式表
以文字格式擷取所有樣式表。
```csharp
List<CssText> allStylesheets = beforeEdit.Css;
```
### 步驟2.5：收集所有資源
透過一次調用收集所有資源。
```csharp
List<IHtmlResource> allResources = beforeEdit.AllResources;
```
這包括圖像、字體和樣式表。
### 步驟2.6：取得HTML標記
取得沒有嵌入資源的文件的 HTML 標記。
```csharp
string htmlMarkup = beforeEdit.GetContent();
```
## 第三步：調整外部鏈接
有時，您需要調整外部連結以指向自訂資源處理程序。操作方法如下：
### 步驟 3.1：準備自訂前綴
準備將在原始外部連結前面添加的前綴。
```csharp
string customImagesRequesthandlerUri = "http://example.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://example.com/CssHandler/id=";
string customFontsRequesthandlerUri = "http://example.com/FontsHandler/id=";
```
### 步驟 3.2：產生帶有前綴的 HTML 標記
產生帶有調整後的連結的 HTML 標記。
```csharp
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```
### 步驟 3.3：取得僅正文的 HTML 內容
一些所見即所得編輯器僅處理沒有標題的純 HTML 標記。
```csharp
string onlyBodyContent = beforeEdit.GetBodyContent();
```
### 步驟 3.4：帶有前綴的純正文內容
使用自訂圖像前綴產生僅正文內容。
```csharp
string prefixedBodyContent = beforeEdit.GetBodyContent(customImagesRequesthandlerUri);
```
### 步驟3.5：擷取樣式表
提取文檔中使用的樣式表。
```csharp
List<string> stylesheets = beforeEdit.GetCssContent();
```
### 步驟 3.6：前綴樣式表
使用自訂前綴提取樣式表。
```csharp
List<string> prefixedStylesheets = beforeEdit.GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri);
```
## 第 4 步：將文件另存為 HTML
將編輯後的文件儲存為 HTML 文件，包括其資源。
```csharp
string htmlFilePath = Path.Combine("output", Path.GetFileNameWithoutExtension(inputFilePath) + ".html");
beforeEdit.Save(htmlFilePath);
```
此方法為樣式表、圖像和字體等資源建立一個單獨的目錄。
## 第 5 步：處理 EditableDocument
可編輯文檔實現`IDisposable`並提供檢查實例是否已處置的能力。
```csharp
Console.WriteLine("EditableDocument is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");
```
### 步驟 5.1 處理 Dispose 事件
您也可以訂閱處置事件。
```csharp
EventHandler someMethod = delegate { Console.WriteLine("Disposing event was spotted!"); };
beforeEdit.Disposed += someMethod;
```
## 第 6 步：從 HTML 建立 EditableDocument
從 HTML 文件建立 EditableDocument 的實例。
### 步驟 6.1：從 HTML 文件
```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
```
### 步驟 6.2：從 HTML 標記
```csharp
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);
```
這些實例（afterEditFromFile 和 afterEditFromMarkup）與原始實例（beforeEdit）相同。
## 第 7 步：手動處置
手動處置您的 EditableDocument 實例。
```csharp
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```
這確保了資源的正確清理。
## 結論
GroupDocs.Editor for .NET 提供了以程式設計方式編輯文件的強大工具。透過遵循此逐步指南，您可以有效地管理文件內容、資源和輸出格式。無論您是嵌入資源、調整外部連結或將文件轉換為 HTML，GroupDocs.Editor 都能為您提供進階文件操作所需的功能。
## 常見問題解答
### GroupDocs.Editor 支援哪些格式？
GroupDocs.Editor 支援多種格式，包括 DOCX、XLSX、PPTX 等。
### 我可以在沒有許可證的情況下使用 GroupDocs.Editor 嗎？
是的，您可以將它與[免費試用](https://releases.groupdocs.com/)或一個[臨時執照](https://purchase.groupdocs.com/temporary-license/).
### 如何從文件中提取特定資源？
您可以使用提供的方法來提取圖像、字體和樣式表，例如`Images`, `Fonts`， 和`Css`.
### 是否可以調整 HTML 輸出中的連結？
是的，您可以透過指定圖像、CSS 和字體的自訂前綴來調整外部連結。
### 如何將已編輯的文件儲存為 HTML 文件？
使用`Save`的方法`EditableDocument`類別將文件儲存為 HTML 文件，包括其資源。