---
date: 2026-06-06
description: Lär dig hur du listar stödda dokumentformat och bestämmer filformatets
  filändelse med GroupDocs.Editor för .NET. Step‑by‑step guide med code snippets,
  quick answers, och FAQs.
keywords:
- list supported document formats
- determine file format extension
- GroupDocs.Editor .NET
- document editing API
- supported formats guide
linktitle: Lista stödda dokumentformat
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to list supported document formats and determine file format
    extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets,
    quick answers, and FAQs.
  headline: List Supported Document Formats with GroupDocs.Editor .NET
  type: TechArticle
- description: Learn how to list supported document formats and determine file format
    extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets,
    quick answers, and FAQs.
  name: List Supported Document Formats with GroupDocs.Editor .NET
  steps:
  - name: '**.NET development environment** – Visual Studio 2022 or any IDE that supports
      .NET 6+.'
    text: '**.NET development environment** – Visual Studio 2022 or any IDE that supports
      .NET 6+.'
  - name: '**GroupDocs.Editor for .NET library** – download from the [GroupDocs releases
      page](https://releases.groupdocs.com/editor/net/).'
    text: '**GroupDocs.Editor for .NET library** – download from the [GroupDocs releases
      page](https://releases.groupdocs.com/editor/net/).'
  - name: '**Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/)
      for unrestricted access.'
    text: '**Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/)
      for unrestricted access.'
  - name: '**Basic C# knowledge** – familiarity with namespaces, `using` statements,
      and console output.'
    text: '**Basic C# knowledge** – familiarity with namespaces, `using` statements,
      and console output.'
  - name: '**Loop Through Formats:** We iterate over all available Word‑processing
      formats.'
    text: '**Loop Through Formats:** We iterate over all available Word‑processing
      formats.'
  - name: '**Output Format Details:** For each format we print its friendly name and
      default file extension.'
    text: '**Output Format Details:** For each format we print its friendly name and
      default file extension.'
  - name: '**Loop Through Formats:** The same looping logic applies to presentations.'
    text: '**Loop Through Formats:** The same looping logic applies to presentations.'
  - name: '**Output Format Details:** The name and extension are displayed for each
      format.'
    text: '**Output Format Details:** The name and extension are displayed for each
      format.'
  - name: '**Parse Format:** `FromExtension` converts the `.xlsm` extension into its
      internal `SpreadsheetFormat` enum.'
    text: '**Parse Format:** `FromExtension` converts the `.xlsm` extension into its
      internal `SpreadsheetFormat` enum.'
  - name: '**Output Format:** The parsed format’s name is printed, confirming the
      mapping.'
    text: '**Output Format:** The parsed format’s name is printed, confirming the
      mapping.'
  type: HowTo
- questions:
  - answer: '`DocumentFormatInfo` provides metadata about supported file types, while
      `SaveOptions` configures how a document is written back to disk (format, compression,
      etc.).'
    question: What is the difference between `DocumentFormatInfo` and `SaveOptions`?
  - answer: Yes—use `DocumentFormatInfo.FromExtension("yourExt")`; if the extension
      isn’t recognized, the method returns `null`.
    question: Can I list formats for a custom file extension?
  - answer: Absolutely. Pass the password to the `Editor` constructor via `EditorSettings`
      to open encrypted documents.
    question: Does GroupDocs.Editor support password‑protected files?
  - answer: Over **30 input and output formats**, spanning Word, Excel, PowerPoint,
      HTML, and plain text.
    question: How many formats does GroupDocs.Editor actually support?
  - answer: Use the `GetEditableWordProcessingFormats()` (or Spreadsheet/Presentation
      equivalents) to retrieve formats that allow full edit capabilities.
    question: Is there a way to restrict the list to only editable formats?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Lista stödda dokumentformat med GroupDocs.Editor .NET
type: docs
url: /sv/net/document-processing/work-document-formats/
weight: 13
---

# Lista stödda dokumentformat

Välkommen till vår omfattande handledning om **hur man listar stödda dokumentformat** med GroupDocs.Editor för .NET. Oavsett om du bygger en dokument‑centrerad webbapp eller ett företags‑klassat skrivbordsverktyg, är det viktigt att veta exakt vilka format du kan redigera eller konvertera. I den här guiden kommer du att upptäcka hur du enumererar format, parsar filändelser och redigerar dokument — allt med tydliga, användar‑vänliga förklaringar och färdiga kodexempel.

## Snabba svar
- **Hur listar jag alla stödda format?** Använd `DocumentFormatInfo.GetSupportedWordProcessingFormats()` (eller motsvarande för Presentation/Spreadsheet) och iterera samlingen.  
- **Kan jag avgöra ett format från en filändelse?** Ja — anropa `DocumentFormatInfo.FromExtension(".docx")`.  
- **Vilka filtyper stöder GroupDocs.Editor?** Över 30 in- och utdataformat, inklusive DOCX, XLSX, PPTX, HTML och vanlig text.  
- **Behöver jag en licens för att lista format?** En tillfällig licens låser upp hela API:et; annars fungerar en provversion med begränsade funktioner.  
- **Vilka .NET-versioner är kompatibla?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.

## Vad betyder “lista stödda dokumentformat”?
Frasen avser att programatiskt hämta samlingen av filtyper som GroupDocs.Editor kan öppna, redigera och spara. Denna operation låter dig bygga dynamiska UI‑rullgardinsmenyer eller validera användaruppladdningar innan de bearbetas, vilket säkerställer att endast kompatibla filer skickas till editorn för vidare manipulation.

## Varför lista stödda dokumentformat?
GroupDocs.Editor **stödjer 30+ in- och utdataformat** och kan hantera filer upp till **2 GB** utan att ladda hela dokumentet i minnet. Att känna till den exakta listan förhindrar körfel, förbättrar användarupplevelsen och gör det möjligt att upprätthålla affärsregler såsom “tillåt endast redigerbara Office‑dokument.” Det hjälper också att visa användarna endast de format som din applikation faktiskt stödjer.

## Förutsättningar
Innan du börjar, se till att du har:

1. **.NET‑utvecklingsmiljö** – Visual Studio 2022 eller någon IDE som stödjer .NET 6+.  
2. **GroupDocs.Editor för .NET‑bibliotek** – ladda ner från den [GroupDocs releases‑sida](https://releases.groupdocs.com/editor/net/).  
3. **Tillfällig licens** – skaffa en [tillfällig licens](https://purchase.groupdocs.com/temporary-license/) för obegränsad åtkomst.  
4. **Grundläggande C#‑kunskaper** – bekantskap med namnrymder, `using`‑satser och konsolutmatning.

## Hur listar man stödda dokumentformat?
Läs in samlingen av stödda format och skriv ut varje formats namn och filändelse. Detta tvåstegs‑mönster fungerar för Word‑processning, kalkylblad och presentationsdokument. Genom att iterera samlingen kan du dynamiskt fylla UI‑element som rullgardinsmenyer, så att användarna endast kan välja format som editorn faktiskt kan hantera.

```csharp
// No actual code block – placeholder retained from original tutorial
```csharp
using System;
using GroupDocs.Editor.Options;
```
```

### Lista Word‑processningsformat
`Formats.WordProcessingFormats` är en uppräkning som beskriver varje Word‑processningsfiltyp som editorn känner igen. `All`‑egenskapen returnerar en samling av dessa formatobjekt.

```csharp
```csharp
foreach (Formats.WordProcessingFormats oneFormat in Formats.WordProcessingFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**Förklaring:**  
1. **Loop Through Formats:** Vi itererar över alla tillgängliga Word‑processningsformat.  
2. **Output Format Details:** För varje format skriver vi ut dess vänliga namn och standardfiländelse.

### Lista presentationsformat
`Formats.PresentationFormats` fungerar på samma sätt för bildspelsfiler, och exponerar varje stödd presentationstyp via `All`‑samlingen.

```csharp
```csharp
foreach (Formats.PresentationFormats oneFormat in Formats.PresentationFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**Förklaring:**  
1. **Loop Through Formats:** Samma loop‑logik gäller för presentationer.  
2. **Output Format Details:** Namnet och filändelsen visas för varje format.

## Hur bestämmer man filformatets filändelse?
Ibland har du bara ett filnamn och måste härleda motsvarande `DocumentFormat`. GroupDocs.Editor erbjuder en enkel statisk hjälpfunktion som mappar en filändelse till dess interna formatrepresentation, vilket låter dig validera eller konvertera filer innan de laddas in i editorn.

### Parsning av kalkylbladsformat
`Formats.SpreadsheetFormats.FromExtension` konverterar en filändelsestring till motsvarande kalkylbladsformat‑enum‑värde.

```csharp
```csharp
Formats.SpreadsheetFormats expectedXlsm = Formats.SpreadsheetFormats.FromExtension(".xlsm");
Console.WriteLine("Parsed Spreadsheet format is {0}", expectedXlsm.Name);
```
```

**Förklaring:**  
1. **Parse Format:** `FromExtension` konverterar `.xlsm`‑ändelsen till sitt interna `SpreadsheetFormat`‑enum.  
2. **Output Format:** Det parsade formatets namn skrivs ut, vilket bekräftar mappningen.

### Parsning av textformat
På samma sätt löser `Formats.TextualFormats.FromExtension` textfiländelser som HTML eller TXT.

```csharp
```csharp
Formats.TextualFormats expectedHtml = Formats.TextualFormats.FromExtension("html");
Console.WriteLine("Parsed Textual format is {0}", expectedHtml.Name);
```
```

**Förklaring:**  
1. **Parse Format:** `FromExtension`‑metoden löser `html`‑ändelsen till ett `TextFormat`.  
2. **Output Format:** Namnet på textformatet visas, användbart för webbaserade editorer.

## Hur redigerar man dokument efter att ha identifierat format?
När du känner till formatet följer inläsning och redigering av ett dokument ett konsekvent mönster. Först skapar du en `Editor`‑instans med sökvägen till källfilen, sedan anropar du `Edit()` för att få ett `EditableDocument`. Därefter kan du läsa, ändra och slutligen spara innehållet med lämpliga `SaveOptions`.

### Ladda ett dokument
`Editor` är kärnklassen som kapslar in alla redigeringsoperationer för en given fil.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/document.docx"))
{
    // Further steps will be covered here.
}
```
```

**Förklaring:**  
1. **Initialize Editor:** Skapa en `Editor`‑instans och ange den fullständiga sökvägen till målfilen.  
2. **Dispose Pattern:** `using`‑satsen garanterar att alla resurser som inte hanteras frigörs omedelbart.

### Extrahera innehåll
`EditableDocument.GetContent()` returnerar dokumentets råa text (eller HTML för webbaserade editorer), som du kan visa eller manipulera.

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    string content = editableDocument.GetContent();
    Console.WriteLine(content);
}
```
```

**Förklaring:**  
1. **Edit Method:** `Edit()` returnerar ett `EditableDocument`‑objekt.  
2. **Get Content:** `GetContent()` extraherar dokumentets råa text (eller HTML för webbaserade editorer).  
3. **Output Content:** Innehållet skrivs ut i konsolen för verifiering.

### Spara ändringar
`SaveOptions` talar om för editorn hur och i vilket format den redigerade dokumentet ska skrivas tillbaka till lagring.

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    // Modify content here
    SaveOptions saveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docx);
    editor.Save(editableDocument, "path/to/save/document.docx", saveOptions);
}
```
```

**Förklaring:**  
1. **Edit Method:** Hämta `EditableDocument` igen efter ändringar.  
2. **Modify Content:** Applicera dina förändringar på strängen (ej visat här).  
3. **Save Options:** Konfigurera `SaveOptions` med önskat utdataformat.  
4. **Save Document:** Spara den redigerade filen tillbaka till disken.

## Hur arbetar man med olika dokumenttyper?
GroupDocs.Editor abstraherar Word-, Spreadsheet- och Presentation‑hantering bakom samma API‑yta, vilket gör det enkelt att byta kontext utan att lära sig en ny uppsättning klasser för varje dokumentfamilj.

### Redigera kalkylbladsdokument
`SpreadsheetSaveOptions` definierar hur ett kalkylblad skrivs, inklusive format och valfria komprimeringsinställningar.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/spreadsheet.xlsx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // Modify content here
        SaveOptions saveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsx);
        editor.Save(editableDocument, "path/to/save/spreadsheet.xlsx", saveOptions);
    }
}
```
```

