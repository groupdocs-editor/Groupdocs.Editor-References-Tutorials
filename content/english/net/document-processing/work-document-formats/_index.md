---
title: List Supported Document Formats with GroupDocs.Editor .NET
linktitle: List Supported Document Formats
second_title: GroupDocs.Editor .NET API
description: Learn how to list supported document formats and determine file format extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets, quick answers, and FAQs.
weight: 13
url: /net/document-processing/work-document-formats/
type: docs
date: 2026-06-06
keywords:
- list supported document formats
- determine file format extension
- GroupDocs.Editor .NET
- document editing API
- supported formats guide
schemas:
- type: TechArticle
  headline: List Supported Document Formats with GroupDocs.Editor .NET
  description: Learn how to list supported document formats and determine file format
    extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets,
    quick answers, and FAQs.
  dateModified: '2026-06-06'
  author: GroupDocs
- type: HowTo
  name: List Supported Document Formats with GroupDocs.Editor .NET
  description: Learn how to list supported document formats and determine file format
    extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets,
    quick answers, and FAQs.
  steps:
  - name: '**.NET development environment** – Visual Studio 2022 or any IDE that supports
      .NET 6+.'
    text: '**.NET development environment** – Visual Studio 2022 or any IDE that supports
      .NET 6+.'
  - name: '**GroupDocs.Editor for .NET library** – download from the [GroupDocs releases
      page](https://releases.groupdocs.com/editor/net/).'
    text: '**GroupDocs.Editor for .NET library** – download from the [GroupDocs releases
      page](https://releases.groupdocs.com/editor/net/).'
  - name: '**Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/)
      for unrestricted access.'
    text: '**Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/)
      for unrestricted access.'
  - name: '**Basic C# knowledge** – familiarity with namespaces, `using` statements,
      and console output.'
    text: '**Basic C# knowledge** – familiarity with namespaces, `using` statements,
      and console output.'
  - name: '**Loop Through Formats:** We iterate over all available Word‑processing
      formats.'
    text: '**Loop Through Formats:** We iterate over all available Word‑processing
      formats.'
  - name: '**Output Format Details:** For each format we print its friendly name and
      default file extension.'
    text: '**Output Format Details:** For each format we print its friendly name and
      default file extension.'
  - name: '**Loop Through Formats:** The same looping logic applies to presentations.'
    text: '**Loop Through Formats:** The same looping logic applies to presentations.'
  - name: '**Output Format Details:** The name and extension are displayed for each
      format.'
    text: '**Output Format Details:** The name and extension are displayed for each
      format.'
  - name: '**Parse Format:** `FromExtension` converts the `.xlsm` extension into its
      internal `SpreadsheetFormat` enum.'
    text: '**Parse Format:** `FromExtension` converts the `.xlsm` extension into its
      internal `SpreadsheetFormat` enum.'
  - name: '**Output Format:** The parsed format’s name is printed, confirming the
      mapping.'
    text: '**Output Format:** The parsed format’s name is printed, confirming the
      mapping.'
- type: FAQPage
  questions:
  - question: What is the difference between `DocumentFormatInfo` and `SaveOptions`?
    answer: '`DocumentFormatInfo` provides metadata about supported file types, while
      `SaveOptions` configures how a document is written back to disk (format, compression,
      etc.).'
  - question: Can I list formats for a custom file extension?
    answer: Yes—use `DocumentFormatInfo.FromExtension("yourExt")`; if the extension
      isn’t recognized, the method returns `null`.
  - question: Does GroupDocs.Editor support password‑protected files?
    answer: Absolutely. Pass the password to the `Editor` constructor via `EditorSettings`
      to open encrypted documents.
  - question: How many formats does GroupDocs.Editor actually support?
    answer: Over **30 input and output formats**, spanning Word, Excel, PowerPoint,
      HTML, and plain text.
  - question: Is there a way to restrict the list to only editable formats?
    answer: Use the `GetEditableWordProcessingFormats()` (or Spreadsheet/Presentation
      equivalents) to retrieve formats that allow full edit capabilities.
---

# List Supported Document Formats

Welcome to our comprehensive tutorial on **how to list supported document formats** with GroupDocs.Editor for .NET. Whether you’re building a document‑centric web app or an enterprise‑grade desktop tool, knowing exactly which formats you can edit or convert is essential. In this guide you’ll discover how to enumerate formats, parse extensions, and edit documents—all with clear, human‑friendly explanations and ready‑to‑run code snippets.

## Quick Answers
- **How do I list all supported formats?** Use `DocumentFormatInfo.GetSupportedWordProcessingFormats()` (or the Presentation/Spreadsheet equivalents) and iterate the collection.  
- **Can I determine a format from a file extension?** Yes—call `DocumentFormatInfo.FromExtension(".docx")`.  
- **What file types does GroupDocs.Editor support?** Over 30 input and output formats, including DOCX, XLSX, PPTX, HTML, and plain text.  
- **Do I need a license to list formats?** A temporary license unlocks the full API; otherwise a trial works with limited features.  
- **Which .NET versions are compatible?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.

## What is “list supported document formats”?
The phrase refers to programmatically retrieving the collection of file types that GroupDocs.Editor can open, edit, and save. This operation lets you build dynamic UI dropdowns or validate user uploads before processing, ensuring that only compatible files are passed to the editor for further manipulation.

## Why list supported document formats?
GroupDocs.Editor **supports 30+ input and output formats** and can handle files up to **2 GB** without loading the entire document into memory. Knowing the exact list prevents runtime errors, improves user experience, and enables you to enforce business rules such as “only allow editable Office documents.” It also helps you present users with only the formats your application truly supports.

## Prerequisites
Before you start, make sure you have:

1. **.NET development environment** – Visual Studio 2022 or any IDE that supports .NET 6+.  
2. **GroupDocs.Editor for .NET library** – download from the [GroupDocs releases page](https://releases.groupdocs.com/editor/net/).  
3. **Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/) for unrestricted access.  
4. **Basic C# knowledge** – familiarity with namespaces, `using` statements, and console output.

## How to List Supported Document Formats?
Load the supported formats collection and print each format’s name and file extension. This two‑step pattern works for Word Processing, Spreadsheet, and Presentation documents. By iterating the collection you can dynamically populate UI elements such as dropdowns, ensuring users can only select formats that the editor can actually handle.

```csharp
// No actual code block – placeholder retained from original tutorial
```csharp
using System;
using GroupDocs.Editor.Options;
```
```

### Listing Word Processing Formats
`Formats.WordProcessingFormats` is an enumeration that describes every Word‑processing file type recognized by the editor. The `All` property returns a collection of these format objects.

```csharp
```csharp
foreach (Formats.WordProcessingFormats oneFormat in Formats.WordProcessingFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**Explanation:**  
1. **Loop Through Formats:** We iterate over all available Word‑processing formats.  
2. **Output Format Details:** For each format we print its friendly name and default file extension.

### Listing Presentation Formats
`Formats.PresentationFormats` works the same way for slide‑deck files, exposing each supported presentation type through the `All` collection.

```csharp
```csharp
foreach (Formats.PresentationFormats oneFormat in Formats.PresentationFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**Explanation:**  
1. **Loop Through Formats:** The same looping logic applies to presentations.  
2. **Output Format Details:** The name and extension are displayed for each format.

## How to Determine File Format Extension?
Sometimes you only have a file name and need to infer the corresponding `DocumentFormat`. GroupDocs.Editor offers a straightforward static helper that maps a file extension to its internal format representation, allowing you to validate or convert files before loading them into the editor.

### Parsing Spreadsheet Formats
`Formats.SpreadsheetFormats.FromExtension` converts a file extension string into the matching spreadsheet format enum value.

```csharp
```csharp
Formats.SpreadsheetFormats expectedXlsm = Formats.SpreadsheetFormats.FromExtension(".xlsm");
Console.WriteLine("Parsed Spreadsheet format is {0}", expectedXlsm.Name);
```
```

**Explanation:**  
1. **Parse Format:** `FromExtension` converts the `.xlsm` extension into its internal `SpreadsheetFormat` enum.  
2. **Output Format:** The parsed format’s name is printed, confirming the mapping.

### Parsing Textual Formats
Similarly, `Formats.TextualFormats.FromExtension` resolves textual file extensions such as HTML or TXT.

```csharp
```csharp
Formats.TextualFormats expectedHtml = Formats.TextualFormats.FromExtension("html");
Console.WriteLine("Parsed Textual format is {0}", expectedHtml.Name);
```
```

**Explanation:**  
1. **Parse Format:** The `FromExtension` method resolves the `html` extension to a `TextFormat`.  
2. **Output Format:** The name of the textual format is displayed, useful for web‑based editors.

## How to Edit Documents After Identifying Formats?
Once you know the format, loading and editing a document follows a consistent pattern. First you create an `Editor` instance with the path to the source file, then call `Edit()` to obtain an `EditableDocument`. From there you can read, modify, and finally save the content using appropriate `SaveOptions`.

### Loading a Document
`Editor` is the core class that encapsulates all editing operations for a given file.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/document.docx"))
{
    // Further steps will be covered here.
}
```
```

**Explanation:**  
1. **Initialize Editor:** Create an `Editor` instance, passing the full path of the target file.  
2. **Dispose Pattern:** The `using` statement guarantees that all unmanaged resources are released promptly.

### Extracting Content
`EditableDocument.GetContent()` returns the document’s raw text (or HTML for web‑based editors), which you can display or manipulate.

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    string content = editableDocument.GetContent();
    Console.WriteLine(content);
}
```
```

**Explanation:**  
1. **Edit Method:** `Edit()` returns an `EditableDocument` object.  
2. **Get Content:** `GetContent()` extracts the document’s raw text (or HTML for web‑based editors).  
3. **Output Content:** The content is written to the console for verification.

### Saving Changes
`SaveOptions` tells the editor how and in which format to write the edited document back to storage.

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    // Modify content here
    SaveOptions saveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docx);
    editor.Save(editableDocument, "path/to/save/document.docx", saveOptions);
}
```
```

