---
date: 2026-03-14
description: Apprenez à extraire des images d’un DOCX, à convertir un DOCX en HTML
  et à enregistrer le document au format HTML en utilisant GroupDocs.Editor pour .NET.
linktitle: Extract Images from DOCX – Advanced Editable Document Usage
second_title: GroupDocs.Editor .NET API
title: Extraire des images d’un DOCX – Utilisation avancée de documents éditables
type: docs
url: /fr/net/document-editing/advanced-usage-of-editable-documents/
weight: 11
---

?" Keep phrase unchanged.

Now we need to ensure we keep code block placeholders exactly as they appear, each on its own line.

Let's produce final French translation.

Be careful with bullet lists: maintain dash and spacing.

Let's start.

We'll produce the content.

# Extract Images from DOCX – Advanced Editable Document Usage

Si vous êtes un développeur .NET souhaitant **extraire des images d’un DOCX** et améliorer vos capacités d’édition de documents, GroupDocs.Editor for .NET propose une suite d’outils puissante. Ce guide complet vous accompagnera pas à pas dans l’utilisation avancée des documents éditables avec GroupDocs.Editor, en détaillant chaque étape afin que vous puissiez exploiter tout son potentiel.

## Quick Answers
- **Comment extraire des images d’un fichier DOCX ?** Utilisez `EditableDocument.Images` après avoir chargé le document avec `Editor`.
- **Puis‑je convertir un DOCX en HTML avec des ressources intégrées ?** Oui — appelez `EditableDocument.GetEmbeddedHtml()` ou `GetContent()` pour obtenir le balisage HTML.
- **Quelle méthode enregistre le document modifié au format HTML ?** `EditableDocument.Save(htmlFilePath)` crée un fichier HTML avec un dossier de ressources.
- **Est‑il possible d’extraire les polices d’un document Word ?** Utilisez `EditableDocument.Fonts` pour récupérer toutes les ressources de police.
- **Ai‑je besoin d’une licence pour une utilisation en production ?** Une licence valide GroupDocs.Editor est requise ; un essai gratuit est disponible.

## What is **extract images from docx**?
Extraire des images d’un fichier DOCX signifie récupérer programmatiquement chaque image intégrée dans le document Word afin de les réutiliser, les modifier ou les stocker séparément. GroupDocs.Editor expose la collection `Images` sur une instance `EditableDocument`, ce qui rend cette tâche simple.

## Why use GroupDocs.Editor for this workflow?
- **Contrôle total** sur les ressources du document (images, polices, CSS) sans manipulation manuelle de ZIP.  
- **Conversion fluide** de DOCX en HTML tout en conservant la mise en page et le style.  
- **Extraction facile des ressources** pour la gestion personnalisée des images, l’intégration de polices ou la diffusion via CDN.  
- **Modèle de libération robuste** qui évite les fuites de mémoire dans les services à long terme.

