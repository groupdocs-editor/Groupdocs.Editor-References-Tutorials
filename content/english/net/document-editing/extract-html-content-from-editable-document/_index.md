---
title: Extract HTML Content from Editable Document
linktitle: Extract HTML Content from Editable Document
second_title: GroupDocs.Editor .NET API
description: 
type: docs
weight: 12
url: /net/document-editing/extract-html-content-from-editable-document/
---

## Complete Source Code
```csharp
using System;
using System.IO;
using GroupDocs.Editor.Options;

namespace GroupDocs.Editor.Examples.CSharp.AdvancedUsage.EditableDocumentExamples
{
    class GetHtmlContent
    {
        internal static void Run()
        {
            using (FileStream fs = File.OpenRead(Constants.SAMPLE_DOCX))
            {
                using (Editor editor = new Editor(delegate { return fs; }, delegate { return new WordProcessingLoadOptions(); }))
                {
                    using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
                    {
                        string htmlContent = document.GetContent();
                        Console.WriteLine("HTML content of the input document (first 200 chars): {0}", htmlContent.Substring(0, 200));
                    }
                }
            }
        }
    }
}
```
