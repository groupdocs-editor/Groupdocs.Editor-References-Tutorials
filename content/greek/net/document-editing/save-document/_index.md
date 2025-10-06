---
title: Αποθήκευση εγγράφου
linktitle: Αποθήκευση εγγράφου
second_title: GroupDocs.Editor .NET API
description: Επεξεργαστείτε και αποθηκεύστε έγγραφα χωρίς κόπο χρησιμοποιώντας το GroupDocs.Editor για .NET. Αυτός ο οδηγός βήμα προς βήμα απλοποιεί τη διαδικασία για τους προγραμματιστές.
weight: 14
url: /el/net/document-editing/save-document/
type: docs
---
# Αποθήκευση εγγράφου

## Εισαγωγή
Θέλετε να επεξεργαστείτε και να αποθηκεύσετε εύκολα έγγραφα χρησιμοποιώντας το GroupDocs.Editor για .NET; Είστε στο σωστό μέρος! Αυτό το σεμινάριο θα σας καθοδηγήσει στη διαδικασία βήμα προς βήμα, διασφαλίζοντας ότι μπορείτε να διαχειριστείτε εύκολα τα έγγραφά σας. Είτε είστε έμπειρος προγραμματιστής είτε αρχάριος, ο οδηγός μας θα σας παρέχει όλες τις πληροφορίες που χρειάζεστε για να ξεκινήσετε.
## Προαπαιτούμενα
Πριν ξεκινήσετε το σεμινάριο, βεβαιωθείτε ότι έχετε τις ακόλουθες προϋποθέσεις:
- Περιβάλλον ανάπτυξης: Το Visual Studio είναι εγκατεστημένο στον υπολογιστή σας.
- .NET Framework: Βεβαιωθείτε ότι έχετε .NET Framework 4.6.1 ή νεότερη έκδοση.
-  GroupDocs.Editor για .NET: Κάντε λήψη της πιο πρόσφατης έκδοσης[εδώ](https://releases.groupdocs.com/editor/net/).
- Βασικές γνώσεις C#: Η εξοικείωση με τον προγραμματισμό C# είναι απαραίτητη.
## Εισαγωγή χώρων ονομάτων
Για να χρησιμοποιήσετε το GroupDocs.Editor στο έργο σας .NET, πρέπει να εισαγάγετε τους απαραίτητους χώρους ονομάτων. Δείτε πώς το κάνετε:
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
Τώρα που έχουμε ρυθμίσει το περιβάλλον μας και έχουμε εισαγάγει τους απαραίτητους χώρους ονομάτων, ας βουτήξουμε στα βήματα που απαιτούνται για τη φόρτωση, την επεξεργασία και την αποθήκευση ενός εγγράφου χρησιμοποιώντας το GroupDocs.Editor για .NET.
## Βήμα 1: Φορτώστε το έγγραφο
Αρχικά, πρέπει να φορτώσουμε το έγγραφο που θέλουμε να επεξεργαστούμε. Το GroupDocs.Editor κάνει αυτή τη διαδικασία απλή. Δείτε πώς μπορείτε να το κάνετε:

```csharp
string inputFilePath = "Your Sample Document";
Editor editor = new Editor(inputFilePath, delegate { return new Options.WordProcessingLoadOptions(); });
EditableDocument defaultWordProcessingDoc = editor.Edit();
```
 Σε αυτό το βήμα, καθορίζουμε τη διαδρομή προς το έγγραφο που θέλουμε να επεξεργαστούμε και δημιουργούμε μια παρουσία του`Editor` τάξη. ο`Edit` Τότε καλείται η μέθοδος για να φορτώσει το έγγραφο σε ένα`EditableDocument` αντικείμενο.
## Βήμα 2: Τροποποίηση του Εγγράφου
Με τη φόρτωση του εγγράφου, ήρθε η ώρα να κάνετε κάποιες τροποποιήσεις. Εφόσον δεν έχουμε συνδεδεμένο πρόγραμμα επεξεργασίας WYSIWYG, θα προσομοιώσουμε τη διαδικασία επεξεργασίας σε κώδικα.

```csharp
string allEmbeddedInsideString = defaultWordProcessingDoc.GetEmbeddedHtml();
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
EditableDocument editedDoc = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```
 Εδώ, ανακτούμε το ενσωματωμένο περιεχόμενο HTML του εγγράφου, πραγματοποιούμε μια απλή αντικατάσταση κειμένου και δημιουργούμε ένα νέο`EditableDocument`παράδειγμα από το τροποποιημένο HTML.
## Βήμα 3: Αποθηκεύστε το έγγραφο
Μετά την επεξεργασία του εγγράφου, το τελευταίο βήμα είναι να το αποθηκεύσετε. Το GroupDocs.Editor παρέχει πολλές επιλογές για την αποθήκευση του εγγράφου σε διαφορετικές μορφές.
## Αποθήκευση ως RTF
```csharp
string outputRtfPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.rtf");
WordProcessingSaveOptions rtfSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
editor.Save(editedDoc, outputRtfPath, rtfSaveOptions);
```
## Αποθήκευση ως DOCM
```csharp
string outputDocmPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.docm");
WordProcessingSaveOptions docmSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm);
using (FileStream outputStream = File.Create(outputDocmPath))
{
    editor.Save(editedDoc, outputStream, docmSaveOptions);
}
```
## Αποθήκευση ως απλού κειμένου
```csharp
string outputTxtPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.txt");
TextSaveOptions textSaveOptions = new TextSaveOptions
{
    Encoding = System.Text.Encoding.UTF8,
    PreserveTableLayout = true
};
editor.Save(editedDoc, outputTxtPath, textSaveOptions);
```
## Βήμα 4: Καθαρισμός
 Τέλος, είναι σημαντικό να απορρίψετε το`EditableDocument` και`Editor` περιπτώσεις για την απελευθέρωση πόρων.
```csharp
editedDoc.Dispose();
defaultWordProcessingDoc.Dispose();
editor.Dispose();
```
Ακολουθώντας αυτά τα βήματα, μπορείτε να φορτώσετε, να επεξεργαστείτε και να αποθηκεύσετε αποτελεσματικά έγγραφα χρησιμοποιώντας το GroupDocs.Editor για .NET. Αυτό το ισχυρό εργαλείο παρέχει ευελιξία και ευκολία στη χρήση, κάνοντας τη διαχείριση εγγράφων παιχνιδάκι.
## συμπέρασμα
Η επεξεργασία και η αποθήκευση εγγράφων μέσω προγραμματισμού δεν ήταν ποτέ πιο εύκολη με το GroupDocs.Editor για .NET. Αυτός ο οδηγός σας καθοδήγησε σε όλη τη διαδικασία, από τη φόρτωση ενός εγγράφου έως την αποθήκευσή του σε διάφορες μορφές. Με το GroupDocs.Editor, έχετε μια ευέλικτη και ισχυρή λύση στα χέρια σας, απλοποιώντας τη διαδικασία επεξεργασίας εγγράφων.
## Συχνές ερωτήσεις
### Ποιες μορφές αρχείων υποστηρίζει το GroupDocs.Editor;
Το GroupDocs.Editor υποστηρίζει διάφορες μορφές αρχείων, συμπεριλαμβανομένων των DOCX, RTF, TXT και πολλών άλλων. Για μια πλήρη λίστα, ρίξτε μια ματιά στο[τεκμηρίωση](https://tutorials.groupdocs.com/editor/net/).
### Μπορώ να δοκιμάσω το GroupDocs.Editor πριν το αγοράσω;
 Ναι, μπορείτε να πάρετε ένα[δωρεάν δοκιμή](https://releases.groupdocs.com/) για να δοκιμάσετε τις δυνατότητες του GroupDocs.Editor.
### Υπάρχει διαθέσιμη υποστήριξη εάν αντιμετωπίζω προβλήματα;
 Απολύτως! Μπορείτε να επισκεφθείτε το[φόρουμ υποστήριξης](https://forum.groupdocs.com/c/editor/20) για βοήθεια σε τυχόν προβλήματα που αντιμετωπίζετε.
### Πώς μπορώ να αποκτήσω προσωρινή άδεια;
 Μπορείτε να ζητήσετε α[προσωρινή άδεια](https://purchase.groupdocs.com/temporary-license/) για σκοπούς αξιολόγησης.
### Πού μπορώ να αγοράσω την πλήρη έκδοση του GroupDocs.Editor;
 Μπορείτε να αγοράσετε την πλήρη έκδοση[εδώ](https://purchase.groupdocs.com/buy).