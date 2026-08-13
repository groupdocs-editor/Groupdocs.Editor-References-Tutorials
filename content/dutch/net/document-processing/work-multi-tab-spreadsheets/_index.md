---
date: 2026-06-06
description: Leer hoe je **elk Excel-tabblad** kunt opslaan met GroupDocs.Editor voor
  .NET – stapsgewijze handleiding, code‑fragmenten en best practices voor het splitsen
  van XLSX‑bestanden.
keywords:
- save each excel tab
- read multiple sheets
- convert excel tab pdf
- split xlsx files
linktitle: Werken met spreadsheets met meerdere tabbladen
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to **save each Excel tab** using GroupDocs.Editor for .NET
    – step‑by‑step guide, code snippets, and best practices for splitting XLSX files.
  headline: How to save each Excel tab with GroupDocs.Editor .NET
  type: TechArticle
- description: Learn how to **save each Excel tab** using GroupDocs.Editor for .NET
    – step‑by‑step guide, code snippets, and best practices for splitting XLSX files.
  name: How to save each Excel tab with GroupDocs.Editor .NET
  steps:
  - name: Get a Path to the Input File
    text: First, specify the full path to the source XLSX that contains multiple tabs.
  - name: Load the Spreadsheet into the Editor Instance
    text: The `Editor` class is the entry point for all document operations in GroupDocs.Editor.
      It reads the file stream and prepares the document for editing or extraction.
  - name: Create an EditableDocument from the First Tab
    text: '`EditableDocument` represents a single, editable sheet within the workbook.
      The constructor takes the `Editor` instance and a zero‑based sheet index.'
  - name: Create an EditableDocument from the Second Tab
    text: You can repeat the same pattern for any additional sheet by changing the
      index value.
  - name: Save the First Tab to a Separate Document
    text: '`Save` writes the edited document to a file in the specified format. Call
      it on the `EditableDocument` instance, providing the output path and format
      (e.g., `SaveFormat.Xlsx`).'
  - name: Save the Second Tab to a Separate Document
    text: The same `Save` call works for the second sheet, and you can choose a different
      format such as PDF if needed.
  - name: Dispose of EditableDocument Instances
    text: '`Dispose` releases unmanaged resources held by the document, such as file
      handles, ensuring no leaks in long‑running services.'
  type: HowTo
