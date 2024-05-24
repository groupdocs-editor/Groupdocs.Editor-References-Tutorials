---
title: Enregistrer le document modifié dans différents formats
linktitle: Enregistrer le document modifié dans différents formats
second_title: API GroupDocs.Editor .NET
description: Découvrez comment enregistrer des documents modifiés dans différents formats à l'aide de GroupDocs.Editor for .NET dans ce guide complet étape par étape.
type: docs
weight: 11
url: /fr/net/document-processing/save-edited-document-various-formats/
---
## Introduction
Cherchez-vous à enregistrer des documents modifiés dans différents formats à l'aide de GroupDocs.Editor pour .NET ? Vous êtes arrivé au bon endroit! Ce guide complet vous guidera tout au long du processus, de la configuration de votre environnement à l'enregistrement de votre document modifié dans plusieurs formats. Plongeons-nous et faisons de l'édition et de la sauvegarde de documents un jeu d'enfant !
## Conditions préalables
Avant de commencer, assurez-vous d'avoir les éléments suivants :
1.  GroupDocs.Editor pour .NET - Téléchargez la dernière version à partir de[ici](https://releases.groupdocs.com/editor/net/).
2. Environnement de développement - Visual Studio ou tout autre IDE compatible .NET.
3. .NET Framework - Assurez-vous que .NET Framework 4.6.1 ou version ultérieure est installé.
4. Exemple de document - Un exemple de document WordProcessing avec lequel travailler.
5. Connaissances de base en C# - Une connaissance de la programmation C# est requise.
## Importer des espaces de noms
Pour commencer, assurez-vous d'importer les espaces de noms nécessaires dans votre projet C#. Ceci est crucial pour accéder à la fonctionnalité GroupDocs.Editor.
```csharp
using System;
using GroupDocs.Editor.Metadata;
```
Décomposons le processus en étapes gérables. Suivez attentivement pour vous assurer que vous comprenez chaque partie.
## Étape 1 : obtenir un chemin d'accès au fichier d'entrée
Tout d’abord, vous devez spécifier le chemin d’accès à votre fichier WordProcessing d’entrée. Ce fichier sera chargé et édité.
```csharp
string inputFilePath = "Your Sample Document";
```
## Étape 2 : Créer des options de chargement pour le document
Ensuite, créez des options de chargement spécifiques aux documents WordProcessing. Ces options aideront à personnaliser la façon dont le document est chargé.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
```
## Étape 3 : Charger le document avec les options
 Maintenant, chargez le document dans un`Editor` instance en utilisant les options de chargement spécifiées.
```csharp
using (Editor editor = new Editor(inputFilePath, delegate { return loadOptions; }))
```
## Étape 4 : Créer des options d'édition
Préparez les options d'édition pour le document. Ces options détermineront la manière dont le document est ouvert pour l'édition.
```csharp
WordProcessingEditOptions editOptions = new WordProcessingEditOptions();
```
## Étape 5 : ouvrir le document pour le modifier
 Ouvrez le document pour le modifier en créant un`EditableDocument`exemple. Cette instance vous permettra d'apporter des modifications au document.
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
```
## Étape 6 : Modifier le contenu du document
Il est maintenant temps de modifier le contenu du document. Tout d’abord, récupérez le document sous la forme d’une seule chaîne codée en base64.
```csharp
string allEmbeddedInsideString = beforeEdit.GetEmbeddedHtml();
```
Par exemple, modifions le sous-titre dans le document.
```csharp
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
```
## Étape 7 : Créer un nouveau document modifiable à partir du contenu modifié
 Créer un nouveau`EditableDocument` instance à partir du contenu et des ressources édités.
```csharp
using (EditableDocument afterEdit = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null))
```
## Étape 8 : Enregistrer le document dans différents formats
Enfin, parcourez tous les formats WordProcessing pris en charge et enregistrez le document modifié dans chaque format.
```csharp
foreach (WordProcessingFormats oneFormat in WordProcessingFormats.All)
{
    // Préparer les options de sauvegarde
    WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(oneFormat);
    // Préparer le chemin de sauvegarde
    string savePath = Path.Combine("OutputDirectory", "MultipleOutFormats." + saveOptions.OutputFormat.Extension);
    // Enregistrez le document
    editor.Save(afterEdit, savePath, saveOptions);
}
```
## Message d'achèvement
Pour conclure, vous pouvez imprimer un message indiquant que le processus s'est terminé avec succès.
```csharp
Console.WriteLine("SavingEditedDocumentToAllFormats routine has successfully finished");
```
## Conclusion
Toutes nos félicitations! Vous avez appris avec succès comment enregistrer des documents modifiés dans différents formats à l'aide de GroupDocs.Editor pour .NET. Cet outil puissant facilite la manipulation et l'enregistrement de documents dans plusieurs formats avec seulement quelques lignes de code. N'oubliez pas que les étapes clés consistent à charger le document, à modifier le contenu et à l'enregistrer dans les formats souhaités.
## FAQ
### Qu’est-ce que GroupDocs.Editor pour .NET ?
GroupDocs.Editor for .NET est une API puissante qui vous permet de modifier des documents dans différents formats à l'aide d'applications .NET.
### Puis-je utiliser GroupDocs.Editor gratuitement ?
 Oui, vous pouvez l'utiliser avec un essai gratuit. Télécharge le[ici](https://releases.groupdocs.com/).
### Quels formats sont pris en charge par GroupDocs.Editor ?
GroupDocs.Editor prend en charge un large éventail de formats, notamment DOCX, PDF, HTML et bien d'autres.
### Comment puis-je obtenir une licence temporaire pour GroupDocs.Editor ?
 Vous pouvez obtenir un permis temporaire[ici](https://purchase.groupdocs.com/temporary-license/).
### Où puis-je trouver plus de documentation et d'assistance ?
 Une documentation détaillée est disponible[ici](https://reference.groupdocs.com/editor/net/) , et vous pouvez obtenir de l'aide[ici](https://forum.groupdocs.com/c/editor/20).