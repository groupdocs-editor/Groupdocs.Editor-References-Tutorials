---
date: '2026-06-16'
description: Apprenez comment extraire les métadonnées, comment extraire les métadonnées
  en Java, et détecter le type de document Java avec GroupDocs.Editor pour Java sur
  les fichiers Word, Excel et texte.
keywords:
- how to extract metadata
- java get page count
- java get document properties
- java read document info
- java detect file format
schemas:
- author: GroupDocs
  dateModified: '2026-06-16'
  description: Learn how to extract metadata, how to extract metadata in Java, and
    detect document type java with GroupDocs.Editor for Java across Word, Excel, and
    text files.
  headline: How to Extract Metadata from Documents Java using GroupDocs.Editor
  type: TechArticle
- questions:
  - answer: GroupDocs.Editor focuses on editable formats (DOCX, XLSX, etc.). For PDFs,
      use GroupDocs.Metadata or GroupDocs.Viewer.
    question: Can I extract metadata from PDF files with the same API?
  - answer: Call `info.getDocumentType()` which returns an enum (e.g., `DocumentType.WordProcessing`,
      `DocumentType.Spreadsheet`).
    question: How do I detect the document type without casting?
  - answer: Yes—`WordProcessingDocumentInfo` and `SpreadsheetDocumentInfo` expose
      methods like `getCustomProperties()`.
    question: Is it possible to extract custom properties embedded in Office files?
  - answer: No, a single GroupDocs.Editor license covers all supported formats.
    question: Do I need a separate license for each document type?
  - answer: Java 8 or later; newer LTS versions (11, 17) are fully supported.
    question: What Java version is required?
  type: FAQPage
title: Comment extraire les métadonnées des documents Java à l'aide de GroupDocs.Editor
type: docs
url: /fr/java/advanced-features/groupdocs-editor-java-document-extraction-guide/
weight: 1
---

# Comment extraire les métadonnées des documents Java avec GroupDocs.Editor

Si vous êtes un développeur **fatigué de récupérer manuellement des informations à partir de fichiers Word, Excel ou texte brut**, ce guide vous montre **comment extraire les métadonnées** rapidement et de manière fiable. Vous verrez pourquoi GroupDocs.Editor pour Java est la bibliothèque de référence pour **detect document type java**, comment lire les propriétés telles que le nombre de pages, l’auteur et l’état de chiffrement, et comment gérer les fichiers protégés par mot de passe — le tout avec des extraits de code concis et prêts pour la production.

## Réponses rapides
- **Que signifie « extract document metadata java » ?** Il s’agit de lire programmétiquement des propriétés telles que le format, le nombre de pages, la taille et l’état de chiffrement des documents en Java.  
- **Quelle bibliothèque aide à cela ?** GroupDocs.Editor pour Java fournit une API simple pour l’extraction des métadonnées et la détection du type.  
- **Puis‑je détecter le type de document java dans le cadre du processus ?** Oui — en inspectant l’`IDocumentInfo` retourné, vous pouvez déterminer si le fichier est un document Word, une feuille de calcul ou un texte.  
- **Ai‑je besoin d’une licence ?** Un essai gratuit suffit pour l’évaluation ; une licence permanente est requise pour la production.  
- **Quelles sont les principales prérequis ?** Java 8+, Maven (ou téléchargement manuel du JAR), et des connaissances de base en Java.

## Qu’est‑ce que extract document metadata java ?
**Extraire les métadonnées d’un document en Java signifie récupérer des informations descriptives — comme le format du fichier, le nombre de pages, l’auteur ou l’état de chiffrement — sans charger le contenu complet du document.** Cette approche légère accélère l’indexation, l’archivage et les contrôles de conformité en vous permettant d’analyser rapidement les fichiers, de réduire la consommation de mémoire et de prendre des décisions éclairées avant d’ouvrir les documents complets.

