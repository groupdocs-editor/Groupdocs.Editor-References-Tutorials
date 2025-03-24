---
title: 获取外部 CSS 内容
linktitle: 获取外部 CSS 内容
second_title: GroupDocs.Editor .NET API
description: 通过本分步指南了解如何使用 GroupDocs.Editor for .NET 从文档中提取外部 CSS 内容。非常适合集成文档的开发人员。
weight: 10
url: /zh/net/css-handling/get-external-css-content/
---

# 获取外部 CSS 内容

## 介绍
在本文中，我们将带您了解开始使用 GroupDocs.Editor for .NET 所需的一切。从设置环境到从文档中提取外部 CSS 内容，我们将涵盖所有内容。让我们开始吧！
## 先决条件
在开始之前，请确保您已满足以下先决条件：
1. .NET Framework：确保您已安装.NET Framework 4.6.1 或更高版本。
2. Visual Studio：安装 Visual Studio 2017 或更高版本以获得无缝开发体验。
3.  GroupDocs.Editor for .NET：从[GroupDocs.Editor 下载页面](https://releases.groupdocs.com/editor/net/).
4. C# 基础知识：熟悉 C# 编程将帮助您理解示例。
## 导入命名空间
在深入研究代码示例之前，您需要在 C# 项目中导入必要的命名空间：
```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Editor.Options;
```
现在我们已经对先决条件进行了分类并导入了命名空间，让我们逐步分解示例代码。
## 步骤 1：初始化编辑器
首先，你需要初始化`Editor`对象与您的示例文档。此步骤设置文档以供编辑。
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
    //继续执行后续步骤
}
```
在此代码片段中，我们创建一个`Editor`通过提供文档路径和返回的委托来实例`WordProcessingLoadOptions`这使文档做好了编辑的准备。
## 第 2 步：编辑文档
接下来，您需要编辑文档以获得其可编辑状态。此步骤将文档转换为可编辑格式。
```csharp
using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
{
    //继续执行后续步骤
}
```
在这里，我们使用`Edit`方法`Editor`班级，通过`WordProcessingEditOptions`得到一个`EditableDocument`对象，以可编辑的形式表示文档。
## 步骤 3：获取 CSS 内容
现在，我们从可编辑文档中提取 CSS 内容。此步骤至关重要，因为它允许您访问和操作文档的样式。
```csharp
List<string> stylesheets = document.GetCssContent();
```
这`GetCssContent`方法返回文档中存在的 CSS 样式表列表。此列表可用于进一步处理或分析。
## 步骤 4：输出 CSS 内容
最后，让我们将提取的 CSS 内容打印到控制台。这将帮助您验证从文档中检索到的样式表。
```csharp
Console.WriteLine("There are {0} stylesheets in the input document", stylesheets.Count);
foreach (string css in stylesheets)
{
    Console.WriteLine(css);
}
```
在这一部分中，我们将样式表的数量及其内容输出到控制台。这可以清晰地查看文档中使用的 CSS。
## 结论
就这样！您已成功使用 GroupDocs.Editor for .NET 从文档中提取外部 CSS 内容。本分步指南应可帮助您了解使用这个功能强大的库满足文档编辑需求的基础知识。无论您是将其集成到更大的应用程序中还是只是探索其功能，GroupDocs.Editor 都提供了一个强大的解决方案，可用于以编程方式处理文档编辑。
## 常见问题解答
### 什么是 GroupDocs.Editor for .NET？
GroupDocs.Editor for .NET 是一个文档编辑 API，允许开发人员在 .NET 应用程序内以编程方式编辑各种格式的文档，包括 Word、Excel 和 PDF。
### 如何开始使用 GroupDocs.Editor for .NET？
首先，您需要从[GroupDocs.Editor 下载页面](https://releases.groupdocs.com/editor/net/)，设置您的 .NET 环境，并按照本指南中概述的步骤进行操作。
### 我可以免费使用 GroupDocs.Editor 吗？
 GroupDocs.Editor 提供免费试用版，您可以从[GroupDocs 免费试用页面](https://releases.groupdocs.com/)。要获得完整功能，请考虑购买许可证。
### GroupDocs.Editor 支持哪些文件格式？
 GroupDocs.Editor 支持多种文件格式，包括 DOCX、XLSX、PPTX、PDF、HTML 等。查看[文档](https://tutorials.groupdocs.com/editor/net/)以获取完整列表。
### 如何获得 GroupDocs.Editor 的支持？
您可以从[GroupDocs 支持论坛](https://forum.groupdocs.com/c/editor/20)您可以在这里提出问题并获得社区和 GroupDocs 专家的帮助。