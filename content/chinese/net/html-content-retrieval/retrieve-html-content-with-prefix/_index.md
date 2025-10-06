---
title: 检索带前缀的 HTML 内容
linktitle: 检索带前缀的 HTML 内容
second_title: GroupDocs.Editor .NET API
description: 了解如何使用 GroupDocs.Editor for .NET 以及图像和样式表的自定义前缀从文档中检索 HTML 内容。包含分步指南。
weight: 11
url: /zh/net/html-content-retrieval/retrieve-html-content-with-prefix/
type: docs
---
# 检索带前缀的 HTML 内容

## 介绍
欢迎阅读我们的分步教程，了解如何使用 GroupDocs.Editor for .NET 从文档中检索 HTML 内容。无论您是经验丰富的开发人员还是刚刚入门，本指南都将以易于理解的方式引导您完成整个过程。我们将介绍您需要了解的所有内容，从设置环境到成功执行代码。让我们开始吧！
## 先决条件
在开始之前，请确保您已满足以下先决条件：
1.  GroupDocs.Editor for .NET：从[下载页面](https://releases.groupdocs.com/editor/net/).
2. 开发环境：Visual Studio 或任何其他首选的 .NET 开发环境。
3. C# 基础知识：熟悉 C# 编程将帮助您理解示例。
4. 要编辑的文档：准备好要测试的示例文档，例如 Word 文档。
5. .NET Framework：确保您的机器上安装了 .NET Framework。
现在您已准备好一切，让我们开始吧！
## 导入命名空间
首先，您需要在 C# 项目中导入必要的命名空间。这些命名空间提供了使用 GroupDocs.Editor for .NET 所需的类和方法。
```csharp
using System;
using GroupDocs.Editor.Options;
```
导入命名空间后，我们可以继续设置编辑器。
## 步骤 1：初始化编辑器
首先，你需要初始化`Editor`类与您的文档。此步骤涉及指定要编辑的文档并提供必要的加载选项。
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
    //此处将添加进一步的步骤
}
```
在此示例中，我们正在加载 Word 文档。您可以替换`"Your Sample Document"`以及您的文档的路径。
## 第 2 步：编辑文档
接下来，我们需要打开文档进行编辑。这是使用`Edit`方法`Editor`类，需要`WordProcessingEditOptions`作为一个论据。
```csharp
using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
{
    //此处将添加进一步的步骤
}
```
这`EditableDocument`实例表示可编辑格式的文档。现在我们准备检索 HTML 内容。
## 步骤 3：定义自定义前缀
要为图像和 CSS 添加自定义前缀，我们需要将前缀定义为字符串。此步骤可确保 HTML 内容具有外部资源的指定前缀。
```csharp
string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
string externalCssPrefix = "http://www.mywebsite.com/css/id=";
```
您可以将 URL 替换为所需的前缀。这些前缀将在下一步中用于自定义 HTML 输出。
## 步骤 4：检索 HTML 内容
现在我们已经设置了前缀，我们可以从文档中检索 HTML 内容。`GetContent`方法`EditableDocument`类允许我们指定图像和 CSS 前缀。
```csharp
string prefixedHtmlContent = document.GetContent(externalImagesPrefix, externalCssPrefix);
Console.WriteLine("HTML content of the input document with custom image and stylesheet prefixes: {0}", prefixedHtmlContent);
```
此代码片段获取带有自定义前缀的 HTML 内容并将其打印到控制台。您可以根据需要进一步处理或保存此 HTML 内容。
## 结论
就这样！按照这些步骤，您可以使用 GroupDocs.Editor for .NET 轻松检索文档中的 HTML 内容，并为图像和样式表添加自定义前缀。这个强大的工具简化了文档操作，让您可以专注于将文档编辑无缝集成到 .NET 应用程序中。
如需了解更多详细信息，请查看[GroupDocs.Editor for .NET 文档](https://tutorials.groupdocs.com/editor/net/)。如果您有任何疑问或需要进一步帮助，请随时通过[支持论坛](https://forum.groupdocs.com/c/editor/20).
## 常见问题解答
### 我可以使用 GroupDocs.Editor for .NET 编辑哪些类型的文档？
GroupDocs.Editor 支持各种文档格式，包括 Word、Excel、PowerPoint、PDF 等。
### 如何免费试用 .NET 的 GroupDocs.Editor？
您可以从[GroupDocs 网站](https://releases.groupdocs.com/).
### 我可以进一步自定义 HTML 内容吗？
是的，您可以在渲染或保存之前根据需要修改检索到的 HTML 内容。
### 是否可以将 GroupDocs.Editor for .NET 与其他 .NET 语言一起使用？
是的，您可以将它与任何与 .NET 兼容的语言（如 VB.NET 或 F#）一起使用。
### 如何获取 GroupDocs.Editor for .NET 的临时许可证？
您可以从[购买页面](https://purchase.groupdocs.com/temporary-license/).