**Förklaring:**  
1. **Initialize Editor:** Ange en kalkylbladsfilväg till `Editor`‑konstruktorn.  
2. **Edit Method:** Hämta ett `EditableDocument`.  
3. **Get Content:** Skriv ut kalkylbladets CSV‑representation (eller HTML).  
4. **Modify Content:** Gör eventuella cell‑nivå‑ändringar du behöver.  
5. **Save Options:** Välj lämpliga `SpreadsheetSaveOptions`.  
6. **Save Document:** Skriv tillbaka det uppdaterade kalkylbladet till lagring.

### Redigera presentationsdokument
`PresentationSaveOptions` styr utdataformatet för bildspelsfiler, vilket låter dig bevara eller ändra den ursprungliga filtypen.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/presentation.pptx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // Modify content here
        SaveOptions saveOptions = new PresentationSaveOptions(PresentationFormats.Pptx);
        editor.Save(editableDocument, "path/to/save/presentation.pptx", saveOptions);
    }
}
```
```

**Förklaring:**  
1. **Initialize Editor:** Ladda en PowerPoint‑fil via `Editor`.  
2. **Edit Method:** Hämta ett `EditableDocument`.  
3. **Get Content:** Extrahera slide‑HTML eller vanlig text.  
4. **Modify Content:** Uppdatera titlar, punktlistor eller bilder.  
5. **Save Options:** Använd `PresentationSaveOptions` för att definiera utdataformatet.  
6. **Save Document:** Spara den redigerade presentationen.

