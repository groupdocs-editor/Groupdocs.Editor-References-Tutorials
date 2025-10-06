---
title: Travailler avec des documents en texte brut
linktitle: Travailler avec des documents en texte brut
second_title: API GroupDocs.Editor .NET
description: Apprenez à modifier des documents en texte brut à l'aide de GroupDocs.Editor pour .NET grâce à notre guide étape par étape. Simplifiez votre processus d'édition de documents .NET.
weight: 15
url: /fr/net/document-processing/work-plain-text-documents/
type: docs
---
# Travailler avec des documents en texte brut

## Introduction
Cherchez-vous à rationaliser votre processus d’édition de documents dans .NET ? Ne cherchez pas plus loin que GroupDocs.Editor pour .NET ! Cette API puissante vous permet de modifier facilement une grande variété de formats de documents. Dans ce didacticiel, nous vous guiderons tout au long du processus d'utilisation de documents en texte brut à l'aide de GroupDocs.Editor for .NET. À la fin, vous serez équipé pour gérer l’édition de documents texte comme un pro. Prêt à plonger ? Commençons!
## Conditions préalables
Avant de commencer, vous devez mettre en place quelques éléments :
- Environnement de développement .NET : assurez-vous d'avoir configuré un environnement de développement .NET fonctionnel. Visual Studio est un choix populaire.
-  GroupDocs.Editor pour .NET : téléchargez et installez le[GroupDocs.Editor pour .NET](https://releases.groupdocs.com/editor/net/).
- Connaissances de base en C# : la familiarité avec le langage de programmation C# vous aidera à suivre les exemples.
- Éditeur de texte : n'importe quel éditeur de texte fera l'affaire, bien que Visual Studio Code soit recommandé pour ses fonctionnalités et sa facilité d'utilisation.
## Importer des espaces de noms
Pour commencer à utiliser GroupDocs.Editor pour .NET, vous devez importer les espaces de noms nécessaires dans votre projet. Cela garantit que toutes les classes et méthodes requises sont disponibles.
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```
Décomposons le processus en étapes gérables. Suivez-nous pendant que nous vous guidons à travers chaque étape de l'édition de documents en texte brut à l'aide de GroupDocs.Editor for .NET.
## Étape 1 : obtenir un chemin d'accès au fichier TXT d'entrée
Tout d’abord, vous devez spécifier le chemin d’accès au fichier TXT d’entrée. Il peut s'agir d'un chemin vers un fichier local ou d'un flux contenant le contenu du fichier.
```csharp
string inputFilePath = "YourSampleDocument.txt";
```
## Étape 2 : Créer une instance d'éditeur
 Ensuite, créez une instance de`Editor` classe. Cette classe est responsable du chargement et de l’édition des documents. Aucune option de chargement n’est requise à ce stade.
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## Étape 3 : Créer des options d'édition TXT
Maintenant, créez les options d'édition TXT. Ces options vous permettent de spécifier comment le contenu du texte doit être traité lors de l'édition.
```csharp
    TextEditOptions editOptions = new TextEditOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        RecognizeLists = true,
        LeadingSpaces = TextLeadingSpacesOptions.ConvertToIndent,
        TrailingSpaces = TextTrailingSpacesOptions.Trim
    };
```
## Étape 4 : Créer une instance EditableDocument
 Une fois les options d'édition définies, créez un`EditableDocument` exemple. Cela représente le document dans un format modifiable.
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## Étape 5 : Modifier le contenu du document
Récupérez le contenu du texte original et apportez les modifications souhaitées. Pour cet exemple, nous remplacerons le mot « texte » par « texte ÉDITÉ ».
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("text", "EDITED text");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## Étape 6 : Créer un document modifiable avec un contenu mis à jour
 Après avoir effectué les modifications nécessaires, créez un nouveau`EditableDocument` avec le contenu mis à jour et les ressources originales.
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## Étape 7 : Créer des options d'enregistrement de traitement de texte
Préparez les options de sauvegarde pour le format WordProcessing. Cet exemple utilise le format DOCM et spécifie les paramètres régionaux.
```csharp
    WordProcessingSaveOptions wordSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm)
    {
        Locale = System.Globalization.CultureInfo.GetCultureInfo("en-GB")
    };
```
## Étape 8 : Créer des options d'enregistrement TXT
De même, créez les options d'enregistrement pour le format TXT. Assurez-vous que le codage est défini sur UTF-8 et conservez la disposition du tableau.
```csharp
    TextSaveOptions txtSaveOptions = new TextSaveOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        PreserveTableLayout = true
    };
```
## Étape 9 : préparer les chemins de sortie
Préparez les chemins pour enregistrer les fichiers DOCX et TXT résultants. Utilisez le chemin du fichier d'entrée pour déterminer le répertoire de sortie et les noms de fichiers.
```csharp
    string outputWordPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".docm");
    string outputTxtPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".txt");
```
## Étape 10 : Enregistrez le document modifié
Enfin, enregistrez le document modifié aux formats DOCX et TXT en utilisant les options d'enregistrement spécifiées.
```csharp
    editor.Save(afterEdit, outputWordPath, wordSaveOptions);
    editor.Save(afterEdit, outputTxtPath, txtSaveOptions);
}
System.Console.WriteLine("Document editing process completed successfully!");
```
## Conclusion
 Toutes nos félicitations! Vous avez modifié avec succès un document en texte brut à l'aide de GroupDocs.Editor pour .NET. Cet outil puissant simplifie l'édition de documents, facilitant ainsi son intégration dans vos applications .NET. Que vous traitiez des fichiers texte simples ou des formats de documents complexes, GroupDocs.Editor a ce qu'il vous faut. Découvrez plus de fonctionnalités et de capacités en visitant le[Documentation GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/).
## FAQ
### Quels formats de fichiers GroupDocs.Editor pour .NET prend-il en charge ?
 GroupDocs.Editor pour .NET prend en charge un large éventail de formats de fichiers, notamment DOCX, TXT, HTML, etc. Vérifier la[Documentation](https://tutorials.groupdocs.com/editor/net/) pour une liste complète.
### Comment puis-je obtenir un essai gratuit de GroupDocs.Editor pour .NET ?
 Vous pouvez télécharger un essai gratuit de GroupDocs.Editor pour .NET à partir du[page des versions](https://releases.groupdocs.com/).
### Puis-je acheter une licence temporaire pour GroupDocs.Editor pour .NET ?
Oui, vous pouvez obtenir une licence temporaire auprès du[Page d'achat de GroupDocs](https://purchase.groupdocs.com/temporary-license/).
### Où puis-je obtenir de l'aide pour GroupDocs.Editor pour .NET ?
 L'assistance est disponible via le[Forum d'assistance GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).
### Existe-t-il une documentation détaillée disponible pour GroupDocs.Editor pour .NET ?
 Oui, une documentation détaillée est disponible sur le[Page de documentation de GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/).