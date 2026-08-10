---
date: 2026-08-10
description: Μάθετε πώς να επεξεργάζεστε αρχεία plain text χρησιμοποιώντας το GroupDocs.Editor
  for .NET. Ο οδηγός καλύπτει τη φόρτωση ενός αρχείου txt, το trimming spaces, το
  setting text encoding και την αποθήκευση του αποτελέσματος.
keywords:
- edit plain text
- load txt file
- trim trailing spaces
- convert leading spaces
- set text encoding
lastmod: 2026-08-10
linktitle: Εργασία με έγγραφα Plain Text
og_description: Μάθετε πώς να επεξεργάζεστε αρχεία plain text χρησιμοποιώντας το GroupDocs.Editor
  for .NET – load txt file, trim trailing spaces, convert leading spaces, set text
  encoding, και αποθήκευση αποδοτικά.
og_image_alt: Guide showing edit plain text workflow with GroupDocs.Editor for .NET
og_title: Επεξεργασία εγγράφων plain text με GroupDocs.Editor for .NET
schemas:
- author: GroupDocs
  dateModified: '2026-08-10'
  description: Learn how to edit plain text files using GroupDocs.Editor for .NET.
    The guide covers loading a txt file, trimming spaces, setting text encoding, and
    saving the result.
  headline: Edit plain text documents with GroupDocs.Editor for .NET
  type: TechArticle
- description: Learn how to edit plain text files using GroupDocs.Editor for .NET.
    The guide covers loading a txt file, trimming spaces, setting text encoding, and
    saving the result.
  name: Edit plain text documents with GroupDocs.Editor for .NET
  steps:
  - name: Get a path to the input TXT file
    text: First, decide whether you’ll work with a physical file path or a memory
      stream. Using a path is the most straightforward approach for local development.
  - name: Create an Editor instance
    text: '`Editor` is the main class that loads a document and provides editing capabilities.'
  - name: Create TXT editing options
    text: '`TxtEditOptions` configures how plain‑text files are parsed and edited,
      allowing you to set encoding and space‑handling rules.'
  - name: Create an EditableDocument instance
    text: '`EditableDocument` represents the in‑memory version of the loaded document,
      including its text and any associated resources.'
  - name: Edit the document content
    text: Retrieve the original text, apply any string operations you need (e.g.,
      replace, trim, change case), and store the result back into the `EditableDocument`.
  - name: Create an EditableDocument with updated content
    text: After you’ve transformed the text, instantiate a new `EditableDocument`
      that contains the edited string and the original resource collection.
  - name: Create WordProcessing save options
    text: '`WordProcessingSaveOptions` defines settings for saving the document in
      a Word‑compatible format such as DOCX or DOCM.'
  - name: Create TXT saving options
    text: '`TxtSaveOptions` specifies how the edited plain‑text file should be written,
      including encoding, line‑ending preservation, and table layout handling.'
  - name: Prepare output paths
    text: Derive the output directory from the input file path, then build the full
      filenames for the DOCX and TXT results.
  - name: Save the edited document
    text: Finally, call `editor.Save` twice—once with the WordProcessing options and
      once with the TXT options—to produce both formats in a single operation.
  type: HowTo
