---
date: '2026-04-07'
description: Apprenez à modifier des fichiers docx et à convertir Word en RTF avec
  GroupDocs.Editor .NET. Automatisez efficacement le flux de travail des documents.
keywords:
- how to edit docx
- convert word to rtf
- convert docx to txt
- document workflow automation
- batch process word docs
- save docx as docm
title: Comment éditer les fichiers DOCX et convertir les formats avec GroupDocs.Editor
type: docs
url: /fr/net/document-editing/groupdocs-editor-net-mastering-document-editing/
weight: 1
---

# Comment éditer DOCX et convertir les formats avec GroupDocs.Editor

Gérez et transformez facilement les documents Word dans votre environnement .NET à l'aide de **GroupDocs.Editor .NET**. Dans ce tutoriel, vous découvrirez **how to edit docx** files, les convertir en formats tels que RTF, DOCM et texte brut, et automatiser votre flux de travail documentaire pour une productivité maximale.

## Réponses rapides
- **Quelle bibliothèque est requise ?** GroupDocs.Editor pour .NET (20.10+).  
- **Puis-je convertir un DOCX en RTF ?** Oui – utilisez `WordProcessingSaveOptions` avec `WordProcessingFormats.Rtf`.  
- **La sauvegarde au format TXT est‑elle prise en charge ?** Absolument, via `TextSaveOptions`.  
- **Ai‑je besoin d’une licence ?** Un essai fonctionne pour le développement ; une licence débloque toutes les fonctionnalités.  
- **Comment gérer de nombreux fichiers ?** Combinez le code avec async/await ou Parallel.ForEach pour le traitement par lots.

## Qu’est‑ce que « how to edit docx » avec GroupDocs.Editor ?
GroupDocs.Editor charge un DOCX, expose son contenu sous forme de HTML éditable, vous permet de modifier ce HTML programmétiquement, puis enregistre le résultat dans n’importe quel format pris en charge. Cette approche élimine le besoin d’interopérabilité avec Office et fonctionne sur toute plateforme .NET côté serveur.

## Pourquoi utiliser GroupDocs.Editor pour l’automatisation des flux de travail documentaires ?
- **Côté serveur uniquement** – aucune installation d’Office requise.  
- **Formats de sortie multiples** – RTF, DOCM, TXT, HTML, PDF, etc.  
- **Haute performance** – API légère conçue pour les scénarios de traitement par lots.  
- **Contrôle total** – éditez, remplacez ou injectez des fragments HTML avant l’enregistrement.

## Prérequis
- **Bibliothèque GroupDocs.Editor** (Version 20.10 ou ultérieure)  
- .NET Framework 4.7.2 + ou .NET 5/6  
- Visual Studio (toute édition récente)  
- Connaissances de base en C# et familiarité avec les entrées/sorties de fichiers  

## Installation de GroupDocs.Editor
Vous pouvez ajouter le package via la CLI .NET, la console du gestionnaire de packages ou l’interface NuGet.

```bash
dotnet add package GroupDocs.Editor
```

```powershell
Install-Package GroupDocs.Editor
```

## Acquisition de licence
Commencez avec un essai gratuit ou demandez une clé de licence temporaire. Pour une utilisation en production, achetez une licence afin de débloquer un traitement illimité.

## Comment charger et éditer un document DOCX
Tout d’abord, pointez l’éditeur vers votre fichier source, récupérez le HTML éditable, effectuez les modifications nécessaires, puis créez un nouveau `EditableDocument` à partir du balisage modifié.

```csharp
using (Editor editor = new Editor("YOUR_DOCUMENT_DIRECTORY/sample.docx", new Options.WordProcessingLoadOptions()))
{
    // Your document manipulation code here
}
```

### Guide pas à pas du code
1. **Définir le chemin du fichier d’entrée**  

```csharp
string inputFilePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
```

2. **Créer l’instance `Editor`**  

```csharp
using GroupDocs.Editor;
using GroupDocs.Editor.Options;

Editor editor = new Editor(inputFilePath, new Options.WordProcessingLoadOptions());
```

3. **Modifier le HTML du document**  

```csharp
EditableDocument defaultWordProcessingDoc = editor.Edit();
string allEmbeddedInsideString = defaultWordProcessingDoc.GetEmbeddedHtml();
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
```

4. **Créer un nouveau `EditableDocument` à partir du HTML modifié**  

```csharp
EditableDocument editedDoc = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```

5. **Libérer les objets temporaires**  

```csharp
editedDoc.Dispose();
defaultWordProcessingDoc.Dispose();
editor.Dispose();
```

