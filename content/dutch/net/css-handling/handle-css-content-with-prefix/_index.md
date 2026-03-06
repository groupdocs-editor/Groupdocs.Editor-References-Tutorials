---
date: 2026-03-06
description: Leer hoe u CSS-inhoud met een prefix kunt verwerken en CSS-inhoud kunt
  extraheren met GroupDocs.Editor voor .NET in deze gedetailleerde stapsgewijze tutorial.
linktitle: Handle CSS Content with Prefix
second_title: GroupDocs.Editor .NET API
title: CSS-inhoud met voorvoegsel behandelen
type: docs
url: /nl/net/css-handling/handle-css-content-with-prefix/
weight: 11
---

# CSS-inhoud behandelen met prefix

In deze tutorial ontdek je **hoe je css‑prefix kunt behandelen** bij het werken met stylesheets binnen een document met GroupDocs.Editor voor .NET. Of je nu een URL moet voorvoegen aan afbeeldingen, lettertypen of een externe bron, de onderstaande stappen laten je precies zien hoe je **css‑prefix kunt behandelen** en ook hoe je **css‑inhoud kunt extraheren** voor verdere verwerking.

## Quick Answers
- **Wat betekent “handle css prefix”?** Het toevoegen van een aangepaste URL‑prefix aan externe bronnen die in CSS worden gerefereerd.  
- **Welke API‑methode retourneert CSS‑stijlen?** `EditableDocument.GetCssContent(...)`.  
- **Heb ik een licentie nodig?** Een proeflicentie is beschikbaar; een commerciële licentie is vereist voor productie.  
- **Welke .NET‑versies worden ondersteund?** .NET Framework 4.5+ en .NET Core/5/6.  
- **Kan ik de prefix tijdens runtime wijzigen?** Ja – geef simpelweg een andere string door aan `GetCssContent`.

## Wat is **handle css prefix**?
Het toepassen van een prefix op CSS‑bronnen herschrijft de paden van afbeeldingen, lettertypen of andere assets zodat ze wijzen naar een locatie die jij beheert (bijv. een CDN of een beveiligde server). Dit is vooral handig wanneer je een document exporteert en alle externe verwijzingen bereikbaar moeten zijn vanuit een webapplicatie.

## Waarom GroupDocs.Editor gebruiken om **css‑inhoud te extraheren**?
GroupDocs.Editor kan de originele CSS die in Word‑verwerkingsdocumenten is ingebed lezen, je de ruwe stylesheet‑strings geven, en je in staat stellen deze te manipuleren vóór weergave of opslaan. Dit elimineert de noodzaak voor handmatige parsing en garandeert dat de geëxtraheerde CSS overeenkomt met de interne representatie van het document.

## Prerequisites
Voordat we beginnen, zorg dat je de volgende zaken klaar hebt staan:
- Visual Studio: Je hebt een werkende installatie van Visual Studio nodig.  
- .NET Framework: Zorg dat je het .NET Framework geïnstalleerd hebt.  
- GroupDocs.Editor for .NET: Je kunt het downloaden [hier](https://releases.groupdocs.com/editor/net/).  
- Sample Document: Zorg voor een voorbeelddocument klaar voor bewerking.

## Import Namespaces
Laten we eerst de benodigde namespaces importeren zodat onze code soepel draait. Deze stap geeft ons toegang tot de kernklassen van GroupDocs.Editor.

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Editor.Options;
```

## Step 1: Initialize the Editor
De eerste stap omvat het aanmaken van een `Editor`‑instance met je voorbeelddocument. Dit zet de bewerkingsomgeving op.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```

## Step 2: Edit the Document
Vervolgens verkrijgen we een `EditableDocument`‑object. Dit object vertegenwoordigt de bewerkbare versie van het bestand en stelt ons in staat om met de interne onderdelen te werken.

```csharp
    using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
    {
```

## Step 3: Set External Prefixes
Definieer de URL‑prefixes voor afbeeldingen en lettertypen. Deze prefixes worden voor elke afbeelding‑ en lettertype‑referentie in de CSS geplaatst.

```csharp
        string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
        string externalFontsPrefix = "http://www.mywebsite.com/fonts/id=";
```

## Step 4: **Extract CSS content** with the Prefixes
Roep `GetCssContent` aan en geef de zojuist gedefinieerde prefixes door. De methode retourneert een lijst met CSS‑stylesheet‑strings die al de geprefixt URLs bevatten.

```csharp
        List<string> stylesheets = document.GetCssContent(externalImagesPrefix, externalFontsPrefix);
```

## Step 5: Output the Results
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

## Common Issues and Solutions
- **No stylesheets returned** – Zorg ervoor dat het bron‑document daadwerkelijk CSS bevat (bijv. een Word‑document met gestylede tabellen of ingebedde HTML).  
- **Incorrect URLs** – Controleer dubbel dat de prefix‑strings eindigen met het juiste scheidingsteken (`/` of `=`) voor jouw server‑routing.  
- **Performance concerns** – Voor zeer grote documenten kun je overwegen om stylesheets in batches te verwerken om hoog geheugenverbruik te vermijden.

## Conclusion
CSS‑inhoud behandelen met een prefix via GroupDocs.Editor voor .NET is eenvoudig en krachtig. Door deze stappen te volgen kun je **css‑prefix** toepassen, de ruwe CSS ophalen via **extract css content**, en externe bronnen naadloos integreren in je web‑workflow. Ontdek andere GroupDocs.Editor‑functies zoals HTML‑conversie, afbeeldingsextractie en document‑samenvoeging om nog meer waarde uit de API te halen.

## FAQ's
### Kan ik GroupDocs.Editor voor .NET gebruiken met andere documentformaten?
Ja, GroupDocs.Editor voor .NET ondersteunt verschillende documentformaten, waaronder PDF, Word, Excel en meer.

### Is er een gratis proefversie beschikbaar voor GroupDocs.Editor voor .NET?
Absoluut! Je kunt je gratis proefversie starten [hier](https://releases.groupdocs.com/).

### Hoe krijg ik een tijdelijke licentie voor GroupDocs.Editor voor .NET?
Je kunt een tijdelijke licentie verkrijgen [hier](https://purchase.groupdocs.com/temporary-license/).

### Waar vind ik gedetailleerde documentatie voor GroupDocs.Editor voor .NET?
Gedetailleerde documentatie is beschikbaar [hier](https://tutorials.groupdocs.com/editor/net/).

### Welke ondersteuningsopties zijn er beschikbaar voor GroupDocs.Editor voor .NET?
Je kunt ondersteuning krijgen [hier](https://forum.groupdocs.com/c/editor/20).

## Additional Frequently Asked Questions

**Q: Kan ik de prefix wijzigen nadat ik de CSS heb geëxtraheerd?**  
A: Ja. Roep `GetCssContent` opnieuw aan met een andere prefix‑string; de methode gebruikt altijd de waarden die je op runtime doorgeeft.

**Q: Werkt dit met met wachtwoord beveiligde documenten?**  
A: Ja. Geef het wachtwoord door in `WordProcessingLoadOptions` bij het aanmaken van de `Editor`‑instance.

**Q: Is het mogelijk om de aangepaste CSS terug op te slaan in het document?**  
A: GroupDocs.Editor biedt momenteel alleen read‑only toegang tot CSS. Om wijzigingen te behouden moet je de originele stylesheet vervangen via de onderliggende XML‑API’s van het document.

---

**Last Updated:** 2026-03-06  
**Tested With:** GroupDocs.Editor 23.12 for .NET  
**Author:** GroupDocs