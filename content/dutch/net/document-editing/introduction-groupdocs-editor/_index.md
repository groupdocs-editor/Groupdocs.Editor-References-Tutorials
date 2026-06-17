---
date: 2026-04-11
description: Leer hoe je via code een Word‑document kunt bewerken met GroupDocs.Editor
  voor .NET en Word naar RTF kunt converteren in deze gedetailleerde stap‑voor‑stap‑gids.
keywords:
- programmatically edit word document
- convert pdf to editable
- replace text in document
- convert word to rtf
- save document to stream
linktitle: Programmeermatig Word‑document bewerken met GroupDocs.Editor voor .NET
second_title: GroupDocs.Editor .NET API
title: Word-document programmatically bewerken met GroupDocs.Editor voor .NET
type: docs
url: /nl/net/document-editing/introduction-groupdocs-editor/
weight: 12
---

# Programmamatig bewerken van Word‑documenten met GroupDocs.Editor voor .NET

Als je een .NET‑ontwikkelaar bent die **programmatig Word‑documenten** moet bewerken — of het nu gaat om tekst vervangen, formaten converteren of het resultaat in een stream inbedden — is GroupDocs.Editor voor .NET een robuuste, gebruiksvriendelijke bibliotheek die de klus klaart. In deze tutorial lopen we een praktisch voorbeeld door dat laat zien hoe je een DOCX‑bestand laadt, de inhoud bewerkt, het resultaat naar RTF converteert en opslaat, hetzij op schijf, hetzij in een geheugen‑stream.

## Snelle antwoorden
- **Wat kan ik bewerken?** Word, PDF, HTML, RTF en vele andere formaten.  
- **Kan ik tekst vervangen?** Ja — gebruik eenvoudige tekenreeksvervanging of meer geavanceerde DOM‑manipulatie.  
- **Hoe converteer ik PDF naar bewerkbaar?** Laad de PDF met `Editor` en bewerk de gegenereerde HTML.  
- **Wat is de gemakkelijkste manier om naar een stream op te slaan?** Gebruik `editor.Save(editableDoc, stream, options)`.  
- **Heb ik een licentie nodig?** Een tijdelijke of volledige licentie is vereist voor productiegebruik.

## Wat betekent programmatig bewerken van een Word‑document?
Programmatig bewerken van een Word‑document betekent dat je met code — in plaats van een gebruikersinterface — een bestand opent, de inhoud (tekst, afbeeldingen, stijlen) wijzigt en de aangepaste versie terugschrijft naar opslag. Deze aanpak maakt geautomatiseerde rapportage, bulk‑documentupdates en aangepaste contentgeneratie mogelijk.

## Waarom GroupDocs.Editor voor .NET gebruiken?
- **Formaatflexibiliteit:** Laad DOCX, PDF, HTML, RTF, enzovoort en sla op in elk ondersteund formaat.  
- **Geen Office‑afhankelijkheid:** Werkt zonder Microsoft Office geïnstalleerd op de server.  
- **Stream‑vriendelijk:** Perfect voor cloudscenario's waarbij je leest/schrijft vanuit streams in plaats van het bestandssysteem.  
- **Rijke API:** Toegang tot afbeeldingen, lettertypen, CSS en andere bronnen voor volledig uitgeruste bewerking.

## Vereisten
Zorg ervoor dat je het volgende hebt voordat we beginnen:

