---
title: Créer un document
linktitle: Créer un document
second_title: API GroupDocs.Editor .NET
description: Apprenez à modifier des documents Word, Excel, PowerPoint, Ebook et Email à l'aide de GroupDocs.Editor for .NET avec ce didacticiel complet étape par étape.
weight: 10
url: /fr/net/document-editing/create-document/
type: docs
---
# Créer un document

## Introduction
Êtes-vous fatigué des tracas liés à la modification de différents types de documents par programmation ? GroupDocs.Editor pour .NET est là pour simplifier le processus. Cet outil puissant permet aux développeurs de modifier facilement divers formats de documents tels que Word, Excel, PowerPoint, ebooks et e-mails. Dans ce didacticiel, nous verrons en profondeur comment utiliser GroupDocs.Editor for .NET pour créer et modifier des documents. Nous décomposerons le processus en étapes faciles à suivre, le rendant accessible même si vous débutez dans ce domaine.
## Conditions préalables
Avant de commencer, assurez-vous d'avoir les éléments suivants :
- Visual Studio installé sur votre ordinateur.
- .NET Framework (4.0 ou supérieur).
-  GroupDocs.Editor pour la bibliothèque .NET. Vous pouvez le télécharger depuis[ici](https://releases.groupdocs.com/editor/net/).
- Connaissance de base de la programmation C#.
## Importer des espaces de noms
Tout d’abord, importons les espaces de noms nécessaires. Cela rendra les classes et méthodes requises accessibles dans notre application.
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using System.IO;
```
## Étape 1 : configuration du flux
Pour commencer, nous devons configurer un flux de mémoire qui servira d'espace réservé pour le contenu du document.
```csharp
Stream memoryStream = Stream.Null;
```
## Étape 2 : Fonction de rappel pour enregistrer le document
Ensuite, définissez une fonction de rappel qui enregistrera le nouveau flux de documents. Cette fonction est essentielle pour gérer le résultat du processus d'édition du document.
```csharp
void SaveNewDocument(Stream resultStream)
{
    memoryStream = resultStream;
}
```
## Étape 3 : Création et modification d'un document WordProcessing
 Maintenant, créons et modifions un document Word. Nous allons commencer par créer un nouveau`Editor` exemple pour les documents WordProcessing et modifiez-le avec les options par défaut.
### Créer et modifier avec les options par défaut
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    EditableDocument defaultWordProcessingDoc = editor.Edit();
}
```
### Créer et modifier avec des options personnalisées
Pour plus de contrôle, nous pouvons spécifier des options telles que la désactivation de la pagination et l'extraction des polices intégrées.
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    WordProcessingEditOptions wordProcessingEditOptions = new WordProcessingEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true,
        FontExtraction = FontExtractionOptions.ExtractAllEmbedded
    };
    EditableDocument editableWordProcessingDocument = editor.Edit(wordProcessingEditOptions);
}
```
## Étape 4 : Création et modification d'une feuille de calcul
De même, nous pouvons créer et éditer un document Excel. Voici comment procéder.
### Créer et modifier avec les options par défaut
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    EditableDocument defaultEditableSpreadsheetDocument = editor.Edit();
}
```
### Créer et modifier avec des options personnalisées
 Pour cibler des feuilles de calcul spécifiques ou exclure celles masquées, nous utilisons`SpreadsheetEditOptions`.
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    SpreadsheetEditOptions spreadsheetEditOptions = new SpreadsheetEditOptions
    {
        WorksheetIndex = 0,
        ExcludeHiddenWorksheets = true
    };
    EditableDocument editableSpreadsheetDocument = editor.Edit(spreadsheetEditOptions);
}
```
## Étape 5 : Création et modification d'un document de présentation
Les présentations PowerPoint sont également prises en charge. Voyons comment les gérer.
### Créer et modifier avec les options par défaut
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    EditableDocument defaultEditablePresentationDocument = editor.Edit();
}
```
### Créer et modifier avec des options personnalisées
Vous pouvez personnaliser vos modifications en spécifiant des options telles que la diapositive à afficher et l'inclusion ou non des diapositives masquées.
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    PresentationEditOptions presentationEditOptions = new PresentationEditOptions
    {
        ShowHiddenSlides = false,
        SlideNumber = 0
    };
    EditableDocument editablePresentationDocument = editor.Edit(presentationEditOptions);
}
```
## Étape 6 : Création et modification d'un document ebook
GroupDocs.Editor permet également d'éditer des formats de livres électroniques comme EPUB. Voici comment vous pouvez gérer cela.
### Créer et modifier avec les options par défaut
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EditableDocument defaultEditableEbookDocument = editor.Edit();
}
```
### Créer et modifier avec des options personnalisées
Personnalisez l'édition de votre ebook en activant ou en désactivant les informations de pagination et de langue.
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EbookEditOptions ebookEditOptions = new EbookEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true
    };
    EditableDocument editableEbookDocument = editor.Edit(ebookEditOptions);
}
```
## Étape 7 : Création et modification d'un document électronique
Enfin, nous verrons comment modifier des documents électroniques. Cela inclut des formats comme EML.
### Créer et modifier avec les options par défaut
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EditableDocument defaultEditableEmailDocument = editor.Edit();
}
```
### Créer et modifier avec des options personnalisées
Spécifiez les options de sortie des messages électroniques pour contrôler le processus d'édition.
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EmailEditOptions emailEditOptions = new EmailEditOptions
    {
        MailMessageOutput = MailMessageOutput.All
    };
    EditableDocument editableEmailDocument = editor.Edit(emailEditOptions);
}
```
## Étape 8 : Finaliser le processus
Après avoir édité les documents, il est crucial de disposer correctement du flux mémoire pour libérer des ressources.
```csharp
memoryStream.Dispose();
System.Console.WriteLine("CreateDocument routine has successfully finished");
```
## Conclusion
GroupDocs.Editor for .NET est un outil polyvalent et puissant qui peut simplifier la tâche de modification de divers types de documents par programmation. En suivant ce guide étape par étape, vous pouvez créer et modifier facilement des documents, qu'il s'agisse de fichiers WordProcessing, de feuilles de calcul, de présentations, de livres électroniques ou d'e-mails. Plongez dans la documentation GroupDocs.Editor pour des fonctionnalités plus avancées et des options de personnalisation.
## FAQ
### Quels types de documents puis-je modifier avec GroupDocs.Editor pour .NET ?
Vous pouvez modifier un large éventail de documents, notamment des documents WordProcessing, des feuilles de calcul, des présentations, des livres électroniques et des e-mails.
### Est-il possible de personnaliser les options d'édition ?
Oui, GroupDocs.Editor pour .NET permet une personnalisation étendue grâce à diverses options d'édition spécifiques à chaque type de document.
### Comment gérer la sortie des documents édités ?
Vous pouvez utiliser une fonction de rappel pour enregistrer le flux de documents modifiés à l'emplacement souhaité.
### Ai-je besoin d’une licence pour utiliser GroupDocs.Editor pour .NET ?
 Oui, vous pouvez obtenir une licence auprès de[ici](https://purchase.groupdocs.com/buy). Il existe également une option pour une licence temporaire.
### Où puis-je trouver une documentation plus détaillée ?
 Une documentation détaillée est disponible sur le[Page de documentation GroupDocs.Editor pour .NET](https://tutorials.groupdocs.com/editor/net/).