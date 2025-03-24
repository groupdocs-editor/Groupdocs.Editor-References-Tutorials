---
title: 检索 HTML 正文内容
linktitle: 检索 HTML 正文内容
second_title: GroupDocs.Editor .NET API
description: 按照我们的分步指南使用 GroupDocs.Editor for .NET 检索 HTML 正文内容。轻松增强您的 .NET 应用程序。
weight: 10
url: /zh/net/html-content-retrieval/retrieve-html-body-content/
---
## 介绍
您准备好彻底改变 .NET 应用程序中处理文档编辑的方式了吗？GroupDocs.Editor for .NET 就是您的最佳选择！这款功能强大的工具可直接在您的应用程序中无缝编辑各种文档格式。无论您使用的是 Word、PDF 还是 HTML，GroupDocs.Editor 都可让您轻松编辑和操作文档，而无需外部工具。
## 先决条件
在开始之前，您需要满足一些先决条件：
- .NET 编程的基本知识：熟悉 C# 和 .NET 框架将帮助您理解示例。
-  GroupDocs.Editor for .NET：您可以从[GroupDocs.Editor 下载页面](https://releases.groupdocs.com/editor/net/).
- 有效许可证：您可以从[GroupDocs 购买页面](https://purchase.groupdocs.com/buy)或请求[临时执照](https://purchase.groupdocs.com/temporary-license/).
- 集成开发环境 (IDE)：建议使用 Visual Studio 以获得最佳开发体验。
## 导入命名空间
要开始使用 GroupDocs.Editor for .NET，您需要导入必要的命名空间。这将允许您访问文档编辑所需的类和方法。
```csharp
using System;
using GroupDocs.Editor.Options;
```
## 步骤 1：初始化编辑器
我们流程的第一步是初始化`Editor`类与您的文档。此类是所有编辑操作的入口点。

您需要加载要编辑的文档。在本例中，我们将使用示例 Word 文档。
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
    //继续下一步
}
```
## 第 2 步：编辑文档
接下来，我们将使用`Edit`方法`Editor`类来创建文档的可编辑版本。

我们将指定文档的编辑选项。在本例中，我们将使用`WordProcessingEditOptions`.
```csharp
using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
{
    //继续下一步
}
```
## 步骤 3：检索 HTML 正文内容
现在，我们将以 HTML 格式检索文档的正文内容。这就是奇迹发生的地方！

使用`GetBodyContent`方法，我们可以提取 HTML 的内部内容`<body>`元素。
```csharp
string bodyContent = document.GetBodyContent();
Console.WriteLine("Inner content of the HTML->BODY element: {0}", bodyContent);
```

## 结论
恭喜！您已成功学会如何使用 GroupDocs.Editor for .NET 从文档中检索 HTML 正文内容。这个功能强大的库简化了 .NET 应用程序中的文档编辑，使其成为开发人员的宝贵工具。
## 常见问题解答
### GroupDocs.Editor 支持哪些文件格式？
GroupDocs.Editor 支持多种文件格式，包括 Word 文档、PDF、Excel 电子表格、PowerPoint 演示文稿和 HTML 文件。
### 如何获得 GroupDocs.Editor 的临时许可证？
您可以向[GroupDocs 临时许可证页面](https://purchase.groupdocs.com/temporary-license/).
### GroupDocs.Editor 有免费试用版吗？
是的，你可以从[GroupDocs.Editor 下载页面](https://releases.groupdocs.com/).
### 我可以将 GroupDocs.Editor 与 .NET Core 一起使用吗？
是的，GroupDocs.Editor 与 .NET Core 兼容，为现代应用程序开发提供了灵活性。
### 在哪里可以找到 GroupDocs.Editor 的更多示例和文档？
您可以在以下位置找到更多示例和详细文档[GroupDocs.Editor 文档页面](https://tutorials.groupdocs.com/editor/net/).