---
date: 2026-06-06
description: 了解如何使用 GroupDocs.Editor for .NET 從 CSV 與 TSV 檔案 **create editable document**
  物件。本指南亦示範如何在 Visual Studio 中有效率地 **read delimited text C#** 與 **edit CSV .NET**。
keywords:
- create editable document
- read delimited text c#
- edit csv .net
- parse delimited values c#
linktitle: 使用分隔值 (DSV) – 建立可編輯文件
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to **create editable document** objects from CSV and TSV
    files using GroupDocs.Editor for .NET. This guide also shows how to **read delimited
    text C#** and **edit CSV .NET** efficiently in Visual Studio.
  headline: Work with Delimited Separated Values (DSV) – create editable document
  type: TechArticle
- questions:
  - answer: Yes, the API streams data and can handle files larger than 1 GB without
      loading the entire document into memory.
    question: Can I use GroupDocs.Editor for .NET to edit large CSV files?
  - answer: Absolutely – any single‑character delimiter (e.g., pipe `|`, semicolon
      `;`) is supported as long as you specify it in `DelimitedTextEditOptions`.
    question: Does GroupDocs.Editor for .NET support other DSV formats besides CSV
      and TSV?
  - answer: Yes, you can set the `Encoding` property in `DelimitedTextSaveOptions`
      to UTF‑8, UTF‑16, ISO‑8859‑1, or any .NET `Encoding` you require.
    question: Is it possible to customize the encoding when saving DSV files?
  - answer: Yes – after editing, simply use `SpreadsheetSaveOptions` to export the
      content as an `.xlsx` workbook.
    question: Can I convert a CSV file to an Excel spreadsheet using GroupDocs.Editor
      for .NET?
  - answer: Detailed API references and code samples are available **[here](https://tutorials.groupdocs.com/editor/net/)**.
    question: Where can I find more documentation on GroupDocs.Editor for .NET?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: 使用分隔值 (DSV) – 建立可編輯文件
type: docs
url: /zh-hant/net/document-processing/work-dsv/
weight: 12
---

# 使用分隔值 (DSV) – 建立可編輯文件

如果您是需要從 CSV 或 TSV 等分隔值 (DSV) **create editable document** 物件的 .NET 開發人員，您來對地方了。在前 100 個字內，我們將說明為什麼 GroupDocs.Editor for .NET 是 **read delimited text C#**、編輯並在不失去格式的情況下重新儲存的最可靠方式。您將獲得一套完整、可直接複製貼上的工作流程，能自然地融入任何 Visual Studio 解決方案。

## 快速解答
- **哪個函式庫在 .NET 中最佳處理 CSV 編輯？** GroupDocs.Editor for .NET.
- **我可以在 Visual Studio 中編輯大型 CSV 檔案嗎？** 可以 – API 以串流方式處理資料，避免將整個檔案載入記憶體。
- **生產環境需要授權嗎？** 需要商業授權；提供免費試用版。
- **編輯後可以輸出哪些格式？** CSV、TSV 以及 Excel 相容的試算表格式。
- **API 是否相容於 .NET 6+？** 完全相容 – 支援 .NET Framework 4.5+、.NET Core 3.1+、.NET 5 以及 .NET 6。

## 「create editable document」在 GroupDocs.Editor 中是什麼意思？
**Create editable document** 指的是產生一個 `EditableDocument` 實例，該實例在記憶體中代表來源檔案 (CSV、TSV 等) 的可變版本。此物件讓您能使用相同的 API 讀取、修改並重新儲存內容。它提供取得文件文字、套用變更以及以各種格式儲存的方法，確保欄位對齊與引號保留。

## 為什麼要使用 GroupDocs.Editor 處理 DSV？
GroupDocs.Editor 處理 **more than 50 input and output formats**，包括 CSV、TSV 以及 Excel 相容的試算表，同時在處理高達 500 MB 的檔案時記憶體使用量低於 10 MB。它亦會自動保留欄位對齊、引號規則與自訂編碼，免除手動解析的需求。

## 前置條件
- **Visual Studio**（任何近期版本）– 您將直接在 IDE 中開發與除錯。
- **GroupDocs.Editor for .NET** – 下載最新套件 **[here](https://releases.groupdocs.com/editor/net/)**。
- **Basic C# knowledge** – 本教學假設您能建立 Console 或 ASP.NET 專案並加入 NuGet 套件。

## 匯入命名空間
`Editor`、`EditableDocument` 與選項類別位於 `GroupDocs.Editor` 命名空間。  

`DelimitedTextEditOptions` 類別是定義分隔符號（逗號、Tab 等）以及其他解析規則的入口點。

```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

## 如何從 CSV 檔案建立 editable document？
使用 `Editor` 載入來源 CSV，然後呼叫 `Edit` 方法，傳入指定逗號分隔符的 `DelimitedTextEditOptions` 實例。此方法會回傳可在記憶體中操作的 `EditableDocument`。這個「載入 → 編輯」的兩步驟模式涵蓋 **read delimited text C#** 情境，並保證原始檔案結構不變。

## 步驟 1：取得輸入 DSV 檔案的路徑
首先，需要指定來源 DSV 檔案的絕對或相對路徑。為示範起見，我們使用專案 `Data` 資料夾中的簡易 CSV。

```csharp
string inputFilePath = "Your Sample Document";
```

## 步驟 2：建立 Editor 實例
`Editor` 是負責載入、編輯與儲存的核心類別。以 `FileInfo` 物件實例化它，即可完整掌控檔案生命週期。

```csharp
using (Editor editor = new Editor(inputFilePath))
{
```

## 步驟 3：建立 DSV 編輯選項
`DelimitedTextEditOptions` 告訴編輯器如何解讀檔案。您可以設定分隔符號、首列是否為標頭，以及字元編碼。

```csharp
    Options.DelimitedTextEditOptions editOptions = new DelimitedTextEditOptions(",");
    editOptions.ConvertDateTimeData = false;
    editOptions.ConvertNumericData = true;
    editOptions.TreatConsecutiveDelimitersAsOne = true;
```

## 步驟 4：建立 EditableDocument 實例
`EditableDocument` 代表來源檔案在記憶體中的可變版本。呼叫 `Editor.Edit` 並傳入選項，即可取得 `EditableDocument`。此物件以可變字串保存檔案文字，隨時可執行 **parse delimited values C#** 操作。

```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```

## 步驟 5：編輯文件內容
`GetDocumentText()` 會回傳可編輯文件目前的文字字串。透過 `EditableDocument.GetDocumentText()` 取得原始文字後，執行修改（例如替換某欄位值），並將結果存入新字串。這就是 **edit CSV .NET**、不必觸碰低階檔案串流的地方。

```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("SsangYong", "Chevrolet").Replace("Kyron", "Camaro");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```

## 步驟 6：以更新後的內容建立 EditableDocument
將修改過的字串重新包裝成 `EditableDocument`。此步驟完成變更，並為之後的任意支援格式儲存做好準備。

```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```

## 步驟 7：建立 CSV 儲存選項
`DelimitedTextSaveOptions` 定義如何將編輯後的內容寫回 CSV 檔案。當您準備好持久化變更時，設定 `DelimitedTextSaveOptions`，可指定相同或不同的分隔符，甚至變更換行樣式。

```csharp
    Options.DelimitedTextSaveOptions csvSaveOptions = new DelimitedTextSaveOptions(",");
    csvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

## 步驟 8：建立 TSV 儲存選項
若需要 Tab 分隔的版本，只需將分隔符切換為 `\t`。同一個 `EditableDocument` 可使用不同選項多次儲存。

```csharp
    Options.DelimitedTextSaveOptions tsvSaveOptions = new DelimitedTextSaveOptions("\t");
    tsvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

## 步驟 9：建立試算表儲存選項
`SpreadsheetSaveOptions` 設定將文件匯出為 Excel 相容格式（如 .xlsx）。GroupDocs.Editor 亦允許您以 `SpreadsheetSaveOptions` 匯出編輯後的資料為 `.xlsx`。此類別會自動處理欄位類型、公式與儲存格樣式。

```csharp
    Options.SpreadsheetSaveOptions cellsSaveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
```

## 步驟 10：準備儲存路徑
為每種格式定義不同的輸出路徑。使用清晰的命名慣例（例如 `output.csv`、`output.tsv`、`output.xlsx`）有助於保持專案井然有序。

```csharp
    string outputCsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".csv");
    string outputTsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".tsv");
    string outputCellsPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".xlsm");
