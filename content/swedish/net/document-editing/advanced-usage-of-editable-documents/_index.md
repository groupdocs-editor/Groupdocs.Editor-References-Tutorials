---
title: Avancerad användning av redigerbara dokument
linktitle: Avancerad användning av redigerbara dokument
second_title: GroupDocs.Editor .NET API
description: Lär dig avancerad användning av GroupDocs.Editor för .NET skapa, redigera och extrahera resurser från dokument programmatiskt.
type: docs
weight: 11
url: /sv/net/document-editing/advanced-usage-of-editable-documents/
---
## Introduktion
Om du är en .NET-utvecklare som vill förbättra dina dokumentredigeringsmöjligheter, erbjuder GroupDocs.Editor för .NET en kraftfull uppsättning verktyg. Den här omfattande guiden leder dig genom den avancerade användningen av redigerbara dokument med GroupDocs.Editor, och delar ner varje steg i detalj för att säkerställa att du kan utnyttja dess fulla potential.
## Förutsättningar
Innan du dyker in i de avancerade funktionerna, se till att du har följande:
- Visual Studio installerat på din utvecklingsmaskin.
- .NET Framework kompatibelt med GroupDocs.Editor.
-  GroupDocs.Editor för .NET-bibliotek. Du kan[ladda ner den här](https://releases.groupdocs.com/editor/net/).
-  En giltig GroupDocs.Editor-licens. Du kan få en[gratis provperiod](https://releases.groupdocs.com/) eller köp en[tillfällig licens](https://purchase.groupdocs.com/temporary-license/).
## Importera namnområden
För att börja, se till att du importerar de nödvändiga namnrymden i ditt .NET-projekt:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```
## Steg 1: Skapa en EditableDocument-instans
 Först måste du skapa en instans av`EditableDocument` genom att ladda och redigera ett inmatningsdokument i ett format som stöds.
```csharp
string inputFilePath = "YourSampleDocument.docx";
Editor editor = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```
I det här steget laddar vi inmatningsdokumentet och förbereder det för redigering.
## Steg 2: Extrahera dokumentresurser
 De`EditableDocument` innehåller olika resurser som kan utvinnas och manipuleras. Låt oss dela upp dessa:
### Steg 2.1: Extrahera hela dokumentet som HTML
Du kan skapa en enda sträng som innehåller hela dokumentet med alla dess resurser inbäddade som HTML.
```csharp
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```
Den här strängen kommer att vara ganska stor eftersom den innehåller stilmallar, bilder och teckensnitt kodade i base64.
### Steg 2.2: Extrahera alla bilder
Extrahera alla bilder från dokumentet.
```csharp
List<IImageResource> allImages = beforeEdit.Images;
```
### Steg 2.3: Extrahera alla teckensnitt
Extrahera alla teckensnitt som används i dokumentet.
```csharp
List<FontResourceBase> allFonts = beforeEdit.Fonts;
```
### Steg 2.4: Extrahera alla stilmallar
Extrahera alla stilmallar i ett textformat.
```csharp
List<CssText> allStylesheets = beforeEdit.Css;
```
### Steg 2.5: Samla alla resurser
Samla alla resurser i ett samtal.
```csharp
List<IHtmlResource> allResources = beforeEdit.AllResources;
```
Detta inkluderar bilder, typsnitt och stilmallar.
### Steg 2.6: Skaffa HTML-uppmärkning
Få HTML-uppmärkningen av dokumentet utan inbäddade resurser.
```csharp
string htmlMarkup = beforeEdit.GetContent();
```
## Steg 3: Justera externa länkar
Ibland måste du justera externa länkar för att peka på en anpassad resurshanterare. Så här gör du:
### Steg 3.1: Förbered anpassade prefix
Förbered prefix som kommer att lägga till ursprungliga externa länkar.
```csharp
string customImagesRequesthandlerUri = "http://example.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://exempel.com/CssHandler/id=";
string customFontsRequesthandlerUri = "http://example.com/FontsHandler/id=";
```
### Steg 3.2: Skapa HTML-kod med prefix
Generera HTML-uppmärkning med anpassade länkar.
```csharp
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```
### Steg 3.3: Skaffa HTML-innehåll endast för kroppen
Vissa WYSIWYG-redigerare hanterar bara ren HTML-uppmärkning utan rubriker.
```csharp
string onlyBodyContent = beforeEdit.GetBodyContent();
```
### Steg 3.4: Innehåll endast för brödtext
Generera innehåll endast för kropp med anpassade bildprefix.
```csharp
string prefixedBodyContent = beforeEdit.GetBodyContent(customImagesRequesthandlerUri);
```
### Steg 3.5: Extrahera stilmallar
Extrahera stilmallar som används i dokumentet.
```csharp
List<string> stylesheets = beforeEdit.GetCssContent();
```
### Steg 3.6: Prefixerade formatmallar
Extrahera stilmallar med anpassade prefix.
```csharp
List<string> prefixedStylesheets = beforeEdit.GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri);
```
## Steg 4: Spara dokument som HTML
Spara det redigerade dokumentet som en HTML-fil, inklusive dess resurser.
```csharp
string htmlFilePath = Path.Combine("output", Path.GetFileNameWithoutExtension(inputFilePath) + ".html");
beforeEdit.Save(htmlFilePath);
```
Den här metoden skapar en separat katalog för resurser som stilmallar, bilder och typsnitt.
## Steg 5: Kasta EditableDocument
 EditableDocument implementerar`IDisposable` och ger möjlighet att kontrollera om instansen är bortskaffad.
```csharp
Console.WriteLine("EditableDocument is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");
```
### Steg 5.1 Hantering av kasseringshändelse
Du kan också prenumerera på avyttringsevenemanget.
```csharp
EventHandler someMethod = delegate { Console.WriteLine("Disposing event was spotted!"); };
beforeEdit.Disposed += someMethod;
```
## Steg 6: Skapa EditableDocument från HTML
Skapa en instans av EditableDocument från ett HTML-dokument.
### Steg 6.1: Från HTML-fil
```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
```
### Steg 6.2: Från HTML Markup
```csharp
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);
```
Dessa instanser (afterEditFromFile och afterEditFromMarkup) är identiska med originalet (beforeEdit).
## Steg 7: Manuell kassering
Kassera dina EditableDocument-instanser manuellt.
```csharp
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```
Detta säkerställer korrekt sanering av resurser.
## Slutsats
GroupDocs.Editor för .NET tillhandahåller robusta verktyg för att redigera dokument programmatiskt. Genom att följa denna steg-för-steg-guide kan du effektivt hantera dokumentinnehåll, resurser och utdataformat. Oavsett om du bäddar in resurser, justerar externa länkar eller konverterar dokument till HTML, utrustar GroupDocs.Editor dig med den funktionalitet som behövs för avancerad dokumenthantering.
## FAQ's
### Vilka format stöder GroupDocs.Editor?
GroupDocs.Editor stöder olika format inklusive DOCX, XLSX, PPTX och mer.
### Kan jag använda GroupDocs.Editor utan licens?
 Ja, du kan använda den med en[gratis provperiod](https://releases.groupdocs.com/) eller a[tillfällig licens](https://purchase.groupdocs.com/temporary-license/).
### Hur extraherar jag specifika resurser från ett dokument?
 Du kan extrahera bilder, typsnitt och stilmallar med hjälp av de medföljande metoderna som`Images`, `Fonts` , och`Css`.
### Är det möjligt att justera länkar i HTML-utdata?
Ja, du kan justera externa länkar genom att ange anpassade prefix för bilder, CSS och teckensnitt.
### Hur sparar jag ett redigerat dokument som en HTML-fil?
 Använd`Save` metod för`EditableDocument`klass för att spara dokumentet som en HTML-fil, inklusive dess resurser.