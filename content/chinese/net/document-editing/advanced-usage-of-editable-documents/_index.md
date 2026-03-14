---
date: 2026-03-14
description: 了解如何使用 GroupDocs.Editor for .NET 从 DOCX 中提取图像、将 DOCX 转换为 HTML，并将文档保存为
  HTML。
linktitle: Extract Images from DOCX – Advanced Editable Document Usage
second_title: GroupDocs.Editor .NET API
title: 从 DOCX 中提取图像——高级可编辑文档用法
type: docs
url: /zh/net/document-editing/advanced-usage-of-editable-documents/
weight: 11
---

 produce final content.# 从 DOCX 中提取图像 – 高级可编辑文档使用

如果您是一名 .NET 开发者，想要 **从 DOCX 中提取图像** 并提升文档编辑能力，GroupDocs.Editor for .NET 提供了一套强大的工具。本综合指南将带您深入了解使用 GroupDocs.Editor 的可编辑文档的高级用法，详细分解每一步，以便您充分发挥其潜力。

## 快速答案
- **如何从 DOCX 文件中提取图像？** 在使用 `Editor` 加载文档后，使用 `EditableDocument.Images`。
- **我可以将 DOCX 转换为带嵌入资源的 HTML 吗？** 可以——调用 `EditableDocument.GetEmbeddedHtml()` 或 `GetContent()` 获取 HTML 标记。
- **哪个方法将编辑后的文档保存为 HTML？** `EditableDocument.Save(htmlFilePath)` 会创建一个带资源文件夹的 HTML 文件。
- **是否可以从 Word 文档中提取字体？** 使用 `EditableDocument.Fonts` 获取所有字体资源。
- **生产环境是否需要许可证？** 需要有效的 GroupDocs.Editor 许可证；提供免费试用。

## 什么是 **extract images from docx**？
从 DOCX 文件中提取图像是指以编程方式获取 Word 文档中嵌入的每张图片，以便您可以单独重用、修改或存储它们。GroupDocs.Editor 在 `EditableDocument` 实例上公开了 `Images` 集合，使此任务变得简单直观。

## 为什么在此工作流中使用 GroupDocs.Editor？
- **完全控制** 文档资源（图像、字体、CSS），无需手动处理 ZIP。  
- **无缝转换** 从 DOCX 到 HTML，同时保留布局和样式。  
- **轻松提取资源**，用于自定义图像处理、字体嵌入或 CDN 分发。  
- **健壮的释放模式** 确保长时间运行的服务中不会出现内存泄漏。

