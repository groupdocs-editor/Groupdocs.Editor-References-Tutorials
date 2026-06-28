---
date: 2026-03-14
description: Μάθετε πώς να εξάγετε εικόνες από DOCX, να μετατρέψετε DOCX σε HTML και
  να αποθηκεύσετε το έγγραφο ως HTML χρησιμοποιώντας το GroupDocs.Editor για .NET.
linktitle: Extract Images from DOCX – Advanced Editable Document Usage
second_title: GroupDocs.Editor .NET API
title: Εξαγωγή εικόνων από DOCX – Προηγμένη χρήση επεξεργάσιμου εγγράφου
type: docs
url: /el/net/document-editing/advanced-usage-of-editable-documents/
weight: 11
---

 markdown formatting.

Let's produce final content.# Εξαγωγή Εικόνων από DOCX – Προχωρημένη Χρήση Επεξεργάσιμων Εγγράφων

Αν είστε προγραμματιστής .NET που θέλει να **εξάγει εικόνες από DOCX** και να βελτιώσει τις δυνατότητες επεξεργασίας εγγράφων, το GroupDocs.Editor για .NET προσφέρει μια ισχυρή σουίτα εργαλείων. Αυτός ο ολοκληρωμένος οδηγός θα σας καθοδηγήσει στη προχωρημένη χρήση επεξεργάσιμων εγγράφων με το GroupDocs.Editor, αναλύοντας κάθε βήμα λεπτομερώς ώστε να αξιοποιήσετε πλήρως τις δυνατότητές του.

## Γρήγορες Απαντήσεις
- **Πώς μπορώ να εξάγω εικόνες από ένα αρχείο DOCX;** Χρησιμοποιήστε `EditableDocument.Images` αφού φορτώσετε το έγγραφο με το `Editor`.
- **Μπορώ να μετατρέψω DOCX σε HTML με ενσωματωμένους πόρους;** Ναι—καλέστε `EditableDocument.GetEmbeddedHtml()` ή `GetContent()` για το HTML markup.
- **Ποια μέθοδος αποθηκεύει το επεξεργασμένο έγγραφο ως HTML;** `EditableDocument.Save(htmlFilePath)` δημιουργεί ένα αρχείο HTML με φάκελο πόρων.
- **Είναι δυνατόν να εξαχθούν γραμματοσειρές από ένα έγγραφο Word;** Χρησιμοποιήστε `EditableDocument.Fonts` για να ανακτήσετε όλους τους πόρους γραμματοσειρών.
- **Χρειάζομαι άδεια για χρήση σε παραγωγή;** Απαιτείται έγκυρη άδεια GroupDocs.Editor· διατίθεται δωρεάν δοκιμή.

## Τι είναι η **εξαγωγή εικόνων από docx**;
Η εξαγωγή εικόνων από ένα αρχείο DOCX σημαίνει την προγραμματιστική ανάκτηση κάθε εικόνας που είναι ενσωματωμένη στο έγγραφο Word, ώστε να μπορείτε να τις χρησιμοποιήσετε ξανά, να τις τροποποιήσετε ή να τις αποθηκεύσετε ξεχωριστά. Το GroupDocs.Editor εκθέτει τη συλλογή `Images` σε ένα αντικείμενο `EditableDocument`, καθιστώντας αυτή τη διαδικασία απλή.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Editor για αυτή τη ροή εργασίας;
- **Πλήρης έλεγχος** στους πόρους του εγγράφου (εικόνες, γραμματοσειρές, CSS) χωρίς χειροκίνητη διαχείριση ZIP.  
- **Απρόσκοπτη μετατροπή** από DOCX σε HTML διατηρώντας τη διάταξη και το στυλ.  
- **Εύκολη εξαγωγή πόρων** για προσαρμοσμένη διαχείριση εικόνων, ενσωμάτωση γραμματοσειρών ή παροχή μέσω CDN.  
- **Ανθεκτικό πρότυπο διαγραφής** που εξασφαλίζει ότι δεν υπάρχουν διαρροές μνήμης σε υπηρεσίες μακράς διάρκειας.

