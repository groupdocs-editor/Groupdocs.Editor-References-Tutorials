---
title: Create Document
linktitle: Create Document
second_title: GroupDocs.Editor .NET API
description: Learn how to edit Word, Excel, PowerPoint, Ebook, and Email documents using GroupDocs.Editor for .NET with this comprehensive step-by-step tutorial.
weight: 10
url: /net/document-editing/create-document/
---
## Introduction
Are you tired of the hassle that comes with editing different document types programmatically? GroupDocs.Editor for .NET is here to simplify the process. This powerful tool allows developers to edit various document formats such as Word, Excel, PowerPoint, Ebooks, and Emails with ease. In this tutorial, we’ll dive deep into how to use GroupDocs.Editor for .NET to create and edit documents. We’ll break down the process into easy-to-follow steps, making it accessible even if you're new to this.
## Prerequisites
Before we start, ensure you have the following:
- Visual Studio installed on your machine.
- .NET Framework (4.0 or higher).
- GroupDocs.Editor for .NET library. You can download it from [here](https://releases.groupdocs.com/editor/net/).
- Basic knowledge of C# programming.
## Import Namespaces
First, let's import the necessary namespaces. This will make the required classes and methods accessible in our application.
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using System.IO;
```
## Step 1: Setting Up the Stream
To begin with, we need to set up a memory stream that will act as our placeholder for the document content.
```csharp
Stream memoryStream = Stream.Null;
```
## Step 2: Callback Function to Save the Document
Next, define a callback function that will save the new document stream. This function is essential for handling the output of the document editing process.
```csharp
void SaveNewDocument(Stream resultStream)
{
    memoryStream = resultStream;
}
```
## Step 3: Creating and Editing a WordProcessing Document
Now, let’s create and edit a Word document. We’ll start by creating a new `Editor` instance for WordProcessing documents and edit it with default options.
### Create and Edit with Default Options
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    EditableDocument defaultWordProcessingDoc = editor.Edit();
}
```
### Create and Edit with Custom Options
For more control, we can specify options like disabling pagination and extracting embedded fonts.
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    WordProcessingEditOptions wordProcessingEditOptions = new WordProcessingEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true,
        FontExtraction = FontExtractionOptions.ExtractAllEmbedded
    };
    EditableDocument editableWordProcessingDocument = editor.Edit(wordProcessingEditOptions);
}
```
## Step 4: Creating and Editing a Spreadsheet Document
Similarly, we can create and edit an Excel document. Here’s how you do it.
### Create and Edit with Default Options
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    EditableDocument defaultEditableSpreadsheetDocument = editor.Edit();
}
```
### Create and Edit with Custom Options
To target specific worksheets or exclude hidden ones, we use `SpreadsheetEditOptions`.
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    SpreadsheetEditOptions spreadsheetEditOptions = new SpreadsheetEditOptions
    {
        WorksheetIndex = 0,
        ExcludeHiddenWorksheets = true
    };
    EditableDocument editableSpreadsheetDocument = editor.Edit(spreadsheetEditOptions);
}
```
## Step 5: Creating and Editing a Presentation Document
PowerPoint presentations are also supported. Let’s see how to handle them.
### Create and Edit with Default Options
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    EditableDocument defaultEditablePresentationDocument = editor.Edit();
}
```
### Create and Edit with Custom Options
You can customize your edits by specifying options such as which slide to show and whether to include hidden slides.
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    PresentationEditOptions presentationEditOptions = new PresentationEditOptions
    {
        ShowHiddenSlides = false,
        SlideNumber = 0
    };
    EditableDocument editablePresentationDocument = editor.Edit(presentationEditOptions);
}
```
## Step 6: Creating and Editing an Ebook Document
GroupDocs.Editor also allows for editing Ebook formats like EPUB. Here’s how you can handle it.
### Create and Edit with Default Options
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EditableDocument defaultEditableEbookDocument = editor.Edit();
}
```
### Create and Edit with Custom Options
Customize your Ebook editing by enabling or disabling pagination and language information.
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EbookEditOptions ebookEditOptions = new EbookEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true
    };
    EditableDocument editableEbookDocument = editor.Edit(ebookEditOptions);
}
```
## Step 7: Creating and Editing an Email Document
Finally, we’ll look at how to edit email documents. This includes formats like EML.
### Create and Edit with Default Options
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EditableDocument defaultEditableEmailDocument = editor.Edit();
}
```
### Create and Edit with Custom Options
Specify mail message output options to control the editing process.
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EmailEditOptions emailEditOptions = new EmailEditOptions
    {
        MailMessageOutput = MailMessageOutput.All
    };
    EditableDocument editableEmailDocument = editor.Edit(emailEditOptions);
}
```
## Step 8: Finalizing the Process
After editing the documents, it’s crucial to dispose of the memory stream properly to free up resources.
```csharp
memoryStream.Dispose();
System.Console.WriteLine("CreateDocument routine has successfully finished");
```
## Conclusion
GroupDocs.Editor for .NET is a versatile and powerful tool that can simplify the task of editing various document types programmatically. By following this step-by-step guide, you can create and edit documents with ease, whether they are WordProcessing files, spreadsheets, presentations, ebooks, or emails. Dive into the GroupDocs.Editor documentation for more advanced features and customization options.
## FAQ's
### What types of documents can I edit with GroupDocs.Editor for .NET?
You can edit a wide range of documents, including WordProcessing, spreadsheets, presentations, ebooks, and emails.
### Is it possible to customize the editing options?
Yes, GroupDocs.Editor for .NET allows for extensive customization through various editing options specific to each document type.
### How do I handle the output of the edited documents?
You can use a callback function to save the edited document stream to your desired location.
### Do I need a license to use GroupDocs.Editor for .NET?
Yes, you can obtain a license from [here](https://purchase.groupdocs.com/buy). There is also an option for a temporary license.
### Where can I find more detailed documentation?
Detailed documentation is available on the [GroupDocs.Editor for .NET documentation page](https://tutorials.groupdocs.com/editor/net/).
