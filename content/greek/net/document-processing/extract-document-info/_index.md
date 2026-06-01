---
date: 2026-06-01
description: Μάθετε πώς να λαμβάνετε τον αριθμό σελίδων και να εξάγετε μεταδεδομένα
  εγγράφου χρησιμοποιώντας το GroupDocs.Editor για .NET σε ένα λεπτομερές step‑by‑step
  tutorial.
keywords:
- get page count
- extract document metadata
- get document info
- find document extension
- retrieve document size
linktitle: Λάβετε αριθμό σελίδων & εξάγετε πληροφορίες εγγράφου
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
title: Λάβετε αριθμό σελίδων & εξάγετε πληροφορίες εγγράφου με το GroupDocs.Editor
type: docs
url: /el/net/document-processing/extract-document-info/
weight: 10
---

# Λήψη Αριθμού Σελίδων & Εξαγωγή Πληροφοριών Εγγράφου με το GroupDocs.Editor

## Εισαγωγή
Σε αυτό το ολοκληρωμένο tutorial θα μάθετε πώς να **get page count** και να εξάγετε λεπτομερείς πληροφορίες εγγράφου —συμπεριλαμβανομένου του μορφότυπου, του μεγέθους και της κατάστασης κρυπτογράφησης— χρησιμοποιώντας το GroupDocs.Editor για .NET. Είτε δημιουργείτε σύστημα διαχείρισης εγγράφων, μηχανή αναφορών ή αυτοματοποιημένη γραμμή μετατροπής, η κατανόηση των μεταδεδομένων ενός αρχείου είναι το πρώτο βήμα για αξιόπιστη επεξεργασία. Ας περάσουμε από όλη τη ροή εργασίας, από τη φόρτωση ενός αρχείου μέχρι την ασφαλή απελευθέρωση των πόρων.

## Γρήγορες Απαντήσεις
- **Πώς μπορώ να ανακτήσω τον αριθμό σελίδων ενός εγγράφου;**  
  Καλέστε `editor.GetDocumentInfo().PageCount` μετά τη φόρτωση του αρχείου με `Editor`.
- **Ποιοι τύποι αρχείων υποστηρίζονται για εξαγωγή μεταδεδομένων;**  
  Πάνω από 50 μορφές, συμπεριλαμβανομένων των DOCX, XLSX, PPTX, PDF, TXT και HTML.
- **Μπορώ να εξάγω μεταδεδομένα από αρχεία με προστασία κωδικού;**  
  Ναι—παρέχετε τον κωδικό πρόσβασης κατά τη δημιουργία του αντικειμένου `Editor`.
- **Πρέπει να απελευθερώσω χειροκίνητα τους πόρους;**  
  Απολύτως· πάντα καλέστε `editor.Dispose()` ή τυλίξτε το editor σε ένα μπλοκ `using`.
- **Ποια έκδοση του GroupDocs.Editor απαιτείται;**  
  Η πιο πρόσφατη σταθερή έκδοση (v23.12+ τη στιγμή της συγγραφής) υποστηρίζει όλες τις παρουσιαζόμενες λειτουργίες.

## Τι είναι το “get page count” στο GroupDocs.Editor;
`GetDocumentInfo()` είναι μια μέθοδος που επιστρέφει ένα αντικείμενο `DocumentInfo` που περιέχει τον αριθμό σελίδων του εγγράφου, το μορφότυπο, το μέγεθος και άλλα μεταδεδομένα. Αυτή η ενιαία κλήση σας παρέχει άμεση πληροφόρηση χωρίς να χρειάζεται να αναλύσετε το αρχείο χειροκίνητα. Χρησιμοποιώντας αυτή τη μέθοδο αποφεύγετε τη φόρτωση ολόκληρου του εγγράφου στη μνήμη, κάτι που βελτιώνει την απόδοση, ειδικά για μεγάλα αρχεία, και μειώνει την κατανάλωση πόρων του διακομιστή.

