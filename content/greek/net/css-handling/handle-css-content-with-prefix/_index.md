---
date: 2026-09-26
description: Μάθετε πώς να διαχειριστείτε το πρόθεμα css και να εξάγετε περιεχόμενο
  css χρησιμοποιώντας το GroupDocs.Editor για .NET σε αυτό το λεπτομερές βήμα‑βήμα
  tutorial.
keywords:
- handle css prefix
- extract css content
- edit document css
- prepend url to css
lastmod: 2026-09-26
linktitle: Διαχείριση Περιεχομένου CSS με Πρόθεμα
og_description: Ανακαλύψτε πώς να διαχειριστείτε το πρόθεμα css και να εξάγετε περιεχόμενο
  css με το GroupDocs.Editor για .NET. Ακολουθήστε έναν βήμα‑βήμα οδηγό για να προσθέσετε
  προθέματα σε URLs σε πόρους CSS και να ανακτήσετε stylesheets.
og_image_alt: Developer guide showing css prefix handling with GroupDocs.Editor for
  .NET
og_title: Πώς να διαχειριστείτε το πρόθεμα css στο GroupDocs.Editor για .NET
schemas:
- author: GroupDocs
  dateModified: '2026-09-26'
  description: Learn how to handle css prefix and extract css content using GroupDocs.Editor
    for .NET in this detailed step‑by‑step tutorial.
  headline: How to handle css prefix in GroupDocs.Editor for .NET
  type: TechArticle
