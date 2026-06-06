---
date: 2026-06-06
description: Apprenez à répertorier les formats de documents pris en charge et à déterminer
  l'extension du format de fichier à l'aide de GroupDocs.Editor pour .NET. Guide étape
  par étape avec extraits de code, réponses rapides et FAQ.
keywords:
- list supported document formats
- determine file format extension
- GroupDocs.Editor .NET
- document editing API
- supported formats guide
linktitle: Lister les formats de documents pris en charge
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to list supported document formats and determine file format
    extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets,
    quick answers, and FAQs.
  headline: List Supported Document Formats with GroupDocs.Editor .NET
  type: TechArticle
- description: Learn how to list supported document formats and determine file format
    extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets,
    quick answers, and FAQs.
  name: List Supported Document Formats with GroupDocs.Editor .NET
  steps:
  - name: '**.NET development environment** – Visual Studio 2022 or any IDE that supports
      .NET 6+.'
    text: '**.NET development environment** – Visual Studio 2022 or any IDE that supports
      .NET 6+.'
  - name: '**GroupDocs.Editor for .NET library** – download from the [GroupDocs releases
      page](https://releases.groupdocs.com/editor/net/).'
    text: '**GroupDocs.Editor for .NET library** – download from the [GroupDocs releases
      page](https://releases.groupdocs.com/editor/net/).'
  - name: '**Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/)
      for unrestricted access.'
    text: '**Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/)
      for unrestricted access.'
  - name: '**Basic C# knowledge** – familiarity with namespaces, `using` statements,
      and console output.'
    text: '**Basic C# knowledge** – familiarity with namespaces, `using` statements,
      and console output.'
  - name: '**Loop Through Formats:** We iterate over all available Word‑processing
      formats.'
    text: '**Loop Through Formats:** We iterate over all available Word‑processing
      formats.'
  - name: '**Output Format Details:** For each format we print its friendly name and
      default file extension.'
    text: '**Output Format Details:** For each format we print its friendly name and
      default file extension.'
  - name: '**Loop Through Formats:** The same looping logic applies to presentations.'
    text: '**Loop Through Formats:** The same looping logic applies to presentations.'
  - name: '**Output Format Details:** The name and extension are displayed for each
      format.'
    text: '**Output Format Details:** The name and extension are displayed for each
      format.'
  - name: '**Parse Format:** `FromExtension` converts the `.xlsm` extension into its
      internal `SpreadsheetFormat` enum.'
    text: '**Parse Format:** `FromExtension` converts the `.xlsm` extension into its
      internal `SpreadsheetFormat` enum.'
  - name: '**Output Format:** The parsed format’s name is printed, confirming the
      mapping.'
    text: '**Output Format:** The parsed format’s name is printed, confirming the
      mapping.'
  type: HowTo
- questions:
  - answer: '`DocumentFormatInfo` provides metadata about supported file types, while
      `SaveOptions` configures how a document is written back to disk (format, compression,
      etc.).'
    question: What is the difference between `DocumentFormatInfo` and `SaveOptions`?
  - answer: Yes—use `DocumentFormatInfo.FromExtension("yourExt")`; if the extension
      isn’t recognized, the method returns `null`.
    question: Can I list formats for a custom file extension?
  - answer: Absolutely. Pass the password to the `Editor` constructor via `EditorSettings`
      to open encrypted documents.
    question: Does GroupDocs.Editor support password‑protected files?
  - answer: Over **30 input and output formats**, spanning Word, Excel, PowerPoint,
      HTML, and plain text.
    question: How many formats does GroupDocs.Editor actually support?
  - answer: Use the `GetEditableWordProcessingFormats()` (or Spreadsheet/Presentation
      equivalents) to retrieve formats that allow full edit capabilities.
    question: Is there a way to restrict the list to only editable formats?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Lister les formats de documents pris en charge avec GroupDocs.Editor .NET
type: docs
url: /fr/net/document-processing/work-document-formats/
weight: 13
---

# Liste des formats de documents pris en charge

Bienvenue dans notre tutoriel complet sur **comment répertorier les formats de documents pris en charge** avec GroupDocs.Editor pour .NET. Que vous construisiez une application web centrée sur les documents ou un outil de bureau de niveau entreprise, connaître exactement les formats que vous pouvez éditer ou convertir est essentiel. Dans ce guide, vous découvrirez comment énumérer les formats, analyser les extensions et modifier des documents — le tout avec des explications claires et conviviales ainsi que des extraits de code prêts à l’exécution.

## Réponses rapides
- **Comment lister tous les formats pris en charge ?** Utilisez `DocumentFormatInfo.GetSupportedWordProcessingFormats()` (ou les équivalents Presentation/Spreadsheet) et itérez la collection.  
- **Puis-je déterminer un format à partir d’une extension de fichier ?** Oui — appelez `DocumentFormatInfo.FromExtension(".docx")`.  
- **Quels types de fichiers GroupDocs.Editor prend‑en charge ?** Plus de 30 formats d’entrée et de sortie, y compris DOCX, XLSX, PPTX, HTML et texte brut.  
- **Ai‑je besoin d’une licence pour lister les formats ?** Une licence temporaire débloque l’API complète ; sinon, un essai fonctionne avec des fonctionnalités limitées.  
- **Quelles versions de .NET sont compatibles ?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.

## Qu’est‑ce que « répertorier les formats de documents pris en charge » ?
Cette expression désigne la récupération programmatique de la collection de types de fichiers que GroupDocs.Editor peut ouvrir, modifier et enregistrer. Cette opération vous permet de créer des listes déroulantes d’interface utilisateur dynamiques ou de valider les téléchargements d’utilisateurs avant le traitement, en veillant à ce que seules les fichiers compatibles soient transmis à l’éditeur pour une manipulation ultérieure.

## Pourquoi répertorier les formats de documents pris en charge ?
GroupDocs.Editor **prend en charge plus de 30 formats d’entrée et de sortie** et peut gérer des fichiers jusqu’à **2 Go** sans charger le document complet en mémoire. Connaître la liste exacte évite les erreurs d’exécution, améliore l’expérience utilisateur et vous permet d’appliquer des règles métier telles que « autoriser uniquement les documents Office modifiables ». Cela vous aide également à ne présenter aux utilisateurs que les formats réellement supportés par votre application.

## Prérequis
1. **Environnement de développement .NET** – Visual Studio 2022 ou tout IDE supportant .NET 6+.  
2. **Bibliothèque GroupDocs.Editor pour .NET** – téléchargez depuis la [page des releases GroupDocs](https://releases.groupdocs.com/editor/net/).  
3. **Licence temporaire** – obtenez une [licence temporaire](https://purchase.groupdocs.com/temporary-license/) pour un accès complet.  
4. **Connaissances de base en C#** – familiarité avec les espaces de noms, les instructions `using` et la sortie console.

## Comment répertorier les formats de documents pris en charge ?
Chargez la collection des formats pris en charge et affichez le nom et l’extension de chaque format. Ce modèle en deux étapes fonctionne pour les documents de traitement de texte, les feuilles de calcul et les présentations. En itérant la collection, vous pouvez remplir dynamiquement des éléments d’interface tels que des listes déroulantes, garantissant que les utilisateurs ne puissent sélectionner que les formats réellement gérés par l’éditeur.

```csharp
// No actual code block – placeholder retained from original tutorial
```csharp
using System;
using GroupDocs.Editor.Options;
```
```

### Répertorier les formats de traitement de texte
`Formats.WordProcessingFormats` est une énumération qui décrit chaque type de fichier de traitement de texte reconnu par l’éditeur. La propriété `All` renvoie une collection de ces objets de format.

```csharp
```csharp
foreach (Formats.WordProcessingFormats oneFormat in Formats.WordProcessingFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**Explication :**  
1. **Boucler sur les formats :** Nous itérons sur tous les formats de traitement de texte disponibles.  
2. **Afficher les détails du format :** Pour chaque format, nous affichons son nom convivial et son extension de fichier par défaut.

### Répertorier les formats de présentation
`Formats.PresentationFormats` fonctionne de la même manière pour les fichiers de présentations, exposant chaque type de présentation pris en charge via la collection `All`.

```csharp
```csharp
foreach (Formats.PresentationFormats oneFormat in Formats.PresentationFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**Explication :**  
1. **Boucler sur les formats :** La même logique de boucle s’applique aux présentations.  
2. **Afficher les détails du format :** Le nom et l’extension sont affichés pour chaque format.

## Comment déterminer l’extension d’un format de fichier ?
Parfois, vous ne disposez que du nom d’un fichier et devez en déduire le `DocumentFormat` correspondant. GroupDocs.Editor propose un assistant statique simple qui associe une extension de fichier à sa représentation interne de format, vous permettant de valider ou de convertir les fichiers avant de les charger dans l’éditeur.

### Analyse des formats de feuilles de calcul
`Formats.SpreadsheetFormats.FromExtension` convertit une chaîne d’extension de fichier en la valeur d’énumération du format de feuille de calcul correspondant.

```csharp
```csharp
Formats.SpreadsheetFormats expectedXlsm = Formats.SpreadsheetFormats.FromExtension(".xlsm");
Console.WriteLine("Parsed Spreadsheet format is {0}", expectedXlsm.Name);
```
```

**Explication :**  
1. **Analyser le format :** `FromExtension` convertit l’extension `.xlsm` en son énumération interne `SpreadsheetFormat`.  
2. **Afficher le format :** Le nom du format analysé est affiché, confirmant le mappage.

### Analyse des formats textuels
De même, `Formats.TextualFormats.FromExtension` résout les extensions de fichiers textuels comme HTML ou TXT.

```csharp
```csharp
Formats.TextualFormats expectedHtml = Formats.TextualFormats.FromExtension("html");
Console.WriteLine("Parsed Textual format is {0}", expectedHtml.Name);
```
```

**Explication :**  
1. **Analyser le format :** La méthode `FromExtension` résout l’extension `html` en un `TextFormat`.  
2. **Afficher le format :** Le nom du format textuel est affiché, utile pour les éditeurs web.

## Comment modifier des documents après avoir identifié les formats ?
Une fois le format connu, le chargement et la modification d’un document suivent un schéma cohérent. Vous créez d’abord une instance `Editor` avec le chemin du fichier source, puis appelez `Edit()` pour obtenir un `EditableDocument`. À partir de là, vous pouvez lire, modifier et enfin enregistrer le contenu en utilisant les `SaveOptions` appropriés.

### Chargement d’un document
`Editor` est la classe principale qui encapsule toutes les opérations d’édition pour un fichier donné.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/document.docx"))
{
    // Further steps will be covered here.
}
```
```

**Explication :**  
1. **Initialiser l’éditeur :** Créez une instance `Editor` en passant le chemin complet du fichier cible.  
2. **Modèle de libération :** L’instruction `using` garantit que toutes les ressources non gérées sont libérées rapidement.

### Extraction du contenu
`EditableDocument.GetContent()` renvoie le texte brut du document (ou le HTML pour les éditeurs web), que vous pouvez afficher ou manipuler.

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    string content = editableDocument.GetContent();
    Console.WriteLine(content);
}
```
```

**Explication :**  
1. **Méthode Edit :** `Edit()` renvoie un objet `EditableDocument`.  
2. **Obtenir le contenu :** `GetContent()` extrait le texte brut du document (ou le HTML pour les éditeurs web).  
3. **Afficher le contenu :** Le contenu est écrit dans la console pour vérification.

### Enregistrement des modifications
`SaveOptions` indique à l’éditeur comment et dans quel format écrire le document modifié dans le stockage.

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    // Modify content here
    SaveOptions saveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docx);
    editor.Save(editableDocument, "path/to/save/document.docx", saveOptions);
}
```
```

**Explication :**  
1. **Méthode Edit :** Récupérez à nouveau le `EditableDocument` après les modifications.  
2. **Modifier le contenu :** Appliquez vos changements à la chaîne (non montré ici).  
3. **Options d’enregistrement :** Configurez `SaveOptions` avec le format de sortie souhaité.  
4. **Enregistrer le document :** Sauvegardez le fichier modifié sur le disque.

## Comment travailler avec différents types de documents ?
GroupDocs.Editor abstrait la gestion de Word, Spreadsheet et Presentation derrière la même surface d’API, facilitant le changement de contexte sans devoir apprendre un nouvel ensemble de classes pour chaque famille de documents.

### Modification de documents de feuille de calcul
`SpreadsheetSaveOptions` définit comment une feuille de calcul est écrite, incluant le format et les paramètres de compression optionnels.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/spreadsheet.xlsx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // Modify content here
        SaveOptions saveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsx);
        editor.Save(editableDocument, "path/to/save/spreadsheet.xlsx", saveOptions);
    }
}
```
```

