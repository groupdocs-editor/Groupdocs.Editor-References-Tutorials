---
date: 2026-06-06
description: Lär dig hur du **skapar redigerbart dokument** objekt från CSV- och TSV-filer
  med GroupDocs.Editor for .NET. Denna guide visar också hur du **läser avgränsad
  text C#** och **redigerar CSV .NET** effektivt i Visual Studio.
keywords:
- create editable document
- read delimited text c#
- edit csv .net
- parse delimited values c#
linktitle: Arbeta med avgränsade separerade värden (DSV) – skapa redigerbart dokument
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to **create editable document** objects from CSV and TSV
    files using GroupDocs.Editor for .NET. This guide also shows how to **read delimited
    text C#** and **edit CSV .NET** efficiently in Visual Studio.
  headline: Work with Delimited Separated Values (DSV) – create editable document
  type: TechArticle
- questions:
  - answer: Yes, the API streams data and can handle files larger than 1 GB without
      loading the entire document into memory.
    question: Can I use GroupDocs.Editor for .NET to edit large CSV files?
  - answer: Absolutely – any single‑character delimiter (e.g., pipe `|`, semicolon
      `;`) is supported as long as you specify it in `DelimitedTextEditOptions`.
    question: Does GroupDocs.Editor for .NET support other DSV formats besides CSV
      and TSV?
  - answer: Yes, you can set the `Encoding` property in `DelimitedTextSaveOptions`
      to UTF‑8, UTF‑16, ISO‑8859‑1, or any .NET `Encoding` you require.
    question: Is it possible to customize the encoding when saving DSV files?
  - answer: Yes – after editing, simply use `SpreadsheetSaveOptions` to export the
      content as an `.xlsx` workbook.
    question: Can I convert a CSV file to an Excel spreadsheet using GroupDocs.Editor
      for .NET?
  - answer: Detailed API references and code samples are available **[here](https://tutorials.groupdocs.com/editor/net/)**.
    question: Where can I find more documentation on GroupDocs.Editor for .NET?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Arbeta med avgränsade separerade värden (DSV) – skapa redigerbart dokument
type: docs
url: /sv/net/document-processing/work-dsv/
weight: 12
---

# Arbeta med avgränsade separerade värden (DSV) – skapa redigerbart dokument

Om du är en .NET‑utvecklare som behöver **create editable document**‑objekt från avgränsade separerade värden (DSV) såsom CSV eller TSV, har du kommit till rätt ställe. På de första 100 orden förklarar vi varför GroupDocs.Editor för .NET är det mest pålitliga sättet att **read delimited text C#**, redigera det och sedan spara tillbaka utan att förlora formatering. Du får ett komplett, kopiera‑och‑klistra‑klart arbetsflöde som passar naturligt i vilken Visual Studio‑lösning som helst.

## Snabba svar
- **Vilket bibliotek hanterar CSV‑redigering bäst i .NET?** GroupDocs.Editor for .NET.
- **Kan jag redigera stora CSV‑filer i Visual Studio?** Ja – API‑et strömmar data och undviker att ladda hela filen i minnet.
- **Behöver jag en licens för produktionsanvändning?** En kommersiell licens krävs; en gratis provversion finns tillgänglig.
- **Vilka format kan jag exportera efter redigering?** CSV, TSV och Excel‑kompatibla kalkylbladsformat.
- **Är API‑et kompatibelt med .NET 6+?** Absolut – det stödjer .NET Framework 4.5+, .NET Core 3.1+, .NET 5 och .NET 6.

## Vad betyder “create editable document” i samband med GroupDocs.Editor?
**Create editable document** betyder att generera en `EditableDocument`‑instans som representerar en muterbar version av en källfil (CSV, TSV, etc.) i minnet. Detta objekt låter dig läsa, modifiera och spara om innehållet med samma API. Det erbjuder metoder för att hämta dokumenttexten, tillämpa ändringar och spara tillbaka i olika format, vilket säkerställer att kolumnjustering och citattecken bevaras.

## Varför använda GroupDocs.Editor för DSV‑hantering?
GroupDocs.Editor hanterar **more than 50 input and output formats**, inklusive CSV, TSV och Excel‑kompatibla kalkylblad, samtidigt som minnesanvändningen hålls under 10 MB för filer upp till 500 MB. Det bevarar också kolumnjustering, citeringsregler och anpassade kodningar automatiskt, vilket eliminerar behovet av manuell parsning.

## Förutsättningar
- **Visual Studio** (any recent edition) – du kommer att utveckla och felsöka direkt i IDE:n.
- **GroupDocs.Editor for .NET** – ladda ner det senaste paketet **[här](https://releases.groupdocs.com/editor/net/)**.
- **Basic C# knowledge** – handledningen förutsätter att du kan skapa ett konsol‑ eller ASP.NET‑projekt och lägga till NuGet‑paket.

## Importera namnrymder
`Editor`, `EditableDocument` och alternativklasserna finns i namnrymden `GroupDocs.Editor`.

`DelimitedTextEditOptions`‑klassen är ingångspunkten för att definiera avgränsaren (komma, tab, etc.) och andra parsningsregler.

```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

## Hur skapar man ett redigerbart dokument från en CSV‑fil?
Läs in käll‑CSV‑filen med `Editor` och anropa `Edit`‑metoden, där du skickar med en `DelimitedTextEditOptions`‑instans som specificerar kommatecken som avgränsare. Metoden returnerar ett `EditableDocument` som du kan manipulera i minnet. Detta tvåstegs‑mönster—load → edit—täckar **read delimited text C#**‑scenarier och garanterar att den ursprungliga filstrukturen bevaras.

## Steg 1: Hämta en sökväg till indata‑DSV‑filen
Först måste du ange den absoluta eller relativa sökvägen till käll‑DSV‑filen. För demonstration använder vi en enkel CSV‑fil som ligger i projektets `Data`‑mapp.

```csharp
string inputFilePath = "Your Sample Document";
```

## Steg 2: Skapa en Editor‑instans
`Editor` är kärnklassen som orkestrerar inläsning, redigering och sparning. Att instansiera den med ett `FileInfo`‑objekt ger dig full kontroll över filens livscykel.

```csharp
using (Editor editor = new Editor(inputFilePath))
{
```

## Steg 3: Skapa DSV‑redigeringsalternativ
`DelimitedTextEditOptions` talar om för editorn hur filen ska tolkas. Du kan ange avgränsare, om den första raden innehåller rubriker samt teckenkodning.

```csharp
    Options.DelimitedTextEditOptions editOptions = new DelimitedTextEditOptions(",");
    editOptions.ConvertDateTimeData = false;
    editOptions.ConvertNumericData = true;
    editOptions.TreatConsecutiveDelimitersAsOne = true;
```

## Steg 4: Skapa en EditableDocument‑instans
`EditableDocument` representerar en muterbar version av källfilen i minnet. Att anropa `Editor.Edit` med alternativen returnerar ett `EditableDocument`. Detta objekt innehåller filens text i en muterbar sträng, redo för vilken **parse delimited values C#**‑operation du än behöver.

```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```

## Steg 5: Redigera dokumentets innehåll
`GetDocumentText()` returnerar den aktuella texten i det redigerbara dokumentet som en sträng. Hämta originaltexten via `EditableDocument.GetDocumentText()`, utför dina modifieringar (t.ex. ersätt ett kolumnvärde) och lagra resultatet i en ny sträng. Här kan du **edit CSV .NET** utan att röra lågnivå‑filströmmar.

```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("SsangYong", "Chevrolet").Replace("Kyron", "Camaro");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```

## Steg 6: Skapa ett EditableDocument med uppdaterat innehåll
Packa in den modifierade strängen tillbaka i ett `EditableDocument`. Detta steg slutför ändringarna och förbereder objektet för sparning i vilket stödformat som helst.

```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```

## Steg 7: Skapa CSV‑spara‑alternativ
`DelimitedTextSaveOptions` specificerar hur det redigerade innehållet ska skrivas tillbaka till en CSV‑fil. När du är redo att spara ändringarna, konfigurera `DelimitedTextSaveOptions`. Du kan ange samma avgränsare, en annan, eller till och med ändra radslut‑stilen.

```csharp
    Options.DelimitedTextSaveOptions csvSaveOptions = new DelimitedTextSaveOptions(",");
    csvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

## Steg 8: Skapa TSV‑spara‑alternativ
Om du behöver en tab‑separerad version, byt helt enkelt avgränsaren till `\t`. Samma `EditableDocument` kan sparas flera gånger med olika alternativ.

```csharp
    Options.DelimitedTextSaveOptions tsvSaveOptions = new DelimitedTextSaveOptions("\t");
    tsvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

## Steg 9: Skapa kalkylblads‑spara‑alternativ
`SpreadsheetSaveOptions` konfigurerar export av dokumentet till Excel‑kompatibla format som .xlsx. GroupDocs.Editor låter dig också exportera de redigerade data till ett Excel‑kompatibelt format (`.xlsx`). `SpreadsheetSaveOptions`‑klassen hanterar kolumntyper, formler och cellformat automatiskt.

```csharp
    Options.SpreadsheetSaveOptions cellsSaveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
```

## Steg 10: Förbered spara‑sökvägar
Definiera separata utdata‑sökvägar för varje format. Att använda tydliga namngivningskonventioner (t.ex. `output.csv`, `output.tsv`, `output.xlsx`) hjälper till att hålla ditt projekt organiserat.

```csharp
    string outputCsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".csv");
    string outputTsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".tsv");
    string outputCellsPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".xlsm");
