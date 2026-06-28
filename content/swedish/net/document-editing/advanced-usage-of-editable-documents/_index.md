---
date: 2026-03-14
description: Lär dig hur du extraherar bilder från DOCX, konverterar DOCX till HTML
  och sparar dokumentet som HTML med GroupDocs.Editor för .NET.
linktitle: Extract Images from DOCX – Advanced Editable Document Usage
second_title: GroupDocs.Editor .NET API
title: Extrahera bilder från DOCX – Avancerad redigerbar dokumentanvändning
type: docs
url: /sv/net/document-editing/advanced-usage-of-editable-documents/
weight: 11
---

# Extrahera bilder från DOCX – Avancerad redigerbar dokumentanvändning

Om du är en .NET‑utvecklare som vill **extrahera bilder från DOCX** och förbättra dina dokumentredigeringsmöjligheter, erbjuder GroupDocs.Editor för .NET en kraftfull verktygssvit. Denna omfattande guide går igenom den avancerade användningen av redigerbara dokument med GroupDocs.Editor och bryter ner varje steg i detalj så att du kan utnyttja dess fulla potential.

## Snabba svar
- **Hur kan jag extrahera bilder från en DOCX‑fil?** Använd `EditableDocument.Images` efter att ha laddat dokumentet med `Editor`.
- **Kan jag konvertera DOCX till HTML med inbäddade resurser?** Ja—anropa `EditableDocument.GetEmbeddedHtml()` eller `GetContent()` för HTML‑markup.
- **Vilken metod sparar det redigerade dokumentet som HTML?** `EditableDocument.Save(htmlFilePath)` skapar en HTML‑fil med en resursmapp.
- **Är det möjligt att extrahera teckensnitt från ett Word‑dokument?** Använd `EditableDocument.Fonts` för att hämta alla teckensnittresurser.
- **Behöver jag en licens för produktionsanvändning?** En giltig GroupDocs.Editor‑licens krävs; en gratis provperiod finns tillgänglig.

## Vad är **extract images from docx**?
Att extrahera bilder från en DOCX‑fil innebär att programatiskt hämta varje bild som är inbäddad i Word‑dokumentet så att du kan återanvända, modifiera eller lagra dem separat. GroupDocs.Editor exponerar `Images`‑samlingen på en `EditableDocument`‑instans, vilket gör denna uppgift enkel.

## Varför använda GroupDocs.Editor för detta arbetsflöde?
- **Full kontroll** över dokumentresurser (bilder, teckensnitt, CSS) utan manuell ZIP‑hantering.  
- **Sömlös konvertering** från DOCX till HTML samtidigt som layout och stil bevaras.  
- **Enkel resursutvinning** för anpassad bildhantering, teckensnittsinbäddning eller CDN‑leverans.  
- **Robust avloppsmönster** säkerställer att inga minnesläckor uppstår i långvariga tjänster.

