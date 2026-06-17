---
date: 2026-06-06
description: 了解如何使用 GroupDocs.Editor for .NET 列出支援的文件格式並判斷檔案格式副檔名。提供逐步指南、程式碼範例、快速解答與常見問題。
keywords:
- list supported document formats
- determine file format extension
- GroupDocs.Editor .NET
- document editing API
- supported formats guide
linktitle: 列出支援的文件格式
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to list supported document formats and determine file format
    extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets,
    quick answers, and FAQs.
  headline: List Supported Document Formats with GroupDocs.Editor .NET
  type: TechArticle
- description: Learn how to list supported document formats and determine file format
    extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets,
    quick answers, and FAQs.
  name: List Supported Document Formats with GroupDocs.Editor .NET
  steps:
  - name: '**.NET development environment** – Visual Studio 2022 or any IDE that supports
      .NET 6+.'
    text: '**.NET development environment** – Visual Studio 2022 or any IDE that supports
      .NET 6+.'
  - name: '**GroupDocs.Editor for .NET library** – download from the [GroupDocs releases
      page](https://releases.groupdocs.com/editor/net/).'
    text: '**GroupDocs.Editor for .NET library** – download from the [GroupDocs releases
      page](https://releases.groupdocs.com/editor/net/).'
  - name: '**Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/)
      for unrestricted access.'
    text: '**Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/)
      for unrestricted access.'
  - name: '**Basic C# knowledge** – familiarity with namespaces, `using` statements,
      and console output.'
    text: '**Basic C# knowledge** – familiarity with namespaces, `using` statements,
      and console output.'
  - name: '**Loop Through Formats:** We iterate over all available Word‑processing
      formats.'
    text: '**Loop Through Formats:** We iterate over all available Word‑processing
      formats.'
  - name: '**Output Format Details:** For each format we print its friendly name and
      default file extension.'
    text: '**Output Format Details:** For each format we print its friendly name and
      default file extension.'
  - name: '**Loop Through Formats:** The same looping logic applies to presentations.'
    text: '**Loop Through Formats:** The same looping logic applies to presentations.'
  - name: '**Output Format Details:** The name and extension are displayed for each
      format.'
    text: '**Output Format Details:** The name and extension are displayed for each
      format.'
  - name: '**Parse Format:** `FromExtension` converts the `.xlsm` extension into its
      internal `SpreadsheetFormat` enum.'
    text: '**Parse Format:** `FromExtension` converts the `.xlsm` extension into its
      internal `SpreadsheetFormat` enum.'
  - name: '**Output Format:** The parsed format’s name is printed, confirming the
      mapping.'
    text: '**Output Format:** The parsed format’s name is printed, confirming the
      mapping.'
  type: HowTo
- questions:
  - answer: '`DocumentFormatInfo` provides metadata about supported file types, while
      `SaveOptions` configures how a document is written back to disk (format, compression,
      etc.).'
    question: What is the difference between `DocumentFormatInfo` and `SaveOptions`?
  - answer: Yes—use `DocumentFormatInfo.FromExtension("yourExt")`; if the extension
      isn’t recognized, the method returns `null`.
    question: Can I list formats for a custom file extension?
  - answer: Absolutely. Pass the password to the `Editor` constructor via `EditorSettings`
      to open encrypted documents.
    question: Does GroupDocs.Editor support password‑protected files?
  - answer: Over **30 input and output formats**, spanning Word, Excel, PowerPoint,
      HTML, and plain text.
    question: How many formats does GroupDocs.Editor actually support?
  - answer: Use the `GetEditableWordProcessingFormats()` (or Spreadsheet/Presentation
      equivalents) to retrieve formats that allow full edit capabilities.
    question: Is there a way to restrict the list to only editable formats?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: 使用 GroupDocs.Editor .NET 列出支援的文件格式
type: docs
url: /zh-hant/net/document-processing/work-document-formats/
weight: 13
---

# 列出支援的文件格式

歡迎閱讀我們關於 **如何列出支援的文件格式** 的完整教學，使用 GroupDocs.Editor for .NET。無論您是構建以文件為中心的網頁應用程式，還是企業級桌面工具，精確了解可以編輯或轉換的格式都是必須的。在本指南中，您將學會如何列舉格式、解析副檔名，並編輯文件——全部以清晰、易於理解的說明和可直接執行的程式碼片段呈現。

## 快速回答
- **如何列出所有支援的格式？** 使用 `DocumentFormatInfo.GetSupportedWordProcessingFormats()`（或 Presentation/Spreadsheet 等效方法）並遍歷集合。  
- **我可以從檔案副檔名判斷格式嗎？** 可以——呼叫 `DocumentFormatInfo.FromExtension(".docx")`。  
- **GroupDocs.Editor 支援哪些檔案類型？** 超過 30 種輸入與輸出格式，包括 DOCX、XLSX、PPTX、HTML 以及純文字。  
- **列出格式需要授權嗎？** 臨時授權可解鎖完整 API；否則試用版僅提供有限功能。  
- **相容的 .NET 版本有哪些？** .NET Framework 4.6+、.NET Core 3.1+、.NET 5/6/7。

## 什麼是「列出支援的文件格式」？
此詞語指以程式方式取得 GroupDocs.Editor 能開啟、編輯與儲存的檔案類型集合。此操作可讓您建立動態 UI 下拉選單或在處理前驗證使用者上傳的檔案，確保僅將相容的檔案傳遞給編輯器進行後續操作。

## 為什麼要列出支援的文件格式？
GroupDocs.Editor **支援超過 30 種輸入與輸出格式**，且可處理高達 **2 GB** 的檔案，而無需將整個文件載入記憶體。了解確切的格式清單可防止執行時錯誤、提升使用者體驗，並讓您能實施如「僅允許可編輯的 Office 文件」等業務規則。它同時協助您只向使用者顯示應用程式實際支援的格式。

## 前置條件
1. **.NET 開發環境** – Visual Studio 2022 或任何支援 .NET 6+ 的 IDE。  
2. **GroupDocs.Editor for .NET 程式庫** – 從 [GroupDocs releases page](https://releases.groupdocs.com/editor/net/) 下載。  
3. **臨時授權** – 取得 [temporary license](https://purchase.groupdocs.com/temporary-license/) 以獲得完整存取權限。  
4. **基本 C# 知識** – 熟悉命名空間、`using` 陳述式與主控台輸出。

## 如何列出支援的文件格式？
載入支援的格式集合，並印出每個格式的名稱與副檔名。此兩步驟模式適用於文字處理、試算表與簡報文件。透過遍歷集合，您可以動態填充 UI 元件（如下拉選單），確保使用者只能選取編輯器實際能處理的格式。

```csharp
// No actual code block – placeholder retained from original tutorial
```csharp
using System;
using GroupDocs.Editor.Options;
```
```

### 列出文字處理格式
`Formats.WordProcessingFormats` 是一個列舉，描述編輯器所識別的每種文字處理檔案類型。`All` 屬性會回傳這些格式物件的集合。

```csharp
```csharp
foreach (Formats.WordProcessingFormats oneFormat in Formats.WordProcessingFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**說明：**  
1. **遍歷格式：** 我們遍歷所有可用的文字處理格式。  
2. **輸出格式細節：** 對每個格式，我們印出其友好名稱與預設副檔名。

### 列出簡報格式
`Formats.PresentationFormats` 以相同方式處理投影片檔案，透過 `All` 集合揭示每種支援的簡報類型。

```csharp
```csharp
foreach (Formats.PresentationFormats oneFormat in Formats.PresentationFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**說明：**  
1. **遍歷格式：** 相同的遍歷邏輯適用於簡報。  
2. **輸出格式細節：** 每個格式的名稱與副檔名皆會顯示。

## 如何判斷檔案格式副檔名？
有時您只有檔名，需要推斷相應的 `DocumentFormat`。GroupDocs.Editor 提供簡單的靜態輔助方法，將檔案副檔名映射到內部格式表示，讓您在載入編輯器前驗證或轉換檔案。

### 解析試算表格式
`Formats.SpreadsheetFormats.FromExtension` 會將檔案副檔名字串轉換為相對應的試算表格式列舉值。

```csharp
```csharp
Formats.SpreadsheetFormats expectedXlsm = Formats.SpreadsheetFormats.FromExtension(".xlsm");
Console.WriteLine("Parsed Spreadsheet format is {0}", expectedXlsm.Name);
```
```

**說明：**  
1. **解析格式：** `FromExtension` 將 `.xlsm` 副檔名轉換為其內部的 `SpreadsheetFormat` 列舉。  
2. **輸出格式：** 印出解析後的格式名稱，以確認映射正確。

### 解析文字格式
同樣地，`Formats.TextualFormats.FromExtension` 解析文字檔案的副檔名，例如 HTML 或 TXT。

```csharp
```csharp
Formats.TextualFormats expectedHtml = Formats.TextualFormats.FromExtension("html");
Console.WriteLine("Parsed Textual format is {0}", expectedHtml.Name);
```
```

**說明：**  
1. **解析格式：** `FromExtension` 方法將 `html` 副檔名解析為 `TextFormat`。  
2. **輸出格式：** 顯示文字格式的名稱，對於基於網頁的編輯器很有用。

## 確認格式後如何編輯文件？
一旦知道格式，載入與編輯文件遵循一致的模式。首先以來源檔案路徑建立 `Editor` 實例，然後呼叫 `Edit()` 取得 `EditableDocument`。接著您可以讀取、修改，最後使用相應的 `SaveOptions` 儲存內容。

### 載入文件
`Editor` 是封裝特定檔案所有編輯操作的核心類別。

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/document.docx"))
{
    // Further steps will be covered here.
}
```
```

**說明：**  
1. **初始化 Editor：** 建立 `Editor` 實例，傳入目標檔案的完整路徑。  
2. **釋放模式：** `using` 陳述式確保所有非受控資源即時釋放。

### 取得內容
`EditableDocument.GetContent()` 會回傳文件的原始文字（或對於基於網頁的編輯器則為 HTML），您可以顯示或操作它。

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    string content = editableDocument.GetContent();
    Console.WriteLine(content);
}
```
```

**說明：**  
1. **Edit 方法：** `Edit()` 回傳 `EditableDocument` 物件。  
2. **取得內容：** `GetContent()` 取得文件的原始文字（或對於基於網頁的編輯器則為 HTML）。  
3. **輸出內容：** 將內容寫入主控台以供驗證。

### 儲存變更
`SaveOptions` 告訴編輯器如何以及以何種格式將編輯後的文件寫回儲存。

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    // Modify content here
    SaveOptions saveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docx);
    editor.Save(editableDocument, "path/to/save/document.docx", saveOptions);
}
```
```

**說明：**  
1. **Edit 方法：** 在修改後重新取得 `EditableDocument`。  
2. **修改內容：** 對字串套用變更（此處未示範）。  
3. **儲存選項：** 使用所需的輸出格式設定 `SaveOptions`。  
4. **儲存文件：** 將編輯後的檔案寫回磁碟。

## 如何處理不同類型的文件？
GroupDocs.Editor 把 Word、試算表與簡報的處理抽象為相同的 API 介面，讓您無需為每種文件族群學習新類別，即可輕鬆切換使用情境。

### 編輯試算表文件
`SpreadsheetSaveOptions` 定義試算表的寫入方式，包括格式與可選的壓縮設定。

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/spreadsheet.xlsx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // Modify content here
        SaveOptions saveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsx);
        editor.Save(editableDocument, "path/to/save/spreadsheet.xlsx", saveOptions);
    }
}
```
```

