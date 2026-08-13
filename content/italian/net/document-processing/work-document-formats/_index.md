---
date: 2026-06-06
description: Scopri come elencare i formati di documento supportati e determinare
  l'estensione del formato file utilizzando GroupDocs.Editor per .NET. Guida step‑by‑step
  con code snippets, quick answers e FAQs.
keywords:
- list supported document formats
- determine file format extension
- GroupDocs.Editor .NET
- document editing API
- supported formats guide
linktitle: Elenca i formati di documento supportati
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to list supported document formats and determine file format
    extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets,
    quick answers, and FAQs.
  headline: List Supported Document Formats with GroupDocs.Editor .NET
  type: TechArticle
- description: Learn how to list supported document formats and determine file format
    extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets,
    quick answers, and FAQs.
  name: List Supported Document Formats with GroupDocs.Editor .NET
  steps:
  - name: '**.NET development environment** – Visual Studio 2022 or any IDE that supports
      .NET 6+.'
    text: '**.NET development environment** – Visual Studio 2022 or any IDE that supports
      .NET 6+.'
  - name: '**GroupDocs.Editor for .NET library** – download from the [GroupDocs releases
      page](https://releases.groupdocs.com/editor/net/).'
    text: '**GroupDocs.Editor for .NET library** – download from the [GroupDocs releases
      page](https://releases.groupdocs.com/editor/net/).'
  - name: '**Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/)
      for unrestricted access.'
    text: '**Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/)
      for unrestricted access.'
  - name: '**Basic C# knowledge** – familiarity with namespaces, `using` statements,
      and console output.'
    text: '**Basic C# knowledge** – familiarity with namespaces, `using` statements,
      and console output.'
  - name: '**Loop Through Formats:** We iterate over all available Word‑processing
      formats.'
    text: '**Loop Through Formats:** We iterate over all available Word‑processing
      formats.'
  - name: '**Output Format Details:** For each format we print its friendly name and
      default file extension.'
    text: '**Output Format Details:** For each format we print its friendly name and
      default file extension.'
  - name: '**Loop Through Formats:** The same looping logic applies to presentations.'
    text: '**Loop Through Formats:** The same looping logic applies to presentations.'
  - name: '**Output Format Details:** The name and extension are displayed for each
      format.'
    text: '**Output Format Details:** The name and extension are displayed for each
      format.'
  - name: '**Parse Format:** `FromExtension` converts the `.xlsm` extension into its
      internal `SpreadsheetFormat` enum.'
    text: '**Parse Format:** `FromExtension` converts the `.xlsm` extension into its
      internal `SpreadsheetFormat` enum.'
  - name: '**Output Format:** The parsed format’s name is printed, confirming the
      mapping.'
    text: '**Output Format:** The parsed format’s name is printed, confirming the
      mapping.'
  type: HowTo
- questions:
  - answer: '`DocumentFormatInfo` provides metadata about supported file types, while
      `SaveOptions` configures how a document is written back to disk (format, compression,
      etc.).'
    question: What is the difference between `DocumentFormatInfo` and `SaveOptions`?
  - answer: Yes—use `DocumentFormatInfo.FromExtension("yourExt")`; if the extension
      isn’t recognized, the method returns `null`.
    question: Can I list formats for a custom file extension?
  - answer: Absolutely. Pass the password to the `Editor` constructor via `EditorSettings`
      to open encrypted documents.
    question: Does GroupDocs.Editor support password‑protected files?
  - answer: Over **30 input and output formats**, spanning Word, Excel, PowerPoint,
      HTML, and plain text.
    question: How many formats does GroupDocs.Editor actually support?
  - answer: Use the `GetEditableWordProcessingFormats()` (or Spreadsheet/Presentation
      equivalents) to retrieve formats that allow full edit capabilities.
    question: Is there a way to restrict the list to only editable formats?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Elenca i formati di documento supportati con GroupDocs.Editor .NET
type: docs
url: /it/net/document-processing/work-document-formats/
weight: 13
---

# Elenco dei formati di documento supportati

Benvenuti al nostro tutorial completo su **come elencare i formati di documento supportati** con GroupDocs.Editor per .NET. Che tu stia creando un'app web incentrata sui documenti o uno strumento desktop di livello enterprise, conoscere esattamente quali formati puoi modificare o convertire è fondamentale. In questa guida scoprirai come enumerare i formati, analizzare le estensioni e modificare i documenti—tutto con spiegazioni chiare e comprensibili e snippet di codice pronti da eseguire.

## Risposte rapide
- **Come faccio a elencare tutti i formati supportati?** Usa `DocumentFormatInfo.GetSupportedWordProcessingFormats()` (o gli equivalenti per Presentation/Spreadsheet) e itera la collezione.  
- **Posso determinare un formato da un'estensione di file?** Sì—chiama `DocumentFormatInfo.FromExtension(".docx")`.  
- **Quali tipi di file supporta GroupDocs.Editor?** Oltre 30 formati di input e output, inclusi DOCX, XLSX, PPTX, HTML e testo semplice.  
- **È necessaria una licenza per elencare i formati?** Una licenza temporanea sblocca l'intera API; altrimenti una versione di prova funziona con funzionalità limitate.  
- **Quali versioni .NET sono compatibili?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.

## Cos'è “elencare i formati di documento supportati”?
La frase si riferisce al recupero programmatico della collezione di tipi di file che GroupDocs.Editor può aprire, modificare e salvare. Questa operazione ti consente di creare menu a discesa UI dinamici o di convalidare i caricamenti degli utenti prima dell'elaborazione, garantendo che solo i file compatibili vengano passati all'editor per ulteriori manipolazioni.

## Perché elencare i formati di documento supportati?
GroupDocs.Editor **supporta oltre 30 formati di input e output** e può gestire file fino a **2 GB** senza caricare l'intero documento in memoria. Conoscere l'elenco esatto previene errori di runtime, migliora l'esperienza dell'utente e consente di applicare regole aziendali come “consentire solo documenti Office modificabili”. Aiuta inoltre a mostrare agli utenti solo i formati che la tua applicazione supporta realmente.

## Prerequisiti
Prima di iniziare, assicurati di avere:

1. **Ambiente di sviluppo .NET** – Visual Studio 2022 o qualsiasi IDE che supporti .NET 6+.  
2. **Libreria GroupDocs.Editor per .NET** – scarica dalla [pagina dei rilasci GroupDocs](https://releases.groupdocs.com/editor/net/).  
3. **Licenza temporanea** – ottieni una [licenza temporanea](https://purchase.groupdocs.com/temporary-license/) per accesso illimitato.  
4. **Conoscenza di base di C#** – familiarità con i namespace, le istruzioni `using` e l'output della console.

## Come elencare i formati di documento supportati?
Carica la collezione dei formati supportati e stampa il nome e l'estensione di ciascun formato. Questo modello a due passaggi funziona per documenti Word Processing, Spreadsheet e Presentation. Iterando la collezione puoi popolare dinamicamente elementi UI come menu a discesa, assicurando che gli utenti possano selezionare solo i formati che l'editor può effettivamente gestire.

```csharp
// No actual code block – placeholder retained from original tutorial
```csharp
using System;
using GroupDocs.Editor.Options;
```
```

### Elencare i formati di Word Processing
`Formats.WordProcessingFormats` è un'enumerazione che descrive ogni tipo di file di elaborazione testi riconosciuto dall'editor. La proprietà `All` restituisce una collezione di questi oggetti formato.

```csharp
```csharp
foreach (Formats.WordProcessingFormats oneFormat in Formats.WordProcessingFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**Spiegazione:**  
1. **Itera sui formati:** Iteriamo tutti i formati di elaborazione testi disponibili.  
2. **Dettagli del formato di output:** Per ogni formato stampiamo il suo nome leggibile e l'estensione di file predefinita.

### Elencare i formati di presentazione
`Formats.PresentationFormats` funziona allo stesso modo per i file di presentazione, esponendo ogni tipo di presentazione supportato tramite la collezione `All`.

```csharp
```csharp
foreach (Formats.PresentationFormats oneFormat in Formats.PresentationFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**Spiegazione:**  
1. **Itera sui formati:** Lo stesso ciclo si applica alle presentazioni.  
2. **Dettagli del formato di output:** Il nome e l'estensione vengono visualizzati per ogni formato.

## Come determinare l'estensione del formato di file?
A volte hai solo un nome file e devi dedurre il corrispondente `DocumentFormat`. GroupDocs.Editor offre un semplice helper statico che mappa un'estensione di file alla sua rappresentazione di formato interno, consentendoti di convalidare o convertire i file prima di caricarli nell'editor.

### Analisi dei formati di foglio di calcolo
`Formats.SpreadsheetFormats.FromExtension` converte una stringa di estensione di file nel valore enum del formato di foglio di calcolo corrispondente.

```csharp
```csharp
Formats.SpreadsheetFormats expectedXlsm = Formats.SpreadsheetFormats.FromExtension(".xlsm");
Console.WriteLine("Parsed Spreadsheet format is {0}", expectedXlsm.Name);
```
```

**Spiegazione:**  
1. **Analizza il formato:** `FromExtension` converte l'estensione `.xlsm` nel suo enum interno `SpreadsheetFormat`.  
2. **Formato di output:** Il nome del formato analizzato viene stampato, confermando la mappatura.

### Analisi dei formati testuali
Analogamente, `Formats.TextualFormats.FromExtension` risolve le estensioni di file testuali come HTML o TXT.

```csharp
```csharp
Formats.TextualFormats expectedHtml = Formats.TextualFormats.FromExtension("html");
Console.WriteLine("Parsed Textual format is {0}", expectedHtml.Name);
```
```

**Spiegazione:**  
1. **Analizza il formato:** Il metodo `FromExtension` risolve l'estensione `html` in un `TextFormat`.  
2. **Formato di output:** Il nome del formato testuale viene mostrato, utile per editor basati sul web.

## Come modificare i documenti dopo aver identificato i formati?
Una volta conosciuto il formato, il caricamento e la modifica di un documento segue un modello coerente. Prima crei un'istanza di `Editor` con il percorso del file sorgente, poi chiami `Edit()` per ottenere un `EditableDocument`. Da lì puoi leggere, modificare e infine salvare il contenuto usando i `SaveOptions` appropriati.

### Caricamento di un documento
`Editor` è la classe principale che incapsula tutte le operazioni di modifica per un determinato file.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/document.docx"))
{
    // Further steps will be covered here.
}
```
```

**Spiegazione:**  
1. **Inizializza Editor:** Crea un'istanza di `Editor`, passando il percorso completo del file di destinazione.  
2. **Pattern di dispose:** L'istruzione `using` garantisce che tutte le risorse non gestite vengano rilasciate prontamente.

### Estrarre il contenuto
`EditableDocument.GetContent()` restituisce il testo grezzo del documento (o HTML per editor basati sul web), che puoi visualizzare o manipolare.

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    string content = editableDocument.GetContent();
    Console.WriteLine(content);
}
```
```

**Spiegazione:**  
1. **Metodo Edit:** `Edit()` restituisce un oggetto `EditableDocument`.  
2. **Ottieni contenuto:** `GetContent()` estrae il testo grezzo del documento (o HTML per editor basati sul web).  
3. **Output del contenuto:** Il contenuto viene scritto sulla console per verifica.

### Salvare le modifiche
`SaveOptions` indica all'editor come e in quale formato scrivere il documento modificato nuovamente nello storage.

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    // Modify content here
    SaveOptions saveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docx);
    editor.Save(editableDocument, "path/to/save/document.docx", saveOptions);
}
```
```

**Spiegazione:**  
1. **Metodo Edit:** Riottieni l'`EditableDocument` dopo le modifiche.  
2. **Modifica contenuto:** Applica le tue modifiche alla stringa (non mostrato qui).  
3. **Opzioni di salvataggio:** Configura `SaveOptions` con il formato di output desiderato.  
4. **Salva documento:** Persiste il file modificato sul disco.

## Come lavorare con diversi tipi di documento?
GroupDocs.Editor astrae la gestione di Word, Spreadsheet e Presentation dietro la stessa interfaccia API, rendendo facile cambiare contesto senza dover apprendere un nuovo set di classi per ogni famiglia di documenti.

### Modifica di documenti Spreadsheet
`SpreadsheetSaveOptions` definisce come viene scritto un foglio di calcolo, includendo il formato e le impostazioni di compressione opzionali.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/spreadsheet.xlsx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // Modify content here
        SaveOptions saveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsx);
        editor.Save(editableDocument, "path/to/save/spreadsheet.xlsx", saveOptions);
    }
}
```
```