## Förutsättningar
- Visual Studio installerat på din utvecklingsmaskin.  
- .NET Framework kompatibel med GroupDocs.Editor.  
- GroupDocs.Editor för .NET‑biblioteket. Du kan [ladda ner det här](https://releases.groupdocs.com/editor/net/).  
- En giltig GroupDocs.Editor‑licens. Du kan få en [gratis provperiod](https://releases.groupdocs.com/) eller köpa en [tillfällig licens](https://purchase.groupdocs.com/temporary-license/).

## Importera namnrymder
För att börja, se till att du importerar de nödvändiga namnrymderna i ditt .NET‑projekt:

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

## Steg 1: Skapa en EditableDocument‑instans
Först måste du skapa en instans av `EditableDocument` genom att ladda och redigera ett inmatningsdokument i ett stödd format.

```csharp
string inputFilePath = "YourSampleDocument.docx";
Editor editor = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```

I detta steg laddar vi inmatningsdokumentet och förbereder det för redigering.

## Hur man **extract images from DOCX**?
Nedan dyker vi ner i resursextraktionsmöjligheterna, med början av det vanligaste behovet—att hämta alla bilder från en Word‑fil.

## Steg 2: Extrahera dokumentresurser
`EditableDocument` innehåller olika resurser som kan extraheras och manipuleras. Låt oss gå igenom dem:

### Steg 2.1: Extrahera hela dokumentet som HTML
Du kan generera en enda sträng som innehåller hela dokumentet med alla dess resurser inbäddade som HTML.

```csharp
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```

### Steg 2.2: Extrahera alla bilder *(primärt nyckelord i handling)*
```csharp
List<IImageResource> allImages = beforeEdit.Images;
```

### Steg 2.3: Extrahera alla teckensnitt *(sekundärt nyckelord)*
Om du också behöver **extrahera teckensnitt från Word**, använd följande anrop:

```csharp
List<FontResourceBase> allFonts = beforeEdit.Fonts;
```

### Steg 2.4: Extrahera alla stilmallar
Extrahera alla stilmallar i ett textformat.

```csharp
List<CssText> allStylesheets = beforeEdit.Css;
```

### Steg 2.5: Samla alla resurser
Samla alla resurser i ett anrop.

```csharp
List<IHtmlResource> allResources = beforeEdit.AllResources;
```

Detta inkluderar bilder, teckensnitt och stilmallar.

### Steg 2.6: Hämta HTML‑markup
Hämta HTML‑markupen för dokumentet utan inbäddade resurser.

```csharp
string htmlMarkup = beforeEdit.GetContent();
```

## Hur man **convert docx to html** med anpassad hantering?
Ibland behöver du justera externa länkar så att de pekar på dina egna resurs‑hanterare.

## Steg 3: Justera externa länkar
### Steg 3.1: Förbered anpassade prefix
Förbered prefix som kommer att läggas till före de ursprungliga externa länkarna.

```csharp
string customImagesRequesthandlerUri = "http://example.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://example.com/CssHandler/id=";
string customFontsRequesthandlerUri = "http://example.com/FontsHandler/id=";
```

### Steg 3.2: Generera HTML‑markup med prefix
Generera HTML‑markup med justerade länkar.

```csharp
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```

### Steg 3.3: Hämta endast kroppens HTML‑innehåll
Vissa WYSIWYG‑redigerare hanterar endast ren HTML‑markup utan huvuddelar.

```csharp
string onlyBodyContent = beforeEdit.GetBodyContent();
```

### Steg 3.4: Kropps‑endast innehåll med prefix
Generera endast kroppsinnehåll med anpassade bild‑prefix.

```csharp
string prefixedBodyContent = beforeEdit.GetBodyContent(customImagesRequesthandlerUri);
```

### Steg 3.5: Extrahera stilmallar
Extrahera stilmallar som används i dokumentet.

```csharp
List<string> stylesheets = beforeEdit.GetCssContent();
```

### Steg 3.6: Stilmallar med prefix
Extrahera stilmallar med anpassade prefix.

```csharp
List<string> prefixedStylesheets = beforeEdit.GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri);
```

## Hur man **save document as html** korrekt?
## Steg 4: Spara dokument som HTML
Spara det redigerade dokumentet som en HTML‑fil, inklusive dess resurser.

```csharp
string htmlFilePath = Path.Combine("output", Path.GetFileNameWithoutExtension(inputFilePath) + ".html");
beforeEdit.Save(htmlFilePath);
```

Denna metod skapar en separat katalog för resurser som stilmallar, bilder och teckensnitt.

## Steg 5: Avsluta EditableDocument
`EditableDocument` implementerar `IDisposable` och ger möjlighet att kontrollera om instansen har avslutats.

```csharp
Console.WriteLine("EditableDocument is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");
```

### Steg 5.1 Hantera Dispose‑händelse
Du kan också prenumerera på disposing‑händelsen.

```csharp
EventHandler someMethod = delegate { Console.WriteLine("Disposing event was spotted!"); };
beforeEdit.Disposed += someMethod;
```

## Steg 6: Skapa EditableDocument från HTML
Skapa en instans av `EditableDocument` från ett HTML‑dokument.

### Steg 6.1: Från HTML‑fil

```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
```

### Steg 6.2: Från HTML‑markup

```csharp
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);
```

Dessa instanser (`afterEditFromFile` och `afterEditFromMarkup`) är identiska med originalet (`beforeEdit`).

## Steg 7: Manuell avstängning
Avsluta manuellt dina `EditableDocument`‑instanser.

```csharp
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```

Detta säkerställer korrekt rensning av resurser.

## Vanliga problem och lösningar
- **Bilder visas inte efter extraktion:** Verifiera att dokumentet faktiskt innehåller inbäddade bilder och att du åtkommer `beforeEdit.Images` efter att ha anropat `Edit`.  
- **Teckensnitt saknas i HTML‑utdata:** Se till att du anropar `GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri)` för att korrekt bädda in teckensnittens URL:er.  
- **Stora HTML‑strängar orsakar minnesbelastning:** Använd `GetContent()` för markup utan inbäddade resurser och servera bilder/CSS från separata filer.

## Vanliga frågor

**Q: Vilka format stöder GroupDocs.Editor?**  
A: GroupDocs.Editor stöder DOCX, XLSX, PPTX och många andra populära kontorsformat.

**Q: Kan jag använda GroupDocs.Editor utan licens?**  
A: Ja, du kan använda det med en [gratis provperiod](https://releases.groupdocs.com/) eller en [tillfällig licens](https://purchase.groupdocs.com/temporary-license/).

**Q: Hur extraherar jag specifika resurser från ett dokument?**  
A: Använd `Images`, `Fonts` och `Css`‑samlingarna på `EditableDocument`‑instansen.

**Q: Är det möjligt att justera länkar i HTML‑utdata?**  
A: Ja, skicka anpassade URI‑prefix till `GetContent` eller `GetBodyContent` för att skriva om bild‑, CSS‑ och teckensnittslänkar.

**Q: Hur sparar jag ett redigerat dokument som en HTML‑fil?**  
A: Anropa `Save`‑metoden på `EditableDocument`‑instansen och ange en filsökväg som slutar med `.html`.

---

**Senast uppdaterad:** 2026-03-14  
**Testat med:** GroupDocs.Editor för .NET (senaste versionen)  
**Författare:** GroupDocs