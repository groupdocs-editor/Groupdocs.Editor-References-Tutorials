---
date: 2026-06-06
description: Leer hoe u ondersteunde documentformaten kunt weergeven en de bestandsextensie
  kunt bepalen met GroupDocs.Editor voor .NET. Stapsgewijze gids met codefragmenten,
  snelle antwoorden en veelgestelde vragen.
keywords:
- list supported document formats
- determine file format extension
- GroupDocs.Editor .NET
- document editing API
- supported formats guide
linktitle: Lijst ondersteunde documentformaten
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to list supported document formats and determine file format
    extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets,
    quick answers, and FAQs.
  headline: List Supported Document Formats with GroupDocs.Editor .NET
  type: TechArticle
- description: Learn how to list supported document formats and determine file format
    extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets,
    quick answers, and FAQs.
  name: List Supported Document Formats with GroupDocs.Editor .NET
  steps:
  - name: '**.NET development environment** – Visual Studio 2022 or any IDE that supports
      .NET 6+.'
    text: '**.NET development environment** – Visual Studio 2022 or any IDE that supports
      .NET 6+.'
  - name: '**GroupDocs.Editor for .NET library** – download from the [GroupDocs releases
      page](https://releases.groupdocs.com/editor/net/).'
    text: '**GroupDocs.Editor for .NET library** – download from the [GroupDocs releases
      page](https://releases.groupdocs.com/editor/net/).'
  - name: '**Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/)
      for unrestricted access.'
    text: '**Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/)
      for unrestricted access.'
  - name: '**Basic C# knowledge** – familiarity with namespaces, `using` statements,
      and console output.'
    text: '**Basic C# knowledge** – familiarity with namespaces, `using` statements,
      and console output.'
  - name: '**Loop Through Formats:** We iterate over all available Word‑processing
      formats.'
    text: '**Loop Through Formats:** We iterate over all available Word‑processing
      formats.'
  - name: '**Output Format Details:** For each format we print its friendly name and
      default file extension.'
    text: '**Output Format Details:** For each format we print its friendly name and
      default file extension.'
  - name: '**Loop Through Formats:** The same looping logic applies to presentations.'
    text: '**Loop Through Formats:** The same looping logic applies to presentations.'
  - name: '**Output Format Details:** The name and extension are displayed for each
      format.'
    text: '**Output Format Details:** The name and extension are displayed for each
      format.'
  - name: '**Parse Format:** `FromExtension` converts the `.xlsm` extension into its
      internal `SpreadsheetFormat` enum.'
    text: '**Parse Format:** `FromExtension` converts the `.xlsm` extension into its
      internal `SpreadsheetFormat` enum.'
  - name: '**Output Format:** The parsed format’s name is printed, confirming the
      mapping.'
    text: '**Output Format:** The parsed format’s name is printed, confirming the
      mapping.'
  type: HowTo
- questions:
  - answer: '`DocumentFormatInfo` provides metadata about supported file types, while
      `SaveOptions` configures how a document is written back to disk (format, compression,
      etc.).'
    question: What is the difference between `DocumentFormatInfo` and `SaveOptions`?
  - answer: Yes—use `DocumentFormatInfo.FromExtension("yourExt")`; if the extension
      isn’t recognized, the method returns `null`.
    question: Can I list formats for a custom file extension?
  - answer: Absolutely. Pass the password to the `Editor` constructor via `EditorSettings`
      to open encrypted documents.
    question: Does GroupDocs.Editor support password‑protected files?
  - answer: Over **30 input and output formats**, spanning Word, Excel, PowerPoint,
      HTML, and plain text.
    question: How many formats does GroupDocs.Editor actually support?
  - answer: Use the `GetEditableWordProcessingFormats()` (or Spreadsheet/Presentation
      equivalents) to retrieve formats that allow full edit capabilities.
    question: Is there a way to restrict the list to only editable formats?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Lijst ondersteunde documentformaten met GroupDocs.Editor .NET
type: docs
url: /nl/net/document-processing/work-document-formats/
weight: 13
---

# Lijst ondersteunde documentformaten

Welkom bij onze uitgebreide tutorial over **hoe ondersteunde documentformaten te lijst** met GroupDocs.Editor voor .NET. Of je nu een document‑gerichte webapp bouwt of een enterprise‑klasse desktoptool, het precies weten welke formaten je kunt bewerken of converteren is essentieel. In deze gids ontdek je hoe je formaten kunt opsommen, extensies kunt parseren en documenten kunt bewerken — allemaal met duidelijke, mensvriendelijke uitleg en kant‑klaar code‑fragmenten.

## Snelle antwoorden
- **Hoe lijst ik alle ondersteunde formaten op?** Gebruik `DocumentFormatInfo.GetSupportedWordProcessingFormats()` (of de Presentation/Spreadsheet-equivalenten) en doorloop de collectie.  
- **Kan ik een formaat bepalen aan de hand van een bestandsextensie?** Ja — roep `DocumentFormatInfo.FromExtension(".docx")` aan.  
- **Welke bestandstypen ondersteunt GroupDocs.Editor?** Meer dan 30 invoer‑ en uitvoerformaten, waaronder DOCX, XLSX, PPTX, HTML en platte tekst.  
- **Heb ik een licentie nodig om formaten te lijst?** Een tijdelijke licentie ontgrendelt de volledige API; anders werkt een proefversie met beperkte functies.  
- **Welke .NET‑versies zijn compatibel?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.

## Wat betekent “lijst ondersteunde documentformaten”?
De uitdrukking verwijst naar het programmatisch ophalen van de collectie bestandstypen die GroupDocs.Editor kan openen, bewerken en opslaan. Deze bewerking stelt je in staat dynamische UI‑dropdowns te bouwen of gebruikersuploads te valideren vóór verwerking, zodat alleen compatibele bestanden naar de editor worden doorgegeven voor verdere manipulatie.

## Waarom ondersteunde documentformaten lijst?
GroupDocs.Editor **ondersteunt meer dan 30 invoer‑ en uitvoerformaten** en kan bestanden tot **2 GB** verwerken zonder het volledige document in het geheugen te laden. Het kennen van de exacte lijst voorkomt runtime‑fouten, verbetert de gebruikerservaring en stelt je in staat bedrijfsregels af te dwingen, zoals “alleen bewerkbare Office‑documenten toestaan”. Het helpt ook om gebruikers alleen de formaten te tonen die je applicatie werkelijk ondersteunt.

## Voorvereisten
Zorg ervoor dat je het volgende hebt voordat je begint:

1. **.NET‑ontwikkelomgeving** – Visual Studio 2022 of een IDE die .NET 6+ ondersteunt.  
2. **GroupDocs.Editor voor .NET‑bibliotheek** – download van de [GroupDocs releases page](https://releases.groupdocs.com/editor/net/).  
3. **Tijdelijke licentie** – verkrijg een [temporary license](https://purchase.groupdocs.com/temporary-license/) voor onbeperkte toegang.  
4. **Basis C#‑kennis** – vertrouwdheid met namespaces, `using`‑statements en console‑output.

## Hoe ondersteunde documentformaten lijst?
Laad de collectie ondersteunde formaten en druk de naam en bestandsextensie van elk formaat af. Dit twee‑stappenpatroon werkt voor Word‑verwerking, Spreadsheet‑ en Presentatiedocumenten. Door de collectie te itereren kun je dynamisch UI‑elementen zoals dropdowns vullen, zodat gebruikers alleen formaten kunnen selecteren die de editor daadwerkelijk kan verwerken.

```csharp
// No actual code block – placeholder retained from original tutorial
```csharp
using System;
using GroupDocs.Editor.Options;
```
```

### Lijst Word‑verwerkingsformaten
`Formats.WordProcessingFormats` is een enumeratie die elk door de editor herkend Word‑verwerkingsbestandstype beschrijft. De eigenschap `All` retourneert een collectie van deze formaatobjecten.

```csharp
```csharp
foreach (Formats.WordProcessingFormats oneFormat in Formats.WordProcessingFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**Uitleg:**  
1. **Doorloop formaten:** We itereren over alle beschikbare Word‑verwerkingsformaten.  
2. **Uitvoer formaatdetails:** Voor elk formaat drukken we de vriendelijke naam en de standaard bestandsextensie af.

### Lijst presentatiefomaten
`Formats.PresentationFormats` werkt op dezelfde manier voor slide‑deck‑bestanden, waarbij elk ondersteund presentatietype wordt blootgesteld via de `All`‑collectie.

```csharp
```csharp
foreach (Formats.PresentationFormats oneFormat in Formats.PresentationFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**Uitleg:**  
1. **Doorloop formaten:** Dezelfde iteratielogica geldt voor presentaties.  
2. **Uitvoer formaatdetails:** De naam en extensie worden voor elk formaat weergegeven.

## Hoe bestandsformatextensie bepalen?
Soms heb je alleen een bestandsnaam en moet je het bijbehorende `DocumentFormat` afleiden. GroupDocs.Editor biedt een eenvoudige statische helper die een bestandsextensie naar de interne formaatrepresentatie mappt, zodat je bestanden kunt valideren of converteren voordat je ze in de editor laadt.

### Spreadsheet‑formaten parseren
`Formats.SpreadsheetFormats.FromExtension` zet een bestandsextensie‑string om in de overeenkomende spreadsheet‑formaat‑enumwaarde.

```csharp
```csharp
Formats.SpreadsheetFormats expectedXlsm = Formats.SpreadsheetFormats.FromExtension(".xlsm");
Console.WriteLine("Parsed Spreadsheet format is {0}", expectedXlsm.Name);
```
```

**Uitleg:**  
1. **Parseer formaat:** `FromExtension` zet de `.xlsm`‑extensie om in de interne `SpreadsheetFormat`‑enum.  
2. **Uitvoer formaat:** De naam van het geparseerde formaat wordt afgedrukt, wat de mapping bevestigt.

### Tekstuele formaten parseren
Evenzo lost `Formats.TextualFormats.FromExtension` tekstuele bestandsextensies op, zoals HTML of TXT.

```csharp
```csharp
Formats.TextualFormats expectedHtml = Formats.TextualFormats.FromExtension("html");
Console.WriteLine("Parsed Textual format is {0}", expectedHtml.Name);
```
```

**Uitleg:**  
1. **Parseer formaat:** De `FromExtension`‑methode lost de `html`‑extensie op naar een `TextFormat`.  
2. **Uitvoer formaat:** De naam van het tekstuele formaat wordt weergegeven, nuttig voor web‑gebaseerde editors.

## Hoe documenten bewerken na het identificeren van formaten?
Zodra je het formaat kent, volgt het laden en bewerken van een document een consistent patroon. Eerst maak je een `Editor`‑instance met het pad naar het bronbestand, vervolgens roep je `Edit()` aan om een `EditableDocument` te verkrijgen. Vanaf daar kun je de inhoud lezen, wijzigen en uiteindelijk opslaan met de juiste `SaveOptions`.

### Een document laden
`Editor` is de kernklasse die alle bewerkingsbewerkingen voor een gegeven bestand omvat.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/document.docx"))
{
    // Further steps will be covered here.
}
```
```

**Uitleg:**  
1. **Initialiseer Editor:** Maak een `Editor`‑instance aan en geef het volledige pad van het doelbestand door.  
2. **Dispose‑patroon:** De `using`‑statement garandeert dat alle niet‑beheerde resources onmiddellijk worden vrijgegeven.

### Inhoud extraheren
`EditableDocument.GetContent()` retourneert de ruwe tekst van het document (of HTML voor web‑gebaseerde editors), die je kunt weergeven of manipuleren.

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    string content = editableDocument.GetContent();
    Console.WriteLine(content);
}
```
```

**Uitleg:**  
1. **Edit‑methode:** `Edit()` retourneert een `EditableDocument`‑object.  
2. **Inhoud ophalen:** `GetContent()` haalt de ruwe tekst van het document op (of HTML voor web‑gebaseerde editors).  
3. **Inhoud weergeven:** De inhoud wordt naar de console geschreven ter verificatie.

### Wijzigingen opslaan
`SaveOptions` vertelt de editor hoe en in welk formaat het bewerkte document terug naar de opslag moet worden geschreven.

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    // Modify content here
    SaveOptions saveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docx);
    editor.Save(editableDocument, "path/to/save/document.docx", saveOptions);
}
```
```

**Uitleg:**  
1. **Edit‑methode:** Verkrijg opnieuw het `EditableDocument` na wijzigingen.  
2. **Inhoud wijzigen:** Pas je wijzigingen toe op de string (hier niet getoond).  
3. **Opslagopties:** Configureer `SaveOptions` met het gewenste uitvoerformaat.  
4. **Document opslaan:** Sla het bewerkte bestand opnieuw op op schijf.

## Hoe met verschillende documenttypen werken?
GroupDocs.Editor abstraheert Word-, Spreadsheet- en Presentation‑verwerking achter dezelfde API‑laag, waardoor het eenvoudig is van context te wisselen zonder een nieuwe set klassen voor elke documentfamilie te leren.

### Spreadsheet‑documenten bewerken
`SpreadsheetSaveOptions` definieert hoe een spreadsheet wordt geschreven, inclusief formaat en optionele compressie‑instellingen.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/spreadsheet.xlsx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // Modify content here
        SaveOptions saveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsx);
        editor.Save(editableDocument, "path/to/save/spreadsheet.xlsx", saveOptions);
    }
}
```
```

