---
title: Ta bort formulärfältsamling
linktitle: Ta bort formulärfältsamling
second_title: GroupDocs.Editor .NET API
description: Lär dig hur du tar bort formulärfält från Word-dokument med GroupDocs.Editor för .NET med denna steg-för-steg-guide. Idealisk för utvecklare.
weight: 13
url: /sv/net/form-field-management/remove-form-field-collection/
type: docs
---
# Ta bort formulärfältsamling

## Introduktion
Vill du hantera formulärfält i dina dokument programmatiskt? GroupDocs.Editor för .NET erbjuder en kraftfull lösning för att hantera och manipulera formulärfält i olika dokumentformat. I den här självstudien guidar vi dig genom stegen för att ta bort formulärfältsamlingar från ett Word-dokument med hjälp av detta robusta bibliotek. 
## Förutsättningar
Innan vi dyker in i koden, låt oss se till att du har allt inställt för en smidig upplevelse:
1. GroupDocs.Editor för .NET: Se till att du har laddat ner och installerat GroupDocs.Editor för .NET. Om inte kan du ladda ner den[här](https://releases.groupdocs.com/editor/net/).
2. Utvecklingsmiljö: Du behöver en utvecklingsmiljö som Visual Studio.
3. .NET Framework: Se till att du har .NET Framework installerat på din dator.
4.  Exempeldokument: Ha ett exempel på Word-dokument (t.ex.`SampleLegacyFormFields.docx`) med formulärfält som du vill manipulera.

## Importera namnområden
För att komma igång måste du importera de nödvändiga namnrymden i ditt .NET-projekt. Detta ger dig tillgång till GroupDocs.Editor-funktioner.
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System.IO;
```
## Steg 1: Ladda dokumentet
Först måste du ladda dokumentet du vill redigera. Låt oss bryta ner det:
### Steg 1.1: Hämta sökvägen till indatafilen
 Du måste ange sökvägen till din indatafil. För det här exemplet använder vi en exempelfil som heter`SampleLegacyFormFields.docx`.
```csharp
string inputFilePath = "path/to/SampleLegacyFormFields.docx";
```
### Steg 1.2: Skapa en FileStream från sökvägen
 Skapa sedan en`FileStream` att läsa dokumentet.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
    // Fortsätt till nästa steg inom detta block.
}
```
## Steg 2: Ställ in laddningsalternativ
När du laddar dokumentet kan du behöva ange laddningsalternativ, särskilt om ditt dokument är lösenordsskyddat.
### Steg 2.1: Skapa laddningsalternativ
 Skapa en instans av`WordProcessingLoadOptions`.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
```
### Steg 2.2: Ange lösenord (om det behövs)
Om ditt dokument är lösenordsskyddat kan du ange lösenordet.
```csharp
loadOptions.Password = "some_password_to_open_a_document";
```
## Steg 3: Ladda dokumentet i Editor
 Ladda nu dokumentet i`Editor` instans med hjälp av`FileStream` och`LoadOptions`.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    // Fortsätt till nästa steg inom detta block.
}
```
## Steg 4: Få åtkomst till och hantera formulärfält
Med dokumentet laddat kan du nu komma åt och manipulera formulärfälten.
### Steg 4.1: Läs FormFieldManager
 Hämta`FormFieldManager` från`Editor` exempel.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
### Steg 4.2: Öppna FormFieldCollection
 Få den`FormFieldCollection` som innehåller alla formulärfält i dokumentet.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
### Steg 4.3: Ta bort ett specifikt textformulärfält
För att ta bort ett specifikt textformulärfält, leta upp det efter dess namn och ta sedan bort det.
```csharp
TextFormField textField = collection.GetFormField<TextFormField>("Text1");
fieldManager.RemoveFormFiled(textField);
```
### Steg 4.4: Ta bort flera formulärfält
Du kan också ta bort flera formulärfält samtidigt genom att ange deras namn.
```csharp
textField = collection.GetFormField<TextFormField>("Text7");
CheckBoxForm checkBoxForm = collection.GetFormField<CheckBoxForm>("Check2");
fieldManager.RemoveFormFields(new IFormField[] { textField, checkBoxForm });
```
## Steg 5: Spara det ändrade dokumentet
Efter att ha ändrat formulärfälten måste du spara dokumentet.
### Steg 5.1: Skapa sparalternativ
Ange format och spara alternativ för utdatadokumentet.
```csharp
WordProcessingFormats docFormat = WordProcessingFormats.Docx;
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(docFormat);
```
### Steg 5.2: Optimera minnesanvändningen
Om du har att göra med stora dokument kanske du vill optimera minnesanvändningen.
```csharp
saveOptions.OptimizeMemoryUsage = true;
```
### Steg 5.3: Ställ in skydd (om det behövs)
Du kan skydda dokumentet från ytterligare redigering genom att ange ett skrivlösenord.
```csharp
saveOptions.Protection = new WordProcessingProtection(WordProcessingProtectionType.AllowOnlyFormFields, "write_password");
```
### Steg 5.4: Spara dokumentet
 Spara slutligen dokumentet med a`MemoryStream`.
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(outputStream, saveOptions);
}
```

## Slutsats
Grattis! Du har tagit bort formulärfält från ett Word-dokument med GroupDocs.Editor för .NET. Detta kraftfulla bibliotek gör det enkelt att manipulera dokumentinnehåll programmatiskt, vilket sparar tid och ansträngning.
## FAQ's
### Kan jag använda GroupDocs.Editor för .NET med andra dokumentformat?
Ja, GroupDocs.Editor för .NET stöder olika dokumentformat, inklusive PDF, HTML och mer.
### Är det möjligt att lägga till formulärfält med GroupDocs.Editor för .NET?
Ja, du kan lägga till, ändra och ta bort formulärfält programmatiskt.
### Vad händer om mitt dokument är mycket stort?
Du kan aktivera minnesoptimering i sparalternativen för att hantera stora dokument effektivt.
### Kan jag använda GroupDocs.Editor för .NET i en webbapplikation?
Absolut! GroupDocs.Editor för .NET kan integreras i webbapplikationer för dokumentbehandling på serversidan.
### Var kan jag få support om jag stöter på problem?
 Du kan besöka[supportforum](https://forum.groupdocs.com/c/editor/20) för hjälp med eventuella problem.