---
title: Retrieve HTML Content with Prefix
linktitle: Retrieve HTML Content with Prefix
second_title: GroupDocs.Editor .NET API
description: Learn how to retrieve HTML content from documents using GroupDocs.Editor for .NET with custom prefixes for images and stylesheets. Step-by-step guide included.
type: docs
weight: 11
url: /net/html-content-retrieval/retrieve-html-content-with-prefix/
---
## Introduction
Welcome to our step-by-step tutorial on how to retrieve HTML content from a document using GroupDocs.Editor for .NET. Whether you’re a seasoned developer or just getting started, this guide will walk you through the process in an easy-to-follow manner. We'll cover everything you need to know, from setting up your environment to executing the code successfully. Let's dive in!
## Prerequisites
Before we start, make sure you have the following prerequisites in place:
1. GroupDocs.Editor for .NET: Download the latest version from the [download page](https://releases.groupdocs.com/editor/net/).
2. Development Environment: Visual Studio or any other preferred .NET development environment.
3. Basic Knowledge of C#: Familiarity with C# programming will help you follow along with the examples.
4. Document to Edit: Have a sample document ready for testing, such as a Word document.
5. .NET Framework: Ensure you have .NET Framework installed on your machine.
Now that you have everything ready, let's get started!
## Import Namespaces
First, you need to import the necessary namespaces in your C# project. These namespaces provide the classes and methods required to work with GroupDocs.Editor for .NET.
```csharp
using System;
using GroupDocs.Editor.Options;
```
With the namespaces imported, we can move on to setting up the editor.
## Step 1: Initialize the Editor
To begin, you need to initialize the `Editor` class with your document. This step involves specifying the document you want to edit and providing the necessary load options.
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
    // Further steps will be added here
}
```
In this example, we are loading a Word document. You can replace `"Your Sample Document"` with the path to your document.
## Step 2: Edit the Document
Next, we need to open the document for editing. This is done using the `Edit` method of the `Editor` class, which requires `WordProcessingEditOptions` as an argument.
```csharp
using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
{
    // Further steps will be added here
}
```
The `EditableDocument` instance represents the document in an editable format. Now we are ready to retrieve the HTML content.
## Step 3: Define Custom Prefixes
To add custom prefixes for images and CSS, we need to define the prefixes as strings. This step ensures that the HTML content will have the specified prefixes for external resources.
```csharp
string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
string externalCssPrefix = "http://www.mywebsite.com/css/id=";
```
You can replace the URLs with your desired prefixes. These prefixes will be used in the next step to customize the HTML output.
## Step 4: Retrieve HTML Content
Now that we have our prefixes set, we can retrieve the HTML content from the document. The `GetContent` method of the `EditableDocument` class allows us to specify the image and CSS prefixes.
```csharp
string prefixedHtmlContent = document.GetContent(externalImagesPrefix, externalCssPrefix);
Console.WriteLine("HTML content of the input document with custom image and stylesheet prefixes: {0}", prefixedHtmlContent);
```
This code snippet fetches the HTML content with the custom prefixes and prints it to the console. You can further process or save this HTML content as needed.
## Conclusion
And there you have it! By following these steps, you can easily retrieve HTML content from a document using GroupDocs.Editor for .NET, complete with custom prefixes for images and stylesheets. This powerful tool simplifies document manipulation, allowing you to focus on integrating document editing into your .NET applications seamlessly.
For more detailed information, check out the [GroupDocs.Editor for .NET documentation](https://reference.groupdocs.com/editor/net/). If you have any questions or need further assistance, feel free to reach out on the [support forum](https://forum.groupdocs.com/c/editor/20).
## FAQ's
### What types of documents can I edit with GroupDocs.Editor for .NET?
GroupDocs.Editor supports various document formats including Word, Excel, PowerPoint, PDF, and more.
### How do I get a free trial of GroupDocs.Editor for .NET?
You can get a free trial from the [GroupDocs website](https://releases.groupdocs.com/).
### Can I customize the HTML content further?
Yes, you can modify the retrieved HTML content as needed before rendering or saving it.
### Is it possible to use GroupDocs.Editor for .NET with other .NET languages?
Yes, you can use it with any .NET compatible language like VB.NET or F#.
### How do I obtain a temporary license for GroupDocs.Editor for .NET?
You can get a temporary license from the [purchase page](https://purchase.groupdocs.com/temporary-license/).
