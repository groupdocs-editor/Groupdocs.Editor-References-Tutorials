---
title: Document maken
linktitle: Document maken
second_title: GroupDocs.Editor .NET API
description: Leer hoe u Word-, Excel-, PowerPoint-, Ebook- en e-maildocumenten kunt bewerken met GroupDocs.Editor voor .NET met deze uitgebreide stapsgewijze zelfstudie.
weight: 10
url: /nl/net/document-editing/create-document/
---
## Invoering
Bent u het gedoe beu dat gepaard gaat met het programmatisch bewerken van verschillende documenttypen? GroupDocs.Editor voor .NET is er om het proces te vereenvoudigen. Met deze krachtige tool kunnen ontwikkelaars gemakkelijk verschillende documentformaten bewerken, zoals Word, Excel, PowerPoint, e-boeken en e-mails. In deze zelfstudie gaan we dieper in op het gebruik van GroupDocs.Editor voor .NET om documenten te maken en te bewerken. We zullen het proces opsplitsen in eenvoudig te volgen stappen, waardoor het toegankelijk wordt, zelfs als u nieuw bent.
## Vereisten
Voordat we beginnen, zorg ervoor dat u over het volgende beschikt:
- Visual Studio is op uw computer geïnstalleerd.
- .NET Framework (4.0 of hoger).
-  GroupDocs.Editor voor .NET-bibliotheek. Je kunt het downloaden van[hier](https://releases.groupdocs.com/editor/net/).
- Basiskennis van programmeren in C#.
## Naamruimten importeren
Laten we eerst de benodigde naamruimten importeren. Hierdoor worden de vereiste klassen en methoden toegankelijk in onze applicatie.
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using System.IO;
```
## Stap 1: De stream instellen
Om te beginnen moeten we een geheugenstroom opzetten die zal fungeren als tijdelijke aanduiding voor de documentinhoud.
```csharp
Stream memoryStream = Stream.Null;
```
## Stap 2: Terugbelfunctie om het document op te slaan
Definieer vervolgens een callback-functie waarmee de nieuwe documentstroom wordt opgeslagen. Deze functie is essentieel voor het afhandelen van de uitvoer van het documentbewerkingsproces.
```csharp
void SaveNewDocument(Stream resultStream)
{
    memoryStream = resultStream;
}
```
## Stap 3: Een tekstverwerkingsdocument maken en bewerken
 Laten we nu een Word-document maken en bewerken. We beginnen met het maken van een nieuwe`Editor` instance voor WordProcessing-documenten en bewerk deze met standaardopties.
### Maken en bewerken met standaardopties
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    EditableDocument defaultWordProcessingDoc = editor.Edit();
}
```
### Maken en bewerken met aangepaste opties
Voor meer controle kunnen we opties opgeven zoals het uitschakelen van paginering en het extraheren van ingesloten lettertypen.
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    WordProcessingEditOptions wordProcessingEditOptions = new WordProcessingEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true,
        FontExtraction = FontExtractionOptions.ExtractAllEmbedded
    };
    EditableDocument editableWordProcessingDocument = editor.Edit(wordProcessingEditOptions);
}
```
## Stap 4: Een spreadsheetdocument maken en bewerken
Op dezelfde manier kunnen we een Excel-document maken en bewerken. Hier is hoe je het doet.
### Maken en bewerken met standaardopties
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    EditableDocument defaultEditableSpreadsheetDocument = editor.Edit();
}
```
### Maken en bewerken met aangepaste opties
 Om specifieke werkbladen te targeten of verborgen werkbladen uit te sluiten, gebruiken we`SpreadsheetEditOptions`.
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    SpreadsheetEditOptions spreadsheetEditOptions = new SpreadsheetEditOptions
    {
        WorksheetIndex = 0,
        ExcludeHiddenWorksheets = true
    };
    EditableDocument editableSpreadsheetDocument = editor.Edit(spreadsheetEditOptions);
}
```
## Stap 5: Een presentatiedocument maken en bewerken
PowerPoint-presentaties worden ook ondersteund. Laten we eens kijken hoe we ermee om moeten gaan.
### Maken en bewerken met standaardopties
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    EditableDocument defaultEditablePresentationDocument = editor.Edit();
}
```
### Maken en bewerken met aangepaste opties
U kunt uw bewerkingen aanpassen door opties op te geven, zoals welke dia u wilt weergeven en of u verborgen dia's wilt opnemen.
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    PresentationEditOptions presentationEditOptions = new PresentationEditOptions
    {
        ShowHiddenSlides = false,
        SlideNumber = 0
    };
    EditableDocument editablePresentationDocument = editor.Edit(presentationEditOptions);
}
```
## Stap 6: Een e-boekdocument maken en bewerken
GroupDocs.Editor maakt het ook mogelijk om e-boekformaten zoals EPUB te bewerken. Hier leest u hoe u het kunt aanpakken.
### Maken en bewerken met standaardopties
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EditableDocument defaultEditableEbookDocument = editor.Edit();
}
```
### Maken en bewerken met aangepaste opties
Pas uw e-boekbewerking aan door paginering en taalinformatie in of uit te schakelen.
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EbookEditOptions ebookEditOptions = new EbookEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true
    };
    EditableDocument editableEbookDocument = editor.Edit(ebookEditOptions);
}
```
## Stap 7: Een e-maildocument maken en bewerken
Ten slotte bekijken we hoe u e-maildocumenten kunt bewerken. Dit omvat formaten zoals EML.
### Maken en bewerken met standaardopties
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EditableDocument defaultEditableEmailDocument = editor.Edit();
}
```
### Maken en bewerken met aangepaste opties
Geef uitvoeropties voor e-mailberichten op om het bewerkingsproces te beheren.
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EmailEditOptions emailEditOptions = new EmailEditOptions
    {
        MailMessageOutput = MailMessageOutput.All
    };
    EditableDocument editableEmailDocument = editor.Edit(emailEditOptions);
}
```
## Stap 8: Het proces voltooien
Na het bewerken van de documenten is het van cruciaal belang om de geheugenstroom op de juiste manier te verwijderen om bronnen vrij te maken.
```csharp
memoryStream.Dispose();
System.Console.WriteLine("CreateDocument routine has successfully finished");
```
## Conclusie
GroupDocs.Editor voor .NET is een veelzijdige en krachtige tool die de taak van het programmatisch bewerken van verschillende documenttypen kan vereenvoudigen. Door deze stapsgewijze handleiding te volgen, kunt u eenvoudig documenten maken en bewerken, of het nu WordProcess-bestanden, spreadsheets, presentaties, e-boeken of e-mails zijn. Duik in de GroupDocs.Editor-documentatie voor meer geavanceerde functies en aanpassingsopties.
## Veelgestelde vragen
### Welke soorten documenten kan ik bewerken met GroupDocs.Editor voor .NET?
U kunt een breed scala aan documenten bewerken, waaronder WordProcessing, spreadsheets, presentaties, e-boeken en e-mails.
### Is het mogelijk om de bewerkingsopties aan te passen?
Ja, GroupDocs.Editor voor .NET maakt uitgebreide aanpassingen mogelijk via verschillende bewerkingsopties die specifiek zijn voor elk documenttype.
### Hoe ga ik om met de uitvoer van de bewerkte documenten?
kunt een callback-functie gebruiken om de bewerkte documentstroom op de gewenste locatie op te slaan.
### Heb ik een licentie nodig om GroupDocs.Editor voor .NET te gebruiken?
 Ja, u kunt een licentie verkrijgen bij[hier](https://purchase.groupdocs.com/buy). Er is ook een optie voor een tijdelijke licentie.
### Waar kan ik meer gedetailleerde documentatie vinden?
 Gedetailleerde documentatie is beschikbaar op de[GroupDocs.Editor voor .NET-documentatiepagina](https://tutorials.groupdocs.com/editor/net/).