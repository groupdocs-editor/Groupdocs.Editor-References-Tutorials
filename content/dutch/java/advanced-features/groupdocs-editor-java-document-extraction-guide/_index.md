---
date: '2026-10-27'
description: Leer hoe u metadata kunt extraheren, hoe u metadata in Java kunt extraheren
  en het documenttype in Java kunt detecteren met GroupDocs.Editor voor Java voor
  Word-, Excel- en tekstbestanden.
keywords:
- how to extract metadata
- java detect file format
- groupdocs editor metadata
- get page count java
- java get document info
lastmod: '2026-10-27'
og_description: Leer hoe u metadata in Java kunt extraheren, het documenttype kunt
  detecteren en eigenschappen zoals paginatelling kunt lezen met GroupDocs.Editor
  – een snelle, geheugen‑efficiënte oplossing.
og_image_alt: Guide showing Java code extracting document metadata with GroupDocs.Editor
og_title: Hoe metadata uit documenten in Java te extraheren met GroupDocs.Editor
schemas:
- author: GroupDocs
  dateModified: '2026-10-27'
  description: Learn how to extract metadata, how to extract metadata in Java, and
    detect document type java with GroupDocs.Editor for Java across Word, Excel, and
    text files.
  headline: How to extract metadata from Documents Java using GroupDocs.Editor
  type: TechArticle
- questions:
  - answer: GroupDocs.Editor focuses on editable formats (DOCX, XLSX, etc.). For PDFs,
      use GroupDocs.Metadata or GroupDocs.Viewer.
    question: Can I extract metadata from PDF files with the same API?
  - answer: Call `info.getDocumentType()` which returns an enum (e.g., `DocumentType.WordProcessing`,
      `DocumentType.Spreadsheet`).
    question: How do I detect the document type without casting?
  - answer: Yes—`WordProcessingDocumentInfo` and `SpreadsheetDocumentInfo` expose
      methods like `getCustomProperties()`.
    question: Is it possible to extract custom properties embedded in Office files?
  - answer: No, a single GroupDocs.Editor license covers all supported formats.
    question: Do I need a separate license for each document type?
  - answer: Java 8 or later; newer LTS versions (11, 17) are fully supported.
    question: What Java version is required?
  type: FAQPage
tags:
- extract metadata
- GroupDocs.Editor
- Java document processing
- document type detection
- metadata extraction
title: Hoe metadata uit documenten in Java te extraheren met GroupDocs.Editor
type: docs
url: /nl/java/advanced-features/groupdocs-editor-java-document-extraction-guide/
weight: 1
---

# Hoe metadata uit documenten Java te extraheren met GroupDocs.Editor

Als je een ontwikkelaar bent die **het zat is om handmatig informatie uit Word-, Excel- of platte‑tekstbestanden te halen**, laat deze gids je **hoe je metadata kunt extraheren** snel en betrouwbaar zien. Je zult ontdekken waarom GroupDocs.Editor voor Java de go‑to bibliotheek is voor **detect document type java**, hoe je eigenschappen zoals paginatelling, auteur en encryptiestatus kunt lezen, en hoe je omgaat met wachtwoord‑beveiligde bestanden — allemaal met beknopte, productie‑klare code‑fragmenten.

## Snelle antwoorden
- **Wat betekent “extract document metadata java”?** Het verwijst naar het programmatisch lezen van eigenschappen zoals formaat, paginatelling, grootte en encryptiestatus van documenten met Java.  
- **Welke bibliotheek helpt hierbij?** GroupDocs.Editor voor Java biedt een eenvoudige API voor metadata‑extractie en type‑detectie.  
- **Kan ik documenttype java detecteren als onderdeel van het proces?** Ja — door het teruggegeven `IDocumentInfo` te inspecteren kun je bepalen of een bestand een Word-, spreadsheet‑ of tekstdocument is.  
- **Heb ik een licentie nodig?** Een gratis proefversie werkt voor evaluatie; een permanente licentie is vereist voor productiegebruik.  
- **Wat zijn de belangrijkste vereisten?** Java 8+, Maven (of handmatige JAR‑download), en basiskennis van Java.

