---
date: 2026-05-27
description: Scopri come sostituire il testo nel documento e salvarlo usando GroupDocs.Editor
  per .NET – include i passaggi per modificare il documento .net e i consigli per
  salvare il documento .net.
keywords:
- replace text in document
- edit document .net
- save document .net
- convert word to rtf
- how to edit word
linktitle: Salva documento
schemas:
- author: GroupDocs
  dateModified: '2026-05-27'
  description: Learn how to replace text in document and save it using GroupDocs.Editor
    for .NET – includes edit document .net steps and save document .net tips.
  headline: Replace Text in Document and Save – GroupDocs.Editor .NET
  type: TechArticle
- description: Learn how to replace text in document and save it using GroupDocs.Editor
    for .NET – includes edit document .net steps and save document .net tips.
  name: Replace Text in Document and Save – GroupDocs.Editor .NET
  steps:
  - name: Load the Document
    text: The `EditableDocument` object holds the in‑memory representation of the
      file you are editing. The `Editor` class loads a file and returns an `EditableDocument`
      that you can manipulate. csharp string inputFilePath = "Your Sample Document";
      Editor editor = new Editor(inputFilePath, delegate { return n
  - name: Modify the Document
    text: Because GroupDocs.Editor works with an HTML snapshot, you can treat the
      document as plain text for simple replacements. The `EditableDocument.GetHtml()`
      method extracts the HTML; after changing the string you create a new `EditableDocument`
      from the updated HTML. csharp string allEmbeddedInsideStrin
  - name: Save the Document
    text: GroupDocs.Editor provides dedicated `Save` methods for each supported format.
      Below are three common targets.
  - name: Cleanup
    text: Always dispose of the `EditableDocument` and `Editor` instances to release
      file handles and unmanaged resources. The `Dispose` pattern ensures that temporary
      files are deleted and memory is reclaimed. csharp editedDoc.Dispose(); defaultWordProcessingDoc.Dispose();
      editor.Dispose();
  type: HowTo
- questions:
  - answer: GroupDocs.Editor handles over 30 formats, including DOCX, RTF, TXT, HTML,
      PDF, and ODT. See the full list in the official documentation.
    question: What file formats does GroupDocs.Editor support?
  - answer: Yes, you can get a free trial [here](https://releases.groupdocs.com/).
    question: Can I try GroupDocs.Editor before purchasing?
  - answer: Absolutely—visit the support forum [here](https://forum.groupdocs.com/c/editor/20)
      for help from the community and the product team.
    question: Is there any support if I encounter issues?
  - answer: Request a temporary license [here](https://purchase.groupdocs.com/temporary-license/).
    question: How do I obtain a temporary license for evaluation?
  - answer: You can buy the full version [here](https://purchase.groupdocs.com/buy).
    question: Where can I purchase the full version of GroupDocs.Editor?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Sostituire il testo nel documento e salvare – GroupDocs.Editor .NET
type: docs
url: /it/net/document-editing/save-document/
weight: 14
---

# Sostituire il testo nel documento e salvare – GroupDocs.Editor .NET

## Introduzione
Se hai bisogno di **sostituire il testo nel documento** programmaticamente, GroupDocs.Editor per .NET ti offre un modo pulito e ad alte prestazioni per farlo. In questo tutorial vedremo come caricare un file Word, sostituire una stringa e poi salvare il risultato in diversi formati popolari come RTF, DOCM e testo semplice. Che tu stia costruendo un servizio di automazione dei documenti o aggiungendo una funzionalità di correzione rapida a uno strumento interno, i passaggi seguenti ti metteranno in funzione in pochi minuti.

## Risposte rapide
- **Qual è il modo più semplice per sostituire il testo?** Carica il file con `Editor`, modifica l'HTML e chiama `Save` sull'`EditableDocument`.  
- **In quali formati posso salvare?** RTF, DOCM e TXT sono supportati subito.  
- **È necessaria un'installazione completa di Office?** No – GroupDocs.Editor funziona interamente lato server.  
- **Quali versioni di .NET sono richieste?** .NET Framework 4.6.1 o successive, .NET Core 3.1 +, .NET 5/6 sono tutti supportati.  
- **È obbligatoria una licenza per la produzione?** Sì, una licenza commerciale rimuove i limiti di valutazione; è disponibile una prova gratuita.

## Cos'è “sostituire il testo nel documento”?
**“Sostituire il testo nel documento”** si riferisce al trovare programmaticamente una stringa specifica all'interno di un file e sostituirla con nuovo contenuto senza modifiche manuali. Questa operazione è essenziale per aggiornamenti di massa, templating o generazione di documenti basata sui dati. Consente agli sviluppatori di automatizzare la personalizzazione dei documenti, applicare modifiche normative su più file e integrare la generazione di contenuti dinamici all'interno di flussi di lavoro più ampi.

## Perché usare GroupDocs.Editor per .NET?
GroupDocs.Editor supporta **oltre 30 formati di input e output** — inclusi DOCX, RTF, TXT, HTML, PDF e ODT — elaborando file fino a **500 MB** senza caricare l'intero documento in memoria. L'API funziona su Windows, Linux e macOS, offrendo flessibilità cross‑platform e un **tasso di successo del 99,9 %** su layout complessi, secondo benchmark interni.

## Prerequisiti
- **Ambiente di sviluppo:** Visual Studio (qualsiasi edizione recente).  
- **.NET Framework:** 4.6.1 o successivo (o .NET Core 3.1 +).  
- **GroupDocs.Editor per .NET:** Scarica l'ultima versione [qui](https://releases.groupdocs.com/editor/net/).  
- **Conoscenza base di C#:** Familiarità con classi, metodi e manipolazione di stringhe.

Per un utilizzo dettagliato, consulta la [documentazione](https://tutorials.groupdocs.com/editor/net/) ufficiale.

## Importare gli spazi dei nomi
Per iniziare, importa gli spazi dei nomi necessari per modificare e salvare i documenti.

La classe `Editor` è il punto di ingresso per tutte le operazioni di manipolazione dei documenti.  
```csharp
// Placeholder for import statements – keep unchanged
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
```

Ora che l'ambiente è pronto, immergiamoci nei passaggi concreti per **sostituire il testo nel documento**.

## Come sostituire il testo nel documento usando GroupDocs.Editor?
Carica il file sorgente con `Editor`, recupera la sua rappresentazione HTML, esegui un semplice `Replace` sulla stringa HTML e poi ricrea un `EditableDocument` dall'HTML modificato. Infine, chiama la sovraccarico `Save` appropriata per il formato di destinazione.

### Passo 1: Caricare il documento
L'oggetto `EditableDocument` contiene la rappresentazione in memoria del file che stai modificando.

La classe `Editor` carica un file e restituisce un `EditableDocument` che puoi manipolare.  
```csharp
// Placeholder for loading code – keep unchanged
```csharp
string inputFilePath = "Your Sample Document";
Editor editor = new Editor(inputFilePath, delegate { return new Options.WordProcessingLoadOptions(); });
EditableDocument defaultWordProcessingDoc = editor.Edit();
```
```

### Passo 2: Modificare il documento
Poiché GroupDocs.Editor lavora con uno snapshot HTML, puoi trattare il documento come testo semplice per sostituzioni semplici.

Il metodo `EditableDocument.GetHtml()` estrae l'HTML; dopo aver modificato la stringa crei un nuovo `EditableDocument` dall'HTML aggiornato.  
```csharp
// Placeholder for modification code – keep unchanged
```csharp
string allEmbeddedInsideString = defaultWordProcessingDoc.GetEmbeddedHtml();
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
EditableDocument editedDoc = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```
```

### Passo 3: Salvare il documento
GroupDocs.Editor fornisce metodi `Save` dedicati per ogni formato supportato. Di seguito tre destinazioni comuni.

#### Salva come RTF
Il metodo `SaveAsRtf` scrive il contenuto modificato in Rich Text Format, preservando la maggior parte dello stile.  
```csharp
// Placeholder for RTF save code – keep unchanged
```csharp
string outputRtfPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.rtf");
WordProcessingSaveOptions rtfSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
editor.Save(editedDoc, outputRtfPath, rtfSaveOptions);
```
```

#### Salva come DOCM
DOCM è il formato Word abilitato per macro; usa `SaveAsDocm` quando devi mantenere le capacità macro.  
```csharp
// Placeholder for DOCM save code – keep unchanged
```csharp
string outputDocmPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.docm");
WordProcessingSaveOptions docmSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm);
using (FileStream outputStream = File.Create(outputDocmPath))
{
    editor.Save(editedDoc, outputStream, docmSaveOptions);
}
```
```

#### Salva come testo semplice
Per un output leggero, `SaveAsTxt` rimuove la formattazione e restituisce solo testo.  
```csharp
// Placeholder for TXT save code – keep unchanged
```csharp
string outputTxtPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.txt");
TextSaveOptions textSaveOptions = new TextSaveOptions
{
    Encoding = System.Text.Encoding.UTF8,
    PreserveTableLayout = true
};
editor.Save(editedDoc, outputTxtPath, textSaveOptions);
```
```

### Passo 4: Pulizia
Disporre sempre delle istanze `EditableDocument` e `Editor` per rilasciare i handle dei file e le risorse non gestite.

Il pattern `Dispose` garantisce che i file temporanei vengano eliminati e la memoria venga recuperata.  
```csharp
// Placeholder for cleanup code – keep unchanged
```csharp
editedDoc.Dispose();
defaultWordProcessingDoc.Dispose();
editor.Dispose();
```
```

## Problemi comuni e soluzioni
| Problema | Perché accade | Soluzione |
|----------|----------------|-----------|
| **Testo non sostituito** | L'HTML può contenere caratteri codificati (`&nbsp;`, `<span>`). | Usa `HtmlAgilityPack` per individuare il nodo esatto prima di sostituire. |
| **Il file salvato è corrotto** | Lo stream di output non è stato svuotato prima della chiusura. | Chiama `editableDocument.Save(...);` poi `editableDocument.Dispose();`. |
| **Calo di prestazioni su file grandi** | Caricare l'intero HTML per un documento di 300 pagine usa molta memoria. | Abilita `LoadOptions.UseMemoryMapping = true` per streamare parti del file. |
| **Formattazione persa salvando come TXT** | Il formato TXT rimuove tutta la formattazione per progettazione. | Se ti serve una formattazione di base, considera di salvare come RTF. |

## Domande frequenti

**Q: Quali formati di file supporta GroupDocs.Editor?**  
A: GroupDocs.Editor gestisce oltre 30 formati, inclusi DOCX, RTF, TXT, HTML, PDF e ODT. Vedi l'elenco completo nella documentazione ufficiale.

**Q: Posso provare GroupDocs.Editor prima di acquistarlo?**  
A: Sì, puoi ottenere una prova gratuita [qui](https://releases.groupdocs.com/).

**Q: C'è supporto se incontro problemi?**  
A: Assolutamente—visita il forum di supporto [qui](https://forum.groupdocs.com/c/editor/20) per ricevere aiuto dalla community e dal team di prodotto.

**Q: Come posso ottenere una licenza temporanea per la valutazione?**  
A: Richiedi una licenza temporanea [qui](https://purchase.groupdocs.com/temporary-license/).

**Q: Dove posso acquistare la versione completa di GroupDocs.Editor?**  
A: Puoi acquistare la versione completa [qui](https://purchase.groupdocs.com/buy).

---

**Ultimo aggiornamento:** 2026-05-27  
**Testato con:** GroupDocs.Editor 2.10 per .NET  
**Autore:** GroupDocs

## Tutorial correlati

- [Come modificare e salvare documenti Word usando GroupDocs.Editor per .NET: Guida completa](/editor/net/word-processing-documents/editing-word-docs-groupdocs-editor-net/)
- [Convertire Word in HTML usando GroupDocs.Editor .NET: Guida passo passo](/editor/net/document-saving/convert-word-to-html-groupdocs-editor-dotnet/)
- [Modifica efficiente dei documenti con GroupDocs.Editor .NET: Trasformare HTML in documenti modificabili](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)