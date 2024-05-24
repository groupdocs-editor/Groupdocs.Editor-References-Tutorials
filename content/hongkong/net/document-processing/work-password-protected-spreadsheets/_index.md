---
title: 使用受密碼保護的電子表格
linktitle: 使用受密碼保護的電子表格
second_title: GroupDocs.Editor .NET API
description: 了解如何使用 GroupDocs.Editor for .NET 處理受密碼保護的電子表格。本詳細指南將引導您完成開啟和儲存安全 Excel 檔案的過程。
type: docs
weight: 18
url: /zh-hant/net/document-processing/work-password-protected-spreadsheets/
---
## 介紹
您是否正在努力管理 .NET 應用程式中受密碼保護的電子表格？如果是這樣，那麼您來對地方了！在本綜合指南中，我們將引導您完成使用 GroupDocs.Editor for .NET 高效處理受密碼保護的電子表格的過程。學完本教學後，您將能夠輕鬆開啟、編輯和儲存加密的 Excel 檔案。
## 先決條件
在深入研究程式碼之前，讓我們確保您擁有遵循所需的一切：
- C# 基礎知識：本教學假設您熟悉 C# 程式設計。
- .NET Framework：確保您的開發電腦上安裝了 .NET Framework。
-  GroupDocs.Editor for .NET：從以下位置下載並安裝 GroupDocs.Editor for .NET[這裡](https://releases.groupdocs.com/editor/net/).
## 導入命名空間
首先，您需要在 C# 專案中匯入必要的命名空間。這些命名空間提供對 GroupDocs.Editor 功能的存取。
```csharp
using System;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
## 第 1 步：取得輸入檔的路徑
首先，您需要輸入檔案的路徑。對於本範例，我們將使用範例 Excel 檔案 (`Your Sample Document`）受密碼保護。
```csharp
string inputFilePath = "Your Sample Document";
```
## 步驟 2：嘗試在沒有密碼的情況下開啟文檔
讓我們看看如果我們嘗試在不提供密碼的情況下開啟文件會發生什麼。
```csharp
Editor editor = new Editor(inputFilePath);
try
{
    editor.Edit();
}
catch (GroupDocs.Editor.PasswordRequiredException)
{
    Console.WriteLine("Cannot edit the document because it is password-protected. A password is required.");
}
editor.Dispose();
```
## 步驟 3：嘗試指定不正確的密碼
現在，我們將指定一個不正確的密碼來示範編輯器如何回應。
```csharp
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.Password = "incorrect_password";
editor = new Editor(inputFilePath, delegate { return loadOptions; });
try
{
    editor.Edit();
}
catch (GroupDocs.Editor.IncorrectPasswordException)
{
    Console.WriteLine("Cannot edit the document because the specified password is incorrect.");
}
editor.Dispose();
```
## 步驟 4：使用正確的密碼開啟文件
讓我們提供正確的密碼並成功開啟檔案。
```csharp
loadOptions.Password = "excel_password";
loadOptions.OptimizeMemoryUsage = true;
editor = new Editor(inputFilePath, delegate { return loadOptions; });
```
## 第 5 步：建立和調整編輯選項
要編輯電子表格，我們需要建立和調整編輯選項。
```csharp
SpreadsheetEditOptions editOptions = new SpreadsheetEditOptions();
```
## 第 6 步：建立中間可編輯文檔
接下來，我們建立一個中間體`EditableDocument`這使我們能夠對電子表格進行更改。
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
{
    //第 7 步：建立儲存選項
    SpreadsheetFormats xlsmFormat = SpreadsheetFormats.Xlsm;
    SpreadsheetSaveOptions saveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
    //步驟7.1：設定新的開啟密碼
    saveOptions.Password = "new password";
    //步驟7.2：設定寫入保護
    saveOptions.WorksheetProtection = new WorksheetProtection(WorksheetProtectionType.All, "write password");
    //步驟 8：儲存文件而不進行修改
    //步驟 8.1：準備輸出檔名和路徑
    string outputFilename = Path.GetFileNameWithoutExtension(inputFilePath) + "." + xlsmFormat.Extension;
    string outputPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename);
    //步驟8.2：建立輸出流
    using (FileStream outputStream = File.Create(outputPath))
    {
        //步驟 8.3：保存
        editor.Save(beforeEdit, outputStream, saveOptions);
    }
}
//第 9 步：處置編輯器實例
editor.Dispose();
Console.WriteLine("Successfully handled the password-protected spreadsheet. Editor instance has been disposed: {0}", editor.IsDisposed ? "Yes" : "No");
```
## 結論
恭喜！您已成功學習如何使用 GroupDocs.Editor for .NET 處理受密碼保護的電子表格。從嘗試在沒有密碼的情況下開啟文檔到使用新的保護設定儲存文檔，您已經涵蓋了所有基本步驟。這些知識無疑將增強您在 .NET 應用程式中管理安全文件的能力。
## 常見問題解答
### 什麼是 .NET 的 GroupDocs.Editor？
GroupDocs.Editor for .NET 是一個功能強大的文件編輯 API，可讓開發人員在 .NET 應用程式中載入、編輯和儲存各種文件格式。
### 如何取得 GroupDocs.Editor 的臨時授權？
您可以從以下地址取得臨時許可證[這裡](https://purchase.groupdocs.com/temporary-license/)來評估產品的功能。
### 編輯大型文檔時是否可以優化記憶體使用？
是的，您可以透過設定啟用記憶體優化`OptimizeMemoryUsage`財產給`true`在載入選項中。
### 我可以為開啟和寫入電子表格設定不同的密碼嗎？
絕對地！您可以使用儲存選項設定單獨的密碼來開啟文件和寫入保護。
### 在哪裡可以找到更詳細的文件？
您可以存取 GroupDocs.Editor for .NET 的綜合文檔[這裡](https://reference.groupdocs.com/editor/net/).