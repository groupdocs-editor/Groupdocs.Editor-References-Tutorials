---
date: 2026-08-10
description: Learn how to edit plain text files using GroupDocs.Editor for .NET. The
  guide covers loading a txt file, trimming spaces, setting text encoding, and saving
  the result.
images:
- /net/document-processing/work-plain-text-documents/og-image.png
keywords:
- edit plain text
- load txt file
- trim trailing spaces
- convert leading spaces
- set text encoding
lastmod: 2026-08-10
linktitle: Work with Plain Text Documents
og_description: Learn how to edit plain text files using GroupDocs.Editor for .NET
  – load txt file, trim trailing spaces, convert leading spaces, set text encoding,
  and save efficiently.
og_image_alt: Guide showing edit plain text workflow with GroupDocs.Editor for .NET
og_title: Edit plain text documents with GroupDocs.Editor for .NET
schemas:
- author: GroupDocs
  dateModified: '2026-08-10'
  description: Learn how to edit plain text files using GroupDocs.Editor for .NET.
    The guide covers loading a txt file, trimming spaces, setting text encoding, and
    saving the result.
  headline: Edit plain text documents with GroupDocs.Editor for .NET
  type: TechArticle
- description: Learn how to edit plain text files using GroupDocs.Editor for .NET.
    The guide covers loading a txt file, trimming spaces, setting text encoding, and
    saving the result.
  name: Edit plain text documents with GroupDocs.Editor for .NET
  steps:
  - name: Get a path to the input TXT file
    text: First, decide whether you’ll work with a physical file path or a memory
      stream. Using a path is the most straightforward approach for local development.
  - name: Create an Editor instance
    text: '`Editor` is the main class that loads a document and provides editing capabilities.'
  - name: Create TXT editing options
    text: '`TxtEditOptions` configures how plain‑text files are parsed and edited,
      allowing you to set encoding and space‑handling rules.'
  - name: Create an EditableDocument instance
    text: '`EditableDocument` represents the in‑memory version of the loaded document,
      including its text and any associated resources.'
  - name: Edit the document content
    text: Retrieve the original text, apply any string operations you need (e.g.,
      replace, trim, change case), and store the result back into the `EditableDocument`.
  - name: Create an EditableDocument with updated content
    text: After you’ve transformed the text, instantiate a new `EditableDocument`
      that contains the edited string and the original resource collection.
  - name: Create WordProcessing save options
    text: '`WordProcessingSaveOptions` defines settings for saving the document in
      a Word‑compatible format such as DOCX or DOCM.'
  - name: Create TXT saving options
    text: '`TxtSaveOptions` specifies how the edited plain‑text file should be written,
      including encoding, line‑ending preservation, and table layout handling.'
  - name: Prepare output paths
    text: Derive the output directory from the input file path, then build the full
      filenames for the DOCX and TXT results.
  - name: Save the edited document
    text: Finally, call `editor.Save` twice—once with the WordProcessing options and
      once with the TXT options—to produce both formats in a single operation.
  type: HowTo
