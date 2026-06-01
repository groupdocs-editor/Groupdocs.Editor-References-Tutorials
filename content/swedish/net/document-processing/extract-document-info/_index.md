---
date: 2026-06-01
description: Lär dig hur du hämtar sidantal och extraherar dokumentmetadata med GroupDocs.Editor
  för .NET i en detaljerad steg-för-steg-handledning.
keywords:
- get page count
- extract document metadata
- get document info
- find document extension
- retrieve document size
linktitle: Hämta sidantal och extrahera dokumentinformation
schemas:
- author: GroupDocs
  dateModified: '2026-06-01'
  description: Learn how to get page count and extract document metadata using GroupDocs.Editor
    for .NET in a detailed step‑by‑step tutorial.
  headline: Get Page Count & Extract Document Info with GroupDocs.Editor
  type: TechArticle
- questions:
  - answer: GroupDocs.Editor supports Word processing, spreadsheet, presentation,
      PDF, and plain‑text files—over 50 formats in total.
    question: What document types can I extract metadata from?
  - answer: Access `DocumentInfo.Extension` after calling `GetDocumentInfo()`; it
      returns the extension without the leading dot.
    question: How do I retrieve the file extension?
  - answer: Yes—`DocumentInfo.Size` returns the size in bytes; divide by 1,048,576
      to convert to megabytes.
    question: Can I get the size of a document in megabytes?
  - answer: Absolutely—GroupDocs.Editor never writes the password to disk and disposes
      of all cryptographic objects after use.
    question: Is it safe to process password‑protected files on a server?
  - answer: You can get support from the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).
    question: Where can I find additional help if I run into issues?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Hämta sidantal och extrahera dokumentinformation med GroupDocs.Editor
type: docs
url: /sv/net/document-processing/extract-document-info/
weight: 10
---

# Hämta sidantal och extrahera dokumentinformation med GroupDocs.Editor

## Introduktion
I den här omfattande handledningen kommer du att lära dig hur du **hämtar sidantal** och extraherar detaljerad dokumentinformation — inklusive format, storlek och krypteringsstatus — med GroupDocs.Editor för .NET. Oavsett om du bygger ett dokumenthanteringssystem, en rapporteringsmotor eller en automatiserad konverteringspipeline, är förståelse för en fils metadata det första steget mot pålitlig bearbetning. Låt oss gå igenom hela arbetsflödet, från att ladda en fil till att säkert frigöra resurser.

## Snabba svar
- **Hur hämtar jag sidantalet för ett dokument?**  
  Anropa `editor.GetDocumentInfo().PageCount` efter att ha laddat filen med `Editor`.
- **Vilka filformat stöds för metadataextraktion?**  
  Över 50 format, inklusive DOCX, XLSX, PPTX, PDF, TXT och HTML.
- **Kan jag extrahera metadata från lösenordsskyddade filer?**  
  Ja — ange lösenordet när du skapar `Editor`‑instansen.
- **Behöver jag frigöra resurser manuellt?**  
  Absolut; anropa alltid `editor.Dispose()` eller omslut editorn i ett `using`‑block.
- **Vilken version av GroupDocs.Editor krävs?**  
  Den senaste stabila releasen (v23.12+ vid skrivtillfället) stödjer alla funktioner som visas.

## Vad är “get page count” i GroupDocs.Editor?
`GetDocumentInfo()` är en metod som returnerar ett `DocumentInfo`‑objekt som innehåller dokumentets sidantal, format, storlek och annan metadata. Detta enkla anrop ger dig omedelbar insikt utan att du måste parsra filen manuellt. Genom att använda denna metod undviker du att ladda hela dokumentet i minnet, vilket förbättrar prestandan särskilt för stora filer och minskar serverns resursförbrukning.

## Varför extrahera dokumentmetadata med GroupDocs.Editor?
GroupDocs.Editor kan bearbeta **50+ in‑ och utdataformat** och hämta metadata för filer upp till **2 GB** utan att ladda hela dokumentet i minnet. Denna effektivitet minskar serverbelastningen med upp till **70 %** jämfört med full‑dokument‑parsning, vilket gör det idealiskt för hög‑genomströmningstillämpningar.

