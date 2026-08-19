---
date: 2026-05-12
description: Leer hoe u lettertypen en andere HTML‑bronnen uit documenten kunt extraheren
  met GroupDocs.Editor for .NET. Stapsgewijze handleiding voor .NET‑ontwikkelaars.
keywords:
- how to extract fonts
- GroupDocs.Editor .NET
- extract HTML resources
linktitle: HTML‑bronnen opslaan in map
schemas:
- author: GroupDocs
  dateModified: '2026-05-12'
  description: Learn how to extract fonts and other HTML resources from documents
    using GroupDocs.Editor for .NET. Step‑by‑step guide for .NET developers.
  headline: How to Extract Fonts and Save HTML Resources to Folder
  type: TechArticle
- description: Learn how to extract fonts and other HTML resources from documents
    using GroupDocs.Editor for .NET. Step‑by‑step guide for .NET developers.
  name: How to Extract Fonts and Save HTML Resources to Folder
  steps:
  - name: '**Basic Knowledge of C# and .NET** – Familiarity with C# programming language
      and .NET framework is essential to follow along with the examples.'
    text: '**Basic Knowledge of C# and .NET** – Familiarity with C# programming language
      and .NET framework is essential to follow along with the examples.'
  - name: '**GroupDocs.Editor for .NET Library** – Download and install GroupDocs.Editor
      for .NET library from the [website](https://releases.groupdocs.com/editor/net/).'
    text: '**GroupDocs.Editor for .NET Library** – Download and install GroupDocs.Editor
      for .NET library from the [website](https://releases.groupdocs.com/editor/net/).'
  - name: '**Development Environment** – Set up your preferred development environment
      such as Visual Studio or any other compatible IDE.'
    text: '**Development Environment** – Set up your preferred development environment
      such as Visual Studio or any other compatible IDE.'
  type: HowTo
- questions:
  - answer: Yes, it supports Excel, PowerPoint, PDF, HTML, and over 50 additional
      formats for both editing and resource extraction.
    question: Is GroupDocs.Editor compatible with other document formats besides Word?
  - answer: Absolutely. The API works seamlessly with ASP.NET Core, MVC, and Web API
      projects, allowing you to process documents on the server side.
    question: Can I integrate GroupDocs.Editor into a web application?
  - answer: Yes, it includes built‑in connectors for Google Drive, Dropbox, OneDrive,
      and Amazon S3, enabling direct loading and saving of documents in the cloud.
    question: Does GroupDocs.Editor provide cloud storage integration?
  - answer: A fully functional 30‑day trial can be downloaded from the GroupDocs website
      without any credit‑card requirement.
    question: Is there a free trial available for GroupDocs.Editor?
  - answer: You can reach the GroupDocs support team via the official forum, submit
      a ticket through the customer portal, or consult the detailed API documentation.
    question: How can I get technical support for extraction issues?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Hoe lettertypen te extraheren en HTML‑bronnen op te slaan in een map
type: docs
url: /nl/net/document-editing/save-html-resources-to-folder/
weight: 13
---

# Hoe lettertypen extraheren en HTML‑resources opslaan in map

## Inleiding
GroupDocs.Editor for .NET laat je **how to extract fonts** en andere assets uit een document halen tijdens het converteren naar HTML. Met een paar regels C# kun je afbeeldingen, stylesheets en lettertypebestanden ophalen en ze opslaan in een map naar keuze. Deze tutorial leidt je door de volledige workflow, van het initialiseren van de editor tot het opslaan van elke resource op schijf.

## Snelle antwoorden
- **Wat betekent “how to extract fonts”?** Het is het proces van het ophalen van ingebedde lettertypebestanden uit een brondocument tijdens HTML-conversie.  
- **Welke bibliotheek behandelt dit?** GroupDocs.Editor for .NET biedt een speciale API voor het extraheren van lettertypen, afbeeldingen en stylesheets.  
- **Heb ik een licentie nodig?** Een gratis proefversie is beschikbaar; een commerciële licentie is vereist voor productiegebruik.  
- **Welke .NET‑versies worden ondersteund?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.  
- **Kan ik een aangepaste map targeten?** Ja, je geeft elk beschrijfbaar pad op bij het opslaan van de geëxtraheerde resources.

## Wat is “how to extract fonts”?
**How to extract fonts** verwijst naar het ophalen van de originele lettertypebestanden die in een brondocument zijn ingebed (bijv. DOCX, PPTX) zodat ze door de gegenereerde HTML kunnen worden geraadpleegd. Dit zorgt ervoor dat tekst exact wordt weergegeven zoals bedoeld in browsers, zonder afhankelijk te zijn van systeembrede lettertypen.

## Waarom GroupDocs.Editor gebruiken voor HTML‑resource‑extractie?
GroupDocs.Editor ondersteunt **meer dan 50 invoer‑ en uitvoerformaten** — waaronder DOCX, PPTX, PDF en HTML — en kan documenten verwerken met **tot 300 pagina’s** zonder het volledige bestand in het geheugen te laden. De API extraheert lettertypen, afbeeldingen en CSS in één enkele stap, waardoor de ontwikkelingstijd met tot **70 %** wordt verminderd ten opzichte van handmatige parsing.

## Vereisten
Voordat je aan de tutorial begint, zorg dat je de volgende vereisten hebt:
1. **Basiskennis van C# en .NET** – Vertrouwdheid met de programmeertaal C# en het .NET‑framework is essentieel om de voorbeelden te kunnen volgen.  
2. **GroupDocs.Editor for .NET‑bibliotheek** – Download en installeer de GroupDocs.Editor for .NET‑bibliotheek vanaf de [website](https://releases.groupdocs.com/editor/net/).  
3. **Ontwikkelomgeving** – Stel je favoriete ontwikkelomgeving in, zoals Visual Studio of een andere compatibele IDE.

## Namespaces importeren
Om te beginnen, importeer de benodigde namespaces in je C#‑project:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```

## Hoe lettertypen extraheren en HTML‑resources opslaan in een map?
Laad je brondocument met `Editor editor = new Editor("sample.docx", new WordProcessingLoadOptions());` en roep vervolgens `editor.Save("output.html", SaveOptions.Html);` aan. Na de opslaan‑operatie bevat de `Resources`‑collectie alle geëxtraheerde assets — inclusief lettertypen — die je kunt itereren en naar schijf kunt schrijven. Deze één‑stap‑benadering behandelt zowel conversie als resource‑extractie automatisch.

## Stap 1: GroupDocs.Editor initialiseren
`Editor` is de kernklasse die het laden, converteren en extraheren van resources van documenten coördineert. Het vertegenwoordigt een enkele documentsessie in het geheugen.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
Initialiseer eerst het `Editor`‑object door het pad naar je voorbeelddocument op te geven. In dit voorbeeld gebruiken we een Word‑document, dus geven we `WordProcessingLoadOptions` op als het documenttype.

## Stap 2: Document bewerken
`EditableDocument` is de bewerkbare weergave die wordt geretourneerd door de `Edit`‑methode, waardoor je het document kunt aanpassen voordat je het opslaat.

```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
Maak vervolgens een `EditableDocument`‑object aan door de `Edit`‑methode van het `Editor`‑object aan te roepen. Hiermee kun je bewerkingsbewerkingen op het document uitvoeren.

## Stap 3: Resources extraheren
`Resources` is een collectie die geëxtraheerde assets — afbeeldingen, lettertypen en stylesheets — groepeert in aparte lijsten voor eenvoudige verwerking.

```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
Extraheer resources zoals afbeeldingen, lettertypen en stylesheets uit het document en sla ze op in de respectieve lijsten.

## Stap 4: Output‑map opgeven
`outputFolder` is een string die aangeeft waar de geëxtraheerde bestanden worden weggeschreven. Je kunt deze naar elke beschrijfbare map op de server of lokale machine laten wijzen.

```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
Definieer de output‑map waarin de geëxtraheerde resources worden opgeslagen. Je kunt het mappad aanpassen aan je vereisten.

## Stap 5: Resources opslaan
`SaveResource` is een hulproutine die een enkele binaire resource (afbeelding, lettertype of stylesheet) naar het bestandssysteem schrijft.

```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
Loop door elke afbeeldingsresource, sla deze op in de output‑map en toon relevante informatie zoals bestandsnaam, type en afmetingen.

```csharp
		foreach (FontResourceBase oneFont in fonts)
		{
			Console.WriteLine("Saving {0} of {1} type",
				oneFont.FilenameWithExtension, oneFont.Type.FormalName);
			oneFont.Save(Path.Combine(outputFolder, oneFont.FilenameWithExtension));
		}
```
Sla op dezelfde manier elk lettertype‑resource op in de output‑map.

```csharp
		foreach (CssText oneStylesheet in stylesheets)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} encoding",
				oneStylesheet.FilenameWithExtension, oneStylesheet.Type.FormalName, oneStylesheet.Encoding);
			oneStylesheet.Save(Path.Combine(outputFolder, oneStylesheet.FilenameWithExtension));
		}
	}
}
```
Sla tenslotte elke stylesheet op in de output‑map en voltooi het bewerkingsproces.

## Veelvoorkomende problemen en oplossingen
- **Ontbrekende lettertypen na conversie** – Zorg ervoor dat het brondocument de lettertypen daadwerkelijk embedt; anders kan GroupDocs.Editor alleen systeemlettertypen refereren.  
- **Toegang geweigerd‑fouten** – Controleer of het toepassingsproces schrijfrechten heeft voor de doel‑output‑map.  
- **Grote documenten veroorzaken hoog geheugenverbruik** – Gebruik `LoadOptions` met `LoadMode = LoadMode.Stream` om grote bestanden te streamen in plaats van ze volledig in het geheugen te laden.

## Veelgestelde vragen

**Q: Is GroupDocs.Editor compatibel met andere documentformaten naast Word?**  
A: Ja, het ondersteunt Excel, PowerPoint, PDF, HTML en meer dan 50 extra formaten voor zowel bewerken als resource‑extractie.

**Q: Kan ik GroupDocs.Editor integreren in een webapplicatie?**  
A: Absoluut. De API werkt naadloos met ASP.NET Core, MVC en Web API‑projecten, waardoor je documenten aan de serverkant kunt verwerken.

**Q: Biedt GroupDocs.Editor cloud‑opslagintegratie?**  
A: Ja, het bevat ingebouwde connectors voor Google Drive, Dropbox, OneDrive en Amazon S3, waarmee je documenten direct in de cloud kunt laden en opslaan.

**Q: Is er een gratis proefversie beschikbaar voor GroupDocs.Editor?**  
A: Een volledig functionele 30‑daagse proefversie kan worden gedownload van de GroupDocs‑website zonder creditcard.

**Q: Hoe kan ik technische ondersteuning krijgen voor extractie‑problemen?**  
A: Je kunt het GroupDocs‑supportteam bereiken via het officiële forum, een ticket indienen via het klantportaal, of de gedetailleerde API‑documentatie raadplegen.

---

**Laatst bijgewerkt:** 2026-05-12  
**Getest met:** GroupDocs.Editor 23.11 for .NET  
**Auteur:** GroupDocs

## Gerelateerde tutorials

- [Efficiënt documenten bewerken met GroupDocs.Editor .NET: HTML omzetten naar bewerkbare documenten](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)
- [DOCX-resources efficiënt extraheren en opslaan met GroupDocs.Editor .NET - Complete gids](/editor/net/document-saving/efficient-extract-save-docx-resources-groupdocs-editor-net/)
- [Documentbewerking en conversie beheersen met GroupDocs.Editor .NET: Een complete gids](/editor/net/document-editing/groupdocs-editor-net-mastering-document-editing/)