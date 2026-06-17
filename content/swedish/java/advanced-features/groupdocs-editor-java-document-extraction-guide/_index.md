---
date: '2026-06-16'
description: Lär dig hur du extraherar metadata, hur du extraherar metadata i Java,
  och upptäcker dokumenttyp i Java med GroupDocs.Editor för Java för Word, Excel och
  textfiler.
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
title: Hur man extraherar metadata från dokument i Java med GroupDocs.Editor
type: docs
url: /sv/java/advanced-features/groupdocs-editor-java-document-extraction-guide/
weight: 1
---

# Hur man extraherar metadata från dokument Java med GroupDocs.Editor

Om du är en utvecklare som är **trött på att manuellt hämta information från Word-, Excel- eller rena textfiler**, visar den här guiden dig **hur du extraherar metadata** snabbt och pålitligt. Du kommer att se varför GroupDocs.Editor för Java är det självklara biblioteket för **detect document type java**, hur du läser egenskaper som sidantal, författare och krypteringsstatus, och hur du hanterar lösenordsskyddade filer — allt med koncisa, produktionsklara kodexempel.

## Snabba svar
- **Vad betyder “extract document metadata java”?** Det avser att programmässigt läsa egenskaper såsom format, sidantal, storlek och krypteringsstatus från dokument med Java.  
- **Vilket bibliotek hjälper med detta?** GroupDocs.Editor för Java tillhandahåller ett enkelt API för metadataextraktion och typdetektering.  
- **Kan jag upptäcka dokumenttyp java som en del av processen?** Ja — genom att inspektera det returnerade `IDocumentInfo` kan du avgöra om en fil är ett Word-, kalkylblad- eller textdokument.  
- **Behöver jag en licens?** En gratis provperiod fungerar för utvärdering; en permanent licens krävs för produktionsanvändning.  
- **Vad är de viktigaste förutsättningarna?** Java 8+, Maven (eller manuell JAR‑nedladdning) och grundläggande Java‑kunskaper.

## Vad är extract document metadata java?
**Att extrahera dokumentmetadata i Java innebär att hämta beskrivande information — som filformat, sidantal, författare eller krypteringsstatus — utan att ladda hela dokumentets innehåll.** Denna lätta metod påskyndar indexering, arkivering och efterlevnadskontroller genom att låta dig analysera filer snabbt, minska minnesförbrukningen och fatta informerade beslut innan hela dokument öppnas.

## Varför använda GroupDocs.Editor för Java för att detect document type java?
**GroupDocs.Editor identifierar automatiskt dokumenttypen och exponerar typ‑specifika egenskaper för över 30 redigerbara format, och bearbetar filer upp till 2 GB utan att ladda hela innehållet i minnet.** Det hanterar också lösenordsskyddade filer direkt, vilket gör det till den mest effektiva lösningen för **detect document type java**‑scenarier.

## Förutsättningar
- **Java Development Kit (JDK)** 8 eller nyare.  
- **Maven** för beroendehantering (eller manuell JAR‑nedladdning).  
- Grundläggande kunskap om Java‑klasser och undantagshantering.  

## Konfigurera GroupDocs.Editor för Java

### Installation via Maven
Lägg till repository och beroende i din `pom.xml`:

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

