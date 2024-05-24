---
title: 使用受密码保护的电子表格
linktitle: 使用受密码保护的电子表格
second_title: GroupDocs.Editor .NET API
description: 了解如何使用 GroupDocs.Editor for .NET 处理受密码保护的电子表格。本详细指南将引导您打开并保存安全的 Excel 文件。
type: docs
weight: 18
url: /zh/net/document-processing/work-password-protected-spreadsheets/
---
## 介绍
您是否正在努力管理 .NET 应用程序中受密码保护的电子表格？如果是这样，您来对地方了！在本综合指南中，我们将引导您完成使用 GroupDocs.Editor for .NET 有效处理受密码保护的电子表格的过程。在本教程结束时，您将能够轻松打开、编辑和保存加密的 Excel 文件。
## 先决条件
在深入研究代码之前，请确保您已准备好接下来需要做的一切：
- C# 基础知识：本教程假设您熟悉 C# 编程。
- .NET Framework：确保您的开发机器上安装了.NET 框架。
-  GroupDocs.Editor for .NET：从以下网址下载并安装 GroupDocs.Editor for .NET[这里](https://releases.groupdocs.com/editor/net/).
## 导入命名空间
首先，您需要在 C# 项目中导入必要的命名空间。这些命名空间提供对 GroupDocs.Editor 功能的访问。
```csharp
using System;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
## 步骤 1：获取输入文件的路径
首先，您需要输入文件的路径。在本例中，我们将使用示例 Excel 文件 (`Your Sample Document`) 受密码保护。
```csharp
string inputFilePath = "Your Sample Document";
```
## 步骤 2：尝试在没有密码的情况下打开文档
让我们看看如果我们尝试在不提供密码的情况下打开文档会发生什么。
```csharp
Editor editor = new Editor(inputFilePath);
try
{
    editor.Edit();
}
catch (GroupDocs.Editor.PasswordRequiredException)
{
    Console.WriteLine("Cannot edit the document because it is password-protected. A password is required.");
}
editor.Dispose();
```
## 步骤 3：尝试指定错误的密码
现在，我们将指定一个错误的密码来演示编辑器如何响应。
```csharp
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.Password = "incorrect_password";
editor = new Editor(inputFilePath, delegate { return loadOptions; });
try
{
    editor.Edit();
}
catch (GroupDocs.Editor.IncorrectPasswordException)
{
    Console.WriteLine("Cannot edit the document because the specified password is incorrect.");
}
editor.Dispose();
```
## 步骤 4：使用正确的密码打开文件
让我们提供正确的密码并成功打开文件。
```csharp
loadOptions.Password = "excel_password";
loadOptions.OptimizeMemoryUsage = true;
editor = new Editor(inputFilePath, delegate { return loadOptions; });
```
## 步骤 5：创建并调整编辑选项
要编辑电子表格，我们需要创建和调整编辑选项。
```csharp
SpreadsheetEditOptions editOptions = new SpreadsheetEditOptions();
```
## 步骤 6：创建中间 EditableDocument
接下来我们创建一个中间体`EditableDocument`这使我们能够对电子表格进行更改。
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
{
    //步骤 7：创建保存选项
    SpreadsheetFormats xlsmFormat = SpreadsheetFormats.Xlsm;
    SpreadsheetSaveOptions saveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
    //步骤7.1：设置新的开机密码
    saveOptions.Password = "new password";
    //步骤7.2：设置写保护
    saveOptions.WorksheetProtection = new WorksheetProtection(WorksheetProtectionType.All, "write password");
    //步骤 8：不做修改地保存文档
    //步骤 8.1：准备输出文件名和路径
    string outputFilename = Path.GetFileNameWithoutExtension(inputFilePath) + "." + xlsmFormat.Extension;
    string outputPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename);
    //步骤 8.2：创建输出流
    using (FileStream outputStream = File.Create(outputPath))
    {
        //步骤 8.3：保存
        editor.Save(beforeEdit, outputStream, saveOptions);
    }
}
//步骤 9：处理编辑器实例
editor.Dispose();
Console.WriteLine("Successfully handled the password-protected spreadsheet. Editor instance has been disposed: {0}", editor.IsDisposed ? "Yes" : "No");
```
## 结论
恭喜！您已成功学会如何使用 GroupDocs.Editor for .NET 处理受密码保护的电子表格。从尝试在没有密码的情况下打开文档到使用新的保护设置保存文档，您已经了解了所有必要的步骤。这些知识无疑将增强您在 .NET 应用程序中管理安全文档的能力。
## 常见问题解答
### 什么是 GroupDocs.Editor for .NET？
GroupDocs.Editor for .NET 是一个强大的文档编辑 API，允许开发人员在 .NET 应用程序内加载、编辑和保存各种文档格式。
### 如何获得 GroupDocs.Editor 的临时许可证？
您可以从[这里](https://purchase.groupdocs.com/temporary-license/)评估产品的功能。
### 在编辑大型文档时是否可以优化内存使用情况？
是的，您可以通过设置来启用内存优化`OptimizeMemoryUsage`财产`true`在加载选项中。
### 我可以为打开和写入电子表格设置不同的密码吗？
当然可以！您可以使用保存选项为打开文档和写保护设置单独的密码。
### 在哪里可以找到更详细的文档？
您可以访问 GroupDocs.Editor for .NET 的综合文档[这里](https://reference.groupdocs.com/editor/net/).