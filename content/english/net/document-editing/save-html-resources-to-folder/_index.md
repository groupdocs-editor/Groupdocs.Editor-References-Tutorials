---
title: How to Extract Fonts and Save HTML Resources to Folder
linktitle: Save HTML Resources to Folder
second_title: GroupDocs.Editor .NET API
description: Learn how to extract fonts and other HTML resources from documents using GroupDocs.Editor for .NET. Step‑by‑step guide for .NET developers.
weight: 13
url: /net/document-editing/save-html-resources-to-folder/
type: docs
date: 2026-05-12
keywords:
- how to extract fonts
- GroupDocs.Editor .NET
- extract HTML resources
schemas:
- type: TechArticle
  headline: How to Extract Fonts and Save HTML Resources to Folder
  description: Learn how to extract fonts and other HTML resources from documents
    using GroupDocs.Editor for .NET. Step‑by‑step guide for .NET developers.
  dateModified: '2026-05-12'
  author: GroupDocs
- type: HowTo
  name: How to Extract Fonts and Save HTML Resources to Folder
  description: Learn how to extract fonts and other HTML resources from documents
    using GroupDocs.Editor for .NET. Step‑by‑step guide for .NET developers.
  steps:
  - name: '**Basic Knowledge of C# and .NET** – Familiarity with C# programming language
      and .NET framework is essential to follow along with the examples.'
    text: '**Basic Knowledge of C# and .NET** – Familiarity with C# programming language
      and .NET framework is essential to follow along with the examples.'
  - name: '**GroupDocs.Editor for .NET Library** – Download and install GroupDocs.Editor
      for .NET library from the [website](https://releases.groupdocs.com/editor/net/).'
    text: '**GroupDocs.Editor for .NET Library** – Download and install GroupDocs.Editor
      for .NET library from the [website](https://releases.groupdocs.com/editor/net/).'
  - name: '**Development Environment** – Set up your preferred development environment
      such as Visual Studio or any other compatible IDE.'
    text: '**Development Environment** – Set up your preferred development environment
      such as Visual Studio or any other compatible IDE.'
- type: FAQPage
  questions:
  - question: Is GroupDocs.Editor compatible with other document formats besides Word?
    answer: Yes, it supports Excel, PowerPoint, PDF, HTML, and over 50 additional
      formats for both editing and resource extraction.
  - question: Can I integrate GroupDocs.Editor into a web application?
    answer: Absolutely. The API works seamlessly with ASP.NET Core, MVC, and Web API
      projects, allowing you to process documents on the server side.
  - question: Does GroupDocs.Editor provide cloud storage integration?
    answer: Yes, it includes built‑in connectors for Google Drive, Dropbox, OneDrive,
      and Amazon S3, enabling direct loading and saving of documents in the cloud.
  - question: Is there a free trial available for GroupDocs.Editor?
    answer: A fully functional 30‑day trial can be downloaded from the GroupDocs website
      without any credit‑card requirement.
  - question: How can I get technical support for extraction issues?
    answer: You can reach the GroupDocs support team via the official forum, submit
      a ticket through the customer portal, or consult the detailed API documentation.
---

# How to Extract Fonts and Save HTML Resources to Folder

## Introduction
GroupDocs.Editor for .NET lets you **how to extract fonts** and other assets from a document while converting it to HTML. In a few lines of C# you can pull out images, stylesheets, and font files, then store them in a folder of your choice. This tutorial walks you through the entire workflow, from initializing the editor to saving each resource on disk.

## Quick Answers
- **What does “how to extract fonts” mean?** It’s the process of retrieving embedded font files from a source document during HTML conversion.  
- **Which library handles this?** GroupDocs.Editor for .NET provides a dedicated API for extracting fonts, images, and stylesheets.  
- **Do I need a license?** A free trial is available; a commercial license is required for production use.  
- **What .NET versions are supported?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.  
- **Can I target a custom folder?** Yes, you specify any writable path when saving the extracted resources.

## What is “how to extract fonts”?
**How to extract fonts** refers to retrieving the original font files embedded in a source document (e.g., DOCX, PPTX) so they can be referenced by the generated HTML. This ensures text renders exactly as intended in browsers without relying on system fonts.

## Why use GroupDocs.Editor for HTML resource extraction?
GroupDocs.Editor supports **50+ input and output formats**—including DOCX, PPTX, PDF, and HTML—and can process documents with **up to 300 pages** without loading the entire file into memory. Its API extracts fonts, images, and CSS in a single pass, reducing development time by up to **70 %** compared with manual parsing.

## Prerequisites
Before diving into the tutorial, ensure you have the following prerequisites:
1. **Basic Knowledge of C# and .NET** – Familiarity with C# programming language and .NET framework is essential to follow along with the examples.  
2. **GroupDocs.Editor for .NET Library** – Download and install GroupDocs.Editor for .NET library from the [website](https://releases.groupdocs.com/editor/net/).  
3. **Development Environment** – Set up your preferred development environment such as Visual Studio or any other compatible IDE.

## Import Namespaces
To get started, import the necessary namespaces in your C# project:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```

## How to extract fonts and save HTML resources to a folder?
Load your source document with `Editor editor = new Editor("sample.docx", new WordProcessingLoadOptions());` then call `editor.Save("output.html", SaveOptions.Html);`. After the save operation, the `Resources` collection contains all extracted assets—including fonts—which you can iterate and write to disk. This single‑step approach handles both conversion and resource extraction automatically.

## Step 1: Initialize GroupDocs.Editor
`Editor` is the core class that orchestrates document loading, conversion, and resource extraction. It represents a single document session in memory.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
First, initialize the `Editor` object by providing the path to your sample document. In this example, we're using a Word document, so we specify `WordProcessingLoadOptions` as the document type.

## Step 2: Edit Document
`EditableDocument` is the editable representation returned by the `Edit` method, allowing you to manipulate the document before saving.

```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
Next, create an `EditableDocument` object by calling the `Edit` method of the `Editor` object. This allows you to perform editing operations on the document.

## Step 3: Extract Resources
`Resources` is a collection that groups extracted assets—images, fonts, and stylesheets—into separate lists for easy handling.

```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
Extract resources such as images, fonts, and stylesheets from the document and store them in respective lists.

## Step 4: Specify Output Folder
`outputFolder` is a string that defines where the extracted files will be written. You can point it to any writable directory on the server or local machine.

```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
Define the output folder where the extracted resources will be saved. You can customize the folder path as per your requirement.

## Step 5: Save Resources
`SaveResource` is a helper routine that writes a single binary resource (image, font, or stylesheet) to the file system.

```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
Loop through each image resource, save it to the output folder, and display relevant information such as filename, type, and dimensions.

```csharp
		foreach (FontResourceBase oneFont in fonts)
		{
			Console.WriteLine("Saving {0} of {1} type",
				oneFont.FilenameWithExtension, oneFont.Type.FormalName);
			oneFont.Save(Path.Combine(outputFolder, oneFont.FilenameWithExtension));
		}
```
Similarly, save each font resource to the output folder.

```csharp
		foreach (CssText oneStylesheet in stylesheets)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} encoding",
				oneStylesheet.FilenameWithExtension, oneStylesheet.Type.FormalName, oneStylesheet.Encoding);
			oneStylesheet.Save(Path.Combine(outputFolder, oneStylesheet.FilenameWithExtension));
		}
	}
}
```
Finally, save each stylesheet to the output folder and complete the editing process.

## Common Issues and Solutions
- **Missing fonts after conversion** – Ensure the source document actually embeds the fonts; otherwise, GroupDocs.Editor can only reference system fonts.  
- **Access denied errors** – Verify that the application process has write permissions to the target output folder.  
- **Large documents cause high memory usage** – Use `LoadOptions` with `LoadMode = LoadMode.Stream` to stream large files instead of loading them entirely into memory.

## Frequently Asked Questions

**Q: Is GroupDocs.Editor compatible with other document formats besides Word?**  
A: Yes, it supports Excel, PowerPoint, PDF, HTML, and over 50 additional formats for both editing and resource extraction.

**Q: Can I integrate GroupDocs.Editor into a web application?**  
A: Absolutely. The API works seamlessly with ASP.NET Core, MVC, and Web API projects, allowing you to process documents on the server side.

**Q: Does GroupDocs.Editor provide cloud storage integration?**  
A: Yes, it includes built‑in connectors for Google Drive, Dropbox, OneDrive, and Amazon S3, enabling direct loading and saving of documents in the cloud.

**Q: Is there a free trial available for GroupDocs.Editor?**  
A: A fully functional 30‑day trial can be downloaded from the GroupDocs website without any credit‑card requirement.

**Q: How can I get technical support for extraction issues?**  
A: You can reach the GroupDocs support team via the official forum, submit a ticket through the customer portal, or consult the detailed API documentation.

---

**Last Updated:** 2026-05-12  
**Tested With:** GroupDocs.Editor 23.11 for .NET  
**Author:** GroupDocs

## Related Tutorials

- [Efficient Document Editing with GroupDocs.Editor .NET&#58; Transform HTML to Editable Documents](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)
- [Efficiently Extract and Save DOCX Resources Using GroupDocs.Editor .NET - Complete Guide](/editor/net/document-saving/efficient-extract-save-docx-resources-groupdocs-editor-net/)
- [Mastering Document Editing and Conversion with GroupDocs.Editor .NET&#58; A Complete Guide](/editor/net/document-editing/groupdocs-editor-net-mastering-document-editing/)
