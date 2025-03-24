---
title: 创建文档
linktitle: 创建文档
second_title: GroupDocs.Editor .NET API
description: 通过本全面的分步教程学习如何使用 GroupDocs.Editor for .NET 编辑 Word、Excel、PowerPoint、电子书和电子邮件文档。
weight: 10
url: /zh/net/document-editing/create-document/
---

# 创建文档

## 介绍
您是否厌倦了以编程方式编辑不同文档类型所带来的麻烦？GroupDocs.Editor for .NET 可以简化此过程。此强大的工具允许开发人员轻松编辑各种文档格式，例如 Word、Excel、PowerPoint、电子书和电子邮件。在本教程中，我们将深入介绍如何使用 GroupDocs.Editor for .NET 创建和编辑文档。我们将把该过程分解为易于遵循的步骤，即使您是新手也可以轻松理解。
## 先决条件
在开始之前，请确保您已准备好以下物品：
- 您的机器上安装了 Visual Studio。
- .NET Framework（4.0 或更高版本）。
-  GroupDocs.Editor for .NET 库。您可以从[这里](https://releases.groupdocs.com/editor/net/).
- C# 编程的基本知识。
## 导入命名空间
首先，让我们导入必要的命名空间。这将使我们的应用程序中可以访问所需的类和方法。
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using System.IO;
```
## 步骤 1：设置流
首先，我们需要建立一个内存流作为文档内容的占位符。
```csharp
Stream memoryStream = Stream.Null;
```
## 步骤2：保存文档的回调函数
接下来，定义一个回调函数来保存新的文档流。此函数对于处理文档编辑过程的输出至关重要。
```csharp
void SaveNewDocument(Stream resultStream)
{
    memoryStream = resultStream;
}
```
## 步骤 3：创建和编辑文字处理文档
现在，让我们创建并编辑一个 Word 文档。我们首先创建一个新的`Editor`WordProcessing 文档的实例并使用默认选项对其进行编辑。
### 使用默认选项创建和编辑
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    EditableDocument defaultWordProcessingDoc = editor.Edit();
}
```
### 使用自定义选项进行创建和编辑
为了获得更多控制，我们可以指定诸如禁用分页和提取嵌入字体等选项。
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    WordProcessingEditOptions wordProcessingEditOptions = new WordProcessingEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true,
        FontExtraction = FontExtractionOptions.ExtractAllEmbedded
    };
    EditableDocument editableWordProcessingDocument = editor.Edit(wordProcessingEditOptions);
}
```
## 步骤 4：创建和编辑电子表格文档
同样，我们可以创建和编辑 Excel 文档。操作方法如下。
### 使用默认选项创建和编辑
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    EditableDocument defaultEditableSpreadsheetDocument = editor.Edit();
}
```
### 使用自定义选项进行创建和编辑
为了定位特定工作表或排除隐藏的工作表，我们使用`SpreadsheetEditOptions`.
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    SpreadsheetEditOptions spreadsheetEditOptions = new SpreadsheetEditOptions
    {
        WorksheetIndex = 0,
        ExcludeHiddenWorksheets = true
    };
    EditableDocument editableSpreadsheetDocument = editor.Edit(spreadsheetEditOptions);
}
```
## 步骤 5：创建和编辑演示文档
还支持 PowerPoint 演示文稿。让我们看看如何处理它们。
### 使用默认选项创建和编辑
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    EditableDocument defaultEditablePresentationDocument = editor.Edit();
}
```
### 使用自定义选项进行创建和编辑
您可以通过指定选项（例如显示哪张幻灯片以及是否包含隐藏幻灯片）来定制您的编辑。
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    PresentationEditOptions presentationEditOptions = new PresentationEditOptions
    {
        ShowHiddenSlides = false,
        SlideNumber = 0
    };
    EditableDocument editablePresentationDocument = editor.Edit(presentationEditOptions);
}
```
## 步骤6：创建和编辑电子书文档
GroupDocs.Editor 还允许编辑电子书格式，例如 EPUB。以下是您可以如何处理它。
### 使用默认选项创建和编辑
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EditableDocument defaultEditableEbookDocument = editor.Edit();
}
```
### 使用自定义选项进行创建和编辑
通过启用或禁用分页和语言信息来定制您的电子书编辑。
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EbookEditOptions ebookEditOptions = new EbookEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true
    };
    EditableDocument editableEbookDocument = editor.Edit(ebookEditOptions);
}
```
## 步骤 7：创建和编辑电子邮件文档
最后，我们将了解如何编辑电子邮件文档。其中包括 EML 等格式。
### 使用默认选项创建和编辑
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EditableDocument defaultEditableEmailDocument = editor.Edit();
}
```
### 使用自定义选项进行创建和编辑
指定邮件消息输出选项来控制编辑过程。
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EmailEditOptions emailEditOptions = new EmailEditOptions
    {
        MailMessageOutput = MailMessageOutput.All
    };
    EditableDocument editableEmailDocument = editor.Edit(emailEditOptions);
}
```
## 步骤 8：完成流程
编辑文档后，正确处理内存流以释放资源至关重要。
```csharp
memoryStream.Dispose();
System.Console.WriteLine("CreateDocument routine has successfully finished");
```
## 结论
GroupDocs.Editor for .NET 是一款功能强大的多功能工具，可以简化以编程方式编辑各种文档类型的任务。通过遵循此分步指南，您可以轻松创建和编辑文档，无论它们是 WordProcessing 文件、电子表格、演示文稿、电子书还是电子邮件。深入了解 GroupDocs.Editor 文档以了解更多高级功能和自定义选项。
## 常见问题解答
### 我可以使用 GroupDocs.Editor for .NET 编辑哪些类型的文档？
您可以编辑各种文档，包括文字处理、电子表格、演示文稿、电子书和电子邮件。
### 可以自定义编辑选项吗？
是的，GroupDocs.Editor for .NET 允许通过针对每种文档类型的各种编辑选项进行广泛的自定义。
### 我如何处理编辑后的文档的输出？
您可以使用回调函数将编辑的文档流保存到您想要的位置。
### 我需要许可证才能使用 GroupDocs.Editor for .NET 吗？
是的，你可以从[这里](https://purchase.groupdocs.com/buy)。还有临时执照的选项。
### 在哪里可以找到更详细的文档？
详细文档可在[GroupDocs.Editor for .NET 文档页面](https://tutorials.groupdocs.com/editor/net/).