**Uitleg:**  
1. **Initialiseer Editor:** Geef een spreadsheet‑bestandspad door aan de `Editor`‑constructor.  
2. **Edit‑methode:** Haal een `EditableDocument` op.  
3. **Inhoud ophalen:** Print de CSV‑representatie (of HTML) van de spreadsheet.  
4. **Inhoud wijzigen:** Pas eventuele cel‑niveau wijzigingen toe die je nodig hebt.  
5. **Opslagopties:** Kies de juiste `SpreadsheetSaveOptions`.  
6. **Document opslaan:** Schrijf de bijgewerkte spreadsheet terug naar de opslag.

### Presentatie‑documenten bewerken
`PresentationSaveOptions` regelt het uitvoerformaat voor slide‑decks, waardoor je het oorspronkelijke bestandstype kunt behouden of wijzigen.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/presentation.pptx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // Modify content here
        SaveOptions saveOptions = new PresentationSaveOptions(PresentationFormats.Pptx);
        editor.Save(editableDocument, "path/to/save/presentation.pptx", saveOptions);
    }
}
```
```

**Uitleg:**  
1. **Initialiseer Editor:** Laad een PowerPoint‑bestand via `Editor`.  
2. **Edit‑methode:** Verkrijg een `EditableDocument`.  
3. **Inhoud ophalen:** Extraheer slide‑HTML of platte tekst.  
4. **Inhoud wijzigen:** Werk titels, opsommingstekens of afbeeldingen bij.  
5. **Opslagopties:** Gebruik `PresentationSaveOptions` om het uitvoerformaat te definiëren.  
6. **Document opslaan:** Sla de bewerkte presentatie op.

