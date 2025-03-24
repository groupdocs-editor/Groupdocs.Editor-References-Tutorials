---
title: Work with Multi-Tab Spreadsheets
linktitle: Work with Multi-Tab Spreadsheets
second_title: GroupDocs.Editor .NET API
description: Learn how to work with multi-tab spreadsheets in .NET using GroupDocs.Editor. Step-by-step guide, code examples, and best practices included.
weight: 17
url: /net/document-processing/work-multi-tab-spreadsheets/
---

# Work with Multi-Tab Spreadsheets

## Introduction
Handling multi-tab spreadsheets can be quite a task, especially when you need to manipulate or extract data from different sheets within the same document. If you're working with .NET and looking for a robust solution, GroupDocs.Editor for .NET is an excellent choice. In this tutorial, we will walk you through the process of working with multi-tab spreadsheets using GroupDocs.Editor for .NET. We'll cover everything from setting up your environment to saving each tab as a separate file.
## Prerequisites
Before diving into the tutorial, make sure you have the following prerequisites in place:
1. Visual Studio: Ensure you have Visual Studio installed on your machine.
2. .NET Framework: GroupDocs.Editor for .NET supports .NET Framework 4.0 or higher.
3. GroupDocs.Editor for .NET: Download and install the GroupDocs.Editor for .NET library. You can get it from the [download page](https://releases.groupdocs.com/editor/net/).
4. License: While you can use a [temporary license](https://purchase.groupdocs.com/temporary-license/) to try out the library, it's recommended to purchase a full license for production use.
## Import Namespaces
Before we start coding, you need to import the necessary namespaces. Add the following using directives to the top of your .cs file:
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
## 1. Get a Path to the Input File
First, you need to specify the path to your input spreadsheet file. This file should be an XLSX (OOXML) with multiple tabs.
```csharp
string inputFilePath = "Your Sample Document";
```
## 2. Load the Spreadsheet into the Editor Instance
Next, you'll load the spreadsheet into an `Editor` instance. This is done using a file stream and specifying the appropriate load options for a spreadsheet.
```csharp
using (FileStream inputStream = File.OpenRead(inputFilePath))
{
    using (Editor editor = new Editor(delegate { return inputStream; }, delegate { return new SpreadsheetLoadOptions(); }))
    {
        // Further steps will go here
    }
}
```
## 3. Create an EditableDocument from the First Tab
To edit or manipulate a specific tab, you need to create an `EditableDocument` instance for that tab. The tab is specified using a 0-based index.
```csharp
SpreadsheetEditOptions editOptions1 = new SpreadsheetEditOptions();
editOptions1.WorksheetIndex = 0; // First tab
EditableDocument firstTabBeforeEdit = editor.Edit(editOptions1);
```
## 4. Create an EditableDocument from the Second Tab
Similarly, create an `EditableDocument` for the second tab.
```csharp
SpreadsheetEditOptions editOptions2 = new SpreadsheetEditOptions();
editOptions2.WorksheetIndex = 1; // Second tab
EditableDocument secondTabBeforeEdit = editor.Edit(editOptions2);
```
## 5. Save the First Tab to a Separate Document
Now, save the first tab as a separate document. Specify the save format and output path.
```csharp
SpreadsheetSaveOptions saveOptions1 = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
string outputFilename1 = Path.GetFileNameWithoutExtension(inputFilePath) + "_tab1.xlsm";
string outputPath1 = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename1);
editor.Save(firstTabBeforeEdit, outputPath1, saveOptions1);
```
## 6. Save the Second Tab to a Separate Document
Repeat the process for the second tab, but this time save it in a different format.
```csharp
SpreadsheetSaveOptions saveOptions2 = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsb);
string outputFilename2 = Path.GetFileNameWithoutExtension(inputFilePath) + "_tab2.xlsb";
string outputPath2 = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename2);
editor.Save(secondTabBeforeEdit, outputPath2, saveOptions2);
```
## 7. Dispose of EditableDocument Instances
Finally, ensure that you properly dispose of the `EditableDocument` instances to free up resources.
```csharp
firstTabBeforeEdit.Dispose();
secondTabBeforeEdit.Dispose();
```

## Conclusion
By following these steps, you can easily work with multi-tab spreadsheets in .NET using GroupDocs.Editor. This powerful library simplifies the process of editing and saving different sheets within a spreadsheet, making your development tasks more manageable. Whether you're dealing with complex data manipulation or simple edits, GroupDocs.Editor for .NET provides the tools you need to get the job done efficiently.
## FAQ's
### What is GroupDocs.Editor for .NET?
GroupDocs.Editor for .NET is a powerful document editing API that allows developers to load, edit, and save documents of various formats within .NET applications.
### Can I try GroupDocs.Editor for .NET before purchasing?
Yes, you can use a [free trial](https://releases.groupdocs.com/) or request a [temporary license](https://purchase.groupdocs.com/temporary-license/) to evaluate the product.
### What file formats are supported by GroupDocs.Editor for .NET?
GroupDocs.Editor supports a wide range of formats, including DOCX, XLSX, PPTX, PDF, and many more.
### How do I get support for GroupDocs.Editor for .NET?
You can get support by visiting the [support forum](https://forum.groupdocs.com/c/editor/20).
### Where can I buy a full license for GroupDocs.Editor for .NET?
You can purchase a full license from the [purchase page](https://purchase.groupdocs.com/buy).
