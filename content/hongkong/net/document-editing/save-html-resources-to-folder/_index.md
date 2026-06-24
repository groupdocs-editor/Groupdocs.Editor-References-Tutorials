---
date: 2026-05-12
description: 了解如何使用 GroupDocs.Editor for .NET 從文件中提取字型及其他 HTML 資源。針對 .NET 開發人員的逐步指南。
keywords:
- how to extract fonts
- GroupDocs.Editor .NET
- extract HTML resources
linktitle: 將 HTML 資源儲存至資料夾
schemas:
- author: GroupDocs
  dateModified: '2026-05-12'
  description: Learn how to extract fonts and other HTML resources from documents
    using GroupDocs.Editor for .NET. Step‑by‑step guide for .NET developers.
  headline: How to Extract Fonts and Save HTML Resources to Folder
  type: TechArticle
- description: Learn how to extract fonts and other HTML resources from documents
    using GroupDocs.Editor for .NET. Step‑by‑step guide for .NET developers.
  name: How to Extract Fonts and Save HTML Resources to Folder
  steps:
  - name: '**Basic Knowledge of C# and .NET** – Familiarity with C# programming language
      and .NET framework is essential to follow along with the examples.'
    text: '**Basic Knowledge of C# and .NET** – Familiarity with C# programming language
      and .NET framework is essential to follow along with the examples.'
  - name: '**GroupDocs.Editor for .NET Library** – Download and install GroupDocs.Editor
      for .NET library from the [website](https://releases.groupdocs.com/editor/net/).'
    text: '**GroupDocs.Editor for .NET Library** – Download and install GroupDocs.Editor
      for .NET library from the [website](https://releases.groupdocs.com/editor/net/).'
  - name: '**Development Environment** – Set up your preferred development environment
      such as Visual Studio or any other compatible IDE.'
    text: '**Development Environment** – Set up your preferred development environment
      such as Visual Studio or any other compatible IDE.'
  type: HowTo
- questions:
  - answer: Yes, it supports Excel, PowerPoint, PDF, HTML, and over 50 additional
      formats for both editing and resource extraction.
    question: Is GroupDocs.Editor compatible with other document formats besides Word?
  - answer: Absolutely. The API works seamlessly with ASP.NET Core, MVC, and Web API
      projects, allowing you to process documents on the server side.
    question: Can I integrate GroupDocs.Editor into a web application?
  - answer: Yes, it includes built‑in connectors for Google Drive, Dropbox, OneDrive,
      and Amazon S3, enabling direct loading and saving of documents in the cloud.
    question: Does GroupDocs.Editor provide cloud storage integration?
  - answer: A fully functional 30‑day trial can be downloaded from the GroupDocs website
      without any credit‑card requirement.
    question: Is there a free trial available for GroupDocs.Editor?
  - answer: You can reach the GroupDocs support team via the official forum, submit
      a ticket through the customer portal, or consult the detailed API documentation.
    question: How can I get technical support for extraction issues?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: 如何提取字型並將 HTML 資源儲存至資料夾
type: docs
url: /zh-hant/net/document-editing/save-html-resources-to-folder/
weight: 13
---

# 如何提取字體並將 HTML 資源儲存至資料夾

## 簡介
GroupDocs.Editor for .NET 讓您在將文件轉換為 HTML 時 **提取字體** 以及其他資產。只需幾行 C# 程式碼，即可提取圖像、樣式表和字體檔，然後儲存到您選擇的資料夾。本教學將帶您完成整個工作流程，從初始化編輯器到將每個資源寫入磁碟。

## 快速解答
- **「提取字體」是什麼意思？** 這是指在 HTML 轉換過程中，從來源文件中取得嵌入的字體檔案的過程。  
- **哪個函式庫負責此功能？** GroupDocs.Editor for .NET 提供專門的 API 用於提取字體、圖像和樣式表。  
- **我需要授權嗎？** 提供免費試用版；商業使用需購買授權。  
- **支援哪些 .NET 版本？** .NET Framework 4.5+、.NET Core 3.1+、.NET 5/6/7。  
- **我可以指定自訂資料夾嗎？** 可以，儲存提取的資源時您可以指定任何可寫入的路徑。

## 什麼是「提取字體」？
**提取字體** 是指取得嵌入於來源文件（例如 DOCX、PPTX）中的原始字體檔，以便在產生的 HTML 中引用。這可確保文字在瀏覽器中呈現時與原始文件完全一致，無需依賴系統字體。

## 為何使用 GroupDocs.Editor 進行 HTML 資源提取？
GroupDocs.Editor 支援 **超過 50 種輸入與輸出格式**——包括 DOCX、PPTX、PDF 與 HTML，且可在不將整個檔案載入記憶體的情況下處理 **最多 300 頁** 的文件。其 API 能在一次處理中提取字體、圖像與 CSS，與手動解析相比，可將開發時間縮短最高 **70 %**。

## 先決條件
在開始本教學之前，請確保您具備以下先決條件：
1. **具備 C# 與 .NET 的基礎知識** – 熟悉 C# 程式語言與 .NET 框架是跟隨範例的前提。  
2. **GroupDocs.Editor for .NET 函式庫** – 從 [網站](https://releases.groupdocs.com/editor/net/) 下載並安裝 GroupDocs.Editor for .NET 函式庫。  
3. **開發環境** – 設定您偏好的開發環境，例如 Visual Studio 或其他相容的 IDE。

## 匯入命名空間
要開始使用，請在 C# 專案中匯入必要的命名空間：

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```

## 如何提取字體並將 HTML 資源儲存至資料夾？
使用 `Editor editor = new Editor("sample.docx", new WordProcessingLoadOptions());` 載入來源文件，然後呼叫 `editor.Save("output.html", SaveOptions.Html);`。儲存完成後，`Resources` 集合會包含所有提取的資產——包括字體——您可以遍歷該集合並寫入磁碟。此單一步驟同時處理轉換與資源提取，全部自動化。

## 步驟 1：初始化 GroupDocs.Editor
`Editor` 是負責文件載入、轉換與資源提取的核心類別，代表記憶體中的單一文件會話。

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
首先，透過提供範例文件的路徑來初始化 `Editor` 物件。在此範例中，我們使用 Word 文件，故指定 `WordProcessingLoadOptions` 為文件類型。

## 步驟 2：編輯文件
`EditableDocument` 是 `Edit` 方法返回的可編輯表示，允許您在儲存前對文件進行操作。

```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
接著，呼叫 `Editor` 物件的 `Edit` 方法以建立 `EditableDocument` 物件，從而對文件執行編輯操作。

## 步驟 3：提取資源
`Resources` 是一個集合，將提取的資產——圖像、字體與樣式表——分別放入不同的清單，以便於處理。

```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
從文件中提取圖像、字體與樣式表等資源，並分別存入對應的清單。

## 步驟 4：指定輸出資料夾
`outputFolder` 是一個字串，用來定義提取檔案的寫入位置。您可以將其指向伺服器或本機上任何可寫入的目錄。

```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
定義儲存提取資源的輸出資料夾。您可以依需求自訂資料夾路徑。

## 步驟 5：儲存資源
`SaveResource` 是一個輔助例程，用於將單一二進位資源（圖像、字體或樣式表）寫入檔案系統。

```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
遍歷每個圖像資源，將其儲存至輸出資料夾，並顯示檔名、類型與尺寸等相關資訊。

```csharp
		foreach (FontResourceBase oneFont in fonts)
		{
			Console.WriteLine("Saving {0} of {1} type",
				oneFont.FilenameWithExtension, oneFont.Type.FormalName);
			oneFont.Save(Path.Combine(outputFolder, oneFont.FilenameWithExtension));
		}
```
同樣地，將每個字體資源儲存至輸出資料夾。

```csharp
		foreach (CssText oneStylesheet in stylesheets)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} encoding",
				oneStylesheet.FilenameWithExtension, oneStylesheet.Type.FormalName, oneStylesheet.Encoding);
			oneStylesheet.Save(Path.Combine(outputFolder, oneStylesheet.FilenameWithExtension));
		}
	}
}
```
最後，將每個樣式表儲存至輸出資料夾，完成編輯流程。

## 常見問題與解決方案
- **轉換後缺少字體** – 確認來源文件已嵌入字體；否則 GroupDocs.Editor 只能引用系統字體。  
- **存取被拒錯誤** – 確認應用程式執行緒對目標輸出資料夾具有寫入權限。  
- **大型文件導致記憶體使用過高** – 使用 `LoadOptions` 並將 `LoadMode = LoadMode.Stream`，以串流方式處理大型檔案，而非一次性載入全部至記憶體。

## 常見問答

**Q: GroupDocs.Editor 是否支援除 Word 之外的其他文件格式？**  
A: 是的，它支援 Excel、PowerPoint、PDF、HTML 以及超過 50 種其他格式，皆可用於編輯與資源提取。

**Q: 我可以將 GroupDocs.Editor 整合到 Web 應用程式中嗎？**  
A: 當然可以。此 API 可無縫配合 ASP.NET Core、MVC 與 Web API 專案，讓您在伺服器端處理文件。

**Q: GroupDocs.Editor 是否提供雲端儲存整合？**  
A: 有，內建支援 Google Drive、Dropbox、OneDrive 與 Amazon S3 連接器，可直接在雲端載入與儲存文件。

**Q: 是否提供 GroupDocs.Editor 的免費試用？**  
A: 可從 GroupDocs 官方網站下載完整功能的 30 天試用版，無需信用卡。

**Q: 若遇到提取問題，如何取得技術支援？**  
A: 您可透過官方論壇聯繫 GroupDocs 支援團隊、在客戶入口提交工單，或參考詳細的 API 文件。

---

**Last Updated:** 2026-05-12  
**Tested With:** GroupDocs.Editor 23.11 for .NET  
**Author:** GroupDocs

## 相關教學

- [使用 GroupDocs.Editor .NET 高效文件編輯：將 HTML 轉換為可編輯文件](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)
- [使用 GroupDocs.Editor .NET 高效提取與儲存 DOCX 資源 - 完整指南](/editor/net/document-saving/efficient-extract-save-docx-resources-groupdocs-editor-net/)
- [精通 GroupDocs.Editor .NET 文件編輯與轉換：完整指南](/editor/net/document-editing/groupdocs-editor-net-mastering-document-editing/)