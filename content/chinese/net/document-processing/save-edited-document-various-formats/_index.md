---
title: 将编辑的文档保存为各种格式
linktitle: 将编辑的文档保存为各种格式
second_title: GroupDocs.Editor .NET API
description: 在本全面的分步指南中了解如何使用 GroupDocs.Editor for .NET 将编辑后的文档保存为各种格式。
weight: 11
url: /zh/net/document-processing/save-edited-document-various-formats/
type: docs
---
# 将编辑的文档保存为各种格式

## 介绍
您是否希望使用 GroupDocs.Editor for .NET 将编辑后的文档保存为各种格式？您来对地方了！本综合指南将引导您完成整个过程，从设置环境到以多种格式保存编辑后的文档。让我们开始吧，让文档编辑和保存变得轻而易举！
## 先决条件
在开始之前，请确保您已准备好以下物品：
1.  GroupDocs.Editor for .NET - 从以下网址下载最新版本[这里](https://releases.groupdocs.com/editor/net/).
2. 开发环境-Visual Studio或任何其他.NET兼容IDE。
3. .NET Framework - 确保您已安装.NET Framework 4.6.1 或更高版本。
4. 示例文档 — 可供使用的 WordProcessing 文档示例。
5. 基本 C# 知识 - 需要熟悉 C# 编程。
## 导入命名空间
首先，确保将必要的命名空间导入到 C# 项目中。这对于访问 GroupDocs.Editor 功能至关重要。
```csharp
using System;
using GroupDocs.Editor.Metadata;
```
让我们将这个过程分解成几个可管理的步骤。仔细遵循以确保你理解每个部分。
## 步骤 1：获取输入文件的路径
首先，您需要指定输入文字处理文件的路径。此文件将被加载和编辑。
```csharp
string inputFilePath = "Your Sample Document";
```
## 步骤 2：为文档创建加载选项
接下来，创建特定于 WordProcessing 文档的加载选项。这些选项将有助于自定义文档的加载方式。
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
```
## 步骤 3：加载带有选项的文档
现在，将文档加载到`Editor`使用指定的加载选项的实例。
```csharp
using (Editor editor = new Editor(inputFilePath, delegate { return loadOptions; }))
```
## 步骤 4：创建编辑选项
准备文档的编辑选项。这些选项将决定如何打开文档进行编辑。
```csharp
WordProcessingEditOptions editOptions = new WordProcessingEditOptions();
```
## 步骤 5：打开文档进行编辑
通过创建`EditableDocument`实例。此实例将允许您对文档进行更改。
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
```
## 步骤6：编辑文档内容
现在是时候编辑文档的内容了。首先，将文档作为单个 base64 编码的字符串获取。
```csharp
string allEmbeddedInsideString = beforeEdit.GetEmbeddedHtml();
```
例如我们来修改文档中的字幕。
```csharp
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
```
## 步骤 7：根据编辑的内容创建新的可编辑文档
创建一个新的`EditableDocument`来自编辑的内容和资源的实例。
```csharp
using (EditableDocument afterEdit = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null))
```
## 步骤 8：将文档保存为各种格式
最后，遍历所有可支持的 WordProcessing 格式并以每种格式保存编辑的文档。
```csharp
foreach (WordProcessingFormats oneFormat in WordProcessingFormats.All)
{
    //准备保存选项
    WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(oneFormat);
    //准备保存路径
    string savePath = Path.Combine("OutputDirectory", "MultipleOutFormats." + saveOptions.OutputFormat.Extension);
    //保存文档
    editor.Save(afterEdit, savePath, saveOptions);
}
```
## 完成消息
最后，您可以打印一条消息，表明该过程已成功完成。
```csharp
Console.WriteLine("SavingEditedDocumentToAllFormats routine has successfully finished");
```
## 结论
恭喜！您已成功了解如何使用 GroupDocs.Editor for .NET 将已编辑的文档保存为各种格式。这个功能强大的工具只需几行代码即可轻松操作和保存多种格式的文档。请记住，关键步骤包括加载文档、编辑内容以及将其保存为所需的格式。
## 常见问题解答
### 什么是 GroupDocs.Editor for .NET？
GroupDocs.Editor for .NET 是一个强大的 API，允许您使用 .NET 应用程序编辑各种格式的文档。
### 我可以免费使用 GroupDocs.Editor 吗？
是的，您可以免费试用。下载[这里](https://releases.groupdocs.com/).
### GroupDocs.Editor 支持哪些格式？
GroupDocs.Editor 支持多种格式，包括 DOCX、PDF、HTML 等。
### 如何获得 GroupDocs.Editor 的临时许可证？
您可以获得临时驾照[这里](https://purchase.groupdocs.com/temporary-license/).
### 在哪里可以找到更多文档和支持？
有详细文档可供查阅[这里](https://tutorials.groupdocs.com/editor/net/) ，你可以得到支持[这里](https://forum.groupdocs.com/c/editor/20).