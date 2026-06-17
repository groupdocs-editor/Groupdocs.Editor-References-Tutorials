---
date: '2026-05-22'
description: Apprenez comment extraire des images de Word en utilisant GroupDocs.Editor
  for Java, y compris les étapes load word document java et extract images java, extract
  css java examples.
keywords:
- extract pictures from word
- load word document java
- extract images java
- extract css java
schemas:
- author: GroupDocs
  dateModified: '2026-05-22'
  description: Learn how to extract pictures from Word using GroupDocs.Editor for
    Java, including load word document java steps and extract images java, extract
    css java examples.
  headline: How to Extract Pictures from Word Documents Using GroupDocs.Editor for
    Java
  type: TechArticle
- description: Learn how to extract pictures from Word using GroupDocs.Editor for
    Java, including load word document java steps and extract images java, extract
    css java examples.
  name: How to Extract Pictures from Word Documents Using GroupDocs.Editor for Java
  steps:
  - name: Load and Prepare the Document for Editing
    text: '*The `FontExtractionOptions.ExtractAll` flag guarantees that every embedded
      font is available for extraction.*'
  - name: Extract Images, Fonts, and Stylesheets
    text: '*These three calls give you collections of each resource type, ready for
      further processing.*'
  - name: Save Extracted Resources to Disk
    text: '*Each loop writes the corresponding resource to the `outputFolderPath`,
      preserving the original filenames.*'
  - name: Retrieve Resource Content Directly (Optional)
    text: 'If you need the raw bytes or a Base64 string—for example, to embed an image
      in an HTML email—use:'
  type: HowTo
- questions:
  - answer: Yes, it supports DOCX, DOC, and other Microsoft Word formats.
    question: Is GroupDocs.Editor compatible with all Word file formats?
  - answer: Absolutely. Provide the password via `WordProcessingLoadOptions` when
      creating the `Editor`.
    question: Can I extract resources from password‑protected documents?
  - answer: It’s optimized for speed; for files over 200 MB we recommend batch processing
      or extracting sections sequentially.
    question: How does the API perform with very large documents?
  - answer: Yes. The API is framework‑agnostic; just include the dependency and inject
      `Editor` where needed.
    question: Can I integrate this with Spring Boot or other Java frameworks?
  - answer: Call only `beforeEdit.getImages()` and skip the font/CSS extraction steps.
    question: What if I need to extract only images and not fonts or CSS?
  type: FAQPage
title: Comment extraire des images de documents Word avec GroupDocs.Editor for Java
type: docs
url: /fr/java/word-processing-documents/edit-extract-resources-groupdocs-editor-java/
weight: 1
---

# Comment extraire des images de documents Word avec GroupDocs.Editor pour Java

Si vous devez **extraire des images de Word** de façon programmatique, vous êtes au bon endroit. Dans ce tutoriel, nous parcourrons le chargement d’un document Word en Java, la configuration de l’éditeur et l’extraction d’images, de polices et de CSS—exactement les étapes nécessaires pour automatiser les pipelines de traitement de documents avec GroupDocs.Editor pour Java.

**Ce que vous apprendrez :**
- Comment **charger un document Word en Java** avec GroupDocs.Editor  
- Comment **extraire des images en Java** et d’autres ressources intégrées  
- Comment **extraire du CSS en Java** pour réutiliser le style  
- Meilleures pratiques pour enregistrer ces ressources sur le disque  
- Scénarios réels où l’extraction de ressources fait gagner du temps et des efforts  

Prêt à rationaliser votre flux de travail documentaire ? Plongeons‑y !

## Réponses rapides
- **Que signifie « extraire des images de word » ?** Cela signifie extraire de façon programmatique des images, des polices, du CSS et d’autres ressources intégrées d’un fichier Word.  
- **Quelle bibliothèque gère cela en Java ?** GroupDocs.Editor pour Java fournit une API de haut niveau pour cette tâche.  
- **Ai‑je besoin d’une licence ?** Un essai gratuit suffit pour les tests ; une licence complète est requise pour la production.  
- **Puis‑je traiter les fichiers DOCX et DOC ?** Oui—les deux sont entièrement pris en charge.  
- **Est‑ce sûr pour les gros documents ?** Oui, mais envisagez un traitement par lots et une libération correcte de la mémoire pour les fichiers de plus de 200 Mo.

