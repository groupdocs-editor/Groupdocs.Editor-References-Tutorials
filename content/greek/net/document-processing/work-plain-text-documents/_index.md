---
title: Εργαστείτε με έγγραφα απλού κειμένου
linktitle: Εργαστείτε με έγγραφα απλού κειμένου
second_title: GroupDocs.Editor .NET API
description: Μάθετε να επεξεργάζεστε έγγραφα απλού κειμένου χρησιμοποιώντας το GroupDocs.Editor για .NET με τον αναλυτικό οδηγό μας. Απλοποιήστε τη διαδικασία επεξεργασίας εγγράφων .NET.
weight: 15
url: /el/net/document-processing/work-plain-text-documents/
---
## Εισαγωγή
Θέλετε να βελτιώσετε τη διαδικασία επεξεργασίας εγγράφων σας στο .NET; Μην ψάχνετε άλλο από το GroupDocs.Editor για .NET! Αυτό το ισχυρό API σάς επιτρέπει να επεξεργάζεστε μια μεγάλη ποικιλία μορφών εγγράφων με ευκολία. Σε αυτό το σεμινάριο, θα σας καθοδηγήσουμε στη διαδικασία εργασίας με έγγραφα απλού κειμένου χρησιμοποιώντας το GroupDocs.Editor για .NET. Στο τέλος, θα είστε εξοπλισμένοι να χειρίζεστε την επεξεργασία εγγράφων κειμένου σαν επαγγελματίας. Είστε έτοιμοι να βουτήξετε; Ας αρχίσουμε!
## Προαπαιτούμενα
Πριν ξεκινήσουμε, υπάρχουν μερικά πράγματα που θα πρέπει να έχετε στη θέση του:
- .NET Development Environment: Βεβαιωθείτε ότι έχετε ρυθμίσει ένα λειτουργικό περιβάλλον ανάπτυξης .NET. Το Visual Studio είναι μια δημοφιλής επιλογή.
-  GroupDocs.Editor για .NET: Κάντε λήψη και εγκαταστήστε το[GroupDocs.Editor για .NET](https://releases.groupdocs.com/editor/net/).
- Βασικές γνώσεις C#: Η εξοικείωση με τη γλώσσα προγραμματισμού C# θα σας βοηθήσει να ακολουθήσετε μαζί με τα παραδείγματα.
- Επεξεργαστής κειμένου: Κάθε πρόγραμμα επεξεργασίας κειμένου θα κάνει, αν και ο κώδικας του Visual Studio συνιστάται για τις δυνατότητες και την ευκολία χρήσης του.
## Εισαγωγή χώρων ονομάτων
Για να ξεκινήσετε να χρησιμοποιείτε το GroupDocs.Editor για .NET, πρέπει να εισαγάγετε τους απαραίτητους χώρους ονομάτων στο έργο σας. Αυτό διασφαλίζει ότι όλες οι απαιτούμενες κλάσεις και μέθοδοι είναι διαθέσιμες για χρήση.
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```
Ας αναλύσουμε τη διαδικασία σε διαχειρίσιμα βήματα. Ακολουθήστε καθώς σας καθοδηγούμε σε κάθε στάδιο της επεξεργασίας εγγράφων απλού κειμένου χρησιμοποιώντας το GroupDocs.Editor για .NET.
## Βήμα 1: Αποκτήστε μια διαδρομή προς το αρχείο εισόδου TXT
Αρχικά, πρέπει να καθορίσετε τη διαδρομή προς το αρχείο εισόδου TXT. Αυτό μπορεί να είναι μια διαδρομή προς ένα τοπικό αρχείο ή μια ροή που περιέχει το περιεχόμενο του αρχείου.
```csharp
string inputFilePath = "YourSampleDocument.txt";
```
## Βήμα 2: Δημιουργήστε μια παρουσία προγράμματος επεξεργασίας
 Στη συνέχεια, δημιουργήστε μια παρουσία του`Editor` τάξη. Αυτή η τάξη είναι υπεύθυνη για τη φόρτωση και την επεξεργασία εγγράφων. Δεν απαιτούνται επιλογές φόρτωσης σε αυτό το στάδιο.
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## Βήμα 3: Δημιουργία επιλογών επεξεργασίας TXT
Τώρα, δημιουργήστε τις επιλογές επεξεργασίας TXT. Αυτές οι επιλογές σάς επιτρέπουν να καθορίσετε τον τρόπο επεξεργασίας του περιεχομένου κειμένου κατά την επεξεργασία.
```csharp
    TextEditOptions editOptions = new TextEditOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        RecognizeLists = true,
        LeadingSpaces = TextLeadingSpacesOptions.ConvertToIndent,
        TrailingSpaces = TextTrailingSpacesOptions.Trim
    };
