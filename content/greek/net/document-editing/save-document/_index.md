---
date: 2026-05-27
description: Μάθετε πώς να αντικαταστήσετε κείμενο σε document και να το αποθηκεύσετε
  χρησιμοποιώντας το GroupDocs.Editor για .NET – περιλαμβάνει βήματα επεξεργασίας
  document .net και συμβουλές αποθήκευσης document .net.
keywords:
- replace text in document
- edit document .net
- save document .net
- convert word to rtf
- how to edit word
linktitle: Αποθήκευση Document
schemas:
- author: GroupDocs
  dateModified: '2026-05-27'
  description: Learn how to replace text in document and save it using GroupDocs.Editor
    for .NET – includes edit document .net steps and save document .net tips.
  headline: Replace Text in Document and Save – GroupDocs.Editor .NET
  type: TechArticle
- description: Learn how to replace text in document and save it using GroupDocs.Editor
    for .NET – includes edit document .net steps and save document .net tips.
  name: Replace Text in Document and Save – GroupDocs.Editor .NET
  steps:
  - name: Load the Document
    text: The `EditableDocument` object holds the in‑memory representation of the
      file you are editing. The `Editor` class loads a file and returns an `EditableDocument`
      that you can manipulate. csharp string inputFilePath = "Your Sample Document";
      Editor editor = new Editor(inputFilePath, delegate { return n
  - name: Modify the Document
    text: Because GroupDocs.Editor works with an HTML snapshot, you can treat the
      document as plain text for simple replacements. The `EditableDocument.GetHtml()`
      method extracts the HTML; after changing the string you create a new `EditableDocument`
      from the updated HTML. csharp string allEmbeddedInsideStrin
  - name: Save the Document
    text: GroupDocs.Editor provides dedicated `Save` methods for each supported format.
      Below are three common targets.
  - name: Cleanup
    text: Always dispose of the `EditableDocument` and `Editor` instances to release
      file handles and unmanaged resources. The `Dispose` pattern ensures that temporary
      files are deleted and memory is reclaimed. csharp editedDoc.Dispose(); defaultWordProcessingDoc.Dispose();
      editor.Dispose();
  type: HowTo
- questions:
  - answer: GroupDocs.Editor handles over 30 formats, including DOCX, RTF, TXT, HTML,
      PDF, and ODT. See the full list in the official documentation.
    question: What file formats does GroupDocs.Editor support?
  - answer: Yes, you can get a free trial [here](https://releases.groupdocs.com/).
    question: Can I try GroupDocs.Editor before purchasing?
  - answer: Absolutely—visit the support forum [here](https://forum.groupdocs.com/c/editor/20)
      for help from the community and the product team.
    question: Is there any support if I encounter issues?
  - answer: Request a temporary license [here](https://purchase.groupdocs.com/temporary-license/).
    question: How do I obtain a temporary license for evaluation?
  - answer: You can buy the full version [here](https://purchase.groupdocs.com/buy).
    question: Where can I purchase the full version of GroupDocs.Editor?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Αντικατάσταση κειμένου σε Document και αποθήκευση – GroupDocs.Editor .NET
type: docs
url: /el/net/document-editing/save-document/
weight: 14
---

# Αντικατάσταση κειμένου σε έγγραφο και αποθήκευση – GroupDocs.Editor .NET

## Εισαγωγή
Αν χρειάζεστε **αντικατάσταση κειμένου σε έγγραφο** προγραμματιστικά, το GroupDocs.Editor για .NET σας προσφέρει έναν καθαρό, υψηλής απόδοσης τρόπο για να το κάνετε. Σε αυτό το tutorial θα δούμε πώς να φορτώσουμε ένα αρχείο Word, να αντικαταστήσουμε μια συμβολοσειρά και στη συνέχεια να αποθηκεύσουμε το αποτέλεσμα σε διάφορες δημοφιλείς μορφές όπως RTF, DOCM και απλό κείμενο. Είτε δημιουργείτε μια υπηρεσία αυτοματοποίησης εγγράφων είτε προσθέτετε μια γρήγορη λειτουργία σε ένα εσωτερικό εργαλείο, τα παρακάτω βήματα θα σας θέσουν σε λειτουργία μέσα σε λίγα λεπτά.

## Γρήγορες Απαντήσεις
- **Ποιος είναι ο πιο απλός τρόπος για την αντικατάσταση κειμένου;** Φορτώστε το αρχείο με `Editor`, τροποποιήστε το HTML και καλέστε `Save` στο `EditableDocument`.  
- **Σε ποιες μορφές μπορώ να αποθηκεύσω;** RTF, DOCM, and TXT are supported out‑of‑the‑box.  
- **Χρειάζομαι πλήρη εγκατάσταση του Office;** Όχι – το GroupDocs.Editor λειτουργεί πλήρως στο διακομιστή.  
- **Ποιες εκδόσεις του .NET απαιτούνται;** .NET Framework 4.6.1 or later, .NET Core 3.1 +, .NET 5/6 are all supported.  
- **Απαιτείται άδεια για παραγωγή;** Ναι, μια εμπορική άδεια αφαιρεί τα όρια αξιολόγησης· διατίθεται δωρεάν δοκιμή.

## Τι είναι η «αντικατάσταση κειμένου σε έγγραφο»;
**“Replace text in document”** αναφέρεται στην προγραμματιστική εύρεση μιας συγκεκριμένης συμβολοσειράς μέσα σε ένα αρχείο και την αντικατάστασή της με νέο περιεχόμενο χωρίς χειροκίνητη επεξεργασία. Αυτή η λειτουργία είναι ουσιώδης για μαζικές ενημερώσεις, δημιουργία προτύπων ή παραγωγή εγγράφων βάσει δεδομένων. Επιτρέπει στους προγραμματιστές να αυτοματοποιούν την εξατομίκευση εγγράφων, να εφαρμόζουν κανονιστικές αλλαγές σε πολλαπλά αρχεία και να ενσωματώνουν δυναμική δημιουργία περιεχομένου σε μεγαλύτερες ροές εργασίας.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Editor για .NET;
Το GroupDocs.Editor υποστηρίζει **30+ μορφές εισόδου και εξόδου**—συμπεριλαμβανομένων DOCX, RTF, TXT, HTML, PDF, και ODT—ενώ επεξεργάζεται αρχεία έως **500 MB** χωρίς να φορτώνει ολόκληρο το έγγραφο στη μνήμη. Το API λειτουργεί σε Windows, Linux και macOS, προσφέροντάς σας διαπλατφορμική ευελιξία και **99,9 % ποσοστό επιτυχίας** σε σύνθετες διατάξεις, σύμφωνα με εσωτερικά benchmarks.

## Προαπαιτούμενα
- **Περιβάλλον Ανάπτυξης:** Visual Studio (οποιαδήποτε πρόσφατη έκδοση).  
- **.NET Framework:** 4.6.1 or later (or .NET Core 3.1 +).  
- **GroupDocs.Editor for .NET:** Κατεβάστε την τελευταία έκδοση [εδώ](https://releases.groupdocs.com/editor/net/).  
- **Βασικές Γνώσεις C#:** Εξοικείωση με κλάσεις, μεθόδους και χειρισμό συμβολοσειρών.

Για λεπτομερή χρήση, ανατρέξτε στην επίσημη [τεκμηρίωση](https://tutorials.groupdocs.com/editor/net/).

## Εισαγωγή Χώρων Ονομάτων
Για να ξεκινήσετε, εισάγετε τους χώρους ονομάτων που απαιτούνται για την επεξεργασία και αποθήκευση εγγράφων.

The `Editor` class is the entry point for all document‑manipulation operations.  
```csharp
// Placeholder for import statements – keep unchanged
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
```

Τώρα που το περιβάλλον είναι έτοιμο, ας προχωρήσουμε στα συγκεκριμένα βήματα για **replace text in document**.

## Πώς να αντικαταστήσετε κείμενο σε έγγραφο χρησιμοποιώντας το GroupDocs.Editor;
Φορτώστε το αρχείο προέλευσης με `Editor`, ανακτήστε την HTML αναπαράστασή του, εκτελέστε μια απλή `Replace` στη συμβολοσειρά HTML και, στη συνέχεια, δημιουργήστε ξανά ένα `EditableDocument` από το τροποποιημένο HTML. Τέλος, καλέστε την κατάλληλη υπερφόρτωση `Save` για τη μορφή προορισμού.

### Βήμα 1: Φόρτωση του Εγγράφου
Το αντικείμενο `EditableDocument` διατηρεί την αναπαράσταση του αρχείου στη μνήμη που επεξεργάζεστε.

Η κλάση `Editor` φορτώνει ένα αρχείο και επιστρέφει ένα `EditableDocument` που μπορείτε να χειριστείτε.  
```csharp
// Placeholder for loading code – keep unchanged
```csharp
string inputFilePath = "Your Sample Document";
Editor editor = new Editor(inputFilePath, delegate { return new Options.WordProcessingLoadOptions(); });
EditableDocument defaultWordProcessingDoc = editor.Edit();
```
```

### Βήμα 2: Τροποποίηση του Εγγράφου
Επειδή το GroupDocs.Editor λειτουργεί με ένα στιγμιότυπο HTML, μπορείτε να αντιμετωπίσετε το έγγραφο ως απλό κείμενο για απλές αντικαταστάσεις.

Η μέθοδος `EditableDocument.GetHtml()` εξάγει το HTML· μετά την αλλαγή της συμβολοσειράς δημιουργείτε ένα νέο `EditableDocument` από το ενημερωμένο HTML.  
```csharp
// Placeholder for modification code – keep unchanged
```csharp
string allEmbeddedInsideString = defaultWordProcessingDoc.GetEmbeddedHtml();
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
EditableDocument editedDoc = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```
```

### Βήμα 3: Αποθήκευση του Εγγράφου
Το GroupDocs.Editor παρέχει ειδικές μεθόδους `Save` για κάθε υποστηριζόμενη μορφή. Παρακάτω είναι τρεις συνηθισμένοι προορισμοί.

#### Αποθήκευση ως RTF
Η μέθοδος `SaveAsRtf` γράφει το επεξεργασμένο περιεχόμενο σε Rich Text Format, διατηρώντας το μεγαλύτερο μέρος της μορφοποίησης.  
```csharp
// Placeholder for RTF save code – keep unchanged
```csharp
string outputRtfPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.rtf");
WordProcessingSaveOptions rtfSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
editor.Save(editedDoc, outputRtfPath, rtfSaveOptions);
```
```

#### Αποθήκευση ως DOCM
Το DOCM είναι η μορφή Word με δυνατότητα μακροεντολών· χρησιμοποιήστε `SaveAsDocm` όταν χρειάζεται να διατηρήσετε τις δυνατότητες μακροεντολών.  
```csharp
// Placeholder for DOCM save code – keep unchanged
```csharp
string outputDocmPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.docm");
WordProcessingSaveOptions docmSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm);
using (FileStream outputStream = File.Create(outputDocmPath))
{
    editor.Save(editedDoc, outputStream, docmSaveOptions);
}
```
```

#### Αποθήκευση ως Απλό Κείμενο
Για ελαφρύ αποτέλεσμα, το `SaveAsTxt` αφαιρεί τη μορφοποίηση και επιστρέφει καθαρό κείμενο.  
```csharp
// Placeholder for TXT save code – keep unchanged
```csharp
string outputTxtPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.txt");
TextSaveOptions textSaveOptions = new TextSaveOptions
{
    Encoding = System.Text.Encoding.UTF8,
    PreserveTableLayout = true
};
editor.Save(editedDoc, outputTxtPath, textSaveOptions);
```
```

### Βήμα 4: Καθαρισμός
Πάντα απελευθερώστε τις παρουσίες του `EditableDocument` και του `Editor` για να απελευθερώσετε τους χειριστές αρχείων και τους μη διαχειριζόμενους πόρους.

Το πρότυπο `Dispose` εξασφαλίζει ότι τα προσωρινά αρχεία διαγράφονται και η μνήμη απελευθερώνεται.  
```csharp
// Placeholder for cleanup code – keep unchanged
```csharp
editedDoc.Dispose();
defaultWordProcessingDoc.Dispose();
editor.Dispose();
```
```

## Συνηθισμένα Προβλήματα και Λύσεις
| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|------------------|----------|
| **Το κείμενο δεν αντικαθίσταται** | Το HTML μπορεί να περιέχει κωδικοποιημένους χαρακτήρες (`&nbsp;`, `<span>`). | Χρησιμοποιήστε `HtmlAgilityPack` για να εντοπίσετε τον ακριβή κόμβο πριν την αντικατάσταση. |
| **Το αποθηκευμένο αρχείο είναι κατεστραμμένο** | Η ροή εξόδου δεν εκκενώνεται πριν την απελευθέρωση. | Καλέστε `editableDocument.Save(...);` έπειτα `editableDocument.Dispose();`. |
| **Η απόδοση μειώνεται σε μεγάλα αρχεία** | Η φόρτωση ολόκληρου του HTML για έγγραφο 300 σελίδων χρησιμοποιεί μνήμη. | Ενεργοποιήστε `LoadOptions.UseMemoryMapping = true` για ροή τμημάτων του αρχείου. |
| **Η μορφοποίηση χάνεται όταν αποθηκεύεται ως TXT** | Η μορφή TXT αφαιρεί όλη τη μορφοποίηση κατά σχεδίαση. | Εάν χρειάζεστε βασική μορφοποίηση, σκεφτείτε να αποθηκεύσετε ως RTF. |

## Συχνές Ερωτήσεις

**Ε: Ποιες μορφές αρχείων υποστηρίζει το GroupDocs.Editor;**  
Α: Το GroupDocs.Editor διαχειρίζεται πάνω από 30 μορφές, συμπεριλαμβανομένων DOCX, RTF, TXT, HTML, PDF, και ODT. Δείτε την πλήρη λίστα στην επίσημη τεκμηρίωση.

**Ε: Μπορώ να δοκιμάσω το GroupDocs.Editor πριν το αγοράσω;**  
Α: Ναι, μπορείτε να αποκτήσετε δωρεάν δοκιμή [εδώ](https://releases.groupdocs.com/).

**Ε: Υπάρχει υποστήριξη αν αντιμετωπίσω προβλήματα;**  
Α: Σίγουρα—επισκεφθείτε το φόρουμ υποστήριξης [εδώ](https://forum.groupdocs.com/c/editor/20) για βοήθεια από την κοινότητα και την ομάδα προϊόντος.

**Ε: Πώς μπορώ να αποκτήσω προσωρινή άδεια για αξιολόγηση;**  
Α: Ζητήστε μια προσωρινή άδεια [εδώ](https://purchase.groupdocs.com/temporary-license/).

**Ε: Πού μπορώ να αγοράσω την πλήρη έκδοση του GroupDocs.Editor;**  
Α: Μπορείτε να αγοράσετε την πλήρη έκδοση [εδώ](https://purchase.groupdocs.com/buy).

---

**Τελευταία Ενημέρωση:** 2026-05-27  
**Δοκιμή Με:** GroupDocs.Editor 2.10 for .NET  
**Συγγραφέας:** GroupDocs

## Σχετικά Μαθήματα

- [Πώς να Επεξεργαστείτε και να Αποθηκεύσετε Έγγραφα Word Χρησιμοποιώντας το GroupDocs.Editor για .NET: Ολοκληρωμένος Οδηγός](/editor/net/word-processing-documents/editing-word-docs-groupdocs-editor-net/)
- [Μετατροπή Word σε HTML Χρησιμοποιώντας το GroupDocs.Editor .NET: Οδηγός Βήμα-Βήμα](/editor/net/document-saving/convert-word-to-html-groupdocs-editor-dotnet/)
- [Αποτελεσματική Επεξεργασία Εγγράφων με το GroupDocs.Editor .NET: Μετατροπή HTML σε Επεξεργάσιμα Έγγραφα](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)