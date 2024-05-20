---
title: Retrieve HTML Body Content
linktitle: Retrieve HTML Body Content
second_title: GroupDocs.Editor .NET API
description: 
type: docs
weight: 10
url: /net/html-content-retrieval/retrieve-html-body-content/
---

## Complete Source Code
```csharp
using System;
using GroupDocs.Editor.Options;

namespace GroupDocs.Editor.Examples.CSharp.AdvancedUsage.EditableDocumentExamples
{
    class GetHtmlBodyContent
    {
        internal static void Run()
        {
            using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
            {
                using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
                {
                    string bodyContent = document.GetBodyContent();
                    Console.WriteLine("Inner content of the HTML->BODY element: {0}", bodyContent);
                }
            }
        }
    }
}
```
