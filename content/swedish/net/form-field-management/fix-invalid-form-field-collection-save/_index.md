---
title: Åtgärda Insamling av ogiltiga formulärfält och spara
linktitle: Åtgärda Insamling av ogiltiga formulärfält och spara
second_title: GroupDocs.Editor .NET API
description: Lär dig hur du fixar ogiltiga formulärfält i DOCX med Groupdocs.Editor för .NET. Följ den här guiden för att säkerställa att dina dokument är felfria och spara dem på ett säkert sätt.
weight: 11
url: /sv/net/form-field-management/fix-invalid-form-field-collection-save/
type: docs
---
# Åtgärda Insamling av ogiltiga formulärfält och spara

## Introduktion
Välkommen! Om du arbetar med formulärfält i dokument och har problem med samlingar av ogiltiga formulärfält är du på rätt plats. I den här självstudien kommer vi att dyka in i hur du fixar ogiltiga formulärfält och sparar ditt dokument med Groupdocs.Editor för .NET. Vi guidar dig genom processen steg-för-steg, så att du har alla detaljer du behöver för att få det att fungera sömlöst. Låt oss börja!
## Förutsättningar
Innan vi går in i koden finns det några saker du måste ha på plats:
-  Groupdocs.Editor för .NET: Se till att du har installerat Groupdocs.Editor-biblioteket för .NET. Du kan ladda ner den[här](https://releases.groupdocs.com/editor/net/).
- Utvecklingsmiljö: Du bör ha en .NET-utvecklingsmiljö inställd, till exempel Visual Studio.
- Grundläggande kunskaper om C#: Denna handledning förutsätter att du har en grundläggande förståelse för C#-programmering.
## Importera namnområden
Först måste du importera de nödvändiga namnrymden i ditt C#-projekt. Lägg till följande rader i början av din kodfil:
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System;
using System.IO;
```
## Steg 1: Hämta sökvägen för inmatningsfilen
Det första steget är att ange sökvägen till din indatafil. Denna fil bör vara ett DOCX-dokument som innehåller formulärfält.
```csharp
string inputFilePath = Constants.SampleLegacyFormFields_docx;
```
## Steg 2: Skapa en ström från filsökvägen
Skapa sedan en filström för att läsa inmatningsdokumentet. Detta gör att du kan ladda dokumentet i editorn.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
```
## Steg 3: Skapa laddningsalternativ för dokumentet
I det här steget måste du skapa laddningsalternativ för ditt dokument. Om ditt dokument är lösenordsskyddat kan du ange lösenordet. I det här exemplet är dokumentet inte skyddat, så lösenordet ignoreras.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
loadOptions.Password = "some_password_to_open_a_document";
```
## Steg 4: Ladda dokumentet i Editor-instansen
Ladda nu dokumentet med de angivna alternativen i Editor-instansen. Det är här de huvudsakliga operationerna på dokumentet kommer att ske.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
```
## Steg 4.1: Läs FormFieldManager-instansen
 De`FormFieldManager` instans ansvarar för att hantera formulärfält i dokumentet. Du måste läsa den här instansen för att komma åt och manipulera formulärfälten.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
## Steg 4.2: Läs FormFieldCollection
 De`FormFieldCollection` innehåller alla formulärfält i dokumentet. Du kommer att läsa den här samlingen för att kontrollera och åtgärda ogiltiga formulärfält.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
## Steg 4.3: Åtgärda ogiltiga formulärfält automatiskt
Försök att automatiskt korrigera eventuella ogiltiga formulärfält i dokumentet. Detta är ett preliminärt steg för att ta itu med uppenbara problem.
```csharp
fieldManager.FixInvalidFormFieldNames(new InvalidFormField[0]);
collection = fieldManager.FormFieldCollection;
```
## Steg 4.4: Kontrollera om det finns ogiltiga formulärfält
Kontrollera om det finns några ogiltiga formulärfält kvar efter det automatiska korrigeringsförsöket.
```csharp
bool hasInvalidFormFields = fieldManager.HasInvalidFormFields();
Console.WriteLine("FormFieldCollection contains invalid items: {0}", hasInvalidFormFields);
```
## Steg 4.4.1: Hämta alla ogiltiga formulärfältnamn
Hämta namnen på alla ogiltiga formulärfält. Dessa namn kommer att användas för att fixa fälten.
```csharp
var invalidFormFields = fieldManager.GetInvalidFormFieldNames();
```
## Steg 4.4.2: Skapa unika namn för ogiltiga fält
Skapa ett unikt namn för varje ogiltigt formulärfält. Detta säkerställer att det inte finns några konflikter med befintliga formulärfältnamn.
```csharp
foreach (var invalidItem in invalidFormFields)
{
    invalidItem.FixedName = string.Format("{0}_{1}", invalidItem.Name, Guid.NewGuid());
}
```
## Steg 4.4.3: Åtgärda ogiltiga formulärfält
Åtgärda de ogiltiga formulärfälten med de unika namnen som skapades i föregående steg.
```csharp
fieldManager.FixInvalidFormFieldNames(invalidFormFields);
collection = fieldManager.FormFieldCollection;
```
## Steg 5: Skapa alternativ för att spara dokument
Ställ in alternativ för att spara dokumentet. Detta inkluderar att ange formatet och eventuella ytterligare sparainställningar.
```csharp
WordProcessingFormats docFormat = WordProcessingFormats.Docx;
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(docFormat);
```
## Steg 5.1: Optimera minnesanvändningen
 Om ditt dokument är stort och kan orsaka en`OutOfMemoryException`aktivera alternativet för minnesoptimering.
```csharp
saveOptions.OptimizeMemoryUsage = true;
```
## Steg 5.2: Skydda dokumentet från att skrivas
För att skydda dokumentet från att ändras, förutom formulärfälten, ställ in ett skyddslösenord.
```csharp
saveOptions.Protection = new WordProcessingProtection(WordProcessingProtectionType.AllowOnlyFormFields, "write_password");
```
## Steg 6: Spara dokumentet
Spara slutligen dokumentet med de angivna sparalternativen. Förbered en minnesström för att spara utdatadokumentet.
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(outputStream, saveOptions);
}
Console.WriteLine("FixInvalidFormFieldCollectionAndSave routine has successfully finished");
```
## Slutsats
 Och där har du det! Du har åtgärdat ogiltiga formulärfält och sparat ditt dokument med Groupdocs.Editor för .NET. Denna steg-för-steg-guide borde ha gjort processen tydlig och hanterbar. Om du stöter på några problem eller har frågor, kolla gärna[dokumentation](https://tutorials.groupdocs.com/editor/net/) eller nå ut till[Stöd](https://forum.groupdocs.com/c/editor/20).
## FAQ's
### Vad händer om mitt dokument är lösenordsskyddat?
 Du kan ange lösenordet i`WordProcessingLoadOptions` för att öppna dokumentet.
### Hur vet jag om det finns ogiltiga formulärfält?
 Använd`HasInvalidFormFields` metod för att kontrollera om det finns ogiltiga formulärfält i dokumentet.
### Kan jag fixa formulärfält utan att ändra deras namn?
Det rekommenderas att skapa unika namn för ogiltiga formulärfält för att undvika konflikter.
### Vilka format kan jag spara dokumentet i?
 Du kan spara dokumentet i olika format som DOCX, PDF och mer genom att ställa in lämpligt`WordProcessingFormats`.
### Hur kan jag optimera minnesanvändningen samtidigt som jag sparar stora dokument?
 Aktivera`OptimizeMemoryUsage` alternativet i`WordProcessingSaveOptions` att hantera stora dokument effektivt.