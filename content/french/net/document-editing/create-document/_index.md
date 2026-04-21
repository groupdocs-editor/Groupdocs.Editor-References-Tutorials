---
date: 2026-03-14
description: Apprenez à modifier les présentations PowerPoint et d’autres types de
  documents à l’aide de GroupDocs.Editor pour .NET. Le guide explique également comment
  enregistrer le document modifié et éditer un document Word avec .NET.
linktitle: Create Document
second_title: GroupDocs.Editor .NET API
title: Modifier une présentation PowerPoint avec GroupDocs.Editor pour .NET
type: docs
url: /fr/net/document-editing/create-document/
weight: 10
---

 installations. Explore the library’s advanced options to tailor the editing experience to your specific business needs.

Translate.

---

**Last Updated:** 2026-03-14  
**Tested With:** GroupDocs.Editor for .NET (latest release)  
**Author:** GroupDocs

Translate the labels but keep dates.

Now produce final output.

Be careful to keep markdown formatting exactly.

Let's craft translation.

We'll keep code block placeholders unchanged.

Also note "step-by-step in order - do not skip sections". We'll keep order.

Now produce final content.# Modifier une présentation PowerPoint avec GroupDocs.Editor pour .NET

## Introduction
Si vous recherchez une façon fiable de **modifier des présentations PowerPoint** de manière programmatique, GroupDocs.Editor pour .NET est la solution. Cette bibliothèque vous permet de travailler avec les formats Word, Excel, PowerPoint, Ebook et Email — le tout via une API unique et facile à utiliser. Dans ce tutoriel, nous parcourrons la création et la modification de chaque type de document pris en charge, vous montrerons comment **enregistrer les flux de documents modifiés**, et vous donnerons des conseils pratiques que vous pourrez appliquer dans des projets réels.

## Quick Answers
- **Quelle bibliothèque me permet de modifier des fichiers PowerPoint en .NET ?** GroupDocs.Editor pour .NET.  
- **Puis‑je modifier des fichiers Word, Excel et Epub avec la même API ?** Oui, la même classe `Editor` prend en charge tous ces formats.  
- **Comment capturer le fichier modifié ?** Fournissez une fonction de rappel (par ex., `SaveNewDocument`) qui reçoit le flux de résultat.  
- **Ai‑je besoin d’une licence pour une utilisation en production ?** Oui — achetez une licence ou utilisez une licence d’essai temporaire.  
- **Quelles versions de .NET sont prises en charge ?** .NET Framework 4.0+, .NET Core et .NET 5/6.

## Qu’est‑ce que la « edit PowerPoint presentation » avec GroupDocs.Editor ?
Modifier une présentation PowerPoint consiste à charger un fichier `.pptx`, appliquer des changements (comme la modification de diapositives, de texte ou d’éléments cachés), puis récupérer le fichier mis à jour — le tout sans nécessiter l’installation de Microsoft Office.

## Pourquoi utiliser GroupDocs.Editor pour .NET ?
- **API unique pour de nombreux formats** – Aucun besoin de jongler avec des bibliothèques distinctes pour Word, Excel ou Epub.  
- **Aucune dépendance à Office** – Fonctionne sur les serveurs, les conteneurs et les pipelines CI.  
- **Contrôle fin** – Personnalisez la pagination, les informations de langue, l’extraction de polices, etc.  
- **Traitement basé sur les flux** – Idéal pour les services cloud où vous travaillez avec des streams en mémoire plutôt qu’avec des fichiers physiques.

## Prérequis
- Visual Studio (toute édition récente).  
- .NET Framework 4.0 ou supérieur (ou .NET Core/.NET 5+).  
- Bibliothèque GroupDocs.Editor pour .NET – téléchargez‑la depuis [here](https://releases.groupdocs.com/editor/net/).  
- Connaissances de base en C#.

## Import Namespaces
Tout d’abord, importez les espaces de noms contenant les classes principales que nous allons utiliser.

```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using System.IO;
```

## Step 1: Setting Up the Stream
Nous utiliserons un flux mémoire comme espace réservé au contenu du document.

```csharp
Stream memoryStream = Stream.Null;
```

## Step 2: Callback Function to **save edited document**
Définissez un rappel qui reçoit le flux modifié et le stocke dans `memoryStream`.

```csharp
void SaveNewDocument(Stream resultStream)
{
    memoryStream = resultStream;
}
```

## Step 3: Creating and Editing a WordProcessing Document  
(Ici nous **edit word document .net**.)

### Create and Edit with Default Options
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    EditableDocument defaultWordProcessingDoc = editor.Edit();
}
```

### Create and Edit with Custom Options
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    WordProcessingEditOptions wordProcessingEditOptions = new WordProcessingEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true,
        FontExtraction = FontExtractionOptions.ExtractAllEmbedded
    };
    EditableDocument editableWordProcessingDocument = editor.Edit(wordProcessingEditOptions);
}
```