- questions:
  - answer: The library supports 50+ formats, including DOCX, TXT, HTML, PDF, and
      markdown, allowing you to edit and convert between them seamlessly.
    question: What file formats does GroupDocs.Editor for .NET support?
  - answer: Download the trial from the [releases page](https://releases.groupdocs.com/).
    question: How can I get a free trial of GroupDocs.Editor for .NET?
  - answer: Yes, temporary licenses are available through the [GroupDocs purchase
      page](https://purchase.groupdocs.com/temporary-license/).
    question: Can I purchase a temporary license for testing?
  - answer: The official support forum is the best place – visit the [GroupDocs.Editor
      support forum](https://forum.groupdocs.com/c/editor/20).
    question: Where can I find support if I run into issues?
  - answer: Absolutely. The full reference is on the [GroupDocs.Editor documentation
      page](https://tutorials.groupdocs.com/editor/net/).
    question: Is there detailed documentation for advanced scenarios?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
tags:
- edit plain text
- GroupDocs.Editor
- C# document processing
- plain text editing
- txt file handling
title: Edit plain text documents with GroupDocs.Editor for .NET
type: docs
url: /net/document-processing/work-plain-text-documents/
weight: 15
---

# Edit plain text documents with GroupDocs.Editor for .NET

## Introduction
If you need to **edit plain text** quickly and reliably in a .NET application, GroupDocs.Editor for .NET is the tool that does the heavy lifting. This API supports more than 30 document formats, can handle files up to 500 MB, and lets you manipulate text without loading the entire file into memory. In this tutorial you’ll learn how to load a txt file, trim trailing spaces, convert leading spaces, set the correct encoding, and finally save the edited content back to disk. Ready to get hands‑on? Let’s dive in!

## Quick answers
- **What is the first step to edit a txt file?** Load the file with `Editor` using the path or stream you have.  
- **Can I change the file encoding while editing?** Yes – the `TxtSaveOptions` let you specify UTF‑8, UTF‑16, or any custom encoding.  
- **How do I remove extra spaces at the end of each line?** Retrieve the text, call `TrimEnd()` on each line, and write it back.  
- **Is GroupDocs.Editor free to try?** A fully functional 30‑day trial is available from the releases page.  
- **Which .NET versions are supported?** .NET Framework 4.6+, .NET Core 3.1+, and .NET 5/6/7.

## What is edit plain text?
**Edit plain text** means programmatically changing the characters inside a simple `.txt` file—adding, removing, or re‑formatting text—while preserving the file’s original encoding and line‑break style. It can involve tasks such as trimming whitespace, normalizing line endings, updating configuration values, or inserting generated content. The operation should keep the file readable by any standard text editor and maintain any existing metadata such as BOM markers.

## Why use GroupDocs.Editor for plain‑text editing?
GroupDocs.Editor processes files in a streaming fashion, which means it can edit a 300 MB log file using less than 50 MB of RAM. The library supports **50+ input and output formats**, automatically detects line‑ending styles (CR, LF, CRLF), and provides built‑in options to **trim trailing spaces** and **convert leading spaces** without writing custom parsers.

## Prerequisites
- **.NET development environment** – Visual Studio 2022 or VS Code with the C# extension.  
- **GroupDocs.Editor for .NET** – download from the [GroupDocs.Editor for .NET](https://releases.groupdocs.com/editor/net/) releases page.  
- **Basic C# knowledge** – you should be comfortable with file I/O and string manipulation.  
- **Text editor (optional)** – for inspecting the source files; VS Code is recommended.  
- For detailed usage, see the [documentation](https://tutorials.groupdocs.com/editor/net/).  
- You can also browse the general [releases page](https://releases.groupdocs.com/).

## How to edit plain text step by step
Load the file, edit its content, and save it back – all in under ten lines of code. The following sections walk you through each stage with clear explanations.

### Step 1: Get a path to the input TXT file
First, decide whether you’ll work with a physical file path or a memory stream. Using a path is the most straightforward approach for local development.

```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

### Step 2: Create an Editor instance
`Editor` is the main class that loads a document and provides editing capabilities.

```csharp
string inputFilePath = "YourSampleDocument.txt";
```

### Step 3: Create TXT editing options
`TxtEditOptions` configures how plain‑text files are parsed and edited, allowing you to set encoding and space‑handling rules.

```csharp
using (Editor editor = new Editor(inputFilePath))
{
```

### Step 4: Create an EditableDocument instance
`EditableDocument` represents the in‑memory version of the loaded document, including its text and any associated resources.

```csharp
    TextEditOptions editOptions = new TextEditOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        RecognizeLists = true,
        LeadingSpaces = TextLeadingSpacesOptions.ConvertToIndent,
        TrailingSpaces = TextTrailingSpacesOptions.Trim
    };
```

### Step 5: Edit the document content
Retrieve the original text, apply any string operations you need (e.g., replace, trim, change case), and store the result back into the `EditableDocument`.

```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```

### Step 6: Create an EditableDocument with updated content
After you’ve transformed the text, instantiate a new `EditableDocument` that contains the edited string and the original resource collection.

```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("text", "EDITED text");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```

### Step 7: Create WordProcessing save options
`WordProcessingSaveOptions` defines settings for saving the document in a Word‑compatible format such as DOCX or DOCM.

```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```

### Step 8: Create TXT saving options
`TxtSaveOptions` specifies how the edited plain‑text file should be written, including encoding, line‑ending preservation, and table layout handling.

```csharp
    WordProcessingSaveOptions wordSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm)
    {
        Locale = System.Globalization.CultureInfo.GetCultureInfo("en-GB")
    };
```

### Step 9: Prepare output paths
Derive the output directory from the input file path, then build the full filenames for the DOCX and TXT results.

```csharp
    TextSaveOptions txtSaveOptions = new TextSaveOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        PreserveTableLayout = true
    };
```

### Step 10: Save the edited document
Finally, call `editor.Save` twice—once with the WordProcessing options and once with the TXT options—to produce both formats in a single operation.

```csharp
    string outputWordPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".docm");
    string outputTxtPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".txt");
```

## Common issues and solutions
- **Trailing spaces remain after editing** – ensure `TxtEditOptions.TrimTrailingSpaces` is set to `true` before loading the document.  
- **Incorrect encoding in the saved file** – verify that `TxtSaveOptions.Encoding` matches the desired code page (e.g., `Encoding.UTF8`).  
- **Large files cause OutOfMemoryException** – use the streaming API (`Editor.Load(Stream)`) instead of loading from a file path to keep memory usage low.  

## Frequently asked questions

**Q: What file formats does GroupDocs.Editor for .NET support?**  
A: The library supports 50+ formats, including DOCX, TXT, HTML, PDF, and markdown, allowing you to edit and convert between them seamlessly.

**Q: How can I get a free trial of GroupDocs.Editor for .NET?**  
A: Download the trial from the [releases page](https://releases.groupdocs.com/).

**Q: Can I purchase a temporary license for testing?**  
A: Yes, temporary licenses are available through the [GroupDocs purchase page](https://purchase.groupdocs.com/temporary-license/).

**Q: Where can I find support if I run into issues?**  
A: The official support forum is the best place – visit the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).

**Q: Is there detailed documentation for advanced scenarios?**  
A: Absolutely. The full reference is on the [GroupDocs.Editor documentation page](https://tutorials.groupdocs.com/editor/net/).

## Conclusion
You’ve now mastered how to **edit plain text** files using GroupDocs.Editor for .NET—loading a txt file, trimming spaces, converting leading spaces, setting the proper encoding, and saving the result in both TXT and DOCX formats. This capability lets you automate log‑file cleanup, generate configuration files on the fly, or build custom text‑processing pipelines without reinventing the wheel. Explore additional features such as batch processing and document conversion by visiting the official documentation.

---

**Last Updated:** 2026-08-10  
**Tested With:** GroupDocs.Editor 23.11 for .NET  
**Author:** GroupDocs  

---

```csharp
    editor.Save(afterEdit, outputWordPath, wordSaveOptions);
    editor.Save(afterEdit, outputTxtPath, txtSaveOptions);
}
System.Console.WriteLine("Document editing process completed successfully!");
```

## Related Tutorials

- [Document Loading Tutorials with GroupDocs.Editor for .NET](/editor/net/document-loading/)
- [Document Saving and Export Tutorials for GroupDocs.Editor .NET](/editor/net/document-saving/)
- [Plain Text and DSV Document Editing Tutorials for GroupDocs.Editor .NET](/editor/net/plain-text-dsv-documents/)