## Wat is metadata extraheren?
`IDocumentInfo` is een interface die generieke metadata voor elk ondersteund document vertegenwoordigt.  
Metadata van documenten extraheren in Java betekent het ophalen van beschrijvende informatie zoals bestandsformaat, paginatelling, auteur of encryptiestatus **zonder de volledige documentinhoud te laden**. Deze lichtgewicht aanpak versnelt indexering, archivering en compliance‑controles door je in staat te stellen bestanden snel te analyseren, het geheugenverbruik te verminderen en weloverwogen beslissingen te nemen voordat volledige documenten worden geopend.

## Waarom GroupDocs.Editor voor Java gebruiken om documenttype java te detecteren?
GroupDocs.Editor identificeert automatisch het documenttype en maakt type‑specifieke eigenschappen beschikbaar voor **meer dan 30 bewerkbare formaten**, en verwerkt bestanden tot **2 GB** terwijl alleen de header wordt gelezen. Het behandelt ook wachtwoord‑beveiligde bestanden direct, waardoor het de meest efficiënte oplossing is voor **detect document type java** scenario's.

## Voorvereisten
- **Java Development Kit (JDK)** 8 of nieuwer.  
- **Maven** voor afhankelijkheidsbeheer (of handmatige JAR‑download).  
- Basiskennis van Java‑klassen en exception‑handling.  

## GroupDocs.Editor voor Java instellen

### Installatie via Maven
Add the repository and dependency to your `pom.xml`:

```xml
<repositories>
   <repository>
      <id>repository.groupdocs.com</id>
      <name>GroupDocs Repository</name>
      <url>https://releases.groupdocs.com/editor/java/</url>
   </repository>
</repositories>

<dependencies>
   <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-editor</artifactId>
      <version>25.3</version>
   </dependency>
</dependencies>
```

