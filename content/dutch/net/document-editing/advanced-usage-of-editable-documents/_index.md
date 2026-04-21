---
date: 2026-03-14
description: Leer hoe je afbeeldingen uit DOCX kunt extraheren, DOCX kunt converteren
  naar HTML en het document als HTML kunt opslaan met GroupDocs.Editor voor .NET.
linktitle: Extract Images from DOCX – Advanced Editable Document Usage
second_title: GroupDocs.Editor .NET API
title: Afbeeldingen uit DOCX extraheren – Geavanceerd bewerkbaar documentgebruik
type: docs
url: /nl/net/document-editing/advanced-usage-of-editable-documents/
weight: 11
---

# Afbeeldingen extraheren uit DOCX – Geavanceerd gebruik van bewerkbare documenten

Als je een .NET‑ontwikkelaar bent die **afbeeldingen uit DOCX** wil extraheren en je documentbewerkingsmogelijkheden wil verbeteren, biedt GroupDocs.Editor voor .NET een krachtige reeks tools. Deze uitgebreide gids leidt je door het geavanceerde gebruik van bewerkbare documenten met GroupDocs.Editor, waarbij elke stap in detail wordt uitgelegd zodat je het volledige potentieel kunt benutten.

## Quick Answers
- **Hoe kan ik afbeeldingen uit een DOCX‑bestand extraheren?** Gebruik `EditableDocument.Images` nadat je het document hebt geladen met `Editor`.
- **Kan ik DOCX naar HTML converteren met ingesloten bronnen?** Ja—roep `EditableDocument.GetEmbeddedHtml()` of `GetContent()` aan voor HTML‑markup.
- **Welke methode slaat het bewerkte document op als HTML?** `EditableDocument.Save(htmlFilePath)` maakt een HTML‑bestand met een resource‑map.
- **Is het mogelijk om lettertypen uit een Word‑document te extraheren?** Gebruik `EditableDocument.Fonts` om alle font‑resources op te halen.
- **Heb ik een licentie nodig voor productiegebruik?** Een geldige GroupDocs.Editor‑licentie is vereist; een gratis proefversie is beschikbaar.

## Wat is **extract images from docx**?
Het extraheren van afbeeldingen uit een DOCX‑bestand betekent dat je programmatically elk in het Word‑document ingesloten plaatje ophaalt zodat je ze apart kunt hergebruiken, aanpassen of opslaan. GroupDocs.Editor maakt de `Images`‑collectie beschikbaar op een `EditableDocument`‑instantie, waardoor deze taak eenvoudig wordt.

## Waarom GroupDocs.Editor gebruiken voor deze workflow?
- **Volledige controle** over documentbronnen (afbeeldingen, lettertypen, CSS) zonder handmatige ZIP‑verwerking.  
- **Naadloze conversie** van DOCX naar HTML met behoud van lay-out en opmaak.  
- **Eenvoudige extractie van bronnen** voor aangepaste afbeeldingsverwerking, lettertype‑inbedding of CDN‑levering.  
- **Robuust disposingspatroon** zorgt voor geen geheugenlekken in langdurige services.

