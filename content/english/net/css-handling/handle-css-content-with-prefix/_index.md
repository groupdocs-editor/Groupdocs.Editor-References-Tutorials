---
title: Handle CSS Content with Prefix
linktitle: Handle CSS Content with Prefix
second_title: GroupDocs.Editor .NET API
description: 
type: docs
weight: 11
url: /net/css-handling/handle-css-content-with-prefix/
---

## Complete Source Code
```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Editor.Options;

namespace GroupDocs.Editor.Examples.CSharp.AdvancedUsage.EditableDocumentExamples
{
    class GetExternalCssContentWithPrefix
    {
        internal static void Run()
        {
            using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
            {
                using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
                {
                    string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
                    string externalFontsPrefix = "http://www.mywebsite.com/fonts/id=";
                    List<string> stylesheets = document.GetCssContent(externalImagesPrefix, externalFontsPrefix);
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
