---
title: Work with Delimited Separated Values (DSV)
linktitle: Work with Delimited Separated Values (DSV)
second_title: GroupDocs.Editor .NET API
description: Learn how to edit CSV and TSV files using GroupDocs.Editor for .NET with this step-by-step guide. Improve your .NET projects effortlessly.
type: docs
weight: 12
url: /net/document-processing/work-dsv/
---
## Introduction
If you’re a developer working with delimited separated values (DSV) like CSV or TSV files, you know that editing these files programmatically can be a daunting task. However, with GroupDocs.Editor for .NET, this task becomes significantly simpler and more efficient. In this tutorial, we will walk you through how to use GroupDocs.Editor for .NET to read, edit, and save DSV files. We’ll break down the process into easy-to-follow steps, making it straightforward for you to implement in your projects.
## Prerequisites
Before we dive into the tutorial, make sure you have the following prerequisites:
- Visual Studio: Ensure you have Visual Studio installed on your machine.
- GroupDocs.Editor for .NET: You will need to download and reference the GroupDocs.Editor for .NET library. You can download it [here](https://releases.groupdocs.com/editor/net/).
- Basic Understanding of C#: This tutorial assumes you have a basic understanding of C# and .NET development.
## Import Namespaces
First, you need to import the necessary namespaces in your project. These namespaces provide the classes and methods required to work with GroupDocs.Editor for .NET.
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

## Step 1: Get a Path to the Input DSV File
First, you need to specify the path to the input DSV file. For this example, we'll assume it's a CSV file.
```csharp
string inputFilePath = "Your Sample Document";
```
## Step 2: Create an Editor Instance
Create an instance of the `Editor` class. This instance will be used to load and manipulate the DSV file.
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## Step 3: Create DSV Edit Options
Next, create an instance of `DelimitedTextEditOptions` and specify the delimiter for the DSV file. Here, we use a comma as the delimiter.
```csharp
    Options.DelimitedTextEditOptions editOptions = new DelimitedTextEditOptions(",");
    editOptions.ConvertDateTimeData = false;
    editOptions.ConvertNumericData = true;
    editOptions.TreatConsecutiveDelimitersAsOne = true;
```
## Step 4: Create an EditableDocument Instance
Create an `EditableDocument` instance using the `Editor.Edit` method. This prepares the document for editing.
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## Step 5: Edit the Document Content
Retrieve the original text content and make the necessary modifications. For demonstration purposes, let's replace some text.
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("SsangYong", "Chevrolet").Replace("Kyron", "Camaro");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## Step 6: Create an EditableDocument with Updated Content
Create a new `EditableDocument` with the updated content.
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## Step 7: Create CSV Save Options
Specify the save options for CSV format, including the delimiter and encoding.
```csharp
    Options.DelimitedTextSaveOptions csvSaveOptions = new DelimitedTextSaveOptions(",");
    csvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## Step 8: Create TSV Save Options
Similarly, specify the save options for TSV format.
```csharp
    Options.DelimitedTextSaveOptions tsvSaveOptions = new DelimitedTextSaveOptions("\t");
    tsvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## Step 9: Create Spreadsheet Save Options
If you need to save the document as a spreadsheet, create the corresponding save options.
```csharp
    Options.SpreadsheetSaveOptions cellsSaveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
```
## Step 10: Prepare Save Paths
Define the paths where the edited files will be saved.
```csharp
    string outputCsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".csv");
    string outputTsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".tsv");
    string outputCellsPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".xlsm");
```
## Step 11: Save the Edited Document
Save the edited document to the specified paths in different formats.
```csharp
    editor.Save(afterEdit, outputCsvPath, csvSaveOptions);
    editor.Save(afterEdit, outputTsvPath, tsvSaveOptions);
    editor.Save(afterEdit, outputCellsPath, cellsSaveOptions);
```
## Step 12: Dispose EditableDocument Instances
Finally, make sure to dispose of the `EditableDocument` instances to free up resources.
```csharp
    beforeEdit.Dispose();
    afterEdit.Dispose();
}
System.Console.WriteLine("WorkingWithDsv routine has successfully finished");
```
## Conclusion
Editing DSV files using GroupDocs.Editor for .NET is a straightforward process that involves creating an editor instance, setting edit options, modifying the content, and saving the changes. This step-by-step guide should help you integrate this functionality into your .NET applications with ease. Whether you're working with CSV, TSV, or other DSV formats, GroupDocs.Editor for .NET provides a robust and flexible solution.
## FAQ's
### Can I use GroupDocs.Editor for .NET to edit large CSV files?
Yes, GroupDocs.Editor for .NET is capable of handling large CSV files efficiently.
### Does GroupDocs.Editor for .NET support other DSV formats besides CSV and TSV?
Yes, it supports various DSV formats as long as you specify the appropriate delimiter.
### Is it possible to customize the encoding when saving DSV files?
Absolutely, you can specify the desired encoding in the save options.
### Can I convert a CSV file to an Excel spreadsheet using GroupDocs.Editor for .NET?
Yes, you can save a CSV file as an Excel spreadsheet by using the appropriate save options.
### Where can I find more documentation on GroupDocs.Editor for .NET?
You can find detailed documentation [here](https://reference.groupdocs.com/editor/net/)
