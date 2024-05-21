---
title: Get External CSS Content
linktitle: Get External CSS Content
second_title: GroupDocs.Editor .NET API
description: Learn how to use GroupDocs.Editor for .NET to extract external CSS content from documents with this step-by-step guide. Perfect for developers integrating document.
type: docs
weight: 10
url: /net/css-handling/get-external-css-content/
---
## Introduction
In this article, we'll walk you through everything you need to get started with GroupDocs.Editor for .NET. From setting up your environment to extracting external CSS content from documents, we’ll cover it all. Let's dive right in!
## Prerequisites
Before we begin, make sure you have the following prerequisites in place:
1. .NET Framework: Ensure you have .NET Framework 4.6.1 or later installed.
2. Visual Studio: Install Visual Studio 2017 or later for a seamless development experience.
3. GroupDocs.Editor for .NET: Download the latest version from the [GroupDocs.Editor download page](https://releases.groupdocs.com/editor/net/).
4. Basic Knowledge of C#: Familiarity with C# programming will help you follow along with the examples.
## Import Namespaces
Before diving into the code examples, you need to import the necessary namespaces in your C# project:
```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Editor.Options;
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
```
Now that we have our prerequisites sorted and namespaces imported, let's break down the example code step-by-step.
## Step 1: Initialize the Editor
First, you'll need to initialize the `Editor` object with your sample document. This step sets up the document for editing.
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
    // Proceed to the next steps
}
```
In this snippet, we create an `Editor` instance by providing the document path and a delegate that returns `WordProcessingLoadOptions`. This prepares the document for editing.
## Step 2: Edit the Document
Next, you need to edit the document to get its editable state. This step converts the document into an editable format.
```csharp
using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
{
    // Proceed to the next steps
}
```
Here, we use the `Edit` method of the `Editor` class, passing in `WordProcessingEditOptions` to get an `EditableDocument` object, which represents the document in an editable form.
## Step 3: Get CSS Content
Now, we extract the CSS content from the editable document. This step is crucial as it allows you to access and manipulate the document's styles.
```csharp
List<string> stylesheets = document.GetCssContent();
```
The `GetCssContent` method returns a list of CSS stylesheets present in the document. This list can be used for further processing or analysis.
## Step 4: Output the CSS Content
Finally, let's print the extracted CSS content to the console. This will help you verify the stylesheets retrieved from the document.
```csharp
Console.WriteLine("There are {0} stylesheets in the input document", stylesheets.Count);
foreach (string css in stylesheets)
{
    Console.WriteLine(css);
}
```
In this part, we output the number of stylesheets and their content to the console. This provides a clear view of the CSS used in the document.
## Conclusion
And there you have it! You've successfully extracted external CSS content from a document using GroupDocs.Editor for .NET. This step-by-step guide should help you understand the basics of using this powerful library for your document editing needs. Whether you're integrating it into a larger application or just exploring its capabilities, GroupDocs.Editor offers a robust solution for handling document editing programmatically.
## FAQ's
### What is GroupDocs.Editor for .NET?
GroupDocs.Editor for .NET is a document editing API that allows developers to programmatically edit documents in various formats, including Word, Excel, and PDF, within .NET applications.
### How do I get started with GroupDocs.Editor for .NET?
To get started, you need to download the latest version of the library from the [GroupDocs.Editor download page](https://releases.groupdocs.com/editor/net/), set up your .NET environment, and follow the steps outlined in this guide.
### Can I use GroupDocs.Editor for free?
GroupDocs.Editor offers a free trial which you can download from the [GroupDocs free trial page](https://releases.groupdocs.com/). For full features, consider purchasing a license.
### What file formats does GroupDocs.Editor support?
GroupDocs.Editor supports a wide range of file formats, including DOCX, XLSX, PPTX, PDF, HTML, and many more. Check the [documentation](https://reference.groupdocs.com/editor/net/) for a complete list.
### How do I get support for GroupDocs.Editor?
You can get support from the [GroupDocs support forum](https://forum.groupdocs.com/c/editor/20) where you can ask questions and receive help from the community and GroupDocs experts.
