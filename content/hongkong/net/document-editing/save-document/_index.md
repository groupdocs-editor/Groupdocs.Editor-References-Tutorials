---
title: 儲存文件
linktitle: 儲存文件
second_title: GroupDocs.Editor .NET API
description: 使用 GroupDocs.Editor for .NET 輕鬆編輯和儲存文件。本逐步指南簡化了開發人員的流程。
type: docs
weight: 14
url: /zh-hant/net/document-editing/save-document/
---
## 介紹
您是否希望使用 GroupDocs.Editor for .NET 輕鬆編輯和儲存文件？您來對地方了！本教學將逐步引導您完成整個過程，確保您可以輕鬆管理文件。無論您是經驗豐富的開發人員還是初學者，我們的指南都會為您提供入門所需的所有資訊。
## 先決條件
在深入學習本教程之前，請確保您具備以下先決條件：
- 開發環境：您的電腦上安裝了 Visual Studio。
- .NET Framework：確保您擁有 .NET Framework 4.6.1 或更高版本。
-  GroupDocs.Editor for .NET：下載最新版本[這裡](https://releases.groupdocs.com/editor/net/).
- 基本 C# 知識：熟悉 C# 程式設計至關重要。
## 導入命名空間
若要在 .NET 專案中使用 GroupDocs.Editor，您需要匯入必要的命名空間。操作方法如下：
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
現在我們已經設定了環境並匯入了必要的命名空間，接下來讓我們深入了解使用 GroupDocs.Editor for .NET 載入、編輯和儲存文件所需的步驟。
## 第 1 步：載入文檔
首先，我們需要載入要編輯的文檔。 GroupDocs.Editor 讓這個過程變得簡單。您可以這樣做：

```csharp
string inputFilePath = "Your Sample Document";
Editor editor = new Editor(inputFilePath, delegate { return new Options.WordProcessingLoadOptions(); });
EditableDocument defaultWordProcessingDoc = editor.Edit();
```
在此步驟中，我們指定要編輯的文件的路徑並建立該文件的實例`Editor`班級。這`Edit`然後呼叫方法將文檔載入到`EditableDocument`目的。
## 第二步：修改文檔
載入文件後，是時候進行一些修改了。由於我們沒有附加所見即所得編輯器，因此我們將在程式碼中模擬編輯過程。

```csharp
string allEmbeddedInsideString = defaultWordProcessingDoc.GetEmbeddedHtml();
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
EditableDocument editedDoc = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```
在這裡，我們檢索文件的嵌入 HTML 內容，執行簡單的文字替換，並建立一個新的`EditableDocument`來自修改後的 HTML 的實例。
## 第 3 步：儲存文檔
編輯文檔後，最後一步是儲存它。 GroupDocs.Editor 提供了多種以不同格式儲存文件的選項。
## 另存為 RTF
```csharp
string outputRtfPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.rtf");
WordProcessingSaveOptions rtfSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
editor.Save(editedDoc, outputRtfPath, rtfSaveOptions);
```
## 另存為 DOCM
```csharp
string outputDocmPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.docm");
WordProcessingSaveOptions docmSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm);
using (FileStream outputStream = File.Create(outputDocmPath))
{
    editor.Save(editedDoc, outputStream, docmSaveOptions);
}
```
## 另存為純文字
```csharp
string outputTxtPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.txt");
TextSaveOptions textSaveOptions = new TextSaveOptions
{
    Encoding = System.Text.Encoding.UTF8,
    PreserveTableLayout = true
};
editor.Save(editedDoc, outputTxtPath, textSaveOptions);
```
## 第四步：清理
最後，處理掉這些東西也很重要`EditableDocument`和`Editor`實例以釋放資源。
```csharp
editedDoc.Dispose();
defaultWordProcessingDoc.Dispose();
editor.Dispose();
```
透過執行以下步驟，您可以使用 GroupDocs.Editor for .NET 有效地載入、編輯和儲存文件。這個強大的工具提供了靈活性和易用性，使文件管理變得輕而易舉。
## 結論
使用 GroupDocs.Editor for .NET 以程式設計方式編輯和儲存文件從未如此簡單。本指南將引導您完成從載入文件到以各種格式儲存文件的整個過程。透過 GroupDocs.Editor，您可以輕鬆獲得多功能且強大的解決方案，從而簡化文件編輯流程。
## 常見問題解答
### GroupDocs.Editor 支援哪些檔案格式？
GroupDocs.Editor 支援各種檔案格式，包括 DOCX、RTF、TXT 等。如需完整列表，請查看[文件](https://reference.groupdocs.com/editor/net/).
### 我可以在購買前試用 GroupDocs.Editor 嗎？
是的，您可以獲得[免費試用](https://releases.groupdocs.com/)測試 GroupDocs.Editor 的功能。
### 如果我遇到問題，可以獲得任何支援嗎？
絕對地！您可以訪問[支援論壇](https://forum.groupdocs.com/c/editor/20)尋求有關您遇到的任何問題的協助。
### 如何獲得臨時許可證？
您可以請求[臨時執照](https://purchase.groupdocs.com/temporary-license/)出於評估目的。
### 哪裡可以購買完整版的 GroupDocs.Editor？
您可以購買完整版[這裡](https://purchase.groupdocs.com/buy).