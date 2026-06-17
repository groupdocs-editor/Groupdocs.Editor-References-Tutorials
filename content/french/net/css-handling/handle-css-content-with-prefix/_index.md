---
date: 2026-03-06
description: Apprenez à gérer le contenu CSS avec préfixe et à extraire le contenu
  CSS en utilisant GroupDocs.Editor pour .NET dans ce tutoriel détaillé étape par
  étape.
linktitle: Handle CSS Content with Prefix
second_title: GroupDocs.Editor .NET API
title: Gérer le contenu CSS avec un préfixe
type: docs
url: /fr/net/css-handling/handle-css-content-with-prefix/
weight: 11
---

# Gérer le contenu CSS avec préfixe

Dans ce tutoriel, vous découvrirez **comment gérer le préfixe CSS** lors de la manipulation de feuilles de style à l'intérieur d'un document en utilisant GroupDocs.Editor pour .NET. Que vous ayez besoin d'ajouter un préfixe d'URL aux images, aux polices ou à toute ressource externe, les étapes ci‑dessous vous montrent exactement comment **gérer le préfixe CSS** et aussi comment **extraire le contenu CSS** pour un traitement ultérieur.

## Quick Answers
- **Que signifie « handle css prefix » ?** Ajout d'un préfixe d'URL personnalisé aux ressources externes référencées dans le CSS.  
- **Quelle méthode API renvoie les styles CSS ?** `EditableDocument.GetCssContent(...)`.  
- **Ai‑je besoin d’une licence ?** Une licence d'essai est disponible ; une licence commerciale est requise pour la production.  
- **Quelles versions de .NET sont prises en charge ?** .NET Framework 4.5+ et .NET Core/5/6.  
- **Puis‑je changer le préfixe à l'exécution ?** Oui – il suffit de passer une chaîne différente à `GetCssContent`.  

## Qu'est‑ce que **handle css prefix** ?
Appliquer un préfixe aux ressources CSS réécrit les chemins des images, des polices ou d'autres actifs afin qu'ils pointent vers un emplacement que vous contrôlez (par ex., un CDN ou un serveur sécurisé). Cela est particulièrement utile lorsque vous exportez un document et avez besoin que toutes les références externes soient accessibles depuis une application web.

## Pourquoi utiliser GroupDocs.Editor pour **extraire le contenu CSS** ?
GroupDocs.Editor peut lire le CSS original intégré dans les documents WordProcessing, vous fournir les chaînes de feuilles de style brutes, et vous permettre de les manipuler avant le rendu ou l'enregistrement. Cela élimine le besoin d'analyse manuelle et garantit que le CSS extrait correspond à la représentation interne du document.

## Prerequisites
- Visual Studio : Vous aurez besoin d’une installation fonctionnelle de Visual Studio.  
- .NET Framework : Assurez‑vous que le .NET Framework est installé.  
- GroupDocs.Editor pour .NET : Vous pouvez le télécharger [ici](https://releases.groupdocs.com/editor/net/).  
- Document d'exemple : Ayez un document d'exemple prêt à être édité.  

## Import Namespaces
Tout d'abord, importons les espaces de noms nécessaires pour garantir que notre code s'exécute correctement. Cette étape nous donne accès aux classes principales de GroupDocs.Editor.

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Editor.Options;
```

## Step 1: Initialize the Editor
La première étape consiste à créer une instance `Editor` avec votre document d'exemple. Cela configure l'environnement d'édition.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```

## Step 2: Edit the Document
Ensuite, nous obtenons un objet `EditableDocument`. Cet objet représente la version éditable du fichier et nous permet de travailler avec ses parties internes.

```csharp
    using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
    {
```

## Step 3: Set External Prefixes
Définissez les préfixes d'URL pour les images et les polices. Ces préfixes seront ajoutés au début de chaque référence d'image et de police trouvée dans le CSS.

```csharp
        string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
        string externalFontsPrefix = "http://www.mywebsite.com/fonts/id=";
```

## Étape 4 : **extraire le contenu CSS** avec les préfixes
Appelez `GetCssContent`, en passant les préfixes que vous venez de définir. La méthode renvoie une liste de chaînes de feuilles de style CSS qui contiennent déjà les URL préfixées.

```csharp
        List<string> stylesheets = document.GetCssContent(externalImagesPrefix, externalFontsPrefix);
```

## Step 5: Output the Results
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

## Common Issues and Solutions
- **Aucune feuille de style renvoyée** – Assurez‑vous que le document source contient réellement du CSS (par ex., un document Word avec des tableaux stylisés ou du HTML intégré).  
- **URL incorrectes** – Vérifiez que les chaînes de préfixe se terminent par le délimiteur approprié (`/` ou `=`) pour le routage de votre serveur.  
- **Problèmes de performance** – Pour des documents très volumineux, envisagez de traiter les feuilles de style par lots afin d'éviter une utilisation élevée de la mémoire.  

## Conclusion
Gérer le contenu CSS avec un préfixe en utilisant GroupDocs.Editor pour .NET est simple et puissant. En suivant ces étapes, vous pouvez **gérer le préfixe CSS**, récupérer le CSS brut via **l'extraction du contenu CSS**, et intégrer de manière transparente les ressources externes dans votre flux de travail web. Explorez d'autres fonctionnalités de GroupDocs.Editor telles que la conversion HTML, l'extraction d'images et la fusion de documents pour tirer encore plus de valeur de l'API.

## FAQ's
### Puis‑je utiliser GroupDocs.Editor pour .NET avec d'autres formats de documents ?
Oui, GroupDocs.Editor pour .NET prend en charge divers formats de documents, y compris PDF, Word, Excel, et plus encore.

### Une version d'essai gratuite est‑elle disponible pour GroupDocs.Editor pour .NET ?
Absolument ! Vous pouvez démarrer votre version d'essai gratuite [ici](https://releases.groupdocs.com/).

### Comment obtenir une licence temporaire pour GroupDocs.Editor pour .NET ?
Vous pouvez obtenir une licence temporaire [ici](https://purchase.groupdocs.com/temporary-license/).

### Où puis‑je trouver la documentation détaillée de GroupDocs.Editor pour .NET ?
La documentation détaillée est disponible [ici](https://tutorials.groupdocs.com/editor/net/).

### Quelles options de support sont disponibles pour GroupDocs.Editor pour .NET ?
Vous pouvez obtenir du support [ici](https://forum.groupdocs.com/c/editor/20).

## Additional Frequently Asked Questions

**Q : Puis‑je changer le préfixe après avoir extrait le CSS ?**  
R : Oui. Appelez à nouveau `GetCssContent` avec une chaîne de préfixe différente ; la méthode utilise toujours les valeurs que vous passez à l'exécution.

**Q : Cela fonctionne‑t‑il avec des documents protégés par mot de passe ?**  
R : Oui. Fournissez le mot de passe dans `WordProcessingLoadOptions` lors de la création de l'instance `Editor`.

**Q : Est‑il possible d'enregistrer le CSS modifié dans le document ?**  
R : GroupDocs.Editor offre actuellement un accès en lecture seule au CSS. Pour persister les modifications, vous devez remplacer la feuille de style originale en utilisant les API XML sous‑jacentes du document.

---

**Dernière mise à jour :** 2026-03-06  
**Testé avec :** GroupDocs.Editor 23.12 pour .NET  
**Auteur :** GroupDocs