---
date: 2026-08-10
description: Leer hoe u platte-tekstbestanden kunt bewerken met GroupDocs.Editor for
  .NET. De gids behandelt het laden van een txt‑bestand, het verwijderen van spaties,
  het instellen van tekstcodering en het opslaan van het resultaat.
keywords:
- edit plain text
- load txt file
- trim trailing spaces
- convert leading spaces
- set text encoding
lastmod: 2026-08-10
linktitle: Werken met platte-tekstdocumenten
og_description: Leer hoe u platte-tekstbestanden kunt bewerken met GroupDocs.Editor
  for .NET – laad txt‑bestand, verwijder afsluitende spaties, converteer leidende
  spaties, stel tekstcodering in en sla efficiënt op.
og_image_alt: Guide showing edit plain text workflow with GroupDocs.Editor for .NET
og_title: Bewerk platte-tekstdocumenten met GroupDocs.Editor for .NET
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
title: Bewerk platte-tekstdocumenten met GroupDocs.Editor for .NET
type: docs
url: /nl/net/document-processing/work-plain-text-documents/
weight: 15
---

# Bewerk platte tekstdocumenten met GroupDocs.Editor voor .NET

## Introductie
Als je snel en betrouwbaar **platte tekst wilt bewerken** in een .NET‑applicatie, is GroupDocs.Editor voor .NET het hulpmiddel dat het zware werk doet. Deze API ondersteunt meer dan 30 documentformaten, kan bestanden tot 500 MB aan, en stelt je in staat tekst te manipuleren zonder het volledige bestand in het geheugen te laden. In deze tutorial leer je hoe je een txt‑bestand laadt, trailing spaces verwijdert, leading spaces converteert, de juiste codering instelt, en uiteindelijk de bewerkte inhoud terug opslaat op schijf. Klaar om praktisch aan de slag te gaan? Laten we duiken!

## Snelle antwoorden
- **Wat is de eerste stap om een txt‑bestand te bewerken?** Laad het bestand met `Editor` met het pad of de stream die je hebt.  
- **Kan ik de bestandscodering wijzigen tijdens het bewerken?** Ja – de `TxtSaveOptions` laten je UTF‑8, UTF‑16 of een aangepaste codering opgeven.  
- **Hoe verwijder ik extra spaties aan het einde van elke regel?** Haal de tekst op, roep `TrimEnd()` aan op elke regel, en schrijf deze terug.  
- **Is GroupDocs.Editor gratis te proberen?** Een volledig functionele proefperiode van 30 dagen is beschikbaar op de releases‑pagina.  
- **Welke .NET‑versies worden ondersteund?** .NET Framework 4.6+, .NET Core 3.1+, en .NET 5/6/7.

## Wat is platte tekst bewerken?
**Platte tekst bewerken** betekent programmatisch de tekens in een eenvoudig `.txt`‑bestand wijzigen — toevoegen, verwijderen of opnieuw formatteren — terwijl de oorspronkelijke codering en regeleinde‑stijl van het bestand behouden blijven. Het kan taken omvatten zoals het verwijderen van witruimte, normaliseren van regeleinden, bijwerken van configuratiewaarden, of het invoegen van gegenereerde inhoud. De bewerking moet het bestand leesbaar houden voor elke standaardteksteditor en eventuele bestaande metadata zoals BOM‑markeringen behouden.

## Waarom GroupDocs.Editor gebruiken voor platte‑tekstbewerking?
GroupDocs.Editor verwerkt bestanden in een streaming‑manier, wat betekent dat het een logbestand van 300 MB kan bewerken met minder dan 50 MB RAM. De bibliotheek ondersteunt **50+ invoer‑ en uitvoerformaten**, detecteert automatisch regeleinde‑stijlen (CR, LF, CRLF), en biedt ingebouwde opties om **trailing spaces** te **trimmen** en **leading spaces** te **converteren** zonder aangepaste parsers te schrijven.

