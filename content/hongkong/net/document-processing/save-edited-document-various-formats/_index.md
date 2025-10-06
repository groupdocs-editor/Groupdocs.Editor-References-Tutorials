---
title: 將編輯的文檔儲存為各種格式
linktitle: 將編輯的文檔儲存為各種格式
second_title: GroupDocs.Editor .NET API
description: 在這份全面的逐步指南中了解如何使用 GroupDocs.Editor for .NET 將編輯後的文件儲存為各種格式。
weight: 11
url: /zh-hant/net/document-processing/save-edited-document-various-formats/
type: docs
---
# 將編輯的文檔儲存為各種格式

## 介紹
您是否希望使用 GroupDocs.Editor for .NET 將編輯後的文件儲存為各種格式？您來對地方了！這個綜合指南將引導您完成整個過程，從設定環境到以多種格式儲存編輯後的文件。讓我們深入研究，讓文件編輯和保存變得輕而易舉！
## 先決條件
在我們開始之前，請確保您具備以下條件：
1.  GroupDocs.Editor for .NET - 從以下位置下載最新版本[這裡](https://releases.groupdocs.com/editor/net/).
2. 開發環境 - Visual Studio 或任何其他 .NET 相容 IDE。
3. .NET Framework - 確保您安裝了 .NET Framework 4.6.1 或更高版本。
4. 範例文件 - 要使用的範例字處理文件。
5. 基本 C# 知識 - 需要熟悉 C# 程式設計。
## 導入命名空間
首先，請確保將必要的命名空間匯入到您的 C# 專案中。這對於存取 GroupDocs.Editor 功能至關重要。
```csharp
using System;
using GroupDocs.Editor.Metadata;
```
讓我們將這個過程分解為可管理的步驟。仔細閱讀以確保您理解每個部分。
## 第 1 步：取得輸入檔的路徑
首先，您需要指定輸入字處理檔的路徑。該文件將被載入並編輯。
```csharp
string inputFilePath = "Your Sample Document";
```
## 步驟 2：為文件建立載入選項
接下來，建立特定於字處理文件的載入選項。這些選項將有助於自訂文件的載入方式。
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
```
## 第 3 步：載入帶有選項的文檔
現在，將文檔載入到`Editor`使用指定載入選項的實例。
```csharp
using (Editor editor = new Editor(inputFilePath, delegate { return loadOptions; }))
```
## 第 4 步：建立編輯選項
準備文檔的編輯選項。這些選項將決定如何開啟文件進行編輯。
```csharp
WordProcessingEditOptions editOptions = new WordProcessingEditOptions();
```
## 步驟5：開啟文檔進行編輯
透過建立一個文件來開啟要編輯的文檔`EditableDocument`實例。該實例將允許您對文件進行更改。
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
```
## 第6步：編輯文檔內容
現在是時候編輯文檔的內容了。首先，取得單一 base64 編碼字串形式的文件。
```csharp
string allEmbeddedInsideString = beforeEdit.GetEmbeddedHtml();
```
例如，我們修改文件中的副標題。
```csharp
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
```
## 步驟 7：從編輯內容建立新的可編輯文檔
創建一個新的`EditableDocument`來自編輯的內容和資源的實例。
```csharp
using (EditableDocument afterEdit = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null))
```
## 步驟 8：將文件儲存為各種格式
最後，迭代所有支援的 WordProcessing 格式並以每種格式儲存編輯後的文件。
```csharp
foreach (WordProcessingFormats oneFormat in WordProcessingFormats.All)
{
    //準備保存選項
    WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(oneFormat);
    //準備保存路徑
    string savePath = Path.Combine("OutputDirectory", "MultipleOutFormats." + saveOptions.OutputFormat.Extension);
    //儲存文件
    editor.Save(afterEdit, savePath, saveOptions);
}
```
## 完成訊息
最後，您可以列印一條訊息，指示該過程已成功完成。
```csharp
Console.WriteLine("SavingEditedDocumentToAllFormats routine has successfully finished");
```
## 結論
恭喜！您已成功學習如何使用 GroupDocs.Editor for .NET 將編輯後的文件儲存為各種格式。這個強大的工具只需幾行程式碼即可輕鬆操作和保存多種格式的文件。請記住，關鍵步驟包括載入文件、編輯內容以及以所需格式儲存。
## 常見問題解答
### 什麼是 .NET 的 GroupDocs.Editor？
GroupDocs.Editor for .NET 是一個功能強大的 API，可讓您使用 .NET 應用程式編輯各種格式的文件。
### 我可以免費使用 GroupDocs.Editor 嗎？
是的，您可以免費試用。下載它[這裡](https://releases.groupdocs.com/).
### GroupDocs.Editor 支援哪些格式？
GroupDocs.Editor 支援多種格式，包括 DOCX、PDF、HTML 等。
### 如何取得 GroupDocs.Editor 的臨時授權？
您可以獲得臨時許可證[這裡](https://purchase.groupdocs.com/temporary-license/).
### 在哪裡可以找到更多文件和支援？
提供詳細文檔[這裡](https://tutorials.groupdocs.com/editor/net/) ，並且您可以獲得支持[這裡](https://forum.groupdocs.com/c/editor/20).