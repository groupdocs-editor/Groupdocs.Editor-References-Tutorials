---
date: 2026-06-06
description: Μάθετε πώς να **αποθηκεύσετε κάθε καρτέλα του Excel** χρησιμοποιώντας
  το GroupDocs.Editor για .NET – βήμα‑βήμα οδηγός, αποσπάσματα κώδικα και βέλτιστες
  πρακτικές για το διαχωρισμό αρχείων XLSX.
keywords:
- save each excel tab
- read multiple sheets
- convert excel tab pdf
- split xlsx files
linktitle: Εργασία με υπολογιστικά φύλλα πολλαπλών καρτελών
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to **save each Excel tab** using GroupDocs.Editor for .NET
    – step‑by‑step guide, code snippets, and best practices for splitting XLSX files.
  headline: How to save each Excel tab with GroupDocs.Editor .NET
  type: TechArticle
- description: Learn how to **save each Excel tab** using GroupDocs.Editor for .NET
    – step‑by‑step guide, code snippets, and best practices for splitting XLSX files.
  name: How to save each Excel tab with GroupDocs.Editor .NET
  steps:
  - name: Get a Path to the Input File
    text: First, specify the full path to the source XLSX that contains multiple tabs.
  - name: Load the Spreadsheet into the Editor Instance
    text: The `Editor` class is the entry point for all document operations in GroupDocs.Editor.
      It reads the file stream and prepares the document for editing or extraction.
  - name: Create an EditableDocument from the First Tab
    text: '`EditableDocument` represents a single, editable sheet within the workbook.
      The constructor takes the `Editor` instance and a zero‑based sheet index.'
  - name: Create an EditableDocument from the Second Tab
    text: You can repeat the same pattern for any additional sheet by changing the
      index value.
  - name: Save the First Tab to a Separate Document
    text: '`Save` writes the edited document to a file in the specified format. Call
      it on the `EditableDocument` instance, providing the output path and format
      (e.g., `SaveFormat.Xlsx`).'
  - name: Save the Second Tab to a Separate Document
    text: The same `Save` call works for the second sheet, and you can choose a different
      format such as PDF if needed.
  - name: Dispose of EditableDocument Instances
    text: '`Dispose` releases unmanaged resources held by the document, such as file
      handles, ensuring no leaks in long‑running services.'
  type: HowTo
