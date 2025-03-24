---
title: Skapa dokument
linktitle: Skapa dokument
second_title: GroupDocs.Editor .NET API
description: Lär dig hur du redigerar Word-, Excel-, PowerPoint-, Ebook- och e-postdokument med hjälp av GroupDocs.Editor för .NET med denna omfattande steg-för-steg-handledning.
weight: 10
url: /sv/net/document-editing/create-document/
---

# Skapa dokument

## Introduktion
Är du trött på krånglet som följer med att redigera olika dokumenttyper programmatiskt? GroupDocs.Editor för .NET är här för att förenkla processen. Detta kraftfulla verktyg låter utvecklare enkelt redigera olika dokumentformat som Word, Excel, PowerPoint, e-böcker och e-postmeddelanden. I den här handledningen kommer vi att fördjupa oss i hur man använder GroupDocs.Editor för .NET för att skapa och redigera dokument. Vi delar upp processen i steg som är lätta att följa, vilket gör den tillgänglig även om du är ny på detta.
## Förutsättningar
Innan vi börjar, se till att du har följande:
- Visual Studio installerat på din dator.
- .NET Framework (4.0 eller högre).
-  GroupDocs.Editor för .NET-bibliotek. Du kan ladda ner den från[här](https://releases.groupdocs.com/editor/net/).
- Grundläggande kunskaper i C#-programmering.
## Importera namnområden
Låt oss först importera de nödvändiga namnrymden. Detta kommer att göra de obligatoriska klasserna och metoderna tillgängliga i vår applikation.
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using System.IO;
```
## Steg 1: Konfigurera strömmen
Till att börja med måste vi sätta upp en minnesström som kommer att fungera som vår platshållare för dokumentinnehållet.
```csharp
Stream memoryStream = Stream.Null;
```
## Steg 2: Återuppringningsfunktion för att spara dokumentet
Därefter definierar du en återuppringningsfunktion som sparar den nya dokumentströmmen. Denna funktion är nödvändig för att hantera utdata från dokumentredigeringsprocessen.
```csharp
void SaveNewDocument(Stream resultStream)
{
    memoryStream = resultStream;
}
```
## Steg 3: Skapa och redigera ett ordbehandlingsdokument
 Låt oss nu skapa och redigera ett Word-dokument. Vi börjar med att skapa en ny`Editor` instans för WordProcessing-dokument och redigera den med standardalternativ.
### Skapa och redigera med standardalternativ
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    EditableDocument defaultWordProcessingDoc = editor.Edit();
}
```
### Skapa och redigera med anpassade alternativ
För mer kontroll kan vi ange alternativ som att inaktivera paginering och extrahera inbäddade teckensnitt.
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
## Steg 4: Skapa och redigera ett kalkylarksdokument
På samma sätt kan vi skapa och redigera ett Excel-dokument. Så här gör du.
### Skapa och redigera med standardalternativ
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    EditableDocument defaultEditableSpreadsheetDocument = editor.Edit();
}
```
### Skapa och redigera med anpassade alternativ
 För att rikta in sig på specifika kalkylblad eller utesluta dolda sådana använder vi`SpreadsheetEditOptions`.
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
## Steg 5: Skapa och redigera ett presentationsdokument
PowerPoint-presentationer stöds också. Låt oss se hur vi hanterar dem.
### Skapa och redigera med standardalternativ
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    EditableDocument defaultEditablePresentationDocument = editor.Edit();
}
```
### Skapa och redigera med anpassade alternativ
Du kan anpassa dina redigeringar genom att ange alternativ som vilken bild som ska visas och om dolda bilder ska inkluderas.
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
## Steg 6: Skapa och redigera ett e-boksdokument
GroupDocs.Editor tillåter också redigering av e-boksformat som EPUB. Så här kan du hantera det.
### Skapa och redigera med standardalternativ
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EditableDocument defaultEditableEbookDocument = editor.Edit();
}
```
### Skapa och redigera med anpassade alternativ
Anpassa din e-bokredigering genom att aktivera eller inaktivera sidnumrering och språkinformation.
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
## Steg 7: Skapa och redigera ett e-postdokument
Slutligen ska vi titta på hur man redigerar e-postdokument. Detta inkluderar format som EML.
### Skapa och redigera med standardalternativ
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EditableDocument defaultEditableEmailDocument = editor.Edit();
}
```
### Skapa och redigera med anpassade alternativ
Ange utmatningsalternativ för e-postmeddelanden för att styra redigeringsprocessen.
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
## Steg 8: Slutför processen
Efter att ha redigerat dokumenten är det viktigt att kassera minnesströmmen på rätt sätt för att frigöra resurser.
```csharp
memoryStream.Dispose();
System.Console.WriteLine("CreateDocument routine has successfully finished");
```
## Slutsats
GroupDocs.Editor för .NET är ett mångsidigt och kraftfullt verktyg som kan förenkla uppgiften att redigera olika dokumenttyper programmatiskt. Genom att följa den här steg-för-steg-guiden kan du enkelt skapa och redigera dokument, oavsett om det är WordProcessing-filer, kalkylblad, presentationer, e-böcker eller e-postmeddelanden. Dyk in i GroupDocs.Editor-dokumentationen för mer avancerade funktioner och anpassningsalternativ.
## FAQ's
### Vilka typer av dokument kan jag redigera med GroupDocs.Editor för .NET?
Du kan redigera ett brett utbud av dokument, inklusive ordbehandling, kalkylblad, presentationer, e-böcker och e-postmeddelanden.
### Är det möjligt att anpassa redigeringsalternativen?
Ja, GroupDocs.Editor för .NET möjliggör omfattande anpassning genom olika redigeringsalternativ som är specifika för varje dokumenttyp.
### Hur hanterar jag utmatningen av de redigerade dokumenten?
Du kan använda en återuppringningsfunktion för att spara den redigerade dokumentströmmen till önskad plats.
### Behöver jag en licens för att använda GroupDocs.Editor för .NET?
 Ja, du kan få en licens från[här](https://purchase.groupdocs.com/buy). Det finns även möjlighet till en tillfällig licens.
### Var kan jag hitta mer detaljerad dokumentation?
 Detaljerad dokumentation finns tillgänglig på[GroupDocs.Editor för .NET dokumentationssida](https://tutorials.groupdocs.com/editor/net/).