## Vanliga problem och lösningar
- **“Format not supported”‑fel:** Verifiera att du använder den senaste GroupDocs.Editor‑versionen; den lägger regelbundet till stöd för nyare Office‑format.  
- **Stort minnesförbrukning för stora filer:** Aktivera streaming‑läge genom att sätta `EditorSettings.EnableStreaming = true` innan dokumentet laddas.  
- **Licens ej tillämpad:** Säkerställ att den tillfälliga licensfilen ligger i applikationens rot eller laddas via `License license = new License(); license.SetLicense("path/to/license.lic");`.

## Vanliga frågor och svar

**Q: Vad är skillnaden mellan `DocumentFormatInfo` och `SaveOptions`?**  
A: `DocumentFormatInfo` ger metadata om stödda filtyper, medan `SaveOptions` konfigurerar hur ett dokument skrivs tillbaka till disk (format, komprimering osv.).

**Q: Kan jag lista format för en anpassad filändelse?**  
A: Ja — använd `DocumentFormatInfo.FromExtension("yourExt")`; om ändelsen inte känns igen returnerar metoden `null`.

**Q: Stöder GroupDocs.Editor lösenordsskyddade filer?**  
A: Absolut. Skicka lösenordet till `Editor`‑konstruktorn via `EditorSettings` för att öppna krypterade dokument.

