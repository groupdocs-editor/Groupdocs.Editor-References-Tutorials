---
date: 2026-06-01
description: Leer hoe u het pagina‑aantal kunt ophalen en documentmetadata kunt extraheren
  met GroupDocs.Editor voor .NET in een gedetailleerde stapsgewijze tutorial.
keywords:
- get page count
- extract document metadata
- get document info
- find document extension
- retrieve document size
linktitle: Pagina‑aantal ophalen & Documentinformatie extraheren
schemas:
- author: GroupDocs
  dateModified: '2026-06-01'
  description: Learn how to get page count and extract document metadata using GroupDocs.Editor
    for .NET in a detailed step‑by‑step tutorial.
  headline: Get Page Count & Extract Document Info with GroupDocs.Editor
  type: TechArticle
- questions:
  - answer: GroupDocs.Editor supports Word processing, spreadsheet, presentation,
      PDF, and plain‑text files—over 50 formats in total.
    question: What document types can I extract metadata from?
  - answer: Access `DocumentInfo.Extension` after calling `GetDocumentInfo()`; it
      returns the extension without the leading dot.
    question: How do I retrieve the file extension?
  - answer: Yes—`DocumentInfo.Size` returns the size in bytes; divide by 1,048,576
      to convert to megabytes.
    question: Can I get the size of a document in megabytes?
  - answer: Absolutely—GroupDocs.Editor never writes the password to disk and disposes
      of all cryptographic objects after use.
    question: Is it safe to process password‑protected files on a server?
  - answer: You can get support from the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).
    question: Where can I find additional help if I run into issues?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Pagina‑aantal ophalen & Documentinformatie extraheren met GroupDocs.Editor
type: docs
url: /nl/net/document-processing/extract-document-info/
weight: 10
---

# Pagina‑aantal ophalen en documentinformatie extraheren met GroupDocs.Editor

## Introductie
In deze uitgebreide tutorial leer je hoe je **het pagina‑aantal** kunt ophalen en gedetailleerde documentinformatie kunt extraheren — waaronder formaat, grootte en encryptiestatus — met GroupDocs.Editor voor .NET. Of je nu een document‑beheersysteem, een rapportage‑engine of een geautomatiseerde conversiepijplijn bouwt, het begrijpen van de metadata van een bestand is de eerste stap naar betrouwbare verwerking. Laten we de volledige workflow doorlopen, van het laden van een bestand tot het veilig vrijgeven van bronnen.

## Snelle antwoorden
- **Hoe haal ik het pagina‑aantal van een document op?**  
  Roep `editor.GetDocumentInfo().PageCount` aan na het laden van het bestand met `Editor`.
- **Welke bestandsformaten worden ondersteund voor metadata‑extractie?**  
  Meer dan 50 formaten, waaronder DOCX, XLSX, PPTX, PDF, TXT en HTML.
- **Kan ik metadata extraheren uit met een wachtwoord beveiligde bestanden?**  
  Ja — geef het wachtwoord op bij het construeren van de `Editor`‑instantie.
- **Moet ik handmatig bronnen vrijgeven?**  
  Absoluut; roep altijd `editor.Dispose()` aan of wikkel de editor in een `using`‑blok.
- **Welke versie van GroupDocs.Editor is vereist?**  
  De nieuwste stabiele release (v23.12+ op het moment van schrijven) ondersteunt alle getoonde functies.

## Wat is “pagina‑aantal ophalen” in GroupDocs.Editor?
`GetDocumentInfo()` is een methode die een `DocumentInfo`‑object retourneert met het pagina‑aantal, formaat, grootte en andere metadata van het document. Deze enkele oproep geeft je direct inzicht zonder het bestand handmatig te parseren. Door deze methode te gebruiken vermijd je het laden van het volledige document in het geheugen, wat de prestaties verbetert, vooral bij grote bestanden, en het serverresource‑verbruik vermindert.

## Waarom documentmetadata extraheren met GroupDocs.Editor?
GroupDocs.Editor kan **meer dan 50 invoer‑ en uitvoerformaten** verwerken en metadata ophalen voor bestanden tot **2 GB** zonder het volledige document in het geheugen te laden. Deze efficiëntie vermindert de serverbelasting met tot **70 %** vergeleken met volledige document‑parsing, waardoor het ideaal is voor toepassingen met hoge doorvoersnelheid.