**說明：**  
1. **初始化 Editor：** 將試算表檔案路徑傳入 `Editor` 建構函式。  
2. **Edit 方法：** 取得 `EditableDocument`。  
3. **取得內容：** 印出試算表的 CSV 表示（或 HTML）。  
4. **修改內容：** 套用您需要的儲存格層級變更。  
5. **儲存選項：** 選擇適當的 `SpreadsheetSaveOptions`。  
6. **儲存文件：** 將更新後的試算表寫回儲存。

### 編輯簡報文件
`PresentationSaveOptions` 控制投影片的輸出格式，讓您可以保留或變更原始檔案類型。

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/presentation.pptx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // Modify content here
        SaveOptions saveOptions = new PresentationSaveOptions(PresentationFormats.Pptx);
        editor.Save(editableDocument, "path/to/save/presentation.pptx", saveOptions);
    }
}
```
```

**說明：**  
1. **初始化 Editor：** 透過 `Editor` 載入 PowerPoint 檔案。  
2. **Edit 方法：** 取得 `EditableDocument`。  
3. **取得內容：** 抽取投影片的 HTML 或純文字。  
4. **修改內容：** 更新標題、項目符號或圖片。  
5. **儲存選項：** 使用 `PresentationSaveOptions` 定義輸出格式。  
6. **儲存文件：** 將編輯後的簡報儲存。