```

## 步驟 11：儲存編輯後的文件
`Save()` 會依照提供的儲存選項將文件寫入磁碟。對每個目標格式呼叫 `EditableDocument.Save` 並傳入相應選項。API 直接寫入檔案，除非您另行指定，否則會保留原始編碼。

```csharp
    editor.Save(afterEdit, outputCsvPath, csvSaveOptions);
    editor.Save(afterEdit, outputTsvPath, tsvSaveOptions);
    editor.Save(afterEdit, outputCellsPath, cellsSaveOptions);
```

## 步驟 12：釋放 EditableDocument 實例
`Editor` 與 `EditableDocument` 皆實作 `IDisposable`。釋放它們可關閉檔案句柄與非受控資源，這在批次處理大量檔案時尤為重要。

```csharp
    beforeEdit.Dispose();
    afterEdit.Dispose();
}
System.Console.WriteLine("WorkingWithDsv routine has successfully finished");
```

## 常見問題與解決方案
| 問題 | 發生原因 | 解決方案 |
|------|----------|----------|
| **Unexpected extra quotes** | 預設的 CSV 解析器可能將內嵌的逗號視為分隔符。 | 在 `DelimitedTextEditOptions` 中設定 `EscapeMode = EscapeMode.DoubleQuote`。 |
| **Large file memory spike** | 未使用串流直接載入 500 MB 檔案。 | 使用 `Editor.Load` 搭配啟用延遲載入的 `LoadOptions`。 |
| **Encoding mismatch** | 原始檔案為 UTF‑16，但選項預設為 UTF‑8。 | 在儲存選項中明確設定 `Encoding = Encoding.Unicode`。 |

## 常見問答

**Q: 我可以使用 GroupDocs.Editor for .NET 編輯大型 CSV 檔案嗎？**  
A: 可以，API 以串流方式處理資料，能在不將整個文件載入記憶體的情況下處理超過 1 GB 的檔案。

**Q: GroupDocs.Editor for .NET 是否支援除 CSV 與 TSV 之外的其他 DSV 格式？**  
A: 當然支援 – 只要在 `DelimitedTextEditOptions` 中指定任意單一字元分隔符（例如管道 `|`、分號 `;`），皆可使用。

**Q: 儲存 DSV 檔案時可以自訂編碼嗎？**  
A: 可以，您可在 `DelimitedTextSaveOptions` 中設定 `Encoding` 屬性為 UTF‑8、UTF‑16、ISO‑8859‑1 或任何 .NET `Encoding`。

**Q: 我能將 CSV 檔案轉換為 Excel 試算表嗎？**  
A: 可以 – 編輯完成後，只需使用 `SpreadsheetSaveOptions` 即可匯出為 `.xlsx` 工作簿。

**Q: 哪裡可以找到更多關於 GroupDocs.Editor for .NET 的文件？**  
A: 詳細的 API 參考與程式碼範例可於 **[here](https://tutorials.groupdocs.com/editor/net/)** 取得。

---

**最後更新：** 2026-06-06  
**測試環境：** GroupDocs.Editor 23.10 for .NET  
**作者：** GroupDocs

## 相關教學

- [Plain Text and DSV 文件編輯教學（適用於 GroupDocs.Editor .NET）](/editor/net/plain-text-dsv-documents/)
- [精通 GroupDocs.Editor .NET 以高效 CSV 文件編輯與轉換](/editor/net/plain-text-dsv-documents/groupdocs-editor-net-csv-editing-guide/)
- [精通 .NET 中的文件載入：使用 GroupDocs.Editor 的完整指南](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)