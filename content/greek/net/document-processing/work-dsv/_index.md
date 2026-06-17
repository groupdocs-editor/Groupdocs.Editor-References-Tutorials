---
date: 2026-06-06
description: Μάθετε πώς να **δημιουργείτε επεξεργάσιμα έγγραφα** από αρχεία CSV και
  TSV χρησιμοποιώντας το GroupDocs.Editor για .NET. Αυτός ο οδηγός δείχνει επίσης
  πώς να **διαβάζετε διαχωρισμένο κείμενο C#** και **επεξεργάζεστε CSV .NET** αποδοτικά
  στο Visual Studio.
keywords:
- create editable document
- read delimited text c#
- edit csv .net
- parse delimited values c#
linktitle: Εργασία με διαχωρισμένες τιμές (DSV) – δημιουργία επεξεργάσιμου εγγράφου
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to **create editable document** objects from CSV and TSV
    files using GroupDocs.Editor for .NET. This guide also shows how to **read delimited
    text C#** and **edit CSV .NET** efficiently in Visual Studio.
  headline: Work with Delimited Separated Values (DSV) – create editable document
  type: TechArticle
- questions:
  - answer: Yes, the API streams data and can handle files larger than 1 GB without
      loading the entire document into memory.
    question: Can I use GroupDocs.Editor for .NET to edit large CSV files?
  - answer: Absolutely – any single‑character delimiter (e.g., pipe `|`, semicolon
      `;`) is supported as long as you specify it in `DelimitedTextEditOptions`.
    question: Does GroupDocs.Editor for .NET support other DSV formats besides CSV
      and TSV?
  - answer: Yes, you can set the `Encoding` property in `DelimitedTextSaveOptions`
      to UTF‑8, UTF‑16, ISO‑8859‑1, or any .NET `Encoding` you require.
    question: Is it possible to customize the encoding when saving DSV files?
  - answer: Yes – after editing, simply use `SpreadsheetSaveOptions` to export the
      content as an `.xlsx` workbook.
    question: Can I convert a CSV file to an Excel spreadsheet using GroupDocs.Editor
      for .NET?
  - answer: Detailed API references and code samples are available **[here](https://tutorials.groupdocs.com/editor/net/)**.
    question: Where can I find more documentation on GroupDocs.Editor for .NET?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Εργασία με διαχωρισμένες τιμές (DSV) – δημιουργία επεξεργάσιμου εγγράφου
type: docs
url: /el/net/document-processing/work-dsv/
weight: 12
---

# Εργασία με Διαχωρισμένες Τιμές (DSV) – δημιουργία επεξεργάσιμου εγγράφου

Αν είστε προγραμματιστής .NET που χρειάζεται να **create editable document** αντικείμενα από διαχωρισμένες τιμές (DSV) όπως CSV ή TSV, βρίσκεστε στο σωστό μέρος. Στις πρώτες 100 λέξεις θα εξηγήσουμε γιατί το GroupDocs.Editor για .NET είναι ο πιο αξιόπιστος τρόπος για **read delimited text C#**, να το επεξεργαστείτε και στη συνέχεια να το αποθηκεύσετε ξανά χωρίς να χάσετε τη μορφοποίηση. Θα αποκτήσετε μια πλήρη, έτοιμη για αντιγραφή‑και‑επικόλληση ροή εργασίας που ενσωματώνεται φυσικά σε οποιαδήποτε λύση Visual Studio.

## Γρήγορες Απαντήσεις
- **Ποια βιβλιοθήκη διαχειρίζεται την επεξεργασία CSV καλύτερα στο .NET;** GroupDocs.Editor for .NET.
- **Μπορώ να επεξεργαστώ μεγάλα αρχεία CSV στο Visual Studio;** Yes – the API streams data and avoids loading the whole file into memory.
- **Χρειάζομαι άδεια για παραγωγική χρήση;** A commercial license is required; a free trial is available.
- **Ποια μορφές μπορώ να εξάγω μετά την επεξεργασία;** CSV, TSV, and Excel‑compatible spreadsheet formats.
- **Είναι το API συμβατό με .NET 6+;** Absolutely – it supports .NET Framework 4.5+, .NET Core 3.1+, .NET 5, and .NET 6.

## Τι είναι το “create editable document” στο πλαίσιο του GroupDocs.Editor;
**Create editable document** σημαίνει τη δημιουργία μιας παρουσίας `EditableDocument` που αντιπροσωπεύει μια μεταβλητή έκδοση ενός αρχικού αρχείου (CSV, TSV κ.λπ.) στη μνήμη. Αυτό το αντικείμενο σας επιτρέπει να διαβάσετε, να τροποποιήσετε και να αποθηκεύσετε ξανά το περιεχόμενο χρησιμοποιώντας το ίδιο API. Παρέχει μεθόδους για την ανάκτηση του κειμένου του εγγράφου, την εφαρμογή αλλαγών και την αποθήκευση του ξανά σε διάφορες μορφές, διασφαλίζοντας ότι η στοίχιση των στηλών και τα εισαγωγικά διατηρούνται.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Editor για τη διαχείριση DSV;
Το GroupDocs.Editor επεξεργάζεται **περισσότερες από 50 μορφές εισόδου και εξόδου**, συμπεριλαμβανομένων CSV, TSV και υπολογιστικών φύλλων συμβατών με Excel, ενώ διατηρεί τη χρήση μνήμης κάτω από 10 MB για αρχεία έως 500 MB. Διατηρεί επίσης αυτόματα τη στοίχιση των στηλών, τους κανόνες εισαγωγικών και τις προσαρμοσμένες κωδικοποιήσεις, κάτι που εξαλείφει την ανάγκη για χειροκίνητη λογική ανάλυσης.

## Προαπαιτούμενα
- **Visual Studio** (οποιαδήποτε πρόσφατη έκδοση) – θα αναπτύσσετε και θα κάνετε αποσφαλμάτωση απευθείας μέσα στο IDE.
- **GroupDocs.Editor for .NET** – κατεβάστε το πιο πρόσφατο πακέτο **[here](https://releases.groupdocs.com/editor/net/)**.
- **Βασικές γνώσεις C#** – το tutorial υποθέτει ότι μπορείτε να δημιουργήσετε ένα έργο console ή ASP.NET και να προσθέσετε πακέτα NuGet.

## Εισαγωγή Χώρων Ονομάτων
Οι κλάσεις `Editor`, `EditableDocument` και οι κλάσεις επιλογών βρίσκονται στον χώρο ονομάτων `GroupDocs.Editor`.  

Η κλάση `DelimitedTextEditOptions` είναι το σημείο εισόδου για τον ορισμό του διαχωριστικού (κόμμα, tab κ.λπ.) και άλλων κανόνων ανάλυσης.

```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

## Πώς να δημιουργήσετε επεξεργάσιμο έγγραφο από αρχείο CSV;
Φορτώστε το αρχικό CSV με το `Editor` και καλέστε τη μέθοδο `Edit`, περνώντας μια παρουσία `DelimitedTextEditOptions` που καθορίζει διαχωριστικό κόμμα. Η μέθοδος επιστρέφει ένα `EditableDocument` που μπορείτε να χειριστείτε στη μνήμη. Αυτό το μοτίβο δύο βημάτων—load → edit— καλύπτει σενάρια **read delimited text C#** και εγγυάται ότι η αρχική δομή του αρχείου διατηρείται.

## Βήμα 1: Λάβετε Διαδρομή προς το Εισαγωγικό Αρχείο DSV
Πρώτα, πρέπει να καθορίσετε την απόλυτη ή σχετική διαδρομή προς το αρχικό αρχείο DSV. Για επίδειξη, θα χρησιμοποιήσουμε ένα απλό CSV που βρίσκεται στον φάκελο `Data` του έργου.

```csharp
string inputFilePath = "Your Sample Document";
```

## Βήμα 2: Δημιουργία Παράδειγματος Editor
`Editor` είναι η κεντρική κλάση που οργανώνει τη φόρτωση, την επεξεργασία και την αποθήκευση. Η δημιουργία ενός αντικειμένου με `FileInfo` σας δίνει πλήρη έλεγχο του κύκλου ζωής του αρχείου.

```csharp
using (Editor editor = new Editor(inputFilePath))
{
```

## Βήμα 3: Δημιουργία Επιλογών Επεξεργασίας DSV
`DelimitedTextEditOptions` καθορίζει στον editor πώς να ερμηνεύσει το αρχείο. Μπορείτε να ορίσετε το διαχωριστικό, αν η πρώτη γραμμή περιέχει κεφαλίδες, και την κωδικοποίηση χαρακτήρων.

```csharp
    Options.DelimitedTextEditOptions editOptions = new DelimitedTextEditOptions(",");
    editOptions.ConvertDateTimeData = false;
    editOptions.ConvertNumericData = true;
    editOptions.TreatConsecutiveDelimitersAsOne = true;
```

## Βήμα 4: Δημιουργία Παράδειγματος EditableDocument
`EditableDocument` αντιπροσωπεύει μια μεταβλητή έκδοση του αρχείου στη μνήμη. Καλώντας `Editor.Edit` με τις επιλογές επιστρέφει ένα `EditableDocument`. Αυτό το αντικείμενο κρατά το κείμενο του αρχείου σε μια μεταβλητή συμβολοσειρά, έτοιμο για οποιαδήποτε λειτουργία **parse delimited values C#** χρειάζεστε.

```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```

## Βήμα 5: Επεξεργασία Περιεχομένου Εγγράφου
`GetDocumentText()` επιστρέφει το τρέχον κείμενο του επεξεργάσιμου εγγράφου ως συμβολοσειρά. Ανακτήστε το αρχικό κείμενο μέσω `EditableDocument.GetDocumentText()`, εκτελέστε τις τροποποιήσεις σας (π.χ., αντικατάσταση τιμής στήλης) και αποθηκεύστε το αποτέλεσμα σε μια νέα συμβολοσειρά. Εδώ είναι όπου μπορείτε να **edit CSV .NET** χωρίς να αγγίξετε ροές αρχείων χαμηλού επιπέδου.

```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("SsangYong", "Chevrolet").Replace("Kyron", "Camaro");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```

## Βήμα 6: Δημιουργία EditableDocument με Ενημερωμένο Περιεχόμενο
Τυλίξτε τη τροποποιημένη συμβολοσειρά ξανά σε ένα `EditableDocument`. Αυτό το βήμα ολοκληρώνει τις αλλαγές και προετοιμάζει το αντικείμενο για αποθήκευση σε οποιαδήποτε υποστηριζόμενη μορφή.

```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```

## Βήμα 7: Δημιουργία Επιλογών Αποθήκευσης CSV
`DelimitedTextSaveOptions` καθορίζει πώς να γράψετε το επεξεργασμένο περιεχόμενο πίσω σε αρχείο CSV. Όταν είστε έτοιμοι να αποθηκεύσετε τις αλλαγές, διαμορφώστε το `DelimitedTextSaveOptions`. Μπορείτε να ορίσετε το ίδιο διαχωριστικό, διαφορετικό, ή ακόμη και να αλλάξετε το στυλ λήξης γραμμής.

```csharp
    Options.DelimitedTextSaveOptions csvSaveOptions = new DelimitedTextSaveOptions(",");
    csvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

## Βήμα 8: Δημιουργία Επιλογών Αποθήκευσης TSV
Αν χρειάζεστε μια έκδοση διαχωρισμένη με tab, απλώς αλλάξτε το διαχωριστικό σε `\t`. Το ίδιο `EditableDocument` μπορεί να αποθηκευτεί πολλές φορές με διαφορετικές επιλογές.

```csharp
    Options.DelimitedTextSaveOptions tsvSaveOptions = new DelimitedTextSaveOptions("\t");
    tsvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

## Βήμα 9: Δημιουργία Επιλογών Αποθήκευσης Φύλλου Υπολογιστικού
`SpreadsheetSaveOptions` διαμορφώνει την εξαγωγή του εγγράφου σε μορφές συμβατές με Excel όπως .xlsx. Το GroupDocs.Editor επίσης σας επιτρέπει να εξάγετε τα επεξεργασμένα δεδομένα σε μορφή συμβατή με Excel (`.xlsx`). Η κλάση `SpreadsheetSaveOptions` διαχειρίζεται αυτόματα τύπους στηλών, τύπους και στυλ κελιών.

```csharp
    Options.SpreadsheetSaveOptions cellsSaveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
```

## Βήμα 10: Προετοιμασία Διαδρομών Αποθήκευσης
Ορίστε ξεχωριστές διαδρομές εξόδου για κάθε μορφή. Η χρήση σαφών συμβάσεων ονοματοδοσίας (π.χ., `output.csv`, `output.tsv`, `output.xlsx`) βοηθά στην οργάνωση του έργου σας.

```csharp
    string outputCsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".csv");
    string outputTsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".tsv");
    string outputCellsPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".xlsm");