## Step 4: Creating and Editing a Spreadsheet Document  
(Utilisez ceci pour **edit excel file .net**.)

### Create and Edit with Default Options
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    EditableDocument defaultEditableSpreadsheetDocument = editor.Edit();
}
```

### Create and Edit with Custom Options
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    SpreadsheetEditOptions spreadsheetEditOptions = new SpreadsheetEditOptions
    {
        WorksheetIndex = 0,
        ExcludeHiddenWorksheets = true
    };
    EditableDocument editableSpreadsheetDocument = editor.Edit(spreadsheetEditOptions);
}
```

## Step 5: **Edit PowerPoint Presentation** – Creating and Editing a Presentation Document
C’est le cœur de notre mot‑clé principal.

### Create and Edit with Default Options
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    EditableDocument defaultEditablePresentationDocument = editor.Edit();
}
```

### Create and Edit with Custom Options
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    PresentationEditOptions presentationEditOptions = new PresentationEditOptions
    {
        ShowHiddenSlides = false,
        SlideNumber = 0
    };
    EditableDocument editablePresentationDocument = editor.Edit(presentationEditOptions);
}
```

## Step 6: Creating and Editing an Ebook Document  
(Ici nous **edit epub file**.)

### Create and Edit with Default Options
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EditableDocument defaultEditableEbookDocument = editor.Edit();
}
```

### Create and Edit with Custom Options
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EbookEditOptions ebookEditOptions = new EbookEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true
    };
    EditableDocument editableEbookDocument = editor.Edit(ebookEditOptions);
}
```

## Step 7: Creating and Editing an Email Document
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EditableDocument defaultEditableEmailDocument = editor.Edit();
}
```

### Create and Edit with Custom Options
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EmailEditOptions emailEditOptions = new EmailEditOptions
    {
        MailMessageOutput = MailMessageOutput.All
    };
    EditableDocument editableEmailDocument = editor.Edit(emailEditOptions);
}
```

## Step 8: Finalizing the Process
Libérez le flux pour libérer les ressources une fois que vous avez terminé.

```csharp
memoryStream.Dispose();
System.Console.WriteLine("CreateDocument routine has successfully finished");
```

## Common Pitfalls & Tips
- **N’oubliez jamais de libérer le flux** – le laisser ouvert peut entraîner des fuites de mémoire dans des services à long terme.  
- **Lors de la modification de PowerPoint, assurez‑vous de définir correctement `SlideNumber`** ; sinon la première diapositive peut être dupliquée.  
- **Si vous devez conserver le nom de fichier original**, stockez‑le avant le rappel et renommez le flux de sortie après la modification.  
- **Pour les documents volumineux**, envisagez de les traiter par morceaux ou d’utiliser `Editor` avec un fichier temporaire afin d’éviter une consommation excessive de mémoire.

## Frequently Asked Questions

**Q : Quels types de documents puis‑je modifier avec GroupDocs.Editor pour .NET ?**  
R : Vous pouvez modifier des documents WordProcessing, des feuilles de calcul, des présentations, des ebooks et des emails — y compris les fichiers PowerPoint pour le cas d’utilisation **edit PowerPoint presentation**.

**Q : Est‑il possible de personnaliser les options de modification ?**  
R : Oui, chaque format possède sa propre classe d’options (par ex., `WordProcessingEditOptions`, `SpreadsheetEditOptions`, `PresentationEditOptions`) qui vous permet d’ajuster la pagination, les diapositives cachées, la sélection de feuilles, etc.

**Q : Comment gérer la sortie des documents modifiés ?**  
R : Utilisez la fonction de rappel (`SaveNewDocument`) pour capturer le flux modifié, puis vous pouvez l’écrire sur disque, dans une base de données ou le renvoyer depuis une API web.

**Q : Ai‑je besoin d’une licence pour utiliser GroupDocs.Editor pour .NET ?**  
R : Oui, une licence est requise en production. Vous pouvez en obtenir une depuis [here](https://purchase.groupdocs.com/buy). Une licence d’essai temporaire est également disponible.

**Q : Où puis‑je trouver une documentation plus détaillée ?**  
R : Une documentation détaillée est disponible sur la [GroupDocs.Editor for .NET documentation page](https://tutorials.groupdocs.com/editor/net/).

## Conclusion
GroupDocs.Editor pour .NET simplifie la **modification des présentations PowerPoint** ainsi qu’un large éventail d’autres types de documents. En suivant les étapes ci‑dessus, vous pouvez créer, modifier et **enregistrer les flux de documents modifiés** entièrement en code, sans dépendre d’installations Office. Explorez les options avancées de la bibliothèque pour adapter l’expérience de modification à vos besoins métier spécifiques.

---

**Last Updated:** 2026-03-14  
**Tested With:** GroupDocs.Editor pour .NET (dernière version)  
**Author:** GroupDocs