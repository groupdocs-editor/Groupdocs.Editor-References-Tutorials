---
date: 2026-06-01
description: 在本详细的分步教程中，了解如何使用 GroupDocs.Editor for .NET 获取页数并提取文档元数据。
keywords:
- get page count
- extract document metadata
- get document info
- find document extension
- retrieve document size
linktitle: 获取页数并提取文档信息
schemas:
- author: GroupDocs
  dateModified: '2026-06-01'
  description: Learn how to get page count and extract document metadata using GroupDocs.Editor
    for .NET in a detailed step‑by‑step tutorial.
  headline: Get Page Count & Extract Document Info with GroupDocs.Editor
  type: TechArticle
- questions:
  - answer: GroupDocs.Editor supports Word processing, spreadsheet, presentation,
      PDF, and plain‑text files—over 50 formats in total.
    question: What document types can I extract metadata from?
  - answer: Access `DocumentInfo.Extension` after calling `GetDocumentInfo()`; it
      returns the extension without the leading dot.
    question: How do I retrieve the file extension?
  - answer: Yes—`DocumentInfo.Size` returns the size in bytes; divide by 1,048,576
      to convert to megabytes.
    question: Can I get the size of a document in megabytes?
  - answer: Absolutely—GroupDocs.Editor never writes the password to disk and disposes
      of all cryptographic objects after use.
    question: Is it safe to process password‑protected files on a server?
  - answer: You can get support from the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).
    question: Where can I find additional help if I run into issues?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: 使用 GroupDocs.Editor 获取页数并提取文档信息
type: docs
url: /zh/net/document-processing/extract-document-info/
weight: 10
---

# 获取页面计数并提取文档信息（使用 GroupDocs.Editor）

## 介绍
在本综合教程中，您将学习如何使用 GroupDocs.Editor for .NET **获取页面计数** 并提取详细的文档信息——包括格式、大小和加密状态。无论您是在构建文档管理系统、报告引擎，还是自动化转换流水线，了解文件的元数据都是可靠处理的第一步。让我们从加载文件到安全释放资源，完整演示整个工作流。

## 快速答案
- **如何检索文档的页面计数？**  
  在使用 `Editor` 加载文件后，调用 `editor.GetDocumentInfo().PageCount`。
- **支持哪些文件格式进行元数据提取？**  
  超过 50 种格式，包括 DOCX、XLSX、PPTX、PDF、TXT 和 HTML。
- **我可以从受密码保护的文件中提取元数据吗？**  
  可以——在构造 `Editor` 实例时提供密码。
- **我需要手动释放资源吗？**  
  当然；始终调用 `editor.Dispose()` 或在 `using` 块中使用编辑器。
- **需要哪个版本的 GroupDocs.Editor？**  
  最新的稳定版（撰写时为 v23.12+）支持所有展示的功能。

## GroupDocs.Editor 中的“获取页面计数”是什么？
`GetDocumentInfo()` 是一个方法，返回包含文档页面计数、格式、大小和其他元数据的 `DocumentInfo` 对象。此单次调用即可让您立即获取信息，而无需手动解析文件。使用此方法可避免将整个文档加载到内存中，从而提升性能，尤其是对大文件，并降低服务器资源消耗。

## 为什么使用 GroupDocs.Editor 提取文档元数据？
GroupDocs.Editor 能处理 **50 多种输入和输出格式**，并可在不将整个文档加载到内存的情况下检索高达 **2 GB** 的文件元数据。与完整文档解析相比，这种效率可将服务器负载降低最多 **70 %**，非常适合高吞吐量的应用场景。

