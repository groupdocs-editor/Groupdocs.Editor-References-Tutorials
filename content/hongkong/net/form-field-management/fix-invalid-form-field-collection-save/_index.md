---
title: 修復無效的表單欄位集合並儲存
linktitle: 修復無效的表單欄位集合並儲存
second_title: GroupDocs.Editor .NET API
description: 了解如何使用 Groupdocs.Editor for .NET 修復 DOCX 中的無效表單欄位。請遵循本指南，確保您的文件沒有錯誤並安全保存。
weight: 11
url: /zh-hant/net/form-field-management/fix-invalid-form-field-collection-save/
---

# 修復無效的表單欄位集合並儲存

## 介紹
歡迎！如果您正在處理文件中的表單欄位並面臨無效表單欄位集合的問題，那麼您來對地方了。在本教程中，我們將深入探討如何修復無效的表單欄位並使用 Groupdocs.Editor for .NET 儲存文件。我們將逐步引導您完成整個過程，確保您掌握順利運行所需的所有詳細資訊。讓我們開始吧！
## 先決條件
在我們開始編寫程式碼之前，您需要做好以下幾件事：
- 適用於 .NET 的 Groupdocs.Editor：確保您已安裝適用於 .NET 的 Groupdocs.Editor 程式庫。你可以下載它[這裡](https://releases.groupdocs.com/editor/net/).
- 開發環境：您應該設定一個.NET開發環境，例如Visual Studio。
- C# 基礎知識：本教學假設您對 C# 程式設計有基本了解。
## 導入命名空間
首先，您需要在 C# 專案中匯入必要的命名空間。在程式碼檔案的開頭新增以下行：
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System;
using System.IO;
```
## 第1步：取得輸入檔路徑
第一步是指定輸入檔案的路徑。該文件應該是包含表單欄位的 DOCX 文件。
```csharp
string inputFilePath = Constants.SampleLegacyFormFields_docx;
```
## 步驟 2：從檔案路徑建立流
接下來，建立一個文件流來讀取輸入文件。這將允許您將文件載入到編輯器中。
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
```
## 步驟 3：為文件建立載入選項
在此步驟中，您需要為文件建立載入選項。如果您的文件受密碼保護，您可以指定密碼。在此範例中，文件不受保護，因此密碼被忽略。
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
loadOptions.Password = "some_password_to_open_a_document";
```
## 第 4 步：將文件載入到編輯器實例中
現在，將具有指定選項的文件載入到編輯器實例中。這是對文件進行主要操作的地方。
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
```
## 步驟4.1：讀取FormFieldManager實例
這`FormFieldManager`實例負責管理文件中的表單欄位。您需要讀取此實例才能存取和操作表單欄位。
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
## 步驟4.2：讀取FormFieldCollection
這`FormFieldCollection`包含文件中的所有表單欄位。您將閱讀此集合來檢查並修復無效的表單欄位。
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
## 步驟 4.3：自動修復無效的表單字段
嘗試自動修復文件中的任何無效表單欄位。這是解決明顯問題的初步步驟。
```csharp
fieldManager.FixInvalidFormFieldNames(new InvalidFormField[0]);
collection = fieldManager.FormFieldCollection;
```
## 步驟 4.4：檢查無效的表單字段
檢查自動修復嘗試後是否剩餘任何無效的表單欄位。
```csharp
bool hasInvalidFormFields = fieldManager.HasInvalidFormFields();
Console.WriteLine("FormFieldCollection contains invalid items: {0}", hasInvalidFormFields);
```
## 步驟4.4.1：取得所有無效的表單欄位名稱
檢索所有無效表單欄位的名稱。這些名稱將用於修復欄位。
```csharp
var invalidFormFields = fieldManager.GetInvalidFormFieldNames();
```
## 步驟 4.4.2：為無效欄位建立唯一名稱
為每個無效表單欄位建立一個唯一的名稱。這可確保與現有表單欄位名稱不會發生衝突。
```csharp
foreach (var invalidItem in invalidFormFields)
{
    invalidItem.FixedName = string.Format("{0}_{1}", invalidItem.Name, Guid.NewGuid());
}
```
## 步驟 4.4.3：修復無效的表單字段
使用上一個步驟中建立的唯一名稱修復無效的表單欄位。
```csharp
fieldManager.FixInvalidFormFieldNames(invalidFormFields);
collection = fieldManager.FormFieldCollection;
```
## 第 5 步：建立文件儲存選項
設定儲存文件的選項。這包括指定格式和任何其他儲存設定。
```csharp
WordProcessingFormats docFormat = WordProcessingFormats.Docx;
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(docFormat);
```
## 步驟 5.1：優化記憶體使用
如果您的文件很大並且可能會導致`OutOfMemoryException`，啟用記憶體優化選項。
```csharp
saveOptions.OptimizeMemoryUsage = true;
```
## 步驟 5.2：保護文件不被寫入
為了防止文件被修改（表單欄位除外），請設定保護密碼。
```csharp
saveOptions.Protection = new WordProcessingProtection(WordProcessingProtectionType.AllowOnlyFormFields, "write_password");
```
## 第 6 步：儲存文檔
最後，使用指定的儲存選項儲存文件。準備一個記憶體流來保存輸出文件。
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(outputStream, saveOptions);
}
Console.WriteLine("FixInvalidFormFieldCollectionAndSave routine has successfully finished");
```
## 結論
現在你就得到它了！您已成功修復無效的表單欄位並使用 Groupdocs.Editor for .NET 儲存了文件。這個逐步指南應該會使整個過程變得清晰且易於管理。如果您遇到任何問題或有疑問，請隨時查看[文件](https://tutorials.groupdocs.com/editor/net/)或聯繫[支援](https://forum.groupdocs.com/c/editor/20).
## 常見問題解答
### 如果我的文件受密碼保護怎麼辦？
您可以在中指定密碼`WordProcessingLoadOptions`開啟文檔。
### 我如何知道是否存在無效的表單欄位？
使用`HasInvalidFormFields`方法來檢查文件中是否有任何無效的表單欄位。
### 我可以修復表單欄位而不更改其名稱嗎？
建議為無效表單欄位建立唯一的名稱以避免衝突。
### 我可以將文件儲存為哪些格式？
您可以透過設定適當的選項以各種格式儲存文檔，例如 DOCX、PDF 等`WordProcessingFormats`.
### 如何在儲存大型文件的同時優化記憶體使用？
啟用`OptimizeMemoryUsage`選項中的`WordProcessingSaveOptions`有效地處理大型文件。