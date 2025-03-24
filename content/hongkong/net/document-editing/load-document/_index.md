---
title: 載入文檔
linktitle: 載入文檔
second_title: GroupDocs.Editor .NET API
description: 了解如何使用 GroupDocs.Editor for .NET 以程式設計方式編輯文件。載入文件、處理受密碼保護的文件等的逐步指南。
weight: 13
url: /zh-hant/net/document-editing/load-document/
---

# 載入文檔

## 介紹
以程式設計方式編輯文件可能是一項艱鉅的任務，特別是當您處理不同的文件格式和複雜的結構時。幸運的是，GroupDocs.Editor for .NET 讓這項任務變得輕而易舉，它提供了強大且易於使用的 API，用於編輯各種文件類型。在本教程中，我們將引導您完成開始使用 GroupDocs.Editor for .NET 所需的一切，包括先決條件、如何匯入命名空間以及使用各種方法載入文件的詳細逐步指南。
## 先決條件
在我們深入之前，請確保您已設定以下先決條件：
- Visual Studio：確保您的電腦上安裝了 Visual Studio。
- .NET Framework：GroupDocs.Editor for .NET 支援 .NET Framework 2.0 或更高版本。確保您的專案針對相容的框架。
-  GroupDocs.Editor for .NET：從以下位置下載最新版本[下載頁面](https://releases.groupdocs.com/editor/net/).
- C# 基礎：要學習本教程，需要熟悉 C# 和 .NET 程式設計。
## 導入命名空間
要開始使用 GroupDocs.Editor for .NET，您需要將必要的命名空間匯入到您的專案中。在 C# 檔案頂部新增以下 using 指令：
```csharp
using GroupDocs.Editor.Options;
using System.IO;
```
這些命名空間將提供對文件編輯任務所需的類別和方法的存取。
## 第 1 步：從文件路徑載入文檔
從文件路徑載入文件非常簡單。此方法非常適合儲存在電腦本機的文件。

```csharp
string inputPath = "Your Sample Document";
//透過路徑將文件載入為文件且不含載入選項
Editor editor1 = new Editor(inputPath);
//處置資源
editor1.Dispose();
System.Console.WriteLine("Document loaded successfully from file path.");
```
## 步驟 2：使用載入選項載入文檔
有時，您可能需要載入需要特殊處理的文檔，例如受密碼保護的文件。在這種情況下，您可以使用載入選項。

```csharp
string inputPath = "Your Sample Document";
//為 Word 文件建立載入選項
WordProcessingLoadOptions wordLoadOptions = new WordProcessingLoadOptions();
wordLoadOptions.Password = "some password";
//透過路徑和載入選項將文件載入為文件
Editor editor2 = new Editor(inputPath, delegate { return wordLoadOptions; });
//處置資源
editor2.Dispose();
System.Console.WriteLine("Password-protected document loaded successfully.");
```
## 第 3 步：從位元組流載入文檔
當您需要處理未儲存為文件的文件（例如從資料庫或 Web 服務檢索的文件）時，從位元組流載入文件非常有用。

```csharp
FileStream inputStream = File.OpenRead("Your Sample Document");
//將文件作為位元組流的內容加載，並且不帶加載選項
Editor editor3 = new Editor(delegate { return inputStream; });
//處置資源
editor3.Dispose();
System.Console.WriteLine("Document loaded successfully from byte stream.");
```
## 步驟 4：從位元組流載入帶有載入選項的文檔
對於從位元組流載入時需要特殊處理的文檔，您可以將位元組流載入與載入選項結合。

```csharp
FileStream inputStream = File.OpenRead("Your Sample Document");
//建立電子表格的載入選項
SpreadsheetLoadOptions sheetLoadOptions = new SpreadsheetLoadOptions();
sheetLoadOptions.OptimizeMemoryUsage = true;
//將文件作為位元組流的內容並使用載入選項加載
Editor editor4 = new Editor(delegate { return inputStream; }, delegate { return sheetLoadOptions; });
//處置資源
editor4.Dispose();
System.Console.WriteLine("Spreadsheet document loaded successfully with load options.");
```
## 結論
恭喜！您已經成功學習如何使用 GroupDocs.Editor for .NET 以各種方式載入文件。無論您是處理本機檔案、受密碼保護的文件還是位元組流，GroupDocs.Editor 都能為您的文件編輯需求提供靈活且強大的解決方案。請記住始終處置資源，以確保應用程式中的最佳效能和資源管理。
## 常見問題解答
### GroupDocs.Editor for .NET 支援哪些檔案格式？
 GroupDocs.Editor 支援多種檔案格式，包括 DOCX、XLSX、PPTX、HTML 等。如需完整列表，請參閱[文件](https://tutorials.groupdocs.com/editor/net/).
### 如何處理受密碼保護的文件？
您可以使用載入選項，例如`WordProcessingLoadOptions`載入受密碼保護的文件時指定密碼。
### 我可以在 Web 應用程式中使用 GroupDocs.Editor 嗎？
是的，GroupDocs.Editor 可以在 Web 應用程式中使用。確保正確處理文件流和資源處置以避免記憶體洩漏。
### 在哪裡可以獲得 GroupDocs.Editor 的臨時授權？
您可以從以下機構獲得臨時許可證[臨時許可證頁面](https://purchase.groupdocs.com/temporary-license/).
### 如果我遇到問題可以獲得支援嗎？
是的，GroupDocs 透過他們的[支援論壇](https://forum.groupdocs.com/c/editor/20).