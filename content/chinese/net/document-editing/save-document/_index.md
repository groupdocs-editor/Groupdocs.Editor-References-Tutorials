---
title: 保存文档
linktitle: 保存文档
second_title: GroupDocs.Editor .NET API
description: 使用 GroupDocs.Editor for .NET 轻松编辑和保存文档。本分步指南简化了开发人员的流程。
weight: 14
url: /zh/net/document-editing/save-document/
type: docs
---
# 保存文档

## 介绍
您是否希望使用 GroupDocs.Editor for .NET 轻松编辑和保存文档？您来对地方了！本教程将逐步指导您完成整个过程，确保您可以轻松管理文档。无论您是经验丰富的开发人员还是初学者，我们的指南都将为您提供入门所需的所有信息。
## 先决条件
在深入学习本教程之前，请确保您已满足以下先决条件：
- 开发环境：您的机器上安装了 Visual Studio。
- .NET Framework：确保您拥有.NET Framework 4.6.1 或更高版本。
-  GroupDocs.Editor for .NET：下载最新版本[这里](https://releases.groupdocs.com/editor/net/).
- 基本 C# 知识：熟悉 C# 编程至关重要。
## 导入命名空间
要在 .NET 项目中使用 GroupDocs.Editor，您需要导入必要的命名空间。操作方法如下：
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
现在我们已经设置好了环境并导入了必要的命名空间，让我们深入了解使用 GroupDocs.Editor for .NET 加载、编辑和保存文档所需的步骤。
## 步骤 1：加载文档
首先，我们需要加载要编辑的文档。GroupDocs.Editor 使这个过程变得简单。您可以这样做：

```csharp
string inputFilePath = "Your Sample Document";
Editor editor = new Editor(inputFilePath, delegate { return new Options.WordProcessingLoadOptions(); });
EditableDocument defaultWordProcessingDoc = editor.Edit();
```
在此步骤中，我们指定要编辑的文档的路径，并创建`Editor`类。`Edit`然后调用方法将文档加载到`EditableDocument`目的。
## 步骤2：修改文档
文档加载完成后，就该进行一些修改了。由于我们没有附加所见即所得的编辑器，因此我们将在代码中模拟编辑过程。

```csharp
string allEmbeddedInsideString = defaultWordProcessingDoc.GetEmbeddedHtml();
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
EditableDocument editedDoc = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```
在这里，我们检索文档嵌入的 HTML 内容，执行简单的文本替换，并创建一个新的`EditableDocument`来自修改后的 HTML 的实例。
## 步骤 3：保存文档
编辑文档后，最后一步是保存。GroupDocs.Editor 提供了多种选项，可用于以不同格式保存文档。
## 另存为 RTF
```csharp
string outputRtfPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.rtf");
WordProcessingSaveOptions rtfSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
editor.Save(editedDoc, outputRtfPath, rtfSaveOptions);
```
## 另存为 DOCM
```csharp
string outputDocmPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.docm");
WordProcessingSaveOptions docmSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm);
using (FileStream outputStream = File.Create(outputDocmPath))
{
    editor.Save(editedDoc, outputStream, docmSaveOptions);
}
```
## 另存为纯文本
```csharp
string outputTxtPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.txt");
TextSaveOptions textSaveOptions = new TextSaveOptions
{
    Encoding = System.Text.Encoding.UTF8,
    PreserveTableLayout = true
};
editor.Save(editedDoc, outputTxtPath, textSaveOptions);
```
## 步骤 4：清理
最后，至关重要的是处理`EditableDocument`和`Editor`实例以释放资源。
```csharp
editedDoc.Dispose();
defaultWordProcessingDoc.Dispose();
editor.Dispose();
```
通过遵循这些步骤，您可以使用 GroupDocs.Editor for .NET 高效地加载、编辑和保存文档。这个强大的工具提供了灵活性和易用性，使文档管理变得轻而易举。
## 结论
使用 GroupDocs.Editor for .NET，以编程方式编辑和保存文档从未如此简单。本指南将引导您完成整个过程，从加载文档到以各种格式保存文档。使用 GroupDocs.Editor，您可以轻松获得多功能且强大的解决方案，从而简化文档编辑过程。
## 常见问题解答
### GroupDocs.Editor 支持哪些文件格式？
GroupDocs.Editor 支持多种文件格式，包括 DOCX、RTF、TXT 等。如需查看完整列表，请查看[文档](https://tutorials.groupdocs.com/editor/net/).
### 我可以在购买之前试用 GroupDocs.Editor 吗？
是的，你可以得到一个[免费试用](https://releases.groupdocs.com/)测试 GroupDocs.Editor 的功能。
### 如果我遇到问题，可以获得任何支持吗？
当然！您可以访问[支持论坛](https://forum.groupdocs.com/c/editor/20)为您遇到的任何问题提供帮助。
### 如何取得临时执照？
您可以请求[临时执照](https://purchase.groupdocs.com/temporary-license/)用于评估目的。
### 我可以在哪里购买 GroupDocs.Editor 的完整版本？
你可以购买完整版[这里](https://purchase.groupdocs.com/buy).