- questions:
  - answer: The library supports 50+ formats, including DOCX, TXT, HTML, PDF, and
      markdown, allowing you to edit and convert between them seamlessly.
    question: What file formats does GroupDocs.Editor for .NET support?
  - answer: Download the trial from the [releases page](https://releases.groupdocs.com/).
    question: How can I get a free trial of GroupDocs.Editor for .NET?
  - answer: Yes, temporary licenses are available through the [GroupDocs purchase
      page](https://purchase.groupdocs.com/temporary-license/).
    question: Can I purchase a temporary license for testing?
  - answer: The official support forum is the best place – visit the [GroupDocs.Editor
      support forum](https://forum.groupdocs.com/c/editor/20).
    question: Where can I find support if I run into issues?
  - answer: Absolutely. The full reference is on the [GroupDocs.Editor documentation
      page](https://tutorials.groupdocs.com/editor/net/).
    question: Is there detailed documentation for advanced scenarios?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
tags:
- edit plain text
- GroupDocs.Editor
- C# document processing
- plain text editing
- txt file handling
title: Επεξεργασία εγγράφων plain text με GroupDocs.Editor for .NET
type: docs
url: /el/net/document-processing/work-plain-text-documents/
weight: 15
---

# Επεξεργασία εγγράφων απλού κειμένου με το GroupDocs.Editor για .NET

## Εισαγωγή
Αν χρειάζεστε **γρήγορη και αξιόπιστη επεξεργασία απλού κειμένου** σε μια εφαρμογή .NET, το GroupDocs.Editor για .NET είναι το εργαλείο που κάνει το σκληρό έργο. Αυτό το API υποστηρίζει περισσότερα από 30 μορφές εγγράφων, μπορεί να χειριστεί αρχεία έως 500 MB και σας επιτρέπει να χειρίζεστε το κείμενο χωρίς να φορτώνετε ολόκληρο το αρχείο στη μνήμη. Σε αυτό το tutorial θα μάθετε πώς να φορτώσετε ένα αρχείο txt, να αφαιρέσετε τα τελικά κενά, να μετατρέψετε τα αρχικά κενά, να ορίσετε τη σωστή κωδικοποίηση και, τέλος, να αποθηκεύσετε το επεξεργασμένο περιεχόμενο ξανά στο δίσκο. Έτοιμοι για πρακτική; Ας ξεκινήσουμε!

## Γρήγορες απαντήσεις
- **Ποιο είναι το πρώτο βήμα για την επεξεργασία ενός αρχείου txt;** Φορτώστε το αρχείο με `Editor` χρησιμοποιώντας τη διαδρομή ή τη ροή που έχετε.  
- **Μπορώ να αλλάξω την κωδικοποίηση του αρχείου κατά την επεξεργασία;** Ναι – το `TxtSaveOptions` σας επιτρέπει να ορίσετε UTF‑8, UTF‑16 ή οποιαδήποτε προσαρμοσμένη κωδικοποίηση.  
- **Πώς αφαιρώ τα επιπλέον κενά στο τέλος κάθε γραμμής;** Ανακτήστε το κείμενο, καλέστε `TrimEnd()` σε κάθε γραμμή και γράψτε το ξανά.  
- **Είναι το GroupDocs.Editor δωρεάν για δοκιμή;** Μια πλήρως λειτουργική δοκιμή 30 ημερών είναι διαθέσιμη από τη σελίδα εκδόσεων.  
- **Ποιες εκδόσεις του .NET υποστηρίζονται;** .NET Framework 4.6+, .NET Core 3.1+, και .NET 5/6/7.

## Τι σημαίνει επεξεργασία απλού κειμένου;
**Edit plain text** σημαίνει η προγραμματιστική αλλαγή των χαρακτήρων μέσα σε ένα απλό αρχείο `.txt`—προσθήκη, αφαίρεση ή επαναδιαμόρφωση κειμένου—διατηρώντας την αρχική κωδικοποίηση του αρχείου και το στυλ αλλαγής γραμμής. Μπορεί να περιλαμβάνει εργασίες όπως αφαίρεση κενών, ομαλοποίηση λήξεων γραμμής, ενημέρωση τιμών ρυθμίσεων ή εισαγωγή παραγόμενου περιεχομένου. Η λειτουργία πρέπει να διατηρεί το αρχείο αναγνώσιμο από οποιονδήποτε τυπικό επεξεργαστή κειμένου και να διατηρεί τυχόν υπάρχοντα μεταδεδομένα όπως δείκτες BOM.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Editor για επεξεργασία απλού κειμένου;
Το GroupDocs.Editor επεξεργάζεται αρχεία με τρόπο ροής, πράγμα που σημαίνει ότι μπορεί να επεξεργαστεί ένα αρχείο καταγραφής 300 MB χρησιμοποιώντας λιγότερα από 50 MB RAM. Η βιβλιοθήκη υποστηρίζει **πάνω από 50 μορφές εισόδου και εξόδου**, ανιχνεύει αυτόματα τα στυλ λήξης γραμμής (CR, LF, CRLF) και παρέχει ενσωματωμένες επιλογές για **αφαίρεση τελικών κενών** και **μετατροπή αρχικών κενών** χωρίς την ανάγκη δημιουργίας προσαρμοσμένων αναλυτών.

## Προαπαιτούμενα
- **Περιβάλλον ανάπτυξης .NET** – Visual Studio 2022 ή VS Code με την επέκταση C#.  
- **GroupDocs.Editor for .NET** – κατεβάστε από τη σελίδα εκδόσεων [GroupDocs.Editor for .NET](https://releases.groupdocs.com/editor/net/).  
- **Βασικές γνώσεις C#** – θα πρέπει να είστε άνετοι με το αρχείο I/O και τη διαχείριση συμβολοσειρών.  
- **Επεξεργαστής κειμένου (προαιρετικό)** – για την επιθεώρηση των πηγαίων αρχείων· συνιστάται το VS Code.  
- Για λεπτομερή χρήση, δείτε την [τεκμηρίωση](https://tutorials.groupdocs.com/editor/net/).  
- Μπορείτε επίσης να περιηγηθείτε στη γενική [σελίδα εκδόσεων](https://releases.groupdocs.com/).

## Πώς να επεξεργαστείτε απλό κείμενο βήμα-βήμα
Φορτώστε το αρχείο, επεξεργαστείτε το περιεχόμενό του και αποθηκεύστε το ξανά – όλα σε λιγότερο από δέκα γραμμές κώδικα. Οι παρακάτω ενότητες σας καθοδηγούν μέσα από κάθε στάδιο με σαφείς εξηγήσεις.

### Βήμα 1: Λάβετε μια διαδρομή προς το αρχείο εισόδου TXT
Πρώτα, αποφασίστε αν θα εργαστείτε με φυσική διαδρομή αρχείου ή με ροή μνήμης. Η χρήση διαδρομής είναι η πιο απλή προσέγγιση για τοπική ανάπτυξη.

```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

### Βήμα 2: Δημιουργήστε μια παρουσία του Editor
`Editor` είναι η κύρια κλάση που φορτώνει ένα έγγραφο και παρέχει δυνατότητες επεξεργασίας.

```csharp
string inputFilePath = "YourSampleDocument.txt";
```

### Βήμα 3: Δημιουργήστε επιλογές επεξεργασίας TXT
`TxtEditOptions` ρυθμίζει πώς τα αρχεία απλού κειμένου αναλύονται και επεξεργάζονται, επιτρέποντάς σας να ορίσετε κωδικοποίηση και κανόνες διαχείρισης κενών.

```csharp
using (Editor editor = new Editor(inputFilePath))
{
```

### Βήμα 4: Δημιουργήστε μια παρουσία του EditableDocument
`EditableDocument` αντιπροσωπεύει την έκδοση στη μνήμη του φορτωμένου εγγράφου, συμπεριλαμβανομένου του κειμένου του και τυχόν σχετικών πόρων.

```csharp
    TextEditOptions editOptions = new TextEditOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        RecognizeLists = true,
        LeadingSpaces = TextLeadingSpacesOptions.ConvertToIndent,
        TrailingSpaces = TextTrailingSpacesOptions.Trim
    };
```

### Βήμα 5: Επεξεργαστείτε το περιεχόμενο του εγγράφου
Ανακτήστε το αρχικό κείμενο, εφαρμόστε τις απαιτούμενες λειτουργίες συμβολοσειράς (π.χ., αντικατάσταση, περικοπή, αλλαγή πεζών/κεφαλαίων) και αποθηκεύστε το αποτέλεσμα ξανά στο `EditableDocument`.

```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```

### Βήμα 6: Δημιουργήστε ένα EditableDocument με ενημερωμένο περιεχόμενο
Αφού μετασχηματίσετε το κείμενο, δημιουργήστε ένα νέο `EditableDocument` που περιέχει τη διορθωμένη συμβολοσειρά και τη συλλογή των αρχικών πόρων.

```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("text", "EDITED text");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```

### Βήμα 7: Δημιουργήστε επιλογές αποθήκευσης WordProcessing
`WordProcessingSaveOptions` ορίζει ρυθμίσεις για την αποθήκευση του εγγράφου σε μορφή συμβατή με το Word, όπως DOCX ή DOCM.

```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```

### Βήμα 8: Δημιουργήστε επιλογές αποθήκευσης TXT
`TxtSaveOptions` καθορίζει πώς θα πρέπει να γραφτεί το επεξεργασμένο αρχείο απλού κειμένου, συμπεριλαμβανομένης της κωδικοποίησης, της διατήρησης των λήξεων γραμμής και της διαχείρισης διάταξης πινάκων.

```csharp
    WordProcessingSaveOptions wordSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm)
    {
        Locale = System.Globalization.CultureInfo.GetCultureInfo("en-GB")
    };
```

### Βήμα 9: Προετοιμάστε τις διαδρομές εξόδου
Παράγετε τον φάκελο εξόδου από τη διαδρομή του αρχείου εισόδου, στη συνέχεια δημιουργήστε τα πλήρη ονόματα αρχείων για τα αποτελέσματα DOCX και TXT.

```csharp
    TextSaveOptions txtSaveOptions = new TextSaveOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        PreserveTableLayout = true
    };
```

### Βήμα 10: Αποθηκεύστε το επεξεργασμένο έγγραφο
Τέλος, καλέστε το `editor.Save` δύο φορές—μία με τις επιλογές WordProcessing και μία με τις επιλογές TXT—για να παραχθούν και οι δύο μορφές σε μία ενέργεια.

```csharp
    string outputWordPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".docm");
    string outputTxtPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".txt");
```

## Κοινά προβλήματα και λύσεις
- **Τα τελικά κενά παραμένουν μετά την επεξεργασία** – βεβαιωθείτε ότι το `TxtEditOptions.TrimTrailingSpaces` είναι ορισμένο σε `true` πριν φορτώσετε το έγγραφο.  
- **Λανθασμένη κωδικοποίηση στο αποθηκευμένο αρχείο** – ελέγξτε ότι το `TxtSaveOptions.Encoding` ταιριάζει με τη ζητούμενη κωδικοσελίδα (π.χ., `Encoding.UTF8`).  
- **Μεγάλα αρχεία προκαλούν OutOfMemoryException** – χρησιμοποιήστε το API ροής (`Editor.Load(Stream)`) αντί για φόρτωση από διαδρομή αρχείου ώστε η χρήση μνήμης να παραμείνει χαμηλή.  

## Συχνές ερωτήσεις

**Q: Ποιοι τύποι αρχείων υποστηρίζει το GroupDocs.Editor για .NET;**  
A: Η βιβλιοθήκη υποστηρίζει πάνω από 50 μορφές, συμπεριλαμβανομένων των DOCX, TXT, HTML, PDF και markdown, επιτρέποντάς σας να επεξεργάζεστε και να μετατρέπετε μεταξύ τους απρόσκοπτα.

**Q: Πώς μπορώ να αποκτήσω δωρεάν δοκιμή του GroupDocs.Editor για .NET;**  
A: Κατεβάστε τη δοκιμή από τη [σελίδα εκδόσεων](https://releases.groupdocs.com/).

**Q: Μπορώ να αγοράσω προσωρινή άδεια για δοκιμή;**  
A: Ναι, προσωρινές άδειες είναι διαθέσιμες μέσω της [σελίδας αγοράς GroupDocs](https://purchase.groupdocs.com/temporary-license/).

**Q: Πού μπορώ να βρω υποστήριξη αν αντιμετωπίσω προβλήματα;**  
A: Το επίσημο φόρουμ υποστήριξης είναι το καλύτερο μέρος – επισκεφθείτε το [φόρουμ υποστήριξης GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).

**Q: Υπάρχει λεπτομερής τεκμηρίωση για προχωρημένα σενάρια;**  
A: Απόλυτα. Η πλήρης αναφορά βρίσκεται στη [σελίδα τεκμηρίωσης GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/).

## Συμπέρασμα
Τώρα έχετε κατακτήσει πώς να **επεξεργάζεστε αρχεία απλού κειμένου** χρησιμοποιώντας το GroupDocs.Editor για .NET—φορτώνοντας ένα αρχείο txt, αφαιρώντας κενά, μετατρέποντας αρχικά κενά, ορίζοντας τη σωστή κωδικοποίηση και αποθηκεύοντας το αποτέλεσμα και σε μορφές TXT και DOCX. Αυτή η δυνατότητα σας επιτρέπει να αυτοματοποιήσετε τον καθαρισμό αρχείων καταγραφής, να δημιουργείτε αρχεία ρυθμίσεων σε πραγματικό χρόνο ή να χτίζετε προσαρμοσμένες αλυσίδες επεξεργασίας κειμένου χωρίς να ξαναδημιουργείτε τη λειτουργία. Εξερευνήστε πρόσθετες δυνατότητες όπως η επεξεργασία σε παρτίδες και η μετατροπή εγγράφων επισκεπτόμενοι την επίσημη τεκμηρίωση.

---

**Τελευταία ενημέρωση:** 2026-08-10  
**Δοκιμάστηκε με:** GroupDocs.Editor 23.11 for .NET  
**Συγγραφέας:** GroupDocs  

```csharp
    editor.Save(afterEdit, outputWordPath, wordSaveOptions);
    editor.Save(afterEdit, outputTxtPath, txtSaveOptions);
}
System.Console.WriteLine("Document editing process completed successfully!");
```

## Σχετικές εκπαιδεύσεις

- [Εκπαιδεύσεις Φόρτωσης Εγγράφων με το GroupDocs.Editor για .NET](/editor/net/document-loading/)
- [Εκπαιδεύσεις Αποθήκευσης και Εξαγωγής Εγγράφων για το GroupDocs.Editor .NET](/editor/net/document-saving/)
- [Εκπαιδεύσεις Επεξεργασίας Απλού Κειμένου και Εγγράφων DSV για το GroupDocs.Editor .NET](/editor/net/plain-text-dsv-documents/)