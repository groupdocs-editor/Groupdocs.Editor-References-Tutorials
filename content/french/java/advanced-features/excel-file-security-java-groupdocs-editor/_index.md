---
date: '2026-02-01'
description: Apprenez à enregistrer un fichier Excel avec un mot de passe en Java
  à l’aide de GroupDocs.Editor, et découvrez comment ouvrir un Excel sans mot de passe
  et ajouter une protection en écriture.
keywords:
- Excel file security in Java
- GroupDocs.Editor for Java
- Java document password protection
title: Enregistrer un fichier Excel avec un mot de passe en Java à l'aide de GroupDocs.Editor
type: docs
url: /fr/java/advanced-features/excel-file-security-java-groupdocs-editor/
weight: 1
---

# Enregistrer Excel avec mot de passe en Java avec GroupDocs.Editor

Dans ce guide, vous apprendrez comment **enregistrer Excel avec mot de passe** en utilisant GroupDocs.Editor en Java. Nous parcourrons l'ouverture des fichiers Excel — à la fois avec et sans mot de passe — la gestion des tentatives de mot de passe incorrectes, et enfin l'application de la protection en écriture lors de l'enregistrement du document. À la fin, Excel dans vos applications Java.

## Réponses rapides
- **Comment ouvrir un fichier Excel sans mot de passe ?** Utilisez `Editor.edit()` directement ; capturez `PasswordRequiredException` si le fichier est protégé.  
- **Quelle exception est levée pour un mot de passe incorrect ?** `IncorrectPasswordException`.  
- **Puis-je définir un nouveau mot de passe lors de l'enregistrement ?** Oui, via `(...) une feuille ?** Utilisez `WorksheetProtection` avec `WorksheetProtectionType.All`.  
- **Quel artefact Maven faut‑il ?** `com.groupdocs:groupdocs-editor:25.3`.

## Ce que vous apprendrez

- Intégrer GroupDocs.Editor dans vos projets Java  
- Ouvrir des fichiers Excel **sans mot de passe** ou avec des mots de passe corrects/incorrects  
- Gérer efficacement les tentatives de mot de passe incorrectes  
 nouveaux mots de passe lors de l'enregistrement  
- Optimiser les performances du traitement de documents  

## Prérequis

Avant de commencer, assurez‑vous de disposer de ce qui suit ise.  
- **Maven** : pour gérer les dépendances et construire votre projet efficacement.  
- **Connaissances de base en Java** : la: nous utiliserure via Maven.  

## Configuration de GroupDocs.Editor pour Java

Pour commencer à travailler avec GroupDocs.Editor dans vos projets Java, suivez ces étapes d'installation :

### Utilisation de Maven

Ajoutez le dépôt et la dépendance suivants à votre fichier `pom.xml` :

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

