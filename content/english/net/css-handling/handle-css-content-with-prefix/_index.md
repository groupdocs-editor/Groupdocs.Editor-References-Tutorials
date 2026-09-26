---
date: 2026-09-26
description: Learn how to handle css prefix and extract css content using GroupDocs.Editor
  for .NET in this detailed step‑by‑step tutorial.
images:
- /net/css-handling/handle-css-content-with-prefix/og-image.png
keywords:
- handle css prefix
- extract css content
- edit document css
- prepend url to css
lastmod: 2026-09-26
linktitle: Handle CSS Content with Prefix
og_description: Discover how to handle css prefix and extract css content with GroupDocs.Editor
  for .NET. Follow a step‑by‑step guide to prepend URLs to CSS resources and retrieve
  stylesheets.
og_image_alt: Developer guide showing css prefix handling with GroupDocs.Editor for
  .NET
og_title: How to handle css prefix in GroupDocs.Editor for .NET
schemas:
- author: GroupDocs
  dateModified: '2026-09-26'
  description: Learn how to handle css prefix and extract css content using GroupDocs.Editor
    for .NET in this detailed step‑by‑step tutorial.
  headline: How to handle css prefix in GroupDocs.Editor for .NET
  type: TechArticle
- questions:
  - answer: Yes, GroupDocs.Editor for .NET supports PDF, Word, Excel, PowerPoint,
      and many other formats.
    question: Can I use GroupDocs.Editor for .NET with other document formats?
  - answer: Absolutely! You can start your free trial on the [GroupDocs free trial
      page](https://releases.groupdocs.com/).
    question: Is there a free trial available for GroupDocs.Editor for .NET?
  - answer: You can obtain a temporary license from the [temporary license page](https://purchase.groupdocs.com/temporary-license/).
    question: How do I get a temporary license for GroupDocs.Editor for .NET?
  - answer: Detailed documentation is available on the [GroupDocs.Editor for .NET
      documentation site](https://tutorials.groupdocs.com/editor/net/).
    question: Where can I find detailed documentation for GroupDocs.Editor for .NET?
  - answer: You can get support through the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).
    question: What support options are available for GroupDocs.Editor for .NET?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
tags:
- css handling
- GroupDocs.Editor
- .NET document processing
- css prefix
- api tutorial
title: How to handle css prefix in GroupDocs.Editor for .NET
type: docs
url: /net/css-handling/handle-css-content-with-prefix/
weight: 11
---

# How to handle css prefix in GroupDocs.Editor for .NET

In this tutorial you’ll learn **how to handle css prefix** when working with stylesheets inside a document using GroupDocs.Editor for .NET. Whether you need to prepend a URL to images, fonts, or any external resource, the steps below show you exactly how to **handle css prefix** and also how to **extract css content** for further processing. By the end of the guide you’ll be able to rewrite resource paths, retrieve the raw CSS strings, and integrate them into your web workflow with confidence.

## Quick answers
- **What does “handle css prefix” mean?** Adding a custom URL prefix to external resources referenced in CSS.  
- **Which API method returns CSS styles?** `EditableDocument.GetCssContent(...)`.  
- **Do I need a license?** A trial license is available; a commercial license is required for production.  
- **What .NET versions are supported?** .NET Framework 4.5+ and .NET Core/5/6.  
- **Can I change the prefix at runtime?** Yes – simply pass a different string to `GetCssContent`.

## What is handle css prefix?
The term refers to rewriting the URLs of images, fonts, or any external asset inside a CSS file so they point to a location you control, such as a CDN or a secure server. By prepending a consistent base URL you guarantee that every resource loads correctly when the document is rendered in a browser or a web‑based viewer.

## Why use GroupDocs.Editor to extract css content?
GroupDocs.Editor can read the original CSS embedded in WordProcessing documents, return the raw stylesheet strings, and let you manipulate them before rendering or saving. This eliminates manual parsing, guarantees fidelity to the document’s internal representation, and supports **30+ file formats** while processing files up to **500 MB** without loading the entire file into memory.

## Prerequisites
Before we get started, make sure you have the following prerequisites in place:
- Visual Studio: You’ll need a working installation of Visual Studio.  
- .NET Framework: Ensure you have the .NET Framework installed.  
- GroupDocs.Editor for .NET: You can download it from the [GroupDocs.Editor for .NET download page](https://releases.groupdocs.com/editor/net/).  
- Sample Document: Have a sample document ready for editing.

## Import namespaces
First, let’s import the necessary namespaces to ensure our code runs smoothly. This step gives us access to the core classes of GroupDocs.Editor.

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Editor.Options;
```

## Step 1: Initialize the Editor
The `Editor` class is the entry point for working with documents in GroupDocs.Editor. It manages loading, editing, and saving operations.  
The first step involves creating an `Editor` instance with your sample document. This sets up the editing environment.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```

## Step 2: Edit the document
The `EditableDocument` object represents the editable version of the file and exposes its internal parts, such as CSS, images, and HTML.  
Next, we obtain an `EditableDocument` object. This object allows us to work with the document’s internal CSS.

```csharp
    using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
    {
```

## Step 3: Set external prefixes
Define the URL prefixes for images and fonts. These prefixes will be prepended to every image and font reference found in the CSS.

```csharp
        string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
        string externalFontsPrefix = "http://www.mywebsite.com/fonts/id=";
```

## Step 4: Extract css content with the prefixes
`GetCssContent` returns a collection of CSS stylesheet strings that already contain the prefixed URLs you supplied.  
Call `GetCssContent`, passing the prefixes you just defined. The method returns a list of CSS stylesheet strings that already contain the prefixed URLs.

```csharp
        List<string> stylesheets = document.GetCssContent(externalImagesPrefix, externalFontsPrefix);
```

## Step 5: Output the results
Print the number of stylesheets found and display each stylesheet. This helps you verify that the prefixes were applied correctly.

```csharp
        Console.WriteLine("There are {0} stylesheets in the input document", stylesheets.Count);
        foreach (string css in stylesheets)
        {
            Console.WriteLine(css);
        }
    }
}
```

## Common issues and solutions
- **No stylesheets returned** – Ensure the source document actually contains CSS (e.g., a Word document with styled tables or embedded HTML).  
- **Incorrect URLs** – Double‑check that the prefix strings end with the appropriate delimiter (`/` or `=`) for your server routing.  
- **Performance concerns** – For very large documents, consider processing stylesheets in batches to avoid high memory usage.

## Frequently asked questions

**Q: Can I use GroupDocs.Editor for .NET with other document formats?**  
A: Yes, GroupDocs.Editor for .NET supports PDF, Word, Excel, PowerPoint, and many other formats.

**Q: Is there a free trial available for GroupDocs.Editor for .NET?**  
A: Absolutely! You can start your free trial on the [GroupDocs free trial page](https://releases.groupdocs.com/).

**Q: How do I get a temporary license for GroupDocs.Editor for .NET?**  
A: You can obtain a temporary license from the [temporary license page](https://purchase.groupdocs.com/temporary-license/).

**Q: Where can I find detailed documentation for GroupDocs.Editor for .NET?**  
A: Detailed documentation is available on the [GroupDocs.Editor for .NET documentation site](https://tutorials.groupdocs.com/editor/net/).

**Q: What support options are available for GroupDocs.Editor for .NET?**  
A: You can get support through the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).

## Additional frequently asked questions

**Q: Can I change the prefix after extracting the CSS?**  
A: Yes. Call `GetCssContent` again with a different prefix string; the method always uses the values you pass at runtime.

**Q: Does this work with password‑protected documents?**  
A: Yes. Provide the password in `WordProcessingLoadOptions` when creating the `Editor` instance.

**Q: Is it possible to save the modified CSS back into the document?**  
A: GroupDocs.Editor currently provides read‑only access to CSS. To persist changes you would need to replace the original stylesheet using the document’s underlying XML APIs.

---

**Last Updated:** 2026-09-26  
**Tested With:** GroupDocs.Editor 23.12 for .NET  
**Author:** GroupDocs

## Related Tutorials

- [Extract External CSS from Word Docs Using GroupDocs.Editor .NET&#58; A Comprehensive Guide](/editor/net/html-web-documents/extract-external-css-word-docs-groupdocs-editor-dotnet/)
- [Extract & Prefix HTML from Word Docs using GroupDocs.Editor .NET](/editor/net/html-web-documents/groupdocs-editor-dotnet-extract-prefix-html-word-docs/)
- [How to Extract and Modify HTML Content in Word Documents Using GroupDocs.Editor .NET](/editor/net/html-web-documents/extract-modify-html-content-word-docs-groupdocs-editor-net/)