**Spiegazione:**  
1. **Inizializza Editor:** Passa il percorso di un file spreadsheet al costruttore `Editor`.  
2. **Metodo Edit:** Recupera un `EditableDocument`.  
3. **Ottieni contenuto:** Stampa la rappresentazione CSV del foglio di calcolo (o HTML).  
4. **Modifica contenuto:** Applica le modifiche a livello di cella necessarie.  
5. **Opzioni di salvataggio:** Scegli le `SpreadsheetSaveOptions` appropriate.  
6. **Salva documento:** Scrivi il foglio di calcolo aggiornato nello storage.

### Modifica di documenti Presentation
`PresentationSaveOptions` controlla il formato di output per le presentazioni, consentendoti di preservare o modificare il tipo di file originale.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/presentation.pptx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // Modify content here
        SaveOptions saveOptions = new PresentationSaveOptions(PresentationFormats.Pptx);
        editor.Save(editableDocument, "path/to/save/presentation.pptx", saveOptions);
    }
}
```
```

**Spiegazione:**  
1. **Inizializza Editor:** Carica un file PowerPoint tramite `Editor`.  
2. **Metodo Edit:** Ottieni un `EditableDocument`.  
3. **Ottieni contenuto:** Estrai l'HTML delle diapositive o il testo semplice.  
4. **Modifica contenuto:** Aggiorna titoli, punti elenco o immagini.  
5. **Opzioni di salvataggio:** Usa `PresentationSaveOptions` per definire il formato di output.  
6. **Salva documento:** Persiste la presentazione modificata.