## Vereisten
- **.NET‑ontwikkelomgeving** – Visual Studio 2022 of VS Code met de C#‑extensie.  
- **GroupDocs.Editor voor .NET** – download van de [GroupDocs.Editor for .NET](https://releases.groupdocs.com/editor/net/) releases‑pagina.  
- **Basis C#‑kennis** – je moet vertrouwd zijn met bestand‑I/O en tekenreeksmanipulatie.  
- **Teksteditor (optioneel)** – voor het inspecteren van de bronbestanden; VS Code wordt aanbevolen.  
- Voor gedetailleerd gebruik, zie de [documentation](https://tutorials.groupdocs.com/editor/net/).  
- Je kunt ook de algemene [releases page](https://releases.groupdocs.com/) bekijken.

## Hoe platte tekst stap voor stap bewerken
Laad het bestand, bewerk de inhoud, en sla het terug op — alles in minder dan tien regels code. De volgende secties leiden je door elke fase met duidelijke uitleg.

### Stap 1: Verkrijg een pad naar het invoer‑TXT‑bestand
Bepaal eerst of je werkt met een fysiek bestandspad of een geheugen‑stream. Een pad gebruiken is de meest eenvoudige aanpak voor lokale ontwikkeling.

```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

### Stap 2: Maak een Editor‑instance
`Editor` is de hoofdklasse die een document laadt en bewerkingsmogelijkheden biedt.

```csharp
string inputFilePath = "YourSampleDocument.txt";
```

### Stap 3: Maak TXT‑bewerkingsopties
`TxtEditOptions` configureert hoe platte‑tekstbestanden worden geparseerd en bewerkt, zodat je codering en spatie‑verwerkingsregels kunt instellen.

```csharp
using (Editor editor = new Editor(inputFilePath))
{
```

### Stap 4: Maak een EditableDocument‑instance
`EditableDocument` vertegenwoordigt de in‑memory versie van het geladen document, inclusief de tekst en eventuele gekoppelde bronnen.

```csharp
    TextEditOptions editOptions = new TextEditOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        RecognizeLists = true,
        LeadingSpaces = TextLeadingSpacesOptions.ConvertToIndent,
        TrailingSpaces = TextTrailingSpacesOptions.Trim
    };
```

### Stap 5: Bewerk de documentinhoud
Haal de oorspronkelijke tekst op, pas de benodigde tekenreeks‑bewerkingen toe (bijv. vervangen, trimmen, hoofdletter‑/kleine‑letter wijzigen), en sla het resultaat terug op in de `EditableDocument`.

```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```

### Stap 6: Maak een EditableDocument met bijgewerkte inhoud
Nadat je de tekst hebt getransformeerd, maak je een nieuw `EditableDocument` aan dat de bewerkte tekenreeks en de oorspronkelijke resource‑collectie bevat.

```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("text", "EDITED text");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```

### Stap 7: Maak WordProcessing‑opslaan‑opties
`WordProcessingSaveOptions` definieert instellingen voor het opslaan van het document in een Word‑compatibel formaat zoals DOCX of DOCM.

```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```

### Stap 8: Maak TXT‑opslaan‑opties
`TxtSaveOptions` specificeert hoe het bewerkte platte‑tekstbestand moet worden weggeschreven, inclusief codering, behoud van regeleinden, en afhandeling van tabel‑lay-out.

```csharp
    WordProcessingSaveOptions wordSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm)
    {
        Locale = System.Globalization.CultureInfo.GetCultureInfo("en-GB")
    };
```

### Stap 9: Bereid uitvoer‑paden voor
Bepaal de uitvoermap op basis van het invoer‑bestandspad, en bouw vervolgens de volledige bestandsnamen voor de DOCX‑ en TXT‑resultaten.

```csharp
    TextSaveOptions txtSaveOptions = new TextSaveOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        PreserveTableLayout = true
    };
```

### Stap 10: Sla het bewerkte document op
Roep tenslotte `editor.Save` twee keer aan — eenmaal met de WordProcessing‑opties en eenmaal met de TXT‑opties — om beide formaten in één bewerking te produceren.

```csharp
    string outputWordPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".docm");
    string outputTxtPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".txt");
```

## Veelvoorkomende problemen en oplossingen
- **Trailing spaces blijven na bewerken** – zorg ervoor dat `TxtEditOptions.TrimTrailingSpaces` is ingesteld op `true` vóór het laden van het document.  
- **Onjuiste codering in het opgeslagen bestand** – controleer of `TxtSaveOptions.Encoding` overeenkomt met de gewenste code‑page (bijv. `Encoding.UTF8`).  
- **Grote bestanden veroorzaken OutOfMemoryException** – gebruik de streaming‑API (`Editor.Load(Stream)`) in plaats van laden vanaf een bestandspad om het geheugenverbruik laag te houden.  

## Veelgestelde vragen

**Q: Welke bestandsformaten ondersteunt GroupDocs.Editor voor .NET?**  
A: De bibliotheek ondersteunt 50+ formaten, waaronder DOCX, TXT, HTML, PDF en markdown, waardoor je ze naadloos kunt bewerken en converteren.

**Q: Hoe kan ik een gratis proefversie van GroupDocs.Editor voor .NET krijgen?**  
A: Download de proefversie van de [releases page](https://releases.groupdocs.com/).

**Q: Kan ik een tijdelijke licentie voor testdoeleinden aanschaffen?**  
A: Ja, tijdelijke licenties zijn beschikbaar via de [GroupDocs purchase page](https://purchase.groupdocs.com/temporary-license/).

**Q: Waar kan ik ondersteuning vinden als ik tegen problemen aanloop?**  
A: Het officiële supportforum is de beste plek – bezoek het [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).

**Q: Is er gedetailleerde documentatie voor geavanceerde scenario's?**  
A: Absoluut. De volledige referentie staat op de [GroupDocs.Editor documentation page](https://tutorials.groupdocs.com/editor/net/).

## Conclusie
Je hebt nu geleerd hoe je **platte tekst** bestanden kunt **bewerken** met GroupDocs.Editor voor .NET — een txt‑bestand laden, spaties trimmen, leading spaces converteren, de juiste codering instellen, en het resultaat opslaan in zowel TXT‑ als DOCX‑formaten. Deze mogelijkheid stelt je in staat log‑bestanden automatisch op te schonen, configuratiebestanden on‑the‑fly te genereren, of aangepaste tekst‑verwerkingspijplijnen te bouwen zonder het wiel opnieuw uit te vinden. Ontdek extra functies zoals batchverwerking en documentconversie door de officiële documentatie te bezoeken.

**Laatst bijgewerkt:** 2026-08-10  
**Getest met:** GroupDocs.Editor 23.11 for .NET  
**Auteur:** GroupDocs  

```csharp
    editor.Save(afterEdit, outputWordPath, wordSaveOptions);
    editor.Save(afterEdit, outputTxtPath, txtSaveOptions);
}
System.Console.WriteLine("Document editing process completed successfully!");
```

## Gerelateerde tutorials

- [Document Loading Tutorials met GroupDocs.Editor voor .NET](/editor/net/document-loading/)
- [Document Opslaan en Exporteren Tutorials voor GroupDocs.Editor .NET](/editor/net/document-saving/)
- [Platte tekst en DSV Document Editing Tutorials voor GroupDocs.Editor .NET](/editor/net/plain-text-dsv-documents/)