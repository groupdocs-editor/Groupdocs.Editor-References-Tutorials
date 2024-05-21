---
title: Save Document
linktitle: Save Document
second_title: GroupDocs.Editor .NET API
description: Effortlessly edit and save documents using GroupDocs.Editor for .NET. This step-by-step guide simplifies the process for developers.
type: docs
weight: 14
url: /net/document-editing/save-document/
---
## Introduction
Are you looking to effortlessly edit and save documents using GroupDocs.Editor for .NET? You're in the right place! This tutorial will guide you through the process step-by-step, ensuring you can easily manage your documents. Whether you're a seasoned developer or a beginner, our guide will provide you with all the information you need to get started.
## Prerequisites
Before diving into the tutorial, make sure you have the following prerequisites in place:
- Development Environment: Visual Studio installed on your machine.
- .NET Framework: Ensure you have .NET Framework 4.6.1 or later.
- GroupDocs.Editor for .NET: Download the latest version [here](https://releases.groupdocs.com/editor/net/).
- Basic C# Knowledge: Familiarity with C# programming is essential.
## Import Namespaces
To use GroupDocs.Editor in your .NET project, you need to import the necessary namespaces. Here's how you do it:
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
Now that we've got our environment set up and the necessary namespaces imported, let's dive into the steps required to load, edit, and save a document using GroupDocs.Editor for .NET.
## Step 1: Load the Document
First, we need to load the document that we want to edit. GroupDocs.Editor makes this process straightforward. Here’s how you can do it:

```csharp
string inputFilePath = "Your Sample Document";
Editor editor = new Editor(inputFilePath, delegate { return new Options.WordProcessingLoadOptions(); });
EditableDocument defaultWordProcessingDoc = editor.Edit();
```
In this step, we specify the path to the document we want to edit and create an instance of the `Editor` class. The `Edit` method is then called to load the document into an `EditableDocument` object.
## Step 2: Modify the Document
With the document loaded, it's time to make some modifications. Since we don't have a WYSIWYG editor attached, we'll simulate the editing process in code.

```csharp
string allEmbeddedInsideString = defaultWordProcessingDoc.GetEmbeddedHtml();
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
EditableDocument editedDoc = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```
Here, we retrieve the embedded HTML content of the document, perform a simple text replacement, and create a new `EditableDocument` instance from the modified HTML.
## Step 3: Save the Document
After editing the document, the final step is to save it. GroupDocs.Editor provides multiple options for saving the document in different formats.
## Save as RTF
```csharp
string outputRtfPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.rtf");
WordProcessingSaveOptions rtfSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
editor.Save(editedDoc, outputRtfPath, rtfSaveOptions);
```
## Save as DOCM
```csharp
string outputDocmPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.docm");
WordProcessingSaveOptions docmSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm);
using (FileStream outputStream = File.Create(outputDocmPath))
{
    editor.Save(editedDoc, outputStream, docmSaveOptions);
}
```
## Save as Plain Text
```csharp
string outputTxtPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.txt");
TextSaveOptions textSaveOptions = new TextSaveOptions
{
    Encoding = System.Text.Encoding.UTF8,
    PreserveTableLayout = true
};
editor.Save(editedDoc, outputTxtPath, textSaveOptions);
```
## Step 4: Cleanup
Finally, it's crucial to dispose of the `EditableDocument` and `Editor` instances to free up resources.
```csharp
editedDoc.Dispose();
defaultWordProcessingDoc.Dispose();
editor.Dispose();
```
By following these steps, you can efficiently load, edit, and save documents using GroupDocs.Editor for .NET. This powerful tool provides flexibility and ease of use, making document management a breeze.
## Conclusion
Editing and saving documents programmatically has never been easier with GroupDocs.Editor for .NET. This guide walked you through the entire process, from loading a document to saving it in various formats. With GroupDocs.Editor, you have a versatile and robust solution at your fingertips, simplifying the document editing process.
## FAQ's
### What file formats does GroupDocs.Editor support?
GroupDocs.Editor supports various file formats, including DOCX, RTF, TXT, and many more. For a full list, check out the [documentation](https://reference.groupdocs.com/editor/net/).
### Can I try GroupDocs.Editor before purchasing?
Yes, you can get a [free trial](https://releases.groupdocs.com/) to test the features of GroupDocs.Editor.
### Is there any support available if I face issues?
Absolutely! You can visit the [support forum](https://forum.groupdocs.com/c/editor/20) for assistance with any issues you encounter.
### How do I obtain a temporary license?
You can request a [temporary license](https://purchase.groupdocs.com/temporary-license/) for evaluation purposes.
### Where can I purchase the full version of GroupDocs.Editor?
You can buy the full version [here](https://purchase.groupdocs.com/buy).
