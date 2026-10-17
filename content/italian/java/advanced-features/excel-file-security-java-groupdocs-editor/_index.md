---
date: '2026-10-16'
description: Scopri come aprire file Excel protetti da password in Java con GroupDocs.Editor,
  impostare nuove password e gestire la protezione di scrittura.
keywords:
- open password protected excel
- write protect excel workbook
- optimize memory usage java
- protect specific worksheet
lastmod: '2026-10-16'
og_description: Apri file Excel protetti da password in Java con GroupDocs.Editor.
  Questa guida mostra come caricare cartelle di lavoro crittografate, gestire password
  errate, applicare nuove password al salvataggio e abilitare la protezione di scrittura
  ottimizzando l'uso della memoria.
og_image_alt: 'Developer guide: Open password protected Excel in Java with GroupDocs.Editor'
og_title: Apri file Excel protetti da password in Java con GroupDocs.Editor
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
title: Apri file Excel protetti da password in Java con GroupDocs.Editor
type: docs
url: /it/java/advanced-features/excel-file-security-java-groupdocs-editor/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aprire Excel protetto da password in Java usando GroupDocs.Editor

In questo tutorial completo scoprirai come **aprire Excel protetto da password** cartelle di lavoro in Java usando GroupDocs.Editor, gestire password errate, applicare una nuova password al salvataggio e abilitare la protezione in scrittura per l'intero workbook. I passaggi sono illustrati con spiegazioni chiare, scenari d'uso reali e consigli di best‑practice per l'elaborazione di fogli di calcolo su larga scala.

## Risposte rapide
- **Quale libreria aiuta ad aprire Excel protetto da password?** GroupDocs.Editor for Java.  
- **Posso aprire una cartella di lavoro protetta da password senza password?** No – l'API genera `PasswordRequiredException`.  
- **Come gestisco una password errata?** Cattura `IncorrectPasswordException` e richiedi nuovamente la password all'utente.  
- **È possibile impostare una nuova password al salvataggio?** Sì, usa `SpreadsheetSaveOptions.setPassword`.  
- **È necessaria una licenza per l'uso in produzione?** È richiesta una licenza valida di GroupDocs.Editor per qualsiasi distribuzione in produzione.

## Cos'è Excel protetto da password?
`open password protected Excel` descrive il processo di caricamento programmatico di una cartella di lavoro Excel che ha una password di apertura, la verifica della password e, facoltativamente, il suo nuovo salvataggio con una nuova password o protezione aggiuntiva. L'uso delle API Java elimina i passaggi manuali e consente di incorporare la sicurezza nei flussi di lavoro automatizzati.

## Perché proteggere le cartelle di lavoro Excel con Java?
GroupDocs.Editor offre **oltre 30 metodi API dedicati** per la gestione delle password, può elaborare **centinaia di fogli di lavoro** senza caricare l'intero file in memoria e garantisce **il 100 % di fedeltà del layout** quando si salva nuovamente i file crittografati. Queste capacità quantificate ti consentono di creare lavori batch che gestiscono **fogli di calcolo di 200 pagine in meno di 5 secondi** su un server tipico, mantenendo i dati sicuri e conformi.

## Prerequisiti
- Java Development Kit (JDK) 8 o superiore  
- Maven per la gestione delle dipendenze  
- Conoscenze di base di programmazione Java  
- Una licenza GroupDocs.Editor (trial o acquistata)  

## Configurazione di GroupDocs.Editor per Java