## 常見問題與解決方案
- **「不支援的格式」錯誤：** 確認您使用的是最新的 GroupDocs.Editor 版本；它會定期加入對新 Office 格式的支援。  
- **大型檔案記憶體消耗：** 在載入文件前將 `EditorSettings.EnableStreaming = true` 以啟用串流模式。  
- **授權未套用：** 確認臨時授權檔案放置於應用程式根目錄，或透過 `License license = new License(); license.SetLicense("path/to/license.lic");` 載入。

## 常見問答

**Q: `DocumentFormatInfo` 與 `SaveOptions` 有何差異？**  
A: `DocumentFormatInfo` 提供支援檔案類型的中繼資料，而 `SaveOptions` 設定文件寫回磁碟的方式（格式、壓縮等）。

**Q: 我可以列出自訂副檔名的格式嗎？**  
A: 可以——使用 `DocumentFormatInfo.FromExtension("yourExt")`；若副檔名未被識別，該方法會回傳 `null`。

**Q: GroupDocs.Editor 支援受密碼保護的檔案嗎？**  
A: 當然支援。透過 `EditorSettings` 將密碼傳入 `Editor` 建構函式，即可開啟加密文件。

**Q: GroupDocs.Editor 實際支援多少種格式？**  
A: 超過 **30 種輸入與輸出格式**，涵蓋 Word、Excel、PowerPoint、HTML 與純文字。