### Direkt nedladdning
Alternativt, ladda ner den senaste JAR‑filen från [GroupDocs.Editor for Java releases](https://releases.groupdocs.com/editor/java/).

### Licensanskaffning
- **Free Trial** – utforska API:t utan kostnad.  
- **Temporary License** – skaffa en tidsbegränsad nyckel via [this link](https://purchase.groupdocs.com/temporary-license).  
- **Purchase** – köp en permanent licens för produktionsdistributioner.

#### Grundläggande initiering och konfiguration
`Editor`‑klassen är ingångspunkten som laddar ett dokument och ger åtkomst till dess metadata. Efter att ha skapat en `Editor`‑instans kan du anropa `getDocumentInfo(null)` för att hämta lättviktig information.

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

## Hur man extraherar metadata i Java
Läs in dokumentet, begär dess `IDocumentInfo` och kasta sedan till den format‑specifika informationsklassen. Detta mönster fungerar för Word-, Excel- och rena textfiler samtidigt som minnesanvändningen hålls låg, eftersom endast dokumenthuvudet läses. Genom att först extrahera metadata kan du avgöra om du ska bearbeta hela innehållet, dirigera filen eller avvisa format som inte stöds.

### Funktion 1: Extrahera metadata från Word‑dokument
#### Läs in dokumentet
`DocumentInfo`‑gränssnittet representerar generisk metadata för alla stödda filer. Att skicka filvägen till `Editor`‑konstruktorn förbereder dokumentet för inspektion.

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.IDocumentInfo;
import com.groupdocs.editor.metadata.WordProcessingDocumentInfo;

String docxInputFilePath = "YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX";
Editor editorDocx = new Editor(docxInputFilePath);
```

#### Extrahera dokumentinformation
`WordProcessingDocumentInfo` är en konkret implementation som lägger till Word‑specifika egenskaper såsom sidantal, författare och krypteringsstatus.

```java
IDocumentInfo infoDocx = editorDocx.getDocumentInfo(null);
if (infoDocx instanceof WordProcessingDocumentInfo) {
    WordProcessingDocumentInfo casted = (WordProcessingDocumentInfo) infoDocx;
    // Access properties like format, page count, and more
}
editorDocx.dispose();
```

*Förklaring*:  
- `getDocumentInfo(null)` hämtar metadata utan att ladda hela dokumentkroppen.  
- Att kasta till `WordProcessingDocumentInfo` låser upp Word‑specifika attribut som **page count**, författarnamn och krypteringsflagga.

### Funktion 2: Detect document type java – Kalkylblad
#### Läs in kalkylbladsfilen
`SpreadsheetDocumentInfo` tillhandahåller kalkylblads‑specifik metadata som bladantal och total storlek.

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.IDocumentInfo;
import com.groupdocs.editor.metadata.SpreadsheetDocumentInfo;

String xlsxInputFilePath = "YOUR_DOCUMENT_DIRECTORY/SAMPLE_XLSX";
Editor editorXlsx = new Editor(xlsxInputFilePath);
```

#### Kontrollera och extrahera information
Genom att använda `instanceof`‑operatorn kan du **detect document type java** och sedan läsa kalkylblads‑specifik metadata såsom bladantal och total storlek.

```java
IDocumentInfo infoXlsx = editorXlsx.getDocumentInfo(null);
if (infoXlsx instanceof SpreadsheetDocumentInfo) {
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo) infoXlsx;
    // Retrieve properties like tab count, size, etc.
}
editorXlsx.dispose();
```

*Förklaring*:  
- `instanceof`‑kontrollen visar om filen är ett kalkylblad, vilket gör att du kan anropa `getSheetCount()` och andra endast‑för‑kalkylblad‑metoder.

### Funktion 3: Hantera lösenordsskyddade dokument
#### Läs in det skyddade dokumentet
`Editor`‑konstruktorn accepterar ett valfritt `LoadOptions`‑objekt där du kan ange ett lösenord.

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.IDocumentInfo;
import com.groupdocs.editor.PasswordRequiredException;
import com.groupdocs.editor.IncorrectPasswordException;

String xlsInputFilePath = "YOUR_DOCUMENT_DIRECTORY/SAMPLE_XLS_PROTECTED";
Editor editorXls = new Editor(xlsInputFilePath);
```

#### Försök att komma åt med lösenord
Om lösenordet saknas eller är felaktigt kastar API:t `PasswordRequiredException` eller `IncorrectPasswordException`, vilket låter dig be användaren om lösenord eller logga problemet.

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

*Förklaring*:  
- API:ets explicita undantag låter dig implementera en smidig fallback‑logik utan gissningar.

### Funktion 4: Text‑baserad dokumentmetadataextraktion
#### Läs in det text‑baserade dokumentet
För rena textformat (TXT, XML, CSV) returnerar `TextDocumentInfo`‑klassen kodning, radantal och fil‑storleksdetaljer.

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.IDocumentInfo;
import com.groupdocs.editor.metadata.TextualDocumentInfo;

String xmlInputFilePath = "YOUR_DOCUMENT_DIRECTORY/SAMPLE_XML";
Editor editorXml = new Editor(xmlInputFilePath);
```

#### Extrahera och visa information
Använd getter‑metoderna på `TextDocumentInfo` för att hämta de lätta egenskaper du behöver för indexering eller validering.

```java
IDocumentInfo infoXml = editorXml.getDocumentInfo(null);
if (infoXml instanceof TextualDocumentInfo) {
    TextualDocumentInfo casted1 = (TextualDocumentInfo) infoXml;
    // Access encoding, size, etc.
}
editorXml.dispose();
```

*Förklaring*:  
- Detta tillvägagångssätt fungerar för rena textformat där du främst behöver kodning och fil‑storleksmetadata.

## Praktiska tillämpningar
- **Automated Document Archiving** – Hämta metadata för att märka och lagra filer i ett sökbart arkiv.  
- **Workflow Automation** – Använd metadata för att dirigera dokument till rätt avdelning eller trigga efterföljande processer.  
- **Data Migration** – Bevara originalegenskaper när filer flyttas mellan system, vilket säkerställer regulatorisk efterlevnad.

## Prestandaöverväganden
- **Dispose Editors** – Anropa alltid `dispose()` för att frigöra inhemska resurser och undvika minnesläckor.  
- **Large Files** – Bearbeta i strömmar eller segment; `getDocumentInfo(null)` läser endast huvudet, vilket håller RAM‑användning under 50 MB även för 2 GB‑filer.  
- **Profiling** – Använd Java‑profiler (t.ex. VisualVM) för att identifiera flaskhalsar när du hanterar tusentals filer.

## Vanliga problem & felsökning
| Symptom | Trolig orsak | Åtgärd |
|---------|--------------|-----|
| `PasswordRequiredException` även om filen inte är skyddad | Fel filväg eller korrupt fil | Verifiera filvägen och filens integritet |
| `null` returned for metadata | Använder en föråldrad biblioteksversion | Uppgradera till den senaste GroupDocs.Editor‑versionen |
| Låg prestanda på stora Excel‑filer | Laddar hela filen i minnet | Använd `getDocumentInfo(null)` (endast metadata) och bearbeta i batchar |

## Vanliga frågor

**Q: Kan jag extrahera metadata från PDF‑filer med samma API?**  
A: GroupDocs.Editor fokuserar på redigerbara format (DOCX, XLSX, etc.). För PDF‑filer, använd GroupDocs.Metadata eller GroupDocs.Viewer.

**Q: Hur upptäcker jag dokumenttypen utan att kasta?**  
A: Anropa `info.getDocumentType()` som returnerar en enum (t.ex. `DocumentType.WordProcessing`, `DocumentType.Spreadsheet`).

**Q: Är det möjligt att extrahera anpassade egenskaper som är inbäddade i Office‑filer?**  
A: Ja — `WordProcessingDocumentInfo` och `SpreadsheetDocumentInfo` exponerar metoder som `getCustomProperties()`.

**Q: Behöver jag en separat licens för varje dokumenttyp?**  
A: Nej, en enda GroupDocs.Editor‑licens täcker alla stödda format.

**Q: Vilken Java‑version krävs?**  
A: Java 8 eller senare; nyare LTS‑versioner (11, 17) stöds fullt ut.

## Slutsats
Du har nu ett komplett, produktionsklart arbetsflöde för **how to extract metadata** och **detect document type java** med hjälp av GroupDocs.Editor. Integrera dessa kodsnuttar med din egen affärslogik för att automatisera arkivering, efterlevnadskontroller eller vilket scenario som helst där dokumentinsikt är värdefull.

---

**Senast uppdaterad:** 2026-06-16  
**Testat med:** GroupDocs.Editor 25.3 for Java  
**Författare:** GroupDocs

## Relaterade handledningar

- [Ladda Word-dokument Java med GroupDocs.Editor – En komplett guide](/editor/java/document-loading/load-word-document-groupdocs-editor-java/)
- [hur man redigerar Excel- och Word‑filer i Java med GroupDocs.Editor](/editor/java/document-editing/java-groupdocs-editor-master-document-editing/)
- [Hur man extraherar resurser från Word‑dokument – GroupDocs.Editor Java](/editor/java/word-processing-documents/edit-extract-resources-groupdocs-editor-java/)