## Problemi comuni e soluzioni
- **Errore “Formato non supportato”**: Verifica di utilizzare l'ultima versione di GroupDocs.Editor; aggiunge regolarmente il supporto per i nuovi formati Office.  
- **Consumo di memoria per file grandi**: Abilita la modalità streaming impostando `EditorSettings.EnableStreaming = true` prima di caricare il documento.  
- **Licenza non applicata**: Assicurati che il file di licenza temporanea sia posizionato nella radice dell'applicazione o caricato tramite `License license = new License(); license.SetLicense("path/to/license.lic");`.

## Domande frequenti

**D: Qual è la differenza tra `DocumentFormatInfo` e `SaveOptions`?**  
R: `DocumentFormatInfo` fornisce metadati sui tipi di file supportati, mentre `SaveOptions` configura come un documento viene scritto nuovamente su disco (formato, compressione, ecc.).

**D: Posso elencare i formati per un'estensione di file personalizzata?**  
R: Sì—usa `DocumentFormatInfo.FromExtension("yourExt")`; se l'estensione non è riconosciuta, il metodo restituisce `null`.

**D: GroupDocs.Editor supporta file protetti da password?**  
R: Assolutamente. Passa la password al costruttore `Editor` tramite `EditorSettings` per aprire documenti crittografati.

