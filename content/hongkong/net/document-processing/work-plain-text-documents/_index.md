---
date: 2026-08-10
description: 了解如何使用 GroupDocs.Editor for .NET 編輯純文字檔案。本指南涵蓋載入 txt 檔、去除空格、設定文字編碼，以及儲存結果。
keywords:
- edit plain text
- load txt file
- trim trailing spaces
- convert leading spaces
- set text encoding
lastmod: 2026-08-10
linktitle: 處理純文字文件
og_description: 了解如何使用 GroupDocs.Editor for .NET 編輯純文字檔案 – 載入 txt 檔、去除尾端空格、轉換前導空格、設定文字編碼，並有效儲存。
og_image_alt: Guide showing edit plain text workflow with GroupDocs.Editor for .NET
og_title: 使用 GroupDocs.Editor for .NET 編輯純文字文件
schemas:
- author: GroupDocs
  dateModified: '2026-08-10'
  description: Learn how to edit plain text files using GroupDocs.Editor for .NET.
    The guide covers loading a txt file, trimming spaces, setting text encoding, and
    saving the result.
  headline: Edit plain text documents with GroupDocs.Editor for .NET
  type: TechArticle
- description: Learn how to edit plain text files using GroupDocs.Editor for .NET.
    The guide covers loading a txt file, trimming spaces, setting text encoding, and
    saving the result.
  name: Edit plain text documents with GroupDocs.Editor for .NET
  steps:
  - name: Get a path to the input TXT file
    text: First, decide whether you’ll work with a physical file path or a memory
      stream. Using a path is the most straightforward approach for local development.
  - name: Create an Editor instance
    text: '`Editor` is the main class that loads a document and provides editing capabilities.'
  - name: Create TXT editing options
    text: '`TxtEditOptions` configures how plain‑text files are parsed and edited,
      allowing you to set encoding and space‑handling rules.'
  - name: Create an EditableDocument instance
    text: '`EditableDocument` represents the in‑memory version of the loaded document,
      including its text and any associated resources.'
  - name: Edit the document content
    text: Retrieve the original text, apply any string operations you need (e.g.,
      replace, trim, change case), and store the result back into the `EditableDocument`.
  - name: Create an EditableDocument with updated content
    text: After you’ve transformed the text, instantiate a new `EditableDocument`
      that contains the edited string and the original resource collection.
  - name: Create WordProcessing save options
    text: '`WordProcessingSaveOptions` defines settings for saving the document in
      a Word‑compatible format such as DOCX or DOCM.'
  - name: Create TXT saving options
    text: '`TxtSaveOptions` specifies how the edited plain‑text file should be written,
      including encoding, line‑ending preservation, and table layout handling.'
  - name: Prepare output paths
    text: Derive the output directory from the input file path, then build the full
      filenames for the DOCX and TXT results.
  - name: Save the edited document
    text: Finally, call `editor.Save` twice—once with the WordProcessing options and
      once with the TXT options—to produce both formats in a single operation.
  type: HowTo
