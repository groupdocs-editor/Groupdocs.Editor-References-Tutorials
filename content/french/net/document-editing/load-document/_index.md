---
title: Charger un document
linktitle: Charger un document
second_title: API GroupDocs.Editor .NET
description: Découvrez comment modifier des documents par programmation avec GroupDocs.Editor for .NET. Guide étape par étape pour le chargement de documents, la gestion des fichiers protégés par mot de passe, et bien plus encore.
type: docs
weight: 13
url: /fr/net/document-editing/load-document/
---
## Introduction
L'édition de documents par programmation peut être une tâche ardue, surtout si vous avez affaire à différents formats de fichiers et structures complexes. Heureusement, GroupDocs.Editor pour .NET facilite cette tâche en fournissant une API robuste et facile à utiliser pour éditer un large éventail de types de documents. Dans ce didacticiel, nous vous expliquerons tout ce dont vous avez besoin pour démarrer avec GroupDocs.Editor pour .NET, y compris les conditions préalables, comment importer des espaces de noms et un guide détaillé, étape par étape, pour charger des documents à l'aide de diverses méthodes.
## Conditions préalables
Avant de plonger dans le vif du sujet, assurez-vous d'avoir configuré les conditions préalables suivantes :
- Visual Studio : assurez-vous que Visual Studio est installé sur votre ordinateur.
- .NET Framework : GroupDocs.Editor pour .NET prend en charge .NET Framework 2.0 ou version ultérieure. Assurez-vous que votre projet cible un framework compatible.
-  GroupDocs.Editor pour .NET : téléchargez la dernière version à partir du[page de téléchargement](https://releases.groupdocs.com/editor/net/).
- Connaissance de base de C# : Une familiarité avec la programmation C# et .NET est nécessaire pour suivre ce didacticiel.
## Importer des espaces de noms
Pour commencer à utiliser GroupDocs.Editor pour .NET, vous devez importer les espaces de noms nécessaires dans votre projet. Ajoutez les directives using suivantes en haut de votre fichier C# :
```csharp
using GroupDocs.Editor.Options;
using System.IO;
```
Ces espaces de noms donneront accès aux classes et méthodes requises pour les tâches d'édition de documents.
## Étape 1 : Charger un document à partir d'un chemin de fichier
Le chargement d'un document à partir d'un chemin de fichier est simple. Cette méthode est idéale pour les documents stockés localement sur votre machine.

```csharp
string inputPath = "Your Sample Document";
// Charger le document en tant que fichier via le chemin et sans options de chargement
Editor editor1 = new Editor(inputPath);
// Éliminer les ressources
editor1.Dispose();
System.Console.WriteLine("Document loaded successfully from file path.");
```
## Étape 2 : Charger le document avec les options de chargement
Parfois, vous devrez peut-être charger des documents nécessitant un traitement spécial, tels que des fichiers protégés par mot de passe. Dans de tels cas, vous pouvez utiliser les options de chargement.

```csharp
string inputPath = "Your Sample Document";
//Créer des options de chargement pour les documents Word
WordProcessingLoadOptions wordLoadOptions = new WordProcessingLoadOptions();
wordLoadOptions.Password = "some password";
// Charger le document en tant que fichier via le chemin et avec les options de chargement
Editor editor2 = new Editor(inputPath, delegate { return wordLoadOptions; });
// Éliminer les ressources
editor2.Dispose();
System.Console.WriteLine("Password-protected document loaded successfully.");
```
## Étape 3 : Charger un document à partir d'un flux d'octets
Le chargement d'un document à partir d'un flux d'octets est utile lorsque vous devez traiter des documents qui ne sont pas stockés sous forme de fichiers, tels que ceux récupérés d'une base de données ou d'un service Web.

```csharp
FileStream inputStream = File.OpenRead("Your Sample Document");
// Charger le document en tant que contenu à partir du flux d'octets et sans options de chargement
Editor editor3 = new Editor(delegate { return inputStream; });
// Éliminer les ressources
editor3.Dispose();
System.Console.WriteLine("Document loaded successfully from byte stream.");
```
## Étape 4 : Charger le document avec les options de chargement à partir d'un flux d'octets
Pour les documents nécessitant un traitement spécial lorsqu'ils sont chargés à partir d'un flux d'octets, vous pouvez combiner le chargement de flux d'octets avec des options de chargement.

```csharp
FileStream inputStream = File.OpenRead("Your Sample Document");
// Créer des options de chargement pour les feuilles de calcul
SpreadsheetLoadOptions sheetLoadOptions = new SpreadsheetLoadOptions();
sheetLoadOptions.OptimizeMemoryUsage = true;
// Charger le document en tant que contenu à partir du flux d'octets et avec les options de chargement
Editor editor4 = new Editor(delegate { return inputStream; }, delegate { return sheetLoadOptions; });
// Éliminer les ressources
editor4.Dispose();
System.Console.WriteLine("Spreadsheet document loaded successfully with load options.");
```
## Conclusion
Toutes nos félicitations! Vous avez appris avec succès comment charger des documents à l'aide de GroupDocs.Editor pour .NET de différentes manières. Que vous traitiez de fichiers locaux, de documents protégés par mot de passe ou de flux d'octets, GroupDocs.Editor fournit une solution flexible et puissante pour vos besoins d'édition de documents. N'oubliez pas de toujours disposer de ressources pour garantir des performances et une gestion optimales des ressources dans vos applications.
## FAQ
### Quels formats de fichiers sont pris en charge par GroupDocs.Editor pour .NET ?
 GroupDocs.Editor prend en charge un large éventail de formats de fichiers, notamment DOCX, XLSX, PPTX, HTML et bien d'autres. Pour une liste complète, reportez-vous au[Documentation](https://reference.groupdocs.com/editor/net/).
### Comment gérer les documents protégés par mot de passe ?
 Vous pouvez utiliser des options de chargement telles que`WordProcessingLoadOptions` pour spécifier le mot de passe lors du chargement de documents protégés par mot de passe.
### Puis-je utiliser GroupDocs.Editor dans une application Web ?
Oui, GroupDocs.Editor peut être utilisé dans les applications Web. Assurez-vous de gérer correctement les flux de fichiers et l’élimination des ressources pour éviter les fuites de mémoire.
### Où puis-je obtenir une licence temporaire pour GroupDocs.Editor ?
 Vous pouvez obtenir une licence temporaire auprès du[page de licence temporaire](https://purchase.groupdocs.com/temporary-license/).
### a-t-il une assistance disponible si je rencontre des problèmes ?
 Oui, GroupDocs fournit une assistance via son[forum d'entraide](https://forum.groupdocs.com/c/editor/20).