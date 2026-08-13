---
date: 2026-06-06
description: Scopri come **creare oggetti documento modificabile** da file CSV e TSV
  utilizzando GroupDocs.Editor per .NET. Questa guida mostra anche come **leggere
  testo delimitato C#** e **modificare CSV .NET** in modo efficiente in Visual Studio.
keywords:
- create editable document
- read delimited text c#
- edit csv .net
- parse delimited values c#
linktitle: Lavorare con Delimited Separated Values (DSV) – creare documento modificabile
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to **create editable document** objects from CSV and TSV
    files using GroupDocs.Editor for .NET. This guide also shows how to **read delimited
    text C#** and **edit CSV .NET** efficiently in Visual Studio.
  headline: Work with Delimited Separated Values (DSV) – create editable document
  type: TechArticle
- questions:
  - answer: Yes, the API streams data and can handle files larger than 1 GB without
      loading the entire document into memory.
    question: Can I use GroupDocs.Editor for .NET to edit large CSV files?
  - answer: Absolutely – any single‑character delimiter (e.g., pipe `|`, semicolon
      `;`) is supported as long as you specify it in `DelimitedTextEditOptions`.
    question: Does GroupDocs.Editor for .NET support other DSV formats besides CSV
      and TSV?
  - answer: Yes, you can set the `Encoding` property in `DelimitedTextSaveOptions`
      to UTF‑8, UTF‑16, ISO‑8859‑1, or any .NET `Encoding` you require.
    question: Is it possible to customize the encoding when saving DSV files?
  - answer: Yes – after editing, simply use `SpreadsheetSaveOptions` to export the
      content as an `.xlsx` workbook.
    question: Can I convert a CSV file to an Excel spreadsheet using GroupDocs.Editor
      for .NET?
  - answer: Detailed API references and code samples are available **[here](https://tutorials.groupdocs.com/editor/net/)**.
    question: Where can I find more documentation on GroupDocs.Editor for .NET?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Lavorare con Delimited Separated Values (DSV) – creare documento modificabile
type: docs
url: /it/net/document-processing/work-dsv/
weight: 12
---

# Lavorare con valori delimitati separati (DSV) – creare documento modificabile

Se sei uno sviluppatore .NET che ha bisogno di **create editable document** oggetti da valori delimitati separati (DSV) come CSV o TSV, sei nel posto giusto. Nei primi 100 parole spiegheremo perché GroupDocs.Editor per .NET è il modo più affidabile per **read delimited text C#**, modificarlo e poi salvarlo senza perdere la formattazione. Avrai a disposizione un flusso di lavoro completo, pronto per il copia‑incolla, che si integra naturalmente in qualsiasi soluzione Visual Studio.

## Risposte rapide
- **Quale libreria gestisce al meglio la modifica dei CSV in .NET?** GroupDocs.Editor for .NET.
- **Posso modificare file CSV di grandi dimensioni in Visual Studio?** Sì – l'API trasmette i dati in streaming e evita di caricare l'intero file in memoria.
- **Ho bisogno di una licenza per l'uso in produzione?** È necessaria una licenza commerciale; è disponibile una prova gratuita.
- **Quali formati posso esportare dopo la modifica?** CSV, TSV e formati di fogli di calcolo compatibili con Excel.
- **L'API è compatibile con .NET 6+?** Assolutamente – supporta .NET Framework 4.5+, .NET Core 3.1+, .NET 5 e .NET 6.

## Cos'è “create editable document” nel contesto di GroupDocs.Editor?
**Create editable document** indica la generazione di un'istanza `EditableDocument` che rappresenta una versione modificabile di un file sorgente (CSV, TSV, ecc.) in memoria. Questo oggetto consente di leggere, modificare e risalvare il contenuto usando la stessa API. Fornisce metodi per recuperare il testo del documento, applicare modifiche e salvarlo nuovamente in vari formati, garantendo che l'allineamento delle colonne e le virgolette siano preservati.

## Perché usare GroupDocs.Editor per la gestione dei DSV?
GroupDocs.Editor elabora **più di 50 formati di input e output**, inclusi CSV, TSV e fogli di calcolo compatibili con Excel, mantenendo l'uso della memoria sotto i 10 MB per file fino a 500 MB. Inoltre preserva automaticamente l'allineamento delle colonne, le regole di quotatura e le codifiche personalizzate, eliminando la necessità di logica di parsing manuale.

## Prerequisiti
Prima di iniziare, assicurati di avere installato quanto segue:

- **Visual Studio** (qualsiasi edizione recente) – svilupperai e eseguirai il debug direttamente nell'IDE.
- **GroupDocs.Editor for .NET** – scarica l'ultimo pacchetto **[here](https://releases.groupdocs.com/editor/net/)**.
- **Conoscenza base di C#** – il tutorial presuppone che tu possa creare un progetto console o ASP.NET e aggiungere pacchetti NuGet.

## Importare gli spazi dei nomi
Le classi `Editor`, `EditableDocument` e le classi di opzioni si trovano nello spazio dei nomi `GroupDocs.Editor`.  

La classe `DelimitedTextEditOptions` è il punto di ingresso per definire il delimitatore (virgola, tabulazione, ecc.) e altre regole di parsing.

```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

## Come creare un documento modificabile da un file CSV?
Carica il CSV sorgente con `Editor` e chiama il metodo `Edit`, passando un'istanza `DelimitedTextEditOptions` che specifica un delimitatore a virgola. Il metodo restituisce un `EditableDocument` che puoi manipolare in memoria. Questo schema a due passaggi—load → edit—copre scenari **read delimited text C#** e garantisce che la struttura originale del file venga mantenuta.

## Passo 1: Ottenere il percorso del file DSV di input
Innanzitutto, devi specificare il percorso assoluto o relativo del file DSV sorgente. Per dimostrazione useremo un semplice CSV situato nella cartella `Data` del progetto.

```csharp
string inputFilePath = "Your Sample Document";
```

## Passo 2: Creare un'istanza di Editor
`Editor` è la classe principale che orchestra il caricamento, la modifica e il salvataggio. Istanziare con un oggetto `FileInfo` ti dà il pieno controllo sul ciclo di vita del file.

```csharp
using (Editor editor = new Editor(inputFilePath))
{
```

## Passo 3: Creare le opzioni di modifica DSV
`DelimitedTextEditOptions` indica all'editor come interpretare il file. Puoi impostare il delimitatore, se la prima riga contiene intestazioni e la codifica dei caratteri.

```csharp
    Options.DelimitedTextEditOptions editOptions = new DelimitedTextEditOptions(",");
    editOptions.ConvertDateTimeData = false;
    editOptions.ConvertNumericData = true;
    editOptions.TreatConsecutiveDelimitersAsOne = true;
```

## Passo 4: Creare un'istanza di EditableDocument
`EditableDocument` rappresenta una versione modificabile in memoria del file sorgente. Chiamare `Editor.Edit` con le opzioni restituisce un `EditableDocument`. Questo oggetto contiene il testo del file in una stringa modificabile, pronta per qualsiasi operazione **parse delimited values C#** di cui hai bisogno.

```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```

## Passo 5: Modificare il contenuto del documento
`GetDocumentText()` restituisce il testo corrente del documento modificabile come stringa. Recupera il testo originale tramite `EditableDocument.GetDocumentText()`, esegui le modifiche (ad esempio, sostituisci il valore di una colonna) e memorizza il risultato in una nuova stringa. Qui è dove **edit CSV .NET** senza toccare i flussi di file a basso livello.

```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("SsangYong", "Chevrolet").Replace("Kyron", "Camaro");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```

## Passo 6: Creare un EditableDocument con contenuto aggiornato
Riconverti la stringa modificata in un `EditableDocument`. Questo passaggio finalizza le modifiche e prepara l'oggetto per il salvataggio in qualsiasi formato supportato.

```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```

## Passo 7: Creare le opzioni di salvataggio CSV
`DelimitedTextSaveOptions` specifica come scrivere il contenuto modificato nuovamente in un file CSV. Quando sei pronto a persistere le modifiche, configura `DelimitedTextSaveOptions`. Puoi specificare lo stesso delimitatore, uno diverso o anche modificare lo stile di terminazione delle righe.

```csharp
    Options.DelimitedTextSaveOptions csvSaveOptions = new DelimitedTextSaveOptions(",");
    csvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

## Passo 8: Creare le opzioni di salvataggio TSV
Se ti serve una versione separata da tabulazioni, basta cambiare il delimitatore in `\t`. Lo stesso `EditableDocument` può essere salvato più volte con opzioni diverse.

```csharp
    Options.DelimitedTextSaveOptions tsvSaveOptions = new DelimitedTextSaveOptions("\t");
    tsvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

## Passo 9: Creare le opzioni di salvataggio Spreadsheet
`SpreadsheetSaveOptions` configura l'esportazione del documento in formati compatibili con Excel come .xlsx. GroupDocs.Editor consente anche di esportare i dati modificati in un formato compatibile con Excel (`.xlsx`). La classe `SpreadsheetSaveOptions` gestisce automaticamente i tipi di colonna, le formule e lo stile delle celle.

```csharp
    Options.SpreadsheetSaveOptions cellsSaveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
```

## Passo 10: Preparare i percorsi di salvataggio
Definisci percorsi di output distinti per ogni formato. Utilizzare convenzioni di denominazione chiare (ad esempio, `output.csv`, `output.tsv`, `output.xlsx`) aiuta a mantenere il progetto organizzato.

```csharp
    string outputCsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".csv");
    string outputTsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".tsv");
    string outputCellsPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".xlsm");
