---
title: Save Edited Document to Various Formats
linktitle: Save Edited Document to Various Formats
second_title: GroupDocs.Editor .NET API
description: 
type: docs
weight: 11
url: /net/document-processing/save-edited-document-various-formats/
---

## Complete Source Code
```csharp
namespace GroupDocs.Editor.Examples.CSharp.AdvancedUsage
{
    /// <summary>
    /// This example demonstrates opening an input DOCX document, editing its content and saving in multiple documents of all supportable formats
    /// </summary>
    internal static class SavingEditedDocumentToAllFormats
    {
        internal static void Run()
        {
            //1. Get a path to the input WordProcessing file (or stream with file content)
            string inputFilePath = "Your Sample Document";

            //2. Create load options for this document
            Options.WordProcessingLoadOptions loadOptions = new Options.WordProcessingLoadOptions();

            //3. Load document with options to the Editor instance
            using (Editor editor = new Editor(inputFilePath, delegate { return loadOptions; }))
            {
                //4. Create editing options
                Options.WordProcessingEditOptions editOptions = new Options.WordProcessingEditOptions();

                //5. Open document for editing by creating intermediate EditableDocument instance
                using (EditableDocument beforeEdit = editor.Edit(editOptions))
                {
                    //6.1. Get document as a single base64-encoded string, where all resources (images, fonts, etc) are embedded inside this string along with main textual content
                    string allEmbeddedInsideString = beforeEdit.GetEmbeddedHtml();
                    //6.2. For example, edit its content somehow
                    string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");

                    //7. Create new EditableDocument instance from edited content and resources
                    using (EditableDocument afterEdit = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null)
                    )
                    {
                        //8. Iterate over all supportable WordProcessing formats and save a document in some of this format at one step
                        foreach (Formats.WordProcessingFormats oneFormat in Formats.WordProcessingFormats.All)
                        {
                            //8.1. Prepare option class
                            Options.WordProcessingSaveOptions saveOptions = new Options.WordProcessingSaveOptions(oneFormat);

                            //8.2. Prepare save path
                            string savePath = System.IO.Path.Combine(Constants.GetOutputDirectoryPath("Your Sample Document"), "MultipleOutFormats." + saveOptions.OutputFormat.Extension);

                            //8.3. Save to this path using save options
                            editor.Save(afterEdit, savePath, saveOptions);
                        }
                    }
                }
            }
            System.Console.WriteLine("SavingEditedDocumentToAllFormats routine has successfully finished");
        }
    }
}
```