```

## Steg 11: Spara det redigerade dokumentet
`Save()` skriver dokumentet till disk med de angivna spara‑alternativen. Anropa `EditableDocument.Save` med lämpliga alternativ för varje målformat. API‑et skriver filen direkt till disk och bevarar den ursprungliga kodningen om du inte åsidosätter den.

```csharp
    editor.Save(afterEdit, outputCsvPath, csvSaveOptions);
    editor.Save(afterEdit, outputTsvPath, tsvSaveOptions);
    editor.Save(afterEdit, outputCellsPath, cellsSaveOptions);
```

## Steg 12: Disposera EditableDocument‑instanser
Både `Editor` och `EditableDocument` implementerar `IDisposable`. Att disponera dem frigör filhandtag och ohanterade resurser, vilket är avgörande när man bearbetar många filer i ett batchjobb.

```csharp
    beforeEdit.Dispose();
    afterEdit.Dispose();
}
System.Console.WriteLine("WorkingWithDsv routine has successfully finished");
```

## Vanliga problem och lösningar
| Problem | Varför det händer | Lösning |
|-------|----------------|-----|
| **Oväntade extra citattecken** | Standard‑CSV‑parsern kan behandla inbäddade kommatecken som avgränsare. | Ställ in `EscapeMode = EscapeMode.DoubleQuote` i `DelimitedTextEditOptions`. |
| **Stort minnesutslag för stora filer** | Laddar en 500 MB‑fil utan strömning. | Använd `Editor.Load` med `LoadOptions` som möjliggör lazy loading. |
| **Kodningsfel** | Källfilen använder UTF‑16 men alternativen är standardinställda på UTF‑8. | Ange explicit `Encoding = Encoding.Unicode` i spara‑alternativen. |

## Vanliga frågor

**Q: Kan jag använda GroupDocs.Editor för .NET för att redigera stora CSV‑filer?**  
A: Ja, API‑et strömmar data och kan hantera filer större än 1 GB utan att ladda hela dokumentet i minnet.

**Q: Stöder GroupDocs.Editor för .NET andra DSV‑format förutom CSV och TSV?**  
A: Absolut – vilken som helst enkelsymbol‑avgränsare (t.ex. pipe `|`, semikolon `;`) stöds så länge du specificerar den i `DelimitedTextEditOptions`.

**Q: Är det möjligt att anpassa kodningen vid sparning av DSV‑filer?**  
A: Ja, du kan sätta `Encoding`‑egenskapen i `DelimitedTextSaveOptions` till UTF‑8, UTF‑16, ISO‑8859‑1 eller någon annan .NET `Encoding` du behöver.

**Q: Kan jag konvertera en CSV‑fil till ett Excel‑kalkylblad med GroupDocs.Editor för .NET?**  
A: Ja – efter redigering, använd helt enkelt `SpreadsheetSaveOptions` för att exportera innehållet som en `.xlsx`‑arbetsbok.

**Q: Var kan jag hitta mer dokumentation om GroupDocs.Editor för .NET?**  
A: Detaljerade API‑referenser och kodexempel finns **[här](https://tutorials.groupdocs.com/editor/net/)**.

---

**Senast uppdaterad:** 2026-06-06  
**Testad med:** GroupDocs.Editor 23.10 for .NET  
**Författare:** GroupDocs

## Relaterade handledningar

- [Handledningar för redigering av vanlig text och DSV‑dokument för GroupDocs.Editor .NET](/editor/net/plain-text-dsv-documents/)
- [Behärska GroupDocs.Editor .NET för effektiv CSV‑dokumentredigering och konvertering](/editor/net/plain-text-dsv-documents/groupdocs-editor-net-csv-editing-guide/)
- [Mästarhandledning för dokumentladdning i .NET med GroupDocs.Editor: En omfattande guide](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)