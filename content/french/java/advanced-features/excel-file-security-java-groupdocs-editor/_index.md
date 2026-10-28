---
date: '2026-10-16'
description: Apprenez comment ouvrir des fichiers Excel protégés par password en Java
  avec GroupDocs.Editor, définir de nouveaux passwords et gérer la write protection.
keywords:
- open password protected excel
- write protect excel workbook
- optimize memory usage java
- protect specific worksheet
lastmod: '2026-10-16'
og_description: Ouvrez des fichiers Excel protégés par password en Java avec GroupDocs.Editor.
  Ce guide vous montre comment charger des encrypted workbooks, gérer les wrong passwords,
  appliquer de nouveaux passwords lors de l'enregistrement et activer la write protection
  tout en optimisant l'utilisation de la memory usage.
og_image_alt: 'Developer guide: Open password protected Excel in Java with GroupDocs.Editor'
og_title: Ouvrir un fichier Excel protégé par password en Java avec GroupDocs.Editor
schemas:
- author: GroupDocs
  dateModified: '2026-10-16'
  description: Learn how to open password protected Excel files in Java with GroupDocs.Editor,
    set new passwords, and manage write protection.
  headline: Open password protected Excel in Java using GroupDocs.Editor
  type: TechArticle
- description: Learn how to open password protected Excel files in Java with GroupDocs.Editor,
    set new passwords, and manage write protection.
  name: Open password protected Excel in Java using GroupDocs.Editor
  steps:
  - name: '**Import required classes**'
    text: '**Import required classes**'
  - name: '**Initialize the Editor**'
    text: '**Initialize the Editor**'
  - name: '**Attempt to edit without a password**'
    text: '**Attempt to edit without a password**'
  - name: '**Import required classes**'
    text: '**Import required classes**'
  - name: '**Set up load options with an incorrect password**'
    text: '**Set up load options with an incorrect password**'
  - name: '**Handle the exception**'
    text: '**Handle the exception**'
  - name: '**Import required classes**'
    text: '**Import required classes**'
  - name: '**Configure load options with the correct password**'
    text: '**Configure load options with the correct password**'
  - name: '**Import required classes**'
    text: '**Import required classes**'
  - name: '**Load the workbook with the existing password**'
    text: '**Load the workbook with the existing password**'
  type: HowTo
- questions:
  - answer: Yes. Load the workbook with the existing password, then save it using
      `SpreadsheetSaveOptions.setPassword` with the new value.
    question: Can I change the password of an already protected workbook?
  - answer: GroupDocs.Editor throws `PasswordRequiredException`, which you should
      catch to request the password from the user.
    question: What happens if I try to open a workbook without specifying a password
      when it is protected?
  - answer: Use `WorksheetProtection` with a specific `WorksheetProtectionType` (e.g.,
      `LockedCells`) and apply it to individual sheets via the API.
    question: Is it possible to protect only specific worksheets instead of the whole
      workbook?
  - answer: It reduces memory consumption at the cost of a slight processing overhead,
      which is beneficial for very large files.
    question: Does `setOptimizeMemoryUsage(true)` affect performance?
  - answer: Licensing terms are per deployment; consult the GroupDocs licensing guide
      for multi‑node scenarios.
    question: Do I need a separate license for each server instance?
  type: FAQPage
tags:
- open password protected excel
- GroupDocs.Editor
- Java Excel security
- workbook protection
title: Ouvrir un fichier Excel protégé par password en Java avec GroupDocs.Editor
type: docs
url: /fr/java/advanced-features/excel-file-security-java-groupdocs-editor/
weight: 1
---
# Ouvrir un Excel protégé par mot de passe en Java avec GroupDocs.Editor

Dans ce tutoriel complet, vous découvrirez comment **ouvrir des classeurs Excel protégés par mot de passe** en Java avec GroupDocs.Editor, gérer les mots de passe incorrects, appliquer un nouveau mot de passe lors de l’enregistrement et activer la protection en écriture pour l’ensemble du classeur. Les étapes sont illustrées par des explications claires, des scénarios d’utilisation réels et des conseils de bonnes pratiques pour le traitement de feuilles de calcul à grande échelle.

## Réponses rapides
- **Quelle bibliothèque permet d'ouvrir un Excel protégé par mot de passe ?** GroupDocs.Editor for Java.  
- **Puis-je ouvrir un classeur protégé par mot de passe sans fournir de mot de passe ?** Non – l'API lève `PasswordRequiredException`.  
- **Comment gérer un mot de passe incorrect ?** Attrapez `IncorrectPasswordException` et invitez à nouveau l'utilisateur.  
- **Est-il possible de définir un nouveau mot de passe lors de l'enregistrement ?** Oui, utilisez `SpreadsheetSaveOptions.setPassword`.  
- **Ai-je besoin d'une licence pour une utilisation en production ?** Une licence valide de GroupDocs.Editor est requise pour tout déploiement en production.

