---
date: '2026-04-11'
description: 学习如何使用 GroupDocs.Editor for .NET 创建可编辑文档并高效地将文档保存为 HTML。
keywords:
- create editable document
- extract images from document
- save document as html
title: 使用 GroupDocs.Editor .NET 创建可编辑文档
type: docs
url: /zh/net/document-editing/groupdocs-editor-net-edit-manage-documents-guide/
weight: 1
---

# 使用 GroupDocs.Editor .NET 创建可编辑文档

在当今的数字时代，**创建可编辑文档**是任何现代工作流的核心需求。无论您是在构建协作编辑器、内容管理系统，还是自动化报告工具，能够以编程方式编辑和保存 HTML 文件都可以节省大量时间。本教程将向您展示如何使用 GroupDocs.Editor for .NET **创建可编辑文档**实例、提取资源以及**将文档保存为 HTML**。

## 快速答案
- **“创建可编辑文档”是什么意思？** 它指的是将源文件加载到 GroupDocs.Editor `EditableDocument` 对象中，您可以以编程方式对其进行修改。  
- **哪些格式可以转换为 HTML？** 支持 Word、Excel、PowerPoint 以及许多其他 Office 格式。  
- **如何从文档中提取图像？** 使用 `EditableDocument.Images` 集合。  
- **我能生成包含所有资源的单个 HTML 字符串吗？** 可以——调用 `GetEmbeddedHtml()`。  
- **生产环境是否需要许可证？** 试用版可用于评估；商业使用需要永久许可证。

## 什么是“创建可编辑文档”？
创建可编辑文档是指将源文件（例如 .docx）加载到 GroupDocs.Editor 中，返回一个 `EditableDocument` 对象。该对象公开文档的 HTML 标记、图像、字体和 CSS，允许您编辑内容、替换资源或将整个文档嵌入网页。

## 为什么在此任务中使用 GroupDocs.Editor .NET？
- **功能完整的 API** – 处理 Word、Excel、PowerPoint 等。  
- **资源提取** – 使用简单属性提取图像、字体和样式表。  
- **嵌入式 HTML 生成** – 生成包含所有资源的单个 HTML 字符串，适用于电子邮件或单页应用。  
- **注重性能** – 及时释放对象，并在需要时使用异步模式。

## 先决条件
在实现 GroupDocs.Editor .NET 功能之前，请确保：
- **.NET 环境**：为 .NET 应用程序设置开发环境。  
- **库和依赖项**：
  - 使用以下方法之一安装 GroupDocs.Editor：
    - **.NET CLI**
      ```bash
      dotnet add package GroupDocs.Editor
      ```
    - **Package Manager**
      ```powershell
      Install-Package GroupDocs.Editor
      ```
    - **NuGet 包管理器 UI**：搜索并安装最新版本。  
- **知识先决条件**：建议熟悉 C# 编程和基本的文档处理概念。

## 设置 GroupDocs.Editor for .NET
### 安装说明
首先，在项目中设置 GroupDocs.Editor：
1. **通过 .NET CLI 安装**：
   ```bash
   dotnet add package GroupDocs.Editor
   ```
2. **使用 Package Manager**：
   - 打开 Package Manager 控制台并运行：
     ```powershell
     Install-Package GroupDocs.Editor
     ```
3. **NuGet 包管理器 UI**：  
   - 前往 NuGet，搜索 "GroupDocs.Editor" 并安装。