**Q: Hur många format stödjer GroupDocs.Editor faktiskt?**  
A: Över **30 in- och utdataformat**, som täcker Word, Excel, PowerPoint, HTML och vanlig text.

**Q: Finns det ett sätt att begränsa listan till endast redigerbara format?**  
A: Använd `GetEditableWordProcessingFormats()` (eller motsvarande för Spreadsheet/Presentation) för att hämta format som tillåter full redigeringskapacitet.

## Ytterligare resurser
- Ladda ner biblioteket från den [GroupDocs releases‑sida](https://releases.groupdocs.com/editor/net/).  
- Skaffa en [tillfällig licens](https://purchase.groupdocs.com/temporary-license/) för full åtkomst till funktioner.  
- Prova produkten med en [gratis provversion](https://releases.groupdocs.com/).  
- Utforska detaljerade användningsexempel i [GroupDocs.Editor-dokumentationen](https://tutorials.groupdocs.com/editor/net/).  
- Få hjälp från communityn på [supportforumet](https://forum.groupdocs.com/c/editor/20).

## Slutsats
Genom att följa den här guiden vet du nu hur du **listar stödda dokumentformat**, **bestämmer ett filformat från dess filändelse** och **redigerar dokument** över Word, Spreadsheet och Presentation‑typer med GroupDocs.Editor för .NET. Integrera dessa kodsnuttar i dina egna projekt för att bygga robusta, format‑medvetna applikationer som glädjer slutanvändare och minskar körfel.

**Senast uppdaterad:** 2026-06-06  
**Testad med:** GroupDocs.Editor 23.9 för .NET  
**Författare:** GroupDocs

## Relaterade handledningar

- [Mästarhandledning för dokumentladdning i .NET med GroupDocs.Editor: En omfattande guide](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)
- [Mästarhandledning för dokumentredigering i .NET med GroupDocs.Editor: En omfattande guide](/editor/net/document-editing/master-document-editing-dotnet-groupdocs-editor/)
- [Konvertera Word till HTML med GroupDocs.Editor .NET: En steg‑för‑steg‑guide](/editor/net/document-saving/convert-word-to-html-groupdocs-editor-dotnet/)