---
title: 使用舊表單欄位集合
linktitle: 使用舊表單欄位集合
second_title: GroupDocs.Editor .NET API
description: 透過我們的詳細指南，了解如何使用 GroupDocs.Editor for .NET 管理舊表單欄位。非常適合處理文字欄位、複選框、日期等。
weight: 12
url: /zh-hant/net/form-field-management/work-legacy-form-field-collection/
---
## 介紹
歡迎閱讀這份關於如何使用 GroupDocs.Editor for .NET 處理舊表單欄位集合的綜合指南。無論您正在處理文字欄位、複選框、日期欄位或下拉式選單，本教學都將引導您完成有效管理這些欄位的每個步驟。在本指南結束時，您將充分了解如何使用 GroupDocs.Editor 處理文件中的各種表單欄位。讓我們深入了解吧！
## 先決條件
在我們開始之前，請確保您符合以下先決條件：
- Visual Studio：任何最新版本都可以使用。
- .NET Framework：確保您已安裝 .NET Framework。
-  GroupDocs.Editor for .NET：下載最新版本[這裡](https://releases.groupdocs.com/editor/net/).
- 範例文件：帶有用於測試目的的表單欄位的範例 DOCX 檔案。
## 導入命名空間
首先，在專案中導入必要的命名空間。這些命名空間對於存取操作表單欄位所需的類別和方法至關重要。
```csharp
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System.IO;
```
## 第1步：取得輸入檔路徑
首先，您需要指定輸入檔案的路徑。在此範例中，我們將使用包含各種表單欄位的範例 DOCX 檔案。
```csharp
string inputFilePath = "path/to/your/sample_legacy_formfields.docx";
```
## 步驟 2：從檔案路徑建立流
接下來，建立一個文件流來讀取文件的內容。該流將用於將文件載入到 GroupDocs.Editor 中。
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
    //附加程式碼將在此處
}
```
## 步驟 3：為文件建立載入選項
在載入文件之前，建立載入選項。這些選項將有助於處理不同的情況，例如受密碼保護的文件。
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
//如果文件受密碼保護，請指定密碼
loadOptions.Password = "your_password_here"; //如有必要，請使用實際密碼
```
## 第 4 步：使用編輯器實例載入文檔
現在，使用您先前建立的文件流和載入選項將文件載入到編輯器實例中。
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    //附加程式碼將在此處
}
```
## 步驟5：讀取FormFieldManager實例
若要管理表單字段，請從編輯器存取 FormFieldManager 實例。此實例將允許您與文件中的表單欄位進行互動。
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
## 第 6 步：讀取 FormFieldCollection
從 FormFieldManager 檢索 FormFieldCollection。此集合包含文件中存在的所有表單欄位。
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
## 第 7 步：遍歷每個表單字段
循環遍歷集合中的每個表單欄位並識別其類型。根據類型，您可以提取和操作欄位的值。
```csharp
foreach (var formField in collection)
{
    switch (formField.Type)
    {
        case FormFieldType.Text:
            TextFormField textFormField = collection.GetFormField<TextFormField>(formField.Name);
            Console.WriteLine($"TextFormField detected, name: {formField.Name}, value: {textFormField.Value}");
            break;
        case FormFieldType.CheckBox:
            CheckBoxForm checkBoxFormField = collection.GetFormField<CheckBoxForm>(formField.Name);
            Console.WriteLine($"CheckBoxForm detected, name: {formField.Name}, value: {checkBoxFormField.Value}");
            break;
        case FormFieldType.Date:
            DateFormField dateFormField = collection.GetFormField<DateFormField>(formField.Name);
            Console.WriteLine($"DateFormField detected, name: {formField.Name}, value: {dateFormField.Value}");
            break;
        case FormFieldType.Number:
            NumberFormField numberFormField = collection.GetFormField<NumberFormField>(formField.Name);
            Console.WriteLine($"NumberFormField detected, name: {formField.Name}, value: {numberFormField.Value}");
            break;
        case FormFieldType.DropDown:
            DropDownFormField dropDownFormField = collection.GetFormField<DropDownFormField>(formField.Name);
            Console.WriteLine($"DropDownFormField detected, name: {formField.Name}, value selected: {dropDownFormField.Value[dropDownFormField.SelectedIndex]}");
            break;
    }
}
```
## 第 8 步：結論
透過執行這些步驟，您可以使用 GroupDocs.Editor for .NET 有效管理文件中的舊表單欄位並與之互動。無論是文字欄位、複選框、日期、數字或下拉列表，本指南都提供了一種清晰簡潔的方法來處理每種類型。
## 結論
使用正確的工具時，處理文件中的舊表單欄位會變得非常簡單。 GroupDocs.Editor for .NET 提供了一個強大的解決方案來有效管理這些欄位。透過遵循此逐步指南，您現在應該能夠輕鬆操作文件中的各種表單欄位。不要忘記探索[文件](https://tutorials.groupdocs.com/editor/net/)了解更多進階功能和選項。
## 常見問題解答
### 1. 我可以將 GroupDocs.Editor for .NET 用於受密碼保護的文件嗎？
是的，您可以在載入選項中指定密碼來處理受密碼保護的文件。
### 2. 如何獲得 GroupDocs.Editor for .NET 的免費試用版？
您可以從以下位置下載免費試用版[這裡](https://releases.groupdocs.com/).
### 3. GroupDocs.Editor for .NET 是否有支援？
是的，您可以獲得支持[這裡](https://forum.groupdocs.com/c/editor/20).
### 4. 我可以購買 GroupDocs.Editor for .NET 的授權嗎？
是的，您可以從以下位置購買許可證[這裡](https://purchase.groupdocs.com/buy).
### 5. 在哪裡可以找到 GroupDocs.Editor for .NET 的文件？
文件可用[這裡](https://tutorials.groupdocs.com/editor/net/).