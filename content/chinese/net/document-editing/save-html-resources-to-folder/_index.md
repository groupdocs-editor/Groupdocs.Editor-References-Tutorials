---
title: 保存 HTML 资源到文件夹
linktitle: 保存 HTML 资源到文件夹
second_title: GroupDocs.Editor .NET API
description: 了解如何使用 Groupdocs.Editor for .NET 从文档中提取 HTML 资源。本综合教程为开发人员提供分步指导。
weight: 13
url: /zh/net/document-editing/save-html-resources-to-folder/
type: docs
---
# 保存 HTML 资源到文件夹

## 介绍
Groupdocs.Editor for .NET 是一款功能强大的工具，可让开发人员无缝地操作和转换 .NET 应用程序中的文档。无论您需要从文档中提取 HTML 资源还是执行高级编辑任务，Groupdocs.Editor 都可以通过其直观的 API 和丰富的文档简化流程。
## 先决条件
在深入学习本教程之前，请确保您满足以下先决条件：
1. C# 和 .NET 的基础知识：熟悉 C# 编程语言和 .NET 框架对于理解示例至关重要。
2.  Groupdocs.Editor for .NET 库：从[网站](https://releases.groupdocs.com/editor/net/).
3. 开发环境：设置您喜欢的开发环境，例如 Visual Studio 或任何其他兼容的 IDE。

## 导入命名空间
首先，在 C# 项目中导入必要的命名空间：
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```
##现在，让我们将使用 Groupdocs.Editor for .NET 将 HTML 资源保存到文件夹的过程分解为多个步骤：
## 步骤 1：初始化 Groupdocs.Editor
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
首先，初始化`Editor`对象，方法是提供示例文档的路径。在此示例中，我们使用 Word 文档，因此我们指定`WordProcessingLoadOptions`作为文档类型。
## 第 2 步：编辑文档
```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
接下来，创建一个`EditableDocument`通过调用`Edit`方法`Editor`对象。这允许您对文档执行编辑操作。
## 步骤 3：提取资源
```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
从文档中提取图像、字体和样式表等资源，并将它们存储在相应的列表中。
## 步骤 4：指定输出文件夹
```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
定义保存提取资源的输出文件夹。您可以根据需要自定义文件夹路径。
## 第 5 步：节省资源
```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
循环遍历每个图像资源，将其保存到输出文件夹，并显示相关信息，如文件名、类型和尺寸。
```csharp
		foreach (FontResourceBase oneFont in fonts)
		{
			Console.WriteLine("Saving {0} of {1} type",
				oneFont.FilenameWithExtension, oneFont.Type.FormalName);
			oneFont.Save(Path.Combine(outputFolder, oneFont.FilenameWithExtension));
		}
```
类似地，将每个字体资源保存到输出文件夹。
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
最后，将每个样式表保存到输出文件夹并完成编辑过程。

## 结论
总之，Groupdocs.Editor for .NET 提供了一种在 .NET 应用程序中以编程方式管理和操作文档的便捷解决方案。通过遵循本教程，您可以轻松地从文档中提取 HTML 资源并根据您的特定要求自定义流程。
## 常见问题解答
### Groupdocs.Editor 除了与 Word 之外还兼容其他文档格式吗？
是的，Groupdocs.Editor 支持多种文档格式，包括 Excel、PowerPoint、PDF 等。
### 我可以将 Groupdocs.Editor 集成到我的 Web 应用程序中吗？
当然，Groupdocs.Editor 提供了与在 .NET 框架上开发的 Web 应用程序的无缝集成。
### Groupdocs.Editor 是否提供云存储服务支持？
是的，Groupdocs.Editor 支持与流行的云存储服务集成，如 Google Drive、Dropbox 和 Microsoft OneDrive。
### Groupdocs.Editor 有免费试用版吗？
是的，您可以从网站上免费试用 Groupdocs.Editor。
### 如何获得 Groupdocs.Editor 的技术支持？
如需技术帮助和社区支持，您可以访问 Groupdocs.Editor 论坛。