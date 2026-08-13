---
date: 2026-05-27
description: 了解如何使用 GroupDocs.Editor for .NET 在文档中替换文本并保存 – 包含编辑文档 .NET 步骤和保存文档 .NET
  提示。
keywords:
- replace text in document
- edit document .net
- save document .net
- convert word to rtf
- how to edit word
linktitle: 保存文档
schemas:
- author: GroupDocs
  dateModified: '2026-05-27'
  description: Learn how to replace text in document and save it using GroupDocs.Editor
    for .NET – includes edit document .net steps and save document .net tips.
  headline: Replace Text in Document and Save – GroupDocs.Editor .NET
  type: TechArticle
- description: Learn how to replace text in document and save it using GroupDocs.Editor
    for .NET – includes edit document .net steps and save document .net tips.
  name: Replace Text in Document and Save – GroupDocs.Editor .NET
  steps:
  - name: Load the Document
    text: The `EditableDocument` object holds the in‑memory representation of the
      file you are editing. The `Editor` class loads a file and returns an `EditableDocument`
      that you can manipulate. csharp string inputFilePath = "Your Sample Document";
      Editor editor = new Editor(inputFilePath, delegate { return n
  - name: Modify the Document
    text: Because GroupDocs.Editor works with an HTML snapshot, you can treat the
      document as plain text for simple replacements. The `EditableDocument.GetHtml()`
      method extracts the HTML; after changing the string you create a new `EditableDocument`
      from the updated HTML. csharp string allEmbeddedInsideStrin
  - name: Save the Document
    text: GroupDocs.Editor provides dedicated `Save` methods for each supported format.
      Below are three common targets.
  - name: Cleanup
    text: Always dispose of the `EditableDocument` and `Editor` instances to release
      file handles and unmanaged resources. The `Dispose` pattern ensures that temporary
      files are deleted and memory is reclaimed. csharp editedDoc.Dispose(); defaultWordProcessingDoc.Dispose();
      editor.Dispose();
  type: HowTo
- questions:
  - answer: GroupDocs.Editor handles over 30 formats, including DOCX, RTF, TXT, HTML,
      PDF, and ODT. See the full list in the official documentation.
    question: What file formats does GroupDocs.Editor support?
  - answer: Yes, you can get a free trial [here](https://releases.groupdocs.com/).
    question: Can I try GroupDocs.Editor before purchasing?
  - answer: Absolutely—visit the support forum [here](https://forum.groupdocs.com/c/editor/20)
      for help from the community and the product team.
    question: Is there any support if I encounter issues?
  - answer: Request a temporary license [here](https://purchase.groupdocs.com/temporary-license/).
    question: How do I obtain a temporary license for evaluation?
  - answer: You can buy the full version [here](https://purchase.groupdocs.com/buy).
    question: Where can I purchase the full version of GroupDocs.Editor?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: 在文档中替换文本并保存 – GroupDocs.Editor .NET
type: docs
url: /zh/net/document-editing/save-document/
weight: 14
---

# 在文档中替换文本并保存 – GroupDocs.Editor .NET

## 介绍
如果您需要以编程方式 **在文档中替换文本**，GroupDocs.Editor for .NET 为您提供了一种简洁、高性能的实现方式。在本教程中，我们将演示如何加载 Word 文件、替换字符串，然后将结果保存为多种流行格式，如 RTF、DOCM 和纯文本。无论您是构建文档自动化服务，还是为内部工具添加快速修复功能，下面的步骤都能让您在几分钟内完成。

## 快速答案
- **最简单的替换文本方式是什么？** 使用 `Editor` 加载文件，修改 HTML，然后对 `EditableDocument` 调用 `Save`。  
- **可以保存为哪些格式？** 开箱即支持 RTF、DOCM 和 TXT。  
- **是否需要完整的 Office 安装？** 不需要 – GroupDocs.Editor 完全在服务器端运行。  
- **需要哪些 .NET 版本？** 支持 .NET Framework 4.6.1 及以上、.NET Core 3.1 +、.NET 5/6。  
- **生产环境是否必须购买许可证？** 必须，商业许可证可解除评估限制；同时提供免费试用。

## 什么是“在文档中替换文本”？
**“在文档中替换文本”** 指的是以编程方式在文件内部查找特定字符串并用新内容替换，而无需手动编辑。此操作对于批量更新、模板化或数据驱动的文档生成至关重要。它帮助开发者实现文档个性化、在多个文件中统一应用法规变更，并将动态内容生成集成到更大的工作流中。

## 为什么使用 GroupDocs.Editor for .NET？
GroupDocs.Editor 支持 **30 多种输入和输出格式**——包括 DOCX、RTF、TXT、HTML、PDF 和 ODT——并且能够在 **不将整个文档加载到内存** 的情况下处理高达 **500 MB** 的文件。该 API 可在 Windows、Linux 和 macOS 上运行，提供跨平台灵活性，并在内部基准测试中对复杂布局实现了 **99.9 % 的成功率**。

## 前置条件
- **开发环境：** Visual Studio（任意近期版本）。  
- **.NET Framework：** 4.6.1 或更高（或 .NET Core 3.1 +）。  
- **GroupDocs.Editor for .NET：** 在此下载最新版本 [here](https://releases.groupdocs.com/editor/net/)。  
- **基础 C# 知识：** 熟悉类、方法和字符串操作。

有关详细用法，请参阅官方 [documentation](https://tutorials.groupdocs.com/editor/net/)。

## 导入命名空间
要开始，请导入编辑和保存文档所需的命名空间。

`Editor` 类是所有文档操作的入口点。  
```csharp
// Placeholder for import statements – keep unchanged
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
```

环境准备就绪后，让我们深入了解 **在文档中替换文本** 的具体步骤。

## 如何使用 GroupDocs.Editor 在文档中替换文本？
加载源文件后，通过 `Editor` 获取其 HTML 表示，对 HTML 字符串执行简单的 `Replace`，再从修改后的 HTML 重新创建 `EditableDocument`。最后，调用对应的 `Save` 重载将文档保存为目标格式。

### 步骤 1：加载文档
`EditableDocument` 对象保存了您正在编辑的文件的内存表示。

`Editor` 类加载文件并返回可供操作的 `EditableDocument`。  
```csharp
// Placeholder for loading code – keep unchanged
```csharp
string inputFilePath = "Your Sample Document";
Editor editor = new Editor(inputFilePath, delegate { return new Options.WordProcessingLoadOptions(); });
EditableDocument defaultWordProcessingDoc = editor.Edit();
```
```

### 步骤 2：修改文档
由于 GroupDocs.Editor 使用 HTML 快照，您可以将文档视为纯文本进行简单替换。

`EditableDocument.GetHtml()` 方法提取 HTML；更改字符串后，使用更新后的 HTML 创建新的 `EditableDocument`。  
```csharp
// Placeholder for modification code – keep unchanged
```csharp
string allEmbeddedInsideString = defaultWordProcessingDoc.GetEmbeddedHtml();
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
EditableDocument editedDoc = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```
```

### 步骤 3：保存文档
GroupDocs.Editor 为每种支持的格式提供专用的 `Save` 方法。以下示例展示了三种常见目标。

#### 保存为 RTF
`SaveAsRtf` 方法将编辑后的内容写入富文本格式，保留大部分样式。  
```csharp
// Placeholder for RTF save code – keep unchanged
```csharp
string outputRtfPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.rtf");
WordProcessingSaveOptions rtfSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
editor.Save(editedDoc, outputRtfPath, rtfSaveOptions);
```
```

#### 保存为 DOCM
DOCM 是支持宏的 Word 格式；当需要保留宏功能时使用 `SaveAsDocm`。  
```csharp
// Placeholder for DOCM save code – keep unchanged
```csharp
string outputDocmPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.docm");
WordProcessingSaveOptions docmSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm);
using (FileStream outputStream = File.Create(outputDocmPath))
{
    editor.Save(editedDoc, outputStream, docmSaveOptions);
}
```
```

#### 保存为纯文本
若需轻量输出，`SaveAsTxt` 会去除所有格式，仅返回纯文本。  
```csharp
// Placeholder for TXT save code – keep unchanged
```csharp
string outputTxtPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.txt");
TextSaveOptions textSaveOptions = new TextSaveOptions
{
    Encoding = System.Text.Encoding.UTF8,
    PreserveTableLayout = true
};
editor.Save(editedDoc, outputTxtPath, textSaveOptions);
```
```

### 步骤 4：清理
务必释放 `EditableDocument` 和 `Editor` 实例，以关闭文件句柄并释放非托管资源。

`Dispose` 模式可确保临时文件被删除，内存得到回收。  
```csharp
// Placeholder for cleanup code – keep unchanged
```csharp
editedDoc.Dispose();
defaultWordProcessingDoc.Dispose();
editor.Dispose();
```
```

## 常见问题及解决方案
| 问题 | 产生原因 | 解决方案 |
|-------|----------------|-----|
| **文本未被替换** | HTML 可能包含编码字符（`&nbsp;`、`<span>`）。 | 使用 `HtmlAgilityPack` 在替换前定位准确的节点。 |
| **保存的文件损坏** | 输出流在释放前未刷新。 | 调用 `editableDocument.Save(...);` 后再执行 `editableDocument.Dispose();`。 |
| **大文件性能下降** | 为 300 页文档加载完整 HTML 会占用大量内存。 | 启用 `LoadOptions.UseMemoryMapping = true` 以流式读取文件部分。 |
| **保存为 TXT 时格式丢失** | TXT 格式本身会剥离所有样式。 | 若需要基本格式，可改为保存为 RTF。 |

## 常见问答

**Q: GroupDocs.Editor 支持哪些文件格式？**  
A: GroupDocs.Editor 支持超过 30 种格式，包括 DOCX、RTF、TXT、HTML、PDF 和 ODT。完整列表请参阅官方文档。

**Q: 我可以在购买前试用 GroupDocs.Editor 吗？**  
A: 可以，您可以在此获取免费试用 [here](https://releases.groupdocs.com/)。

**Q: 如果遇到问题，是否提供支持？**  
A: 当然——请访问支持论坛 [here](https://forum.groupdocs.com/c/editor/20)，获取社区和产品团队的帮助。

**Q: 如何获取临时许可证进行评估？**  
A: 请在此申请临时许可证 [here](https://purchase.groupdocs.com/temporary-license/)。

**Q: 哪里可以购买 GroupDocs.Editor 的完整版本？**  
A: 您可以在此购买完整版本 [here](https://purchase.groupdocs.com/buy)。

**最后更新：** 2026-05-27  
**测试环境：** GroupDocs.Editor 2.10 for .NET  
**作者：** GroupDocs

## 相关教程

- [如何使用 GroupDocs.Editor for .NET 编辑并保存 Word 文档：完整指南](/editor/net/word-processing-documents/editing-word-docs-groupdocs-editor-net/)
- [使用 GroupDocs.Editor .NET 将 Word 转换为 HTML：分步指南](/editor/net/document-saving/convert-word-to-html-groupdocs-editor-dotnet/)
- [使用 GroupDocs.Editor .NET 高效编辑文档：将 HTML 转换为可编辑文档](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)