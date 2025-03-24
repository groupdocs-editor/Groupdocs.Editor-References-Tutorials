---
title: 使用旧版表单字段集合
linktitle: 使用旧版表单字段集合
second_title: GroupDocs.Editor .NET API
description: 通过我们的详细指南了解如何使用 GroupDocs.Editor for .NET 管理旧式表单字段。非常适合处理文本字段、复选框、日期等。
weight: 12
url: /zh/net/form-field-management/work-legacy-form-field-collection/
---

# 使用旧版表单字段集合

## 介绍
欢迎阅读本指南，了解如何使用 GroupDocs.Editor for .NET 处理旧式表单字段集合。无论您处理的是文本字段、复选框、日期字段还是下拉菜单，本教程都将引导您完成每个步骤，以有效地管理这些字段。在本指南结束时，您将对如何利用 GroupDocs.Editor 处理文档中的各种表单字段有一个深入的理解。让我们开始吧！
## 先决条件
在开始之前，请确保您满足以下先决条件：
- Visual Studio：任何最新版本都可以。
- .NET Framework：确保您已安装.NET Framework。
-  GroupDocs.Editor for .NET：下载最新版本[这里](https://releases.groupdocs.com/editor/net/).
- 示例文档：用于测试目的的包含表单字段的示例 DOCX 文件。
## 导入命名空间
首先，在项目中导入必要的命名空间。这些命名空间对于访问操作表单字段所需的类和方法至关重要。
```csharp
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System.IO;
```
## 步骤 1：获取输入文件路径
首先，您需要指定输入文件的路径。在此示例中，我们将使用包含各种表单字段的示例 DOCX 文件。
```csharp
string inputFilePath = "path/to/your/sample_legacy_formfields.docx";
```
## 步骤 2：从文件路径创建流
接下来，创建一个文件流来读取文档的内容。此流将用于将文档加载到 GroupDocs.Editor 中。
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
    //附加代码将放在此处
}
```
## 步骤 3：为文档创建加载选项
在加载文档之前，请创建加载选项。这些选项将有助于处理不同的场景，例如受密码保护的文档。
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
//如果文档受密码保护，请指定密码
loadOptions.Password = "your_password_here"; //必要时使用真实密码
```
## 步骤 4：使用编辑器实例加载文档
现在，使用您之前创建的文件流和加载选项将文档加载到编辑器实例中。
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    //附加代码将放在此处
}
```
## 步骤 5：读取 FormFieldManager 实例
要管理表单字段，请从编辑器访问 FormFieldManager 实例。此实例将允许您与文档中的表单字段进行交互。
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
## 步骤 6：读取 FormFieldCollection
从 FormFieldManager 中检索 FormFieldCollection。此集合包含文档中存在的所有表单字段。
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
## 步骤 7：遍历每个表单字段
循环遍历集合中的每个表单字段并识别其类型。根据类型，您可以提取和操作字段的值。
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
## 步骤8：结论
通过遵循这些步骤，您可以使用 GroupDocs.Editor for .NET 有效地管理和与文档中的旧表单字段进行交互。无论是文本字段、复选框、日期、数字还是下拉菜单，本指南都提供了一种清晰简洁的方式来处理每种类型。
## 结论
使用正确的工具处理文档中的旧表单字段会变得非常简单。GroupDocs.Editor for .NET 提供了一个强大的解决方案来有效地管理这些字段。通过遵循本分步指南，您现在应该能够轻松地操作文档中的各种表单字段。别忘了探索[文档](https://tutorials.groupdocs.com/editor/net/)获得更多高级功能和选项。
## 常见问题解答
### 1. 我可以使用 GroupDocs.Editor for .NET 来处理受密码保护的文档吗？
是的，您可以在加载选项中指定密码来处理受密码保护的文档。
### 2. 如何免费试用 GroupDocs.Editor for .NET？
您可以从下载免费试用版[这里](https://releases.groupdocs.com/).
### 3. GroupDocs.Editor 是否支持 .NET？
是的，您可以获得支持[这里](https://forum.groupdocs.com/c/editor/20).
### 4. 我可以购买 GroupDocs.Editor for .NET 的许可证吗？
是的，你可以从[这里](https://purchase.groupdocs.com/buy).
### 5. 在哪里可以找到 GroupDocs.Editor for .NET 的文档？
文档可用[这里](https://tutorials.groupdocs.com/editor/net/).