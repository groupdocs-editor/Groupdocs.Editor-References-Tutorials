---
title: Haal HTML-inhoud met voorvoegsel op
linktitle: Haal HTML-inhoud met voorvoegsel op
second_title: GroupDocs.Editor .NET API
description: Leer hoe u HTML-inhoud uit documenten kunt ophalen met GroupDocs.Editor voor .NET met aangepaste voorvoegsels voor afbeeldingen en stylesheets. Stap-voor-stap handleiding inbegrepen.
weight: 11
url: /nl/net/html-content-retrieval/retrieve-html-content-with-prefix/
---

# Haal HTML-inhoud met voorvoegsel op

## Invoering
Welkom bij onze stapsgewijze zelfstudie over hoe u HTML-inhoud uit een document kunt ophalen met GroupDocs.Editor voor .NET. Of u nu een doorgewinterde ontwikkelaar bent of net begint, deze gids leidt u op een eenvoudig te volgen manier door het proces. We behandelen alles wat u moet weten, van het opzetten van uw omgeving tot het succesvol uitvoeren van de code. Laten we erin duiken!
## Vereisten
Voordat we beginnen, zorg ervoor dat u aan de volgende vereisten voldoet:
1.  GroupDocs.Editor voor .NET: Download de nieuwste versie van de[downloadpagina](https://releases.groupdocs.com/editor/net/).
2. Ontwikkelomgeving: Visual Studio of een andere .NET-ontwikkelomgeving van uw voorkeur.
3. Basiskennis van C#: Bekendheid met programmeren in C# zal u helpen de voorbeelden te volgen.
4. Document om te bewerken: Zorg ervoor dat u een voorbeelddocument gereed heeft om te testen, zoals een Word-document.
5. .NET Framework: Zorg ervoor dat .NET Framework op uw computer is geïnstalleerd.
Nu je alles klaar hebt, gaan we aan de slag!
## Naamruimten importeren
Eerst moet u de benodigde naamruimten in uw C#-project importeren. Deze naamruimten bieden de klassen en methoden die nodig zijn om met GroupDocs.Editor voor .NET te werken.
```csharp
using System;
using GroupDocs.Editor.Options;
```
Nu de naamruimten zijn geïmporteerd, kunnen we doorgaan met het instellen van de editor.
## Stap 1: Initialiseer de editor
 Om te beginnen moet u het`Editor`klasse met uw document. Deze stap omvat het specificeren van het document dat u wilt bewerken en het opgeven van de benodigde laadopties.
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
    // Hier zullen verdere stappen worden toegevoegd
}
```
 In dit voorbeeld laden we een Word-document. Je kunt vervangen`"Your Sample Document"` met het pad naar uw document.
## Stap 2: bewerk het document
 Vervolgens moeten we het document openen om te bewerken. Dit gebeurt met behulp van de`Edit` werkwijze van de`Editor` klasse, wat vereist`WordProcessingEditOptions` als argument.
```csharp
using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
{
    // Hier zullen verdere stappen worden toegevoegd
}
```
 De`EditableDocument` instance vertegenwoordigt het document in een bewerkbaar formaat. Nu zijn we klaar om de HTML-inhoud op te halen.
## Stap 3: Definieer aangepaste voorvoegsels
Om aangepaste voorvoegsels voor afbeeldingen en CSS toe te voegen, moeten we de voorvoegsels als tekenreeksen definiëren. Deze stap zorgt ervoor dat de HTML-inhoud de opgegeven voorvoegsels voor externe bronnen heeft.
```csharp
string externalImagesPrefix = "http://www.mijnwebsite.com/images/id=”;
string externalCssPrefix = "http://www.mijnwebsite.com/css/id=”;
```
U kunt de URL's vervangen door de gewenste voorvoegsels. Deze voorvoegsels zullen in de volgende stap worden gebruikt om de HTML-uitvoer aan te passen.
## Stap 4: HTML-inhoud ophalen
Nu we onze voorvoegsels hebben ingesteld, kunnen we de HTML-inhoud uit het document ophalen. De`GetContent` werkwijze van de`EditableDocument` class stelt ons in staat om de afbeelding en CSS-voorvoegsels te specificeren.
```csharp
string prefixedHtmlContent = document.GetContent(externalImagesPrefix, externalCssPrefix);
Console.WriteLine("HTML content of the input document with custom image and stylesheet prefixes: {0}", prefixedHtmlContent);
```
Met dit codefragment wordt de HTML-inhoud met de aangepaste voorvoegsels opgehaald en naar de console afgedrukt. U kunt deze HTML-inhoud indien nodig verder verwerken of opslaan.
## Conclusie
En daar heb je het! Door deze stappen te volgen, kunt u eenvoudig HTML-inhoud uit een document ophalen met GroupDocs.Editor voor .NET, compleet met aangepaste voorvoegsels voor afbeeldingen en stylesheets. Deze krachtige tool vereenvoudigt documentmanipulatie, zodat u zich kunt concentreren op het naadloos integreren van documentbewerking in uw .NET-applicaties.
 Voor meer gedetailleerde informatie, bekijk de[GroupDocs.Editor voor .NET-documentatie](https://tutorials.groupdocs.com/editor/net/) . Als u vragen heeft of meer hulp nodig heeft, kunt u contact opnemen met de[Helpforum](https://forum.groupdocs.com/c/editor/20).
## Veelgestelde vragen
### Welke soorten documenten kan ik bewerken met GroupDocs.Editor voor .NET?
GroupDocs.Editor ondersteunt verschillende documentformaten, waaronder Word, Excel, PowerPoint, PDF en meer.
### Hoe krijg ik een gratis proefversie van GroupDocs.Editor voor .NET?
 U kunt een gratis proefversie krijgen van de[GroupDocs-website](https://releases.groupdocs.com/).
### Kan ik de HTML-inhoud verder aanpassen?
Ja, u kunt de opgehaalde HTML-inhoud indien nodig wijzigen voordat u deze weergeeft of opslaat.
### Is het mogelijk om GroupDocs.Editor voor .NET te gebruiken met andere .NET-talen?
Ja, je kunt het gebruiken met elke .NET-compatibele taal, zoals VB.NET of F#.
### Hoe verkrijg ik een tijdelijke licentie voor GroupDocs.Editor voor .NET?
 U kunt een tijdelijke licentie verkrijgen bij de[aankooppagina](https://purchase.groupdocs.com/temporary-license/).