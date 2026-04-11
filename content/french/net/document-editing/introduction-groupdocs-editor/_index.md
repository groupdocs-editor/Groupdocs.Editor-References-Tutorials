---
date: 2026-04-11
description: Apprenez à modifier programmétiquement un document Word en utilisant
  GroupDocs.Editor pour .NET et à convertir un document Word en RTF grâce à ce guide
  détaillé étape par étape.
keywords:
- programmatically edit word document
- convert pdf to editable
- replace text in document
- convert word to rtf
- save document to stream
linktitle: Modifier un document Word par programmation avec GroupDocs.Editor pour
  .NET
second_title: GroupDocs.Editor .NET API
title: Modifier un document Word de façon programmatique avec GroupDocs.Editor pour
  .NET
type: docs
url: /fr/net/document-editing/introduction-groupdocs-editor/
weight: 12
---

# Modifier un document Word de façon programmatique avec GroupDocs.Editor pour .NET

Si vous êtes développeur .NET et que vous devez **modifier programmatique un document Word** — que ce soit pour remplacer du texte, convertir des formats ou intégrer le résultat dans un flux — GroupDocs.Editor pour .NET est une bibliothèque robuste et facile à utiliser qui fait le travail. Dans ce tutoriel, nous parcourrons un exemple concret qui couvre le chargement d'un fichier DOCX, la modification de son contenu, la conversion du résultat en RTF et l'enregistrement soit sur le disque, soit dans un flux mémoire.

## Réponses rapides
- **Que puis‑je modifier ?** Word, PDF, HTML, RTF et de nombreux autres formats.  
- **Puis‑je remplacer du texte ?** Oui – utilisez un remplacement de chaîne simple ou une manipulation DOM plus avancée.  
- **Comment convertir un PDF en éditable ?** Chargez le PDF avec `Editor` et modifiez le HTML généré.  
- **Quelle est la façon la plus simple d’enregistrer dans un flux ?** Use `editor.Save(editableDoc, stream, options)`.  
- **Ai‑je besoin d’une licence ?** Une licence temporaire ou complète est requise pour une utilisation en production.

## Qu’est‑ce que la modification programmatique d’un document Word ?
Modifier programmatique un document Word signifie utiliser du code — plutôt qu’une interface utilisateur — pour ouvrir un fichier, modifier son contenu (texte, images, styles) et écrire la version modifiée dans le stockage. Cette approche alimente les rapports automatisés, les mises à jour massives de documents et la génération de contenu personnalisé.

## Pourquoi utiliser GroupDocs.Editor pour .NET ?
- **Flexibilité de format :** Load DOCX, PDF, HTML, RTF, etc., and save to any supported format.  
- **Pas de dépendance à Office :** Works without Microsoft Office installed on the server.  
- **Compatible avec les flux :** Perfect for cloud scenarios where you read/write from streams instead of the file system.  
- **API riche :** Access to images, fonts, CSS, and other resources for full‑featured editing.

