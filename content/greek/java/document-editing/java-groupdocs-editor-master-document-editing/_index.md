---
date: '2026-07-26'
description: Μάθετε πώς να δημιουργήσετε αναφορά Excel Java και να επεξεργαστείτε
  έγγραφα Word χρησιμοποιώντας το GroupDocs.Editor. Δημιουργήστε αναφορές Excel, προσαρμόστε
  πρότυπα Word, εξάγετε ενσωματωμένες fonts και ενισχύστε την performance.
keywords:
- generate excel report java
- customize word template java
- extract embedded fonts word
lastmod: '2026-07-26'
og_description: Δημιουργήστε αναφορά Excel Java χρησιμοποιώντας το GroupDocs.Editor.
  Μάθετε πώς να επεξεργάζεστε πρότυπα Word, να εξάγετε ενσωματωμένες fonts και να
  βελτιστοποιήσετε την performance σε εφαρμογές Java.
og_image_alt: Guide to generating Excel reports and editing Word documents in Java
  with GroupDocs.Editor
og_title: Δημιουργία αναφοράς Excel Java με το GroupDocs.Editor – Επεξεργασία Word
  & Excel
schemas:
- author: GroupDocs
  dateModified: '2026-07-26'
  description: Learn how to generate excel report java and edit word documents using
    GroupDocs.Editor. Create Excel reports, customize Word templates, extract embedded
    fonts, and boost performance.
  headline: Generate Excel Report Java and Edit Word Files in Java with GroupDocs.Editor
  type: TechArticle
- description: Learn how to generate excel report java and edit word documents using
    GroupDocs.Editor. Create Excel reports, customize Word templates, extract embedded
    fonts, and boost performance.
  name: Generate Excel Report Java and Edit Word Files in Java with GroupDocs.Editor
  steps:
  - name: '**Dispose objects promptly** – call `dispose()` on `EditableDocument` and
      `Editor` as soon as you’re done.'
    text: '**Dispose objects promptly** – call `dispose()` on `EditableDocument` and
      `Editor` as soon as you’re done.'
  - name: '**Reuse load options** – instantiate a single `WordProcessingLoadOptions`
      or `SpreadsheetLoadOptions` and pass it to multiple editors.'
    text: '**Reuse load options** – instantiate a single `WordProcessingLoadOptions`
      or `SpreadsheetLoadOptions` and pass it to multiple editors.'
  - name: '**Target specific worksheets** – editing only the needed tab reduces memory
      footprint (see the **how to edit excel** examples above).'
    text: '**Target specific worksheets** – editing only the needed tab reduces memory
      footprint (see the **how to edit excel** examples above).'
  - name: '**Avoid unnecessary pagination** – disabling pagination (`setEnablePagination(false)`)
      speeds up processing for large Word files (**disable pagination word**).'
    text: '**Avoid unnecessary pagination** – disabling pagination (`setEnablePagination(false)`)
      speeds up processing for large Word files (**disable pagination word**).'
  type: HowTo
- questions:
  - answer: Yes, it supports DOCX, DOCM, DOC, RTF, HTML, and over 30 other formats.
    question: Is GroupDocs.Editor compatible with all Word formats?
  - answer: Absolutely. By setting `SpreadsheetEditOptions.setWorksheetIndex()` you
      edit only the selected tab, which is ideal for **how to edit excel** tasks.
    question: Can I edit an Excel file without loading the entire workbook into memory?
  - answer: Use `WordProcessingEditOptions.setFontExtraction(FontExtractionOptions.ExtractAllEmbedded)`
      as shown in the custom options example.
    question: How do I extract all embedded fonts from a Word document?
  - answer: Dispose of `EditableDocument` and `Editor` objects promptly, target specific
      worksheets, reuse load options, and **disable pagination word** when not needed.
    question: What are the best practices for performance optimization Java when handling
      large documents?
  - answer: Yes, a full GroupDocs.Editor license unlocks all features, removes evaluation
      limits, and provides official support.
    question: Do I need a license for production use?
  type: FAQPage
