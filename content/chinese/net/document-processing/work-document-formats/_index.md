---
date: 2026-06-06
description: 了解如何使用 GroupDocs.Editor for .NET 列出支持的文档格式并确定文件格式扩展名。提供代码示例的分步指南、快速答案和常见问题解答。
keywords:
- list supported document formats
- determine file format extension
- GroupDocs.Editor .NET
- document editing API
- supported formats guide
linktitle: 列出支持的文档格式
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to list supported document formats and determine file format
    extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets,
    quick answers, and FAQs.
  headline: List Supported Document Formats with GroupDocs.Editor .NET
  type: TechArticle
- description: Learn how to list supported document formats and determine file format
    extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets,
    quick answers, and FAQs.
  name: List Supported Document Formats with GroupDocs.Editor .NET
  steps:
  - name: '**.NET development environment** – Visual Studio 2022 or any IDE that supports
      .NET 6+.'
    text: '**.NET development environment** – Visual Studio 2022 or any IDE that supports
      .NET 6+.'
  - name: '**GroupDocs.Editor for .NET library** – download from the [GroupDocs releases
      page](https://releases.groupdocs.com/editor/net/).'
    text: '**GroupDocs.Editor for .NET library** – download from the [GroupDocs releases
      page](https://releases.groupdocs.com/editor/net/).'
  - name: '**Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/)
      for unrestricted access.'
    text: '**Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/)
      for unrestricted access.'
  - name: '**Basic C# knowledge** – familiarity with namespaces, `using` statements,
      and console output.'
    text: '**Basic C# knowledge** – familiarity with namespaces, `using` statements,
      and console output.'
  - name: '**Loop Through Formats:** We iterate over all available Word‑processing
      formats.'
    text: '**Loop Through Formats:** We iterate over all available Word‑processing
      formats.'
  - name: '**Output Format Details:** For each format we print its friendly name and
      default file extension.'
    text: '**Output Format Details:** For each format we print its friendly name and
      default file extension.'
  - name: '**Loop Through Formats:** The same looping logic applies to presentations.'
    text: '**Loop Through Formats:** The same looping logic applies to presentations.'
  - name: '**Output Format Details:** The name and extension are displayed for each
      format.'
    text: '**Output Format Details:** The name and extension are displayed for each
      format.'
  - name: '**Parse Format:** `FromExtension` converts the `.xlsm` extension into its
      internal `SpreadsheetFormat` enum.'
    text: '**Parse Format:** `FromExtension` converts the `.xlsm` extension into its
      internal `SpreadsheetFormat` enum.'
  - name: '**Output Format:** The parsed format’s name is printed, confirming the
      mapping.'
    text: '**Output Format:** The parsed format’s name is printed, confirming the
      mapping.'
  type: HowTo
- questions:
  - answer: '`DocumentFormatInfo` provides metadata about supported file types, while
      `SaveOptions` configures how a document is written back to disk (format, compression,
      etc.).'
    question: What is the difference between `DocumentFormatInfo` and `SaveOptions`?
  - answer: Yes—use `DocumentFormatInfo.FromExtension("yourExt")`; if the extension
      isn’t recognized, the method returns `null`.
    question: Can I list formats for a custom file extension?
  - answer: Absolutely. Pass the password to the `Editor` constructor via `EditorSettings`
      to open encrypted documents.
    question: Does GroupDocs.Editor support password‑protected files?
  - answer: Over **30 input and output formats**, spanning Word, Excel, PowerPoint,
      HTML, and plain text.
    question: How many formats does GroupDocs.Editor actually support?
  - answer: Use the `GetEditableWordProcessingFormats()` (or Spreadsheet/Presentation
      equivalents) to retrieve formats that allow full edit capabilities.
    question: Is there a way to restrict the list to only editable formats?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: 使用 GroupDocs.Editor .NET 列出支持的文档格式
type: docs
url: /zh/net/document-processing/work-document-formats/
weight: 13
---

# 列出支持的文档格式

欢迎阅读我们关于 **如何列出支持的文档格式** 的完整教程，使用适用于 .NET 的 GroupDocs.Editor。无论您是在构建以文档为中心的 Web 应用还是企业级桌面工具，准确了解可以编辑或转换的格式都是必不可少的。在本指南中，您将学习如何枚举格式、解析扩展名以及编辑文档——所有内容均配有清晰、易懂的说明和可直接运行的代码片段。

## 快速答案
- **如何列出所有支持的格式？** 使用 `DocumentFormatInfo.GetSupportedWordProcessingFormats()`（或对应的 Presentation/Spreadsheet 方法）并遍历集合。  
- **我可以根据文件扩展名确定格式吗？** 可以——调用 `DocumentFormatInfo.FromExtension(".docx")`。  
- **GroupDocs.Editor 支持哪些文件类型？** 超过 30 种输入和输出格式，包括 DOCX、XLSX、PPTX、HTML 和纯文本。  
- **列出格式是否需要许可证？** 临时许可证可解锁完整 API；否则试用版只能使用有限功能。  
- **兼容哪些 .NET 版本？** .NET Framework 4.6+、.NET Core 3.1+、.NET 5/6/7。

## 什么是“列出支持的文档格式”？

该短语指以编程方式获取 GroupDocs.Editor 能够打开、编辑和保存的文件类型集合。此操作可帮助您构建动态 UI 下拉列表或在处理前验证用户上传的文件，确保仅将兼容的文件传递给编辑器进行后续操作。

## 为什么要列出支持的文档格式？

GroupDocs.Editor **支持 30 多种输入和输出格式**，并且能够在不将整个文档加载到内存的情况下处理高达 **2 GB** 的文件。了解确切的格式列表可防止运行时错误，提升用户体验，并使您能够强制执行诸如“仅允许可编辑的 Office 文档”等业务规则。这也有助于只向用户展示您应用真正支持的格式。

## 前置条件

在开始之前，请确保您已具备以下条件：

1. **.NET 开发环境** – Visual Studio 2022 或任何支持 .NET 6+ 的 IDE。  
2. **GroupDocs.Editor for .NET 库** – 从 [GroupDocs 发布页面](https://releases.groupdocs.com/editor/net/) 下载。  
3. **临时许可证** – 获取 [临时许可证](https://purchase.groupdocs.com/temporary-license/) 以获得无限制访问。  
4. **基本的 C# 知识** – 熟悉命名空间、`using` 语句和控制台输出。

## 如何列出支持的文档格式？

加载支持的格式集合并打印每种格式的名称和文件扩展名。这种两步模式适用于文字处理、电子表格和演示文稿。通过遍历集合，您可以动态填充 UI 元素（如下拉列表），确保用户只能选择编辑器实际能够处理的格式。

```csharp
// No actual code block – placeholder retained from original tutorial
```csharp
using System;
using GroupDocs.Editor.Options;
```
```

### 列出文字处理格式
`Formats.WordProcessingFormats` 是一个枚举，描述编辑器识别的每种文字处理文件类型。`All` 属性返回这些格式对象的集合。

```csharp
```csharp
foreach (Formats.WordProcessingFormats oneFormat in Formats.WordProcessingFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**说明：**  
1. **遍历格式：** 我们遍历所有可用的文字处理格式。  
2. **输出格式详情：** 对每种格式打印其友好名称和默认文件扩展名。

### 列出演示文稿格式
`Formats.PresentationFormats` 对幻灯片文件的处理方式相同，通过 `All` 集合公开每种支持的演示文稿类型。

```csharp
```csharp
foreach (Formats.PresentationFormats oneFormat in Formats.PresentationFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**说明：**  
1. **遍历格式：** 相同的遍历逻辑适用于演示文稿。  
2. **输出格式详情：** 每种格式的名称和扩展名都会显示。

## 如何确定文件格式扩展名？

有时您只有文件名，需要推断相应的 `DocumentFormat`。GroupDocs.Editor 提供了一个简洁的静态帮助方法，将文件扩展名映射到内部格式表示，便于在加载到编辑器之前验证或转换文件。

### 解析电子表格格式
`Formats.SpreadsheetFormats.FromExtension` 将文件扩展名字符串转换为相应的电子表格格式枚举值。

```csharp
```csharp
Formats.SpreadsheetFormats expectedXlsm = Formats.SpreadsheetFormats.FromExtension(".xlsm");
Console.WriteLine("Parsed Spreadsheet format is {0}", expectedXlsm.Name);
```
```

**说明：**  
1. **解析格式：** `FromExtension` 将 `.xlsm` 扩展名转换为内部的 `SpreadsheetFormat` 枚举。  
2. **输出格式：** 打印解析后的格式名称，以确认映射。

### 解析文本格式
同样，`Formats.TextualFormats.FromExtension` 解析文本文件扩展名，如 HTML 或 TXT。

```csharp
```csharp
Formats.TextualFormats expectedHtml = Formats.TextualFormats.FromExtension("html");
Console.WriteLine("Parsed Textual format is {0}", expectedHtml.Name);
```
```

**说明：**  
1. **解析格式：** `FromExtension` 方法将 `html` 扩展名解析为 `TextFormat`。  
2. **输出格式：** 显示文本格式的名称，对基于 Web 的编辑器很有用。

## 确定格式后如何编辑文档？

确认格式后，加载和编辑文档遵循一致的模式。首先使用源文件路径创建 `Editor` 实例，然后调用 `Edit()` 获取 `EditableDocument`。随后您可以读取、修改，最后使用相应的 `SaveOptions` 保存内容。

### 加载文档
`Editor` 是封装给定文件所有编辑操作的核心类。

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/document.docx"))
{
    // Further steps will be covered here.
}
```
```

**说明：**  
1. **初始化 Editor：** 创建 `Editor` 实例，传入目标文件的完整路径。  
2. **释放模式：** `using` 语句确保及时释放所有非托管资源。

### 提取内容
`EditableDocument.GetContent()` 返回文档的原始文本（或针对基于 Web 的编辑器的 HTML），您可以对其进行显示或操作。

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    string content = editableDocument.GetContent();
    Console.WriteLine(content);
}
```
```

**说明：**  
1. **Edit 方法：** `Edit()` 返回 `EditableDocument` 对象。  
2. **获取内容：** `GetContent()` 提取文档的原始文本（或针对基于 Web 的编辑器的 HTML）。  
3. **输出内容：** 将内容写入控制台以进行验证。

### 保存更改
`SaveOptions` 指定编辑器如何以及以何种格式将编辑后的文档写回存储。

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    // Modify content here
    SaveOptions saveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docx);
    editor.Save(editableDocument, "path/to/save/document.docx", saveOptions);
}
```
```

**说明：**  
1. **Edit 方法：** 在修改后重新获取 `EditableDocument`。  
2. **修改内容：** 对字符串进行更改（此处未展示）。  
3. **保存选项：** 使用所需的输出格式配置 `SaveOptions`。  
4. **保存文档：** 将编辑后的文件写回磁盘。

## 如何处理不同的文档类型？

GroupDocs.Editor 将 Word、电子表格和演示文稿的处理抽象为相同的 API 接口，使得在不同文档类型之间切换变得轻松，无需为每个文档族学习一套新类。

### 编辑电子表格文档
`SpreadsheetSaveOptions` 定义电子表格的写入方式，包括格式和可选的压缩设置。

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/spreadsheet.xlsx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // Modify content here
        SaveOptions saveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsx);
        editor.Save(editableDocument, "path/to/save/spreadsheet.xlsx", saveOptions);
    }
}
```
```

