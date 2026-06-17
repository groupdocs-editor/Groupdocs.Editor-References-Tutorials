---
date: 2026-04-11
description: 在本详细的分步指南中，学习如何使用 GroupDocs.Editor for .NET 以编程方式编辑 Word 文档并将 Word 转换为
  RTF。
keywords:
- programmatically edit word document
- convert pdf to editable
- replace text in document
- convert word to rtf
- save document to stream
linktitle: 使用 GroupDocs.Editor for .NET 以编程方式编辑 Word 文档
second_title: GroupDocs.Editor .NET API
title: 使用 GroupDocs.Editor for .NET 以编程方式编辑 Word 文档
type: docs
url: /zh/net/document-editing/introduction-groupdocs-editor/
weight: 12
---

# 使用 GroupDocs.Editor for .NET 编程编辑 Word 文档

如果您是需要 **以编程方式编辑 Word 文档** 文件的 .NET 开发者——无论是替换文本、转换格式，还是将结果嵌入流中——GroupDocs.Editor for .NET 是一个强大且易于使用的库，能够完成此任务。在本教程中，我们将演示一个实际示例，涵盖加载 DOCX 文件、编辑其内容、将结果转换为 RTF，并将其保存到磁盘或内存流中。

## 快速答案
- **我可以编辑什么？** Word、PDF、HTML、RTF 以及许多其他格式。  
- **我可以替换文本吗？** 可以——使用简单的字符串替换或更高级的 DOM 操作。  
- **如何将 PDF 转换为可编辑？** 使用 `Editor` 加载 PDF 并编辑生成的 HTML。  
- **保存到流的最简方法是什么？** 使用 `editor.Save(editableDoc, stream, options)`。  
- **我需要许可证吗？** 生产环境需要临时许可证或正式许可证。

## 什么是以编程方式编辑 Word 文档？
以编程方式编辑 Word 文档是指使用代码——而非用户界面——打开文件、修改其内容（文本、图像、样式），并将修改后的版本写回存储。这种方式支持自动化报告、大批量文档更新以及自定义内容生成。

## 为什么使用 GroupDocs.Editor for .NET？
- **格式灵活性：** 加载 DOCX、PDF、HTML、RTF 等，并保存为任何受支持的格式。  
- **无 Office 依赖：** 在服务器上无需安装 Microsoft Office 即可运行。  
- **流友好：** 适用于从流而非文件系统读取/写入的云场景。  
- **丰富的 API：** 可访问图像、字体、CSS 等资源，实现完整功能的编辑。

## 前置条件
在深入实现之前，请确保您具备以下条件：

