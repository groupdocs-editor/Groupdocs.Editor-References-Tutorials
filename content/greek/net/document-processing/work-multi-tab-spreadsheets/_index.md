---
title: Εργαστείτε με υπολογιστικά φύλλα πολλαπλών καρτελών
linktitle: Εργαστείτε με υπολογιστικά φύλλα πολλαπλών καρτελών
second_title: GroupDocs.Editor .NET API
description: Μάθετε πώς να εργάζεστε με υπολογιστικά φύλλα πολλών καρτελών στο .NET χρησιμοποιώντας το GroupDocs.Editor. Περιλαμβάνονται οδηγός βήμα προς βήμα, παραδείγματα κώδικα και βέλτιστες πρακτικές.
weight: 17
url: /el/net/document-processing/work-multi-tab-spreadsheets/
type: docs
---
# Εργαστείτε με υπολογιστικά φύλλα πολλαπλών καρτελών

## Εισαγωγή
Ο χειρισμός υπολογιστικών φύλλων πολλαπλών καρτελών μπορεί να είναι αρκετά δύσκολος, ειδικά όταν χρειάζεται να χειριστείτε ή να εξαγάγετε δεδομένα από διαφορετικά φύλλα μέσα στο ίδιο έγγραφο. Εάν εργάζεστε με .NET και αναζητάτε μια ισχυρή λύση, το GroupDocs.Editor για .NET είναι μια εξαιρετική επιλογή. Σε αυτό το σεμινάριο, θα σας καθοδηγήσουμε στη διαδικασία εργασίας με υπολογιστικά φύλλα πολλών καρτελών χρησιμοποιώντας το GroupDocs.Editor για .NET. Θα καλύψουμε τα πάντα, από τη ρύθμιση του περιβάλλοντος σας έως την αποθήκευση κάθε καρτέλας ως ξεχωριστό αρχείο.
## Προαπαιτούμενα
Πριν ξεκινήσετε το σεμινάριο, βεβαιωθείτε ότι έχετε τις ακόλουθες προϋποθέσεις:
1. Visual Studio: Βεβαιωθείτε ότι έχετε εγκαταστήσει το Visual Studio στον υπολογιστή σας.
2. .NET Framework: Το GroupDocs.Editor για .NET υποστηρίζει .NET Framework 4.0 ή νεότερη έκδοση.
3. GroupDocs.Editor για .NET: Πραγματοποιήστε λήψη και εγκατάσταση της βιβλιοθήκης GroupDocs.Editor για .NET. Μπορείτε να το πάρετε από το[σελίδα λήψης](https://releases.groupdocs.com/editor/net/).
4.  Άδεια χρήσης: Ενώ μπορείτε να χρησιμοποιήσετε α[προσωρινή άδεια](https://purchase.groupdocs.com/temporary-license/) Για να δοκιμάσετε τη βιβλιοθήκη, συνιστάται να αγοράσετε μια πλήρη άδεια χρήσης για παραγωγή.
## Εισαγωγή χώρων ονομάτων
Πριν ξεκινήσουμε την κωδικοποίηση, πρέπει να εισαγάγετε τους απαραίτητους χώρους ονομάτων. Προσθέστε τα ακόλουθα χρησιμοποιώντας οδηγίες στην κορυφή του αρχείου σας .cs:
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
## 1. Λάβετε μια διαδρομή προς το αρχείο εισόδου
Αρχικά, πρέπει να καθορίσετε τη διαδρομή προς το αρχείο υπολογιστικού φύλλου εισόδου. Αυτό το αρχείο πρέπει να είναι XLSX (OOXML) με πολλές καρτέλες.
```csharp
string inputFilePath = "Your Sample Document";
```
## 2. Τοποθετήστε το υπολογιστικό φύλλο στην παρουσία του επεξεργαστή
 Στη συνέχεια, θα φορτώσετε το υπολογιστικό φύλλο σε ένα`Editor` παράδειγμα. Αυτό γίνεται χρησιμοποιώντας μια ροή αρχείων και καθορίζοντας τις κατάλληλες επιλογές φόρτωσης για ένα υπολογιστικό φύλλο.
```csharp
using (FileStream inputStream = File.OpenRead(inputFilePath))
{
    using (Editor editor = new Editor(delegate { return inputStream; }, delegate { return new SpreadsheetLoadOptions(); }))
    {
        // Τα περαιτέρω βήματα θα πάνε εδώ
    }
}
```
## 3. Δημιουργήστε ένα EditableDocument από την Πρώτη καρτέλα
 Για να επεξεργαστείτε ή να χειριστείτε μια συγκεκριμένη καρτέλα, πρέπει να δημιουργήσετε μια`EditableDocument` παράδειγμα για αυτήν την καρτέλα. Η καρτέλα καθορίζεται χρησιμοποιώντας ένα ευρετήριο που βασίζεται στο 0.
```csharp
SpreadsheetEditOptions editOptions1 = new SpreadsheetEditOptions();
editOptions1.WorksheetIndex = 0; // Πρώτη καρτέλα
EditableDocument firstTabBeforeEdit = editor.Edit(editOptions1);
```
## 4. Δημιουργήστε ένα EditableDocument από τη δεύτερη καρτέλα
 Ομοίως, δημιουργήστε ένα`EditableDocument` για τη δεύτερη καρτέλα.
```csharp
SpreadsheetEditOptions editOptions2 = new SpreadsheetEditOptions();
editOptions2.WorksheetIndex = 1; // Δεύτερη καρτέλα
EditableDocument secondTabBeforeEdit = editor.Edit(editOptions2);
```
## 5. Αποθηκεύστε την Πρώτη καρτέλα σε ξεχωριστό έγγραφο
Τώρα, αποθηκεύστε την πρώτη καρτέλα ως ξεχωριστό έγγραφο. Καθορίστε τη μορφή αποθήκευσης και τη διαδρομή εξόδου.
```csharp
SpreadsheetSaveOptions saveOptions1 = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
string outputFilename1 = Path.GetFileNameWithoutExtension(inputFilePath) + "_tab1.xlsm";
string outputPath1 = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename1);
editor.Save(firstTabBeforeEdit, outputPath1, saveOptions1);
```
## 6. Αποθηκεύστε τη δεύτερη καρτέλα σε ένα ξεχωριστό έγγραφο
Επαναλάβετε τη διαδικασία για τη δεύτερη καρτέλα, αλλά αυτή τη φορά αποθηκεύστε την σε διαφορετική μορφή.
```csharp
SpreadsheetSaveOptions saveOptions2 = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsb);
string outputFilename2 = Path.GetFileNameWithoutExtension(inputFilePath) + "_tab2.xlsb";
string outputPath2 = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename2);
editor.Save(secondTabBeforeEdit, outputPath2, saveOptions2);
```
## 7. Απορρίψτε τις περιπτώσεις EditableDocument
 Τέλος, βεβαιωθείτε ότι έχετε απορρίψει σωστά`EditableDocument` περιπτώσεις για την απελευθέρωση πόρων.
```csharp
firstTabBeforeEdit.Dispose();
secondTabBeforeEdit.Dispose();
```

## συμπέρασμα
Ακολουθώντας αυτά τα βήματα, μπορείτε εύκολα να εργαστείτε με υπολογιστικά φύλλα πολλών καρτελών στο .NET χρησιμοποιώντας το GroupDocs.Editor. Αυτή η ισχυρή βιβλιοθήκη απλοποιεί τη διαδικασία επεξεργασίας και αποθήκευσης διαφορετικών φύλλων σε ένα υπολογιστικό φύλλο, καθιστώντας τις εργασίες ανάπτυξης πιο διαχειρίσιμες. Είτε έχετε να κάνετε με πολύπλοκο χειρισμό δεδομένων είτε με απλές επεξεργασίες, το GroupDocs.Editor για .NET παρέχει τα εργαλεία που χρειάζεστε για να κάνετε τη δουλειά αποτελεσματικά.
## Συχνές ερωτήσεις
### Τι είναι το GroupDocs.Editor για .NET;
Το GroupDocs.Editor για .NET είναι ένα ισχυρό API επεξεργασίας εγγράφων που επιτρέπει στους προγραμματιστές να φορτώνουν, να επεξεργάζονται και να αποθηκεύουν έγγραφα διαφόρων μορφών σε εφαρμογές .NET.
### Μπορώ να δοκιμάσω το GroupDocs.Editor για .NET πριν το αγοράσω;
 Ναι, μπορείτε να χρησιμοποιήσετε ένα[δωρεάν δοκιμή](https://releases.groupdocs.com/) ή ζητήστε α[προσωρινή άδεια](https://purchase.groupdocs.com/temporary-license/) για την αξιολόγηση του προϊόντος.
### Ποιες μορφές αρχείων υποστηρίζονται από το GroupDocs.Editor για .NET;
Το GroupDocs.Editor υποστηρίζει ένα ευρύ φάσμα μορφών, συμπεριλαμβανομένων των DOCX, XLSX, PPTX, PDF και πολλών άλλων.
### Πώς μπορώ να λάβω υποστήριξη για το GroupDocs.Editor για .NET;
 Μπορείτε να λάβετε υποστήριξη μεταβαίνοντας στο[φόρουμ υποστήριξης](https://forum.groupdocs.com/c/editor/20).
### Πού μπορώ να αγοράσω μια πλήρη άδεια χρήσης για το GroupDocs.Editor για .NET;
 Μπορείτε να αγοράσετε μια πλήρη άδεια χρήσης από το[σελίδα αγοράς](https://purchase.groupdocs.com/buy).