## Γιατί να εξάγετε μεταδεδομένα εγγράφου με το GroupDocs.Editor;
Το GroupDocs.Editor μπορεί να επεξεργαστεί **πάνω από 50 μορφές εισόδου και εξόδου** και να ανακτήσει μεταδεδομένα για αρχεία έως **2 GB** χωρίς να φορτώνει ολόκληρο το έγγραφο στη μνήμη. Αυτή η αποδοτικότητα μειώνει το φορτίο του διακομιστή έως και **70 %** σε σύγκριση με την πλήρη ανάλυση εγγράφου, καθιστώντας το ιδανικό για εφαρμογές υψηλής απόδοσης.

## Προαπαιτούμενα
- **Βασικές γνώσεις ανάπτυξης C#** – πρέπει να είστε άνετοι με το Visual Studio και τις δομές έργων .NET.
- **Visual Studio 2022** (ή οποιαδήποτε πρόσφατη έκδοση) εγκατεστημένο στον υπολογιστή σας.
- **GroupDocs.Editor for .NET** – κατεβάστε το πιο πρόσφατο πακέτο από τη [download page](https://releases.groupdocs.com/editor/net/).

## Πώς να φορτώσετε το έγγραφό σας;
`Editor` είναι η κύρια κλάση που αντιπροσωπεύει ένα έγγραφο και παρέχει μεθόδους για τη φόρτωση και τη διαχείρισή του. Φορτώστε το αρχείο-στόχο δημιουργώντας μια παρουσία `Editor` και περνώντας τη διαδρομή του αρχείου. Ο επεξεργαστής ανιχνεύει αυτόματα το μορφότυπο, οπότε δεν χρειάζεται να καθορίσετε επιλογές φόρτωσης. Αυτή η προσέγγιση λειτουργεί για οποιονδήποτε υποστηριζόμενο τύπο αρχείου και απλοποιεί τη αρχική ρύθμιση.

```csharp
using System;
using GroupDocs.Editor.Metadata;
```

## Πώς να ανακτήσετε τις πληροφορίες του εγγράφου;
`GetDocumentInfo()` επιστρέφει ένα αντικείμενο `DocumentInfo` που περιέχει μεταδεδομένα όπως αριθμός σελίδων, μορφότυπο, μέγεθος και κατάσταση κρυπτογράφησης. Μετά τη φόρτωση, καλέστε αυτή τη μέθοδο για να λάβετε το αντικείμενο. Το επιστρεφόμενο `DocumentInfo` σας παρέχει μια συνοπτική εικόνα των χαρακτηριστικών του αρχείου, επιτρέποντάς σας να λάβετε αποφάσεις χωρίς περαιτέρω επεξεργασία.

```csharp
string docxInputFilePath = "YourSampleDocument.docx";
Editor editorDocx = new Editor(docxInputFilePath);
```

## Πώς να προσδιορίσετε τον τύπο του εγγράφου;
`DocumentType` είναι ένα enum που υποδεικνύει αν το έγγραφο είναι WordProcessing, Spreadsheet ή Text. Η γνώση του αν ένα αρχείο είναι έγγραφο επεξεργασίας κειμένου, λογιστικό φύλλο ή απλό κείμενο επηρεάζει τον τρόπο με τον οποίο θα το διαχειριστείτε αργότερα. Χρησιμοποιήστε την ιδιότητα `DocumentType` του αντικειμένου `DocumentInfo` για να πάρετε αυτή την απόφαση και να διακλαδώσετε τη λογική σας ανάλογα.

```csharp
IDocumentInfo infoDocx = editorDocx.GetDocumentInfo(null);
```

## Πώς να εξάγετε λεπτομερείς πληροφορίες για αρχεία επεξεργασίας κειμένου;
`WordProcessing` αναφέρεται σε έγγραφα όπως DOCX, ODT και RTF που αντιμετωπίζονται ως αρχεία επεξεργασίας κειμένου. Εάν ο τύπος του εγγράφου είναι `WordProcessing`, μπορείτε να διαβάσετε πρόσθετες ιδιότητες όπως **format**, **extension**, **page count**, **size**, και **encryption flag** απευθείας από το αντικείμενο `DocumentInfo`. Αυτές οι λεπτομέρειες σας βοηθούν να προσαρμόσετε τα βήματα επεξεργασίας, όπως η εφαρμογή συγκεκριμένων μετατροπών ή ελέγχων ασφαλείας.

```csharp
bool isSpreadsheet = infoDocx is SpreadsheetDocumentInfo;
bool isText = infoDocx is TextualDocumentInfo;
bool isWordProcessing = infoDocx is WordProcessingDocumentInfo;
Console.WriteLine($"Is '{docxInputFilePath}' a Spreadsheet: {isSpreadsheet}");
Console.WriteLine($"Is '{docxInputFilePath}' a Textual document: {isText}");
Console.WriteLine($"Is '{docxInputFilePath}' a WordProcessing document: {isWordProcessing}");
```

## Πώς να διαχειριστείτε αρχεία λογιστικών φύλλων και κειμένου;
`Spreadsheet` υποδηλώνει αρχεία λογιστικών φύλλων όπως XLSX, ενώ `Text` αντιπροσωπεύει έγγραφα απλού κειμένου. Για λογιστικά φύλλα (`Spreadsheet`) και αρχεία απλού κειμένου (`Text`), το αντικείμενο `DocumentInfo` παρέχει ακόμη βασικά μεταδεδομένα (extension, size, page count). Ορισμένες μορφές μπορεί να μην εκθέτουν αριθμό σελίδων· σε αυτή την περίπτωση η τιμή θα είναι `0`. Μπορείτε ακόμη να βασιστείτε σε άλλα μεταδεδομένα για τη λογική downstream.

```csharp
if (isWordProcessing)
{
    WordProcessingDocumentInfo casted = (WordProcessingDocumentInfo)infoDocx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Page count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```

## Πώς να εργαστείτε με αρχεία προστατευμένα με κωδικό;
`Password` είναι μια συμβολοσειρά που περνιέται στον κατασκευαστή `Editor` για το άνοιγμα κρυπτογραφημένων αρχείων. Όταν ένα έγγραφο είναι κρυπτογραφημένο, προσπαθήστε πρώτα να το ανοίξετε χωρίς κωδικό. Εάν αποτύχει, πιάστε την εξαίρεση και δοκιμάστε ξανά με τον σωστό κωδικό. Ο κατασκευαστής `Editor` δέχεται μια παράμετρο `Password` για αυτό το σκοπό, επιτρέποντας απρόσκοπτη διαχείριση προστατευμένων αρχείων.

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

## Πώς να επεξεργαστείτε έγγραφα κειμένου;
`DocumentInfo` παρέχει βασικά μεταδεδομένα όπως μέγεθος, επέκταση και κωδικοποίηση για αρχεία κειμένου. Τα αρχεία κειμένου (π.χ., `.txt`, `.md`) αντιμετωπίζονται ως απλές ροές. Μπορείτε ακόμη να ανακτήσετε πληροφορίες μεγέθους και κωδικοποίησης από το `DocumentInfo`, κάτι που είναι χρήσιμο για την επαλήθευση της ακεραιότητας του αρχείου ή τον καθορισμό κατάλληλων pipelines επεξεργασίας.

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

## Πώς να απελευθερώσετε τους πόρους σωστά;
`Editor` είναι η κύρια κλάση που διατηρεί μη διαχειριζόμενους πόρους και πρέπει να απελευθερώνεται μετά τη χρήση. Για να αποφύγετε διαρροές μνήμης, πάντα απελευθερώστε την παρουσία `Editor` αφού ολοκληρώσετε την εξαγωγή πληροφοριών. Η δήλωση `using` είναι το πιο ασφαλές μοτίβο επειδή εγγυάται την απελευθέρωση ακόμη και αν προκύψει εξαίρεση, εξασφαλίζοντας καθαρή διαχείριση πόρων.

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

## Κοινά Προβλήματα και Λύσεις
| Πρόβλημα | Αιτία | Λύση |
|----------|-------|------|
| **PageCount returns 0** | Η μορφή δεν υποστηρίζει σελιδοποίηση (π.χ., απλό κείμενο) | Ελέγξτε το `DocumentInfo.DocumentType` πριν βασιστείτε στο `PageCount`. |
| **Unsupported file format** | Η επέκταση αρχείου δεν αναγνωρίζεται | Βεβαιωθείτε ότι το αρχείο είναι μία από τις 50+ υποστηριζόμενες μορφές· ενημερώστε το GroupDocs.Editor στην πιο πρόσφατη έκδοση. |
| **Password exception** | Δόθηκε λανθασμένος κωδικός πρόσβασης | Πιάστε το `PasswordProtectedException` και ζητήστε από τον χρήστη να εισάγει ξανά τον κωδικό. |
| **Memory spike on large files** | Φόρτωση πολύ μεγάλων PDF χωρίς ροή | Χρησιμοποιήστε `LoadOptions` με `LoadOptions.LoadMode = LoadMode.Stream` (διαθέσιμο σε νεότερες εκδόσεις). |

## Συχνές Ερωτήσεις

**Q: Από ποιους τύπους εγγράφων μπορώ να εξάγω μεταδεδομένα;**  
A: Το GroupDocs.Editor υποστηρίζει αρχεία Word processing, spreadsheet, presentation, PDF και plain‑text — πάνω από 50 μορφές συνολικά.

**Q: Πώς μπορώ να ανακτήσω την επέκταση του αρχείου;**  
A: Πρόσβαση στο `DocumentInfo.Extension` μετά την κλήση του `GetDocumentInfo()`· επιστρέφει την επέκταση χωρίς την αρχική τελεία.

**Q: Μπορώ να λάβω το μέγεθος ενός εγγράφου σε megabytes;**  
A: Ναι—`DocumentInfo.Size` επιστρέφει το μέγεθος σε bytes· διαιρέστε με 1 048 576 για να το μετατρέψετε σε megabytes.

**Q: Είναι ασφαλές να επεξεργάζεστε αρχεία προστατευμένα με κωδικό σε διακομιστή;**  
A: Απόλυτα—το GroupDocs.Editor δεν γράφει ποτέ τον κωδικό σε δίσκο και απελευθερώνει όλα τα κρυπτογραφικά αντικείμενα μετά τη χρήση.

**Q: Πού μπορώ να βρω πρόσθετη βοήθεια αν αντιμετωπίσω προβλήματα;**  
A: Μπορείτε να λάβετε υποστήριξη από το [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).

---

**Τελευταία ενημέρωση:** 2026-06-01  
**Δοκιμή με:** GroupDocs.Editor 23.12 for .NET  
**Συγγραφέας:** GroupDocs

```csharp
editorDocx.Dispose();
editorXlsx.Dispose();
editorXls.Dispose();
editorXml.Dispose();
Console.WriteLine("ExtractingDocumentInfo routine has successfully finished");
```

## Σχετικά Μαθήματα

- [Αναλυτικός οδηγός εξαγωγής μεταδεδομένων σε .NET με το GroupDocs.Editor: Μια ολοκληρωμένη καθοδήγηση](/editor/net/advanced-features/groupdocs-editor-net-metadata-extraction-guide/)
- [Μαθήματα φόρτωσης εγγράφων με το GroupDocs.Editor για .NET](/editor/net/document-loading/)
- [Αποτελεσματική επεξεργασία εγγράφων με το GroupDocs.Editor .NET: Μετατροπή HTML σε επεξεργάσιμα έγγραφα](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)