```

## Βήμα 11: Αποθήκευση του Επεξεργασμένου Εγγράφου
`Save()` γράφει το έγγραφο στο δίσκο χρησιμοποιώντας τις παρεχόμενες επιλογές αποθήκευσης. Καλείτε το `EditableDocument.Save` με τις κατάλληλες επιλογές για κάθε μορφή προορισμού. Το API γράφει το αρχείο απευθείας στο δίσκο, διατηρώντας την αρχική κωδικοποίηση εκτός αν την αντικαταστήσετε.

```csharp
    editor.Save(afterEdit, outputCsvPath, csvSaveOptions);
    editor.Save(afterEdit, outputTsvPath, tsvSaveOptions);
    editor.Save(afterEdit, outputCellsPath, cellsSaveOptions);
```

## Βήμα 12: Αποδέσμευση Παραδειγμάτων EditableDocument
Τanto `Editor` όσο και `EditableDocument` υλοποιούν το `IDisposable`. Η αποδέσμευση τους ελευθερώνει τους χειριστές αρχείων και τους μη διαχειριζόμενους πόρους, κάτι που είναι κρίσιμο όταν επεξεργάζεστε πολλά αρχεία σε μια παρτίδα εργασιών.

```csharp
    beforeEdit.Dispose();
    afterEdit.Dispose();
}
System.Console.WriteLine("WorkingWithDsv routine has successfully finished");
```

## Συχνά Προβλήματα και Λύσεις
| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|---|---|---|
| **Απρόσμενα επιπλέον εισαγωγικά** | Ο προεπιλεγμένος αναλυτής CSV μπορεί να θεωρεί ενσωματωμένα κόμματα ως διαχωριστικά. | Ορίστε `EscapeMode = EscapeMode.DoubleQuote` στο `DelimitedTextEditOptions`. |
| **Αύξηση μνήμης σε μεγάλο αρχείο** | Φόρτωση αρχείου 500 MB χωρίς ροή. | Χρησιμοποιήστε `Editor.Load` με `LoadOptions` που ενεργοποιούν lazy loading. |
| **Ασυμφωνία κωδικοποίησης** | Το αρχείο προέλευσης χρησιμοποιεί UTF‑16 αλλά οι επιλογές προεπιλογής είναι UTF‑8. | Ορίστε ρητά `Encoding = Encoding.Unicode` στις επιλογές αποθήκευσης. |

## Συχνές Ερωτήσεις

**Q: Μπορώ να χρησιμοποιήσω το GroupDocs.Editor για .NET για την επεξεργασία μεγάλων αρχείων CSV;**  
A: Yes, the API streams data and can handle files larger than 1 GB without loading the entire document into memory.

**Q: Το GroupDocs.Editor για .NET υποστηρίζει άλλες μορφές DSV εκτός από CSV και TSV;**  
A: Absolutely – any single‑character delimiter (e.g., pipe `|`, semicolon `;`) is supported as long as you specify it in `DelimitedTextEditOptions`.

**Q: Είναι δυνατόν να προσαρμόσετε την κωδικοποίηση κατά την αποθήκευση αρχείων DSV;**  
A: Yes, you can set the `Encoding` property in `DelimitedTextSaveOptions` to UTF‑8, UTF‑16, ISO‑8859‑1, or any .NET `Encoding` you require.

**Q: Μπορώ να μετατρέψω ένα αρχείο CSV σε φύλλο Excel χρησιμοποιώντας το GroupDocs.Editor για .NET;**  
A: Yes – after editing, simply use `SpreadsheetSaveOptions` to export the content as an `.xlsx` workbook.

**Q: Πού μπορώ να βρω περισσότερη τεκμηρίωση για το GroupDocs.Editor για .NET;**  
A: Detailed API references and code samples are available **[here](https://tutorials.groupdocs.com/editor/net/)**.

**Last Updated:** 2026-06-06  
**Tested With:** GroupDocs.Editor 23.10 for .NET  
**Author:** GroupDocs

## Σχετικά Μαθήματα

- [Οδηγοί Επεξεργασίας Απλού Κειμένου και Εγγράφων DSV για το GroupDocs.Editor .NET](/editor/net/plain-text-dsv-documents/)
- [Κατακτήστε το GroupDocs.Editor .NET για Αποτελεσματική Επεξεργασία και Μετατροπή Εγγράφων CSV](/editor/net/plain-text-dsv-documents/groupdocs-editor-net-csv-editing-guide/)
- [Απόκτηση Εξαιρετικής Φόρτωσης Εγγράφων σε .NET με το GroupDocs.Editor: Ένας Πλήρης Οδηγός](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)