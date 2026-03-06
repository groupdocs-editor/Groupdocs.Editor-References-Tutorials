---
date: 2026-03-06
description: 在本詳細的逐步教學中，學習如何使用 GroupDocs.Editor for .NET 處理帶前綴的 CSS 內容並提取 CSS 內容。
linktitle: Handle CSS Content with Prefix
second_title: GroupDocs.Editor .NET API
title: 使用前綴處理 CSS 內容
type: docs
url: /zh-hant/net/css-handling/handle-css-content-with-prefix/
weight: 11
---

# 處理帶前綴的 CSS 內容

在本教學中，您將了解在使用 GroupDocs.Editor for .NET 處理文件內樣式表時，**如何處理 css prefix**。無論您需要在圖像、字體或任何外部資源前加上 URL，以下步驟將精確說明如何**處理 css prefix**，以及如何**extract css content** 以進一步處理。

## 快速解答
- **「處理 css prefix」是什麼意思？** 在 CSS 中引用的外部資源前添加自訂 URL 前綴。  
- **哪個 API 方法會返回 CSS 樣式？** `EditableDocument.GetCssContent(...)`。  
- **我需要授權嗎？** 提供試用授權；正式環境需購買商業授權。  
- **支援哪些 .NET 版本？** .NET Framework 4.5 以上以及 .NET Core/5/6。  
- **我可以在執行時變更前綴嗎？** 可以，只需將不同的字串傳遞給 `GetCssContent` 即可。  

## 什麼是 **handle css prefix**？
在 CSS 資源上套用前綴會重新寫入圖像、字體或其他資產的路徑，使其指向您可控制的位置（例如 CDN 或受保護的伺服器）。當您匯出文件且需要所有外部引用能從 Web 應用程式存取時，這特別有用。

## 為什麼使用 GroupDocs.Editor 來 **extract css content**？
GroupDocs.Editor 能讀取嵌入於 WordProcessing 文件中的原始 CSS，提供原始樣式表字串，讓您在渲染或儲存前進行操作。這可免除手動解析的需求，且確保提取的 CSS 與文件的內部表示相符。

## 前置條件
在開始之前，請確保已具備以下前置條件：
- Visual Studio: 您需要安裝好的 Visual Studio。  
- .NET Framework: 確認已安裝 .NET Framework。  
- GroupDocs.Editor for .NET: 您可從 [here](https://releases.groupdocs.com/editor/net/) 下載。  
- Sample Document: 準備好用於編輯的範例文件。  

## 匯入命名空間
首先，匯入必要的命名空間以確保程式碼順利執行。此步驟讓我們能存取 GroupDocs.Editor 的核心類別。

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Editor.Options;
```

## 步驟 1：初始化 Editor
第一步是使用您的範例文件建立 `Editor` 實例，這會設定編輯環境。

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```

## 步驟 2：編輯文件
接著，我們取得 `EditableDocument` 物件。此物件代表檔案的可編輯版本，讓我們能操作其內部部件。

```csharp
    using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
    {
```

## 步驟 3：設定外部前綴
定義圖像與字體的 URL 前綴。這些前綴會加在 CSS 中每個圖像與字體的引用前。

```csharp
        string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
        string externalFontsPrefix = "http://www.mywebsite.com/fonts/id=";
```

## 步驟 4：使用前綴 **Extract CSS content**
呼叫 `GetCssContent`，傳入剛才定義的前綴。此方法會回傳已包含前綴 URL 的 CSS 樣式表字串清單。

```csharp
        List<string> stylesheets = document.GetCssContent(externalImagesPrefix, externalFontsPrefix);
```

## 步驟 5：輸出結果
列印找到的樣式表數量並顯示每個樣式表。這可協助您驗證前綴是否正確套用。

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
- **未返回樣式表** – 確認來源文件實際包含 CSS（例如具有樣式化表格或嵌入 HTML 的 Word 文件）。  
- **URL 不正確** – 再次確認前綴字串是否以正確的分隔符（`/` 或 `=`）結尾，以符合伺服器路由設定。  
- **效能問題** – 對於非常大的文件，建議分批處理樣式表，以避免高記憶體使用量。  

## 結論
使用 GroupDocs.Editor for .NET 以帶前綴的方式處理 CSS 內容既簡單又強大。依循上述步驟，您即可 **handle css prefix**，透過 **extract css content** 取得原始 CSS，並將外部資源無縫整合至您的 Web 工作流程。探索 GroupDocs.Editor 的其他功能，如 HTML 轉換、圖像提取與文件合併，以發揮 API 更大的價值。

## 常見問答
### 我可以在 .NET 上使用 GroupDocs.Editor 處理其他文件格式嗎？
是的，GroupDocs.Editor for .NET 支援多種文件格式，包括 PDF、Word、Excel 等。

### 是否提供 GroupDocs.Editor for .NET 的免費試用？
當然！您可從 [here](https://releases.groupdocs.com/) 開始免費試用。

### 如何取得 GroupDocs.Editor for .NET 的臨時授權？
您可於 [here](https://purchase.groupdocs.com/temporary-license/) 取得臨時授權。

### 我在哪裡可以找到 GroupDocs.Editor for .NET 的詳細文件？
詳細文件可於 [here](https://tutorials.groupdocs.com/editor/net/) 取得。

### GroupDocs.Editor for .NET 提供哪些支援選項？
您可在 [here](https://forum.groupdocs.com/c/editor/20) 獲得支援。

## 其他常見問答

**Q: 提取 CSS 後我可以變更前綴嗎？**  
A: 可以。再次呼叫 `GetCssContent` 並傳入不同的前綴字串；此方法會使用您在執行時傳入的值。

**Q: 這能用於受密碼保護的文件嗎？**  
A: 能。建立 `Editor` 實例時，於 `WordProcessingLoadOptions` 中提供密碼。

**Q: 能將修改後的 CSS 儲存回文件嗎？**  
A: 目前 GroupDocs.Editor 只提供 CSS 的唯讀存取。若要永久保存變更，需使用文件底層的 XML API 取代原始樣式表。

---

**最後更新：** 2026-03-06  
**測試環境：** GroupDocs.Editor 23.12 for .NET  
**作者：** GroupDocs