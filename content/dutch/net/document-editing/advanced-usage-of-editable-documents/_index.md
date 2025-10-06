---
title: Geavanceerd gebruik van bewerkbare documenten
linktitle: Geavanceerd gebruik van bewerkbare documenten
second_title: GroupDocs.Editor .NET API
description: Leer geavanceerd gebruik van GroupDocs.Editor voor .NET bij het programmatisch maken, bewerken en extraheren van bronnen uit documenten.
weight: 11
url: /nl/net/document-editing/advanced-usage-of-editable-documents/
type: docs
---
# Geavanceerd gebruik van bewerkbare documenten

## Invoering
Als u een .NET-ontwikkelaar bent en uw documentbewerkingsmogelijkheden wilt verbeteren, biedt GroupDocs.Editor voor .NET een krachtig pakket tools. Deze uitgebreide handleiding leidt u door het geavanceerde gebruik van bewerkbare documenten met GroupDocs.Editor, waarbij elke stap gedetailleerd wordt beschreven om ervoor te zorgen dat u het volledige potentieel ervan kunt benutten.
## Vereisten
Voordat u in de geavanceerde functionaliteiten duikt, moet u ervoor zorgen dat u over het volgende beschikt:
- Visual Studio is geïnstalleerd op uw ontwikkelmachine.
- .NET Framework compatibel met GroupDocs.Editor.
-  GroupDocs.Editor voor .NET-bibliotheek. Jij kan[download het hier](https://releases.groupdocs.com/editor/net/).
-  Een geldige GroupDocs.Editor-licentie. Je kunt een[gratis proefperiode](https://releases.groupdocs.com/) of koop een[tijdelijke licentie](https://purchase.groupdocs.com/temporary-license/).
## Naamruimten importeren
Zorg er om te beginnen voor dat u de benodigde naamruimten in uw .NET-project importeert:
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
## Stap 1: Een EditableDocument-exemplaar maken
 Eerst moet u een exemplaar maken van`EditableDocument` door een invoerdocument van een ondersteund formaat te laden en te bewerken.
```csharp
string inputFilePath = "YourSampleDocument.docx";
Editor editor = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```
In deze stap laden we het invoerdocument en maken het gereed voor bewerking.
## Stap 2: Documentbronnen extraheren
 De`EditableDocument` bevat verschillende bronnen die kunnen worden geëxtraheerd en gemanipuleerd. Laten we deze opsplitsen:
### Stap 2.1: Pak het volledige document uit als HTML
U kunt één enkele tekenreeks genereren die het hele document bevat, met alle bronnen ingesloten als HTML.
```csharp
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```
Deze tekenreeks zal behoorlijk groot zijn, omdat deze stylesheets, afbeeldingen en lettertypen bevat die zijn gecodeerd in base64.
### Stap 2.2: Extraheer alle afbeeldingen
Extraheer alle afbeeldingen uit het document.
```csharp
List<IImageResource> allImages = beforeEdit.Images;
```
### Stap 2.3: Pak alle lettertypen uit
Pak alle lettertypen uit die in het document worden gebruikt.
```csharp
List<FontResourceBase> allFonts = beforeEdit.Fonts;
```
### Stap 2.4: Pak alle stylesheets uit
Pak alle stylesheets uit in een tekstformaat.
```csharp
List<CssText> allStylesheets = beforeEdit.Css;
```
### Stap 2.5: Verzamel alle bronnen
Verzamel alle bronnen in één gesprek.
```csharp
List<IHtmlResource> allResources = beforeEdit.AllResources;
```
Dit omvat afbeeldingen, lettertypen en stylesheets.
### Stap 2.6: Verkrijg HTML-markeringen
Haal de HTML-opmaak van het document op zonder ingesloten bronnen.
```csharp
string htmlMarkup = beforeEdit.GetContent();
```
## Stap 3: Externe links aanpassen
Soms moet u externe links aanpassen zodat ze naar een aangepaste resourcehandler verwijzen. Hier leest u hoe u het moet doen:
### Stap 3.1: Aangepaste voorvoegsels voorbereiden
Bereid voorvoegsels voor die vóór originele externe links staan.
```csharp
string customImagesRequesthandlerUri = "http://voorbeeld.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://voorbeeld.com/CssHandler/id=”;
string customFontsRequesthandlerUri = "http://voorbeeld.com/FontsHandler/id=”;
```
### Stap 3.2: Genereer vooraf ingestelde HTML-opmaak
Genereer HTML-opmaak met aangepaste links.
```csharp
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```
### Stap 3.3: Verkrijg HTML-inhoud die alleen in het hoofdgedeelte staat
Sommige WYSIWYG-editors verwerken alleen pure HTML-opmaak zonder headers.
```csharp
string onlyBodyContent = beforeEdit.GetBodyContent();
```
### Stap 3.4: Vooraf ingestelde alleen-inhoud
Genereer alleen inhoud met aangepaste afbeeldingsvoorvoegsels.
```csharp
string prefixedBodyContent = beforeEdit.GetBodyContent(customImagesRequesthandlerUri);
```
### Stap 3.5: Stylesheets extraheren
Extraheer stylesheets die in het document worden gebruikt.
```csharp
List<string> stylesheets = beforeEdit.GetCssContent();
```
### Stap 3.6: Vooraf ingestelde stijlbladen
Extraheer stylesheets met aangepaste voorvoegsels.
```csharp
List<string> prefixedStylesheets = beforeEdit.GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri);
```
## Stap 4: Document opslaan als HTML
Sla het bewerkte document op als HTML-bestand, inclusief de bronnen.
```csharp
string htmlFilePath = Path.Combine("output", Path.GetFileNameWithoutExtension(inputFilePath) + ".html");
beforeEdit.Save(htmlFilePath);
```
Met deze methode wordt een aparte map gemaakt voor bronnen zoals stylesheets, afbeeldingen en lettertypen.
## Stap 5: EditableDocument verwijderen
 EditableDocument-implementen`IDisposable` en biedt de mogelijkheid om te controleren of de instantie is verwijderd.
```csharp
Console.WriteLine("EditableDocument is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");
```
### Stap 5.1 Afhandeling van een afvoergebeurtenis
U kunt zich ook abonneren op het afvoerevenement.
```csharp
EventHandler someMethod = delegate { Console.WriteLine("Disposing event was spotted!"); };
beforeEdit.Disposed += someMethod;
```
## Stap 6: Een bewerkbaar document maken van HTML
Maak een exemplaar van EditableDocument van een HTML-document.
### Stap 6.1: Van HTML-bestand
```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
```
### Stap 6.2: Van HTML-opmaak
```csharp
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);
```
Deze exemplaren (afterEditFromFile en afterEditFromMarkup) zijn identiek aan het origineel (beforeEdit).
## Stap 7: Handmatige verwijdering
Verwijder uw EditableDocument-exemplaren handmatig.
```csharp
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```
Dit zorgt voor een goede opruiming van hulpbronnen.
## Conclusie
GroupDocs.Editor voor .NET biedt robuuste tools voor het programmatisch bewerken van documenten. Door deze stapsgewijze handleiding te volgen, kunt u de documentinhoud, bronnen en uitvoerformaten efficiënt beheren. Of u nu bronnen insluit, externe links aanpast of documenten naar HTML converteert, GroupDocs.Editor voorziet u van de functionaliteit die nodig is voor geavanceerde documentmanipulatie.
## Veelgestelde vragen
### Welke formaten ondersteunt GroupDocs.Editor?
GroupDocs.Editor ondersteunt verschillende formaten, waaronder DOCX, XLSX, PPTX en meer.
### Kan ik GroupDocs.Editor zonder licentie gebruiken?
 Ja, je kunt het gebruiken met een[gratis proefperiode](https://releases.groupdocs.com/) of een[tijdelijke licentie](https://purchase.groupdocs.com/temporary-license/).
### Hoe haal ik specifieke bronnen uit een document?
 U kunt afbeeldingen, lettertypen en stylesheets extraheren met behulp van de meegeleverde methoden, zoals`Images`, `Fonts` , En`Css`.
### Is het mogelijk om links in de HTML-uitvoer aan te passen?
Ja, u kunt externe links aanpassen door aangepaste voorvoegsels op te geven voor afbeeldingen, CSS en lettertypen.
### Hoe sla ik een bewerkt document op als HTML-bestand?
 Gebruik de`Save` werkwijze van de`EditableDocument`class om het document op te slaan als een HTML-bestand, inclusief de bronnen.