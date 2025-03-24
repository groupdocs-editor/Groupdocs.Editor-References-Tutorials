---
title: Load Document
linktitle: Load Document
second_title: GroupDocs.Editor .NET API
description: Learn how to edit documents programmatically with GroupDocs.Editor for .NET. Step-by-step guide for loading documents, handling password-protected files, and more.
weight: 13
url: /net/document-editing/load-document/
---
## Introduction
Editing documents programmatically can be a daunting task, especially if you're dealing with different file formats and complex structures. Luckily, GroupDocs.Editor for .NET makes this task a breeze, providing a robust and easy-to-use API for editing a wide range of document types. In this tutorial, we’ll walk you through everything you need to get started with GroupDocs.Editor for .NET, including the prerequisites, how to import namespaces, and a detailed, step-by-step guide to loading documents using various methods.
## Prerequisites
Before we dive in, make sure you have the following prerequisites set up:
- Visual Studio: Ensure you have Visual Studio installed on your machine.
- .NET Framework: GroupDocs.Editor for .NET supports .NET Framework 2.0 or later. Ensure your project is targeting a compatible framework.
- GroupDocs.Editor for .NET: Download the latest version from the [download page](https://releases.groupdocs.com/editor/net/).
- Basic Knowledge of C#: Familiarity with C# and .NET programming is necessary to follow along with this tutorial.
## Import Namespaces
To begin using GroupDocs.Editor for .NET, you need to import the necessary namespaces into your project. Add the following using directives at the top of your C# file:
```csharp
using GroupDocs.Editor.Options;
using System.IO;
```
These namespaces will provide access to the classes and methods required for document editing tasks.
## Step 1: Load Document from a File Path
Loading a document from a file path is straightforward. This method is ideal for documents stored locally on your machine.

```csharp
string inputPath = "Your Sample Document";
// Load document as file via path and without load options
Editor editor1 = new Editor(inputPath);
// Dispose resources
editor1.Dispose();
System.Console.WriteLine("Document loaded successfully from file path.");
```
## Step 2: Load Document with Load Options
Sometimes, you may need to load documents that require special handling, such as password-protected files. In such cases, you can use load options.

```csharp
string inputPath = "Your Sample Document";
// Create load options for Word documents
WordProcessingLoadOptions wordLoadOptions = new WordProcessingLoadOptions();
wordLoadOptions.Password = "some password";
// Load document as file via path and with load options
Editor editor2 = new Editor(inputPath, delegate { return wordLoadOptions; });
// Dispose resources
editor2.Dispose();
System.Console.WriteLine("Password-protected document loaded successfully.");
```
## Step 3: Load Document from a Byte Stream
Loading a document from a byte stream is useful when you need to process documents that are not stored as files, such as those retrieved from a database or a web service.

```csharp
FileStream inputStream = File.OpenRead("Your Sample Document");
// Load document as content from byte stream and without load options
Editor editor3 = new Editor(delegate { return inputStream; });
// Dispose resources
editor3.Dispose();
System.Console.WriteLine("Document loaded successfully from byte stream.");
```
## Step 4: Load Document with Load Options from a Byte Stream
For documents requiring special handling when loaded from a byte stream, you can combine byte stream loading with load options.

```csharp
FileStream inputStream = File.OpenRead("Your Sample Document");
// Create load options for spreadsheets
SpreadsheetLoadOptions sheetLoadOptions = new SpreadsheetLoadOptions();
sheetLoadOptions.OptimizeMemoryUsage = true;
// Load document as content from byte stream and with load options
Editor editor4 = new Editor(delegate { return inputStream; }, delegate { return sheetLoadOptions; });
// Dispose resources
editor4.Dispose();
System.Console.WriteLine("Spreadsheet document loaded successfully with load options.");
```
## Conclusion
Congratulations! You’ve successfully learned how to load documents using GroupDocs.Editor for .NET in various ways. Whether you’re dealing with local files, password-protected documents, or byte streams, GroupDocs.Editor provides a flexible and powerful solution for your document editing needs. Remember to always dispose of resources to ensure optimal performance and resource management in your applications.
## FAQ's
### What file formats are supported by GroupDocs.Editor for .NET?
GroupDocs.Editor supports a wide range of file formats, including DOCX, XLSX, PPTX, HTML, and many more. For a full list, refer to the [documentation](https://tutorials.groupdocs.com/editor/net/).
### How do I handle password-protected documents?
You can use load options such as `WordProcessingLoadOptions` to specify the password when loading password-protected documents.
### Can I use GroupDocs.Editor in a web application?
Yes, GroupDocs.Editor can be used in web applications. Ensure you handle file streams and resource disposal properly to avoid memory leaks.
### Where can I get a temporary license for GroupDocs.Editor?
You can obtain a temporary license from the [temporary license page](https://purchase.groupdocs.com/temporary-license/).
### Is there support available if I encounter issues?
Yes, GroupDocs provides support through their [support forum](https://forum.groupdocs.com/c/editor/20).
