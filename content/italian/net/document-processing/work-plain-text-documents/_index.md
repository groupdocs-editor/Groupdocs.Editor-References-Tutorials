---
date: 2026-08-10
description: Scopri come modificare file di testo semplice usando GroupDocs.Editor
  per .NET. La guida copre il caricamento di un file txt, la rimozione degli spazi,
  l'impostazione della codifica del testo e il salvataggio del risultato.
keywords:
- edit plain text
- load txt file
- trim trailing spaces
- convert leading spaces
- set text encoding
lastmod: 2026-08-10
linktitle: Lavorare con documenti di testo semplice
og_description: Scopri come modificare file di testo semplice usando GroupDocs.Editor
  per .NET – carica file txt, rimuovi spazi finali, converte spazi iniziali, imposta
  la codifica del testo e salva in modo efficiente.
og_image_alt: Guide showing edit plain text workflow with GroupDocs.Editor for .NET
og_title: Modifica documenti di testo semplice con GroupDocs.Editor per .NET
schemas:
- author: GroupDocs
  dateModified: '2026-08-10'
  description: Learn how to edit plain text files using GroupDocs.Editor for .NET.
    The guide covers loading a txt file, trimming spaces, setting text encoding, and
    saving the result.
  headline: Edit plain text documents with GroupDocs.Editor for .NET
  type: TechArticle
- description: Learn how to edit plain text files using GroupDocs.Editor for .NET.
    The guide covers loading a txt file, trimming spaces, setting text encoding, and
    saving the result.
  name: Edit plain text documents with GroupDocs.Editor for .NET
  steps:
  - name: Get a path to the input TXT file
    text: First, decide whether you’ll work with a physical file path or a memory
      stream. Using a path is the most straightforward approach for local development.
  - name: Create an Editor instance
    text: '`Editor` is the main class that loads a document and provides editing capabilities.'
  - name: Create TXT editing options
    text: '`TxtEditOptions` configures how plain‑text files are parsed and edited,
      allowing you to set encoding and space‑handling rules.'
  - name: Create an EditableDocument instance
    text: '`EditableDocument` represents the in‑memory version of the loaded document,
      including its text and any associated resources.'
  - name: Edit the document content
    text: Retrieve the original text, apply any string operations you need (e.g.,
      replace, trim, change case), and store the result back into the `EditableDocument`.
  - name: Create an EditableDocument with updated content
    text: After you’ve transformed the text, instantiate a new `EditableDocument`
      that contains the edited string and the original resource collection.
  - name: Create WordProcessing save options
    text: '`WordProcessingSaveOptions` defines settings for saving the document in
      a Word‑compatible format such as DOCX or DOCM.'
  - name: Create TXT saving options
    text: '`TxtSaveOptions` specifies how the edited plain‑text file should be written,
      including encoding, line‑ending preservation, and table layout handling.'
  - name: Prepare output paths
    text: Derive the output directory from the input file path, then build the full
      filenames for the DOCX and TXT results.
  - name: Save the edited document
    text: Finally, call `editor.Save` twice—once with the WordProcessing options and
      once with the TXT options—to produce both formats in a single operation.
  type: HowTo
