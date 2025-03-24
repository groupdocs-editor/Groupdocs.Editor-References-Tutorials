---
title: Récupérer du contenu HTML avec préfixe
linktitle: Récupérer du contenu HTML avec préfixe
second_title: API GroupDocs.Editor .NET
description: Découvrez comment récupérer du contenu HTML à partir de documents à l'aide de GroupDocs.Editor pour .NET avec des préfixes personnalisés pour les images et les feuilles de style. Guide étape par étape inclus.
weight: 11
url: /fr/net/html-content-retrieval/retrieve-html-content-with-prefix/
---

# Récupérer du contenu HTML avec préfixe

## Introduction
Bienvenue dans notre didacticiel étape par étape sur la façon de récupérer le contenu HTML d'un document à l'aide de GroupDocs.Editor pour .NET. Que vous soyez un développeur chevronné ou que vous débutiez tout juste, ce guide vous guidera tout au long du processus de manière facile à suivre. Nous couvrirons tout ce que vous devez savoir, de la configuration de votre environnement à l'exécution réussie du code. Allons-y !
## Conditions préalables
Avant de commencer, assurez-vous que les conditions préalables suivantes sont remplies :
1.  GroupDocs.Editor pour .NET : téléchargez la dernière version à partir du[page de téléchargement](https://releases.groupdocs.com/editor/net/).
2. Environnement de développement : Visual Studio ou tout autre environnement de développement .NET préféré.
3. Connaissance de base de C# : La familiarité avec la programmation C# vous aidera à suivre les exemples.
4. Document à modifier : préparez un exemple de document pour le test, tel qu'un document Word.
5. .NET Framework : assurez-vous que .NET Framework est installé sur votre ordinateur.
Maintenant que tout est prêt, commençons !
## Importer des espaces de noms
Tout d’abord, vous devez importer les espaces de noms nécessaires dans votre projet C#. Ces espaces de noms fournissent les classes et méthodes requises pour travailler avec GroupDocs.Editor for .NET.
```csharp
using System;
using GroupDocs.Editor.Options;
```
Une fois les espaces de noms importés, nous pouvons passer à la configuration de l'éditeur.
## Étape 1 : initialiser l'éditeur
 Pour commencer, vous devez initialiser le`Editor`classe avec votre document. Cette étape consiste à spécifier le document que vous souhaitez modifier et à fournir les options de chargement nécessaires.
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
    // D'autres étapes seront ajoutées ici
}
```
 Dans cet exemple, nous chargeons un document Word. Vous pouvez remplacer`"Your Sample Document"` avec le chemin d'accès à votre document.
## Étape 2 : modifier le document
 Ensuite, nous devons ouvrir le document pour le modifier. Cela se fait en utilisant le`Edit` méthode du`Editor` classe, ce qui nécessite`WordProcessingEditOptions` comme argument.
```csharp
using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
{
    // D'autres étapes seront ajoutées ici
}
```
 Le`EditableDocument` L'instance représente le document dans un format modifiable. Nous sommes maintenant prêts à récupérer le contenu HTML.
## Étape 3 : Définir des préfixes personnalisés
Pour ajouter des préfixes personnalisés pour les images et CSS, nous devons définir les préfixes sous forme de chaînes. Cette étape garantit que le contenu HTML aura les préfixes spécifiés pour les ressources externes.
```csharp
string externalImagesPrefix = "http://www.monsiteweb.com/images/id=";
string externalCssPrefix = "http://www.monsiteweb.com/css/id=";
```
Vous pouvez remplacer les URL par les préfixes souhaités. Ces préfixes seront utilisés à l'étape suivante pour personnaliser la sortie HTML.
## Étape 4 : Récupérer le contenu HTML
Maintenant que nos préfixes sont définis, nous pouvons récupérer le contenu HTML du document. Le`GetContent` méthode du`EditableDocument` class nous permet de spécifier l’image et les préfixes CSS.
```csharp
string prefixedHtmlContent = document.GetContent(externalImagesPrefix, externalCssPrefix);
Console.WriteLine("HTML content of the input document with custom image and stylesheet prefixes: {0}", prefixedHtmlContent);
```
Cet extrait de code récupère le contenu HTML avec les préfixes personnalisés et l'imprime sur la console. Vous pouvez poursuivre le traitement ou enregistrer ce contenu HTML selon vos besoins.
## Conclusion
Et voila! En suivant ces étapes, vous pouvez facilement récupérer le contenu HTML d'un document à l'aide de GroupDocs.Editor pour .NET, avec des préfixes personnalisés pour les images et les feuilles de style. Cet outil puissant simplifie la manipulation des documents, vous permettant de vous concentrer sur l'intégration transparente de l'édition de documents dans vos applications .NET.
 Pour des informations plus détaillées, consultez le[Documentation GroupDocs.Editor pour .NET](https://tutorials.groupdocs.com/editor/net/) . Si vous avez des questions ou avez besoin d'aide supplémentaire, n'hésitez pas à nous contacter sur le[forum d'entraide](https://forum.groupdocs.com/c/editor/20).
## FAQ
### Quels types de documents puis-je modifier avec GroupDocs.Editor pour .NET ?
GroupDocs.Editor prend en charge divers formats de documents, notamment Word, Excel, PowerPoint, PDF, etc.
### Comment puis-je obtenir un essai gratuit de GroupDocs.Editor pour .NET ?
 Vous pouvez obtenir un essai gratuit auprès du[Site Web GroupDocs](https://releases.groupdocs.com/).
### Puis-je personnaliser davantage le contenu HTML ?
Oui, vous pouvez modifier le contenu HTML récupéré selon vos besoins avant de le restituer ou de l'enregistrer.
### Est-il possible d'utiliser GroupDocs.Editor pour .NET avec d'autres langages .NET ?
Oui, vous pouvez l'utiliser avec n'importe quel langage compatible .NET comme VB.NET ou F#.
### Comment puis-je obtenir une licence temporaire pour GroupDocs.Editor pour .NET ?
 Vous pouvez obtenir une licence temporaire auprès du[page d'achat](https://purchase.groupdocs.com/temporary-license/).