### Directe download
Alternatively, download the latest JAR from [GroupDocs.Editor for Java releases](https://releases.groupdocs.com/editor/java/).

### Licentie‑acquisitie
- **Gratis proefversie** – verken de API zonder kosten.  
- **Tijdelijke licentie** – verkrijg een tijd‑beperkte sleutel via [this link](https://purchase.groupdocs.com/temporary-license).  
- **Aankoop** – koop een permanente licentie voor productie‑implementaties.

#### Basisinitialisatie en configuratie
De `Editor`‑klasse is het toegangspunt dat een document laadt en toegang biedt tot de metadata. Na het aanmaken van een `Editor`‑instance kun je `getDocumentInfo(null)` aanroepen om lichtgewicht informatie op te halen.  
`getDocumentInfo(null)` haalt alleen de metadata van het document op zonder de volledige inhoud te laden.

## Hoe metadata te extraheren in Java
Laad het document, vraag zijn `IDocumentInfo` op, en cast vervolgens naar de formaat‑specifieke info‑klasse.

### Functie 1: Metadata extraheren uit Word‑documenten
#### Het document laden
De `DocumentInfo`‑interface vertegenwoordigt generieke metadata voor elk ondersteund bestand. Het doorgeven van het bestandspad aan de `Editor`‑constructor bereidt het document voor inspectie voor.

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.IDocumentInfo;
import com.groupdocs.editor.metadata.WordProcessingDocumentInfo;

String docxInputFilePath = "YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX";
Editor editorDocx = new Editor(docxInputFilePath);
```

#### Documentinformatie extraheren
`WordProcessingDocumentInfo` is een concrete implementatie die Word‑specifieke eigenschappen toevoegt, zoals paginatelling, auteur en encryptiestatus.

```java
IDocumentInfo infoDocx = editorDocx.getDocumentInfo(null);
if (infoDocx instanceof WordProcessingDocumentInfo) {
    WordProcessingDocumentInfo casted = (WordProcessingDocumentInfo) infoDocx;
    // Access properties like format, page count, and more
}
editorDocx.dispose();
```

*Uitleg*:  
- `getDocumentInfo(null)` haalt metadata op zonder de volledige documentbody te laden.  
- Casten naar `WordProcessingDocumentInfo` ontgrendelt Word‑specifieke attributen zoals **paginatelling**, auteursnaam en encryptievlag.

### Functie 2: Documenttype java detecteren – spreadsheets
#### Het spreadsheet‑bestand laden
`SpreadsheetDocumentInfo` biedt spreadsheet‑specifieke metadata zoals aantal bladen en totale grootte.

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.IDocumentInfo;
import com.groupdocs.editor.metadata.SpreadsheetDocumentInfo;

String xlsxInputFilePath = "YOUR_DOCUMENT_DIRECTORY/SAMPLE_XLSX";
Editor editorXlsx = new Editor(xlsxInputFilePath);
```

#### Controleer en extraheer informatie
Door de `instanceof`‑operator te gebruiken kun je **documenttype java detecteren** en vervolgens spreadsheet‑specifieke metadata lezen, zoals aantal bladen en totale grootte.  
`getSheetCount()` retourneert het aantal werkbladen in de spreadsheet.

```java
IDocumentInfo infoXlsx = editorXlsx.getDocumentInfo(null);
if (infoXlsx instanceof SpreadsheetDocumentInfo) {
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo) infoXlsx;
    // Retrieve properties like tab count, size, etc.
}
editorXlsx.dispose();
```

*Uitleg*:  
- De `instanceof`‑controle vertelt je of het bestand een spreadsheet is, waardoor je `getSheetCount()` en andere alleen‑voor‑spreadsheets methoden kunt aanroepen.

### Functie 3: Omgaan met wachtwoord‑beveiligde documenten
#### Het beveiligde document laden
De `Editor`‑constructor accepteert een optioneel `LoadOptions`‑object waarin je een wachtwoord kunt opgeven.

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.IDocumentInfo;
import com.groupdocs.editor.PasswordRequiredException;
import com.groupdocs.editor.IncorrectPasswordException;

String xlsInputFilePath = "YOUR_DOCUMENT_DIRECTORY/SAMPLE_XLS_PROTECTED";
Editor editorXls = new Editor(xlsInputFilePath);
```

#### Probeer toegang met wachtwoord
Als het wachtwoord ontbreekt of onjuist is, gooit de API `PasswordRequiredException` of `IncorrectPasswordException`, waardoor je de gebruiker kunt vragen om een wachtwoord of het probleem kunt loggen.  
`PasswordRequiredException` wordt gegooid wanneer een document een wachtwoord vereist maar er geen is opgegeven.  
`IncorrectPasswordException` geeft aan dat het opgegeven wachtwoord niet overeenkomt met het document.

```java
try {
    IDocumentInfo infoXls = editorXls.getDocumentInfo(null); // Attempt without password
} catch (PasswordRequiredException ex) {
    System.out.println("A password is required to access this document.");
}

try {
    IDocumentInfo infoXls = editorXls.getDocumentInfo("incorrect_password");
} catch (IncorrectPasswordException ex) {
    System.out.println("The provided password is incorrect. Please try again.");
}

IDocumentInfo infoXls = editorXls.getDocumentInfo("excel_password"); // Correct password
if (infoXls instanceof SpreadsheetDocumentInfo) {
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo) infoXls;
    // Extract document details
}
editorXls.dispose();
```

*Uitleg*:  
- De expliciete exceptions van de API laten je een elegante fallback‑logica implementeren zonder te gokken.

### Functie 4: Metadata‑extractie van tekst‑gebaseerde documenten
#### Het tekst‑gebaseerde document laden
Voor platte‑tekstformaten (TXT, XML, CSV) geeft de `TextDocumentInfo`‑klasse codering, regel‑telling en bestandsgrootte‑details terug.

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.IDocumentInfo;
import com.groupdocs.editor.metadata.TextualDocumentInfo;

String xmlInputFilePath = "YOUR_DOCUMENT_DIRECTORY/SAMPLE_XML";
Editor editorXml = new Editor(xmlInputFilePath);
```

#### Informatie extraheren en weergeven
Gebruik de getters op `TextDocumentInfo` om de lichtgewicht eigenschappen op te halen die je nodig hebt voor indexering of validatie.

```java
IDocumentInfo infoXml = editorXml.getDocumentInfo(null);
if (infoXml instanceof TextualDocumentInfo) {
    TextualDocumentInfo casted1 = (TextualDocumentInfo) infoXml;
    // Access encoding, size, etc.
}
editorXml.dispose();
```

*Uitleg*:  
- Deze aanpak werkt voor platte‑tekstformaten waarbij je voornamelijk codering en bestandsgrootte‑metadata nodig hebt.

## Praktische toepassingen
- **Geautomatiseerde documentarchivering** – Haal metadata op om bestanden te taggen en op te slaan in een doorzoekbare repository.  
- **Workflow‑automatisering** – Gebruik metadata om documenten naar de juiste afdeling te routeren of downstream processen te activeren.  
- **Datamigratie** – Behoud originele eigenschappen bij het verplaatsen van bestanden tussen systemen, waardoor naleving van regelgeving wordt gegarandeerd.

## Prestatie‑overwegingen
- **Editors vrijgeven** – Roep altijd `dispose()` aan om native resources vrij te maken en geheugenlekken te voorkomen.  
- **Grote bestanden** – Verwerk in streams of chunks; `getDocumentInfo(null)` leest alleen de header, waardoor RAM‑gebruik onder **50 MB** blijft, zelfs voor **2 GB** bestanden.  
- **Profiling** – Gebruik Java‑profilers (bijv. VisualVM) om knelpunten te vinden bij het verwerken van duizenden bestanden.

## Veelvoorkomende problemen & probleemoplossing
| Symptoom | Waarschijnlijke oorzaak | Oplossing |
|----------|--------------------------|-----------|
| `PasswordRequiredException` zelfs al is het bestand niet beveiligd | Verkeerd bestandspad of beschadigd bestand | Controleer het pad en de integriteit van het bestand |
| `null` geretourneerd voor metadata | Gebruik van een verouderde bibliotheekversie | Upgrade naar de nieuwste GroupDocs.Editor release |
| Lage prestaties bij grote Excel‑bestanden | Het volledige bestand in het geheugen laden | Gebruik `getDocumentInfo(null)` (alleen metadata) en verwerk in batches |

## Veelgestelde vragen

**Q: Kan ik metadata uit PDF‑bestanden extraheren met dezelfde API?**  
A: GroupDocs.Editor richt zich op bewerkbare formaten (DOCX, XLSX, enz.). Voor PDF's gebruik je GroupDocs.Metadata of GroupDocs.Viewer.

**Q: Hoe detecteer ik het documenttype zonder te casten?**  
A: Roep `info.getDocumentType()` aan, die een enum retourneert (bijv. `DocumentType.WordProcessing`, `DocumentType.Spreadsheet`).

**Q: Is het mogelijk om aangepaste eigenschappen die in Office‑bestanden zijn ingebed te extraheren?**  
A: Ja — `WordProcessingDocumentInfo` en `SpreadsheetDocumentInfo` bieden methoden zoals `getCustomProperties()`.

**Q: Heb ik een aparte licentie nodig voor elk documenttype?**  
A: Nee, één GroupDocs.Editor‑licentie dekt alle ondersteunde formaten.

**Q: Welke Java‑versie is vereist?**  
A: Java 8 of hoger; nieuwere LTS‑versies (11, 17) worden volledig ondersteund.

## Conclusie
Je hebt nu een volledige, productie‑klare workflow voor **hoe metadata te extraheren** en **documenttype java te detecteren** met GroupDocs.Editor. Integreer deze fragmenten met je eigen bedrijfslogica om archivering, compliance‑controles of elke situatie waarin documentinzichten waardevol zijn, te automatiseren.

---

**Laatst bijgewerkt:** 2026-10-27  
**Getest met:** GroupDocs.Editor 25.3 for Java  
**Auteur:** GroupDocs

## Gerelateerde tutorials

- [Word‑document laden in Java met GroupDocs.Editor – Een volledige gids](/editor/java/document-loading/load-word-document-groupdocs-editor-java/)
- [Hoe Excel‑ en Word‑bestanden te bewerken in Java met GroupDocs.Editor](/editor/java/document-editing/java-groupdocs-editor-master-document-editing/)
- [Hoe bronnen uit Word‑documenten te extraheren – GroupDocs.Editor Java](/editor/java/word-processing-documents/edit-extract-resources-groupdocs-editor-java/)

```java
import com.groupdocs.editor.Editor;

public class DocumentEditorSetup {
    public static void main(String[] args) {
        String filePath = "YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX";
        Editor editor = new Editor(filePath);
        // Initialize your document processing workflow here
        editor.dispose();
    }
}
```