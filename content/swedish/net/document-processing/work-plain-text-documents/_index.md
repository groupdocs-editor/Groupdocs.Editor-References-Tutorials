---
title: Arbeta med vanliga textdokument
linktitle: Arbeta med vanliga textdokument
second_title: GroupDocs.Editor .NET API
description: Lär dig att redigera vanliga textdokument med GroupDocs.Editor för .NET med vår steg-för-steg-guide. Förenkla din .NET-dokumentredigeringsprocessen.
weight: 15
url: /sv/net/document-processing/work-plain-text-documents/
---

# Arbeta med vanliga textdokument

## Introduktion
Vill du effektivisera din dokumentredigering i .NET? Leta inte längre än till GroupDocs.Editor för .NET! Detta kraftfulla API låter dig redigera en mängd olika dokumentformat med lätthet. I den här självstudien guidar vi dig genom processen att arbeta med vanliga textdokument med GroupDocs.Editor för .NET. I slutet kommer du att vara utrustad för att hantera textdokumentredigering som ett proffs. Redo att dyka i? Låt oss börja!
## Förutsättningar
Innan vi börjar finns det några saker du måste ha på plats:
- .NET-utvecklingsmiljö: Se till att du har en fungerande .NET-utvecklingsmiljö inrättad. Visual Studio är ett populärt val.
-  GroupDocs.Editor för .NET: Ladda ner och installera[GroupDocs.Editor för .NET](https://releases.groupdocs.com/editor/net/).
- Grundläggande C#-kunskaper: Bekantskap med C#-programmeringsspråket hjälper dig att följa exemplen.
- Textredigerare: Alla textredigerare fungerar, även om Visual Studio Code rekommenderas för dess funktioner och användarvänlighet.
## Importera namnområden
För att börja använda GroupDocs.Editor för .NET måste du importera de nödvändiga namnrymden till ditt projekt. Detta säkerställer att alla erforderliga klasser och metoder är tillgängliga för användning.
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```
Låt oss dela upp processen i hanterbara steg. Följ med när vi guidar dig genom varje steg av redigering av vanliga textdokument med GroupDocs.Editor för .NET.
## Steg 1: Få en sökväg till TXT-inmatningsfilen
Först måste du ange sökvägen till TXT-inmatningsfilen. Detta kan vara en sökväg till en lokal fil eller en ström som innehåller filinnehållet.
```csharp
string inputFilePath = "YourSampleDocument.txt";
```
## Steg 2: Skapa en Editor-instans
 Skapa sedan en instans av`Editor` klass. Denna klass ansvarar för att ladda och redigera dokument. Inga laddningsalternativ krävs i detta skede.
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## Steg 3: Skapa TXT-redigeringsalternativ
Skapa nu TXT-redigeringsalternativen. Dessa alternativ låter dig ange hur textinnehållet ska bearbetas under redigering.
```csharp
    TextEditOptions editOptions = new TextEditOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        RecognizeLists = true,
        LeadingSpaces = TextLeadingSpacesOptions.ConvertToIndent,
        TrailingSpaces = TextTrailingSpacesOptions.Trim
    };
```
## Steg 4: Skapa en EditableDocument-instans
 Med redigeringsalternativen inställda skapar du en`EditableDocument` exempel. Detta representerar dokumentet i ett redigerbart format.
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## Steg 5: Redigera dokumentinnehållet
Hämta det ursprungliga textinnehållet och gör önskade ändringar. I det här exemplet kommer vi att ersätta ordet "text" med "REDIGERAD text".
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("text", "EDITED text");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## Steg 6: Skapa ett redigerbart dokument med uppdaterat innehåll
 När du har gjort de nödvändiga ändringarna skapar du en ny`EditableDocument` med det uppdaterade innehållet och de ursprungliga resurserna.
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## Steg 7: Skapa WordProcessing Spara alternativ
Förbered sparalternativen för WordProcessing-formatet. Det här exemplet använder DOCM-formatet och anger språket.
```csharp
    WordProcessingSaveOptions wordSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm)
    {
        Locale = System.Globalization.CultureInfo.GetCultureInfo("en-GB")
    };
```
## Steg 8: Skapa TXT-sparalternativ
Skapa på samma sätt sparalternativen för TXT-formatet. Se till att kodningen är inställd på UTF-8 och bevara tabelllayouten.
```csharp
    TextSaveOptions txtSaveOptions = new TextSaveOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        PreserveTableLayout = true
    };
```
## Steg 9: Förbered utdatabanor
Förbered sökvägarna för att spara de resulterande DOCX- och TXT-filerna. Använd indatafilens sökväg för att bestämma utdatakatalogen och filnamnen.
```csharp
    string outputWordPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".docm");
    string outputTxtPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".txt");
```
## Steg 10: Spara det redigerade dokumentet
Slutligen sparar du det redigerade dokumentet i både DOCX- och TXT-formaten med de angivna sparalternativen.
```csharp
    editor.Save(afterEdit, outputWordPath, wordSaveOptions);
    editor.Save(afterEdit, outputTxtPath, txtSaveOptions);
}
System.Console.WriteLine("Document editing process completed successfully!");
```
## Slutsats
 Grattis! Du har framgångsrikt redigerat ett vanligt textdokument med GroupDocs.Editor för .NET. Detta kraftfulla verktyg förenklar dokumentredigering, vilket gör det enkelt att integrera i dina .NET-applikationer. Oavsett om du hanterar enkla textfiler eller komplexa dokumentformat, har GroupDocs.Editor dig täckt. Utforska fler funktioner och möjligheter genom att besöka[GroupDocs.Editor dokumentation](https://tutorials.groupdocs.com/editor/net/).
## FAQ's
### Vilka filformat stöder GroupDocs.Editor för .NET?
 GroupDocs.Editor för .NET stöder ett brett utbud av filformat, inklusive DOCX, TXT, HTML och mer. Kolla[dokumentation](https://tutorials.groupdocs.com/editor/net/) för en fullständig lista.
### Hur kan jag få en gratis provversion av GroupDocs.Editor för .NET?
 Du kan ladda ner en gratis provversion av GroupDocs.Editor för .NET från[släpper sida](https://releases.groupdocs.com/).
### Kan jag köpa en tillfällig licens för GroupDocs.Editor för .NET?
Ja, du kan få en tillfällig licens från[GroupDocs köpsida](https://purchase.groupdocs.com/temporary-license/).
### Var kan jag få support för GroupDocs.Editor för .NET?
 Support finns tillgänglig via[GroupDocs.Editor supportforum](https://forum.groupdocs.com/c/editor/20).
### Finns det detaljerad dokumentation tillgänglig för GroupDocs.Editor för .NET?
 Ja, detaljerad dokumentation finns tillgänglig på[GroupDocs.Editor dokumentationssida](https://tutorials.groupdocs.com/editor/net/).