- questions:
  - answer: Hidden sheets are treated like any other sheet; you can access them by
      index and save them, but you may need to set `EditableDocument.IsVisible = true`
      before saving if you want them visible in the output.
    question: What if my workbook contains hidden sheets?
  - answer: Yes, specify `SaveFormat.Pdf` when calling `Save` on the `EditableDocument`.
      The library preserves layout, images, and charts during conversion.
    question: Can I convert an Excel tab directly to PDF?
  - answer: Absolutely. Use `SaveFormat.Csv` for each `EditableDocument` to generate
      plain‑text CSV representations of each sheet.
    question: Is it possible to split a workbook into CSV files instead of XLSX?
  - answer: It does. Provide the password via `LoadOptions.Password` when creating
      the `Editor` instance.
    question: Does GroupDocs.Editor support password‑protected Excel files?
  - answer: The official documentation and sample projects on the [download page](https://releases.groupdocs.com/editor/net/)
      contain additional use‑cases.
    question: Where can I find more examples of working with spreadsheets?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Hoe elk Excel-tabblad opslaan met GroupDocs.Editor .NET
type: docs
url: /nl/net/document-processing/work-multi-tab-spreadsheets/
weight: 17
---

# Werken met meerdere tabbladen in spreadsheets

## Introductie
Als je elke Excel‑tabblad als een onafhankelijk bestand wilt **opslaan**, maakt GroupDocs.Editor for .NET het moeiteloos. Of je nu financiële rapporten extraheert, per‑afdeling werkbladen genereert, of tabbladen naar PDF converteert, deze tutorial leidt je door de volledige workflow — van het opzetten van de omgeving tot het vrijgeven van bronnen — zodat je multi‑sheet verwerking met vertrouwen kunt automatiseren.

## Snelle antwoorden
- **Kan GroupDocs.Editor een XLSX splitsen in afzonderlijke bestanden?** Ja, je kunt de werkmap laden en elk blad afzonderlijk exporteren.  
- **In welke formaten kan elk tabblad worden opgeslagen?** XLSX, CSV, PDF, HTML en meer – meer dan 30 uitvoerformaten worden ondersteund.  
- **Heb ik een licentie nodig voor deze functie?** Een tijdelijke licentie werkt voor testen; een volledige licentie is vereist voor productie.  
- **Wordt .NET Core ondersteund?** Absoluut – de bibliotheek werkt met .NET Framework 4.0+ en .NET Core/5/6+.  
- **Hoeveel tabbladen kunnen er tegelijk worden verwerkt?** GroupDocs.Editor kan werkmappen met meer dan 500 bladen aan zonder het hele bestand in het geheugen te laden.

## Wat betekent “save each excel tab”?
**“Save each Excel tab”** betekent het extraheren van elk werkblad uit een multi‑sheet werkmap en elk werkblad naar een eigen losstaand document schrijven (bijv. aparte XLSX‑ of PDF‑bestanden). Deze aanpak vereenvoudigt downstream verwerking, rapportage en distributie door je een bestand per blad te geven, dat vervolgens onafhankelijk kan worden gedeeld, gearchiveerd of verder getransformeerd.

## Waarom GroupDocs.Editor voor deze taak gebruiken?
GroupDocs.Editor ondersteunt **meer dan 30 invoer‑ en uitvoerformaten** en kan spreadsheets met **tot 1.000 bladen** verwerken, terwijl het geheugenverbruik laag blijft door data te streamen in plaats van het volledige bestand te laden. De API behoudt ook celstijlen, formules en ingesloten afbeeldingen, waardoor elk geëxporteerd tabblad er identiek uitziet als het origineel.

## Voorvereisten
1. **Visual Studio** – elke recente editie (Community, Professional of Enterprise).  
2. **.NET Framework 4.0+** – of .NET Core/5/6 als je de cross‑platform runtime verkiest.  
3. **GroupDocs.Editor for .NET** – download het van de [download page](https://releases.groupdocs.com/editor/net/).  
4. **License** – een [temporary license](https://purchase.groupdocs.com/temporary-license/) is voldoende voor testen; koop een volledige licentie voor productie.  
5. **Free trial** – je kunt de bibliotheek ook uitproberen via de [free trial](https://releases.groupdocs.com/) pagina.  
6. **Support** – als je problemen ondervindt, bezoek dan het [support forum](https://forum.groupdocs.com/c/editor/20) of overweeg de [purchase page](https://purchase.groupdocs.com/buy) voor een volledige licentie.

## Importeer Namespaces
Voordat we beginnen met coderen, moet je de benodigde namespaces importeren. Voeg de volgende using‑directieven toe aan de bovenkant van je `.cs`‑bestand:

```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```

## Hoe elk Excel‑tabblad opslaan als een apart bestand?
Laad de werkmap, maak een `EditableDocument` voor elk blad, en roep `Save` aan met het gewenste formaat. Dit proces isoleert elk tabblad, laat je een apart uitvoerpad kiezen, en geeft bronnen automatisch vrij. Hieronder vind je de stap‑voor‑stap workflow die je volgt, met uitleg voor elke API‑aanroep en best‑practice tips om veelvoorkomende valkuilen te vermijden.

### Stap 1: Haal een pad op naar het invoerbestand
Geef eerst het volledige pad op naar de bron‑XLSX die meerdere tabbladen bevat.

```csharp
string inputFilePath = "Your Sample Document";
```

### Stap 2: Laad de spreadsheet in de Editor‑instantie
De `Editor`‑klasse is het toegangspunt voor alle documentbewerkingen in GroupDocs.Editor. Het leest de bestandsstroom en bereidt het document voor op bewerken of extraheren.

```csharp
using (FileStream inputStream = File.OpenRead(inputFilePath))
{
    using (Editor editor = new Editor(delegate { return inputStream; }, delegate { return new SpreadsheetLoadOptions(); }))
    {
        // Further steps will go here
    }
}
```

### Stap 3: Maak een EditableDocument van het eerste tabblad
`EditableDocument` vertegenwoordigt een enkel, bewerkbaar blad binnen de werkmap. De constructor neemt de `Editor`‑instantie en een nul‑gebaseerde blad‑index.

```csharp
SpreadsheetEditOptions editOptions1 = new SpreadsheetEditOptions();
editOptions1.WorksheetIndex = 0; // First tab
EditableDocument firstTabBeforeEdit = editor.Edit(editOptions1);
```

### Stap 4: Maak een EditableDocument van het tweede tabblad
Je kunt hetzelfde patroon herhalen voor elk extra blad door de indexwaarde te wijzigen.

```csharp
SpreadsheetEditOptions editOptions2 = new SpreadsheetEditOptions();
editOptions2.WorksheetIndex = 1; // Second tab
EditableDocument secondTabBeforeEdit = editor.Edit(editOptions2);
```

### Stap 5: Sla het eerste tabblad op als een apart document
`Save` schrijft het bewerkte document naar een bestand in het opgegeven formaat. Roep het aan op de `EditableDocument`‑instantie, met het uitvoerpad en formaat (bijv. `SaveFormat.Xlsx`).

```csharp
SpreadsheetSaveOptions saveOptions1 = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
string outputFilename1 = Path.GetFileNameWithoutExtension(inputFilePath) + "_tab1.xlsm";
string outputPath1 = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename1);
editor.Save(firstTabBeforeEdit, outputPath1, saveOptions1);
```

### Stap 6: Sla het tweede tabblad op als een apart document
Dezelfde `Save`‑aanroep werkt voor het tweede blad, en je kunt een ander formaat kiezen, zoals PDF, indien nodig.

```csharp
SpreadsheetSaveOptions saveOptions2 = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsb);
string outputFilename2 = Path.GetFileNameWithoutExtension(inputFilePath) + "_tab2.xlsb";
string outputPath2 = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename2);
editor.Save(secondTabBeforeEdit, outputPath2, saveOptions2);
```

### Stap 7: Ruim EditableDocument‑instanties op
`Dispose` geeft niet‑beheerde bronnen vrij die door het document worden gehouden, zoals bestands‑handles, waardoor er geen lekken ontstaan in langdurige services.

```csharp
firstTabBeforeEdit.Dispose();
secondTabBeforeEdit.Dispose();
```

## Veelvoorkomende problemen en oplossingen
- **“File is locked” fouten** – Zorg ervoor dat je `Dispose()` aanroept op elk `EditableDocument` en de `Editor`‑instantie, of wikkel ze in `using`‑statements.  
- **Ontbrekende stijlen na export** – Controleer of je opslaat naar een formaat dat opmaak ondersteunt (bijv. XLSX of PDF). CSV verliest opmaak per definitie.  
- **Grote werkmappen veroorzaken trage prestaties** – Gebruik de streaming‑laadopties (`LoadOptions.Streaming = true`) om het geheugenverbruik laag te houden.

## Veelgestelde vragen

**Q: Wat als mijn werkmap verborgen bladen bevat?**  
A: Verborgen bladen worden behandeld als elk ander blad; je kunt ze via de index benaderen en opslaan, maar je moet mogelijk `EditableDocument.IsVisible = true` instellen vóór het opslaan als je ze zichtbaar wilt in de output.

**Q: Kan ik een Excel‑tabblad direct naar PDF converteren?**  
A: Ja, specificeer `SaveFormat.Pdf` bij het aanroepen van `Save` op het `EditableDocument`. De bibliotheek behoudt lay-out, afbeeldingen en grafieken tijdens de conversie.

**Q: Is het mogelijk om een werkmap te splitsen in CSV‑bestanden in plaats van XLSX?**  
A: Absoluut. Gebruik `SaveFormat.Csv` voor elk `EditableDocument` om platte‑tekst CSV‑representaties van elk blad te genereren.

**Q: Ondersteunt GroupDocs.Editor wachtwoord‑beveiligde Excel‑bestanden?**  
A: Ja. Geef het wachtwoord op via `LoadOptions.Password` bij het maken van de `Editor`‑instantie.

**Q: Waar kan ik meer voorbeelden vinden van werken met spreadsheets?**  
A: De officiële documentatie en voorbeeldprojecten op de [download page](https://releases.groupdocs.com/editor/net/) bevatten extra use‑cases.

## Conclusie
Door deze stappen te volgen, kun je **elke Excel‑tabblad** opslaan als een onafhankelijk document, tabbladen naar PDF converteren, en grote werkmappen opsplitsen in beheersbare stukken — allemaal met de betrouwbare, high‑performance GroupDocs.Editor for .NET bibliotheek. Deze mogelijkheid stroomlijnt rapportage‑pijplijnen, automatiseert data‑extractie, en vermindert handmatige spreadsheet‑verwerking.

---

**Last Updated:** 2026-06-06  
**Tested With:** GroupDocs.Editor 23.11 for .NET  
**Author:** GroupDocs  

---

## Gerelateerde tutorials

- [Meester Spreadsheet Tab Extractie in .NET met GroupDocs.Editor](/editor/net/spreadsheet-documents/mastering-spreadsheet-tab-extraction-dotnet-groupdocs-editor/)
- [Excel‑bestanden beveiligen met GroupDocs.Editor voor .NET | Beheer van beveiligde spreadsheets](/editor/net/spreadsheet-documents/groupdocs-editor-net-password-excel-files/)
- [Documentladen onder de knie krijgen in .NET met GroupDocs.Editor: Een uitgebreide gids](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)