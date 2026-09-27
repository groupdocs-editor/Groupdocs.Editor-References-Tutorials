---
date: 2026-09-26
description: Lär dig hur du hanterar CSS-prefix och extraherar CSS-innehåll med GroupDocs.Editor
  för .NET i den här detaljerade steg‑för‑steg‑handledningen.
keywords:
- handle css prefix
- extract css content
- edit document css
- prepend url to css
lastmod: 2026-09-26
linktitle: Hantera CSS-innehåll med prefix
og_description: Upptäck hur du hanterar CSS-prefix och extraherar CSS-innehåll med
  GroupDocs.Editor för .NET. Följ en steg‑för‑steg‑guide för att lägga till URL:er
  före CSS-resurser och hämta stilmallar.
og_image_alt: Developer guide showing css prefix handling with GroupDocs.Editor for
  .NET
og_title: Hur man hanterar CSS-prefix i GroupDocs.Editor för .NET
schemas:
- author: GroupDocs
  dateModified: '2026-09-26'
  description: Learn how to handle css prefix and extract css content using GroupDocs.Editor
    for .NET in this detailed step‑by‑step tutorial.
  headline: How to handle css prefix in GroupDocs.Editor for .NET
  type: TechArticle
- questions:
  - answer: Yes, GroupDocs.Editor for .NET supports PDF, Word, Excel, PowerPoint,
      and many other formats.
    question: Can I use GroupDocs.Editor for .NET with other document formats?
  - answer: Absolutely! You can start your free trial on the [GroupDocs free trial
      page](https://releases.groupdocs.com/).
    question: Is there a free trial available for GroupDocs.Editor for .NET?
  - answer: You can obtain a temporary license from the [temporary license page](https://purchase.groupdocs.com/temporary-license/).
    question: How do I get a temporary license for GroupDocs.Editor for .NET?
  - answer: Detailed documentation is available on the [GroupDocs.Editor for .NET
      documentation site](https://tutorials.groupdocs.com/editor/net/).
    question: Where can I find detailed documentation for GroupDocs.Editor for .NET?
  - answer: You can get support through the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).
    question: What support options are available for GroupDocs.Editor for .NET?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
tags:
- css handling
- GroupDocs.Editor
- .NET document processing
- css prefix
- api tutorial
title: Hur man hanterar CSS-prefix i GroupDocs.Editor för .NET
type: docs
url: /sv/net/css-handling/handle-css-content-with-prefix/
weight: 11
---

# Hur man hanterar css‑prefix i GroupDocs.Editor för .NET

I den här handledningen kommer du att lära dig **hur man hanterar css‑prefix** när du arbetar med stilmallar i ett dokument med GroupDocs.Editor för .NET. Oavsett om du behöver lägga till en URL före bilder, teckensnitt eller någon extern resurs, visar stegen nedan exakt hur du **hanterar css‑prefix** och även hur du **extraherar css‑innehåll** för vidare bearbetning. I slutet av guiden kommer du att kunna skriva om resursvägar, hämta de råa CSS‑strängarna och integrera dem i ditt webbflöde med förtroende.

## Snabba svar
- **Vad betyder “handle css prefix”?** Att lägga till ett anpassat URL‑prefix till externa resurser som refereras i CSS.  
- **Vilken API‑metod returnerar CSS‑stilar?** `EditableDocument.GetCssContent(...)`.  
- **Behöver jag en licens?** En provlicens finns tillgänglig; en kommersiell licens krävs för produktion.  
- **Vilka .NET‑versioner stöds?** .NET Framework 4.5+ och .NET Core/5/6.  
- **Kan jag ändra prefixet vid körning?** Ja – skicka helt enkelt en annan sträng till `GetCssContent`.

## Vad innebär hantera css‑prefix?
Begreppet avser att skriva om URL‑erna för bilder, teckensnitt eller någon extern tillgång i en CSS‑fil så att de pekar på en plats du kontrollerar, till exempel ett CDN eller en säker server. Genom att lägga till ett konsekvent bas‑URL garanterar du att varje resurs laddas korrekt när dokumentet renderas i en webbläsare eller en webbaserad visare.

## Varför använda GroupDocs.Editor för att extrahera css‑innehåll?
GroupDocs.Editor kan läsa den ursprungliga CSS som är inbäddad i Word‑processordokument, returnera de råa stilmallssträngarna och låta dig manipulera dem innan rendering eller sparning. Detta eliminerar manuell parsning, garanterar trohet mot dokumentets interna representation och stödjer **30+ filformat** samtidigt som filer upp till **500 MB** kan bearbetas utan att hela filen laddas in i minnet.

## Förutsättningar
- Visual Studio: Du behöver en fungerande installation av Visual Studio.  
- .NET Framework: Säkerställ att .NET Framework är installerat.  
- GroupDocs.Editor för .NET: Du kan ladda ner det från [GroupDocs.Editor for .NET download page](https://releases.groupdocs.com/editor/net/).  
- Exempeldokument: Ha ett exempeldokument redo för redigering.

## Importera namnrymder
Först importerar vi de nödvändiga namnrymderna för att säkerställa att vår kod körs smidigt. Detta steg ger oss åtkomst till GroupDocs.Editor:s kärnklasser.

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Editor.Options;
```

## Steg 1: Initiera redigeraren
`Editor`‑klassen är ingångspunkten för att arbeta med dokument i GroupDocs.Editor. Den hanterar laddning, redigering och sparningsoperationer.  
Det första steget innebär att skapa en `Editor`‑instans med ditt exempeldokument. Detta sätter upp redigeringsmiljön.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```

## Steg 2: Redigera dokumentet
`EditableDocument`‑objektet representerar den redigerbara versionen av filen och exponerar dess interna delar, såsom CSS, bilder och HTML.  
Nästa steg är att erhålla ett `EditableDocument`‑objekt. Detta objekt låter oss arbeta med dokumentets interna CSS.

```csharp
    using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
    {
```

## Steg 3: Ange externa prefix
Definiera URL‑prefixen för bilder och teckensnitt. Dessa prefix kommer att läggas till före varje bild‑ och teckensnittreferens som hittas i CSS‑filen.

```csharp
        string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
        string externalFontsPrefix = "http://www.mywebsite.com/fonts/id=";
```

## Steg 4: Extrahera css‑innehåll med prefixen
`GetCssContent` returnerar en samling av CSS‑stilmallssträngar som redan innehåller de prefix‑URL:er du angav.  
Anropa `GetCssContent` och skicka med de prefix du just definierade. Metoden returnerar en lista med CSS‑stilmallssträngar som redan innehåller de prefix‑URL:er.

```csharp
        List<string> stylesheets = document.GetCssContent(externalImagesPrefix, externalFontsPrefix);
```

## Steg 5: Skriv ut resultaten
Skriv ut antalet hittade stilmallar och visa varje stilmall. Detta hjälper dig verifiera att prefixen har tillämpats korrekt.

```csharp
        Console.WriteLine("There are {0} stylesheets in the input document", stylesheets.Count);
        foreach (string css in stylesheets)
        {
            Console.WriteLine(css);
        }
    }
}
```

## Vanliga problem och lösningar
- **Inga stilmallar returnerades** – Säkerställ att källdokumentet faktiskt innehåller CSS (t.ex. ett Word‑dokument med formaterade tabeller eller inbäddad HTML).  
- **Felaktiga URL‑er** – Dubbelkolla att prefixsträngarna avslutas med rätt avgränsare (`/` eller `=`) för din server‑routing.  
- **Prestandaproblem** – För mycket stora dokument, överväg att bearbeta stilmallar i batcher för att undvika hög minnesanvändning.

## Vanliga frågor

**Q: Kan jag använda GroupDocs.Editor för .NET med andra dokumentformat?**  
A: Ja, GroupDocs.Editor för .NET stödjer PDF, Word, Excel, PowerPoint och många andra format.

**Q: Finns det en gratis provperiod för GroupDocs.Editor för .NET?**  
A: Absolut! Du kan starta din gratis provperiod på [GroupDocs free trial page](https://releases.groupdocs.com/).

**Q: Hur får jag en tillfällig licens för GroupDocs.Editor för .NET?**  
A: Du kan skaffa en tillfällig licens från [temporary license page](https://purchase.groupdocs.com/temporary-license/).

**Q: Var kan jag hitta detaljerad dokumentation för GroupDocs.Editor för .NET?**  
A: Detaljerad dokumentation finns på [GroupDocs.Editor for .NET documentation site](https://tutorials.groupdocs.com/editor/net/).

**Q: Vilka supportalternativ finns för GroupDocs.Editor för .NET?**  
A: Du kan få support via [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).

## Ytterligare vanliga frågor

**Q: Kan jag ändra prefixet efter att ha extraherat CSS?**  
A: Ja. Anropa `GetCssContent` igen med en annan prefixsträng; metoden använder alltid de värden du skickar vid körning.

**Q: Fungerar detta med lösenordsskyddade dokument?**  
A: Ja. Ange lösenordet i `WordProcessingLoadOptions` när du skapar `Editor`‑instansen.

**Q: Är det möjligt att spara den modifierade CSS‑filen tillbaka i dokumentet?**  
A: GroupDocs.Editor erbjuder för närvarande endast skrivskyddad åtkomst till CSS. För att bestå förändringarna måste du ersätta den ursprungliga stilmallen via dokumentets underliggande XML‑API:er.

---

**Senast uppdaterad:** 2026-09-26  
**Testad med:** GroupDocs.Editor 23.12 för .NET  
**Författare:** GroupDocs

## Relaterade handledningar

- [Extrahera extern CSS från Word-dokument med GroupDocs.Editor .NET&#58; En omfattande guide](/editor/net/html-web-documents/extract-external-css-word-docs-groupdocs-editor-dotnet/)
- [Extrahera & prefixa HTML från Word-dokument med GroupDocs.Editor .NET](/editor/net/html-web-documents/groupdocs-editor-dotnet-extract-prefix-html-word-docs/)
- [Hur man extraherar och modifierar HTML-innehåll i Word-dokument med GroupDocs.Editor .NET](/editor/net/html-web-documents/extract-modify-html-content-word-docs-groupdocs-editor-net/)