---
title: Extraire les informations du document
linktitle: Extraire les informations du document
second_title: API GroupDocs.Editor .NET
description: Découvrez comment extraire des informations sur un document à l'aide de GroupDocs.Editor pour .NET grâce à notre didacticiel détaillé étape par étape. Parfait pour gérer différents types de documents.
weight: 10
url: /fr/net/document-processing/extract-document-info/
---

# Extraire les informations du document

## Introduction
Bienvenue dans ce didacticiel complet sur l'extraction d'informations sur un document à l'aide de GroupDocs.Editor pour .NET. Dans ce guide, nous vous guiderons pas à pas tout au long du processus, en nous assurant que vous comprenez chaque partie de manière claire et concise. Que vous soyez un développeur chevronné ou que vous débutiez tout juste, ce didacticiel vous aidera à intégrer de manière transparente GroupDocs.Editor dans vos projets .NET pour gérer et manipuler efficacement les documents.
## Conditions préalables
Avant de plonger dans le code, assurons-nous que vous disposez de tout ce dont vous avez besoin :
- Connaissance de base de C# : Comprendre les bases de la programmation C# est essentiel.
- Visual Studio : assurez-vous que Visual Studio est installé.
-  GroupDocs.Editor pour .NET : vous aurez besoin de la bibliothèque GroupDocs.Editor pour .NET. Vous pouvez le télécharger depuis le[page de téléchargement](https://releases.groupdocs.com/editor/net/).
## Importer des espaces de noms
Pour commencer, vous devrez importer les espaces de noms nécessaires. Cela vous permet d'accéder aux classes et méthodes nécessaires pour manipuler des documents.
```csharp
using System;
using GroupDocs.Editor.Metadata;
```
## Étape 1 : Chargez votre document
Tout d’abord, vous devez charger le document dont vous souhaitez extraire les informations. Cela peut être fait en fournissant le chemin d'accès au document.
```csharp
string docxInputFilePath = "YourSampleDocument.docx";
Editor editorDocx = new Editor(docxInputFilePath);
```
## Étape 2 : Récupérer les informations du document
 Ensuite, vous récupérerez les informations du document à l'aide du`GetDocumentInfo` méthode. Cette méthode ne nécessite aucune option de chargement spécifique si vous n'êtes pas sûr du format du document.
```csharp
IDocumentInfo infoDocx = editorDocx.GetDocumentInfo(null);
```
## Étape 3 : Déterminer le type de document
Maintenant, vous devez vérifier le type de document que vous traitez. Ceci est crucial car cela dicte la manière dont vous gérerez le document.
```csharp
bool isSpreadsheet = infoDocx is SpreadsheetDocumentInfo;
bool isText = infoDocx is TextualDocumentInfo;
bool isWordProcessing = infoDocx is WordProcessingDocumentInfo;
Console.WriteLine($"Is '{docxInputFilePath}' a Spreadsheet: {isSpreadsheet}");
Console.WriteLine($"Is '{docxInputFilePath}' a Textual document: {isText}");
Console.WriteLine($"Is '{docxInputFilePath}' a WordProcessing document: {isWordProcessing}");
```
## Étape 4 : Extraire les informations détaillées
Si le document est un document de traitement de texte, vous pouvez extraire des informations détaillées telles que le format, l'extension, le nombre de pages, la taille et s'il est crypté.
```csharp
if (isWordProcessing)
{
    WordProcessingDocumentInfo casted = (WordProcessingDocumentInfo)infoDocx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Page count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```
## Étape 5 : Répétez l'opération pour différents types de documents
Répétez les mêmes étapes pour d'autres types de documents tels que les feuilles de calcul et les documents textuels.
```csharp
string xlsxInputFilePath = "YourSampleDocument.xlsx";
Editor editorXlsx = new Editor(xlsxInputFilePath);
IDocumentInfo infoXlsx = editorXlsx.GetDocumentInfo(null);
bool isXlsxSpreadsheet = infoXlsx is SpreadsheetDocumentInfo;
Console.WriteLine($"Is '{xlsxInputFilePath}' a Spreadsheet: {isXlsxSpreadsheet}");
if (isXlsxSpreadsheet)
{
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo)infoXlsx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Tabs count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```
## Étape 6 : Gérer les documents protégés par mot de passe
Lorsque vous traitez des documents protégés par mot de passe, vous devez d'abord essayer de les ouvrir sans mot de passe, puis avec un mot de passe incorrect et enfin avec le mot de passe correct.
```csharp
string xlsInputFilePath = "YourSampleDocument.xls";
Editor editorXls = new Editor(xlsInputFilePath);
try
{
    IDocumentInfo infoXls = editorXls.GetDocumentInfo(null);
}
catch (PasswordRequiredException)
{
    Console.WriteLine("This document is password-protected.");
}
try
{
    IDocumentInfo infoXls = editorXls.GetDocumentInfo("incorrect_password");
}
catch (IncorrectPasswordException)
{
    Console.WriteLine("The provided password is incorrect.");
}
IDocumentInfo infoXlsValid = editorXls.GetDocumentInfo("correct_password");
bool isXlsSpreadsheet = infoXlsValid is SpreadsheetDocumentInfo;
Console.WriteLine($"Password-protected document is a Spreadsheet: {isXlsSpreadsheet}");
if (isXlsSpreadsheet)
{
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo)infoXlsValid;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Tabs count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```
## Étape 7 : Gérer les documents textuels
```csharp
string xmlInputFilePath = "YourSampleDocument.xml";
Editor editorXml = new Editor(xmlInputFilePath);
IDocumentInfo infoXml = editorXml.GetDocumentInfo(null);
bool isXmlText = infoXml is TextualDocumentInfo;
Console.WriteLine($"Is '{xmlInputFilePath}' a Textual document: {isXmlText}");
if (isXmlText)
{
    TextualDocumentInfo casted = (TextualDocumentInfo)infoXml;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Encoding: {casted.Encoding}; Size: {casted.Size} bytes");
}
```
## Étape 8 : éliminer les ressources
Enfin, assurez-vous de disposer de toutes les ressources pour éviter les fuites de mémoire.
```csharp
editorDocx.Dispose();
editorXlsx.Dispose();
editorXls.Dispose();
editorXml.Dispose();
Console.WriteLine("ExtractingDocumentInfo routine has successfully finished");
```
## Conclusion
Toutes nos félicitations! Vous avez maintenant appris à extraire des informations sur un document à l'aide de GroupDocs.Editor for .NET. Cette puissante bibliothèque simplifie la gestion et la manipulation des documents, vous permettant de gérer différents types de documents de manière transparente. Que vous traitiez de documents de traitement de texte, de feuilles de calcul ou de texte, GroupDocs.Editor fournit une solution robuste.
## FAQ
### Quels types de documents GroupDocs.Editor peut-il gérer ?
GroupDocs.Editor peut gérer différents types de documents, notamment le traitement de texte, les feuilles de calcul et les documents texte.
### GroupDocs.Editor peut-il gérer des documents protégés par mot de passe ?
Oui, GroupDocs.Editor peut gérer des documents protégés par mot de passe. Il peut identifier et ouvrir ces documents grâce au mot de passe correct.
### Est-il nécessaire de supprimer les objets Editor ?
Oui, il est crucial de supprimer les objets Editor pour libérer des ressources et éviter les fuites de mémoire.
### Puis-je extraire des informations détaillées sur le format et la taille du document ?
Absolument! GroupDocs.Editor vous permet d'extraire des informations détaillées, notamment le format, l'extension, la taille, le nombre de pages et l'état de cryptage.
### Où puis-je obtenir de l'aide si je rencontre des problèmes ?
 Vous pouvez bénéficier du soutien du[Forum d'assistance GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).