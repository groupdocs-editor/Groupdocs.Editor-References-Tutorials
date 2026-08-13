---
date: 2026-06-06
description: 了解如何使用 GroupDocs.Editor for .NET 从 CSV 和 TSV 文件 **创建可编辑文档** 对象。本指南还展示了如何在
  Visual Studio 中高效地 **读取分隔文本 C#** 和 **编辑 CSV .NET**。
keywords:
- create editable document
- read delimited text c#
- edit csv .net
- parse delimited values c#
linktitle: 使用分隔值 (DSV) – 创建可编辑文档
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to **create editable document** objects from CSV and TSV
    files using GroupDocs.Editor for .NET. This guide also shows how to **read delimited
    text C#** and **edit CSV .NET** efficiently in Visual Studio.
  headline: Work with Delimited Separated Values (DSV) – create editable document
  type: TechArticle
- questions:
  - answer: Yes, the API streams data and can handle files larger than 1 GB without
      loading the entire document into memory.
    question: Can I use GroupDocs.Editor for .NET to edit large CSV files?
  - answer: Absolutely – any single‑character delimiter (e.g., pipe `|`, semicolon
      `;`) is supported as long as you specify it in `DelimitedTextEditOptions`.
    question: Does GroupDocs.Editor for .NET support other DSV formats besides CSV
      and TSV?
  - answer: Yes, you can set the `Encoding` property in `DelimitedTextSaveOptions`
      to UTF‑8, UTF‑16, ISO‑8859‑1, or any .NET `Encoding` you require.
    question: Is it possible to customize the encoding when saving DSV files?
  - answer: Yes – after editing, simply use `SpreadsheetSaveOptions` to export the
      content as an `.xlsx` workbook.
    question: Can I convert a CSV file to an Excel spreadsheet using GroupDocs.Editor
      for .NET?
  - answer: Detailed API references and code samples are available **[here](https://tutorials.groupdocs.com/editor/net/)**.
    question: Where can I find more documentation on GroupDocs.Editor for .NET?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: 使用分隔值 (DSV) – 创建可编辑文档
type: docs
url: /zh/net/document-processing/work-dsv/
weight: 12
---

# 使用分隔值 (DSV) – 创建可编辑文档

如果您是一名需要从 CSV 或 TSV 等分隔值 (DSV) 创建 **create editable document** 对象的 .NET 开发者，您来对地方了。在前 100 个字里我们将说明为什么 GroupDocs.Editor for .NET 是 **read delimited text C#**、编辑并在不丢失格式的情况下保存的最可靠方式。您将获得一个完整的、可直接复制粘贴的工作流，能够自然地融入任何 Visual Studio 解决方案。

## 快速答案
- **哪个库在 .NET 中处理 CSV 编辑最佳？** GroupDocs.Editor for .NET.
- **我可以在 Visual Studio 中编辑大型 CSV 文件吗？** 是 – API 采用流式处理并避免将整个文件加载到内存中。
- **生产环境使用是否需要许可证？** 需要商业许可证；提供免费试用。
- **编辑后我可以输出哪些格式？** CSV、TSV 和兼容 Excel 的电子表格格式。
- **API 是否兼容 .NET 6+？** 当然 – 它支持 .NET Framework 4.5+、.NET Core 3.1+、.NET 5 和 .NET 6.

## 在 GroupDocs.Editor 中，“create editable document” 是什么？
**Create editable document** 指生成一个 `EditableDocument` 实例，该实例在内存中表示源文件（CSV、TSV 等）的可变版本。该对象允许您使用相同的 API 读取、修改并重新保存内容。它提供了获取文档文本、应用更改以及以各种格式保存的方式，确保列对齐和引用方式得以保留。

## 为什么在 DSV 处理时使用 GroupDocs.Editor？
GroupDocs.Editor 处理 **超过 50 种输入和输出格式**，包括 CSV、TSV 和兼容 Excel 的电子表格，同时对最高 500 MB 的文件保持内存使用低于 10 MB。它还能自动保留列对齐、引用规则和自定义编码，从而消除手动解析逻辑的需求。

## 前置条件
在开始之前，请确保已安装以下内容：

- **Visual Studio**（任意近期版本）– 您将在 IDE 中直接进行开发和调试。
- **GroupDocs.Editor for .NET** – 在 **[here](https://releases.groupdocs.com/editor/net/)** 下载最新包。
- **Basic C# knowledge** – 本教程假设您能够创建控制台或 ASP.NET 项目并添加 NuGet 包。

## 导入命名空间
`Editor`、`EditableDocument` 以及选项类位于 `GroupDocs.Editor` 命名空间。

`DelimitedTextEditOptions` 类是定义分隔符（逗号、制表符等）及其他解析规则的入口。

```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

## 如何从 CSV 文件创建 editable document？
使用 `Editor` 加载源 CSV 并调用 `Edit` 方法，传入指定逗号分隔符的 `DelimitedTextEditOptions` 实例。该方法返回一个可在内存中操作的 `EditableDocument`。这种加载 → 编辑的两步模式覆盖了 **read delimited text C#** 场景，并确保原始文件结构得以保留。

## 步骤 1：获取输入 DSV 文件的路径
首先，您需要指定源 DSV 文件的绝对或相对路径。演示中我们使用项目 `Data` 文件夹下的一个简单 CSV。

```csharp
string inputFilePath = "Your Sample Document";
```

## 步骤 2：创建 Editor 实例
`Editor` 是负责加载、编辑和保存的核心类。使用 `FileInfo` 对象实例化它即可完全控制文件的生命周期。

```csharp
using (Editor editor = new Editor(inputFilePath))
{
```

## 步骤 3：创建 DSV 编辑选项
`DelimitedTextEditOptions` 告诉编辑器如何解释文件。您可以设置分隔符、首行是否为标题以及字符编码。

```csharp
    Options.DelimitedTextEditOptions editOptions = new DelimitedTextEditOptions(",");
    editOptions.ConvertDateTimeData = false;
    editOptions.ConvertNumericData = true;
    editOptions.TreatConsecutiveDelimitersAsOne = true;
```

## 步骤 4：创建 EditableDocument 实例
`EditableDocument` 代表源文件在内存中的可变版本。使用选项调用 `Editor.Edit` 会返回一个 `EditableDocument`。该对象以可变字符串保存文件文本，随时可进行任何 **parse delimited values C#** 操作。

```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```

## 步骤 5：编辑文档内容
`GetDocumentText()` 以字符串形式返回可编辑文档的当前文本。通过 `EditableDocument.GetDocumentText()` 获取原始文本，进行修改（例如替换列值），并将结果存入新字符串。这就是在不触碰底层文件流的情况下 **edit CSV .NET** 的位置。

```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("SsangYong", "Chevrolet").Replace("Kyron", "Camaro");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```

## 步骤 6：使用更新内容创建 EditableDocument
将修改后的字符串重新包装为 `EditableDocument`。此步骤完成更改并准备将对象保存为任何受支持的格式。

```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```

## 步骤 7：创建 CSV 保存选项
`DelimitedTextSaveOptions` 指定如何将编辑后的内容写回 CSV 文件。当您准备持久化更改时，配置 `DelimitedTextSaveOptions`。您可以使用相同的分隔符、不同的分隔符，甚至更改换行样式。

```csharp
    Options.DelimitedTextSaveOptions csvSaveOptions = new DelimitedTextSaveOptions(",");
    csvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

## 步骤 8：创建 TSV 保存选项
如果需要制表符分隔的版本，只需将分隔符切换为 `\t`。同一个 `EditableDocument` 可以使用不同选项多次保存。

```csharp
    Options.DelimitedTextSaveOptions tsvSaveOptions = new DelimitedTextSaveOptions("\t");
    tsvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

## 步骤 9：创建电子表格保存选项
`SpreadsheetSaveOptions` 配置将文档导出为 Excel 兼容格式（如 .xlsx）。GroupDocs.Editor 还允许您将编辑后的数据导出为 Excel 兼容格式（`.xlsx`）。`SpreadsheetSaveOptions` 类会自动处理列类型、公式和单元格样式。

```csharp
    Options.SpreadsheetSaveOptions cellsSaveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
```

## 步骤 10：准备保存路径
为每种格式定义不同的输出路径。使用清晰的命名约定（例如 `output.csv`、`output.tsv`、`output.xlsx`）有助于保持项目组织有序。

```csharp
    string outputCsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".csv");
    string outputTsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".tsv");
    string outputCellsPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".xlsm");
