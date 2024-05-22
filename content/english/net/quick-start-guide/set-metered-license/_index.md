---
title: Set Metered License
linktitle: Set Metered License
second_title: GroupDocs.Editor .NET API
description: Learn how to integrate and use GroupDocs.Editor for .NET with our comprehensive guide. Unlock powerful document editing features within your .NET applications.
type: docs
weight: 12
url: /net/quick-start-guide/set-metered-license/
---
## Introduction
Welcome to our step-by-step guide on using GroupDocs.Editor for .NET! Whether you're a seasoned developer or just starting, this tutorial will help you harness the full potential of this powerful library. GroupDocs.Editor for .NET allows you to edit documents of various formats within your .NET applications effortlessly. Let's dive in and explore how you can get started with this robust tool.
## Prerequisites
Before we jump into the technical details, make sure you have the following prerequisites:
- Basic knowledge of .NET programming: Familiarity with C# and .NET Framework.
- Visual Studio installed: Ensure you have the latest version of Visual Studio installed on your machine.
- GroupDocs.Editor for .NET: Download the library from the [download page](https://releases.groupdocs.com/editor/net/).
- A valid license: Obtain a temporary or full license from the [GroupDocs purchase page](https://purchase.groupdocs.com/temporary-license/).
## Import Namespaces
To use GroupDocs.Editor for .NET, you'll need to import the necessary namespaces in your project. This step is crucial as it sets up your project to utilize the library's functionalities.
```csharp
using System;
```
Let's break down each example into multiple steps to ensure you can follow along easily.
## Step 1: Install GroupDocs.Editor for .NET
First things first, you need to install GroupDocs.Editor for .NET in your project. You can do this via NuGet Package Manager in Visual Studio.
### Install via NuGet Package Manager
1. Open your project in Visual Studio.
2. Go to `Tools` > `NuGet Package Manager` > `Manage NuGet Packages for Solution`.
3. Search for `GroupDocs.Editor`.
4. Click on `Install`.
This will add the necessary references to your project.
## Step 2: Set Up a Metered License
To unlock the full features of GroupDocs.Editor, you'll need to set up a metered license. This allows you to use the API without any limitations.
### Setting the Metered License
1. Obtain your public and private keys from the [GroupDocs purchase page](https://purchase.groupdocs.com/temporary-license/).
2. Add the following code to your project to set the metered license:
```csharp
string publicKey = "*****";
string privateKey = "*****";
Metered metered = new Metered();
metered.SetMeteredKey(publicKey, privateKey);
Console.WriteLine("License set successfully.");
```
## Step 3: Load and Edit a Document
Now that your project is set up and licensed, let's move on to loading and editing a document.
### Loading a Document
1. Add the following code to load a document:
```csharp
string filePath = "sample.docx";
Editor editor = new Editor(filePath);
Console.WriteLine("Document loaded successfully.");
```
### Editing the Document
2. To edit the document, you need to convert it to an editable format:
```csharp
EditableDocument editableDocument = editor.Edit();
string content = editableDocument.GetContent();
Console.WriteLine("Document converted to editable format.");
```
## Step 4: Save the Edited Document
Once you have edited the document, the final step is to save your changes.
### Saving the Document
1. Convert the edited content back to the original format:
```csharp
string updatedContent = "<html><body>Updated content</body></html>";
editableDocument = EditableDocument.FromMarkup(updatedContent, new WordProcessingSaveOptions());
editor.Save(editableDocument, "updated_sample.docx");
Console.WriteLine("Document saved successfully.");
```
## Conclusion
Congratulations! You've successfully integrated and used GroupDocs.Editor for .NET in your application. From installing the library to setting up a metered license and editing documents, you've covered all the essential steps. This powerful tool can significantly streamline your document editing workflows within your .NET applications. For further information, refer to the [GroupDocs.Editor for .NET documentation](https://reference.groupdocs.com/editor/net/).
## FAQ's
### How do I obtain a GroupDocs.Editor license?
You can obtain a license from the [GroupDocs purchase page](https://purchase.groupdocs.com/buy). For a temporary license, visit [here](https://purchase.groupdocs.com/temporary-license/).
### Can I try GroupDocs.Editor for free?
Yes, you can download a free trial from the [download page](https://releases.groupdocs.com/) and request a temporary license.
### What document formats are supported by GroupDocs.Editor?
GroupDocs.Editor supports various formats including DOCX, PPTX, XLSX, TXT, HTML, and more. For a full list, check the [documentation](https://reference.groupdocs.com/editor/net/).
### Is there any community support available for GroupDocs.Editor?
Yes, you can get community support from the [GroupDocs.Editor forum](https://forum.groupdocs.com/c/editor/20).
### How do I get started with GroupDocs.Editor for .NET?
Follow our step-by-step guide to set up the library, obtain a license, and start editing documents. For detailed instructions, visit the [documentation](https://reference.groupdocs.com/editor/net/).
