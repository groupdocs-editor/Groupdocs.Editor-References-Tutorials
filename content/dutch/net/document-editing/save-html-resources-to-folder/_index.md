---
title: HTML-bronnen opslaan in map
linktitle: HTML-bronnen opslaan in map
second_title: GroupDocs.Editor .NET API
description: Leer hoe u HTML-bronnen uit documenten kunt extraheren met Groupdocs.Editor voor .NET. Deze uitgebreide tutorial biedt stapsgewijze begeleiding voor ontwikkelaars.
type: docs
weight: 13
url: /nl/net/document-editing/save-html-resources-to-folder/
---
## Invoering
Groupdocs.Editor voor .NET is een krachtige tool waarmee ontwikkelaars documenten binnen hun .NET-applicaties naadloos kunnen manipuleren en converteren. Of u nu HTML-bronnen uit een document moet halen of geavanceerde bewerkingstaken moet uitvoeren, Groupdocs.Editor vereenvoudigt het proces met zijn intuïtieve API en uitgebreide documentatie.
## Vereisten
Voordat u in de zelfstudie duikt, moet u ervoor zorgen dat u aan de volgende vereisten voldoet:
1. Basiskennis van C# en .NET: Bekendheid met de programmeertaal C# en het .NET-framework is essentieel om de voorbeelden te volgen.
2.  Groupdocs.Editor voor .NET-bibliotheek: Download en installeer Groupdocs.Editor voor .NET-bibliotheek vanaf de[website](https://releases.groupdocs.com/editor/net/).
3. Ontwikkelomgeving: Stel uw favoriete ontwikkelomgeving in, zoals Visual Studio of een andere compatibele IDE.

## Naamruimten importeren
Importeer om te beginnen de benodigde naamruimten in uw C#-project:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```
##Laten we nu het proces van het opslaan van HTML-bronnen in een map met Groupdocs.Editor voor .NET in meerdere stappen opsplitsen:
## Stap 1: Initialiseer Groupdocs.Editor
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
 Initialiseer eerst de`Editor`object door het pad naar uw voorbeelddocument op te geven. In dit voorbeeld gebruiken we een Word-document, dus specificeren we dit`WordProcessingLoadOptions` als documenttype.
## Stap 2: Document bewerken
```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
 Maak vervolgens een`EditableDocument` bezwaar maken door te bellen naar de`Edit` werkwijze van de`Editor` voorwerp. Hiermee kunt u bewerkingsbewerkingen op het document uitvoeren.
## Stap 3: Bronnen extraheren
```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
Extraheer bronnen zoals afbeeldingen, lettertypen en stylesheets uit het document en sla ze op in de respectievelijke lijsten.
## Stap 4: Geef de uitvoermap op
```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
Definieer de uitvoermap waar de uitgepakte bronnen worden opgeslagen. U kunt het mappad naar wens aanpassen.
## Stap 5: Bewaar bronnen
```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
Loop door elke afbeeldingsbron, sla deze op in de uitvoermap en geef relevante informatie weer, zoals bestandsnaam, type en afmetingen.
```csharp
		foreach (FontResourceBase oneFont in fonts)
		{
			Console.WriteLine("Saving {0} of {1} type",
				oneFont.FilenameWithExtension, oneFont.Type.FormalName);
			oneFont.Save(Path.Combine(outputFolder, oneFont.FilenameWithExtension));
		}
```
Op dezelfde manier slaat u elke lettertypebron op in de uitvoermap.
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
Sla ten slotte elk stylesheet op in de uitvoermap en voltooi het bewerkingsproces.

## Conclusie
Concluderend biedt Groupdocs.Editor voor .NET een handige oplossing voor het programmatisch beheren en manipuleren van documenten binnen .NET-applicaties. Door deze tutorial te volgen, kunt u eenvoudig HTML-bronnen uit documenten halen en het proces aanpassen aan uw specifieke vereisten.
## Veelgestelde vragen
### Is Groupdocs.Editor compatibel met andere documentformaten dan Word?
Ja, Groupdocs.Editor ondersteunt een breed scala aan documentformaten, waaronder Excel, PowerPoint, PDF en meer.
### Kan ik Groupdocs.Editor integreren in mijn webapplicatie?
Absoluut, Groupdocs.Editor biedt naadloze integratie met webapplicaties die zijn ontwikkeld op het .NET-framework.
### Biedt Groupdocs.Editor ondersteuning voor cloudopslagdiensten?
Ja, Groupdocs.Editor ondersteunt integratie met populaire cloudopslagdiensten zoals Google Drive, Dropbox en Microsoft OneDrive.
### Is er een gratis proefversie beschikbaar voor Groupdocs.Editor?
Ja, u kunt via de website profiteren van een gratis proefversie van Groupdocs.Editor.
### Hoe kan ik technische ondersteuning krijgen voor Groupdocs.Editor?
Voor technische assistentie en communityondersteuning kunt u het Groupdocs.Editor-forum bezoeken.