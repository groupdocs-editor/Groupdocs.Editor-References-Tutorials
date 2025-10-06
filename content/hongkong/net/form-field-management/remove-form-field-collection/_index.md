---
title: 刪除表單欄位集合
linktitle: 刪除表單欄位集合
second_title: GroupDocs.Editor .NET API
description: 透過此逐步指南，了解如何使用 GroupDocs.Editor for .NET 從 Word 文件中刪除表單欄位。非常適合開發人員。
weight: 13
url: /zh-hant/net/form-field-management/remove-form-field-collection/
type: docs
---
# 刪除表單欄位集合

## 介紹
您是否希望以程式設計方式管理文件中的表單欄位？ GroupDocs.Editor for .NET 提供了一個強大的解決方案來處理和操作各種文件格式的表單欄位。在本教學中，我們將引導您完成使用這個強大的庫從 Word 文件中刪除表單欄位集合的步驟。 
## 先決條件
在我們深入研究程式碼之前，讓我們確保您已完成一切設定以獲得流暢的體驗：
1. GroupDocs.Editor for .NET：確保您已下載並安裝 GroupDocs.Editor for .NET。如果沒有的話可以下載[這裡](https://releases.groupdocs.com/editor/net/).
2. 開發環境：您需要一個開發環境，例如 Visual Studio。
3. .NET Framework：請確定您的電腦上安裝了 .NET Framework。
4. 範例文件：有一個範例 Word 文件（例如，`SampleLegacyFormFields.docx`) 以及您想要操作的表單欄位。

## 導入命名空間
首先，您需要在 .NET 專案中匯入必要的命名空間。這將允許您存取 GroupDocs.Editor 功能。
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System.IO;
```
## 第 1 步：載入文檔
首先，您需要載入要編輯的文檔。讓我們來分解一下：
### 步驟1.1：取得輸入檔的路徑
您需要指定輸入檔案的路徑。對於本範例，我們將使用名為的範例文件`SampleLegacyFormFields.docx`.
```csharp
string inputFilePath = "path/to/SampleLegacyFormFields.docx";
```
### 步驟1.2：從路徑建立檔案流
接下來，創建一個`FileStream`閱讀文檔。
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
    //繼續此 using 區塊中的後續步驟。
}
```
## 第 2 步：設定載入選項
載入文件時，您可能需要指定載入選項，尤其是當您的文件受密碼保護時。
### 步驟2.1：建立載入選項
建立一個實例`WordProcessingLoadOptions`.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
```
### 步驟 2.2：指定密碼（如果需要）
如果您的文件受密碼保護，您可以指定密碼。
```csharp
loadOptions.Password = "some_password_to_open_a_document";
```
## 第 3 步：將文件載入到編輯器中
現在，將文檔載入到`Editor`實例使用`FileStream`和`LoadOptions`.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    //繼續此 using 區塊中的後續步驟。
}
```
## 第 4 步：存取和管理表單字段
載入文件後，您現在可以存取和操作表單欄位。
### 步驟4.1：讀取FormFieldManager
檢索`FormFieldManager`來自`Editor`實例。
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
### 步驟4.2：存取FormFieldCollection
獲取`FormFieldCollection`其中包含文件中的所有表單欄位。
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
### 步驟 4.3：刪除特定文字表單字段
若要刪除特定文字表單字段，請按其名稱找到它，然後將其刪除。
```csharp
TextFormField textField = collection.GetFormField<TextFormField>("Text1");
fieldManager.RemoveFormFiled(textField);
```
### 步驟 4.4：刪除多個表單字段
您也可以透過指定名稱一次刪除多個表單欄位。
```csharp
textField = collection.GetFormField<TextFormField>("Text7");
CheckBoxForm checkBoxForm = collection.GetFormField<CheckBoxForm>("Check2");
fieldManager.RemoveFormFields(new IFormField[] { textField, checkBoxForm });
```
## 第五步：儲存修改後的文檔
修改表單欄位後，您需要儲存文件。
### 步驟 5.1：建立儲存選項
指定輸出文件的格式和儲存選項。
```csharp
WordProcessingFormats docFormat = WordProcessingFormats.Docx;
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(docFormat);
```
### 步驟 5.2：優化記憶體使用
如果處理大型文檔，您可能需要優化記憶體使用。
```csharp
saveOptions.OptimizeMemoryUsage = true;
```
### 步驟 5.3：設定保護（如果需要）
您可以透過設定寫入密碼來保護文件免於進一步編輯。
```csharp
saveOptions.Protection = new WordProcessingProtection(WordProcessingProtectionType.AllowOnlyFormFields, "write_password");
```
### 步驟5.4：儲存文檔
最後，使用儲存文檔`MemoryStream`.
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(outputStream, saveOptions);
}
```

## 結論
恭喜！您已使用 GroupDocs.Editor for .NET 成功從 Word 文件中刪除表單欄位。這個功能強大的程式庫使您可以輕鬆地以程式設計方式操作文件內容，從而節省您的時間和精力。
## 常見問題解答
### 我可以將 GroupDocs.Editor for .NET 與其他文件格式一起使用嗎？
是的，GroupDocs.Editor for .NET 支援各種文件格式，包括 PDF、HTML 等。
### 是否可以使用 GroupDocs.Editor for .NET 新增表單欄位？
是的，您可以透過程式設計方式新增、修改和刪除表單欄位。
### 如果我的文件很大怎麼辦？
您可以在儲存選項中啟用記憶體最佳化，以有效地處理大型文件。
### 我可以在 Web 應用程式中使用 GroupDocs.Editor for .NET 嗎？
絕對地！ GroupDocs.Editor for .NET 可以整合到 Web 應用程式中以進行伺服器端文件處理。
### 如果遇到問題，我可以在哪裡獲得支援？
您可以訪問[支援論壇](https://forum.groupdocs.com/c/editor/20)尋求任何問題的幫助。