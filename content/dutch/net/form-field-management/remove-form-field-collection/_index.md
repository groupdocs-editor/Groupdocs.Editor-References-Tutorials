---
title: Formulierveldverzameling verwijderen
linktitle: Formulierveldverzameling verwijderen
second_title: GroupDocs.Editor .NET API
description: Leer met deze stapsgewijze handleiding hoe u formuliervelden uit Word-documenten kunt verwijderen met GroupDocs.Editor voor .NET. Ideaal voor ontwikkelaars.
weight: 13
url: /nl/net/form-field-management/remove-form-field-collection/
---

# Formulierveldverzameling verwijderen

## Invoering
Wilt u formuliervelden in uw documenten programmatisch beheren? GroupDocs.Editor voor .NET biedt een krachtige oplossing voor het verwerken en manipuleren van formuliervelden in verschillende documentformaten. In deze zelfstudie begeleiden we u bij de stappen om formulierveldverzamelingen uit een Word-document te verwijderen met behulp van deze robuuste bibliotheek. 
## Vereisten
Voordat we in de code duiken, zorgen we ervoor dat je alles hebt ingesteld voor een soepele ervaring:
1. GroupDocs.Editor voor .NET: Zorg ervoor dat u GroupDocs.Editor voor .NET hebt gedownload en geïnstalleerd. Zo niet, dan kunt u deze downloaden[hier](https://releases.groupdocs.com/editor/net/).
2. Ontwikkelomgeving: Je hebt een ontwikkelomgeving zoals Visual Studio nodig.
3. .NET Framework: Zorg ervoor dat .NET Framework op uw computer is geïnstalleerd.
4.  Voorbeelddocument: zorg dat u een voorbeeld van een Word-document hebt (bijv.`SampleLegacyFormFields.docx`) met formuliervelden die u wilt manipuleren.

## Naamruimten importeren
Om aan de slag te gaan, moet u de benodigde naamruimten in uw .NET-project importeren. Hierdoor krijgt u toegang tot de functionaliteiten van GroupDocs.Editor.
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System.IO;
```
## Stap 1: Laad het document
Eerst moet u het document laden dat u wilt bewerken. Laten we het opsplitsen:
### Stap 1.1: Haal het pad naar het invoerbestand op
 U moet het pad naar uw invoerbestand opgeven. Voor dit voorbeeld gebruiken we een voorbeeldbestand genaamd`SampleLegacyFormFields.docx`.
```csharp
string inputFilePath = "path/to/SampleLegacyFormFields.docx";
```
### Stap 1.2: Maak een FileStream vanaf het pad
 Maak vervolgens een`FileStream` om het document te lezen.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
    // Ga verder met de volgende stappen binnen dit gebruiksblok.
}
```
## Stap 2: Laadopties instellen
Wanneer u het document laadt, moet u mogelijk laadopties opgeven, vooral als uw document met een wachtwoord is beveiligd.
### Stap 2.1: Maak laadopties aan
 Maak een exemplaar van`WordProcessingLoadOptions`.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
```
### Stap 2.2: Wachtwoord opgeven (indien nodig)
Als uw document met een wachtwoord is beveiligd, kunt u het wachtwoord opgeven.
```csharp
loadOptions.Password = "some_password_to_open_a_document";
```
## Stap 3: Laad het document in de Editor
 Laad nu het document in het`Editor` bijvoorbeeld met behulp van de`FileStream` En`LoadOptions`.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    // Ga verder met de volgende stappen binnen dit gebruiksblok.
}
```
## Stap 4: Formuliervelden openen en beheren
Nu het document is geladen, kunt u nu de formuliervelden openen en manipuleren.
### Stap 4.1: Lees de FormFieldManager
 Haal de`FormFieldManager` van de`Editor` voorbeeld.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
### Stap 4.2: Toegang tot FormFieldCollection
 Pak de`FormFieldCollection` die alle formuliervelden in het document bevat.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
### Stap 4.3: Verwijder een specifiek tekstformulierveld
Om een specifiek tekstformulierveld te verwijderen, zoekt u het op de naam en verwijdert u het vervolgens.
```csharp
TextFormField textField = collection.GetFormField<TextFormField>("Text1");
fieldManager.RemoveFormFiled(textField);
```
### Stap 4.4: Meerdere formuliervelden verwijderen
U kunt ook meerdere formuliervelden tegelijk verwijderen door hun namen op te geven.
```csharp
textField = collection.GetFormField<TextFormField>("Text7");
CheckBoxForm checkBoxForm = collection.GetFormField<CheckBoxForm>("Check2");
fieldManager.RemoveFormFields(new IFormField[] { textField, checkBoxForm });
```
## Stap 5: Sla het gewijzigde document op
Nadat u de formuliervelden heeft gewijzigd, moet u het document opslaan.
### Stap 5.1: Creëer opslagopties
Geef het formaat en de opslagopties op voor het uitvoerdocument.
```csharp
WordProcessingFormats docFormat = WordProcessingFormats.Docx;
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(docFormat);
```
### Stap 5.2: Optimaliseer het geheugengebruik
Als u met grote documenten te maken heeft, wilt u wellicht het geheugengebruik optimaliseren.
```csharp
saveOptions.OptimizeMemoryUsage = true;
```
### Stap 5.3: Beveiliging instellen (indien nodig)
U kunt het document tegen verdere bewerking beveiligen door een schrijfwachtwoord in te stellen.
```csharp
saveOptions.Protection = new WordProcessingProtection(WordProcessingProtectionType.AllowOnlyFormFields, "write_password");
```
### Stap 5.4: Bewaar het document
 Sla het document ten slotte op met behulp van een`MemoryStream`.
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(outputStream, saveOptions);
}
```

## Conclusie
Gefeliciteerd! U hebt met succes formuliervelden uit een Word-document verwijderd met GroupDocs.Editor voor .NET. Deze krachtige bibliotheek maakt het eenvoudig om documentinhoud programmatisch te manipuleren, waardoor u tijd en moeite bespaart.
## Veelgestelde vragen
### Kan ik GroupDocs.Editor voor .NET gebruiken met andere documentformaten?
Ja, GroupDocs.Editor voor .NET ondersteunt verschillende documentformaten, waaronder PDF, HTML en meer.
### Is het mogelijk om formuliervelden toe te voegen met GroupDocs.Editor voor .NET?
Ja, u kunt formuliervelden programmatisch toevoegen, wijzigen en verwijderen.
### Wat moet ik doen als mijn document erg groot is?
U kunt geheugenoptimalisatie inschakelen in de opslagopties om grote documenten efficiënt te verwerken.
### Kan ik GroupDocs.Editor voor .NET gebruiken in een webapplicatie?
Absoluut! GroupDocs.Editor voor .NET kan worden geïntegreerd in webapplicaties voor documentverwerking op de server.
### Waar kan ik ondersteuning krijgen als ik problemen tegenkom?
 U kunt een bezoek brengen aan de[Helpforum](https://forum.groupdocs.com/c/editor/20) voor hulp bij eventuele problemen.