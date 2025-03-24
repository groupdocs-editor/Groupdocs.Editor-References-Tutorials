---
title: Hämta HTML-innehåll med prefix
linktitle: Hämta HTML-innehåll med prefix
second_title: GroupDocs.Editor .NET API
description: Lär dig hur du hämtar HTML-innehåll från dokument med GroupDocs.Editor för .NET med anpassade prefix för bilder och stilmallar. Steg-för-steg-guide ingår.
weight: 11
url: /sv/net/html-content-retrieval/retrieve-html-content-with-prefix/
---

# Hämta HTML-innehåll med prefix

## Introduktion
Välkommen till vår steg-för-steg handledning om hur du hämtar HTML-innehåll från ett dokument med GroupDocs.Editor för .NET. Oavsett om du är en erfaren utvecklare eller precis har börjat, kommer den här guiden att leda dig genom processen på ett lätt att följa. Vi kommer att täcka allt du behöver veta, från att konfigurera din miljö till att köra koden framgångsrikt. Låt oss dyka in!
## Förutsättningar
Innan vi börjar, se till att du har följande förutsättningar på plats:
1.  GroupDocs.Editor för .NET: Ladda ner den senaste versionen från[nedladdningssida](https://releases.groupdocs.com/editor/net/).
2. Utvecklingsmiljö: Visual Studio eller någon annan föredragen .NET-utvecklingsmiljö.
3. Grundläggande kunskaper i C#: Bekantskap med C#-programmering hjälper dig att följa exemplen.
4. Dokument att redigera: Ha ett exempeldokument redo för testning, till exempel ett Word-dokument.
5. .NET Framework: Se till att du har .NET Framework installerat på din dator.
Nu när du har allt klart, låt oss börja!
## Importera namnområden
Först måste du importera de nödvändiga namnrymden i ditt C#-projekt. Dessa namnområden tillhandahåller de klasser och metoder som krävs för att arbeta med GroupDocs.Editor för .NET.
```csharp
using System;
using GroupDocs.Editor.Options;
```
Med namnrymden importerade kan vi gå vidare till att ställa in redigeraren.
## Steg 1: Initiera redigeraren
 För att börja måste du initiera`Editor`klass med ditt dokument. Det här steget innebär att du specificerar dokumentet du vill redigera och tillhandahåller nödvändiga laddningsalternativ.
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
    // Ytterligare steg kommer att läggas till här
}
```
 I det här exemplet laddar vi ett Word-dokument. Du kan byta ut`"Your Sample Document"` med sökvägen till ditt dokument.
## Steg 2: Redigera dokumentet
 Därefter måste vi öppna dokumentet för redigering. Detta görs med hjälp av`Edit` metod för`Editor` klass, vilket kräver`WordProcessingEditOptions` som ett argument.
```csharp
using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
{
    // Ytterligare steg kommer att läggas till här
}
```
 De`EditableDocument` instans representerar dokumentet i ett redigerbart format. Nu är vi redo att hämta HTML-innehållet.
## Steg 3: Definiera anpassade prefix
För att lägga till anpassade prefix för bilder och CSS måste vi definiera prefixen som strängar. Detta steg säkerställer att HTML-innehållet kommer att ha de angivna prefixen för externa resurser.
```csharp
string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
string externalCssPrefix = "http://www.minwebbplats.com/css/id=";
```
Du kan ersätta webbadresserna med dina önskade prefix. Dessa prefix kommer att användas i nästa steg för att anpassa HTML-utdata.
## Steg 4: Hämta HTML-innehåll
Nu när vi har våra prefix inställda kan vi hämta HTML-innehållet från dokumentet. De`GetContent` metod för`EditableDocument` klass tillåter oss att specificera bilden och CSS-prefix.
```csharp
string prefixedHtmlContent = document.GetContent(externalImagesPrefix, externalCssPrefix);
Console.WriteLine("HTML content of the input document with custom image and stylesheet prefixes: {0}", prefixedHtmlContent);
```
Det här kodavsnittet hämtar HTML-innehållet med de anpassade prefixen och skriver ut det till konsolen. Du kan vidarebearbeta eller spara detta HTML-innehåll efter behov.
## Slutsats
Och där har du det! Genom att följa dessa steg kan du enkelt hämta HTML-innehåll från ett dokument med GroupDocs.Editor för .NET, komplett med anpassade prefix för bilder och stilmallar. Det här kraftfulla verktyget förenklar dokumenthanteringen, så att du kan fokusera på att integrera dokumentredigering i dina .NET-applikationer sömlöst.
 För mer detaljerad information, kolla in[GroupDocs.Editor för .NET-dokumentation](https://tutorials.groupdocs.com/editor/net/) . Om du har några frågor eller behöver mer hjälp, hör gärna av dig på[supportforum](https://forum.groupdocs.com/c/editor/20).
## FAQ's
### Vilka typer av dokument kan jag redigera med GroupDocs.Editor för .NET?
GroupDocs.Editor stöder olika dokumentformat inklusive Word, Excel, PowerPoint, PDF och mer.
### Hur får jag en gratis provversion av GroupDocs.Editor för .NET?
 Du kan få en gratis provperiod från[GroupDocs webbplats](https://releases.groupdocs.com/).
### Kan jag anpassa HTML-innehållet ytterligare?
Ja, du kan ändra det hämtade HTML-innehållet efter behov innan du renderar eller sparar det.
### Är det möjligt att använda GroupDocs.Editor för .NET med andra .NET-språk?
Ja, du kan använda det med alla .NET-kompatibla språk som VB.NET eller F#.
### Hur får jag en tillfällig licens för GroupDocs.Editor för .NET?
 Du kan få en tillfällig licens från[köpsidan](https://purchase.groupdocs.com/temporary-license/).