```
## Βήμα 4: Δημιουργήστε ένα EditableDocument Instance
 Με τις επιλογές επεξεργασίας που έχουν οριστεί, δημιουργήστε ένα`EditableDocument` παράδειγμα. Αυτό αντιπροσωπεύει το έγγραφο σε επεξεργάσιμη μορφή.
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## Βήμα 5: Επεξεργαστείτε το περιεχόμενο του εγγράφου
Ανακτήστε το αρχικό περιεχόμενο κειμένου και πραγματοποιήστε τις αλλαγές που επιθυμείτε. Για αυτό το παράδειγμα, θα αντικαταστήσουμε τη λέξη "κείμενο" με "ΕΠΕΞΕΡΓΑΣΜΕΝΟ κείμενο".
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("text", "EDITED text");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## Βήμα 6: Δημιουργήστε ένα Επεξεργάσιμο Έγγραφο με Ενημερωμένο Περιεχόμενο
 Αφού κάνετε τις απαραίτητες αλλαγές, δημιουργήστε ένα νέο`EditableDocument` με το ενημερωμένο περιεχόμενο και τους αρχικούς πόρους.
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## Βήμα 7: Δημιουργήστε Επιλογές Αποθήκευσης Επεξεργασίας Κειμένου
Προετοιμάστε τις επιλογές αποθήκευσης για τη μορφή WordProcessing. Αυτό το παράδειγμα χρησιμοποιεί τη μορφή DOCM και καθορίζει τις τοπικές ρυθμίσεις.
```csharp
    WordProcessingSaveOptions wordSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm)
    {
        Locale = System.Globalization.CultureInfo.GetCultureInfo("en-GB")
    };
```
## Βήμα 8: Δημιουργία επιλογών αποθήκευσης TXT
Ομοίως, δημιουργήστε τις επιλογές αποθήκευσης για τη μορφή TXT. Βεβαιωθείτε ότι η κωδικοποίηση έχει οριστεί σε UTF-8 και διατηρήστε τη διάταξη του πίνακα.
```csharp
    TextSaveOptions txtSaveOptions = new TextSaveOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        PreserveTableLayout = true
    };
```
## Βήμα 9: Προετοιμάστε τις διαδρομές εξόδου
Προετοιμάστε τις διαδρομές για την αποθήκευση των αρχείων DOCX και TXT που προκύπτουν. Χρησιμοποιήστε τη διαδρομή του αρχείου εισόδου για να προσδιορίσετε τον κατάλογο εξόδου και τα ονόματα αρχείων.
```csharp
    string outputWordPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".docm");
    string outputTxtPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".txt");
```
## Βήμα 10: Αποθηκεύστε το επεξεργασμένο έγγραφο
Τέλος, αποθηκεύστε το επεξεργασμένο έγγραφο και στις δύο μορφές DOCX και TXT χρησιμοποιώντας τις καθορισμένες επιλογές αποθήκευσης.
```csharp
    editor.Save(afterEdit, outputWordPath, wordSaveOptions);
    editor.Save(afterEdit, outputTxtPath, txtSaveOptions);
}
System.Console.WriteLine("Document editing process completed successfully!");
```
## συμπέρασμα
 Συγχαρητήρια! Επεξεργαστήκατε επιτυχώς ένα έγγραφο απλού κειμένου χρησιμοποιώντας το GroupDocs.Editor για .NET. Αυτό το ισχυρό εργαλείο απλοποιεί την επεξεργασία εγγράφων, καθιστώντας εύκολη την ενσωμάτωση στις εφαρμογές σας .NET. Είτε χειρίζεστε απλά αρχεία κειμένου είτε σύνθετες μορφές εγγράφων, το GroupDocs.Editor σας καλύπτει. Εξερευνήστε περισσότερες δυνατότητες και δυνατότητες μεταβαίνοντας στο[Τεκμηρίωση GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/).
## Συχνές ερωτήσεις
### Ποιες μορφές αρχείων υποστηρίζει το GroupDocs.Editor για .NET;
 Το GroupDocs.Editor για .NET υποστηρίζει ένα ευρύ φάσμα μορφών αρχείων, συμπεριλαμβανομένων των DOCX, TXT, HTML και άλλων. Ελεγξε το[τεκμηρίωση](https://tutorials.groupdocs.com/editor/net/) για πλήρη λίστα.
### Πώς μπορώ να αποκτήσω μια δωρεάν δοκιμή του GroupDocs.Editor για .NET;
 Μπορείτε να κάνετε λήψη μιας δωρεάν δοκιμής του GroupDocs.Editor για .NET από το[σελίδα εκδόσεων](https://releases.groupdocs.com/).
### Μπορώ να αγοράσω μια προσωρινή άδεια χρήσης για το GroupDocs.Editor για .NET;
Ναι, μπορείτε να αποκτήσετε προσωρινή άδεια από το[Σελίδα αγοράς GroupDocs](https://purchase.groupdocs.com/temporary-license/).
### Πού μπορώ να λάβω υποστήριξη για το GroupDocs.Editor για .NET;
 Η υποστήριξη είναι διαθέσιμη μέσω του[Φόρουμ υποστήριξης GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).
### Υπάρχει διαθέσιμη λεπτομερής τεκμηρίωση για το GroupDocs.Editor για .NET;
 Ναι, υπάρχει αναλυτική τεκμηρίωση στο[Σελίδα τεκμηρίωσης GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/).