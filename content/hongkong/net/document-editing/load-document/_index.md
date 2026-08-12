---
date: 2026-04-20
description: 了解如何使用 GroupDocs.Editor for .NET 載入受密碼保護的文件，包括從檔案路徑、位元組串流以及資料庫載入。
keywords:
- load password protected document
- load document from stream
- load document from database
linktitle: 載入受密碼保護的文件
second_title: GroupDocs.Editor .NET API
title: 使用 GroupDocs.Editor .NET 載入受密碼保護的文件
type: docs
url: /zh-hant/net/document-editing/load-document/
weight: 13
---

# 使用 GroupDocs.Editor .NET 載入受密碼保護的文件

## 介紹
以程式方式編輯文件可能會讓人感到壓力，尤其是當你需要 **load password protected document** 檔案且這些檔案分散在不同位置時。無論檔案是儲存在磁碟、來自位元組串流，或存放於資料庫，GroupDocs.Editor for .NET 都提供乾淨且一致的 API 來處理所有情境。在本指南中，我們將說明前置條件、匯入必要的命名空間，並一步步示範如何使用各種方法載入文件——包括受密碼保護的特殊情況。

## 快速解答
- **GroupDocs.Editor 能開啟受密碼保護的檔案嗎？** 可以，使用設定了密碼的相應載入選項即可。  
- **支援哪些 .NET 版本？** .NET Framework 2.0 以上以及 .NET Core/5/6 均相容。  
- **是否需要釋放 Editor 物件？** 必須——呼叫 `Dispose()` 以釋放資源。  
- **可以從資料庫載入文件嗎？** 可以，將檔案以位元組陣列或串流方式取得，並傳入 `Editor` 建構函式。  
- **檔案大小有上限嗎？** 支援大型檔案；建議使用基於串流的載入方式並搭配記憶體最佳化選項。

## 什麼是「load password protected document」？
載入受密碼保護的文件是指開啟需要密碼才能存取的檔案，並以程式方式提供該密碼，使 API 能解密並處理內容。GroupDocs.Editor 透過載入選項抽象化解密步驟，使整個流程變得簡單。

## 為何使用 GroupDocs.Editor 載入文件？
- **統一的 API** – 相同程式碼即可處理 Word、Excel、PowerPoint 與 HTML 檔案。  
- **密碼處理** – 內建對加密檔案的支援，無需手動解密。  
- **串流彈性** – 可從檔案路徑、串流或任何自訂來源（如資料庫）載入。  
- **資源管理** – 簡易的 `Dispose()` 模式可降低記憶體使用量。

