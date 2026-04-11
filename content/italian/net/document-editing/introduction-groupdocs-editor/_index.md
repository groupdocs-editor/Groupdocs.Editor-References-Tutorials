---
date: 2026-04-11
description: Scopri come modificare programmaticamente un documento Word usando GroupDocs.Editor
  per .NET e convertire Word in RTF in questa guida dettagliata passo‑passo.
keywords:
- programmatically edit word document
- convert pdf to editable
- replace text in document
- convert word to rtf
- save document to stream
linktitle: Modifica programmaticamente un documento Word con GroupDocs.Editor per
  .NET
second_title: GroupDocs.Editor .NET API
title: Modifica programmaticamente un documento Word con GroupDocs.Editor per .NET
type: docs
url: /it/net/document-editing/introduction-groupdocs-editor/
weight: 12
---

# Modifica programmaticamente documenti Word con GroupDocs.Editor per .NET

Se sei uno sviluppatore .NET che ha bisogno di **modificare programmaticamente documenti Word** — che sia per sostituire testo, convertire formati o incorporare il risultato in uno stream — GroupDocs.Editor per .NET è una libreria robusta e facile da usare che porta a termine il lavoro. In questo tutorial vedremo un esempio reale che copre il caricamento di un file DOCX, la modifica del suo contenuto, la conversione del risultato in RTF e il salvataggio sia su disco che in uno stream di memoria.

## Risposte rapide
- **Cosa posso modificare?** Word, PDF, HTML, RTF e molti altri formati.  
- **Posso sostituire il testo?** Sì – usa la semplice sostituzione di stringhe o una manipolazione DOM più avanzata.  
- **Come converto un PDF in editabile?** Carica il PDF con `Editor` e modifica l'HTML generato.  
- **Qual è il modo più semplice per salvare su uno stream?** Usa `editor.Save(editableDoc, stream, options)`.  
- **Ho bisogno di una licenza?** È necessaria una licenza temporanea o completa per l'uso in produzione.

## Cos'è la modifica programmatica di documenti Word?
Modificare programmaticamente un documento Word significa utilizzare il codice — anziché un'interfaccia grafica — per aprire un file, modificarne il contenuto (testo, immagini, stili) e scrivere la versione modificata nuovamente nello storage. Questo approccio alimenta la generazione automatizzata di report, gli aggiornamenti massivi di documenti e la creazione di contenuti personalizzati.

## Perché usare GroupDocs.Editor per .NET?
- **Flessibilità di formato:** Carica DOCX, PDF, HTML, RTF, ecc., e salva in qualsiasi formato supportato.  
- **Nessuna dipendenza da Office:** Funziona senza che Microsoft Office sia installato sul server.  
- **Compatibile con gli stream:** Perfetto per scenari cloud in cui si legge/scrive da stream invece che dal file system.  
- **API ricca:** Accesso a immagini, font, CSS e altre risorse per una modifica completa.

## Prerequisiti
Prima di immergerci nell'implementazione, assicurati di avere:

