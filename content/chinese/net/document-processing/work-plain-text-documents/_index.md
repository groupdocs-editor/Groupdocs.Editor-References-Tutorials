---
title: 处理纯文本文档
linktitle: 处理纯文本文档
second_title: GroupDocs.Editor .NET API
description: 通过我们的分步指南学习如何使用 GroupDocs.Editor for .NET 编辑纯文本文档。简化您的 .NET 文档编辑过程。
weight: 15
url: /zh/net/document-processing/work-plain-text-documents/
---
## 介绍
您是否希望简化 .NET 中的文档编辑流程？GroupDocs.Editor for .NET 就是您的最佳选择！这个强大的 API 可让您轻松编辑各种文档格式。在本教程中，我们将指导您使用 GroupDocs.Editor for .NET 处理纯文本文档的过程。最后，您将能够像专业人士一样处理文本文档编辑。准备好了吗？让我们开始吧！
## 先决条件
在开始之前，您需要准备好以下几件事：
- .NET 开发环境：确保您已设置好可用的 .NET 开发环境。Visual Studio 是常用的选择。
-  适用于 .NET 的 GroupDocs.Editor：下载并安装[GroupDocs.Editor for .NET](https://releases.groupdocs.com/editor/net/).
- 基本 C# 知识：熟悉 C# 编程语言将帮助您理解示例。
- 文本编辑器：任何文本编辑器都可以，但考虑到其功能和易用性，我们推荐使用 Visual Studio Code。
## 导入命名空间
要开始使用 GroupDocs.Editor for .NET，您需要将必要的命名空间导入到您的项目中。这可确保所有必需的类和方法都可供使用。
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```
让我们将这个过程分解成易于管理的步骤。跟随我们的指引，完成使用 GroupDocs.Editor for .NET 编辑纯文本文档的每个阶段。
## 步骤 1：获取输入 TXT 文件的路径
首先，您需要指定输入 TXT 文件的路径。这可以是本地文件的路径，也可以是包含文件内容的流。
```csharp
string inputFilePath = "YourSampleDocument.txt";
```
## 步骤 2：创建编辑器实例
接下来，创建一个实例`Editor`类。该类负责加载和编辑文档。此阶段不需要加载选项。
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## 步骤 3：创建 TXT 编辑选项
现在，创建 TXT 编辑选项。这些选项允许您指定在编辑过程中如何处理文本内容。
```csharp
    TextEditOptions editOptions = new TextEditOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        RecognizeLists = true,
        LeadingSpaces = TextLeadingSpacesOptions.ConvertToIndent,
        TrailingSpaces = TextTrailingSpacesOptions.Trim
    };
```
## 步骤 4：创建 EditableDocument 实例
设置编辑选项后，创建一个`EditableDocument`实例。这表示可编辑格式的文档。
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## 步骤5：编辑文档内容
检索原始文本内容并进行所需的编辑。在此示例中，我们将用“已编辑的文本”替换“文本”一词。
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("text", "EDITED text");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## 步骤 6：创建包含更新内容的 EditableDocument
进行必要的编辑后，创建一个新的`EditableDocument`包含更新的内容和原始资源。
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## 步骤 7：创建文字处理保存选项
准备 WordProcessing 格式的保存选项。此示例使用 DOCM 格式并指定区域设置。
```csharp
    WordProcessingSaveOptions wordSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm)
    {
        Locale = System.Globalization.CultureInfo.GetCultureInfo("en-GB")
    };
```
## 步骤 8：创建 TXT 保存选项
同样，创建 TXT 格式的保存选项。确保编码设置为 UTF-8 并保留表格布局。
```csharp
    TextSaveOptions txtSaveOptions = new TextSaveOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        PreserveTableLayout = true
    };
```
## 步骤 9：准备输出路径
准备保存生成的 DOCX 和 TXT 文件的路径。使用输入文件路径确定输出目录和文件名。
```csharp
    string outputWordPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".docm");
    string outputTxtPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".txt");
```
## 步骤 10：保存编辑后的文档
最后，使用指定的保存选项以 DOCX 和 TXT 格式保存编辑的文档。
```csharp
    editor.Save(afterEdit, outputWordPath, wordSaveOptions);
    editor.Save(afterEdit, outputTxtPath, txtSaveOptions);
}
System.Console.WriteLine("Document editing process completed successfully!");
```
## 结论
恭喜！您已成功使用 GroupDocs.Editor for .NET 编辑纯文本文档。这款功能强大的工具简化了文档编辑，使其易于集成到您的 .NET 应用程序中。无论您处理的是简单的文本文件还是复杂的文档格式，GroupDocs.Editor 都能满足您的需求。访问[GroupDocs.Editor 文档](https://tutorials.groupdocs.com/editor/net/).
## 常见问题解答
### GroupDocs.Editor for .NET 支持哪些文件格式？
 GroupDocs.Editor for .NET 支持多种文件格式，包括 DOCX、TXT、HTML 等。查看[文档](https://tutorials.groupdocs.com/editor/net/)以获取完整列表。
### 如何免费试用 .NET 版 GroupDocs.Editor？
您可以从以下网址下载 GroupDocs.Editor for .NET 的免费试用版[发布页面](https://releases.groupdocs.com/).
### 我可以购买 GroupDocs.Editor for .NET 的临时许可证吗？
是的，你可以从[GroupDocs 购买页面](https://purchase.groupdocs.com/temporary-license/).
### 在哪里可以获得 .NET 的 GroupDocs.Editor 支持？
可通过以下方式获得支持[GroupDocs.Editor 支持论坛](https://forum.groupdocs.com/c/editor/20).
### 是否有关于 GroupDocs.Editor for .NET 的详细文档？
是的，详细文档可在[GroupDocs.Editor 文档页面](https://tutorials.groupdocs.com/editor/net/).