## 前置條件
在開始之前，請確保已設定以下前置條件：
- **Visual Studio** – 確認你的機器已安裝 Visual Studio。  
- **.NET Framework** – GroupDocs.Editor for .NET 支援 .NET Framework 2.0 以上。請確保你的專案目標為相容的框架。  
- **GroupDocs.Editor for .NET** – 從[下載頁面](https://releases.groupdocs.com/editor/net/)取得最新版本。  
- **C# 基礎知識** – 需要熟悉 C# 與 .NET 程式設計，才能跟隨本教學。

## 匯入命名空間
要開始使用 GroupDocs.Editor for .NET，必須在專案中匯入必要的命名空間。於 C# 檔案的頂部加入以下 using 陳述式：

```csharp
using GroupDocs.Editor.Options;
using System.IO;
```

這些命名空間將提供文件編輯所需的類別與方法。

## 步驟 1：從檔案路徑載入文件
從檔案路徑載入文件相當簡單。此方法適用於本機儲存的文件。

```csharp
string inputPath = "Your Sample Document";
// Load document as file via path and without load options
Editor editor1 = new Editor(inputPath);
// Dispose resources
editor1.Dispose();
System.Console.WriteLine("Document loaded successfully from file path.");
```

## 步驟 2：使用載入選項載入文件（受密碼保護的檔案）
有時候，你可能需要載入需要特殊處理的文件，例如受密碼保護的檔案。此時可使用載入選項。

```csharp
string inputPath = "Your Sample Document";
// Create load options for Word documents
WordProcessingLoadOptions wordLoadOptions = new WordProcessingLoadOptions();
wordLoadOptions.Password = "some password";
// Load document as file via path and with load options
Editor editor2 = new Editor(inputPath, delegate { return wordLoadOptions; });
// Dispose resources
editor2.Dispose();
System.Console.WriteLine("Password-protected document loaded successfully.");
```

## 如何從串流載入文件
從位元組串流載入文件在處理非檔案形式的文件時很有用，例如從資料庫或 Web 服務取得的文件。

```csharp
FileStream inputStream = File.OpenRead("Your Sample Document");
// Load document as content from byte stream and without load options
Editor editor3 = new Editor(delegate { return inputStream; });
// Dispose resources
editor3.Dispose();
System.Console.WriteLine("Document loaded successfully from byte stream.");
```

## 步驟 4：從位元組串流使用載入選項載入文件
對於需要特殊處理的位元組串流文件，可將串流載入與載入選項結合使用。

```csharp
FileStream inputStream = File.OpenRead("Your Sample Document");
// Create load options for spreadsheets
SpreadsheetLoadOptions sheetLoadOptions = new SpreadsheetLoadOptions();
sheetLoadOptions.OptimizeMemoryUsage = true;
// Load document as content from byte stream and with load options
Editor editor4 = new Editor(delegate { return inputStream; }, delegate { return sheetLoadOptions; });
// Dispose resources
editor4.Dispose();
System.Console.WriteLine("Spreadsheet document loaded successfully with load options.");
```

## 如何從資料庫載入文件
如果文件儲存在關聯式資料庫中，請取得二進位資料（例如使用 `SELECT FileData FROM Documents WHERE Id = @id`），並將取得的 `byte[]` 或 `MemoryStream` 傳入 `Editor` 建構函式，就像上述串流範例一樣。這樣可確保程式碼不論來源皆保持一致。

## 常見問題與解決方案
- **密碼錯誤** – 編輯器會拋出例外。請確認密碼值，並確保使用正確的載入選項類別對應檔案類型。  
- **串流已關閉** – 確保串流在 `Editor` 實例存活期間保持開啟，或將串流複製到 `MemoryStream`。  
- **大型檔案的記憶體消耗** – 使用 `SpreadsheetLoadOptions.OptimizeMemoryUsage = true`（如範例所示）或其他格式的等效選項以降低記憶體使用。

## 常見問答

**Q: GroupDocs.Editor for .NET 支援哪些檔案格式？**  
A: GroupDocs.Editor 支援多種檔案格式，包括 DOCX、XLSX、PPTX、HTML 等等。完整列表請參考[文件說明](https://tutorials.groupdocs.com/editor/net/)。

**Q: 如何處理受密碼保護的文件？**  
A: 可使用如 `WordProcessingLoadOptions` 等載入選項，在載入受密碼保護的文件時指定密碼。

**Q: 可以在 Web 應用程式中使用 GroupDocs.Editor 嗎？**  
A: 可以，GroupDocs.Editor 可用於 Web 應用程式。請妥善處理檔案串流與資源釋放，以避免記憶體洩漏。

**Q: 從哪裡可以取得 GroupDocs.Editor 的暫時授權？**  
A: 可從[暫時授權頁面](https://purchase.groupdocs.com/temporary-license/)取得暫時授權。

**Q: 若遇到問題是否有支援？**  
A: 有，GroupDocs 透過其[支援論壇](https://forum.groupdocs.com/c/editor/20)提供協助。

**Q: 從資料庫載入是否需要特殊設定？**  
A: 不需要，僅需取得二進位資料並以串流或位元組陣列傳入 `Editor` 建構函式即可。

**Q: 如何提升載入極大型試算表的效能？**  
A: 啟用記憶體最佳化選項，例如 `SpreadsheetLoadOptions.OptimizeMemoryUsage = true`，以減少記憶體佔用。

## 結論
恭喜！您已成功學會如何使用 GroupDocs.Editor for .NET 以各種方式 **load password protected document** 檔案。無論是本機檔案、受密碼保護的文件、位元組串流，或是儲存在資料庫的內容，GroupDocs.Editor 都提供彈性且強大的文件編輯解決方案。請務必記得釋放 `Editor` 實例，以確保應用程式效能與資源效率。

---

**最後更新：** 2026-04-20  
**測試環境：** GroupDocs.Editor 2.0 (latest)  
**作者：** GroupDocs