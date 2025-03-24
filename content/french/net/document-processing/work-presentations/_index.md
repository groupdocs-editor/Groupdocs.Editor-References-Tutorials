---
title: Travailler avec des présentations
linktitle: Travailler avec des présentations
second_title: API GroupDocs.Editor .NET
description: Apprenez à modifier des présentations PowerPoint à l'aide de GroupDocs.Editor pour .NET. Suivez ce guide étape par étape pour rationaliser votre processus d'édition de documents.
weight: 16
url: /fr/net/document-processing/work-presentations/
---
## Introduction
À l’ère numérique d’aujourd’hui, une gestion et une édition efficaces des documents sont cruciales. Que vous soyez un développeur ou quelqu'un qui traite fréquemment des présentations, savoir comment travailler avec des outils qui rationalisent ces processus peut vous faire gagner du temps et des efforts. L'un de ces outils est GroupDocs.Editor pour .NET, une API puissante qui vous permet de modifier des documents, y compris des présentations, par programmation. Ce didacticiel vous guidera à travers les étapes de travail avec des présentations à l'aide de GroupDocs.Editor pour .NET, de la configuration de votre environnement à la modification et à l'enregistrement de vos fichiers de présentation.
## Conditions préalables
Avant de plonger dans le didacticiel, assurez-vous d'avoir les prérequis suivants :
1. Visual Studio : un IDE adapté au développement .NET.
2.  GroupDocs.Editor pour .NET : vous pouvez le télécharger à partir du[site web](https://releases.groupdocs.com/editor/net/).
3. .NET Framework : assurez-vous qu'une version compatible est installée.
4. Exemple de fichier PPTX : un exemple de fichier PowerPoint à des fins de test.
5. Connaissance de base de C# : Une connaissance de la programmation C# sera utile.
## Importer des espaces de noms
Pour commencer, importez les espaces de noms nécessaires dans votre projet C#. Ces espaces de noms donneront accès aux classes et méthodes requises pour l'édition des présentations.
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```
## Étape 1 : obtenir le chemin du fichier d'entrée
Tout d’abord, vous devez spécifier le chemin d’accès à votre fichier de présentation d’entrée. Ce fichier sera utilisé à des fins d'édition.
```csharp
string inputFilePath = "YourSampleDocument.pptx";
```
## Étape 2 : Créer un flux de fichiers
Ensuite, créez un flux de fichiers à partir du chemin spécifié. Ce flux servira à charger la présentation dans l'éditeur.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
```
## Étape 3 : Créer des options de chargement
Vous devez créer des options de chargement spécifiques aux présentations. Cette étape inclut la gestion des fichiers protégés par mot de passe, le cas échéant.

```csharp
PresentationLoadOptions loadOptions = new PresentationLoadOptions
{
    Password = "some_password_to_open_a_document"
};
```
## Étape 4 : Charger le document dans l'éditeur
Une fois le flux de fichiers et les options de chargement prêts, chargez la présentation dans l'instance de l'éditeur.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
```
## Étape 5 : Créer des options d'édition
Configurez les options d'édition, telles que la diapositive spécifique que vous souhaitez modifier et l'affichage ou non des diapositives masquées.
Spécifiez l'index de la diapositive que vous souhaitez modifier. Notez que l'index est de base zéro, donc la première diapositive est l'index 0.
```csharp
PresentationEditOptions editOptions = new PresentationEditOptions
{
    SlideNumber = 0, // Première diapositive
    ShowHiddenSlides = true
};
```
## Étape 6 : Créer un document modifiable
Créez un document modifiable intermédiaire à l'aide de l'éditeur et des options d'édition spécifiées.
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
{
```
## Étape 7 : Extraire le contenu et les ressources
Extrayez le contenu textuel sous forme de balisage HTML et récupérez toutes les ressources du document original.
```csharp
string originalContent = beforeEdit.GetContent();
```
## Étape 7.1 : Extraire les ressources
Récupérez toutes les ressources, telles que les images et les styles.
```csharp
List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## Étape 8 : Modifier le contenu
Modifiez le contenu si nécessaire. Par exemple, remplacez un texte spécifique dans le contenu HTML.
```csharp
string editedContent = originalContent.Replace("New text", "edited text");
```
## Étape 9 : Créer un nouveau document modifiable
 Créer une nouvelle instance de`EditableDocument` avec le contenu édité et les mêmes ressources.
```csharp
using (EditableDocument afterEdit = EditableDocument.FromMarkup(editedContent, allResources))
{
```
## Étape 10 : Créer des options de sauvegarde
Configurez les options d'enregistrement du document modifié, y compris le format et le cryptage.
```csharp
PresentationSaveOptions saveOptions = new PresentationSaveOptions(PresentationFormats.Pptm)
{
    Password = "password"
};
```
## Étape 11 : Enregistrez le document modifié
Enfin, enregistrez la présentation modifiée à l'emplacement souhaité.

```csharp
string outputFilename = Path.GetFileNameWithoutExtension(inputFilePath) + "." + saveOptions.OutputFormat.Extension;
string outputPath = Path.Combine("YourOutputDirectory", outputFilename);
```
## Étape 11.1 : Créer un flux de fichiers pour l'enregistrement
Créez un flux de fichiers pour enregistrer la présentation modifiée.
```csharp
using (FileStream outputStream = File.Create(outputPath))
{
```
## Étape 11.2 : Enregistrez le document
Enregistrez le document à l'aide de l'instance de l'éditeur.
```csharp
editor.Save(afterEdit, outputStream, saveOptions);
```
```csharp
}
}
}
System.Console.WriteLine("Working with presentations routine has successfully finished");
```
## Conclusion
Travailler avec des présentations à l’aide de GroupDocs.Editor pour .NET est simple et efficace. En suivant ce guide étape par étape, vous pouvez facilement modifier et enregistrer des fichiers PowerPoint par programme. Que vous automatisiez les flux de travail documentaires ou intégriez l'édition de présentations dans vos applications, GroupDocs.Editor fournit les outils dont vous avez besoin pour accomplir votre travail.
## FAQ
### GroupDocs.Editor for .NET peut-il gérer des présentations protégées par mot de passe ?
Oui il peut. Vous pouvez spécifier le mot de passe dans les options de chargement pour ouvrir et modifier des présentations protégées par mot de passe.
### Quels formats GroupDocs.Editor for .NET prend-il en charge pour enregistrer des présentations ?
GroupDocs.Editor prend en charge divers formats, notamment PPTX, PPTM, etc. Vous pouvez spécifier le format souhaité dans les options de sauvegarde.
### Est-il possible de modifier plusieurs diapositives à la fois ?
Actuellement, GroupDocs.Editor vous permet de modifier une diapositive à la fois. Vous pouvez parcourir les diapositives et appliquer des modifications individuellement si nécessaire.
### Puis-je utiliser GroupDocs.Editor pour .NET dans une application Web ?
Oui, GroupDocs.Editor pour .NET peut être intégré aux applications Web pour fournir des fonctionnalités d'édition de documents.
### Où puis-je trouver une documentation et une assistance plus détaillées ?
 Vous pouvez trouver une documentation détaillée[ici](https://tutorials.groupdocs.com/editor/net/) . Pour obtenir de l'aide, visitez le[forum d'entraide](https://forum.groupdocs.com/c/editor/20).