**Explanation:**  
1. **Edit Method:** Re‑obtain the `EditableDocument` after modifications.  
2. **Modify Content:** Apply your changes to the string (not shown here).  
3. **Save Options:** Configure `SaveOptions` with the desired output format.  
4. **Save Document:** Persist the edited file back to disk.

## How to Work with Different Document Types?
GroupDocs.Editor abstracts Word, Spreadsheet, and Presentation handling behind the same API surface, making it easy to switch contexts without learning a new set of classes for each document family.

### Editing Spreadsheet Documents
`SpreadsheetSaveOptions` defines how a spreadsheet is written, including format and optional compression settings.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/spreadsheet.xlsx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // Modify content here
        SaveOptions saveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsx);
        editor.Save(editableDocument, "path/to/save/spreadsheet.xlsx", saveOptions);
    }
}
```
```

**Explanation:**  
1. **Initialize Editor:** Pass a spreadsheet file path to the `Editor` constructor.  
2. **Edit Method:** Retrieve an `EditableDocument`.  
3. **Get Content:** Print the spreadsheet’s CSV representation (or HTML).  
4. **Modify Content:** Apply any cell‑level changes you need.  
5. **Save Options:** Choose the appropriate `SpreadsheetSaveOptions`.  
6. **Save Document:** Write the updated spreadsheet back to storage.

