---
date: 2026-04-20
description: Apprenez à charger un document protégé par mot de passe à l'aide de GroupDocs.Editor
  pour .NET, y compris le chargement depuis un chemin de fichier, depuis un flux d'octets
  et depuis une base de données.
keywords:
- load password protected document
- load document from stream
- load document from database
linktitle: Charger le document protégé par mot de passe
second_title: GroupDocs.Editor .NET API
title: Charger un document protégé par mot de passe avec GroupDocs.Editor .NET
type: docs
url: /fr/net/document-editing/load-document/
weight: 13
---

# Charger un document protégé par mot de passe avec GroupDocs.Editor .NET

## Introduction
Modifier des documents de manière programmatique peut sembler intimidant, surtout lorsque vous devez **charger un document protégé par mot de passe** qui se trouve à différents emplacements. Que le fichier soit sur le disque, provienne d’un flux d’octets ou soit stocké dans une base de données, GroupDocs.Editor pour .NET vous offre une API propre et cohérente pour gérer tous ces scénarios. Dans ce guide, nous passerons en revue les prérequis, importerons les espaces de noms requis et vous montrerons étape par étape comment charger des documents en utilisant diverses méthodes — y compris le cas spécial des fichiers protégés par mot de passe.

## Réponses rapides
- **GroupDocs.Editor peut-il ouvrir des fichiers protégés par mot de passe ?** Oui, utilisez les options de chargement appropriées avec le mot de passe défini.  
- **Quelles versions de .NET sont prises en charge ?** .NET Framework 2.0+ et .NET Core/5/6 sont tous compatibles.  
- **Can GroupDocs.Editor open password‑protected files?** Absolutely—call `Dispose()` to free resources.  
- **Puis-je charger un document depuis une base de données ?** Oui, récupérez le fichier sous forme de tableau d’octets ou de flux et passez‑le au constructeur `Editor`.  
- **Existe‑t‑il une limite de taille de fichier ?** Les gros fichiers sont pris en charge ; envisagez d’utiliser le chargement basé sur les flux avec des options d’optimisation de la mémoire.

## Qu’est‑ce que « charger un document protégé par mot de passe » ?
Charger un document protégé par mot de passe consiste à ouvrir un fichier qui nécessite un mot de passe pour y accéder, puis à fournir ce mot de passe de façon programmatique afin que l’API puisse le déchiffrer et travailler avec le contenu. GroupDocs.Editor abstrait l’étape de déchiffrement via les options de chargement, rendant le processus simple.

## Pourquoi utiliser GroupDocs.Editor pour charger des documents ?
- **API unifiée** – Le même code fonctionne pour les fichiers Word, Excel, PowerPoint et HTML.  
- **Gestion des mots de passe** – Prise en charge intégrée des fichiers chiffrés sans déchiffrement manuel.  
- **Flexibilité des flux** – Chargement depuis des chemins de fichiers, des flux ou toute source personnalisée comme une base de données.  
- **Gestion des ressources** – Le modèle simple `Dispose()` maintient une faible utilisation de la mémoire.

