---
date: 2026-06-06
description: Apprenez à **enregistrer chaque onglet Excel** avec GroupDocs.Editor
  pour .NET – guide étape par étape, extraits de code et meilleures pratiques pour
  diviser les fichiers XLSX.
keywords:
- save each excel tab
- read multiple sheets
- convert excel tab pdf
- split xlsx files
linktitle: Travailler avec les feuilles de calcul à onglets multiples
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to **save each Excel tab** using GroupDocs.Editor for .NET
    – step‑by‑step guide, code snippets, and best practices for splitting XLSX files.
  headline: How to save each Excel tab with GroupDocs.Editor .NET
  type: TechArticle
- description: Learn how to **save each Excel tab** using GroupDocs.Editor for .NET
    – step‑by‑step guide, code snippets, and best practices for splitting XLSX files.
  name: How to save each Excel tab with GroupDocs.Editor .NET
  steps:
  - name: Get a Path to the Input File
    text: First, specify the full path to the source XLSX that contains multiple tabs.
  - name: Load the Spreadsheet into the Editor Instance
    text: The `Editor` class is the entry point for all document operations in GroupDocs.Editor.
      It reads the file stream and prepares the document for editing or extraction.
  - name: Create an EditableDocument from the First Tab
    text: '`EditableDocument` represents a single, editable sheet within the workbook.
      The constructor takes the `Editor` instance and a zero‑based sheet index.'
  - name: Create an EditableDocument from the Second Tab
    text: You can repeat the same pattern for any additional sheet by changing the
      index value.
  - name: Save the First Tab to a Separate Document
    text: '`Save` writes the edited document to a file in the specified format. Call
      it on the `EditableDocument` instance, providing the output path and format
      (e.g., `SaveFormat.Xlsx`).'
  - name: Save the Second Tab to a Separate Document
    text: The same `Save` call works for the second sheet, and you can choose a different
      format such as PDF if needed.
  - name: Dispose of EditableDocument Instances
    text: '`Dispose` releases unmanaged resources held by the document, such as file
      handles, ensuring no leaks in long‑running services.'
  type: HowTo