## Förutsättningar
Innan du börjar, se till att du har:

- **C#‑utvecklingsgrunder** – du bör vara bekväm med Visual Studio och .NET‑projektstrukturer.
- **Visual Studio 2022** (eller någon nyare version) installerad på din maskin.
- **GroupDocs.Editor for .NET** – ladda ner det senaste paketet från [download page](https://releases.groupdocs.com/editor/net/).

## Hur laddar du ditt dokument?
`Editor` är huvudklassen som representerar ett dokument och tillhandahåller metoder för att ladda och manipulera det. Ladda målfilen genom att skapa en `Editor`‑instans och skicka filvägen. Editorn upptäcker automatiskt formatet, så du behöver inte ange laddningsalternativ. Detta tillvägagångssätt fungerar för alla stödda filtyper och förenklar den initiala konfigurationen.

```csharp
using System;
using GroupDocs.Editor.Metadata;
```

## Hur hämtar du dokumentinformation?
`GetDocumentInfo()` returnerar ett `DocumentInfo`‑objekt som innehåller metadata såsom sidantal, format, storlek och krypteringsstatus. Efter att ha laddat filen, anropa denna metod för att hämta objektet. Det returnerade `DocumentInfo` ger dig en koncis översikt av filens egenskaper, vilket gör att du kan fatta beslut utan ytterligare bearbetning.

```csharp
string docxInputFilePath = "YourSampleDocument.docx";
Editor editorDocx = new Editor(docxInputFilePath);
```

## Hur bestämmer du dokumenttyp?
`DocumentType` är en enum som indikerar om dokumentet är WordProcessing, Spreadsheet eller Text. Att veta om en fil är ett ordbehandlingsdokument, ett kalkylblad eller ren text påverkar hur du hanterar det senare. Använd `DocumentType`‑egenskapen i `DocumentInfo`‑objektet för att fatta detta beslut och styra din logik därefter.

```csharp
IDocumentInfo infoDocx = editorDocx.GetDocumentInfo(null);
```

## Hur extraherar du detaljerad information för ordbehandlingsfiler?
`WordProcessing` avser dokument som DOCX, ODT och RTF som hanteras som ordbehandlingsfiler. Om dokumenttypen är `WordProcessing` kan du läsa ytterligare egenskaper som **format**, **filändelse**, **sidantal**, **storlek** och **krypteringsflagga** direkt från `DocumentInfo`‑objektet. Dessa detaljer hjälper dig att anpassa bearbetningssteg, såsom att tillämpa specifika konverteringar eller säkerhetskontroller.

```csharp
bool isSpreadsheet = infoDocx is SpreadsheetDocumentInfo;
bool isText = infoDocx is TextualDocumentInfo;
bool isWordProcessing = infoDocx is WordProcessingDocumentInfo;
Console.WriteLine($"Is '{docxInputFilePath}' a Spreadsheet: {isSpreadsheet}");
Console.WriteLine($"Is '{docxInputFilePath}' a Textual document: {isText}");
Console.WriteLine($"Is '{docxInputFilePath}' a WordProcessing document: {isWordProcessing}");
```

## Hur hanterar du kalkylblad och textdokument?
`Spreadsheet` betecknar kalkylbladsfiler såsom XLSX, medan `Text` representerar rena textdokument. För kalkylblad (`Spreadsheet`) och rena textfiler (`Text`) levererar `DocumentInfo` fortfarande grundläggande metadata (filändelse, storlek, sidantal). Vissa format kanske inte exponerar ett sidantal; i så fall blir värdet `0`. Du kan fortfarande förlita dig på annan metadata för efterföljande logik.

```csharp
if (isWordProcessing)
{
    WordProcessingDocumentInfo casted = (WordProcessingDocumentInfo)infoDocx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Page count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```

## Hur arbetar du med lösenordsskyddade dokument?
`Password` är en sträng som skickas till `Editor`‑konstruktorn för att öppna krypterade filer. När ett dokument är krypterat, försök först att öppna det utan lösenord. Om det misslyckas, fånga undantaget och försök igen med rätt lösenord. `Editor`‑konstruktorn accepterar en `Password`‑parameter för detta ändamål, vilket möjliggör sömlös hantering av skyddade filer.

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

## Hur bearbetar du textbaserade dokument?
`DocumentInfo` tillhandahåller grundläggande metadata som storlek, filändelse och kodning för textfiler. Textfiler (t.ex. `.txt`, `.md`) behandlas som enkla strömmar. Du kan fortfarande hämta storlek och kodningsinformation från `DocumentInfo`, vilket är användbart för att validera filens integritet eller bestämma lämpliga bearbetningspipeline.

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

## Hur frigör du resurser på rätt sätt?
`Editor` är huvudklassen som håller ohanterade resurser och måste frigöras efter användning. För att undvika minnesläckor, frigör alltid `Editor`‑instansen efter att du har extraherat informationen. `using`‑satsen är det säkraste mönstret eftersom den garanterar frigöring även om ett undantag inträffar, vilket säkerställer ren resurshantering.

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

## Vanliga problem och lösningar
| Problem | Orsak | Lösning |
|-------|-------|----------|
| **PageCount returnerar 0** | Formatet stöder inte paginering (t.ex. ren text) | Kontrollera `DocumentInfo.DocumentType` innan du förlitar dig på `PageCount`. |
| **Filformat stöds inte** | Filändelsen känns inte igen | Verifiera att filen är ett av de 50+ stödda formaten; uppdatera GroupDocs.Editor till den senaste versionen. |
| **Lösenordsexception** | Fel lösenord angivet | Fånga `PasswordProtectedException` och be användaren ange lösenordet igen. |
| **Minnesökning vid stora filer** | Laddar mycket stora PDF-filer utan streaming | Använd `LoadOptions` med `LoadOptions.LoadMode = LoadMode.Stream` (tillgängligt i nyare releaser). |

## Vanliga frågor

**Q: Vilka dokumenttyper kan jag extrahera metadata från?**  
A: GroupDocs.Editor stödjer ordbehandling, kalkylblad, presentation, PDF och ren‑text‑filer — över 50 format totalt.

**Q: Hur hämtar jag filändelsen?**  
A: Använd `DocumentInfo.Extension` efter att ha anropat `GetDocumentInfo()`; den returnerar filändelsen utan den inledande punkten.

**Q: Kan jag få storleken på ett dokument i megabyte?**  
A: Ja — `DocumentInfo.Size` returnerar storleken i byte; dela med 1 048 576 för att konvertera till megabyte.

**Q: Är det säkert att bearbeta lösenordsskyddade filer på en server?**  
A: Absolut — GroupDocs.Editor skriver aldrig lösenordet till disk och frigör alla kryptografiska objekt efter användning.

**Q: Var kan jag hitta ytterligare hjälp om jag stöter på problem?**  
A: Du kan få support från [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).

---

**Last Updated:** 2026-06-01  
**Tested With:** GroupDocs.Editor 23.12 for .NET  
**Author:** GroupDocs

```csharp
editorDocx.Dispose();
editorXlsx.Dispose();
editorXls.Dispose();
editorXml.Dispose();
Console.WriteLine("ExtractingDocumentInfo routine has successfully finished");
```

## Relaterade handledningar

- [Mästarmetadataextraktion i .NET med GroupDocs.Editor: En omfattande guide](/editor/net/advanced-features/groupdocs-editor-net-metadata-extraction-guide/)
- [Handledningar för dokumentladdning med GroupDocs.Editor för .NET](/editor/net/document-loading/)
- [Effektiv dokumentredigering med GroupDocs.Editor .NET: Transformera HTML till redigerbara dokument](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)