## 前置条件
- 在开发机器上安装 Visual Studio。  
- 与 GroupDocs.Editor 兼容的 .NET Framework。  
- GroupDocs.Editor for .NET 库。您可以在此[下载](https://releases.groupdocs.com/editor/net/)。  
- 有效的 GroupDocs.Editor 许可证。您可以获取[免费试用](https://releases.groupdocs.com/)或购买[临时许可证](https://purchase.groupdocs.com/temporary-license/)。

## 导入命名空间
为了开始，请确保在 .NET 项目中导入必要的命名空间：

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
首先，您需要通过加载并编辑受支持格式的输入文档来创建 `EditableDocument` 的实例。

```csharp
string inputFilePath = "YourSampleDocument.docx";
Editor editor = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```

在此步骤中，我们加载输入文档并为编辑做准备。

## 如何 **extract images from DOCX**？
下面我们深入资源提取功能，从最常见的需求——获取 Word 文件中的所有图像——开始。

## 步骤 2：提取文档资源
`EditableDocument` 包含多种可提取和操作的资源。让我们逐一拆解：

### 步骤 2.1：将整个文档提取为 HTML
您可以生成一个包含整个文档及其所有嵌入资源的 HTML 字符串。

```csharp
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```

由于该字符串包含样式表、图像和以 base64 编码的字体，因而会相当大。

### 步骤 2.2：提取所有图像 *(主要关键词操作)*
从文档中提取所有图像——这正是 **extract images from docx** 的核心。

```csharp
List<IImageResource> allImages = beforeEdit.Images;
```

### 步骤 2.3：提取所有字体 *(次要关键词)*
如果您还需要 **从 word 中提取字体**，请使用以下调用：

```csharp
List<FontResourceBase> allFonts = beforeEdit.Fonts;
```

### 步骤 2.4：提取所有样式表
以文本格式提取所有样式表。

```csharp
List<CssText> allStylesheets = beforeEdit.Css;
```

### 步骤 2.5：收集所有资源
一次调用收集所有资源。

```csharp
List<IHtmlResource> allResources = beforeEdit.AllResources;
```

包括图像、字体和样式表。

### 步骤 2.6：获取 HTML 标记
获取不含嵌入资源的文档 HTML 标记。

```csharp
string htmlMarkup = beforeEdit.GetContent();
```

## 如何使用自定义处理 **convert docx to html**？
有时您需要调整外部链接，使其指向您自己的资源处理程序。

## 步骤 3：调整外部链接
### 步骤 3.1：准备自定义前缀
准备将在原始外部链接前添加的前缀。

```csharp
string customImagesRequesthandlerUri = "http://example.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://example.com/CssHandler/id=";
string customFontsRequesthandlerUri = "http://example.com/FontsHandler/id=";
```

### 步骤 3.2：生成带前缀的 HTML 标记
生成带有调整后链接的 HTML 标记。

```csharp
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```

### 步骤 3.3：获取仅包含主体的 HTML 内容
某些所见即所得编辑器仅处理不含头部的纯 HTML 标记。

```csharp
string onlyBodyContent = beforeEdit.GetBodyContent();
```

### 步骤 3.4：带前缀的仅主体内容
使用自定义图像前缀生成仅主体内容。

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

## 如何正确 **save document as html**？
## 步骤 4：将文档保存为 HTML
将编辑后的文档保存为 HTML 文件，并包含其资源。

```csharp
string htmlFilePath = Path.Combine("output", Path.GetFileNameWithoutExtension(inputFilePath) + ".html");
beforeEdit.Save(htmlFilePath);
```

此方法会为样式表、图像和字体等资源创建单独的目录。

## 步骤 5：释放 EditableDocument
`EditableDocument` 实现了 `IDisposable`，并提供检查实例是否已释放的功能。

```csharp
Console.WriteLine("EditableDocument is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");
```

### 步骤 5.1 处理 Dispose 事件
您还可以订阅 disposing 事件。

```csharp
EventHandler someMethod = delegate { Console.WriteLine("Disposing event was spotted!"); };
beforeEdit.Disposed += someMethod;
```

## 步骤 6：从 HTML 创建 EditableDocument
从 HTML 文档创建 `EditableDocument` 实例。

### 步骤 6.1：来自 HTML 文件

```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
```

### 步骤 6.2：来自 HTML 标记

```csharp
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);
```

这些实例（`afterEditFromFile` 和 `afterEditFromMarkup`）与原始实例（`beforeEdit`）相同。

## 步骤 7：手动释放
手动释放您的 `EditableDocument` 实例。

```csharp
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```

这可确保资源得到正确清理。

## 常见问题与解决方案
- **提取后图像未显示：** 确认文档确实包含嵌入的图像，并且在调用 `Edit` 后访问 `beforeEdit.Images`。  
- **HTML 输出中缺少字体：** 确保调用 `GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri)` 正确嵌入字体 URL。  
- **大型 HTML 字符串导致内存压力：** 使用 `GetContent()` 获取不含嵌入资源的标记，并从单独文件提供图像/CSS。

## 常见问答

**Q: GroupDocs.Editor 支持哪些格式？**  
A: GroupDocs.Editor 支持 DOCX、XLSX、PPTX 以及许多其他流行的办公格式。

**Q: 可以在没有许可证的情况下使用 GroupDocs.Editor 吗？**  
A: 可以，您可以使用[免费试用](https://releases.groupdocs.com/)或[临时许可证](https://purchase.groupdocs.com/temporary-license/)。

**Q: 如何从文档中提取特定资源？**  
A: 使用 `EditableDocument` 实例上的 `Images`、`Fonts` 和 `Css` 集合。

**Q: 能否在 HTML 输出中调整链接？**  
A: 可以，将自定义 URI 前缀传递给 `GetContent` 或 `GetBodyContent` 以重写图像、CSS 和字体链接。

**Q: 如何将编辑后的文档保存为 HTML 文件？**  
A: 在 `EditableDocument` 实例上调用 `Save` 方法，提供以 `.html` 结尾的文件路径。

---

**最后更新：** 2026-03-14  
**测试环境：** GroupDocs.Editor for .NET（最新版本）  
**作者：** GroupDocs