- questions:
  - answer: Hidden sheets are treated like any other sheet; you can access them by
      index and save them, but you may need to set `EditableDocument.IsVisible = true`
      before saving if you want them visible in the output.
    question: What if my workbook contains hidden sheets?
  - answer: Yes, specify `SaveFormat.Pdf` when calling `Save` on the `EditableDocument`.
      The library preserves layout, images, and charts during conversion.
    question: Can I convert an Excel tab directly to PDF?
  - answer: Absolutely. Use `SaveFormat.Csv` for each `EditableDocument` to generate
      plain‑text CSV representations of each sheet.
    question: Is it possible to split a workbook into CSV files instead of XLSX?
  - answer: It does. Provide the password via `LoadOptions.Password` when creating
      the `Editor` instance.
    question: Does GroupDocs.Editor support password‑protected Excel files?
  - answer: The official documentation and sample projects on the [download page](https://releases.groupdocs.com/editor/net/)
      contain additional use‑cases.
    question: Where can I find more examples of working with spreadsheets?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Comment enregistrer chaque onglet Excel avec GroupDocs.Editor .NET
type: docs
url: /fr/net/document-processing/work-multi-tab-spreadsheets/
weight: 17
---

# Travailler avec des feuilles de calcul à onglets multiples

## Introduction
Si vous devez **save each Excel tab** en tant que fichier indépendant, GroupDocs.Editor for .NET rend cela simple. Que vous extrayiez des rapports financiers, génériez des feuilles de travail par département, ou convertissiez des onglets en PDF, ce tutoriel vous guide à travers l’ensemble du flux de travail — de la configuration de l’environnement à la libération des ressources — afin que vous puissiez automatiser la gestion multi‑feuilles avec confiance.

## Réponses rapides
- **GroupDocs.Editor peut‑il diviser un XLSX en fichiers séparés ?** Oui, vous pouvez charger le classeur et exporter chaque feuille individuellement.  
- **Dans quels formats chaque onglet peut‑il être enregistré ?** XLSX, CSV, PDF, HTML, et plus – plus de 30 formats de sortie sont pris en charge.  
- **Ai‑je besoin d’une licence pour cette fonctionnalité ?** Une licence temporaire suffit pour les tests ; une licence complète est requise pour la production.  
- **.NET Core est‑il pris en charge ?** Absolument – la bibliothèque fonctionne avec .NET Framework 4.0+ et .NET Core/5/6+.  
- **Combien d’onglets peuvent être traités simultanément ?** GroupDocs.Editor peut gérer des classeurs contenant plus de 500 feuilles sans charger le fichier complet en mémoire.

## Qu’est‑ce que “save each excel tab” ?
**“Save each Excel tab”** signifie extraire chaque feuille de calcul d’un classeur à plusieurs onglets et écrire chacune dans son propre document autonome (par ex., fichiers XLSX ou PDF séparés). Cette approche simplifie le traitement en aval, le reporting et la distribution en vous fournissant un fichier par feuille, qui peut ensuite être partagé, archivé ou transformé indépendamment.

## Pourquoi utiliser GroupDocs.Editor pour cette tâche ?
GroupDocs.Editor prend en charge **30+ formats d’entrée et de sortie** et peut traiter des feuilles de calcul avec **jusqu’à 1 000 feuilles** tout en maintenant une faible consommation de mémoire grâce au streaming des données plutôt qu’au chargement complet du fichier. L’API préserve également les styles de cellules, les formules et les images intégrées, garantissant que chaque onglet exporté ressemble exactement à l’original.

## Prérequis
Avant de commencer, assurez‑vous d’avoir :

1. **Visual Studio** – toute édition récente (Community, Professional ou Enterprise).  
2. **.NET Framework 4.0+** – ou .NET Core/5/6 si vous préférez le runtime multiplateforme.  
3. **GroupDocs.Editor for .NET** – téléchargez‑le depuis la [download page](https://releases.groupdocs.com/editor/net/).  
4. **License** – une [temporary license](https://purchase.groupdocs.com/temporary-license/) convient pour les tests ; achetez une licence complète pour la production.  
5. **Free trial** – vous pouvez également essayer la bibliothèque via la page [free trial](https://releases.groupdocs.com/).  
6. **Support** – si vous rencontrez des problèmes, visitez le [support forum](https://forum.groupdocs.com/c/editor/20) ou consultez la [purchase page](https://purchase.groupdocs.com/buy) pour une licence complète.

## Importer les espaces de noms
Avant de commencer à coder, vous devez importer les espaces de noms nécessaires. Ajoutez les directives using suivantes en haut de votre fichier `.cs` :

```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```

## Comment enregistrer chaque onglet Excel en tant que fichier séparé ?
Chargez le classeur, créez un `EditableDocument` pour chaque feuille, puis appelez `Save` avec le format souhaité. Ce processus isole chaque onglet, vous permet de choisir un chemin de sortie distinct et libère automatiquement les ressources. Vous trouverez ci‑dessous le flux de travail étape par étape, avec des explications pour chaque appel d’API et des conseils de bonnes pratiques pour éviter les pièges courants.

### Étape 1 : Obtenir le chemin du fichier d’entrée
Tout d’abord, spécifiez le chemin complet du fichier XLSX source contenant plusieurs onglets.

```csharp
string inputFilePath = "Your Sample Document";
```

### Étape 2 : Charger la feuille de calcul dans l’instance Editor
La classe `Editor` est le point d’entrée pour toutes les opérations de document dans GroupDocs.Editor. Elle lit le flux du fichier et prépare le document pour l’édition ou l’extraction.

```csharp
using (FileStream inputStream = File.OpenRead(inputFilePath))
{
    using (Editor editor = new Editor(delegate { return inputStream; }, delegate { return new SpreadsheetLoadOptions(); }))
    {
        // Further steps will go here
    }
}
```

### Étape 3 : Créer un EditableDocument à partir du premier onglet
`EditableDocument` représente une seule feuille éditable du classeur. Le constructeur prend l’instance `Editor` et un indice de feuille basé sur zéro.

```csharp
SpreadsheetEditOptions editOptions1 = new SpreadsheetEditOptions();
editOptions1.WorksheetIndex = 0; // First tab
EditableDocument firstTabBeforeEdit = editor.Edit(editOptions1);
```

### Étape 4 : Créer un EditableDocument à partir du deuxième onglet
Vous pouvez répéter le même schéma pour toute feuille supplémentaire en modifiant la valeur de l’indice.

```csharp
SpreadsheetEditOptions editOptions2 = new SpreadsheetEditOptions();
editOptions2.WorksheetIndex = 1; // Second tab
EditableDocument secondTabBeforeEdit = editor.Edit(editOptions2);
```

### Étape 5 : Enregistrer le premier onglet dans un document séparé
`Save` écrit le document édité dans un fichier au format spécifié. Appelez‑le sur l’instance `EditableDocument`, en fournissant le chemin de sortie et le format (par ex., `SaveFormat.Xlsx`).

```csharp
SpreadsheetSaveOptions saveOptions1 = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
string outputFilename1 = Path.GetFileNameWithoutExtension(inputFilePath) + "_tab1.xlsm";
string outputPath1 = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename1);
editor.Save(firstTabBeforeEdit, outputPath1, saveOptions1);
```

### Étape 6 : Enregistrer le deuxième onglet dans un document séparé
Le même appel `Save` fonctionne pour la deuxième feuille, et vous pouvez choisir un format différent tel que PDF si nécessaire.

```csharp
SpreadsheetSaveOptions saveOptions2 = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsb);
string outputFilename2 = Path.GetFileNameWithoutExtension(inputFilePath) + "_tab2.xlsb";
string outputPath2 = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename2);
editor.Save(secondTabBeforeEdit, outputPath2, saveOptions2);
```

### Étape 7 : Libérer les instances EditableDocument
`Dispose` libère les ressources non gérées détenues par le document, comme les handles de fichier, garantissant l’absence de fuites dans les services à long terme.

```csharp
firstTabBeforeEdit.Dispose();
secondTabBeforeEdit.Dispose();
```

## Problèmes courants et solutions
- **“File is locked” errors** – Assurez‑vous d’appeler `Dispose()` sur chaque `EditableDocument` et sur l’instance `Editor`, ou encapsulez‑les dans des instructions `using`.  
- **Missing styles after export** – Vérifiez que vous enregistrez dans un format qui prend en charge le style (par ex., XLSX ou PDF). CSV perdra le formatage par conception.  
- **Large workbooks cause slow performance** – Utilisez les options de chargement en streaming (`LoadOptions.Streaming = true`) pour maintenir une faible consommation de mémoire.

## Questions fréquentes

**Q : Que se passe‑t‑il si mon classeur contient des feuilles masquées ?**  
R : Les feuilles masquées sont traitées comme n’importe quelle autre feuille ; vous pouvez y accéder par indice et les enregistrer, mais il peut être nécessaire de définir `EditableDocument.IsVisible = true` avant l’enregistrement si vous souhaitez qu’elles soient visibles dans le résultat.

**Q : Puis‑je convertir directement un onglet Excel en PDF ?**  
R : Oui, spécifiez `SaveFormat.Pdf` lors de l’appel à `Save` sur le `EditableDocument`. La bibliothèque préserve la mise en page, les images et les graphiques pendant la conversion.

**Q : Est‑il possible de diviser un classeur en fichiers CSV au lieu de XLSX ?**  
R : Absolument. Utilisez `SaveFormat.Csv` pour chaque `EditableDocument` afin de générer des représentations CSV en texte brut de chaque feuille.

**Q : GroupDocs.Editor prend‑il en charge les fichiers Excel protégés par mot de passe ?**  
R : Oui. Fournissez le mot de passe via `LoadOptions.Password` lors de la création de l’instance `Editor`.

**Q : Où puis‑je trouver plus d’exemples de travail avec les feuilles de calcul ?**  
R : La documentation officielle et les projets d’exemple sur la [download page](https://releases.groupdocs.com/editor/net/) contiennent des cas d’utilisation supplémentaires.

## Conclusion
En suivant ces étapes, vous pouvez **save each Excel tab** en tant que document indépendant, convertir des onglets en PDF ou diviser de grands classeurs en morceaux gérables — le tout avec la bibliothèque fiable et haute performance GroupDocs.Editor for .NET. Cette capacité rationalise les pipelines de reporting, automatise l’extraction de données et réduit la manipulation manuelle des feuilles de calcul.

---

**Dernière mise à jour :** 2026-06-06  
**Testé avec :** GroupDocs.Editor 23.11 for .NET  
**Auteur :** GroupDocs  

## Tutoriels associés

- [Maîtriser l'extraction d'onglets de feuille de calcul en .NET avec GroupDocs.Editor](/editor/net/spreadsheet-documents/mastering-spreadsheet-tab-extraction-dotnet-groupdocs-editor/)
- [Protéger par mot de passe les fichiers Excel avec GroupDocs.Editor pour .NET | Gestion sécurisée des feuilles de calcul](/editor/net/spreadsheet-documents/groupdocs-editor-net-password-excel-files/)
- [Maîtriser le chargement de documents en .NET avec GroupDocs.Editor : guide complet](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)