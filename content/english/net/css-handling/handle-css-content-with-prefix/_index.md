---
title: Handle CSS Content with Prefix
linktitle: Handle CSS Content with Prefix
second_title: GroupDocs.Editor .NET API
description: Learn how to handle CSS content with prefix and extract CSS content using GroupDocs.Editor for .NET in this detailed step‑by‑step tutorial.
weight: 11
url: /net/css-handling/handle-css-content-with-prefix/
type: docs
date: 2026-03-06
---

# Handle CSS Content with Prefix

In this tutorial you’ll discover **how to handle css prefix** when working with stylesheets inside a document using GroupDocs.Editor for .NET. Whether you need to prepend a URL to images, fonts, or any external resource, the steps below show you exactly how to **handle css prefix** and also how to **extract css content** for further processing.

## Quick Answers
- **What does “handle css prefix” mean?** Adding a custom URL prefix to external resources referenced in CSS.
- **Which API method returns CSS styles?** `EditableDocument.GetCssContent(...)`.
- **Do I need a license?** A trial license is available; a commercial license is required for production.
- **What .NET versions are supported?** .NET Framework 4.5+ and .NET Core/5/6.
- **Can I change the prefix at runtime?** Yes – simply pass a different string to `GetCssContent`.

## What is **handle css prefix**?
Applying a prefix to CSS resources rewrites the paths of images, fonts, or other assets so they point to a location you control (e.g., a CDN or a secured server). This is especially useful when you export a document and need all external references to be reachable from a web application.

## Why use GroupDocs.Editor to **extract css content**?
GroupDocs.Editor can read the original CSS embedded in WordProcessing documents, give you the raw stylesheet strings, and let you manipulate them before rendering or saving. This eliminates the need for manual parsing and guarantees that the extracted CSS matches the document’s internal representation.

## Prerequisites
Before we get started, make sure you have the following prerequisites in place:
- Visual Studio: You’ll need a working installation of Visual Studio.  
- .NET Framework: Ensure you have the .NET Framework installed.  
- GroupDocs.Editor for .NET: You can download it [here](https://releases.groupdocs.com/editor/net/).  
- Sample Document: Have a sample document ready for editing.

## Import Namespaces
First, let’s import the necessary namespaces to ensure our code runs smoothly. This step gives us access to the core classes of GroupDocs.Editor.

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Editor.Options;
```

## Step 1: Initialize the Editor
The first step involves creating an `Editor` instance with your sample document. This sets up the editing environment.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```

## Step 2: Edit the Document
Next, we obtain an `EditableDocument` object. This object represents the editable version of the file and allows us to work with its internal parts.

```csharp
    using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
    {
```

## Step 3: Set External Prefixes
Define the URL prefixes for images and fonts. These prefixes will be prepended to every image and font reference found in the CSS.

```csharp
        string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
        string externalFontsPrefix = "http://www.mywebsite.com/fonts/id=";
```

## Step 4: **Extract CSS content** with the Prefixes
Call `GetCssContent`, passing the prefixes you just defined. The method returns a list of CSS stylesheet strings that already contain the prefixed URLs.

```csharp
        List<string> stylesheets = document.GetCssContent(externalImagesPrefix, externalFontsPrefix);
```

## Step 5: Output the Results
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

## Common Issues and Solutions
- **No stylesheets returned** – Ensure the source document actually contains CSS (e.g., a Word document with styled tables or embedded HTML).  
- **Incorrect URLs** – Double‑check that the prefix strings end with the appropriate delimiter (`/` or `=`) for your server routing.  
- **Performance concerns** – For very large documents, consider processing stylesheets in batches to avoid high memory usage.

## Conclusion
Handling CSS content with a prefix using GroupDocs.Editor for .NET is straightforward and powerful. By following these steps you can **handle css prefix**, retrieve the raw CSS via **extract css content**, and seamlessly integrate external resources into your web workflow. Explore other GroupDocs.Editor features such as HTML conversion, image extraction, and document merging to get even more value out of the API.

## FAQ's
### Can I use GroupDocs.Editor for .NET with other document formats?
Yes, GroupDocs.Editor for .NET supports various document formats including PDF, Word, Excel, and more.

### Is there a free trial available for GroupDocs.Editor for .NET?
Absolutely! You can start your free trial [here](https://releases.groupdocs.com/).

### How do I get a temporary license for GroupDocs.Editor for .NET?
You can obtain a temporary license [here](https://purchase.groupdocs.com/temporary-license/).

### Where can I find detailed documentation for GroupDocs.Editor for .NET?
Detailed documentation is available [here](https://tutorials.groupdocs.com/editor/net/).

### What support options are available for GroupDocs.Editor for .NET?
You can get support [here](https://forum.groupdocs.com/c/editor/20).

## Additional Frequently Asked Questions

**Q: Can I change the prefix after extracting the CSS?**  
A: Yes. Call `GetCssContent` again with a different prefix string; the method always uses the values you pass at runtime.

**Q: Does this work with password‑protected documents?**  
A: Yes. Provide the password in `WordProcessingLoadOptions` when creating the `Editor` instance.

**Q: Is it possible to save the modified CSS back into the document?**  
A: GroupDocs.Editor currently provides read‑only access to CSS. To persist changes you would need to replace the original stylesheet using the document’s underlying XML APIs.

---

**Last Updated:** 2026-03-06  
**Tested With:** GroupDocs.Editor 23.12 for .NET  
**Author:** GroupDocs