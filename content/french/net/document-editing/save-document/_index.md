---
title: Enregistrer le document
linktitle: Enregistrer le document
second_title: API GroupDocs.Editor .NET
description: Modifiez et enregistrez sans effort des documents à l'aide de GroupDocs.Editor pour .NET. Ce guide étape par étape simplifie le processus pour les développeurs.
weight: 14
url: /fr/net/document-editing/save-document/
---

# Enregistrer le document

## Introduction
Cherchez-vous à modifier et enregistrer des documents sans effort à l’aide de GroupDocs.Editor pour .NET ? Vous êtes au bon endroit ! Ce didacticiel vous guidera tout au long du processus étape par étape, vous garantissant ainsi une gestion facile de vos documents. Que vous soyez un développeur chevronné ou un débutant, notre guide vous fournira toutes les informations dont vous avez besoin pour vous lancer.
## Conditions préalables
Avant de plonger dans le didacticiel, assurez-vous que les conditions préalables suivantes sont remplies :
- Environnement de développement : Visual Studio installé sur votre machine.
- .NET Framework : assurez-vous que vous disposez de .NET Framework 4.6.1 ou version ultérieure.
-  GroupDocs.Editor pour .NET : téléchargez la dernière version[ici](https://releases.groupdocs.com/editor/net/).
- Connaissances de base en C# : Une connaissance de la programmation C# est essentielle.
## Importer des espaces de noms
Pour utiliser GroupDocs.Editor dans votre projet .NET, vous devez importer les espaces de noms nécessaires. Voici comment procéder :
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
Maintenant que notre environnement est configuré et que les espaces de noms nécessaires sont importés, passons aux étapes requises pour charger, modifier et enregistrer un document à l'aide de GroupDocs.Editor for .NET.
## Étape 1 : Charger le document
Tout d’abord, nous devons charger le document que nous souhaitons modifier. GroupDocs.Editor simplifie ce processus. Voici comment procéder :

```csharp
string inputFilePath = "Your Sample Document";
Editor editor = new Editor(inputFilePath, delegate { return new Options.WordProcessingLoadOptions(); });
EditableDocument defaultWordProcessingDoc = editor.Edit();
```
 Dans cette étape, nous spécifions le chemin d'accès au document que nous souhaitons modifier et créons une instance du`Editor` classe. Le`Edit` La méthode est ensuite appelée pour charger le document dans un`EditableDocument` objet.
## Étape 2 : modifier le document
Une fois le document chargé, il est temps d'apporter quelques modifications. Comme nous n'avons pas d'éditeur WYSIWYG connecté, nous allons simuler le processus d'édition dans le code.

```csharp
string allEmbeddedInsideString = defaultWordProcessingDoc.GetEmbeddedHtml();
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
EditableDocument editedDoc = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```
 Ici, nous récupérons le contenu HTML intégré du document, effectuons un simple remplacement de texte et créons un nouveau`EditableDocument`instance à partir du code HTML modifié.
## Étape 3 : Enregistrez le document
Après avoir modifié le document, la dernière étape consiste à l'enregistrer. GroupDocs.Editor propose plusieurs options pour enregistrer le document dans différents formats.
## Enregistrer au format RTF
```csharp
string outputRtfPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.rtf");
WordProcessingSaveOptions rtfSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
editor.Save(editedDoc, outputRtfPath, rtfSaveOptions);
```
## Enregistrer sous DOCM
```csharp
string outputDocmPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.docm");
WordProcessingSaveOptions docmSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm);
using (FileStream outputStream = File.Create(outputDocmPath))
{
    editor.Save(editedDoc, outputStream, docmSaveOptions);
}
```
## Enregistrer en texte brut
```csharp
string outputTxtPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.txt");
TextSaveOptions textSaveOptions = new TextSaveOptions
{
    Encoding = System.Text.Encoding.UTF8,
    PreserveTableLayout = true
};
editor.Save(editedDoc, outputTxtPath, textSaveOptions);
```
## Étape 4 : Nettoyage
 Enfin, il est crucial de disposer du`EditableDocument` et`Editor` instances pour libérer des ressources.
```csharp
editedDoc.Dispose();
defaultWordProcessingDoc.Dispose();
editor.Dispose();
```
En suivant ces étapes, vous pouvez charger, modifier et enregistrer efficacement des documents à l'aide de GroupDocs.Editor for .NET. Cet outil puissant offre flexibilité et facilité d’utilisation, faisant de la gestion des documents un jeu d’enfant.
## Conclusion
La modification et l'enregistrement de documents par programmation n'ont jamais été aussi simples avec GroupDocs.Editor for .NET. Ce guide vous a guidé tout au long du processus, du chargement d'un document à son enregistrement dans différents formats. Avec GroupDocs.Editor, vous disposez d'une solution polyvalente et robuste à portée de main, simplifiant le processus d'édition de documents.
## FAQ
### Quels formats de fichiers GroupDocs.Editor prend-il en charge ?
GroupDocs.Editor prend en charge divers formats de fichiers, notamment DOCX, RTF, TXT et bien d'autres. Pour une liste complète, consultez le[Documentation](https://tutorials.groupdocs.com/editor/net/).
### Puis-je essayer GroupDocs.Editor avant d'acheter ?
 Oui, vous pouvez obtenir un[essai gratuit](https://releases.groupdocs.com/) pour tester les fonctionnalités de GroupDocs.Editor.
### Existe-t-il une assistance disponible si je rencontre des problèmes ?
 Absolument! Vous pouvez visiter le[forum d'entraide](https://forum.groupdocs.com/c/editor/20) pour obtenir de l'aide concernant tout problème que vous rencontrez.
### Comment obtenir un permis temporaire ?
 Vous pouvez demander un[permis temporaire](https://purchase.groupdocs.com/temporary-license/) à des fins d’évaluation.
### Où puis-je acheter la version complète de GroupDocs.Editor ?
 Vous pouvez acheter la version complète[ici](https://purchase.groupdocs.com/buy).