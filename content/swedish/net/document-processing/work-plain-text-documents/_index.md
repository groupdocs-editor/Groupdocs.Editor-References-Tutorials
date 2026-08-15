---
date: 2026-08-10
description: Lär dig hur du redigerar plain text-filer med GroupDocs.Editor for .NET.
  Guiden täcker inläsning av en txt file, trimming spaces, setting text encoding och
  sparar resultatet.
keywords:
- edit plain text
- load txt file
- trim trailing spaces
- convert leading spaces
- set text encoding
lastmod: 2026-08-10
linktitle: Arbeta med plain text-dokument
og_description: Lär dig hur du redigerar plain text-filer med GroupDocs.Editor for
  .NET – load txt file, trim trailing spaces, convert leading spaces, set text encoding,
  och spara effektivt.
og_image_alt: Guide showing edit plain text workflow with GroupDocs.Editor for .NET
og_title: Redigera plain text-dokument med GroupDocs.Editor for .NET
schemas:
- author: GroupDocs
  dateModified: '2026-08-10'
  description: Learn how to edit plain text files using GroupDocs.Editor for .NET.
    The guide covers loading a txt file, trimming spaces, setting text encoding, and
    saving the result.
  headline: Edit plain text documents with GroupDocs.Editor for .NET
  type: TechArticle
- description: Learn how to edit plain text files using GroupDocs.Editor for .NET.
    The guide covers loading a txt file, trimming spaces, setting text encoding, and
    saving the result.
  name: Edit plain text documents with GroupDocs.Editor for .NET
  steps:
  - name: Get a path to the input TXT file
    text: First, decide whether you’ll work with a physical file path or a memory
      stream. Using a path is the most straightforward approach for local development.
  - name: Create an Editor instance
    text: '`Editor` is the main class that loads a document and provides editing capabilities.'
  - name: Create TXT editing options
    text: '`TxtEditOptions` configures how plain‑text files are parsed and edited,
      allowing you to set encoding and space‑handling rules.'
  - name: Create an EditableDocument instance
    text: '`EditableDocument` represents the in‑memory version of the loaded document,
      including its text and any associated resources.'
  - name: Edit the document content
    text: Retrieve the original text, apply any string operations you need (e.g.,
      replace, trim, change case), and store the result back into the `EditableDocument`.
  - name: Create an EditableDocument with updated content
    text: After you’ve transformed the text, instantiate a new `EditableDocument`
      that contains the edited string and the original resource collection.
  - name: Create WordProcessing save options
    text: '`WordProcessingSaveOptions` defines settings for saving the document in
      a Word‑compatible format such as DOCX or DOCM.'
  - name: Create TXT saving options
    text: '`TxtSaveOptions` specifies how the edited plain‑text file should be written,
      including encoding, line‑ending preservation, and table layout handling.'
  - name: Prepare output paths
    text: Derive the output directory from the input file path, then build the full
      filenames for the DOCX and TXT results.
  - name: Save the edited document
    text: Finally, call `editor.Save` twice—once with the WordProcessing options and
      once with the TXT options—to produce both formats in a single operation.
  type: HowTo
