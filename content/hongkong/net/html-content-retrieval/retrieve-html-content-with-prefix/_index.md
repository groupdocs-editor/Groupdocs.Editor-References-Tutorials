---
title: 檢索帶有前綴的 HTML 內容
linktitle: 檢索帶有前綴的 HTML 內容
second_title: GroupDocs.Editor .NET API
description: 了解如何使用適用於 .NET 的 GroupDocs.Editor 以及圖像和樣式表的自訂前綴從文件中擷取 HTML 內容。包括逐步指南。
weight: 11
url: /zh-hant/net/html-content-retrieval/retrieve-html-content-with-prefix/
type: docs
---
# 檢索帶有前綴的 HTML 內容

## 介紹
歡迎來到我們的逐步教學，了解如何使用 GroupDocs.Editor for .NET 從文件中擷取 HTML 內容。無論您是經驗豐富的開發人員還是剛剛入門，本指南都將以易於理解的方式引導您完成整個過程。我們將涵蓋您需要了解的所有內容，從設定環境到成功執行程式碼。讓我們深入了解吧！
## 先決條件
在我們開始之前，請確保您具備以下先決條件：
1.  GroupDocs.Editor for .NET：從以下位置下載最新版本[下載頁面](https://releases.groupdocs.com/editor/net/).
2. 開發環境：Visual Studio 或任何其他首選的.NET 開發環境。
3. C# 基礎知識：熟悉 C# 程式設計將有助於您理解範例。
4. 要編輯的文件：準備好範例文件以供測試，例如 Word 文件。
5. .NET Framework：請確定您的電腦上安裝了 .NET Framework。
現在一切準備就緒，讓我們開始吧！
## 導入命名空間
首先，您需要在 C# 專案中匯入必要的命名空間。這些命名空間提供使用 GroupDocs.Editor for .NET 所需的類別和方法。
```csharp
using System;
using GroupDocs.Editor.Options;
```
匯入命名空間後，我們可以繼續設定編輯器。
## 第 1 步：初始化編輯器
首先，您需要初始化`Editor`與您的文件一起上課。此步驟涉及指定要編輯的文件並提供必要的載入選項。
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
    //進一步的步驟將在此處添加
}
```
在此範例中，我們正在載入 Word 文件。您可以更換`"Your Sample Document"`以及您的文件的路徑。
## 第 2 步：編輯文檔
接下來，我們需要開啟文件進行編輯。這是使用以下方法完成的`Edit`的方法`Editor`類，這需要`WordProcessingEditOptions`作為一個論點。
```csharp
using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
{
    //進一步的步驟將在此處添加
}
```
這`EditableDocument`實例表示可編輯格式的文件。現在我們已準備好檢索 HTML 內容。
## 第 3 步：定義自訂前綴
要為圖像和 CSS 添加自訂前綴，我們需要將前綴定義為字串。此步驟可確保 HTML 內容具有外部資源的指定前綴。
```csharp
string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
string externalCssPrefix = "http://www.mywebsite.com/css/id=";
```
您可以將 URL 替換為您所需的前綴。這些前綴將在下一個步驟中用於自訂 HTML 輸出。
## 第 4 步：檢索 HTML 內容
現在我們已經設定了前綴，我們可以從文件中檢索 HTML 內容。這`GetContent`的方法`EditableDocument`class 允許我們指定圖像和 CSS 前綴。
```csharp
string prefixedHtmlContent = document.GetContent(externalImagesPrefix, externalCssPrefix);
Console.WriteLine("HTML content of the input document with custom image and stylesheet prefixes: {0}", prefixedHtmlContent);
```
此程式碼片段使用自訂前綴來取得 HTML 內容並將其列印到控制台。您可以根據需要進一步處理或儲存此 HTML 內容。
## 結論
現在你就得到它了！透過執行這些步驟，您可以使用 GroupDocs.Editor for .NET 輕鬆地從文件中擷取 HTML 內容，並提供圖片和樣式表的自訂前綴。這個強大的工具簡化了文件操作，使您能夠專注於將文件編輯無縫整合到 .NET 應用程式中。
欲了解更多詳細信息，請查看[用於 .NET 文件的 GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/) 。如果您有任何疑問或需要進一步協助，請隨時聯繫[支援論壇](https://forum.groupdocs.com/c/editor/20).
## 常見問題解答
### 我可以使用 GroupDocs.Editor for .NET 編輯哪些類型的文件？
GroupDocs.Editor 支援多種文件格式，包括 Word、Excel、PowerPoint、PDF 等。
### 如何取得 GroupDocs.Editor for .NET 的免費試用版？
您可以從以下網站獲得免費試用[集團文件網站](https://releases.groupdocs.com/).
### 我可以進一步自訂 HTML 內容嗎？
是的，您可以在渲染或儲存檢索到的 HTML 內容之前根據需要進行修改。
### 是否可以將 GroupDocs.Editor for .NET 與其他 .NET 語言一起使用？
是的，您可以將其與任何 .NET 相容語言（例如 VB.NET 或 F#）一起使用。
### 如何取得 GroupDocs.Editor for .NET 的臨時授權？
您可以從以下機構獲得臨時許可證[購買頁面](https://purchase.groupdocs.com/temporary-license/).