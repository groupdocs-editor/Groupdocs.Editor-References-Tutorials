---
date: 2026-03-06
description: Impara come gestire il contenuto CSS con prefisso ed estrarre il contenuto
  CSS usando GroupDocs.Editor per .NET in questo dettagliato tutorial passo‑passo.
linktitle: Handle CSS Content with Prefix
second_title: GroupDocs.Editor .NET API
title: Gestisci il contenuto CSS con prefisso
type: docs
url: /it/net/css-handling/handle-css-content-with-prefix/
weight: 11
---

# Gestire il contenuto CSS con prefisso

In questo tutorial scoprirai **come gestire il prefisso CSS** quando lavori con i fogli di stile all'interno di un documento usando GroupDocs.Editor per .NET. Che tu debba anteporre un URL a immagini, font o qualsiasi risorsa esterna, i passaggi seguenti ti mostrano esattamente come **gestire il prefisso CSS** e anche come **estrarre il contenuto CSS** per ulteriori elaborazioni.

## Risposte rapide
- **Cosa significa “gestire il prefisso CSS”?** Aggiungere un prefisso URL personalizzato alle risorse esterne referenziate nel CSS.
- **Quale metodo API restituisce gli stili CSS?** `EditableDocument.GetCssContent(...)`.
- **Ho bisogno di una licenza?** È disponibile una licenza di prova; è necessaria una licenza commerciale per la produzione.
- **Quali versioni di .NET sono supportate?** .NET Framework 4.5+ e .NET Core/5/6.
- **Posso cambiare il prefisso a runtime?** Sì – basta passare una stringa diversa a `GetCssContent`.

## Cos'è **gestire il prefisso CSS**?
Applicare un prefisso alle risorse CSS riscrive i percorsi di immagini, font o altri asset in modo che puntino a una posizione che controlli (ad esempio, un CDN o un server sicuro). Questo è particolarmente utile quando esporti un documento e hai bisogno che tutti i riferimenti esterni siano raggiungibili da un'applicazione web.

## Perché usare GroupDocs.Editor per **estrarre il contenuto CSS**?
GroupDocs.Editor può leggere il CSS originale incorporato nei documenti WordProcessing, fornirti le stringhe del foglio di stile grezzo e consentirti di manipolarle prima del rendering o del salvataggio. Questo elimina la necessità di parsing manuale e garantisce che il CSS estratto corrisponda alla rappresentazione interna del documento.

## Prerequisiti
Prima di iniziare, assicurati di avere i seguenti prerequisiti:
- Visual Studio: Avrai bisogno di un'installazione funzionante di Visual Studio.  
- .NET Framework: Assicurati di avere installato il .NET Framework.  
- GroupDocs.Editor per .NET: Puoi scaricarlo [qui](https://releases.groupdocs.com/editor/net/).  
- Documento di esempio: Preparati un documento di esempio pronto per la modifica.

## Importare gli spazi dei nomi
Per prima cosa, importiamo gli spazi dei nomi necessari per garantire che il nostro codice funzioni senza problemi. Questo passaggio ci dà accesso alle classi core di GroupDocs.Editor.

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Editor.Options;
```

## Passo 1: Inizializzare l'Editor
Il primo passo consiste nel creare un'istanza di `Editor` con il tuo documento di esempio. Questo imposta l'ambiente di modifica.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```

## Passo 2: Modificare il documento
Successivamente, otteniamo un oggetto `EditableDocument`. Questo oggetto rappresenta la versione modificabile del file e ci permette di lavorare con le sue parti interne.

```csharp
    using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
    {
```

## Passo 3: Impostare i prefissi esterni
Definisci i prefissi URL per immagini e font. Questi prefissi saranno anteposti a ogni riferimento di immagine e font trovato nel CSS.

```csharp
        string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
        string externalFontsPrefix = "http://www.mywebsite.com/fonts/id=";
```

## Passo 4: **Estrarre il contenuto CSS** con i prefissi
Chiama `GetCssContent`, passando i prefissi appena definiti. Il metodo restituisce un elenco di stringhe di fogli di stile CSS che contengono già gli URL prefissati.

```csharp
        List<string> stylesheets = document.GetCssContent(externalImagesPrefix, externalFontsPrefix);
```

## Passo 5: Visualizzare i risultati
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
- **Nessun foglio di stile restituito** – Assicurati che il documento di origine contenga effettivamente CSS (ad esempio, un documento Word con tabelle stilizzate o HTML incorporato).  
- **URL errati** – Verifica che le stringhe del prefisso terminino con il delimitatore appropriato (`/` o `=`) per il routing del tuo server.  
- **Problemi di prestazioni** – Per documenti molto grandi, considera di elaborare i fogli di stile in batch per evitare un elevato utilizzo della memoria.

## Conclusione
Gestire il contenuto CSS con un prefisso usando GroupDocs.Editor per .NET è semplice e potente. Seguendo questi passaggi puoi **gestire il prefisso CSS**, recuperare il CSS grezzo tramite **estrarre il contenuto CSS**, e integrare senza problemi le risorse esterne nel tuo flusso di lavoro web. Esplora altre funzionalità di GroupDocs.Editor come la conversione HTML, l'estrazione di immagini e l'unione di documenti per ottenere ancora più valore dall'API.

## FAQ
### Posso usare GroupDocs.Editor per .NET con altri formati di documento?
Sì, GroupDocs.Editor per .NET supporta vari formati di documento, tra cui PDF, Word, Excel e altri.

### È disponibile una prova gratuita per GroupDocs.Editor per .NET?
Assolutamente! Puoi avviare la tua prova gratuita [qui](https://releases.groupdocs.com/).

### Come posso ottenere una licenza temporanea per GroupDocs.Editor per .NET?
Puoi ottenere una licenza temporanea [qui](https://purchase.groupdocs.com/temporary-license/).

### Dove posso trovare la documentazione dettagliata per GroupDocs.Editor per .NET?
La documentazione dettagliata è disponibile [qui](https://tutorials.groupdocs.com/editor/net/).

### Quali opzioni di supporto sono disponibili per GroupDocs.Editor per .NET?
Puoi ottenere supporto [qui](https://forum.groupdocs.com/c/editor/20).

## Ulteriori domande frequenti

**D: Posso cambiare il prefisso dopo aver estratto il CSS?**  
R: Sì. Chiama nuovamente `GetCssContent` con una stringa di prefisso diversa; il metodo utilizza sempre i valori che passi a runtime.

**D: Funziona con documenti protetti da password?**  
R: Sì. Fornisci la password in `WordProcessingLoadOptions` quando crei l'istanza di `Editor`.

**D: È possibile salvare il CSS modificato nuovamente nel documento?**  
R: GroupDocs.Editor attualmente fornisce accesso in sola lettura al CSS. Per persistere le modifiche dovresti sostituire il foglio di stile originale usando le API XML sottostanti del documento.

---

**Ultimo aggiornamento:** 2026-03-06  
**Testato con:** GroupDocs.Editor 23.12 for .NET  
**Autore:** GroupDocs