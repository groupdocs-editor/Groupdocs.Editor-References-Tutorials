---
title: Travailler avec des feuilles de calcul protégées par mot de passe
linktitle: Travailler avec des feuilles de calcul protégées par mot de passe
second_title: API GroupDocs.Editor .NET
description: Découvrez comment gérer des feuilles de calcul protégées par mot de passe à l'aide de GroupDocs.Editor for .NET. Ce guide détaillé vous guide tout au long de l'ouverture pour enregistrer des fichiers Excel sécurisés.
weight: 18
url: /fr/net/document-processing/work-password-protected-spreadsheets/
---

# Travailler avec des feuilles de calcul protégées par mot de passe

## Introduction
Avez-vous du mal à gérer des feuilles de calcul protégées par mot de passe dans vos applications .NET ? Si c'est le cas, vous êtes au bon endroit ! Dans ce guide complet, nous vous guiderons tout au long du processus d'utilisation de GroupDocs.Editor for .NET pour gérer efficacement les feuilles de calcul protégées par mot de passe. À la fin de ce didacticiel, vous serez parfaitement équipé pour ouvrir, modifier et enregistrer facilement des fichiers Excel cryptés.
## Conditions préalables
Avant de plonger dans le code, assurons-nous que vous disposez de tout ce dont vous avez besoin pour suivre :
- Connaissance de base de C# : ce didacticiel suppose que vous êtes familier avec la programmation C#.
- .NET Framework : assurez-vous que le framework .NET est installé sur votre ordinateur de développement.
-  GroupDocs.Editor pour .NET : téléchargez et installez GroupDocs.Editor pour .NET à partir de[ici](https://releases.groupdocs.com/editor/net/).
## Importer des espaces de noms
Pour commencer, vous devrez importer les espaces de noms nécessaires dans votre projet C#. Ces espaces de noms donnent accès aux fonctionnalités de GroupDocs.Editor.
```csharp
using System;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
## Étape 1 : obtenir un chemin d'accès au fichier d'entrée
Tout d’abord, vous aurez besoin d’un chemin d’accès au fichier d’entrée. Pour cet exemple, nous utiliserons un exemple de fichier Excel (`Your Sample Document`) protégé par mot de passe.
```csharp
string inputFilePath = "Your Sample Document";
```
## Étape 2 : Tentative d'ouverture du document sans mot de passe
Voyons ce qui se passe si nous essayons d'ouvrir le document sans fournir de mot de passe.
```csharp
Editor editor = new Editor(inputFilePath);
try
{
    editor.Edit();
}
catch (GroupDocs.Editor.PasswordRequiredException)
{
    Console.WriteLine("Cannot edit the document because it is password-protected. A password is required.");
}
editor.Dispose();
```
## Étape 3 : essayez de spécifier un mot de passe incorrect
Nous allons maintenant spécifier un mot de passe incorrect pour montrer comment l'éditeur répond.
```csharp
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.Password = "incorrect_password";
editor = new Editor(inputFilePath, delegate { return loadOptions; });
try
{
    editor.Edit();
}
catch (GroupDocs.Editor.IncorrectPasswordException)
{
    Console.WriteLine("Cannot edit the document because the specified password is incorrect.");
}
editor.Dispose();
```
## Étape 4 : ouvrez le fichier avec le mot de passe correct
Fournissons le mot de passe correct et ouvrons le fichier avec succès.
```csharp
loadOptions.Password = "excel_password";
loadOptions.OptimizeMemoryUsage = true;
editor = new Editor(inputFilePath, delegate { return loadOptions; });
```
## Étape 5 : Créer et ajuster les options d'édition
Pour modifier la feuille de calcul, nous devons créer et ajuster les options d'édition.
```csharp
SpreadsheetEditOptions editOptions = new SpreadsheetEditOptions();
```
## Étape 6 : Créer un document modifiable intermédiaire
 Ensuite, nous créons un intermédiaire`EditableDocument` cela nous permet d'apporter des modifications à la feuille de calcul.
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
{
    // Étape 7 : Créer des options de sauvegarde
    SpreadsheetFormats xlsmFormat = SpreadsheetFormats.Xlsm;
    SpreadsheetSaveOptions saveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
    // Étape 7.1 : Définir un nouveau mot de passe d'ouverture
    saveOptions.Password = "new password";
    // Étape 7.2 : Définir la protection en écriture
    saveOptions.WorksheetProtection = new WorksheetProtection(WorksheetProtectionType.All, "write password");
    // Étape 8 : Enregistrez le document sans modification
    //Étape 8.1 : Préparer le nom et le chemin du fichier de sortie
    string outputFilename = Path.GetFileNameWithoutExtension(inputFilePath) + "." + xlsmFormat.Extension;
    string outputPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename);
    // Étape 8.2 : Créer un flux de sortie
    using (FileStream outputStream = File.Create(outputPath))
    {
        // Étape 8.3 : Enregistrer
        editor.Save(beforeEdit, outputStream, saveOptions);
    }
}
// Étape 9 : Supprimer l'instance de l'éditeur
editor.Dispose();
Console.WriteLine("Successfully handled the password-protected spreadsheet. Editor instance has been disposed: {0}", editor.IsDisposed ? "Yes" : "No");
```
## Conclusion
Toutes nos félicitations! Vous avez appris avec succès à gérer des feuilles de calcul protégées par mot de passe à l'aide de GroupDocs.Editor for .NET. De la tentative d'ouverture du document sans mot de passe à son enregistrement avec de nouveaux paramètres de protection, vous avez couvert toutes les étapes essentielles. Ces connaissances amélioreront sans aucun doute votre capacité à gérer des documents sécurisés au sein de vos applications .NET.
## FAQ
### Qu’est-ce que GroupDocs.Editor pour .NET ?
GroupDocs.Editor for .NET est une puissante API d'édition de documents qui permet aux développeurs de charger, modifier et enregistrer une variété de formats de documents dans les applications .NET.
### Comment puis-je obtenir une licence temporaire pour GroupDocs.Editor ?
 Vous pouvez obtenir une licence temporaire auprès de[ici](https://purchase.groupdocs.com/temporary-license/) pour évaluer les fonctionnalités du produit.
### Est-il possible d'optimiser l'utilisation de la mémoire lors de l'édition de documents volumineux ?
 Oui, vous pouvez activer l'optimisation de la mémoire en définissant le`OptimizeMemoryUsage` propriété à`true`dans les options de chargement.
### Puis-je définir des mots de passe différents pour ouvrir et écrire dans une feuille de calcul ?
Absolument! Vous pouvez définir des mots de passe distincts pour l'ouverture du document et pour la protection en écriture à l'aide des options d'enregistrement.
### Où puis-je trouver une documentation plus détaillée ?
 Vous pouvez accéder à la documentation complète de GroupDocs.Editor pour .NET[ici](https://tutorials.groupdocs.com/editor/net/).