**说明：**  
1. **初始化 Editor：** 将电子表格文件路径传递给 `Editor` 构造函数。  
2. **Edit 方法：** 获取 `EditableDocument`。  
3. **获取内容：** 打印电子表格的 CSV 表示（或 HTML）。  
4. **修改内容：** 应用所需的单元格级别更改。  
5. **保存选项：** 选择合适的 `SpreadsheetSaveOptions`。  
6. **保存文档：** 将更新后的电子表格写回存储。

### 编辑演示文稿文档
`PresentationSaveOptions` 控制幻灯片文件的输出格式，允许您保持或更改原始文件类型。

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/presentation.pptx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // Modify content here
        SaveOptions saveOptions = new PresentationSaveOptions(PresentationFormats.Pptx);
        editor.Save(editableDocument, "path/to/save/presentation.pptx", saveOptions);
    }
}
```
```

**说明：**  
1. **初始化 Editor：** 通过 `Editor` 加载 PowerPoint 文件。  
2. **Edit 方法：** 获取 `EditableDocument`。  
3. **获取内容：** 提取幻灯片的 HTML 或纯文本。  
4. **修改内容：** 更新标题、项目符号或图像。  
5. **保存选项：** 使用 `PresentationSaveOptions` 定义输出格式。  
6. **保存文档：** 将编辑后的演示文稿保存。

