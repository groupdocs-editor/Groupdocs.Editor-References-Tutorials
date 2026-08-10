---
date: 2026-08-10
description: 了解如何使用 GroupDocs.Editor for .NET 编辑纯文本文件。指南涵盖加载 txt 文件、去除空格、设置文本编码以及保存结果。
keywords:
- edit plain text
- load txt file
- trim trailing spaces
- convert leading spaces
- set text encoding
lastmod: 2026-08-10
linktitle: 处理纯文本文档
og_description: 了解如何使用 GroupDocs.Editor for .NET 编辑纯文本文件——加载 txt 文件、去除尾部空格、转换前导空格、设置文本编码，并高效保存。
og_image_alt: Guide showing edit plain text workflow with GroupDocs.Editor for .NET
og_title: 使用 GroupDocs.Editor for .NET 编辑纯文本文档
schemas:
- author: GroupDocs
  dateModified: '2026-08-10'
  description: Learn how to edit plain text files using GroupDocs.Editor for .NET.
    The guide covers loading a txt file, trimming spaces, setting text encoding, and
    saving the result.
  headline: Edit plain text documents with GroupDocs.Editor for .NET
  type: TechArticle
- description: Learn how to edit plain text files using GroupDocs.Editor for .NET.
    The guide covers loading a txt file, trimming spaces, setting text encoding, and
    saving the result.
  name: Edit plain text documents with GroupDocs.Editor for .NET
  steps:
  - name: Get a path to the input TXT file
    text: First, decide whether you’ll work with a physical file path or a memory
      stream. Using a path is the most straightforward approach for local development.
  - name: Create an Editor instance
    text: '`Editor` is the main class that loads a document and provides editing capabilities.'
  - name: Create TXT editing options
    text: '`TxtEditOptions` configures how plain‑text files are parsed and edited,
      allowing you to set encoding and space‑handling rules.'
  - name: Create an EditableDocument instance
    text: '`EditableDocument` represents the in‑memory version of the loaded document,
      including its text and any associated resources.'
  - name: Edit the document content
    text: Retrieve the original text, apply any string operations you need (e.g.,
      replace, trim, change case), and store the result back into the `EditableDocument`.
  - name: Create an EditableDocument with updated content
    text: After you’ve transformed the text, instantiate a new `EditableDocument`
      that contains the edited string and the original resource collection.
  - name: Create WordProcessing save options
    text: '`WordProcessingSaveOptions` defines settings for saving the document in
      a Word‑compatible format such as DOCX or DOCM.'
  - name: Create TXT saving options
    text: '`TxtSaveOptions` specifies how the edited plain‑text file should be written,
      including encoding, line‑ending preservation, and table layout handling.'
  - name: Prepare output paths
    text: Derive the output directory from the input file path, then build the full
      filenames for the DOCX and TXT results.
  - name: Save the edited document
    text: Finally, call `editor.Save` twice—once with the WordProcessing options and
      once with the TXT options—to produce both formats in a single operation.
  type: HowTo
