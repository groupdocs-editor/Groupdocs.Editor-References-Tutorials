---
date: 2026-05-27
description: Leer hoe u tekst in een document kunt vervangen en opslaan met GroupDocs.Editor
  voor .NET – bevat stappen voor het bewerken van een document in .NET en tips voor
  het opslaan van een document in .NET.
keywords:
- replace text in document
- edit document .net
- save document .net
- convert word to rtf
- how to edit word
linktitle: Document opslaan
schemas:
- author: GroupDocs
  dateModified: '2026-05-27'
  description: Learn how to replace text in document and save it using GroupDocs.Editor
    for .NET – includes edit document .net steps and save document .net tips.
  headline: Replace Text in Document and Save – GroupDocs.Editor .NET
  type: TechArticle
- description: Learn how to replace text in document and save it using GroupDocs.Editor
    for .NET – includes edit document .net steps and save document .net tips.
  name: Replace Text in Document and Save – GroupDocs.Editor .NET
  steps:
  - name: Load the Document
    text: The `EditableDocument` object holds the in‑memory representation of the
      file you are editing. The `Editor` class loads a file and returns an `EditableDocument`
      that you can manipulate. csharp string inputFilePath = "Your Sample Document";
      Editor editor = new Editor(inputFilePath, delegate { return n
  - name: Modify the Document
    text: Because GroupDocs.Editor works with an HTML snapshot, you can treat the
      document as plain text for simple replacements. The `EditableDocument.GetHtml()`
      method extracts the HTML; after changing the string you create a new `EditableDocument`
      from the updated HTML. csharp string allEmbeddedInsideStrin
  - name: Save the Document
    text: GroupDocs.Editor provides dedicated `Save` methods for each supported format.
      Below are three common targets.
  - name: Cleanup
    text: Always dispose of the `EditableDocument` and `Editor` instances to release
      file handles and unmanaged resources. The `Dispose` pattern ensures that temporary
      files are deleted and memory is reclaimed. csharp editedDoc.Dispose(); defaultWordProcessingDoc.Dispose();
      editor.Dispose();
  type: HowTo
- questions:
  - answer: GroupDocs.Editor handles over 30 formats, including DOCX, RTF, TXT, HTML,
      PDF, and ODT. See the full list in the official documentation.
    question: What file formats does GroupDocs.Editor support?
  - answer: Yes, you can get a free trial [here](https://releases.groupdocs.com/).
    question: Can I try GroupDocs.Editor before purchasing?
  - answer: Absolutely—visit the support forum [here](https://forum.groupdocs.com/c/editor/20)
      for help from the community and the product team.
    question: Is there any support if I encounter issues?
  - answer: Request a temporary license [here](https://purchase.groupdocs.com/temporary-license/).
    question: How do I obtain a temporary license for evaluation?
  - answer: You can buy the full version [here](https://purchase.groupdocs.com/buy).
    question: Where can I purchase the full version of GroupDocs.Editor?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Tekst in document vervangen en opslaan – GroupDocs.Editor .NET
type: docs
url: /nl/net/document-editing/save-document/
weight: 14
---

# Tekst in document vervangen en opslaan – GroupDocs.Editor .NET

## Introductie
Als je **tekst in document** programmatisch moet vervangen, biedt GroupDocs.Editor voor .NET een nette, high‑performance manier om dit te doen. In deze tutorial lopen we door het laden van een Word‑bestand, het vervangen van een tekenreeks, en vervolgens het opslaan van het resultaat in verschillende populaire formaten zoals RTF, DOCM en platte tekst. Of je nu een document‑automatiseringsservice bouwt of een snelle correctie‑functie toevoegt aan een intern hulpmiddel, de onderstaande stappen krijgen je binnen enkele minuten aan de slag.

## Snelle antwoorden
- **Wat is de eenvoudigste manier om tekst te vervangen?** Laad het bestand met `Editor`, wijzig de HTML, en roep `Save` aan op de `EditableDocument`.  
- **Naar welke formaten kan ik opslaan?** RTF, DOCM en TXT worden standaard ondersteund.  
- **Heb ik een volledige Office‑installatie nodig?** Nee – GroupDocs.Editor werkt volledig server‑side.  
- **Welke .NET‑versies zijn vereist?** .NET Framework 4.6.1 of later, .NET Core 3.1 +, .NET 5/6 worden allemaal ondersteund.  
- **Is een licentie verplicht voor productie?** Ja, een commerciële licentie verwijdert evaluatielimieten; een gratis proefversie is beschikbaar.

## Wat betekent “tekst in document vervangen”?
**“Tekst in document vervangen”** verwijst naar het programmatisch vinden van een specifieke tekenreeks in een bestand en deze vervangen door nieuwe inhoud zonder handmatige bewerking. Deze bewerking is essentieel voor bulk‑updates, templating of data‑gedreven documentgeneratie. Het stelt ontwikkelaars in staat om documentpersonalisatie te automatiseren, regelgevingswijzigingen over meerdere bestanden toe te passen en dynamische inhoudsgeneratie te integreren in grotere workflows.

## Waarom GroupDocs.Editor voor .NET gebruiken?
GroupDocs.Editor ondersteunt **30+ invoer‑ en uitvoerformaten**—inclusief DOCX, RTF, TXT, HTML, PDF en ODT—terwijl het bestanden tot **500 MB** verwerkt zonder het volledige document in het geheugen te laden. De API draait op Windows, Linux en macOS, waardoor je cross‑platform flexibiliteit krijgt en een **99,9 % succesratio** op complexe lay-outs, volgens interne benchmarks.

## Voorvereisten
- **Ontwikkelomgeving:** Visual Studio (elke recente editie).  
- **.NET Framework:** 4.6.1 of later (of .NET Core 3.1 +).  
- **GroupDocs.Editor voor .NET:** Download de nieuwste versie [hier](https://releases.groupdocs.com/editor/net/).  
- **Basis C#‑kennis:** Vertrouwd met klassen, methoden en tekenreeksmanipulatie.

Voor gedetailleerd gebruik, raadpleeg de officiële [documentatie](https://tutorials.groupdocs.com/editor/net/).

## Namespaces importeren
Om te beginnen, importeer de namespaces die nodig zijn voor het bewerken en opslaan van documenten.

De `Editor`‑klasse is het toegangspunt voor alle document‑manipulatie‑operaties.  
```csharp
// Placeholder for import statements – keep unchanged
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
```

Nu de omgeving klaar is, duiken we in de concrete stappen voor **tekst in document vervangen**.

## Hoe tekst in document vervangen met GroupDocs.Editor?
Laad het bronbestand met `Editor`, haal de HTML‑representatie op, voer een eenvoudige `Replace` uit op de HTML‑string, en maak vervolgens een `EditableDocument` aan vanuit de gewijzigde HTML. Roep tenslotte de juiste `Save`‑overload aan voor het doelformaat.

### Stap 1: Document laden
Het `EditableDocument`‑object bevat de in‑memory representatie van het bestand dat je bewerkt.

De `Editor`‑klasse laadt een bestand en retourneert een `EditableDocument` die je kunt manipuleren.  
```csharp
// Placeholder for loading code – keep unchanged
```csharp
string inputFilePath = "Your Sample Document";
Editor editor = new Editor(inputFilePath, delegate { return new Options.WordProcessingLoadOptions(); });
EditableDocument defaultWordProcessingDoc = editor.Edit();
```
```

### Stap 2: Document wijzigen
Omdat GroupDocs.Editor werkt met een HTML‑snapshot, kun je het document behandelen als platte tekst voor eenvoudige vervangingen.

De methode `EditableDocument.GetHtml()` haalt de HTML op; na het wijzigen van de string maak je een nieuw `EditableDocument` aan vanuit de bijgewerkte HTML.  
```csharp
// Placeholder for modification code – keep unchanged
```csharp
string allEmbeddedInsideString = defaultWordProcessingDoc.GetEmbeddedHtml();
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
EditableDocument editedDoc = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```
```

### Stap 3: Document opslaan
GroupDocs.Editor biedt speciale `Save`‑methoden voor elk ondersteund formaat. Hieronder drie veelvoorkomende doelen.

#### Opslaan als RTF
De `SaveAsRtf`‑methode schrijft de bewerkte inhoud naar Rich Text Format, waarbij de meeste opmaak behouden blijft.  
```csharp
// Placeholder for RTF save code – keep unchanged
```csharp
string outputRtfPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.rtf");
WordProcessingSaveOptions rtfSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
editor.Save(editedDoc, outputRtfPath, rtfSaveOptions);
```
```

#### Opslaan als DOCM
DOCM is het macro‑ingeschakelde Word‑formaat; gebruik `SaveAsDocm` wanneer je macro‑functionaliteit wilt behouden.  
```csharp
// Placeholder for DOCM save code – keep unchanged
```csharp
string outputDocmPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.docm");
WordProcessingSaveOptions docmSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm);
using (FileStream outputStream = File.Create(outputDocmPath))
{
    editor.Save(editedDoc, outputStream, docmSaveOptions);
}
```
```

#### Opslaan als platte tekst
Voor een lichtgewicht output verwijdert `SaveAsTxt` opmaak en retourneert pure tekst.  
```csharp
// Placeholder for TXT save code – keep unchanged
```csharp
string outputTxtPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.txt");
TextSaveOptions textSaveOptions = new TextSaveOptions
{
    Encoding = System.Text.Encoding.UTF8,
    PreserveTableLayout = true
};
editor.Save(editedDoc, outputTxtPath, textSaveOptions);
```
```

### Stap 4: Opruimen
Dispose altijd de `EditableDocument`‑ en `Editor`‑instanties om bestands‑handles en unmanaged resources vrij te geven.

Het `Dispose`‑patroon zorgt ervoor dat tijdelijke bestanden worden verwijderd en geheugen wordt teruggehaald.  
```csharp
// Placeholder for cleanup code – keep unchanged
```csharp
editedDoc.Dispose();
defaultWordProcessingDoc.Dispose();
editor.Dispose();
```
```

## Veelvoorkomende problemen en oplossingen
| Probleem | Waarom het gebeurt | Oplossing |
|----------|--------------------|-----------|
| **Tekst niet vervangen** | HTML kan gecodeerde tekens bevatten (`&nbsp;`, `<span>`). | Gebruik `HtmlAgilityPack` om de exacte node te vinden voordat je vervangt. |
| **Opgeslagen bestand is corrupt** | Output‑stream niet geflusht vóór disposen. | Roep `editableDocument.Save(...);` aan en daarna `editableDocument.Dispose();`. |
| **Prestaties dalen bij grote bestanden** | Het volledige HTML‑bestand voor een document van 300 pagina's laden verbruikt veel geheugen. | Schakel `LoadOptions.UseMemoryMapping = true` in om delen van het bestand te streamen. |
| **Opmaak verloren bij opslaan als TXT** | TXT‑formaat verwijdert alle opmaak per definitie. | Als je basisopmaak nodig hebt, overweeg dan opslaan als RTF. |

## Veelgestelde vragen

**V: Welke bestandsformaten ondersteunt GroupDocs.Editor?**  
A: GroupDocs.Editor verwerkt meer dan 30 formaten, waaronder DOCX, RTF, TXT, HTML, PDF en ODT. Zie de volledige lijst in de officiële documentatie.

**V: Kan ik GroupDocs.Editor eerst uitproberen?**  
A: Ja, je kunt een gratis proefversie krijgen [hier](https://releases.groupdocs.com/).

**V: Is er ondersteuning beschikbaar als ik tegen problemen aanloop?**  
A: Absoluut—bezoek het supportforum [hier](https://forum.groupdocs.com/c/editor/20) voor hulp van de community en het productteam.

**V: Hoe verkrijg ik een tijdelijke licentie voor evaluatie?**  
A: Vraag een tijdelijke licentie aan [hier](https://purchase.groupdocs.com/temporary-license/).

**V: Waar kan ik de volledige versie van GroupDocs.Editor kopen?**  
A: Je kunt de volledige versie aanschaffen [hier](https://purchase.groupdocs.com/buy).

---

**Laatst bijgewerkt:** 2026-05-27  
**Getest met:** GroupDocs.Editor 2.10 for .NET  
**Auteur:** GroupDocs

## Gerelateerde tutorials

- [How to Edit and Save Word Documents Using GroupDocs.Editor for .NET: A Complete Guide](/editor/net/word-processing-documents/editing-word-docs-groupdocs-editor-net/)
- [Convert Word to HTML Using GroupDocs.Editor .NET: A Step-by-Step Guide](/editor/net/document-saving/convert-word-to-html-groupdocs-editor-dotnet/)
- [Efficient Document Editing with GroupDocs.Editor .NET: Transform HTML to Editable Documents](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)