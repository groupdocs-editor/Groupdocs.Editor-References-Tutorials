---
title: Advanced Usage of Editable Documents
linktitle: Advanced Usage of Editable Documents
second_title: GroupDocs.Editor .NET API
description: Learn advanced usage of GroupDocs.Editor for .NET creating, editing, and extracting resources from documents programmatically.
weight: 11
url: /net/document-editing/advanced-usage-of-editable-documents/
---
## Introduction
If you're a .NET developer looking to enhance your document editing capabilities, GroupDocs.Editor for .NET offers a powerful suite of tools. This comprehensive guide will walk you through the advanced usage of editable documents using GroupDocs.Editor, breaking down each step in detail to ensure you can harness its full potential.
## Prerequisites
Before diving into the advanced functionalities, make sure you have the following:
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
## Step 2: Extracting Document Resources
The `EditableDocument` contains various resources that can be extracted and manipulated. Let's break these down:
### Step 2.1: Extract Entire Document as HTML
You can generate a single string that contains the entire document with all its resources embedded as HTML.
```csharp
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```
This string will be quite large as it includes stylesheets, images, and fonts encoded in base64.
### Step 2.2: Extract All Images
Extract all images from the document.
```csharp
List<IImageResource> allImages = beforeEdit.Images;
```
### Step 2.3: Extract All Fonts
Extract all fonts used in the document.
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
## Step 3: Adjusting External Links
Sometimes, you need to adjust external links to point to a custom resource handler. Here's how to do it:
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
## Step 4: Save Document as HTML
Save the edited document as an HTML file, including its resources.
```csharp
string htmlFilePath = Path.Combine("output", Path.GetFileNameWithoutExtension(inputFilePath) + ".html");
beforeEdit.Save(htmlFilePath);
```
This method creates a separate directory for resources like stylesheets, images, and fonts.
## Step 5: Disposing of EditableDocument
EditableDocument implements `IDisposable` and provides the ability to check if the instance is disposed.
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
Create an instance of EditableDocument from an HTML document.
### Step 6.1: From HTML File
```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
```
### Step 6.2: From HTML Markup
```csharp
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);
```
These instances (afterEditFromFile and afterEditFromMarkup) are identical to the original (beforeEdit).
## Step 7: Manual Disposal
Manually dispose of your EditableDocument instances.
```csharp
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```
This ensures proper cleanup of resources.
## Conclusion
GroupDocs.Editor for .NET provides robust tools for editing documents programmatically. By following this step-by-step guide, you can efficiently manage document content, resources, and output formats. Whether you are embedding resources, adjusting external links, or converting documents to HTML, GroupDocs.Editor equips you with the functionality needed for advanced document manipulation.
## FAQ's
### What formats does GroupDocs.Editor support?
GroupDocs.Editor supports various formats including DOCX, XLSX, PPTX, and more.
### Can I use GroupDocs.Editor without a license?
Yes, you can use it with a [free trial](https://releases.groupdocs.com/) or a [temporary license](https://purchase.groupdocs.com/temporary-license/).
### How do I extract specific resources from a document?
You can extract images, fonts, and stylesheets using the provided methods like `Images`, `Fonts`, and `Css`.
### Is it possible to adjust links in the HTML output?
Yes, you can adjust external links by specifying custom prefixes for images, CSS, and fonts.
### How do I save an edited document as an HTML file?
Use the `Save` method of the `EditableDocument` class to save the document as an HTML file, including its resources.
