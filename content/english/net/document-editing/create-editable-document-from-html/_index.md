---
title: Create Editable Document from HTML
linktitle: Create Editable Document from HTML
second_title: GroupDocs.Editor .NET API
description: 
type: docs
weight: 10
url: /net/document-editing/create-editable-document-from-html/
---

## Complete Source Code
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;

namespace GroupDocs.Editor.Examples.CSharp.AdvancedUsage.EditableDocumentExamples
{
    /// <summary>
    /// This example demonstrates, how to open EditableDocument from HTML file with resource folder from disk and save it as DOCX
    /// </summary>
    class CreateEditableDocumentFromHtmlFile
    {
        internal static void Run()
        {
            string htmlFilePath = "Your Sample Document";
            using (EditableDocument document = EditableDocument.FromFile(htmlFilePath, null))
            {
                using (Editor editor = new Editor(htmlFilePath))
                {
                    Options.WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docx);
                    string savePath = Path.Combine(Constants.GetOutputDirectoryPath(htmlFilePath), Path.GetFileNameWithoutExtension(htmlFilePath) + ".docx");
                    editor.Save(document, savePath, saveOptions);
                }
            }
        }
    }
}
```