## 常见问题及解决方案
- **“不支持的格式”错误：** 确认您使用的是最新的 GroupDocs.Editor 版本；它会定期添加对新 Office 格式的支持。  
- **大文件内存消耗：** 在加载文档前将 `EditorSettings.EnableStreaming = true` 设置为启用流式模式。  
- **许可证未应用：** 确保临时许可证文件放置在应用程序根目录，或通过 `License license = new License(); license.SetLicense("path/to/license.lic");` 加载。

## 常见问答

**问：`DocumentFormatInfo` 与 `SaveOptions` 有何区别？**  
答：`DocumentFormatInfo` 提供关于支持的文件类型的元数据，而 `SaveOptions` 配置文档写回磁盘的方式（格式、压缩等）。

**问：我可以列出自定义文件扩展名的格式吗？**  
答：可以——使用 `DocumentFormatInfo.FromExtension("yourExt")`；如果未识别该扩展名，方法返回 `null`。

**问：GroupDocs.Editor 是否支持受密码保护的文件？**  
答：当然。通过 `EditorSettings` 将密码传递给 `Editor` 构造函数即可打开加密文档。

**问：GroupDocs.Editor 实际支持多少种格式？**  
答：超过 **30 种输入和输出格式**，涵盖 Word、Excel、PowerPoint、HTML 和纯文本。

