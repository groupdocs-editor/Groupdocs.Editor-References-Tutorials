---
title: 移除表单字段集合
linktitle: 移除表单字段集合
second_title: GroupDocs.Editor .NET API
description: 通过本分步指南了解如何使用 GroupDocs.Editor for .NET 从 Word 文档中删除表单字段。非常适合开发人员。
type: docs
weight: 13
url: /zh/net/form-field-management/remove-form-field-collection/
---
## 介绍
您是否希望以编程方式管理文档中的表单字段？GroupDocs.Editor for .NET 提供了强大的解决方案来处理和操作各种文档格式的表单字段。在本教程中，我们将指导您完成使用此强大的库从 Word 文档中删除表单字段集合的步骤。 
## 先决条件
在深入研究代码之前，让我们确保您已完成所有设置，以获得顺畅的体验：
1. GroupDocs.Editor for .NET：请确保您已下载并安装了 GroupDocs.Editor for .NET。如果没有，您可以下载它[这里](https://releases.groupdocs.com/editor/net/).
2. 开发环境：您需要一个开发环境，例如 Visual Studio。
3. .NET Framework：确保您的机器上安装了 .NET Framework。
4. 示例文档：准备一个示例 Word 文档（例如，`SampleLegacyFormFields.docx`) 包含您想要操作的表单字段。

## 导入命名空间
首先，您需要在 .NET 项目中导入必要的命名空间。这将允许您访问 GroupDocs.Editor 功能。
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System.IO;
```
## 步骤 1：加载文档
首先，您需要加载要编辑的文档。让我们分解一下：
### 步骤 1.1：获取输入文件的路径
您需要指定输入文件的路径。在本例中，我们将使用名为`SampleLegacyFormFields.docx`.
```csharp
string inputFilePath = "path/to/SampleLegacyFormFields.docx";
```
### 步骤 1.2：从路径创建 FileStream
接下来，创建一个`FileStream`阅读文档。
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
    //继续此使用块内的后续步骤。
}
```
## 步骤 2：设置加载选项
加载文档时，您可能需要指定加载选项，尤其是在您的文档受密码保护的情况下。
### 步骤 2.1：创建加载选项
创建一个实例`WordProcessingLoadOptions`.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
```
### 步骤 2.2：指定密码（如果需要）
如果您的文档受密码保护，您可以指定密码。
```csharp
loadOptions.Password = "some_password_to_open_a_document";
```
## 步骤 3：将文档加载到编辑器中
现在，将文档加载到`Editor`实例使用`FileStream`和`LoadOptions`.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    //继续此使用块内的后续步骤。
}
```
## 步骤 4：访问和管理表单字段
加载文档后，您现在可以访问和操作表单字段。
### 步骤 4.1：读取 FormFieldManager
检索`FormFieldManager`来自`Editor`实例。
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
### 步骤 4.2：访问 FormFieldCollection
获取`FormFieldCollection`其中包含文档中的所有表单字段。
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
### 步骤 4.3：删除特定文本表单字段
要删除特定的文本表单字段，请通过其名称找到它，然后将其删除。
```csharp
TextFormField textField = collection.GetFormField<TextFormField>("Text1");
fieldManager.RemoveFormFiled(textField);
```
### 步骤 4.4：删除多个表单字段
您还可以通过指定名称一次删除多个表单字段。
```csharp
textField = collection.GetFormField<TextFormField>("Text7");
CheckBoxForm checkBoxForm = collection.GetFormField<CheckBoxForm>("Check2");
fieldManager.RemoveFormFields(new IFormField[] { textField, checkBoxForm });
```
## 步骤5：保存修改后的文档
修改表单字段后，需要保存文档。
### 步骤 5.1：创建保存选项
指定输出文档的格式和保存选项。
```csharp
WordProcessingFormats docFormat = WordProcessingFormats.Docx;
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(docFormat);
```
### 步骤 5.2：优化内存使用
如果处理大型文档，您可能需要优化内存使用。
```csharp
saveOptions.OptimizeMemoryUsage = true;
```
### 步骤 5.3：设置保护（如果需要）
您可以通过设置写密码来保护文档不被进一步编辑。
```csharp
saveOptions.Protection = new WordProcessingProtection(WordProcessingProtectionType.AllowOnlyFormFields, "write_password");
```
### 步骤 5.4：保存文档
最后，使用`MemoryStream`.
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(outputStream, saveOptions);
}
```

## 结论
恭喜！您已成功使用 GroupDocs.Editor for .NET 从 Word 文档中删除表单字段。这个功能强大的库可让您轻松地以编程方式操作文档内容，从而节省您的时间和精力。
## 常见问题解答
### 我可以将 GroupDocs.Editor for .NET 与其他文档格式一起使用吗？
是的，GroupDocs.Editor for .NET 支持各种文档格式，包括 PDF、HTML 等。
### 是否可以使用 GroupDocs.Editor for .NET 添加表单字段？
是的，您可以通过编程添加、修改和删除表单字段。
### 如果我的文档很大怎么办？
您可以在保存选项中启用内存优化，以有效地处理大型文档。
### 我可以在 Web 应用程序中使用 GroupDocs.Editor for .NET 吗？
当然！GroupDocs.Editor for .NET 可以集成到 Web 应用程序中，用于服务器端文档处理。
### 如果我遇到问题，可以在哪里获得支持？
您可以访问[支持论坛](https://forum.groupdocs.com/c/editor/20)以获得有关任何问题的帮助。