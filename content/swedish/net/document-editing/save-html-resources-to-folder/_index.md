---
date: 2026-05-12
description: Lär dig hur du extraherar teckensnitt och andra HTML-resurser från dokument
  med GroupDocs.Editor för .NET. Steg‑för‑steg‑guide för .NET‑utvecklare.
keywords:
- how to extract fonts
- GroupDocs.Editor .NET
- extract HTML resources
linktitle: Spara HTML-resurser till mapp
schemas:
- author: GroupDocs
  dateModified: '2026-05-12'
  description: Learn how to extract fonts and other HTML resources from documents
    using GroupDocs.Editor for .NET. Step‑by‑step guide for .NET developers.
  headline: How to Extract Fonts and Save HTML Resources to Folder
  type: TechArticle
- description: Learn how to extract fonts and other HTML resources from documents
    using GroupDocs.Editor for .NET. Step‑by‑step guide for .NET developers.
  name: How to Extract Fonts and Save HTML Resources to Folder
  steps:
  - name: '**Basic Knowledge of C# and .NET** – Familiarity with C# programming language
      and .NET framework is essential to follow along with the examples.'
    text: '**Basic Knowledge of C# and .NET** – Familiarity with C# programming language
      and .NET framework is essential to follow along with the examples.'
  - name: '**GroupDocs.Editor for .NET Library** – Download and install GroupDocs.Editor
      for .NET library from the [website](https://releases.groupdocs.com/editor/net/).'
    text: '**GroupDocs.Editor for .NET Library** – Download and install GroupDocs.Editor
      for .NET library from the [website](https://releases.groupdocs.com/editor/net/).'
  - name: '**Development Environment** – Set up your preferred development environment
      such as Visual Studio or any other compatible IDE.'
    text: '**Development Environment** – Set up your preferred development environment
      such as Visual Studio or any other compatible IDE.'
  type: HowTo
- questions:
  - answer: Yes, it supports Excel, PowerPoint, PDF, HTML, and over 50 additional
      formats for both editing and resource extraction.
    question: Is GroupDocs.Editor compatible with other document formats besides Word?
  - answer: Absolutely. The API works seamlessly with ASP.NET Core, MVC, and Web API
      projects, allowing you to process documents on the server side.
    question: Can I integrate GroupDocs.Editor into a web application?
  - answer: Yes, it includes built‑in connectors for Google Drive, Dropbox, OneDrive,
      and Amazon S3, enabling direct loading and saving of documents in the cloud.
    question: Does GroupDocs.Editor provide cloud storage integration?
  - answer: A fully functional 30‑day trial can be downloaded from the GroupDocs website
      without any credit‑card requirement.
    question: Is there a free trial available for GroupDocs.Editor?
  - answer: You can reach the GroupDocs support team via the official forum, submit
      a ticket through the customer portal, or consult the detailed API documentation.
    question: How can I get technical support for extraction issues?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Hur man extraherar teckensnitt och sparar HTML-resurser till en mapp
type: docs
url: /sv/net/document-editing/save-html-resources-to-folder/
weight: 13
---

# Hur man extraherar teckensnitt och sparar HTML-resurser i en mapp

## Introduktion
GroupDocs.Editor för .NET låter dig **hur man extraherar teckensnitt** och andra resurser från ett dokument medan det konverteras till HTML. På några rader C# kan du hämta bilder, stilmallar och teckensnittsfiler och sedan lagra dem i en mapp du väljer. Denna handledning guidar dig genom hela arbetsflödet, från att initiera editorn till att spara varje resurs på disk.

## Snabba svar
- **Vad betyder “how to extract fonts”?** Det är processen att hämta inbäddade teckensnittsfiler från ett källdokument under HTML-konvertering.  
- **Vilket bibliotek hanterar detta?** GroupDocs.Editor för .NET tillhandahåller ett dedikerat API för att extrahera teckensnitt, bilder och stilmallar.  
- **Behöver jag en licens?** En gratis provversion finns tillgänglig; en kommersiell licens krävs för produktionsanvändning.  
- **Vilka .NET-versioner stöds?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.  
- **Kan jag rikta in mig på en anpassad mapp?** Ja, du anger någon skrivbar sökväg när du sparar de extraherade resurserna.

## Vad är “how to extract fonts”?
**Hur man extraherar teckensnitt** avser att hämta de ursprungliga teckensnittsfilerna som är inbäddade i ett källdokument (t.ex. DOCX, PPTX) så att de kan refereras av den genererade HTML‑koden. Detta säkerställer att text visas exakt som avsett i webbläsare utan att förlita sig på systemteckensnitt.

## Varför använda GroupDocs.Editor för extrahering av HTML-resurser?
GroupDocs.Editor stöder **50+ in- och utdataformat** — inklusive DOCX, PPTX, PDF och HTML — och kan bearbeta dokument med **upp till 300 sidor** utan att ladda hela filen i minnet. Dess API extraherar teckensnitt, bilder och CSS i ett enda pass, vilket minskar utvecklingstiden med upp till **70 %** jämfört med manuell parsning.

## Förutsättningar
1. **Grundläggande kunskap om C# och .NET** – Bekantskap med programmeringsspråket C# och .NET‑ramverket är nödvändig för att följa med i exemplen.  
2. **GroupDocs.Editor för .NET‑bibliotek** – Ladda ner och installera GroupDocs.Editor för .NET‑biblioteket från [webbplatsen](https://releases.groupdocs.com/editor/net/).  
3. **Utvecklingsmiljö** – Ställ in din föredragna utvecklingsmiljö, såsom Visual Studio eller någon annan kompatibel IDE.

## Importera namnrymder
To get started, import the necessary namespaces in your C# project:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```

## Hur man extraherar teckensnitt och sparar HTML-resurser i en mapp?
Läs in ditt källdokument med `Editor editor = new Editor("sample.docx", new WordProcessingLoadOptions());` och anropa sedan `editor.Save("output.html", SaveOptions.Html);`. Efter sparningsoperationen innehåller `Resources`‑samlingen alla extraherade tillgångar — inklusive teckensnitt — som du kan iterera över och skriva till disk. Detta enstegstillvägagångssätt hanterar både konvertering och resursutvinning automatiskt.

## Steg 1: Initiera GroupDocs.Editor
`Editor` är kärnklassen som orkestrerar dokumentladdning, konvertering och resursutvinning. Den representerar en enskild dokumentsession i minnet.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
Först initierar du `Editor`‑objektet genom att ange sökvägen till ditt exempel‑dokument. I detta exempel använder vi ett Word‑dokument, så vi specificerar `WordProcessingLoadOptions` som dokumenttyp.

## Steg 2: Redigera dokument
`EditableDocument` är den redigerbara representationen som returneras av `Edit`‑metoden, vilket låter dig manipulera dokumentet innan det sparas.

```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
Därefter skapar du ett `EditableDocument`‑objekt genom att anropa `Edit`‑metoden på `Editor`‑objektet. Detta gör att du kan utföra redigeringsoperationer på dokumentet.

## Steg 3: Extrahera resurser
`Resources` är en samling som grupperar extraherade tillgångar — bilder, teckensnitt och stilmallar — i separata listor för enkel hantering.

```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
Extrahera resurser såsom bilder, teckensnitt och stilmallar från dokumentet och lagra dem i respektive listor.

## Steg 4: Ange utdatamapp
`outputFolder` är en sträng som definierar var de extraherade filerna ska skrivas. Du kan peka den på någon skrivbar katalog på servern eller den lokala maskinen.

```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
Definiera utdatamappen där de extraherade resurserna kommer att sparas. Du kan anpassa sökvägen efter dina behov.

## Steg 5: Spara resurser
`SaveResource` är en hjälprutin som skriver en enskild binär resurs (bild, teckensnitt eller stilmall) till filsystemet.

```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
Loopa igenom varje bildresurs, spara den i utdatamappen och visa relevant information såsom filnamn, typ och dimensioner.

```csharp
		foreach (FontResourceBase oneFont in fonts)
		{
			Console.WriteLine("Saving {0} of {1} type",
				oneFont.FilenameWithExtension, oneFont.Type.FormalName);
			oneFont.Save(Path.Combine(outputFolder, oneFont.FilenameWithExtension));
		}
```
På samma sätt sparas varje teckensnittresurs i utdatamappen.

```csharp
		foreach (CssText oneStylesheet in stylesheets)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} encoding",
				oneStylesheet.FilenameWithExtension, oneStylesheet.Type.FormalName, oneStylesheet.Encoding);
			oneStylesheet.Save(Path.Combine(outputFolder, oneStylesheet.FilenameWithExtension));
		}
	}
}
```
Till sist sparas varje stilmall i utdatamappen och redigeringsprocessen avslutas.

## Vanliga problem och lösningar
- **Saknade teckensnitt efter konvertering** – Säkerställ att källdokumentet faktiskt bäddar in teckensnitten; annars kan GroupDocs.Editor bara referera till systemteckensnitt.  
- **Åtkomst nekad‑fel** – Verifiera att applikationsprocessen har skrivbehörighet till den valda utdatamappen.  
- **Stora dokument orsakar hög minnesanvändning** – Använd `LoadOptions` med `LoadMode = LoadMode.Stream` för att strömma stora filer istället för att ladda dem helt i minnet.

## Vanliga frågor

**Q: Är GroupDocs.Editor kompatibel med andra dokumentformat förutom Word?**  
A: Ja, den stöder Excel, PowerPoint, PDF, HTML och över 50 ytterligare format för både redigering och resursutvinning.

**Q: Kan jag integrera GroupDocs.Editor i en webbapplikation?**  
A: Absolut. API:et fungerar sömlöst med ASP.NET Core, MVC och Web API‑projekt, vilket låter dig bearbeta dokument på serversidan.

**Q: Erbjuder GroupDocs.Editor integration med molnlagring?**  
A: Ja, den inkluderar inbyggda anslutningar för Google Drive, Dropbox, OneDrive och Amazon S3, vilket möjliggör direkt laddning och sparande av dokument i molnet.

**Q: Finns det en gratis provversion av GroupDocs.Editor?**  
A: En fullt funktionell 30‑dagars provversion kan laddas ner från GroupDocs‑webbplatsen utan krav på kreditkort.

**Q: Hur kan jag få teknisk support för extraheringsproblem?**  
A: Du kan nå GroupDocs supportteam via det officiella forumet, skicka in ett ärende via kundportalen eller konsultera den detaljerade API‑dokumentationen.

---

**Senast uppdaterad:** 2026-05-12  
**Testat med:** GroupDocs.Editor 23.11 for .NET  
**Författare:** GroupDocs

## Relaterade handledningar

- [Effektiv dokumentredigering med GroupDocs.Editor .NET: Omvandla HTML till redigerbara dokument](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)
- [Effektiv extrahering och sparande av DOCX-resurser med GroupDocs.Editor .NET – Komplett guide](/editor/net/document-saving/efficient-extract-save-docx-resources-groupdocs-editor-net/)
- [Mästra dokumentredigering och konvertering med GroupDocs.Editor .NET: En komplett guide](/editor/net/document-editing/groupdocs-editor-net-mastering-document-editing/)