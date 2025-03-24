---
title: Fix Invalid Form Field Collection and Save
linktitle: Fix Invalid Form Field Collection and Save
second_title: GroupDocs.Editor .NET API
description: Learn how to fix invalid form fields in DOCX using Groupdocs.Editor for .NET. Follow this guide to ensure your documents are error-free and save them securely.
weight: 11
url: /net/form-field-management/fix-invalid-form-field-collection-save/
---

# Fix Invalid Form Field Collection and Save

## Introduction
Welcome! If you're working with form fields in documents and facing issues with invalid form field collections, you're in the right place. In this tutorial, we'll dive into how to fix invalid form fields and save your document using Groupdocs.Editor for .NET. We'll guide you through the process step-by-step, ensuring you have all the details you need to make it work seamlessly. Let's get started!
## Prerequisites
Before we jump into the code, there are a few things you need to have in place:
- Groupdocs.Editor for .NET: Make sure you have installed the Groupdocs.Editor library for .NET. You can download it [here](https://releases.groupdocs.com/editor/net/).
- Development Environment: You should have a .NET development environment set up, such as Visual Studio.
- Basic Knowledge of C#: This tutorial assumes you have a basic understanding of C# programming.
## Import Namespaces
First, you need to import the necessary namespaces in your C# project. Add the following lines at the beginning of your code file:
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System;
using System.IO;
```
## Step 1: Get the Input File Path
The first step is to specify the path to your input file. This file should be a DOCX document containing form fields.
```csharp
string inputFilePath = Constants.SampleLegacyFormFields_docx;
```
## Step 2: Create a Stream from the File Path
Next, create a file stream to read the input document. This will allow you to load the document into the editor.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
```
## Step 3: Create Load Options for the Document
In this step, you need to create load options for your document. If your document is password-protected, you can specify the password. In this example, the document is not protected, so the password is ignored.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
loadOptions.Password = "some_password_to_open_a_document";
```
## Step 4: Load the Document into the Editor Instance
Now, load the document with the specified options into the Editor instance. This is where the main operations on the document will take place.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
```
## Step 4.1: Read the FormFieldManager Instance
The `FormFieldManager` instance is responsible for managing form fields in the document. You'll need to read this instance to access and manipulate the form fields.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
## Step 4.2: Read the FormFieldCollection
The `FormFieldCollection` contains all the form fields in the document. You'll read this collection to check and fix invalid form fields.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
## Step 4.3: Auto-Fix Invalid Form Fields
Attempt to auto-fix any invalid form fields in the document. This is a preliminary step to address obvious issues.
```csharp
fieldManager.FixInvalidFormFieldNames(new InvalidFormField[0]);
collection = fieldManager.FormFieldCollection;
```
## Step 4.4: Check for Invalid Form Fields
Check if there are any invalid form fields remaining after the auto-fix attempt.
```csharp
bool hasInvalidFormFields = fieldManager.HasInvalidFormFields();
Console.WriteLine("FormFieldCollection contains invalid items: {0}", hasInvalidFormFields);
```
## Step 4.4.1: Get All Invalid Form Field Names
Retrieve the names of all invalid form fields. These names will be used to fix the fields.
```csharp
var invalidFormFields = fieldManager.GetInvalidFormFieldNames();
```
## Step 4.4.2: Create Unique Names for Invalid Fields
For each invalid form field, create a unique name. This ensures that there are no conflicts with existing form field names.
```csharp
foreach (var invalidItem in invalidFormFields)
{
    invalidItem.FixedName = string.Format("{0}_{1}", invalidItem.Name, Guid.NewGuid());
}
```
## Step 4.4.3: Fix Invalid Form Fields
Fix the invalid form fields using the unique names created in the previous step.
```csharp
fieldManager.FixInvalidFormFieldNames(invalidFormFields);
collection = fieldManager.FormFieldCollection;
```
## Step 5: Create Document Save Options
Set up options for saving the document. This includes specifying the format and any additional save settings.
```csharp
WordProcessingFormats docFormat = WordProcessingFormats.Docx;
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(docFormat);
```
## Step 5.1: Optimize Memory Usage
If your document is large and might cause an `OutOfMemoryException`, enable the memory optimization option.
```csharp
saveOptions.OptimizeMemoryUsage = true;
```
## Step 5.2: Protect the Document from Writing
To protect the document from being modified, except for the form fields, set a protection password.
```csharp
saveOptions.Protection = new WordProcessingProtection(WordProcessingProtectionType.AllowOnlyFormFields, "write_password");
```
## Step 6: Save the Document
Finally, save the document with the specified save options. Prepare a memory stream for saving the output document.
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(outputStream, saveOptions);
}
Console.WriteLine("FixInvalidFormFieldCollectionAndSave routine has successfully finished");
```
## Conclusion
And there you have it! You've successfully fixed invalid form fields and saved your document using Groupdocs.Editor for .NET. This step-by-step guide should have made the process clear and manageable. If you run into any issues or have questions, feel free to check the [documentation](https://tutorials.groupdocs.com/editor/net/) or reach out to [support](https://forum.groupdocs.com/c/editor/20).
## FAQ's
### What if my document is password-protected?
You can specify the password in the `WordProcessingLoadOptions` to open the document.
### How do I know if there are invalid form fields?
Use the `HasInvalidFormFields` method to check for any invalid form fields in the document.
### Can I fix form fields without changing their names?
It's recommended to create unique names for invalid form fields to avoid conflicts.
### What formats can I save the document in?
You can save the document in various formats like DOCX, PDF, and more by setting the appropriate `WordProcessingFormats`.
### How can I optimize memory usage while saving large documents?
Enable the `OptimizeMemoryUsage` option in the `WordProcessingSaveOptions` to handle large documents efficiently.
