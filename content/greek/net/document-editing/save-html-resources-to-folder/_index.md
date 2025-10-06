---
title: Αποθήκευση πόρων HTML στο φάκελο
linktitle: Αποθήκευση πόρων HTML στο φάκελο
second_title: GroupDocs.Editor .NET API
description: Μάθετε πώς να εξάγετε πόρους HTML από έγγραφα χρησιμοποιώντας το Groupdocs.Editor για .NET. Αυτό το περιεκτικό σεμινάριο παρέχει βήμα προς βήμα καθοδήγηση για προγραμματιστές.
weight: 13
url: /el/net/document-editing/save-html-resources-to-folder/
type: docs
---
# Αποθήκευση πόρων HTML στο φάκελο

## Εισαγωγή
Το Groupdocs.Editor για .NET είναι ένα ισχυρό εργαλείο που επιτρέπει στους προγραμματιστές να χειρίζονται και να μετατρέπουν έγγραφα στις εφαρμογές τους .NET απρόσκοπτα. Είτε θέλετε να εξαγάγετε πόρους HTML από ένα έγγραφο είτε να εκτελέσετε προηγμένες εργασίες επεξεργασίας, το Groupdocs.Editor απλοποιεί τη διαδικασία με το διαισθητικό API και την εκτενή τεκμηρίωση.
## Προαπαιτούμενα
Πριν βουτήξετε στο σεμινάριο, βεβαιωθείτε ότι έχετε τις ακόλουθες προϋποθέσεις:
1. Βασικές γνώσεις C# και .NET: Η εξοικείωση με τη γλώσσα προγραμματισμού C# και το πλαίσιο .NET είναι απαραίτητη για να ακολουθήσετε μαζί με τα παραδείγματα.
2.  Groupdocs.Editor για .NET Library: Κατεβάστε και εγκαταστήστε το Groupdocs.Editor για τη βιβλιοθήκη .NET από το[δικτυακός τόπος](https://releases.groupdocs.com/editor/net/).
3. Περιβάλλον ανάπτυξης: Ρυθμίστε το περιβάλλον ανάπτυξης που προτιμάτε, όπως το Visual Studio ή οποιοδήποτε άλλο συμβατό IDE.

## Εισαγωγή χώρων ονομάτων
Για να ξεκινήσετε, εισαγάγετε τους απαραίτητους χώρους ονομάτων στο έργο σας C#:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```
##Τώρα, ας αναλύσουμε τη διαδικασία αποθήκευσης πόρων HTML σε έναν φάκελο χρησιμοποιώντας το Groupdocs.Editor για .NET σε πολλά βήματα:
## Βήμα 1: Εκκίνηση Groupdocs.Editor
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
 Αρχικά, αρχικοποιήστε το`Editor`αντικείμενο παρέχοντας τη διαδρομή προς το δείγμα εγγράφου σας. Σε αυτό το παράδειγμα, χρησιμοποιούμε ένα έγγραφο του Word, επομένως προσδιορίζουμε`WordProcessingLoadOptions` ως τύπος εγγράφου.
## Βήμα 2: Επεξεργασία εγγράφου
```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
 Στη συνέχεια, δημιουργήστε ένα`EditableDocument` αντικείμενο καλώντας το`Edit` μέθοδος του`Editor` αντικείμενο. Αυτό σας επιτρέπει να εκτελείτε λειτουργίες επεξεργασίας στο έγγραφο.
## Βήμα 3: Εξαγωγή πόρων
```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
Εξάγετε πόρους όπως εικόνες, γραμματοσειρές και φύλλα στυλ από το έγγραφο και αποθηκεύστε τους σε αντίστοιχες λίστες.
## Βήμα 4: Καθορίστε τον φάκελο εξόδου
```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
Καθορίστε το φάκελο εξόδου όπου θα αποθηκευτούν οι εξαγόμενοι πόροι. Μπορείτε να προσαρμόσετε τη διαδρομή φακέλου σύμφωνα με τις απαιτήσεις σας.
## Βήμα 5: Αποθήκευση πόρων
```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
Κάντε βρόχο σε κάθε πόρο εικόνας, αποθηκεύστε τον στο φάκελο εξόδου και εμφανίστε σχετικές πληροφορίες όπως το όνομα αρχείου, τον τύπο και τις διαστάσεις.
```csharp
		foreach (FontResourceBase oneFont in fonts)
		{
			Console.WriteLine("Saving {0} of {1} type",
				oneFont.FilenameWithExtension, oneFont.Type.FormalName);
			oneFont.Save(Path.Combine(outputFolder, oneFont.FilenameWithExtension));
		}
```
Ομοίως, αποθηκεύστε κάθε πόρο γραμματοσειράς στο φάκελο εξόδου.
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

## συμπέρασμα
Εν κατακλείδι, το Groupdocs.Editor για .NET παρέχει μια βολική λύση για τη διαχείριση και τον χειρισμό εγγράφων μέσω προγραμματισμού εντός εφαρμογών .NET. Ακολουθώντας αυτό το σεμινάριο, μπορείτε εύκολα να εξαγάγετε πόρους HTML από έγγραφα και να προσαρμόσετε τη διαδικασία σύμφωνα με τις συγκεκριμένες απαιτήσεις σας.
## Συχνές ερωτήσεις
### Είναι το Groupdocs.Editor συμβατό με άλλες μορφές εγγράφων εκτός από το Word;
Ναι, το Groupdocs.Editor υποστηρίζει ένα ευρύ φάσμα μορφών εγγράφων, όπως Excel, PowerPoint, PDF και άλλα.
### Μπορώ να ενσωματώσω το Groupdocs.Editor στην εφαρμογή Ιστού μου;
Οπωσδήποτε, το Groupdocs.Editor προσφέρει απρόσκοπτη ενοποίηση με εφαρμογές web που έχουν αναπτυχθεί στο πλαίσιο .NET.
### Το Groupdocs.Editor παρέχει υποστήριξη για υπηρεσίες αποθήκευσης cloud;
Ναι, το Groupdocs.Editor υποστηρίζει την ενοποίηση με δημοφιλείς υπηρεσίες αποθήκευσης cloud όπως το Google Drive, το Dropbox και το Microsoft OneDrive.
### Υπάρχει διαθέσιμη δωρεάν δοκιμή για το Groupdocs.Editor;
Ναι, μπορείτε να επωφεληθείτε από μια δωρεάν δοκιμή του Groupdocs.Editor από τον ιστότοπο.
### Πώς μπορώ να λάβω τεχνική υποστήριξη για το Groupdocs.Editor;
Για τεχνική βοήθεια και υποστήριξη της κοινότητας, μπορείτε να επισκεφτείτε το φόρουμ του Groupdocs.Editor.