- questions:
  - answer: Hidden sheets are treated like any other sheet; you can access them by
      index and save them, but you may need to set `EditableDocument.IsVisible = true`
      before saving if you want them visible in the output.
    question: What if my workbook contains hidden sheets?
  - answer: Yes, specify `SaveFormat.Pdf` when calling `Save` on the `EditableDocument`.
      The library preserves layout, images, and charts during conversion.
    question: Can I convert an Excel tab directly to PDF?
  - answer: Absolutely. Use `SaveFormat.Csv` for each `EditableDocument` to generate
      plain‑text CSV representations of each sheet.
    question: Is it possible to split a workbook into CSV files instead of XLSX?
  - answer: It does. Provide the password via `LoadOptions.Password` when creating
      the `Editor` instance.
    question: Does GroupDocs.Editor support password‑protected Excel files?
  - answer: The official documentation and sample projects on the [download page](https://releases.groupdocs.com/editor/net/)
      contain additional use‑cases.
    question: Where can I find more examples of working with spreadsheets?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Πώς να αποθηκεύσετε κάθε καρτέλα του Excel με το GroupDocs.Editor .NET
type: docs
url: /el/net/document-processing/work-multi-tab-spreadsheets/
weight: 17
---

# Εργασία με Πίνακες πολλαπλών καρτελών

## Εισαγωγή
Αν χρειάζεστε **να αποθηκεύσετε κάθε καρτέλα του Excel** ως ανεξάρτητο αρχείο, το GroupDocs.Editor για .NET το κάνει εύκολο. Είτε εξάγετε οικονομικές αναφορές, δημιουργείτε φύλλα εργασίας ανά τμήμα, είτε μετατρέπετε τις καρτέλες σε PDF, αυτό το tutorial σας καθοδηγεί σε όλη τη ροή εργασίας — από τη ρύθμιση του περιβάλλοντος μέχρι την απελευθέρωση των πόρων — ώστε να μπορείτε να αυτοματοποιήσετε τη διαχείριση πολλαπλών φύλλων με σιγουριά.

## Γρήγορες Απαντήσεις
- **Μπορεί το GroupDocs.Editor να χωρίσει ένα XLSX σε ξεχωριστά αρχεία;** Ναι, μπορείτε να φορτώσετε το βιβλίο εργασίας και να εξάγετε κάθε φύλλο ξεχωριστά.  
- **Σε ποιες μορφές μπορεί να αποθηκευτεί κάθε καρτέλα;** XLSX, CSV, PDF, HTML, και άλλα – υποστηρίζονται πάνω από 30 μορφές εξόδου.  
- **Χρειάζομαι άδεια για αυτή τη λειτουργία;** Μια προσωρινή άδεια λειτουργεί για δοκιμές· απαιτείται πλήρης άδεια για παραγωγή.  
- **Υποστηρίζεται το .NET Core;** Απολύτως – η βιβλιοθήκη λειτουργεί με .NET Framework 4.0+ και .NET Core/5/6+.  
- **Πόσες καρτέλες μπορούν να επεξεργαστούν ταυτόχρονα;** Το GroupDocs.Editor μπορεί να διαχειριστεί βιβλία εργασίας με 500+ φύλλα χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη.

## Τι είναι το “save each excel tab”;
**“Save each Excel tab”** σημαίνει την εξαγωγή κάθε φύλλου εργασίας από ένα βιβλίο εργασίας πολλαπλών φύλλων και τη γραφή του καθενός σε ένα ανεξάρτητο έγγραφο (π.χ., ξεχωριστά αρχεία XLSX ή PDF). Αυτή η προσέγγιση απλοποιεί την επεξεργασία, την αναφορά και τη διανομή, παρέχοντάς σας ένα αρχείο ανά φύλλο, το οποίο μπορεί στη συνέχεια να μοιραστεί, να αρχειοθετηθεί ή να μετατραπεί περαιτέρω ανεξάρτητα.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Editor για αυτήν την εργασία;
Το GroupDocs.Editor υποστηρίζει **πάνω από 30 μορφές εισόδου και εξόδου** και μπορεί να επεξεργαστεί λογιστικά φύλλα με **έως 1.000 φύλλα** διατηρώντας τη χρήση μνήμης χαμηλή μέσω ροής δεδομένων αντί της φόρτωσης ολόκληρου του αρχείου. Το API διατηρεί επίσης τα στυλ των κελιών, τους τύπους και τις ενσωματωμένες εικόνες, εξασφαλίζοντας ότι κάθε εξαγόμενη καρτέλα φαίνεται ακριβώς όπως το αρχικό.

## Προαπαιτούμενα
1. **Visual Studio** – οποιαδήποτε πρόσφατη έκδοση (Community, Professional ή Enterprise).  
2. **.NET Framework 4.0+** – ή .NET Core/5/6 αν προτιμάτε το δια‑πλατφορμικό runtime.  
3. **GroupDocs.Editor for .NET** – κατεβάστε το από τη [download page](https://releases.groupdocs.com/editor/net/).  
4. **License** – μια [temporary license](https://purchase.groupdocs.com/temporary-license/) είναι εντάξει για δοκιμές· αγοράστε πλήρη άδεια για παραγωγική χρήση.  
5. **Free trial** – μπορείτε επίσης να δοκιμάσετε τη βιβλιοθήκη μέσω της σελίδας [free trial](https://releases.groupdocs.com/).  
6. **Support** – εάν αντιμετωπίσετε προβλήματα, επισκεφθείτε το [support forum](https://forum.groupdocs.com/c/editor/20) ή σκεφτείτε τη [purchase page](https://purchase.groupdocs.com/buy) για πλήρη άδεια.

## Εισαγωγή Namespaces
Πριν ξεκινήσουμε τον κώδικα, πρέπει να εισάγετε τα απαραίτητα namespaces. Προσθέστε τις παρακάτω οδηγίες using στην αρχή του αρχείου `.cs` σας:

```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```

## Πώς να αποθηκεύσετε κάθε καρτέλα Excel ως ξεχωριστό αρχείο;
Φορτώστε το βιβλίο εργασίας, δημιουργήστε ένα `EditableDocument` για κάθε φύλλο και καλέστε `Save` με τη ζητούμενη μορφή. Αυτή η διαδικασία απομονώνει κάθε καρτέλα, σας επιτρέπει να επιλέξετε διαφορετική διαδρομή εξόδου και απελευθερώνει τους πόρους αυτόματα. Παρακάτω είναι η βήμα‑βήμα ροή εργασίας που θα ακολουθήσετε, με εξηγήσεις για κάθε κλήση API και συμβουλές βέλτιστων πρακτικών για αποφυγή κοινών παγίδων.

### Βήμα 1: Λάβετε Διαδρομή στο Αρχείο Εισόδου
Πρώτα, καθορίστε τη πλήρη διαδρομή προς το αρχικό XLSX που περιέχει πολλαπλές καρτέλες.

```csharp
string inputFilePath = "Your Sample Document";
```

### Βήμα 2: Φορτώστε το Λογιστικό Φύλλο στην Περίπτωση του Editor
Η κλάση `Editor` είναι το σημείο εισόδου για όλες τις λειτουργίες εγγράφων στο GroupDocs.Editor. Διαβάζει το ρεύμα αρχείου και προετοιμάζει το έγγραφο για επεξεργασία ή εξαγωγή.

```csharp
using (FileStream inputStream = File.OpenRead(inputFilePath))
{
    using (Editor editor = new Editor(delegate { return inputStream; }, delegate { return new SpreadsheetLoadOptions(); }))
    {
        // Further steps will go here
    }
}
```

### Βήμα 3: Δημιουργήστε ένα EditableDocument από την Πρώτη Καρτέλα
`EditableDocument` αντιπροσωπεύει ένα μοναδικό, επεξεργάσιμο φύλλο μέσα στο βιβλίο εργασίας. Ο κατασκευαστής λαμβάνει την περίπτωση `Editor` και έναν δείκτη φύλλου που αρχίζει από το μηδέν.

```csharp
SpreadsheetEditOptions editOptions1 = new SpreadsheetEditOptions();
editOptions1.WorksheetIndex = 0; // First tab
EditableDocument firstTabBeforeEdit = editor.Edit(editOptions1);
```

### Βήμα 4: Δημιουργήστε ένα EditableDocument από τη Δεύτερη Καρτέλα
Μπορείτε να επαναλάβετε το ίδιο μοτίβο για οποιοδήποτε επιπλέον φύλλο αλλάζοντας την τιμή του δείκτη.

```csharp
SpreadsheetEditOptions editOptions2 = new SpreadsheetEditOptions();
editOptions2.WorksheetIndex = 1; // Second tab
EditableDocument secondTabBeforeEdit = editor.Edit(editOptions2);
```

### Βήμα 5: Αποθηκεύστε την Πρώτη Καρτέλα σε Ξεχωριστό Έγγραφο
`Save` γράφει το επεξεργασμένο έγγραφο σε αρχείο στην καθορισμένη μορφή. Καλέστε το στην περίπτωση `EditableDocument`, παρέχοντας τη διαδρομή εξόδου και τη μορφή (π.χ., `SaveFormat.Xlsx`).

```csharp
SpreadsheetSaveOptions saveOptions1 = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
string outputFilename1 = Path.GetFileNameWithoutExtension(inputFilePath) + "_tab1.xlsm";
string outputPath1 = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename1);
editor.Save(firstTabBeforeEdit, outputPath1, saveOptions1);
```

### Βήμα 6: Αποθηκεύστε τη Δεύτερη Καρτέλα σε Ξεχωριστό Έγγραφο
Η ίδια κλήση `Save` λειτουργεί για το δεύτερο φύλλο, και μπορείτε να επιλέξετε διαφορετική μορφή όπως PDF αν χρειάζεται.

```csharp
SpreadsheetSaveOptions saveOptions2 = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsb);
string outputFilename2 = Path.GetFileNameWithoutExtension(inputFilePath) + "_tab2.xlsb";
string outputPath2 = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename2);
editor.Save(secondTabBeforeEdit, outputPath2, saveOptions2);
```

### Βήμα 7: Αποδεσμεύστε τις Περιπτώσεις EditableDocument
`Dispose` απελευθερώνει μη διαχειριζόμενους πόρους που κρατά το έγγραφο, όπως χειριστές αρχείων, εξασφαλίζοντας ότι δεν υπάρχουν διαρροές σε υπηρεσίες μεγάλης διάρκειας.

```csharp
firstTabBeforeEdit.Dispose();
secondTabBeforeEdit.Dispose();
```

## Συνηθισμένα Προβλήματα και Λύσεις
- **Σφάλματα “File is locked”** – Βεβαιωθείτε ότι καλείτε `Dispose()` σε κάθε `EditableDocument` και στην περίπτωση `Editor`, ή τυλίξτε τα σε δηλώσεις `using`.  
- **Απουσία στυλ μετά την εξαγωγή** – Επαληθεύστε ότι αποθηκεύετε σε μορφή που υποστηρίζει στυλ (π.χ., XLSX ή PDF). Το CSV θα χάσει τη μορφοποίηση κατά σχεδίαση.  
- **Μεγάλα βιβλία εργασίας προκαλούν αργή απόδοση** – Χρησιμοποιήστε τις επιλογές φόρτωσης με ροή (`LoadOptions.Streaming = true`) για να διατηρήσετε τη χρήση μνήμης χαμηλή.

## Συχνές Ερωτήσεις

**Q: Τι γίνεται αν το βιβλίο εργασίας μου περιέχει κρυφά φύλλα;**  
A: Τα κρυφά φύλλα αντιμετωπίζονται όπως οποιοδήποτε άλλο φύλλο· μπορείτε να τα προσπελάσετε με δείκτη και να τα αποθηκεύσετε, αλλά ίσως χρειαστεί να ορίσετε `EditableDocument.IsVisible = true` πριν την αποθήκευση αν θέλετε να είναι ορατά στην έξοδο.

**Q: Μπορώ να μετατρέψω μια καρτέλα Excel απευθείας σε PDF;**  
A: Ναι, καθορίστε `SaveFormat.Pdf` όταν καλείτε `Save` στο `EditableDocument`. Η βιβλιοθήκη διατηρεί τη διάταξη, τις εικόνες και τα διαγράμματα κατά τη μετατροπή.

**Q: Είναι δυνατόν να χωρίσω ένα βιβλίο εργασίας σε αρχεία CSV αντί για XLSX;**  
A: Απόλυτα. Χρησιμοποιήστε `SaveFormat.Csv` για κάθε `EditableDocument` ώστε να δημιουργήσετε απλό‑κείμενο CSV αναπαραστάσεις κάθε φύλλου.

**Q: Υποστηρίζει το GroupDocs.Editor αρχεία Excel με προστασία κωδικού;**  
A: Ναι. Παρέχετε τον κωδικό μέσω `LoadOptions.Password` όταν δημιουργείτε την περίπτωση `Editor`.

**Q: Πού μπορώ να βρω περισσότερα παραδείγματα εργασίας με λογιστικά φύλλα;**  
A: Η επίσημη τεκμηρίωση και τα δείγματα έργων στη [download page](https://releases.groupdocs.com/editor/net/) περιέχουν επιπλέον περιπτώσεις χρήσης.

## Συμπέρασμα
Ακολουθώντας αυτά τα βήματα, μπορείτε να **αποθηκεύσετε κάθε καρτέλα Excel** ως ανεξάρτητο έγγραφο, να μετατρέψετε τις καρτέλες σε PDF ή να χωρίσετε μεγάλα βιβλία εργασίας σε διαχειρίσιμα κομμάτια — όλα με τη αξιόπιστη, υψηλής απόδοσης βιβλιοθήκη GroupDocs.Editor για .NET. Αυτή η δυνατότητα βελτιστοποιεί τις γραμμές αναφοράς, αυτοματοποιεί την εξαγωγή δεδομένων και μειώνει την χειροκίνητη διαχείριση λογιστικών φύλλων.

---

**Last Updated:** 2026-06-06  
**Tested With:** GroupDocs.Editor 23.11 for .NET  
**Author:** GroupDocs  

---

## Σχετικά Μαθήματα

- [Αποκτήστε τον έλεγχο εξαγωγής καρτελών λογιστικού φύλλου σε .NET με το GroupDocs.Editor](/editor/net/spreadsheet-documents/mastering-spreadsheet-tab-extraction-dotnet-groupdocs-editor/)
- [Προστασία Excel με κωδικό χρησιμοποιώντας το GroupDocs.Editor για .NET | Ασφαλής διαχείριση λογιστικών φύλλων](/editor/net/spreadsheet-documents/groupdocs-editor-net-password-excel-files/)
- [Απόκτηση δεξιοτήτων φόρτωσης εγγράφων σε .NET με το GroupDocs.Editor: Ένας ολοκληρωμένος οδηγός](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)