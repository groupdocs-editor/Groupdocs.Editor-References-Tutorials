---
title: 设置计量许可证
linktitle: 设置计量许可证
second_title: GroupDocs.Editor .NET API
description: 通过我们的综合指南了解如何集成和使用 GroupDocs.Editor for .NET。在您的 .NET 应用程序中解锁强大的文档编辑功能。
weight: 12
url: /zh/net/quick-start-guide/set-metered-license/
type: docs
---
# 设置计量许可证

## 介绍
欢迎阅读我们关于如何使用 GroupDocs.Editor for .NET 的分步指南！无论您是经验丰富的开发人员还是刚刚入门，本教程都将帮助您充分利用这个强大库的潜力。GroupDocs.Editor for .NET 允许您在 .NET 应用程序中轻松编辑各种格式的文档。让我们深入探索如何开始使用这个强大的工具。
## 先决条件
在了解技术细节之前，请确保您满足以下先决条件：
- .NET 编程基础知识：熟悉 C# 和 .NET Framework。
- 已安装 Visual Studio：确保您的计算机上安装了最新版本的 Visual Studio。
-  GroupDocs.Editor for .NET：从[下载页面](https://releases.groupdocs.com/editor/net/).
- 有效的执照：从[GroupDocs 购买页面](https://purchase.groupdocs.com/temporary-license/).
## 导入命名空间
要使用 GroupDocs.Editor for .NET，您需要在项目中导入必要的命名空间。此步骤至关重要，因为它会设置您的项目以利用库的功能。
```csharp
using System;
using GroupDocs.Editor;
```
我们将每个示例分解为多个步骤，以确保您可以轻松地跟进。
## 步骤 1：安装 GroupDocs.Editor for .NET
首先，您需要在项目中安装 GroupDocs.Editor for .NET。您可以通过 Visual Studio 中的 NuGet 包管理器执行此操作。
### 通过 NuGet 包管理器安装
1. 在 Visual Studio 中打开您的项目。
2. 去`Tools`>`NuGet Package Manager`>`Manage NuGet Packages for Solution`.
3. 搜索`GroupDocs.Editor`.
4. 点击`Install`.
这将为您的项目添加必要的引用。
## 第 2 步：设置计量许可证
要解锁 GroupDocs.Editor 的全部功能，您需要设置计量许可证。这样您就可以不受任何限制地使用 API。
### 设置计量许可证
1. 从以下位置获取您的公钥和私钥[GroupDocs 购买页面](https://purchase.groupdocs.com/temporary-license/).
2. 将以下代码添加到您的项目以设置计量许可证：
```csharp
string publicKey = "*****";
string privateKey = "*****";
Metered metered = new Metered();
metered.SetMeteredKey(publicKey, privateKey);
Console.WriteLine("License set successfully.");
```
## 步骤 3：加载并编辑文档
现在您的项目已设置并获得许可，让我们继续加载和编辑文档。
### 加载文档
1. 添加以下代码来加载文档：
```csharp
string filePath = "sample.docx";
Editor editor = new Editor(filePath);
Console.WriteLine("Document loaded successfully.");
```
### 编辑文档
2. 要编辑文档，您需要将其转换为可编辑格式：
```csharp
EditableDocument editableDocument = editor.Edit();
string content = editableDocument.GetContent();
Console.WriteLine("Document converted to editable format.");
```
## 步骤 4：保存编辑后的文档
编辑文档后，最后一步是保存更改。
### 保存文档
1. 将编辑的内容转换回原始格式：
```csharp
string updatedContent = "<html><body>Updated content</body></html>";
editableDocument = EditableDocument.FromMarkup(updatedContent, new WordProcessingSaveOptions());
editor.Save(editableDocument, "updated_sample.docx");
Console.WriteLine("Document saved successfully.");
```
## 结论
恭喜！您已成功在应用程序中集成并使用 GroupDocs.Editor for .NET。从安装库到设置计量许可证和编辑文档，您已了解所有必要步骤。这个强大的工具可以显著简化 .NET 应用程序中的文档编辑工作流程。有关更多信息，请参阅[GroupDocs.Editor for .NET 文档](https://tutorials.groupdocs.com/editor/net/).
## 常见问题解答
### 如何获得 GroupDocs.Editor 许可证？
您可以从[GroupDocs 购买页面](https://purchase.groupdocs.com/buy)。如需临时许可证，请访问[这里](https://purchase.groupdocs.com/temporary-license/).
### 我可以免费试用 GroupDocs.Editor 吗？
是的，你可以从[下载页面](https://releases.groupdocs.com/)并申请临时执照。
### GroupDocs.Editor 支持哪些文档格式？
 GroupDocs.Editor 支持多种格式，包括 DOCX、PPTX、XLSX、TXT、HTML 等。如需查看完整列表，请查看[文档](https://tutorials.groupdocs.com/editor/net/).
### GroupDocs.Editor 是否有任何社区支持？
是的，你可以从[GroupDocs.Editor 论坛](https://forum.groupdocs.com/c/editor/20).
### 如何开始使用 GroupDocs.Editor for .NET？
按照我们的分步指南设置库、获取许可证并开始编辑文档。有关详细说明，请访问[文档](https://tutorials.groupdocs.com/editor/net/).