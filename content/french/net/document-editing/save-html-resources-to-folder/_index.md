---
title: Enregistrer les ressources HTML dans un dossier
linktitle: Enregistrer les ressources HTML dans un dossier
second_title: API GroupDocs.Editor .NET
description: Découvrez comment extraire des ressources HTML à partir de documents à l'aide de Groupdocs.Editor for .NET. Ce didacticiel complet fournit des conseils étape par étape aux développeurs.
weight: 13
url: /fr/net/document-editing/save-html-resources-to-folder/
type: docs
---
# Enregistrer les ressources HTML dans un dossier

## Introduction
Groupdocs.Editor for .NET est un outil puissant qui permet aux développeurs de manipuler et de convertir des documents de manière transparente dans leurs applications .NET. Que vous ayez besoin d'extraire des ressources HTML d'un document ou d'effectuer des tâches d'édition avancées, Groupdocs.Editor simplifie le processus grâce à son API intuitive et sa documentation complète.
## Conditions préalables
Avant de plonger dans le didacticiel, assurez-vous d'avoir les prérequis suivants :
1. Connaissance de base de C# et .NET : Une connaissance du langage de programmation C# et du framework .NET est essentielle pour suivre les exemples.
2.  Groupdocs.Editor for .NET Library : téléchargez et installez la bibliothèque Groupdocs.Editor for .NET à partir du[site web](https://releases.groupdocs.com/editor/net/).
3. Environnement de développement : configurez votre environnement de développement préféré tel que Visual Studio ou tout autre IDE compatible.

## Importer des espaces de noms
Pour commencer, importez les espaces de noms nécessaires dans votre projet C# :
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```
##Maintenant, décomposons le processus d'enregistrement des ressources HTML dans un dossier à l'aide de Groupdocs.Editor for .NET en plusieurs étapes :
## Étape 1 : initialiser Groupdocs.Editor
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
 Tout d'abord, initialisez le`Editor`objet en fournissant le chemin d’accès à votre exemple de document. Dans cet exemple, nous utilisons un document Word, nous précisons donc`WordProcessingLoadOptions` comme type de document.
## Étape 2 : Modifier le document
```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
 Ensuite, créez un`EditableDocument` objet en appelant le`Edit` méthode du`Editor` objet. Cela vous permet d'effectuer des opérations d'édition sur le document.
## Étape 3 : Extraire les ressources
```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
Extrayez des ressources telles que des images, des polices et des feuilles de style du document et stockez-les dans les listes respectives.
## Étape 4 : Spécifier le dossier de sortie
```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
Définissez le dossier de sortie dans lequel les ressources extraites seront enregistrées. Vous pouvez personnaliser le chemin du dossier selon vos besoins.
## Étape 5 : Enregistrer les ressources
```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
Parcourez chaque ressource d'image, enregistrez-la dans le dossier de sortie et affichez les informations pertinentes telles que le nom de fichier, le type et les dimensions.
```csharp
		foreach (FontResourceBase oneFont in fonts)
		{
			Console.WriteLine("Saving {0} of {1} type",
				oneFont.FilenameWithExtension, oneFont.Type.FormalName);
			oneFont.Save(Path.Combine(outputFolder, oneFont.FilenameWithExtension));
		}
```
De même, enregistrez chaque ressource de police dans le dossier de sortie.
```csharp
		foreach (CssText oneStylesheet in stylesheets)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} encoding",
				oneStylesheet.FilenameWithExtension, oneStylesheet.Type.FormalName, oneStylesheet.Encoding);
			oneStylesheet.Save(Path.Combine(outputFolder, oneStylesheet.FilenameWithExtension));
		}
	}
}
```
Enfin, enregistrez chaque feuille de style dans le dossier de sortie et terminez le processus d'édition.

## Conclusion
En conclusion, Groupdocs.Editor for .NET fournit une solution pratique pour gérer et manipuler des documents par programmation au sein d'applications .NET. En suivant ce didacticiel, vous pouvez facilement extraire des ressources HTML à partir de documents et personnaliser le processus en fonction de vos besoins spécifiques.
## FAQ
### Groupdocs.Editor est-il compatible avec d’autres formats de documents que Word ?
Oui, Groupdocs.Editor prend en charge un large éventail de formats de documents, notamment Excel, PowerPoint, PDF, etc.
### Puis-je intégrer Groupdocs.Editor dans mon application web ?
Absolument, Groupdocs.Editor offre une intégration transparente avec les applications Web développées sur le framework .NET.
### Groupdocs.Editor prend-il en charge les services de stockage cloud ?
Oui, Groupdocs.Editor prend en charge l'intégration avec les services de stockage cloud populaires tels que Google Drive, Dropbox et Microsoft OneDrive.
### Existe-t-il un essai gratuit disponible pour Groupdocs.Editor ?
Oui, vous pouvez bénéficier d'un essai gratuit de Groupdocs.Editor sur le site Web.
### Comment puis-je obtenir une assistance technique pour Groupdocs.Editor ?
Pour obtenir une assistance technique et un support communautaire, vous pouvez visiter le forum Groupdocs.Editor.