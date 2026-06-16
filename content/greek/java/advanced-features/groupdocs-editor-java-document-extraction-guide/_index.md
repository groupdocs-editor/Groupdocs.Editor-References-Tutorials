---
date: '2026-06-16'
description: Μάθετε πώς να εξάγετε μεταδεδομένα, πώς να εξάγετε μεταδεδομένα σε Java
  και πώς να εντοπίζετε τον τύπο εγγράφου java με το GroupDocs.Editor για Java σε
  αρχεία Word, Excel και κειμένου.
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
title: Πώς να εξάγετε μεταδεδομένα από έγγραφα Java χρησιμοποιώντας το GroupDocs.Editor
type: docs
url: /el/java/advanced-features/groupdocs-editor-java-document-extraction-guide/
weight: 1
---

# Πώς να εξάγετε μεταδεδομένα από έγγραφα Java χρησιμοποιώντας το GroupDocs.Editor

Αν είστε προγραμματιστής που είναι **κουρασμένος από την χειροκίνητη εξαγωγή πληροφοριών από αρχεία Word, Excel ή απλού‑κειμένου**, αυτός ο οδηγός σας δείχνει **πώς να εξάγετε μεταδεδομένα** γρήγορα και αξιόπιστα. Θα δείτε γιατί το GroupDocs.Editor for Java είναι η βιβλιοθήκη‑αναφορά για **detect document type java**, πώς να διαβάσετε ιδιότητες όπως αριθμός σελίδων, συγγραφέας και κατάσταση κρυπτογράφησης, και πώς να διαχειριστείτε αρχεία με κωδικό πρόσβασης—όλα με σύντομες, έτοιμες για παραγωγή αποσπάσματα κώδικα.

## Γρήγορες Απαντήσεις
- **Τι σημαίνει “extract document metadata java”**; Αναφέρεται στην προγραμματική ανάγνωση ιδιοτήτων όπως μορφή, αριθμός σελίδων, μέγεθος και κατάσταση κρυπτογράφησης από έγγραφα χρησιμοποιώντας Java.  
- **Ποια βιβλιοθήκη βοηθά σε αυτό**; Το GroupDocs.Editor for Java παρέχει ένα απλό API για εξαγωγή μεταδεδομένων και ανίχνευση τύπου.  
- **Μπορώ να ανιχνεύσω τον τύπο εγγράφου java ως μέρος της διαδικασίας**; Ναι—εξετάζοντας το επιστρεφόμενο `IDocumentInfo` μπορείτε να καθορίσετε αν το αρχείο είναι Word, υπολογιστικό φύλλο ή κείμενο.  
- **Χρειάζομαι άδεια**; Μια δωρεάν δοκιμή λειτουργεί για αξιολόγηση· απαιτείται μόνιμη άδεια για παραγωγική χρήση.  
- **Ποιες είναι οι κύριες προαπαιτήσεις**; Java 8+, Maven (ή χειροκίνητη λήψη JAR), και βασικές γνώσεις Java.

## Τι είναι η εξαγωγή μεταδεδομένων εγγράφου java;
**Η εξαγωγή μεταδεδομένων εγγράφου σε Java σημαίνει την ανάκτηση περιγραφικών πληροφοριών—όπως μορφή αρχείου, αριθμός σελίδων, συγγραφέας ή κατάσταση κρυπτογράφησης—χωρίς τη φόρτωση ολόκληρης της περιεχομένου του εγγράφου.** Αυτή η ελαφριά προσέγγιση επιταχύνει την ευρετηρίαση, την αρχειοθέτηση και τους ελέγχους συμμόρφωσης, επιτρέποντάς σας να αναλύετε αρχεία γρήγορα, να μειώνετε την κατανάλωση μνήμης και να λαμβάνετε ενημερωμένες αποφάσεις πριν ανοίξετε πλήρη έγγραφα.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Editor για Java για την ανίχνευση τύπου εγγράφου java;
**Το GroupDocs.Editor εντοπίζει αυτόματα τον τύπο του εγγράφου και εκθέτει ιδιότητες ειδικές για τον τύπο για πάνω από 30 επεξεργάσιμες μορφές, επεξεργαζόμενο αρχεία έως 2 GB χωρίς τη φόρτωση ολόκληρου του περιεχομένου στη μνήμη.** Διαχειρίζεται επίσης αρχεία με κωδικό πρόσβασης έτοιμο, καθιστώντας το την πιο αποδοτική λύση για σενάρια **detect document type java**.

