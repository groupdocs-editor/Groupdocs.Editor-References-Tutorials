---
title: Utilisation avancée des documents modifiables
linktitle: Utilisation avancée des documents modifiables
second_title: API GroupDocs.Editor .NET
description: Découvrez l'utilisation avancée de GroupDocs.Editor pour .NET en créant, modifiant et extrayant des ressources à partir de documents par programmation.
type: docs
weight: 11
url: /fr/net/document-editing/advanced-usage-of-editable-documents/
---
## Introduction
Si vous êtes un développeur .NET cherchant à améliorer vos capacités d'édition de documents, GroupDocs.Editor for .NET propose une puissante suite d'outils. Ce guide complet vous guidera dans l'utilisation avancée des documents modifiables à l'aide de GroupDocs.Editor, en décomposant chaque étape en détail pour vous assurer que vous pouvez exploiter tout son potentiel.
## Conditions préalables
Avant de plonger dans les fonctionnalités avancées, assurez-vous de disposer des éléments suivants :
- Visual Studio installé sur votre machine de développement.
- .NET Framework compatible avec GroupDocs.Editor.
-  GroupDocs.Editor pour la bibliothèque .NET. Tu peux[Télécharger les ici](https://releases.groupdocs.com/editor/net/).
-  Une licence GroupDocs.Editor valide. Vous pouvez obtenir un[essai gratuit](https://releases.groupdocs.com/) ou acheter un[permis temporaire](https://purchase.groupdocs.com/temporary-license/).
## Importer des espaces de noms
Pour commencer, assurez-vous d'importer les espaces de noms nécessaires dans votre projet .NET :
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```
## Étape 1 : Création d'une instance EditableDocument
 Tout d'abord, vous devez créer une instance de`EditableDocument` en chargeant et en éditant un document d'entrée d'un format pris en charge.
```csharp
string inputFilePath = "YourSampleDocument.docx";
Editor editor = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```
Dans cette étape, nous chargeons le document d'entrée et le préparons pour l'édition.
## Étape 2 : Extraction des ressources documentaires
 Le`EditableDocument` contient diverses ressources qui peuvent être extraites et manipulées. Décomposons-les :
### Étape 2.1 : extraire l'intégralité du document au format HTML
Vous pouvez générer une seule chaîne contenant l'intégralité du document avec toutes ses ressources intégrées au format HTML.
```csharp
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```
Cette chaîne sera assez volumineuse car elle comprend des feuilles de style, des images et des polices codées en base64.
### Étape 2.2 : Extraire toutes les images
Extrayez toutes les images du document.
```csharp
List<IImageResource> allImages = beforeEdit.Images;
```
### Étape 2.3 : Extraire toutes les polices
Extrayez toutes les polices utilisées dans le document.
```csharp
List<FontResourceBase> allFonts = beforeEdit.Fonts;
```
### Étape 2.4 : Extraire toutes les feuilles de style
Extrayez toutes les feuilles de style dans un format textuel.
```csharp
List<CssText> allStylesheets = beforeEdit.Css;
```
### Étape 2.5 : Rassemblez toutes les ressources
Rassemblez toutes les ressources en un seul appel.
```csharp
List<IHtmlResource> allResources = beforeEdit.AllResources;
```
Cela inclut les images, les polices et les feuilles de style.
### Étape 2.6 : Obtenir le balisage HTML
Obtenez le balisage HTML du document sans ressources intégrées.
```csharp
string htmlMarkup = beforeEdit.GetContent();
```
## Étape 3 : Ajustement des liens externes
Parfois, vous devez ajuster les liens externes pour pointer vers un gestionnaire de ressources personnalisé. Voici comment procéder :
### Étape 3.1 : Préparer des préfixes personnalisés
Préparez des préfixes qui ajouteront les liens externes d'origine.
```csharp
string customImagesRequesthandlerUri = "http://exemple.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://example.com/CssHandler/id=";
string customFontsRequesthandlerUri = "http://example.com/FontsHandler/id=";
```
### Étape 3.2 : Générer un balisage HTML préfixé
Générez un balisage HTML avec des liens ajustés.
```csharp
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```
### Étape 3.3 : Obtenir du contenu HTML contenant uniquement le corps
Certains éditeurs WYSIWYG ne gèrent que le balisage HTML pur sans en-têtes.
```csharp
string onlyBodyContent = beforeEdit.GetBodyContent();
```
### Étape 3.4 : Contenu préfixé réservé au corps
Générez du contenu composé uniquement de corps avec des préfixes d'image personnalisés.
```csharp
string prefixedBodyContent = beforeEdit.GetBodyContent(customImagesRequesthandlerUri);
```
### Étape 3.5 : Extraire les feuilles de style
Extrayez les feuilles de style utilisées dans le document.
```csharp
List<string> stylesheets = beforeEdit.GetCssContent();
```
### Étape 3.6 : Feuilles de style préfixées
Extrayez les feuilles de style avec des préfixes personnalisés.
```csharp
List<string> prefixedStylesheets = beforeEdit.GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri);
```
## Étape 4 : Enregistrer le document au format HTML
Enregistrez le document modifié sous forme de fichier HTML, y compris ses ressources.
```csharp
string htmlFilePath = Path.Combine("output", Path.GetFileNameWithoutExtension(inputFilePath) + ".html");
beforeEdit.Save(htmlFilePath);
```
Cette méthode crée un répertoire distinct pour les ressources telles que les feuilles de style, les images et les polices.
## Étape 5 : élimination du document modifiable
 Implémentations de EditableDocument`IDisposable` et offre la possibilité de vérifier si l'instance est supprimée.
```csharp
Console.WriteLine("EditableDocument is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");
```
### Étape 5.1 Gestion de l'événement Dispose
Vous pouvez également vous inscrire à l'événement de disposition.
```csharp
EventHandler someMethod = delegate { Console.WriteLine("Disposing event was spotted!"); };
beforeEdit.Disposed += someMethod;
```
## Étape 6 : Création d'un document modifiable à partir de HTML
Créez une instance de EditableDocument à partir d'un document HTML.
### Étape 6.1 : À partir d'un fichier HTML
```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
```
### Étape 6.2 : à partir du balisage HTML
```csharp
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);
```
Ces instances (afterEditFromFile et afterEditFromMarkup) sont identiques à l'original (beforeEdit).
## Étape 7 : Élimination manuelle
Supprimez manuellement vos instances EditableDocument.
```csharp
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```
Cela garantit un nettoyage approprié des ressources.
## Conclusion
GroupDocs.Editor pour .NET fournit des outils robustes pour éditer des documents par programmation. En suivant ce guide étape par étape, vous pouvez gérer efficacement le contenu, les ressources et les formats de sortie des documents. Que vous intégriez des ressources, ajustiez des liens externes ou convertissiez des documents au format HTML, GroupDocs.Editor vous offre les fonctionnalités nécessaires à la manipulation avancée de documents.
## FAQ
### Quels formats GroupDocs.Editor prend-il en charge ?
GroupDocs.Editor prend en charge divers formats, notamment DOCX, XLSX, PPTX, etc.
### Puis-je utiliser GroupDocs.Editor sans licence ?
 Oui, vous pouvez l'utiliser avec un[essai gratuit](https://releases.groupdocs.com/) ou un[permis temporaire](https://purchase.groupdocs.com/temporary-license/).
### Comment extraire des ressources spécifiques d’un document ?
 Vous pouvez extraire des images, des polices et des feuilles de style à l'aide des méthodes fournies telles que`Images`, `Fonts` , et`Css`.
### Est-il possible d'ajuster les liens dans la sortie HTML ?
Oui, vous pouvez ajuster les liens externes en spécifiant des préfixes personnalisés pour les images, CSS et polices.
### Comment enregistrer un document modifié sous forme de fichier HTML ?
 Utilisez le`Save` méthode du`EditableDocument`classe pour enregistrer le document sous forme de fichier HTML, y compris ses ressources.