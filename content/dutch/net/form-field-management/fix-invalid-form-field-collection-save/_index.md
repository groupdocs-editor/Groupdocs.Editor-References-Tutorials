---
title: Herstel ongeldige formulierveldverzameling en sla op
linktitle: Herstel ongeldige formulierveldverzameling en sla op
second_title: GroupDocs.Editor .NET API
description: Leer hoe u ongeldige formuliervelden in DOCX kunt corrigeren met Groupdocs.Editor voor .NET. Volg deze handleiding om ervoor te zorgen dat uw documenten foutloos zijn en ze veilig opslaan.
weight: 11
url: /nl/net/form-field-management/fix-invalid-form-field-collection-save/
type: docs
---
# Herstel ongeldige formulierveldverzameling en sla op

## Invoering
Welkom! Als u met formuliervelden in documenten werkt en problemen ondervindt met ongeldige formulierveldverzamelingen, bent u hier aan het juiste adres. In deze zelfstudie gaan we dieper in op het corrigeren van ongeldige formuliervelden en het opslaan van uw document met Groupdocs.Editor voor .NET. We begeleiden u stap voor stap door het proces, zodat u over alle details beschikt die u nodig heeft om het naadloos te laten werken. Laten we beginnen!
## Vereisten
Voordat we ingaan op de code, zijn er een paar dingen die u moet regelen:
-  Groupdocs.Editor voor .NET: Zorg ervoor dat u de Groupdocs.Editor-bibliotheek voor .NET hebt geïnstalleerd. Je kunt het downloaden[hier](https://releases.groupdocs.com/editor/net/).
- Ontwikkelomgeving: U moet een .NET-ontwikkelomgeving hebben ingesteld, zoals Visual Studio.
- Basiskennis van C#: Deze tutorial gaat ervan uit dat je een basiskennis hebt van programmeren in C#.
## Naamruimten importeren
Eerst moet u de benodigde naamruimten in uw C#-project importeren. Voeg de volgende regels toe aan het begin van uw codebestand:
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System;
using System.IO;
```
## Stap 1: Haal het invoerbestandspad op
De eerste stap is het opgeven van het pad naar uw invoerbestand. Dit bestand moet een DOCX-document zijn dat formuliervelden bevat.
```csharp
string inputFilePath = Constants.SampleLegacyFormFields_docx;
```
## Stap 2: Maak een stream vanuit het bestandspad
Maak vervolgens een bestandsstream om het invoerdocument te lezen. Hierdoor kunt u het document in de editor laden.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
```
## Stap 3: Maak laadopties voor het document
In deze stap moet u laadopties voor uw document maken. Als uw document met een wachtwoord is beveiligd, kunt u het wachtwoord opgeven. In dit voorbeeld is het document niet beveiligd en wordt het wachtwoord genegeerd.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
loadOptions.Password = "some_password_to_open_a_document";
```
## Stap 4: Laad het document in de Editor-instantie
Laad nu het document met de opgegeven opties in de Editor-instantie. Dit is waar de belangrijkste bewerkingen op het document zullen plaatsvinden.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
```
## Stap 4.1: Lees de FormFieldManager-instantie
 De`FormFieldManager` instance is verantwoordelijk voor het beheer van formuliervelden in het document. U moet dit exemplaar lezen om toegang te krijgen tot de formuliervelden en deze te kunnen manipuleren.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
## Stap 4.2: Lees de FormFieldCollection
 De`FormFieldCollection` bevat alle formuliervelden in het document. U leest deze verzameling om ongeldige formuliervelden te controleren en op te lossen.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
## Stap 4.3: Ongeldige formuliervelden automatisch corrigeren
Probeer eventuele ongeldige formuliervelden in het document automatisch aan te passen. Dit is een voorbereidende stap om voor de hand liggende problemen aan te pakken.
```csharp
fieldManager.FixInvalidFormFieldNames(new InvalidFormField[0]);
collection = fieldManager.FormFieldCollection;
```
## Stap 4.4: Controleer op ongeldige formuliervelden
Controleer of er ongeldige formuliervelden overblijven na de autofix-poging.
```csharp
bool hasInvalidFormFields = fieldManager.HasInvalidFormFields();
Console.WriteLine("FormFieldCollection contains invalid items: {0}", hasInvalidFormFields);
```
## Stap 4.4.1: Haal alle ongeldige formulierveldnamen op
Haal de namen op van alle ongeldige formuliervelden. Deze namen worden gebruikt om de velden te corrigeren.
```csharp
var invalidFormFields = fieldManager.GetInvalidFormFieldNames();
```
## Stap 4.4.2: Creëer unieke namen voor ongeldige velden
Maak voor elk ongeldig formulierveld een unieke naam. Dit zorgt ervoor dat er geen conflicten ontstaan met bestaande formulierveldnamen.
```csharp
foreach (var invalidItem in invalidFormFields)
{
    invalidItem.FixedName = string.Format("{0}_{1}", invalidItem.Name, Guid.NewGuid());
}
```
## Stap 4.4.3: Herstel ongeldige formuliervelden
Corrigeer de ongeldige formuliervelden met behulp van de unieke namen die in de vorige stap zijn gemaakt.
```csharp
fieldManager.FixInvalidFormFieldNames(invalidFormFields);
collection = fieldManager.FormFieldCollection;
```
## Stap 5: Creëer opties voor documentopslag
Opties instellen voor het opslaan van het document. Dit omvat het opgeven van het formaat en eventuele aanvullende opslaginstellingen.
```csharp
WordProcessingFormats docFormat = WordProcessingFormats.Docx;
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(docFormat);
```
## Stap 5.1: Optimaliseer het geheugengebruik
 Als uw document groot is en een`OutOfMemoryException`schakel de optie voor geheugenoptimalisatie in.
```csharp
saveOptions.OptimizeMemoryUsage = true;
```
## Stap 5.2: Beveilig het document tegen schrijven
Om te voorkomen dat het document wordt gewijzigd, behalve de formuliervelden, stelt u een beveiligingswachtwoord in.
```csharp
saveOptions.Protection = new WordProcessingProtection(WordProcessingProtectionType.AllowOnlyFormFields, "write_password");
```
## Stap 6: Bewaar het document
Sla ten slotte het document op met de opgegeven opslagopties. Bereid een geheugenstroom voor voor het opslaan van het uitvoerdocument.
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(outputStream, saveOptions);
}
Console.WriteLine("FixInvalidFormFieldCollectionAndSave routine has successfully finished");
```
## Conclusie
 En daar heb je het! U heeft ongeldige formuliervelden hersteld en uw document opgeslagen met Groupdocs.Editor voor .NET. Deze stapsgewijze handleiding had het proces duidelijk en beheersbaar moeten maken. Als u problemen ondervindt of vragen heeft, kunt u terecht op de[documentatie](https://tutorials.groupdocs.com/editor/net/) of contact opnemen[steun](https://forum.groupdocs.com/c/editor/20).
## Veelgestelde vragen
### Wat moet ik doen als mijn document met een wachtwoord is beveiligd?
 U kunt het wachtwoord opgeven in het`WordProcessingLoadOptions` om het document te openen.
### Hoe weet ik of er ongeldige formuliervelden zijn?
 Gebruik de`HasInvalidFormFields` methode om te controleren op ongeldige formuliervelden in het document.
### Kan ik formuliervelden corrigeren zonder hun namen te wijzigen?
Het wordt aanbevolen om unieke namen te maken voor ongeldige formuliervelden om conflicten te voorkomen.
### In welke formaten kan ik het document opslaan?
 U kunt het document in verschillende formaten opslaan, zoals DOCX, PDF en meer, door de juiste instelling in te stellen`WordProcessingFormats`.
### Hoe kan ik het geheugengebruik optimaliseren terwijl ik grote documenten opsla?
 Schakel de`OptimizeMemoryUsage` optie in de`WordProcessingSaveOptions` om grote documenten efficiënt te verwerken.