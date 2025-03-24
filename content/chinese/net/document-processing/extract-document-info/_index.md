---
title: 提取文档信息
linktitle: 提取文档信息
second_title: GroupDocs.Editor .NET API
description: 通过我们详细的分步教程学习如何使用 GroupDocs.Editor for .NET 提取文档信息。非常适合管理各种文档类型。
weight: 10
url: /zh/net/document-processing/extract-document-info/
---

# 提取文档信息

## 介绍
欢迎阅读本篇关于使用 GroupDocs.Editor for .NET 提取文档信息的综合教程。在本指南中，我们将逐步指导您完成整个过程，确保您清楚、简洁地理解每个部分。无论您是经验丰富的开发人员还是刚刚入门，本教程都将帮助您将 GroupDocs.Editor 无缝集成到您的 .NET 项目中，以高效地管理和操作文档。
## 先决条件
在深入研究代码之前，请确保您已准备好所需的一切：
- C# 基础知识：了解 C# 编程基础知识至关重要。
- Visual Studio：确保您已安装 Visual Studio。
-  GroupDocs.Editor for .NET：您需要 GroupDocs.Editor for .NET 库。您可以从[下载页面](https://releases.groupdocs.com/editor/net/).
## 导入命名空间
首先，您需要导入必要的命名空间。这样您就可以访问操作文档所需的类和方法。
```csharp
using System;
using GroupDocs.Editor.Metadata;
```
## 步骤 1：加载文档
首先，您需要加载要从中提取信息的文档。这可以通过提供文档的文件路径来完成。
```csharp
string docxInputFilePath = "YourSampleDocument.docx";
Editor editorDocx = new Editor(docxInputFilePath);
```
## 第 2 步：检索文档信息
接下来，您将使用`GetDocumentInfo`方法。如果您不确定文档格式，此方法不需要任何特定的加载选项。
```csharp
IDocumentInfo infoDocx = editorDocx.GetDocumentInfo(null);
```
## 步骤 3：确定文档类型
现在，您需要检查正在处理的文档类型。这很重要，因为它决定了您将如何处理该文档。
```csharp
bool isSpreadsheet = infoDocx is SpreadsheetDocumentInfo;
bool isText = infoDocx is TextualDocumentInfo;
bool isWordProcessing = infoDocx is WordProcessingDocumentInfo;
Console.WriteLine($"Is '{docxInputFilePath}' a Spreadsheet: {isSpreadsheet}");
Console.WriteLine($"Is '{docxInputFilePath}' a Textual document: {isText}");
Console.WriteLine($"Is '{docxInputFilePath}' a WordProcessing document: {isWordProcessing}");
```
## 步骤 4：提取详细信息
如果该文档是文字处理文档，您可以提取详细信息，例如格式、扩展名、页数、大小以及是否加密。
```csharp
if (isWordProcessing)
{
    WordProcessingDocumentInfo casted = (WordProcessingDocumentInfo)infoDocx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Page count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```
## 步骤 5：针对不同的文档类型重复上述步骤
对其他文档类型（如电子表格和文本文档）重复相同的步骤。
```csharp
string xlsxInputFilePath = "YourSampleDocument.xlsx";
Editor editorXlsx = new Editor(xlsxInputFilePath);
IDocumentInfo infoXlsx = editorXlsx.GetDocumentInfo(null);
bool isXlsxSpreadsheet = infoXlsx is SpreadsheetDocumentInfo;
Console.WriteLine($"Is '{xlsxInputFilePath}' a Spreadsheet: {isXlsxSpreadsheet}");
if (isXlsxSpreadsheet)
{
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo)infoXlsx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Tabs count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```
## 步骤6：处理受密码保护的文档
处理受密码保护的文档时，您应该首先尝试不使用密码来打开它们，然后使用错误密码来打开它们，最后使用正确密码来打开它们。
```csharp
string xlsInputFilePath = "YourSampleDocument.xls";
Editor editorXls = new Editor(xlsInputFilePath);
try
{
    IDocumentInfo infoXls = editorXls.GetDocumentInfo(null);
}
catch (PasswordRequiredException)
{
    Console.WriteLine("This document is password-protected.");
}
try
{
    IDocumentInfo infoXls = editorXls.GetDocumentInfo("incorrect_password");
}
catch (IncorrectPasswordException)
{
    Console.WriteLine("The provided password is incorrect.");
}
IDocumentInfo infoXlsValid = editorXls.GetDocumentInfo("correct_password");
bool isXlsSpreadsheet = infoXlsValid is SpreadsheetDocumentInfo;
Console.WriteLine($"Password-protected document is a Spreadsheet: {isXlsSpreadsheet}");
if (isXlsSpreadsheet)
{
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo)infoXlsValid;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Tabs count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```
## 步骤 7：处理基于文本的文档
```csharp
string xmlInputFilePath = "YourSampleDocument.xml";
Editor editorXml = new Editor(xmlInputFilePath);
IDocumentInfo infoXml = editorXml.GetDocumentInfo(null);
bool isXmlText = infoXml is TextualDocumentInfo;
Console.WriteLine($"Is '{xmlInputFilePath}' a Textual document: {isXmlText}");
if (isXmlText)
{
    TextualDocumentInfo casted = (TextualDocumentInfo)infoXml;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Encoding: {casted.Encoding}; Size: {casted.Size} bytes");
}
```
## 步骤 8：处置资源
最后，确保处置所有资源以防止内存泄漏。
```csharp
editorDocx.Dispose();
editorXlsx.Dispose();
editorXls.Dispose();
editorXml.Dispose();
Console.WriteLine("ExtractingDocumentInfo routine has successfully finished");
```
## 结论
恭喜！您现在已经学会了如何使用 GroupDocs.Editor for .NET 提取文档信息。这个功能强大的库简化了文档管理和操作，让您可以无缝处理各种文档类型。无论您处理的是文字处理、电子表格还是基于文本的文档，GroupDocs.Editor 都能提供强大的解决方案。
## 常见问题解答
### GroupDocs.Editor 可以处理哪些类型的文档？
GroupDocs.Editor 可以处理各种文档类型，包括文字处理、电子表格和基于文本的文档。
### GroupDocs.Editor 可以管理受密码保护的文档吗？
是的，GroupDocs.Editor 可以管理受密码保护的文档。只要输入正确的密码，它就能识别并打开这些文档。
### 是否有必要处置编辑器对象？
是的，处理编辑器对象以释放资源和防止内存泄漏至关重要。
### 我可以提取有关文档格式和大小的详细信息吗？
当然！GroupDocs.Editor 允许您提取详细信息，包括格式、扩展名、大小、页数和加密状态。
### 如果我遇到问题，可以在哪里获得支持？
您可以从[GroupDocs.Editor 支持论坛](https://forum.groupdocs.com/c/editor/20).