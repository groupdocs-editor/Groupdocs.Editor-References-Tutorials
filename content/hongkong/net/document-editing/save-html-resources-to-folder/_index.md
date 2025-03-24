---
title: 將 HTML 資源儲存到資料夾
linktitle: 將 HTML 資源儲存到資料夾
second_title: GroupDocs.Editor .NET API
description: 了解如何使用 Groupdocs.Editor for .NET 從文件中擷取 HTML 資源。這個綜合教程為開發人員提供了逐步指導。
weight: 13
url: /zh-hant/net/document-editing/save-html-resources-to-folder/
---
## 介紹
Groupdocs.Editor for .NET 是一個功能強大的工具，使開發人員能夠在其 .NET 應用程式中無縫地操作和轉換文件。無論您需要從文件中提取 HTML 資源還是執行高級編輯任務，Groupdocs.Editor 都可以透過其直覺的 API 和豐富的文件簡化流程。
## 先決條件
在深入學習本教程之前，請確保您具備以下先決條件：
1. C# 和 .NET 的基本知識：熟悉 C# 程式語言和 .NET 框架對於理解範例至關重要。
2.  Groupdocs.Editor for .NET 函式庫：從下列位置下載並安裝 Groupdocs.Editor for .NET 函式庫[網站](https://releases.groupdocs.com/editor/net/).
3. 開發環境：設定您首選的開發環境，例如 Visual Studio 或任何其他相容的 IDE。

## 導入命名空間
首先，在您的 C# 專案中匯入必要的命名空間：
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```
##現在，讓我們將使用 Groupdocs.Editor for .NET 將 HTML 資源儲存到資料夾的過程分解為多個步驟：
## 步驟1：初始化Groupdocs.Editor
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
首先，初始化`Editor`透過提供範例文件的路徑來取得物件。在此範例中，我們使用的是 Word 文檔，因此我們指定`WordProcessingLoadOptions`作為文檔類型。
## 第 2 步：編輯文檔
```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
接下來，創建一個`EditableDocument`對象透過調用`Edit`的方法`Editor`目的。這允許您對文件執行編輯操作。
## 第三步：提取資源
```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
從文件中提取圖像、字體和樣式表等資源並將它們儲存在各自的清單中。
## 步驟 4：指定輸出資料夾
```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
定義將保存提取的資源的輸出資料夾。您可以根據您的要求自訂資料夾路徑。
## 第五步：節省資源
```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
循環遍歷每個影像資源，將其儲存到輸出資料夾，並顯示相關訊息，例如檔案名稱、類型和尺寸。
```csharp
		foreach (FontResourceBase oneFont in fonts)
		{
			Console.WriteLine("Saving {0} of {1} type",
				oneFont.FilenameWithExtension, oneFont.Type.FormalName);
			oneFont.Save(Path.Combine(outputFolder, oneFont.FilenameWithExtension));
		}
```
同樣，將每個字體資源保存到輸出資料夾中。
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
最後，將每個樣式表儲存到輸出資料夾並完成編輯過程。

## 結論
總之，Groupdocs.Editor for .NET 提供了一種方便的解決方案，用於在 .NET 應用程式中以程式設計方式管理和操作文件。透過遵循本教學課程，您可以輕鬆地從文件中提取 HTML 資源，並根據您的特定要求自訂流程。
## 常見問題解答
### Groupdocs.Editor 是否與 Word 以外的其他文件格式相容？
是的，Groupdocs.Editor 支援多種文件格式，包括 Excel、PowerPoint、PDF 等。
### 我可以將 Groupdocs.Editor 整合到我的 Web 應用程式中嗎？
當然，Groupdocs.Editor 可以與在 .NET 框架上開發的 Web 應用程式無縫整合。
### Groupdocs.Editor 是否提供雲端儲存服務支援？
是的，Groupdocs.Editor 支援與 Google Drive、Dropbox 和 Microsoft OneDrive 等流行的雲端儲存服務整合。
### Groupdocs.Editor 是否有免費試用版？
是的，您可以從網站免費試用 Groupdocs.Editor。
### 如何獲得 Groupdocs.Editor 的技術支援？
如需技術協助和社群支持，您可以造訪 Groupdocs.Editor 論壇。