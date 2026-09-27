---
date: 2026-09-26
description: Apprenez à gérer le préfixe CSS et à extraire le contenu CSS en utilisant
  GroupDocs.Editor for .NET dans ce tutoriel détaillé pas à pas.
keywords:
- handle css prefix
- extract css content
- edit document css
- prepend url to css
lastmod: 2026-09-26
linktitle: Gérer le contenu CSS avec préfixe
og_description: Découvrez comment gérer le préfixe CSS et extraire le contenu CSS
  avec GroupDocs.Editor for .NET. Suivez un guide pas à pas pour préfixer les URL
  des ressources CSS et récupérer les feuilles de style.
og_image_alt: Developer guide showing css prefix handling with GroupDocs.Editor for
  .NET
og_title: Comment gérer le préfixe CSS dans GroupDocs.Editor for .NET
schemas:
- author: GroupDocs
  dateModified: '2026-09-26'
  description: Learn how to handle css prefix and extract css content using GroupDocs.Editor
    for .NET in this detailed step‑by‑step tutorial.
  headline: How to handle css prefix in GroupDocs.Editor for .NET
  type: TechArticle
- questions:
  - answer: Yes, GroupDocs.Editor for .NET supports PDF, Word, Excel, PowerPoint,
      and many other formats.
    question: Can I use GroupDocs.Editor for .NET with other document formats?
  - answer: Absolutely! You can start your free trial on the [GroupDocs free trial
      page](https://releases.groupdocs.com/).
    question: Is there a free trial available for GroupDocs.Editor for .NET?
  - answer: You can obtain a temporary license from the [temporary license page](https://purchase.groupdocs.com/temporary-license/).
    question: How do I get a temporary license for GroupDocs.Editor for .NET?
  - answer: Detailed documentation is available on the [GroupDocs.Editor for .NET
      documentation site](https://tutorials.groupdocs.com/editor/net/).
    question: Where can I find detailed documentation for GroupDocs.Editor for .NET?
  - answer: You can get support through the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).
    question: What support options are available for GroupDocs.Editor for .NET?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
tags:
- css handling
- GroupDocs.Editor
- .NET document processing
- css prefix
- api tutorial
title: Comment gérer le préfixe CSS dans GroupDocs.Editor for .NET
type: docs
url: /fr/net/css-handling/handle-css-content-with-prefix/
weight: 11
---

# Comment gérer le préfixe CSS dans GroupDocs.Editor pour .NET

Dans ce tutoriel, vous apprendrez **comment gérer le préfixe CSS** lors de la manipulation de feuilles de style à l'intérieur d'un document en utilisant GroupDocs.Editor pour .NET. Que vous ayez besoin d'ajouter un préfixe d'URL aux images, aux polices ou à toute ressource externe, les étapes ci‑dessous vous montrent exactement comment **gérer le préfixe CSS** et aussi comment **extraire le contenu CSS** pour un traitement ultérieur. À la fin du guide, vous serez capable de réécrire les chemins des ressources, de récupérer les chaînes CSS brutes et de les intégrer à votre flux de travail web en toute confiance.

## Réponses rapides
- **What does “handle css prefix” mean?** Ajout d'un préfixe d'URL personnalisé aux ressources externes référencées dans le CSS.  
- **Which API method returns CSS styles?** `EditableDocument.GetCssContent(...)`.  
- **Do I need a license?** Une licence d'essai est disponible ; une licence commerciale est requise pour la production.  
- **What .NET versions are supported?** .NET Framework 4.5+ et .NET Core/5/6.  
- **Can I change the prefix at runtime?** Oui – il suffit de passer une chaîne différente à `GetCssContent`.

## Qu'est-ce que le préfixe CSS ?
Le terme désigne la réécriture des URL d'images, de polices ou de toute ressource externe à l'intérieur d'un fichier CSS afin qu'elles pointent vers un emplacement que vous contrôlez, tel qu'un CDN ou un serveur sécurisé. En ajoutant un URL de base cohérent, vous garantissez que chaque ressource se charge correctement lorsque le document est rendu dans un navigateur ou un visualiseur web.

## Pourquoi utiliser GroupDocs.Editor pour extraire le contenu CSS ?
GroupDocs.Editor peut lire le CSS original intégré dans les documents de traitement de texte, renvoyer les chaînes de feuilles de style brutes et vous permettre de les manipuler avant le rendu ou l'enregistrement. Cela élimine l'analyse manuelle, garantit la fidélité à la représentation interne du document et prend en charge **plus de 30 formats de fichiers** tout en traitant des fichiers jusqu'à **500 Mo** sans charger le fichier complet en mémoire.

## Prérequis
Avant de commencer, assurez-vous d'avoir les prérequis suivants en place :
- Visual Studio : Vous aurez besoin d'une installation fonctionnelle de Visual Studio.  
- .NET Framework : Assurez‑vous d'avoir le .NET Framework installé.  
- GroupDocs.Editor for .NET : Vous pouvez le télécharger depuis la [page de téléchargement GroupDocs.Editor for .NET](https://releases.groupdocs.com/editor/net/).  
- Sample Document : Préparez un document d'exemple prêt à être édité.

## Importer les espaces de noms
Tout d'abord, importons les espaces de noms nécessaires pour garantir que notre code s'exécute correctement. Cette étape nous donne accès aux classes principales de GroupDocs.Editor.

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Editor.Options;
```

## Étape 1 : Initialiser l'éditeur
La classe `Editor` est le point d'entrée pour travailler avec les documents dans GroupDocs.Editor. Elle gère les opérations de chargement, d'édition et d'enregistrement.  
La première étape consiste à créer une instance `Editor` avec votre document d'exemple. Cela configure l'environnement d'édition.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```

## Étape 2 : Modifier le document
L'objet `EditableDocument` représente la version modifiable du fichier et expose ses parties internes, telles que le CSS, les images et le HTML.  
Ensuite, nous obtenons un objet `EditableDocument`. Cet objet nous permet de travailler avec le CSS interne du document.

```csharp
    using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
    {
```

## Étape 3 : Définir les préfixes externes
Définissez les préfixes d'URL pour les images et les polices. Ces préfixes seront ajoutés à chaque référence d'image et de police trouvée dans le CSS.

```csharp
        string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
        string externalFontsPrefix = "http://www.mywebsite.com/fonts/id=";
```

## Étape 4 : Extraire le contenu CSS avec les préfixes
`GetCssContent` renvoie une collection de chaînes de feuilles de style CSS qui contiennent déjà les URL préfixés que vous avez fournis.  
Appelez `GetCssContent`, en passant les préfixes que vous venez de définir. La méthode renvoie une liste de chaînes de feuilles de style CSS qui contiennent déjà les URL préfixés.

```csharp
        List<string> stylesheets = document.GetCssContent(externalImagesPrefix, externalFontsPrefix);
```

## Étape 5 : Afficher les résultats
Affichez le nombre de feuilles de style trouvées et affichez chaque feuille de style. Cela vous aide à vérifier que les préfixes ont été appliqués correctement.

```csharp
        Console.WriteLine("There are {0} stylesheets in the input document", stylesheets.Count);
        foreach (string css in stylesheets)
        {
            Console.WriteLine(css);
        }
    }
}
```

## Problèmes courants et solutions
- **No stylesheets returned** – Assurez‑vous que le document source contient réellement du CSS (par ex., un document Word avec des tableaux stylisés ou du HTML intégré).  
- **Incorrect URLs** – Vérifiez que les chaînes de préfixe se terminent par le délimiteur approprié (`/` ou `=`) pour le routage de votre serveur.  
- **Performance concerns** – Pour les documents très volumineux, envisagez de traiter les feuilles de style par lots afin d'éviter une utilisation élevée de la mémoire.

## Questions fréquemment posées

**Q : Puis‑je utiliser GroupDocs.Editor pour .NET avec d'autres formats de documents ?**  
R : Oui, GroupDocs.Editor pour .NET prend en charge PDF, Word, Excel, PowerPoint et de nombreux autres formats.

**Q : Existe‑t‑il un essai gratuit disponible pour GroupDocs.Editor pour .NET ?**  
R : Absolument ! Vous pouvez démarrer votre essai gratuit sur la [page d'essai gratuit de GroupDocs](https://releases.groupdocs.com/).

**Q : Comment obtenir une licence temporaire pour GroupDocs.Editor pour .NET ?**  
R : Vous pouvez obtenir une licence temporaire depuis la [page de licence temporaire](https://purchase.groupdocs.com/temporary-license/).

**Q : Où puis‑je trouver la documentation détaillée de GroupDocs.Editor pour .NET ?**  
R : La documentation détaillée est disponible sur le [site de documentation GroupDocs.Editor pour .NET](https://tutorials.groupdocs.com/editor/net/).

**Q : Quelles options de support sont disponibles pour GroupDocs.Editor pour .NET ?**  
R : Vous pouvez obtenir du support via le [forum de support GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).

## Questions supplémentaires fréquemment posées

**Q : Puis‑je changer le préfixe après avoir extrait le CSS ?**  
R : Oui. Appelez `GetCssContent` à nouveau avec une chaîne de préfixe différente ; la méthode utilise toujours les valeurs que vous passez à l'exécution.

**Q : Cela fonctionne‑t‑il avec des documents protégés par mot de passe ?**  
R : Oui. Fournissez le mot de passe dans `WordProcessingLoadOptions` lors de la création de l'instance `Editor`.

**Q : Est‑il possible d'enregistrer le CSS modifié dans le document ?**  
R : GroupDocs.Editor offre actuellement un accès en lecture seule au CSS. Pour persister les modifications, vous devez remplacer la feuille de style originale en utilisant les API XML sous‑jacentes du document.

---

**Dernière mise à jour:** 2026-09-26  
**Testé avec:** GroupDocs.Editor 23.12 for .NET  
**Auteur:** GroupDocs

## Tutoriels associés

- [Extraire le CSS externe des documents Word avec GroupDocs.Editor .NET : Guide complet](/editor/net/html-web-documents/extract-external-css-word-docs-groupdocs-editor-dotnet/)
- [Extraire et préfixer le HTML des documents Word avec GroupDocs.Editor .NET](/editor/net/html-web-documents/groupdocs-editor-dotnet-extract-prefix-html-word-docs/)
- [Comment extraire et modifier le contenu HTML dans les documents Word avec GroupDocs.Editor .NET](/editor/net/html-web-documents/extract-modify-html-content-word-docs-groupdocs-editor-net/)