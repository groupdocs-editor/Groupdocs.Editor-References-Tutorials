---
date: 2026-09-26
description: Scopri come gestire il prefisso CSS ed estrarre il contenuto CSS usando
  GroupDocs.Editor per .NET in questo tutorial dettagliato passo‑passo.
keywords:
- handle css prefix
- extract css content
- edit document css
- prepend url to css
lastmod: 2026-09-26
linktitle: Gestisci il contenuto CSS con prefisso
og_description: Scopri come gestire il prefisso CSS ed estrarre il contenuto CSS con
  GroupDocs.Editor per .NET. Segui una guida passo‑passo per anteporre gli URL alle
  risorse CSS e recuperare i fogli di stile.
og_image_alt: Developer guide showing css prefix handling with GroupDocs.Editor for
  .NET
og_title: Come gestire il prefisso CSS in GroupDocs.Editor per .NET
schemas:
- author: GroupDocs
  dateModified: '2026-09-26'
  description: Learn how to handle css prefix and extract css content using GroupDocs.Editor
    for .NET in this detailed step‑by‑step tutorial.
  headline: How to handle css prefix in GroupDocs.Editor for .NET
  type: TechArticle
- questions:
  - answer: Yes, GroupDocs.Editor for .NET supports PDF, Word, Excel, PowerPoint,
      and many other formats.
    question: Can I use GroupDocs.Editor for .NET with other document formats?
  - answer: Absolutely! You can start your free trial on the [GroupDocs free trial
      page](https://releases.groupdocs.com/).
    question: Is there a free trial available for GroupDocs.Editor for .NET?
  - answer: You can obtain a temporary license from the [temporary license page](https://purchase.groupdocs.com/temporary-license/).
    question: How do I get a temporary license for GroupDocs.Editor for .NET?
  - answer: Detailed documentation is available on the [GroupDocs.Editor for .NET
      documentation site](https://tutorials.groupdocs.com/editor/net/).
    question: Where can I find detailed documentation for GroupDocs.Editor for .NET?
  - answer: You can get support through the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).
    question: What support options are available for GroupDocs.Editor for .NET?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
tags:
- css handling
- GroupDocs.Editor
- .NET document processing
- css prefix
- api tutorial
title: Come gestire il prefisso CSS in GroupDocs.Editor per .NET
type: docs
url: /it/net/css-handling/handle-css-content-with-prefix/
weight: 11
---

# Come gestire il prefisso CSS in GroupDocs.Editor per .NET

In questo tutorial imparerai **come gestire il prefisso CSS** quando lavori con i fogli di stile all'interno di un documento usando GroupDocs.Editor per .NET. Che tu debba anteporre un URL a immagini, font o qualsiasi risorsa esterna, i passaggi seguenti ti mostrano esattamente come **gestire il prefisso CSS** e anche come **estrarre il contenuto CSS** per ulteriori elaborazioni. Alla fine della guida sarai in grado di riscrivere i percorsi delle risorse, recuperare le stringhe CSS grezze e integrarle nel tuo flusso di lavoro web con fiducia.

## Risposte rapide
- **Cosa significa “gestire il prefisso CSS”?** Aggiungere un prefisso URL personalizzato alle risorse esterne referenziate nel CSS.  
- **Quale metodo API restituisce gli stili CSS?** `EditableDocument.GetCssContent(...)`.  
- **Ho bisogno di una licenza?** È disponibile una licenza di prova; è necessaria una licenza commerciale per la produzione.  
- **Quali versioni di .NET sono supportate?** .NET Framework 4.5+ e .NET Core/5/6.  
- **Posso cambiare il prefisso a runtime?** Sì – basta passare una stringa diversa a `GetCssContent`.  

## Cos'è il prefisso CSS?
Il termine si riferisce alla riscrittura degli URL di immagini, font o qualsiasi asset esterno all'interno di un file CSS in modo che puntino a una posizione sotto il tuo controllo, come un CDN o un server sicuro. Anteponendo un URL base coerente garantisci che ogni risorsa venga caricata correttamente quando il documento viene visualizzato in un browser o in un visualizzatore web.

## Perché usare GroupDocs.Editor per estrarre il contenuto CSS?
GroupDocs.Editor può leggere il CSS originale incorporato nei documenti WordProcessing, restituire le stringhe del foglio di stile grezzo e consentirti di manipolarle prima del rendering o del salvataggio. Questo elimina l'analisi manuale, garantisce la fedeltà alla rappresentazione interna del documento e supporta **oltre 30 formati di file** elaborando file fino a **500 MB** senza caricare l'intero file in memoria.

## Prerequisiti
- Visual Studio: Avrai bisogno di un'installazione funzionante di Visual Studio.  
- .NET Framework: Assicurati di avere installato il .NET Framework.  
- GroupDocs.Editor per .NET: Puoi scaricarlo dalla [pagina di download di GroupDocs.Editor per .NET](https://releases.groupdocs.com/editor/net/).  
- Documento di esempio: Preparati un documento di esempio pronto per la modifica.

## Importa gli spazi dei nomi
Per prima cosa, importiamo gli spazi dei nomi necessari per garantire che il nostro codice funzioni senza problemi. Questo passaggio ci dà accesso alle classi principali di GroupDocs.Editor.

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Editor.Options;
```

## Passo 1: Inizializza l'Editor
La classe `Editor` è il punto di ingresso per lavorare con i documenti in GroupDocs.Editor. Gestisce le operazioni di caricamento, modifica e salvataggio.  
Il primo passo consiste nel creare un'istanza di `Editor` con il tuo documento di esempio. Questo configura l'ambiente di modifica.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```

## Passo 2: Modifica il documento
L'oggetto `EditableDocument` rappresenta la versione modificabile del file e espone le sue parti interne, come CSS, immagini e HTML.  
Successivamente, otteniamo un oggetto `EditableDocument`. Questo oggetto ci permette di lavorare con il CSS interno del documento.

```csharp
    using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
    {
```

## Passo 3: Imposta i prefissi esterni
Definisci i prefissi URL per immagini e font. Questi prefissi saranno anteposti a ogni riferimento di immagine e font trovato nel CSS.

```csharp
        string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
        string externalFontsPrefix = "http://www.mywebsite.com/fonts/id=";
```

## Passo 4: Estrai il contenuto CSS con i prefissi
`GetCssContent` restituisce una collezione di stringhe di fogli di stile CSS che contengono già gli URL prefissati forniti.  
Chiama `GetCssContent`, passando i prefissi appena definiti. Il metodo restituisce un elenco di stringhe di fogli di stile CSS che contengono già gli URL prefissati.

```csharp
        List<string> stylesheets = document.GetCssContent(externalImagesPrefix, externalFontsPrefix);
```

## Passo 5: Visualizza i risultati
Stampa il numero di fogli di stile trovati e visualizza ciascun foglio di stile. Questo ti aiuta a verificare che i prefissi siano stati applicati correttamente.

```csharp
        Console.WriteLine("There are {0} stylesheets in the input document", stylesheets.Count);
        foreach (string css in stylesheets)
        {
            Console.WriteLine(css);
        }
    }
}
```

## Problemi comuni e soluzioni
- **Nessun foglio di stile restituito** – Assicurati che il documento di origine contenga effettivamente CSS (ad esempio, un documento Word con tabelle formattate o HTML incorporato).  
- **URL errati** – Verifica che le stringhe di prefisso terminino con il delimitatore appropriato (`/` o `=`) per il routing del tuo server.  
- **Problemi di prestazioni** – Per documenti molto grandi, considera di elaborare i fogli di stile in batch per evitare un elevato utilizzo di memoria.  

## Domande frequenti

**Q: Posso usare GroupDocs.Editor per .NET con altri formati di documento?**  
A: Sì, GroupDocs.Editor per .NET supporta PDF, Word, Excel, PowerPoint e molti altri formati.

**Q: È disponibile una versione di prova gratuita per GroupDocs.Editor per .NET?**  
A: Assolutamente! Puoi avviare la tua prova gratuita sulla [pagina di prova gratuita di GroupDocs](https://releases.groupdocs.com/).

**Q: Come posso ottenere una licenza temporanea per GroupDocs.Editor per .NET?**  
A: Puoi ottenere una licenza temporanea dalla [pagina della licenza temporanea](https://purchase.groupdocs.com/temporary-license/).

**Q: Dove posso trovare la documentazione dettagliata per GroupDocs.Editor per .NET?**  
A: La documentazione dettagliata è disponibile sul [sito di documentazione di GroupDocs.Editor per .NET](https://tutorials.groupdocs.com/editor/net/).

**Q: Quali opzioni di supporto sono disponibili per GroupDocs.Editor per .NET?**  
A: Puoi ottenere supporto tramite il [forum di supporto di GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).

## Ulteriori domande frequenti

**Q: Posso cambiare il prefisso dopo aver estratto il CSS?**  
A: Sì. Chiama nuovamente `GetCssContent` con una stringa di prefisso diversa; il metodo utilizza sempre i valori che passi a runtime.

**Q: Funziona con documenti protetti da password?**  
A: Sì. Fornisci la password in `WordProcessingLoadOptions` quando crei l'istanza di `Editor`.

**Q: È possibile salvare il CSS modificato nuovamente nel documento?**  
A: Attualmente GroupDocs.Editor fornisce accesso in sola lettura al CSS. Per persistere le modifiche dovresti sostituire il foglio di stile originale usando le API XML sottostanti del documento.

---

**Ultimo aggiornamento:** 2026-09-26  
**Testato con:** GroupDocs.Editor 23.12 per .NET  
**Autore:** GroupDocs

## Tutorial correlati

- [Estrai CSS esterno da documenti Word usando GroupDocs.Editor .NET&#58; Guida completa](/editor/net/html-web-documents/extract-external-css-word-docs-groupdocs-editor-dotnet/)
- [Estrai e prefissa HTML da documenti Word usando GroupDocs.Editor .NET](/editor/net/html-web-documents/groupdocs-editor-dotnet-extract-prefix-html-word-docs/)
- [Come estrarre e modificare il contenuto HTML nei documenti Word usando GroupDocs.Editor .NET](/editor/net/html-web-documents/extract-modify-html-content-word-docs-groupdocs-editor-net/)