- Visual Studio 2017 或更高版本。  
- .NET Framework 4.6.1 或更高版本。  
- GroupDocs.Editor for .NET —— 您可以从网站[下载](https://releases.groupdocs.com/editor/net/)。  
- 来自 GroupDocs 的有效许可证或[临时许可证](https://purchase.groupdocs.com/temporary-license/)。

## 导入命名空间
要开始使用 GroupDocs.Editor for .NET，请导入所需的命名空间：

```csharp
using System;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```

在接下来的章节中，我们将把工作流拆分为易于跟随的步骤。

## 步骤 1：获取输入文件的路径
指定要编辑的 Word 文件的位置。此示例中我们假设有一个名为 **Your Sample Document.docx** 的 DOCX 文件。

```csharp
string inputFilePath = "Your Sample Document.docx";
```

## 步骤 2：实例化 Editor 对象
通过传入输入路径创建 `Editor` 实例。这会加载文档并为编辑做好准备。

```csharp
using (GroupDocs.Editor.Editor editor = new Editor(inputFilePath))
{
    // Subsequent steps will be nested inside this block
}
```

## 步骤 3：打开文档进行编辑
获取 `EditableDocument`，它提供对文档 HTML 表示及其资源的访问。

```csharp
EditableDocument beforeEdit = editor.Edit();
```

## 步骤 4：检索文档内容和资源
您可以提取原始 HTML、图像、字体和 CSS。当需要直接操作标记时，这非常有用。

```csharp
string content = beforeEdit.GetContent();
var images = beforeEdit.Images;
var fonts = beforeEdit.Fonts;
var stylesheets = beforeEdit.Css;
```

### 步骤 4.1：获取文档的单个 Base64 编码字符串
如果您希望使用包含所有嵌入资源的单个字符串，请调用 `GetEmbeddedHtml()`。

```csharp
string allEmbeddedInsideString = beforeEdit.GetEmbeddedHtml();
```

### 步骤 4.2：编辑内容
让我们将单词 **Subtitle** 替换为 **Edited subtitle**，演示一次简单的文本替换。

```csharp
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
```

## 步骤 5：创建新的 EditableDocument 实例
编辑完标记后，将其重新包装为 `EditableDocument` 对象。

```csharp
EditableDocument afterEdit = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```

## 步骤 6：保存编辑后的文档
我们将把结果保存为 RTF 文件，展示文件系统路径和内存流两种方式。

### 步骤 6.1：准备输出路径
定义 RTF 文件的写入位置。

```csharp
string outputPath = Path.Combine("Output Directory Path", Path.GetFileNameWithoutExtension(inputFilePath) + ".rtf");
```

### 步骤 6.2：准备保存选项
通过 `WordProcessingSaveOptions` 选择 RTF 格式。

```csharp
Options.WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
```

### 步骤 6.3：保存到路径
将编辑后的文档写入文件系统。

```csharp
editor.Save(afterEdit, outputPath, saveOptions);
```

### 步骤 6.4：保存到流
如果需要将结果保存在内存中（例如上传到云存储），请使用 `MemoryStream`。

```csharp
using (MemoryStream ms = new MemoryStream())
{
    editor.Save(afterEdit, ms, saveOptions);
}
```

## 步骤 7：释放 Editor 和 EditableDocument 实例
及时释放资源以避免内存泄漏。

```csharp
beforeEdit.Dispose();
afterEdit.Dispose();
editor.Dispose();
```

## 常见用例与技巧
- **将 PDF 转换为可编辑：** 使用 `Editor` 加载 PDF，编辑生成的 HTML，然后保存回 PDF 或其他格式。  
- **替换文档中的文本：** 对于简单情况使用 `string.Replace`，复杂场景则操作 DOM。  
- **将 Word 转换为 RTF：** 如上所示，在保存选项中设置 `WordProcessingFormats.Rtf`。  
- **将文档保存到流：** 适用于直接向客户端返回文件的 Web API。  
- **加载文档进行编辑：** 始终将 `Editor` 包装在 `using` 块中，以确保正确释放。

## 常见问题

**问：我可以使用 GroupDocs.Editor for .NET 编辑 PDF 文件吗？**  
答：可以，GroupDocs.Editor 通过将 PDF 转换为中间 HTML 表示来支持编辑。

**问：如何获取 GroupDocs.Editor for .NET 的临时许可证？**  
答：您可以从 [GroupDocs 网站](https://purchase.groupdocs.com/temporary-license/)获取临时许可证。

**问：GroupDocs.Editor for .NET 支持哪些文件格式？**  
答：支持 DOCX、PDF、HTML、RTF 以及许多其他格式。

**问：是否可以将 GroupDocs.Editor 与云存储集成？**  
答：完全可以——您可以从 Azure Blob、Amazon S3、Google Cloud Storage 等读取/写入流。

**问：在哪里可以找到 GroupDocs.Editor for .NET 的文档？**  
答：文档可在[此处](https://tutorials.groupdocs.com/editor/net/)获取。

---

**最后更新：** 2026-04-11  
**测试环境：** GroupDocs.Editor 23.12 for .NET  
**作者：** GroupDocs