---
title: Κατάργηση συλλογής πεδίων φόρμας
linktitle: Κατάργηση συλλογής πεδίων φόρμας
second_title: GroupDocs.Editor .NET API
description: Μάθετε πώς να αφαιρείτε πεδία φόρμας από έγγραφα του Word χρησιμοποιώντας το GroupDocs.Editor για .NET με αυτόν τον αναλυτικό οδηγό. Ιδανικό για προγραμματιστές.
weight: 13
url: /el/net/form-field-management/remove-form-field-collection/
---
## Εισαγωγή
Ψάχνετε να διαχειριστείτε τα πεδία φόρμας στα έγγραφά σας μέσω προγραμματισμού; Το GroupDocs.Editor για .NET προσφέρει μια ισχυρή λύση για το χειρισμό και το χειρισμό πεδίων φόρμας σε διάφορες μορφές εγγράφων. Σε αυτό το σεμινάριο, θα σας καθοδηγήσουμε στα βήματα για την κατάργηση συλλογών πεδίων φορμών από ένα έγγραφο του Word χρησιμοποιώντας αυτήν την ισχυρή βιβλιοθήκη. 
## Προαπαιτούμενα
Πριν βουτήξουμε στον κώδικα, ας βεβαιωθούμε ότι έχετε ρυθμίσει τα πάντα για μια ομαλή εμπειρία:
1. GroupDocs.Editor για .NET: Βεβαιωθείτε ότι έχετε κατεβάσει και εγκαταστήσει το GroupDocs.Editor για .NET. Εάν όχι, μπορείτε να το κατεβάσετε[εδώ](https://releases.groupdocs.com/editor/net/).
2. Περιβάλλον ανάπτυξης: Θα χρειαστείτε ένα περιβάλλον ανάπτυξης όπως το Visual Studio.
3. .NET Framework: Βεβαιωθείτε ότι έχετε εγκαταστήσει το .NET Framework στον υπολογιστή σας.
4.  Δείγμα εγγράφου: Έχετε ένα δείγμα εγγράφου Word (π.χ.`SampleLegacyFormFields.docx`) με πεδία φόρμας που θέλετε να χειριστείτε.

## Εισαγωγή χώρων ονομάτων
Για να ξεκινήσετε, πρέπει να εισαγάγετε τους απαραίτητους χώρους ονομάτων στο έργο σας .NET. Αυτό θα σας επιτρέψει να αποκτήσετε πρόσβαση στις λειτουργίες του GroupDocs.Editor.
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System.IO;
```
## Βήμα 1: Φορτώστε το έγγραφο
Αρχικά, θα χρειαστεί να φορτώσετε το έγγραφο που θέλετε να επεξεργαστείτε. Ας το αναλύσουμε:
### Βήμα 1.1: Λάβετε τη διαδρομή προς το αρχείο εισόδου
 Πρέπει να καθορίσετε τη διαδρομή προς το αρχείο εισόδου σας. Για αυτό το παράδειγμα, θα χρησιμοποιήσουμε ένα δείγμα αρχείου που ονομάζεται`SampleLegacyFormFields.docx`.
```csharp
string inputFilePath = "path/to/SampleLegacyFormFields.docx";
```
### Βήμα 1.2: Δημιουργήστε ένα FileStream από τη διαδρομή
 Στη συνέχεια, δημιουργήστε ένα`FileStream` για να διαβάσετε το έγγραφο.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
    // Συνεχίστε στα επόμενα βήματα σε αυτό χρησιμοποιώντας το μπλοκ.
}
```
## Βήμα 2: Ορίστε τις επιλογές φόρτωσης
Κατά τη φόρτωση του εγγράφου, ίσως χρειαστεί να καθορίσετε επιλογές φόρτωσης, ειδικά εάν το έγγραφό σας προστατεύεται με κωδικό πρόσβασης.
### Βήμα 2.1: Δημιουργία επιλογών φόρτωσης
 Δημιουργήστε ένα παράδειγμα του`WordProcessingLoadOptions`.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
```
### Βήμα 2.2: Καθορίστε τον κωδικό πρόσβασης (εάν χρειάζεται)
Εάν το έγγραφό σας προστατεύεται με κωδικό πρόσβασης, μπορείτε να καθορίσετε τον κωδικό πρόσβασης.
```csharp
loadOptions.Password = "some_password_to_open_a_document";
```
## Βήμα 3: Φορτώστε το έγγραφο στο πρόγραμμα επεξεργασίας
 Τώρα, φορτώστε το έγγραφο στο`Editor` παράδειγμα χρησιμοποιώντας το`FileStream` και`LoadOptions`.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    // Συνεχίστε στα επόμενα βήματα σε αυτό χρησιμοποιώντας το μπλοκ.
}
```
## Βήμα 4: Πρόσβαση και διαχείριση πεδίων φόρμας
Με τη φόρτωση του εγγράφου, μπορείτε πλέον να έχετε πρόσβαση και να χειρίζεστε τα πεδία της φόρμας.
### Βήμα 4.1: Διαβάστε το FormFieldManager
 Ανακτήστε το`FormFieldManager` από το`Editor` παράδειγμα.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
### Βήμα 4.2: Πρόσβαση στο FormFieldCollection
 Να πάρει το`FormFieldCollection` που περιέχει όλα τα πεδία φόρμας στο έγγραφο.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
### Βήμα 4.3: Αφαιρέστε ένα συγκεκριμένο πεδίο φόρμας κειμένου
Για να αφαιρέσετε ένα συγκεκριμένο πεδίο φόρμας κειμένου, εντοπίστε το με το όνομά του και, στη συνέχεια, αφαιρέστε το.
```csharp
TextFormField textField = collection.GetFormField<TextFormField>("Text1");
fieldManager.RemoveFormFiled(textField);
```
### Βήμα 4.4: Αφαιρέστε πολλαπλά πεδία φόρμας
Μπορείτε επίσης να αφαιρέσετε πολλά πεδία φόρμας ταυτόχρονα, προσδιορίζοντας τα ονόματά τους.
```csharp
textField = collection.GetFormField<TextFormField>("Text7");
CheckBoxForm checkBoxForm = collection.GetFormField<CheckBoxForm>("Check2");
fieldManager.RemoveFormFields(new IFormField[] { textField, checkBoxForm });
```
## Βήμα 5: Αποθηκεύστε το τροποποιημένο έγγραφο
Αφού τροποποιήσετε τα πεδία της φόρμας, πρέπει να αποθηκεύσετε το έγγραφο.
### Βήμα 5.1: Δημιουργία επιλογών αποθήκευσης
Καθορίστε τη μορφή και τις επιλογές αποθήκευσης για το έγγραφο εξόδου.
```csharp
WordProcessingFormats docFormat = WordProcessingFormats.Docx;
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(docFormat);
```
### Βήμα 5.2: Βελτιστοποιήστε τη χρήση της μνήμης
Εάν έχετε να κάνετε με μεγάλα έγγραφα, ίσως θέλετε να βελτιστοποιήσετε τη χρήση της μνήμης.
```csharp
saveOptions.OptimizeMemoryUsage = true;
```
### Βήμα 5.3: Ρύθμιση προστασίας (εάν χρειάζεται)
Μπορείτε να προστατεύσετε το έγγραφο από περαιτέρω επεξεργασία ορίζοντας έναν κωδικό πρόσβασης εγγραφής.
```csharp
saveOptions.Protection = new WordProcessingProtection(WordProcessingProtectionType.AllowOnlyFormFields, "write_password");
```
### Βήμα 5.4: Αποθηκεύστε το έγγραφο
 Τέλος, αποθηκεύστε το έγγραφο χρησιμοποιώντας α`MemoryStream`.
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(outputStream, saveOptions);
}
```

## συμπέρασμα
Συγχαρητήρια! Καταργήσατε επιτυχώς τα πεδία φόρμας από ένα έγγραφο του Word χρησιμοποιώντας το GroupDocs.Editor για .NET. Αυτή η ισχυρή βιβλιοθήκη διευκολύνει τον χειρισμό του περιεχομένου του εγγράφου μέσω προγραμματισμού, εξοικονομώντας χρόνο και προσπάθεια.
## Συχνές ερωτήσεις
### Μπορώ να χρησιμοποιήσω το GroupDocs.Editor για .NET με άλλες μορφές εγγράφων;
Ναι, το GroupDocs.Editor για .NET υποστηρίζει διάφορες μορφές εγγράφων, συμπεριλαμβανομένων των PDF, HTML και άλλων.
### Είναι δυνατή η προσθήκη πεδίων φόρμας χρησιμοποιώντας το GroupDocs.Editor για .NET;
Ναι, μπορείτε να προσθέσετε, να τροποποιήσετε και να αφαιρέσετε πεδία φόρμας μέσω προγραμματισμού.
### Τι γίνεται αν το έγγραφό μου είναι πολύ μεγάλο;
Μπορείτε να ενεργοποιήσετε τη βελτιστοποίηση μνήμης στις επιλογές αποθήκευσης για τον αποτελεσματικό χειρισμό μεγάλων εγγράφων.
### Μπορώ να χρησιμοποιήσω το GroupDocs.Editor για .NET σε μια εφαρμογή Ιστού;
Απολύτως! Το GroupDocs.Editor για .NET μπορεί να ενσωματωθεί σε εφαρμογές web για επεξεργασία εγγράφων από την πλευρά του διακομιστή.
### Πού μπορώ να λάβω υποστήριξη εάν αντιμετωπίσω προβλήματα;
 Μπορείτε να επισκεφθείτε το[φόρουμ υποστήριξης](https://forum.groupdocs.com/c/editor/20) για βοήθεια σε οποιοδήποτε θέμα.