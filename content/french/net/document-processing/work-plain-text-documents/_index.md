---
date: 2026-08-10
description: Découvrez comment modifier des fichiers texte brut à l'aide de GroupDocs.Editor
  pour .NET. Le guide couvre le chargement d'un fichier txt, la suppression des espaces,
  la définition de l'encodage du texte et l'enregistrement du résultat.
keywords:
- edit plain text
- load txt file
- trim trailing spaces
- convert leading spaces
- set text encoding
lastmod: 2026-08-10
linktitle: Travailler avec des documents texte brut
og_description: Découvrez comment modifier des fichiers texte brut avec GroupDocs.Editor
  pour .NET – charger un fichier txt, supprimer les espaces de fin, convertir les
  espaces de début, définir l'encodage du texte et enregistrer efficacement.
og_image_alt: Guide showing edit plain text workflow with GroupDocs.Editor for .NET
og_title: Modifier des documents texte brut avec GroupDocs.Editor pour .NET
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
title: Modifier des documents texte brut avec GroupDocs.Editor pour .NET
type: docs
url: /fr/net/document-processing/work-plain-text-documents/
weight: 15
---

# Modifier des documents texte brut avec GroupDocs.Editor pour .NET

## Introduction
Si vous devez **modifier du texte brut** rapidement et de manière fiable dans une application .NET, GroupDocs.Editor pour .NET est l'outil qui fait le gros du travail. Cette API prend en charge plus de 30 formats de documents, peut gérer des fichiers jusqu'à 500 Mo, et vous permet de manipuler du texte sans charger le fichier complet en mémoire. Dans ce tutoriel, vous apprendrez comment charger un fichier txt, supprimer les espaces de fin, convertir les espaces de début, définir le bon encodage, puis enregistrer le contenu modifié sur le disque. Prêt à mettre les mains à la pâte ? Plongeons‑y !

## Réponses rapides
- **Quelle est la première étape pour modifier un fichier txt ?** Chargez le fichier avec `Editor` en utilisant le chemin ou le flux dont vous disposez.  
- **Puis‑je changer l'encodage du fichier pendant la modification ?** Oui – le `TxtSaveOptions` vous permet de spécifier UTF‑8, UTF‑16, ou tout encodage personnalisé.  
- **Comment supprimer les espaces supplémentaires à la fin de chaque ligne ?** Récupérez le texte, appelez `TrimEnd()` sur chaque ligne, puis réécrivez‑le.  
- **GroupDocs.Editor est‑il gratuit à essayer ?** Un essai complet de 30 jours est disponible sur la page des releases.  
- **Quelles versions de .NET sont prises en charge ?** .NET Framework 4.6+, .NET Core 3.1+, et .NET 5/6/7.

## Qu’est‑ce que la modification de texte brut ?
**Edit plain text** signifie modifier programmétiquement les caractères à l'intérieur d'un simple fichier `.txt` — ajouter, supprimer ou reformater du texte — tout en préservant l'encodage d'origine du fichier et le style des sauts de ligne. Cela peut impliquer des tâches telles que la suppression des espaces blancs, la normalisation des fins de ligne, la mise à jour des valeurs de configuration ou l'insertion de contenu généré. L'opération doit garder le fichier lisible par n'importe quel éditeur de texte standard et maintenir les métadonnées existantes comme les marqueurs BOM.

## Pourquoi utiliser GroupDocs.Editor pour l’édition de texte brut ?
GroupDocs.Editor traite les fichiers de manière flux, ce qui signifie qu'il peut modifier un fichier journal de 300 Mo en utilisant moins de 50 Mo de RAM. La bibliothèque prend en charge **plus de 50 formats d’entrée et de sortie**, détecte automatiquement les styles de fin de ligne (CR, LF, CRLF), et offre des options intégrées pour **supprimer les espaces de fin** et **convertir les espaces de début** sans écrire de parseurs personnalisés.