- questions:
  - answer: Yes, GroupDocs.Editor for .NET supports PDF, Word, Excel, PowerPoint,
      and many other formats.
    question: Can I use GroupDocs.Editor for .NET with other document formats?
  - answer: Absolutely! You can start your free trial on the [GroupDocs free trial
      page](https://releases.groupdocs.com/).
    question: Is there a free trial available for GroupDocs.Editor for .NET?
  - answer: You can obtain a temporary license from the [temporary license page](https://purchase.groupdocs.com/temporary-license/).
    question: How do I get a temporary license for GroupDocs.Editor for .NET?
  - answer: Detailed documentation is available on the [GroupDocs.Editor for .NET
      documentation site](https://tutorials.groupdocs.com/editor/net/).
    question: Where can I find detailed documentation for GroupDocs.Editor for .NET?
  - answer: You can get support through the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).
    question: What support options are available for GroupDocs.Editor for .NET?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
tags:
- css handling
- GroupDocs.Editor
- .NET document processing
- css prefix
- api tutorial
title: Πώς να διαχειριστείτε το πρόθεμα css στο GroupDocs.Editor για .NET
type: docs
url: /el/net/css-handling/handle-css-content-with-prefix/
weight: 11
---

# Πώς να διαχειριστείτε το πρόθεμα css στο GroupDocs.Editor για .NET

Σε αυτό το σεμινάριο θα μάθετε **πώς να διαχειριστείτε το πρόθεμα css** όταν εργάζεστε με φύλλα στυλ μέσα σε ένα έγγραφο χρησιμοποιώντας το GroupDocs.Editor για .NET. Είτε χρειάζεται να προσθέσετε ένα URL σε εικόνες, γραμματοσειρές ή οποιονδήποτε εξωτερικό πόρο, τα παρακάτω βήματα σας δείχνουν ακριβώς πώς να **διαχειριστείτε το πρόθεμα css** και επίσης πώς να **εξάγετε το περιεχόμενο css** για περαιτέρω επεξεργασία. Στο τέλος του οδηγού θα μπορείτε να ξαναγράψετε τις διαδρομές πόρων, να ανακτήσετε τις ακατέργαστες συμβολοσειρές CSS και να τις ενσωματώσετε στη διαδικτυακή ροή εργασίας σας με σιγουριά.

## Γρήγορες απαντήσεις
- **Τι σημαίνει “διαχείριση προθέματος css”;** Προσθήκη προσαρμοσμένου προθέματος URL σε εξωτερικούς πόρους που αναφέρονται στο CSS.  
- **Ποια μέθοδος API επιστρέφει τα στυλ CSS;** `EditableDocument.GetCssContent(...)`.  
- **Χρειάζομαι άδεια;** Διατίθεται δοκιμαστική άδεια· απαιτείται εμπορική άδεια για παραγωγή.  
- **Ποιες εκδόσεις .NET υποστηρίζονται;** .NET Framework 4.5+ και .NET Core/5/6.  
- **Μπορώ να αλλάξω το πρόθεμα κατά την εκτέλεση;** Ναι – απλώς περάστε μια διαφορετική συμβολοσειρά στο `GetCssContent`.

## Τι είναι η διαχείριση προθέματος css;
Ο όρος αναφέρεται στην επανεγγραφή των URL εικόνων, γραμματοσειρών ή οποιουδήποτε εξωτερικού πόρου μέσα σε ένα αρχείο CSS ώστε να δείχνουν σε μια τοποθεσία που ελέγχετε, όπως ένα CDN ή ένας ασφαλής διακομιστής. Προσθέτοντας ένα συνεπές βασικό URL, εξασφαλίζετε ότι κάθε πόρος φορτώνεται σωστά όταν το έγγραφο αποδίδεται σε πρόγραμμα περιήγησης ή σε προβολέα βασισμένο στο web.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Editor για την εξαγωγή περιεχομένου css;
Το GroupDocs.Editor μπορεί να διαβάσει το αρχικό CSS που είναι ενσωματωμένο σε έγγραφα WordProcessing, να επιστρέψει τις ακατέργαστες συμβολοσειρές φύλλων στυλ και να σας επιτρέψει να τις επεξεργαστείτε πριν από την απόδοση ή την αποθήκευση. Αυτό εξαλείφει την χειροκίνητη ανάλυση, εγγυάται την πιστότητα στην εσωτερική αναπαράσταση του εγγράφου και υποστηρίζει **30+ μορφές αρχείων** ενώ επεξεργάζεται αρχεία έως **500 MB** χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη.

## Προαπαιτούμενα
Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε τα παρακάτω προαπαιτούμενα:
- Visual Studio: Θα χρειαστείτε μια λειτουργική εγκατάσταση του Visual Studio.  
- .NET Framework: Βεβαιωθείτε ότι έχετε εγκατεστημένο το .NET Framework.  
- GroupDocs.Editor for .NET: Μπορείτε να το κατεβάσετε από τη [σελίδα λήψης GroupDocs.Editor for .NET](https://releases.groupdocs.com/editor/net/).  
- Δείγμα Εγγράφου: Έχετε ένα δείγμα εγγράφου έτοιμο για επεξεργασία.

## Εισαγωγή ονομάτων χώρων
Αρχικά, ας εισάγουμε τους απαραίτητους χώρους ονομάτων ώστε ο κώδικάς μας να εκτελείται ομαλά. Αυτό το βήμα μας δίνει πρόσβαση στις βασικές κλάσεις του GroupDocs.Editor.

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Editor.Options;
```

## Βήμα 1: Αρχικοποίηση του Editor
Η κλάση `Editor` είναι το σημείο εισόδου για εργασία με έγγραφα στο GroupDocs.Editor. Διαχειρίζεται τις λειτουργίες φόρτωσης, επεξεργασίας και αποθήκευσης.  
Το πρώτο βήμα περιλαμβάνει τη δημιουργία ενός αντικειμένου `Editor` με το δείγμα εγγράφου σας. Αυτό ρυθμίζει το περιβάλλον επεξεργασίας.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```

## Βήμα 2: Επεξεργασία του εγγράφου
Το αντικείμενο `EditableDocument` αντιπροσωπεύει την επεξεργάσιμη έκδοση του αρχείου και εκθέτει τα εσωτερικά του μέρη, όπως CSS, εικόνες και HTML.  
Στη συνέχεια, λαμβάνουμε ένα αντικείμενο `EditableDocument`. Αυτό το αντικείμενο μας επιτρέπει να εργαστούμε με το εσωτερικό CSS του εγγράφου.

```csharp
    using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
    {
```

## Βήμα 3: Ορισμός εξωτερικών προθεμάτων
Ορίστε τα προθέματα URL για εικόνες και γραμματοσειρές. Αυτά τα προθέματα θα προσαρτηθούν σε κάθε αναφορά εικόνας και γραμματοσειρά που βρίσκεται στο CSS.

```csharp
        string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
        string externalFontsPrefix = "http://www.mywebsite.com/fonts/id=";
```

## Βήμα 4: Εξαγωγή περιεχομένου css με τα προθέματα
Το `GetCssContent` επιστρέφει μια συλλογή συμβολοσειρών φύλλων στυλ CSS που ήδη περιέχουν τα προσαρτημένα URL που δώσατε.  
Καλείτε το `GetCssContent`, περνώντας τα προθέματα που μόλις ορίσατε. Η μέθοδος επιστρέφει μια λίστα συμβολοσειρών φύλλων στυλ CSS που ήδη περιέχουν τα προσαρτημένα URL.

```csharp
        List<string> stylesheets = document.GetCssContent(externalImagesPrefix, externalFontsPrefix);
```

## Βήμα 5: Εξαγωγή των αποτελεσμάτων
Εκτυπώστε τον αριθμό των φύλλων στυλ που βρέθηκαν και εμφανίστε κάθε φύλλο στυλ. Αυτό σας βοηθά να επαληθεύσετε ότι τα προθέματα εφαρμόστηκαν σωστά.

```csharp
        Console.WriteLine("There are {0} stylesheets in the input document", stylesheets.Count);
        foreach (string css in stylesheets)
        {
            Console.WriteLine(css);
        }
    }
}
```

## Συνηθισμένα προβλήματα και λύσεις
- **Δεν επιστράφηκαν φύλλα στυλ** – Βεβαιωθείτε ότι το πηγαίο έγγραφο περιέχει πραγματικά CSS (π.χ., ένα έγγραφο Word με μορφοποιημένους πίνακες ή ενσωματωμένο HTML).  
- **Λανθασμένα URL** – Ελέγξτε ξανά ότι οι συμβολοσειρές προθέματος τελειώνουν με το κατάλληλο διαχωριστικό (`/` ή `=`) για τη δρομολόγηση του διακομιστή σας.  
- **Ανησυχίες απόδοσης** – Για πολύ μεγάλα έγγραφα, εξετάστε την επεξεργασία των φύλλων στυλ σε παρτίδες ώστε να αποφύγετε υψηλή χρήση μνήμης.

## Συχνές ερωτήσεις

**Q: Μπορώ να χρησιμοποιήσω το GroupDocs.Editor για .NET με άλλες μορφές εγγράφων;**  
A: Ναι, το GroupDocs.Editor για .NET υποστηρίζει PDF, Word, Excel, PowerPoint και πολλές άλλες μορφές.

**Q: Υπάρχει δωρεάν δοκιμαστική έκδοση για το GroupDocs.Editor για .NET;**  
A: Απόλυτα! Μπορείτε να ξεκινήσετε τη δωρεάν δοκιμή σας στη [σελίδα δωρεάν δοκιμής GroupDocs](https://releases.groupdocs.com/).

**Q: Πώς μπορώ να αποκτήσω προσωρινή άδεια για το GroupDocs.Editor για .NET;**  
A: Μπορείτε να αποκτήσετε προσωρινή άδεια από τη [σελίδα προσωρινής άδειας](https://purchase.groupdocs.com/temporary-license/).

**Q: Πού μπορώ να βρω λεπτομερή τεκμηρίωση για το GroupDocs.Editor για .NET;**  
A: Λεπτομερής τεκμηρίωση είναι διαθέσιμη στην [ιστοσελίδα τεκμηρίωσης GroupDocs.Editor για .NET](https://tutorials.groupdocs.com/editor/net/).

**Q: Ποιες επιλογές υποστήριξης είναι διαθέσιμες για το GroupDocs.Editor για .NET;**  
A: Μπορείτε να λάβετε υποστήριξη μέσω του [φόρουμ υποστήριξης GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).

## Πρόσθετες συχνές ερωτήσεις

**Q: Μπορώ να αλλάξω το πρόθεμα μετά την εξαγωγή του CSS;**  
A: Ναι. Καλέστε ξανά το `GetCssContent` με διαφορετική συμβολοσειρά προθέματος· η μέθοδος χρησιμοποιεί πάντα τις τιμές που περνάτε κατά την εκτέλεση.

**Q: Λειτουργεί αυτό με έγγραφα προστατευμένα με κωδικό;**  
A: Ναι. Παρέχετε τον κωδικό στο `WordProcessingLoadOptions` κατά τη δημιουργία του αντικειμένου `Editor`.

**Q: Είναι δυνατόν να αποθηκεύσετε το τροποποιημένο CSS πίσω στο έγγραφο;**  
A: Το GroupDocs.Editor αυτή τη στιγμή παρέχει πρόσβαση μόνο για ανάγνωση στο CSS. Για να διατηρήσετε τις αλλαγές, θα πρέπει να αντικαταστήσετε το αρχικό φύλλο στυλ χρησιμοποιώντας τα υποκείμενα XML API του εγγράφου.

---

**Τελευταία ενημέρωση:** 2026-09-26  
**Δοκιμάστηκε με:** GroupDocs.Editor 23.12 for .NET  
**Συγγραφέας:** GroupDocs

## Σχετικά Σεμινάρια

- [Εξαγωγή Εξωτερικού CSS από Έγγραφα Word Χρησιμοποιώντας το GroupDocs.Editor .NET: Ένας Πλήρης Οδηγός](/editor/net/html-web-documents/extract-external-css-word-docs-groupdocs-editor-dotnet/)
- [Εξαγωγή & Πρόσθεση Προθέματος HTML από Έγγραφα Word χρησιμοποιώντας το GroupDocs.Editor .NET](/editor/net/html-web-documents/groupdocs-editor-dotnet-extract-prefix-html-word-docs/)
- [Πώς να Εξάγετε και να Τροποποιήσετε το Περιεχόμενο HTML σε Έγγραφα Word Χρησιμοποιώντας το GroupDocs.Editor .NET](/editor/net/html-web-documents/extract-modify-html-content-word-docs-groupdocs-editor-net/)