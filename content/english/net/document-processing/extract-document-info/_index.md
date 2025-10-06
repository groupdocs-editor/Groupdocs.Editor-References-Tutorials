---
title: Extract Document Info
linktitle: Extract Document Info
second_title: GroupDocs.Editor .NET API
description: Learn how to extract document information using GroupDocs.Editor for .NET with our detailed, step-by-step tutorial. Perfect for managing various document types.
weight: 10
url: /net/document-processing/extract-document-info/
type: docs
---
# Extract Document Info

## Introduction
Welcome to this comprehensive tutorial on extracting document information using GroupDocs.Editor for .NET. In this guide, we’ll walk you through the process step by step, making sure you understand each part clearly and concisely. Whether you're a seasoned developer or just getting started, this tutorial will help you seamlessly integrate GroupDocs.Editor into your .NET projects to manage and manipulate documents efficiently.
## Prerequisites
Before diving into the code, let's ensure you have everything you need:
- Basic Knowledge of C#: Understanding the basics of C# programming is essential.
- Visual Studio: Make sure you have Visual Studio installed.
- GroupDocs.Editor for .NET: You’ll need the GroupDocs.Editor for .NET library. You can download it from the [download page](https://releases.groupdocs.com/editor/net/).
## Import Namespaces
To start, you’ll need to import the necessary namespaces. This allows you to access the classes and methods required to manipulate documents.
```csharp
using System;
using GroupDocs.Editor.Metadata;
```
## Step 1: Load Your Document
First, you need to load the document you want to extract information from. This can be done by providing the file path to the document.
```csharp
string docxInputFilePath = "YourSampleDocument.docx";
Editor editorDocx = new Editor(docxInputFilePath);
```
## Step 2: Retrieve Document Information
Next, you will retrieve the document information using the `GetDocumentInfo` method. This method does not require any specific load options if you're unsure about the document format.
```csharp
IDocumentInfo infoDocx = editorDocx.GetDocumentInfo(null);
```
## Step 3: Determine Document Type
Now, you need to check the type of document you are dealing with. This is crucial as it dictates how you will handle the document.
```csharp
bool isSpreadsheet = infoDocx is SpreadsheetDocumentInfo;
bool isText = infoDocx is TextualDocumentInfo;
bool isWordProcessing = infoDocx is WordProcessingDocumentInfo;
Console.WriteLine($"Is '{docxInputFilePath}' a Spreadsheet: {isSpreadsheet}");
Console.WriteLine($"Is '{docxInputFilePath}' a Textual document: {isText}");
Console.WriteLine($"Is '{docxInputFilePath}' a WordProcessing document: {isWordProcessing}");
```
## Step 4: Extract Detailed Information
If the document is a Word Processing document, you can extract detailed information such as format, extension, page count, size, and whether it is encrypted.
```csharp
if (isWordProcessing)
{
    WordProcessingDocumentInfo casted = (WordProcessingDocumentInfo)infoDocx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Page count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```
## Step 5: Repeat for Different Document Types
Repeat the same steps for other document types like Spreadsheets and Textual documents.
```csharp
string xlsxInputFilePath = "YourSampleDocument.xlsx";
Editor editorXlsx = new Editor(xlsxInputFilePath);
IDocumentInfo infoXlsx = editorXlsx.GetDocumentInfo(null);
bool isXlsxSpreadsheet = infoXlsx is SpreadsheetDocumentInfo;
Console.WriteLine($"Is '{xlsxInputFilePath}' a Spreadsheet: {isXlsxSpreadsheet}");
if (isXlsxSpreadsheet)
{
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo)infoXlsx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Tabs count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```
## Step 6: Handle Password-Protected Documents
When dealing with password-protected documents, you should first try to open them without a password, then with an incorrect password, and finally with the correct password.
```csharp
string xlsInputFilePath = "YourSampleDocument.xls";
Editor editorXls = new Editor(xlsInputFilePath);
try
{
    IDocumentInfo infoXls = editorXls.GetDocumentInfo(null);
}
catch (PasswordRequiredException)
{
    Console.WriteLine("This document is password-protected.");
}
try
{
    IDocumentInfo infoXls = editorXls.GetDocumentInfo("incorrect_password");
}
catch (IncorrectPasswordException)
{
    Console.WriteLine("The provided password is incorrect.");
}
IDocumentInfo infoXlsValid = editorXls.GetDocumentInfo("correct_password");
bool isXlsSpreadsheet = infoXlsValid is SpreadsheetDocumentInfo;
Console.WriteLine($"Password-protected document is a Spreadsheet: {isXlsSpreadsheet}");
if (isXlsSpreadsheet)
{
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo)infoXlsValid;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Tabs count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```
## Step 7: Handle Text-Based Documents
```csharp
string xmlInputFilePath = "YourSampleDocument.xml";
Editor editorXml = new Editor(xmlInputFilePath);
IDocumentInfo infoXml = editorXml.GetDocumentInfo(null);
bool isXmlText = infoXml is TextualDocumentInfo;
Console.WriteLine($"Is '{xmlInputFilePath}' a Textual document: {isXmlText}");
if (isXmlText)
{
    TextualDocumentInfo casted = (TextualDocumentInfo)infoXml;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Encoding: {casted.Encoding}; Size: {casted.Size} bytes");
}
```
## Step 8: Dispose Resources
Finally, ensure you dispose of all resources to prevent memory leaks.
```csharp
editorDocx.Dispose();
editorXlsx.Dispose();
editorXls.Dispose();
editorXml.Dispose();
Console.WriteLine("ExtractingDocumentInfo routine has successfully finished");
```
## Conclusion
Congratulations! You've now learned how to extract document information using GroupDocs.Editor for .NET. This powerful library simplifies document management and manipulation, allowing you to handle various document types seamlessly. Whether you’re dealing with Word Processing, Spreadsheet, or Text-based documents, GroupDocs.Editor provides a robust solution.
## FAQ's
### What types of documents can GroupDocs.Editor handle?
GroupDocs.Editor can handle various document types including Word Processing, Spreadsheets, and Text-based documents.
### Can GroupDocs.Editor manage password-protected documents?
Yes, GroupDocs.Editor can manage password-protected documents. It can identify and open these documents given the correct password.
### Is it necessary to dispose of the Editor objects?
Yes, it’s crucial to dispose of Editor objects to free up resources and prevent memory leaks.
### Can I extract detailed information about the document format and size?
Absolutely! GroupDocs.Editor allows you to extract detailed information including format, extension, size, page count, and encryption status.
### Where can I get support if I encounter issues?
You can get support from the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).
