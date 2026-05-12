---
date: 2026-05-12
description: Μάθετε πώς να εξάγετε γραμματοσειρές και άλλους πόρους HTML από έγγραφα
  χρησιμοποιώντας το GroupDocs.Editor για .NET. Οδηγός βήμα‑βήμα για προγραμματιστές
  .NET.
keywords:
- how to extract fonts
- GroupDocs.Editor .NET
- extract HTML resources
linktitle: Αποθήκευση πόρων HTML σε φάκελο
schemas:
- author: GroupDocs
  dateModified: '2026-05-12'
  description: Learn how to extract fonts and other HTML resources from documents
    using GroupDocs.Editor for .NET. Step‑by‑step guide for .NET developers.
  headline: How to Extract Fonts and Save HTML Resources to Folder
  type: TechArticle
- description: Learn how to extract fonts and other HTML resources from documents
    using GroupDocs.Editor for .NET. Step‑by‑step guide for .NET developers.
  name: How to Extract Fonts and Save HTML Resources to Folder
  steps:
  - name: '**Basic Knowledge of C# and .NET** – Familiarity with C# programming language
      and .NET framework is essential to follow along with the examples.'
    text: '**Basic Knowledge of C# and .NET** – Familiarity with C# programming language
      and .NET framework is essential to follow along with the examples.'
  - name: '**GroupDocs.Editor for .NET Library** – Download and install GroupDocs.Editor
      for .NET library from the [website](https://releases.groupdocs.com/editor/net/).'
    text: '**GroupDocs.Editor for .NET Library** – Download and install GroupDocs.Editor
      for .NET library from the [website](https://releases.groupdocs.com/editor/net/).'
  - name: '**Development Environment** – Set up your preferred development environment
      such as Visual Studio or any other compatible IDE.'
    text: '**Development Environment** – Set up your preferred development environment
      such as Visual Studio or any other compatible IDE.'
  type: HowTo
- questions:
  - answer: Yes, it supports Excel, PowerPoint, PDF, HTML, and over 50 additional
      formats for both editing and resource extraction.
    question: Is GroupDocs.Editor compatible with other document formats besides Word?
  - answer: Absolutely. The API works seamlessly with ASP.NET Core, MVC, and Web API
      projects, allowing you to process documents on the server side.
    question: Can I integrate GroupDocs.Editor into a web application?
  - answer: Yes, it includes built‑in connectors for Google Drive, Dropbox, OneDrive,
      and Amazon S3, enabling direct loading and saving of documents in the cloud.
    question: Does GroupDocs.Editor provide cloud storage integration?
  - answer: A fully functional 30‑day trial can be downloaded from the GroupDocs website
      without any credit‑card requirement.
    question: Is there a free trial available for GroupDocs.Editor?
  - answer: You can reach the GroupDocs support team via the official forum, submit
      a ticket through the customer portal, or consult the detailed API documentation.
    question: How can I get technical support for extraction issues?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Πώς να εξάγετε γραμματοσειρές και να αποθηκεύσετε πόρους HTML σε φάκελο
type: docs
url: /el/net/document-editing/save-html-resources-to-folder/
weight: 13
---

# Πώς να εξάγετε γραμματοσειρές και να αποθηκεύσετε πόρους HTML σε φάκελο

## Εισαγωγή
Το GroupDocs.Editor for .NET σας επιτρέπει να **εξάγετε γραμματοσειρές** και άλλα στοιχεία από ένα έγγραφο ενώ το μετατρέπει σε HTML. Σε λίγες γραμμές C# μπορείτε να εξάγετε εικόνες, φύλλα στυλ και αρχεία γραμματοσειρών, και στη συνέχεια να τα αποθηκεύσετε σε φάκελο της επιλογής σας. Αυτό το σεμινάριο σας καθοδηγεί μέσα από όλη τη ροή εργασίας, από την αρχικοποίηση του επεξεργαστή μέχρι την αποθήκευση κάθε πόρου στο δίσκο.

## Γρήγορες Απαντήσεις
- **Τι σημαίνει “how to extract fonts”;** Είναι η διαδικασία ανάκτησης ενσωματωμένων αρχείων γραμματοσειρών από ένα πηγαίο έγγραφο κατά τη μετατροπή σε HTML.  
- **Ποια βιβλιοθήκη το διαχειρίζεται;** Το GroupDocs.Editor for .NET παρέχει μια ειδική API για την εξαγωγή γραμματοσειρών, εικόνων και φύλλων στυλ.  
- **Χρειάζομαι άδεια;** Διατίθεται δωρεάν δοκιμή· απαιτείται εμπορική άδεια για χρήση σε παραγωγή.  
- **Ποιες εκδόσεις .NET υποστηρίζονται;** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.  
- **Μπορώ να στοχεύσω σε προσαρμοσμένο φάκελο;** Ναι, μπορείτε να καθορίσετε οποιοδήποτε εγγράψιμο μονοπάτι κατά την αποθήκευση των εξαγόμενων πόρων.

## Τι είναι το “how to extract fonts”;
**How to extract fonts** αναφέρεται στην ανάκτηση των αρχικών αρχείων γραμματοσειρών που είναι ενσωματωμένα σε ένα πηγαίο έγγραφο (π.χ., DOCX, PPTX) ώστε να μπορούν να αναφέρονται από το παραγόμενο HTML. Αυτό εξασφαλίζει ότι το κείμενο εμφανίζεται ακριβώς όπως προορίζεται στα προγράμματα περιήγησης χωρίς να εξαρτάται από τις γραμματοσειρές του συστήματος.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Editor για εξαγωγή πόρων HTML;
Το GroupDocs.Editor υποστηρίζει **πάνω από 50 μορφές εισόδου και εξόδου** — συμπεριλαμβανομένων των DOCX, PPTX, PDF και HTML — και μπορεί να επεξεργαστεί έγγραφα με **έως 300 σελίδες** χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη. Η API του εξάγει γραμματοσειρές, εικόνες και CSS σε μία μόνο διεργασία, μειώνοντας τον χρόνο ανάπτυξης έως και **70 %** σε σύγκριση με την χειροκίνητη ανάλυση.

## Προαπαιτούμενα
Πριν ξεκινήσετε το σεμινάριο, βεβαιωθείτε ότι έχετε τα παρακάτω προαπαιτούμενα:
1. **Βασικές γνώσεις C# και .NET** – Η εξοικείωση με τη γλώσσα προγραμματισμού C# και το .NET framework είναι απαραίτητη για να ακολουθήσετε τα παραδείγματα.  
2. **GroupDocs.Editor for .NET Library** – Κατεβάστε και εγκαταστήστε τη βιβλιοθήκη GroupDocs.Editor for .NET από την [ιστοσελίδα](https://releases.groupdocs.com/editor/net/).  
3. **Περιβάλλον Ανάπτυξης** – Ρυθμίστε το προτιμώμενο περιβάλλον ανάπτυξης, όπως το Visual Studio ή οποιοδήποτε άλλο συμβατό IDE.

## Εισαγωγή Namespaces
Για να ξεκινήσετε, εισάγετε τα απαραίτητα namespaces στο έργο C# σας:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```

## Πώς να εξάγετε γραμματοσειρές και να αποθηκεύσετε πόρους HTML σε φάκελο;
Φορτώστε το πηγαίο έγγραφό σας με `Editor editor = new Editor("sample.docx", new WordProcessingLoadOptions());` και στη συνέχεια καλέστε `editor.Save("output.html", SaveOptions.Html);`. Μετά την αποθήκευση, η συλλογή `Resources` περιέχει όλα τα εξαγόμενα στοιχεία — συμπεριλαμβανομένων των γραμματοσειρών — τα οποία μπορείτε να επαναλάβετε και να γράψετε στο δίσκο. Αυτή η προσέγγιση ενός βήματος διαχειρίζεται αυτόματα τόσο τη μετατροπή όσο και την εξαγωγή πόρων.

## Βήμα 1: Αρχικοποίηση GroupDocs.Editor
`Editor` είναι η κεντρική κλάση που οργανώνει τη φόρτωση, τη μετατροπή και την εξαγωγή πόρων του εγγράφου. Αντιπροσωπεύει μια μοναδική συνεδρία εγγράφου στη μνήμη.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
Αρχικά, αρχικοποιήστε το αντικείμενο `Editor` παρέχοντας τη διαδρομή προς το δείγμα εγγράφου σας. Σε αυτό το παράδειγμα, χρησιμοποιούμε ένα έγγραφο Word, επομένως καθορίζουμε `WordProcessingLoadOptions` ως τύπο εγγράφου.

## Βήμα 2: Επεξεργασία Εγγράφου
`EditableDocument` είναι η επεξεργάσιμη αναπαράσταση που επιστρέφεται από τη μέθοδο `Edit`, επιτρέποντάς σας να χειριστείτε το έγγραφο πριν από την αποθήκευση.

```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
Στη συνέχεια, δημιουργήστε ένα αντικείμενο `EditableDocument` καλώντας τη μέθοδο `Edit` του αντικειμένου `Editor`. Αυτό σας επιτρέπει να εκτελέσετε λειτουργίες επεξεργασίας στο έγγραφο.

## Βήμα 3: Εξαγωγή Πόρων
`Resources` είναι μια συλλογή που ομαδοποιεί τα εξαγόμενα στοιχεία — εικόνες, γραμματοσειρές και φύλλα στυλ — σε ξεχωριστές λίστες για εύκολη διαχείριση.

```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
Εξάγετε πόρους όπως εικόνες, γραμματοσειρές και φύλλα στυλ από το έγγραφο και αποθηκεύστε τα σε αντίστοιχες λίστες.

## Βήμα 4: Καθορισμός Φακέλου Εξόδου
`outputFolder` είναι μια συμβολοσειρά που ορίζει πού θα γραφτούν τα εξαγόμενα αρχεία. Μπορείτε να το κατευθύνετε σε οποιονδήποτε εγγράψιμο κατάλογο στον διακομιστή ή στον τοπικό υπολογιστή.

```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
Ορίστε το φάκελο εξόδου όπου θα αποθηκευτούν οι εξαγόμενοι πόροι. Μπορείτε να προσαρμόσετε τη διαδρομή του φακέλου σύμφωνα με τις απαιτήσεις σας.

## Βήμα 5: Αποθήκευση Πόρων
`SaveResource` είναι μια βοηθητική ρουτίνα που γράφει έναν μοναδικό δυαδικό πόρο (εικόνα, γραμματοσειρά ή φύλλο στυλ) στο σύστημα αρχείων.

```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
Επανάληψη σε κάθε πόρο εικόνας, αποθήκευση του στο φάκελο εξόδου και εμφάνιση σχετικών πληροφοριών όπως όνομα αρχείου, τύπος και διαστάσεις.

```csharp
		foreach (FontResourceBase oneFont in fonts)
		{
			Console.WriteLine("Saving {0} of {1} type",
				oneFont.FilenameWithExtension, oneFont.Type.FormalName);
			oneFont.Save(Path.Combine(outputFolder, oneFont.FilenameWithExtension));
		}
```
Ανάλογα, αποθηκεύστε κάθε πόρο γραμματοσειράς στο φάκελο εξόδου.

```csharp
		foreach (CssText oneStylesheet in stylesheets)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} encoding",
				oneStylesheet.FilenameWithExtension, oneStylesheet.Type.FormalName, oneStylesheet.Encoding);
			oneStylesheet.Save(Path.Combine(outputFolder, oneStylesheet.FilenameWithExtension));
		}
	}
}
```
Τέλος, αποθηκεύστε κάθε φύλλο στυλ στο φάκελο εξόδου και ολοκληρώστε τη διαδικασία επεξεργασίας.

## Κοινά Προβλήματα και Λύσεις
- **Απουσία γραμματοσειρών μετά τη μετατροπή** – Βεβαιωθείτε ότι το πηγαίο έγγραφο ενσωματώνει πραγματικά τις γραμματοσειρές· διαφορετικά, το GroupDocs.Editor μπορεί να αναφέρεται μόνο σε γραμματοσειρές συστήματος.  
- **Σφάλματα άρνησης πρόσβασης** – Επαληθεύστε ότι η διαδικασία της εφαρμογής έχει δικαιώματα εγγραφής στον προορισμό του φακέλου εξόδου.  
- **Μεγάλα έγγραφα προκαλούν υψηλή χρήση μνήμης** – Χρησιμοποιήστε `LoadOptions` με `LoadMode = LoadMode.Stream` για ροή μεγάλων αρχείων αντί για πλήρη φόρτωση στη μνήμη.

## Συχνές Ερωτήσεις

**Ε: Είναι το GroupDocs.Editor συμβατό με άλλες μορφές εγγράφων εκτός από το Word;**  
Α: Ναι, υποστηρίζει Excel, PowerPoint, PDF, HTML και πάνω από 50 επιπλέον μορφές τόσο για επεξεργασία όσο και για εξαγωγή πόρων.

**Ε: Μπορώ να ενσωματώσω το GroupDocs.Editor σε μια web εφαρμογή;**  
Α: Απόλυτα. Η API λειτουργεί απρόσκοπτα με έργα ASP.NET Core, MVC και Web API, επιτρέποντάς σας να επεξεργάζεστε έγγραφα στην πλευρά του διακομιστή.

**Ε: Παρέχει το GroupDocs.Editor ενσωμάτωση αποθήκευσης στο cloud;**  
Α: Ναι, περιλαμβάνει ενσωματωμένους συνδέσμους για Google Drive, Dropbox, OneDrive και Amazon S3, επιτρέποντας άμεση φόρτωση και αποθήκευση εγγράφων στο cloud.

**Ε: Υπάρχει δωρεάν δοκιμή διαθέσιμη για το GroupDocs.Editor;**  
Α: Μια πλήρως λειτουργική δοκιμή 30 ημερών μπορεί να ληφθεί από την ιστοσελίδα του GroupDocs χωρίς απαίτηση πιστωτικής κάρτας.

**Ε: Πώς μπορώ να λάβω τεχνική υποστήριξη για προβλήματα εξαγωγής;**  
Α: Μπορείτε να επικοινωνήσετε με την ομάδα υποστήριξης του GroupDocs μέσω του επίσημου φόρουμ, να υποβάλετε αίτημα μέσω του πελατειακού portal, ή να συμβουλευτείτε την αναλυτική τεκμηρίωση της API.

---

**Τελευταία Ενημέρωση:** 2026-05-12  
**Δοκιμή Με:** GroupDocs.Editor 23.11 for .NET  
**Συγγραφέας:** GroupDocs

## Σχετικά Σεμινάρια

- [Αποτελεσματική Επεξεργασία Εγγράφων με το GroupDocs.Editor .NET: Μετατροπή HTML σε Επεξεργάσιμα Έγγραφα](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)
- [Αποτελεσματική Εξαγωγή και Αποθήκευση Πόρων DOCX με το GroupDocs.Editor .NET - Πλήρης Οδηγός](/editor/net/document-saving/efficient-extract-save-docx-resources-groupdocs-editor-net/)
- [Απόκτηση Εξοικείωσης στην Επεξεργασία και Μετατροπή Εγγράφων με το GroupDocs.Editor .NET: Πλήρης Οδηγός](/editor/net/document-editing/groupdocs-editor-net-mastering-document-editing/)