---
title: Carica documento
linktitle: Carica documento
second_title: API GroupDocs.Editor .NET
description: Scopri come modificare i documenti a livello di codice con GroupDocs.Editor per .NET. Guida passo passo per caricare documenti, gestire file protetti da password e altro ancora.
weight: 13
url: /it/net/document-editing/load-document/
---

# Carica documento

## introduzione
La modifica dei documenti a livello di codice può essere un compito arduo, soprattutto se hai a che fare con formati di file diversi e strutture complesse. Fortunatamente, GroupDocs.Editor per .NET rende questo compito un gioco da ragazzi, fornendo un'API robusta e facile da usare per modificare un'ampia gamma di tipi di documenti. In questo tutorial ti guideremo attraverso tutto ciò di cui hai bisogno per iniziare con GroupDocs.Editor per .NET, inclusi i prerequisiti, come importare gli spazi dei nomi e una guida dettagliata passo passo per caricare i documenti utilizzando vari metodi.
## Prerequisiti
Prima di approfondire, assicurati di aver configurato i seguenti prerequisiti:
- Visual Studio: assicurati di avere Visual Studio installato sul tuo computer.
- .NET Framework: GroupDocs.Editor per .NET supporta .NET Framework 2.0 o versione successiva. Assicurati che il tuo progetto abbia come target un framework compatibile.
-  GroupDocs.Editor per .NET: scarica la versione più recente da[pagina di download](https://releases.groupdocs.com/editor/net/).
- Conoscenza di base di C#: per seguire questo tutorial è necessaria la familiarità con la programmazione C# e .NET.
## Importa spazi dei nomi
Per iniziare a utilizzare GroupDocs.Editor per .NET, devi importare gli spazi dei nomi necessari nel tuo progetto. Aggiungi le seguenti direttive using nella parte superiore del file C#:
```csharp
using GroupDocs.Editor.Options;
using System.IO;
```
Questi spazi dei nomi forniranno l'accesso alle classi e ai metodi richiesti per le attività di modifica dei documenti.
## Passaggio 1: caricare il documento da un percorso file
Caricare un documento da un percorso file è semplice. Questo metodo è ideale per i documenti archiviati localmente sul computer.

```csharp
string inputPath = "Your Sample Document";
// Carica il documento come file tramite percorso e senza opzioni di caricamento
Editor editor1 = new Editor(inputPath);
// Smaltire le risorse
editor1.Dispose();
System.Console.WriteLine("Document loaded successfully from file path.");
```
## Passaggio 2: caricare il documento con le opzioni di caricamento
A volte potrebbe essere necessario caricare documenti che richiedono una gestione speciale, come file protetti da password. In questi casi, puoi utilizzare le opzioni di caricamento.

```csharp
string inputPath = "Your Sample Document";
//Crea opzioni di caricamento per i documenti Word
WordProcessingLoadOptions wordLoadOptions = new WordProcessingLoadOptions();
wordLoadOptions.Password = "some password";
// Carica il documento come file tramite percorso e con opzioni di caricamento
Editor editor2 = new Editor(inputPath, delegate { return wordLoadOptions; });
// Smaltire le risorse
editor2.Dispose();
System.Console.WriteLine("Password-protected document loaded successfully.");
```
## Passaggio 3: caricare il documento da un flusso di byte
Il caricamento di un documento da un flusso di byte è utile quando è necessario elaborare documenti che non sono archiviati come file, come quelli recuperati da un database o da un servizio Web.

```csharp
FileStream inputStream = File.OpenRead("Your Sample Document");
// Carica il documento come contenuto dal flusso di byte e senza opzioni di caricamento
Editor editor3 = new Editor(delegate { return inputStream; });
// Smaltire le risorse
editor3.Dispose();
System.Console.WriteLine("Document loaded successfully from byte stream.");
```
## Passaggio 4: caricare il documento con le opzioni di caricamento da un flusso di byte
Per i documenti che richiedono una gestione speciale quando caricati da un flusso di byte, è possibile combinare il caricamento del flusso di byte con le opzioni di caricamento.

```csharp
FileStream inputStream = File.OpenRead("Your Sample Document");
// Crea opzioni di caricamento per i fogli di calcolo
SpreadsheetLoadOptions sheetLoadOptions = new SpreadsheetLoadOptions();
sheetLoadOptions.OptimizeMemoryUsage = true;
// Carica il documento come contenuto dal flusso di byte e con le opzioni di caricamento
Editor editor4 = new Editor(delegate { return inputStream; }, delegate { return sheetLoadOptions; });
// Smaltire le risorse
editor4.Dispose();
System.Console.WriteLine("Spreadsheet document loaded successfully with load options.");
```
## Conclusione
Congratulazioni! Hai imparato con successo come caricare documenti utilizzando GroupDocs.Editor per .NET in vari modi. Che tu abbia a che fare con file locali, documenti protetti da password o flussi di byte, GroupDocs.Editor fornisce una soluzione flessibile e potente per le tue esigenze di modifica dei documenti. Ricordati di smaltire sempre le risorse per garantire prestazioni e gestione delle risorse ottimali nelle tue applicazioni.
## Domande frequenti
### Quali formati di file sono supportati da GroupDocs.Editor per .NET?
 GroupDocs.Editor supporta un'ampia gamma di formati di file, inclusi DOCX, XLSX, PPTX, HTML e molti altri. Per un elenco completo, fare riferimento a[documentazione](https://tutorials.groupdocs.com/editor/net/).
### Come gestisco i documenti protetti da password?
 Puoi utilizzare opzioni di caricamento come`WordProcessingLoadOptions` per specificare la password durante il caricamento di documenti protetti da password.
### Posso utilizzare GroupDocs.Editor in un'applicazione web?
Sì, GroupDocs.Editor può essere utilizzato nelle applicazioni web. Assicurati di gestire correttamente i flussi di file e l'eliminazione delle risorse per evitare perdite di memoria.
### Dove posso ottenere una licenza temporanea per GroupDocs.Editor?
 È possibile ottenere una licenza temporanea da[pagina della licenza temporanea](https://purchase.groupdocs.com/temporary-license/).
### È disponibile supporto se riscontro problemi?
 Sì, GroupDocs fornisce supporto tramite il proprio[Forum di assistenza](https://forum.groupdocs.com/c/editor/20).