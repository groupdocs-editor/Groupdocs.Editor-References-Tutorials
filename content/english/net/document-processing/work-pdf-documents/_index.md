---
title: Work with PDF Documents
linktitle: Work with PDF Documents
second_title: GroupDocs.Editor .NET API
description: Learn how to edit PDF documents using GroupDocs.Editor for .NET with this tutorial. Modify content, handle large files, and save your edits securely.
type: docs
weight: 14
url: /net/document-processing/work-pdf-documents/
---
## Introduction
Are you looking for a comprehensive guide to manipulate and edit PDF documents using GroupDocs.Editor for .NET? You're in the right place! In this tutorial, we'll walk you through the entire process, from setting up your project to saving your edited PDF document. Whether you're a seasoned developer or just starting, you'll find this guide helpful and easy to follow. Let's dive in!
## Prerequisites
Before we get started, there are a few things you'll need:
1. .NET Development Environment: Ensure you have a .NET development environment set up. This could be Visual Studio or any other preferred IDE.
2. GroupDocs.Editor for .NET: Download and install the GroupDocs.Editor for .NET library. You can get it from the [release page](https://releases.groupdocs.com/editor/net/).
3. Basic Understanding of C#: Familiarity with C# programming will be beneficial as this tutorial involves writing and understanding C# code.
## Import Namespaces
Before writing any code, ensure you have the necessary namespaces imported into your project:
```csharp
using System;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Reflection;
```
## Step 1: Get a Path to the Input File
First, you need to specify the path to your PDF document. For this tutorial, we'll assume you have a sample PDF file.
```csharp
string inputFilePath = "Your Sample Document.pdf";
```
## Step 2: Create a Stream from the Path
Next, create a file stream from the path you specified. This stream will be used to read the PDF document.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
```
## Step 3: Create Load Options for the Document
To load the PDF document, you need to specify load options. If your PDF is password-protected, you can provide the password here.
```csharp
Options.PdfLoadOptions loadOptions = new PdfLoadOptions();
// If the document is password-protected
loadOptions.Password = "your_password";
```
## Step 4: Load the Document into the Editor Instance
Now, use the file stream and load options to load the document into an `Editor` instance.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    var documentInfo = editor.GetDocumentInfo(null);
```
## Step 5: Create Editing Options
Set the editing options for the document. In this case, we'll enable pagination mode.
```csharp
Options.PdfEditOptions editOptions = new PdfEditOptions();
editOptions.EnablePagination = true;
```
## Step 6: Create an Intermediate Editable Document
Create an intermediate editable document using the editor instance and editing options.
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
{
    // Extract textual content as HTML markup
    string originalContent = beforeEdit.GetContent();
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## Step 7: Modify the Content
Modify the content of the document as needed. Here, we are simply replacing a word in the document.
```csharp
string editedContent = originalContent.Replace("document", "edited document");
```
## Step 8: Create a New Editable Document with Edited Content
Create a new `EditableDocument` instance with the edited content and resources.
```csharp
using (EditableDocument afterEdit = EditableDocument.FromMarkup(editedContent, allResources))
{
    string originalContent3 = afterEdit.GetContent();
```
## Step 9: Create Document Save Options
Specify the save options for the PDF document. You can also set a password for the output document.
```csharp
FixedLayoutFormats docmFormat = FixedLayoutFormats.Pdf;
Options.PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.Password = "output_password";
saveOptions.OptimizeMemoryUsage = true;
```
## Step 10: Save the Edited Document
Finally, save the edited document to the specified output path.
```csharp
string outputFilename = Path.GetFileNameWithoutExtension(inputFilePath) + "." + docmFormat.Extension;
string outputPath = Path.Combine("OutputDirectoryPath", outputFilename);
using (FileStream outputStream = File.Create(outputPath))
{
    editor.Save(afterEdit, outputStream, saveOptions);
}
```

## Conclusion
There you have it! By following these steps, you can successfully edit PDF documents using GroupDocs.Editor for .NET. This powerful library makes it easy to manipulate and save PDF files programmatically. Whether you're making simple text replacements or more complex modifications, GroupDocs.Editor for .NET has you covered.
## FAQ's
### Can I use GroupDocs.Editor for .NET to edit other document formats?
Yes, GroupDocs.Editor for .NET supports various document formats including Word, Excel, PowerPoint, and more.
### How can I get a free trial of GroupDocs.Editor for .NET?
You can download a free trial from the [GroupDocs.Editor free trial page](https://releases.groupdocs.com/).
### Is it possible to handle large PDF documents with GroupDocs.Editor for .NET?
Yes, GroupDocs.Editor for .NET includes options to optimize memory usage, making it suitable for handling large documents.
### How do I get support if I encounter issues?
For support, you can visit the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).
### Can I encrypt the PDF document while saving it?
Yes, you can set a password to encrypt the PDF document during the saving process using the `PdfSaveOptions.Password` property.
