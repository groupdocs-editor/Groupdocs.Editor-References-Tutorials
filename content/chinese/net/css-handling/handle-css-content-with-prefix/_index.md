---
date: 2026-09-26
description: 在本详细的分步教程中，了解如何使用 GroupDocs.Editor for .NET 处理 css 前缀并提取 css 内容。
keywords:
- handle css prefix
- extract css content
- edit document css
- prepend url to css
lastmod: 2026-09-26
linktitle: 使用前缀处理 CSS 内容
og_description: 了解如何使用 GroupDocs.Editor for .NET 处理 css 前缀并提取 css 内容。按照分步指南，将 URLs
  添加到 CSS 资源前缀并检索样式表。
og_image_alt: Developer guide showing css prefix handling with GroupDocs.Editor for
  .NET
og_title: 如何在 GroupDocs.Editor for .NET 中处理 css 前缀
schemas:
- author: GroupDocs
  dateModified: '2026-09-26'
  description: Learn how to handle css prefix and extract css content using GroupDocs.Editor
    for .NET in this detailed step‑by‑step tutorial.
  headline: How to handle css prefix in GroupDocs.Editor for .NET
  type: TechArticle
- questions:
  - answer: Yes, GroupDocs.Editor for .NET supports PDF, Word, Excel, PowerPoint,
      and many other formats.
    question: Can I use GroupDocs.Editor for .NET with other document formats?
  - answer: Absolutely! You can start your free trial on the [GroupDocs free trial
      page](https://releases.groupdocs.com/).
    question: Is there a free trial available for GroupDocs.Editor for .NET?
  - answer: You can obtain a temporary license from the [temporary license page](https://purchase.groupdocs.com/temporary-license/).
    question: How do I get a temporary license for GroupDocs.Editor for .NET?
  - answer: Detailed documentation is available on the [GroupDocs.Editor for .NET
      documentation site](https://tutorials.groupdocs.com/editor/net/).
    question: Where can I find detailed documentation for GroupDocs.Editor for .NET?
  - answer: You can get support through the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).
    question: What support options are available for GroupDocs.Editor for .NET?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
tags:
- css handling
- GroupDocs.Editor
- .NET document processing
- css prefix
- api tutorial
title: 如何在 GroupDocs.Editor for .NET 中处理 css 前缀
type: docs
url: /zh/net/css-handling/handle-css-content-with-prefix/
weight: 11
---

# 如何在 GroupDocs.Editor for .NET 中处理 css 前缀

在本教程中，您将学习 **如何处理 css 前缀**，在使用 GroupDocs.Editor for .NET 处理文档内部样式表时，无论是需要为图像、字体或任何外部资源添加 URL 前缀，下面的步骤都将准确展示 **如何处理 css 前缀**，以及 **如何提取 css 内容** 以便进一步处理。完成本指南后，您将能够重写资源路径、获取原始 CSS 字符串，并自信地将其集成到您的 Web 工作流中。

## 快速答案
- **“handle css prefix” 是什么意思？** 在 CSS 中为外部资源添加自定义 URL 前缀。  
- **哪个 API 方法返回 CSS 样式？** `EditableDocument.GetCssContent(...)`。  
- **我需要许可证吗？** 提供试用许可证；生产环境需要商业许可证。  
- **支持哪些 .NET 版本？** .NET Framework 4.5+ 和 .NET Core/5/6。  
- **我可以在运行时更改前缀吗？** 可以——只需向 `GetCssContent` 传递不同的字符串。

## 什么是 handle css prefix？
该术语指的是重写 CSS 文件中图像、字体或任何外部资源的 URL，使其指向您控制的位置，例如 CDN 或安全服务器。通过在所有资源前统一添加基准 URL，您可以确保文档在浏览器或基于 Web 的查看器中渲染时，所有资源都能正确加载。

## 为什么使用 GroupDocs.Editor 提取 css 内容？
GroupDocs.Editor 能读取嵌入在 WordProcessing 文档中的原始 CSS，返回原始样式表字符串，并允许您在渲染或保存之前对其进行操作。这消除了手动解析的需求，保证了对文档内部表示的忠实度，并支持 **30+ 种文件格式**，在处理高达 **500 MB** 的文件时无需将整个文件加载到内存中。

## 前提条件
在开始之前，请确保您已具备以下条件：
- Visual Studio：您需要已安装的 Visual Studio。  
- .NET Framework：确保已安装 .NET Framework。  
- GroupDocs.Editor for .NET：您可以从 [GroupDocs.Editor for .NET 下载页面](https://releases.groupdocs.com/editor/net/) 下载。  
- 示例文档：准备好用于编辑的示例文档。

## 导入命名空间
首先，让我们导入必要的命名空间，以确保代码顺利运行。此步骤为我们提供了访问 GroupDocs.Editor 核心类的权限。

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Editor.Options;
```

## 步骤 1：初始化 Editor
`Editor` 类是使用 GroupDocs.Editor 处理文档的入口点。它管理加载、编辑和保存操作。  
第一步是使用您的示例文档创建一个 `Editor` 实例。这将设置编辑环境。

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```

## 步骤 2：编辑文档
`EditableDocument` 对象代表文件的可编辑版本，并公开其内部部分，如 CSS、图像和 HTML。  
接下来，我们获取一个 `EditableDocument` 对象。该对象允许我们操作文档内部的 CSS。

```csharp
    using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
    {
```

## 步骤 3：设置外部前缀
为图像和字体定义 URL 前缀。这些前缀将被添加到 CSS 中找到的每个图像和字体引用前。

```csharp
        string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
        string externalFontsPrefix = "http://www.mywebsite.com/fonts/id=";
```

## 步骤 4：使用前缀提取 css 内容
`GetCssContent` 返回一组已经包含您提供的前缀 URL 的 CSS 样式表字符串。  
调用 `GetCssContent`，传入刚才定义的前缀。该方法返回的列表已包含前缀 URL 的 CSS 样式表字符串。

```csharp
        List<string> stylesheets = document.GetCssContent(externalImagesPrefix, externalFontsPrefix);
```

## 步骤 5：输出结果
打印找到的样式表数量并显示每个样式表。这有助于您验证前缀是否已正确应用。

```csharp
        Console.WriteLine("There are {0} stylesheets in the input document", stylesheets.Count);
        foreach (string css in stylesheets)
        {
            Console.WriteLine(css);
        }
    }
}
```

## 常见问题及解决方案
- **未返回样式表** – 确保源文档实际包含 CSS（例如，包含样式表格或嵌入 HTML 的 Word 文档）。  
- **URL 不正确** – 再次检查前缀字符串是否以适当的分隔符（`/` 或 `=`）结尾，以匹配服务器路由。  
- **性能问题** – 对于非常大的文档，考虑分批处理样式表以避免高内存使用。

## 常见问答

**Q: 我可以将 GroupDocs.Editor for .NET 与其他文档格式一起使用吗？**  
A: 是的，GroupDocs.Editor for .NET 支持 PDF、Word、Excel、PowerPoint 以及许多其他格式。

**Q: 是否提供 GroupDocs.Editor for .NET 的免费试用？**  
A: 当然！您可以在 [GroupDocs 免费试用页面](https://releases.groupdocs.com/) 开始免费试用。

**Q: 如何获取 GroupDocs.Editor for .NET 的临时许可证？**  
A: 您可以从 [临时许可证页面](https://purchase.groupdocs.com/temporary-license/) 获取临时许可证。

**Q: 在哪里可以找到 GroupDocs.Editor for .NET 的详细文档？**  
A: 详细文档可在 [GroupDocs.Editor for .NET 文档站点](https://tutorials.groupdocs.com/editor/net/) 查看。

**Q: GroupDocs.Editor for .NET 提供哪些支持选项？**  
A: 您可以通过 [GroupDocs.Editor 支持论坛](https://forum.groupdocs.com/c/editor/20) 获取支持。

## 其他常见问答

**Q: 提取 CSS 后我可以更改前缀吗？**  
A: 可以。再次调用 `GetCssContent` 并传入不同的前缀字符串；该方法始终使用您在运行时传入的值。

**Q: 这是否适用于受密码保护的文档？**  
A: 适用。在创建 `Editor` 实例时，在 `WordProcessingLoadOptions` 中提供密码。

**Q: 是否可以将修改后的 CSS 保存回文档中？**  
A: GroupDocs.Editor 目前仅提供对 CSS 的只读访问。若要持久化更改，需使用文档底层的 XML API 替换原始样式表。

---

**最后更新：** 2026-09-26  
**测试环境：** GroupDocs.Editor 23.12 for .NET  
**作者：** GroupDocs

## 相关教程

- [使用 GroupDocs.Editor .NET 提取 Word 文档中的外部 CSS：全面指南](/editor/net/html-web-documents/extract-external-css-word-docs-groupdocs-editor-dotnet/)
- [使用 GroupDocs.Editor .NET 提取并前缀化 Word 文档中的 HTML](/editor/net/html-web-documents/groupdocs-editor-dotnet-extract-prefix-html-word-docs/)
- [如何使用 GroupDocs.Editor .NET 提取和修改 Word 文档中的 HTML 内容](/editor/net/html-web-documents/extract-modify-html-content-word-docs-groupdocs-editor-net/)