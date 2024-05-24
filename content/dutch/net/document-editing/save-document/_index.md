---
title: Document opslaan
linktitle: Document opslaan
second_title: GroupDocs.Editor .NET API
description: Bewerk en bewaar documenten moeiteloos met GroupDocs.Editor voor .NET. Deze stapsgewijze handleiding vereenvoudigt het proces voor ontwikkelaars.
type: docs
weight: 14
url: /nl/net/document-editing/save-document/
---
## Invoering
Wilt u moeiteloos documenten bewerken en opslaan met GroupDocs.Editor voor .NET? Je bent op de juiste plek! Deze tutorial begeleidt u stap voor stap door het proces, zodat u uw documenten eenvoudig kunt beheren. Of u nu een doorgewinterde ontwikkelaar of een beginner bent, onze gids geeft u alle informatie die u nodig heeft om aan de slag te gaan.
## Vereisten
Voordat u in de zelfstudie duikt, moet u ervoor zorgen dat u aan de volgende vereisten voldoet:
- Ontwikkelomgeving: Visual Studio geïnstalleerd op uw machine.
- .NET Framework: Zorg ervoor dat u .NET Framework 4.6.1 of hoger hebt.
-  GroupDocs.Editor voor .NET: Download de nieuwste versie[hier](https://releases.groupdocs.com/editor/net/).
- Basiskennis C#: Bekendheid met programmeren in C# is essentieel.
## Naamruimten importeren
Om GroupDocs.Editor in uw .NET-project te gebruiken, moet u de benodigde naamruimten importeren. Zo doe je het:
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
Nu we onze omgeving hebben ingesteld en de benodigde naamruimten hebben geïmporteerd, gaan we dieper in op de stappen die nodig zijn om een document te laden, bewerken en opslaan met GroupDocs.Editor voor .NET.
## Stap 1: Laad het document
Eerst moeten we het document laden dat we willen bewerken. GroupDocs.Editor maakt dit proces eenvoudig. Hier ziet u hoe u het kunt doen:

```csharp
string inputFilePath = "Your Sample Document";
Editor editor = new Editor(inputFilePath, delegate { return new Options.WordProcessingLoadOptions(); });
EditableDocument defaultWordProcessingDoc = editor.Edit();
```
 In deze stap specificeren we het pad naar het document dat we willen bewerken en maken we een exemplaar van het`Editor` klas. De`Edit` methode wordt vervolgens aangeroepen om het document in een`EditableDocument` voorwerp.
## Stap 2: Wijzig het document
Nu het document is geladen, is het tijd om enkele wijzigingen aan te brengen. Omdat we geen WYSIWYG-editor hebben, simuleren we het bewerkingsproces in code.

```csharp
string allEmbeddedInsideString = defaultWordProcessingDoc.GetEmbeddedHtml();
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
EditableDocument editedDoc = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```
 Hier halen we de ingesloten HTML-inhoud van het document op, voeren een eenvoudige tekstvervanging uit en maken een nieuwe`EditableDocument`exemplaar van de gewijzigde HTML.
## Stap 3: Sla het document op
Nadat u het document hebt bewerkt, is de laatste stap het opslaan ervan. GroupDocs.Editor biedt meerdere opties om het document in verschillende formaten op te slaan.
## Opslaan als RTF
```csharp
string outputRtfPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.rtf");
WordProcessingSaveOptions rtfSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
editor.Save(editedDoc, outputRtfPath, rtfSaveOptions);
```
## Opslaan als DOCM
```csharp
string outputDocmPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.docm");
WordProcessingSaveOptions docmSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm);
using (FileStream outputStream = File.Create(outputDocmPath))
{
    editor.Save(editedDoc, outputStream, docmSaveOptions);
}
```
## Opslaan als platte tekst
```csharp
string outputTxtPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.txt");
TextSaveOptions textSaveOptions = new TextSaveOptions
{
    Encoding = System.Text.Encoding.UTF8,
    PreserveTableLayout = true
};
editor.Save(editedDoc, outputTxtPath, textSaveOptions);
```
## Stap 4: Opruimen
 Ten slotte is het van cruciaal belang om de`EditableDocument` En`Editor` instances om bronnen vrij te maken.
```csharp
editedDoc.Dispose();
defaultWordProcessingDoc.Dispose();
editor.Dispose();
```
Door deze stappen te volgen, kunt u documenten efficiënt laden, bewerken en opslaan met GroupDocs.Editor voor .NET. Deze krachtige tool biedt flexibiliteit en gebruiksgemak, waardoor documentbeheer een fluitje van een cent wordt.
## Conclusie
Documenten programmatisch bewerken en opslaan is nog nooit zo eenvoudig geweest met GroupDocs.Editor voor .NET. Deze gids begeleidt u door het hele proces, van het laden van een document tot het opslaan in verschillende formaten. Met GroupDocs.Editor heeft u een veelzijdige en robuuste oplossing binnen handbereik, die het documentbewerkingsproces vereenvoudigt.
## Veelgestelde vragen
### Welke bestandsformaten ondersteunt GroupDocs.Editor?
GroupDocs.Editor ondersteunt verschillende bestandsformaten, waaronder DOCX, RTF, TXT en nog veel meer. Voor een volledige lijst, bekijk de[documentatie](https://reference.groupdocs.com/editor/net/).
### Kan ik GroupDocs.Editor uitproberen voordat ik het aanschaf?
 Ja, je kunt een[gratis proefperiode](https://releases.groupdocs.com/) om de functies van GroupDocs.Editor te testen.
### Is er ondersteuning beschikbaar als ik problemen ondervind?
 Absoluut! U kunt een bezoek brengen aan de[Helpforum](https://forum.groupdocs.com/c/editor/20) voor hulp bij eventuele problemen die u tegenkomt.
### Hoe verkrijg ik een tijdelijke licentie?
 U kunt een aanvraag indienen voor een[tijdelijke licentie](https://purchase.groupdocs.com/temporary-license/) voor evaluatiedoeleinden.
### Waar kan ik de volledige versie van GroupDocs.Editor kopen?
 Je kunt de volledige versie kopen[hier](https://purchase.groupdocs.com/buy).