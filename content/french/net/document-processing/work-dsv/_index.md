---
date: 2026-06-06
description: Apprenez comment **créer des documents modifiables** à partir de fichiers
  CSV et TSV en utilisant GroupDocs.Editor pour .NET. Ce guide montre également comment
  **lire du texte délimité en C#** et **modifier des CSV avec .NET** efficacement
  dans Visual Studio.
keywords:
- create editable document
- read delimited text c#
- edit csv .net
- parse delimited values c#
linktitle: Travailler avec les valeurs séparées par délimiteur (DSV) – créer un document
  modifiable
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to **create editable document** objects from CSV and TSV
    files using GroupDocs.Editor for .NET. This guide also shows how to **read delimited
    text C#** and **edit CSV .NET** efficiently in Visual Studio.
  headline: Work with Delimited Separated Values (DSV) – create editable document
  type: TechArticle
- questions:
  - answer: Yes, the API streams data and can handle files larger than 1 GB without
      loading the entire document into memory.
    question: Can I use GroupDocs.Editor for .NET to edit large CSV files?
  - answer: Absolutely – any single‑character delimiter (e.g., pipe `|`, semicolon
      `;`) is supported as long as you specify it in `DelimitedTextEditOptions`.
    question: Does GroupDocs.Editor for .NET support other DSV formats besides CSV
      and TSV?
  - answer: Yes, you can set the `Encoding` property in `DelimitedTextSaveOptions`
      to UTF‑8, UTF‑16, ISO‑8859‑1, or any .NET `Encoding` you require.
    question: Is it possible to customize the encoding when saving DSV files?
  - answer: Yes – after editing, simply use `SpreadsheetSaveOptions` to export the
      content as an `.xlsx` workbook.
    question: Can I convert a CSV file to an Excel spreadsheet using GroupDocs.Editor
      for .NET?
  - answer: Detailed API references and code samples are available **[here](https://tutorials.groupdocs.com/editor/net/)**.
    question: Where can I find more documentation on GroupDocs.Editor for .NET?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Travailler avec les valeurs séparées par délimiteur (DSV) – créer un document
  modifiable
type: docs
url: /fr/net/document-processing/work-dsv/
weight: 12
---

# Travailler avec des valeurs séparées par des délimiteurs (DSV) – créer un document modifiable

Si vous êtes un développeur .NET qui doit **create editable document** des objets à partir de valeurs séparées par des délimiteurs (DSV) telles que CSV ou TSV, vous êtes au bon endroit. Dans les 100 premiers mots, nous expliquerons pourquoi GroupDocs.Editor pour .NET est la façon la plus fiable de **read delimited text C#**, le modifier, puis le sauvegarder sans perdre le formatage. Vous repartirez avec un flux de travail complet, prêt à copier‑coller, qui s’intègre naturellement à n’importe quelle solution Visual Studio.

## Réponses rapides
- **Quelle bibliothèque gère le mieux l'édition CSV en .NET ?** GroupDocs.Editor for .NET.
- **Puis-je éditer de gros fichiers CSV dans Visual Studio ?** Oui – l’API diffuse les données et évite de charger le fichier complet en mémoire.
- **Ai-je besoin d’une licence pour une utilisation en production ?** Une licence commerciale est requise ; un essai gratuit est disponible.
- **Quels formats puis‑je exporter après l'édition ?** CSV, TSV et formats de feuilles de calcul compatibles Excel.
- **L'API est‑elle compatible avec .NET 6+ ?** Absolument – elle prend en charge .NET Framework 4.5+, .NET Core 3.1+, .NET 5 et .NET 6.

## Qu’est‑ce que « create editable document » dans le contexte de GroupDocs.Editor ?
**Create editable document** signifie générer une instance `EditableDocument` qui représente une version mutable d’un fichier source (CSV, TSV, etc.) en mémoire. Cet objet vous permet de lire, modifier et ré‑enregistrer le contenu en utilisant la même API. Il fournit des méthodes pour récupérer le texte du document, appliquer des modifications et le sauvegarder dans divers formats, en veillant à ce que l’alignement des colonnes et les guillemets soient conservés.

## Pourquoi utiliser GroupDocs.Editor pour la gestion des DSV ?
GroupDocs.Editor traite **plus de 50 formats d’entrée et de sortie**, y compris CSV, TSV et les feuilles de calcul compatibles Excel, tout en maintenant l’utilisation de la mémoire sous 10 Mo pour des fichiers allant jusqu’à 500 Mo. Il préserve également l’alignement des colonnes, les règles de guillemets et les encodages personnalisés automatiquement, ce qui élimine le besoin d’une logique d’analyse manuelle.

## Prérequis
Avant de commencer, assurez-vous d’avoir les éléments suivants installés :

- **Visual Studio** (toute édition récente) – vous développerez et déboguerez directement dans l’IDE.
- **GroupDocs.Editor for .NET** – téléchargez le dernier package **[ici](https://releases.groupdocs.com/editor/net/)**.
- **Connaissances de base en C#** – le tutoriel suppose que vous pouvez créer un projet console ou ASP.NET et ajouter des packages NuGet.

## Importer les espaces de noms
Les classes `Editor`, `EditableDocument` et les classes d’options se trouvent dans l’espace de noms `GroupDocs.Editor`.  

La classe `DelimitedTextEditOptions` est le point d’entrée pour définir le délimiteur (virgule, tabulation, etc.) et d’autres règles d’analyse.

```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

## Comment créer un document modifiable à partir d’un fichier CSV ?
Chargez le CSV source avec `Editor` et appelez la méthode `Edit`, en passant une instance `DelimitedTextEditOptions` qui spécifie un délimiteur virgule. La méthode renvoie un `EditableDocument` que vous pouvez manipuler en mémoire. Ce modèle en deux étapes—chargement → édition—couvre les scénarios **read delimited text C#** et garantit que la structure du fichier original est conservée.

## Étape 1 : Obtenir le chemin du fichier DSV d’entrée
Tout d’abord, vous devez spécifier le chemin absolu ou relatif du fichier DSV source. Pour la démonstration, nous utiliserons un simple CSV situé dans le dossier `Data` du projet.

```csharp
string inputFilePath = "Your Sample Document";
```

## Étape 2 : Créer une instance Editor
`Editor` est la classe principale qui orchestre le chargement, l’édition et la sauvegarde. L’instancier avec un objet `FileInfo` vous donne un contrôle complet sur le cycle de vie du fichier.

```csharp
using (Editor editor = new Editor(inputFilePath))
{
```

## Étape 3 : Créer les options d’édition DSV
`DelimitedTextEditOptions` indique à l’éditeur comment interpréter le fichier. Vous pouvez définir le délimiteur, si la première ligne contient des en‑têtes, et l’encodage des caractères.

```csharp
    Options.DelimitedTextEditOptions editOptions = new DelimitedTextEditOptions(",");
    editOptions.ConvertDateTimeData = false;
    editOptions.ConvertNumericData = true;
    editOptions.TreatConsecutiveDelimitersAsOne = true;
```

## Étape 4 : Créer une instance EditableDocument
`EditableDocument` représente une version mutable en mémoire du fichier source. Appeler `Editor.Edit` avec les options renvoie un `EditableDocument`. Cet objet contient le texte du fichier dans une chaîne mutable, prête pour toute opération **parse delimited values C#** dont vous avez besoin.

```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```

## Étape 5 : Modifier le contenu du document
`GetDocumentText()` renvoie le texte actuel du document modifiable sous forme de chaîne. Récupérez le texte original via `EditableDocument.GetDocumentText()`, effectuez vos modifications (par ex., remplacer la valeur d’une colonne), et stockez le résultat dans une nouvelle chaîne. C’est ici que vous **edit CSV .NET** sans toucher aux flux de fichiers de bas niveau.

```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("SsangYong", "Chevrolet").Replace("Kyron", "Camaro");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```

## Étape 6 : Créer un EditableDocument avec le contenu mis à jour
Enveloppez la chaîne modifiée dans un `EditableDocument`. Cette étape finalise les modifications et prépare l’objet à être sauvegardé dans n’importe quel format pris en charge.

```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```

## Étape 7 : Créer les options d’enregistrement CSV
`DelimitedTextSaveOptions` spécifie comment écrire le contenu édité dans un fichier CSV. Lorsque vous êtes prêt à enregistrer les modifications, configurez `DelimitedTextSaveOptions`. Vous pouvez spécifier le même délimiteur, un différent, ou même changer le style de fin de ligne.

```csharp
    Options.DelimitedTextSaveOptions csvSaveOptions = new DelimitedTextSaveOptions(",");
    csvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

## Étape 8 : Créer les options d’enregistrement TSV
Si vous avez besoin d’une version séparée par des tabulations, il suffit de changer le délimiteur en `\t`. Le même `EditableDocument` peut être enregistré plusieurs fois avec des options différentes.

```csharp
    Options.DelimitedTextSaveOptions tsvSaveOptions = new DelimitedTextSaveOptions("\t");
    tsvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

## Étape 9 : Créer les options d’enregistrement de feuille de calcul
`SpreadsheetSaveOptions` configure l’exportation du document vers des formats compatibles Excel comme .xlsx. GroupDocs.Editor vous permet également d’exporter les données éditées vers un format compatible Excel (`.xlsx`). La classe `SpreadsheetSaveOptions` gère automatiquement les types de colonnes, les formules et le style des cellules.

```csharp
    Options.SpreadsheetSaveOptions cellsSaveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
```

## Étape 10 : Préparer les chemins d’enregistrement
Définissez des chemins de sortie distincts pour chaque format. Utiliser des conventions de nommage claires (par ex., `output.csv`, `output.tsv`, `output.xlsx`) aide à garder votre projet organisé.

```csharp
    string outputCsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".csv");
    string outputTsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".tsv");
    string outputCellsPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".xlsm");
