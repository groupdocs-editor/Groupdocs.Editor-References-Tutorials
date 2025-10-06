---
title: Corrigez la collecte de champs de formulaire invalides et enregistrez
linktitle: Corrigez la collecte de champs de formulaire invalides et enregistrez
second_title: API GroupDocs.Editor .NET
description: Découvrez comment corriger les champs de formulaire non valides dans DOCX à l'aide de Groupdocs.Editor pour .NET. Suivez ce guide pour vous assurer que vos documents sont exempts d'erreurs et enregistrez-les en toute sécurité.
weight: 11
url: /fr/net/form-field-management/fix-invalid-form-field-collection-save/
type: docs
---
# Corrigez la collecte de champs de formulaire invalides et enregistrez

## Introduction
Accueillir! Si vous travaillez avec des champs de formulaire dans des documents et que vous rencontrez des problèmes avec des collections de champs de formulaire non valides, vous êtes au bon endroit. Dans ce didacticiel, nous verrons comment corriger les champs de formulaire non valides et enregistrer votre document à l'aide de Groupdocs.Editor pour .NET. Nous vous guiderons pas à pas tout au long du processus, en veillant à ce que vous disposiez de tous les détails dont vous avez besoin pour que tout fonctionne sans problème. Commençons!
## Conditions préalables
Avant de passer au code, vous devez mettre en place quelques éléments :
-  Groupdocs.Editor pour .NET : assurez-vous d'avoir installé la bibliothèque Groupdocs.Editor pour .NET. Vous pouvez le télécharger[ici](https://releases.groupdocs.com/editor/net/).
- Environnement de développement : vous devez disposer d'un environnement de développement .NET, tel que Visual Studio.
- Connaissance de base de C# : ce didacticiel suppose que vous possédez une compréhension de base de la programmation C#.
## Importer des espaces de noms
Tout d’abord, vous devez importer les espaces de noms nécessaires dans votre projet C#. Ajoutez les lignes suivantes au début de votre fichier de code :
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System;
using System.IO;
```
## Étape 1 : obtenir le chemin du fichier d'entrée
La première étape consiste à spécifier le chemin d'accès à votre fichier d'entrée. Ce fichier doit être un document DOCX contenant des champs de formulaire.
```csharp
string inputFilePath = Constants.SampleLegacyFormFields_docx;
```
## Étape 2 : Créer un flux à partir du chemin du fichier
Ensuite, créez un flux de fichiers pour lire le document d'entrée. Cela vous permettra de charger le document dans l'éditeur.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
```
## Étape 3 : Créer des options de chargement pour le document
Dans cette étape, vous devez créer des options de chargement pour votre document. Si votre document est protégé par mot de passe, vous pouvez spécifier le mot de passe. Dans cet exemple, le document n'est pas protégé, le mot de passe est donc ignoré.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
loadOptions.Password = "some_password_to_open_a_document";
```
## Étape 4 : charger le document dans l'instance de l'éditeur
Maintenant, chargez le document avec les options spécifiées dans l'instance Editor. C’est ici que se dérouleront les principales opérations sur le document.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
```
## Étape 4.1 : Lire l'instance FormFieldManager
 Le`FormFieldManager` L'instance est responsable de la gestion des champs de formulaire dans le document. Vous devrez lire cette instance pour accéder et manipuler les champs du formulaire.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
## Étape 4.2 : Lire le FormFieldCollection
 Le`FormFieldCollection` contient tous les champs de formulaire du document. Vous lirez cette collection pour vérifier et corriger les champs de formulaire invalides.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
