---
title: Get Page Count & Extract Document Info with GroupDocs.Editor
linktitle: Get Page Count & Extract Document Info
second_title: GroupDocs.Editor .NET API
description: Learn how to get page count and extract document metadata using GroupDocs.Editor for .NET in a detailed step‑by‑step tutorial.
weight: 10
url: /net/document-processing/extract-document-info/
type: docs
date: 2026-06-01
keywords:
  - get page count
  - extract document metadata
  - get document info
  - find document extension
  - retrieve document size
schemas:
- type: TechArticle
  headline: Get Page Count & Extract Document Info with GroupDocs.Editor
  description: Learn how to get page count and extract document metadata using GroupDocs.Editor
    for .NET in a detailed step‑by‑step tutorial.
  dateModified: '2026-06-01'
  author: GroupDocs
- type: FAQPage
  questions:
  - question: What document types can I extract metadata from?
    answer: GroupDocs.Editor supports Word processing, spreadsheet, presentation,
      PDF, and plain‑text files—over 50 formats in total.
  - question: How do I retrieve the file extension?
    answer: Access `DocumentInfo.Extension` after calling `GetDocumentInfo()`; it
      returns the extension without the leading dot.
  - question: Can I get the size of a document in megabytes?
    answer: Yes—`DocumentInfo.Size` returns the size in bytes; divide by 1,048,576
      to convert to megabytes.
  - question: Is it safe to process password‑protected files on a server?
    answer: Absolutely—GroupDocs.Editor never writes the password to disk and disposes
      of all cryptographic objects after use.
  - question: Where can I find additional help if I run into issues?
    answer: You can get support from the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).
---
# Get Page Count & Extract Document Info with GroupDocs.Editor

## Introduction
In this comprehensive tutorial you’ll learn how to **get page count** and extract detailed document information—including format, size, and encryption status—using GroupDocs.Editor for .NET. Whether you’re building a document‑management system, a reporting engine, or an automated conversion pipeline, understanding a file’s metadata is the first step toward reliable processing. Let’s walk through the entire workflow, from loading a file to safely disposing of resources.

## Quick Answers
- **How do I retrieve the page count of a document?**  
  Call `editor.GetDocumentInfo().PageCount` after loading the file with `Editor`.
- **Which file formats are supported for metadata extraction?**  
  Over 50 formats, including DOCX, XLSX, PPTX, PDF, TXT, and HTML.
- **Can I extract metadata from password‑protected files?**  
  Yes—provide the password when constructing the `Editor` instance.
- **Do I need to manually release resources?**  
  Absolutely; always call `editor.Dispose()` or wrap the editor in a `using` block.
- **What version of GroupDocs.Editor is required?**  
  The latest stable release (v23.12+ at the time of writing) supports all features shown.

## What is “get page count” in GroupDocs.Editor?
`GetDocumentInfo()` is a method that returns a `DocumentInfo` object containing the document’s page count, format, size, and other metadata. This single call gives you immediate insight without parsing the file manually. By using this method you avoid loading the entire document into memory, which improves performance especially for large files and reduces server resource consumption.

## Why extract document metadata with GroupDocs.Editor?
GroupDocs.Editor can process **50+ input and output formats** and retrieve metadata for files up to **2 GB** without loading the entire document into memory. This efficiency reduces server load by up to **70 %** compared to full‑document parsing, making it ideal for high‑throughput applications.

## Prerequisites
Before you start, make sure you have:

- **C# development basics** – you should be comfortable with Visual Studio and .NET project structures.
- **Visual Studio 2022** (or any recent version) installed on your machine.
- **GroupDocs.Editor for .NET** – download the latest package from the [download page](https://releases.groupdocs.com/editor/net/).

## How to Load Your Document?
`Editor` is the main class that represents a document and provides methods for loading and manipulating it. Load the target file by creating an `Editor` instance and passing the file path. The editor automatically detects the format, so you don’t need to specify load options. This approach works for any supported file type and simplifies the initial setup.

```csharp
using System;
using GroupDocs.Editor.Metadata;
```

## How to Retrieve Document Information?
`GetDocumentInfo()` returns a `DocumentInfo` object containing metadata such as page count, format, size, and encryption status. After loading, call this method to fetch the object. The returned `DocumentInfo` gives you a concise snapshot of the file’s characteristics, enabling you to make decisions without further processing.

```csharp
string docxInputFilePath = "YourSampleDocument.docx";
Editor editorDocx = new Editor(docxInputFilePath);
```

## How to Determine Document Type?
`DocumentType` is an enum indicating whether the document is WordProcessing, Spreadsheet, or Text. Knowing whether a file is a Word processing document, spreadsheet, or plain text influences how you handle it later. Use the `DocumentType` property of the `DocumentInfo` object to make this decision and branch your logic accordingly.

```csharp
IDocumentInfo infoDocx = editorDocx.GetDocumentInfo(null);
```

## How to Extract Detailed Information for Word Processing Files?
`WordProcessing` refers to documents like DOCX, ODT, and RTF handled as word processing files. If the document type is `WordProcessing`, you can read additional properties like **format**, **extension**, **page count**, **size**, and **encryption flag** directly from the `DocumentInfo` object. These details help you tailor processing steps, such as applying specific conversions or security checks.

```csharp
bool isSpreadsheet = infoDocx is SpreadsheetDocumentInfo;
bool isText = infoDocx is TextualDocumentInfo;
bool isWordProcessing = infoDocx is WordProcessingDocumentInfo;
Console.WriteLine($"Is '{docxInputFilePath}' a Spreadsheet: {isSpreadsheet}");
Console.WriteLine($"Is '{docxInputFilePath}' a Textual document: {isText}");
Console.WriteLine($"Is '{docxInputFilePath}' a WordProcessing document: {isWordProcessing}");
```

## How to Handle Spreadsheet and Textual Documents?
`Spreadsheet` denotes spreadsheet files such as XLSX, while `Text` represents plain‑text documents. For spreadsheets (`Spreadsheet`) and plain‑text files (`Text`), the `DocumentInfo` object still supplies core metadata (extension, size, page count). Some formats may not expose a page count, in which case the value will be `0`. You can still rely on other metadata for downstream logic.

```csharp
if (isWordProcessing)
{
    WordProcessingDocumentInfo casted = (WordProcessingDocumentInfo)infoDocx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Page count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```

## How to Work with Password‑Protected Documents?
`Password` is a string passed to the `Editor` constructor to open encrypted files. When a document is encrypted, first attempt to open it without a password. If that fails, catch the exception, then retry with the correct password. The `Editor` constructor accepts a `Password` parameter for this purpose, allowing seamless handling of protected files.

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

## How to Process Text‑Based Documents?
`DocumentInfo` provides basic metadata like size, extension, and encoding for text files. Text files (e.g., `.txt`, `.md`) are treated as simple streams. You can still retrieve size and encoding information from `DocumentInfo`, which is useful for validating file integrity or determining appropriate processing pipelines.

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

## How to Dispose Resources Properly?
`Editor` is the primary class that holds unmanaged resources and must be disposed after use. To avoid memory leaks, always dispose of the `Editor` instance after you finish extracting information. The `using` statement is the safest pattern because it guarantees disposal even if an exception occurs, ensuring clean resource management.

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

## Common Issues and Solutions
| Issue | Cause | Solution |
|-------|-------|----------|
| **PageCount returns 0** | Format does not support pagination (e.g., plain text) | Check `DocumentInfo.DocumentType` before relying on `PageCount`. |
| **Unsupported file format** | File extension not recognized | Verify the file is one of the 50+ supported formats; update GroupDocs.Editor to the latest version. |
| **Password exception** | Wrong password supplied | Catch `PasswordProtectedException` and prompt the user to re‑enter the password. |
| **Memory spike on large files** | Loading very large PDFs without streaming | Use `LoadOptions` with `LoadOptions.LoadMode = LoadMode.Stream` (available in newer releases). |

## Frequently Asked Questions

**Q: What document types can I extract metadata from?**  
A: GroupDocs.Editor supports Word processing, spreadsheet, presentation, PDF, and plain‑text files—over 50 formats in total.

**Q: How do I retrieve the file extension?**  
A: Access `DocumentInfo.Extension` after calling `GetDocumentInfo()`; it returns the extension without the leading dot.

**Q: Can I get the size of a document in megabytes?**  
A: Yes—`DocumentInfo.Size` returns the size in bytes; divide by 1,048,576 to convert to megabytes.

**Q: Is it safe to process password‑protected files on a server?**  
A: Absolutely—GroupDocs.Editor never writes the password to disk and disposes of all cryptographic objects after use.

**Q: Where can I find additional help if I run into issues?**  
A: You can get support from the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).

---

**Last Updated:** 2026-06-01  
**Tested With:** GroupDocs.Editor 23.12 for .NET  
**Author:** GroupDocs

```csharp
editorDocx.Dispose();
editorXlsx.Dispose();
editorXls.Dispose();
editorXml.Dispose();
Console.WriteLine("ExtractingDocumentInfo routine has successfully finished");
```

## Related Tutorials

- [Master Metadata Extraction in .NET with GroupDocs.Editor: A Comprehensive Guide](/editor/net/advanced-features/groupdocs-editor-net-metadata-extraction-guide/)
- [Document Loading Tutorials with GroupDocs.Editor for .NET](/editor/net/document-loading/)
- [Efficient Document Editing with GroupDocs.Editor .NET: Transform HTML to Editable Documents](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)
