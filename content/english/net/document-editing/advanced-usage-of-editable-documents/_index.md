---
title: "Extract Images from DOCX – Advanced Editable Document Usage"
linktitle: "Extract Images from DOCX – Advanced Editable Document Usage"
second_title: "GroupDocs.Editor .NET API"
description: "Learn how to extract images from DOCX, convert DOCX to HTML, and save document as HTML using GroupDocs.Editor for .NET."
weight: 11
url: /net/document-editing/advanced-usage-of-editable-documents/
type: docs
date: 2026-03-14
---
# Extract Images from DOCX – Advanced Editable Document Usage

If you're a .NET developer looking to **extract images from DOCX** and enhance your document editing capabilities, GroupDocs.Editor for .NET offers a powerful suite of tools. This comprehensive guide will walk you through the advanced usage of editable documents using GroupDocs.Editor, breaking down each step in detail so you can harness its full potential.

## Quick Answers
- **How can I extract images from a DOCX file?** Use `EditableDocument.Images` after loading the document with `Editor`.
- **Can I convert DOCX to HTML with embedded resources?** Yes—call `EditableDocument.GetEmbeddedHtml()` or `GetContent()` for HTML markup.
- **What method saves the edited document as HTML?** `EditableDocument.Save(htmlFilePath)` creates an HTML file with a resource folder.
- **Is it possible to extract fonts from a Word document?** Use `EditableDocument.Fonts` to retrieve all font resources.
- **Do I need a license for production use?** A valid GroupDocs.Editor license is required; a free trial is available.

## What is **extract images from docx**?
Extracting images from a DOCX file means programmatically retrieving each picture embedded in the Word document so you can reuse, modify, or store them separately. GroupDocs.Editor exposes the `Images` collection on an `EditableDocument` instance, making this task straightforward.

## Why use GroupDocs.Editor for this workflow?
- **Full control** over document resources (images, fonts, CSS) without manual ZIP handling.  
- **Seamless conversion** from DOCX to HTML while preserving layout and styling.  
- **Easy resource extraction** for custom image handling, font embedding, or CDN delivery.  
- **Robust disposal pattern** ensures no memory leaks in long‑running services.