## Qu’est‑ce que l’extraction de ressources dans les documents Word ?
L’extraction de ressources désigne la récupération systématique de toutes les ressources intégrées d’un fichier Word, y compris les images, les polices personnalisées, les feuilles de style, les macros et d’autres objets binaires. En extrayant ces composants, les développeurs peuvent les réutiliser dans des applications séparées, les archiver pour la conformité, ou les transformer en formats adaptés au web, étendant ainsi la valeur du document original.

## Pourquoi utiliser GroupDocs.Editor pour Java ?
GroupDocs.Editor pour Java abstrait le format Office Open XML, vous permettant de vous concentrer sur **comment extraire des images de word** sans écrire de code ZIP ou XML de bas niveau. Il prend en charge **plus de 30 formats d’entrée et de sortie** et peut traiter des documents jusqu’à **500 Mo** sans charger le fichier complet en mémoire, offrant à la fois rapidité et évolutivité.

## Prérequis
- **Maven** (ou téléchargement direct du JAR) pour gérer les dépendances.  
- **JDK 8+** installé sur votre machine de développement.  
- Un IDE comme **IntelliJ IDEA** ou **Eclipse** pour éditer et exécuter le code Java.

## Configuration de GroupDocs.Editor pour Java
Ajoutez le dépôt et la dépendance à votre `pom.xml` :

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