**Explication :**  
1. **Initialiser l’éditeur :** Passez le chemin d’un fichier de feuille de calcul au constructeur `Editor`.  
2. **Méthode Edit :** Récupérez un `EditableDocument`.  
3. **Obtenir le contenu :** Affichez la représentation CSV de la feuille de calcul (ou HTML).  
4. **Modifier le contenu :** Appliquez les modifications au niveau des cellules nécessaires.  
5. **Options d’enregistrement :** Choisissez les `SpreadsheetSaveOptions` appropriées.  
6. **Enregistrer le document :** Écrivez la feuille de calcul mise à jour dans le stockage.

### Modification de documents de présentation
`PresentationSaveOptions` contrôle le format de sortie des présentations, vous permettant de conserver ou de changer le type de fichier original.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/presentation.pptx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // Modify content here
        SaveOptions saveOptions = new PresentationSaveOptions(PresentationFormats.Pptx);
        editor.Save(editableDocument, "path/to/save/presentation.pptx", saveOptions);
    }
}
```
```

**Explication :**  
1. **Initialiser l’éditeur :** Chargez un fichier PowerPoint via `Editor`.  
2. **Méthode Edit :** Obtenez un `EditableDocument`.  
3. **Obtenir le contenu :** Extrayez le HTML des diapositives ou le texte brut.  
4. **Modifier le contenu :** Mettez à jour les titres, puces ou images.  
5. **Options d’enregistrement :** Utilisez `PresentationSaveOptions` pour définir le format de sortie.  
6. **Enregistrer le document :** Sauvegardez la présentation modifiée.

