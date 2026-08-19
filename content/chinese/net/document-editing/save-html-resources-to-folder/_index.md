---
date: 2026-05-12
description: 学习如何使用 GroupDocs.Editor for .NET 从文档中提取字体和其他 HTML 资源。针对 .NET 开发者的分步指南。
keywords:
- how to extract fonts
- GroupDocs.Editor .NET
- extract HTML resources
linktitle: 将 HTML 资源保存到文件夹
schemas:
- author: GroupDocs
  dateModified: '2026-05-12'
  description: Learn how to extract fonts and other HTML resources from documents
    using GroupDocs.Editor for .NET. Step‑by‑step guide for .NET developers.
  headline: How to Extract Fonts and Save HTML Resources to Folder
  type: TechArticle
- description: Learn how to extract fonts and other HTML resources from documents
    using GroupDocs.Editor for .NET. Step‑by‑step guide for .NET developers.
  name: How to Extract Fonts and Save HTML Resources to Folder
  steps:
  - name: '**Basic Knowledge of C# and .NET** – Familiarity with C# programming language
      and .NET framework is essential to follow along with the examples.'
    text: '**Basic Knowledge of C# and .NET** – Familiarity with C# programming language
      and .NET framework is essential to follow along with the examples.'
  - name: '**GroupDocs.Editor for .NET Library** – Download and install GroupDocs.Editor
      for .NET library from the [website](https://releases.groupdocs.com/editor/net/).'
    text: '**GroupDocs.Editor for .NET Library** – Download and install GroupDocs.Editor
      for .NET library from the [website](https://releases.groupdocs.com/editor/net/).'
  - name: '**Development Environment** – Set up your preferred development environment
      such as Visual Studio or any other compatible IDE.'
    text: '**Development Environment** – Set up your preferred development environment
      such as Visual Studio or any other compatible IDE.'
  type: HowTo
- questions:
  - answer: Yes, it supports Excel, PowerPoint, PDF, HTML, and over 50 additional
      formats for both editing and resource extraction.
    question: Is GroupDocs.Editor compatible with other document formats besides Word?
  - answer: Absolutely. The API works seamlessly with ASP.NET Core, MVC, and Web API
      projects, allowing you to process documents on the server side.
    question: Can I integrate GroupDocs.Editor into a web application?
  - answer: Yes, it includes built‑in connectors for Google Drive, Dropbox, OneDrive,
      and Amazon S3, enabling direct loading and saving of documents in the cloud.
    question: Does GroupDocs.Editor provide cloud storage integration?
  - answer: A fully functional 30‑day trial can be downloaded from the GroupDocs website
      without any credit‑card requirement.
    question: Is there a free trial available for GroupDocs.Editor?
  - answer: You can reach the GroupDocs support team via the official forum, submit
      a ticket through the customer portal, or consult the detailed API documentation.
    question: How can I get technical support for extraction issues?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: 如何提取字体并将 HTML 资源保存到文件夹
type: docs
url: /zh/net/document-editing/save-html-resources-to-folder/
weight: 13
---

# 如何提取字体并将 HTML 资源保存到文件夹

## 介绍
GroupDocs.Editor for .NET 让您 **提取字体** 并从文档中提取其他资源，同时将其转换为 HTML。只需几行 C# 代码，您就可以提取图像、样式表和字体文件，然后将它们存储在您选择的文件夹中。本教程将带您完整了解工作流程，从初始化编辑器到将每个资源保存到磁盘。

## 快速答案
- **“how to extract fonts” 是什么意思？** 它是指在 HTML 转换过程中检索源文档中嵌入的字体文件的过程。  
- **哪个库处理此操作？** GroupDocs.Editor for .NET 提供了专用的 API 用于提取字体、图像和样式表。  
- **我需要许可证吗？** 有免费试用版；在生产环境中需要商业许可证。  
- **支持哪些 .NET 版本？** .NET Framework 4.5+、.NET Core 3.1+、.NET 5/6/7。  
- **我可以指定自定义文件夹吗？** 可以，您可以在保存提取的资源时指定任意可写路径。

## 什么是 “how to extract fonts”？
**提取字体** 是指检索源文档（例如 DOCX、PPTX）中嵌入的原始字体文件，以便在生成的 HTML 中引用它们。这可确保文本在浏览器中呈现时与预期完全一致，而无需依赖系统字体。

## 为什么使用 GroupDocs.Editor 进行 HTML 资源提取？
GroupDocs.Editor 支持 **50 多种输入和输出格式**——包括 DOCX、PPTX、PDF 和 HTML——并且能够在不将整个文件加载到内存的情况下处理 **最多 300 页**的文档。其 API 在一次遍历中提取字体、图像和 CSS，将开发时间相比手动解析降低最多 **70 %**。

## 先决条件
在深入教程之前，请确保您具备以下先决条件：

1. **C# 和 .NET 的基础知识** – 熟悉 C# 编程语言和 .NET 框架对于跟随示例至关重要。  
2. **GroupDocs.Editor for .NET 库** – 从[网站](https://releases.groupdocs.com/editor/net/)下载并安装 GroupDocs.Editor for .NET 库。  
3. **开发环境** – 设置您喜欢的开发环境，例如 Visual Studio 或其他兼容的 IDE。

## 导入命名空间
要开始，请在 C# 项目中导入必要的命名空间：

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```

## 如何提取字体并将 HTML 资源保存到文件夹？
使用 `Editor editor = new Editor("sample.docx", new WordProcessingLoadOptions());` 加载源文档，然后调用 `editor.Save("output.html", SaveOptions.Html);`。保存操作完成后，`Resources` 集合包含所有提取的资源——包括字体——您可以遍历并写入磁盘。这种一步式方法会自动处理转换和资源提取。

## 步骤 1：初始化 GroupDocs.Editor
`Editor` 是负责文档加载、转换和资源提取的核心类。它在内存中表示一个文档会话。

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
首先，通过提供示例文档的路径来初始化 `Editor` 对象。在本例中，我们使用 Word 文档，因此指定 `WordProcessingLoadOptions` 作为文档类型。

## 步骤 2：编辑文档
`EditableDocument` 是 `Edit` 方法返回的可编辑表示，允许您在保存之前对文档进行操作。

```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
接下来，调用 `Editor` 对象的 `Edit` 方法创建 `EditableDocument` 对象。这使您能够对文档执行编辑操作。

## 步骤 3：提取资源
`Resources` 是一个集合，将提取的资产——图像、字体和样式表——分组到不同的列表中，便于处理。

```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
从文档中提取图像、字体和样式表等资源，并将它们存储在相应的列表中。

## 步骤 4：指定输出文件夹
`outputFolder` 是一个字符串，定义提取的文件将写入的位置。您可以将其指向服务器或本机上的任何可写目录。

```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
定义提取资源将保存的输出文件夹。您可以根据需求自定义文件夹路径。

## 步骤 5：保存资源
`SaveResource` 是一个辅助例程，用于将单个二进制资源（图像、字体或样式表）写入文件系统。

```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
遍历每个图像资源，将其保存到输出文件夹，并显示相关信息，如文件名、类型和尺寸。

```csharp
		foreach (FontResourceBase oneFont in fonts)
		{
			Console.WriteLine("Saving {0} of {1} type",
				oneFont.FilenameWithExtension, oneFont.Type.FormalName);
			oneFont.Save(Path.Combine(outputFolder, oneFont.FilenameWithExtension));
		}
```
同样，将每个字体资源保存到输出文件夹。

```csharp
		foreach (CssText oneStylesheet in stylesheets)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} encoding",
				oneStylesheet.FilenameWithExtension, oneStylesheet.Type.FormalName, oneStylesheet.Encoding);
			oneStylesheet.Save(Path.Combine(outputFolder, oneStylesheet.FilenameWithExtension));
		}
	}
}
```
最后，将每个样式表保存到输出文件夹，完成编辑过程。

## 常见问题及解决方案
- **转换后缺少字体** – 确保源文档实际嵌入了字体；否则，GroupDocs.Editor 只能引用系统字体。  
- **访问被拒绝错误** – 验证应用程序进程对目标输出文件夹具有写入权限。  
- **大文档导致高内存使用** – 使用 `LoadOptions` 并将 `LoadMode = LoadMode.Stream`，以流式处理大文件，而不是将其完整加载到内存中。

## 常见问答

**问：GroupDocs.Editor 是否兼容除 Word 之外的其他文档格式？**  
答：是的，它支持 Excel、PowerPoint、PDF、HTML，以及超过 50 种其他格式，均可用于编辑和资源提取。

**问：我可以将 GroupDocs.Editor 集成到 Web 应用程序中吗？**  
答：当然可以。该 API 可与 ASP.NET Core、MVC 和 Web API 项目无缝配合，允许您在服务器端处理文档。

**问：GroupDocs.Editor 是否提供云存储集成？**  
答：是的，它内置了 Google Drive、Dropbox、OneDrive 和 Amazon S3 的连接器，支持在云端直接加载和保存文档。

**问：GroupDocs.Editor 是否提供免费试用？**  
答：可以从 GroupDocs 网站下载功能完整的 30 天试用版，无需信用卡。

**问：如何获取提取问题的技术支持？**  
答：您可以通过官方论坛联系 GroupDocs 支持团队，在客户门户提交工单，或查阅详细的 API 文档。

---

**最后更新：** 2026-05-12  
**测试环境：** GroupDocs.Editor 23.11 for .NET  
**作者：** GroupDocs

## 相关教程

- [使用 GroupDocs.Editor .NET 高效文档编辑：将 HTML 转换为可编辑文档](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)
- [使用 GroupDocs.Editor .NET 高效提取并保存 DOCX 资源 - 完整指南](/editor/net/document-saving/efficient-extract-save-docx-resources-groupdocs-editor-net/)
- [掌握使用 GroupDocs.Editor .NET 进行文档编辑和转换：完整指南](/editor/net/document-editing/groupdocs-editor-net-mastering-document-editing/)