## 先决条件
- **C# 开发基础** – 您应熟悉 Visual Studio 和 .NET 项目结构。
- **Visual Studio 2022**（或任何近期版本）已安装在您的机器上。
- **GroupDocs.Editor for .NET** – 从[下载页面](https://releases.groupdocs.com/editor/net/)下载最新包。

## 如何加载文档？
`Editor` 是表示文档的主要类，提供加载和操作文档的方法。通过创建 `Editor` 实例并传入文件路径来加载目标文件。编辑器会自动检测格式，无需指定加载选项。此方法适用于任何受支持的文件类型，简化了初始设置。

```csharp
using System;
using GroupDocs.Editor.Metadata;
```

## 如何检索文档信息？
`GetDocumentInfo()` 返回一个包含页面计数、格式、大小和加密状态等元数据的 `DocumentInfo` 对象。加载后，调用此方法获取该对象。返回的 `DocumentInfo` 为文件特性提供简明快照，使您能够在无需进一步处理的情况下做出决策。

```csharp
string docxInputFilePath = "YourSampleDocument.docx";
Editor editorDocx = new Editor(docxInputFilePath);
```

## 如何确定文档类型？
`DocumentType` 是一个枚举，指示文档是 WordProcessing、Spreadsheet 还是 Text。了解文件是文字处理文档、电子表格还是纯文本会影响后续的处理方式。使用 `DocumentInfo` 对象的 `DocumentType` 属性来做出决定，并相应地分支您的逻辑。

```csharp
IDocumentInfo infoDocx = editorDocx.GetDocumentInfo(null);
```

## 如何提取 WordProcessing 文件的详细信息？
`WordProcessing` 指的是如 DOCX、ODT、RTF 等作为文字处理文件处理的文档。如果文档类型为 `WordProcessing`，您可以直接从 `DocumentInfo` 对象读取诸如 **format**、**extension**、**page count**、**size** 和 **encryption flag** 等附加属性。这些细节帮助您定制处理步骤，例如应用特定的转换或安全检查。

```csharp
bool isSpreadsheet = infoDocx is SpreadsheetDocumentInfo;
bool isText = infoDocx is TextualDocumentInfo;
bool isWordProcessing = infoDocx is WordProcessingDocumentInfo;
Console.WriteLine($"Is '{docxInputFilePath}' a Spreadsheet: {isSpreadsheet}");
Console.WriteLine($"Is '{docxInputFilePath}' a Textual document: {isText}");
Console.WriteLine($"Is '{docxInputFilePath}' a WordProcessing document: {isWordProcessing}");
```

## 如何处理 Spreadsheet 和 Text 文档？
`Spreadsheet` 表示如 XLSX 等电子表格文件，而 `Text` 代表纯文本文档。对于电子表格（`Spreadsheet`）和纯文本文件（`Text`），`DocumentInfo` 对象仍提供核心元数据（扩展名、大小、页面计数）。某些格式可能不提供页面计数，此时值为 `0`。您仍可依赖其他元数据进行后续逻辑处理。

```csharp
if (isWordProcessing)
{
    WordProcessingDocumentInfo casted = (WordProcessingDocumentInfo)infoDocx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Page count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```

## 如何处理受密码保护的文档？
`Password` 是传递给 `Editor` 构造函数以打开加密文件的字符串。当文档被加密时，首先尝试在不提供密码的情况下打开。如果失败，捕获异常，然后使用正确的密码重试。`Editor` 构造函数接受 `Password` 参数，以实现对受保护文件的无缝处理。

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

## 如何处理基于文本的文档？
`DocumentInfo` 为文本文件提供基本的元数据，如大小、扩展名和编码。文本文件（例如 `.txt`、`.md`）被视为简单流。您仍可从 `DocumentInfo` 获取大小和编码信息，这对于验证文件完整性或确定合适的处理流水线很有用。

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

## 如何正确释放资源？
`Editor` 是持有非托管资源的主要类，使用后必须释放。为避免内存泄漏，完成信息提取后始终释放 `Editor` 实例。`using` 语句是最安全的模式，因为它即使在出现异常时也能保证释放，从而确保资源管理的清洁。

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

## 常见问题及解决方案
| 问题 | 原因 | 解决方案 |
|-------|-------|----------|
| **PageCount 返回 0** | 格式不支持分页（例如纯文本） | 在依赖 `PageCount` 之前检查 `DocumentInfo.DocumentType`。 |
| **不支持的文件格式** | 文件扩展名未被识别 | 确认文件属于 50 多种受支持的格式之一；将 GroupDocs.Editor 更新至最新版本。 |
| **密码异常** | 提供的密码错误 | 捕获 `PasswordProtectedException` 并提示用户重新输入密码。 |
| **大文件内存激增** | 在未使用流式加载的情况下加载非常大的 PDF | 使用 `LoadOptions` 并将 `LoadOptions.LoadMode = LoadMode.Stream`（在新版本中可用）。 |

## 常见问题

**问：我可以从哪些文档类型提取元数据？**  
答：GroupDocs.Editor 支持文字处理、电子表格、演示文稿、PDF 和纯文本文件——共计超过 50 种格式。

**问：如何获取文件扩展名？**  
答：在调用 `GetDocumentInfo()` 后访问 `DocumentInfo.Extension`；它返回不带前导点的扩展名。

**问：我能以兆字节获取文档大小吗？**  
答：可以——`DocumentInfo.Size` 返回字节数；除以 1,048,576 即可转换为兆字节。

**问：在服务器上处理受密码保护的文件安全吗？**  
答：绝对安全——GroupDocs.Editor 从不将密码写入磁盘，且在使用后会释放所有加密对象。

**问：如果遇到问题，我可以在哪里获得更多帮助？**  
答：您可以在[GroupDocs.Editor 支持论坛](https://forum.groupdocs.com/c/editor/20)获取支持。

---

**最后更新：** 2026-06-01  
**测试环境：** GroupDocs.Editor 23.12 for .NET  
**作者：** GroupDocs

```csharp
editorDocx.Dispose();
editorXlsx.Dispose();
editorXls.Dispose();
editorXml.Dispose();
Console.WriteLine("ExtractingDocumentInfo routine has successfully finished");
```

## 相关教程

- [在 .NET 中使用 GroupDocs.Editor 的元数据提取大全指南](/editor/net/advanced-features/groupdocs-editor-net-metadata-extraction-guide/)
- [GroupDocs.Editor for .NET 文档加载教程](/editor/net/document-loading/)
- [使用 GroupDocs.Editor .NET 高效文档编辑：将 HTML 转换为可编辑文档](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)