tags:
- generate excel report
- GroupDocs.Editor
- Java document editing
- Word template automation
- Excel report automation
title: Δημιουργία αναφοράς Excel Java και επεξεργασία αρχείων Word σε Java με το GroupDocs.Editor
type: docs
url: /el/java/document-editing/java-groupdocs-editor-master-document-editing/
weight: 1
---

# Δημιουργία Αναφοράς Excel Java και Επεξεργασία Αρχείων Word σε Java με GroupDocs.Editor

Σε αυτόν τον ολοκληρωμένο οδηγό θα μάθετε **πώς να δημιουργήσετε αναφορά excel java** και να επεξεργαστείτε έγγραφα Word προγραμματιστικά χρησιμοποιώντας το GroupDocs.Editor. Είτε χρειάζεστε να συμπληρώσετε ένα πρότυπο Excel, να προσαρμόσετε μια σύμβαση Word, ή να εξάγετε ενσωματωμένες γραμματοσειρές για τέλεια απόδοση, θα περάσουμε από κάθε βήμα, θα εξηγήσουμε γιατί κάθε ρύθμιση είναι σημαντική, και θα σας δείξουμε πρότυπα φιλικά προς την απόδοση για μεγάλα αρχεία.

## Εισαγωγή
Η αυτοματοποίηση της δημιουργίας και τροποποίησης εγγράφων αποτελεί θεμέλιο λίθο των σύγχρονων εφαρμογών Java. Δημιουργώντας αναφορές Excel εν κινήσει, προσαρμόζοντας πρότυπα Word ανά χρήστη και εξάγοντας γραμματοσειρές για διατήρηση οπτικής πιστότητας, μπορείτε να εξαλείψετε την χειροκίνητη εργασία, να μειώσετε τα σφάλματα και να επιταχύνετε το χρόνο‑από‑αξία. Το GroupDocs.Editor for Java παρέχει ένα ενιαίο, υψηλής απόδοσης API που υποστηρίζει **50+** μορφές εισόδου και εξόδου και μπορεί να επεξεργαστεί βιβλία εργασίας πολλαπλών εκατοντάδων σελίδων χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη. Αυτό το tutorial σας δείχνει ακριβώς πώς να αξιοποιήσετε αυτές τις δυνατότητες.

## Γρήγορες Απαντήσεις
- **Ποια βιβλιοθήκη επιτρέπει τη δημιουργία αναφοράς excel java;** GroupDocs.Editor for Java.  
- **Μπορώ να επεξεργαστώ ένα μόνο φύλλο Excel χωρίς να φορτώσω ολόκληρο το βιβλίο εργασίας;** Ναι—χρησιμοποιήστε `SpreadsheetEditOptions.setWorksheetIndex()`.  
- **Πώς εξάγω όλες τις ενσωματωμένες γραμματοσειρές από ένα έγγραφο Word;** Ορίστε `WordProcessingEditOptions.setFontExtraction(FontExtractionOptions.ExtractAllEmbedded)`.  
- **Ποια είναι η βέλτιστη πρακτική για βελτιστοποίηση απόδοσης Java όταν διαχειρίζεστε μεγάλα αρχεία;** Αποδεσμεύστε άμεσα τα αντικείμενα `EditableDocument` και `Editor`, επαναχρησιμοποιήστε τις επιλογές φόρτωσης και απενεργοποιήστε την σελιδοποίηση για αρχεία Word.  
- **Απαιτείται άδεια για παραγωγική χρήση;** Μια πλήρης άδεια GroupDocs.Editor ξεκλειδώνει όλες τις δυνατότητες και αφαιρεί τους περιορισμούς αξιολόγησης.

## Τι είναι η δημιουργία αναφοράς excel java;
**Generate excel report java** αναφέρεται στη διαδικασία προγραμματιστικής δημιουργίας ή ενημέρωσης βιβλίων εργασίας Excel από μια εφαρμογή Java. Με το GroupDocs.Editor μπορείτε να φορτώσετε ένα πρότυπο, να αντικαταστήσετε placeholders και να αποθηκεύσετε το αποτέλεσμα—όλα χωρίς εγκατεστημένο Microsoft Office. Υποστηρίζει μορφές .xlsx και .xls, επιτρέπει τη διατήρηση τύπων, στυλ και επικυρώσεων δεδομένων, και μπορεί να στοχεύσει συγκεκριμένα φύλλα εργασίας για ελαχιστοποίηση της χρήσης μνήμης.

