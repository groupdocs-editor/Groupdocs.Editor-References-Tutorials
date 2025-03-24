---
title: Εργαστείτε με υπολογιστικά φύλλα που προστατεύονται με κωδικό πρόσβασης
linktitle: Εργαστείτε με υπολογιστικά φύλλα που προστατεύονται με κωδικό πρόσβασης
second_title: GroupDocs.Editor .NET API
description: Μάθετε πώς να χειρίζεστε υπολογιστικά φύλλα που προστατεύονται με κωδικό πρόσβασης χρησιμοποιώντας το GroupDocs.Editor για .NET. Αυτός ο λεπτομερής οδηγός σας καθοδηγεί στο άνοιγμα στην αποθήκευση ασφαλών αρχείων Excel.
weight: 18
url: /el/net/document-processing/work-password-protected-spreadsheets/
---
## Εισαγωγή
Δυσκολεύεστε να διαχειριστείτε υπολογιστικά φύλλα που προστατεύονται με κωδικό πρόσβασης στις εφαρμογές σας .NET; Αν ναι, είστε στο σωστό μέρος! Σε αυτόν τον αναλυτικό οδηγό, θα σας καθοδηγήσουμε στη διαδικασία χρήσης του GroupDocs.Editor για .NET για τον αποτελεσματικό χειρισμό υπολογιστικών φύλλων που προστατεύονται με κωδικό πρόσβασης. Μέχρι το τέλος αυτού του σεμιναρίου, θα είστε καλά εξοπλισμένοι για να ανοίγετε, να επεξεργάζεστε και να αποθηκεύετε κρυπτογραφημένα αρχεία Excel με ευκολία.
## Προαπαιτούμενα
Πριν βουτήξετε στον κώδικα, ας βεβαιωθούμε ότι έχετε όλα όσα χρειάζεται να ακολουθήσετε:
- Βασικές γνώσεις C#: Αυτό το σεμινάριο προϋποθέτει ότι είστε εξοικειωμένοι με τον προγραμματισμό C#.
- .NET Framework: Βεβαιωθείτε ότι έχετε εγκαταστήσει το πλαίσιο .NET στο μηχάνημα ανάπτυξης.
-  GroupDocs.Editor για .NET: Λήψη και εγκατάσταση του GroupDocs.Editor για .NET από[εδώ](https://releases.groupdocs.com/editor/net/).
## Εισαγωγή χώρων ονομάτων
Για να ξεκινήσετε, θα χρειαστεί να εισαγάγετε τους απαραίτητους χώρους ονομάτων στο έργο σας C#. Αυτοί οι χώροι ονομάτων παρέχουν πρόσβαση στις λειτουργίες του GroupDocs.Editor.
```csharp
using System;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
## Βήμα 1: Λάβετε μια διαδρομή προς το αρχείο εισόδου
Αρχικά, θα χρειαστείτε μια διαδρομή προς το αρχείο εισόδου. Για αυτό το παράδειγμα, θα χρησιμοποιήσουμε ένα δείγμα αρχείου Excel (`Your Sample Document`) που προστατεύεται με κωδικό πρόσβασης.
```csharp
string inputFilePath = "Your Sample Document";
```
## Βήμα 2: Προσπαθήστε να ανοίξετε το έγγραφο χωρίς κωδικό πρόσβασης
Ας δούμε τι θα συμβεί αν προσπαθήσουμε να ανοίξουμε το έγγραφο χωρίς να παρέχουμε κωδικό πρόσβασης.
```csharp
Editor editor = new Editor(inputFilePath);
try
{
    editor.Edit();
}
catch (GroupDocs.Editor.PasswordRequiredException)
{
    Console.WriteLine("Cannot edit the document because it is password-protected. A password is required.");
}
editor.Dispose();
```
## Βήμα 3: Δοκιμάστε να καθορίσετε έναν λανθασμένο κωδικό πρόσβασης
Τώρα, θα καθορίσουμε έναν εσφαλμένο κωδικό πρόσβασης για να δείξουμε πώς αποκρίνεται ο επεξεργαστής.
```csharp
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.Password = "incorrect_password";
editor = new Editor(inputFilePath, delegate { return loadOptions; });
try
{
    editor.Edit();
}
catch (GroupDocs.Editor.IncorrectPasswordException)
{
    Console.WriteLine("Cannot edit the document because the specified password is incorrect.");
}
editor.Dispose();
```
## Βήμα 4: Ανοίξτε το Αρχείο με τον σωστό κωδικό πρόσβασης
Ας δώσουμε τον σωστό κωδικό πρόσβασης και ας ανοίξουμε το αρχείο με επιτυχία.
```csharp
loadOptions.Password = "excel_password";
loadOptions.OptimizeMemoryUsage = true;
editor = new Editor(inputFilePath, delegate { return loadOptions; });
```
## Βήμα 5: Δημιουργία και προσαρμογή επιλογών επεξεργασίας
Για να επεξεργαστούμε το υπολογιστικό φύλλο, πρέπει να δημιουργήσουμε και να προσαρμόσουμε τις επιλογές επεξεργασίας.
```csharp
SpreadsheetEditOptions editOptions = new SpreadsheetEditOptions();
```
## Βήμα 6: Δημιουργήστε ένα Ενδιάμεσο Επεξεργάσιμο Έγγραφο
 Στη συνέχεια, δημιουργούμε ένα ενδιάμεσο`EditableDocument` που μας επιτρέπει να κάνουμε αλλαγές στο υπολογιστικό φύλλο.
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
{
    // Βήμα 7: Δημιουργία επιλογών αποθήκευσης
    SpreadsheetFormats xlsmFormat = SpreadsheetFormats.Xlsm;
    SpreadsheetSaveOptions saveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
    // Βήμα 7.1: Ορισμός νέου κωδικού πρόσβασης ανοίγματος
    saveOptions.Password = "new password";
    // Βήμα 7.2: Ορισμός Προστασίας Εγγραφής
    saveOptions.WorksheetProtection = new WorksheetProtection(WorksheetProtectionType.All, "write password");
    // Βήμα 8: Αποθηκεύστε το έγγραφο χωρίς τροποποίηση
    //Βήμα 8.1: Προετοιμάστε το Όνομα αρχείου και τη διαδρομή εξόδου
    string outputFilename = Path.GetFileNameWithoutExtension(inputFilePath) + "." + xlsmFormat.Extension;
    string outputPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename);
    // Βήμα 8.2: Δημιουργία ροής εξόδου
    using (FileStream outputStream = File.Create(outputPath))
    {
        // Βήμα 8.3: Αποθήκευση
        editor.Save(beforeEdit, outputStream, saveOptions);
    }
}
// Βήμα 9: Απορρίψτε την παρουσία του Editor
editor.Dispose();
Console.WriteLine("Successfully handled the password-protected spreadsheet. Editor instance has been disposed: {0}", editor.IsDisposed ? "Yes" : "No");
```
## συμπέρασμα
Συγχαρητήρια! Έχετε μάθει με επιτυχία πώς να χειρίζεστε υπολογιστικά φύλλα που προστατεύονται με κωδικό πρόσβασης χρησιμοποιώντας το GroupDocs.Editor για .NET. Από την προσπάθεια ανοίγματος του εγγράφου χωρίς κωδικό πρόσβασης έως την αποθήκευση του με νέες ρυθμίσεις προστασίας, έχετε καλύψει όλα τα βασικά βήματα. Αυτή η γνώση αναμφίβολα θα ενισχύσει την ικανότητά σας να διαχειρίζεστε ασφαλή έγγραφα στις εφαρμογές σας .NET.
## Συχνές ερωτήσεις
### Τι είναι το GroupDocs.Editor για .NET;
Το GroupDocs.Editor για .NET είναι ένα ισχυρό API επεξεργασίας εγγράφων που επιτρέπει στους προγραμματιστές να φορτώνουν, να επεξεργάζονται και να αποθηκεύουν μια ποικιλία μορφών εγγράφων σε εφαρμογές .NET.
### Πώς μπορώ να αποκτήσω μια προσωρινή άδεια για το GroupDocs.Editor;
 Μπορείτε να αποκτήσετε προσωρινή άδεια από[εδώ](https://purchase.groupdocs.com/temporary-license/) για την αξιολόγηση των χαρακτηριστικών του προϊόντος.
### Είναι δυνατή η βελτιστοποίηση της χρήσης της μνήμης κατά την επεξεργασία μεγάλων εγγράφων;
 Ναι, μπορείτε να ενεργοποιήσετε τη βελτιστοποίηση μνήμης ρυθμίζοντας το`OptimizeMemoryUsage` ιδιοκτησία σε`true`στις επιλογές φόρτωσης.
### Μπορώ να ορίσω διαφορετικούς κωδικούς πρόσβασης για άνοιγμα και εγγραφή σε ένα υπολογιστικό φύλλο;
Απολύτως! Μπορείτε να ορίσετε ξεχωριστούς κωδικούς πρόσβασης για το άνοιγμα του εγγράφου και για την προστασία εγγραφής χρησιμοποιώντας τις επιλογές αποθήκευσης.
### Πού μπορώ να βρω πιο αναλυτική τεκμηρίωση;
 Μπορείτε να αποκτήσετε πρόσβαση στην ολοκληρωμένη τεκμηρίωση για το GroupDocs.Editor για .NET[εδώ](https://tutorials.groupdocs.com/editor/net/).