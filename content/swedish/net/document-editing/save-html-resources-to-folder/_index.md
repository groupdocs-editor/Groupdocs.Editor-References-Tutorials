---
title: Spara HTML-resurser till mapp
linktitle: Spara HTML-resurser till mapp
second_title: GroupDocs.Editor .NET API
description: Lär dig hur du extraherar HTML-resurser från dokument med Groupdocs.Editor för .NET. Denna omfattande handledning ger steg-för-steg-vägledning för utvecklare.
weight: 13
url: /sv/net/document-editing/save-html-resources-to-folder/
---
## Introduktion
Groupdocs.Editor för .NET är ett kraftfullt verktyg som gör det möjligt för utvecklare att manipulera och konvertera dokument i sina .NET-applikationer sömlöst. Oavsett om du behöver extrahera HTML-resurser från ett dokument eller utföra avancerade redigeringsuppgifter, förenklar Groupdocs.Editor processen med sitt intuitiva API och omfattande dokumentation.
## Förutsättningar
Innan du dyker in i handledningen, se till att du har följande förutsättningar:
1. Grundläggande kunskaper om C# och .NET: Bekantskap med programmeringsspråket C# och .NET framework är viktigt att följa med i exemplen.
2.  Groupdocs.Editor for .NET Library: Ladda ner och installera Groupdocs.Editor for .NET-biblioteket från[hemsida](https://releases.groupdocs.com/editor/net/).
3. Utvecklingsmiljö: Konfigurera din föredragna utvecklingsmiljö som Visual Studio eller någon annan kompatibel IDE.

## Importera namnområden
För att komma igång, importera de nödvändiga namnrymden i ditt C#-projekt:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```
##Låt oss nu dela upp processen att spara HTML-resurser i en mapp med Groupdocs.Editor för .NET i flera steg:
## Steg 1: Initiera Groupdocs.Editor
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
 Initiera först`Editor`objekt genom att ange sökvägen till ditt exempeldokument. I det här exemplet använder vi ett Word-dokument, så vi specificerar`WordProcessingLoadOptions` som dokumenttyp.
## Steg 2: Redigera dokument
```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
 Skapa sedan en`EditableDocument` objekt genom att anropa`Edit` metod för`Editor` objekt. Detta gör att du kan utföra redigeringsåtgärder på dokumentet.
## Steg 3: Extrahera resurser
```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
Extrahera resurser som bilder, typsnitt och stilmallar från dokumentet och lagra dem i respektive listor.
## Steg 4: Ange utdatamapp
```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
Definiera utdatamappen där de extraherade resurserna ska sparas. Du kan anpassa mappsökvägen enligt dina krav.
## Steg 5: Spara resurser
```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
Gå igenom varje bildresurs, spara den i utdatamappen och visa relevant information som filnamn, typ och mått.
```csharp
		foreach (FontResourceBase oneFont in fonts)
		{
			Console.WriteLine("Saving {0} of {1} type",
				oneFont.FilenameWithExtension, oneFont.Type.FormalName);
			oneFont.Save(Path.Combine(outputFolder, oneFont.FilenameWithExtension));
		}
```
På samma sätt sparar du varje teckensnittsresurs i utdatamappen.
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
Slutligen, spara varje stilmall i utdatamappen och slutför redigeringsprocessen.

## Slutsats
Sammanfattningsvis erbjuder Groupdocs.Editor för .NET en bekväm lösning för att hantera och manipulera dokument programmatiskt i .NET-applikationer. Genom att följa denna handledning kan du enkelt extrahera HTML-resurser från dokument och anpassa processen efter dina specifika krav.
## FAQ's
### Är Groupdocs.Editor kompatibel med andra dokumentformat än Word?
Ja, Groupdocs.Editor stöder ett brett utbud av dokumentformat inklusive Excel, PowerPoint, PDF och mer.
### Kan jag integrera Groupdocs.Editor i min webbapplikation?
Absolut, Groupdocs.Editor erbjuder sömlös integration med webbapplikationer utvecklade på .NET-ramverket.
### Ger Groupdocs.Editor stöd för molnlagringstjänster?
Ja, Groupdocs.Editor stöder integration med populära molnlagringstjänster som Google Drive, Dropbox och Microsoft OneDrive.
### Finns det en gratis testversion tillgänglig för Groupdocs.Editor?
Ja, du kan använda en gratis provversion av Groupdocs.Editor från webbplatsen.
### Hur kan jag få teknisk support för Groupdocs.Editor?
För teknisk assistans och communitysupport kan du besöka Groupdocs.Editor-forumet.