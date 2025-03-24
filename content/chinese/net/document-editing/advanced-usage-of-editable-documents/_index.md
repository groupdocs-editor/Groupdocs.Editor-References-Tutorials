---
title: 可编辑文档的高级用法
linktitle: 可编辑文档的高级用法
second_title: GroupDocs.Editor .NET API
description: 学习 GroupDocs.Editor for .NET 的高级用法，以编程方式创建、编辑和提取文档中的资源。
weight: 11
url: /zh/net/document-editing/advanced-usage-of-editable-documents/
---

# 可编辑文档的高级用法

## 介绍
如果您是一名 .NET 开发人员，希望增强文档编辑功能，GroupDocs.Editor for .NET 提供了一套强大的工具。本综合指南将引导您使用 GroupDocs.Editor 高级使用可编辑文档，详细分解每个步骤，确保您能够充分利用其潜力。
## 先决条件
在深入了解高级功能之前，请确保您已具备以下条件：
- 您的开发机器上安装了 Visual Studio。
- .NET Framework 与 GroupDocs.Editor 兼容。
-  GroupDocs.Editor for .NET 库。您可以[点击下载](https://releases.groupdocs.com/editor/net/).
- 有效的 GroupDocs.Editor 许可证。您可以获取[免费试用](https://releases.groupdocs.com/)或购买[临时执照](https://purchase.groupdocs.com/temporary-license/).
## 导入命名空间
首先，确保在 .NET 项目中导入必要的命名空间：
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```
## 步骤 1：创建 EditableDocument 实例
首先，你需要创建一个实例`EditableDocument`通过加载和编辑支持格式的输入文档。
```csharp
string inputFilePath = "YourSampleDocument.docx";
Editor editor = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```
在此步骤中，我们加载输入文档并准备进行编辑。
## 第 2 步：提取文档资源
这`EditableDocument`包含各种可提取和操作的资源。让我们来分解一下：
### 步骤 2.1：将整个文档提取为 HTML
您可以生成一个包含整个文档的字符串，其中所有资源都以 HTML 形式嵌入。
```csharp
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```
这个字符串会非常大，因为它包含以 base64 编码的样式表、图像和字体。
### 步骤 2.2：提取所有图像
从文档中提取所有图像。
```csharp
List<IImageResource> allImages = beforeEdit.Images;
```
### 步骤 2.3：提取所有字体
提取文档中使用的所有字体。
```csharp
List<FontResourceBase> allFonts = beforeEdit.Fonts;
```
### 步骤 2.4：提取所有样式表
以文本格式提取所有样式表。
```csharp
List<CssText> allStylesheets = beforeEdit.Css;
```
### 步骤 2.5：收集所有资源
一次通话即可聚集所有资源。
```csharp
List<IHtmlResource> allResources = beforeEdit.AllResources;
```
其中包括图像、字体和样式表。
### 步骤 2.6：获取 HTML 标记
获取不包含嵌入资源的文档的 HTML 标记。
```csharp
string htmlMarkup = beforeEdit.GetContent();
```
## 步骤3：调整外部链接
有时，您需要调整外部链接以指向自定义资源处理程序。操作方法如下：
### 步骤 3.1：准备自定义前缀
准备将添加到原始外部链接前面的前缀。
```csharp
string customImagesRequesthandlerUri = "http://example.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://example.com/CssHandler/id=";
string customFontsRequesthandlerUri = "http://example.com/FontsHandler/id=";
```
### 步骤 3.2：生成带前缀的 HTML 标记
生成带有调整链接的 HTML 标记。
```csharp
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```
### 步骤 3.3：获取仅正文的 HTML 内容
一些所见即所得的编辑器只能处理没有标题的纯 HTML 标记。
```csharp
string onlyBodyContent = beforeEdit.GetBodyContent();
```
### 步骤 3.4：带前缀的正文内容
使用自定义图像前缀生成仅正文内容。
```csharp
string prefixedBodyContent = beforeEdit.GetBodyContent(customImagesRequesthandlerUri);
```
### 步骤 3.5：提取样式表
提取文档中使用的样式表。
```csharp
List<string> stylesheets = beforeEdit.GetCssContent();
```
### 步骤 3.6：带前缀的样式表
使用自定义前缀提取样式表。
```csharp
List<string> prefixedStylesheets = beforeEdit.GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri);
```
## 步骤 4：将文档另存为 HTML
将编辑后的文档保存为 HTML 文件，包括其资源。
```csharp
string htmlFilePath = Path.Combine("output", Path.GetFileNameWithoutExtension(inputFilePath) + ".html");
beforeEdit.Save(htmlFilePath);
```
此方法为样式表、图像和字体等资源创建一个单独的目录。
## 步骤 5：处理 EditableDocument
 EditableDocument 实现`IDisposable`并提供检查实例是否已被处置的能力。
```csharp
Console.WriteLine("EditableDocument is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");
```
### 步骤 5.1 处理 Dispose 事件
您还可以订阅处置事件。
```csharp
EventHandler someMethod = delegate { Console.WriteLine("Disposing event was spotted!"); };
beforeEdit.Disposed += someMethod;
```
## 步骤 6：从 HTML 创建 EditableDocument
从 HTML 文档创建 EditableDocument 的实例。
### 步骤 6.1：从 HTML 文件
```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
```
### 步骤 6.2：从 HTML 标记
```csharp
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);
```
这些实例（afterEditFromFile 和 afterEditFromMarkup）与原始实例（beforeEdit）相同。
## 步骤 7：手动处置
手动处理您的 EditableDocument 实例。
```csharp
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```
这确保了资源的正确清理。
## 结论
GroupDocs.Editor for .NET 提供了强大的工具，可用于以编程方式编辑文档。通过遵循本分步指南，您可以高效地管理文档内容、资源和输出格式。无论您是嵌入资源、调整外部链接还是将文档转换为 HTML，GroupDocs.Editor 都能为您提供高级文档操作所需的功能。
## 常见问题解答
### GroupDocs.Editor 支持哪些格式？
GroupDocs.Editor 支持各种格式，包括 DOCX、XLSX、PPTX 等。
### 我可以在没有许可证的情况下使用 GroupDocs.Editor 吗？
是的，你可以使用它[免费试用](https://releases.groupdocs.com/)或[临时执照](https://purchase.groupdocs.com/temporary-license/).
### 如何从文档中提取特定资源？
您可以使用提供的方法提取图像、字体和样式表，例如`Images`, `Fonts`， 和`Css`.
### 是否可以调整 HTML 输出中的链接？
是的，您可以通过为图像、CSS 和字体指定自定义前缀来调整外部链接。
### 如何将编辑的文档保存为 HTML 文件？
使用`Save`方法`EditableDocument`类将文档保存为 HTML 文件，包括其资源。