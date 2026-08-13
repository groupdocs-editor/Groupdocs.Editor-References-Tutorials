---
date: 2026-06-06
description: Leer hoe u **create editable document** objecten maakt van CSV- en TSV-bestanden
  met GroupDocs.Editor voor .NET. Deze gids laat ook zien hoe u **read delimited text
  C#** en **edit CSV .NET** efficiënt kunt uitvoeren in Visual Studio.
keywords:
- create editable document
- read delimited text c#
- edit csv .net
- parse delimited values c#
linktitle: Werken met gescheiden waarden (DSV) – maak bewerkbaar document
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to **create editable document** objects from CSV and TSV
    files using GroupDocs.Editor for .NET. This guide also shows how to **read delimited
    text C#** and **edit CSV .NET** efficiently in Visual Studio.
  headline: Work with Delimited Separated Values (DSV) – create editable document
  type: TechArticle
- questions:
  - answer: Yes, the API streams data and can handle files larger than 1 GB without
      loading the entire document into memory.
    question: Can I use GroupDocs.Editor for .NET to edit large CSV files?
  - answer: Absolutely – any single‑character delimiter (e.g., pipe `|`, semicolon
      `;`) is supported as long as you specify it in `DelimitedTextEditOptions`.
    question: Does GroupDocs.Editor for .NET support other DSV formats besides CSV
      and TSV?
  - answer: Yes, you can set the `Encoding` property in `DelimitedTextSaveOptions`
      to UTF‑8, UTF‑16, ISO‑8859‑1, or any .NET `Encoding` you require.
    question: Is it possible to customize the encoding when saving DSV files?
  - answer: Yes – after editing, simply use `SpreadsheetSaveOptions` to export the
      content as an `.xlsx` workbook.
    question: Can I convert a CSV file to an Excel spreadsheet using GroupDocs.Editor
      for .NET?
  - answer: Detailed API references and code samples are available **[here](https://tutorials.groupdocs.com/editor/net/)**.
    question: Where can I find more documentation on GroupDocs.Editor for .NET?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Werken met gescheiden waarden (DSV) – maak bewerkbaar document
type: docs
url: /nl/net/document-processing/work-dsv/
weight: 12
---

# Werken met door komma's gescheiden waarden (DSV) – bewerkbaar document maken

Als je een .NET‑ontwikkelaar bent die **create editable document**‑objecten moet maken van door komma's gescheiden waarden (DSV) zoals CSV of TSV, dan ben je hier aan het juiste adres. In de eerste 100 woorden leggen we uit waarom GroupDocs.Editor voor .NET de meest betrouwbare manier is om **read delimited text C#** te lezen, te bewerken en vervolgens weer op te slaan zonder formattering te verliezen. Je krijgt een volledige, copy‑and‑paste‑klaar workflow die natuurlijk in elke Visual Studio‑oplossing past.

## Snelle antwoorden
- **Welke bibliotheek biedt de beste CSV-bewerking in .NET?** GroupDocs.Editor for .NET.
- **Kan ik grote CSV‑bestanden bewerken in Visual Studio?** Ja – de API streams data and avoids loading the whole file into memory.
- **Heb ik een licentie nodig voor productiegebruik?** A commercial license is required; a free trial is available.
- **Welke formaten kan ik na het bewerken exporteren?** CSV, TSV, and Excel‑compatible spreadsheet formats.
- **Is de API compatibel met .NET 6+?** Absolutely – it supports .NET Framework 4.5+, .NET Core 3.1+, .NET 5, and .NET 6.

## Wat betekent “create editable document” in de context van GroupDocs.Editor?
**Create editable document** betekent het genereren van een `EditableDocument`‑instantie die een mutabele versie van een bronbestand (CSV, TSV, enz.) in het geheugen vertegenwoordigt. Dit object stelt je in staat om de inhoud te lezen, te wijzigen en opnieuw op te slaan met dezelfde API. Het biedt methoden om de documenttekst op te halen, wijzigingen toe te passen en het terug op te slaan in verschillende formaten, waarbij kolomuitlijning en aanhalingstekens behouden blijven.

## Waarom GroupDocs.Editor gebruiken voor DSV‑verwerking?
GroupDocs.Editor verwerkt **meer dan 50 in‑ en uitvoerformaten**, waaronder CSV, TSV en Excel‑compatibele spreadsheets, terwijl het geheugengebruik onder de 10 MB blijft voor bestanden tot 500 MB. Het behoudt ook automatisch kolomuitlijning, aanhalingstekenregels en aangepaste coderingen, waardoor handmatige parse‑logica overbodig wordt.

## Vereisten
Voordat we beginnen, zorg ervoor dat je het volgende geïnstalleerd hebt:

- **Visual Studio** (any recent edition) – je ontwikkelt en debugt direct binnen de IDE.
- **GroupDocs.Editor for .NET** – download het nieuwste pakket **[here](https://releases.groupdocs.com/editor/net/)**.
- **Basic C# knowledge** – de tutorial gaat ervan uit dat je een console‑ of ASP.NET‑project kunt maken en NuGet‑pakketten kunt toevoegen.

## Namespaces importeren
De `Editor`, `EditableDocument` en optieklassen bevinden zich in de `GroupDocs.Editor`‑namespace.  

De `DelimitedTextEditOptions`‑klasse is het startpunt voor het definiëren van de scheidingsteken (komma, tab, enz.) en andere parse‑regels.

```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

## Hoe maak je een bewerkbaar document van een CSV‑bestand?
Laad de bron‑CSV met `Editor` en roep de `Edit`‑methode aan, waarbij je een `DelimitedTextEditOptions`‑instantie doorgeeft die een komma‑scheidingsteken specificeert. De methode retourneert een `EditableDocument` die je in het geheugen kunt manipuleren. Dit twee‑stappen‑patroon—load → edit—dekt **read delimited text C#**‑scenario's en garandeert dat de oorspronkelijke bestandsstructuur behouden blijft.

## Stap 1: Haal een pad op naar het invoer‑DSV‑bestand
Eerst moet je het absolute of relatieve pad naar het bron‑DSV‑bestand opgeven. Voor de demonstratie gebruiken we een eenvoudige CSV in de `Data`‑map van het project.

```csharp
string inputFilePath = "Your Sample Document";
```

## Stap 2: Maak een Editor‑instantie
`Editor` is de kernklasse die het laden, bewerken en opslaan coördineert. Een instantie maken met een `FileInfo`‑object geeft je volledige controle over de levenscyclus van het bestand.

```csharp
using (Editor editor = new Editor(inputFilePath))
{
```

## Stap 3: Maak DSV‑bewerkingsopties
`DelimitedTextEditOptions` vertelt de editor hoe het bestand geïnterpreteerd moet worden. Je kunt het scheidingsteken, of de eerste rij kopteksten bevat, en de tekencodering instellen.

```csharp
    Options.DelimitedTextEditOptions editOptions = new DelimitedTextEditOptions(",");
    editOptions.ConvertDateTimeData = false;
    editOptions.ConvertNumericData = true;
    editOptions.TreatConsecutiveDelimitersAsOne = true;
```

## Stap 4: Maak een EditableDocument‑instantie
`EditableDocument` vertegenwoordigt een mutabele in‑memory‑versie van het bronbestand. Het aanroepen van `Editor.Edit` met de opties retourneert een `EditableDocument`. Dit object bevat de tekst van het bestand in een mutabele string, klaar voor elke **parse delimited values C#**‑bewerking die je nodig hebt.

```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```

## Stap 5: Bewerk de documentinhoud
`GetDocumentText()` retourneert de huidige tekst van het bewerkbare document als een string. Haal de originele tekst op via `EditableDocument.GetDocumentText()`, voer je wijzigingen uit (bijv. een kolomwaarde vervangen), en sla het resultaat op in een nieuwe string. Hier kun je **edit CSV .NET** uitvoeren zonder low‑level bestands‑streams aan te raken.

```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("SsangYong", "Chevrolet").Replace("Kyron", "Camaro");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```

## Stap 6: Maak een EditableDocument met bijgewerkte inhoud
Wikkel de gewijzigde string terug in een `EditableDocument`. Deze stap voltooit de wijzigingen en maakt het object klaar om op te slaan in elk ondersteund formaat.

```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```

## Stap 7: Maak CSV‑opslaoptopties
`DelimitedTextSaveOptions` specificeert hoe de bewerkte inhoud terug naar een CSV‑bestand moet worden geschreven. Wanneer je klaar bent om de wijzigingen op te slaan, configureer je `DelimitedTextSaveOptions`. Je kunt hetzelfde scheidingsteken, een ander scheidingsteken, of zelfs de regeleinde‑stijl opgeven.

```csharp
    Options.DelimitedTextSaveOptions csvSaveOptions = new DelimitedTextSaveOptions(",");
    csvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

## Stap 8: Maak TSV‑opslaoptopties
Als je een tab‑gescheiden versie nodig hebt, schakel je eenvoudig het scheidingsteken naar `\t`. Hetzelfde `EditableDocument` kan meerdere keren worden opgeslagen met verschillende opties.

```csharp
    Options.DelimitedTextSaveOptions tsvSaveOptions = new DelimitedTextSaveOptions("\t");
    tsvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

## Stap 9: Maak Spreadsheet‑opslaoptopties
`SpreadsheetSaveOptions` configureert de export van het document naar Excel‑compatibele formaten zoals .xlsx. GroupDocs.Editor stelt je ook in staat om de bewerkte gegevens te exporteren naar een Excel‑compatibel formaat (`.xlsx`). De `SpreadsheetSaveOptions`‑klasse behandelt kolomtypes, formules en celopmaak automatisch.

```csharp
    Options.SpreadsheetSaveOptions cellsSaveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
```

## Stap 10: Bereid opslag‑paden voor
Definieer afzonderlijke uitvoer‑paden voor elk formaat. Het gebruik van duidelijke naamgevingsconventies (bijv. `output.csv`, `output.tsv`, `output.xlsx`) helpt je project georganiseerd te houden.

```csharp
    string outputCsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".csv");
    string outputTsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".tsv");
    string outputCellsPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".xlsm");
