---
title: Save Edited Document to Various Formats
linktitle: Save Edited Document to Various Formats
second_title: GroupDocs.Editor .NET API
description: Learn how to save edited documents to various formats using GroupDocs.Editor for .NET in this comprehensive step-by-step guide.
weight: 11
url: /net/document-processing/save-edited-document-various-formats/
---

# Save Edited Document to Various Formats

## Introduction
Are you looking to save edited documents to various formats using GroupDocs.Editor for .NET? You've come to the right place! This comprehensive guide will walk you through the entire process, from setting up your environment to saving your edited document in multiple formats. Let's dive in and make document editing and saving a breeze!
## Prerequisites
Before we start, ensure you have the following:
1. GroupDocs.Editor for .NET - Download the latest version from [here](https://releases.groupdocs.com/editor/net/).
2. Development Environment - Visual Studio or any other .NET compatible IDE.
3. .NET Framework - Ensure you have .NET Framework 4.6.1 or higher installed.
4. Sample Document - A sample WordProcessing document to work with.
5. Basic C# Knowledge - Familiarity with C# programming is required.
## Import Namespaces
To begin, make sure you import the necessary namespaces into your C# project. This is crucial for accessing GroupDocs.Editor functionality.
```csharp
using System;
using GroupDocs.Editor.Metadata;
```
Let's break down the process into manageable steps. Follow along carefully to ensure you understand each part.
## Step 1: Get a Path to the Input File
First, you need to specify the path to your input WordProcessing file. This file will be loaded and edited.
```csharp
string inputFilePath = "Your Sample Document";
```
## Step 2: Create Load Options for the Document
Next, create load options specific to WordProcessing documents. These options will help customize how the document is loaded.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
```
## Step 3: Load the Document with Options
Now, load the document into an `Editor` instance using the specified load options.
```csharp
using (Editor editor = new Editor(inputFilePath, delegate { return loadOptions; }))
```
## Step 4: Create Editing Options
Prepare editing options for the document. These options will determine how the document is opened for editing.
```csharp
WordProcessingEditOptions editOptions = new WordProcessingEditOptions();
```
## Step 5: Open Document for Editing
Open the document for editing by creating an `EditableDocument` instance. This instance will allow you to make changes to the document.
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
```
## Step 6: Edit the Document Content
Now it's time to edit the content of the document. First, get the document as a single base64-encoded string.
```csharp
string allEmbeddedInsideString = beforeEdit.GetEmbeddedHtml();
```
For example, let's modify the subtitle in the document.
```csharp
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
```
## Step 7: Create New Editable Document from Edited Content
Create a new `EditableDocument` instance from the edited content and resources.
```csharp
using (EditableDocument afterEdit = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null))
```
## Step 8: Save Document to Various Formats
Finally, iterate over all supportable WordProcessing formats and save the edited document in each format.
```csharp
foreach (WordProcessingFormats oneFormat in WordProcessingFormats.All)
{
    // Prepare save options
    WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(oneFormat);
    // Prepare save path
    string savePath = Path.Combine("OutputDirectory", "MultipleOutFormats." + saveOptions.OutputFormat.Extension);
    // Save the document
    editor.Save(afterEdit, savePath, saveOptions);
}
```
## Completion Message
To conclude, you can print a message indicating that the process has successfully finished.
```csharp
Console.WriteLine("SavingEditedDocumentToAllFormats routine has successfully finished");
```
## Conclusion
Congratulations! You’ve successfully learned how to save edited documents to various formats using GroupDocs.Editor for .NET. This powerful tool makes it easy to manipulate and save documents in multiple formats with just a few lines of code. Remember, the key steps involve loading the document, editing the content, and saving it in the desired formats.
## FAQ's
### What is GroupDocs.Editor for .NET?
GroupDocs.Editor for .NET is a powerful API that allows you to edit documents in various formats using .NET applications.
### Can I use GroupDocs.Editor for free?
Yes, you can use it with a free trial. Download it [here](https://releases.groupdocs.com/).
### What formats are supported by GroupDocs.Editor?
GroupDocs.Editor supports a wide range of formats, including DOCX, PDF, HTML, and many more.
### How do I get a temporary license for GroupDocs.Editor?
You can obtain a temporary license [here](https://purchase.groupdocs.com/temporary-license/).
### Where can I find more documentation and support?
Detailed documentation is available [here](https://tutorials.groupdocs.com/editor/net/), and you can get support [here](https://forum.groupdocs.com/c/editor/20).
