---
title: Retrieve HTML Content with Prefix
linktitle: Retrieve HTML Content with Prefix
second_title: GroupDocs.Editor .NET API
description: 
type: docs
weight: 11
url: /net/html-content-retrieval/retrieve-html-content-with-prefix/
---

## Complete Source Code
```csharp
using System;
using GroupDocs.Editor.Options;

namespace GroupDocs.Editor.Examples.CSharp.AdvancedUsage.EditableDocumentExamples
{
    class GetHtmlContentWithPrefix
    {
        internal static void Run()
        {
            using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
            {
                using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
                {
                    string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
                    string externalCssPrefix = "http://www.mywebsite.com/css/id=";
                    string prefixedHtmlContent = document.GetContent(externalImagesPrefix, externalCssPrefix);
                    Console.WriteLine("HTML content of the input document with custom image and stylesheet prefixes: {0}", prefixedHtmlContent);
                }
            }
        }
    }
}
```