## Problèmes courants et solutions
- **Erreur « Format non pris en charge » :** Vérifiez que vous utilisez la dernière version de GroupDocs.Editor ; elle ajoute régulièrement la prise en charge de nouveaux formats Office.  
- **Consommation mémoire pour les gros fichiers :** Activez le mode streaming en définissant `EditorSettings.EnableStreaming = true` avant de charger le document.  
- **Licence non appliquée :** Assurez‑vous que le fichier de licence temporaire est placé à la racine de l’application ou chargé via `License license = new License(); license.SetLicense("path/to/license.lic");`.

## Questions fréquemment posées

**Q : Quelle est la différence entre `DocumentFormatInfo` et `SaveOptions` ?**  
R : `DocumentFormatInfo` fournit des métadonnées sur les types de fichiers pris en charge, tandis que `SaveOptions` configure la façon dont un document est enregistré sur le disque (format, compression, etc.).

**Q : Puis‑je répertorier les formats pour une extension de fichier personnalisée ?**  
R : Oui — utilisez `DocumentFormatInfo.FromExtension("yourExt")` ; si l’extension n’est pas reconnue, la méthode renvoie `null`.

**Q : GroupDocs.Editor prend‑il en charge les fichiers protégés par mot de passe ?**  
R : Absolument. Transmettez le mot de passe au constructeur `Editor` via `EditorSettings` pour ouvrir les documents chiffrés.

