---
date: 2026-05-27
description: Scopri come caricare documenti da file, stream o cloud storage utilizzando
  GroupDocs.Editor per .NET – la guida più completa per gestire più formati di file.
keywords:
- how to load documents
- load documents from file
- load documents from stream
- handle multiple file formats
- load pdf .net
schemas:
- author: GroupDocs
  dateModified: '2026-05-27'
  description: Learn how to load documents from file, stream, or cloud storage using
    GroupDocs.Editor for .NET – the most complete guide for handling multiple file
    formats.
  headline: How to Load Documents with GroupDocs.Editor for .NET
  type: TechArticle
- description: Learn how to load documents from file, stream, or cloud storage using
    GroupDocs.Editor for .NET – the most complete guide for handling multiple file
    formats.
  name: How to Load Documents with GroupDocs.Editor for .NET
  steps:
  - name: Initialize the Editor
    text: Create the `Editor` object once per application lifecycle to reuse internal
      resources.
  - name: Choose the Correct Load Options
    text: 'Select `LoadOptions` that match your source type: - `FileLoadOptions` for
      local files. - `StreamLoadOptions` for streams. - `CustomStorageLoadOptions`
      for custom storage providers.'
  - name: Call the Load Method
    text: Pass the source path or stream along with the options. The method returns
      an `EditorDocument` you can edit, extract text from, or convert to another format.
  - name: Dispose Resources
    text: After you finish editing, call `Dispose()` on the `Editor` instance or wrap
      it in a `using` block to free unmanaged resources.
  type: HowTo
- questions:
  - answer: Yes. Provide the password in `LoadOptions.Password` before calling the
      load method; the library will decrypt the file automatically.
    question: Can I load a password‑protected PDF?
  - answer: Absolutely. Implement `IStorageProvider` for Azure Blob, then use `CustomStorageLoadOptions`
      to point to the blob URL.
    question: Does GroupDocs.Editor support loading documents from Azure Blob Storage?
  - answer: The library can stream files up to **2 GB** without loading the entire
      content into memory, limited only by the underlying storage and .NET runtime.
    question: What is the maximum file size I can load?
  - answer: Use `Editor.GetDocumentInfo(filePath)` to retrieve metadata such as page
      count and format without loading the full document.
    question: Is there a way to preview a document before fully loading it?
  - answer: Wrap the `Editor` instance in a `using` block or call `Dispose()` manually;
      this ensures all native handles are freed promptly.
    question: How do I release resources after editing?
  type: FAQPage
title: Come caricare documenti con GroupDocs.Editor per .NET
type: docs
url: /it/net/document-loading/
weight: 2
---

# Come caricare documenti con GroupDocs.Editor per .NET

Caricare documenti in modo efficiente è un requisito fondamentale per qualsiasi applicazione .NET che lavora con contratti, report o contenuti generati dagli utenti. In questa guida scoprirai **come caricare documenti** da un file system locale, da uno stream di memoria o da qualsiasi provider di storage personalizzato usando GroupDocs.Editor. Esamineremo ogni scenario, spiegheremo perché l'API si comporta in questo modo e ti mostreremo consigli pratici per mantenere basso l'uso della memoria supportando oltre 30 diversi formati di file.

## Risposte rapide
- **Qual è il primo passo per caricare un documento?** Inizializza l'istanza `Editor` con i `LoadOptions` appropriati.  
- **Posso caricare PDF direttamente?** Sì – GroupDocs.Editor tratta i PDF allo stesso modo di file Word, Excel o PowerPoint.  
- **È necessaria una licenza per lo sviluppo?** Una licenza temporanea funziona per i test; è necessaria una licenza completa per la produzione.  
- **Quali versioni .NET sono supportate?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.  
- **Quanti formati vengono gestiti?** Oltre 30 formati di input e output, inclusi DOCX, XLSX, PPTX, PDF, HTML e tipi di immagine.

