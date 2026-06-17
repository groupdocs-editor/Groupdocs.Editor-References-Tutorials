---
date: 2026-03-06
description: 在本详细的分步教程中，学习如何使用 GroupDocs.Editor for .NET 处理带前缀的 CSS 内容并提取 CSS 内容。
linktitle: Handle CSS Content with Prefix
second_title: GroupDocs.Editor .NET API
title: 处理带前缀的 CSS 内容
type: docs
url: /zh/net/css-handling/handle-css-content-with-prefix/
weight: 11
---

# 处理带前缀的 CSS 内容

在本教程中，您将了解在使用 GroupDocs.Editor for .NET 处理文档内部样式表时，**如何处理 css 前缀**。无论是需要为图片、字体或任何外部资源添加 URL 前缀，下面的步骤都将向您展示如何**处理 css 前缀**以及如何**提取 css 内容**以便进一步处理。

## 快速答案
- **“处理 css 前缀” 是什么意思？** 为 CSS 中引用的外部资源添加自定义 URL 前缀。  
- **哪个 API 方法返回 CSS 样式？** `EditableDocument.GetCssContent(...)`。  
- **我需要许可证吗？** 提供试用许可证；生产环境需要商业许可证。  
- **支持哪些 .NET 版本？** .NET Framework 4.5+ 和 .NET Core/5/6。  
- **可以在运行时更改前缀吗？** 可以——只需向 `GetCssContent` 传入不同的字符串即可。

## 什么是 **handle css prefix**？
为 CSS 资源添加前缀会重写图片、字体或其他资产的路径，使其指向您控制的位置（例如 CDN 或受保护的服务器）。在导出文档并需要让所有外部引用在 Web 应用中可访问时，这尤其有用。

## 为什么使用 GroupDocs.Editor 来 **extract css content**？
GroupDocs.Editor 能读取 WordProcessing 文档中嵌入的原始 CSS，提供原始样式表字符串，并允许您在渲染或保存之前对其进行操作。这消除了手动解析的需求，并确保提取的 CSS 与文档内部表示一致。

## 前置条件
在开始之前，请确保已具备以下前置条件：
- Visual Studio：需要已安装的 Visual Studio。  
- .NET Framework：确保已安装 .NET Framework。  
- GroupDocs.Editor for .NET：您可以在[此处](https://releases.groupdocs.com/editor/net/)下载。  
- 示例文档：准备好用于编辑的示例文档。

## 导入命名空间
首先，导入必要的命名空间，以确保代码能够顺利运行。此步骤让我们能够访问 GroupDocs.Editor 的核心类。

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Editor.Options;
```

## 步骤 1：初始化编辑器
第一步是使用示例文档创建 `Editor` 实例。这将搭建编辑环境。

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```

## 步骤 2：编辑文档
接下来，获取 `EditableDocument` 对象。该对象代表文件的可编辑版本，允许我们操作其内部部分。

```csharp
    using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
    {
```

## 步骤 3：设置外部前缀
为图片和字体定义 URL 前缀。这些前缀将被添加到 CSS 中找到的每个图片和字体引用前。

```csharp
        string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
        string externalFontsPrefix = "http://www.mywebsite.com/fonts/id=";
```

## 步骤 4：使用前缀 **提取 CSS 内容**
调用 `GetCssContent`，并传入刚才定义的前缀。该方法返回已包含前缀 URL 的 CSS 样式表字符串列表。

```csharp
        List<string> stylesheets = document.GetCssContent(externalImagesPrefix, externalFontsPrefix);
```

## 步骤 5：输出结果
打印找到的样式表数量并显示每个样式表内容，以便验证前缀是否正确应用。

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
- **未返回样式表** – 确认源文档实际包含 CSS（例如带有样式表格或嵌入 HTML 的 Word 文档）。  
- **URL 不正确** – 再次检查前缀字符串是否以正确的分隔符（`/` 或 `=`）结尾，以匹配服务器路由。  
- **性能问题** – 对于非常大的文档，考虑分批处理样式表，以避免高内存占用。

## 结论
使用 GroupDocs.Editor for .NET 通过前缀处理 CSS 内容既简便又强大。按照这些步骤，您可以**处理 css 前缀**、通过**提取 css 内容**获取原始 CSS，并将外部资源无缝集成到 Web 工作流中。探索 GroupDocs.Editor 的其他功能，如 HTML 转换、图片提取和文档合并，以获得 API 的更多价值。

## 常见问答
### 我可以在 .NET 中将 GroupDocs.Editor 与其他文档格式一起使用吗？
可以，GroupDocs.Editor for .NET 支持多种文档格式，包括 PDF、Word、Excel 等。

### 是否提供 GroupDocs.Editor for .NET 的免费试用？
当然！您可以在[此处](https://releases.groupdocs.com/)开始免费试用。

### 如何获取 GroupDocs.Editor for .NET 的临时许可证？
您可以在[此处](https://purchase.groupdocs.com/temporary-license/)获取临时许可证。

### 在哪里可以找到 GroupDocs.Editor for .NET 的详细文档？
详细文档可在[此处](https://tutorials.groupdocs.com/editor/net/)查看。

### GroupDocs.Editor for .NET 提供哪些支持选项？
您可以在[此处](https://forum.groupdocs.com/c/editor/20)获取支持。

## 其他常见问题

**问：提取 CSS 后可以更改前缀吗？**  
答：可以。再次调用 `GetCssContent` 并传入不同的前缀字符串；该方法始终使用您在运行时传入的值。

**问：这是否适用于受密码保护的文档？**  
答：适用。在创建 `Editor` 实例时，在 `WordProcessingLoadOptions` 中提供密码。

**问：是否可以将修改后的 CSS 保存回文档中？**  
答：GroupDocs.Editor 目前仅提供只读访问 CSS。若要持久化更改，需要使用文档底层的 XML API 替换原始样式表。

---

**最后更新：** 2026-03-06  
**测试环境：** GroupDocs.Editor 23.12 for .NET  
**作者：** GroupDocs