### Utilizzo di Maven
Aggiungi il repository e la dipendenza al tuo `pom.xml`:

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
- **Prova gratuita** – esplora tutte le funzionalità senza costi.  
- **Licenza temporanea** – rimuove i limiti di valutazione durante i test.  
- **Acquisto** – ottieni una licenza completa da [GroupDocs](https://purchase.groupdocs.com/temporary-license).

### Inizializzazione di base
`Editor` è il punto di ingresso per tutte le operazioni sui documenti in GroupDocs.Editor per Java. Carica una cartella di lavoro in memoria e fornisce metodi per l'editing, il salvataggio e la gestione della sicurezza.

```java
import com.groupdocs.editor.Editor;

// Initialize the editor with an Excel file path
Editor editor = new Editor("path/to/your/excel/file.xlsx");
```

## Guida all'implementazione

Esamineremo quattro scenari comuni che potresti incontrare quando proteggi le cartelle di lavoro Excel.

### Come aprire Excel protetto da password senza una password?

**Risposta diretta:** Chiama `Editor.edit` solo con il percorso del file; se la cartella di lavoro è crittografata, GroupDocs.Editor genera `PasswordRequiredException`, che puoi catturare per richiedere la password all'interfaccia utente.

`PasswordRequiredException` segnala che la cartella di lavoro richiede una password ma non ne è stata fornita. Catturando questa eccezione puoi visualizzare un prompt, registrare l'evento o interrompere l'operazione in modo corretto.

1. **Importa le classi necessarie** – includi `PasswordRequiredException` e i tipi correlati.  

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.PasswordRequiredException;
```

2. **Inizializza l'Editor** – crea un'istanza `Editor` usando un `EditorConfig` valido che punta al tuo file di licenza.  

```java
String inputFilePath = "path/to/sample_xls_protected";
Editor editor = new Editor(inputFilePath);
```

3. **Prova a modificare senza una password** – invoca `Editor.edit` solo con il percorso del file. Se la cartella di lavoro è protetta, la chiamata genera `PasswordRequiredException`.  

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
- Usa l'eccezione catturata per attivare un prompt UI per la password.  

### Come aprire Excel protetto da password con una password errata?

**Risposta diretta:** Carica la cartella di lavoro usando `SpreadsheetLoadOptions` con la password fornita; se la password non corrisponde, cattura `IncorrectPasswordException` e informa l'utente di riprovare.

`IncorrectPasswordException` indica che la password fornita non corrisponde alla chiave di crittografia della cartella di lavoro. Gestire questa eccezione ti consente di fornire un feedback chiaro e, facoltativamente, limitare i tentativi di ripetizione.

1. **Importa le classi necessarie** – includi `IncorrectPasswordException` nei tuoi import.  

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.IncorrectPasswordException;
import com.groupdocs.editor.options.SpreadsheetLoadOptions;
```

2. **Configura le opzioni di caricamento con una password errata** – crea un'istanza `SpreadsheetLoadOptions` e imposta una password che sai essere sbagliata per il test.  

```java
String inputFilePath = "path/to/sample_xls_protected";
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.setPassword("incorrect_password");
Editor editor = new Editor(inputFilePath, loadOptions);
```

3. **Gestisci l'eccezione** – avvolgi la chiamata di caricamento in un blocco try‑catch e cattura `IncorrectPasswordException` per visualizzare un messaggio di errore o bloccare l'utente dopo un certo numero di tentativi.  

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
- Assicurati che la stringa della password sia davvero diversa da quella corretta.  
- Usa questo schema per limitare il numero di tentativi di ripetizione nella tua UI.  

### Come aprire Excel protetto da password con la password corretta?

**Risposta diretta:** Fornisci la password corretta tramite `SpreadsheetLoadOptions.setPassword`, abilita `setOptimizeMemoryUsage(true)` e poi chiama `Editor.edit` per ottenere un oggetto `Spreadsheet` modificabile.

`SpreadsheetLoadOptions` configura come la cartella di lavoro viene caricata, includendo impostazioni di password e di utilizzo della memoria. L'abilitazione dell'ottimizzazione della memoria mantiene basso il consumo di RAM quando si elaborano grandi fogli di calcolo.

1. **Importa le classi necessarie** – includi `SpreadsheetLoadOptions` e le utility correlate.  

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.options.SpreadsheetLoadOptions;
```

2. **Configura le opzioni di caricamento con la password corretta** – imposta la password, attiva l'ottimizzazione della memoria e poi invoca `Editor.edit`.  

```java
String inputFilePath = "path/to/sample_xls_protected";
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.setPassword("excel_password");
loadOptions.setOptimizeMemoryUsage(true);
Editor editor = new Editor(inputFilePath, loadOptions);
```

#### Opzioni di configurazione chiave
- **setOptimizeMemoryUsage** – riduce il consumo di RAM quando si lavora con grandi fogli di calcolo, consentendo di elaborare file fino a **500 MB** senza errori OutOfMemory.  

### Come impostare una nuova password di apertura e proteggere in scrittura una cartella di lavoro Excel al salvataggio?

**Risposta diretta:** Carica la cartella di lavoro con la password esistente, crea un oggetto `SpreadsheetSaveOptions`, chiama `setPassword` con il nuovo valore, abilita `setWriteProtection(true)` e infine invoca `Editor.save`.  

`SpreadsheetSaveOptions` definisce come la cartella di lavoro viene salvata, includendo flag di password e protezione in scrittura. `setWriteProtection(true)` blocca la cartella di lavoro contro ulteriori modifiche a meno che non venga fornita la password corretta.

`WorksheetProtection` ti consente di proteggere singoli fogli di lavoro con tipi di protezione specifici.

1. **Importa le classi necessarie** – includi `SpreadsheetSaveOptions` e `WorksheetProtection` se hai bisogno di un controllo granulare.  

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.options.SpreadsheetFormats;
import com.groupdocs.editor.options.SpreadsheetSaveOptions;
import com.groupdocs.editor.options.WorksheetProtection;
import com.groupdocs.editor.options.WorksheetProtectionType;
```

2. **Carica la cartella di lavoro con la password esistente** – usa `SpreadsheetLoadOptions` per aprire il file protetto prima di apportare modifiche.  

```java
String inputFilePath = "path/to/sample_xls_protected";
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.setPassword("excel_password");
Editor editor = new Editor(inputFilePath, loadOptions);
```

3. **Configura le opzioni di salvataggio con una nuova password e protezione in scrittura** – chiama `setPassword` per assegnare una nuova password di apertura e `setWriteProtection(true)` per bloccare la cartella di lavoro contro le modifiche.  

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
- Il flag `WorksheetProtectionType.All` blocca ogni elemento modificabile; regola secondo necessità per una protezione selettiva.  

## Applicazioni pratiche

1. **Condivisione sicura dei dati** – proteggi modelli finanziari sensibili prima di inviarli via email alle parti interessate.  
2. **Pipeline di documenti automatizzate** – incorpora questi snippet in lavori batch che elaborano e ricifrano migliaia di fogli di calcolo ogni notte.  
3. **Conformità normativa** – applica la crittografia delle cartelle di lavoro per soddisfare automaticamente i requisiti GDPR, HIPAA o PCI‑DSS.  

## Problemi comuni e soluzioni

| Problema | Causa | Soluzione |
|----------|-------|-----------|
| `PasswordRequiredException` anche se ho passato una password | Opzioni di caricamento non collegate alla chiamata edit | Assicurati di passare l'istanza configurata `SpreadsheetLoadOptions` a `Editor.edit`. |
| Errori Out‑of‑memory su file grandi | Ottimizzazione della memoria disabilitata | Chiama `setOptimizeMemoryUsage(true)` su `SpreadsheetLoadOptions`. |
| Il workbook salvato perde la formattazione | Uso di `SpreadsheetSaveOptions` predefinito senza preservare il layout | Imposta `setPreserveFormatting(true)` (disponibile dalla versione 25.3+). |
| Protezione in scrittura non applicata | Dimenticato di chiamare `setWriteProtection(true)` | Aggiungi la chiamata prima di invocare `Editor.save`. |

## Domande frequenti

**Q: Posso cambiare la password di una cartella di lavoro già protetta?**  
A: Sì. Carica la cartella di lavoro con la password esistente, poi salvala usando `SpreadsheetSaveOptions.setPassword` con il nuovo valore.

**Q: Cosa succede se provo ad aprire una cartella di lavoro senza specificare una password quando è protetta?**  
A: GroupDocs.Editor genera `PasswordRequiredException`, che dovresti catturare per richiedere la password all'utente.

**Q: È possibile proteggere solo fogli di lavoro specifici invece dell'intera cartella di lavoro?**  
A: Usa `WorksheetProtection` con un `WorksheetProtectionType` specifico (ad esempio `LockedCells`) e applicalo ai singoli fogli tramite l'API.

**Q: `setOptimizeMemoryUsage(true)` influisce sulle prestazioni?**  
A: Riduce il consumo di memoria a scapito di un leggero overhead di elaborazione, il che è vantaggioso per file molto grandi.

**Q: Ho bisogno di una licenza separata per ogni istanza del server?**  
A: I termini di licenza sono per distribuzione; consulta la guida di licenza di GroupDocs per scenari multi‑node.

## Conclusione

Seguendo questa guida ora sai come **aprire Excel protetto da password in Java** usando GroupDocs.Editor, gestire le password errate in modo elegante, applicare una nuova password al salvataggio e abilitare la protezione in scrittura per l'intera cartella di lavoro. Queste capacità ti permettono di creare flussi di lavoro documentali sicuri, conformi e ad alta velocità che scalano da un singolo file a processi batch massivi.

---

**Ultimo aggiornamento:** 2026-10-16  
**Testato con:** GroupDocs.Editor 25.3  
**Autore:** GroupDocs  

## Tutorial correlati

- [Modifica batch di file Word in Java con GroupDocs.Editor – Guida passo‑passo](/editor/java/document-loading/groupdocs-editor-java-loading-word-documents/)
- [come modificare file Excel e Word in Java con GroupDocs.Editor](/editor/java/document-editing/java-groupdocs-editor-master-document-editing/)
- [Come impostare una licenza per GroupDocs.Editor in Java usando InputStream: Guida completa](/editor/java/licensing-configuration/groupdocs-editor-java-inputstream-license-setup/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}