---
date: 2026-09-26
description: 在本詳細的逐步教學中，學習如何使用 GroupDocs.Editor for .NET 處理 CSS 前綴並提取 CSS 內容。
keywords:
- handle css prefix
- extract css content
- edit document css
- prepend url to css
lastmod: 2026-09-26
linktitle: 使用前綴處理 CSS 內容
og_description: 了解如何使用 GroupDocs.Editor for .NET 處理 CSS 前綴並提取 CSS 內容。遵循逐步指南，將 URL
  前置於 CSS 資源並取得樣式表。
og_image_alt: Developer guide showing css prefix handling with GroupDocs.Editor for
  .NET
og_title: 如何在 GroupDocs.Editor for .NET 中處理 CSS 前綴
schemas:
- author: GroupDocs
  dateModified: '2026-09-26'
  description: Learn how to handle css prefix and extract css content using GroupDocs.Editor
    for .NET in this detailed step‑by‑step tutorial.
  headline: How to handle css prefix in GroupDocs.Editor for .NET
  type: TechArticle
- questions:
  - answer: Yes, GroupDocs.Editor for .NET supports PDF, Word, Excel, PowerPoint,
      and many other formats.
    question: Can I use GroupDocs.Editor for .NET with other document formats?
  - answer: Absolutely! You can start your free trial on the [GroupDocs free trial
      page](https://releases.groupdocs.com/).
    question: Is there a free trial available for GroupDocs.Editor for .NET?
  - answer: You can obtain a temporary license from the [temporary license page](https://purchase.groupdocs.com/temporary-license/).
    question: How do I get a temporary license for GroupDocs.Editor for .NET?
  - answer: Detailed documentation is available on the [GroupDocs.Editor for .NET
      documentation site](https://tutorials.groupdocs.com/editor/net/).
    question: Where can I find detailed documentation for GroupDocs.Editor for .NET?
  - answer: You can get support through the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).
    question: What support options are available for GroupDocs.Editor for .NET?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
tags:
- css handling
- GroupDocs.Editor
- .NET document processing
- css prefix
- api tutorial
title: 如何在 GroupDocs.Editor for .NET 中處理 CSS 前綴
type: docs
url: /zh-hant/net/css-handling/handle-css-content-with-prefix/
weight: 11
---

# 如何在 GroupDocs.Editor for .NET 中處理 CSS 前綴

在本教學中，您將學習 **如何處理 CSS 前綴**，在使用 GroupDocs.Editor for .NET 處理文件內的樣式表時。無論您需要為圖片、字型或任何外部資源加上 URL 前綴，以下步驟將向您展示如何 **處理 CSS 前綴**，以及如何 **提取 CSS 內容** 以進一步處理。完成本指南後，您將能重新寫入資源路徑、取得原始 CSS 字串，並自信地將它們整合到您的 Web 工作流程中。

## 快速解答
- **什麼是「處理 CSS 前綴」的意思？** 為 CSS 中引用的外部資源添加自訂 URL 前綴。  
- **哪個 API 方法會返回 CSS 樣式？** `EditableDocument.GetCssContent(...)`。  
- **我需要授權嗎？** 可使用試用授權；正式環境需購買商業授權。  
- **支援哪些 .NET 版本？** .NET Framework 4.5 以上以及 .NET Core/5/6。  
- **我可以在執行時變更前綴嗎？** 可以——只需將不同的字串傳遞給 `GetCssContent` 即可。  

## 什麼是處理 CSS 前綴？
此術語指的是重新寫入 CSS 檔案中圖片、字型或任何外部資產的 URL，使其指向您可控制的位置，例如 CDN 或安全伺服器。透過在前面加上統一的基礎 URL，您可確保文件在瀏覽器或基於 Web 的檢視器中渲染時，所有資源皆能正確載入。

## 為何使用 GroupDocs.Editor 來提取 CSS 內容？
GroupDocs.Editor 能讀取嵌入於 WordProcessing 文件中的原始 CSS，返回原始樣式表字串，並允許您在渲染或儲存前進行操作。此功能可免除手動解析，確保與文件內部表示的高度一致，且支援 **30 多種檔案格式**，在處理高達 **500 MB** 的檔案時，無需將整個檔案載入記憶體。

## 前置條件
在開始之前，請確保您已具備以下前置條件：
- Visual Studio：您需要安裝可正常使用的 Visual Studio。  
- .NET Framework：確保已安裝 .NET Framework。  
- GroupDocs.Editor for .NET：您可從 [GroupDocs.Editor for .NET 下載頁面](https://releases.groupdocs.com/editor/net/) 下載。  
- 範例文件：準備好用於編輯的範例文件。  

## 匯入命名空間
首先，匯入必要的命名空間，以確保程式碼順利執行。此步驟讓我們能存取 GroupDocs.Editor 的核心類別。

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Editor.Options;
```

## 步驟 1：初始化 Editor
`Editor` 類別是使用 GroupDocs.Editor 處理文件的入口點。它負責載入、編輯與儲存操作。  
第一步是使用您的範例文件建立 `Editor` 實例，這會設定編輯環境。

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```

## 步驟 2：編輯文件
`EditableDocument` 物件代表檔案的可編輯版本，並揭露其內部部件，如 CSS、圖片與 HTML。  
接著，我們取得 `EditableDocument` 物件。此物件讓我們能操作文件內部的 CSS。

```csharp
    using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
    {
```

## 步驟 3：設定外部前綴
定義圖片與字型的 URL 前綴。這些前綴會加在 CSS 中每個圖片與字型參考的前面。

```csharp
        string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
        string externalFontsPrefix = "http://www.mywebsite.com/fonts/id=";
```

## 步驟 4：使用前綴提取 CSS 內容
`GetCssContent` 會回傳一組已包含您提供之前綴 URL 的 CSS 樣式表字串。  
呼叫 `GetCssContent`，並傳入剛才定義的前綴。此方法會回傳已包含前綴 URL 的 CSS 樣式表字串清單。

```csharp
        List<string> stylesheets = document.GetCssContent(externalImagesPrefix, externalFontsPrefix);
```

## 步驟 5：輸出結果
列印找到的樣式表數量並顯示每個樣式表。這有助於您驗證前綴是否正確套用。

```csharp
        Console.WriteLine("There are {0} stylesheets in the input document", stylesheets.Count);
        foreach (string css in stylesheets)
        {
            Console.WriteLine(css);
        }
    }
}
```

## 常見問題與解決方案
- **未返回樣式表** – 確認來源文件實際包含 CSS（例如，具有樣式化表格或嵌入 HTML 的 Word 文件）。  
- **URL 不正確** – 再次確認前綴字串是否以正確的分隔符（`/` 或 `=`）結尾，以符合您的伺服器路由設定。  
- **效能問題** – 對於非常大的文件，建議分批處理樣式表，以避免過高的記憶體使用量。  

## 常見問答

**Q: 我可以在 .NET 上的 GroupDocs.Editor 與其他文件格式一起使用嗎？**  
A: 可以，GroupDocs.Editor for .NET 支援 PDF、Word、Excel、PowerPoint 以及許多其他格式。

**Q: 是否提供 GroupDocs.Editor for .NET 的免費試用？**  
A: 當然！您可在 [GroupDocs 免費試用頁面](https://releases.groupdocs.com/) 開始免費試用。

**Q: 我要如何取得 GroupDocs.Editor for .NET 的臨時授權？**  
A: 您可從 [臨時授權頁面](https://purchase.groupdocs.com/temporary-license/) 取得臨時授權。

**Q: 我在哪裡可以找到 GroupDocs.Editor for .NET 的詳細文件？**  
A: 詳細文件可於 [GroupDocs.Editor for .NET 文件站點](https://tutorials.groupdocs.com/editor/net/) 取得。

**Q: GroupDocs.Editor for .NET 提供哪些支援選項？**  
A: 您可透過 [GroupDocs.Editor 支援論壇](https://forum.groupdocs.com/c/editor/20) 獲得協助。

## 其他常見問答

**Q: 提取 CSS 後，我可以變更前綴嗎？**  
A: 可以。再次呼叫 `GetCssContent` 並傳入不同的前綴字串；此方法會使用您在執行時傳入的值。

**Q: 這能用於受密碼保護的文件嗎？**  
A: 可以。建立 `Editor` 實例時，於 `WordProcessingLoadOptions` 中提供密碼。

**Q: 能將修改後的 CSS 儲存回文件中嗎？**  
A: 目前 GroupDocs.Editor 只提供 CSS 的唯讀存取。若要永久保存變更，需使用文件底層的 XML API 取代原始樣式表。

---

**最後更新：** 2026-09-26  
**測試版本：** GroupDocs.Editor 23.12 for .NET  
**作者：** GroupDocs

## 相關教學

- [使用 GroupDocs.Editor .NET 從 Word 文件提取外部 CSS&#58; 完整指南](/editor/net/html-web-documents/extract-external-css-word-docs-groupdocs-editor-dotnet/)
- [使用 GroupDocs.Editor .NET 從 Word 文件提取並加上前綴的 HTML](/editor/net/html-web-documents/groupdocs-editor-dotnet-extract-prefix-html-word-docs/)
- [如何使用 GroupDocs.Editor .NET 提取並修改 Word 文件中的 HTML 內容](/editor/net/html-web-documents/extract-modify-html-content-word-docs-groupdocs-editor-net/)