- questions:
  - answer: The library supports 50+ formats, including DOCX, TXT, HTML, PDF, and
      markdown, allowing you to edit and convert between them seamlessly.
    question: What file formats does GroupDocs.Editor for .NET support?
  - answer: Download the trial from the [releases page](https://releases.groupdocs.com/).
    question: How can I get a free trial of GroupDocs.Editor for .NET?
  - answer: Yes, temporary licenses are available through the [GroupDocs purchase
      page](https://purchase.groupdocs.com/temporary-license/).
    question: Can I purchase a temporary license for testing?
  - answer: The official support forum is the best place – visit the [GroupDocs.Editor
      support forum](https://forum.groupdocs.com/c/editor/20).
    question: Where can I find support if I run into issues?
  - answer: Absolutely. The full reference is on the [GroupDocs.Editor documentation
      page](https://tutorials.groupdocs.com/editor/net/).
    question: Is there detailed documentation for advanced scenarios?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
tags:
- edit plain text
- GroupDocs.Editor
- C# document processing
- plain text editing
- txt file handling
title: 使用 GroupDocs.Editor for .NET 编辑纯文本文档
type: docs
url: /zh/net/document-processing/work-plain-text-documents/
weight: 15
---

# 使用 GroupDocs.Editor for .NET 编辑纯文本文档

## 介绍
如果您需要在 .NET 应用程序中快速且可靠地 **编辑纯文本**，GroupDocs.Editor for .NET 是完成繁重工作的重要工具。该 API 支持 30 多种文档格式，能够处理高达 500 MB 的文件，并且让您在不将整个文件加载到内存中的情况下操作文本。在本教程中，您将学习如何加载 txt 文件、去除行尾空格、转换前导空格、设置正确的编码，最后将编辑后的内容保存回磁盘。准备好动手了吗？让我们开始吧！

## 快速答案
- **编辑 txt 文件的第一步是什么？** 使用 `Editor` 加载文件，使用您拥有的路径或流。  
- **编辑时我可以更改文件编码吗？** 可以——`TxtSaveOptions` 允许您指定 UTF‑8、UTF‑16 或任何自定义编码。  
- **如何删除每行末尾的多余空格？** 获取文本，对每行调用 `TrimEnd()`，然后写回。  
- **GroupDocs.Editor 可以免费试用吗？** 可在发布页面获取功能完整的 30 天试用版。  
- **支持哪些 .NET 版本？** .NET Framework 4.6+、.NET Core 3.1+ 和 .NET 5/6/7。

## 什么是编辑纯文本？
**编辑纯文本** 是指以编程方式更改简单 `.txt` 文件中的字符——添加、删除或重新格式化文本——同时保留文件的原始编码和换行样式。它可能涉及修剪空白、规范化换行符、更新配置值或插入生成的内容等任务。此操作应保持文件可被任何标准文本编辑器读取，并保留诸如 BOM 标记等现有元数据。

## 为什么使用 GroupDocs.Editor 进行纯文本编辑？
GroupDocs.Editor 以流式方式处理文件，这意味着它可以使用不到 50 MB 的 RAM 编辑 300 MB 的日志文件。该库支持 **50+ 输入和输出格式**，自动检测换行样式（CR、LF、CRLF），并提供内置选项来 **去除尾随空格** 和 **转换前导空格**，无需编写自定义解析器。

## 前提条件
- **.NET 开发环境** – Visual Studio 2022 或带 C# 扩展的 VS Code。  
- **GroupDocs.Editor for .NET** – 从 [GroupDocs.Editor for .NET](https://releases.groupdocs.com/editor/net/) 发布页面下载。  
- **基本的 C# 知识** – 您应该熟悉文件 I/O 和字符串操作。  
- **文本编辑器（可选）** – 用于检查源文件；推荐使用 VS Code。  
- 有关详细用法，请参阅 [文档](https://tutorials.groupdocs.com/editor/net/)。  
- 您也可以浏览通用的 [发布页面](https://releases.groupdocs.com/)。

## 如何一步步编辑纯文本
加载文件、编辑其内容并保存回去——全部代码不超过十行。以下章节将逐步带您了解每个阶段，并提供清晰的说明。

### 步骤 1：获取输入 TXT 文件的路径
首先，决定是使用物理文件路径还是内存流。对于本地开发，使用路径是最直接的方式。

```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

### 步骤 2：创建 Editor 实例
`Editor` 是加载文档并提供编辑功能的主要类。

```csharp
string inputFilePath = "YourSampleDocument.txt";
```

### 步骤 3：创建 TXT 编辑选项
`TxtEditOptions` 配置纯文本文件的解析和编辑方式，允许您设置编码和空格处理规则。

```csharp
using (Editor editor = new Editor(inputFilePath))
{
```

### 步骤 4：创建 EditableDocument 实例
`EditableDocument` 表示已加载文档的内存版本，包括其文本和任何关联资源。

```csharp
    TextEditOptions editOptions = new TextEditOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        RecognizeLists = true,
        LeadingSpaces = TextLeadingSpacesOptions.ConvertToIndent,
        TrailingSpaces = TextTrailingSpacesOptions.Trim
    };
```

### 步骤 5：编辑文档内容
获取原始文本，应用所需的字符串操作（例如替换、修剪、大小写转换），并将结果存回 `EditableDocument`。

```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```

### 步骤 6：使用更新的内容创建 EditableDocument
在转换文本后，实例化一个新的 `EditableDocument`，其中包含编辑后的字符串和原始资源集合。

```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("text", "EDITED text");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```

### 步骤 7：创建 WordProcessing 保存选项
`WordProcessingSaveOptions` 定义将文档保存为 Word 兼容格式（如 DOCX 或 DOCM）的设置。

```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```

### 步骤 8：创建 TXT 保存选项
`TxtSaveOptions` 指定编辑后的纯文本文件应如何写入，包括编码、换行保留以及表格布局处理。

```csharp
    WordProcessingSaveOptions wordSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm)
    {
        Locale = System.Globalization.CultureInfo.GetCultureInfo("en-GB")
    };
```

### 步骤 9：准备输出路径
从输入文件路径派生输出目录，然后构建 DOCX 和 TXT 结果的完整文件名。

```csharp
    TextSaveOptions txtSaveOptions = new TextSaveOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        PreserveTableLayout = true
    };
```

### 步骤 10：保存编辑后的文档
最后，调用 `editor.Save` 两次——一次使用 WordProcessing 选项，一次使用 TXT 选项，以一次操作生成两种格式。

```csharp
    string outputWordPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".docm");
    string outputTxtPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".txt");
```

## 常见问题及解决方案
- **编辑后仍然存在尾随空格** – 确保在加载文档前将 `TxtEditOptions.TrimTrailingSpaces` 设置为 `true`。  
- **保存的文件编码不正确** – 验证 `TxtSaveOptions.Encoding` 与所需的代码页匹配（例如 `Encoding.UTF8`）。  
- **大文件导致 OutOfMemoryException** – 使用流式 API（`Editor.Load(Stream)`）而不是从文件路径加载，以保持低内存使用。  

## 常见问题

**Q: GroupDocs.Editor for .NET 支持哪些文件格式？**  
A: 该库支持 50+ 格式，包括 DOCX、TXT、HTML、PDF 和 markdown，能够无缝编辑和相互转换。

**Q: 我如何获取 GroupDocs.Editor for .NET 的免费试用？**  
A: 从 [发布页面](https://releases.groupdocs.com/) 下载试用版。

**Q: 我可以购买临时许可证用于测试吗？**  
A: 可以，临时许可证可通过 [GroupDocs 购买页面](https://purchase.groupdocs.com/temporary-license/) 获取。

**Q: 如果遇到问题，我可以在哪里获得支持？**  
A: 官方支持论坛是最佳渠道——访问 [GroupDocs.Editor 支持论坛](https://forum.groupdocs.com/c/editor/20)。

**Q: 是否有针对高级场景的详细文档？**  
A: 当然。完整参考位于 [GroupDocs.Editor 文档页面](https://tutorials.groupdocs.com/editor/net/)。

## 结论
您现在已经掌握了使用 GroupDocs.Editor for .NET **编辑纯文本** 文件的全部技巧——加载 txt 文件、修剪空格、转换前导空格、设置正确的编码，并将结果保存为 TXT 和 DOCX 两种格式。此功能让您能够自动化日志文件清理、即时生成配置文件，或构建自定义文本处理流水线，而无需重复造轮子。通过访问官方文档，探索批处理、文档转换等更多功能。

---

**最后更新：** 2026-08-10  
**测试环境：** GroupDocs.Editor 23.11 for .NET  
**作者：** GroupDocs  

---

```csharp
    editor.Save(afterEdit, outputWordPath, wordSaveOptions);
    editor.Save(afterEdit, outputTxtPath, txtSaveOptions);
}
System.Console.WriteLine("Document editing process completed successfully!");
```

## 相关教程

- [使用 GroupDocs.Editor for .NET 的文档加载教程](/editor/net/document-loading/)
- [GroupDocs.Editor .NET 的文档保存和导出教程](/editor/net/document-saving/)
- [GroupDocs.Editor .NET 的纯文本和 DSV 文档编辑教程](/editor/net/plain-text-dsv-documents/)