```

## Stap 11: Sla het bewerkte document op
`Save()` schrijft het document naar schijf met de opgegeven opslaoptopties. Roep `EditableDocument.Save` aan met de juiste opties voor elk doelformaat. De API schrijft het bestand direct naar schijf, waarbij de originele codering behouden blijft tenzij je deze overschrijft.

```csharp
    editor.Save(afterEdit, outputCsvPath, csvSaveOptions);
    editor.Save(afterEdit, outputTsvPath, tsvSaveOptions);
    editor.Save(afterEdit, outputCellsPath, cellsSaveOptions);
```

## Stap 12: Ruim EditableDocument‑instanties op
Zowel `Editor` als `EditableDocument` implementeren `IDisposable`. Het vrijgeven ervan maakt bestands‑handles en niet‑beheerde resources vrij, wat cruciaal is bij het verwerken van veel bestanden in een batch‑taak.

```csharp
    beforeEdit.Dispose();
    afterEdit.Dispose();
}
System.Console.WriteLine("WorkingWithDsv routine has successfully finished");
```

## Veelvoorkomende problemen en oplossingen
| Probleem | Waarom het gebeurt | Oplossing |
|----------|--------------------|-----------|
| **Onverwachte extra aanhalingstekens** | De standaard CSV‑parser kan ingesloten komma's als scheidingstekens behandelen. | Stel `EscapeMode = EscapeMode.DoubleQuote` in `DelimitedTextEditOptions` in. |
| **Geheugenspike bij groot bestand** | Een bestand van 500 MB laden zonder streaming. | Gebruik `Editor.Load` met `LoadOptions` die lazy loading inschakelen. |
| **Codering mismatch** | Bronbestand gebruikt UTF‑16 maar de opties standaard naar UTF‑8. | Stel expliciet `Encoding = Encoding.Unicode` in de opslaoptopties in. |

## Veelgestelde vragen

**Q: Kan ik GroupDocs.Editor voor .NET gebruiken om grote CSV‑bestanden te bewerken?**  
A: Ja, de API streamt data en kan bestanden groter dan 1 GB verwerken zonder het volledige document in het geheugen te laden.

**Q: Ondersteunt GroupDocs.Editor voor .NET andere DSV‑formaten naast CSV en TSV?**  
A: Absoluut – elk scheidingsteken van één teken (bijv. pipe `|`, puntkomma `;`) wordt ondersteund zolang je het opgeeft in `DelimitedTextEditOptions`.

**Q: Is het mogelijk om de codering aan te passen bij het opslaan van DSV‑bestanden?**  
A: Ja, je kunt de `Encoding`‑eigenschap in `DelimitedTextSaveOptions` instellen op UTF‑8, UTF‑16, ISO‑8859‑1, of elke .NET `Encoding` die je nodig hebt.

**Q: Kan ik een CSV‑bestand converteren naar een Excel‑spreadsheet met GroupDocs.Editor voor .NET?**  
A: Ja – na het bewerken gebruik je eenvoudig `SpreadsheetSaveOptions` om de inhoud te exporteren als een `.xlsx`‑werkmap.

**Q: Waar kan ik meer documentatie vinden over GroupDocs.Editor voor .NET?**  
A: Gedetailleerde API‑referenties en code‑voorbeelden zijn beschikbaar **[hier](https://tutorials.groupdocs.com/editor/net/)**.

---

**Laatst bijgewerkt:** 2026-06-06  
**Getest met:** GroupDocs.Editor 23.10 for .NET  
**Auteur:** GroupDocs

## Gerelateerde tutorials

- [Handleiding voor bewerken van platte tekst en DSV‑documenten voor GroupDocs.Editor .NET](/editor/net/plain-text-dsv-documents/)
- [Beheers GroupDocs.Editor .NET voor efficiënte CSV‑documentbewerking en conversie](/editor/net/plain-text-dsv-documents/groupdocs-editor-net-csv-editing-guide/)
- [Documentladen in .NET met GroupDocs.Editor onder de knie: een uitgebreide gids](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)