**问：有没有办法将列表限制为仅可编辑的格式？**  
答：使用 `GetEditableWordProcessingFormats()`（或对应的 Spreadsheet/Presentation 方法）获取允许完整编辑功能的格式。

## 其他资源
- 从 [GroupDocs 发布页面](https://releases.groupdocs.com/editor/net/) 下载库。  
- 获取 [临时许可证](https://purchase.groupdocs.com/temporary-license/) 以获得完整功能访问。  
- 使用 [免费试用](https://releases.groupdocs.com/) 体验产品。  
- 在 [GroupDocs.Editor 文档](https://tutorials.groupdocs.com/editor/net/) 中查阅详细使用示例。  
- 在 [支持论坛](https://forum.groupdocs.com/c/editor/20) 上获取社区帮助。

## 结论

通过本指南，您现在了解如何 **列出支持的文档格式**、**根据扩展名确定文件格式**，以及使用适用于 .NET 的 GroupDocs.Editor **编辑 Word、电子表格和演示文稿**。将这些代码片段集成到自己的项目中，构建强大且具备格式感知的应用程序，提升终端用户体验并降低运行时错误。

---

**最后更新：** 2026-06-06  
**测试环境：** GroupDocs.Editor 23.9 for .NET  
**作者：** GroupDocs

## 相关教程

- [精通 .NET 中的文档加载（使用 GroupDocs.Editor）：全面指南](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)
- [精通 .NET 中的文档编辑（使用 GroupDocs.Editor）：全面指南](/editor/net/document-editing/master-document-editing-dotnet-groupdocs-editor/)
- [使用 GroupDocs.Editor .NET 将 Word 转换为 HTML：分步指南](/editor/net/document-saving/convert-word-to-html-groupdocs-editor-dotnet/)