## Προαπαιτούμενα
- **Java Development Kit (JDK)** 8 ή νεότερο.  
- **Maven** για διαχείριση εξαρτήσεων (ή χειροκίνητη λήψη JAR).  
- Βασική εξοικείωση με κλάσεις Java και διαχείριση εξαιρέσεων.  

## Ρύθμιση του GroupDocs.Editor για Java

### Εγκατάσταση μέσω Maven
Προσθέστε το αποθετήριο και την εξάρτηση στο `pom.xml` σας:

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

### Άμεση Λήψη
Εναλλακτικά, κατεβάστε το τελευταίο JAR από [GroupDocs.Editor for Java releases](https://releases.groupdocs.com/editor/java/).

### Απόκτηση Άδειας
- **Free Trial** – εξερευνήστε το API χωρίς κόστος.  
- **Temporary License** – αποκτήστε κλειδί περιορισμένου χρόνου μέσω [this link](https://purchase.groupdocs.com/temporary-license).  
- **Purchase** – αγοράστε μόνιμη άδεια για παραγωγικές εγκαταστάσεις.

#### Βασική Αρχικοποίηση και Ρύθμιση
Η κλάση `Editor` είναι το σημείο εισόδου που φορτώνει ένα έγγραφο και παρέχει πρόσβαση στα μεταδεδομένα του. Αφού δημιουργήσετε μια παρουσία `Editor`, μπορείτε να καλέσετε `getDocumentInfo(null)` για να λάβετε ελαφριές πληροφορίες.

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

## Πώς να εξάγετε μεταδεδομένα σε Java
Φορτώστε το έγγραφο, ζητήστε το `IDocumentInfo` του, και στη συνέχεια κάντε cast στην κλάση ειδική για τη μορφή. Αυτό το μοτίβο λειτουργεί για Word, Excel και αρχεία απλού κειμένου, διατηρώντας τη χρήση μνήμης χαμηλή, επειδή διαβάζεται μόνο η κεφαλίδα του εγγράφου. Εξάγοντας πρώτα τα μεταδεδομένα, μπορείτε να αποφασίσετε αν θα επεξεργαστείτε το πλήρες περιεχόμενο, να δρομολογήσετε το αρχείο ή να απορρίψετε μη υποστηριζόμενες μορφές.

### Χαρακτηριστικό 1: Εξαγωγή Μεταδεδομένων από Έγγραφα Word
#### Φόρτωση του Εγγράφου
Η διεπαφή `DocumentInfo` αντιπροσωπεύει γενικά μεταδεδομένα για οποιοδήποτε υποστηριζόμενο αρχείο. Η παροχή της διαδρομής του αρχείου στον κατασκευαστή `Editor` προετοιμάζει το έγγραφο για επιθεώρηση.

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.IDocumentInfo;
import com.groupdocs.editor.metadata.WordProcessingDocumentInfo;

String docxInputFilePath = "YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX";
Editor editorDocx = new Editor(docxInputFilePath);
```

#### Εξαγωγή Πληροφοριών Εγγράφου
Το `WordProcessingDocumentInfo` είναι μια συγκεκριμένη υλοποίηση που προσθέτει ιδιότητες ειδικές για Word όπως αριθμός σελίδων, συγγραφέας και κατάσταση κρυπτογράφησης.

```java
IDocumentInfo infoDocx = editorDocx.getDocumentInfo(null);
if (infoDocx instanceof WordProcessingDocumentInfo) {
    WordProcessingDocumentInfo casted = (WordProcessingDocumentInfo) infoDocx;
    // Access properties like format, page count, and more
}
editorDocx.dispose();
```

*Εξήγηση*:  
- `getDocumentInfo(null)` ανακτά μεταδεδομένα χωρίς να φορτώνει ολόκληρο το σώμα του εγγράφου.  
- Η μετατροπή σε `WordProcessingDocumentInfo` αποκαλύπτει ιδιότητες ειδικές για Word όπως **αριθμός σελίδων**, όνομα συγγραφέα και σημαία κρυπτογράφησης.

### Χαρακτηριστικό 2: Ανίχνευση τύπου εγγράφου java – Φύλλα Εργασίας
#### Φόρτωση του Αρχείου Φύλλου Εργασίας
Το `SpreadsheetDocumentInfo` παρέχει μεταδεδομένα ειδικά για φύλλα εργασίας όπως αριθμός φύλλων και συνολικό μέγεθος.

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.IDocumentInfo;
import com.groupdocs.editor.metadata.SpreadsheetDocumentInfo;

String xlsxInputFilePath = "YOUR_DOCUMENT_DIRECTORY/SAMPLE_XLSX";
Editor editorXlsx = new Editor(xlsxInputFilePath);
```

#### Έλεγχος και Εξαγωγή Πληροφοριών
Χρησιμοποιώντας τον τελεστή `instanceof` μπορείτε να **detect document type java** και στη συνέχεια να διαβάσετε μεταδεδομένα ειδικά για φύλλα εργασίας όπως αριθμός φύλλων και συνολικό μέγεθος.

```java
IDocumentInfo infoXlsx = editorXlsx.getDocumentInfo(null);
if (infoXlsx instanceof SpreadsheetDocumentInfo) {
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo) infoXlsx;
    // Retrieve properties like tab count, size, etc.
}
editorXlsx.dispose();
```

*Εξήγηση*:  
- Ο έλεγχος `instanceof` σας λέει αν το αρχείο είναι φύλλο εργασίας, επιτρέποντάς σας να καλέσετε `getSheetCount()` και άλλες μεθόδους μόνο για φύλλα εργασίας.

### Χαρακτηριστικό 3: Διαχείριση Εγγράφων με Κωδικό Πρόσβασης
#### Φόρτωση του Προστατευμένου Εγγράφου
Ο κατασκευαστής `Editor` δέχεται προαιρετικό αντικείμενο `LoadOptions` όπου μπορείτε να παρέχετε κωδικό πρόσβασης.

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.IDocumentInfo;
import com.groupdocs.editor.PasswordRequiredException;
import com.groupdocs.editor.IncorrectPasswordException;

String xlsInputFilePath = "YOUR_DOCUMENT_DIRECTORY/SAMPLE_XLS_PROTECTED";
Editor editorXls = new Editor(xlsInputFilePath);
```

#### Προσπάθεια Πρόσβασης με Κωδικό
Αν λείπει ή είναι λανθασμένος ο κωδικός, το API ρίχνει `PasswordRequiredException` ή `IncorrectPasswordException`, επιτρέποντάς σας να προτρέψετε τον χρήστη ή να καταγράψετε το πρόβλημα.

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

*Εξήγηση*:  
- Οι σαφείς εξαιρέσεις του API σας επιτρέπουν να υλοποιήσετε λογική εναλλακτικής αντιμετώπισης χωρίς εικασίες.

### Χαρακτηριστικό 4: Εξαγωγή Μεταδεδομένων Εγγράφων Κειμένου
#### Φόρτωση Εγγράφου Κειμένου
Για μορφές απλού κειμένου (TXT, XML, CSV) η κλάση `TextDocumentInfo` επιστρέφει κωδικοποίηση, αριθμό γραμμών και λεπτομέρειες μεγέθους αρχείου.

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.IDocumentInfo;
import com.groupdocs.editor.metadata.TextualDocumentInfo;

String xmlInputFilePath = "YOUR_DOCUMENT_DIRECTORY/SAMPLE_XML";
Editor editorXml = new Editor(xmlInputFilePath);
```

#### Εξαγωγή και Εμφάνιση Πληροφοριών
Χρησιμοποιήστε τα getters της `TextDocumentInfo` για να ανακτήσετε τις ελαφριές ιδιότητες που χρειάζεστε για ευρετηρίαση ή επικύρωση.

```java
IDocumentInfo infoXml = editorXml.getDocumentInfo(null);
if (infoXml instanceof TextualDocumentInfo) {
    TextualDocumentInfo casted1 = (TextualDocumentInfo) infoXml;
    // Access encoding, size, etc.
}
editorXml.dispose();
```

*Εξήγηση*:  
- Αυτή η προσέγγιση λειτουργεί για μορφές απλού κειμένου όπου κυρίως χρειάζεστε κωδικοποίηση και μεταδεδομένα μεγέθους αρχείου.

## Πρακτικές Εφαρμογές
- **Αυτοματοποιημένη Αρχειοθέτηση Εγγράφων** – Εξάγετε μεταδεδομένα για να ετικετοποιήσετε και να αποθηκεύσετε αρχεία σε ένα αναζητήσιμο αποθετήριο.  
- **Αυτοματοποίηση Ροής Εργασίας** – Χρησιμοποιήστε τα μεταδεδομένα για να δρομολογήσετε έγγραφα στο σωστό τμήμα ή να ενεργοποιήσετε επόμενες διαδικασίες.  
- **Μεταφορά Δεδομένων** – Διατηρήστε τις αρχικές ιδιότητες κατά τη μετακίνηση αρχείων μεταξύ συστημάτων, εξασφαλίζοντας συμμόρφωση με κανονισμούς.

## Σκέψεις Απόδοσης
- **Dispose Editors** – Πάντα καλέστε `dispose()` για να ελευθερώσετε εγγενείς πόρους και να αποφύγετε διαρροές μνήμης.  
- **Μεγάλα Αρχεία** – Επεξεργαστείτε σε ροές ή τμήματα· το `getDocumentInfo(null)` διαβάζει μόνο την κεφαλίδα, διατηρώντας τη χρήση RAM κάτω από 50 MB ακόμη και για αρχεία 2 GB.  
- **Profiling** – Χρησιμοποιήστε προφίλ Java (π.χ., VisualVM) για να εντοπίσετε σημεία συμφόρησης όταν διαχειρίζεστε χιλιάδες αρχεία.

## Συνηθισμένα Προβλήματα & Επίλυση
| Σύμπτωμα | Πιθανή Αιτία | Διόρθωση |
|---------|--------------|----------|
| `PasswordRequiredException` παρόλο που το αρχείο δεν είναι προστατευμένο | Λάθος διαδρομή αρχείου ή κατεστραμμένο αρχείο | Επαληθεύστε τη διαδρομή και την ακεραιότητα του αρχείου |
| `null` επιστρέφεται για μεταδεδομένα | Χρήση παλιάς έκδοσης της βιβλιοθήκης | Αναβαθμίστε στην πιο πρόσφατη έκδοση του GroupDocs.Editor |
| Χαμηλή απόδοση σε μεγάλα αρχεία Excel | Φόρτωση ολόκληρου του αρχείου στη μνήμη | Χρησιμοποιήστε `getDocumentInfo(null)` (μόνο μεταδεδομένα) και επεξεργαστείτε σε παρτίδες |

## Συχνές Ερωτήσεις

**Q: Μπορώ να εξάγω μεταδεδομένα από αρχεία PDF με το ίδιο API;**  
A: Το GroupDocs.Editor εστιάζει σε επεξεργάσιμες μορφές (DOCX, XLSX, κ.λπ.). Για PDFs, χρησιμοποιήστε GroupDocs.Metadata ή GroupDocs.Viewer.

**Q: Πώς μπορώ να ανιχνεύσω τον τύπο του εγγράφου χωρίς μετατροπή (casting);**  
A: Καλέστε `info.getDocumentType()` που επιστρέφει ένα enum (π.χ., `DocumentType.WordProcessing`, `DocumentType.Spreadsheet`).

**Q: Είναι δυνατόν να εξάγω προσαρμοσμένες ιδιότητες ενσωματωμένες σε αρχεία Office;**  
A: Ναι—`WordProcessingDocumentInfo` και `SpreadsheetDocumentInfo` εκθέτουν μεθόδους όπως `getCustomProperties()`.

**Q: Χρειάζομαι ξεχωριστή άδεια για κάθε τύπο εγγράφου;**  
A: Όχι, μια άδεια GroupDocs.Editor καλύπτει όλες τις υποστηριζόμενες μορφές.

**Q: Ποια έκδοση Java απαιτείται;**  
A: Java 8 ή νεότερη· οι νεότερες LTS εκδόσεις (11, 17) υποστηρίζονται πλήρως.

## Συμπέρασμα
Τώρα έχετε μια πλήρη, έτοιμη για παραγωγή ροή εργασίας για **πώς να εξάγετε μεταδεδομένα** και **detect document type java** χρησιμοποιώντας το GroupDocs.Editor. Ενσωματώστε αυτά τα αποσπάσματα με τη δική σας επιχειρηματική λογική για να αυτοματοποιήσετε την αρχειοθέτηση, τους ελέγχους συμμόρφωσης ή οποιοδήποτε σενάριο όπου η γνώση του εγγράφου είναι πολύτιμη.

---

**Τελευταία Ενημέρωση:** 2026-06-16  
**Δοκιμή με:** GroupDocs.Editor 25.3 for Java  
**Συγγραφέας:** GroupDocs

## Σχετικά Μαθήματα

- [Φόρτωση Εγγράφου Word Java με GroupDocs.Editor – Πλήρης Οδηγός](/editor/java/document-loading/load-word-document-groupdocs-editor-java/)
- [πώς να επεξεργαστείτε αρχεία excel και Word σε Java με GroupDocs.Editor](/editor/java/document-editing/java-groupdocs-editor-master-document-editing/)
- [Πώς να εξάγετε πόρους από έγγραφα Word – GroupDocs.Editor Java](/editor/java/word-processing-documents/edit-extract-resources-groupdocs-editor-java/)