---
title: Spara dokument
linktitle: Spara dokument
second_title: GroupDocs.Editor .NET API
description: Redigera och spara dokument enkelt med GroupDocs.Editor för .NET. Denna steg-för-steg-guide förenklar processen för utvecklare.
type: docs
weight: 14
url: /sv/net/document-editing/save-document/
---
## Introduktion
Vill du enkelt redigera och spara dokument med GroupDocs.Editor för .NET? Du är på rätt plats! Denna handledning guidar dig genom processen steg-för-steg, vilket säkerställer att du enkelt kan hantera dina dokument. Oavsett om du är en erfaren utvecklare eller nybörjare, kommer vår guide att ge dig all information du behöver för att komma igång.
## Förutsättningar
Innan du dyker in i handledningen, se till att du har följande förutsättningar på plats:
- Utvecklingsmiljö: Visual Studio installerad på din maskin.
- .NET Framework: Se till att du har .NET Framework 4.6.1 eller senare.
-  GroupDocs.Editor för .NET: Ladda ner den senaste versionen[här](https://releases.groupdocs.com/editor/net/).
- Grundläggande C#-kunskaper: Bekantskap med C#-programmering är viktigt.
## Importera namnområden
För att använda GroupDocs.Editor i ditt .NET-projekt måste du importera de nödvändiga namnrymden. Så här gör du:
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
Nu när vi har ställt in vår miljö och de nödvändiga namnområdena importerade, låt oss dyka in i stegen som krävs för att ladda, redigera och spara ett dokument med GroupDocs.Editor för .NET.
## Steg 1: Ladda dokumentet
Först måste vi ladda dokumentet som vi vill redigera. GroupDocs.Editor gör denna process enkel. Så här kan du göra det:

```csharp
string inputFilePath = "Your Sample Document";
Editor editor = new Editor(inputFilePath, delegate { return new Options.WordProcessingLoadOptions(); });
EditableDocument defaultWordProcessingDoc = editor.Edit();
```
 I det här steget anger vi sökvägen till dokumentet vi vill redigera och skapar en instans av`Editor` klass. De`Edit` metoden anropas sedan för att ladda dokumentet i en`EditableDocument` objekt.
## Steg 2: Ändra dokumentet
Med dokumentet laddat är det dags att göra några ändringar. Eftersom vi inte har en WYSIWYG-redigerare kopplad kommer vi att simulera redigeringsprocessen i kod.

```csharp
string allEmbeddedInsideString = defaultWordProcessingDoc.GetEmbeddedHtml();
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
EditableDocument editedDoc = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```
 Här hämtar vi dokumentets inbäddade HTML-innehåll, utför en enkel textersättning och skapar en ny`EditableDocument`instans från den modifierade HTML-koden.
## Steg 3: Spara dokumentet
Efter att ha redigerat dokumentet är det sista steget att spara det. GroupDocs.Editor ger flera alternativ för att spara dokumentet i olika format.
## Spara som RTF
```csharp
string outputRtfPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.rtf");
WordProcessingSaveOptions rtfSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
editor.Save(editedDoc, outputRtfPath, rtfSaveOptions);
```
## Spara som DOCM
```csharp
string outputDocmPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.docm");
WordProcessingSaveOptions docmSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm);
using (FileStream outputStream = File.Create(outputDocmPath))
{
    editor.Save(editedDoc, outputStream, docmSaveOptions);
}
```
## Spara som vanlig text
```csharp
string outputTxtPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.txt");
TextSaveOptions textSaveOptions = new TextSaveOptions
{
    Encoding = System.Text.Encoding.UTF8,
    PreserveTableLayout = true
};
editor.Save(editedDoc, outputTxtPath, textSaveOptions);
```
## Steg 4: Rengöring
 Slutligen är det viktigt att göra sig av med`EditableDocument` och`Editor` instanser för att frigöra resurser.
```csharp
editedDoc.Dispose();
defaultWordProcessingDoc.Dispose();
editor.Dispose();
```
Genom att följa dessa steg kan du effektivt ladda, redigera och spara dokument med GroupDocs.Editor för .NET. Detta kraftfulla verktyg ger flexibilitet och användarvänlighet, vilket gör dokumenthanteringen till en lek.
## Slutsats
Att redigera och spara dokument programmatiskt har aldrig varit enklare med GroupDocs.Editor för .NET. Den här guiden ledde dig genom hela processen, från att ladda ett dokument till att spara det i olika format. Med GroupDocs.Editor har du en mångsidig och robust lösning till hands, vilket förenklar dokumentredigeringsprocessen.
## FAQ's
### Vilka filformat stöder GroupDocs.Editor?
GroupDocs.Editor stöder olika filformat, inklusive DOCX, RTF, TXT och många fler. För en fullständig lista, kolla in[dokumentation](https://reference.groupdocs.com/editor/net/).
### Kan jag prova GroupDocs.Editor innan jag köper?
 Ja, du kan få en[gratis provperiod](https://releases.groupdocs.com/) för att testa funktionerna i GroupDocs.Editor.
### Finns det någon support tillgänglig om jag stöter på problem?
 Absolut! Du kan besöka[supportforum](https://forum.groupdocs.com/c/editor/20) för hjälp med eventuella problem du stöter på.
### Hur får jag en tillfällig licens?
 Du kan begära en[tillfällig licens](https://purchase.groupdocs.com/temporary-license/) i utvärderingssyfte.
### Var kan jag köpa den fullständiga versionen av GroupDocs.Editor?
 Du kan köpa den fullständiga versionen[här](https://purchase.groupdocs.com/buy).