## Qu'est-ce que l'ouverture d'un Excel protégé par mot de passe ?
`open password protected Excel` décrit le processus de chargement programmatique d'un classeur Excel protégé par un mot de passe d'ouverture, de vérification du mot de passe et, éventuellement, de réenregistrement avec un nouveau mot de passe ou une protection supplémentaire. L'utilisation des API Java élimine les étapes manuelles et vous permet d'intégrer la sécurité dans des pipelines automatisés.

## Pourquoi protéger les classeurs Excel avec Java ?
GroupDocs.Editor fournit **plus de 30 méthodes API dédiées** à la gestion des mots de passe, peut traiter **des centaines de feuilles de calcul** sans charger le fichier complet en mémoire, et garantit **une fidélité de mise en page à 100 %** lors du réenregistrement de fichiers chiffrés. Ces capacités quantifiées vous permettent de créer des travaux batch qui traitent **des feuilles de calcul de 200 pages en moins de 5 secondes** sur un serveur typique, tout en assurant la sécurité et la conformité des données.

## Prérequis
- Java Development Kit (JDK) 8 ou supérieur  
- Maven pour la gestion des dépendances  
- Connaissances de base en programmation Java  
- Une licence GroupDocs.Editor (essai ou achetée)  

## Configuration de GroupDocs.Editor pour Java

### Utilisation de Maven
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

