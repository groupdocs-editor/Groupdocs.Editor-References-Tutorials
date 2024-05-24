---
title: Werken met gescheiden gescheiden waarden (DSV)
linktitle: Werken met gescheiden gescheiden waarden (DSV)
second_title: GroupDocs.Editor .NET API
description: Leer hoe u CSV- en TSV-bestanden kunt bewerken met GroupDocs.Editor voor .NET met deze stapsgewijze handleiding. Verbeter moeiteloos uw .NET-projecten.
type: docs
weight: 12
url: /nl/net/document-processing/work-dsv/
---
## Invoering
Als u een ontwikkelaar bent die met gescheiden waarden (DSV) werkt, zoals CSV- of TSV-bestanden, weet u dat het programmatisch bewerken van deze bestanden een hele klus kan zijn. Met GroupDocs.Editor voor .NET wordt deze taak echter aanzienlijk eenvoudiger en efficiënter. In deze zelfstudie laten we u zien hoe u GroupDocs.Editor voor .NET kunt gebruiken om DSV-bestanden te lezen, bewerken en opslaan. We verdelen het proces in eenvoudig te volgen stappen, zodat u het eenvoudig in uw projecten kunt implementeren.
## Vereisten
Voordat we ingaan op de tutorial, zorg ervoor dat je aan de volgende vereisten voldoet:
- Visual Studio: Zorg ervoor dat Visual Studio op uw computer is geïnstalleerd.
-  GroupDocs.Editor voor .NET: u moet de GroupDocs.Editor voor .NET-bibliotheek downloaden en ernaar verwijzen. Je kunt het downloaden[hier](https://releases.groupdocs.com/editor/net/).
- Basiskennis van C#: Deze tutorial gaat ervan uit dat je een basiskennis hebt van C# en .NET-ontwikkeling.
## Naamruimten importeren
Eerst moet u de benodigde naamruimten in uw project importeren. Deze naamruimten bieden de klassen en methoden die nodig zijn om met GroupDocs.Editor voor .NET te werken.
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

## Stap 1: Haal een pad op naar het invoer-DSV-bestand
Eerst moet u het pad naar het invoer-DSV-bestand opgeven. Voor dit voorbeeld gaan we ervan uit dat het een CSV-bestand is.
```csharp
string inputFilePath = "Your Sample Document";
```
## Stap 2: Maak een Editor-instantie
 Maak een exemplaar van de`Editor` klas. Deze instantie wordt gebruikt om het DSV-bestand te laden en te manipuleren.
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## Stap 3: Maak DSV-bewerkingsopties
 Maak vervolgens een exemplaar van`DelimitedTextEditOptions` en geef het scheidingsteken voor het DSV-bestand op. Hier gebruiken we een komma als scheidingsteken.
```csharp
    Options.DelimitedTextEditOptions editOptions = new DelimitedTextEditOptions(",");
    editOptions.ConvertDateTimeData = false;
    editOptions.ConvertNumericData = true;
    editOptions.TreatConsecutiveDelimitersAsOne = true;
```
## Stap 4: Maak een EditableDocument-exemplaar
 Creëer een`EditableDocument` bijvoorbeeld met behulp van de`Editor.Edit` methode. Hiermee wordt het document gereedgemaakt voor bewerking.
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## Stap 5: Bewerk de documentinhoud
Haal de originele tekstinhoud op en breng de nodige wijzigingen aan. Laten we voor demonstratiedoeleinden wat tekst vervangen.
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("SsangYong", "Chevrolet").Replace("Kyron", "Camaro");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## Stap 6: Maak een bewerkbaar document met bijgewerkte inhoud
 Maak een nieuwe`EditableDocument` met de bijgewerkte inhoud.
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## Stap 7: Maak CSV-opslagopties
Geef de opslagopties op voor de CSV-indeling, inclusief het scheidingsteken en de codering.
```csharp
    Options.DelimitedTextSaveOptions csvSaveOptions = new DelimitedTextSaveOptions(",");
    csvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## Stap 8: Maak TSV-opslagopties
Geef op dezelfde manier de opslagopties op voor het TSV-formaat.
```csharp
    Options.DelimitedTextSaveOptions tsvSaveOptions = new DelimitedTextSaveOptions("\t");
    tsvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## Stap 9: Maak spreadsheet-opslagopties aan
Als u het document als spreadsheet wilt opslaan, maakt u de bijbehorende opslagopties aan.
```csharp
    Options.SpreadsheetSaveOptions cellsSaveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
```
## Stap 10: Bereid opslagpaden voor
Definieer de paden waar de bewerkte bestanden worden opgeslagen.
```csharp
    string outputCsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".csv");
    string outputTsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".tsv");
    string outputCellsPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".xlsm");
```
## Stap 11: Sla het bewerkte document op
Sla het bewerkte document op in de opgegeven paden in verschillende formaten.
```csharp
    editor.Save(afterEdit, outputCsvPath, csvSaveOptions);
    editor.Save(afterEdit, outputTsvPath, tsvSaveOptions);
    editor.Save(afterEdit, outputCellsPath, cellsSaveOptions);
```
## Stap 12: Verwijder bewerkbare documenten
 Zorg er ten slotte voor dat u de`EditableDocument` instances om bronnen vrij te maken.
```csharp
    beforeEdit.Dispose();
    afterEdit.Dispose();
}
System.Console.WriteLine("WorkingWithDsv routine has successfully finished");
```
## Conclusie
Het bewerken van DSV-bestanden met GroupDocs.Editor voor .NET is een eenvoudig proces waarbij een editorinstantie wordt gemaakt, bewerkingsopties worden ingesteld, de inhoud wordt gewijzigd en de wijzigingen worden opgeslagen. Met deze stapsgewijze handleiding kunt u deze functionaliteit eenvoudig in uw .NET-applicaties integreren. Of u nu met CSV-, TSV- of andere DSV-formaten werkt, GroupDocs.Editor voor .NET biedt een robuuste en flexibele oplossing.
## Veelgestelde vragen
### Kan ik GroupDocs.Editor voor .NET gebruiken om grote CSV-bestanden te bewerken?
Ja, GroupDocs.Editor voor .NET kan grote CSV-bestanden efficiënt verwerken.
### Ondersteunt GroupDocs.Editor voor .NET naast CSV en TSV ook andere DSV-formaten?
Ja, het ondersteunt verschillende DSV-formaten, zolang u het juiste scheidingsteken opgeeft.
### Is het mogelijk om de codering aan te passen bij het opslaan van DSV-bestanden?
Absoluut, u kunt de gewenste codering opgeven in de opslagopties.
### Kan ik een CSV-bestand naar een Excel-spreadsheet converteren met GroupDocs.Editor voor .NET?
Ja, u kunt een CSV-bestand opslaan als Excel-spreadsheet met behulp van de juiste opslagopties.
### Waar kan ik meer documentatie vinden over GroupDocs.Editor voor .NET?
 U kunt gedetailleerde documentatie vinden[hier](https://reference.groupdocs.com/editor/net/)