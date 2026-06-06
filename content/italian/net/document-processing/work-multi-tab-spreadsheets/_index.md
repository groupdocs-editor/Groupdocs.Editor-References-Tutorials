---
date: 2026-06-06
description: Scopri come **salvare ogni scheda Excel** usando GroupDocs.Editor per
  .NET – guida passo‑passo, esempi di codice e best practices per suddividere i file
  XLSX.
keywords:
- save each excel tab
- read multiple sheets
- convert excel tab pdf
- split xlsx files
linktitle: Lavorare con fogli di calcolo a più schede
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to **save each Excel tab** using GroupDocs.Editor for .NET
    – step‑by‑step guide, code snippets, and best practices for splitting XLSX files.
  headline: How to save each Excel tab with GroupDocs.Editor .NET
  type: TechArticle
- description: Learn how to **save each Excel tab** using GroupDocs.Editor for .NET
    – step‑by‑step guide, code snippets, and best practices for splitting XLSX files.
  name: How to save each Excel tab with GroupDocs.Editor .NET
  steps:
  - name: Get a Path to the Input File
    text: First, specify the full path to the source XLSX that contains multiple tabs.
  - name: Load the Spreadsheet into the Editor Instance
    text: The `Editor` class is the entry point for all document operations in GroupDocs.Editor.
      It reads the file stream and prepares the document for editing or extraction.
  - name: Create an EditableDocument from the First Tab
    text: '`EditableDocument` represents a single, editable sheet within the workbook.
      The constructor takes the `Editor` instance and a zero‑based sheet index.'
  - name: Create an EditableDocument from the Second Tab
    text: You can repeat the same pattern for any additional sheet by changing the
      index value.
  - name: Save the First Tab to a Separate Document
    text: '`Save` writes the edited document to a file in the specified format. Call
      it on the `EditableDocument` instance, providing the output path and format
      (e.g., `SaveFormat.Xlsx`).'
  - name: Save the Second Tab to a Separate Document
    text: The same `Save` call works for the second sheet, and you can choose a different
      format such as PDF if needed.
  - name: Dispose of EditableDocument Instances
    text: '`Dispose` releases unmanaged resources held by the document, such as file
      handles, ensuring no leaks in long‑running services.'
  type: HowTo
