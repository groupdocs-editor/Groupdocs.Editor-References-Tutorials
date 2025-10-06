---
title: Spara redigerat dokument i olika format
linktitle: Spara redigerat dokument i olika format
second_title: GroupDocs.Editor .NET API
description: Lär dig hur du sparar redigerade dokument i olika format med GroupDocs.Editor för .NET i den här omfattande steg-för-steg-guiden.
weight: 11
url: /sv/net/document-processing/save-edited-document-various-formats/
type: docs
---
# Spara redigerat dokument i olika format

## Introduktion
Vill du spara redigerade dokument i olika format med GroupDocs.Editor för .NET? Du har kommit till rätt ställe! Den här omfattande guiden leder dig genom hela processen, från att ställa in din miljö till att spara ditt redigerade dokument i flera format. Låt oss dyka in och göra dokumentredigering och spara enkelt!
## Förutsättningar
Innan vi börjar, se till att du har följande:
1.  GroupDocs.Editor för .NET - Ladda ner den senaste versionen från[här](https://releases.groupdocs.com/editor/net/).
2. Utvecklingsmiljö - Visual Studio eller någon annan .NET-kompatibel IDE.
3. .NET Framework - Se till att du har .NET Framework 4.6.1 eller senare installerat.
4. Exempeldokument - Ett exempel på WordProcessing-dokument att arbeta med.
5. Grundläggande C#-kunskaper - Bekantskap med C#-programmering krävs.
## Importera namnområden
För att börja, se till att du importerar de nödvändiga namnrymden till ditt C#-projekt. Detta är avgörande för att få åtkomst till GroupDocs.Editor-funktionalitet.
```csharp
using System;
using GroupDocs.Editor.Metadata;
```
Låt oss dela upp processen i hanterbara steg. Följ noga för att säkerställa att du förstår varje del.
## Steg 1: Få en sökväg till indatafilen
Först måste du ange sökvägen till din inmatade WordProcessing-fil. Den här filen kommer att laddas och redigeras.
```csharp
string inputFilePath = "Your Sample Document";
```
## Steg 2: Skapa laddningsalternativ för dokumentet
Skapa sedan laddningsalternativ som är specifika för WordProcessing-dokument. Dessa alternativ hjälper dig att anpassa hur dokumentet laddas.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
```
## Steg 3: Ladda dokumentet med alternativ
 Ladda nu dokumentet i en`Editor` instans med de angivna laddningsalternativen.
```csharp
using (Editor editor = new Editor(inputFilePath, delegate { return loadOptions; }))
```
## Steg 4: Skapa redigeringsalternativ
Förbered redigeringsalternativ för dokumentet. Dessa alternativ avgör hur dokumentet öppnas för redigering.
```csharp
WordProcessingEditOptions editOptions = new WordProcessingEditOptions();
```
## Steg 5: Öppna dokument för redigering
 Öppna dokumentet för redigering genom att skapa en`EditableDocument`exempel. Den här instansen låter dig göra ändringar i dokumentet.
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
```
## Steg 6: Redigera dokumentinnehållet
Nu är det dags att redigera innehållet i dokumentet. Skaffa först dokumentet som en enda base64-kodad sträng.
```csharp
string allEmbeddedInsideString = beforeEdit.GetEmbeddedHtml();
```
Låt oss till exempel ändra undertexten i dokumentet.
```csharp
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
```
## Steg 7: Skapa nytt redigerbart dokument från redigerat innehåll
 Skapa en ny`EditableDocument` instans från det redigerade innehållet och resurserna.
```csharp
using (EditableDocument afterEdit = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null))
```
## Steg 8: Spara dokument i olika format
Slutligen, iterera över alla stödbara WordProcessing-format och spara det redigerade dokumentet i varje format.
```csharp
foreach (WordProcessingFormats oneFormat in WordProcessingFormats.All)
{
    // Förbered sparalternativ
    WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(oneFormat);
    // Förbered sparväg
    string savePath = Path.Combine("OutputDirectory", "MultipleOutFormats." + saveOptions.OutputFormat.Extension);
    // Spara dokumentet
    editor.Save(afterEdit, savePath, saveOptions);
}
```
## Meddelande om slutförande
Som avslutning kan du skriva ut ett meddelande som anger att processen har slutförts.
```csharp
Console.WriteLine("SavingEditedDocumentToAllFormats routine has successfully finished");
```
## Slutsats
Grattis! Du har framgångsrikt lärt dig hur du sparar redigerade dokument i olika format med GroupDocs.Editor för .NET. Detta kraftfulla verktyg gör det enkelt att manipulera och spara dokument i flera format med bara några rader kod. Kom ihåg att de viktigaste stegen innebär att ladda dokumentet, redigera innehållet och spara det i önskade format.
## FAQ's
### Vad är GroupDocs.Editor för .NET?
GroupDocs.Editor för .NET är ett kraftfullt API som låter dig redigera dokument i olika format med .NET-applikationer.
### Kan jag använda GroupDocs.Editor gratis?
 Ja, du kan använda den med en gratis provperiod. Ladda ner det[här](https://releases.groupdocs.com/).
### Vilka format stöds av GroupDocs.Editor?
GroupDocs.Editor stöder ett brett utbud av format, inklusive DOCX, PDF, HTML och många fler.
### Hur får jag en tillfällig licens för GroupDocs.Editor?
 Du kan få en tillfällig licens[här](https://purchase.groupdocs.com/temporary-license/).
### Var kan jag hitta mer dokumentation och support?
 Detaljerad dokumentation finns tillgänglig[här](https://tutorials.groupdocs.com/editor/net/) , och du kan få stöd[här](https://forum.groupdocs.com/c/editor/20).