## Comment convertir Word en RTF
Enregistrer le document édité au format RTF est simple avec les options d’enregistrement appropriées.

```csharp
string outputRtfPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "editedDoc.rtf");
```

```csharp
WordProcessingSaveOptions rtfSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
```

```csharp
using (Editor editor = new Editor(inputFilePath, new Options.WordProcessingLoadOptions()))
{
    editor.Save(editedDoc, outputRtfPath, rtfSaveOptions);
}
editor.Dispose();
```

## Comment enregistrer DOCX en DOCM en utilisant un flux
Lorsque vous avez besoin du format DOCM avec macros, vous pouvez écrire directement dans un `FileStream`.

```csharp
string outputDocmPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "editedDoc.docm");
```

```csharp
WordProcessingSaveOptions docmSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm);
```

```csharp
using (Editor editor = new Editor(inputFilePath, new Options.WordProcessingLoadOptions()))
{
    using (FileStream outputStream = File.Create(outputDocmPath))
    {
        editor.Save(editedDoc, outputStream, docmSaveOptions);
    }
}
editor.Dispose();
```

## Comment convertir DOCX en TXT (texte brut)
L’extraction de texte brut est utile pour l’indexation, la recherche ou les notifications par e‑mail.

```csharp
string outputTxtPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "editedDoc.txt");
```

```csharp
TextSaveOptions textSaveOptions = new TextSaveOptions()
{
    Encoding = Encoding.UTF8,
    PreserveTableLayout = true
};
```

```csharp
using (Editor editor = new Editor(inputFilePath, new Options.WordProcessingLoadOptions()))
{
    editor.Save(editedDoc, outputTxtPath, textSaveOptions);
}
editor.Dispose();
```

## Cas d’utilisation courants et scénarios réels
- **Génération de rapports automatisée :** Convertir les rapports Word analytiques en TXT pour la distribution par e‑mail.  
- **Plateformes d’édition collaborative :** Permettre aux utilisateurs d’éditer des fragments HTML et d’enregistrer le résultat en DOCM ou RTF.  
- **Archivage de documents :** Migrer les anciens fichiers DOCX vers DOCM pour le support des macros tout en préservant le contenu.  
- **Services Web :** Diffuser les conversions DOCX → PDF/RTF à la volée sans fichiers temporaires.

## Conseils de performance pour le traitement par lots de documents Word
- **Libérer rapidement :** Appelez toujours `Dispose()` sur les objets `Editor` et les documents.  
- **Charger judicieusement :** Choisissez les `LoadOptions` les plus spécifiques pour éviter un parsing inutile.  
- **Paralléliser en toute sécurité :** Utilisez `Parallel.ForEach` avec des instances `Editor` distinctes par thread.  
- **Éviter les grosses chaînes en mémoire :** Lors du traitement de documents volumineux, travaillez avec des flux plutôt qu’avec des chaînes HTML complètes.

## Questions fréquemment posées

**Q : Puis‑je éditer un DOCX protégé par mot de passe ?**  
R : Oui. Fournissez le mot de passe via `WordProcessingLoadOptions.Password` lors de la création de l’`Editor`.

**Q : Est‑il possible de convertir de nombreux fichiers en une seule exécution ?**  
R : Absolument. Enveloppez la logique d’un seul fichier dans une boucle ou utilisez `Parallel.ForEach` pour un traitement concurrent.

**Q : GroupDocs.Editor prend‑il en charge .NET Core ?**  
R : La bibliothèque fonctionne avec .NET 5, .NET 6 et .NET Core 3.1 ainsi qu’avec le .NET Framework complet.

**Q : Que se passe‑t‑il des macros lorsque j’enregistre en DOCM ?**  
R : Les macros sont conservées lorsque vous utilisez le format d’enregistrement `Docm` ; elles sont supprimées pour RTF/TXT.

**Q : Comment dépanner une « OutOfMemoryException » lors de gros traitements par lots ?**  
R : Traitez les fichiers en plus petits lots, libérez les objets immédiatement et envisagez d’augmenter la limite de mémoire de l’application.

## Conclusion
Vous disposez désormais d’un flux de travail complet et prêt pour la production pour **how to edit docx** et les convertir en RTF, DOCM ou texte brut à l’aide de GroupDocs.Editor .NET. En suivant les étapes ci‑dessus, vous pouvez automatiser les flux de travail documentaires, gérer le traitement par lots et intégrer une conversion de format transparente dans toute application .NET.

---

**Dernière mise à jour :** 2026-04-07  
**Testé avec :** GroupDocs.Editor 20.10 (dernière version au moment de la rédaction)  
**Auteur :** GroupDocs