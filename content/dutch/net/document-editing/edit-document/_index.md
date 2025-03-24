---
title: Document bewerken
linktitle: Document bewerken
second_title: GroupDocs.Editor .NET API
description: Leer moeiteloos documenten bewerken met GroupDocs.Editor voor .NET. Stapsgewijze handleiding voor tekstverwerkings- en spreadsheetbestanden.
weight: 11
url: /nl/net/document-editing/edit-document/
---

# Document bewerken

## Invoering
Bent u ooit verstrikt geraakt in de complexiteit van het bewerken van documenten binnen uw .NET-applicaties? Wees niet bang! Met GroupDocs.Editor voor .NET heeft u een krachtige bondgenoot om deze taak te vereenvoudigen. Deze uitgebreide handleiding laat u zien hoe u deze robuuste tool kunt gebruiken om documenten gemakkelijk te bewerken. Of u nu te maken heeft met tekstverwerkingsdocumenten of spreadsheets, aan het einde van deze tutorial navigeert u als een professional door GroupDocs.Editor.
## Vereisten
Voordat u in de zelfstudie duikt, moet u ervoor zorgen dat u over het volgende beschikt:
- Visual Studio: geïnstalleerd en klaar voor gebruik.
- .NET Framework: een compatibele versie die op uw systeem is geïnstalleerd.
-  GroupDocs.Editor voor .NET: dat kan[download de nieuwste versie](https://releases.groupdocs.com/editor/net/) en verkrijgen van een[tijdelijke licentie](https://purchase.groupdocs.com/temporary-license/) indien nodig.
- Basiskennis van C#: In deze handleiding wordt ervan uitgegaan dat u een basiskennis hebt van de ontwikkeling van C# en .NET.
## Naamruimten importeren
Om aan de slag te gaan, moet u de benodigde naamruimten in uw project importeren. Voeg de volgende regels toe bovenaan uw C#-bestand:
```csharp
using System.Collections.Generic;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.Options;
```
Nu u helemaal klaar bent, gaan we het documentbewerkingsproces opsplitsen in beheersbare stappen.
## Stap 1: Laad een tekstverwerkingsdocument
Laten we eerst een tekstverwerkingsdocument laden. Hier wijst u de Editor-instantie naar de locatie van uw document en geeft u indien nodig eventuele laadopties op.
### 1.1 Initialiseer de Editor met standaardopties
```csharp
string inputFilePath = "Your Sample Document"; // Pad naar uw document
Editor editor1 = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
```
Dit codefragment initialiseert de Editor-instantie met behulp van standaardlaadopties voor een tekstverwerkingsdocument.
## Stap 2: bewerk het document
Nu kunnen we doorgaan met het bewerken van het geladen document. Met GroupDocs.Editor kunt u de bewerkingsopties aanpassen aan uw behoeften.
### 2.1 Bewerken met standaardopties
```csharp
EditableDocument defaultWordProcessingDoc = editor1.Edit();
```
Het bewerken van het document met standaardopties is eenvoudig en vereist minimale configuratie.
### 2.2 Bewerken met aangepaste opties
Laten we eens kijken naar meer geavanceerde configuraties door aangepaste bewerkingsopties op te geven.
```csharp
WordProcessingEditOptions wordProcessingEditOptions1 = new WordProcessingEditOptions();
wordProcessingEditOptions1.EnablePagination = false;
wordProcessingEditOptions1.EnableLanguageInformation = true;
wordProcessingEditOptions1.FontExtraction = FontExtractionOptions.ExtractAllEmbedded;
EditableDocument version1WordProcessingDoc = editor1.Edit(wordProcessingEditOptions1);
```
In dit fragment hebben we paginering uitgeschakeld, taalinformatie ingeschakeld en lettertype-extractie ingesteld om alle ingesloten lettertypen te extraheren.
### 2.3 Nog een configuratievoorbeeld
U kunt het document ook bewerken met een andere reeks opties:
```csharp
WordProcessingEditOptions wordProcessingEditOptions2 = new WordProcessingEditOptions(true);
wordProcessingEditOptions2.FontExtraction = FontExtractionOptions.ExtractAll;
EditableDocument version2WordProcessingDoc = editor1.Edit(wordProcessingEditOptions2);
```
Hier hebben we paginering ingeschakeld en lettertype-extractie ingesteld om alle lettertypen te extraheren.
## Stap 3: Een spreadsheet laden en bewerken
Het bewerken van spreadsheets is net zo eenvoudig met GroupDocs.Editor.
### 3.1 Laad het spreadsheet
```csharp
Editor editor2 = new Editor("Your Sample Document", delegate { return new SpreadsheetLoadOptions(); });
```
Hiermee wordt een Editor-instantie voor een spreadsheetdocument geïnitialiseerd.
### 3.2 Bewerk het eerste tabblad
```csharp
SpreadsheetEditOptions sheetTab1EditOptions = new SpreadsheetEditOptions();
sheetTab1EditOptions.WorksheetIndex = 0; // De index is gebaseerd op 0, dus dit is het eerste tabblad
EditableDocument firstTab = editor2.Edit(sheetTab1EditOptions);
```
U kunt het eerste tabblad van het spreadsheet bewerken met de opgegeven opties.
### 3.3 Bewerk het tweede tabblad
```csharp
SpreadsheetEditOptions sheetTab2EditOptions = new SpreadsheetEditOptions();
sheetTab2EditOptions.WorksheetIndex = 1; // De index is gebaseerd op 0, dus dit is het tweede tabblad
EditableDocument secondTab = editor2.Edit(sheetTab2EditOptions);
```
Op dezelfde manier bewerkt dit codefragment het tweede tabblad van de spreadsheet.
## Stap 4: Inhoud extraheren
Nadat u uw document heeft bewerkt, moet u mogelijk de inhoud ervan extraheren. GroupDocs.Editor biedt hiervoor verschillende methoden.
### 4.1 HTML-inhoud ophalen
```csharp
string bodyContent = firstTab.GetBodyContent(); // HTML-opmaak vanuit het HTML->BODY-element
string allContent = firstTab.GetContent(); // Volledige HTML-opmaak van het hele document, inclusief HTML->HEAD-header en de inhoud ervan
```
Deze code extraheert de HTML-inhoud van het bewerkte document.
### 4.2 Bronnen extraheren
```csharp
List<IImageResource> onlyImages = firstTab.Images;
List<IHtmlResource> allResourcesTogether = firstTab.AllResources;
```
Hier kunt u afbeeldingen en alle andere HTML-bronnen uit het document extraheren.
## Stap 5: Opruimen
Vergeet niet alle exemplaren te verwijderen om bronnen vrij te maken.
```csharp
defaultWordProcessingDoc.Dispose();
version1WordProcessingDoc.Dispose();
version2WordProcessingDoc.Dispose();
firstTab.Dispose();
secondTab.Dispose();
editor1.Dispose();
editor2.Dispose();
```
Een juiste verwijdering zorgt ervoor dat er geen geheugenlekken of prestatieproblemen in uw toepassing optreden.
## Conclusie
 Gefeliciteerd! U heeft nu een goed begrip van hoe u GroupDocs.Editor voor .NET kunt gebruiken om inhoud uit tekstverwerkingsdocumenten en spreadsheets te laden, bewerken en extraheren. Deze krachtige tool vereenvoudigt documentbewerkingstaken en kan naadloos worden geïntegreerd met uw .NET-applicaties. Voor meer details kunt u de[documentatie](https://tutorials.groupdocs.com/editor/net/), [download de nieuwste versie](https://releases.groupdocs.com/editor/net/) , of verkrijg een[tijdelijke licentie](https://purchase.groupdocs.com/temporary-license/).
## Veelgestelde vragen
### Kan ik PDF-documenten bewerken met GroupDocs.Editor voor .NET?
Momenteel ondersteunt GroupDocs.Editor voor .NET voornamelijk de indelingen Tekstverwerking, Spreadsheet en Presentatie.
### Hoe ga ik efficiënt om met grote documenten?
Gebruik de bewerkingsopties om alleen noodzakelijke delen van het document te laden en te verwerken, en zorg ervoor dat u exemplaren op de juiste manier weggooit om het geheugen te beheren.
### Is er een limiet aan de documentgrootte die ik kan bewerken?
Er zijn geen strikte groottelimieten, maar de prestaties zijn afhankelijk van de mogelijkheden van uw systeem.
### Kan ik de HTML-uitvoer verder aanpassen?
Ja, GroupDocs.Editor maakt uitgebreide aanpassing van HTML-uitvoer mogelijk via verschillende opties en instellingen.
### Waar kan ik ondersteuning krijgen als ik problemen tegenkom?
 U kunt een bezoek brengen aan de[GroupDocs.Editor-ondersteuningsforum](https://forum.groupdocs.com/c/editor/20) voor hulp en bijstand.