## Étape 4.3 : Correction automatique des champs de formulaire invalides
Essayez de corriger automatiquement tous les champs de formulaire non valides dans le document. Il s’agit d’une étape préliminaire pour résoudre des problèmes évidents.
```csharp
fieldManager.FixInvalidFormFieldNames(new InvalidFormField[0]);
collection = fieldManager.FormFieldCollection;
```
## Étape 4.4 : Rechercher les champs de formulaire invalides
Vérifiez s'il reste des champs de formulaire non valides après la tentative de correction automatique.
```csharp
bool hasInvalidFormFields = fieldManager.HasInvalidFormFields();
Console.WriteLine("FormFieldCollection contains invalid items: {0}", hasInvalidFormFields);
```
## Étape 4.4.1 : Obtenir tous les noms de champs de formulaire invalides
Récupérez les noms de tous les champs de formulaire invalides. Ces noms seront utilisés pour corriger les champs.
```csharp
var invalidFormFields = fieldManager.GetInvalidFormFieldNames();
```
## Étape 4.4.2 : Créer des noms uniques pour les champs non valides
Pour chaque champ de formulaire non valide, créez un nom unique. Cela garantit qu'il n'y a aucun conflit avec les noms de champs de formulaire existants.
```csharp
foreach (var invalidItem in invalidFormFields)
{
    invalidItem.FixedName = string.Format("{0}_{1}", invalidItem.Name, Guid.NewGuid());
}
```
## Étape 4.4.3 : Corriger les champs de formulaire invalides
Corrigez les champs de formulaire invalides en utilisant les noms uniques créés à l'étape précédente.
```csharp
fieldManager.FixInvalidFormFieldNames(invalidFormFields);
collection = fieldManager.FormFieldCollection;
```
## Étape 5 : Créer des options d'enregistrement de document
Configurez les options d'enregistrement du document. Cela inclut la spécification du format et de tous les paramètres de sauvegarde supplémentaires.
```csharp
WordProcessingFormats docFormat = WordProcessingFormats.Docx;
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(docFormat);
```
## Étape 5.1 : optimiser l'utilisation de la mémoire
 Si votre document est volumineux et risque de provoquer un`OutOfMemoryException`activez l'option d'optimisation de la mémoire.
```csharp
saveOptions.OptimizeMemoryUsage = true;
```
## Étape 5.2 : Protéger le document contre l'écriture
Pour protéger le document contre toute modification, à l'exception des champs du formulaire, définissez un mot de passe de protection.
```csharp
saveOptions.Protection = new WordProcessingProtection(WordProcessingProtectionType.AllowOnlyFormFields, "write_password");
```
## Étape 6 : Enregistrez le document
Enfin, enregistrez le document avec les options d'enregistrement spécifiées. Préparez un flux de mémoire pour enregistrer le document de sortie.
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(outputStream, saveOptions);
}
Console.WriteLine("FixInvalidFormFieldCollectionAndSave routine has successfully finished");
```
## Conclusion
 Et voila! Vous avez réussi à corriger les champs de formulaire non valides et à enregistrer votre document à l'aide de Groupdocs.Editor pour .NET. Ce guide étape par étape aurait dû rendre le processus clair et gérable. Si vous rencontrez des problèmes ou avez des questions, n'hésitez pas à consulter le[Documentation](https://tutorials.groupdocs.com/editor/net/) ou contactez[soutien](https://forum.groupdocs.com/c/editor/20).
## FAQ
### Que faire si mon document est protégé par mot de passe ?
 Vous pouvez spécifier le mot de passe dans le`WordProcessingLoadOptions` pour ouvrir le document.
### Comment savoir s’il y a des champs de formulaire invalides ?
 Utilisez le`HasInvalidFormFields` méthode pour vérifier les champs de formulaire non valides dans le document.
### Puis-je corriger les champs du formulaire sans changer leurs noms ?
Il est recommandé de créer des noms uniques pour les champs de formulaire non valides afin d'éviter les conflits.
### Dans quels formats puis-je enregistrer le document ?
 Vous pouvez enregistrer le document dans différents formats tels que DOCX, PDF, etc. en définissant le paramètre approprié.`WordProcessingFormats`.
### Comment puis-je optimiser l’utilisation de la mémoire tout en enregistrant des documents volumineux ?
 Activer le`OptimizeMemoryUsage` possibilité dans le`WordProcessingSaveOptions` pour gérer efficacement des documents volumineux.