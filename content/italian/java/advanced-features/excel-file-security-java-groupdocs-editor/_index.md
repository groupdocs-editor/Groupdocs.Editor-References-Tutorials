---
date: '2026-02-03'
description: Impara a proteggere Excel con Java usando GroupDocs.Editor. Scopri come
  caricare Excel con password, aprire, proteggere e gestire le password nei documenti.
keywords:
- Excel file security in Java
- GroupDocs.Editor for Java
- Java document password protection
title: 'Proteggi Excel con Java: padroneggiare GroupDocs.Editor per la protezione
  e la gestione delle password'
type: docs
url: /it/java/advanced-features/excel-file-security-java-groupdocs-editor/
weight: 1
---

# Proteggi Excel con Java usando GroupDocs.Editor

In questa guida completa imparerai come **proteggere Excel con Java** sfruttando le potenti funzionalità di GroupDocs.Editor. Ti mostreremo come **caricare Excel con password**, aprire i file in modo sicuro, gestire password errate e applicare la protezione in scrittura al salvataggio. Che tu stia costruendo un flusso di lavoro documentale aziendale o un piccolo utility, queste tecniche manterranno i tuoi fogli di calcolo al sicuro.

## Risposte rapide
- **Quale libreria aiuta a proteggere Excel con Java?** GroupDocs.Editor for Java  
- **Posso aprire una cartella di lavoro protetta da password senza la password?** Puoi provare, ma verrà sollevata un'`PasswordRequiredException`.  
- **Come gestisco una password errata?** Cattura `IncorrectPasswordException` e informa l'utente.  
- **È possibile impostare una nuova password al salvataggio?** Sì, usando `SpreadsheetSaveOptions.setPassword`.  
- **Ho bisogno di una licenza per l'uso in produzione?** È necessaria una licenza valida di GroupDocs.Editor per le distribuzioni in produzione.

## Cosa imparerai
- Integra GroupDocs.Editor nei tuoi progetti Java  
- **Carica Excel con password** e gestisci gli errori di autenticazione  
- Imposta nuove password e applica la protezione in scrittura al salvataggio dei file  
- Ottimizza l'uso della memoria per cartelle di lavoro di grandi dimensioni  

## Perché proteggere Excel con Java?
Proteggere i file Excel programmaticamente elimina il rischio di perdite accidentali di dati, supporta i requisiti di conformità e consente flussi di lavoro automatizzati che rispettano la riservatezza dei documenti. GroupDocs.Editor ti offre un controllo granulare sia sull'apertura che ideale per soluzioni di livello enterprise.

## Prere8 o superiore  
- **Maven** per la gestione delleenza **GroupDocs`:

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

### Download diretto
In alternativa, scarica l'ultimo JAR da [GroupDocs.Editor for Java releases](https://releases.groupdocs.com/editor/java/).

#### Acquisizione della licenza
- **Free Trial** – esplora tutte le- **Temporary License** – rimuove i limiti di valutazione durante i test.  
- **Purchase** – ottieni una licenza completa da [GroupDocs](https://purchase.groupdocs.com/temporary-license).

### Inizializzazione di base
Inizia creando un'istanza `Editor` che punti al tuo workbook:

```java
import com.groupdocs.editor.Editor;

// Initialize the editor with an Excel file path
Editor editor = new Editor("path/to/your/excel/file.xlsx");
```

## Guida all'implementazione

Esamineremo quattro scenari comuni che potresti incontrare quando proteggi le cartelle di lavoro Excel.

### Come proteggere Excel con Java – Apri documento senza password

#### Panoramica
A volte è necessario verificare se una cartella di lavoro è protetta da password prima di chiedere all'utente. Questo snippet tenta di aprire il file senza password e gestisce l'eccezione in modo elegante.

#### Passo‑per‑passo

1. **Importa le classi necessarie**

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.PasswordRequiredException;
```

2. **Inizializza l'Editor**

```java
String inputFilePath = "path/to/sample_xls_protected";
Editor editor = new Editor(inputFilePath);
```

3. **Prova a modificare senza password**

```java
try {
    // Try editing without a password
    editor.edit();
} catch (PasswordRequiredException ex) {
    System.out.println("Cannot edit the document because it is password-protected.");
}
editor.dispose();
```

#### Suggerimenti per la risoluzione dei problemi
- Verifica che il percorso del file punti a una cartella di lavoro esistente.  
- Usa l'`PasswordRequiredException` catturata per attivare un prompt UI per la password.

### Apri documento con password errata

#### Panoramica
Quando un utente fornisce una password errata, GroupDocs.Editor lancia un'`IncorrectPasswordException`. Gestirla ti consente di fornire un feedback chiaro.

#### Passo‑per‑passo

