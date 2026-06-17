---
date: 2026-03-06
description: Lär dig hur du hanterar CSS‑innehåll med prefix och extraherar CSS‑innehåll
  med GroupDocs.Editor för .NET i den här detaljerade steg‑för‑steg‑handledningen.
linktitle: Handle CSS Content with Prefix
second_title: GroupDocs.Editor .NET API
title: Hantera CSS‑innehåll med prefix
type: docs
url: /sv/net/css-handling/handle-css-content-with-prefix/
weight: 11
---

# Hantera CSS-innehåll med prefix

I den här handledningen kommer du att upptäcka **hur man hanterar css prefix** när du arbetar med stilmallar i ett dokument med GroupDocs.Editor för .NET. Oavsett om du behöver lägga till en URL före bilder, teckensnitt eller någon extern resurs, visar stegen nedan exakt hur du **hanterar css prefix** och även hur du **extraherar css-innehåll** för vidare bearbetning.

## Snabba svar
- **Vad betyder “handle css prefix”?** Att lägga till ett anpassat URL-prefix till externa resurser som refereras i CSS.
- **Vilken API‑metod returnerar CSS‑stilar?** `EditableDocument.GetCssContent(...)`.
- **Behöver jag en licens?** En provlicens är tillgänglig; en kommersiell licens krävs för produktion.
- **Vilka .NET‑versioner stöds?** .NET Framework 4.5+ och .NET Core/5/6.
- **Kan jag ändra prefixet vid körning?** Ja – skicka bara en annan sträng till `GetCssContent`.

## Vad är **handle css prefix**?
Att applicera ett prefix på CSS‑resurser omskriver sökvägarna för bilder, teckensnitt eller andra tillgångar så att de pekar på en plats du kontrollerar (t.ex. ett CDN eller en säker server). Detta är särskilt användbart när du exporterar ett dokument och behöver att alla externa referenser ska vara åtkomliga från en webbapplikation.

## Varför använda GroupDocs.Editor för att **extrahera css-innehåll**?
GroupDocs.Editor kan läsa den ursprungliga CSS som är inbäddad i WordProcessing‑dokument, ge dig de råa stilbladssträngarna och låta dig manipulera dem innan rendering eller sparning. Detta eliminerar behovet av manuell parsning och garanterar att den extraherade CSS‑en matchar dokumentets interna representation.

## Förutsättningar
Innan vi börjar, se till att du har följande förutsättningar på plats:
- Visual Studio: Du behöver en fungerande installation av Visual Studio.  
- .NET Framework: Se till att du har .NET Framework installerat.  
- GroupDocs.Editor för .NET: Du kan ladda ner det [här](https://releases.groupdocs.com/editor/net/).  
- Exempeldokument: Ha ett exempeldokument redo för redigering.

## Importera namnrymder
Först, låt oss importera de nödvändiga namnrymderna för att säkerställa att vår kod körs smidigt. Detta steg ger oss åtkomst till de centrala klasserna i GroupDocs.Editor.

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Editor.Options;
```

## Steg 1: Initiera editorn
Det första steget innebär att skapa en `Editor`‑instans med ditt exempeldokument. Detta sätter upp redigeringsmiljön.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```

## Steg 2: Redigera dokumentet
Därefter får vi ett `EditableDocument`‑objekt. Detta objekt representerar den redigerbara versionen av filen och låter oss arbeta med dess interna delar.

```csharp
    using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
    {
```

## Steg 3: Ställ in externa prefix
Definiera URL‑prefixen för bilder och teckensnitt. Dessa prefix kommer att läggas till före varje bild‑ och teckensnittreferens som hittas i CSS.

```csharp
        string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
        string externalFontsPrefix = "http://www.mywebsite.com/fonts/id=";
```

## Steg 4: **Extrahera CSS-innehåll** med prefixen
Anropa `GetCssContent` och skicka de prefix du just definierade. Metoden returnerar en lista med CSS‑stilbladssträngar som redan innehåller de prefixade URL‑erna.

```csharp
        List<string> stylesheets = document.GetCssContent(externalImagesPrefix, externalFontsPrefix);
```

## Steg 5: Skriv ut resultaten
Skriv ut antalet stilblad som hittades och visa varje stilblad. Detta hjälper dig att verifiera att prefixen har tillämpats korrekt.

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
- **Inga stilblad returnerades** – Se till att källdokumentet faktiskt innehåller CSS (t.ex. ett Word‑dokument med formaterade tabeller eller inbäddad HTML).  
- **Felaktiga URL‑er** – Dubbelkolla att prefixsträngarna avslutas med rätt avgränsare (`/` eller `=`) för din server‑routing.  
- **Prestandaproblem** – För mycket stora dokument, överväg att bearbeta stilblad i batchar för att undvika hög minnesanvändning.

## Slutsats
Att hantera CSS‑innehåll med ett prefix med GroupDocs.Editor för .NET är enkelt och kraftfullt. Genom att följa dessa steg kan du **hantera css prefix**, hämta den råa CSS‑en via **extrahera css-innehåll**, och sömlöst integrera externa resurser i ditt webbflöde. Utforska andra GroupDocs.Editor‑funktioner såsom HTML‑konvertering, bildextraktion och dokumentsammanfogning för att få ännu mer värde ur API‑et.

## Vanliga frågor
### Kan jag använda GroupDocs.Editor för .NET med andra dokumentformat?
Ja, GroupDocs.Editor för .NET stöder olika dokumentformat inklusive PDF, Word, Excel och mer.

### Finns det en gratis provperiod för GroupDocs.Editor för .NET?
Absolut! Du kan starta din gratis provperiod [här](https://releases.groupdocs.com/).

### Hur får jag en tillfällig licens för GroupDocs.Editor för .NET?
Du kan skaffa en tillfällig licens [här](https://purchase.groupdocs.com/temporary-license/).

### Var kan jag hitta detaljerad dokumentation för GroupDocs.Editor för .NET?
Detaljerad dokumentation finns tillgänglig [här](https://tutorials.groupdocs.com/editor/net/).

### Vilka supportalternativ finns tillgängliga för GroupDocs.Editor för .NET?
Du kan få support [här](https://forum.groupdocs.com/c/editor/20).

## Ytterligare vanliga frågor

**Q: Kan jag ändra prefixet efter att ha extraherat CSS?**  
A: Ja. Anropa `GetCssContent` igen med en annan prefixsträng; metoden använder alltid de värden du skickar vid körning.

**Q: Fungerar detta med lösenordsskyddade dokument?**  
A: Ja. Ange lösenordet i `WordProcessingLoadOptions` när du skapar `Editor`‑instansen.

**Q: Är det möjligt att spara den modifierade CSS‑en tillbaka i dokumentet?**  
A: GroupDocs.Editor erbjuder för närvarande endast läsåtkomst till CSS. För att bevara ändringarna måste du ersätta den ursprungliga stilbladet med hjälp av dokumentets underliggande XML‑API:er.

---

**Senast uppdaterad:** 2026-03-06  
**Testad med:** GroupDocs.Editor 23.12 för .NET  
**Författare:** GroupDocs