## Prerequisites
- Visual Studio installé sur votre machine de développement.  
- .NET Framework compatible avec GroupDocs.Editor.  
- Bibliothèque GroupDocs.Editor for .NET. Vous pouvez [download it here](https://releases.groupdocs.com/editor/net/).  
- Une licence valide GroupDocs.Editor. Vous pouvez obtenir un [free trial](https://releases.groupdocs.com/) ou acheter une [temporary license](https://purchase.groupdocs.com/temporary-license/).

## Import Namespaces
Pour commencer, assurez‑vous d’importer les espaces de noms nécessaires dans votre projet .NET :

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

## Step 1: Creating an EditableDocument Instance
Tout d’abord, créez une instance de `EditableDocument` en chargeant et en éditant un document d’entrée d’un format pris en charge.

```csharp
string inputFilePath = "YourSampleDocument.docx";
Editor editor = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```

Dans cette étape, nous chargeons le document d’entrée et le préparons à l’édition.

## How to **extract images from DOCX**?
Ci‑dessous, nous explorons les capacités d’extraction des ressources, en commençant par le besoin le plus fréquent — récupérer toutes les images d’un fichier Word.

## Step 2: Extracting Document Resources
`EditableDocument` contient diverses ressources qui peuvent être extraites et manipulées. Décomposons‑les :

### Step 2.1: Extract Entire Document as HTML
Vous pouvez générer une chaîne unique contenant l’ensemble du document avec toutes ses ressources intégrées sous forme de HTML.

```csharp
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```

Cette chaîne sera assez volumineuse car elle inclut les feuilles de style, les images et les polices encodées en base64.

### Step 2.2: Extract All Images *(primary keyword in action)*
Extrayez toutes les images du document — c’est le cœur de **extract images from docx**.

```csharp
List<IImageResource> allImages = beforeEdit.Images;
```

### Step 2.3: Extract All Fonts *(secondary keyword)*
Si vous avez également besoin de **extract fonts from word**, utilisez l’appel suivant :

```csharp
List<FontResourceBase> allFonts = beforeEdit.Fonts;
```

### Step 2.4: Extract All Stylesheets
Extrayez toutes les feuilles de style au format texte.

```csharp
List<CssText> allStylesheets = beforeEdit.Css;
```

### Step 2.5: Gather All Resources
Rassemblez toutes les ressources en un seul appel.

```csharp
List<IHtmlResource> allResources = beforeEdit.AllResources;
```

Cela comprend les images, les polices et les feuilles de style.

### Step 2.6: Obtain HTML Markup
Obtenez le balisage HTML du document sans les ressources intégrées.

```csharp
string htmlMarkup = beforeEdit.GetContent();
```

## How to **convert docx to html** with custom handling?
Parfois, vous devez ajuster les liens externes afin qu’ils pointent vers vos propres gestionnaires de ressources.

## Step 3: Adjusting External Links
### Step 3.1: Prepare Custom Prefixes
Préparez les préfixes qui seront ajoutés aux liens externes d’origine.

```csharp
string customImagesRequesthandlerUri = "http://example.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://example.com/CssHandler/id=";
string customFontsRequesthandlerUri = "http://example.com/FontsHandler/id=";
```

### Step 3.2: Generate Prefixed HTML Markup
Générez le balisage HTML avec les liens ajustés.

```csharp
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```

### Step 3.3: Obtain Body-Only HTML Content
Certains éditeurs WYSIWYG ne gèrent que le HTML pur sans en‑têtes.

```csharp
string onlyBodyContent = beforeEdit.GetBodyContent();
```

### Step 3.4: Prefixed Body-Only Content
Générez le contenu uniquement du corps avec des préfixes d’image personnalisés.

```csharp
string prefixedBodyContent = beforeEdit.GetBodyContent(customImagesRequesthandlerUri);
```

### Step 3.5: Extract Stylesheets
Extrayez les feuilles de style utilisées dans le document.

```csharp
List<string> stylesheets = beforeEdit.GetCssContent();
```

### Step 3.6: Prefixed Stylesheets
Extrayez les feuilles de style avec des préfixes personnalisés.

```csharp
List<string> prefixedStylesheets = beforeEdit.GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri);
```

## How to **save document as html** correctly?
## Step 4: Save Document as HTML
Enregistrez le document modifié sous forme de fichier HTML, incluant ses ressources.

```csharp
string htmlFilePath = Path.Combine("output", Path.GetFileNameWithoutExtension(inputFilePath) + ".html");
beforeEdit.Save(htmlFilePath);
```

Cette méthode crée un répertoire séparé pour les ressources telles que les feuilles de style, les images et les polices.

## Step 5: Disposing of EditableDocument
`EditableDocument` implémente `IDisposable` et permet de vérifier si l’instance a été libérée.

```csharp
Console.WriteLine("EditableDocument is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");
```

### Step 5.1 Handling Dispose Event
Vous pouvez également vous abonner à l’événement de libération.

```csharp
EventHandler someMethod = delegate { Console.WriteLine("Disposing event was spotted!"); };
beforeEdit.Disposed += someMethod;
```

## Step 6: Creating EditableDocument from HTML
Créez une instance de `EditableDocument` à partir d’un document HTML.

### Step 6.1: From HTML File

```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
```

### Step 6.2: From HTML Markup

```csharp
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);
```

Ces instances (`afterEditFromFile` et `afterEditFromMarkup`) sont identiques à l’originale (`beforeEdit`).

## Step 7: Manual Disposal
Libérez manuellement vos instances `EditableDocument`.

```csharp
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```

Cela garantit un nettoyage correct des ressources.

## Common Issues and Solutions
- **Images not appearing after extraction :** Vérifiez que le document contient réellement des images intégrées et que vous accédez à `beforeEdit.Images` après avoir appelé `Edit`.  
- **Fonts missing in HTML output :** Assurez‑vous d’appeler `GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri)` pour intégrer correctement les URL des polices.  
- **Large HTML strings causing memory pressure :** Utilisez `GetContent()` pour obtenir le balisage sans les ressources intégrées et servez les images/CSS depuis des fichiers séparés.

## Frequently Asked Questions

**Q : Quels formats GroupDocs.Editor prend‑il en charge ?**  
R : GroupDocs.Editor prend en charge DOCX, XLSX, PPTX et de nombreux autres formats bureautiques populaires.

**Q : Puis‑je utiliser GroupDocs.Editor sans licence ?**  
R : Oui, vous pouvez l’utiliser avec un [free trial](https://releases.groupdocs.com/) ou une [temporary license](https://purchase.groupdocs.com/temporary-license/).

**Q : Comment extraire des ressources spécifiques d’un document ?**  
R : Utilisez les collections `Images`, `Fonts` et `Css` sur l’instance `EditableDocument`.

**Q : Est‑il possible d’ajuster les liens dans le rendu HTML ?**  
R : Oui, transmettez des préfixes URI personnalisés à `GetContent` ou `GetBodyContent` pour réécrire les liens d’image, de CSS et de police.

**Q : Comment enregistrer un document modifié au format HTML ?**  
R : Appelez la méthode `Save` sur l’instance `EditableDocument`, en fournissant un chemin de fichier se terminant par `.html`.

---

**Last Updated:** 2026-03-14  
**Tested With:** GroupDocs.Editor for .NET (latest release)  
**Author:** GroupDocs