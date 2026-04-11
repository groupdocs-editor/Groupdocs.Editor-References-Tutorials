---
date: '2026-04-11'
description: Apprenez à créer un document éditable avec GroupDocs.Editor pour .NET
  et à enregistrer le document au format HTML de manière efficace.
keywords:
- create editable document
- extract images from document
- save document as html
title: Créer un document modifiable avec GroupDocs.Editor .NET
type: docs
url: /fr/net/document-editing/groupdocs-editor-net-edit-manage-documents-guide/
weight: 1
---

# Créer un document modifiable avec GroupDocs.Editor .NET

Dans l'ère numérique actuelle, **créer un document modifiable** est une exigence fondamentale pour tout flux de travail moderne. Que vous construisiez un éditeur collaboratif, un système de gestion de contenu ou un outil de génération de rapports automatisé, la capacité de modifier et d'enregistrer des fichiers HTML programmatiquement peut faire gagner d'innombrables heures. Ce tutoriel vous montre comment **créer des instances de document modifiable**, extraire les ressources et **enregistrer le document au format HTML** en utilisant GroupDocs.Editor pour .NET.

## Réponses rapides
- **Que signifie « créer un document modifiable » ?** Cela signifie charger un fichier source dans un objet `EditableDocument` de GroupDocs.Editor que vous pouvez modifier programmatiquement.  
- **Quels formats puis‑je convertir en HTML ?** Word, Excel, PowerPoint et de nombreux autres formats Office sont pris en charge.  
- **Comment extraire les images d'un document ?** Utilisez la collection `EditableDocument.Images`.  
- **Puis‑je générer une chaîne HTML unique avec toutes les ressources intégrées ?** Oui—appelez `GetEmbeddedHtml()`.  
- **Ai‑je besoin d'une licence pour la production ?** Un essai fonctionne pour l'évaluation ; une licence permanente est requise pour une utilisation commerciale.

## Qu’est‑ce que « créer un document modifiable » ?
Créer un document modifiable signifie charger un fichier source (par exemple, un .docx) dans GroupDocs.Editor, qui renvoie un objet `EditableDocument`. Cet objet expose le balisage HTML du document, les images, les polices et le CSS, vous permettant de modifier le contenu, de remplacer les ressources ou d'intégrer le tout dans une page web.

## Pourquoi utiliser GroupDocs.Editor .NET pour cette tâche ?
- **API complète** – Gère Word, Excel, PowerPoint et plus encore.  
- **Extraction de ressources** – Extrait les images, les polices et les feuilles de style avec des propriétés simples.  
- **Génération de HTML intégré** – Produit une chaîne HTML unique contenant toutes les ressources, idéale pour les e‑mails ou les applications monopage.  
- **Axé sur la performance** – Libère les objets rapidement et utilise des modèles asynchrones lorsque nécessaire.

## Prérequis
- **Environnement .NET** : Configurez votre environnement de développement pour les applications .NET.
- **Bibliothèques et dépendances** :
  - Installez GroupDocs.Editor en utilisant l'une de ces méthodes :
    - **.NET CLI**
      ```bash
      dotnet add package GroupDocs.Editor
      ```
    - **Package Manager**
      ```powershell
      Install-Package GroupDocs.Editor
      ```
    - **NuGet Package Manager UI** : Recherchez et installez la dernière version.
- **Prérequis de connaissances** : La familiarité avec la programmation C# et les concepts de base de la gestion de documents est recommandée.

## Configuration de GroupDocs.Editor pour .NET
### Instructions d'installation
Pour commencer, configurez GroupDocs.Editor dans votre projet :
1. **Installer via .NET CLI** :
   ```bash
   dotnet add package GroupDocs.Editor
   ```
2. **Utiliser le Package Manager** :
   - Ouvrez la console du Package Manager et exécutez :
     ```powershell
     Install-Package GroupDocs.Editor
     ```
3. **NuGet Package Manager UI** :
   - Accédez à NuGet, recherchez "GroupDocs.Editor" et installez-le.