- questions:
  - answer: The library supports 50+ formats, including DOCX, TXT, HTML, PDF, and
      markdown, allowing you to edit and convert between them seamlessly.
    question: What file formats does GroupDocs.Editor for .NET support?
  - answer: Download the trial from the [releases page](https://releases.groupdocs.com/).
    question: How can I get a free trial of GroupDocs.Editor for .NET?
  - answer: Yes, temporary licenses are available through the [GroupDocs purchase
      page](https://purchase.groupdocs.com/temporary-license/).
    question: Can I purchase a temporary license for testing?
  - answer: The official support forum is the best place – visit the [GroupDocs.Editor
      support forum](https://forum.groupdocs.com/c/editor/20).
    question: Where can I find support if I run into issues?
  - answer: Absolutely. The full reference is on the [GroupDocs.Editor documentation
      page](https://tutorials.groupdocs.com/editor/net/).
    question: Is there detailed documentation for advanced scenarios?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
tags:
- edit plain text
- GroupDocs.Editor
- C# document processing
- plain text editing
- txt file handling
title: 使用 GroupDocs.Editor for .NET 編輯純文字文件
type: docs
url: /zh-hant/net/document-processing/work-plain-text-documents/
weight: 15
---

# 編輯純文字文件使用 GroupDocs.Editor for .NET

## 簡介
如果您需要在 .NET 應用程式中快速且可靠地 **edit plain text**，GroupDocs.Editor for .NET 是能夠完成繁重工作的工具。此 API 支援超過 30 種文件格式，能處理高達 500 MB 的檔案，且讓您在不將整個檔案載入記憶體的情況下操作文字。在本教學中，您將學會如何載入 txt 檔案、修剪行尾空格、轉換行首空格、設定正確的編碼，最後將編輯後的內容儲存回磁碟。準備好動手了嗎？讓我們開始吧！

## 快速解答
- **編輯 txt 檔案的第一步是什麼？** 使用 `Editor` 並以您擁有的路徑或串流載入檔案。  
- **編輯時我可以變更檔案編碼嗎？** 可以 – `TxtSaveOptions` 允許您指定 UTF‑8、UTF‑16 或任何自訂編碼。  
- **如何移除每行結尾的多餘空格？** 取得文字，對每行呼叫 `TrimEnd()`，然後寫回。  
- **GroupDocs.Editor 可以免費試用嗎？** 可從發行頁面取得功能完整的 30 天試用版。  
- **支援哪些 .NET 版本？** .NET Framework 4.6+、.NET Core 3.1+ 以及 .NET 5/6/7。

## 什麼是 edit plain text？
**Edit plain text** 指以程式方式變更簡易 `.txt` 檔案內的字元——加入、刪除或重新格式化文字——同時保留檔案原本的編碼與換行樣式。可能涉及的工作包括修剪空白字元、正規化換行符號、更新設定值，或插入產生的內容。此操作應確保檔案仍能被任何標準文字編輯器讀取，並保留任何現有的中繼資料，例如 BOM 標記。

## 為什麼使用 GroupDocs.Editor 進行純文字編輯？
GroupDocs.Editor 以串流方式處理檔案，這表示它能在使用不到 50 MB 記憶體的情況下編輯 300 MB 的日誌檔案。此函式庫支援 **50+ 輸入與輸出格式**，自動偵測換行樣式（CR、LF、CRLF），並提供內建選項可 **trim trailing spaces** 與 **convert leading spaces**，無需自行撰寫解析器。

## 先決條件
- **.NET 開發環境** – Visual Studio 2022 或搭配 C# 擴充功能的 VS Code。  
- **GroupDocs.Editor for .NET** – 從 [GroupDocs.Editor for .NET](https://releases.groupdocs.com/editor/net/) 發行頁面下載。  
- **基本 C# 知識** – 您應該熟悉檔案 I/O 與字串操作。  
- **文字編輯器（可選）** – 用於檢視原始檔案；建議使用 VS Code。  
- 欲取得詳細使用說明，請參閱 [documentation](https://tutorials.groupdocs.com/editor/net/)。  
- 您也可以瀏覽一般的 [releases page](https://releases.groupdocs.com/)。  

## 如何一步步編輯純文字
載入檔案、編輯其內容，然後儲存回去——全部只需不到十行程式碼。以下各節將以清晰說明帶您逐步完成每個階段。

### 步驟 1：取得輸入 TXT 檔案的路徑
首先，決定您是使用實體檔案路徑還是記憶體串流。對於本機開發而言，使用路徑是最直接的方式。

```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

### 步驟 2：建立 Editor 實例
`Editor` 是負責載入文件並提供編輯功能的主要類別。

```csharp
string inputFilePath = "YourSampleDocument.txt";
```

### 步驟 3：建立 TXT 編輯選項
`TxtEditOptions` 設定純文字檔案的解析與編輯方式，讓您可以指定編碼與空格處理規則。

```csharp
using (Editor editor = new Editor(inputFilePath))
{
```

### 步驟 4：建立 EditableDocument 實例
`EditableDocument` 代表已載入文件的記憶體內版本，包含其文字及任何相關資源。

```csharp
    TextEditOptions editOptions = new TextEditOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        RecognizeLists = true,
        LeadingSpaces = TextLeadingSpacesOptions.ConvertToIndent,
        TrailingSpaces = TextTrailingSpacesOptions.Trim
    };
```

### 步驟 5：編輯文件內容
取得原始文字，套用您需要的字串操作（例如取代、trim、變更大小寫），並將結果存回 `EditableDocument`。

```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```

### 步驟 6：使用更新後的內容建立 EditableDocument
在您轉換文字後，實例化一個新的 `EditableDocument`，其中包含編輯過的字串與原始資源集合。

```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("text", "EDITED text");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```

### 步驟 7：建立 WordProcessing 儲存選項
`WordProcessingSaveOptions` 定義將文件儲存為 Word 相容格式（如 DOCX 或 DOCM）的設定。

```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```

### 步驟 8：建立 TXT 儲存選項
`TxtSaveOptions` 指定編輯後的純文字檔案寫入方式，包含編碼、換行保留與表格版面處理等。

```csharp
    WordProcessingSaveOptions wordSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm)
    {
        Locale = System.Globalization.CultureInfo.GetCultureInfo("en-GB")
    };
```

### 步驟 9：準備輸出路徑
從輸入檔案路徑衍生輸出目錄，接著組合 DOCX 與 TXT 結果的完整檔名。

```csharp
    TextSaveOptions txtSaveOptions = new TextSaveOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        PreserveTableLayout = true
    };
```

### 步驟 10：儲存編輯後的文件
最後，呼叫 `editor.Save` 兩次——一次使用 WordProcessing 選項，一次使用 TXT 選項，即可在單一操作中產生兩種格式。

```csharp
    string outputWordPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".docm");
    string outputTxtPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".txt");
```

## 常見問題與解決方案
- **編輯後仍有行尾空格** – 請確保在載入文件前將 `TxtEditOptions.TrimTrailingSpaces` 設為 `true`。  
- **儲存的檔案編碼不正確** – 請確認 `TxtSaveOptions.Encoding` 與目標代碼頁相符（例如 `Encoding.UTF8`）。  
- **大型檔案導致 OutOfMemoryException** – 請使用串流 API（`Editor.Load(Stream)`）而非從檔案路徑載入，以降低記憶體使用。  

## 常見問答

**Q: GroupDocs.Editor for .NET 支援哪些檔案格式？**  
A: 此函式庫支援 50+ 種格式，包括 DOCX、TXT、HTML、PDF 與 markdown，讓您能無縫編輯與轉換。

**Q: 我該如何取得 GroupDocs.Editor for .NET 的免費試用？**  
A: 從 [releases page](https://releases.groupdocs.com/) 下載試用版。

**Q: 我可以購買臨時授權來測試嗎？**  
A: 可以，臨時授權可於 [GroupDocs purchase page](https://purchase.groupdocs.com/temporary-license/) 取得。

**Q: 若遇到問題，我該去哪裡尋求支援？**  
A: 官方支援論壇是最佳選擇 – 前往 [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20)。

**Q: 是否有進階情境的詳細文件？**  
A: 當然有。完整參考位於 [GroupDocs.Editor documentation page](https://tutorials.groupdocs.com/editor/net/)。

## 結論
您現在已掌握使用 GroupDocs.Editor for .NET **edit plain text** 檔案的技巧——載入 txt 檔、修剪空格、轉換行首空格、設定正確編碼，並將結果儲存為 TXT 與 DOCX 兩種格式。此功能讓您能自動化日誌檔清理、即時產生設定檔，或建構自訂文字處理管線，而無需重新發明輪子。請前往官方文件探索批次處理與文件轉換等其他功能。

**最後更新：** 2026-08-10  
**測試環境：** GroupDocs.Editor 23.11 for .NET  
**作者：** GroupDocs  

```csharp
    editor.Save(afterEdit, outputWordPath, wordSaveOptions);
    editor.Save(afterEdit, outputTxtPath, txtSaveOptions);
}
System.Console.WriteLine("Document editing process completed successfully!");
```

## 相關教學

- [使用 GroupDocs.Editor for .NET 的文件載入教學](/editor/net/document-loading/)
- [使用 GroupDocs.Editor .NET 的文件儲存與匯出教學](/editor/net/document-saving/)
- [使用 GroupDocs.Editor .NET 的純文字與 DSV 文件編輯教學](/editor/net/plain-text-dsv-documents/)