- questions:
  - answer: The library supports 50+ formats, including DOCX, TXT, HTML, PDF, and
      markdown, allowing you to edit and convert between them seamlessly.
    question: What file formats does GroupDocs.Editor for .NET support?
  - answer: Download the trial from the [releases page](https://releases.groupdocs.com/).
    question: How can I get a free trial of GroupDocs.Editor for .NET?
  - answer: Yes, temporary licenses are available through the [GroupDocs purchase
      page](https://purchase.groupdocs.com/temporary-license/).
    question: Can I purchase a temporary license for testing?
  - answer: The official support forum is the best place – visit the [GroupDocs.Editor
      support forum](https://forum.groupdocs.com/c/editor/20).
    question: Where can I find support if I run into issues?
  - answer: Absolutely. The full reference is on the [GroupDocs.Editor documentation
      page](https://tutorials.groupdocs.com/editor/net/).
    question: Is there detailed documentation for advanced scenarios?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
tags:
- edit plain text
- GroupDocs.Editor
- C# document processing
- plain text editing
- txt file handling
title: Redigera plain text-dokument med GroupDocs.Editor for .NET
type: docs
url: /sv/net/document-processing/work-plain-text-documents/
weight: 15
---

# Redigera textdokument med GroupDocs.Editor för .NET

## Introduktion
Om du behöver **redigera vanlig text** snabbt och pålitligt i en .NET-applikation, är GroupDocs.Editor för .NET verktyget som gör det tunga arbetet. Detta API stödjer mer än 30 dokumentformat, kan hantera filer upp till 500 MB, och låter dig manipulera text utan att ladda hela filen i minnet. I den här handledningen kommer du att lära dig hur du laddar en txt‑fil, tar bort efterföljande mellanslag, konverterar inledande mellanslag, ställer in rätt kodning och slutligen sparar det redigerade innehållet tillbaka till disk. Är du redo att börja? Låt oss dyka ner!

## Snabba svar
- **Vad är det första steget för att redigera en txt‑fil?** Ladda filen med `Editor` med den sökväg eller ström du har.  
- **Kan jag ändra filens kodning medan jag redigerar?** Ja – `TxtSaveOptions` låter dig specificera UTF‑8, UTF‑16 eller någon anpassad kodning.  
- **Hur tar jag bort extra mellanslag i slutet av varje rad?** Hämta texten, anropa `TrimEnd()` på varje rad och skriv tillbaka den.  
- **Är GroupDocs.Editor gratis att prova?** En fullt funktionell 30‑dagars provversion finns tillgänglig på releases‑sidan.  
- **Vilka .NET‑versioner stöds?** .NET Framework 4.6+, .NET Core 3.1+, och .NET 5/6/7.

## Vad är redigering av vanlig text?
**Redigera vanlig text** betyder att programatiskt ändra tecknen i en enkel `.txt`‑fil—lägga till, ta bort eller omformatera text—medan filens ursprungliga kodning och radbrytning bevaras. Det kan innebära uppgifter som att trimma blanksteg, normalisera radslut, uppdatera konfigurationsvärden eller infoga genererat innehåll. Operationen bör hålla filen läsbar i vilken standardtextredigerare som helst och bevara eventuell befintlig metadata såsom BOM‑markörer.

## Varför använda GroupDocs.Editor för redigering av vanlig text?
GroupDocs.Editor behandlar filer i ett streaming‑sätt, vilket betyder att den kan redigera en 300 MB loggfil med mindre än 50 MB RAM. Biblioteket stödjer **50+ in‑ och utdataformat**, upptäcker automatiskt radslutsstilar (CR, LF, CRLF) och erbjuder inbyggda alternativ för att **trimma efterföljande mellanslag** och **konvertera inledande mellanslag** utan att skriva egna parsers.

## Förutsättningar
- **.NET‑utvecklingsmiljö** – Visual Studio 2022 eller VS Code med C#‑tillägget.  
- **GroupDocs.Editor för .NET** – ladda ner från [GroupDocs.Editor for .NET](https://releases.groupdocs.com/editor/net/) releases‑sidan.  
- **Grundläggande C#‑kunskaper** – du bör vara bekväm med fil‑I/O och strängmanipulation.  
- **Textredigerare (valfritt)** – för att inspektera källfilerna; VS Code rekommenderas.  
- För detaljerad användning, se [dokumentationen](https://tutorials.groupdocs.com/editor/net/).  
- Du kan också bläddra i den allmänna [releases‑sidan](https://releases.groupdocs.com/).

## Hur man redigerar vanlig text steg för steg
Ladda filen, redigera dess innehåll och spara tillbaka – allt på under tio kodrader. Följande avsnitt guidar dig genom varje steg med tydliga förklaringar.

### Steg 1: Hämta en sökväg till inmatnings‑TXT‑filen
Först, bestäm om du ska arbeta med en fysisk filsökväg eller en minnesström. Att använda en sökväg är det mest enkla tillvägagångssättet för lokal utveckling.

```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

### Steg 2: Skapa en Editor‑instans
`Editor` är huvudklassen som laddar ett dokument och erbjuder redigeringsmöjligheter.

```csharp
string inputFilePath = "YourSampleDocument.txt";
```

### Steg 3: Skapa TXT‑redigeringsalternativ
`TxtEditOptions` konfigurerar hur vanlig‑text‑filer parsas och redigeras, vilket låter dig ange kodning och regler för mellanslagshantering.

```csharp
using (Editor editor = new Editor(inputFilePath))
{
```

### Steg 4: Skapa en EditableDocument‑instans
`EditableDocument` representerar den in‑minnet‑version av det laddade dokumentet, inklusive dess text och eventuella associerade resurser.

```csharp
    TextEditOptions editOptions = new TextEditOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        RecognizeLists = true,
        LeadingSpaces = TextLeadingSpacesOptions.ConvertToIndent,
        TrailingSpaces = TextTrailingSpacesOptions.Trim
    };
```

### Steg 5: Redigera dokumentets innehåll
Hämta den ursprungliga texten, tillämpa de strängoperationer du behöver (t.ex. ersätta, trimma, ändra skiftläge) och lagra resultatet tillbaka i `EditableDocument`.

```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```

### Steg 6: Skapa ett EditableDocument med uppdaterat innehåll
Efter att du har transformerat texten, skapa en ny `EditableDocument` som innehåller den redigerade strängen och den ursprungliga resurskollektionen.

```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("text", "EDITED text");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```

### Steg 7: Skapa WordProcessing‑spara‑alternativ
`WordProcessingSaveOptions` definierar inställningar för att spara dokumentet i ett Word‑kompatibelt format som DOCX eller DOCM.

```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```

### Steg 8: Skapa TXT‑spara‑alternativ
`TxtSaveOptions` specificerar hur den redigerade vanlig‑text‑filen ska skrivas, inklusive kodning, bevarande av radslut och hantering av tabelllayout.

```csharp
    WordProcessingSaveOptions wordSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm)
    {
        Locale = System.Globalization.CultureInfo.GetCultureInfo("en-GB")
    };
```

### Steg 9: Förbered utdata‑sökvägar
Härleda utdata‑katalogen från inmatningsfilens sökväg, och bygg sedan de fullständiga filnamnen för DOCX‑ och TXT‑resultaten.

```csharp
    TextSaveOptions txtSaveOptions = new TextSaveOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        PreserveTableLayout = true
    };
```

### Steg 10: Spara det redigerade dokumentet
Slutligen, anropa `editor.Save` två gånger—en gång med WordProcessing‑alternativen och en gång med TXT‑alternativen—för att producera båda formaten i en enda operation.

```csharp
    string outputWordPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".docm");
    string outputTxtPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".txt");
```

## Vanliga problem och lösningar
- **Efterföljande mellanslag kvarstår efter redigering** – se till att `TxtEditOptions.TrimTrailingSpaces` är satt till `true` innan dokumentet laddas.  
- **Fel kodning i den sparade filen** – verifiera att `TxtSaveOptions.Encoding` matchar önskad kodsida (t.ex. `Encoding.UTF8`).  
- **Stora filer orsakar OutOfMemoryException** – använd streaming‑API:t (`Editor.Load(Stream)`) istället för att ladda från en filsökväg för att hålla minnesanvändningen låg.  

## Vanliga frågor

**Q: Vilka filformat stödjer GroupDocs.Editor för .NET?**  
A: Biblioteket stödjer 50+ format, inklusive DOCX, TXT, HTML, PDF och markdown, vilket låter dig redigera och konvertera mellan dem sömlöst.

**Q: Hur kan jag få en gratis provversion av GroupDocs.Editor för .NET?**  
A: Ladda ner provversionen från [releases‑sidan](https://releases.groupdocs.com/).

**Q: Kan jag köpa en tillfällig licens för testning?**  
A: Ja, tillfälliga licenser finns tillgängliga via [GroupDocs purchase page](https://purchase.groupdocs.com/temporary-license/).

**Q: Var kan jag hitta support om jag stöter på problem?**  
A: Det officiella supportforumet är den bästa platsen – besök [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).

**Q: Finns det detaljerad dokumentation för avancerade scenarier?**  
A: Absolut. Fullständig referens finns på [GroupDocs.Editor documentation page](https://tutorials.groupdocs.com/editor/net/).

## Slutsats
Du har nu lärt dig hur du **redigerar vanlig text**‑filer med GroupDocs.Editor för .NET—laddar en txt‑fil, trimmar mellanslag, konverterar inledande mellanslag, ställer in korrekt kodning och sparar resultatet i både TXT‑ och DOCX‑format. Denna funktionalitet låter dig automatisera rensning av loggfiler, generera konfigurationsfiler i farten eller bygga anpassade text‑bearbetningspipelines utan att uppfinna hjulet på nytt. Utforska ytterligare funktioner som batch‑bearbetning och dokumentkonvertering genom att besöka den officiella dokumentationen.

---

**Senast uppdaterad:** 2026-08-10  
**Testat med:** GroupDocs.Editor 23.11 for .NET  
**Författare:** GroupDocs  

```csharp
    editor.Save(afterEdit, outputWordPath, wordSaveOptions);
    editor.Save(afterEdit, outputTxtPath, txtSaveOptions);
}
System.Console.WriteLine("Document editing process completed successfully!");
```

## Relaterade handledningar

- [Handledningar för dokumentladdning med GroupDocs.Editor för .NET](/editor/net/document-loading/)
- [Handledningar för dokumentlagring och export för GroupDocs.Editor .NET](/editor/net/document-saving/)
- [Handledningar för redigering av vanlig text och DSV‑dokument för GroupDocs.Editor .NET](/editor/net/plain-text-dsv-documents/)