### Acquisition de licence
- **Essai gratuit & licence temporaire** :
  Commencez avec un essai gratuit en téléchargeant depuis [GroupDocs releases](https://releases.groupdocs.com/editor/net/). Pour des tests prolongés, demandez une licence temporaire sur la [page d'achat](https://purchase.groupdocs.com/temporary-license).

### Initialisation et configuration de base
Voici comment initialiser GroupDocs.Editor dans votre application :
```csharp
using System;
using GroupDocs.Editor;

string inputFilePath = "YOUR_DOCUMENT_DIRECTORY"; // Replace with your actual document path
Editor editor = new Editor(inputFilePath, new WordProcessingLoadOptions());
```

## Comment créer un document modifiable avec GroupDocs.Editor .NET
### Création d'une instance EditableDocument
**Aperçu** : Chargez et modifiez des documents en créant une instance `EditableDocument`.

#### Chargement d'un document
```csharp
using GroupDocs.Editor.Options;

// Load your document with appropriate options
Editor editor = new Editor(inputFilePath, new WordProcessingLoadOptions());

// Create EditableDocument from the loaded file
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```

## Comment générer du HTML intégré
### Génération de HTML intégré à partir d'EditableDocument
**Aperçu** : Convertissez un document complet en une chaîne HTML intégrée unique contenant les feuilles de style et les ressources.
```csharp
using System.Collections.Generic;
using GroupDocs.Editor.HtmlCss.Resources;

// Generate embedded HTML
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```

## Comment extraire les images d'un document
### Extraction des ressources depuis EditableDocument
**Aperçu** : Récupérez les images, les polices, le CSS et d'autres ressources de votre document.
```csharp
List<IImageResource> allImages = beforeEdit.Images;
List<FontResourceBase> allFonts = beforeEdit.Fonts;
List<CssText> allStylesheets = beforeEdit.Css;
List<IHtmlResource> allResources = beforeEdit.AllResources;
```

## Comment extraire les polices d'un document
*Le même bloc de code ci‑dessus montre également comment extraire les ressources de police via `beforeEdit.Fonts`.*

## Comment obtenir du contenu HTML pur
### Obtention du contenu HTML depuis EditableDocument
**Aperçu** : Extrayez le contenu HTML pur sans ressources intégrées.
```csharp
string htmlMarkup = beforeEdit.GetContent();
```

## Comment ajuster les liens externes dans le contenu HTML
### Ajustement des liens externes dans le contenu HTML
**Aperçu** : Modifiez les liens externes pour les images, le CSS et les polices en utilisant des préfixes personnalisés.
```csharp
using System.Collections.Generic;

// Define custom handlers for resource URLs
string customImagesRequesthandlerUri = "http://example.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://example.com/CssHandler/id=";

// Adjust HTML content with prefixed links
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```

## Comment enregistrer le document au format HTML
### Enregistrement d'EditableDocument en fichier HTML
**Aperçu** : Enregistrez le document modifié sur le disque au format HTML.
```csharp
using System.IO;

string htmlFilePath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "document.html"); // Adjust the output path
beforeEdit.Save(htmlFilePath);
```

## Libération et gestion des événements pour EditableDocument
**Aperçu** : Gérez la libération des ressources et traitez les événements liés au cycle de vie du document.
```csharp
Console.WriteLine("beforeEdit variable of EditableDocument type is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");

// Subscribe to the disposing event
EventHandler someMethod = delegate {
    Console.WriteLine("Disposing event was spotted!");
};
beforeEdit.Disposed += someMethod;
```

## Comment créer un document modifiable à partir de contenu HTML
### Création d'EditableDocument à partir de contenu HTML
**Aperçu** : Reconstruisez une instance `EditableDocument` à partir d'un contenu HTML existant.
```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);

// Dispose resources once done
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```

## Applications pratiques
GroupDocs.Editor .NET peut être exploité dans de nombreux scénarios réels :
- **Édition collaborative** : Facilitez l'édition fluide de documents par plusieurs utilisateurs.  
- **Publication web** : Convertissez les documents en formats adaptés au web pour la visualisation et l'interaction en ligne.  
- **Systèmes de gestion de contenu** : Intégrez avec les plateformes CMS pour permettre des mises à jour dynamiques du contenu.  
- **Génération automatisée de rapports** : Automatisez la génération et le formatage de rapports à partir de diverses sources de données.

## Considérations de performance
Pour optimiser les performances de GroupDocs.Editor .NET :
- Gérez la mémoire efficacement en libérant les objets rapidement après utilisation.  
- Réduisez les temps de chargement des ressources en optimisant les chemins de fichiers et les URL.  
- Utilisez le traitement asynchrone lorsque c'est possible pour améliorer la réactivité de l'application.

## Problèmes courants et solutions
- **Les gros fichiers entraînent une forte utilisation de la mémoire** – Libérez les objets `EditableDocument` dès que vous avez terminé leur traitement.  
- **Liens d'images cassés après conversion** – Assurez‑vous d'utiliser les URI corrects du gestionnaire de ressources lors de l'appel à `GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri)`.  
- **Polices manquantes dans le HTML généré** – Vérifiez que le document source intègre les polices requises ou qu'elles sont disponibles sur le serveur.

## Questions fréquemment posées

**Q : GroupDocs.Editor .NET est‑il compatible avec tous les formats de documents ?**  
R : GroupDocs.Editor prend en charge un large éventail de formats, y compris Word, Excel, PowerPoint et bien d'autres, vous offrant une flexibilité pour différents cas d'utilisation.

**Q : Comment gérer efficacement les gros fichiers avec GroupDocs.Editor ?**  
R : Utilisez les API asynchrones lorsqu'elles sont disponibles, traitez les fichiers par morceaux lorsque possible, et libérez toujours rapidement les objets `EditableDocument` et `Editor` pour libérer la mémoire.

**Q : Puis‑je intégrer GroupDocs.Editor à des solutions de stockage cloud ?**  
R : Oui, vous pouvez vous connecter à Azure Blob Storage, Amazon S3, Google Cloud Storage ou tout autre fournisseur cloud en transmettant les flux de fichiers au constructeur `Editor`.

**Q : Quelles sont les options de licence pour GroupDocs.Editor ?**  
R : Vous pouvez commencer avec un essai gratuit ou demander une licence temporaire pour l'évaluation. Les déploiements en production nécessitent une licence payante.

**Q : Où puis‑je obtenir de l'aide en cas de problème ?**  
R : Le [Forum de support GroupDocs](https://forum.groupdocs.com) est disponible pour l'assistance, et vous pouvez également contacter directement l'équipe de support GroupDocs.

---

**Dernière mise à jour :** 2026-04-11  
**Testé avec :** GroupDocs.Editor 23.12 pour .NET  
**Auteur :** GroupDocs  

---