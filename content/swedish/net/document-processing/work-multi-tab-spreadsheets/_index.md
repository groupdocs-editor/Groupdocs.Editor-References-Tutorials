---
title: Arbeta med kalkylblad med flera flikar
linktitle: Arbeta med kalkylblad med flera flikar
second_title: GroupDocs.Editor .NET API
description: Lär dig hur du arbetar med kalkylblad med flera flikar i .NET med GroupDocs.Editor. Steg-för-steg-guide, kodexempel och bästa praxis ingår.
weight: 17
url: /sv/net/document-processing/work-multi-tab-spreadsheets/
---

# Arbeta med kalkylblad med flera flikar

## Introduktion
Att hantera kalkylblad med flera flikar kan vara en ganska stor uppgift, särskilt när du behöver manipulera eller extrahera data från olika ark i samma dokument. Om du arbetar med .NET och letar efter en robust lösning är GroupDocs.Editor för .NET ett utmärkt val. I den här självstudien går vi igenom processen att arbeta med kalkylblad med flera flikar med hjälp av GroupDocs.Editor för .NET. Vi kommer att täcka allt från att ställa in din miljö till att spara varje flik som en separat fil.
## Förutsättningar
Innan du dyker in i handledningen, se till att du har följande förutsättningar på plats:
1. Visual Studio: Se till att du har Visual Studio installerat på din dator.
2. .NET Framework: GroupDocs.Editor för .NET stöder .NET Framework 4.0 eller högre.
3. GroupDocs.Editor för .NET: Ladda ner och installera GroupDocs.Editor för .NET-biblioteket. Du kan få det från[nedladdningssida](https://releases.groupdocs.com/editor/net/).
4.  Licens: Medan du kan använda en[tillfällig licens](https://purchase.groupdocs.com/temporary-license/) för att prova biblioteket rekommenderas det att köpa en fullständig licens för produktionsanvändning.
## Importera namnområden
Innan vi börjar koda måste du importera de nödvändiga namnrymden. Lägg till följande med hjälp av direktiv överst i din .cs-fil:
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
## 1. Hämta en sökväg till indatafilen
Först måste du ange sökvägen till din inmatade kalkylarksfil. Den här filen bör vara en XLSX (OOXML) med flera flikar.
```csharp
string inputFilePath = "Your Sample Document";
```
## 2. Ladda kalkylarket i Editor-instansen
 Därefter ska du ladda kalkylarket i en`Editor` exempel. Detta görs med hjälp av en filström och ange lämpliga laddningsalternativ för ett kalkylblad.
```csharp
using (FileStream inputStream = File.OpenRead(inputFilePath))
{
    using (Editor editor = new Editor(delegate { return inputStream; }, delegate { return new SpreadsheetLoadOptions(); }))
    {
        // Ytterligare steg kommer att gå här
    }
}
```
## 3. Skapa ett redigerbart dokument från den första fliken
 För att redigera eller manipulera en specifik flik måste du skapa en`EditableDocument` instans för den fliken. Fliken anges med ett 0-baserat index.
```csharp
SpreadsheetEditOptions editOptions1 = new SpreadsheetEditOptions();
editOptions1.WorksheetIndex = 0; // Första fliken
EditableDocument firstTabBeforeEdit = editor.Edit(editOptions1);
```
## 4. Skapa ett redigerbart dokument från den andra fliken
 Skapa på samma sätt en`EditableDocument` för den andra fliken.
```csharp
SpreadsheetEditOptions editOptions2 = new SpreadsheetEditOptions();
editOptions2.WorksheetIndex = 1; // Andra fliken
EditableDocument secondTabBeforeEdit = editor.Edit(editOptions2);
```
## 5. Spara den första fliken i ett separat dokument
Spara nu den första fliken som ett separat dokument. Ange sparformat och utdatasökväg.
```csharp
SpreadsheetSaveOptions saveOptions1 = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
string outputFilename1 = Path.GetFileNameWithoutExtension(inputFilePath) + "_tab1.xlsm";
string outputPath1 = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename1);
editor.Save(firstTabBeforeEdit, outputPath1, saveOptions1);
```
## 6. Spara den andra fliken i ett separat dokument
Upprepa processen för den andra fliken, men denna gång spara den i ett annat format.
```csharp
SpreadsheetSaveOptions saveOptions2 = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsb);
string outputFilename2 = Path.GetFileNameWithoutExtension(inputFilePath) + "_tab2.xlsb";
string outputPath2 = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename2);
editor.Save(secondTabBeforeEdit, outputPath2, saveOptions2);
```
## 7. Kassera EditableDocument Instances
 Slutligen, se till att du kasserar den på rätt sätt`EditableDocument` instanser för att frigöra resurser.
```csharp
firstTabBeforeEdit.Dispose();
secondTabBeforeEdit.Dispose();
```

## Slutsats
Genom att följa dessa steg kan du enkelt arbeta med kalkylblad med flera flikar i .NET med GroupDocs.Editor. Detta kraftfulla bibliotek förenklar processen att redigera och spara olika ark i ett kalkylblad, vilket gör dina utvecklingsuppgifter mer hanterbara. Oavsett om du har att göra med komplex datamanipulation eller enkla redigeringar, tillhandahåller GroupDocs.Editor för .NET de verktyg du behöver för att få jobbet gjort effektivt.
## FAQ's
### Vad är GroupDocs.Editor för .NET?
GroupDocs.Editor för .NET är ett kraftfullt dokumentredigerings-API som tillåter utvecklare att ladda, redigera och spara dokument i olika format inom .NET-applikationer.
### Kan jag prova GroupDocs.Editor för .NET innan jag köper?
 Ja, du kan använda en[gratis provperiod](https://releases.groupdocs.com/) eller begära en[tillfällig licens](https://purchase.groupdocs.com/temporary-license/) att utvärdera produkten.
### Vilka filformat stöds av GroupDocs.Editor för .NET?
GroupDocs.Editor stöder ett brett utbud av format, inklusive DOCX, XLSX, PPTX, PDF och många fler.
### Hur får jag support för GroupDocs.Editor för .NET?
 Du kan få stöd genom att besöka[supportforum](https://forum.groupdocs.com/c/editor/20).
### Var kan jag köpa en fullständig licens för GroupDocs.Editor för .NET?
 Du kan köpa en fullständig licens från[köpsidan](https://purchase.groupdocs.com/buy).