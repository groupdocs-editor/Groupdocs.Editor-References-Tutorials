---
date: 2026-06-01
description: Apprenez comment obtenir le nombre de pages et extraire les métadonnées
  du document en utilisant GroupDocs.Editor pour .NET dans un tutoriel détaillé étape
  par étape.
keywords:
- get page count
- extract document metadata
- get document info
- find document extension
- retrieve document size
linktitle: Obtenez le nombre de pages & extrayez les informations du document
schemas:
- author: GroupDocs
  dateModified: '2026-06-01'
  description: Learn how to get page count and extract document metadata using GroupDocs.Editor
    for .NET in a detailed step‑by‑step tutorial.
  headline: Get Page Count & Extract Document Info with GroupDocs.Editor
  type: TechArticle
- questions:
  - answer: GroupDocs.Editor supports Word processing, spreadsheet, presentation,
      PDF, and plain‑text files—over 50 formats in total.
    question: What document types can I extract metadata from?
  - answer: Access `DocumentInfo.Extension` after calling `GetDocumentInfo()`; it
      returns the extension without the leading dot.
    question: How do I retrieve the file extension?
  - answer: Yes—`DocumentInfo.Size` returns the size in bytes; divide by 1,048,576
      to convert to megabytes.
    question: Can I get the size of a document in megabytes?
  - answer: Absolutely—GroupDocs.Editor never writes the password to disk and disposes
      of all cryptographic objects after use.
    question: Is it safe to process password‑protected files on a server?
  - answer: You can get support from the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).
    question: Where can I find additional help if I run into issues?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Obtenez le nombre de pages & extrayez les informations du document avec GroupDocs.Editor
type: docs
url: /fr/net/document-processing/extract-document-info/
weight: 10
---

# Obtenir le nombre de pages et extraire les informations du document avec GroupDocs.Editor

## Introduction
Dans ce tutoriel complet, vous apprendrez comment **obtenir le nombre de pages** et extraire des informations détaillées sur le document — notamment le format, la taille et le statut de chiffrement — en utilisant GroupDocs.Editor pour .NET. Que vous construisiez un système de gestion de documents, un moteur de reporting ou un pipeline de conversion automatisé, comprendre les métadonnées d’un fichier est la première étape d’un traitement fiable. Parcourons l’ensemble du flux de travail, du chargement d’un fichier à la libération sécurisée des ressources.

## Réponses rapides
- **Comment récupérer le nombre de pages d'un document ?**  
  Call `editor.GetDocumentInfo().PageCount` after loading the file with `Editor`.
- **Quels formats de fichiers sont pris en charge pour l'extraction des métadonnées ?**  
  Over 50 formats, including DOCX, XLSX, PPTX, PDF, TXT, and HTML.
- **Puis-je extraire les métadonnées de fichiers protégés par mot de passe ?**  
  Yes—provide the password when constructing the `Editor` instance.
- **Dois-je libérer manuellement les ressources ?**  
  Absolutely; always call `editor.Dispose()` or wrap the editor in a `using` block.
- **Quelle version de GroupDocs.Editor est requise ?**  
  The latest stable release (v23.12+ at the time of writing) supports all features shown.

## Qu’est‑ce que « obtenir le nombre de pages » dans GroupDocs.Editor ?
`GetDocumentInfo()` is a method that returns a `DocumentInfo` object containing the document’s page count, format, size, and other metadata. This single call gives you immediate insight without parsing the file manually. By using this method you avoid loading the entire document into memory, which improves performance especially for large files and reduces server resource consumption.

## Pourquoi extraire les métadonnées du document avec GroupDocs.Editor ?
GroupDocs.Editor can process **50+ input and output formats** and retrieve metadata for files up to **2 GB** without loading the entire document into memory. This efficiency reduces server load by up to **70 %** compared to full‑document parsing, making it ideal for high‑throughput applications.

