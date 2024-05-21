---
title: Save HTML Resources to Folder
linktitle: Save HTML Resources to Folder
second_title: GroupDocs.Editor .NET API
description: Learn how to extract HTML resources from documents using Groupdocs.Editor for .NET. This comprehensive tutorial provides step-by-step guidance for developers.
type: docs
weight: 13
url: /net/document-editing/save-html-resources-to-folder/
---
## Introduction
Groupdocs.Editor for .NET is a powerful tool that enables developers to manipulate and convert documents within their .NET applications seamlessly. Whether you need to extract HTML resources from a document or perform advanced editing tasks, Groupdocs.Editor simplifies the process with its intuitive API and extensive documentation.
## Prerequisites
Before diving into the tutorial, ensure you have the following prerequisites:
1. Basic Knowledge of C# and .NET: Familiarity with C# programming language and .NET framework is essential to follow along with the examples.
2. Groupdocs.Editor for .NET Library: Download and install Groupdocs.Editor for .NET library from the [website](https://releases.groupdocs.com/editor/net/).
3. Development Environment: Set up your preferred development environment such as Visual Studio or any other compatible IDE.

## Import Namespaces
To get started, import the necessary namespaces in your C# project:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
```
##Now, let's break down the process of saving HTML resources to a folder using Groupdocs.Editor for .NET into multiple steps:
## Step 1: Initialize Groupdocs.Editor
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
First, initialize the `Editor` object by providing the path to your sample document. In this example, we're using a Word document, so we specify `WordProcessingLoadOptions` as the document type.
## Step 2: Edit Document
```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
Next, create an `EditableDocument` object by calling the `Edit` method of the `Editor` object. This allows you to perform editing operations on the document.
## Step 3: Extract Resources
```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
Extract resources such as images, fonts, and stylesheets from the document and store them in respective lists.
## Step 4: Specify Output Folder
```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
Define the output folder where the extracted resources will be saved. You can customize the folder path as per your requirement.
## Step 5: Save Resources
```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
Loop through each image resource, save it to the output folder, and display relevant information such as filename, type, and dimensions.
```csharp
		foreach (FontResourceBase oneFont in fonts)
		{
			Console.WriteLine("Saving {0} of {1} type",
				oneFont.FilenameWithExtension, oneFont.Type.FormalName);
			oneFont.Save(Path.Combine(outputFolder, oneFont.FilenameWithExtension));
		}
```
Similarly, save each font resource to the output folder.
```csharp
		foreach (CssText oneStylesheet in stylesheets)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} encoding",
				oneStylesheet.FilenameWithExtension, oneStylesheet.Type.FormalName, oneStylesheet.Encoding);
			oneStylesheet.Save(Path.Combine(outputFolder, oneStylesheet.FilenameWithExtension));
		}
	}
}
```
Finally, save each stylesheet to the output folder and complete the editing process.

## Conclusion
In conclusion, Groupdocs.Editor for .NET provides a convenient solution for managing and manipulating documents programmatically within .NET applications. By following this tutorial, you can easily extract HTML resources from documents and customize the process according to your specific requirements.
## FAQ's
### Is Groupdocs.Editor compatible with other document formats besides Word?
Yes, Groupdocs.Editor supports a wide range of document formats including Excel, PowerPoint, PDF, and more.
### Can I integrate Groupdocs.Editor into my web application?
Absolutely, Groupdocs.Editor offers seamless integration with web applications developed on the .NET framework.
### Does Groupdocs.Editor provide support for cloud storage services?
Yes, Groupdocs.Editor supports integration with popular cloud storage services like Google Drive, Dropbox, and Microsoft OneDrive.
### Is there a free trial available for Groupdocs.Editor?
Yes, you can avail of a free trial of Groupdocs.Editor from the website.
### How can I get technical support for Groupdocs.Editor?
For technical assistance and community support, you can visit the Groupdocs.Editor forum.