Vous pouvez également télécharger le dernier JAR depuis [GroupDocs.Editor for Java releases](https://releases.groupdocs.com/editor/java/).

### Acquisition de licence
- **Essai gratuit :** Idéal pour explorer l’API.  
- **Licence temporaire :** Obtenez‑en une depuis la [Page de licence temporaire GroupDocs](https://purchase.groupdocs.com/temporary-license).  
- **Licence complète :** Achetez‑la pour une utilisation en production sans restriction.

### Initialisation de base
`Editor` est le point d’entrée principal de GroupDocs.Editor pour Java qui fournit des méthodes pour charger, modifier et extraire des ressources à partir de fichiers Word.

Créez une instance `Editor` pointant vers votre fichier Word :

```java
String inputFilePath = "YOUR_DOCUMENT_DIRECTORY";
Editor editor = new Editor(inputFilePath, new WordProcessingLoadOptions());
```

## Comment extraire des ressources d’un document Word
L’extraction de ressources commence par charger le fichier Word cible dans une instance `Editor`, puis en configurant `WordProcessingEditOptions` pour activer l’extraction d’images, de polices et de CSS. Une fois le document préparé, l’API fournit des collections pour chaque type de ressource, qui peuvent être parcourues et enregistrées sur le système de fichiers ou traitées davantage selon les exigences de votre flux de travail.

### Étape 1 : Charger et préparer le document pour l’édition
```java
// Initialize editor and edit options
String inputFilePath = "YOUR_DOCUMENT_DIRECTORY";
Editor editor = new Editor(inputFilePath, new WordProcessingLoadOptions());
WordProcessingEditOptions editOptions = new WordProcessingEditOptions();
editOptions.setFontExtraction(FontExtractionOptions.ExtractAll);
EditableDocument beforeEdit = editor.edit(editOptions);
```  
*Le drapeau `FontExtractionOptions.ExtractAll` garantit que chaque police intégrée est disponible pour l’extraction.*

### Étape 2 : Extraire les images, les polices et les feuilles de style
```java
List<IImageResource> images = beforeEdit.getImages();
```  

```java
List<FontResourceBase> fonts = beforeEdit.getFonts();
```  

```java
List<CssText> stylesheets = beforeEdit.getCss();
```  
*Ces trois appels vous fournissent des collections de chaque type de ressource, prêtes pour un traitement ultérieur.*

### Étape 3 : Enregistrer les ressources extraites sur le disque
```java
String outputFolderPath = "YOUR_OUTPUT_DIRECTORY";
for (int i = 0; i < images.size(); i++) {
    IImageResource oneImage = images.get(i);
    File outputFile = new File(outputFolderPath + oneImage.getFilenameWithExtension());
    oneImage.save(outputFile.getAbsolutePath());
}
```  

```java
for (int i = 0; i < fonts.size(); i++) {
    FontResourceBase oneFont = fonts.get(i);
    File outputFile = new File(outputFolderPath + oneFont.getFilenameWithExtension());
    oneFont.save(outputFile.getAbsolutePath());
}
```  

```java
for (int i = 0; i < stylesheets.size(); i++) {
    CssText oneStylesheet = stylesheets.get(i);
    File outputFile = new File(outputFolderPath + oneStylesheet.getFilenameWithExtension());
    oneStylesheet.save(outputFile.getAbsolutePath());
}
```  
*Chaque boucle écrit la ressource correspondante dans le `outputFolderPath`, en conservant les noms de fichiers d’origine.*

### Étape 4 : Récupérer le contenu de la ressource directement (optionnel)
Si vous avez besoin des octets bruts ou d’une chaîne Base64—par exemple, pour intégrer une image dans un e‑mail HTML—utilisez :

```java
InputStream ms = images.get(0).getByteContent(); // raw bytes
String base64EncodedResource = images.get(0).getTextContent(); // Base64 string
```

## Problèmes courants et solutions
| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| **OutOfMemoryError on large files** | Les ressources sont chargées en mémoire en une seule fois. | Traitez les documents par lots plus petits et appelez `editor.dispose()` après chaque fichier. |
| **Missing fonts after extraction** | Extraction des polices désactivée dans les options. | Assurez‑vous que `editOptions.setFontExtraction(FontExtractionOptions.ExtractAll)` est défini. |
| **Images saved with wrong extension** | Certaines images n'ont pas de détection correcte du type MIME. | Vérifiez `oneImage.getFilenameWithExtension()` avant l’enregistrement ; renommez si nécessaire. |

## Questions fréquemment posées

**Q : GroupDocs.Editor est‑il compatible avec tous les formats de fichiers Word ?**  
R : Oui, il prend en charge DOCX, DOC et d’autres formats Microsoft Word.

**Q : Puis‑je extraire des ressources de documents protégés par mot de passe ?**  
R : Absolument. Fournissez le mot de passe via `WordProcessingLoadOptions` lors de la création de l’`Editor`.

**Q : Comment l’API se comporte‑t‑elle avec des documents très volumineux ?**  
R : Elle est optimisée pour la vitesse ; pour les fichiers de plus de 200 Mo nous recommandons le traitement par lots ou l’extraction séquentielle de sections.

**Q : Puis‑je intégrer cela avec Spring Boot ou d’autres frameworks Java ?**  
R : Oui. L’API est indépendante du framework ; il suffit d’inclure la dépendance et d’injecter `Editor` où nécessaire.

**Q : Que faire si je ne veux extraire que les images et pas les polices ou le CSS ?**  
R : Appelez uniquement `beforeEdit.getImages()` et ignorez les étapes d’extraction des polices/CSS.

## Conclusion
Vous disposez maintenant d’un guide complet et prêt pour la production sur **comment extraire des images de word** à l’aide de GroupDocs.Editor pour Java. En chargeant le document, en configurant les options d’édition et en parcourant les collections de ressources retournées, vous pouvez automatiser l’archivage, la création de modèles et la génération de contenu dynamique avec facilité.

**Étapes suivantes :**  
- Expérimentez avec différents `WordProcessingEditOptions` pour affiner l’extraction.  
- Combinez ce flux de travail avec un SDK de stockage cloud pour télécharger les ressources directement vers S3 ou Azure Blob.  
- Explorez les API de conversion GroupDocs pour transformer les ressources extraites en d’autres formats.

---

**Last Updated:** 2026-05-22  
**Tested With:** GroupDocs.Editor 25.3 for Java  
**Author:** GroupDocs  

---

## Tutoriels associés

- [Comment extraire des ressources des documents Word – GroupDocs.Editor Java](/editor/java/word-processing-documents/edit-extract-resources-groupdocs-editor-java/)
- [Charger un document Word Java avec GroupDocs.Editor – Guide complet](/editor/java/document-loading/load-word-document-groupdocs-editor-java/)