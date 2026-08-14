---
date: '2026-06-16'
description: Leer hoe u metadata kunt extraheren, hoe u metadata in Java kunt extraheren
  en het documenttype in Java kunt detecteren met GroupDocs.Editor voor Java voor
  Word-, Excel- en tekstbestanden.
keywords:
- how to extract metadata
- java get page count
- java get document properties
- java read document info
- java detect file format
schemas:
- author: GroupDocs
  dateModified: '2026-06-16'
  description: Learn how to extract metadata, how to extract metadata in Java, and
    detect document type java with GroupDocs.Editor for Java across Word, Excel, and
    text files.
  headline: How to Extract Metadata from Documents Java using GroupDocs.Editor
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
title: Hoe metadata uit documenten in Java extraheren met GroupDocs.Editor
type: docs
url: /nl/java/advanced-features/groupdocs-editor-java-document-extraction-guide/
weight: 1
---

# Hoe metadata uit documenten Java extraheren met GroupDocs.Editor

Als je een ontwikkelaar bent die **het zat is om handmatig informatie uit Word-, Excel- of platte‑tekstbestanden te halen**, laat deze gids je zien **hoe je metadata snel en betrouwbaar kunt extraheren**. Je ziet waarom GroupDocs.Editor voor Java de go‑to bibliotheek is voor **detect document type java**, hoe je eigenschappen zoals paginatelling, auteur en encryptiestatus kunt lezen, en hoe je wachtwoord‑beveiligde bestanden kunt afhandelen — allemaal met beknopte, productie‑klare code‑fragmenten.

## Snelle antwoorden
- **Wat betekent “extract document metadata java”?** Het verwijst naar het programmatisch lezen van eigenschappen zoals formaat, paginatelling, grootte en encryptiestatus van documenten met Java.  
- **Welke bibliotheek helpt hierbij?** GroupDocs.Editor voor Java biedt een eenvoudige API voor metadata‑extractie en type‑detectie.  
- **Kan ik documenttype java detecteren als onderdeel van het proces?** Ja — door het teruggegeven `IDocumentInfo` te inspecteren kun je bepalen of een bestand een Word‑, spreadsheet‑ of tekstdocument is.  
- **Heb ik een licentie nodig?** Een gratis proefversie werkt voor evaluatie; een permanente licentie is vereist voor productiegebruik.  
- **Wat zijn de belangrijkste vereisten?** Java 8+, Maven (of handmatige JAR‑download), en basiskennis van Java.

## Wat is extract document metadata java?
**Metadata uit documenten extraheren in Java betekent het ophalen van beschrijvende informatie — zoals bestandsformaat, paginatelling, auteur of encryptiestatus — zonder de volledige documentinhoud te laden.** Deze lichtgewicht aanpak versnelt indexering, archivering en compliance‑controles door bestanden snel te analyseren, het geheugenverbruik te verminderen en weloverwogen beslissingen te nemen voordat volledige documenten worden geopend.

## Waarom GroupDocs.Editor voor Java gebruiken om document type java te detecteren?
**GroupDocs.Editor identificeert automatisch het documenttype en maakt type‑specifieke eigenschappen beschikbaar voor meer dan 30 bewerkbare formaten, en verwerkt bestanden tot 2 GB zonder de volledige inhoud in het geheugen te laden.** Het ondersteunt ook wachtwoord‑beveiligde bestanden out‑of‑the‑box, waardoor het de meest efficiënte oplossing is voor **detect document type java** scenario's.

## Vereisten
- **Java Development Kit (JDK)** 8 of nieuwer.  
- **Maven** voor afhankelijkheidsbeheer (of handmatige JAR‑download).  
- Basisvertrouwdheid met Java‑klassen en exception‑handling.  

## GroupDocs.Editor voor Java instellen