## Veelvoorkomende problemen en oplossingen
- **“Format not supported”‑fout:** Controleer of je de nieuwste GroupDocs.Editor‑versie gebruikt; deze voegt regelmatig ondersteuning toe voor nieuwere Office‑formaten.  
- **Geheugengebruik bij grote bestanden:** Schakel streaming‑modus in door `EditorSettings.EnableStreaming = true` in te stellen vóór het laden van het document.  
- **Licentie niet toegepast:** Zorg ervoor dat het tijdelijke licentiebestand in de toepassings‑root staat of geladen wordt via `License license = new License(); license.SetLicense("path/to/license.lic");`.

## Veelgestelde vragen

**Q: Wat is het verschil tussen `DocumentFormatInfo` en `SaveOptions`?**  
A: `DocumentFormatInfo` biedt metadata over ondersteunde bestandstypen, terwijl `SaveOptions` configureert hoe een document terug naar schijf wordt geschreven (formaat, compressie, enz.).

**Q: Kan ik formaten lijst voor een aangepaste bestandsextensie?**  
A: Ja — gebruik `DocumentFormatInfo.FromExtension("yourExt")`; als de extensie niet wordt herkend, retourneert de methode `null`.

**Q: Ondersteunt GroupDocs.Editor wachtwoord‑beveiligde bestanden?**  
A: Absoluut. Geef het wachtwoord door aan de `Editor`‑constructor via `EditorSettings` om versleutelde documenten te openen.

