---
title: Travailler avec des valeurs séparées délimitées (DSV)
linktitle: Travailler avec des valeurs séparées délimitées (DSV)
second_title: API GroupDocs.Editor .NET
description: Découvrez comment modifier des fichiers CSV et TSV à l'aide de GroupDocs.Editor for .NET avec ce guide étape par étape. Améliorez vos projets .NET sans effort.
weight: 12
url: /fr/net/document-processing/work-dsv/
---
## Introduction
Si vous êtes un développeur travaillant avec des valeurs séparées délimitées (DSV) telles que des fichiers CSV ou TSV, vous savez que la modification de ces fichiers par programmation peut être une tâche ardue. Cependant, avec GroupDocs.Editor pour .NET, cette tâche devient nettement plus simple et plus efficace. Dans ce didacticiel, nous vous expliquerons comment utiliser GroupDocs.Editor for .NET pour lire, modifier et enregistrer des fichiers DSV. Nous décomposerons le processus en étapes faciles à suivre, ce qui facilitera votre mise en œuvre dans vos projets.
## Conditions préalables
Avant de plonger dans le didacticiel, assurez-vous de disposer des prérequis suivants :
- Visual Studio : assurez-vous que Visual Studio est installé sur votre ordinateur.
-  GroupDocs.Editor pour .NET : vous devrez télécharger et référencer la bibliothèque GroupDocs.Editor pour .NET. Vous pouvez le télécharger[ici](https://releases.groupdocs.com/editor/net/).
- Compréhension de base de C# : ce didacticiel suppose que vous possédez une compréhension de base du développement C# et .NET.
## Importer des espaces de noms
Tout d’abord, vous devez importer les espaces de noms nécessaires dans votre projet. Ces espaces de noms fournissent les classes et méthodes requises pour travailler avec GroupDocs.Editor for .NET.
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

## Étape 1 : obtenir un chemin d'accès au fichier DSV d'entrée
Tout d’abord, vous devez spécifier le chemin d’accès au fichier DSV d’entrée. Pour cet exemple, nous supposerons qu'il s'agit d'un fichier CSV.
```csharp
string inputFilePath = "Your Sample Document";
```
## Étape 2 : Créer une instance d'éditeur
 Créez une instance du`Editor` classe. Cette instance sera utilisée pour charger et manipuler le fichier DSV.
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## Étape 3 : Créer des options de modification DSV
 Ensuite, créez une instance de`DelimitedTextEditOptions` et spécifiez le délimiteur du fichier DSV. Ici, nous utilisons une virgule comme délimiteur.
```csharp
    Options.DelimitedTextEditOptions editOptions = new DelimitedTextEditOptions(",");
    editOptions.ConvertDateTimeData = false;
    editOptions.ConvertNumericData = true;
    editOptions.TreatConsecutiveDelimitersAsOne = true;
```
## Étape 4 : Créer une instance EditableDocument
 Créé un`EditableDocument` exemple en utilisant le`Editor.Edit` méthode. Cela prépare le document pour l'édition.
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## Étape 5 : Modifier le contenu du document
Récupérez le contenu du texte original et apportez les modifications nécessaires. À des fins de démonstration, remplaçons du texte.
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("SsangYong", "Chevrolet").Replace("Kyron", "Camaro");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## Étape 6 : Créer un document modifiable avec un contenu mis à jour
 Créer un nouveau`EditableDocument` avec le contenu mis à jour.
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## Étape 7 : Créer des options d'enregistrement CSV
Spécifiez les options d'enregistrement pour le format CSV, y compris le délimiteur et l'encodage.
```csharp
    Options.DelimitedTextSaveOptions csvSaveOptions = new DelimitedTextSaveOptions(",");
    csvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## Étape 8 : Créer des options de sauvegarde TSV
De même, spécifiez les options de sauvegarde pour le format TSV.
```csharp
    Options.DelimitedTextSaveOptions tsvSaveOptions = new DelimitedTextSaveOptions("\t");
    tsvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## Étape 9 : Créer des options d'enregistrement dans une feuille de calcul
Si vous devez enregistrer le document sous forme de feuille de calcul, créez les options d'enregistrement correspondantes.
```csharp
    Options.SpreadsheetSaveOptions cellsSaveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
```
## Étape 10 : Préparer les chemins de sauvegarde
Définissez les chemins où les fichiers modifiés seront enregistrés.
```csharp
    string outputCsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".csv");
    string outputTsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".tsv");
    string outputCellsPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".xlsm");
```
## Étape 11 : Enregistrez le document modifié
Enregistrez le document modifié dans les chemins spécifiés dans différents formats.
```csharp
    editor.Save(afterEdit, outputCsvPath, csvSaveOptions);
    editor.Save(afterEdit, outputTsvPath, tsvSaveOptions);
    editor.Save(afterEdit, outputCellsPath, cellsSaveOptions);
```
## Étape 12 : Supprimer les instances EditableDocument
 Enfin, assurez-vous de jeter le`EditableDocument` instances pour libérer des ressources.
```csharp
    beforeEdit.Dispose();
    afterEdit.Dispose();
}
System.Console.WriteLine("WorkingWithDsv routine has successfully finished");
```
## Conclusion
La modification de fichiers DSV à l'aide de GroupDocs.Editor pour .NET est un processus simple qui implique la création d'une instance d'éditeur, la définition des options d'édition, la modification du contenu et l'enregistrement des modifications. Ce guide étape par étape devrait vous aider à intégrer facilement cette fonctionnalité dans vos applications .NET. Que vous travailliez avec CSV, TSV ou d'autres formats DSV, GroupDocs.Editor for .NET fournit une solution robuste et flexible.
## FAQ
### Puis-je utiliser GroupDocs.Editor pour .NET pour modifier des fichiers CSV volumineux ?
Oui, GroupDocs.Editor pour .NET est capable de gérer efficacement des fichiers CSV volumineux.
### GroupDocs.Editor pour .NET prend-il en charge d'autres formats DSV que CSV et TSV ?
Oui, il prend en charge différents formats DSV à condition que vous spécifiiez le délimiteur approprié.
### Est-il possible de personnaliser l'encodage lors de l'enregistrement des fichiers DSV ?
Absolument, vous pouvez préciser l'encodage souhaité dans les options de sauvegarde.
### Puis-je convertir un fichier CSV en feuille de calcul Excel à l'aide de GroupDocs.Editor for .NET ?
Oui, vous pouvez enregistrer un fichier CSV sous forme de feuille de calcul Excel en utilisant les options d'enregistrement appropriées.
### Où puis-je trouver plus de documentation sur GroupDocs.Editor pour .NET ?
 Vous pouvez trouver une documentation détaillée[ici](https://tutorials.groupdocs.com/editor/net/)