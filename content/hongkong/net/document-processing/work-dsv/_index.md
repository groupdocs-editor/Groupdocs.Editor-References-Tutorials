---
title: 使用分隔分隔值 (DSV)
linktitle: 使用分隔分隔值 (DSV)
second_title: GroupDocs.Editor .NET API
description: 透過此逐步指南，了解如何使用 GroupDocs.Editor for .NET 編輯 CSV 和 TSV 檔案。輕鬆改進您的 .NET 專案。
weight: 12
url: /zh-hant/net/document-processing/work-dsv/
---
## 介紹
如果您是使用 CSV 或 TSV 檔案等分隔分隔值 (DSV) 的開發人員，您就會知道以程式方式編輯這些檔案可能是一項艱鉅的任務。然而，使用 GroupDocs.Editor for .NET，這項任務變得更加簡單和有效率。在本教程中，我們將引導您了解如何使用 GroupDocs.Editor for .NET 讀取、編輯和儲存 DSV 檔案。我們將把這個過程分解為易於遵循的步驟，讓您可以在專案中輕鬆實施。
## 先決條件
在我們深入學習本教程之前，請確保您具備以下先決條件：
- Visual Studio：確保您的電腦上安裝了 Visual Studio。
-  GroupDocs.Editor for .NET：您需要下載並參考 GroupDocs.Editor for .NET 程式庫。你可以下載它[這裡](https://releases.groupdocs.com/editor/net/).
- 對 C# 的基本了解：本教學假設您對 C# 和 .NET 開發有基本的了解。
## 導入命名空間
首先，您需要在專案中匯入必要的命名空間。這些命名空間提供使用 GroupDocs.Editor for .NET 所需的類別和方法。
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

## 第 1 步：取得輸入 DSV 檔案的路徑
首先，您需要指定輸入 DSV 檔案的路徑。對於此範例，我們假設它是 CSV 檔案。
```csharp
string inputFilePath = "Your Sample Document";
```
## 步驟2：建立編輯器實例
建立一個實例`Editor`班級。該實例將用於載入和操作 DSV 檔案。
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## 第 3 步：建立 DSV 編輯選項
接下來，建立一個實例`DelimitedTextEditOptions`並指定 DSV 檔案的分隔符號。在這裡，我們使用逗號作為分隔符號。
```csharp
    Options.DelimitedTextEditOptions editOptions = new DelimitedTextEditOptions(",");
    editOptions.ConvertDateTimeData = false;
    editOptions.ConvertNumericData = true;
    editOptions.TreatConsecutiveDelimitersAsOne = true;
```
## 步驟 4：建立一個 EditableDocument 實例
創建一個`EditableDocument`實例使用`Editor.Edit`方法。這將為編輯文件做好準備。
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## 步驟5：編輯文檔內容
檢索原始文字內容並進行必要的修改。出於演示目的，讓我們替換一些文字。
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("SsangYong", "Chevrolet").Replace("Kyron", "Camaro");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## 步驟 6：建立包含更新內容的 EditableDocument
創建一個新的`EditableDocument`與更新的內容。
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## 第 7 步：建立 CSV 儲存選項
指定 CSV 格式的儲存選項，包括分隔符號和編碼。
```csharp
    Options.DelimitedTextSaveOptions csvSaveOptions = new DelimitedTextSaveOptions(",");
    csvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## 第 8 步：建立 TSV 儲存選項
同樣，指定 TSV 格式的儲存選項。
```csharp
    Options.DelimitedTextSaveOptions tsvSaveOptions = new DelimitedTextSaveOptions("\t");
    tsvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## 第 9 步：建立電子表格儲存選項
如果需要將文件儲存為電子表格，請建立對應的儲存選項。
```csharp
    Options.SpreadsheetSaveOptions cellsSaveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
```
## 第10步：準備保存路徑
定義編輯文件的儲存路徑。
```csharp
    string outputCsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".csv");
    string outputTsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".tsv");
    string outputCellsPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".xlsm");
```
## 第11步：儲存編輯後的文檔
將編輯後的文件以不同格式儲存到指定路徑。
```csharp
    editor.Save(afterEdit, outputCsvPath, csvSaveOptions);
    editor.Save(afterEdit, outputTsvPath, tsvSaveOptions);
    editor.Save(afterEdit, outputCellsPath, cellsSaveOptions);
```
## 第 12 步：處置 EditableDocument 實例
最後，請務必處理掉`EditableDocument`實例以釋放資源。
```csharp
    beforeEdit.Dispose();
    afterEdit.Dispose();
}
System.Console.WriteLine("WorkingWithDsv routine has successfully finished");
```
## 結論
使用 GroupDocs.Editor for .NET 編輯 DSV 檔案是一個簡單的過程，涉及建立編輯器實例、設定編輯選項、修改內容和儲存變更。本逐步指南應可協助您輕鬆將此功能整合到您的 .NET 應用程式中。無論您使用的是 CSV、TSV 或其他 DSV 格式，GroupDocs.Editor for .NET 都能提供強大且靈活的解決方案。
## 常見問題解答
### 我可以使用 GroupDocs.Editor for .NET 編輯大型 CSV 檔案嗎？
是的，GroupDocs.Editor for .NET 能夠有效處理大型 CSV 檔案。
### 除 CSV 和 TSV 之外，GroupDocs.Editor for .NET 是否支援其他 DSV 格式？
是的，只要指定適當的分隔符，它就支援各種 DSV 格式。
### 儲存DSV檔案時可以自訂編碼嗎？
當然，您可以在儲存選項中指定所需的編碼。
### 我可以使用 GroupDocs.Editor for .NET 將 CSV 檔案轉換為 Excel 電子表格嗎？
是的，您可以使用適當的儲存選項將 CSV 檔案儲存為 Excel 電子表格。
### 在哪裡可以找到更多關於 GroupDocs.Editor for .NET 的文件？
你可以找到詳細的文檔[這裡](https://tutorials.groupdocs.com/editor/net/)