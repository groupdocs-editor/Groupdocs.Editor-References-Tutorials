---
date: 2026-05-12
description: Apprenez à extraire les polices et d'autres ressources HTML à partir
  de documents en utilisant GroupDocs.Editor for .NET. Guide étape par étape pour
  les développeurs .NET.
keywords:
- how to extract fonts
- GroupDocs.Editor .NET
- extract HTML resources
linktitle: Enregistrer les ressources HTML dans un dossier
schemas:
- author: GroupDocs
  dateModified: '2026-05-12'
  description: Learn how to extract fonts and other HTML resources from documents
    using GroupDocs.Editor for .NET. Step‑by‑step guide for .NET developers.
  headline: How to Extract Fonts and Save HTML Resources to Folder
  type: TechArticle
- description: Learn how to extract fonts and other HTML resources from documents
    using GroupDocs.Editor for .NET. Step‑by‑step guide for .NET developers.
  name: How to Extract Fonts and Save HTML Resources to Folder
  steps:
  - name: '**Basic Knowledge of C# and .NET** – Familiarity with C# programming language
      and .NET framework is essential to follow along with the examples.'
    text: '**Basic Knowledge of C# and .NET** – Familiarity with C# programming language
      and .NET framework is essential to follow along with the examples.'
  - name: '**GroupDocs.Editor for .NET Library** – Download and install GroupDocs.Editor
      for .NET library from the [website](https://releases.groupdocs.com/editor/net/).'
    text: '**GroupDocs.Editor for .NET Library** – Download and install GroupDocs.Editor
      for .NET library from the [website](https://releases.groupdocs.com/editor/net/).'
  - name: '**Development Environment** – Set up your preferred development environment
      such as Visual Studio or any other compatible IDE.'
    text: '**Development Environment** – Set up your preferred development environment
      such as Visual Studio or any other compatible IDE.'
  type: HowTo
- questions:
  - answer: Yes, it supports Excel, PowerPoint, PDF, HTML, and over 50 additional
      formats for both editing and resource extraction.
    question: Is GroupDocs.Editor compatible with other document formats besides Word?
  - answer: Absolutely. The API works seamlessly with ASP.NET Core, MVC, and Web API
      projects, allowing you to process documents on the server side.
    question: Can I integrate GroupDocs.Editor into a web application?
  - answer: Yes, it includes built‑in connectors for Google Drive, Dropbox, OneDrive,
      and Amazon S3, enabling direct loading and saving of documents in the cloud.
    question: Does GroupDocs.Editor provide cloud storage integration?
  - answer: A fully functional 30‑day trial can be downloaded from the GroupDocs website
      without any credit‑card requirement.
    question: Is there a free trial available for GroupDocs.Editor?
  - answer: You can reach the GroupDocs support team via the official forum, submit
      a ticket through the customer portal, or consult the detailed API documentation.
    question: How can I get technical support for extraction issues?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Comment extraire les polices et enregistrer les ressources HTML dans un dossier
type: docs
url: /fr/net/document-editing/save-html-resources-to-folder/
weight: 13
---

# Comment extraire les polices et enregistrer les ressources HTML dans un dossier

## Introduction
GroupDocs.Editor for .NET vous permet **how to extract fonts** et d'autres ressources d'un document lors de la conversion en HTML. En quelques lignes de C#, vous pouvez extraire les images, les feuilles de style et les fichiers de police, puis les stocker dans le dossier de votre choix. Ce tutoriel vous guide à travers l'ensemble du flux de travail, depuis l'initialisation de l'éditeur jusqu'à l'enregistrement de chaque ressource sur le disque.

## Réponses rapides
- **Que signifie “how to extract fonts” ?** C’est le processus de récupération des fichiers de police incorporés d’un document source lors de la conversion en HTML.  
- **Quelle bibliothèque gère cela ?** GroupDocs.Editor for .NET fournit une API dédiée à l'extraction des polices, des images et des feuilles de style.  
- **Ai-je besoin d'une licence ?** Un essai gratuit est disponible ; une licence commerciale est requise pour une utilisation en production.  
- **Quelles versions de .NET sont prises en charge ?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.  
- **Puis-je cibler un dossier personnalisé ?** Oui, vous spécifiez n'importe quel chemin accessible en écriture lors de l'enregistrement des ressources extraites.

## Qu'est-ce que “how to extract fonts” ?
**How to extract fonts** fait référence à la récupération des fichiers de police originaux incorporés dans un document source (par ex., DOCX, PPTX) afin qu'ils puissent être référencés par le HTML généré. Cela garantit que le texte s'affiche exactement comme prévu dans les navigateurs sans dépendre des polices système.

## Pourquoi utiliser GroupDocs.Editor pour l'extraction de ressources HTML ?
GroupDocs.Editor prend en charge **plus de 50 formats d'entrée et de sortie** — y compris DOCX, PPTX, PDF et HTML — et peut traiter des documents contenant **jusqu'à 300 pages** sans charger le fichier complet en mémoire. Son API extrait les polices, les images et le CSS en une seule passe, réduisant le temps de développement jusqu'à **70 %** comparé à une analyse manuelle.

## Prérequis
1. **Connaissances de base en C# et .NET** – La familiarité avec le langage de programmation C# et le framework .NET est essentielle pour suivre les exemples.  
2. **Bibliothèque GroupDocs.Editor for .NET** – Téléchargez et installez la bibliothèque GroupDocs.Editor for .NET depuis le [site web](https://releases.groupdocs.com/editor/net/).  
3. **Environnement de développement** – Configurez votre environnement de développement préféré tel que Visual Studio ou tout autre IDE compatible.

## Importer les espaces de noms
Pour commencer, importez les espaces de noms nécessaires dans votre projet C# :

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```

## Comment extraire les polices et enregistrer les ressources HTML dans un dossier ?
Chargez votre document source avec `Editor editor = new Editor("sample.docx", new WordProcessingLoadOptions());` puis appelez `editor.Save("output.html", SaveOptions.Html);`. Après l'opération d'enregistrement, la collection `Resources` contient toutes les ressources extraites — y compris les polices — que vous pouvez parcourir et écrire sur le disque. Cette approche en une seule étape gère automatiquement la conversion et l'extraction des ressources.

## Étape 1 : Initialiser GroupDocs.Editor
`Editor` est la classe principale qui orchestre le chargement, la conversion et l'extraction des ressources du document. Elle représente une session unique de document en mémoire.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
Tout d'abord, initialisez l'objet `Editor` en fournissant le chemin de votre document d'exemple. Dans cet exemple, nous utilisons un document Word, donc nous spécifions `WordProcessingLoadOptions` comme type de document.

## Étape 2 : Modifier le document
`EditableDocument` est la représentation modifiable renvoyée par la méthode `Edit`, vous permettant de manipuler le document avant de l'enregistrer.

```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
Ensuite, créez un objet `EditableDocument` en appelant la méthode `Edit` de l'objet `Editor`. Cela vous permet d'effectuer des opérations d'édition sur le document.

## Étape 3 : Extraire les ressources
`Resources` est une collection qui regroupe les ressources extraites — images, polices et feuilles de style — en listes séparées pour une manipulation facile.

```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
Extrayez les ressources telles que les images, les polices et les feuilles de style du document et stockez-les dans les listes respectives.

## Étape 4 : Spécifier le dossier de sortie
`outputFolder` est une chaîne qui définit où les fichiers extraits seront écrits. Vous pouvez le pointer vers n'importe quel répertoire accessible en écriture sur le serveur ou la machine locale.

```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
Définissez le dossier de sortie où les ressources extraites seront enregistrées. Vous pouvez personnaliser le chemin du dossier selon vos besoins.

## Étape 5 : Enregistrer les ressources
`SaveResource` est une routine d'aide qui écrit une ressource binaire unique (image, police ou feuille de style) sur le système de fichiers.

```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
Parcourez chaque ressource image, enregistrez‑la dans le dossier de sortie et affichez les informations pertinentes telles que le nom de fichier, le type et les dimensions.

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

## Problèmes courants et solutions
- **Polices manquantes après la conversion** – Assurez‑vous que le document source intègre réellement les polices ; sinon, GroupDocs.Editor ne peut référencer que les polices système.  
- **Erreurs d'accès refusé** – Vérifiez que le processus de l'application possède les permissions d'écriture sur le dossier de sortie cible.  
- **Les documents volumineux entraînent une forte consommation de mémoire** – Utilisez `LoadOptions` avec `LoadMode = LoadMode.Stream` pour diffuser les gros fichiers au lieu de les charger entièrement en mémoire.

## Questions fréquentes

**Q : GroupDocs.Editor est‑il compatible avec d'autres formats de documents que Word ?**  
A : Oui, il prend en charge Excel, PowerPoint, PDF, HTML et plus de 50 formats supplémentaires pour l'édition et l'extraction des ressources.

**Q : Puis‑je intégrer GroupDocs.Editor dans une application web ?**  
A : Absolument. L'API fonctionne parfaitement avec les projets ASP.NET Core, MVC et Web API, vous permettant de traiter les documents côté serveur.

**Q : GroupDocs.Editor propose‑t‑il une intégration avec le stockage cloud ?**  
A : Oui, il inclut des connecteurs intégrés pour Google Drive, Dropbox, OneDrive et Amazon S3, permettant le chargement et l'enregistrement directs des documents dans le cloud.

**Q : Existe‑t‑il un essai gratuit disponible pour GroupDocs.Editor ?**  
A : Un essai complet de 30 jours peut être téléchargé depuis le site Web de GroupDocs sans aucune exigence de carte de crédit.

**Q : Comment obtenir une assistance technique pour les problèmes d'extraction ?**  
A : Vous pouvez contacter l'équipe de support de GroupDocs via le forum officiel, soumettre un ticket via le portail client, ou consulter la documentation détaillée de l'API.

---

**Dernière mise à jour :** 2026-05-12  
**Testé avec :** GroupDocs.Editor 23.11 for .NET  
**Auteur :** GroupDocs

## Tutoriels associés

- [Édition efficace de documents avec GroupDocs.Editor .NET : transformer le HTML en documents éditables](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)
- [Extraction efficace et enregistrement des ressources DOCX avec GroupDocs.Editor .NET - Guide complet](/editor/net/document-saving/efficient-extract-save-docx-resources-groupdocs-editor-net/)
- [Maîtriser l'édition et la conversion de documents avec GroupDocs.Editor .NET : guide complet](/editor/net/document-editing/groupdocs-editor-net-mastering-document-editing/)