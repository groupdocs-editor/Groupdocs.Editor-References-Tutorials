---
title: Προηγμένη χρήση επεξεργάσιμων εγγράφων
linktitle: Προηγμένη χρήση επεξεργάσιμων εγγράφων
second_title: GroupDocs.Editor .NET API
description: Μάθετε προηγμένη χρήση του GroupDocs.Editor για .NET δημιουργία, επεξεργασία και εξαγωγή πόρων από έγγραφα μέσω προγραμματισμού.
weight: 11
url: /el/net/document-editing/advanced-usage-of-editable-documents/
type: docs
---
# Προηγμένη χρήση επεξεργάσιμων εγγράφων

## Εισαγωγή
Εάν είστε προγραμματιστής .NET που θέλει να βελτιώσει τις δυνατότητες επεξεργασίας εγγράφων σας, το GroupDocs.Editor για .NET προσφέρει μια ισχυρή σουίτα εργαλείων. Αυτός ο περιεκτικός οδηγός θα σας καθοδηγήσει στην προηγμένη χρήση επεξεργάσιμων εγγράφων χρησιμοποιώντας το GroupDocs.Editor, αναλύοντας κάθε βήμα λεπτομερώς για να διασφαλίσετε ότι μπορείτε να αξιοποιήσετε πλήρως τις δυνατότητές του.
## Προαπαιτούμενα
Πριν βουτήξετε στις προηγμένες λειτουργίες, βεβαιωθείτε ότι έχετε τα εξής:
- Το Visual Studio είναι εγκατεστημένο στο μηχάνημα ανάπτυξης.
- .NET Framework συμβατό με GroupDocs.Editor.
-  GroupDocs.Editor για τη βιβλιοθήκη .NET. Μπορείς[κατεβάστε το εδώ](https://releases.groupdocs.com/editor/net/).
-  Μια έγκυρη άδεια GroupDocs.Editor. Μπορείτε να πάρετε ένα[δωρεάν δοκιμή](https://releases.groupdocs.com/) ή αγοράστε α[προσωρινή άδεια](https://purchase.groupdocs.com/temporary-license/).
## Εισαγωγή χώρων ονομάτων
Για να ξεκινήσετε, βεβαιωθείτε ότι εισάγετε τους απαραίτητους χώρους ονομάτων στο έργο σας .NET:
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
## Βήμα 1: Δημιουργία παρουσίας EditableDocument
 Πρώτα, πρέπει να δημιουργήσετε ένα παράδειγμα του`EditableDocument` με τη φόρτωση και την επεξεργασία ενός εγγράφου εισόδου υποστηριζόμενης μορφής.
```csharp
string inputFilePath = "YourSampleDocument.docx";
Editor editor = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```
Σε αυτό το βήμα, φορτώνουμε το έγγραφο εισόδου και το προετοιμάζουμε για επεξεργασία.
## Βήμα 2: Εξαγωγή πόρων εγγράφων
 ο`EditableDocument` περιέχει διάφορους πόρους που μπορούν να εξαχθούν και να χειριστούν. Ας τα αναλύσουμε:
### Βήμα 2.1: Εξαγωγή ολόκληρου του εγγράφου ως HTML
Μπορείτε να δημιουργήσετε μια συμβολοσειρά που περιέχει ολόκληρο το έγγραφο με όλους τους πόρους του ενσωματωμένους ως HTML.
```csharp
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```
Αυτή η συμβολοσειρά θα είναι αρκετά μεγάλη καθώς περιλαμβάνει φύλλα στυλ, εικόνες και γραμματοσειρές κωδικοποιημένες στο base64.
### Βήμα 2.2: Εξαγωγή όλων των εικόνων
Εξαγωγή όλων των εικόνων από το έγγραφο.
```csharp
List<IImageResource> allImages = beforeEdit.Images;
```
### Βήμα 2.3: Εξαγωγή όλων των γραμματοσειρών
Εξαγάγετε όλες τις γραμματοσειρές που χρησιμοποιούνται στο έγγραφο.
```csharp
List<FontResourceBase> allFonts = beforeEdit.Fonts;
```
### Βήμα 2.4: Εξαγωγή όλων των φύλλων στυλ
Εξαγωγή όλων των φύλλων στυλ σε μορφή κειμένου.
```csharp
List<CssText> allStylesheets = beforeEdit.Css;
```
### Βήμα 2.5: Συγκεντρώστε όλους τους πόρους
Συγκεντρώστε όλους τους πόρους σε μία κλήση.
```csharp
List<IHtmlResource> allResources = beforeEdit.AllResources;
```
Αυτό περιλαμβάνει εικόνες, γραμματοσειρές και φύλλα στυλ.
### Βήμα 2.6: Λήψη σήμανσης HTML
Λάβετε τη σήμανση HTML του εγγράφου χωρίς ενσωματωμένους πόρους.
```csharp
string htmlMarkup = beforeEdit.GetContent();
```
## Βήμα 3: Προσαρμογή εξωτερικών συνδέσμων
Μερικές φορές, χρειάζεται να προσαρμόσετε τους εξωτερικούς συνδέσμους ώστε να παραπέμπουν σε έναν προσαρμοσμένο χειριστή πόρων. Δείτε πώς να το κάνετε:
### Βήμα 3.1: Προετοιμάστε προσαρμοσμένα προθέματα
Προετοιμάστε προθέματα που θα προσαρτούν αρχικούς εξωτερικούς συνδέσμους.
```csharp
string customImagesRequesthandlerUri = "http://example.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://example.com/CssHandler/id=";
string customFontsRequesthandlerUri = "http://example.com/FontsHandler/id=";
```
### Βήμα 3.2: Δημιουργία προθέματος σήμανσης HTML
Δημιουργήστε σήμανση HTML με προσαρμοσμένους συνδέσμους.
```csharp
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```
### Βήμα 3.3: Αποκτήστε Περιεχόμενο HTML μόνο για το σώμα
Ορισμένοι επεξεργαστές WYSIWYG χειρίζονται μόνο σήμανση καθαρού HTML χωρίς κεφαλίδες.
```csharp
string onlyBodyContent = beforeEdit.GetBodyContent();
```
### Βήμα 3.4: Περιεχόμενο μόνο για σώμα με πρόθεμα
Δημιουργήστε περιεχόμενο μόνο για το σώμα με προσαρμοσμένα προθέματα εικόνας.
```csharp
string prefixedBodyContent = beforeEdit.GetBodyContent(customImagesRequesthandlerUri);
```
### Βήμα 3.5: Εξαγωγή φύλλων στυλ
Εξαγωγή φύλλων στυλ που χρησιμοποιούνται στο έγγραφο.
```csharp
List<string> stylesheets = beforeEdit.GetCssContent();
```
### Βήμα 3.6: Φύλλα στυλ με πρόθεμα
Εξαγωγή φύλλων στυλ με προσαρμοσμένα προθέματα.
```csharp
List<string> prefixedStylesheets = beforeEdit.GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri);
```
## Βήμα 4: Αποθήκευση εγγράφου ως HTML
Αποθηκεύστε το επεξεργασμένο έγγραφο ως αρχείο HTML, συμπεριλαμβανομένων των πόρων του.
```csharp
string htmlFilePath = Path.Combine("output", Path.GetFileNameWithoutExtension(inputFilePath) + ".html");
beforeEdit.Save(htmlFilePath);
```
Αυτή η μέθοδος δημιουργεί έναν ξεχωριστό κατάλογο για πόρους όπως φύλλα στυλ, εικόνες και γραμματοσειρές.
## Βήμα 5: Απόρριψη του EditableDocument
 Εργαλεία EditableDocument`IDisposable` και παρέχει τη δυνατότητα ελέγχου εάν το στιγμιότυπο έχει απορριφθεί.
```csharp
Console.WriteLine("EditableDocument is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");
```
### Βήμα 5.1 Χειρισμός Συμβάντος Διάθεσης
Μπορείτε επίσης να εγγραφείτε στην εκδήλωση απόρριψης.
```csharp
EventHandler someMethod = delegate { Console.WriteLine("Disposing event was spotted!"); };
beforeEdit.Disposed += someMethod;
```
## Βήμα 6: Δημιουργία EditableDocument από HTML
Δημιουργήστε μια παρουσία του EditableDocument από ένα έγγραφο HTML.
### Βήμα 6.1: Από το αρχείο HTML
```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
```
### Βήμα 6.2: Από τη σήμανση HTML
```csharp
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);
```
Αυτές οι περιπτώσεις (μετά το EditFromFile και afterEditFromMarkup) είναι πανομοιότυπες με τις πρωτότυπες (πριν από την Επεξεργασία).
## Βήμα 7: Χειροκίνητη απόρριψη
Απορρίψτε με μη αυτόματο τρόπο τις περιπτώσεις EditableDocument.
```csharp
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```
Αυτό διασφαλίζει τη σωστή εκκαθάριση των πόρων.
## συμπέρασμα
Το GroupDocs.Editor για .NET παρέχει ισχυρά εργαλεία για την επεξεργασία εγγράφων μέσω προγραμματισμού. Ακολουθώντας αυτόν τον οδηγό βήμα προς βήμα, μπορείτε να διαχειριστείτε αποτελεσματικά το περιεχόμενο, τους πόρους και τις μορφές εξόδου εγγράφων. Είτε ενσωματώνετε πόρους, προσαρμόζετε εξωτερικούς συνδέσμους ή μετατρέπετε έγγραφα σε HTML, το GroupDocs.Editor σάς εξοπλίζει με τη λειτουργικότητα που απαιτείται για προηγμένη επεξεργασία εγγράφων.
## Συχνές ερωτήσεις
### Ποιες μορφές υποστηρίζει το GroupDocs.Editor;
Το GroupDocs.Editor υποστηρίζει διάφορες μορφές, συμπεριλαμβανομένων των DOCX, XLSX, PPTX και άλλων.
### Μπορώ να χρησιμοποιήσω το GroupDocs.Editor χωρίς άδεια χρήσης;
 Ναι, μπορείτε να το χρησιμοποιήσετε με α[δωρεάν δοκιμή](https://releases.groupdocs.com/) ή α[προσωρινή άδεια](https://purchase.groupdocs.com/temporary-license/).
### Πώς μπορώ να εξαγάγω συγκεκριμένους πόρους από ένα έγγραφο;
 Μπορείτε να εξαγάγετε εικόνες, γραμματοσειρές και φύλλα στυλ χρησιμοποιώντας τις παρεχόμενες μεθόδους όπως`Images`, `Fonts` , και`Css`.
### Είναι δυνατή η προσαρμογή των συνδέσμων στην έξοδο HTML;
Ναι, μπορείτε να προσαρμόσετε εξωτερικούς συνδέσμους καθορίζοντας προσαρμοσμένα προθέματα για εικόνες, CSS και γραμματοσειρές.
### Πώς μπορώ να αποθηκεύσω ένα επεξεργασμένο έγγραφο ως αρχείο HTML;
 Χρησιμοποιήστε το`Save` μέθοδος του`EditableDocument`class για να αποθηκεύσετε το έγγραφο ως αρχείο HTML, συμπεριλαμβανομένων των πόρων του.