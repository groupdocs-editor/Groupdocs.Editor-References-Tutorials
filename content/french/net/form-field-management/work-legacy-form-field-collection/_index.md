---
title: Travailler avec la collection de champs de formulaire héritée
linktitle: Travailler avec la collection de champs de formulaire héritée
second_title: API GroupDocs.Editor .NET
description: Découvrez comment gérer les anciens champs de formulaire à l'aide de GroupDocs.Editor pour .NET avec notre guide détaillé. Parfait pour gérer les champs de texte, les cases à cocher, les dates et bien plus encore.
weight: 12
url: /fr/net/form-field-management/work-legacy-form-field-collection/
---

# Travailler avec la collection de champs de formulaire héritée

## Introduction
Bienvenue dans ce guide complet sur la façon de travailler avec les anciennes collections de champs de formulaire à l'aide de GroupDocs.Editor pour .NET. Qu'il s'agisse de champs de texte, de cases à cocher, de champs de date ou de menus déroulants, ce didacticiel vous guidera à travers chaque étape pour gérer efficacement ces champs. À la fin de ce guide, vous aurez une solide compréhension de la façon d'utiliser GroupDocs.Editor pour gérer divers champs de formulaire dans vos documents. Allons-y !
## Conditions préalables
Avant de commencer, assurez-vous d'avoir les prérequis suivants :
- Visual Studio : toute version récente fonctionnera.
- .NET Framework : assurez-vous que .NET Framework est installé.
-  GroupDocs.Editor pour .NET : téléchargez la dernière version[ici](https://releases.groupdocs.com/editor/net/).
- Exemple de document : un exemple de fichier DOCX avec des champs de formulaire à des fins de test.
## Importer des espaces de noms
Pour commencer, importez les espaces de noms nécessaires dans votre projet. Ces espaces de noms sont essentiels pour accéder aux classes et méthodes requises pour manipuler les champs de formulaire.
```csharp
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System.IO;
```
## Étape 1 : obtenir le chemin du fichier d'entrée
Tout d’abord, vous devez spécifier le chemin d’accès à votre fichier d’entrée. Dans cet exemple, nous utiliserons un exemple de fichier DOCX contenant divers champs de formulaire.
```csharp
string inputFilePath = "path/to/your/sample_legacy_formfields.docx";
```
## Étape 2 : Créer un flux à partir du chemin du fichier
Ensuite, créez un flux de fichiers pour lire le contenu de votre document. Ce flux sera utilisé pour charger le document dans GroupDocs.Editor.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
    // Le code supplémentaire ira ici
}
```
## Étape 3 : Créer des options de chargement pour le document
Avant de charger le document, créez des options de chargement. Ces options aideront à gérer différents scénarios, tels que les documents protégés par mot de passe.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
// Si le document est protégé par mot de passe, précisez le mot de passe
loadOptions.Password = "your_password_here"; // Utilisez un mot de passe réel si nécessaire
```
## Étape 4 : charger le document avec l'instance de l'éditeur
Maintenant, chargez le document dans l'instance Editor à l'aide du flux de fichiers et des options de chargement que vous avez créées précédemment.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    // Le code supplémentaire ira ici
}
```
## Étape 5 : Lire l'instance FormFieldManager
Pour gérer les champs de formulaire, accédez à l'instance FormFieldManager depuis l'éditeur. Cette instance vous permettra d'interagir avec les champs de formulaire de votre document.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
## Étape 6 : Lire le FormFieldCollection
Récupérez le FormFieldCollection à partir du FormFieldManager. Cette collection contient tous les champs de formulaire présents dans le document.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
## Étape 7 : Parcourir chaque champ du formulaire
Parcourez chaque champ de formulaire de la collection et identifiez son type. Selon le type, vous pouvez extraire et manipuler la valeur du champ.
```csharp
foreach (var formField in collection)
{
    switch (formField.Type)
    {
        case FormFieldType.Text:
            TextFormField textFormField = collection.GetFormField<TextFormField>(formField.Name);
            Console.WriteLine($"TextFormField detected, name: {formField.Name}, value: {textFormField.Value}");
            break;
        case FormFieldType.CheckBox:
            CheckBoxForm checkBoxFormField = collection.GetFormField<CheckBoxForm>(formField.Name);
            Console.WriteLine($"CheckBoxForm detected, name: {formField.Name}, value: {checkBoxFormField.Value}");
            break;
        case FormFieldType.Date:
            DateFormField dateFormField = collection.GetFormField<DateFormField>(formField.Name);
            Console.WriteLine($"DateFormField detected, name: {formField.Name}, value: {dateFormField.Value}");
            break;
        case FormFieldType.Number:
            NumberFormField numberFormField = collection.GetFormField<NumberFormField>(formField.Name);
            Console.WriteLine($"NumberFormField detected, name: {formField.Name}, value: {numberFormField.Value}");
            break;
        case FormFieldType.DropDown:
            DropDownFormField dropDownFormField = collection.GetFormField<DropDownFormField>(formField.Name);
            Console.WriteLine($"DropDownFormField detected, name: {formField.Name}, value selected: {dropDownFormField.Value[dropDownFormField.SelectedIndex]}");
            break;
    }
}
```
## Étape 8 : Conclusion
En suivant ces étapes, vous pouvez gérer et interagir efficacement avec les champs de formulaire hérités de vos documents à l'aide de GroupDocs.Editor for .NET. Qu'il s'agisse de champs de texte, de cases à cocher, de dates, de nombres ou de listes déroulantes, ce guide fournit une manière claire et concise de gérer chaque type.
## Conclusion
 Travailler avec des champs de formulaire existants dans des documents peut être simple lorsque vous utilisez les bons outils. GroupDocs.Editor pour .NET fournit une solution robuste pour gérer efficacement ces champs. En suivant ce guide étape par étape, vous devriez désormais pouvoir manipuler facilement différents champs de formulaire dans vos documents. N'oubliez pas d'explorer le[Documentation](https://tutorials.groupdocs.com/editor/net/)pour des fonctionnalités et des options plus avancées.
## FAQ
### 1. Puis-je utiliser GroupDocs.Editor pour .NET avec des documents protégés par mot de passe ?
Oui, vous pouvez spécifier le mot de passe dans les options de chargement pour gérer les documents protégés par mot de passe.
### 2. Comment puis-je obtenir un essai gratuit de GroupDocs.Editor pour .NET ?
 Vous pouvez télécharger un essai gratuit à partir de[ici](https://releases.groupdocs.com/).
### 3. Existe-t-il une prise en charge disponible pour GroupDocs.Editor pour .NET ?
 Oui, vous pouvez accéder à l'assistance[ici](https://forum.groupdocs.com/c/editor/20).
### 4. Puis-je acheter une licence pour GroupDocs.Editor pour .NET ?
 Oui, vous pouvez acheter une licence auprès de[ici](https://purchase.groupdocs.com/buy).
### 5. Où puis-je trouver la documentation de GroupDocs.Editor pour .NET ?
La documentation est disponible[ici](https://tutorials.groupdocs.com/editor/net/).