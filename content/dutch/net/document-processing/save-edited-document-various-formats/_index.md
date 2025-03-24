---
title: Bewaar het bewerkte document in verschillende formaten
linktitle: Bewaar het bewerkte document in verschillende formaten
second_title: GroupDocs.Editor .NET API
description: Leer hoe u bewerkte documenten in verschillende formaten kunt opslaan met GroupDocs.Editor voor .NET in deze uitgebreide stapsgewijze handleiding.
weight: 11
url: /nl/net/document-processing/save-edited-document-various-formats/
---
## Invoering
Wilt u bewerkte documenten in verschillende formaten opslaan met GroupDocs.Editor voor .NET? U bent bij ons aan het juiste adres! Deze uitgebreide handleiding leidt u door het hele proces, van het opzetten van uw omgeving tot het opslaan van uw bewerkte document in meerdere indelingen. Laten we erin duiken en het bewerken en opslaan van documenten een fluitje van een cent maken!
## Vereisten
Voordat we beginnen, zorg ervoor dat u over het volgende beschikt:
1.  GroupDocs.Editor voor .NET - Download de nieuwste versie van[hier](https://releases.groupdocs.com/editor/net/).
2. Ontwikkelomgeving - Visual Studio of een andere .NET-compatibele IDE.
3. .NET Framework - Zorg ervoor dat .NET Framework 4.6.1 of hoger is geïnstalleerd.
4. Voorbeelddocument - Een voorbeeld van een WordProcess-document om mee te werken.
5. Basiskennis C# - Bekendheid met programmeren in C# is vereist.
## Naamruimten importeren
Zorg er om te beginnen voor dat u de benodigde naamruimten in uw C#-project importeert. Dit is cruciaal voor toegang tot de GroupDocs.Editor-functionaliteit.
```csharp
using System;
using GroupDocs.Editor.Metadata;
```
Laten we het proces opsplitsen in beheersbare stappen. Volg zorgvuldig om er zeker van te zijn dat u elk onderdeel begrijpt.
## Stap 1: Haal een pad naar het invoerbestand op
Eerst moet u het pad naar uw ingevoerde WordProcessing-bestand opgeven. Dit bestand wordt geladen en bewerkt.
```csharp
string inputFilePath = "Your Sample Document";
```
## Stap 2: Maak laadopties voor het document
Maak vervolgens laadopties die specifiek zijn voor WordProcessing-documenten. Met deze opties kunt u aanpassen hoe het document wordt geladen.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
```
## Stap 3: Laad het document met opties
 Laad het document nu in een`Editor` instance met behulp van de opgegeven laadopties.
```csharp
using (Editor editor = new Editor(inputFilePath, delegate { return loadOptions; }))
```
## Stap 4: Maak bewerkingsopties
Bereid bewerkingsopties voor het document voor. Deze opties bepalen hoe het document wordt geopend voor bewerking.
```csharp
WordProcessingEditOptions editOptions = new WordProcessingEditOptions();
```
## Stap 5: Open het document om te bewerken
 Open het document voor bewerking door een`EditableDocument`voorbeeld. Met deze instantie kunt u wijzigingen in het document aanbrengen.
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
```
## Stap 6: Bewerk de documentinhoud
Nu is het tijd om de inhoud van het document te bewerken. Haal eerst het document op als een enkele base64-gecodeerde tekenreeks.
```csharp
string allEmbeddedInsideString = beforeEdit.GetEmbeddedHtml();
```
Laten we bijvoorbeeld de ondertitel in het document aanpassen.
```csharp
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
```
## Stap 7: Maak een nieuw bewerkbaar document van bewerkte inhoud
 Maak een nieuwe`EditableDocument` exemplaar van de bewerkte inhoud en bronnen.
```csharp
using (EditableDocument afterEdit = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null))
```
## Stap 8: Document opslaan in verschillende formaten
Herhaal ten slotte alle ondersteunde WordProcessing-formaten en sla het bewerkte document in elk formaat op.
```csharp
foreach (WordProcessingFormats oneFormat in WordProcessingFormats.All)
{
    // Bereid opslagopties voor
    WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(oneFormat);
    // Bereid het opslagpad voor
    string savePath = Path.Combine("OutputDirectory", "MultipleOutFormats." + saveOptions.OutputFormat.Extension);
    // Bewaar het document
    editor.Save(afterEdit, savePath, saveOptions);
}
```
## Voltooiingsbericht
Ter afsluiting kunt u een bericht afdrukken waarin wordt aangegeven dat het proces met succes is voltooid.
```csharp
Console.WriteLine("SavingEditedDocumentToAllFormats routine has successfully finished");
```
## Conclusie
Gefeliciteerd! U hebt met succes geleerd hoe u bewerkte documenten in verschillende formaten kunt opslaan met GroupDocs.Editor voor .NET. Deze krachtige tool maakt het gemakkelijk om documenten in meerdere formaten te manipuleren en op te slaan met slechts een paar regels code. Houd er rekening mee dat de belangrijkste stappen bestaan uit het laden van het document, het bewerken van de inhoud en het opslaan in de gewenste indeling.
## Veelgestelde vragen
### Wat is GroupDocs.Editor voor .NET?
GroupDocs.Editor voor .NET is een krachtige API waarmee u documenten in verschillende formaten kunt bewerken met behulp van .NET-toepassingen.
### Kan ik GroupDocs.Editor gratis gebruiken?
 Ja, u kunt het gebruiken met een gratis proefperiode. Download het[hier](https://releases.groupdocs.com/).
### Welke formaten worden ondersteund door GroupDocs.Editor?
GroupDocs.Editor ondersteunt een breed scala aan formaten, waaronder DOCX, PDF, HTML en nog veel meer.
### Hoe krijg ik een tijdelijke licentie voor GroupDocs.Editor?
 U kunt een tijdelijke licentie verkrijgen[hier](https://purchase.groupdocs.com/temporary-license/).
### Waar kan ik meer documentatie en ondersteuning vinden?
 Gedetailleerde documentatie is beschikbaar[hier](https://tutorials.groupdocs.com/editor/net/) en u kunt ondersteuning krijgen[hier](https://forum.groupdocs.com/c/editor/20).