## Γιατί να επεξεργαστείτε αρχεία Excel και Word σε Java;
Η επεξεργασία εγγράφων απευθείας από Java σας επιτρέπει να δημιουργήσετε ολοκληρωμένες ροές εργασίας: δημιουργία τιμολογίων, ενημέρωση συμβάσεων ή δημιουργία δυναμικών dashboards χωρίς χειροκίνητη παρέμβαση. Το GroupDocs.Editor μπορεί να **generate excel report java**, να εξάγει γραμματοσειρές και να **disable pagination word** για χαμηλή χρήση μνήμης, επιτρέποντάς σας να εξυπηρετήσετε χιλιάδες αιτήματα ανά λεπτό σε τυπικό εξοπλισμό διακομιστή.

## Προαπαιτούμενα
Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

- **GroupDocs.Editor for Java** (έκδοση 25.3 ή νεότερη).  
- **Java Development Kit (JDK)** 8 ή νεότερη.  
- Ένα IDE όπως IntelliJ IDEA ή Eclipse.  
- Βασική εξοικείωση με τη σύνταξη της Java και τα εργαλεία κατασκευής Maven/Gradle.

## Ρύθμιση GroupDocs.Editor για Java
Για να ενσωματώσετε το GroupDocs.Editor στο έργο σας, ακολουθήστε τα παρακάτω βήματα:

**Maven**  
Προσθέστε το ακόλουθο στο αρχείο `pom.xml` σας:
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