## Prerequisites
- Visual Studio geïnstalleerd op je ontwikkelmachine.  
- .NET Framework compatibel met GroupDocs.Editor.  
- GroupDocs.Editor voor .NET bibliotheek. Je kunt het [hier downloaden](https://releases.groupdocs.com/editor/net/).  
- Een geldige GroupDocs.Editor‑licentie. Je kunt een [gratis proefversie](https://releases.groupdocs.com/) krijgen of een [tijdelijke licentie](https://purchase.groupdocs.com/temporary-license/) aanschaffen.

## Import Namespaces
Om te beginnen, zorg ervoor dat je de benodigde namespaces importeert in je .NET‑project:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```

## Step 1: Creating an EditableDocument Instance
Eerst moet je een instantie van `EditableDocument` maken door een invoerdocument van een ondersteund formaat te laden en te bewerken.

```csharp
string inputFilePath = "YourSampleDocument.docx";
Editor editor = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```

In deze stap laden we het invoerdocument en bereiden het voor op bewerking.

## How to **extract images from DOCX**?
Hieronder duiken we in de mogelijkheden voor resource‑extractie, beginnend met de meest voorkomende behoefte—alle afbeeldingen uit een Word‑bestand halen.

## Step 2: Extracting Document Resources
De `EditableDocument` bevat verschillende resources die geëxtraheerd en gemanipuleerd kunnen worden. Laten we deze opsplitsen:

### Step 2.1: Extract Entire Document as HTML
Je kunt een enkele string genereren die het volledige document bevat met al zijn resources ingesloten als HTML.

```csharp
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```

Deze string zal behoorlijk groot zijn omdat hij stylesheets, afbeeldingen en lettertypen bevat die in base64 zijn gecodeerd.

### Step 2.2: Extract All Images *(primary keyword in action)*
Exporteer alle afbeeldingen uit het document—dit is de kern van **extract images from docx**.

```csharp
List<IImageResource> allImages = beforeEdit.Images;
```

### Step 2.3: Extract All Fonts *(secondary keyword)*
Als je ook **fonts uit Word moet extraheren**, gebruik dan de volgende aanroep:

```csharp
List<FontResourceBase> allFonts = beforeEdit.Fonts;
```

### Step 2.4: Extract All Stylesheets
Exporteer alle stylesheets in een tekstueel formaat.

```csharp
List<CssText> allStylesheets = beforeEdit.Css;
```

### Step 2.5: Gather All Resources
Verzamel alle resources in één aanroep.

```csharp
List<IHtmlResource> allResources = beforeEdit.AllResources;
```

Dit omvat afbeeldingen, lettertypen en stylesheets.

### Step 2.6: Obtain HTML Markup
Haal de HTML‑markup van het document op zonder ingesloten resources.

```csharp
string htmlMarkup = beforeEdit.GetContent();
```

## How to **convert docx to html** with custom handling?
Soms moet je externe links aanpassen zodat ze naar je eigen resource‑handlers wijzen.

## Step 3: Adjusting External Links
### Step 3.1: Prepare Custom Prefixes
Bereid prefixes voor die de oorspronkelijke externe links zullen voorafgaan.

```csharp
string customImagesRequesthandlerUri = "http://example.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://example.com/CssHandler/id=";
string customFontsRequesthandlerUri = "http://example.com/FontsHandler/id=";
```

### Step 3.2: Generate Prefixed HTML Markup
Genereer HTML‑markup met aangepaste links.

```csharp
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```

### Step 3.3: Obtain Body-Only HTML Content
Sommige WYSIWYG‑editors verwerken alleen pure HTML‑markup zonder headers.

```csharp
string onlyBodyContent = beforeEdit.GetBodyContent();
```

### Step 3.4: Prefixed Body-Only Content
Genereer body‑only content met aangepaste afbeeldings‑prefixes.

```csharp
string prefixedBodyContent = beforeEdit.GetBodyContent(customImagesRequesthandlerUri);
```

### Step 3.5: Extract Stylesheets
Exporteer de stylesheets die in het document worden gebruikt.

```csharp
List<string> stylesheets = beforeEdit.GetCssContent();
```

### Step 3.6: Prefixed Stylesheets
Exporteer stylesheets met aangepaste prefixes.

```csharp
List<string> prefixedStylesheets = beforeEdit.GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri);
```

## How to **save document as html** correctly?
## Step 4: Save Document as HTML
Sla het bewerkte document op als een HTML‑bestand, inclusief de bijbehorende resources.

```csharp
string htmlFilePath = Path.Combine("output", Path.GetFileNameWithoutExtension(inputFilePath) + ".html");
beforeEdit.Save(htmlFilePath);
```

Deze methode maakt een aparte directory aan voor resources zoals stylesheets, afbeeldingen en lettertypen.

## Step 5: Disposing of EditableDocument
`EditableDocument` implementeert `IDisposable` en biedt de mogelijkheid om te controleren of de instantie is disposed.

```csharp
Console.WriteLine("EditableDocument is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");
```

### Step 5.1 Handling Dispose Event
Je kunt je ook abonneren op het disposing‑event.

```csharp
EventHandler someMethod = delegate { Console.WriteLine("Disposing event was spotted!"); };
beforeEdit.Disposed += someMethod;
```

## Step 6: Creating EditableDocument from HTML
Maak een instantie van `EditableDocument` aan vanuit een HTML‑document.

### Step 6.1: From HTML File

```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
```

### Step 6.2: From HTML Markup

```csharp
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);
```

Deze instanties (`afterEditFromFile` en `afterEditFromMarkup`) zijn identiek aan de originele (`beforeEdit`).

## Step 7: Manual Disposal
Dispose handmatig je `EditableDocument`‑instanties.

```csharp
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```

Dit zorgt voor een correcte opruiming van resources.

## Common Issues and Solutions
- **Afbeeldingen verschijnen niet na extractie:** Controleer of het document daadwerkelijk ingesloten afbeeldingen bevat en of je `beforeEdit.Images` benadert na het aanroepen van `Edit`.  
- **Lettertypen ontbreken in HTML‑output:** Zorg ervoor dat je `GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri)` aanroept om font‑URL’s correct in te sluiten.  
- **Grote HTML‑strings veroorzaken geheugen‑druk:** Gebruik `GetContent()` voor markup zonder ingesloten resources en serveer afbeeldingen/CSS vanuit afzonderlijke bestanden.

## Frequently Asked Questions

**Q: Welke formaten ondersteunt GroupDocs.Editor?**  
A: GroupDocs.Editor ondersteunt DOCX, XLSX, PPTX en vele andere populaire office‑formaten.

**Q: Kan ik GroupDocs.Editor gebruiken zonder licentie?**  
A: Ja, je kunt het gebruiken met een [gratis proefversie](https://releases.groupdocs.com/) of een [tijdelijke licentie](https://purchase.groupdocs.com/temporary-license/).

**Q: Hoe haal ik specifieke resources uit een document?**  
A: Gebruik de `Images`, `Fonts` en `Css` collecties op de `EditableDocument`‑instantie.

**Q: Is het mogelijk om links in de HTML‑output aan te passen?**  
A: Ja, geef aangepaste URI‑prefixes door aan `GetContent` of `GetBodyContent` om afbeeldings‑, CSS‑ en font‑links te herschrijven.

**Q: Hoe sla ik een bewerkt document op als een HTML‑bestand?**  
A: Roep de `Save`‑methode aan op de `EditableDocument`‑instantie en geef een pad op dat eindigt op `.html`.

---

**Last Updated:** 2026-03-14  
**Tested With:** GroupDocs.Editor voor .NET (latest release)  
**Author:** GroupDocs