## Pourquoi utiliser GroupDocs.Editor pour Java afin de detect document type java ?
**GroupDocs.Editor identifie automatiquement le type de document et expose des propriétés spécifiques au type pour plus de 30 formats éditables, traitant des fichiers jusqu’à 2 Go sans charger le contenu complet en mémoire.** Il gère également les fichiers protégés par mot de passe dès le départ, ce qui en fait la solution la plus efficace pour les scénarios de **detect document type java**.

## Prérequis
- **Java Development Kit (JDK)** 8 ou plus récent.  
- **Maven** pour la gestion des dépendances (ou téléchargement manuel du JAR).  
- Familiarité de base avec les classes Java et la gestion des exceptions.  

## Configuration de GroupDocs.Editor pour Java

### Installation via Maven
Add the repository and dependency to your `pom.xml`:

```xml
<repositories>
   <repository>
      <id>repository.groupdocs.com</id>
      <name>GroupDocs Repository</name>
      <url>https://releases.groupdocs.com/editor/java/</url>
   </repository>
</repositories>

<dependencies>
   <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-editor</artifactId>
      <version>25.3</version>
   </dependency>
</dependencies>
```

### Téléchargement direct
Alternatively, download the latest JAR from [GroupDocs.Editor for Java releases](https://releases.groupdocs.com/editor/java/).

### Acquisition de licence
- **Essai gratuit** – explorez l’API sans frais.  
- **Licence temporaire** – obtenez une clé à durée limitée via [this link](https://purchase.groupdocs.com/temporary-license).  
- **Achat** – achetez une licence permanente pour les déploiements en production.

#### Initialisation et configuration de base
La classe `Editor` est le point d’entrée qui charge un document et fournit l’accès à ses métadonnées. Après avoir créé une instance `Editor`, vous pouvez appeler `getDocumentInfo(null)` pour récupérer des informations légères.

```java
import com.groupdocs.editor.Editor;

public class DocumentEditorSetup {
    public static void main(String[] args) {
        String filePath = "YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX";
        Editor editor = new Editor(filePath);
        // Initialize your document processing workflow here
        editor.dispose();
    }
}
```

## Comment extraire les métadonnées en Java
Chargez le document, demandez son `IDocumentInfo`, puis castiez-le vers la classe d’informations spécifique au format. Ce schéma fonctionne pour les fichiers Word, Excel et texte brut tout en maintenant une faible utilisation de la mémoire, car seul l’en‑tête du document est lu. En extrayant d’abord les métadonnées, vous pouvez décider de traiter le contenu complet, de router le fichier ou de rejeter les formats non pris en charge.

### Fonctionnalité 1 : Extraction des métadonnées des documents Word
#### Charger le document
L’interface `DocumentInfo` représente les métadonnées génériques pour tout fichier pris en charge. Passer le chemin du fichier au constructeur `Editor` prépare le document pour l’inspection.

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.IDocumentInfo;
import com.groupdocs.editor.metadata.WordProcessingDocumentInfo;

String docxInputFilePath = "YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX";
Editor editorDocx = new Editor(docxInputFilePath);
```

#### Extraire les informations du document
`WordProcessingDocumentInfo` est une implémentation concrète qui ajoute des propriétés spécifiques à Word telles que le nombre de pages, l’auteur et l’état de chiffrement.

```java
IDocumentInfo infoDocx = editorDocx.getDocumentInfo(null);
if (infoDocx instanceof WordProcessingDocumentInfo) {
    WordProcessingDocumentInfo casted = (WordProcessingDocumentInfo) infoDocx;
    // Access properties like format, page count, and more
}
editorDocx.dispose();
```

*Explication* :  
- `getDocumentInfo(null)` récupère les métadonnées sans charger le corps complet du document.  
- Le cast vers `WordProcessingDocumentInfo` débloque les attributs spécifiques à Word tels que **le nombre de pages**, le nom de l’auteur et le drapeau de chiffrement.

### Fonctionnalité 2 : Detect document type java – Feuilles de calcul
#### Charger le fichier de feuille de calcul
`SpreadsheetDocumentInfo` fournit des métadonnées spécifiques aux feuilles de calcul comme le nombre de feuilles et la taille totale.

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.IDocumentInfo;
import com.groupdocs.editor.metadata.SpreadsheetDocumentInfo;

String xlsxInputFilePath = "YOUR_DOCUMENT_DIRECTORY/SAMPLE_XLSX";
Editor editorXlsx = new Editor(xlsxInputFilePath);
```

#### Vérifier et extraire les informations
En utilisant l’opérateur `instanceof`, vous pouvez **detect document type java** puis lire les métadonnées spécifiques aux feuilles de calcul telles que le nombre de feuilles et la taille totale.

```java
IDocumentInfo infoXlsx = editorXlsx.getDocumentInfo(null);
if (infoXlsx instanceof SpreadsheetDocumentInfo) {
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo) infoXlsx;
    // Retrieve properties like tab count, size, etc.
}
editorXlsx.dispose();
```

*Explication* :  
- Le test `instanceof` indique si le fichier est une feuille de calcul, vous permettant d’appeler `getSheetCount()` et d’autres méthodes propres aux feuilles de calcul.

### Fonctionnalité 3 : Gestion des documents protégés par mot de passe
#### Charger le document protégé
Le constructeur `Editor` accepte un objet `LoadOptions` optionnel où vous pouvez fournir un mot de passe.

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.IDocumentInfo;
import com.groupdocs.editor.PasswordRequiredException;
import com.groupdocs.editor.IncorrectPasswordException;

String xlsInputFilePath = "YOUR_DOCUMENT_DIRECTORY/SAMPLE_XLS_PROTECTED";
Editor editorXls = new Editor(xlsInputFilePath);
```

#### Essayer d’accéder avec le mot de passe
Si le mot de passe est absent ou incorrect, l’API lève `PasswordRequiredException` ou `IncorrectPasswordException`, vous permettant de demander le mot de passe à l’utilisateur ou d’enregistrer le problème.

```java
try {
    IDocumentInfo infoXls = editorXls.getDocumentInfo(null); // Attempt without password
} catch (PasswordRequiredException ex) {
    System.out.println("A password is required to access this document.");
}

try {
    IDocumentInfo infoXls = editorXls.getDocumentInfo("incorrect_password");
} catch (IncorrectPasswordException ex) {
    System.out.println("The provided password is incorrect. Please try again.");
}

IDocumentInfo infoXls = editorXls.getDocumentInfo("excel_password"); // Correct password
if (infoXls instanceof SpreadsheetDocumentInfo) {
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo) infoXls;
    // Extract document details
}
editorXls.dispose();
```

*Explication* :  
- Les exceptions explicites de l’API vous permettent d’implémenter une logique de secours élégante sans deviner.

### Fonctionnalité 4 : Extraction des métadonnées des documents texte
#### Charger le document texte
Pour les formats texte brut (TXT, XML, CSV), la classe `TextDocumentInfo` renvoie l’encodage, le nombre de lignes et les détails de la taille du fichier.

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.IDocumentInfo;
import com.groupdocs.editor.metadata.TextualDocumentInfo;

String xmlInputFilePath = "YOUR_DOCUMENT_DIRECTORY/SAMPLE_XML";
Editor editorXml = new Editor(xmlInputFilePath);
```

#### Extraire et afficher les informations
Utilisez les getters de `TextDocumentInfo` pour récupérer les propriétés légères dont vous avez besoin pour l’indexation ou la validation.

```java
IDocumentInfo infoXml = editorXml.getDocumentInfo(null);
if (infoXml instanceof TextualDocumentInfo) {
    TextualDocumentInfo casted1 = (TextualDocumentInfo) infoXml;
    // Access encoding, size, etc.
}
editorXml.dispose();
```

*Explication* :  
- Cette approche fonctionne pour les formats texte où vous avez principalement besoin de l’encodage et des métadonnées de taille de fichier.

## Applications pratiques
- **Archivage automatisé des documents** – Extraire les métadonnées pour taguer et stocker les fichiers dans un référentiel consultable.  
- **Automatisation des flux de travail** – Utiliser les métadonnées pour acheminer les documents vers le bon service ou déclencher des processus en aval.  
- **Migration de données** – Conserver les propriétés originales lors du déplacement des fichiers entre systèmes, garantissant la conformité réglementaire.

## Considérations de performance
- **Libérer les éditeurs** – Appelez toujours `dispose()` pour libérer les ressources natives et éviter les fuites de mémoire.  
- **Fichiers volumineux** – Traitez en flux ou en morceaux ; `getDocumentInfo(null)` lit uniquement l’en‑tête, maintenant l’utilisation RAM sous 50 Mo même pour des fichiers de 2 Go.  
- **Profilage** – Utilisez des profileurs Java (par ex., VisualVM) pour repérer les goulots d’étranglement lors du traitement de milliers de fichiers.

## Problèmes courants et dépannage
| Symptôme | Cause probable | Solution |
|----------|----------------|----------|
| `PasswordRequiredException` même si le fichier n’est pas protégé | Chemin de fichier incorrect ou fichier corrompu | Vérifiez le chemin et l’intégrité du fichier |
| `null` renvoyé pour les métadonnées | Utilisation d’une version de bibliothèque obsolète | Mettez à jour vers la dernière version de GroupDocs.Editor |
| Performance faible sur les gros fichiers Excel | Chargement complet du fichier en mémoire | Utilisez `getDocumentInfo(null)` (métadonnées uniquement) et traitez par lots |

## Questions fréquentes

**Q : Puis‑je extraire les métadonnées des fichiers PDF avec la même API ?**  
R : GroupDocs.Editor se concentre sur les formats éditables (DOCX, XLSX, etc.). Pour les PDF, utilisez GroupDocs.Metadata ou GroupDocs.Viewer.

**Q : Comment détecter le type de document sans cast ?**  
R : Appelez `info.getDocumentType()` qui renvoie une énumération (par ex., `DocumentType.WordProcessing`, `DocumentType.Spreadsheet`).

**Q : Est‑il possible d’extraire les propriétés personnalisées intégrées dans les fichiers Office ?**  
R : Oui — `WordProcessingDocumentInfo` et `SpreadsheetDocumentInfo` exposent des méthodes comme `getCustomProperties()`.

**Q : Ai‑je besoin d’une licence séparée pour chaque type de document ?**  
R : Non, une seule licence GroupDocs.Editor couvre tous les formats pris en charge.

**Q : Quelle version de Java est requise ?**  
R : Java 8 ou ultérieure ; les versions LTS plus récentes (11, 17) sont entièrement prises en charge.

## Conclusion
Vous disposez maintenant d’un flux de travail complet et prêt pour la production pour **how to extract metadata** et **detect document type java** en utilisant GroupDocs.Editor. Intégrez ces extraits à votre propre logique métier pour automatiser l’archivage, les contrôles de conformité ou tout scénario où la connaissance du document est précieuse.

---

**Dernière mise à jour :** 2026-06-16  
**Testé avec :** GroupDocs.Editor 25.3 pour Java  
**Auteur :** GroupDocs

## Tutoriels associés

- [Charger un document Word Java avec GroupDocs.Editor – Guide complet](/editor/java/document-loading/load-word-document-groupdocs-editor-java/)
- [Comment modifier des fichiers Excel et Word en Java avec GroupDocs.Editor](/editor/java/document-editing/java-groupdocs-editor-master-document-editing/)
- [Comment extraire des ressources des documents Word – GroupDocs.Editor Java](/editor/java/word-processing-documents/edit-extract-resources-groupdocs-editor-java/)