## Prérequis
- **Visual Studio** – Assurez‑vous d’avoir Visual Studio installé sur votre machine.  
- **.NET Framework** – GroupDocs.Editor pour .NET prend en charge .NET Framework 2.0 ou ultérieur. Assurez‑vous que votre projet cible un framework compatible.  
- **GroupDocs.Editor pour .NET** – Téléchargez la dernière version depuis la [page de téléchargement](https://releases.groupdocs.com/editor/net/).  
- **Connaissances de base en C#** – Une familiarité avec C# et la programmation .NET est nécessaire pour suivre ce tutoriel.

## Importer les espaces de noms
Pour commencer à utiliser GroupDocs.Editor pour .NET, vous devez importer les espaces de noms nécessaires dans votre projet. Ajoutez les directives `using` suivantes en haut de votre fichier C# :

```csharp
using GroupDocs.Editor.Options;
using System.IO;
```

Ces espaces de noms fourniront l’accès aux classes et méthodes requises pour les tâches d’édition de documents.

## Étape 1 : Charger le document depuis un chemin de fichier
Charger un document depuis un chemin de fichier est simple. Cette méthode est idéale pour les documents stockés localement sur votre machine.

```csharp
string inputPath = "Your Sample Document";
// Load document as file via path and without load options
Editor editor1 = new Editor(inputPath);
// Dispose resources
editor1.Dispose();
System.Console.WriteLine("Document loaded successfully from file path.");
```

## Étape 2 : Charger le document avec des options de chargement (fichiers protégés par mot de passe)
Parfois, vous devez charger des documents qui nécessitent une manipulation spéciale, comme les fichiers protégés par mot de passe. Dans ces cas, vous pouvez utiliser les options de chargement.

```csharp
string inputPath = "Your Sample Document";
// Create load options for Word documents
WordProcessingLoadOptions wordLoadOptions = new WordProcessingLoadOptions();
wordLoadOptions.Password = "some password";
// Load document as file via path and with load options
Editor editor2 = new Editor(inputPath, delegate { return wordLoadOptions; });
// Dispose resources
editor2.Dispose();
System.Console.WriteLine("Password-protected document loaded successfully.");
```

## Comment charger un document depuis un flux
Charger un document depuis un flux d’octets est utile lorsque vous devez traiter des documents qui ne sont pas stockés sous forme de fichiers, par exemple ceux récupérés d’une base de données ou d’un service web.

```csharp
FileStream inputStream = File.OpenRead("Your Sample Document");
// Load document as content from byte stream and without load options
Editor editor3 = new Editor(delegate { return inputStream; });
// Dispose resources
editor3.Dispose();
System.Console.WriteLine("Document loaded successfully from byte stream.");
```

## Étape 4 : Charger le document avec des options de chargement depuis un flux d’octets
Pour les documents nécessitant une manipulation spéciale lorsqu’ils sont chargés depuis un flux d’octets, vous pouvez combiner le chargement du flux d’octets avec les options de chargement.

```csharp
FileStream inputStream = File.OpenRead("Your Sample Document");
// Create load options for spreadsheets
SpreadsheetLoadOptions sheetLoadOptions = new SpreadsheetLoadOptions();
sheetLoadOptions.OptimizeMemoryUsage = true;
// Load document as content from byte stream and with load options
Editor editor4 = new Editor(delegate { return inputStream; }, delegate { return sheetLoadOptions; });
// Dispose resources
editor4.Dispose();
System.Console.WriteLine("Spreadsheet document loaded successfully with load options.");
```

## Comment charger un document depuis une base de données
Si vos documents sont stockés dans une base de données relationnelle, récupérez les données binaires (par ex., en utilisant `SELECT FileData FROM Documents WHERE Id = @id`) et passez le `byte[]` ou le `MemoryStream` résultant au constructeur `Editor` de la même manière que dans l’exemple de flux ci‑dessus. Cela maintient votre code cohérent quel que soit la source.

## Problèmes courants et solutions
- **Mot de passe incorrect** – L’éditeur lèvera une exception. Vérifiez la valeur du mot de passe et assurez‑vous d’utiliser la bonne classe d’options de chargement pour le type de fichier.  
- **Flux déjà fermé** – Assurez‑vous que le flux reste ouvert pendant la durée de vie de l’instance `Editor`, ou copiez le flux dans un `MemoryStream`.  
- **Consommation de mémoire avec de gros fichiers** – Utilisez `SpreadsheetLoadOptions.OptimizeMemoryUsage = true` (comme indiqué) ou des options équivalentes pour les autres formats.

## Questions fréquentes

**Q : Quels formats de fichiers sont pris en charge par GroupDocs.Editor pour .NET ?**  
R : GroupDocs.Editor prend en charge un large éventail de formats, y compris DOCX, XLSX, PPTX, HTML et bien d’autres. Pour la liste complète, consultez la [documentation](https://tutorials.groupdocs.com/editor/net/).

**Q : Comment gérer les documents protégés par mot de passe ?**  
R : Vous pouvez utiliser des options de chargement telles que `WordProcessingLoadOptions` pour spécifier le mot de passe lors du chargement de documents protégés.

**Q : Puis‑je utiliser GroupDocs.Editor dans une application web ?**  
R : Oui, GroupDocs.Editor peut être utilisé dans des applications web. Veillez à gérer correctement les flux de fichiers et la libération des ressources afin d’éviter les fuites de mémoire.

**Q : Où obtenir une licence temporaire pour GroupDocs.Editor ?**  
R : Vous pouvez obtenir une licence temporaire depuis la [page de licence temporaire](https://purchase.groupdocs.com/temporary-license/).

**Q : Existe‑t‑il un support disponible en cas de problème ?**  
R : Oui, GroupDocs fournit un support via leur [forum d’assistance](https://forum.groupdocs.com/c/editor/20).

**Q : Le chargement depuis une base de données nécessite‑t‑il une configuration spéciale ?**  
R : Aucune configuration spéciale n’est requise au‑delà de la récupération des données binaires et de leur passage sous forme de flux ou de tableau d’octets au constructeur `Editor`.

**Q : Comment améliorer les performances lors du chargement de très grands classeurs ?**  
R : Activez les options d’optimisation de la mémoire comme `SpreadsheetLoadOptions.OptimizeMemoryUsage = true` pour réduire l’empreinte mémoire.

## Conclusion
Félicitations ! Vous avez appris à **charger un document protégé par mot de passe** en utilisant GroupDocs.Editor pour .NET de différentes manières. Que vous travailliez avec des fichiers locaux, des documents protégés, des flux d’octets ou du contenu stocké en base de données, GroupDocs.Editor offre une solution flexible et puissante pour vos besoins d’édition de documents. N’oubliez pas de toujours libérer l’instance `Editor` afin de garder votre application performante et efficace en ressources.

---

**Dernière mise à jour :** 2026-04-20  
**Testé avec :** GroupDocs.Editor 2.0 (latest)  
**Auteur :** GroupDocs