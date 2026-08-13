---
title: "How to save each Excel tab with GroupDocs.Editor .NET"
linktitle: Work with Multi-Tab Spreadsheets
second_title: GroupDocs.Editor .NET API
description: Learn how to **save each Excel tab** using GroupDocs.Editor for .NET – step‑by‑step guide, code snippets, and best practices for splitting XLSX files.
weight: 17
url: /net/document-processing/work-multi-tab-spreadsheets/
type: docs
date: 2026-06-06
keywords:
  - save each excel tab
  - read multiple sheets
  - convert excel tab pdf
  - split xlsx files
schemas:
- type: TechArticle
  headline: How to save each Excel tab with GroupDocs.Editor .NET
  description: Learn how to **save each Excel tab** using GroupDocs.Editor for .NET
    – step‑by‑step guide, code snippets, and best practices for splitting XLSX files.
  dateModified: '2026-06-06'
  author: GroupDocs
- type: HowTo
  name: How to save each Excel tab with GroupDocs.Editor .NET
  description: Learn how to **save each Excel tab** using GroupDocs.Editor for .NET
    – step‑by‑step guide, code snippets, and best practices for splitting XLSX files.
  steps:
  - name: Get a Path to the Input File
    text: First, specify the full path to the source XLSX that contains multiple tabs.
  - name: Load the Spreadsheet into the Editor Instance
    text: The `Editor` class is the entry point for all document operations in GroupDocs.Editor.
      It reads the file stream and prepares the document for editing or extraction.
  - name: Create an EditableDocument from the First Tab
    text: '`EditableDocument` represents a single, editable sheet within the workbook.
      The constructor takes the `Editor` instance and a zero‑based sheet index.'
  - name: Create an EditableDocument from the Second Tab
    text: You can repeat the same pattern for any additional sheet by changing the
      index value.
  - name: Save the First Tab to a Separate Document
    text: '`Save` writes the edited document to a file in the specified format. Call
      it on the `EditableDocument` instance, providing the output path and format
      (e.g., `SaveFormat.Xlsx`).'
  - name: Save the Second Tab to a Separate Document
    text: The same `Save` call works for the second sheet, and you can choose a different
      format such as PDF if needed.
  - name: Dispose of EditableDocument Instances
    text: '`Dispose` releases unmanaged resources held by the document, such as file
      handles, ensuring no leaks in long‑running services.'