- questions:
  - answer: The library supports 50+ formats, including DOCX, TXT, HTML, PDF, and
      markdown, allowing you to edit and convert between them seamlessly.
    question: What file formats does GroupDocs.Editor for .NET support?
  - answer: Download the trial from the [releases page](https://releases.groupdocs.com/).
    question: How can I get a free trial of GroupDocs.Editor for .NET?
  - answer: Yes, temporary licenses are available through the [GroupDocs purchase
      page](https://purchase.groupdocs.com/temporary-license/).
    question: Can I purchase a temporary license for testing?
  - answer: The official support forum is the best place – visit the [GroupDocs.Editor
      support forum](https://forum.groupdocs.com/c/editor/20).
    question: Where can I find support if I run into issues?
  - answer: Absolutely. The full reference is on the [GroupDocs.Editor documentation
      page](https://tutorials.groupdocs.com/editor/net/).
    question: Is there detailed documentation for advanced scenarios?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
tags:
- edit plain text
- GroupDocs.Editor
- C# document processing
- plain text editing
- txt file handling
title: Modifica documenti di testo semplice con GroupDocs.Editor per .NET
type: docs
url: /it/net/document-processing/work-plain-text-documents/
weight: 15
---

# Modifica documenti di testo semplice con GroupDocs.Editor per .NET

## Introduzione
Se hai bisogno di **modificare testo semplice** rapidamente e in modo affidabile in un'applicazione .NET, GroupDocs.Editor per .NET è lo strumento che fa il lavoro pesante. Questa API supporta più di 30 formati di documento, può gestire file fino a 500 MB e ti consente di manipolare il testo senza caricare l'intero file in memoria. In questo tutorial imparerai come caricare un file txt, rimuovere gli spazi finali, convertire gli spazi iniziali, impostare la codifica corretta e infine salvare il contenuto modificato su disco. Pronto per mettere le mani sul codice? Immergiamoci!

## Risposte rapide
- **Qual è il primo passo per modificare un file txt?** Carica il file con `Editor` usando il percorso o lo stream a tua disposizione.  
- **Posso cambiare la codifica del file durante la modifica?** Sì – il `TxtSaveOptions` ti permette di specificare UTF‑8, UTF‑16 o qualsiasi codifica personalizzata.  
- **Come rimuovo gli spazi extra alla fine di ogni riga?** Recupera il testo, chiama `TrimEnd()` su ogni riga e riscrivilo.  
- **GroupDocs.Editor è gratuito per la prova?** È disponibile una versione di prova completamente funzionale di 30 giorni dalla pagina dei rilasci.  
- **Quali versioni di .NET sono supportate?** .NET Framework 4.6+, .NET Core 3.1+ e .NET 5/6/7.

## Che cosa significa modificare testo semplice?
**Edit plain text** significa modificare programmaticamente i caratteri all'interno di un semplice file `.txt`—aggiungendo, rimuovendo o riformattando il testo—preservando la codifica originale del file e lo stile di interruzione di riga. Può includere operazioni come la rimozione di spazi bianchi, la normalizzazione delle terminazioni di riga, l'aggiornamento dei valori di configurazione o l'inserimento di contenuti generati. L'operazione dovrebbe mantenere il file leggibile da qualsiasi editor di testo standard e conservare eventuali metadati esistenti come i marker BOM.

## Perché usare GroupDocs.Editor per la modifica di testo semplice?
GroupDocs.Editor elabora i file in modalità streaming, il che significa che può modificare un file di log da 300 MB utilizzando meno di 50 MB di RAM. La libreria supporta **oltre 50 formati di input e output**, rileva automaticamente gli stili di terminazione di riga (CR, LF, CRLF) e fornisce opzioni integrate per **rimuovere gli spazi finali** e **convertire gli spazi iniziali** senza scrivere parser personalizzati.

## Prerequisiti
- **Ambiente di sviluppo .NET** – Visual Studio 2022 o VS Code con l'estensione C#.  
- **GroupDocs.Editor per .NET** – scarica dalla pagina dei rilasci [GroupDocs.Editor for .NET](https://releases.groupdocs.com/editor/net/) .  
- **Conoscenza di base di C#** – dovresti sentirti a tuo agio con I/O di file e manipolazione di stringhe.  
- **Editor di testo (opzionale)** – per ispezionare i file sorgente; VS Code è consigliato.  
- Per un utilizzo dettagliato, consulta la [documentazione](https://tutorials.groupdocs.com/editor/net/).  
- Puoi anche navigare nella [pagina dei rilasci](https://releases.groupdocs.com/).

## Come modificare testo semplice passo dopo passo
Carica il file, modifica il suo contenuto e salvalo nuovamente – il tutto in meno di dieci righe di codice. Le sezioni seguenti ti guidano attraverso ogni fase con spiegazioni chiare.

### Passo 1: Ottieni il percorso del file TXT di input
Innanzitutto, decidi se lavorare con un percorso di file fisico o con uno stream in memoria. Usare un percorso è l'approccio più semplice per lo sviluppo locale.

```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

### Passo 2: Crea un'istanza di Editor
`Editor` è la classe principale che carica un documento e fornisce funzionalità di modifica.

```csharp
string inputFilePath = "YourSampleDocument.txt";
```

### Passo 3: Crea le opzioni di modifica TXT
`TxtEditOptions` configura come i file di testo semplice vengono analizzati e modificati, consentendo di impostare la codifica e le regole di gestione degli spazi.

```csharp
using (Editor editor = new Editor(inputFilePath))
{
```

### Passo 4: Crea un'istanza di EditableDocument
`EditableDocument` rappresenta la versione in memoria del documento caricato, includendo il suo testo e eventuali risorse associate.

```csharp
    TextEditOptions editOptions = new TextEditOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        RecognizeLists = true,
        LeadingSpaces = TextLeadingSpacesOptions.ConvertToIndent,
        TrailingSpaces = TextTrailingSpacesOptions.Trim
    };
```

### Passo 5: Modifica il contenuto del documento
Recupera il testo originale, applica le operazioni di stringa necessarie (ad esempio, replace, trim, change case) e memorizza il risultato nuovamente nell'`EditableDocument`.

```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```

### Passo 6: Crea un EditableDocument con contenuto aggiornato
Dopo aver trasformato il testo, istanzia un nuovo `EditableDocument` che contiene la stringa modificata e la collezione di risorse originale.

```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("text", "EDITED text");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```

### Passo 7: Crea le opzioni di salvataggio WordProcessing
`WordProcessingSaveOptions` definisce le impostazioni per salvare il documento in un formato compatibile con Word, come DOCX o DOCM.

```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```

### Passo 8: Crea le opzioni di salvataggio TXT
`TxtSaveOptions` specifica come il file di testo semplice modificato deve essere scritto, includendo la codifica, la conservazione delle terminazioni di riga e la gestione del layout delle tabelle.

```csharp
    WordProcessingSaveOptions wordSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm)
    {
        Locale = System.Globalization.CultureInfo.GetCultureInfo("en-GB")
    };
```

### Passo 9: Prepara i percorsi di output
Deriva la directory di output dal percorso del file di input, quindi costruisci i nomi completi dei file per i risultati DOCX e TXT.

```csharp
    TextSaveOptions txtSaveOptions = new TextSaveOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        PreserveTableLayout = true
    };
```

### Passo 10: Salva il documento modificato
Infine, chiama `editor.Save` due volte—una volta con le opzioni WordProcessing e una volta con le opzioni TXT—per produrre entrambi i formati in un'unica operazione.

```csharp
    string outputWordPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".docm");
    string outputTxtPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".txt");
```

## Problemi comuni e soluzioni
- **Gli spazi finali rimangono dopo la modifica** – assicurati che `TxtEditOptions.TrimTrailingSpaces` sia impostato su `true` prima di caricare il documento.  
- **Codifica errata nel file salvato** – verifica che `TxtSaveOptions.Encoding` corrisponda alla pagina di codice desiderata (ad es., `Encoding.UTF8`).  
- **File di grandi dimensioni causano OutOfMemoryException** – utilizza l'API streaming (`Editor.Load(Stream)`) invece di caricare da un percorso file per mantenere basso l'uso della memoria.  

## Domande frequenti

**D: Quali formati di file supporta GroupDocs.Editor per .NET?**  
R: La libreria supporta oltre 50 formati, inclusi DOCX, TXT, HTML, PDF e markdown, consentendo di modificare e convertire tra di essi senza problemi.

**D: Come posso ottenere una prova gratuita di GroupDocs.Editor per .NET?**  
R: Scarica la versione di prova dalla [pagina dei rilasci](https://releases.groupdocs.com/).

**D: Posso acquistare una licenza temporanea per i test?**  
R: Sì, le licenze temporanee sono disponibili tramite la [pagina di acquisto di GroupDocs](https://purchase.groupdocs.com/temporary-license/).

**D: Dove posso trovare supporto se riscontro problemi?**  
R: Il forum di supporto ufficiale è il posto migliore – visita il [forum di supporto di GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).

**D: Esiste una documentazione dettagliata per scenari avanzati?**  
R: Assolutamente. Il riferimento completo è disponibile nella [pagina di documentazione di GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/).

## Conclusione
Ora hai imparato a **modificare testo semplice** usando GroupDocs.Editor per .NET—caricando un file txt, rimuovendo gli spazi, convertendo gli spazi iniziali, impostando la codifica corretta e salvando il risultato sia in formato TXT che DOCX. Questa funzionalità ti consente di automatizzare la pulizia dei file di log, generare file di configurazione al volo o creare pipeline di elaborazione testo personalizzate senza reinventare la ruota. Esplora funzionalità aggiuntive come l'elaborazione batch e la conversione di documenti visitando la documentazione ufficiale.

---

**Last Updated:** 2026-08-10  
**Tested With:** GroupDocs.Editor 23.11 for .NET  
**Author:** GroupDocs  

```csharp
    editor.Save(afterEdit, outputWordPath, wordSaveOptions);
    editor.Save(afterEdit, outputTxtPath, txtSaveOptions);
}
System.Console.WriteLine("Document editing process completed successfully!");
```

## Tutorial correlati

- [Tutorial di caricamento documenti con GroupDocs.Editor per .NET](/editor/net/document-loading/)
- [Tutorial di salvataggio ed esportazione documenti per GroupDocs.Editor .NET](/editor/net/document-saving/)
- [Tutorial di modifica di testo semplice e documenti DSV per GroupDocs.Editor .NET](/editor/net/plain-text-dsv-documents/)