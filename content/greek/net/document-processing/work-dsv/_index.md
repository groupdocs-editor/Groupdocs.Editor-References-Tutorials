---
title: Εργασία με οριοθετημένες διαχωρισμένες τιμές (DSV)
linktitle: Εργασία με οριοθετημένες διαχωρισμένες τιμές (DSV)
second_title: GroupDocs.Editor .NET API
description: Μάθετε πώς να επεξεργάζεστε αρχεία CSV και TSV χρησιμοποιώντας το GroupDocs.Editor για .NET με αυτόν τον οδηγό βήμα προς βήμα. Βελτιώστε τα έργα σας .NET χωρίς κόπο.
type: docs
weight: 12
url: /el/net/document-processing/work-dsv/
---
## Εισαγωγή
Εάν είστε προγραμματιστής που εργάζεται με οριοθετημένες διαχωρισμένες τιμές (DSV), όπως αρχεία CSV ή TSV, γνωρίζετε ότι η επεξεργασία αυτών των αρχείων μέσω προγραμματισμού μπορεί να είναι μια τρομακτική εργασία. Ωστόσο, με το GroupDocs.Editor για .NET, αυτή η εργασία γίνεται σημαντικά πιο απλή και αποτελεσματική. Σε αυτό το σεμινάριο, θα σας καθοδηγήσουμε στον τρόπο χρήσης του GroupDocs.Editor για .NET για ανάγνωση, επεξεργασία και αποθήκευση αρχείων DSV. Θα αναλύσουμε τη διαδικασία σε βήματα που ακολουθούνται εύκολα, καθιστώντας την απλή για εσάς να την εφαρμόσετε στα έργα σας.
## Προαπαιτούμενα
Πριν ξεκινήσουμε το σεμινάριο, βεβαιωθείτε ότι έχετε τις ακόλουθες προϋποθέσεις:
- Visual Studio: Βεβαιωθείτε ότι έχετε εγκαταστήσει το Visual Studio στον υπολογιστή σας.
-  GroupDocs.Editor για .NET: Θα χρειαστεί να πραγματοποιήσετε λήψη και αναφορά στη βιβλιοθήκη GroupDocs.Editor για .NET. Μπορείτε να το κατεβάσετε[εδώ](https://releases.groupdocs.com/editor/net/).
- Βασική κατανόηση της C#: Αυτό το σεμινάριο προϋποθέτει ότι έχετε βασική κατανόηση της ανάπτυξης C# και .NET.
## Εισαγωγή χώρων ονομάτων
Αρχικά, πρέπει να εισαγάγετε τους απαραίτητους χώρους ονομάτων στο έργο σας. Αυτοί οι χώροι ονομάτων παρέχουν τις κλάσεις και τις μεθόδους που απαιτούνται για την εργασία με το GroupDocs.Editor για .NET.
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

## Βήμα 1: Λάβετε μια διαδρομή προς το αρχείο εισόδου DSV
Αρχικά, πρέπει να καθορίσετε τη διαδρομή προς το αρχείο εισόδου DSV. Για αυτό το παράδειγμα, θα υποθέσουμε ότι πρόκειται για αρχείο CSV.
```csharp
string inputFilePath = "Your Sample Document";
```
## Βήμα 2: Δημιουργήστε μια παρουσία προγράμματος επεξεργασίας
 Δημιουργήστε ένα παράδειγμα του`Editor` τάξη. Αυτή η παρουσία θα χρησιμοποιηθεί για τη φόρτωση και τον χειρισμό του αρχείου DSV.
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## Βήμα 3: Δημιουργήστε Επιλογές Επεξεργασίας DSV
 Στη συνέχεια, δημιουργήστε ένα παράδειγμα του`DelimitedTextEditOptions` και καθορίστε τον οριοθέτη για το αρχείο DSV. Εδώ, χρησιμοποιούμε κόμμα ως οριοθέτη.
```csharp
    Options.DelimitedTextEditOptions editOptions = new DelimitedTextEditOptions(",");
    editOptions.ConvertDateTimeData = false;
    editOptions.ConvertNumericData = true;
    editOptions.TreatConsecutiveDelimitersAsOne = true;
```
## Βήμα 4: Δημιουργήστε ένα EditableDocument Instance
 Δημιουργήστε ένα`EditableDocument` παράδειγμα χρησιμοποιώντας το`Editor.Edit` μέθοδος. Αυτό προετοιμάζει το έγγραφο για επεξεργασία.
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## Βήμα 5: Επεξεργαστείτε το περιεχόμενο του εγγράφου
Ανακτήστε το αρχικό περιεχόμενο κειμένου και κάντε τις απαραίτητες τροποποιήσεις. Για λόγους επίδειξης, ας αντικαταστήσουμε κάποιο κείμενο.
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("SsangYong", "Chevrolet").Replace("Kyron", "Camaro");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## Βήμα 6: Δημιουργήστε ένα Επεξεργάσιμο Έγγραφο με Ενημερωμένο Περιεχόμενο
 Δημιούργησε ένα νέο`EditableDocument` με το ενημερωμένο περιεχόμενο.
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## Βήμα 7: Δημιουργία επιλογών αποθήκευσης CSV
Καθορίστε τις επιλογές αποθήκευσης για τη μορφή CSV, συμπεριλαμβανομένου του οριοθέτη και της κωδικοποίησης.
```csharp
    Options.DelimitedTextSaveOptions csvSaveOptions = new DelimitedTextSaveOptions(",");
    csvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## Βήμα 8: Δημιουργία επιλογών αποθήκευσης TSV
Ομοίως, καθορίστε τις επιλογές αποθήκευσης για τη μορφή TSV.
```csharp
    Options.DelimitedTextSaveOptions tsvSaveOptions = new DelimitedTextSaveOptions("\t");
    tsvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## Βήμα 9: Δημιουργία επιλογών αποθήκευσης υπολογιστικού φύλλου
Εάν πρέπει να αποθηκεύσετε το έγγραφο ως υπολογιστικό φύλλο, δημιουργήστε τις αντίστοιχες επιλογές αποθήκευσης.
```csharp
    Options.SpreadsheetSaveOptions cellsSaveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
```
## Βήμα 10: Προετοιμάστε τις διαδρομές αποθήκευσης
Καθορίστε τις διαδρομές όπου θα αποθηκευτούν τα επεξεργασμένα αρχεία.
```csharp
    string outputCsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".csv");
    string outputTsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".tsv");
    string outputCellsPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".xlsm");
```
## Βήμα 11: Αποθηκεύστε το επεξεργασμένο έγγραφο
Αποθηκεύστε το επεξεργασμένο έγγραφο στις καθορισμένες διαδρομές σε διαφορετικές μορφές.
```csharp
    editor.Save(afterEdit, outputCsvPath, csvSaveOptions);
    editor.Save(afterEdit, outputTsvPath, tsvSaveOptions);
    editor.Save(afterEdit, outputCellsPath, cellsSaveOptions);
```
## Βήμα 12: Απόρριψη παρουσιών EditableDocument
 Τέλος, φροντίστε να απορρίψετε το`EditableDocument` περιπτώσεις για την απελευθέρωση πόρων.
```csharp
    beforeEdit.Dispose();
    afterEdit.Dispose();
}
System.Console.WriteLine("WorkingWithDsv routine has successfully finished");
```
## συμπέρασμα
Η επεξεργασία αρχείων DSV χρησιμοποιώντας το GroupDocs.Editor για .NET είναι μια απλή διαδικασία που περιλαμβάνει τη δημιουργία μιας παρουσίας επεξεργασίας, τον ορισμό επιλογών επεξεργασίας, την τροποποίηση του περιεχομένου και την αποθήκευση των αλλαγών. Αυτός ο οδηγός βήμα προς βήμα θα σας βοηθήσει να ενσωματώσετε αυτή τη λειτουργικότητα στις εφαρμογές σας .NET με ευκολία. Είτε εργάζεστε με CSV, TSV ή άλλες μορφές DSV, το GroupDocs.Editor για .NET παρέχει μια ισχυρή και ευέλικτη λύση.
## Συχνές ερωτήσεις
### Μπορώ να χρησιμοποιήσω το GroupDocs.Editor για .NET για να επεξεργαστώ μεγάλα αρχεία CSV;
Ναι, το GroupDocs.Editor για .NET είναι σε θέση να χειρίζεται μεγάλα αρχεία CSV αποτελεσματικά.
### Το GroupDocs.Editor για .NET υποστηρίζει άλλες μορφές DSV εκτός από το CSV και το TSV;
Ναι, υποστηρίζει διάφορες μορφές DSV αρκεί να καθορίσετε τον κατάλληλο οριοθέτη.
### Είναι δυνατή η προσαρμογή της κωδικοποίησης κατά την αποθήκευση αρχείων DSV;
Οπωσδήποτε, μπορείτε να καθορίσετε την επιθυμητή κωδικοποίηση στις επιλογές αποθήκευσης.
### Μπορώ να μετατρέψω ένα αρχείο CSV σε υπολογιστικό φύλλο Excel χρησιμοποιώντας το GroupDocs.Editor για .NET;
Ναι, μπορείτε να αποθηκεύσετε ένα αρχείο CSV ως υπολογιστικό φύλλο Excel χρησιμοποιώντας τις κατάλληλες επιλογές αποθήκευσης.
### Πού μπορώ να βρω περισσότερη τεκμηρίωση για το GroupDocs.Editor για .NET;
 Μπορείτε να βρείτε αναλυτική τεκμηρίωση[εδώ](https://reference.groupdocs.com/editor/net/)