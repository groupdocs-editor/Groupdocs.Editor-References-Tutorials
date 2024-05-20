---
title: Get External CSS Content
linktitle: Get External CSS Content
second_title: GroupDocs.Editor .NET API
description: 
type: docs
weight: 10
url: /net/css-handling/get-external-css-content/
---

## Complete Source Code
```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Editor.Options;

namespace GroupDocs.Editor.Examples.CSharp.AdvancedUsage.EditableDocumentExamples
{
    class GetExternalCssContent
    {
        internal static void Run()
        {
            using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
            {
                using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
                {
                    List<string> stylesheets = document.GetCssContent();
                    Console.WriteLine("There are {0} stylesheets in the input document", stylesheets.Count);
                    foreach (string css in stylesheets)
                    {
                        Console.WriteLine(css);
                    }
                }
            }
        }
    }
}
```