## Prerequisites
- Visual Studio installed on your development machine.  
- .NET Framework compatible with GroupDocs.Editor.  
- GroupDocs.Editor for .NET library. You can [download it here](https://releases.groupdocs.com/editor/net/).  
- A valid GroupDocs.Editor license. You can get a [free trial](https://releases.groupdocs.com/) or purchase a [temporary license](https://purchase.groupdocs.com/temporary-license/).

## Import Namespaces
To begin, ensure you import the necessary namespaces in your .NET project:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```

## Step 1: Creating an EditableDocument Instance
First, you need to create an instance of `EditableDocument` by loading and editing an input document of a supported format.

```csharp
string inputFilePath = "YourSampleDocument.docx";
Editor editor = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```

In this step, we load the input document and prepare it for editing.

## How to **extract images from DOCX**?
Below we dive into the resource extraction capabilities, starting with the most common need—getting all images out of a Word file.

## Step 2: Extracting Document Resources
The `EditableDocument` contains various resources that can be extracted and manipulated. Let's break these down:

### Step 2.1: Extract Entire Document as HTML
You can generate a single string that contains the entire document with all its resources embedded as HTML.

```csharp
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```

This string will be quite large as it includes stylesheets, images, and fonts encoded in base64.

### Step 2.2: Extract All Images *(primary keyword in action)*
Extract all images from the document—this is the core of **extract images from docx**.

```csharp
List<IImageResource> allImages = beforeEdit.Images;
```

### Step 2.3: Extract All Fonts *(secondary keyword)*
If you also need to **extract fonts from word**, use the following call:

```csharp
List<FontResourceBase> allFonts = beforeEdit.Fonts;
```

### Step 2.4: Extract All Stylesheets
Extract all stylesheets in a textual format.

```csharp
List<CssText> allStylesheets = beforeEdit.Css;
```

### Step 2.5: Gather All Resources
Gather all resources in one call.

```csharp
List<IHtmlResource> allResources = beforeEdit.AllResources;
```

This includes images, fonts, and stylesheets.

### Step 2.6: Obtain HTML Markup
Get the HTML markup of the document without embedded resources.

```csharp
string htmlMarkup = beforeEdit.GetContent();
```

## How to **convert docx to html** with custom handling?
Sometimes you need to adjust external links so they point to your own resource handlers.

## Step 3: Adjusting External Links
### Step 3.1: Prepare Custom Prefixes
Prepare prefixes that will prepend original external links.

```csharp
string customImagesRequesthandlerUri = "http://example.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://example.com/CssHandler/id=";
string customFontsRequesthandlerUri = "http://example.com/FontsHandler/id=";
```

### Step 3.2: Generate Prefixed HTML Markup
Generate HTML markup with adjusted links.

```csharp
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```

### Step 3.3: Obtain Body-Only HTML Content
Some WYSIWYG editors only handle pure HTML markup without headers.

```csharp
string onlyBodyContent = beforeEdit.GetBodyContent();
```

### Step 3.4: Prefixed Body-Only Content
Generate body-only content with custom image prefixes.

```csharp
string prefixedBodyContent = beforeEdit.GetBodyContent(customImagesRequesthandlerUri);
```

### Step 3.5: Extract Stylesheets
Extract stylesheets used in the document.

```csharp
List<string> stylesheets = beforeEdit.GetCssContent();
```

### Step 3.6: Prefixed Stylesheets
Extract stylesheets with custom prefixes.

```csharp
List<string> prefixedStylesheets = beforeEdit.GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri);
```

## How to **save document as html** correctly?
## Step 4: Save Document as HTML
Save the edited document as an HTML file, including its resources.

```csharp
string htmlFilePath = Path.Combine("output", Path.GetFileNameWithoutExtension(inputFilePath) + ".html");
beforeEdit.Save(htmlFilePath);
```

This method creates a separate directory for resources like stylesheets, images, and fonts.

## Step 5: Disposing of EditableDocument
`EditableDocument` implements `IDisposable` and provides the ability to check if the instance is disposed.

```csharp
Console.WriteLine("EditableDocument is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");
```

### Step 5.1 Handling Dispose Event
You can also subscribe to the disposing event.

```csharp
EventHandler someMethod = delegate { Console.WriteLine("Disposing event was spotted!"); };
beforeEdit.Disposed += someMethod;
```

## Step 6: Creating EditableDocument from HTML
Create an instance of `EditableDocument` from an HTML document.

### Step 6.1: From HTML File

```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
```

### Step 6.2: From HTML Markup

```csharp
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);
```

These instances (`afterEditFromFile` and `afterEditFromMarkup`) are identical to the original (`beforeEdit`).

## Step 7: Manual Disposal
Manually dispose of your `EditableDocument` instances.

```csharp
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```

This ensures proper cleanup of resources.

## Common Issues and Solutions
- **Images not appearing after extraction:** Verify that the document actually contains embedded images and that you are accessing `beforeEdit.Images` after calling `Edit`.  
- **Fonts missing in HTML output:** Ensure you call `GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri)` to embed font URLs correctly.  
- **Large HTML strings causing memory pressure:** Use `GetContent()` for markup without embedded resources and serve images/CSS from separate files.

## Frequently Asked Questions

**Q: What formats does GroupDocs.Editor support?**  
A: GroupDocs.Editor supports DOCX, XLSX, PPTX, and many other popular office formats.

**Q: Can I use GroupDocs.Editor without a license?**  
A: Yes, you can use it with a [free trial](https://releases.groupdocs.com/) or a [temporary license](https://purchase.groupdocs.com/temporary-license/).

**Q: How do I extract specific resources from a document?**  
A: Use the `Images`, `Fonts`, and `Css` collections on the `EditableDocument` instance.

**Q: Is it possible to adjust links in the HTML output?**  
A: Yes, pass custom URI prefixes to `GetContent` or `GetBodyContent` to rewrite image, CSS, and font links.

**Q: How do I save an edited document as an HTML file?**  
A: Call the `Save` method on the `EditableDocument` instance, providing a file path ending with `.html`.

---

**Last Updated:** 2026-03-14  
**Tested With:** GroupDocs.Editor for .NET (latest release)  
**Author:** GroupDocs