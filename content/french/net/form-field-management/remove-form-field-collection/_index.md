---
title: Supprimer la collection de champs de formulaire
linktitle: Supprimer la collection de champs de formulaire
second_title: API GroupDocs.Editor .NET
description: Découvrez comment supprimer des champs de formulaire des documents Word à l'aide de GroupDocs.Editor pour .NET avec ce guide étape par étape. Idéal pour les développeurs.
weight: 13
url: /fr/net/form-field-management/remove-form-field-collection/
---

# Supprimer la collection de champs de formulaire

## Introduction
Cherchez-vous à gérer les champs de formulaire dans vos documents par programmation ? GroupDocs.Editor pour .NET offre une solution puissante pour gérer et manipuler les champs de formulaire dans différents formats de document. Dans ce didacticiel, nous vous guiderons à travers les étapes permettant de supprimer des collections de champs de formulaire d'un document Word à l'aide de cette bibliothèque robuste. 
## Conditions préalables
Avant de plonger dans le code, assurons-nous que tout est configuré pour une expérience fluide :
1. GroupDocs.Editor pour .NET : assurez-vous d'avoir téléchargé et installé GroupDocs.Editor pour .NET. Sinon, vous pouvez le télécharger[ici](https://releases.groupdocs.com/editor/net/).
2. Environnement de développement : vous aurez besoin d'un environnement de développement tel que Visual Studio.
3. .NET Framework : assurez-vous que .NET Framework est installé sur votre ordinateur.
4.  Exemple de document : ayez un exemple de document Word (par exemple,`SampleLegacyFormFields.docx`) avec les champs de formulaire que vous souhaitez manipuler.

## Importer des espaces de noms
Pour commencer, vous devez importer les espaces de noms nécessaires dans votre projet .NET. Cela vous permettra d'accéder aux fonctionnalités de GroupDocs.Editor.
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System.IO;
```
## Étape 1 : Charger le document
Tout d’abord, vous devrez charger le document que vous souhaitez modifier. Décomposons-le :
### Étape 1.1 : obtenir le chemin d'accès au fichier d'entrée
 Vous devez spécifier le chemin d'accès à votre fichier d'entrée. Pour cet exemple, nous utiliserons un exemple de fichier appelé`SampleLegacyFormFields.docx`.
```csharp
string inputFilePath = "path/to/SampleLegacyFormFields.docx";
```
### Étape 1.2 : Créer un FileStream à partir du chemin
 Ensuite, créez un`FileStream` pour lire le document.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
    // Passez aux étapes suivantes dans ce bloc using.
}
```
## Étape 2 : définir les options de chargement
Lors du chargement du document, vous devrez peut-être spécifier des options de chargement, surtout si votre document est protégé par mot de passe.
### Étape 2.1 : Créer des options de chargement
 Créer une instance de`WordProcessingLoadOptions`.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
```
### Étape 2.2 : Spécifiez le mot de passe (si nécessaire)
Si votre document est protégé par mot de passe, vous pouvez spécifier le mot de passe.
```csharp
loadOptions.Password = "some_password_to_open_a_document";
```
## Étape 3 : Charger le document dans l'éditeur
 Maintenant, chargez le document dans le`Editor` exemple en utilisant le`FileStream` et`LoadOptions`.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    // Passez aux étapes suivantes dans ce bloc using.
}
```
## Étape 4 : Accéder et gérer les champs du formulaire
Une fois le document chargé, vous pouvez désormais accéder et manipuler les champs du formulaire.
### Étape 4.1 : Lire le FormFieldManager
 Récupérer le`FormFieldManager` du`Editor` exemple.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
### Étape 4.2 : accéder à FormFieldCollection
 Obtenir le`FormFieldCollection` qui contient tous les champs de formulaire du document.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
### Étape 4.3 : Supprimer un champ de formulaire de texte spécifique
Pour supprimer un champ de formulaire de texte spécifique, recherchez-le par son nom, puis supprimez-le.
```csharp
TextFormField textField = collection.GetFormField<TextFormField>("Text1");
fieldManager.RemoveFormFiled(textField);
```
### Étape 4.4 : Supprimer plusieurs champs de formulaire
Vous pouvez également supprimer plusieurs champs de formulaire à la fois en spécifiant leurs noms.
```csharp
textField = collection.GetFormField<TextFormField>("Text7");
CheckBoxForm checkBoxForm = collection.GetFormField<CheckBoxForm>("Check2");
fieldManager.RemoveFormFields(new IFormField[] { textField, checkBoxForm });
```
## Étape 5 : Enregistrez le document modifié
Après avoir modifié les champs du formulaire, vous devez enregistrer le document.
### Étape 5.1 : Créer des options de sauvegarde
Spécifiez le format et les options d'enregistrement du document de sortie.
```csharp
WordProcessingFormats docFormat = WordProcessingFormats.Docx;
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(docFormat);
```
### Étape 5.2 : optimiser l'utilisation de la mémoire
Si vous traitez des documents volumineux, vous souhaiterez peut-être optimiser l’utilisation de la mémoire.
```csharp
saveOptions.OptimizeMemoryUsage = true;
```
### Étape 5.3 : Définir la protection (si nécessaire)
Vous pouvez protéger le document contre toute modification ultérieure en définissant un mot de passe en écriture.
```csharp
saveOptions.Protection = new WordProcessingProtection(WordProcessingProtectionType.AllowOnlyFormFields, "write_password");
```
### Étape 5.4 : Enregistrez le document
 Enfin, enregistrez le document à l'aide d'un`MemoryStream`.
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(outputStream, saveOptions);
}
```

## Conclusion
Toutes nos félicitations! Vous avez supprimé avec succès les champs de formulaire d'un document Word à l'aide de GroupDocs.Editor pour .NET. Cette puissante bibliothèque facilite la manipulation du contenu des documents par programmation, ce qui vous fait gagner du temps et des efforts.
## FAQ
### Puis-je utiliser GroupDocs.Editor pour .NET avec d’autres formats de document ?
Oui, GroupDocs.Editor pour .NET prend en charge divers formats de documents, notamment PDF, HTML, etc.
### Est-il possible d'ajouter des champs de formulaire à l'aide de GroupDocs.Editor pour .NET ?
Oui, vous pouvez ajouter, modifier et supprimer des champs de formulaire par programmation.
### Que faire si mon document est très volumineux ?
Vous pouvez activer l'optimisation de la mémoire dans les options d'enregistrement pour gérer efficacement les documents volumineux.
### Puis-je utiliser GroupDocs.Editor pour .NET dans une application Web ?
Absolument! GroupDocs.Editor pour .NET peut être intégré dans des applications Web pour le traitement de documents côté serveur.
### Où puis-je obtenir de l'aide si je rencontre des problèmes ?
 Vous pouvez visiter le[forum d'entraide](https://forum.groupdocs.com/c/editor/20) pour obtenir de l'aide en cas de problème.