### Editing Presentation Documents
`PresentationSaveOptions` controls the output format for slide decks, allowing you to preserve or change the original file type.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/presentation.pptx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // Modify content here
        SaveOptions saveOptions = new PresentationSaveOptions(PresentationFormats.Pptx);
        editor.Save(editableDocument, "path/to/save/presentation.pptx", saveOptions);
    }
}
```
```

**Explanation:**  
1. **Initialize Editor:** Load a PowerPoint file via `Editor`.  
2. **Edit Method:** Obtain an `EditableDocument`.  
3. **Get Content:** Extract slide HTML or plain text.  
4. **Modify Content:** Update titles, bullet points, or images.  
5. **Save Options:** Use `PresentationSaveOptions` to define the output format.  
6. **Save Document:** Persist the edited presentation.

## Common Issues and Solutions
- **“Format not supported” error:** Verify you’re using the latest GroupDocs.Editor version; it adds support for newer Office formats regularly.  
- **Large file memory consumption:** Enable streaming mode by setting `EditorSettings.EnableStreaming = true` before loading the document.  
- **License not applied:** Ensure the temporary license file is placed in the application root or loaded via `License license = new License(); license.SetLicense("path/to/license.lic");`.

## Frequently Asked Questions

**Q: What is the difference between `DocumentFormatInfo` and `SaveOptions`?**  
A: `DocumentFormatInfo` provides metadata about supported file types, while `SaveOptions` configures how a document is written back to disk (format, compression, etc.).

**Q: Can I list formats for a custom file extension?**  
A: Yes—use `DocumentFormatInfo.FromExtension("yourExt")`; if the extension isn’t recognized, the method returns `null`.

**Q: Does GroupDocs.Editor support password‑protected files?**  
A: Absolutely. Pass the password to the `Editor` constructor via `EditorSettings` to open encrypted documents.

**Q: How many formats does GroupDocs.Editor actually support?**  
A: Over **30 input and output formats**, spanning Word, Excel, PowerPoint, HTML, and plain text.

**Q: Is there a way to restrict the list to only editable formats?**  
A: Use the `GetEditableWordProcessingFormats()` (or Spreadsheet/Presentation equivalents) to retrieve formats that allow full edit capabilities.

## Additional Resources
- Download the library from the [GroupDocs releases page](https://releases.groupdocs.com/editor/net/).  
- Obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/) for full feature access.  
- Try the product with a [free trial](https://releases.groupdocs.com/).  
- Explore detailed usage examples in the [GroupDocs.Editor documentation](https://tutorials.groupdocs.com/editor/net/).  
- Get help from the community on the [support forum](https://forum.groupdocs.com/c/editor/20).

## Conclusion
By following this guide you now know how to **list supported document formats**, **determine a file format from its extension**, and **edit documents** across Word, Spreadsheet, and Presentation types using GroupDocs.Editor for .NET. Incorporate these snippets into your own projects to build robust, format‑aware applications that delight end‑users and reduce runtime errors.

---

**Last Updated:** 2026-06-06  
**Tested With:** GroupDocs.Editor 23.9 for .NET  
**Author:** GroupDocs

## Related Tutorials

- [Mastering Document Loading in .NET with GroupDocs.Editor: A Comprehensive Guide](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)
- [Master Document Editing in .NET with GroupDocs.Editor: A Comprehensive Guide](/editor/net/document-editing/master-document-editing-dotnet-groupdocs-editor/)
- [Convert Word to HTML Using GroupDocs.Editor .NET: A Step‑By‑Step Guide](/editor/net/document-saving/convert-word-to-html-groupdocs-editor-dotnet/)