## Prérequis
- **Notions de base en développement C#** – you should be comfortable with Visual Studio and .NET project structures.
- **Visual Studio 2022** (or any recent version) installed on your machine.
- **GroupDocs.Editor pour .NET** – download the latest package from the [page de téléchargement](https://releases.groupdocs.com/editor/net/).

## Comment charger votre document ?
`Editor` is the main class that represents a document and provides methods for loading and manipulating it. Load the target file by creating an `Editor` instance and passing the file path. The editor automatically detects the format, so you don’t need to specify load options. This approach works for any supported file type and simplifies the initial setup.

```csharp
using System;
using GroupDocs.Editor.Metadata;
```

## Comment récupérer les informations du document ?
`GetDocumentInfo()` returns a `DocumentInfo` object containing metadata such as page count, format, size, and encryption status. After loading, call this method to fetch the object. The returned `DocumentInfo` gives you a concise snapshot of the file’s characteristics, enabling you to make decisions without further processing.

```csharp
string docxInputFilePath = "YourSampleDocument.docx";
Editor editorDocx = new Editor(docxInputFilePath);
```

## Comment déterminer le type de document ?
`DocumentType` is an enum indicating whether the document is WordProcessing, Spreadsheet, or Text. Knowing whether a file is a Word processing document, spreadsheet, or plain text influences how you handle it later. Use the `DocumentType` property of the `DocumentInfo` object to make this decision and branch your logic accordingly.

```csharp
IDocumentInfo infoDocx = editorDocx.GetDocumentInfo(null);
```

## Comment extraire des informations détaillées pour les fichiers de traitement de texte ?
`WordProcessing` refers to documents like DOCX, ODT, and RTF handled as word processing files. If the document type is `WordProcessing`, you can read additional properties like **format**, **extension**, **page count**, **size**, and **encryption flag** directly from the `DocumentInfo` object. These details help you tailor processing steps, such as applying specific conversions or security checks.

```csharp
bool isSpreadsheet = infoDocx is SpreadsheetDocumentInfo;
bool isText = infoDocx is TextualDocumentInfo;
bool isWordProcessing = infoDocx is WordProcessingDocumentInfo;
Console.WriteLine($"Is '{docxInputFilePath}' a Spreadsheet: {isSpreadsheet}");
Console.WriteLine($"Is '{docxInputFilePath}' a Textual document: {isText}");
Console.WriteLine($"Is '{docxInputFilePath}' a WordProcessing document: {isWordProcessing}");
```

## Comment gérer les documents de type feuille de calcul et texte ?
`Spreadsheet` denotes spreadsheet files such as XLSX, while `Text` represents plain‑text documents. For spreadsheets (`Spreadsheet`) and plain‑text files (`Text`), the `DocumentInfo` object still supplies core metadata (extension, size, page count). Some formats may not expose a page count, in which case the value will be `0`. You can still rely on other metadata for downstream logic.

```csharp
if (isWordProcessing)
{
    WordProcessingDocumentInfo casted = (WordProcessingDocumentInfo)infoDocx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Page count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```

## Comment travailler avec des documents protégés par mot de passe ?
`Password` is a string passed to the `Editor` constructor to open encrypted files. When a document is encrypted, first attempt to open it without a password. If that fails, catch the exception, then retry with the correct password. The `Editor` constructor accepts a `Password` parameter for this purpose, allowing seamless handling of protected files.

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

## Comment traiter les documents basés sur du texte ?
`DocumentInfo` provides basic metadata like size, extension, and encoding for text files. Text files (e.g., `.txt`, `.md`) are treated as simple streams. You can still retrieve size and encoding information from `DocumentInfo`, which is useful for validating file integrity or determining appropriate processing pipelines.

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

## Comment libérer correctement les ressources ?
`Editor` is the primary class that holds unmanaged resources and must be disposed after use. To avoid memory leaks, always dispose of the `Editor` instance after you finish extracting information. The `using` statement is the safest pattern because it guarantees disposal even if an exception occurs, ensuring clean resource management.

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

## Problèmes courants et solutions
| Problème | Cause | Solution |
|----------|-------|----------|
| **PageCount renvoie 0** | Le format ne prend pas en charge la pagination (par ex., texte brut) | Vérifiez `DocumentInfo.DocumentType` avant de vous fier à `PageCount`. |
| **Format de fichier non pris en charge** | Extension de fichier non reconnue | Vérifiez que le fichier fait partie des plus de 50 formats pris en charge ; mettez à jour GroupDocs.Editor vers la dernière version. |
| **Exception de mot de passe** | Mot de passe fourni incorrect | Capturez `PasswordProtectedException` et invitez l'utilisateur à ressaisir le mot de passe. |
| **Pic de mémoire sur les gros fichiers** | Chargement de PDF très volumineux sans diffusion | Utilisez `LoadOptions` avec `LoadOptions.LoadMode = LoadMode.Stream` (disponible dans les versions récentes). |

## Questions fréquentes

**Q : Quels types de documents puis‑je extraire les métadonnées ?**  
R : GroupDocs.Editor prend en charge les fichiers de traitement de texte, les feuilles de calcul, les présentations, les PDF et les fichiers texte brut — plus de 50 formats au total.

**Q : Comment récupérer l'extension du fichier ?**  
R : Accédez à `DocumentInfo.Extension` après avoir appelé `GetDocumentInfo()` ; il renvoie l'extension sans le point initial.

**Q : Puis‑je obtenir la taille d’un document en mégaoctets ?**  
R : Oui — `DocumentInfo.Size` renvoie la taille en octets ; divisez par 1 048 576 pour convertir en mégaoctets.

**Q : Est‑il sûr de traiter des fichiers protégés par mot de passe sur un serveur ?**  
R : Absolument — GroupDocs.Editor n’écrit jamais le mot de passe sur le disque et libère tous les objets cryptographiques après utilisation.

**Q : Où puis‑je trouver de l’aide supplémentaire en cas de problème ?**  
R : Vous pouvez obtenir du support sur le [forum de support GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).

**Dernière mise à jour** : 2026-06-01  
**Testé avec** : GroupDocs.Editor 23.12 pour .NET  
**Auteur** : GroupDocs

```csharp
editorDocx.Dispose();
editorXlsx.Dispose();
editorXls.Dispose();
editorXml.Dispose();
Console.WriteLine("ExtractingDocumentInfo routine has successfully finished");
```

## Tutoriels associés

- [Maîtriser l'extraction des métadonnées en .NET avec GroupDocs.Editor : guide complet](/editor/net/advanced-features/groupdocs-editor-net-metadata-extraction-guide/)
- [Tutoriels de chargement de documents avec GroupDocs.Editor pour .NET](/editor/net/document-loading/)
- [Édition efficace de documents avec GroupDocs.Editor .NET : transformer le HTML en documents éditables](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)