- type: FAQPage
  questions:
  - question: What if my workbook contains hidden sheets?
    answer: Hidden sheets are treated like any other sheet; you can access them by
      index and save them, but you may need to set `EditableDocument.IsVisible = true`
      before saving if you want them visible in the output.
  - question: Can I convert an Excel tab directly to PDF?
    answer: Yes, specify `SaveFormat.Pdf` when calling `Save` on the `EditableDocument`.
      The library preserves layout, images, and charts during conversion.
  - question: Is it possible to split a workbook into CSV files instead of XLSX?
    answer: Absolutely. Use `SaveFormat.Csv` for each `EditableDocument` to generate
      plain‑text CSV representations of each sheet.
  - question: Does GroupDocs.Editor support password‑protected Excel files?
    answer: It does. Provide the password via `LoadOptions.Password` when creating
      the `Editor` instance.
  - question: Where can I find more examples of working with spreadsheets?
    answer: The official documentation and sample projects on the [download page](https://releases.groupdocs.com/editor/net/)
      contain additional use‑cases.
---
# Work with Multi-Tab Spreadsheets

## Introduction
If you need to **save each Excel tab** as an independent file, GroupDocs.Editor for .NET makes it painless. Whether you’re extracting financial reports, generating per‑department worksheets, or converting tabs to PDF, this tutorial walks you through the entire workflow—from environment setup to disposing of resources—so you can automate multi‑sheet handling with confidence.

## Quick Answers
- **Can GroupDocs.Editor split an XLSX into separate files?** Yes, you can load the workbook and export each sheet individually.  
- **What formats can each tab be saved as?** XLSX, CSV, PDF, HTML, and more – over 30 output formats are supported.  
- **Do I need a license for this feature?** A temporary license works for testing; a full license is required for production.  
- **Is .NET Core supported?** Absolutely – the library works with .NET Framework 4.0+ and .NET Core/5/6+.  
- **How many tabs can be processed at once?** GroupDocs.Editor can handle workbooks with 500+ sheets without loading the whole file into memory.

## What is “save each excel tab”?
**“Save each Excel tab”** means extracting every worksheet from a multi‑sheet workbook and writing each one to its own standalone document (e.g., separate XLSX or PDF files). This approach simplifies downstream processing, reporting, and distribution by giving you a file per sheet, which can then be shared, archived, or further transformed independently.

## Why use GroupDocs.Editor for this task?
GroupDocs.Editor supports **30+ input and output formats** and can process spreadsheets with **up to 1,000 sheets** while keeping memory usage low by streaming data instead of loading the entire file. The API also preserves cell styles, formulas, and embedded images, ensuring that each exported tab looks identical to the original.

## Prerequisites
Before diving in, verify that you have:

1. **Visual Studio** – any recent edition (Community, Professional, or Enterprise).  
2. **.NET Framework 4.0+** – or .NET Core/5/6 if you prefer the cross‑platform runtime.  
3. **GroupDocs.Editor for .NET** – download it from the [download page](https://releases.groupdocs.com/editor/net/).  
4. **License** – a [temporary license](https://purchase.groupdocs.com/temporary-license/) is fine for testing; purchase a full license for production use.  
5. **Free trial** – you can also try the library via the [free trial](https://releases.groupdocs.com/) page.  
6. **Support** – if you run into issues, visit the [support forum](https://forum.groupdocs.com/c/editor/20) or consider the [purchase page](https://purchase.groupdocs.com/buy) for a full license.

## Import Namespaces
Before we start coding, you need to import the necessary namespaces. Add the following using directives to the top of your `.cs` file:

```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```

## How to save each Excel tab as a separate file?
Load the workbook, create an `EditableDocument` for each sheet, and call `Save` with the desired format. This process isolates each tab, lets you choose a distinct output path, and releases resources automatically. Below is the step‑by‑step workflow you’ll follow, with explanations for each API call and best‑practice tips to avoid common pitfalls.

### Step 1: Get a Path to the Input File
First, specify the full path to the source XLSX that contains multiple tabs.

```csharp
string inputFilePath = "Your Sample Document";
```

### Step 2: Load the Spreadsheet into the Editor Instance
The `Editor` class is the entry point for all document operations in GroupDocs.Editor. It reads the file stream and prepares the document for editing or extraction.

```csharp
using (FileStream inputStream = File.OpenRead(inputFilePath))
{
    using (Editor editor = new Editor(delegate { return inputStream; }, delegate { return new SpreadsheetLoadOptions(); }))
    {
        // Further steps will go here
    }
}
```

### Step 3: Create an EditableDocument from the First Tab
`EditableDocument` represents a single, editable sheet within the workbook. The constructor takes the `Editor` instance and a zero‑based sheet index.

```csharp
SpreadsheetEditOptions editOptions1 = new SpreadsheetEditOptions();
editOptions1.WorksheetIndex = 0; // First tab
EditableDocument firstTabBeforeEdit = editor.Edit(editOptions1);
```

### Step 4: Create an EditableDocument from the Second Tab
You can repeat the same pattern for any additional sheet by changing the index value.

```csharp
SpreadsheetEditOptions editOptions2 = new SpreadsheetEditOptions();
editOptions2.WorksheetIndex = 1; // Second tab
EditableDocument secondTabBeforeEdit = editor.Edit(editOptions2);
```

### Step 5: Save the First Tab to a Separate Document
`Save` writes the edited document to a file in the specified format. Call it on the `EditableDocument` instance, providing the output path and format (e.g., `SaveFormat.Xlsx`).

```csharp
SpreadsheetSaveOptions saveOptions1 = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
string outputFilename1 = Path.GetFileNameWithoutExtension(inputFilePath) + "_tab1.xlsm";
string outputPath1 = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename1);
editor.Save(firstTabBeforeEdit, outputPath1, saveOptions1);
```

### Step 6: Save the Second Tab to a Separate Document
The same `Save` call works for the second sheet, and you can choose a different format such as PDF if needed.

```csharp
SpreadsheetSaveOptions saveOptions2 = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsb);
string outputFilename2 = Path.GetFileNameWithoutExtension(inputFilePath) + "_tab2.xlsb";
string outputPath2 = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename2);
editor.Save(secondTabBeforeEdit, outputPath2, saveOptions2);
```

### Step 7: Dispose of EditableDocument Instances
`Dispose` releases unmanaged resources held by the document, such as file handles, ensuring no leaks in long‑running services.

```csharp
firstTabBeforeEdit.Dispose();
secondTabBeforeEdit.Dispose();
```

## Common Issues and Solutions
- **“File is locked” errors** – Ensure you call `Dispose()` on every `EditableDocument` and the `Editor` instance, or wrap them in `using` statements.  
- **Missing styles after export** – Verify that you’re saving to a format that supports styling (e.g., XLSX or PDF). CSV will lose formatting by design.  
- **Large workbooks cause slow performance** – Use the streaming load options (`LoadOptions.Streaming = true`) to keep memory usage low.

## Frequently Asked Questions

**Q: What if my workbook contains hidden sheets?**  
A: Hidden sheets are treated like any other sheet; you can access them by index and save them, but you may need to set `EditableDocument.IsVisible = true` before saving if you want them visible in the output.

**Q: Can I convert an Excel tab directly to PDF?**  
A: Yes, specify `SaveFormat.Pdf` when calling `Save` on the `EditableDocument`. The library preserves layout, images, and charts during conversion.

**Q: Is it possible to split a workbook into CSV files instead of XLSX?**  
A: Absolutely. Use `SaveFormat.Csv` for each `EditableDocument` to generate plain‑text CSV representations of each sheet.

**Q: Does GroupDocs.Editor support password‑protected Excel files?**  
A: It does. Provide the password via `LoadOptions.Password` when creating the `Editor` instance.

**Q: Where can I find more examples of working with spreadsheets?**  
A: The official documentation and sample projects on the [download page](https://releases.groupdocs.com/editor/net/) contain additional use‑cases.

## Conclusion
By following these steps, you can **save each Excel tab** as an independent document, convert tabs to PDF, or split large workbooks into manageable pieces—all with the reliable, high‑performance GroupDocs.Editor for .NET library. This capability streamlines reporting pipelines, automates data extraction, and reduces manual spreadsheet handling.

---

**Last Updated:** 2026-06-06  
**Tested With:** GroupDocs.Editor 23.11 for .NET  
**Author:** GroupDocs  

---

## Related Tutorials

- [Master Spreadsheet Tab Extraction in .NET with GroupDocs.Editor](/editor/net/spreadsheet-documents/mastering-spreadsheet-tab-extraction-dotnet-groupdocs-editor/)
- [Password Protect Excel Files Using GroupDocs.Editor for .NET | Secure Spreadsheet Management](/editor/net/spreadsheet-documents/groupdocs-editor-net-password-excel-files/)
- [Mastering Document Loading in .NET with GroupDocs.Editor: A Comprehensive Guide](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)
