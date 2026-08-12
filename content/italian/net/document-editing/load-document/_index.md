---
date: 2026-04-20
description: Scopri come caricare un documento protetto da password utilizzando GroupDocs.Editor
  per .NET, inclusi il caricamento da un percorso file, da un flusso di byte e da
  un database.
keywords:
- load password protected document
- load document from stream
- load document from database
linktitle: Carica documento protetto da password
second_title: GroupDocs.Editor .NET API
title: Carica documento protetto da password con GroupDocs.Editor .NET
type: docs
url: /it/net/document-editing/load-document/
weight: 13
---

# Carica documento protetto da password con GroupDocs.Editor .NET

## Introduzione
Modificare i documenti programmaticamente può sembrare opprimente, soprattutto quando è necessario **load password protected document** file che risiedono in posizioni diverse. Che il file sia su disco, provenga da un flusso di byte o sia memorizzato in un database, GroupDocs.Editor per .NET ti offre un'API pulita e coerente per gestire tutti questi scenari. In questa guida percorreremo i prerequisiti, importeremo gli spazi dei nomi richiesti e ti mostreremo passo‑passo come caricare i documenti usando vari metodi—compreso il caso speciale dei file protetti da password.

## Risposte rapide
- **GroupDocs.Editor può aprire file protetti da password?** Sì, utilizza le opzioni di caricamento appropriate impostando la password.  
- **Quali versioni .NET sono supportate?** .NET Framework 2.0+ e .NET Core/5/6 sono tutti compatibili.  
- **Devo rilasciare l'oggetto Editor?** Assolutamente—chiama `Dispose()` per liberare le risorse.  
- **Posso caricare un documento da un database?** Sì, recupera il file come array di byte o stream e passalo al costruttore `Editor`.  
- **Esiste un limite di dimensione del file?** I file di grandi dimensioni sono supportati; considera di utilizzare il caricamento basato su stream con opzioni di ottimizzazione della memoria.

## Che cosa è “load password protected document”?
Caricare un documento protetto da password significa aprire un file che richiede una password per l'accesso, quindi fornire quella password programmaticamente affinché l'API possa decrittare e lavorare con il contenuto. GroupDocs.Editor astrae il passaggio di decrittazione tramite le opzioni di caricamento, rendendo il processo semplice.

## Perché usare GroupDocs.Editor per caricare i documenti?
- **Unified API** – Lo stesso codice funziona per file Word, Excel, PowerPoint e HTML.  
- **Password handling** – Supporto integrato per file crittografati senza decrittazione manuale.  
- **Stream flexibility** – Carica da percorsi file, stream o qualsiasi fonte personalizzata come un database.  
- **Resource management** – Il semplice pattern `Dispose()` mantiene basso l'uso della memoria.

## Prerequisiti
Prima di iniziare, assicurati di avere i seguenti prerequisiti configurati:
- **Visual Studio** – Assicurati di avere Visual Studio installato sulla tua macchina.  
- **.NET Framework** – GroupDocs.Editor per .NET supporta .NET Framework 2.0 o successivo. Assicurati che il tuo progetto punti a un framework compatibile.  
- **GroupDocs.Editor for .NET** – Scarica l'ultima versione dalla [download page](https://releases.groupdocs.com/editor/net/).  
- **Basic Knowledge of C#** – Familiarità con C# e la programmazione .NET è necessaria per seguire questo tutorial.

## Importa spazi dei nomi
Per iniziare a usare GroupDocs.Editor per .NET, devi importare gli spazi dei nomi necessari nel tuo progetto. Aggiungi le seguenti direttive using all'inizio del tuo file C#:

```csharp
using GroupDocs.Editor.Options;
using System.IO;
```

Questi spazi dei nomi forniranno l'accesso alle classi e ai metodi richiesti per le attività di modifica dei documenti.

## Passo 1: Carica documento da un percorso file
Caricare un documento da un percorso file è semplice. Questo metodo è ideale per documenti memorizzati localmente sulla tua macchina.

```csharp
string inputPath = "Your Sample Document";
// Load document as file via path and without load options
Editor editor1 = new Editor(inputPath);
// Dispose resources
editor1.Dispose();
System.Console.WriteLine("Document loaded successfully from file path.");
```

## Passo 2: Carica documento con Load Options (file protetti da password)
A volte, potresti dover caricare documenti che richiedono una gestione speciale, come i file protetti da password. In tali casi, puoi utilizzare le opzioni di caricamento.

```csharp
string inputPath = "Your Sample Document";
// Create load options for Word documents
WordProcessingLoadOptions wordLoadOptions = new WordProcessingLoadOptions();
wordLoadOptions.Password = "some password";
// Load document as file via path and with load options
Editor editor2 = new Editor(inputPath, delegate { return wordLoadOptions; });
// Dispose resources
editor2.Dispose();
System.Console.WriteLine("Password-protected document loaded successfully.");
```