### 获取许可证
- **免费试用和临时许可证**：  
  从 [GroupDocs releases](https://releases.groupdocs.com/editor/net/) 下载开始免费试用。若需延长测试，可在 [purchase page](https://purchase.groupdocs.com/temporary-license) 申请临时许可证。

### 基本初始化和设置
以下是在应用程序中初始化 GroupDocs.Editor 的方法：
```csharp
using System;
using GroupDocs.Editor;

string inputFilePath = "YOUR_DOCUMENT_DIRECTORY"; // Replace with your actual document path
Editor editor = new Editor(inputFilePath, new WordProcessingLoadOptions());
```

## 如何使用 GroupDocs.Editor .NET 创建可编辑文档
### 创建 EditableDocument 实例
**概述**：通过创建 `EditableDocument` 实例来加载和编辑文档。

#### 加载文档
```csharp
using GroupDocs.Editor.Options;

// Load your document with appropriate options
Editor editor = new Editor(inputFilePath, new WordProcessingLoadOptions());

// Create EditableDocument from the loaded file
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```

## 如何生成嵌入式 HTML
### 从 EditableDocument 生成嵌入式 HTML
**概述**：将整个文档转换为包含样式表和资源的单个嵌入式 HTML 字符串。
```csharp
using System.Collections.Generic;
using GroupDocs.Editor.HtmlCss.Resources;

// Generate embedded HTML
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```

## 如何从文档中提取图像
### 从 EditableDocument 提取资源
**概述**：从文档中检索图像、字体、CSS 和其他资源。
```csharp
List<IImageResource> allImages = beforeEdit.Images;
List<FontResourceBase> allFonts = beforeEdit.Fonts;
List<CssText> allStylesheets = beforeEdit.Css;
List<IHtmlResource> allResources = beforeEdit.AllResources;
```

## 如何从文档中提取字体
*上面的代码块同样展示了如何通过 `beforeEdit.Fonts` 提取字体资源。*

## 如何获取纯 HTML 内容
### 从 EditableDocument 获取 HTML 内容
**概述**：提取不含嵌入资源的纯 HTML 内容。
```csharp
string htmlMarkup = beforeEdit.GetContent();
```

## 如何调整 HTML 内容中的外部链接
### 调整 HTML 内容中的外部链接
**概述**：使用自定义前缀修改图像、CSS 和字体的外部链接。
```csharp
using System.Collections.Generic;

// Define custom handlers for resource URLs
string customImagesRequesthandlerUri = "http://example.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://example.com/CssHandler/id=";

// Adjust HTML content with prefixed links
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```

## 如何将文档保存为 HTML
### 将 EditableDocument 保存为 HTML 文件
**概述**：将编辑后的文档以 HTML 格式保存回磁盘。
```csharp
using System.IO;

string htmlFilePath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "document.html"); // Adjust the output path
beforeEdit.Save(htmlFilePath);
```

## 释放和事件处理 EditableDocument
**概述**：管理资源释放并处理与文档生命周期相关的事件。
```csharp
Console.WriteLine("beforeEdit variable of EditableDocument type is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");

// Subscribe to the disposing event
EventHandler someMethod = delegate {
    Console.WriteLine("Disposing event was spotted!");
};
beforeEdit.Disposed += someMethod;
```

## 如何从 HTML 内容创建可编辑文档
### 从 HTML 内容创建 EditableDocument
**概述**：从现有 HTML 内容重建 `EditableDocument` 实例。
```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);

// Dispose resources once done
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```

## 实际应用
GroupDocs.Editor .NET 可在众多实际场景中发挥作用：
- **协作编辑**：促进多用户无缝文档编辑。  
- **网页发布**：将文档转换为适合在线查看和交互的网页友好格式。  
- **内容管理系统**：与 CMS 平台集成，实现动态内容更新。  
- **自动化报告生成**：从各种数据源自动生成和格式化报告。

## 性能考虑
为了优化 GroupDocs.Editor .NET 的性能：
- 通过在使用后及时释放对象来高效管理内存。  
- 通过优化文件路径和 URL 来最小化资源加载时间。  
- 在适用情况下使用异步处理，以提升应用响应性。

## 常见问题及解决方案
- **大文件导致高内存使用** – 在完成处理后立即释放 `EditableDocument` 对象。  
- **转换后图像链接破损** – 调用 `GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri)` 时，确保使用正确的资源处理程序 URI。  
- **生成的 HTML 中缺少字体** – 验证源文档是否嵌入了所需字体，或确保服务器上可用这些字体。

## 常见问题
**Q: GroupDocs.Editor .NET 是否兼容所有文档格式？**  
A: GroupDocs.Editor 支持广泛的格式，包括 Word、Excel、PowerPoint 等众多格式，为您在不同使用场景中提供灵活性。

**Q: 如何使用 GroupDocs.Editor 高效处理大文件？**  
A: 在可用时使用异步 API，尽可能分块处理文件，并始终及时释放 `EditableDocument` 和 `Editor` 对象以释放内存。

**Q: 我可以将 GroupDocs.Editor 与云存储解决方案集成吗？**  
A: 可以，您可以通过将文件流传入 `Editor` 构造函数，连接到 Azure Blob Storage、Amazon S3、Google Cloud Storage 或任何其他云提供商。

**Q: GroupDocs.Editor 的授权选项有哪些？**  
A: 您可以先使用免费试用或申请临时许可证进行评估。生产部署需要付费许可证。

**Q: 如果遇到问题，我可以在哪里获得支持？**  
A: 可访问 [GroupDocs Support Forum](https://forum.groupdocs.com) 寻求帮助，也可以直接联系 GroupDocs 支持团队。

---

**最后更新：** 2026-04-11  
**测试环境：** GroupDocs.Editor 23.12 for .NET  
**作者：** GroupDocs