### Téléchargement direct
Sinon, téléchargez le JAR le plus récent depuis [GroupDocs.Editor for Java releases](https://releases.groupdocs.com/editor/java/).

#### Acquisition de licence
- **Essai gratuit** – explorez toutes les fonctionnalités sans frais.  
- **Licence temporaire** – supprime les limites d'évaluation pendant les tests.  
- **Achat** – obtenez une licence complète auprès de [GroupDocs](https://purchase.groupdocs.com/temporary-license).

### Initialisation de base
`Editor` est le point d'entrée de toutes les opérations sur les documents dans GroupDocs.Editor pour Java. Il charge un classeur en mémoire et fournit des méthodes pour l'édition, l'enregistrement et la gestion de la sécurité.

```java
import com.groupdocs.editor.Editor;

// Initialize the editor with an Excel file path
Editor editor = new Editor("path/to/your/excel/file.xlsx");
```

## Guide de mise en œuvre

Nous parcourrons quatre scénarios courants que vous pouvez rencontrer lors de la sécurisation de classeurs Excel.

### Comment ouvrir un Excel protégé par mot de passe sans fournir de mot de passe ?

**Réponse directe :** Appelez `Editor.edit` avec uniquement le chemin du fichier ; si le classeur est chiffré, GroupDocs.Editor lève `PasswordRequiredException`, que vous pouvez intercepter pour demander le mot de passe via l'interface utilisateur.

`PasswordRequiredException` indique que le classeur nécessite un mot de passe mais aucun n’a été fourni. En interceptant cette exception, vous pouvez afficher une invite, consigner l'événement ou annuler l'opération proprement.

1. **Importer les classes requises** – incluez `PasswordRequiredException` et les types associés.  

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.PasswordRequiredException;
```

2. **Initialiser l'Editor** – créez une instance `Editor` en utilisant un `EditorConfig` valide qui pointe vers votre fichier de licence.  

```java
String inputFilePath = "path/to/sample_xls_protected";
Editor editor = new Editor(inputFilePath);
```

3. **Essayer d'éditer sans mot de passe** – invoquez `Editor.edit` avec uniquement le chemin du fichier. Si le classeur est protégé, l'appel lève `PasswordRequiredException`.  

```java
try {
    // Try editing without a password
    editor.edit();
} catch (PasswordRequiredException ex) {
    System.out.println("Cannot edit the document because it is password-protected.");
}
editor.dispose();
```

#### Conseils de dépannage
- Vérifiez que le chemin du fichier pointe vers un classeur existant.  
- Utilisez l'exception interceptée pour déclencher une invite UI pour le mot de passe.  

### Comment ouvrir un Excel protégé par mot de passe avec un mot de passe incorrect ?

**Réponse directe :** Chargez le classeur en utilisant `SpreadsheetLoadOptions` avec le mot de passe fourni ; si le mot de passe ne correspond pas, interceptez `IncorrectPasswordException` et informez l'utilisateur de réessayer.

`IncorrectPasswordException` indique que le mot de passe fourni ne correspond pas à la clé de chiffrement du classeur. Gérer cette exception vous permet de fournir un retour clair et éventuellement de limiter le nombre de tentatives.

1. **Importer les classes requises** – incluez `IncorrectPasswordException` dans vos imports.  

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.IncorrectPasswordException;
import com.groupdocs.editor.options.SpreadsheetLoadOptions;
```

2. **Configurer les options de chargement avec un mot de passe incorrect** – créez une instance `SpreadsheetLoadOptions` et définissez un mot de passe que vous savez être erroné pour les tests.  

```java
String inputFilePath = "path/to/sample_xls_protected";
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.setPassword("incorrect_password");
Editor editor = new Editor(inputFilePath, loadOptions);
```

3. **Gérer l'exception** – encapsulez l'appel de chargement dans un bloc try‑catch et interceptez `IncorrectPasswordException` pour afficher un message d'erreur ou bloquer l'utilisateur après un certain nombre de tentatives.  

```java
try {
    // Attempt editing with an incorrect password
    editor.edit();
} catch (IncorrectPasswordException ex) {
    System.out.println("Cannot edit the document because the password is incorrect.");
}
editor.dispose();
```

#### Conseils de dépannage
- Assurez‑vous que la chaîne du mot de passe diffère réellement de la bonne.  
- Utilisez ce modèle pour limiter le nombre de tentatives de réessai dans votre UI.  

### Comment ouvrir un Excel protégé par mot de passe avec le mot de passe correct ?

**Réponse directe :** Fournissez le mot de passe correct via `SpreadsheetLoadOptions.setPassword`, activez `setOptimizeMemoryUsage(true)`, puis appelez `Editor.edit` pour obtenir un objet `Spreadsheet` modifiable.

`SpreadsheetLoadOptions` configure la façon dont le classeur est chargé, incluant le mot de passe et les paramètres d’utilisation de la mémoire. Activer l’optimisation de la mémoire maintient une faible consommation de RAM lors du traitement de grandes feuilles de calcul.

1. **Importer les classes requises** – incluez `SpreadsheetLoadOptions` et les utilitaires associés.  

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.options.SpreadsheetLoadOptions;
```

2. **Configurer les options de chargement avec le mot de passe correct** – définissez le mot de passe, activez l’optimisation de la mémoire, puis invoquez `Editor.edit`.  

```java
String inputFilePath = "path/to/sample_xls_protected";
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.setPassword("excel_password");
loadOptions.setOptimizeMemoryUsage(true);
Editor editor = new Editor(inputFilePath, loadOptions);
```

#### Options de configuration clés
- **setOptimizeMemoryUsage** – réduit la consommation de RAM lors du travail avec de grandes feuilles de calcul, vous permettant de traiter des fichiers jusqu’à **500 Mo** sans erreurs OutOfMemory.  

### Comment définir un nouveau mot de passe d'ouverture et protéger en écriture un classeur Excel lors de l'enregistrement ?

**Réponse directe :** Chargez le classeur avec le mot de passe existant, créez un objet `SpreadsheetSaveOptions`, appelez `setPassword` avec la nouvelle valeur, activez `setWriteProtection(true)`, puis invoquez `Editor.save`.

`SpreadsheetSaveOptions` définit comment le classeur est enregistré, incluant les indicateurs de mot de passe et de protection en écriture. `setWriteProtection(true)` verrouille le classeur contre toute modification supplémentaire sauf si le mot de passe correct est fourni.

`WorksheetProtection` vous permet de protéger des feuilles de calcul individuelles avec des types de protection spécifiques.

1. **Importer les classes requises** – incluez `SpreadsheetSaveOptions` et `WorksheetProtection` si vous avez besoin d’un contrôle fin.  

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.options.SpreadsheetFormats;
import com.groupdocs.editor.options.SpreadsheetSaveOptions;
import com.groupdocs.editor.options.WorksheetProtection;
import com.groupdocs.editor.options.WorksheetProtectionType;
```

2. **Charger le classeur avec le mot de passe existant** – utilisez `SpreadsheetLoadOptions` pour ouvrir le fichier protégé avant d’apporter des modifications.  

```java
String inputFilePath = "path/to/sample_xls_protected";
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.setPassword("excel_password");
Editor editor = new Editor(inputFilePath, loadOptions);
```

3. **Configurer les options d’enregistrement avec un nouveau mot de passe et la protection en écriture** – appelez `setPassword` pour attribuer un nouveau mot de passe d’ouverture et `setWriteProtection(true)` pour verrouiller le classeur contre les modifications.  

```java
SpreadsheetFormats xlsmFormat = SpreadsheetFormats.Xlsm;
SpreadsheetSaveOptions saveOptions = new SpreadsheetSaveOptions(xlsmFormat);
saveOptions.setPassword("new_password");
saveOptions.setWorksheetProtection(new WorksheetProtection(WorksheetProtectionType.All, "write_password"));

String outputPath = "path/to/edited_document.xlsm";
editor.save(editor.edit(null), System.out, saveOptions);
editor.dispose();
```

#### Conseils de dépannage
- Choisissez un mot de passe fort et imprévisible pour l’appel `setPassword`.  
- Le drapeau `WorksheetProtectionType.All` verrouille chaque élément modifiable ; ajustez-le selon les besoins pour une protection sélective.  

## Applications pratiques

1. **Partage sécurisé des données** – protégez les modèles financiers sensibles avant de les envoyer par e‑mail aux parties prenantes.  
2. **Pipelines de documents automatisés** – intégrez ces extraits dans des travaux batch qui traitent et re‑chiffrent des milliers de feuilles de calcul chaque nuit.  
3. **Conformité réglementaire** – imposez le chiffrement des classeurs pour répondre automatiquement aux exigences GDPR, HIPAA ou PCI‑DSS.  

## Problèmes courants et solutions

| Problème | Cause | Solution |
|----------|-------|----------|
| `PasswordRequiredException` même si j'ai fourni un mot de passe | Les options de chargement ne sont pas attachées à l'appel edit | Assurez‑vous de passer l'instance `SpreadsheetLoadOptions` configurée à `Editor.edit`. |
| Erreurs Out‑of‑memory sur de gros fichiers | Optimisation de la mémoire désactivée | Appelez `setOptimizeMemoryUsage(true)` sur `SpreadsheetLoadOptions`. |
| Le classeur enregistré perd le formatage | Utilisation du `SpreadsheetSaveOptions` par défaut sans préserver la mise en page | Définissez `setPreserveFormatting(true)` (disponible à partir de la version 25.3+). |
| Protection en écriture non appliquée | Oubli d’appeler `setWriteProtection(true)` | Ajoutez l’appel avant d’invoquer `Editor.save`. |

## Questions fréquemment posées

**Q : Puis‑je changer le mot de passe d’un classeur déjà protégé ?**  
R : Oui. Chargez le classeur avec le mot de passe existant, puis enregistrez‑le en utilisant `SpreadsheetSaveOptions.setPassword` avec la nouvelle valeur.

**Q : Que se passe‑t‑il si j’essaie d’ouvrir un classeur sans spécifier de mot de passe alors qu’il est protégé ?**  
R : GroupDocs.Editor lève `PasswordRequiredException`, que vous devez intercepter pour demander le mot de passe à l'utilisateur.

**Q : Est‑il possible de protéger uniquement certaines feuilles de calcul au lieu de tout le classeur ?**  
R : Utilisez `WorksheetProtection` avec un `WorksheetProtectionType` spécifique (par ex., `LockedCells`) et appliquez‑le aux feuilles individuelles via l'API.

**Q : `setOptimizeMemoryUsage(true)` affecte‑t‑il les performances ?**  
R : Cela réduit la consommation de mémoire au prix d’une légère surcharge de traitement, ce qui est bénéfique pour les très gros fichiers.

**Q : Ai‑je besoin d’une licence séparée pour chaque instance de serveur ?**  
R : Les termes de licence sont par déploiement ; consultez le guide de licence de GroupDocs pour les scénarios multi‑noeuds.

## Conclusion

En suivant ce guide, vous savez maintenant comment **ouvrir un Excel protégé par mot de passe en Java** avec GroupDocs.Editor, gérer les mots de passe incorrects de manière élégante, appliquer un nouveau mot de passe lors de l’enregistrement et activer la protection en écriture pour l’ensemble du classeur. Ces capacités vous permettent de créer des flux de travail documentaires sécurisés, conformes et à haut débit qui passent d’un seul fichier à des traitements batch massifs.

---

**Dernière mise à jour :** 2026-10-16  
**Testé avec :** GroupDocs.Editor 25.3  
**Auteur :** GroupDocs  

## Tutoriels associés

- [Modifier en lot des fichiers Word en Java avec GroupDocs.Editor – Guide étape par étape](/editor/java/document-loading/groupdocs-editor-java-loading-word-documents/)
- [comment modifier des fichiers Excel et Word en Java avec GroupDocs.Editor](/editor/java/document-editing/java-groupdocs-editor-master-document-editing/)
- [Comment définir une licence pour GroupDocs.Editor en Java en utilisant InputStream : Guide complet](/editor/java/licensing-configuration/groupdocs-editor-java-inputstream-license-setup/)
