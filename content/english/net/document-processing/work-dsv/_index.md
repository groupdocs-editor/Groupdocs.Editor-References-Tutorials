---
title: Work with Delimited Separated Values (DSV) – create editable document
linktitle: Work with Delimited Separated Values (DSV) – create editable document
second_title: GroupDocs.Editor .NET API
description: Learn how to **create editable document** objects from CSV and TSV files using GroupDocs.Editor for .NET. This guide also shows how to **read delimited text C#** and **edit CSV .NET** efficiently in Visual Studio.
weight: 12
url: /net/document-processing/work-dsv/
type: docs
date: 2026-06-06
keywords:
- create editable document
- read delimited text c#
- edit csv .net
- parse delimited values c#
schemas:
- type: TechArticle
  headline: Work with Delimited Separated Values (DSV) – create editable document
  description: Learn how to **create editable document** objects from CSV and TSV
    files using GroupDocs.Editor for .NET. This guide also shows how to **read delimited
    text C#** and **edit CSV .NET** efficiently in Visual Studio.
  dateModified: '2026-06-06'
  author: GroupDocs
- type: FAQPage
  questions:
  - question: Can I use GroupDocs.Editor for .NET to edit large CSV files?
    answer: Yes, the API streams data and can handle files larger than 1 GB without
      loading the entire document into memory.
  - question: Does GroupDocs.Editor for .NET support other DSV formats besides CSV
      and TSV?
    answer: Absolutely – any single‑character delimiter (e.g., pipe `|`, semicolon
      `;`) is supported as long as you specify it in `DelimitedTextEditOptions`.
  - question: Is it possible to customize the encoding when saving DSV files?
    answer: Yes, you can set the `Encoding` property in `DelimitedTextSaveOptions`
      to UTF‑8, UTF‑16, ISO‑8859‑1, or any .NET `Encoding` you require.
  - question: Can I convert a CSV file to an Excel spreadsheet using GroupDocs.Editor
      for .NET?
    answer: Yes – after editing, simply use `SpreadsheetSaveOptions` to export the
      content as an `.xlsx` workbook.
  - question: Where can I find more documentation on GroupDocs.Editor for .NET?
    answer: Detailed API references and code samples are available **[here](https://tutorials.groupdocs.com/editor/net/)**.
---

# Work with Delimited Separated Values (DSV) – create editable document

If you’re a .NET developer who needs to **create editable document** objects from delimited separated values (DSV) such as CSV or TSV, you’ve come to the right place. In the first 100 words we’ll explain why GroupDocs.Editor for .NET is the most reliable way to **read delimited text C#**, edit it, and then save it back without losing formatting. You’ll walk away with a complete, copy‑and‑paste‑ready workflow that fits naturally into any Visual Studio solution.

## Quick Answers
- **Which library handles CSV editing best in .NET?** GroupDocs.Editor for .NET.
- **Can I edit large CSV files in Visual Studio?** Yes – the API streams data and avoids loading the whole file into memory.
- **Do I need a license for production use?** A commercial license is required; a free trial is available.
- **Which formats can I output after editing?** CSV, TSV, and Excel‑compatible spreadsheet formats.
- **Is the API compatible with .NET 6+?** Absolutely – it supports .NET Framework 4.5+, .NET Core 3.1+, .NET 5, and .NET 6.

## What is “create editable document” in the context of GroupDocs.Editor?
**Create editable document** means generating an `EditableDocument` instance that represents a mutable version of a source file (CSV, TSV, etc.) in memory. This object lets you read, modify, and re‑save the content using the same API. It provides methods to retrieve the document text, apply changes, and save it back in various formats, ensuring that column alignment and quoting are preserved.

## Why use GroupDocs.Editor for DSV handling?
GroupDocs.Editor processes **more than 50 input and output formats**, including CSV, TSV, and Excel‑compatible spreadsheets, while keeping memory usage under 10 MB for files up to 500 MB. It also preserves column alignment, quoting rules, and custom encodings automatically, which eliminates the need for manual parsing logic.

## Prerequisites
Before we dive in, make sure you have the following installed:

- **Visual Studio** (any recent edition) – you’ll develop and debug directly inside the IDE.
- **GroupDocs.Editor for .NET** – download the latest package **[here](https://releases.groupdocs.com/editor/net/)**.
- **Basic C# knowledge** – the tutorial assumes you can create a console or ASP.NET project and add NuGet packages.

## Import Namespaces
The `Editor`, `EditableDocument`, and option classes live in the `GroupDocs.Editor` namespace.  

The `DelimitedTextEditOptions` class is the entry point for defining the delimiter (comma, tab, etc.) and other parsing rules.

```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

## How to create editable document from a CSV file?
Load the source CSV with `Editor` and call the `Edit` method, passing a `DelimitedTextEditOptions` instance that specifies a comma delimiter. The method returns an `EditableDocument` that you can manipulate in memory. This two‑step pattern—load → edit—covers **read delimited text C#** scenarios and guarantees that the original file structure is retained.

## Step 1: Get a Path to the Input DSV File
First, you need to specify the absolute or relative path to the source DSV file. For demonstration we’ll use a simple CSV located in the project’s `Data` folder.

```csharp
string inputFilePath = "Your Sample Document";
```

## Step 2: Create an Editor Instance
`Editor` is the core class that orchestrates loading, editing, and saving. Instantiating it with a `FileInfo` object gives you full control over the file lifecycle.

```csharp
using (Editor editor = new Editor(inputFilePath))
{
```

## Step 3: Create DSV Edit Options
`DelimitedTextEditOptions` tells the editor how to interpret the file. You can set the delimiter, whether the first row contains headers, and the character encoding.

```csharp
    Options.DelimitedTextEditOptions editOptions = new DelimitedTextEditOptions(",");
    editOptions.ConvertDateTimeData = false;
    editOptions.ConvertNumericData = true;
    editOptions.TreatConsecutiveDelimitersAsOne = true;
```

## Step 4: Create EditableDocument Instance
`EditableDocument` represents a mutable in‑memory version of the source file. Calling `Editor.Edit` with the options returns an `EditableDocument`. This object holds the file’s text in a mutable string, ready for any **parse delimited values C#** operation you need.

```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```

## Step 5: Edit the Document Content
`GetDocumentText()` returns the current text of the editable document as a string. Retrieve the original text via `EditableDocument.GetDocumentText()`, perform your modifications (e.g., replace a column value), and store the result in a new string. This is where you **edit CSV .NET** without touching low‑level file streams.

```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("SsangYong", "Chevrolet").Replace("Kyron", "Camaro");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```

## Step 6: Create an EditableDocument with Updated Content
Wrap the modified string back into an `EditableDocument`. This step finalises the changes and prepares the object for saving in any supported format.

```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```

## Step 7: Create CSV Save Options
`DelimitedTextSaveOptions` specifies how to write the edited content back to a CSV file. When you’re ready to persist the changes, configure `DelimitedTextSaveOptions`. You can specify the same delimiter, a different one, or even change the line‑ending style.

```csharp
    Options.DelimitedTextSaveOptions csvSaveOptions = new DelimitedTextSaveOptions(",");
    csvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

## Step 8: Create TSV Save Options
If you need a tab‑separated version, simply switch the delimiter to `\t`. The same `EditableDocument` can be saved multiple times with different options.

```csharp
    Options.DelimitedTextSaveOptions tsvSaveOptions = new DelimitedTextSaveOptions("\t");
    tsvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

## Step 9: Create Spreadsheet Save Options
`SpreadsheetSaveOptions` configures export of the document to Excel‑compatible formats like .xlsx. GroupDocs.Editor also lets you export the edited data to an Excel‑compatible format (`.xlsx`). The `SpreadsheetSaveOptions` class handles column types, formulas, and cell styling automatically.

```csharp
    Options.SpreadsheetSaveOptions cellsSaveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
```

## Step 10: Prepare Save Paths
Define distinct output paths for each format. Using clear naming conventions (e.g., `output.csv`, `output.tsv`, `output.xlsx`) helps keep your project organized.

```csharp
    string outputCsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".csv");
    string outputTsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".tsv");
    string outputCellsPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".xlsm");
