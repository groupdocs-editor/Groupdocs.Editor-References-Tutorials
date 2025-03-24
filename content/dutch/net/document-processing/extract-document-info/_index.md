---
title: Documentinformatie extraheren
linktitle: Documentinformatie extraheren
second_title: GroupDocs.Editor .NET API
description: Leer hoe u documentinformatie kunt extraheren met GroupDocs.Editor voor .NET met onze gedetailleerde, stapsgewijze zelfstudie. Perfect voor het beheren van verschillende documenttypen.
weight: 10
url: /nl/net/document-processing/extract-document-info/
---
## Invoering
Welkom bij deze uitgebreide tutorial over het extraheren van documentinformatie met GroupDocs.Editor voor .NET. In deze handleiding leiden we u stap voor stap door het proces, zodat u elk onderdeel duidelijk en beknopt begrijpt. Of u nu een doorgewinterde ontwikkelaar bent of net begint, deze tutorial helpt u GroupDocs.Editor naadloos te integreren in uw .NET-projecten om documenten efficiënt te beheren en te manipuleren.
## Vereisten
Voordat we in de code duiken, zorgen we ervoor dat je alles hebt wat je nodig hebt:
- Basiskennis van C#: Het begrijpen van de basisprincipes van C#-programmeren is essentieel.
- Visual Studio: Zorg ervoor dat Visual Studio is geïnstalleerd.
-  GroupDocs.Editor voor .NET: u hebt de GroupDocs.Editor voor .NET-bibliotheek nodig. Je kunt het downloaden van de[downloadpagina](https://releases.groupdocs.com/editor/net/).
## Naamruimten importeren
Om te beginnen moet u de benodigde naamruimten importeren. Hierdoor hebt u toegang tot de klassen en methoden die nodig zijn om documenten te manipuleren.
```csharp
using System;
using GroupDocs.Editor.Metadata;
```
## Stap 1: Laad uw document
Eerst moet u het document laden waaruit u informatie wilt extraheren. Dit kunt u doen door het bestandspad naar het document op te geven.
```csharp
string docxInputFilePath = "YourSampleDocument.docx";
Editor editorDocx = new Editor(docxInputFilePath);
```
## Stap 2: Documentinformatie ophalen
 Vervolgens haalt u de documentinformatie op met behulp van de`GetDocumentInfo` methode. Deze methode vereist geen specifieke laadopties als u niet zeker bent over het documentformaat.
```csharp
IDocumentInfo infoDocx = editorDocx.GetDocumentInfo(null);
```
## Stap 3: Bepaal het documenttype
Nu moet u controleren met welk type document u te maken heeft. Dit is van cruciaal belang omdat het bepaalt hoe u met het document omgaat.
```csharp
bool isSpreadsheet = infoDocx is SpreadsheetDocumentInfo;
bool isText = infoDocx is TextualDocumentInfo;
bool isWordProcessing = infoDocx is WordProcessingDocumentInfo;
Console.WriteLine($"Is '{docxInputFilePath}' a Spreadsheet: {isSpreadsheet}");
Console.WriteLine($"Is '{docxInputFilePath}' a Textual document: {isText}");
Console.WriteLine($"Is '{docxInputFilePath}' a WordProcessing document: {isWordProcessing}");
```
## Stap 4: Extraheer gedetailleerde informatie
Als het document een tekstverwerkingsdocument is, kunt u gedetailleerde informatie extraheren, zoals formaat, extensie, aantal pagina's, grootte en of het gecodeerd is.
```csharp
if (isWordProcessing)
{
    WordProcessingDocumentInfo casted = (WordProcessingDocumentInfo)infoDocx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Page count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```
## Stap 5: Herhaal dit voor verschillende documenttypen
Herhaal dezelfde stappen voor andere documenttypen, zoals spreadsheets en tekstdocumenten.
```csharp
string xlsxInputFilePath = "YourSampleDocument.xlsx";
Editor editorXlsx = new Editor(xlsxInputFilePath);
IDocumentInfo infoXlsx = editorXlsx.GetDocumentInfo(null);
bool isXlsxSpreadsheet = infoXlsx is SpreadsheetDocumentInfo;
Console.WriteLine($"Is '{xlsxInputFilePath}' a Spreadsheet: {isXlsxSpreadsheet}");
if (isXlsxSpreadsheet)
{
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo)infoXlsx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Tabs count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```
## Stap 6: Behandel met wachtwoord beveiligde documenten
Wanneer u te maken heeft met met een wachtwoord beveiligde documenten, moet u eerst proberen deze te openen zonder wachtwoord, vervolgens met een onjuist wachtwoord en ten slotte met het juiste wachtwoord.
```csharp
string xlsInputFilePath = "YourSampleDocument.xls";
Editor editorXls = new Editor(xlsInputFilePath);
try
{
    IDocumentInfo infoXls = editorXls.GetDocumentInfo(null);
}
catch (PasswordRequiredException)
{
    Console.WriteLine("This document is password-protected.");
}
try
{
    IDocumentInfo infoXls = editorXls.GetDocumentInfo("incorrect_password");
}
catch (IncorrectPasswordException)
{
    Console.WriteLine("The provided password is incorrect.");
}
IDocumentInfo infoXlsValid = editorXls.GetDocumentInfo("correct_password");
bool isXlsSpreadsheet = infoXlsValid is SpreadsheetDocumentInfo;
Console.WriteLine($"Password-protected document is a Spreadsheet: {isXlsSpreadsheet}");
if (isXlsSpreadsheet)
{
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo)infoXlsValid;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Tabs count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```
## Stap 7: Behandel op tekst gebaseerde documenten
```csharp
string xmlInputFilePath = "YourSampleDocument.xml";
Editor editorXml = new Editor(xmlInputFilePath);
IDocumentInfo infoXml = editorXml.GetDocumentInfo(null);
bool isXmlText = infoXml is TextualDocumentInfo;
Console.WriteLine($"Is '{xmlInputFilePath}' a Textual document: {isXmlText}");
if (isXmlText)
{
    TextualDocumentInfo casted = (TextualDocumentInfo)infoXml;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Encoding: {casted.Encoding}; Size: {casted.Size} bytes");
}
```
## Stap 8: Gooi hulpbronnen weg
Zorg er ten slotte voor dat u over alle bronnen beschikt om geheugenlekken te voorkomen.
```csharp
editorDocx.Dispose();
editorXlsx.Dispose();
editorXls.Dispose();
editorXml.Dispose();
Console.WriteLine("ExtractingDocumentInfo routine has successfully finished");
```
## Conclusie
Gefeliciteerd! U hebt nu geleerd hoe u documentinformatie kunt extraheren met GroupDocs.Editor voor .NET. Deze krachtige bibliotheek vereenvoudigt documentbeheer en -manipulatie, waardoor u naadloos met verschillende documenttypen kunt omgaan. Of u nu te maken heeft met tekstverwerking, spreadsheets of op tekst gebaseerde documenten, GroupDocs.Editor biedt een robuuste oplossing.
## Veelgestelde vragen
### Welke soorten documenten kan GroupDocs.Editor verwerken?
GroupDocs.Editor kan verschillende documenttypen verwerken, waaronder tekstverwerking, spreadsheets en op tekst gebaseerde documenten.
### Kan GroupDocs.Editor met een wachtwoord beveiligde documenten beheren?
Ja, GroupDocs.Editor kan met een wachtwoord beveiligde documenten beheren. Het kan deze documenten identificeren en openen met het juiste wachtwoord.
### Is het nodig om de Editor-objecten te verwijderen?
Ja, het is van cruciaal belang om Editor-objecten te verwijderen om bronnen vrij te maken en geheugenlekken te voorkomen.
### Kan ik gedetailleerde informatie over het documentformaat en de documentgrootte opvragen?
Absoluut! Met GroupDocs.Editor kunt u gedetailleerde informatie extraheren, waaronder formaat, extensie, grootte, aantal pagina's en coderingsstatus.
### Waar kan ik ondersteuning krijgen als ik problemen tegenkom?
 U kunt ondersteuning krijgen van de[GroupDocs.Editor-ondersteuningsforum](https://forum.groupdocs.com/c/editor/20).