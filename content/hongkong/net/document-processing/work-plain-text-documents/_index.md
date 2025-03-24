---
title: 處理純文字文檔
linktitle: 處理純文字文檔
second_title: GroupDocs.Editor .NET API
description: 透過我們的逐步指南，學習使用 GroupDocs.Editor for .NET 編輯純文字文件。簡化您的 .NET 文件編輯流程。
weight: 15
url: /zh-hant/net/document-processing/work-plain-text-documents/
---

# 處理純文字文檔

## 介紹
您是否希望簡化 .NET 中的文件編輯流程？ .NET 的 GroupDocs.Editor 就是您的最佳選擇！這個強大的 API 允許您輕鬆編輯各種文件格式。在本教程中，我們將引導您完成使用 GroupDocs.Editor for .NET 處理純文字文件的流程。最後，您將能夠像專業人士一樣處理文字文檔編輯。準備好潛入了嗎？讓我們開始吧！
## 先決條件
在我們開始之前，您需要準備好一些東西：
- .NET 開發環境：確保您已設定有效的 .NET 開發環境。 Visual Studio 是個受歡迎的選擇。
-  適用於 .NET 的 GroupDocs.Editor：下載並安裝[GroupDocs.Editor for .NET](https://releases.groupdocs.com/editor/net/).
- 基本 C# 知識：熟悉 C# 程式語言將幫助您理解範例。
- 文字編輯器：任何文字編輯器都可以，但建議使用 Visual Studio Code，因為它的功能和易用性。
## 導入命名空間
要開始使用 GroupDocs.Editor for .NET，您需要將必要的命名空間匯入到您的專案中。這確保了所有必需的類別和方法都可供使用。
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```
讓我們將這個過程分解為可管理的步驟。請跟隨我們指導您完成使用 GroupDocs.Editor for .NET 編輯純文字文件的每個階段。
## 第 1 步：取得輸入 TXT 檔案的路徑
首先，您需要指定輸入 TXT 檔案的路徑。這可以是本機檔案的路徑或包含檔案內容的流。
```csharp
string inputFilePath = "YourSampleDocument.txt";
```
## 步驟2：建立編輯器實例
接下來，建立一個實例`Editor`班級。該類別負責載入和編輯文檔。此階段不需要載入選項。
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## 第 3 步：建立 TXT 編輯選項
現在，建立 TXT 編輯選項。這些選項可讓您指定在編輯期間應如何處理文字內容。
```csharp
    TextEditOptions editOptions = new TextEditOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        RecognizeLists = true,
        LeadingSpaces = TextLeadingSpacesOptions.ConvertToIndent,
        TrailingSpaces = TextTrailingSpacesOptions.Trim
    };
```
## 步驟 4：建立一個 EditableDocument 實例
設定編輯選項後，建立一個`EditableDocument`實例。這表示可編輯格式的文件。
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## 步驟5：編輯文檔內容
檢索原始文字內容並進行所需的編輯。在此範例中，我們將用「編輯文字」取代「文字」一詞。
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("text", "EDITED text");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## 步驟 6：建立包含更新內容的 EditableDocument
進行必要的編輯後，建立一個新的`EditableDocument`包含更新的內容和原始資源。
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## 第 7 步：建立字處理儲存選項
準備 WordProcessing 格式的儲存選項。此範例使用 DOCM 格式並指定區域設定。
```csharp
    WordProcessingSaveOptions wordSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm)
    {
        Locale = System.Globalization.CultureInfo.GetCultureInfo("en-GB")
    };
```
## 第 8 步：建立 TXT 儲存選項
同樣，建立 TXT 格式的儲存選項。確保編碼設定為 UTF-8 並保留表格佈局。
```csharp
    TextSaveOptions txtSaveOptions = new TextSaveOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        PreserveTableLayout = true
    };
```
## 第9步：準備輸出路徑
準備保存生成的 DOCX 和 TXT 檔案的路徑。使用輸入檔案路徑來確定輸出目錄和檔案名稱。
```csharp
    string outputWordPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".docm");
    string outputTxtPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".txt");
```
## 第10步：儲存編輯後的文檔
最後，使用指定的儲存選項以 DOCX 和 TXT 格式儲存編輯後的文件。
```csharp
    editor.Save(afterEdit, outputWordPath, wordSaveOptions);
    editor.Save(afterEdit, outputTxtPath, txtSaveOptions);
}
System.Console.WriteLine("Document editing process completed successfully!");
```
## 結論
恭喜！您已使用 GroupDocs.Editor for .NET 成功編輯了純文字文件。這個強大的工具簡化了文件編輯，使其可以輕鬆整合到您的 .NET 應用程式中。無論您是處理簡單的文字檔案還是複雜的文件格式，GroupDocs.Editor 都能滿足您的需求。透過存取探索更多特性和功能[GroupDocs.Editor 文檔](https://tutorials.groupdocs.com/editor/net/).
## 常見問題解答
### GroupDocs.Editor for .NET 支援哪些檔案格式？
 GroupDocs.Editor for .NET 支援多種檔案格式，包括 DOCX、TXT、HTML 等。檢查[文件](https://tutorials.groupdocs.com/editor/net/)以獲得完整清單。
### 如何取得 GroupDocs.Editor for .NET 的免費試用版？
您可以從以下位置下載 GroupDocs.Editor for .NET 的免費試用版：[發布頁面](https://releases.groupdocs.com/).
### 我可以購買 GroupDocs.Editor for .NET 的臨時授權嗎？
是的，您可以從以下機構獲得臨時許可證[GroupDocs 購買頁面](https://purchase.groupdocs.com/temporary-license/).
### 在哪裡可以獲得 GroupDocs.Editor for .NET 的支援？
可透過以下方式獲得支持[GroupDocs.Editor 支援論壇](https://forum.groupdocs.com/c/editor/20).
### 是否有適用於 .NET 的 GroupDocs.Editor 的詳細文件？
是的，詳細文件可在[GroupDocs.Editor 文件頁面](https://tutorials.groupdocs.com/editor/net/).