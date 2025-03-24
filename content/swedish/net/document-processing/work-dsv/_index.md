---
title: Arbeta med avgränsade separerade värden (DSV)
linktitle: Arbeta med avgränsade separerade värden (DSV)
second_title: GroupDocs.Editor .NET API
description: Lär dig hur du redigerar CSV- och TSV-filer med GroupDocs.Editor för .NET med denna steg-för-steg-guide. Förbättra dina .NET-projekt utan ansträngning.
weight: 12
url: /sv/net/document-processing/work-dsv/
---

# Arbeta med avgränsade separerade värden (DSV)

## Introduktion
Om du är en utvecklare som arbetar med avgränsade separerade värden (DSV) som CSV- eller TSV-filer, vet du att det kan vara en skrämmande uppgift att redigera dessa filer programmatiskt. Men med GroupDocs.Editor för .NET blir denna uppgift betydligt enklare och effektivare. I den här handledningen går vi igenom hur du använder GroupDocs.Editor för .NET för att läsa, redigera och spara DSV-filer. Vi delar upp processen i steg som är lätta att följa, vilket gör det enkelt för dig att implementera i dina projekt.
## Förutsättningar
Innan vi dyker in i handledningen, se till att du har följande förutsättningar:
- Visual Studio: Se till att du har Visual Studio installerat på din dator.
-  GroupDocs.Editor för .NET: Du måste ladda ner och referera till GroupDocs.Editor for .NET-biblioteket. Du kan ladda ner den[här](https://releases.groupdocs.com/editor/net/).
- Grundläggande förståelse för C#: Denna handledning förutsätter att du har en grundläggande förståelse för C#- och .NET-utveckling.
## Importera namnområden
Först måste du importera de nödvändiga namnrymden i ditt projekt. Dessa namnområden tillhandahåller de klasser och metoder som krävs för att arbeta med GroupDocs.Editor för .NET.
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

## Steg 1: Hämta en sökväg till DSV-inmatningsfilen
Först måste du ange sökvägen till DSV-inmatningsfilen. I det här exemplet antar vi att det är en CSV-fil.
```csharp
string inputFilePath = "Your Sample Document";
```
## Steg 2: Skapa en Editor-instans
 Skapa en instans av`Editor` klass. Denna instans kommer att användas för att ladda och manipulera DSV-filen.
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## Steg 3: Skapa DSV-redigeringsalternativ
 Skapa sedan en instans av`DelimitedTextEditOptions` och ange avgränsaren för DSV-filen. Här använder vi ett kommatecken som avgränsare.
```csharp
    Options.DelimitedTextEditOptions editOptions = new DelimitedTextEditOptions(",");
    editOptions.ConvertDateTimeData = false;
    editOptions.ConvertNumericData = true;
    editOptions.TreatConsecutiveDelimitersAsOne = true;
```
## Steg 4: Skapa en EditableDocument-instans
 Skapa en`EditableDocument` instans med hjälp av`Editor.Edit` metod. Detta förbereder dokumentet för redigering.
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## Steg 5: Redigera dokumentinnehållet
Hämta det ursprungliga textinnehållet och gör nödvändiga ändringar. Låt oss ersätta lite text i demonstrationssyfte.
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("SsangYong", "Chevrolet").Replace("Kyron", "Camaro");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## Steg 6: Skapa ett redigerbart dokument med uppdaterat innehåll
 Skapa en ny`EditableDocument` med det uppdaterade innehållet.
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## Steg 7: Skapa CSV-sparalternativ
Ange sparalternativ för CSV-format, inklusive avgränsare och kodning.
```csharp
    Options.DelimitedTextSaveOptions csvSaveOptions = new DelimitedTextSaveOptions(",");
    csvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## Steg 8: Skapa TSV-sparalternativ
På samma sätt, ange sparalternativen för TSV-format.
```csharp
    Options.DelimitedTextSaveOptions tsvSaveOptions = new DelimitedTextSaveOptions("\t");
    tsvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## Steg 9: Skapa sparalternativ för kalkylblad
Om du behöver spara dokumentet som ett kalkylblad, skapa motsvarande sparalternativ.
```csharp
    Options.SpreadsheetSaveOptions cellsSaveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
```
## Steg 10: Förbered Spara sökvägar
Definiera sökvägarna där de redigerade filerna ska sparas.
```csharp
    string outputCsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".csv");
    string outputTsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".tsv");
    string outputCellsPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".xlsm");
```
## Steg 11: Spara det redigerade dokumentet
Spara det redigerade dokumentet till de angivna sökvägarna i olika format.
```csharp
    editor.Save(afterEdit, outputCsvPath, csvSaveOptions);
    editor.Save(afterEdit, outputTsvPath, tsvSaveOptions);
    editor.Save(afterEdit, outputCellsPath, cellsSaveOptions);
```
## Steg 12: Kasta EditableDocument Instances
 Slutligen, se till att kassera`EditableDocument` instanser för att frigöra resurser.
```csharp
    beforeEdit.Dispose();
    afterEdit.Dispose();
}
System.Console.WriteLine("WorkingWithDsv routine has successfully finished");
```
## Slutsats
Att redigera DSV-filer med GroupDocs.Editor för .NET är en enkel process som innebär att skapa en redigeringsinstans, ställa in redigeringsalternativ, ändra innehållet och spara ändringarna. Den här steg-för-steg-guiden bör hjälpa dig att enkelt integrera denna funktion i dina .NET-applikationer. Oavsett om du arbetar med CSV, TSV eller andra DSV-format erbjuder GroupDocs.Editor för .NET en robust och flexibel lösning.
## FAQ's
### Kan jag använda GroupDocs.Editor för .NET för att redigera stora CSV-filer?
Ja, GroupDocs.Editor för .NET kan hantera stora CSV-filer effektivt.
### Stöder GroupDocs.Editor för .NET andra DSV-format förutom CSV och TSV?
Ja, den stöder olika DSV-format så länge du anger lämplig avgränsare.
### Är det möjligt att anpassa kodningen när du sparar DSV-filer?
Absolut, du kan ange önskad kodning i sparalternativen.
### Kan jag konvertera en CSV-fil till ett Excel-kalkylblad med GroupDocs.Editor för .NET?
Ja, du kan spara en CSV-fil som ett Excel-kalkylblad genom att använda lämpliga sparaalternativ.
### Var kan jag hitta mer dokumentation om GroupDocs.Editor för .NET?
 Du kan hitta detaljerad dokumentation[här](https://tutorials.groupdocs.com/editor/net/)