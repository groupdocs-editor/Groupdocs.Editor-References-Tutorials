---
title: 使用多選項卡電子表格
linktitle: 使用多選項卡電子表格
second_title: GroupDocs.Editor .NET API
description: 了解如何使用 GroupDocs.Editor 在 .NET 中處理多選項卡電子表格。包含逐步指南、程式碼範例和最佳實務。
weight: 17
url: /zh-hant/net/document-processing/work-multi-tab-spreadsheets/
type: docs
---
# 使用多選項卡電子表格

## 介紹
處理多選項卡電子表格可能是一項艱鉅的任務，尤其是當您需要從同一文件中的不同工作表操作或提取資料時。如果您正在使用 .NET 並尋找強大的解決方案，那麼適用於 .NET 的 GroupDocs.Editor 是一個絕佳的選擇。在本教程中，我們將引導您完成使用 GroupDocs.Editor for .NET 處理多選項卡電子表格的過程。我們將涵蓋從設定環境到將每個選項卡保存為單獨文件的所有內容。
## 先決條件
在深入學習本教程之前，請確保您具備以下先決條件：
1. Visual Studio：確保您的電腦上安裝了 Visual Studio。
2. .NET Framework：.NET 的 GroupDocs.Editor 支援 .NET Framework 4.0 或更高版本。
3. GroupDocs.Editor for .NET：下載並安裝 GroupDocs.Editor for .NET 程式庫。您可以從[下載頁面](https://releases.groupdocs.com/editor/net/).
4. 許可證：雖然您可以使用[臨時執照](https://purchase.groupdocs.com/temporary-license/)要試用該庫，建議購買用於生產用途的完整許可證。
## 導入命名空間
在開始編碼之前，您需要匯入必要的名稱空間。將以下 using 指令加入 .cs 檔案的頂部：
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
## 1. 取得輸入檔的路徑
首先，您需要指定輸入電子表格檔案的路徑。該檔案應該是具有多個選項卡的 XLSX (OOXML)。
```csharp
string inputFilePath = "Your Sample Document";
```
## 2. 將電子表格載入到編輯器實例中
接下來，您將電子表格加載到`Editor`實例。這是使用文件流並為電子表格指定適當的載入選項來完成的。
```csharp
using (FileStream inputStream = File.OpenRead(inputFilePath))
{
    using (Editor editor = new Editor(delegate { return inputStream; }, delegate { return new SpreadsheetLoadOptions(); }))
    {
        //進一步的步驟將在此處進行
    }
}
```
## 3. 從第一個選項卡建立可編輯文檔
要編輯或操作特定選項卡，您需要建立一個`EditableDocument`該選項卡的實例。此選項卡是使用基於 0 的索引指定的。
```csharp
SpreadsheetEditOptions editOptions1 = new SpreadsheetEditOptions();
editOptions1.WorksheetIndex = 0; //第一個選項卡
EditableDocument firstTabBeforeEdit = editor.Edit(editOptions1);
```
## 4. 從第二個標籤建立可編輯文檔
同樣，創建一個`EditableDocument`對於第二個選項卡。
```csharp
SpreadsheetEditOptions editOptions2 = new SpreadsheetEditOptions();
editOptions2.WorksheetIndex = 1; //第二個選項卡
EditableDocument secondTabBeforeEdit = editor.Edit(editOptions2);
```
## 5. 將第一個選項卡儲存到單獨的文件中
現在，將第一個選項卡另存為單獨的文檔。指定儲存格式和輸出路徑。
```csharp
SpreadsheetSaveOptions saveOptions1 = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
string outputFilename1 = Path.GetFileNameWithoutExtension(inputFilePath) + "_tab1.xlsm";
string outputPath1 = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename1);
editor.Save(firstTabBeforeEdit, outputPath1, saveOptions1);
```
## 6. 將第二個選項卡儲存到單獨的文件中
對第二個選項卡重複此過程，但這次以不同的格式儲存。
```csharp
SpreadsheetSaveOptions saveOptions2 = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsb);
string outputFilename2 = Path.GetFileNameWithoutExtension(inputFilePath) + "_tab2.xlsb";
string outputPath2 = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename2);
editor.Save(secondTabBeforeEdit, outputPath2, saveOptions2);
```
## 7. 處理 EditableDocument 實例
最後，確保您正確處置`EditableDocument`實例以釋放資源。
```csharp
firstTabBeforeEdit.Dispose();
secondTabBeforeEdit.Dispose();
```

## 結論
透過執行以下步驟，您可以使用 GroupDocs.Editor 在 .NET 中輕鬆處理多選項卡電子表格。這個功能強大的庫簡化了在電子表格中編輯和保存不同工作表的過程，使您的開發任務更易於管理。無論您要處理複雜的資料操作還是簡單的編輯，GroupDocs.Editor for .NET 都能提供您高效完成工作所需的工具。
## 常見問題解答
### 什麼是 .NET 的 GroupDocs.Editor？
GroupDocs.Editor for .NET 是一個功能強大的文件編輯 API，允許開發人員在 .NET 應用程式中載入、編輯和保存各種格式的文件。
### 我可以在購買之前嘗試適用於 .NET 的 GroupDocs.Editor 嗎？
是的，您可以使用[免費試用](https://releases.groupdocs.com/)或請求[臨時執照](https://purchase.groupdocs.com/temporary-license/)來評估產品。
### GroupDocs.Editor for .NET 支援哪些檔案格式？
GroupDocs.Editor 支援多種格式，包括 DOCX、XLSX、PPTX、PDF 等。
### 如何獲得對 GroupDocs.Editor for .NET 的支援？
您可以透過訪問獲得支持[支援論壇](https://forum.groupdocs.com/c/editor/20).
### 哪裡可以購買 GroupDocs.Editor for .NET 的完整授權？
您可以從以下位置購買完整許可證[購買頁面](https://purchase.groupdocs.com/buy).