## Prérequis
- **Environnement de développement .NET** – Visual Studio 2022 ou VS Code avec l'extension C#.  
- **GroupDocs.Editor pour .NET** – téléchargez depuis la page des releases [GroupDocs.Editor for .NET](https://releases.groupdocs.com/editor/net/) .  
- **Connaissances de base en C#** – vous devez être à l'aise avec les entrées/sorties de fichiers et la manipulation de chaînes.  
- **Éditeur de texte (optionnel)** – pour inspecter les fichiers source ; VS Code est recommandé.  
- Pour une utilisation détaillée, consultez la [documentation](https://tutorials.groupdocs.com/editor/net/).  
- Vous pouvez également parcourir la [page des releases](https://releases.groupdocs.com/).

## Comment modifier du texte brut étape par étape
Chargez le fichier, modifiez son contenu, puis enregistrez‑le – le tout en moins de dix lignes de code. Les sections suivantes vous guident à travers chaque étape avec des explications claires.

### Étape 1 : Obtenir le chemin du fichier TXT d’entrée
Tout d'abord, décidez si vous allez travailler avec un chemin de fichier physique ou un flux mémoire. Utiliser un chemin est l'approche la plus simple pour le développement local.

```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

### Étape 2 : Créer une instance d’Editor
`Editor` est la classe principale qui charge un document et fournit des capacités d’édition.

```csharp
string inputFilePath = "YourSampleDocument.txt";
```

### Étape 3 : Créer les options d’édition TXT
`TxtEditOptions` configure la façon dont les fichiers texte brut sont analysés et édités, vous permettant de définir l’encodage et les règles de gestion des espaces.

```csharp
using (Editor editor = new Editor(inputFilePath))
{
```

### Étape 4 : Créer une instance d’EditableDocument
`EditableDocument` représente la version en mémoire du document chargé, incluant son texte et toutes les ressources associées.

```csharp
    TextEditOptions editOptions = new TextEditOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        RecognizeLists = true,
        LeadingSpaces = TextLeadingSpacesOptions.ConvertToIndent,
        TrailingSpaces = TextTrailingSpacesOptions.Trim
    };
```

### Étape 5 : Modifier le contenu du document
Récupérez le texte original, appliquez les opérations de chaîne dont vous avez besoin (par ex., remplacer, tronquer, changer la casse), et stockez le résultat dans le `EditableDocument`.

```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```

### Étape 6 : Créer un EditableDocument avec le contenu mis à jour
Après avoir transformé le texte, créez une nouvelle instance de `EditableDocument` contenant la chaîne modifiée et la collection de ressources d'origine.

```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("text", "EDITED text");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```

### Étape 7 : Créer les options d’enregistrement WordProcessing
`WordProcessingSaveOptions` définit les paramètres pour enregistrer le document dans un format compatible Word tel que DOCX ou DOCM.

```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```

### Étape 8 : Créer les options d’enregistrement TXT
`TxtSaveOptions` spécifie comment le fichier texte brut modifié doit être écrit, incluant l’encodage, la préservation des fins de ligne, et la gestion de la mise en page des tableaux.

```csharp
    WordProcessingSaveOptions wordSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm)
    {
        Locale = System.Globalization.CultureInfo.GetCultureInfo("en-GB")
    };
```

### Étape 9 : Préparer les chemins de sortie
Déduisez le répertoire de sortie à partir du chemin du fichier d’entrée, puis construisez les noms de fichiers complets pour les résultats DOCX et TXT.

```csharp
    TextSaveOptions txtSaveOptions = new TextSaveOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        PreserveTableLayout = true
    };
```

### Étape 10 : Enregistrer le document modifié
Enfin, appelez `editor.Save` deux fois — une fois avec les options WordProcessing et une fois avec les options TXT — pour produire les deux formats en une seule opération.

```csharp
    string outputWordPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".docm");
    string outputTxtPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".txt");
```

## Problèmes courants et solutions
- **Les espaces de fin restent après l’édition** – assurez‑vous que `TxtEditOptions.TrimTrailingSpaces` est réglé sur `true` avant de charger le document.  
- **Encodage incorrect dans le fichier enregistré** – vérifiez que `TxtSaveOptions.Encoding` correspond à la page de code souhaitée (par ex., `Encoding.UTF8`).  
- **Les gros fichiers provoquent OutOfMemoryException** – utilisez l’API de streaming (`Editor.Load(Stream)`) au lieu de charger depuis un chemin de fichier pour limiter l’utilisation de la mémoire.  

## Questions fréquentes

**Q : Quels formats de fichiers GroupDocs.Editor pour .NET prend‑il en charge ?**  
R : La bibliothèque prend en charge plus de 50 formats, dont DOCX, TXT, HTML, PDF et markdown, vous permettant d’éditer et de convertir entre eux sans effort.

**Q : Comment obtenir un essai gratuit de GroupDocs.Editor pour .NET ?**  
R : Téléchargez l’essai depuis la [page des releases](https://releases.groupdocs.com/).

**Q : Puis‑je acheter une licence temporaire pour les tests ?**  
R : Oui, des licences temporaires sont disponibles via la [page d’achat GroupDocs](https://purchase.groupdocs.com/temporary-license/).

**Q : Où puis‑je trouver du support en cas de problème ?**  
R : Le forum officiel de support est le meilleur endroit – visitez le [forum de support GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).

**Q : Existe‑t‑il une documentation détaillée pour les scénarios avancés ?**  
R : Absolument. La référence complète se trouve sur la [page de documentation GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/).

## Conclusion
Vous avez maintenant maîtrisé comment **modifier du texte brut** à l’aide de GroupDocs.Editor pour .NET — charger un fichier txt, supprimer les espaces, convertir les espaces de début, définir le bon encodage, et enregistrer le résultat aux formats TXT et DOCX. Cette capacité vous permet d’automatiser le nettoyage de fichiers journaux, de générer des fichiers de configuration à la volée, ou de créer des pipelines de traitement de texte personnalisés sans réinventer la roue. Explorez des fonctionnalités supplémentaires telles que le traitement par lots et la conversion de documents en visitant la documentation officielle.

---

**Dernière mise à jour :** 2026-08-10  
**Testé avec :** GroupDocs.Editor 23.11 for .NET  
**Auteur :** GroupDocs  

```csharp
    editor.Save(afterEdit, outputWordPath, wordSaveOptions);
    editor.Save(afterEdit, outputTxtPath, txtSaveOptions);
}
System.Console.WriteLine("Document editing process completed successfully!");
```

## Tutoriels associés

- [Tutoriels de chargement de documents avec GroupDocs.Editor pour .NET](/editor/net/document-loading/)
- [Tutoriels d’enregistrement et d’exportation de documents pour GroupDocs.Editor .NET](/editor/net/document-saving/)
- [Tutoriels d’édition de texte brut et de documents DSV pour GroupDocs.Editor .NET](/editor/net/plain-text-dsv-documents/)