### Installatie via Maven
Voeg de repository en afhankelijkheid toe aan je `pom.xml`:

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
Download anders de nieuwste JAR vanaf [GroupDocs.Editor for Java releases](https://releases.groupdocs.com/editor/java/).

### Licentie‑acquisitie
- **Gratis proefversie** – verken de API zonder kosten.  
- **Tijdelijke licentie** – verkrijg een tijdelijk sleutel via [this link](https://purchase.groupdocs.com/temporary-license).  
- **Aankoop** – koop een permanente licentie voor productie‑implementaties.

#### Basisinitialisatie en configuratie
De `Editor`‑klasse is het toegangspunt dat een document laadt en toegang biedt tot de metadata. Nadat je een `Editor`‑instantie hebt gemaakt, kun je `getDocumentInfo(null)` aanroepen om lichte informatie op te halen.

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

## Hoe metadata extraheren in Java
Laad het document, vraag zijn `IDocumentInfo` op, en cast vervolgens naar de formaat‑specifieke info‑klasse. Dit patroon werkt voor Word-, Excel- en platte‑tekstbestanden terwijl het geheugenverbruik laag blijft, omdat alleen de documentheader wordt gelezen. Door eerst metadata te extraheren, kun je beslissen of je de volledige inhoud wilt verwerken, het bestand wilt routeren, of onondersteunde formaten wilt afwijzen.

### Functie 1: Metadata extraheren uit Word‑documenten
#### Document laden
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

### Functie 2: Detect document type java – Spreadsheets
#### Spreadsheet‑bestand laden
`SpreadsheetDocumentInfo` biedt spreadsheet‑specifieke metadata zoals aantal bladen en totale grootte.

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.IDocumentInfo;
import com.groupdocs.editor.metadata.SpreadsheetDocumentInfo;

String xlsxInputFilePath = "YOUR_DOCUMENT_DIRECTORY/SAMPLE_XLSX";
Editor editorXlsx = new Editor(xlsxInputFilePath);
```

#### Controleren en informatie extraheren
Door de `instanceof`‑operator te gebruiken kun je **detect document type java** uitvoeren en vervolgens spreadsheet‑specifieke metadata lezen, zoals blad‑aantal en totale grootte.

```java
IDocumentInfo infoXlsx = editorXlsx.getDocumentInfo(null);
if (infoXlsx instanceof SpreadsheetDocumentInfo) {
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo) infoXlsx;
    // Retrieve properties like tab count, size, etc.
}
editorXlsx.dispose();
```

*Uitleg*:  
- De `instanceof`‑controle vertelt je of het bestand een spreadsheet is, waardoor je `getSheetCount()` en andere spreadsheet‑enkel methoden kunt aanroepen.

### Functie 3: Wachtwoord‑beveiligde documenten afhandelen
#### Beschermd document laden
De `Editor`‑constructor accepteert een optioneel `LoadOptions`‑object waarin je een wachtwoord kunt opgeven.

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.IDocumentInfo;
import com.groupdocs.editor.PasswordRequiredException;
import com.groupdocs.editor.IncorrectPasswordException;

String xlsInputFilePath = "YOUR_DOCUMENT_DIRECTORY/SAMPLE_XLS_PROTECTED";
Editor editorXls = new Editor(xlsInputFilePath);
```

#### Toegang proberen met wachtwoord
Als het wachtwoord ontbreekt of onjuist is, gooit de API `PasswordRequiredException` of `IncorrectPasswordException`, zodat je de gebruiker kunt vragen om invoer of het probleem kunt loggen.

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
- De expliciete uitzonderingen van de API stellen je in staat om een elegante fallback‑logica te implementeren zonder te gokken.

### Functie 4: Metadata‑extractie voor tekst‑gebaseerde documenten
#### Tekst‑gebaseerd document laden
Voor platte‑tekstformaten (TXT, XML, CSV) geeft de `TextDocumentInfo`‑klasse codering, regelaantal en bestandsgrootte‑details terug.

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.IDocumentInfo;
import com.groupdocs.editor.metadata.TextualDocumentInfo;

String xmlInputFilePath = "YOUR_DOCUMENT_DIRECTORY/SAMPLE_XML";
Editor editorXml = new Editor(xmlInputFilePath);
```

#### Informatie extraheren en weergeven
Gebruik de getters op `TextDocumentInfo` om de lichte eigenschappen op te halen die je nodig hebt voor indexering of validatie.

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
- **Datamigratie** – Behoud originele eigenschappen bij het verplaatsen van bestanden tussen systemen, zodat naleving van regelgeving wordt gegarandeerd.

## Prestatie‑overwegingen
- **Editors vrijgeven** – Roep altijd `dispose()` aan om native resources vrij te geven en geheugenlekken te voorkomen.  
- **Grote bestanden** – Verwerk in streams of delen; `getDocumentInfo(null)` leest alleen de header, waardoor RAM‑gebruik onder 50 MB blijft, zelfs voor 2 GB‑bestanden.  
- **Profiling** – Gebruik Java‑profilers (bijv. VisualVM) om knelpunten te identificeren bij het verwerken van duizenden bestanden.

## Veelvoorkomende problemen & foutopsporing
| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| `PasswordRequiredException` zelfs wanneer bestand niet beschermd is | Verkeerd bestandspad of corrupt bestand | Controleer het pad en de integriteit van het bestand |
| `null` geretourneerd voor metadata | Een verouderde bibliotheekversie wordt gebruikt | Upgrade naar de nieuwste GroupDocs.Editor‑release |
| Lage prestaties bij grote Excel‑bestanden | Het volledige bestand wordt in het geheugen geladen | Gebruik `getDocumentInfo(null)` (alleen metadata) en verwerk in batches |

## Veelgestelde vragen

**Q: Kan ik metadata uit PDF‑bestanden extraheren met dezelfde API?**  
A: GroupDocs.Editor richt zich op bewerkbare formaten (DOCX, XLSX, enz.). Voor PDF‑bestanden gebruik je GroupDocs.Metadata of GroupDocs.Viewer.

**Q: Hoe detecteer ik het documenttype zonder te casten?**  
A: Roep `info.getDocumentType()` aan, die een enum retourneert (bijv. `DocumentType.WordProcessing`, `DocumentType.Spreadsheet`).

**Q: Is het mogelijk om aangepaste eigenschappen die in Office‑bestanden zijn ingebed te extraheren?**  
A: Ja — `WordProcessingDocumentInfo` en `SpreadsheetDocumentInfo` bieden methoden zoals `getCustomProperties()`.

**Q: Heb ik een aparte licentie nodig voor elk documenttype?**  
A: Nee, één GroupDocs.Editor‑licentie dekt alle ondersteunde formaten.

**Q: Welke Java‑versie is vereist?**  
A: Java 8 of later; nieuwere LTS‑versies (11, 17) worden volledig ondersteund.

## Conclusie
Je beschikt nu over een volledige, productie‑klare workflow voor **how to extract metadata** en **detect document type java** met GroupDocs.Editor. Integreer deze fragmenten met je eigen bedrijfslogica om archivering, compliance‑controles of elke andere situatie waarin documentinzichten waardevol zijn, te automatiseren.

---

**Last Updated:** 2026-06-16  
**Tested With:** GroupDocs.Editor 25.3 for Java  
**Author:** GroupDocs

## Gerelateerde tutorials

- [Load Word Document Java with GroupDocs.Editor – A Complete Guide](/editor/java/document-loading/load-word-document-groupdocs-editor-java/)
- [how to edit excel and Word files in Java with GroupDocs.Editor](/editor/java/document-editing/java-groupdocs-editor-master-document-editing/)
- [How to Extract Resources from Word Docs – GroupDocs.Editor Java](/editor/java/word-processing-documents/edit-extract-resources-groupdocs-editor-java/)