```

## Step 11: Save the Edited Document
`Save()` writes the document to disk using the provided save options. Invoke `EditableDocument.Save` with the appropriate options for each target format. The API writes the file directly to disk, preserving the original encoding unless you override it.

```csharp
    editor.Save(afterEdit, outputCsvPath, csvSaveOptions);
    editor.Save(afterEdit, outputTsvPath, tsvSaveOptions);
    editor.Save(afterEdit, outputCellsPath, cellsSaveOptions);
```

## Step 12: Dispose EditableDocument Instances
Both `Editor` and `EditableDocument` implement `IDisposable`. Disposing them releases file handles and unmanaged resources, which is crucial when processing many files in a batch job.

```csharp
    beforeEdit.Dispose();
    afterEdit.Dispose();
}
System.Console.WriteLine("WorkingWithDsv routine has successfully finished");
```

## Common Issues and Solutions
| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Unexpected extra quotes** | The default CSV parser may treat embedded commas as delimiters. | Set `EscapeMode = EscapeMode.DoubleQuote` in `DelimitedTextEditOptions`. |
| **Large file memory spike** | Loading a 500 MB file without streaming. | Use `Editor.Load` with `LoadOptions` that enable lazy loading. |
| **Encoding mismatch** | Source file uses UTF‑16 but options default to UTF‑8. | Explicitly set `Encoding = Encoding.Unicode` in save options. |

## Frequently Asked Questions

**Q: Can I use GroupDocs.Editor for .NET to edit large CSV files?**  
A: Yes, the API streams data and can handle files larger than 1 GB without loading the entire document into memory.

**Q: Does GroupDocs.Editor for .NET support other DSV formats besides CSV and TSV?**  
A: Absolutely – any single‑character delimiter (e.g., pipe `|`, semicolon `;`) is supported as long as you specify it in `DelimitedTextEditOptions`.

**Q: Is it possible to customize the encoding when saving DSV files?**  
A: Yes, you can set the `Encoding` property in `DelimitedTextSaveOptions` to UTF‑8, UTF‑16, ISO‑8859‑1, or any .NET `Encoding` you require.

**Q: Can I convert a CSV file to an Excel spreadsheet using GroupDocs.Editor for .NET?**  
A: Yes – after editing, simply use `SpreadsheetSaveOptions` to export the content as an `.xlsx` workbook.

**Q: Where can I find more documentation on GroupDocs.Editor for .NET?**  
A: Detailed API references and code samples are available **[here](https://tutorials.groupdocs.com/editor/net/)**.

---

**Last Updated:** 2026-06-06  
**Tested With:** GroupDocs.Editor 23.10 for .NET  
**Author:** GroupDocs

## Related Tutorials

- [Plain Text and DSV Document Editing Tutorials for GroupDocs.Editor .NET](/editor/net/plain-text-dsv-documents/)
- [Master GroupDocs.Editor .NET for Efficient CSV Document Editing and Conversion](/editor/net/plain-text-dsv-documents/groupdocs-editor-net-csv-editing-guide/)
- [Mastering Document Loading in .NET with GroupDocs.Editor: A Comprehensive Guide](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)
