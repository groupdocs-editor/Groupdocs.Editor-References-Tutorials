---
date: 2026-09-26
description: Leer hoe je css-prefix kunt behandelen en css-inhoud kunt extraheren
  met GroupDocs.Editor voor .NET in deze gedetailleerde stapsgewijze tutorial.
keywords:
- handle css prefix
- extract css content
- edit document css
- prepend url to css
lastmod: 2026-09-26
linktitle: CSS-inhoud met prefix behandelen
og_description: Ontdek hoe je css-prefix kunt behandelen en css-inhoud kunt extraheren
  met GroupDocs.Editor voor .NET. Volg een stapsgewijze handleiding om URL's toe te
  voegen aan CSS-bronnen en stylesheets op te halen.
og_image_alt: Developer guide showing css prefix handling with GroupDocs.Editor for
  .NET
og_title: Hoe css-prefix te behandelen in GroupDocs.Editor voor .NET
schemas:
- author: GroupDocs
  dateModified: '2026-09-26'
  description: Learn how to handle css prefix and extract css content using GroupDocs.Editor
    for .NET in this detailed step‑by‑step tutorial.
  headline: How to handle css prefix in GroupDocs.Editor for .NET
  type: TechArticle
- questions:
  - answer: Yes, GroupDocs.Editor for .NET supports PDF, Word, Excel, PowerPoint,
      and many other formats.
    question: Can I use GroupDocs.Editor for .NET with other document formats?
  - answer: Absolutely! You can start your free trial on the [GroupDocs free trial
      page](https://releases.groupdocs.com/).
    question: Is there a free trial available for GroupDocs.Editor for .NET?
  - answer: You can obtain a temporary license from the [temporary license page](https://purchase.groupdocs.com/temporary-license/).
    question: How do I get a temporary license for GroupDocs.Editor for .NET?
  - answer: Detailed documentation is available on the [GroupDocs.Editor for .NET
      documentation site](https://tutorials.groupdocs.com/editor/net/).
    question: Where can I find detailed documentation for GroupDocs.Editor for .NET?
  - answer: You can get support through the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).
    question: What support options are available for GroupDocs.Editor for .NET?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
tags:
- css handling
- GroupDocs.Editor
- .NET document processing
- css prefix
- api tutorial
title: Hoe css-prefix te behandelen in GroupDocs.Editor voor .NET
type: docs
url: /nl/net/css-handling/handle-css-content-with-prefix/
weight: 11
---

# Hoe css‑prefix te verwerken in GroupDocs.Editor voor .NET

In deze tutorial leer je **hoe je css‑prefix moet verwerken** bij het werken met stylesheets binnen een document met GroupDocs.Editor voor .NET. Of je nu een URL moet toevoegen aan afbeeldingen, lettertypen of een andere externe bron, de onderstaande stappen laten precies zien hoe je **css‑prefix moet verwerken** en ook hoe je **css‑inhoud kunt extraheren** voor verdere verwerking. Aan het einde van de gids kun je resource‑paden herschrijven, de ruwe CSS‑strings ophalen en ze met vertrouwen integreren in je web‑workflow.

## Snelle antwoorden
- **Wat betekent “css‑prefix verwerken”?** Een aangepaste URL‑prefix toevoegen aan externe bronnen die in CSS worden verwezen.  
- **Welke API‑methode retourneert CSS‑stijlen?** `EditableDocument.GetCssContent(...)`.  
- **Heb ik een licentie nodig?** Een proeflicentie is beschikbaar; een commerciële licentie is vereist voor productie.  
- **Welke .NET‑versies worden ondersteund?** .NET Framework 4.5+ en .NET Core/5/6.  
- **Kan ik de prefix tijdens runtime wijzigen?** Ja – geef simpelweg een andere string door aan `GetCssContent`.

## Wat is css‑prefix verwerken?
De term verwijst naar het herschrijven van de URL‑s van afbeeldingen, lettertypen of andere externe assets in een CSS‑bestand zodat ze verwijzen naar een locatie die jij beheert, bijvoorbeeld een CDN of een beveiligde server. Door een consistente basis‑URL toe te voegen, zorg je ervoor dat elke resource correct wordt geladen wanneer het document wordt weergegeven in een browser of een web‑gebaseerde viewer.

## Waarom GroupDocs.Editor gebruiken om css‑inhoud te extraheren?
GroupDocs.Editor kan de originele CSS die in WordProcessing‑documenten is ingebed lezen, de ruwe stylesheet‑strings retourneren en je deze laten manipuleren vóór weergave of opslaan. Dit elimineert handmatig parsen, garandeert trouw aan de interne representatie van het document, en ondersteunt **30+ bestandsformaten** terwijl bestanden tot **500 MB** worden verwerkt zonder het volledige bestand in het geheugen te laden.

## Voorvereisten
Voordat we beginnen, zorg dat je de volgende zaken gereed hebt:
- Visual Studio: Je hebt een werkende installatie van Visual Studio nodig.  
- .NET Framework: Zorg dat het .NET Framework geïnstalleerd is.  
- GroupDocs.Editor voor .NET: Je kunt het downloaden van de [GroupDocs.Editor for .NET download page](https://releases.groupdocs.com/editor/net/).  
- Voorbeelddocument: Heb een voorbeelddocument klaar voor bewerking.

## Namespaces importeren
Laten we eerst de benodigde namespaces importeren zodat onze code soepel draait. Deze stap geeft ons toegang tot de kernklassen van GroupDocs.Editor.

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Editor.Options;
```

## Stap 1: De Editor initialiseren
De `Editor`‑klasse is het toegangspunt voor het werken met documenten in GroupDocs.Editor. Het beheert laad‑, bewerkings‑ en opslagoperaties.  
De eerste stap bestaat uit het maken van een `Editor`‑instantie met je voorbeelddocument. Dit zet de bewerkingsomgeving op.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```

## Stap 2: Het document bewerken
Het `EditableDocument`‑object vertegenwoordigt de bewerkbare versie van het bestand en geeft toegang tot de interne onderdelen, zoals CSS, afbeeldingen en HTML.  
Vervolgens verkrijgen we een `EditableDocument`‑object. Dit object stelt ons in staat om met de interne CSS van het document te werken.

```csharp
    using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
    {
```

## Stap 3: Externe prefixes instellen
Definieer de URL‑prefixes voor afbeeldingen en lettertypen. Deze prefixes worden toegevoegd aan elke afbeelding‑ en lettertype‑referentie die in de CSS wordt gevonden.

```csharp
        string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
        string externalFontsPrefix = "http://www.mywebsite.com/fonts/id=";
```

## Stap 4: css‑inhoud extraheren met de prefixes
`GetCssContent` retourneert een collectie van CSS‑stylesheet‑strings die al de door jou opgegeven geprefixede URL‑s bevatten.  
Roep `GetCssContent` aan en geef de zojuist gedefinieerde prefixes door. De methode retourneert een lijst van CSS‑stylesheet‑strings die al de geprefixede URL‑s bevatten.

```csharp
        List<string> stylesheets = document.GetCssContent(externalImagesPrefix, externalFontsPrefix);
```

## Stap 5: De resultaten weergeven
Print het aantal gevonden stylesheets en toon elke stylesheet. Dit helpt je te verifiëren dat de prefixes correct zijn toegepast.

```csharp
        Console.WriteLine("There are {0} stylesheets in the input document", stylesheets.Count);
        foreach (string css in stylesheets)
        {
            Console.WriteLine(css);
        }
    }
}
```

## Veelvoorkomende problemen en oplossingen
- **Geen stylesheets geretourneerd** – Zorg ervoor dat het bron‑document daadwerkelijk CSS bevat (bijv. een Word‑document met gestylede tabellen of ingebedde HTML).  
- **Onjuiste URL‑s** – Controleer of de prefix‑strings eindigen met het juiste scheidingsteken (`/` of `=`) voor je server‑routing.  
- **Prestatie‑zorgen** – Overweeg bij zeer grote documenten de stylesheets in batches te verwerken om hoog geheugenverbruik te vermijden.

## Veelgestelde vragen

**V: Kan ik GroupDocs.Editor voor .NET gebruiken met andere documentformaten?**  
A: Ja, GroupDocs.Editor voor .NET ondersteunt PDF, Word, Excel, PowerPoint, en vele andere formaten.

**V: Is er een gratis proefversie beschikbaar voor GroupDocs.Editor voor .NET?**  
A: Absoluut! Je kunt je gratis proefversie starten op de [GroupDocs free trial page](https://releases.groupdocs.com/).

**V: Hoe krijg ik een tijdelijke licentie voor GroupDocs.Editor voor .NET?**  
A: Je kunt een tijdelijke licentie verkrijgen via de [temporary license page](https://purchase.groupdocs.com/temporary-license/).

**V: Waar vind ik gedetailleerde documentatie voor GroupDocs.Editor voor .NET?**  
A: Gedetailleerde documentatie is beschikbaar op de [GroupDocs.Editor for .NET documentation site](https://tutorials.groupdocs.com/editor/net/).

**V: Welke ondersteuningsopties zijn er voor GroupDocs.Editor voor .NET?**  
A: Je kunt ondersteuning krijgen via het [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).

## Aanvullende veelgestelde vragen

**V: Kan ik de prefix wijzigen nadat ik de CSS heb geëxtraheerd?**  
A: Ja. Roep `GetCssContent` opnieuw aan met een andere prefix‑string; de methode gebruikt altijd de waarden die je tijdens runtime doorgeeft.

**V: Werkt dit met met wachtwoord beveiligde documenten?**  
A: Ja. Geef het wachtwoord op in `WordProcessingLoadOptions` bij het maken van de `Editor`‑instantie.

**V: Is het mogelijk de aangepaste CSS terug op te slaan in het document?**  
A: GroupDocs.Editor biedt momenteel alleen‑lezen toegang tot CSS. Om wijzigingen te behouden moet je het originele stylesheet vervangen via de onderliggende XML‑API's van het document.

---

**Last Updated:** 2026-09-26  
**Tested With:** GroupDocs.Editor 23.12 for .NET  
**Author:** GroupDocs

## Gerelateerde tutorials

- [Externe CSS extraheren uit Word‑documenten met GroupDocs.Editor .NET&#58; Een uitgebreide gids](/editor/net/html-web-documents/extract-external-css-word-docs-groupdocs-editor-dotnet/)
- [HTML extraheren & prefixen uit Word‑documenten met GroupDocs.Editor .NET](/editor/net/html-web-documents/groupdocs-editor-dotnet-extract-prefix-html-word-docs/)
- [Hoe HTML‑inhoud te extraheren en te wijzigen in Word‑documenten met GroupDocs.Editor .NET](/editor/net/html-web-documents/extract-modify-html-content-word-docs-groupdocs-editor-net/)