**D: Quanti formati supporta effettivamente GroupDocs.Editor?**  
R: Oltre **30 formati di input e output**, che includono Word, Excel, PowerPoint, HTML e testo semplice.

**D: Esiste un modo per limitare l'elenco solo ai formati modificabili?**  
R: Usa `GetEditableWordProcessingFormats()` (o gli equivalenti per Spreadsheet/Presentation) per recuperare i formati che consentono piena capacità di modifica.

## Risorse aggiuntive
- Scarica la libreria dalla [pagina dei rilasci GroupDocs](https://releases.groupdocs.com/editor/net/).  
- Ottieni una [licenza temporanea](https://purchase.groupdocs.com/temporary-license/) per l'accesso a tutte le funzionalità.  
- Prova il prodotto con una [prova gratuita](https://releases.groupdocs.com/).  
- Esplora esempi di utilizzo dettagliati nella [documentazione GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/).  
- Ottieni aiuto dalla community sul [forum di supporto](https://forum.groupdocs.com/c/editor/20).

## Conclusione
Seguendo questa guida ora sai come **elencare i formati di documento supportati**, **determinare un formato di file dalla sua estensione** e **modificare i documenti** nei tipi Word, Spreadsheet e Presentation usando GroupDocs.Editor per .NET. Integra questi snippet nei tuoi progetti per costruire applicazioni robuste, consapevoli dei formati, che deliziano gli utenti finali e riducono gli errori di runtime.

---

**Ultimo aggiornamento:** 2026-06-06  
**Testato con:** GroupDocs.Editor 23.9 per .NET  
**Autore:** GroupDocs

## Tutorial correlati

- [Padronanza del caricamento di documenti in .NET con GroupDocs.Editor: Guida completa](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)
- [Master Editing di documenti in .NET con GroupDocs.Editor: Guida completa](/editor/net/document-editing/master-document-editing-dotnet-groupdocs-editor/)
- [Converti Word in HTML usando GroupDocs.Editor .NET: Guida passo‑passo](/editor/net/document-saving/convert-word-to-html-groupdocs-editor-dotnet/)