**Q: 有沒有方法將清單限制為僅可編輯的格式？**  
A: 使用 `GetEditableWordProcessingFormats()`（或 Spreadsheet/Presentation 等效方法）取得允許完整編輯功能的格式。

## 其他資源
- 從 [GroupDocs releases page](https://releases.groupdocs.com/editor/net/) 下載程式庫。  
- 取得 [temporary license](https://purchase.groupdocs.com/temporary-license/) 以獲得完整功能存取。  
- 透過 [free trial](https://releases.groupdocs.com/) 試用產品。  
- 在 [GroupDocs.Editor documentation](https://tutorials.groupdocs.com/editor/net/) 中探索詳細使用範例。  
- 在 [support forum](https://forum.groupdocs.com/c/editor/20) 上向社群尋求協助。

## 結論
透過本指南，您現在已了解如何 **列出支援的文件格式**、**從副檔名判斷檔案格式**，以及使用 GroupDocs.Editor for .NET **編輯 Word、試算表與簡報類型的文件**。將這些程式碼片段整合至您的專案，以打造具備格式感知的穩健應用程式，提升終端使用者體驗並減少執行時錯誤。

---

**最後更新：** 2026-06-06  
**測試環境：** GroupDocs.Editor 23.9 for .NET  
**作者：** GroupDocs

## 相關教學

- [精通 .NET 中的文件載入（使用 GroupDocs.Editor）：完整指南](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)
- [精通 .NET 中的文件編輯（使用 GroupDocs.Editor）：完整指南](/editor/net/document-editing/master-document-editing-dotnet-groupdocs-editor/)
- [使用 GroupDocs.Editor .NET 將 Word 轉換為 HTML：一步步指南](/editor/net/document-saving/convert-word-to-html-groupdocs-editor-dotnet/)