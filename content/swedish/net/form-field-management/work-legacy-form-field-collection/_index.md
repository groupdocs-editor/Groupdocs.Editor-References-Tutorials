---
title: Arbeta med Legacy Form Field Collection
linktitle: Arbeta med Legacy Form Field Collection
second_title: GroupDocs.Editor .NET API
description: Lär dig hur du hanterar äldre formulärfält med hjälp av GroupDocs.Editor för .NET med vår detaljerade guide. Perfekt för att hantera textfält, kryssrutor, datum och mer.
weight: 12
url: /sv/net/form-field-management/work-legacy-form-field-collection/
---

# Arbeta med Legacy Form Field Collection

## Introduktion
Välkommen till den här omfattande guiden om hur man arbetar med äldre formulärfältsamlingar med GroupDocs.Editor för .NET. Oavsett om du har att göra med textfält, kryssrutor, datumfält eller rullgardinsmenyer, kommer den här handledningen att gå igenom varje steg för att hantera dessa fält effektivt. I slutet av den här guiden har du en gedigen förståelse för hur du använder GroupDocs.Editor för att hantera olika formulärfält i dina dokument. Låt oss dyka in!
## Förutsättningar
Innan vi börjar, se till att du har följande förutsättningar:
- Visual Studio: Alla senaste versioner fungerar.
- .NET Framework: Se till att du har .NET Framework installerat.
-  GroupDocs.Editor för .NET: Ladda ner den senaste versionen[här](https://releases.groupdocs.com/editor/net/).
- Exempeldokument: Ett exempel på DOCX-fil med formulärfält för teständamål.
## Importera namnområden
Till att börja med, importera de nödvändiga namnrymden i ditt projekt. Dessa namnutrymmen är viktiga för att komma åt de klasser och metoder som krävs för att manipulera formulärfält.
```csharp
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System.IO;
```
## Steg 1: Hämta sökvägen för inmatningsfilen
Först måste du ange sökvägen till din indatafil. I det här exemplet använder vi ett exempel på DOCX-fil som innehåller olika formulärfält.
```csharp
string inputFilePath = "path/to/your/sample_legacy_formfields.docx";
```
## Steg 2: Skapa en ström från filsökvägen
Skapa sedan en filström för att läsa innehållet i ditt dokument. Denna ström kommer att användas för att ladda dokumentet i GroupDocs.Editor.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
    // Ytterligare kod kommer hit
}
```
## Steg 3: Skapa laddningsalternativ för dokumentet
Skapa laddningsalternativ innan du laddar dokumentet. Dessa alternativ hjälper till att hantera olika scenarier, till exempel lösenordsskyddade dokument.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
// Om dokumentet är lösenordsskyddat anger du lösenordet
loadOptions.Password = "your_password_here"; // Använd ett faktiskt lösenord om det behövs
```
## Steg 4: Ladda dokumentet med Editor Instance
Ladda nu dokumentet i Editor-instansen med hjälp av filströmmen och laddningsalternativ du skapade tidigare.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    // Ytterligare kod kommer hit
}
```
## Steg 5: Läs FormFieldManager-instansen
För att hantera formulärfält, gå till FormFieldManager-instansen från editorn. Den här instansen låter dig interagera med formulärfälten i ditt dokument.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
## Steg 6: Läs FormFieldCollection
Hämta FormFieldCollection från FormFieldManager. Den här samlingen innehåller alla formulärfält som finns i dokumentet.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
## Steg 7: Iterera genom varje formulärfält
Gå igenom varje formulärfält i samlingen och identifiera dess typ. Beroende på typen kan du extrahera och manipulera fältets värde.
```csharp
foreach (var formField in collection)
{
    switch (formField.Type)
    {
        case FormFieldType.Text:
            TextFormField textFormField = collection.GetFormField<TextFormField>(formField.Name);
            Console.WriteLine($"TextFormField detected, name: {formField.Name}, value: {textFormField.Value}");
            break;
        case FormFieldType.CheckBox:
            CheckBoxForm checkBoxFormField = collection.GetFormField<CheckBoxForm>(formField.Name);
            Console.WriteLine($"CheckBoxForm detected, name: {formField.Name}, value: {checkBoxFormField.Value}");
            break;
        case FormFieldType.Date:
            DateFormField dateFormField = collection.GetFormField<DateFormField>(formField.Name);
            Console.WriteLine($"DateFormField detected, name: {formField.Name}, value: {dateFormField.Value}");
            break;
        case FormFieldType.Number:
            NumberFormField numberFormField = collection.GetFormField<NumberFormField>(formField.Name);
            Console.WriteLine($"NumberFormField detected, name: {formField.Name}, value: {numberFormField.Value}");
            break;
        case FormFieldType.DropDown:
            DropDownFormField dropDownFormField = collection.GetFormField<DropDownFormField>(formField.Name);
            Console.WriteLine($"DropDownFormField detected, name: {formField.Name}, value selected: {dropDownFormField.Value[dropDownFormField.SelectedIndex]}");
            break;
    }
}
```
## Steg 8: Slutsats
Genom att följa dessa steg kan du effektivt hantera och interagera med äldre formulärfält i dina dokument med GroupDocs.Editor för .NET. Oavsett om det är textfält, kryssrutor, datum, siffror eller rullgardinsmenyer, ger den här guiden ett tydligt och kortfattat sätt att hantera varje typ.
## Slutsats
 Att arbeta med äldre formulärfält i dokument kan vara enkelt när du använder rätt verktyg. GroupDocs.Editor för .NET tillhandahåller en robust lösning för att hantera dessa fält effektivt. Genom att följa denna steg-för-steg-guide bör du nu kunna manipulera olika formulärfält i dina dokument med lätthet. Glöm inte att utforska[dokumentation](https://tutorials.groupdocs.com/editor/net/)för mer avancerade funktioner och alternativ.
## FAQ's
### 1. Kan jag använda GroupDocs.Editor för .NET med lösenordsskyddade dokument?
Ja, du kan ange lösenordet i laddningsalternativen för att hantera lösenordsskyddade dokument.
### 2. Hur får jag en gratis provversion av GroupDocs.Editor för .NET?
 Du kan ladda ner en gratis testversion från[här](https://releases.groupdocs.com/).
### 3. Finns det något stöd tillgängligt för GroupDocs.Editor för .NET?
 Ja, du kan få tillgång till support[här](https://forum.groupdocs.com/c/editor/20).
### 4. Kan jag köpa en licens för GroupDocs.Editor för .NET?
 Ja, du kan köpa en licens från[här](https://purchase.groupdocs.com/buy).
### 5. Var kan jag hitta dokumentationen för GroupDocs.Editor för .NET?
Dokumentationen finns tillgänglig[här](https://tutorials.groupdocs.com/editor/net/).