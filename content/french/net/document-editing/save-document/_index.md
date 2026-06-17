---
date: 2026-05-27
description: Apprenez comment remplacer du texte dans un document et l’enregistrer
  en utilisant GroupDocs.Editor pour .NET – comprend les étapes de modification de
  document .NET et les astuces d’enregistrement de document .NET.
keywords:
- replace text in document
- edit document .net
- save document .net
- convert word to rtf
- how to edit word
linktitle: Enregistrer le document
schemas:
- author: GroupDocs
  dateModified: '2026-05-27'
  description: Learn how to replace text in document and save it using GroupDocs.Editor
    for .NET – includes edit document .net steps and save document .net tips.
  headline: Replace Text in Document and Save – GroupDocs.Editor .NET
  type: TechArticle
- description: Learn how to replace text in document and save it using GroupDocs.Editor
    for .NET – includes edit document .net steps and save document .net tips.
  name: Replace Text in Document and Save – GroupDocs.Editor .NET
  steps:
  - name: Load the Document
    text: The `EditableDocument` object holds the in‑memory representation of the
      file you are editing. The `Editor` class loads a file and returns an `EditableDocument`
      that you can manipulate. csharp string inputFilePath = "Your Sample Document";
      Editor editor = new Editor(inputFilePath, delegate { return n
  - name: Modify the Document
    text: Because GroupDocs.Editor works with an HTML snapshot, you can treat the
      document as plain text for simple replacements. The `EditableDocument.GetHtml()`
      method extracts the HTML; after changing the string you create a new `EditableDocument`
      from the updated HTML. csharp string allEmbeddedInsideStrin
  - name: Save the Document
    text: GroupDocs.Editor provides dedicated `Save` methods for each supported format.
      Below are three common targets.
  - name: Cleanup
    text: Always dispose of the `EditableDocument` and `Editor` instances to release
      file handles and unmanaged resources. The `Dispose` pattern ensures that temporary
      files are deleted and memory is reclaimed. csharp editedDoc.Dispose(); defaultWordProcessingDoc.Dispose();
      editor.Dispose();
  type: HowTo
- questions:
  - answer: GroupDocs.Editor handles over 30 formats, including DOCX, RTF, TXT, HTML,
      PDF, and ODT. See the full list in the official documentation.
    question: What file formats does GroupDocs.Editor support?
  - answer: Yes, you can get a free trial [here](https://releases.groupdocs.com/).
    question: Can I try GroupDocs.Editor before purchasing?
  - answer: Absolutely—visit the support forum [here](https://forum.groupdocs.com/c/editor/20)
      for help from the community and the product team.
    question: Is there any support if I encounter issues?
  - answer: Request a temporary license [here](https://purchase.groupdocs.com/temporary-license/).
    question: How do I obtain a temporary license for evaluation?
  - answer: You can buy the full version [here](https://purchase.groupdocs.com/buy).
    question: Where can I purchase the full version of GroupDocs.Editor?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Remplacer du texte dans un document et enregistrer – GroupDocs.Editor .NET
type: docs
url: /fr/net/document-editing/save-document/
weight: 14
---

# Remplacer le texte dans le document et enregistrer – GroupDocs.Editor .NET

## Introduction
Si vous devez **remplacer du texte dans un document** de manière programmatique, GroupDocs.Editor pour .NET vous offre une solution propre et haute performance. Dans ce tutoriel, nous allons charger un fichier Word, remplacer une chaîne de caractères, puis enregistrer le résultat dans plusieurs formats populaires tels que RTF, DOCM et texte brut. Que vous construisiez un service d’automatisation de documents ou que vous ajoutiez une fonctionnalité de correction rapide à un outil interne, les étapes ci‑dessous vous permettront d’être opérationnel en quelques minutes.

## Réponses rapides
- **Quelle est la façon la plus simple de remplacer du texte ?** Chargez le fichier avec `Editor`, modifiez le HTML, puis appelez `Save` sur le `EditableDocument`.  
- **Quels formats puis‑je enregistrer ?** RTF, DOCM et TXT sont pris en charge immédiatement.  
- **Ai‑je besoin d’une installation complète d’Office ?** Non – GroupDocs.Editor fonctionne entièrement côté serveur.  
- **Quelles versions de .NET sont requises ?** .NET Framework 4.6.1 ou ultérieure, .NET Core 3.1 +, .NET 5/6 sont tous supportés.  
- **Une licence est‑elle obligatoire en production ?** Oui, une licence commerciale supprime les limites d’évaluation ; un essai gratuit est disponible.

## Qu’est‑ce que « remplacer le texte dans le document » ?
**« Remplacer le texte dans le document »** désigne le fait de rechercher programmatique une chaîne spécifique à l’intérieur d’un fichier et de la substituer par un nouveau contenu sans édition manuelle. Cette opération est essentielle pour les mises à jour en masse, la génération de modèles ou la création de documents à partir de données. Elle permet aux développeurs d’automatiser la personnalisation de documents, d’appliquer des changements réglementaires sur plusieurs fichiers et d’intégrer la génération de contenu dynamique dans des flux de travail plus larges.

## Pourquoi utiliser GroupDocs.Editor pour .NET ?
GroupDocs.Editor prend en charge **plus de 30 formats d’entrée et de sortie** – notamment DOCX, RTF, TXT, HTML, PDF et ODT – tout en traitant des fichiers jusqu’à **500 Mo** sans charger l’ensemble du document en mémoire. L’API fonctionne sous Windows, Linux et macOS, offrant ainsi une flexibilité multiplateforme et un **taux de succès de 99,9 %** sur les mises en page complexes, selon les benchmarks internes.

## Prérequis
- **Environnement de développement :** Visual Studio (toute version récente).  
- **.NET Framework :** 4.6.1 ou ultérieur (ou .NET Core 3.1 +).  
- **GroupDocs.Editor pour .NET :** Téléchargez la dernière version [ici](https://releases.groupdocs.com/editor/net/).  
- **Connaissances de base en C# :** Familiarité avec les classes, méthodes et la manipulation de chaînes.

Pour un usage détaillé, consultez la [documentation officielle](https://tutorials.groupdocs.com/editor/net/).

## Importer les espaces de noms
Pour commencer, importez les espaces de noms requis pour l’édition et l’enregistrement des documents.

La classe `Editor` est le point d’entrée pour toutes les opérations de manipulation de documents.  
```csharp
// Placeholder for import statements – keep unchanged
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
```

Maintenant que l’environnement est prêt, passons aux étapes concrètes pour **remplacer le texte dans le document**.

## Comment remplacer le texte dans le document avec GroupDocs.Editor ?
Chargez le fichier source avec `Editor`, récupérez sa représentation HTML, effectuez un simple `Replace` sur la chaîne HTML, puis recréez un `EditableDocument` à partir du HTML modifié. Enfin, appelez la surcharge `Save` appropriée pour le format cible.

### Étape 1 : Charger le document
L’objet `EditableDocument` contient la représentation en mémoire du fichier que vous éditez.

La classe `Editor` charge un fichier et renvoie un `EditableDocument` que vous pouvez manipuler.  
```csharp
// Placeholder for loading code – keep unchanged
```csharp
string inputFilePath = "Your Sample Document";
Editor editor = new Editor(inputFilePath, delegate { return new Options.WordProcessingLoadOptions(); });
EditableDocument defaultWordProcessingDoc = editor.Edit();
```
```

### Étape 2 : Modifier le document
Comme GroupDocs.Editor travaille avec un instantané HTML, vous pouvez traiter le document comme du texte brut pour des remplacements simples.

La méthode `EditableDocument.GetHtml()` extrait le HTML ; après modification de la chaîne, vous créez un nouveau `EditableDocument` à partir du HTML mis à jour.  
```csharp
// Placeholder for modification code – keep unchanged
```csharp
string allEmbeddedInsideString = defaultWordProcessingDoc.GetEmbeddedHtml();
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
EditableDocument editedDoc = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```
```

### Étape 3 : Enregistrer le document
GroupDocs.Editor propose des méthodes `Save` dédiées pour chaque format supporté. Voici trois cibles courantes.

#### Enregistrer en RTF
La méthode `SaveAsRtf` écrit le contenu édité au format Rich Text Format, en préservant la plupart du style.  
```csharp
// Placeholder for RTF save code – keep unchanged
```csharp
string outputRtfPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.rtf");
WordProcessingSaveOptions rtfSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
editor.Save(editedDoc, outputRtfPath, rtfSaveOptions);
```
```

#### Enregistrer en DOCM
DOCM est le format Word avec macros ; utilisez `SaveAsDocm` lorsque vous devez conserver les capacités de macro.  
```csharp
// Placeholder for DOCM save code – keep unchanged
```csharp
string outputDocmPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.docm");
WordProcessingSaveOptions docmSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm);
using (FileStream outputStream = File.Create(outputDocmPath))
{
    editor.Save(editedDoc, outputStream, docmSaveOptions);
}
```
```

#### Enregistrer en texte brut
Pour une sortie légère, `SaveAsTxt` supprime la mise en forme et renvoie du texte pur.  
```csharp
// Placeholder for TXT save code – keep unchanged
```csharp
string outputTxtPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.txt");
TextSaveOptions textSaveOptions = new TextSaveOptions
{
    Encoding = System.Text.Encoding.UTF8,
    PreserveTableLayout = true
};
editor.Save(editedDoc, outputTxtPath, textSaveOptions);
```
```

### Étape 4 : Nettoyage
Disposez toujours des instances `EditableDocument` et `Editor` afin de libérer les poignées de fichiers et les ressources non gérées.

Le pattern `Dispose` garantit que les fichiers temporaires sont supprimés et que la mémoire est récupérée.  
```csharp
// Placeholder for cleanup code – keep unchanged
```csharp
editedDoc.Dispose();
defaultWordProcessingDoc.Dispose();
editor.Dispose();
```
```

## Problèmes courants et solutions
| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| **Texte non remplacé** | Le HTML peut contenir des caractères encodés (`&nbsp;`, `<span>`). | Utilisez `HtmlAgilityPack` pour localiser le nœud exact avant de remplacer. |
| **Fichier enregistré corrompu** | Le flux de sortie n’est pas flushé avant la libération. | Appelez `editableDocument.Save(...);` puis `editableDocument.Dispose();`. |
| **Baisse de performance sur de gros fichiers** | Charger tout le HTML d’un document de 300 pages consomme beaucoup de mémoire. | Activez `LoadOptions.UseMemoryMapping = true` pour diffuser des parties du fichier. |
| **Mise en forme perdue lors de l’enregistrement en TXT** | Le format TXT supprime toute mise en forme par conception. | Si vous avez besoin d’une mise en forme basique, envisagez d’enregistrer en RTF à la place. |

## Questions fréquentes

**Q : Quels formats de fichiers GroupDocs.Editor prend‑en charge ?**  
R : GroupDocs.Editor gère plus de 30 formats, dont DOCX, RTF, TXT, HTML, PDF et ODT. Consultez la liste complète dans la documentation officielle.

**Q : Puis‑je essayer GroupDocs.Editor avant d’acheter ?**  
R : Oui, vous pouvez obtenir un essai gratuit [ici](https://releases.groupdocs.com/).

**Q : Existe‑t‑il un support si je rencontre des problèmes ?**  
R : Absolument — visitez le forum de support [ici](https://forum.groupdocs.com/c/editor/20) pour obtenir de l’aide de la communauté et de l’équipe produit.

**Q : Comment obtenir une licence temporaire pour l’évaluation ?**  
R : Demandez une licence temporaire [ici](https://purchase.groupdocs.com/temporary-license/).

**Q : Où puis‑je acheter la version complète de GroupDocs.Editor ?**  
R : Vous pouvez acheter la version complète [ici](https://purchase.groupdocs.com/buy).

---

**Dernière mise à jour :** 2026-05-27  
**Testé avec :** GroupDocs.Editor 2.10 for .NET  
**Auteur :** GroupDocs

## Tutoriels associés

- [Comment modifier et enregistrer des documents Word avec GroupDocs.Editor pour .NET : guide complet](/editor/net/word-processing-documents/editing-word-docs-groupdocs-editor-net/)
- [Convertir Word en HTML avec GroupDocs.Editor .NET : guide étape par étape](/editor/net/document-saving/convert-word-to-html-groupdocs-editor-dotnet/)
- [Édition efficace de documents avec GroupDocs.Editor .NET : transformer HTML en documents éditables](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)