```

## 步骤 11：保存编辑后的文档
`Save()` 使用提供的保存选项将文档写入磁盘。对每种目标格式调用 `EditableDocument.Save` 并传入相应选项。API 直接将文件写入磁盘，除非您手动覆盖，否则会保留原始编码。

```csharp
    editor.Save(afterEdit, outputCsvPath, csvSaveOptions);
    editor.Save(afterEdit, outputTsvPath, tsvSaveOptions);
    editor.Save(afterEdit, outputCellsPath, cellsSaveOptions);
```

## 步骤 12：释放 EditableDocument 实例
`Editor` 和 `EditableDocument` 都实现了 `IDisposable`。释放它们可以关闭文件句柄和非托管资源，这在批量处理大量文件时至关重要。

```csharp
    beforeEdit.Dispose();
    afterEdit.Dispose();
}
System.Console.WriteLine("WorkingWithDsv routine has successfully finished");
```

## 常见问题及解决方案
| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **意外的额外引号** | 默认的 CSV 解析器可能会把嵌入的逗号当作分隔符。 | 在 `DelimitedTextEditOptions` 中设置 `EscapeMode = EscapeMode.DoubleQuote`。 |
| **大文件内存激增** | 在未使用流式处理的情况下加载 500 MB 文件。 | 使用带有启用惰性加载的 `LoadOptions` 的 `Editor.Load`。 |
| **编码不匹配** | 源文件使用 UTF‑16，但选项默认使用 UTF‑8。 | 在保存选项中显式设置 `Encoding = Encoding.Unicode`。 |

## 常见问题

**Q: 我可以使用 GroupDocs.Editor for .NET 编辑大型 CSV 文件吗？**  
A: 是的，API 采用流式处理，能够在不将整个文档加载到内存的情况下处理大于 1 GB 的文件。

**Q: GroupDocs.Editor for .NET 是否支持除 CSV 和 TSV 之外的其他 DSV 格式？**  
A: 绝对支持 – 只要在 `DelimitedTextEditOptions` 中指定，任何单字符分隔符（例如管道 `|`、分号 `;`）均受支持。

**Q: 在保存 DSV 文件时可以自定义编码吗？**  
A: 可以，在 `DelimitedTextSaveOptions` 中设置 `Encoding` 属性为 UTF‑8、UTF‑16、ISO‑8859‑1 或任何 .NET `Encoding`。

**Q: 我可以使用 GroupDocs.Editor for .NET 将 CSV 文件转换为 Excel 电子表格吗？**  
A: 可以 – 编辑完成后，只需使用 `SpreadsheetSaveOptions` 将内容导出为 `.xlsx` 工作簿。

**Q: 在哪里可以找到更多关于 GroupDocs.Editor for .NET 的文档？**  
A: 详细的 API 参考和代码示例可在 **[here](https://tutorials.groupdocs.com/editor/net/)** 获取。

---

**最后更新：** 2026-06-06  
**测试环境：** GroupDocs.Editor 23.10 for .NET  
**作者：** GroupDocs

## 相关教程

- [GroupDocs.Editor .NET 的纯文本和 DSV 文档编辑教程](/editor/net/plain-text-dsv-documents/)
- [精通 GroupDocs.Editor .NET，实现高效 CSV 文档编辑与转换](/editor/net/plain-text-dsv-documents/groupdocs-editor-net-csv-editing-guide/)
- [在 .NET 中使用 GroupDocs.Editor 精通文档加载：完整指南](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)