- Visual Studio 2017 o successivo.  
- .NET Framework 4.6.1 o successivo.  
- GroupDocs.Editor per .NET – puoi [scaricare](https://releases.groupdocs.com/editor/net/) dal sito.  
- Una licenza valida o una [licenza temporanea](https://purchase.groupdocs.com/temporary-license/) da GroupDocs.

## Importa gli spazi dei nomi
Per iniziare a usare GroupDocs.Editor per .NET, importa gli spazi dei nomi richiesti:

```csharp
using System;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```

Nelle sezioni successive suddivideremo il flusso di lavoro in passaggi di piccole dimensioni così potrai seguirlo facilmente.

## Passo 1: Ottieni il percorso del file di input
Specifica la posizione del file Word che desideri modificare. Per questo esempio supporremo un DOCX chiamato **Your Sample Document.docx**.

```csharp
string inputFilePath = "Your Sample Document.docx";
```

## Passo 2: Istanzia l'oggetto Editor
Crea un'istanza di `Editor` passando il percorso di input. Questo carica il documento e lo prepara per la modifica.

```csharp
using (GroupDocs.Editor.Editor editor = new Editor(inputFilePath))
{
    // Subsequent steps will be nested inside this block
}
```

## Passo 3: Apri il documento per la modifica
Ottieni un `EditableDocument` che ti dà accesso alla rappresentazione HTML del documento e alle sue risorse.

```csharp
EditableDocument beforeEdit = editor.Edit();
```

## Passo 4: Recupera il contenuto e le risorse del documento
Puoi estrarre l'HTML grezzo, le immagini, i font e il CSS. Questo è utile quando devi manipolare direttamente il markup.

```csharp
string content = beforeEdit.GetContent();
var images = beforeEdit.Images;
var fonts = beforeEdit.Fonts;
var stylesheets = beforeEdit.Css;
```

### Passo 4.1: Ottieni il documento come singola stringa codificata Base64
Se preferisci una singola stringa che contiene tutte le risorse incorporate, chiama `GetEmbeddedHtml()`.

```csharp
string allEmbeddedInsideString = beforeEdit.GetEmbeddedHtml();
```

### Passo 4.2: Modifica il contenuto
Sostituiamo la parola **Subtitle** con **Edited subtitle** per dimostrare una semplice sostituzione di testo.

```csharp
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
```

## Passo 5: Crea una nuova istanza di EditableDocument
Dopo aver modificato il markup, avvolgilo nuovamente in un oggetto `EditableDocument`.

```csharp
EditableDocument afterEdit = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```

## Passo 6: Salva il documento modificato
Salveremo il risultato come file RTF, mostrando sia un percorso del file system sia un'opzione di stream di memoria.

### Passo 6.1: Prepara il percorso di output
Definisci dove deve essere scritto il RTF.

```csharp
string outputPath = Path.Combine("Output Directory Path", Path.GetFileNameWithoutExtension(inputFilePath) + ".rtf");
```

### Passo 6.2: Prepara le opzioni di salvataggio
Seleziona il formato RTF tramite `WordProcessingSaveOptions`.

```csharp
Options.WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
```

### Passo 6.3: Salva su percorso
Scrivi il documento modificato sul file system.

```csharp
editor.Save(afterEdit, outputPath, saveOptions);
```

### Passo 6.4: Salva su uno stream
Se ti serve il risultato in memoria (ad esempio per caricarlo su storage cloud), usa un `MemoryStream`.

```csharp
using (MemoryStream ms = new MemoryStream())
{
    editor.Save(afterEdit, ms, saveOptions);
}
```

## Passo 7: Rilascia le istanze di Editor e EditableDocument
Libera le risorse tempestivamente per evitare perdite di memoria.

```csharp
beforeEdit.Dispose();
afterEdit.Dispose();
editor.Dispose();
```

## Casi d'uso comuni e suggerimenti
- **Converti PDF in editabile:** Carica un PDF con `Editor`, modifica l'HTML generato, poi salva nuovamente in PDF o in un altro formato.  
- **Sostituisci testo nel documento:** Usa `string.Replace` per casi semplici o manipola il DOM per scenari complessi.  
- **Converti Word in RTF:** Come mostrato sopra, imposta `WordProcessingFormats.Rtf` nelle opzioni di salvataggio.  
- **Salva documento su stream:** Ideale per API web che restituiscono file direttamente al client.  
- **Carica documento per la modifica:** Avvolgi sempre `Editor` in un blocco `using` per garantire il corretto rilascio.

## Domande frequenti

**Q:** Posso modificare file PDF usando GroupDocs.Editor per .NET?  
**A:** Sì, GroupDocs.Editor supporta la modifica dei PDF convertendoli in una rappresentazione HTML intermedia.

**Q:** Come ottengo una licenza temporanea per GroupDocs.Editor per .NET?  
**A:** Puoi ottenere una licenza temporanea dal [sito web di GroupDocs](https://purchase.groupdocs.com/temporary-license/).

**Q:** Quali formati di file sono supportati da GroupDocs.Editor per .NET?  
**A:** Sono supportati DOCX, PDF, HTML, RTF e molti altri formati.

**Q:** È possibile integrare GroupDocs.Editor con lo storage cloud?  
**A:** Assolutamente – puoi leggere/scrivere stream da Azure Blob, Amazon S3, Google Cloud Storage, ecc.

**Q:** Dove posso trovare la documentazione per GroupDocs.Editor per .NET?  
**A:** La documentazione è disponibile [qui](https://tutorials.groupdocs.com/editor/net/).

---

**Ultimo aggiornamento:** 2026-04-11  
**Testato con:** GroupDocs.Editor 23.12 per .NET  
**Autore:** GroupDocs