```

## Étape 11 : Enregistrer le document édité
`Save()` écrit le document sur le disque en utilisant les options d’enregistrement fournies. Appelez `EditableDocument.Save` avec les options appropriées pour chaque format cible. L’API écrit le fichier directement sur le disque, en conservant l’encodage original sauf si vous le remplacez.

```csharp
    editor.Save(afterEdit, outputCsvPath, csvSaveOptions);
    editor.Save(afterEdit, outputTsvPath, tsvSaveOptions);
    editor.Save(afterEdit, outputCellsPath, cellsSaveOptions);
```

## Étape 12 : Libérer les instances EditableDocument
`Editor` et `EditableDocument` implémentent tous deux `IDisposable`. Les libérer libère les poignées de fichiers et les ressources non gérées, ce qui est crucial lors du traitement de nombreux fichiers dans un travail par lots.

```csharp
    beforeEdit.Dispose();
    afterEdit.Dispose();
}
System.Console.WriteLine("WorkingWithDsv routine has successfully finished");
```

## Problèmes courants et solutions
| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| **Guillemets supplémentaires inattendus** | Le parseur CSV par défaut peut considérer les virgules intégrées comme des délimiteurs. | Définissez `EscapeMode = EscapeMode.DoubleQuote` dans `DelimitedTextEditOptions`. |
| **Pic de mémoire avec un gros fichier** | Chargement d’un fichier de 500 Mo sans diffusion. | Utilisez `Editor.Load` avec `LoadOptions` qui activent le chargement paresseux. |
| **Incompatibilité d’encodage** | Le fichier source utilise UTF‑16 mais les options sont par défaut UTF‑8. | Définissez explicitement `Encoding = Encoding.Unicode` dans les options d’enregistrement. |

## Questions fréquemment posées

**Q : Puis‑je utiliser GroupDocs.Editor pour .NET afin d’éditer de gros fichiers CSV ?**  
R : Oui, l’API diffuse les données et peut gérer des fichiers de plus de 1 Go sans charger le document complet en mémoire.

**Q : GroupDocs.Editor pour .NET prend‑il en charge d’autres formats DSV en plus de CSV et TSV ?**  
R : Absolument – tout délimiteur à caractère unique (par ex., pipe `|`, point‑virgule `;`) est pris en charge tant que vous le spécifiez dans `DelimitedTextEditOptions`.

**Q : Est‑il possible de personnaliser l’encodage lors de l’enregistrement de fichiers DSV ?**  
R : Oui, vous pouvez définir la propriété `Encoding` dans `DelimitedTextSaveOptions` sur UTF‑8, UTF‑16, ISO‑8859‑1, ou tout autre `Encoding` .NET dont vous avez besoin.

**Q : Puis‑je convertir un fichier CSV en feuille de calcul Excel à l’aide de GroupDocs.Editor pour .NET ?**  
R : Oui – après l’édition, utilisez simplement `SpreadsheetSaveOptions` pour exporter le contenu sous forme de classeur `.xlsx`.

**Q : Où puis‑je trouver plus de documentation sur GroupDocs.Editor pour .NET ?**  
R : Des références API détaillées et des exemples de code sont disponibles **[ici](https://tutorials.groupdocs.com/editor/net/)**.

---

**Dernière mise à jour :** 2026-06-06  
**Testé avec :** GroupDocs.Editor 23.10 pour .NET  
**Auteur :** GroupDocs

## Tutoriels associés

- [Tutoriels d’édition de texte brut et de documents DSV pour GroupDocs.Editor .NET](/editor/net/plain-text-dsv-documents/)
- [Maîtriser GroupDocs.Editor .NET pour l’édition efficace de documents CSV et la conversion](/editor/net/plain-text-dsv-documents/groupdocs-editor-net-csv-editing-guide/)
- [Maîtriser le chargement de documents en .NET avec GroupDocs.Editor : guide complet](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)