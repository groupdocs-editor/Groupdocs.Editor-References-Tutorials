---
title: 檢索 HTML 正文內容
linktitle: 檢索 HTML 正文內容
second_title: GroupDocs.Editor .NET API
description: 根據我們的逐步指南，使用適用於 .NET 的 GroupDocs.Editor 來擷取 HTML 正文內容。輕鬆增強您的 .NET 應用程式。
type: docs
weight: 10
url: /zh-hant/net/html-content-retrieval/retrieve-html-body-content/
---
## 介紹
您準備好徹底改變 .NET 應用程式中處理文件編輯的方式了嗎？ .NET 的 GroupDocs.Editor 就是您的最佳選擇！這個強大的工具可以直接在您的應用程式中無縫編輯各種文件格式。無論您使用的是 Word、PDF 還是 HTML，GroupDocs.Editor 都可以讓您輕鬆編輯和操作文檔，而無需使用外部工具。
## 先決條件
在我們開始之前，您需要滿足一些先決條件：
- .NET 程式設計的基本知識：熟悉 C# 和 .NET 框架將幫助您理解範例。
-  GroupDocs.Editor for .NET：您可以從[GroupDocs.Editor下載頁面](https://releases.groupdocs.com/editor/net/).
- 有效的許可證：您可以從[GroupDocs 購買頁面](https://purchase.groupdocs.com/buy)或請求[臨時執照](https://purchase.groupdocs.com/temporary-license/).
- 整合開發環境（IDE）：建議使用 Visual Studio 以獲得最佳開發體驗。
## 導入命名空間
若要開始使用適用於 .NET 的 GroupDocs.Editor，您需要匯入必要的命名空間。這將允許您存取文件編輯所需的類別和方法。
```csharp
using System;
using GroupDocs.Editor.Options;
```
## 第 1 步：初始化編輯器
我們流程的第一步是初始化`Editor`與您的文件一起上課。該類別是所有編輯操作的入口點。

您需要載入要編輯的文檔。對於本範例，我們將使用範例 Word 文件。
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
    //繼續下一步
}
```
## 第 2 步：編輯文檔
接下來，我們將使用`Edit`的方法`Editor`類別來建立文檔的可編輯版本。

我們將指定文檔的編輯選項。在這種情況下，我們將使用`WordProcessingEditOptions`.
```csharp
using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
{
    //繼續下一步
}
```
## 第 3 步：檢索 HTML 正文內容
現在，我們將以 HTML 格式檢索文件的正文內容。這就是魔法發生的地方！

使用`GetBodyContent`方法，我們可以擷取HTML的內部內容`<body>`元素。
```csharp
string bodyContent = document.GetBodyContent();
Console.WriteLine("Inner content of the HTML->BODY element: {0}", bodyContent);
```

## 結論
恭喜！您已成功學習如何使用 GroupDocs.Editor for .NET 從文件中擷取 HTML 正文內容。這個功能強大的程式庫簡化了 .NET 應用程式中的文件編輯，使其成為開發人員的寶貴工具。
## 常見問題解答
### GroupDocs.Editor 支援哪些檔案格式？
GroupDocs.Editor 支援多種文件格式，包括 Word 文件、PDF、Excel 電子表格、PowerPoint 簡報和 HTML 文件。
### 如何取得 GroupDocs.Editor 的臨時授權？
您可以向以下機構申請臨時許可證[GroupDocs 臨時許可證頁面](https://purchase.groupdocs.com/temporary-license/).
### GroupDocs.Editor 是否有免費試用版？
是的，您可以從以下位置下載免費試用版：[GroupDocs.Editor下載頁面](https://releases.groupdocs.com/).
### 我可以將 GroupDocs.Editor 與 .NET Core 一起使用嗎？
是的，GroupDocs.Editor 與 .NET Core 相容，為現代應用程式開發提供靈活性。
### 在哪裡可以找到 GroupDocs.Editor 的更多範例和文件？
您可以在以下位置找到更多範例和詳細文檔[GroupDocs.Editor 文件頁面](https://reference.groupdocs.com/editor/net/).