**Q : Combien de formats GroupDocs.Editor prend‑il réellement en charge ?**  
R : Plus de **30 formats d’entrée et de sortie**, couvrant Word, Excel, PowerPoint, HTML et texte brut.

**Q : Existe‑t‑il un moyen de restreindre la liste aux seuls formats éditables ?**  
R : Utilisez `GetEditableWordProcessingFormats()` (ou les équivalents Spreadsheet/Presentation) pour récupérer les formats qui permettent des capacités d’édition complètes.

## Ressources supplémentaires
- Téléchargez la bibliothèque depuis la [page des releases GroupDocs](https://releases.groupdocs.com/editor/net/).  
- Obtenez une [licence temporaire](https://purchase.groupdocs.com/temporary-license/) pour un accès complet aux fonctionnalités.  
- Essayez le produit avec un [essai gratuit](https://releases.groupdocs.com/).  
- Explorez des exemples d’utilisation détaillés dans la [documentation GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/).  
- Obtenez de l’aide de la communauté sur le [forum de support](https://forum.groupdocs.com/c/editor/20).

## Conclusion
En suivant ce guide, vous savez maintenant comment **répertorier les formats de documents pris en charge**, **déterminer le format d’un fichier à partir de son extension**, et **modifier des documents** pour les types Word, Spreadsheet et Presentation en utilisant GroupDocs.Editor pour .NET. Intégrez ces extraits dans vos propres projets pour créer des applications robustes et conscientes des formats, qui raviront les utilisateurs finaux et réduiront les erreurs d’exécution.

---

**Last Updated:** 2026-06-06  
**Tested With:** GroupDocs.Editor 23.9 for .NET  
**Author:** GroupDocs

## Tutoriels associés

- [Maîtriser le chargement de documents en .NET avec GroupDocs.Editor : Guide complet](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)
- [Maîtriser l’édition de documents en .NET avec GroupDocs.Editor : Guide complet](/editor/net/document-editing/master-document-editing-dotnet-groupdocs-editor/)
- [Convertir Word en HTML avec GroupDocs.Editor .NET : Guide étape par étape](/editor/net/document-saving/convert-word-to-html-groupdocs-editor-dotnet/)