```

## Passo 11: Salvare il documento modificato
`Save()` scrive il documento su disco usando le opzioni di salvataggio fornite. Invoca `EditableDocument.Save` con le opzioni appropriate per ogni formato di destinazione. L'API scrive il file direttamente su disco, preservando la codifica originale a meno che non la sovrascrivi.

```csharp
    editor.Save(afterEdit, outputCsvPath, csvSaveOptions);
    editor.Save(afterEdit, outputTsvPath, tsvSaveOptions);
    editor.Save(afterEdit, outputCellsPath, cellsSaveOptions);
```

## Passo 12: Rilasciare le istanze di EditableDocument
Sia `Editor` che `EditableDocument` implementano `IDisposable`. Rilasciarli libera i handle dei file e le risorse non gestite, cosa cruciale quando si elaborano molti file in un lavoro batch.

```csharp
    beforeEdit.Dispose();
    afterEdit.Dispose();
}
System.Console.WriteLine("WorkingWithDsv routine has successfully finished");
```

## Problemi comuni e soluzioni
| Problema | Perché accade | Soluzione |
|----------|----------------|-----------|
| **Virgolette extra inattese** | Il parser CSV predefinito può trattare le virgole incorporate come delimitatori. | Imposta `EscapeMode = EscapeMode.DoubleQuote` in `DelimitedTextEditOptions`. |
| **Picco di memoria con file grandi** | Caricamento di un file da 500 MB senza streaming. | Usa `Editor.Load` con `LoadOptions` che abilitano il caricamento pigro. |
| **Mancata corrispondenza di codifica** | Il file sorgente usa UTF‑16 ma le opzioni di default sono UTF‑8. | Imposta esplicitamente `Encoding = Encoding.Unicode` nelle opzioni di salvataggio. |

## Domande frequenti

**Q: Posso usare GroupDocs.Editor per .NET per modificare file CSV di grandi dimensioni?**  
A: Sì, l'API trasmette i dati in streaming e può gestire file più grandi di 1 GB senza caricare l'intero documento in memoria.

**Q: GroupDocs.Editor per .NET supporta altri formati DSV oltre a CSV e TSV?**  
A: Assolutamente – qualsiasi delimitatore a singolo carattere (ad esempio, pipe `|`, punto e virgola `;`) è supportato purché lo specifichi in `DelimitedTextEditOptions`.

**Q: È possibile personalizzare la codifica durante il salvataggio dei file DSV?**  
A: Sì, puoi impostare la proprietà `Encoding` in `DelimitedTextSaveOptions` a UTF‑8, UTF‑16, ISO‑8859‑1, o qualsiasi `Encoding` .NET tu richieda.

**Q: Posso convertire un file CSV in un foglio di calcolo Excel usando GroupDocs.Editor per .NET?**  
A: Sì – dopo la modifica, usa semplicemente `SpreadsheetSaveOptions` per esportare il contenuto come un workbook `.xlsx`.

**Q: Dove posso trovare ulteriore documentazione su GroupDocs.Editor per .NET?**  
A: Riferimenti API dettagliati e esempi di codice sono disponibili **[here](https://tutorials.groupdocs.com/editor/net/)**.

**Last Updated:** 2026-06-06  
**Tested With:** GroupDocs.Editor 23.10 for .NET  
**Author:** GroupDocs

## Tutorial correlati

- [Tutorial di editing di testo semplice e documenti DSV per GroupDocs.Editor .NET](/editor/net/plain-text-dsv-documents/)
- [Padroneggiare GroupDocs.Editor .NET per l'editing efficiente di documenti CSV e la conversione](/editor/net/plain-text-dsv-documents/groupdocs-editor-net-csv-editing-guide/)
- [Padroneggiare il caricamento dei documenti in .NET con GroupDocs.Editor: Guida completa](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)