## Prérequis
Avant de plonger dans l’implémentation, assurez‑vous d’avoir :
- Visual Studio 2017 ou version ultérieure.  
- .NET Framework 4.6.1 ou version ultérieure.  
- GroupDocs.Editor for .NET – you can [télécharger](https://releases.groupdocs.com/editor/net/) it from the site.  
- A valid license or a [licence temporaire](https://purchase.groupdocs.com/temporary-license/) from GroupDocs.

## Importer les espaces de noms
Pour commencer à utiliser GroupDocs.Editor pour .NET, importez les espaces de noms requis :

```csharp
using System;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```

Dans les sections suivantes, nous décomposerons le flux de travail en étapes faciles à suivre.

## Étape 1 : Obtenir le chemin du fichier d’entrée
Spécifiez l’emplacement du fichier Word que vous souhaitez modifier. Pour cet exemple, nous supposerons un DOCX nommé **Your Sample Document.docx**.

```csharp
string inputFilePath = "Your Sample Document.docx";
```

## Étape 2 : Instancier l’objet Editor
Créez une instance `Editor` en passant le chemin d’entrée. Cela charge le document et le prépare à l’édition.

```csharp
using (GroupDocs.Editor.Editor editor = new Editor(inputFilePath))
{
    // Subsequent steps will be nested inside this block
}
```

## Étape 3 : Ouvrir le document pour l’édition
Obtenez un `EditableDocument` qui vous donne accès à la représentation HTML du document et à ses ressources.

```csharp
EditableDocument beforeEdit = editor.Edit();
```

## Étape 4 : Récupérer le contenu et les ressources du document
Vous pouvez extraire le HTML brut, les images, les polices et le CSS. Ceci est utile lorsque vous devez manipuler directement le balisage.

```csharp
string content = beforeEdit.GetContent();
var images = beforeEdit.Images;
var fonts = beforeEdit.Fonts;
var stylesheets = beforeEdit.Css;
```

### Étape 4.1 : Obtenir le document sous forme d’une chaîne Base64 unique
Si vous préférez une chaîne unique contenant toutes les ressources intégrées, appelez `GetEmbeddedHtml()`.

```csharp
string allEmbeddedInsideString = beforeEdit.GetEmbeddedHtml();
```

### Étape 4.2 : Modifier le contenu
Remplaçons le mot **Subtitle** par **Edited subtitle** pour démontrer un remplacement de texte simple.

```csharp
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
```

## Étape 5 : Créer une nouvelle instance EditableDocument
Après avoir modifié le balisage, encapsulez-le à nouveau dans un objet `EditableDocument`.

```csharp
EditableDocument afterEdit = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```

## Étape 6 : Enregistrer le document modifié
Nous enregistrerons le résultat sous forme de fichier RTF, en montrant à la fois un chemin système de fichiers et une option de flux mémoire.

### Étape 6.1 : Préparer le chemin de sortie
Définissez où le RTF doit être écrit.

```csharp
string outputPath = Path.Combine("Output Directory Path", Path.GetFileNameWithoutExtension(inputFilePath) + ".rtf");
```

### Étape 6.2 : Préparer les options d’enregistrement
Sélectionnez le format RTF via `WordProcessingSaveOptions`.

```csharp
Options.WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
```

### Étape 6.3 : Enregistrer sur le chemin
Écrivez le document modifié sur le système de fichiers.

```csharp
editor.Save(afterEdit, outputPath, saveOptions);
```

### Étape 6.4 : Enregistrer dans un flux
Si vous avez besoin du résultat en mémoire (par ex., pour le télécharger vers un stockage cloud), utilisez un `MemoryStream`.

```csharp
using (MemoryStream ms = new MemoryStream())
{
    editor.Save(afterEdit, ms, saveOptions);
}
```

## Étape 7 : Libérer les instances Editor et EditableDocument
Libérez les ressources rapidement pour éviter les fuites de mémoire.

```csharp
beforeEdit.Dispose();
afterEdit.Dispose();
editor.Dispose();
```

## Cas d’utilisation courants & astuces
- **Convertir PDF en éditable :** Load a PDF with `Editor`, edit the generated HTML, then save back to PDF or another format.  
- **Remplacer du texte dans le document :** Use `string.Replace` for simple cases or manipulate the DOM for complex scenarios.  
- **Convertir Word en RTF :** As shown above, set `WordProcessingFormats.Rtf` in the save options.  
- **Enregistrer le document dans un flux :** Ideal for web APIs that return files directly to the client.  
- **Charger le document pour l’édition :** Always wrap the `Editor` in a `using` block to ensure proper disposal.

## Questions fréquemment posées

**Q : Puis‑je modifier des fichiers PDF avec GroupDocs.Editor pour .NET ?**  
A : Oui, GroupDocs.Editor prend en charge la modification des PDF en les convertissant en une représentation HTML intermédiaire.

**Q : Comment obtenir une licence temporaire pour GroupDocs.Editor pour .NET ?**  
A : Vous pouvez obtenir une licence temporaire depuis le [site GroupDocs](https://purchase.groupdocs.com/temporary-license/).

**Q : Quels formats de fichiers sont pris en charge par GroupDocs.Editor pour .NET ?**  
A : DOCX, PDF, HTML, RTF, et de nombreux autres formats sont pris en charge.

**Q : Est‑il possible d’intégrer GroupDocs.Editor avec le stockage cloud ?**  
A : Absolument – vous pouvez lire/écrire des flux depuis Azure Blob, Amazon S3, Google Cloud Storage, etc.

**Q : Où puis‑je trouver la documentation de GroupDocs.Editor pour .NET ?**  
A : La documentation est disponible [ici](https://tutorials.groupdocs.com/editor/net/).

---

**Dernière mise à jour** : 2026-04-11  
**Testé avec** : GroupDocs.Editor 23.12 for .NET  
**Auteur** : GroupDocs