## Come caricare un documento da stream
Caricare un documento da un byte stream è utile quando devi elaborare documenti che non sono memorizzati come file, ad esempio quelli recuperati da un database o da un servizio web.

```csharp
FileStream inputStream = File.OpenRead("Your Sample Document");
// Load document as content from byte stream and without load options
Editor editor3 = new Editor(delegate { return inputStream; });
// Dispose resources
editor3.Dispose();
System.Console.WriteLine("Document loaded successfully from byte stream.");
```

## Passo 4: Carica documento con Load Options da un byte stream
Per i documenti che richiedono una gestione speciale quando vengono caricati da un byte stream, puoi combinare il caricamento da stream con le opzioni di caricamento.

```csharp
FileStream inputStream = File.OpenRead("Your Sample Document");
// Create load options for spreadsheets
SpreadsheetLoadOptions sheetLoadOptions = new SpreadsheetLoadOptions();
sheetLoadOptions.OptimizeMemoryUsage = true;
// Load document as content from byte stream and with load options
Editor editor4 = new Editor(delegate { return inputStream; }, delegate { return sheetLoadOptions; });
// Dispose resources
editor4.Dispose();
System.Console.WriteLine("Spreadsheet document loaded successfully with load options.");
```

## Come caricare un documento da un database
Se i tuoi documenti sono memorizzati in un database relazionale, recupera i dati binari (ad es., usando `SELECT FileData FROM Documents WHERE Id = @id`) e passa il risultato `byte[]` o `MemoryStream` al costruttore `Editor` proprio come nell'esempio di stream sopra. Questo mantiene il tuo codice coerente indipendentemente dalla sorgente.

## Problemi comuni e soluzioni
- **Incorrect password** – L'editor genererà un'eccezione. Verifica il valore della password e assicurati di utilizzare la classe di load options corretta per il tipo di file.  
- **Stream already closed** – Assicurati che lo stream rimanga aperto per tutta la durata dell'istanza `Editor`, oppure copia lo stream in un `MemoryStream`.  
- **Memory consumption with large files** – Usa `SpreadsheetLoadOptions.OptimizeMemoryUsage = true` (come mostrato) o opzioni equivalenti per altri formati.

## Domande frequenti

**Q: Quali formati di file sono supportati da GroupDocs.Editor per .NET?**  
**A:** GroupDocs.Editor supporta un'ampia gamma di formati di file, inclusi DOCX, XLSX, PPTX, HTML e molti altri. Per un elenco completo, consulta la [documentation](https://tutorials.groupdocs.com/editor/net/).

**Q: Come gestisco i documenti protetti da password?**  
**A:** Puoi utilizzare le opzioni di caricamento come `WordProcessingLoadOptions` per specificare la password durante il caricamento di documenti protetti da password.

**Q: Posso usare GroupDocs.Editor in un'applicazione web?**  
**A:** Sì, GroupDocs.Editor può essere utilizzato in applicazioni web. Assicurati di gestire correttamente gli stream dei file e lo smaltimento delle risorse per evitare perdite di memoria.

**Q: Dove posso ottenere una licenza temporanea per GroupDocs.Editor?**  
**A:** Puoi ottenere una licenza temporanea dalla [temporary license page](https://purchase.groupdocs.com/temporary-license/).

**Q: È disponibile supporto se incontro problemi?**  
**A:** Sì, GroupDocs fornisce supporto tramite il loro [support forum](https://forum.groupdocs.com/c/editor/20).

**Q: Il caricamento da un database richiede configurazioni speciali?**  
**A:** Nessuna configurazione speciale è necessaria oltre al recupero dei dati binari e al loro passaggio come stream o array di byte al costruttore `Editor`.

**Q: Come posso migliorare le prestazioni quando carico fogli di calcolo molto grandi?**  
**A:** Abilita opzioni di ottimizzazione della memoria come `SpreadsheetLoadOptions.OptimizeMemoryUsage = true` per ridurre l'impronta di memoria.

## Conclusione
Congratulazioni! Hai imparato con successo come **load password protected document** file usando GroupDocs.Editor per .NET in vari modi. Che tu stia gestendo file locali, documenti protetti da password, byte stream o contenuti memorizzati in un database, GroupDocs.Editor fornisce una soluzione flessibile e potente per le tue esigenze di modifica dei documenti. Ricorda di rilasciare sempre l'istanza `Editor` per mantenere la tua applicazione performante ed efficiente in termini di risorse.

---

**Last Updated:** 2026-04-20  
**Tested With:** GroupDocs.Editor 2.0 (latest)  
**Author:** GroupDocs