**Q: Hoeveel formaten ondersteunt GroupDocs.Editor daadwerkelijk?**  
A: Meer dan **30 invoer‑ en uitvoerformaten**, variërend van Word, Excel, PowerPoint, HTML tot platte tekst.

**Q: Is er een manier om de lijst te beperken tot alleen bewerkbare formaten?**  
A: Gebruik `GetEditableWordProcessingFormats()` (of de Spreadsheet/Presentation‑equivalenten) om formaten op te halen die volledige bewerkingsmogelijkheden bieden.

## Aanvullende bronnen
- Download de bibliotheek van de [GroupDocs releases page](https://releases.groupdocs.com/editor/net/).  
- Verkrijg een [temporary license](https://purchase.groupdocs.com/temporary-license/) voor volledige functionaliteit.  
- Probeer het product met een [free trial](https://releases.groupdocs.com/).  
- Bekijk gedetailleerde gebruiksvoorbeelden in de [GroupDocs.Editor documentation](https://tutorials.groupdocs.com/editor/net/).  
- Krijg hulp van de community op het [support forum](https://forum.groupdocs.com/c/editor/20).

## Conclusie
Door deze gids te volgen weet je nu hoe je **ondersteunde documentformaten kunt lijst**, **een bestandsformaat kunt bepalen aan de hand van de extensie**, en **documenten kunt bewerken** voor Word-, Spreadsheet- en Presentatietypen met GroupDocs.Editor voor .NET. Integreer deze fragmenten in je eigen projecten om robuuste, formaat‑bewuste applicaties te bouwen die eindgebruikers verrassen en runtime‑fouten verminderen.

---

**Laatst bijgewerkt:** 2026-06-06  
**Getest met:** GroupDocs.Editor 23.9 for .NET  
**Auteur:** GroupDocs

## Gerelateerde tutorials

- [Documentladen in .NET met GroupDocs.Editor beheersen: Een uitgebreide gids](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)
- [Documentbewerking in .NET met GroupDocs.Editor beheersen: Een uitgebreide gids](/editor/net/document-editing/master-document-editing-dotnet-groupdocs-editor/)
- [Word naar HTML converteren met GroupDocs.Editor .NET: Een stapsgewijze gids](/editor/net/document-saving/convert-word-to-html-groupdocs-editor-dotnet/)