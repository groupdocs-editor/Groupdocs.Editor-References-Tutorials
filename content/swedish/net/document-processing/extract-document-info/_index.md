---
title: Extrahera dokumentinformation
linktitle: Extrahera dokumentinformation
second_title: GroupDocs.Editor .NET API
description: Lär dig hur du extraherar dokumentinformation med GroupDocs.Editor för .NET med vår detaljerade, steg-för-steg handledning. Perfekt för att hantera olika dokumenttyper.
weight: 10
url: /sv/net/document-processing/extract-document-info/
type: docs
---
# Extrahera dokumentinformation

## Introduktion
Välkommen till denna omfattande handledning om att extrahera dokumentinformation med GroupDocs.Editor för .NET. I den här guiden går vi igenom processen steg för steg, och ser till att du förstår varje del tydligt och koncist. Oavsett om du är en erfaren utvecklare eller precis har börjat, kommer den här handledningen att hjälpa dig att sömlöst integrera GroupDocs.Editor i dina .NET-projekt för att hantera och manipulera dokument effektivt.
## Förutsättningar
Innan vi dyker in i koden, låt oss se till att du har allt du behöver:
- Grundläggande kunskaper om C#: Att förstå grunderna i C#-programmering är viktigt.
- Visual Studio: Se till att du har Visual Studio installerat.
-  GroupDocs.Editor för .NET: Du behöver GroupDocs.Editor för .NET-biblioteket. Du kan ladda ner den från[nedladdningssida](https://releases.groupdocs.com/editor/net/).
## Importera namnområden
För att börja måste du importera de nödvändiga namnrymden. Detta låter dig komma åt de klasser och metoder som krävs för att manipulera dokument.
```csharp
using System;
using GroupDocs.Editor.Metadata;
```
## Steg 1: Ladda ditt dokument
Först måste du ladda dokumentet du vill extrahera information från. Detta kan göras genom att ange sökvägen till dokumentet.
```csharp
string docxInputFilePath = "YourSampleDocument.docx";
Editor editorDocx = new Editor(docxInputFilePath);
```
## Steg 2: Hämta dokumentinformation
 Därefter kommer du att hämta dokumentinformationen med hjälp av`GetDocumentInfo` metod. Den här metoden kräver inga specifika laddningsalternativ om du är osäker på dokumentformatet.
```csharp
IDocumentInfo infoDocx = editorDocx.GetDocumentInfo(null);
```
## Steg 3: Bestäm dokumenttyp
Nu måste du kontrollera vilken typ av dokument du har att göra med. Detta är avgörande eftersom det dikterar hur du ska hantera dokumentet.
```csharp
bool isSpreadsheet = infoDocx is SpreadsheetDocumentInfo;
bool isText = infoDocx is TextualDocumentInfo;
bool isWordProcessing = infoDocx is WordProcessingDocumentInfo;
Console.WriteLine($"Is '{docxInputFilePath}' a Spreadsheet: {isSpreadsheet}");
Console.WriteLine($"Is '{docxInputFilePath}' a Textual document: {isText}");
Console.WriteLine($"Is '{docxInputFilePath}' a WordProcessing document: {isWordProcessing}");
```
## Steg 4: Extrahera detaljerad information
Om dokumentet är ett ordbehandlingsdokument kan du extrahera detaljerad information som format, tillägg, sidantal, storlek och om det är krypterat.
```csharp
if (isWordProcessing)
{
    WordProcessingDocumentInfo casted = (WordProcessingDocumentInfo)infoDocx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Page count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```
## Steg 5: Upprepa för olika dokumenttyper
Upprepa samma steg för andra dokumenttyper som kalkylblad och textdokument.
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
## Steg 6: Hantera lösenordsskyddade dokument
När du hanterar lösenordsskyddade dokument bör du först försöka öppna dem utan lösenord, sedan med ett felaktigt lösenord och slutligen med rätt lösenord.
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
## Steg 7: Hantera textbaserade dokument
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
## Steg 8: Kasta resurser
Slutligen, se till att du gör dig av med alla resurser för att förhindra minnesläckor.
```csharp
editorDocx.Dispose();
editorXlsx.Dispose();
editorXls.Dispose();
editorXml.Dispose();
Console.WriteLine("ExtractingDocumentInfo routine has successfully finished");
```
## Slutsats
Grattis! Du har nu lärt dig hur du extraherar dokumentinformation med GroupDocs.Editor för .NET. Detta kraftfulla bibliotek förenklar dokumenthantering och manipulering, vilket gör att du kan hantera olika dokumenttyper sömlöst. Oavsett om du har att göra med ordbehandling, kalkylblad eller textbaserade dokument erbjuder GroupDocs.Editor en robust lösning.
## FAQ's
### Vilka typer av dokument kan GroupDocs.Editor hantera?
GroupDocs.Editor kan hantera olika dokumenttyper inklusive ordbehandling, kalkylblad och textbaserade dokument.
### Kan GroupDocs.Editor hantera lösenordsskyddade dokument?
Ja, GroupDocs.Editor kan hantera lösenordsskyddade dokument. Den kan identifiera och öppna dessa dokument med rätt lösenord.
### Är det nödvändigt att kassera Editor-objekten?
Ja, det är viktigt att kassera Editor-objekt för att frigöra resurser och förhindra minnesläckor.
### Kan jag extrahera detaljerad information om dokumentets format och storlek?
Absolut! GroupDocs.Editor låter dig extrahera detaljerad information inklusive format, tillägg, storlek, sidantal och krypteringsstatus.
### Var kan jag få support om jag stöter på problem?
 Du kan få stöd från[GroupDocs.Editor supportforum](https://forum.groupdocs.com/c/editor/20).