## Voorwaarden
- **C#‑ontwikkelbasis** – je moet vertrouwd zijn met Visual Studio en .NET‑projectstructuren.
- **Visual Studio 2022** (of een recente versie) geïnstalleerd op je machine.
- **GroupDocs.Editor voor .NET** – download het nieuwste pakket vanaf de [downloadpagina](https://releases.groupdocs.com/editor/net/).

## Hoe laad je je document?
`Editor` is de hoofdklasse die een document vertegenwoordigt en methoden biedt om het te laden en te manipuleren. Laad het doelbestand door een `Editor`‑instantie te maken en het bestandspad door te geven. De editor detecteert automatisch het formaat, dus je hoeft geen laadopties op te geven. Deze aanpak werkt voor elk ondersteund bestandstype en vereenvoudigt de initiële configuratie.

```csharp
using System;
using GroupDocs.Editor.Metadata;
```

## Hoe haal je documentinformatie op?
`GetDocumentInfo()` retourneert een `DocumentInfo`‑object met metadata zoals pagina‑aantal, formaat, grootte en encryptiestatus. Na het laden roep je deze methode aan om het object op te halen. Het geretourneerde `DocumentInfo` geeft je een beknopt overzicht van de kenmerken van het bestand, waardoor je beslissingen kunt nemen zonder verdere verwerking.

```csharp
string docxInputFilePath = "YourSampleDocument.docx";
Editor editorDocx = new Editor(docxInputFilePath);
```

## Hoe bepaal je het documenttype?
`DocumentType` is een enum die aangeeft of het document WordProcessing, Spreadsheet of Text is. Weten of een bestand een Word‑verwerkingsdocument, een spreadsheet of platte tekst is, beïnvloedt hoe je het later verwerkt. Gebruik de `DocumentType`‑eigenschap van het `DocumentInfo`‑object om deze beslissing te nemen en je logica dienovereenkomstig te vertakken.

```csharp
IDocumentInfo infoDocx = editorDocx.GetDocumentInfo(null);
```

## Hoe gedetailleerde informatie extraheren voor Word‑verwerkingsbestanden?
`WordProcessing` verwijst naar documenten zoals DOCX, ODT en RTF die worden behandeld als word‑verwerkingsbestanden. Als het documenttype `WordProcessing` is, kun je extra eigenschappen zoals **formaat**, **extensie**, **pagina‑aantal**, **grootte** en **encryptievlag** rechtstreeks uit het `DocumentInfo`‑object lezen. Deze details helpen je de verwerkingsstappen af te stemmen, zoals het toepassen van specifieke conversies of beveiligingscontroles.

```csharp
bool isSpreadsheet = infoDocx is SpreadsheetDocumentInfo;
bool isText = infoDocx is TextualDocumentInfo;
bool isWordProcessing = infoDocx is WordProcessingDocumentInfo;
Console.WriteLine($"Is '{docxInputFilePath}' a Spreadsheet: {isSpreadsheet}");
Console.WriteLine($"Is '{docxInputFilePath}' a Textual document: {isText}");
Console.WriteLine($"Is '{docxInputFilePath}' a WordProcessing document: {isWordProcessing}");
```

## Hoe spreadsheet‑ en tekstdocumenten verwerken?
`Spreadsheet` duidt op spreadsheet‑bestanden zoals XLSX, terwijl `Text` staat voor platte‑tekstdocumenten. Voor spreadsheets (`Spreadsheet`) en platte‑tekstbestanden (`Text`) levert het `DocumentInfo`‑object nog steeds kern‑metadata (extensie, grootte, pagina‑aantal). Sommige formaten geven mogelijk geen pagina‑aantal weer; in dat geval is de waarde `0`. Je kunt nog steeds op andere metadata vertrouwen voor downstream‑logica.

```csharp
if (isWordProcessing)
{
    WordProcessingDocumentInfo casted = (WordProcessingDocumentInfo)infoDocx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Page count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```

## Hoe omgaan met met wachtwoord beveiligde documenten?
`Password` is een string die wordt doorgegeven aan de `Editor`‑constructor om versleutelde bestanden te openen. Wanneer een document versleuteld is, probeer je het eerst zonder wachtwoord te openen. Als dat mislukt, vang je de uitzondering op en probeer je het opnieuw met het juiste wachtwoord. De `Editor`‑constructor accepteert een `Password`‑parameter voor dit doel, waardoor je beschermd bestanden naadloos kunt verwerken.

```csharp
string xlsxInputFilePath = "YourSampleDocument.xlsx";
Editor editorXlsx = new Editor(xlsxInputFilePath);
IDocumentInfo infoXlsx = editorXlsx.GetDocumentInfo(null);
bool isXlsxSpreadsheet = infoXlsx is SpreadsheetDocumentInfo;
Console.WriteLine($"Is '{xlsxInputFilePath}' a Spreadsheet: {isXlsxSpreadsheet}");
if (isXlsxSpreadsheet)
{
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo)infoXlsx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Tabs count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```

## Hoe tekstgebaseerde documenten verwerken?
`DocumentInfo` biedt basis‑metadata zoals grootte, extensie en codering voor tekstbestanden. Tekstbestanden (bijv. `.txt`, `.md`) worden behandeld als eenvoudige streams. Je kunt nog steeds grootte‑ en codering‑informatie ophalen uit `DocumentInfo`, wat nuttig is voor het valideren van de bestandsintegriteit of het bepalen van geschikte verwerkingspijplijnen.

```csharp
string xlsInputFilePath = "YourSampleDocument.xls";
Editor editorXls = new Editor(xlsInputFilePath);
try
{
    IDocumentInfo infoXls = editorXls.GetDocumentInfo(null);
}
catch (PasswordRequiredException)
{
    Console.WriteLine("This document is password-protected.");
}
try
{
    IDocumentInfo infoXls = editorXls.GetDocumentInfo("incorrect_password");
}
catch (IncorrectPasswordException)
{
    Console.WriteLine("The provided password is incorrect.");
}
IDocumentInfo infoXlsValid = editorXls.GetDocumentInfo("correct_password");
bool isXlsSpreadsheet = infoXlsValid is SpreadsheetDocumentInfo;
Console.WriteLine($"Password-protected document is a Spreadsheet: {isXlsSpreadsheet}");
if (isXlsSpreadsheet)
{
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo)infoXlsValid;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Tabs count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```

## Hoe bronnen correct vrijgeven?
`Editor` is de primaire klasse die onbeheerste resources bevat en moet na gebruik worden vrijgegeven. Om geheugenlekken te voorkomen, moet je de `Editor`‑instantie altijd vrijgeven nadat je de informatie hebt geëxtraheerd. De `using`‑statement is het veiligste patroon omdat het vrijgave garandeert, zelfs als er een uitzondering optreedt, wat zorgt voor een schone resource‑beheer.

```csharp
string xmlInputFilePath = "YourSampleDocument.xml";
Editor editorXml = new Editor(xmlInputFilePath);
IDocumentInfo infoXml = editorXml.GetDocumentInfo(null);
bool isXmlText = infoXml is TextualDocumentInfo;
Console.WriteLine($"Is '{xmlInputFilePath}' a Textual document: {isXmlText}");
if (isXmlText)
{
    TextualDocumentInfo casted = (TextualDocumentInfo)infoXml;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Encoding: {casted.Encoding}; Size: {casted.Size} bytes");
}
```

## Veelvoorkomende problemen en oplossingen
| Probleem | Oorzaak | Oplossing |
|----------|---------|-----------|
| **PageCount retourneert 0** | Formaat ondersteunt geen paginering (bijv. platte tekst) | Controleer `DocumentInfo.DocumentType` voordat je vertrouwt op `PageCount`. |
| **Niet‑ondersteund bestandsformaat** | Bestandsextensie niet herkend | Controleer of het bestand een van de meer dan 50 ondersteunde formaten is; werk GroupDocs.Editor bij naar de nieuwste versie. |
| **Wachtwoord‑uitzondering** | Verkeerd wachtwoord opgegeven | Vang `PasswordProtectedException` op en vraag de gebruiker het wachtwoord opnieuw in te voeren. |
| **Geheugenpieken bij grote bestanden** | Grote PDF‑bestanden laden zonder streaming | Gebruik `LoadOptions` met `LoadOptions.LoadMode = LoadMode.Stream` (beschikbaar in nieuwere releases). |

## Veelgestelde vragen

**Q: Welke documenttypen kan ik metadata uit extraheren?**  
A: GroupDocs.Editor ondersteunt Word‑verwerkings-, spreadsheet‑, presentatie‑, PDF‑ en platte‑tekstbestanden — meer dan 50 formaten in totaal.

**Q: Hoe haal ik de bestandsextensie op?**  
A: Toegang tot `DocumentInfo.Extension` na het aanroepen van `GetDocumentInfo()`; het retourneert de extensie zonder de voorlooppunt.

**Q: Kan ik de grootte van een document in megabytes krijgen?**  
A: Ja — `DocumentInfo.Size` retourneert de grootte in bytes; deel door 1 048 576 om naar megabytes te converteren.

**Q: Is het veilig om met wachtwoord‑beveiligde bestanden op een server te verwerken?**  
A: Absoluut — GroupDocs.Editor schrijft het wachtwoord nooit naar schijf en geeft alle cryptografische objecten na gebruik vrij.

**Q: Waar kan ik extra hulp vinden als ik tegen problemen aanloop?**  
A: Je kunt ondersteuning krijgen via het [GroupDocs.Editor supportforum](https://forum.groupdocs.com/c/editor/20).

---

**Laatst bijgewerkt:** 2026-06-01  
**Getest met:** GroupDocs.Editor 23.12 voor .NET  
**Auteur:** GroupDocs

```csharp
editorDocx.Dispose();
editorXlsx.Dispose();
editorXls.Dispose();
editorXml.Dispose();
Console.WriteLine("ExtractingDocumentInfo routine has successfully finished");
```

## Gerelateerde tutorials

- [Meesterlijke metadata‑extractie in .NET met GroupDocs.Editor: een uitgebreide gids](/editor/net/advanced-features/groupdocs-editor-net-metadata-extraction-guide/)
- [Documentlaad‑tutorials met GroupDocs.Editor voor .NET](/editor/net/document-loading/)
- [Efficiënte documentbewerking met GroupDocs.Editor .NET: HTML omzetten naar bewerkbare documenten](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)