1. **Importa le classi necessarie**

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.IncorrectPasswordException;
import com.groupdocs.editor.options.SpreadsheetLoadOptions;
```

2. **Configura le opzioni di caricamento con una password errata**

```java
String inputFilePath = "path/to/sample_xls_protected";
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.setPassword("incorrect_password");
Editor editor = new Editor(inputFilePath, loadOptions);
```

3. **Gestisci l'eccezione**

```java
try {
    // Attempt editing with an incorrect password
    editor.edit();
} catch (IncorrectPasswordException ex) {
    System.out.println("Cannot edit the document because the password is incorrect.");
}
editor.dispose();
```

#### Suggerimenti per la risoluzione dei problemi
- Assicurati che la stringa della password sia effettivamente diversa da quella corretta.  
- Usa questo schema per limitare il numero di tentativi di nuovo inserimento nella tua UI.

### Apri documento con password corretta

#### Panoramica
Fornire la password corretta consente l'accesso completo alla cartella di lavoro. Abilitare anche l'ottimizzazione della memoria per file di grandi dimensioni.

#### Passo‑per‑passo

1. **Importa le classi necessarie**

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.options.SpreadsheetLoadOptions;
```

2. **Configura le opzioni di caricamento con la password corretta**

```java
String inputFilePath = "path/to/sample_xls_protected";
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.setPassword("excel_password");
loadOptions.setOptimizeMemoryUsage(true);
Editor editor = new Editor(inputFilePath, loadOptions);
```

#### Opzioni di configurazione chiave
- **setOptimizeMemoryUsage** – riduce il consumo di RAM quando si lavora con fogli di calcolo di grandi dimensioni.

### Imposta password di apertura e protezione in scrittura al salvataggio

#### Panoramica
Dopo la modifica, potresti voler imporre una nuova password e impedire ad altri di modificare la cartella di lavoro. Questo esempio mostra come applicare entrambi.

#### Passo‑per‑passo

1. **Importa le classi necessarie**

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.options.SpreadsheetFormats;
import com.groupdocs.editor.options.SpreadsheetSaveOptions;
import com.groupdocs.editor.options.WorksheetProtection;
import com.groupdocs.editor.options.WorksheetProtectionType;
```

2. **Carica la cartella di lavoro con la password esistente**

```java
String inputFilePath = "path/to/sample_xls_protected";
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.setPassword("excel_password");
Editor editor = new Editor(inputFilePath, loadOptions);
```

3. **Configura le opzioni di salvataggio con una nuova password e protezione in scrittura**

```java
SpreadsheetFormats xlsmFormat = SpreadsheetFormats.Xlsm;
SpreadsheetSaveOptions saveOptions = new SpreadsheetSaveOptions(xlsmFormat);
saveOptions.setPassword("new_password");
saveOptions.setWorksheetProtection(new WorksheetProtection(WorksheetProtectionType.All, "write_password"));

String outputPath = "path/to/edited_document.xlsm";
editor.save(editor.edit(null), System.out, saveOptions);
editor.dispose();
```

#### Suggerimenti per la risoluzione dei problemi
- Scegli una password forte e imprevedibile per la chiamata `setPassword`.  
- Il flag `WorksheetProtectionType.All` blocca ogni elemento modificabile; regola secondo necessità.

## Applicazioni pratiche

1. **Condivisione sicura dei dati** – Proteggi i modelli finanziari sensibili prima di inviarli via email agli stakeholder.  
2. **Pipeline di documenti automatizzate** – Integra questi snippet in job batch che elaborano e ri‑crittografano grandi quantità di fogli di calcolo.

## Domande frequenti

**Q: Posso cambiare la password di una cartella di lavoro già protetta?**  
A: Sì. Carica la cartella di lavoro con la password esistente, poi salvala usando `SpreadsheetSaveOptions.setPassword` con il nuovo valore.

**Q: Cosa succede se provo ad aprire una cartella di lavoro senza specificare una password quando è protetta?**  
A: GroupDocs.Editor lancia `PasswordRequiredException`, che dovresti cattQ: È possibile proteggere solo fogli di lavoro specifici invece dell'intera cartella di lavoro?**  
A: Usa `Worksheet applicalo'API.

**Q: `setOptimizeMemoryUsage(true)` influisce sulle prestazioni?**  
A: Riduce il consumo di memoria a scapito di un leggero overhead di elaborazione, il che è vantaggioso per ogni istanza del server?**  
A: I termini di licenza sono per distribuzione; consulta la guida di licenza di GroupSeguendo questo con al aiutano a costruire flussi di lavoro documentali sicuri, conformi e automatizzati.

---

**Ultimo aggiornamento:** 2026-02-03  
**Testato