## Προαπαιτούμενα
- Visual Studio εγκατεστημένο στο μηχάνημά σας.  
- .NET Framework συμβατό με το GroupDocs.Editor.  
- Βιβλιοθήκη GroupDocs.Editor για .NET. Μπορείτε να την [κατεβάσετε εδώ](https://releases.groupdocs.com/editor/net/).  
- Έγκυρη άδεια GroupDocs.Editor. Μπορείτε να αποκτήσετε [δωρεάν δοκιμή](https://releases.groupdocs.com/) ή να αγοράσετε [προσωρινή άδεια](https://purchase.groupdocs.com/temporary-license/).

## Εισαγωγή Χώρων Ονομάτων
Για να ξεκινήσετε, βεβαιωθείτε ότι εισάγετε τους απαραίτητους χώρους ονομάτων στο .NET project σας:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```

## Βήμα 1: Δημιουργία Παραδείγματος EditableDocument
Αρχικά, πρέπει να δημιουργήσετε ένα παράδειγμα του `EditableDocument` φορτώνοντας και επεξεργαζόμενοι ένα εισαγόμενο έγγραφο υποστηριζόμενης μορφής.

```csharp
string inputFilePath = "YourSampleDocument.docx";
Editor editor = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```

Σε αυτό το βήμα, φορτώνουμε το εισαγόμενο έγγραφο και το προετοιμάζουμε για επεξεργασία.

## Πώς να **εξάγετε εικόνες από DOCX**;
Παρακάτω εμβαθύνουμε στις δυνατότητες εξαγωγής πόρων, ξεκινώντας με την πιο συνηθισμένη ανάγκη—την λήψη όλων των εικόνων από ένα αρχείο Word.

## Βήμα 2: Εξαγωγή Πόρων Εγγράφου
Το `EditableDocument` περιέχει διάφορους πόρους που μπορούν να εξαχθούν και να χειριστούν. Ας τους αναλύσουμε:

### Βήμα 2.1: Εξαγωγή Ολόκληρου Εγγράφου ως HTML
Μπορείτε να δημιουργήσετε μια μοναδική συμβολοσειρά που περιέχει ολόκληρο το έγγραφο με όλους τους πόρους ενσωματωμένους ως HTML.

```csharp
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```

Αυτή η συμβολοσειρά θα είναι αρκετά μεγάλη, καθώς περιλαμβάνει φύλλα στυλ, εικόνες και γραμματοσειρές κωδικοποιημένες σε base64.

### Βήμα 2.2: Εξαγωγή Όλων των Εικόνων *(κύρια λέξη-κλειδί σε δράση)*
Εξάγετε όλες τις εικόνες από το έγγραφο—αυτή είναι η ουσία της **εξαγωγής εικόνων από docx**.

```csharp
List<IImageResource> allImages = beforeEdit.Images;
```

### Βήμα 2.3: Εξαγωγή Όλων των Γραμματοσειρών *(δευτερεύουσα λέξη-κλειδί)*
Αν χρειάζεστε επίσης να **εξάγετε γραμματοσειρές από word**, χρησιμοποιήστε την παρακάτω κλήση:

```csharp
List<FontResourceBase> allFonts = beforeEdit.Fonts;
```

### Βήμα 2.4: Εξαγωγή Όλων των Φυλλομετρήσεων Στυλ
Εξάγετε όλα τα φύλλα στυλ σε κειμενική μορφή.

```csharp
List<CssText> allStylesheets = beforeEdit.Css;
```

### Βήμα 2.5: Συγκέντρωση Όλων των Πόρων
Συγκεντρώστε όλους τους πόρους με μία κλήση.

```csharp
List<IHtmlResource> allResources = beforeEdit.AllResources;
```

Αυτό περιλαμβάνει εικόνες, γραμματοσειρές και φύλλα στυλ.

### Βήμα 2.6: Λήψη HTML Markup
Αποκτήστε το HTML markup του εγγράφου χωρίς ενσωματωμένους πόρους.

```csharp
string htmlMarkup = beforeEdit.GetContent();
```

## Πώς να **μετατρέψετε docx σε html** με προσαρμοσμένη διαχείριση;
Μερικές φορές χρειάζεται να προσαρμόσετε τους εξωτερικούς συνδέσμους ώστε να δείχνουν στους δικούς σας διαχειριστές πόρων.

## Βήμα 3: Προσαρμογή Εξωτερικών Συνδέσμων
### Βήμα 3.1: Προετοιμασία Προσαρμοσμένων Προθεμάτων
Προετοιμάστε προθέματα που θα προσαρτούν στα αρχικά εξωτερικά links.

```csharp
string customImagesRequesthandlerUri = "http://example.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://example.com/CssHandler/id=";
string customFontsRequesthandlerUri = "http://example.com/FontsHandler/id=";
```

### Βήμα 3.2: Δημιουργία Προθεματισμένου HTML Markup
Δημιουργήστε HTML markup με προσαρμοσμένους συνδέσμους.

```csharp
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```

### Βήμα 3.3: Λήψη Περιεχομένου HTML μόνο για το Body
Κάποιοι επεξεργαστές WYSIWYG χειρίζονται μόνο καθαρό HTML markup χωρίς κεφαλίδες.

```csharp
string onlyBodyContent = beforeEdit.GetBodyContent();
```

### Βήμα 3.4: Προθεματισμένο Περιεχόμενο μόνο Body
Δημιουργήστε περιεχόμενο μόνο για το body με προσαρμοσμένα προθέματα εικόνων.

```csharp
string prefixedBodyContent = beforeEdit.GetBodyContent(customImagesRequesthandlerUri);
```

### Βήμα 3.5: Εξαγωγή Φυλλομετρήσεων Στυλ
Εξάγετε τα φύλλα στυλ που χρησιμοποιούνται στο έγγραφο.

```csharp
List<string> stylesheets = beforeEdit.GetCssContent();
```

### Βήμα 3.6: Προθεματισμένα Φύλλα Στυλ
Εξάγετε τα φύλλα στυλ με προσαρμοσμένα προθέματα.

```csharp
List<string> prefixedStylesheets = beforeEdit.GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri);
```

## Πώς να **αποθηκεύσετε το έγγραφο ως html** σωστά;
## Βήμα 4: Αποθήκευση Εγγράφου ως HTML
Αποθηκεύστε το επεξεργασμένο έγγραφο ως αρχείο HTML, συμπεριλαμβανομένων των πόρων του.

```csharp
string htmlFilePath = Path.Combine("output", Path.GetFileNameWithoutExtension(inputFilePath) + ".html");
beforeEdit.Save(htmlFilePath);
```

Αυτή η μέθοδος δημιουργεί ξεχωριστό φάκελο για πόρους όπως φύλλα στυλ, εικόνες και γραμματοσειρές.

## Βήμα 5: Καταστροφή του EditableDocument
`EditableDocument` υλοποιεί το `IDisposable` και παρέχει τη δυνατότητα ελέγχου αν το αντικείμενο έχει καταστραφεί.

```csharp
Console.WriteLine("EditableDocument is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");
```

### Βήμα 5.1 Διαχείριση Συμβάντος Dispose
Μπορείτε επίσης να εγγραφείτε στο συμβάν διαγραφής.

```csharp
EventHandler someMethod = delegate { Console.WriteLine("Disposing event was spotted!"); };
beforeEdit.Disposed += someMethod;
```

## Βήμα 6: Δημιουργία EditableDocument από HTML
Δημιουργήστε ένα παράδειγμα του `EditableDocument` από ένα έγγραφο HTML.

### Βήμα 6.1: Από Αρχείο HTML

```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
```

### Βήμα 6.2: Από HTML Markup

```csharp
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);
```

Αυτά τα παραδείγματα (`afterEditFromFile` και `afterEditFromMarkup`) είναι πανομοιότυπα με το αρχικό (`beforeEdit`).

## Βήμα 7: Χειροκίνητη Καταστροφή
Καταστρέψτε χειροκίνητα τα παραδείγματα `EditableDocument`.

```csharp
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```

Αυτό εξασφαλίζει σωστό καθαρισμό των πόρων.

## Συνηθισμένα Προβλήματα και Λύσεις
- **Οι εικόνες δεν εμφανίζονται μετά την εξαγωγή:** Επαληθεύστε ότι το έγγραφο περιέχει ενσωματωμένες εικόνες και ότι προσπελάζετε το `beforeEdit.Images` μετά την κλήση του `Edit`.  
- **Οι γραμματοσειρές λείπουν στο HTML αποτέλεσμα:** Βεβαιωθείτε ότι καλείτε το `GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri)` για σωστή ενσωμάτωση των URL γραμματοσειρών.  
- **Μεγάλες συμβολοσειρές HTML προκαλούν πίεση μνήμης:** Χρησιμοποιήστε το `GetContent()` για markup χωρίς ενσωματωμένους πόρους και σερβίρετε εικόνες/CSS από ξεχωριστά αρχεία.

## Συχνές Ερωτήσεις

**Ε: Ποια μορφές υποστηρίζει το GroupDocs.Editor;**  
Α: Το GroupDocs.Editor υποστηρίζει DOCX, XLSX, PPTX και πολλές άλλες δημοφιλείς μορφές γραφείου.

**Ε: Μπορώ να χρησιμοποιήσω το GroupDocs.Editor χωρίς άδεια;**  
Α: Ναι, μπορείτε να το χρησιμοποιήσετε με [δωρεάν δοκιμή](https://releases.groupdocs.com/) ή [προσωρινή άδεια](https://purchase.groupdocs.com/temporary-license/).

**Ε: Πώς εξάγω συγκεκριμένους πόρους από ένα έγγραφο;**  
Α: Χρησιμοποιήστε τις συλλογές `Images`, `Fonts` και `Css` στο αντικείμενο `EditableDocument`.

**Ε: Είναι δυνατόν να προσαρμόσετε τους συνδέσμους στο HTML αποτέλεσμα;**  
Α: Ναι, περάστε προσαρμοσμένα προθέματα URI στο `GetContent` ή στο `GetBodyContent` για να ξαναγράψετε τους συνδέσμους εικόνων, CSS και γραμματοσειρών.

**Ε: Πώς αποθηκεύω ένα επεξεργασμένο έγγραφο ως αρχείο HTML;**  
Α: Καλέστε τη μέθοδο `Save` στο αντικείμενο `EditableDocument`, παρέχοντας διαδρομή αρχείου που λήγει σε `.html`.

---

**Τελευταία Ενημέρωση:** 2026-03-14  
**Δοκιμάστηκε Με:** GroupDocs.Editor for .NET (τελευταία έκδοση)  
**Συγγραφέας:** GroupDocs