- questions:
  - answer: Hidden sheets are treated like any other sheet; you can access them by
      index and save them, but you may need to set `EditableDocument.IsVisible = true`
      before saving if you want them visible in the output.
    question: What if my workbook contains hidden sheets?
  - answer: Yes, specify `SaveFormat.Pdf` when calling `Save` on the `EditableDocument`.
      The library preserves layout, images, and charts during conversion.
    question: Can I convert an Excel tab directly to PDF?
  - answer: Absolutely. Use `SaveFormat.Csv` for each `EditableDocument` to generate
      plain‑text CSV representations of each sheet.
    question: Is it possible to split a workbook into CSV files instead of XLSX?
  - answer: It does. Provide the password via `LoadOptions.Password` when creating
      the `Editor` instance.
    question: Does GroupDocs.Editor support password‑protected Excel files?
  - answer: The official documentation and sample projects on the [download page](https://releases.groupdocs.com/editor/net/)
      contain additional use‑cases.
    question: Where can I find more examples of working with spreadsheets?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Come salvare ogni scheda Excel con GroupDocs.Editor .NET
type: docs
url: /it/net/document-processing/work-multi-tab-spreadsheets/
weight: 17
---

# Lavorare con fogli di calcolo a più schede

## Introduzione
Se hai bisogno di **salvare ogni scheda Excel** come file indipendente, GroupDocs.Editor per .NET lo rende semplice. Che tu stia estraendo report finanziari, generando fogli di lavoro per dipartimento o convertendo le schede in PDF, questo tutorial ti guida attraverso l'intero flusso di lavoro — dalla configurazione dell'ambiente al rilascio delle risorse — così potrai automatizzare la gestione di più fogli con sicurezza.

## Risposte rapide
- **GroupDocs.Editor può dividere un XLSX in file separati?** Sì, puoi caricare la cartella di lavoro ed esportare ogni foglio singolarmente.  
- **In quali formati può essere salvata ogni scheda?** XLSX, CSV, PDF, HTML e altri – sono supportati oltre 30 formati di output.  
- **È necessaria una licenza per questa funzionalità?** Una licenza temporanea è sufficiente per i test; è necessaria una licenza completa per la produzione.  
- **.NET Core è supportato?** Assolutamente – la libreria funziona con .NET Framework 4.0+ e .NET Core/5/6+.  
- **Quante schede possono essere elaborate contemporaneamente?** GroupDocs.Editor può gestire cartelle di lavoro con più di 500 fogli senza caricare l'intero file in memoria.

## Cos'è “salvare ogni scheda Excel”?
**“Salvare ogni scheda Excel”** significa estrarre ogni foglio di lavoro da una cartella di lavoro a più fogli e scrivere ciascuno in un documento autonomo (ad esempio file XLSX o PDF separati). Questo approccio semplifica l'elaborazione a valle, la generazione di report e la distribuzione fornendo un file per foglio, che può poi essere condiviso, archiviato o trasformato ulteriormente in modo indipendente.

## Perché usare GroupDocs.Editor per questo compito?
GroupDocs.Editor supporta **oltre 30 formati di input e output** e può elaborare fogli di calcolo con **fino a 1.000 fogli** mantenendo un basso utilizzo di memoria grazie allo streaming dei dati invece di caricare l'intero file. L'API preserva inoltre gli stili delle celle, le formule e le immagini incorporate, garantendo che ogni scheda esportata abbia lo stesso aspetto dell'originale.

## Prerequisiti
Prima di immergerti, verifica di avere:

1. **Visual Studio** – qualsiasi edizione recente (Community, Professional o Enterprise).  
2. **.NET Framework 4.0+** – oppure .NET Core/5/6 se preferisci l'ambiente di esecuzione multipiattaforma.  
3. **GroupDocs.Editor for .NET** – scaricalo dalla [pagina di download](https://releases.groupdocs.com/editor/net/).  
4. **Licenza** – una [licenza temporanea](https://purchase.groupdocs.com/temporary-license/) è sufficiente per i test; acquista una licenza completa per l'uso in produzione.  
5. **Prova gratuita** – puoi anche provare la libreria tramite la pagina di [prova gratuita](https://releases.groupdocs.com/) .  
6. **Supporto** – se incontri problemi, visita il [forum di supporto](https://forum.groupdocs.com/c/editor/20) o considera la [pagina di acquisto](https://purchase.groupdocs.com/buy) per una licenza completa.

## Importare i namespace
Prima di iniziare a scrivere codice, devi importare gli spazi dei nomi necessari. Aggiungi le seguenti direttive using all'inizio del tuo file `.cs`:

```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```

## Come salvare ogni scheda Excel come file separato?
Carica la cartella di lavoro, crea un `EditableDocument` per ogni foglio e chiama `Save` con il formato desiderato. Questo processo isola ogni scheda, ti consente di scegliere un percorso di output distinto e rilascia le risorse automaticamente. Di seguito trovi il flusso di lavoro passo‑passo da seguire, con spiegazioni per ogni chiamata API e consigli di best practice per evitare problemi comuni.

### Passo 1: Ottenere il percorso del file di input
Innanzitutto, specifica il percorso completo del file XLSX di origine che contiene più schede.

```csharp
string inputFilePath = "Your Sample Document";
```

### Passo 2: Caricare il foglio di calcolo nell'istanza Editor
La classe `Editor` è il punto di ingresso per tutte le operazioni sui documenti in GroupDocs.Editor. Legge lo stream del file e prepara il documento per la modifica o l'estrazione.

```csharp
using (FileStream inputStream = File.OpenRead(inputFilePath))
{
    using (Editor editor = new Editor(delegate { return inputStream; }, delegate { return new SpreadsheetLoadOptions(); }))
    {
        // Further steps will go here
    }
}
```

### Passo 3: Creare un EditableDocument dalla prima scheda
`EditableDocument` rappresenta un singolo foglio modificabile all'interno della cartella di lavoro. Il costruttore accetta l'istanza `Editor` e un indice di foglio basato su zero.

```csharp
SpreadsheetEditOptions editOptions1 = new SpreadsheetEditOptions();
editOptions1.WorksheetIndex = 0; // First tab
EditableDocument firstTabBeforeEdit = editor.Edit(editOptions1);
```

### Passo 4: Creare un EditableDocument dalla seconda scheda
Puoi ripetere lo stesso schema per qualsiasi foglio aggiuntivo modificando il valore dell'indice.

```csharp
SpreadsheetEditOptions editOptions2 = new SpreadsheetEditOptions();
editOptions2.WorksheetIndex = 1; // Second tab
EditableDocument secondTabBeforeEdit = editor.Edit(editOptions2);
```

### Passo 5: Salvare la prima scheda in un documento separato
`Save` scrive il documento modificato in un file nel formato specificato. Invocalo sull'istanza `EditableDocument`, fornendo il percorso di output e il formato (ad esempio, `SaveFormat.Xlsx`).

```csharp
SpreadsheetSaveOptions saveOptions1 = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
string outputFilename1 = Path.GetFileNameWithoutExtension(inputFilePath) + "_tab1.xlsm";
string outputPath1 = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename1);
editor.Save(firstTabBeforeEdit, outputPath1, saveOptions1);
```

### Passo 6: Salvare la seconda scheda in un documento separato
La stessa chiamata `Save` funziona per il secondo foglio, e puoi scegliere un formato diverso come PDF se necessario.

```csharp
SpreadsheetSaveOptions saveOptions2 = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsb);
string outputFilename2 = Path.GetFileNameWithoutExtension(inputFilePath) + "_tab2.xlsb";
string outputPath2 = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename2);
editor.Save(secondTabBeforeEdit, outputPath2, saveOptions2);
```

### Passo 7: Rilasciare le istanze di EditableDocument
`Dispose` rilascia le risorse non gestite detenute dal documento, come i handle dei file, garantendo l'assenza di perdite in servizi a lungo termine.

```csharp
firstTabBeforeEdit.Dispose();
secondTabBeforeEdit.Dispose();
```

## Problemi comuni e soluzioni
- **Errori “File is locked”** – Assicurati di chiamare `Dispose()` su ogni `EditableDocument` e sull'istanza `Editor`, oppure avvolgili in istruzioni `using`.  
- **Stili mancanti dopo l'esportazione** – Verifica di salvare in un formato che supporta lo styling (ad esempio, XLSX o PDF). CSV perderà la formattazione per design.  
- **Cartelle di lavoro grandi causano prestazioni lente** – Usa le opzioni di caricamento in streaming (`LoadOptions.Streaming = true`) per mantenere basso l'uso della memoria.

## Domande frequenti

**D: Cosa succede se la mia cartella di lavoro contiene fogli nascosti?**  
R: I fogli nascosti sono trattati come qualsiasi altro foglio; puoi accedervi per indice e salvarli, ma potresti dover impostare `EditableDocument.IsVisible = true` prima di salvare se desideri che siano visibili nell'output.

**D: Posso convertire direttamente una scheda Excel in PDF?**  
R: Sì, specifica `SaveFormat.Pdf` quando chiami `Save` sul `EditableDocument`. La libreria preserva layout, immagini e grafici durante la conversione.

**D: È possibile dividere una cartella di lavoro in file CSV invece di XLSX?**  
R: Assolutamente. Usa `SaveFormat.Csv` per ogni `EditableDocument` per generare rappresentazioni CSV in testo semplice di ogni foglio.

**D: GroupDocs.Editor supporta file Excel protetti da password?**  
R: Sì. Fornisci la password tramite `LoadOptions.Password` quando crei l'istanza `Editor`.

**D: Dove posso trovare più esempi di lavoro con i fogli di calcolo?**  
R: La documentazione ufficiale e i progetti di esempio sulla [pagina di download](https://releases.groupdocs.com/editor/net/) contengono ulteriori casi d'uso.

## Conclusione
Seguendo questi passaggi, puoi **salvare ogni scheda Excel** come documento indipendente, convertire le schede in PDF o dividere grandi cartelle di lavoro in parti gestibili — tutto con la affidabile e ad alte prestazioni libreria GroupDocs.Editor per .NET. Questa funzionalità semplifica le pipeline di reporting, automatizza l'estrazione dei dati e riduce la gestione manuale dei fogli di calcolo.

---

**Ultimo aggiornamento:** 2026-06-06  
**Testato con:** GroupDocs.Editor 23.11 per .NET  
**Autore:** GroupDocs  

---

## Tutorial correlati

- [Estrazione avanzata delle schede di foglio di calcolo in .NET con GroupDocs.Editor](/editor/net/spreadsheet-documents/mastering-spreadsheet-tab-extraction-dotnet-groupdocs-editor/)
- [Proteggi con password i file Excel usando GroupDocs.Editor per .NET \| Gestione sicura dei fogli di calcolo](/editor/net/spreadsheet-documents/groupdocs-editor-net-password-excel-files/)
- [Padronanza del caricamento dei documenti in .NET con GroupDocs.Editor: Guida completa](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)