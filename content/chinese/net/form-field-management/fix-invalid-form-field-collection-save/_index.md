---
title: 修复无效的表单字段收集并保存
linktitle: 修复无效的表单字段收集并保存
second_title: GroupDocs.Editor .NET API
description: 了解如何使用 Groupdocs.Editor for .NET 修复 DOCX 中的无效表单字段。按照本指南确保您的文档没有错误并安全保存。
weight: 11
url: /zh/net/form-field-management/fix-invalid-form-field-collection-save/
---

# 修复无效的表单字段收集并保存

## 介绍
欢迎！如果您正在处理文档中的表单字段，并且遇到无效表单字段集合的问题，那么您来对地方了。在本教程中，我们将深入介绍如何修复无效表单字段并使用 Groupdocs.Editor for .NET 保存文档。我们将逐步指导您完成该过程，确保您拥有使其无缝运行所需的所有详细信息。让我们开始吧！
## 先决条件
在我们进入代码之前，你需要做好以下几件事：
-  Groupdocs.Editor for .NET：请确保您已安装 Groupdocs.Editor for .NET 库。您可以下载它[这里](https://releases.groupdocs.com/editor/net/).
- 开发环境：您应该设置一个 .NET 开发环境，例如 Visual Studio。
- C# 基础知识：本教程假设您对 C# 编程有基本的了解。
## 导入命名空间
首先，您需要在 C# 项目中导入必要的命名空间。在代码文件的开头添加以下几行：
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System;
using System.IO;
```
## 步骤 1：获取输入文件路径
第一步是指定输入文件的路径。此文件应为包含表单字段的 DOCX 文档。
```csharp
string inputFilePath = Constants.SampleLegacyFormFields_docx;
```
## 步骤 2：从文件路径创建流
接下来，创建一个文件流来读取输入文档。这将允许您将文档加载到编辑器中。
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
```
## 步骤 3：为文档创建加载选项
在此步骤中，您需要为文档创建加载选项。如果您的文档受密码保护，您可以指定密码。在此示例中，文档不受保护，因此密码将被忽略。
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
loadOptions.Password = "some_password_to_open_a_document";
```
## 步骤 4：将文档加载到编辑器实例中
现在，将具有指定选项的文档加载到编辑器实例中。这是对文档进行主要操作的地方。
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
```
## 步骤 4.1：读取 FormFieldManager 实例
这`FormFieldManager`实例负责管理文档中的表单字段。您需要读取此实例才能访问和操作表单字段。
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
## 步骤 4.2：读取 FormFieldCollection
这`FormFieldCollection`包含文档中的所有表单字段。您将阅读此集合以检查和修复无效的表单字段。
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
## 步骤 4.3：自动修复无效的表单字段
尝试自动修复文档中任何无效的表单字段。这是解决明显问题的初步步骤。
```csharp
fieldManager.FixInvalidFormFieldNames(new InvalidFormField[0]);
collection = fieldManager.FormFieldCollection;
```
## 步骤 4.4：检查无效的表单字段
检查自动修复尝试后是否还有任何无效的表单字段。
```csharp
bool hasInvalidFormFields = fieldManager.HasInvalidFormFields();
Console.WriteLine("FormFieldCollection contains invalid items: {0}", hasInvalidFormFields);
```
## 步骤 4.4.1：获取所有无效的表单字段名称
检索所有无效表单字段的名称。这些名称将用于修复字段。
```csharp
var invalidFormFields = fieldManager.GetInvalidFormFieldNames();
```
## 步骤 4.4.2：为无效字段创建唯一名称
为每个无效的表单字段创建一个唯一的名称。这可确保不会与现有的表单字段名称发生冲突。
```csharp
foreach (var invalidItem in invalidFormFields)
{
    invalidItem.FixedName = string.Format("{0}_{1}", invalidItem.Name, Guid.NewGuid());
}
```
## 步骤 4.4.3：修复无效的表单字段
使用上一步中创建的唯一名称修复无效的表单字段。
```csharp
fieldManager.FixInvalidFormFieldNames(invalidFormFields);
collection = fieldManager.FormFieldCollection;
```
## 步骤 5：创建文档保存选项
设置保存文档的选项。这包括指定格式和任何其他保存设置。
```csharp
WordProcessingFormats docFormat = WordProcessingFormats.Docx;
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(docFormat);
```
## 步骤 5.1：优化内存使用
如果您的文档很大并且可能导致`OutOfMemoryException`，启用内存优化选项。
```csharp
saveOptions.OptimizeMemoryUsage = true;
```
## 步骤 5.2：保护文档不被写入
为了保护文档不被修改（表单字段除外），请设置保护密码。
```csharp
saveOptions.Protection = new WordProcessingProtection(WordProcessingProtectionType.AllowOnlyFormFields, "write_password");
```
## 步骤 6：保存文档
最后，使用指定的保存选项保存文档。准备一个内存流用于保存输出文档。
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(outputStream, saveOptions);
}
Console.WriteLine("FixInvalidFormFieldCollectionAndSave routine has successfully finished");
```
## 结论
就这样！您已成功修复无效的表单字段并使用 Groupdocs.Editor for .NET 保存了文档。本分步指南应该使该过程清晰易懂。如果您遇到任何问题或有疑问，请随时查看[文档](https://tutorials.groupdocs.com/editor/net/)或联系[支持](https://forum.groupdocs.com/c/editor/20).
## 常见问题解答
### 如果我的文档受密码保护怎么办？
您可以在`WordProcessingLoadOptions`打开文档。
### 我如何知道是否存在无效的表单字段？
使用`HasInvalidFormFields`方法检查文档中是否存在任何无效的表单字段。
### 我可以修复表单字段而不改变其名称吗？
建议为无效的表单字段创建唯一的名称以避免冲突。
### 我可以用什么格式保存该文档？
您可以通过设置适当的格式将文档保存为 DOCX、PDF 等各种格式`WordProcessingFormats`.
### 如何在保存大型文档的同时优化内存使用？
启用`OptimizeMemoryUsage`选项中的`WordProcessingSaveOptions`有效地处理大型文档。