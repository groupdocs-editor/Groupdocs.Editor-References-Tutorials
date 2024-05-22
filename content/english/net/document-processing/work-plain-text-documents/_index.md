---
title: Work with Plain Text Documents
linktitle: Work with Plain Text Documents
second_title: GroupDocs.Editor .NET API
description: Learn to edit plain text documents using GroupDocs.Editor for .NET with our step-by-step guide. Simplify your .NET document editing process.
type: docs
weight: 15
url: /net/document-processing/work-plain-text-documents/
---
## Introduction
Are you looking to streamline your document editing process in .NET? Look no further than GroupDocs.Editor for .NET! This powerful API allows you to edit a wide variety of document formats with ease. In this tutorial, we'll guide you through the process of working with plain text documents using GroupDocs.Editor for .NET. By the end, you'll be equipped to handle text document editing like a pro. Ready to dive in? Let's get started!
## Prerequisites
Before we start, there are a few things you'll need to have in place:
- .NET Development Environment: Ensure you have a working .NET development environment set up. Visual Studio is a popular choice.
- GroupDocs.Editor for .NET: Download and install the [GroupDocs.Editor for .NET](https://releases.groupdocs.com/editor/net/).
- Basic C# Knowledge: Familiarity with C# programming language will help you follow along with the examples.
- Text Editor: Any text editor will do, though Visual Studio Code is recommended for its features and ease of use.
## Import Namespaces
To start using GroupDocs.Editor for .NET, you need to import the necessary namespaces into your project. This ensures that all the required classes and methods are available for use.
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```
Let's break down the process into manageable steps. Follow along as we guide you through each stage of editing plain text documents using GroupDocs.Editor for .NET.
## Step 1: Get a Path to the Input TXT File
First, you need to specify the path to the input TXT file. This can be a path to a local file or a stream containing the file content.
```csharp
string inputFilePath = "YourSampleDocument.txt";
```
## Step 2: Create an Editor Instance
Next, create an instance of the `Editor` class. This class is responsible for loading and editing documents. No load options are required at this stage.
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## Step 3: Create TXT Editing Options
Now, create the TXT editing options. These options allow you to specify how the text content should be processed during editing.
```csharp
    TextEditOptions editOptions = new TextEditOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        RecognizeLists = true,
        LeadingSpaces = TextLeadingSpacesOptions.ConvertToIndent,
        TrailingSpaces = TextTrailingSpacesOptions.Trim
    };
```
## Step 4: Create an EditableDocument Instance
With the editing options set, create an `EditableDocument` instance. This represents the document in an editable format.
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## Step 5: Edit the Document Content
Retrieve the original text content and make your desired edits. For this example, we'll replace the word "text" with "EDITED text".
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("text", "EDITED text");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## Step 6: Create an EditableDocument with Updated Content
After making the necessary edits, create a new `EditableDocument` with the updated content and the original resources.
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## Step 7: Create WordProcessing Save Options
Prepare the save options for the WordProcessing format. This example uses the DOCM format and specifies the locale.
```csharp
    WordProcessingSaveOptions wordSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm)
    {
        Locale = System.Globalization.CultureInfo.GetCultureInfo("en-GB")
    };
```
## Step 8: Create TXT Saving Options
Similarly, create the saving options for the TXT format. Ensure the encoding is set to UTF-8 and preserve the table layout.
```csharp
    TextSaveOptions txtSaveOptions = new TextSaveOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        PreserveTableLayout = true
    };
```
## Step 9: Prepare Output Paths
Prepare the paths for saving the resultant DOCX and TXT files. Use the input file path to determine the output directory and file names.
```csharp
    string outputWordPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".docm");
    string outputTxtPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".txt");
```
## Step 10: Save the Edited Document
Finally, save the edited document in both the DOCX and TXT formats using the specified save options.
```csharp
    editor.Save(afterEdit, outputWordPath, wordSaveOptions);
    editor.Save(afterEdit, outputTxtPath, txtSaveOptions);
}
System.Console.WriteLine("Document editing process completed successfully!");
```
## Conclusion
Congratulations! You've successfully edited a plain text document using GroupDocs.Editor for .NET. This powerful tool simplifies document editing, making it easy to integrate into your .NET applications. Whether you're handling simple text files or complex document formats, GroupDocs.Editor has you covered. Explore more features and capabilities by visiting the [GroupDocs.Editor documentation](https://reference.groupdocs.com/editor/net/).
## FAQ's
### What file formats does GroupDocs.Editor for .NET support?
GroupDocs.Editor for .NET supports a wide range of file formats, including DOCX, TXT, HTML, and more. Check the [documentation](https://reference.groupdocs.com/editor/net/) for a full list.
### How can I get a free trial of GroupDocs.Editor for .NET?
You can download a free trial of GroupDocs.Editor for .NET from the [releases page](https://releases.groupdocs.com/).
### Can I purchase a temporary license for GroupDocs.Editor for .NET?
Yes, you can obtain a temporary license from the [GroupDocs purchase page](https://purchase.groupdocs.com/temporary-license/).
### Where can I get support for GroupDocs.Editor for .NET?
Support is available through the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).
### Is there detailed documentation available for GroupDocs.Editor for .NET?
Yes, detailed documentation is available on the [GroupDocs.Editor documentation page](https://reference.groupdocs.com/editor/net/).
