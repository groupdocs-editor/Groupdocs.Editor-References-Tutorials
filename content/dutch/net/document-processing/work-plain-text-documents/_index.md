---
title: Werken met platte tekstdocumenten
linktitle: Werken met platte tekstdocumenten
second_title: GroupDocs.Editor .NET API
description: Leer hoe u platte-tekstdocumenten kunt bewerken met GroupDocs.Editor voor .NET met onze stapsgewijze handleiding. Vereenvoudig uw .NET-documentbewerkingsproces.
weight: 15
url: /nl/net/document-processing/work-plain-text-documents/
---
## Invoering
Wilt u uw documentbewerkingsproces in .NET stroomlijnen? Zoek niet verder dan GroupDocs.Editor voor .NET! Met deze krachtige API kunt u eenvoudig een grote verscheidenheid aan documentformaten bewerken. In deze zelfstudie begeleiden we u bij het werken met platte-tekstdocumenten met GroupDocs.Editor voor .NET. Tegen het einde zul je in staat zijn om als een professional met het bewerken van tekstdocumenten om te gaan. Klaar om erin te duiken? Laten we beginnen!
## Vereisten
Voordat we beginnen, zijn er een paar dingen die u moet regelen:
- .NET-ontwikkelomgeving: Zorg ervoor dat u een werkende .NET-ontwikkelomgeving hebt ingesteld. Visual Studio is een populaire keuze.
-  GroupDocs.Editor voor .NET: Download en installeer het[GroupDocs.Editor voor .NET](https://releases.groupdocs.com/editor/net/).
- Basiskennis van C#: Bekendheid met de programmeertaal C# helpt u de voorbeelden te volgen.
- Teksteditor: elke teksteditor is geschikt, hoewel Visual Studio Code wordt aanbevolen vanwege de functies en het gebruiksgemak.
## Naamruimten importeren
Om GroupDocs.Editor voor .NET te gaan gebruiken, moet u de benodigde naamruimten in uw project importeren. Dit zorgt ervoor dat alle vereiste klassen en methoden beschikbaar zijn voor gebruik.
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```
Laten we het proces opsplitsen in beheersbare stappen. Volg ons terwijl we u door elke fase begeleiden van het bewerken van platte-tekstdocumenten met GroupDocs.Editor voor .NET.
## Stap 1: verkrijg een pad naar het invoer-TXT-bestand
Eerst moet u het pad naar het invoer-TXT-bestand opgeven. Dit kan een pad zijn naar een lokaal bestand of een stream die de bestandsinhoud bevat.
```csharp
string inputFilePath = "YourSampleDocument.txt";
```
## Stap 2: Maak een Editor-instantie
 Maak vervolgens een exemplaar van de`Editor` klas. Deze klasse is verantwoordelijk voor het laden en bewerken van documenten. In dit stadium zijn er geen laadopties vereist.
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## Stap 3: Maak TXT-bewerkingsopties
Maak nu de TXT-bewerkingsopties. Met deze opties kunt u opgeven hoe de tekstinhoud tijdens het bewerken moet worden verwerkt.
```csharp
    TextEditOptions editOptions = new TextEditOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        RecognizeLists = true,
        LeadingSpaces = TextLeadingSpacesOptions.ConvertToIndent,
        TrailingSpaces = TextTrailingSpacesOptions.Trim
    };
```
## Stap 4: Maak een EditableDocument-exemplaar
 Zorg ervoor dat de bewerkingsopties zijn ingesteld en maak een`EditableDocument` voorbeeld. Dit vertegenwoordigt het document in een bewerkbaar formaat.
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## Stap 5: Bewerk de documentinhoud
Haal de originele tekstinhoud op en voer de gewenste bewerkingen uit. Voor dit voorbeeld vervangen we het woord 'tekst' door 'BEWERKTE tekst'.
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("text", "EDITED text");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## Stap 6: Maak een bewerkbaar document met bijgewerkte inhoud
 Nadat u de nodige wijzigingen heeft aangebracht, maakt u een nieuw`EditableDocument` met de bijgewerkte inhoud en de originele bronnen.
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## Stap 7: Creëer opties voor het opslaan van tekstverwerking
Bereid de opslagopties voor het WordProcessing-formaat voor. In dit voorbeeld wordt de DOCM-indeling gebruikt en wordt de landinstelling opgegeven.
```csharp
    WordProcessingSaveOptions wordSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm)
    {
        Locale = System.Globalization.CultureInfo.GetCultureInfo("en-GB")
    };
```
## Stap 8: Creëer TXT-opslagopties
Maak op dezelfde manier de opslagopties voor het TXT-formaat. Zorg ervoor dat de codering is ingesteld op UTF-8 en behoud de tabelindeling.
```csharp
    TextSaveOptions txtSaveOptions = new TextSaveOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        PreserveTableLayout = true
    };
```
## Stap 9: Uitvoerpaden voorbereiden
Bereid de paden voor voor het opslaan van de resulterende DOCX- en TXT-bestanden. Gebruik het invoerbestandspad om de uitvoermap en bestandsnamen te bepalen.
```csharp
    string outputWordPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".docm");
    string outputTxtPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".txt");
```
## Stap 10: Sla het bewerkte document op
Sla ten slotte het bewerkte document op in zowel de DOCX- als de TXT-indeling met behulp van de opgegeven opslagopties.
```csharp
    editor.Save(afterEdit, outputWordPath, wordSaveOptions);
    editor.Save(afterEdit, outputTxtPath, txtSaveOptions);
}
System.Console.WriteLine("Document editing process completed successfully!");
```
## Conclusie
 Gefeliciteerd! U hebt met succes een document zonder opmaak bewerkt met GroupDocs.Editor voor .NET. Deze krachtige tool vereenvoudigt het bewerken van documenten, waardoor deze eenvoudig in uw .NET-applicaties kan worden geïntegreerd. Of u nu eenvoudige tekstbestanden of complexe documentformaten verwerkt, GroupDocs.Editor staat voor u klaar. Ontdek meer functies en mogelijkheden door naar de[GroupDocs.Editor-documentatie](https://tutorials.groupdocs.com/editor/net/).
## Veelgestelde vragen
### Welke bestandsindelingen ondersteunt GroupDocs.Editor voor .NET?
 GroupDocs.Editor voor .NET ondersteunt een breed scala aan bestandsindelingen, waaronder DOCX, TXT, HTML en meer. Controleer de[documentatie](https://tutorials.groupdocs.com/editor/net/) voor een volledige lijst.
### Hoe kan ik een gratis proefversie van GroupDocs.Editor voor .NET krijgen?
 U kunt een gratis proefversie van GroupDocs.Editor voor .NET downloaden van de[releases pagina](https://releases.groupdocs.com/).
### Kan ik een tijdelijke licentie kopen voor GroupDocs.Editor voor .NET?
Ja, u kunt een tijdelijke licentie verkrijgen bij de[GroupDocs-aankooppagina](https://purchase.groupdocs.com/temporary-license/).
### Waar kan ik ondersteuning krijgen voor GroupDocs.Editor voor .NET?
 Ondersteuning is beschikbaar via de[GroupDocs.Editor-ondersteuningsforum](https://forum.groupdocs.com/c/editor/20).
### Is er gedetailleerde documentatie beschikbaar voor GroupDocs.Editor voor .NET?
 Ja, gedetailleerde documentatie is beschikbaar op de[GroupDocs.Editor-documentatiepagina](https://tutorials.groupdocs.com/editor/net/).