- Visual Studio 2017 of nieuwer.  
- .NET Framework 4.6.1 of nieuwer.  
- GroupDocs.Editor voor .NET – je kunt het [downloaden](https://releases.groupdocs.com/editor/net/) vanaf de site.  
- Een geldige licentie of een [tijdelijke licentie](https://purchase.groupdocs.com/temporary-license/) van GroupDocs.

## Namespaces importeren
Om GroupDocs.Editor voor .NET te gebruiken, importeer je de benodigde namespaces:

```csharp
using System;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```

In de volgende secties splitsen we de workflow op in hapklare stappen zodat je gemakkelijk kunt volgen.

## Stap 1: Een pad naar het invoerbestand verkrijgen
Geef de locatie op van het Word‑bestand dat je wilt bewerken. Voor dit voorbeeld gaan we uit van een DOCX met de naam **Your Sample Document.docx**.

```csharp
string inputFilePath = "Your Sample Document.docx";
```

## Stap 2: Het Editor‑object instantieren
Maak een `Editor`‑instantie aan door het invoerpad door te geven. Dit laadt het document en maakt het klaar voor bewerking.

```csharp
using (GroupDocs.Editor.Editor editor = new Editor(inputFilePath))
{
    // Subsequent steps will be nested inside this block
}
```

## Stap 3: Het document openen voor bewerking
Verkrijg een `EditableDocument` die je toegang geeft tot de HTML‑representatie van het document en de bijbehorende bronnen.

```csharp
EditableDocument beforeEdit = editor.Edit();
```

## Stap 4: Documentinhoud en bronnen ophalen
Je kunt de ruwe HTML, afbeeldingen, lettertypen en CSS ophalen. Dit is handig wanneer je de markup direct wilt manipuleren.

```csharp
string content = beforeEdit.GetContent();
var images = beforeEdit.Images;
var fonts = beforeEdit.Fonts;
var stylesheets = beforeEdit.Css;
```

### Stap 4.1: Document ophalen als één Base64‑gecodeerde tekenreeks
Als je liever één tekenreeks hebt die alle ingesloten bronnen bevat, roep je `GetEmbeddedHtml()` aan.

```csharp
string allEmbeddedInsideString = beforeEdit.GetEmbeddedHtml();
```

### Stap 4.2: De inhoud bewerken
Laten we het woord **Subtitle** vervangen door **Edited subtitle** om een eenvoudige tekstvervanging te demonstreren.

```csharp
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
```

## Stap 5: Een nieuw EditableDocument‑object maken
Na het bewerken van de markup, wikkel je het terug in een `EditableDocument`‑object.

```csharp
EditableDocument afterEdit = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```

## Stap 6: Het bewerkte document opslaan
We slaan het resultaat op als een RTF‑bestand, waarbij we zowel een pad op het bestandssysteem als een geheugen‑stream laten zien.

### Stap 6.1: Het uitvoerpad voorbereiden
Definieer waar de RTF moet worden weggeschreven.

```csharp
string outputPath = Path.Combine("Output Directory Path", Path.GetFileNameWithoutExtension(inputFilePath) + ".rtf");
```

### Stap 6.2: Opslagopties voorbereiden
Selecteer het RTF‑formaat via `WordProcessingSaveOptions`.

```csharp
Options.WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
```

### Stap 6.3: Opslaan naar pad
Schrijf het bewerkte document naar het bestandssysteem.

```csharp
editor.Save(afterEdit, outputPath, saveOptions);
```

### Stap 6.4: Opslaan naar een stream
Als je het resultaat in het geheugen nodig hebt (bijvoorbeeld om te uploaden naar cloudopslag), gebruik dan een `MemoryStream`.

```csharp
using (MemoryStream ms = new MemoryStream())
{
    editor.Save(afterEdit, ms, saveOptions);
}
```

## Stap 7: De Editor‑ en EditableDocument‑instanties vrijgeven
Maak bronnen snel vrij om geheugenlekken te voorkomen.

```csharp
beforeEdit.Dispose();
afterEdit.Dispose();
editor.Dispose();
```

## Veelvoorkomende use‑cases & tips
- **PDF naar bewerkbaar converteren:** Laad een PDF met `Editor`, bewerk de gegenereerde HTML en sla vervolgens op als PDF of een ander formaat.  
- **Tekst in document vervangen:** Gebruik `string.Replace` voor eenvoudige gevallen of manipuleer de DOM voor complexe scenario's.  
- **Word naar RTF converteren:** Zoals hierboven getoond, stel `WordProcessingFormats.Rtf` in de opslagopties in.  
- **Document opslaan naar stream:** Ideaal voor web‑API’s die bestanden direct naar de client retourneren.  
- **Document laden voor bewerking:** Plaats de `Editor` altijd in een `using`‑blok om correcte vrijgave te garanderen.

## Veelgestelde vragen

**V: Kan ik PDF‑bestanden bewerken met GroupDocs.Editor voor .NET?**  
A: Ja, GroupDocs.Editor ondersteunt het bewerken van PDF’s door ze om te zetten naar een tussenliggende HTML‑representatie.

**V: Hoe krijg ik een tijdelijke licentie voor GroupDocs.Editor voor .NET?**  
A: Je kunt een tijdelijke licentie verkrijgen via de [GroupDocs‑website](https://purchase.groupdocs.com/temporary-license/).

**V: Welke bestandsformaten ondersteunt GroupDocs.Editor voor .NET?**  
A: DOCX, PDF, HTML, RTF en vele andere formaten worden ondersteund.

**V: Is het mogelijk om GroupDocs.Editor te integreren met cloudopslag?**  
A: Absoluut — je kunt streams lezen/schrijven vanuit Azure Blob, Amazon S3, Google Cloud Storage, enzovoort.

**V: Waar vind ik de documentatie voor GroupDocs.Editor voor .NET?**  
A: De documentatie is beschikbaar [hier](https://tutorials.groupdocs.com/editor/net/).

---

**Laatst bijgewerkt:** 2026-04-11  
**Getest met:** GroupDocs.Editor 23.12 voor .NET  
**Auteur:** GroupDocs