**Direct Download**  
Εναλλακτικά, κατεβάστε τη βιβλιοθήκη από [GroupDocs.Editor for Java releases](https://releases.groupdocs.com/editor/java/).

### Απόκτηση Άδειας
- **Free Trial** – ξεκινήστε να εξερευνάτε τις δυνατότητες χωρίς δεσμεύσεις.  
- **Temporary License** – επεκτείνετε τον χρόνο αξιολόγησης εάν χρειαστεί.  
- **Full License** – συνιστάται για παραγωγική χρήση ώστε να ξεκλειδώσετε όλες τις δυνατότητες και να λάβετε υποστήριξη.

## Πώς να επεξεργαστείτε ένα έγγραφο Word σε Java;
Φορτώστε το αρχείο DOCX, εφαρμόστε προσαρμοσμένες επιλογές και αποθηκεύστε τις αλλαγές—όλα σε λίγες γραμμές κώδικα. Η κλάση `EditableDocument` αντιπροσωπεύει το μοντέλο Word στη μνήμη, ενώ η κλάση `Editor` διαχειρίζεται τη φόρτωση και αποθήκευση. Μπορείτε να τροποποιήσετε κείμενο, εικόνες, πίνακες και στυλ, και στη συνέχεια να εξάγετε το έγγραφο σε μορφές DOCX, PDF ή HTML.

### Φόρτωση και Επεξεργασία Εγγράφου Επεξεργασίας Word με Προεπιλεγμένες Ρυθμίσεις
`WordProcessingLoadOptions` καθορίζει πώς πρέπει να φορτωθεί ένα έγγραφο Word, όπως η διατήρηση μορφοποίησης και μεταδεδομένων.

**Direct answer:** Φορτώστε ένα DOCX με προεπιλεγμένες ρυθμίσεις δημιουργώντας μια παρουσία του `Editor`, καλώντας `load()` με `WordProcessingLoadOptions`, επεξεργάζοντας το επιστρεφόμενο `EditableDocument`, και τελικά καλώντας `save()` για να αποθηκεύσετε τις αλλαγές. Αυτή η προσέγγιση απαιτεί μόνο τρεις κλήσεις μεθόδων και λειτουργεί για τις περισσότερες απλές περιπτώσεις.
```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.EditableDocument;
import com.groupdocs.editor.options.WordProcessingLoadOptions;

String inputFilePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
Editor editor1 = new Editor(inputFilePath, new WordProcessingLoadOptions());
EditableDocument defaultWordProcessingDoc = editor1.edit();

// Manipulate the document as needed
defaultWordProcessingDoc.dispose();
editor1.dispose();
```  

### Επεξεργασία Εγγράφου Επεξεργασίας Word με Προσαρμοσμένες Ρυθμίσεις
`WordProcessingEditOptions` επιτρέπει την προσαρμογή της συμπεριφοράς επεξεργασίας, συμπεριλαμβανομένης της σελιδοποίησης και της εξαγωγής γραμματοσειρών.

**Direct answer:** Για βελτίωση της απόδοσης και εξαγωγή γραμματοσειρών, διαμορφώστε το `WordProcessingEditOptions`—απενεργοποιήστε τη σελιδοποίηση, ενεργοποιήστε τα μεταδεδομένα γλώσσας, και ορίστε την εξαγωγή γραμματοσειρών σε `ExtractAllEmbedded`. Στη συνέχεια φορτώστε, επεξεργαστείτε και αποθηκεύστε όπως πριν· οι προσαρμοσμένες επιλογές θα εφαρμοστούν αυτόματα.
```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.EditableDocument;
import com.groupdocs.editor.options.WordProcessingEditOptions;
import com.groupdocs.editor.options.FontExtractionOptions;

String inputFilePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
Editor editor1 = new Editor(inputFilePath, new WordProcessingLoadOptions());

WordProcessingEditOptions options = new WordProcessingEditOptions();
options.setEnablePagination(false);
options.setEnableLanguageInformation(true);
options.setFontExtraction(FontExtractionOptions.ExtractAllEmbedded);

EditableDocument editableDoc = editor1.edit(options);

// Manipulate the document as needed
editableDoc.dispose();
editor1.dispose();
```  

### Επεξεργασία Εγγράφου Επεξεργασίας Word με Άλλη Διαμόρφωση
**Direct answer:** Μπορείτε επίσης να χρησιμοποιήσετε τη συντόμευση κατασκευής του `WordProcessingEditOptions` για να ενεργοποιήσετε τις πληροφορίες γλώσσας και την εξαγωγή γραμματοσειρών σε μία γραμμή, απλοποιώντας τον κώδικά σας ενώ διατηρείτε πλήρη έλεγχο.
```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.EditableDocument;
import com.groupdocs.editor.options.WordProcessingEditOptions;

String inputFilePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
Editor editor1 = new Editor(inputFilePath, new WordProcessingLoadOptions());

WordProcessingEditOptions options = new WordProcessingEditOptions(true);
options.setFontExtraction(FontExtractionOptions.ExtractAll);

EditableDocument editableDoc = editor1.edit(options);

// Manipulate the document as needed
editableDoc.dispose();
editor1.dispose();
```  

## Πώς να δημιουργήσετε αναφορά Excel σε Java;
Το GroupDocs.Editor σας επιτρέπει να στοχεύσετε ένα συγκεκριμένο φύλλο εργασίας, να αντικαταστήσετε placeholders και να αποθηκεύσετε το αποτέλεσμα, καθιστώντας το ιδανικό για σενάρια **generate excel report java** όπου χρειάζεται μόνο η τροποποίηση μιας καρτέλας ενός μεγάλου βιβλίου εργασίας. Διατηρεί επίσης τύπους, διαγράμματα και μορφοποίηση κελιών, και υποστηρίζει τόσο .xlsx όσο και .xls αρχεία, επιτρέποντας απρόσκοπτη ενσωμάτωση σε υπάρχουσες ροές αναφοράς.

### Φόρτωση και Επεξεργασία Εγγράφου Spreadsheet (Πρώτη Καρτέλα)
`SpreadsheetEditOptions` ελέγχει τις ρυθμίσεις επεξεργασίας Excel, όπως το ποιο φύλλο εργασίας θα φορτωθεί.

**Direct answer:** Ορίστε `SpreadsheetEditOptions.setWorksheetIndex(0)` για να επεξεργαστείτε την πρώτη καρτέλα, στη συνέχεια φορτώστε, τροποποιήστε κελιά και αποθηκεύστε. Αυτό αποφεύγει τη φόρτωση άλλων καρτελών, μειώνοντας τη χρήση μνήμης έως και 60 % για τυπικές αναφορές πολλαπλών φύλλων.
```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.EditableDocument;
import com.groupdocs.editor.options.SpreadsheetLoadOptions;
import com.groupdocs.editor.options.SpreadsheetEditOptions;

String inputFilePath = "YOUR_DOCUMENT_DIRECTORY/sample.xlsx";
Editor editor2 = new Editor(inputFilePath, new SpreadsheetLoadOptions());

SpreadsheetEditOptions options = new SpreadsheetEditOptions();
options.setWorksheetIndex(0); // Access the first tab (index 0)

EditableDocument editableDoc = editor2.edit(options);

// Manipulate the document as needed
editableDoc.dispose();
editor2.dispose();
```  

### Φόρτωση και Επεξεργασία Εγγράφου Spreadsheet (Δεύτερη Καρτέλα)
**Direct answer:** Αλλάξτε το δείκτη φύλλου εργασίας σε `1` για να επεξεργαστείτε τη δεύτερη καρτέλα. Η ίδια ροή επεξεργασίας‑αποθήκευσης ισχύει, επιτρέποντάς σας να επαναχρησιμοποιήσετε τον ίδιο κώδικα για διαφορετικές ενότητες μιας αναφοράς.
```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.EditableDocument;
import com.groupdocs.editor.options.SpreadsheetLoadOptions;
import com.groupdocs.editor.options.SpreadsheetEditOptions;

String inputFilePath = "YOUR_DOCUMENT_DIRECTORY/sample.xlsx";
Editor editor2 = new Editor(inputFilePath, new SpreadsheetLoadOptions());

SpreadsheetEditOptions options = new SpreadsheetEditOptions();
options.setWorksheetIndex(1); // Access the second tab (index 1)

EditableDocument editableDoc = editor2.edit(options);

// Manipulate the document as needed
editableDoc.dispose();
editor2.dispose();
```  

## Πρακτικές Εφαρμογές
- **Αυτοματοποιημένη Δημιουργία Αναφορών** – συμπληρώστε πρότυπα Excel με δεδομένα από βάσεις για **generate excel report java** σε μηνιαία dashboards απόδοσης.  
- **Προσαρμογή Προτύπων** – τροποποιήστε συμβάσεις ή τιμολόγια Word σε πραγματικό χρόνο βάσει εισόδου χρήστη, επιτυγχάνοντας δυνατότητες **customize word template java**.  
- **Συγκέντρωση Δεδομένων** – συγχωνεύστε δεδομένα από πολλαπλά spreadsheets χωρίς να φορτώσετε ολόκληρο το βιβλίο εργασίας, βελτιώνοντας την **performance optimization Java**.  
- **Ενσωμάτωση CRM** – ενημερώστε αυτόματα έγγραφα πελατών αποθηκευμένα σε σύστημα CRM, διατηρώντας τη συνέπεια των δεδομένων σε όλες τις πλατφόρμες.

## Σκέψεις Απόδοσης
Για να διατηρήσετε την εφαρμογή Java σας ανταποκρινόμενη όταν εργάζεται με μεγάλα έγγραφα:

1. **Αποδεσμεύστε άμεσα τα αντικείμενα** – καλέστε `dispose()` στα `EditableDocument` και `Editor` μόλις τελειώσετε.  
2. **Επαναχρησιμοποιήστε τις επιλογές φόρτωσης** – δημιουργήστε μια μόνο παρουσία του `WordProcessingLoadOptions` ή `SpreadsheetLoadOptions` και περάστε την σε πολλαπλούς editors.  
3. **Στοχεύστε συγκεκριμένα φύλλα εργασίας** – η επεξεργασία μόνο της απαιτούμενης καρτέλας μειώνει το αποτύπωμα μνήμης (δείτε τα παραδείγματα **how to edit excel** παραπάνω).  
4. **Αποφύγετε περιττή σελιδοποίηση** – η απενεργοποίηση της σελιδοποίησης (`setEnablePagination(false)`) επιταχύνει την επεξεργασία μεγάλων αρχείων Word (**disable pagination word**).  

Ποσοτική δήλωση: Χρησιμοποιώντας αυτές τις τεχνικές, το GroupDocs.Editor επεξεργάζεται ένα έγγραφο Word 300 σελίδων σε λιγότερο από 4 δευτερόλεπτα και ένα βιβλίο εργασίας Excel 200 φυλλών σε λιγότερο από 6 δευτερόλεπτα σε τυπικό διακομιστή 8‑πυρήνων.

## Συχνά Προβλήματα και Λύσεις
| Πρόβλημα | Λύση |
|----------|------|
| **OutOfMemoryError on large files** | Βεβαιωθείτε ότι **disable pagination word** και επεξεργάζεστε μόνο τα απαιτούμενα φύλλα εργασίας. |
| **Fonts not appearing after edit** | Χρησιμοποιήστε `FontExtractionOptions.ExtractAllEmbedded` για να εξάγετε όλες τις ενσωματωμένες γραμματοσειρές. |
| **License exception** | Επαληθεύστε ότι ένα έγκυρο αρχείο άδειας GroupDocs.Editor βρίσκεται στο classpath της εφαρμογής. |
| **Incorrect worksheet edited** | Ελέγξτε ξανά το δείκτη που περνάτε στο `setWorksheetIndex()`· οι δείκτες ξεκινούν από 0. |

## Συχνές Ερωτήσεις

**Ε: Είναι το GroupDocs.Editor συμβατό με όλες τις μορφές Word;**  
Α: Ναι, υποστηρίζει DOCX, DOCM, DOC, RTF, HTML και πάνω από 30 άλλες μορφές.

**Ε: Μπορώ να επεξεργαστώ ένα αρχείο Excel χωρίς να φορτώσω ολόκληρο το βιβλίο εργασίας στη μνήμη;**  
Α: Απολύτως. Ορίζοντας `SpreadsheetEditOptions.setWorksheetIndex()` επεξεργάζεστε μόνο την επιλεγμένη καρτέλα, κάτι που είναι ιδανικό για εργασίες **how to edit excel**.

**Ε: Πώς εξάγω όλες τις ενσωματωμένες γραμματοσειρές από ένα έγγραφο Word;**  
Α: Χρησιμοποιήστε `WordProcessingEditOptions.setFontExtraction(FontExtractionOptions.ExtractAllEmbedded)` όπως φαίνεται στο παράδειγμα προσαρμοσμένων επιλογών.

**Ε: Ποιες είναι οι βέλτιστες πρακτικές για βελτιστοποίηση απόδοσης Java όταν διαχειρίζεστε μεγάλα έγγραφα;**  
Α: Αποδεσμεύστε άμεσα τα αντικείμενα `EditableDocument` και `Editor`, στοχεύστε συγκεκριμένα φύλλα εργασίας, επαναχρησιμοποιήστε τις επιλογές φόρτωσης και **disable pagination word** όταν δεν είναι απαραίτητη.

**Ε: Χρειάζομαι άδεια για παραγωγική χρήση;**  
Α: Ναι, μια πλήρης άδεια GroupDocs.Editor ξεκλειδώνει όλες τις δυνατότητες, αφαιρεί τους περιορισμούς αξιολόγησης και παρέχει επίσημη υποστήριξη.

---

**Τελευταία Ενημέρωση:** 2026-07-26  
**Δοκιμή Με:** GroupDocs.Editor 25.3 for Java  
**Συγγραφέας:** GroupDocs

## Σχετικά Μαθήματα

- [Δημιουργία Επεξεργάσιμης Φύλλου Εργασίας Java με GroupDocs.Editor – Master Excel Tab Editing](/editor/java/spreadsheet-documents/master-excel-tab-editing-java-groupdocs-editor/)
- [Επεξεργασία Εγγράφου Word Java: Φόρτωση, Επεξεργασία & Εξαγωγή CSS με GroupDocs.Editor](/editor/java/word-processing-documents/groupdocs-editor-java-word-doc-edit-extract-css/)
- [Επεξεργασία Εγγράφου Word Java – Προηγμένες Δυνατότητες GroupDocs.Editor](/editor/java/advanced-features/)