Sinon, téléchargez la dernière version depuis [GroupDocs.Editor for Java releases](https://releases.groupdocs.com/editor/java/).

#### Acquisition de licence

- **Essai gratuit** : commencez par télécharger une version d'essai gratuite pour explorer les fonctionnalités.  
- **Licence temporaire** : demandez une licence temporaire pour supprimer les limitations pendant votre période d'évaluation.  
- **Achat** : pour une utilisation en production, achetez une licence sur [GroupDocs](https://purchase.groupdocs.com/temporary-license).

### Initialisation de base

Pour initialiser GroupDocs.Editor dans votre application Java :

```java
import com.groupdocs.editor.Editor;

// Initialize the editor with an Excel file path
Editor editor = new Editor("path/to/your/excel/file.xlsx");
```

## Guide de mise en œuvre

Nous décomposerons la mise en œuvre en quatre fonctionnalités distinctes, chacune répondant à une fonctionnalité spécifique liée à la sécurité des documents.

### Comment ouvrir Excel sans mot de passe

Si vous devez vérifier si un classeur peut être accédé sans mot de passe, cet extrait montre l'approche.

#### Étape 1 – Importer les classes requises

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.PasswordRequiredException;
```

#### Étape 2 – Initialiser l'éditeur

```java
String inputFilePath = "path/to/sample_xls_protected";
Editor editor = new Editor(inputFilePath);
```

#### Étape 3 – Tenter d'ouvrir sans mot de passe

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
- Capturez `PasswordRequiredException` pour gérer gracieusement les fichiers protégés.

### Comment ouvrir Excel avec un mot de passe incorrect

Lorsqu'un utilisateur fournit un mauvais mot de passe, `IncorrectPasswordException` est levée. Cet exemple montre comment capturer ce scénario.

#### Étape 1 – Importer les classes requises

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.IncorrectPasswordException;
import com.groupdocs.editor.options.SpreadsheetLoadOptions;
```

#### Étape 2 – Configurer les options de chargement avec un mot de passe incorrect

```java
String inputFilePath = "path/to/sample_xls_protected";
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.setPassword("incorrect_password");
Editor editor = new Editor(inputFilePath, loadOptions);
```

#### Étape 3 – Gérer l'exception de mot de passe incorrect

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
- Assurez‑vous que le mot de passe fourni est bien incorrect à des fins de test.  
- Utilisez ce modèle pour informer les utilisateurs finaux que leur saisie d'identifiants a échoué.

### Comment ouvrir Excel avec le bon mot de passe

Cette section montre la bonne façon d'ouvrir un classeur protégé par mot de passe en utilisant les bonnes informations d'identification, activant les fonctionnalités de **groupdocs passwordape 1 – Importer les classes requises

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.options.SpreadsheetLoadOptions;
```

#### Étape 2 – Configurer les options de chargement avec le bon mot de passe

```java
String inputFilePath = "path/to/sample_xls_protected";
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.setPassword("excel_password");
loadOptions.setOptimizeMemoryUsage(true);
Editor editor = new Editor(inputFilePath, loadOptions);
```

**Options de configuration clésUsage(true)` .

### Comment enregistrer Excel avec mot de passe et ajouter une protection en écriture Excel

Nous combinons maintenant tout : ouvrez le classeur avecregistrez Excel avec mot de passe** tout en appliquant **add write protection excel** pour empêcher les modifications non autorisées.

#### Étape 1 – Importer les classes requises

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.options.SpreadsheetFormats;
import com.groupdocs.editor.options.SpreadsheetSaveOptions;
import com.groupdocs.editor.options.WorksheetProtection;
import com.groupdocs.editor.options.WorksheetProtectionType;
```

#### Étape 2 – Charger le classeur protégé

```java
String inputFilePath = "path/to/sample_xls_protected";
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.setPassword("excel_password");
Editor editor = new Editor(inputFilePath, loadOptions);
```

#### Étape 3 – Configurer les options d'enregistrement avec un nouveau mot de passe et la protection en écriture

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
- Choisissez un `new_password` fort pour sécuriser le fichier.  
- Le drapeau `WorksheetProtectionType.All` protège chaque feuille contre la modification sans le `write_password`.

## Applications pratiques

1. **Partage sécurisé de données** – Protégez les modèles financiers confidentiels avant de les envoyer par courriel aux parties prenantes.  
2. **Pipelines de documents automatisés** – Intégrez ces extraits dans des travaux batch qui traitent et re‑chiffrent un grand nombre de feuilles de calcul.

## Conclusion

En maîtrisant l'utilisation de GroupDocs.Editor en Java, vous pouvez en toute confiance **enregistrer Excel avec mot de passe**, ouvrir des fichiers avec ou sans mot de passe, et **add write protection Excel** pour protéger vos données. Ces capacités vous offrent un contrôle granulaire sur la sécurité des classeurs, vous aidant à répondre aux exigences de conformité et à protéger la propriété intellectuelle.

---

**Dernière mise à jour :** 2026-02-01  
**Testé avec :** GroupDocs.Editor 25.3  
**Auteur :** GroupDocs