## Cos'è GroupDocs.Editor?
GroupDocs.Editor è una libreria .NET che consente agli sviluppatori di **caricare, modificare e salvare** una vasta gamma di tipi di documento senza richiedere l'installazione di Microsoft Office sul server. Astrae le specifiche dei formati di file dietro un'API unificata, rendendo semplice lavorare con Word, Excel, PowerPoint, PDF e molti altri formati in un unico codebase.

## Perché usare GroupDocs.Editor per caricare documenti?
GroupDocs.Editor elabora **oltre 30 formati di file** e può gestire documenti fino a **500 MB** senza caricare l'intero file in memoria, grazie alla sua architettura di streaming. Questa capacità quantificata riduce il consumo di RAM del server fino al **70 %** rispetto agli approcci tradizionali di interop Office, ed elimina i problemi di licenza associati a Microsoft Office.

## Prerequisiti
- Runtime .NET Framework 4.6+ o .NET Core 3.1+ installato.  
- Una licenza valida di GroupDocs.Editor per .NET (licenza temporanea per la valutazione).  
- Pacchetto NuGet `GroupDocs.Editor` aggiunto al tuo progetto.  

## Come caricare documenti da un file?
La classe `Editor` è il componente principale usato per caricare e modificare documenti. `FileLoadOptions` specifica i parametri di caricamento come formato e password quando si apre un file. Per caricare un documento da un percorso locale, crea un'istanza `Editor` e passa un oggetto `FileLoadOptions` che definisce il formato se non può essere dedotto automaticamente. La libreria legge l'intestazione del file, valida il formato e restituisce un `EditorDocument` pronto per la modifica.

## Come caricare documenti da uno stream?
Uno `Stream` è una rappresentazione di una sequenza di byte per operazioni I/O. `StreamLoadOptions` ti consente di fornire il nome originale del file affinché il formato possa essere rilevato. Se il tuo documento si trova in un database o in un blob cloud, puoi caricarlo direttamente da uno `Stream` fornendo lo stream e `StreamLoadOptions`. Questo evita file temporanei su disco, migliora la sicurezza e velocizza l'elaborazione per conversioni batch ad alto throughput.

## Come caricare documenti da storage personalizzato?
`IStorageProvider` è un'interfaccia per implementare backend di storage personalizzati. `CustomStorageLoadOptions` ti consente di specificare il provider di storage e le credenziali necessarie. GroupDocs.Editor ti permette di collegare un'implementazione di storage personalizzata ereditando da `IStorageProvider`. Questo è utile quando devi leggere da Amazon S3, Azure Blob o da un server di file on‑premises mantenendo la stessa logica di caricamento, consentendo un'integrazione fluida con i servizi cloud esistenti.

## Guida passo‑passo al caricamento

### Passo 1: Inizializzare l'Editor
Crea l'oggetto `Editor` una volta per ciclo di vita dell'applicazione per riutilizzare le risorse interne.

### Passo 2: Scegliere le opzioni di caricamento corrette
Seleziona `LoadOptions` che corrispondono al tuo tipo di origine:

- `FileLoadOptions` per file locali.  
- `StreamLoadOptions` per stream.  
- `CustomStorageLoadOptions` per provider di storage personalizzati.

### Passo 3: Chiamare il metodo Load
Passa il percorso o lo stream di origine insieme alle opzioni. Il metodo restituisce un `EditorDocument` che puoi modificare, estrarre testo o convertire in un altro formato.

### Passo 4: Rilasciare le risorse
Dopo aver terminato la modifica, chiama `Dispose()` sull'istanza `Editor` o avvolgila in un blocco `using` per liberare le risorse non gestite.

## Problemi comuni e soluzioni
- **Errore di formato non supportato** – Verifica che l'estensione del file corrisponda a uno dei più di 30 formati supportati; altrimenti, specifica esplicitamente il formato in `LoadOptions`.  
- **Out‑of‑memory per PDF di grandi dimensioni** – Abilita `LoadOptions.MemoryLimit` per forzare la modalità streaming, che mantiene l'uso della memoria sotto la soglia configurata.  
- **Permesso negato sullo storage cloud** – Assicurati che le credenziali del provider di storage abbiano accesso in lettura e che l'implementazione `IStorageProvider` dell'SDK inoltri correttamente il token di autenticazione.

## Tutorial disponibili

### [Come caricare documenti Word usando GroupDocs.Editor in .NET: Guida completa](./load-word-documents-groupdocs-editor-net/)
Scopri come caricare e modificare documenti Word con GroupDocs.Editor in .NET. Questa guida fornisce istruzioni passo‑passo, consigli sulle prestazioni e applicazioni reali.

### [Padroneggiare i formati di documento con GroupDocs.Editor .NET: Guida completa alla gestione di diversi tipi di file](./groupdocs-editor-net-tutorial-document-formats/)
Scopri come gestire vari formati di documento usando GroupDocs.Editor per .NET. Questa guida copre l'elenco, l'analisi e l'integrazione dei tipi di file supportati nei tuoi progetti.

### [Padroneggiare il caricamento di documenti in .NET con GroupDocs.Editor: Guida completa](./groupdocs-editor-net-document-loading-guide/)
Scopri come caricare ed editare documenti in modo efficiente usando GroupDocs.Editor per .NET. Questa guida copre il caricamento senza opzioni, l'applicazione di opzioni di caricamento specifiche e l'ottimizzazione dell'uso della memoria.

## Risorse aggiuntive

- [Documentazione di GroupDocs.Editor per .net](https://docs.groupdocs.com/editor/net/)
- [Riferimento API di GroupDocs.Editor per .net](https://reference.groupdocs.com/editor/net/)
- [Download di GroupDocs.Editor per .net](https://releases.groupdocs.com/editor/net/)
- [Forum di GroupDocs.Editor](https://forum.groupdocs.com/c/editor)
- [Supporto gratuito](https://forum.groupdocs.com/)
- [Licenza temporanea](https://purchase.groupdocs.com/temporary-license/)

## Domande frequenti

**Q: Posso caricare un PDF protetto da password?**  
A: Sì. Fornisci la password in `LoadOptions.Password` prima di chiamare il metodo di caricamento; la libreria decritterà il file automaticamente.

**Q: GroupDocs.Editor supporta il caricamento di documenti da Azure Blob Storage?**  
A: Assolutamente. Implementa `IStorageProvider` per Azure Blob, quindi usa `CustomStorageLoadOptions` per puntare all'URL del blob.

**Q: Qual è la dimensione massima del file che posso caricare?**  
A: La libreria può fare streaming di file fino a **2 GB** senza caricare l'intero contenuto in memoria, limitata solo dallo storage sottostante e dal runtime .NET.

**Q: Esiste un modo per visualizzare un'anteprima di un documento prima di caricarlo completamente?**  
A: Usa `Editor.GetDocumentInfo(filePath)` per recuperare i metadati come il conteggio delle pagine e il formato senza caricare l'intero documento.

**Q: Come rilascio le risorse dopo la modifica?**  
A: Avvolgi l'istanza `Editor` in un blocco `using` o chiama `Dispose()` manualmente; questo garantisce che tutte le handle native vengano liberate prontamente.

---

**Ultimo aggiornamento:** 2026-05-27  
**Testato con:** GroupDocs.Editor 23.12 per .NET  
**Autore:** GroupDocs

## Tutorial correlati

- [Padroneggiare la modifica e la conversione di documenti con GroupDocs.Editor .NET: Guida completa](/editor/net/document-editing/groupdocs-editor-net-mastering-document-editing/)
- [Modifica PDF efficiente con GroupDocs.Editor .NET: Opzioni di caricamento e funzionalità di paginazione](/editor/net/pdf-documents/edit-pdfs-groupdocs-editor-net/)
- [Guida all'implementazione della licenza GroupDocs.Editor .NET da file](/editor/net/licensing-configuration/implement-groupdocs-editor-net-license-file/)