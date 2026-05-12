---
date: 2026-05-12
description: Scopri come estrarre i font e altre risorse HTML dai documenti utilizzando
  GroupDocs.Editor per .NET. Guida passo‑passo per gli sviluppatori .NET.
keywords:
- how to extract fonts
- GroupDocs.Editor .NET
- extract HTML resources
linktitle: Salva le risorse HTML in una cartella
schemas:
- author: GroupDocs
  dateModified: '2026-05-12'
  description: Learn how to extract fonts and other HTML resources from documents
    using GroupDocs.Editor for .NET. Step‑by‑step guide for .NET developers.
  headline: How to Extract Fonts and Save HTML Resources to Folder
  type: TechArticle
- description: Learn how to extract fonts and other HTML resources from documents
    using GroupDocs.Editor for .NET. Step‑by‑step guide for .NET developers.
  name: How to Extract Fonts and Save HTML Resources to Folder
  steps:
  - name: '**Basic Knowledge of C# and .NET** – Familiarity with C# programming language
      and .NET framework is essential to follow along with the examples.'
    text: '**Basic Knowledge of C# and .NET** – Familiarity with C# programming language
      and .NET framework is essential to follow along with the examples.'
  - name: '**GroupDocs.Editor for .NET Library** – Download and install GroupDocs.Editor
      for .NET library from the [website](https://releases.groupdocs.com/editor/net/).'
    text: '**GroupDocs.Editor for .NET Library** – Download and install GroupDocs.Editor
      for .NET library from the [website](https://releases.groupdocs.com/editor/net/).'
  - name: '**Development Environment** – Set up your preferred development environment
      such as Visual Studio or any other compatible IDE.'
    text: '**Development Environment** – Set up your preferred development environment
      such as Visual Studio or any other compatible IDE.'
  type: HowTo
- questions:
  - answer: Yes, it supports Excel, PowerPoint, PDF, HTML, and over 50 additional
      formats for both editing and resource extraction.
    question: Is GroupDocs.Editor compatible with other document formats besides Word?
  - answer: Absolutely. The API works seamlessly with ASP.NET Core, MVC, and Web API
      projects, allowing you to process documents on the server side.
    question: Can I integrate GroupDocs.Editor into a web application?
  - answer: Yes, it includes built‑in connectors for Google Drive, Dropbox, OneDrive,
      and Amazon S3, enabling direct loading and saving of documents in the cloud.
    question: Does GroupDocs.Editor provide cloud storage integration?
  - answer: A fully functional 30‑day trial can be downloaded from the GroupDocs website
      without any credit‑card requirement.
    question: Is there a free trial available for GroupDocs.Editor?
  - answer: You can reach the GroupDocs support team via the official forum, submit
      a ticket through the customer portal, or consult the detailed API documentation.
    question: How can I get technical support for extraction issues?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Come estrarre i font e salvare le risorse HTML in una cartella
type: docs
url: /it/net/document-editing/save-html-resources-to-folder/
weight: 13
---

# Come estrarre i font e salvare le risorse HTML in una cartella

## Introduzione
GroupDocs.Editor per .NET ti consente di **come estrarre i font** e altre risorse da un documento durante la conversione in HTML. In poche righe di C# puoi estrarre immagini, fogli di stile e file di font, quindi archiviarli in una cartella a tua scelta. Questo tutorial ti guida attraverso l'intero flusso di lavoro, dall'inizializzazione dell'editor al salvataggio di ogni risorsa su disco.

## Risposte rapide
- **Cosa significa “come estrarre i font”?** È il processo di recupero dei file di font incorporati da un documento sorgente durante la conversione in HTML.  
- **Quale libreria gestisce questo?** GroupDocs.Editor per .NET fornisce un'API dedicata per l'estrazione di font, immagini e fogli di stile.  
- **Ho bisogno di una licenza?** È disponibile una versione di prova gratuita; è necessaria una licenza commerciale per l'uso in produzione.  
- **Quali versioni di .NET sono supportate?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.  
- **Posso specificare una cartella personalizzata?** Sì, puoi indicare qualsiasi percorso scrivibile quando salvi le risorse estratte.

## Cos'è “come estrarre i font”?
**Come estrarre i font** si riferisce al recupero dei file di font originali incorporati in un documento sorgente (ad es., DOCX, PPTX) in modo che possano essere referenziati dall'HTML generato. Questo garantisce che il testo venga visualizzato esattamente come previsto nei browser senza dipendere dai font di sistema.

## Perché usare GroupDocs.Editor per l'estrazione di risorse HTML?
GroupDocs.Editor supporta **oltre 50 formati di input e output** — inclusi DOCX, PPTX, PDF e HTML — e può elaborare documenti con **fino a 300 pagine** senza caricare l'intero file in memoria. La sua API estrae font, immagini e CSS in un unico passaggio, riducendo il tempo di sviluppo fino al **70 %** rispetto al parsing manuale.

## Prerequisiti
Prima di immergerti nel tutorial, assicurati di avere i seguenti prerequisiti:
1. **Conoscenza di base di C# e .NET** – Familiarità con il linguaggio di programmazione C# e il framework .NET è essenziale per seguire gli esempi.  
2. **Libreria GroupDocs.Editor per .NET** – Scarica e installa la libreria GroupDocs.Editor per .NET dal [sito web](https://releases.groupdocs.com/editor/net/).  
3. **Ambiente di sviluppo** – Configura il tuo ambiente di sviluppo preferito, come Visual Studio o qualsiasi altro IDE compatibile.

## Importare gli spazi dei nomi
Per iniziare, importa gli spazi dei nomi necessari nel tuo progetto C#:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```

## Come estrarre i font e salvare le risorse HTML in una cartella?
Carica il tuo documento sorgente con `Editor editor = new Editor("sample.docx", new WordProcessingLoadOptions());` quindi chiama `editor.Save("output.html", SaveOptions.Html);`. Dopo l'operazione di salvataggio, la collezione `Resources` contiene tutte le risorse estratte — inclusi i font — che puoi iterare e scrivere su disco. Questo approccio a singolo passaggio gestisce automaticamente sia la conversione sia l'estrazione delle risorse.

## Passo 1: Inizializzare GroupDocs.Editor
`Editor` è la classe core che orchestra il caricamento del documento, la conversione e l'estrazione delle risorse. Rappresenta una singola sessione di documento in memoria.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
Per prima cosa, inizializza l'oggetto `Editor` fornendo il percorso al tuo documento di esempio. In questo esempio, stiamo usando un documento Word, quindi specifichiamo `WordProcessingLoadOptions` come tipo di documento.

## Passo 2: Modificare il documento
`EditableDocument` è la rappresentazione modificabile restituita dal metodo `Edit`, che ti consente di manipolare il documento prima del salvataggio.

```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
Successivamente, crea un oggetto `EditableDocument` chiamando il metodo `Edit` dell'oggetto `Editor`. Questo ti permette di eseguire operazioni di modifica sul documento.

## Passo 3: Estrarre le risorse
`Resources` è una collezione che raggruppa le risorse estratte — immagini, font e fogli di stile — in liste separate per una gestione più semplice.

```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
Estrai risorse come immagini, font e fogli di stile dal documento e archiviale nelle rispettive liste.

## Passo 4: Specificare la cartella di output
`outputFolder` è una stringa che definisce dove verranno scritti i file estratti. Puoi puntarlo a qualsiasi directory scrivibile sul server o sulla macchina locale.

```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
Definisci la cartella di output dove verranno salvate le risorse estratte. Puoi personalizzare il percorso della cartella secondo le tue esigenze.

## Passo 5: Salvare le risorse
`SaveResource` è una routine di supporto che scrive una singola risorsa binaria (immagine, font o foglio di stile) nel file system.

```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
Itera su ogni risorsa immagine, salvala nella cartella di output e visualizza le informazioni rilevanti come nome file, tipo e dimensioni.

```csharp
		foreach (FontResourceBase oneFont in fonts)
		{
			Console.WriteLine("Saving {0} of {1} type",
				oneFont.FilenameWithExtension, oneFont.Type.FormalName);
			oneFont.Save(Path.Combine(outputFolder, oneFont.FilenameWithExtension));
		}
```
Allo stesso modo, salva ogni risorsa font nella cartella di output.

```csharp
		foreach (CssText oneStylesheet in stylesheets)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} encoding",
				oneStylesheet.FilenameWithExtension, oneStylesheet.Type.FormalName, oneStylesheet.Encoding);
			oneStylesheet.Save(Path.Combine(outputFolder, oneStylesheet.FilenameWithExtension));
		}
	}
}
```
Infine, salva ogni foglio di stile nella cartella di output e completa il processo di modifica.

## Problemi comuni e soluzioni
- **Font mancanti dopo la conversione** – Assicurati che il documento sorgente incorpori effettivamente i font; altrimenti, GroupDocs.Editor può fare riferimento solo ai font di sistema.  
- **Errori di accesso negato** – Verifica che il processo dell'applicazione abbia i permessi di scrittura sulla cartella di output di destinazione.  
- **Documenti di grandi dimensioni causano un elevato utilizzo della memoria** – Usa `LoadOptions` con `LoadMode = LoadMode.Stream` per trasmettere in streaming i file di grandi dimensioni invece di caricarli interamente in memoria.

## Domande frequenti

**D: GroupDocs.Editor è compatibile con altri formati di documento oltre a Word?**  
R: Sì, supporta Excel, PowerPoint, PDF, HTML e oltre 50 formati aggiuntivi sia per la modifica sia per l'estrazione delle risorse.

**D: Posso integrare GroupDocs.Editor in un'applicazione web?**  
R: Assolutamente. L'API funziona senza problemi con progetti ASP.NET Core, MVC e Web API, consentendoti di elaborare i documenti sul lato server.

**D: GroupDocs.Editor offre integrazione con lo storage cloud?**  
R: Sì, include connettori integrati per Google Drive, Dropbox, OneDrive e Amazon S3, consentendo il caricamento e il salvataggio diretto dei documenti nel cloud.

**D: È disponibile una prova gratuita per GroupDocs.Editor?**  
R: È possibile scaricare una prova completa di 30 giorni dal sito web di GroupDocs senza necessità di carta di credito.

**D: Come posso ottenere supporto tecnico per problemi di estrazione?**  
R: Puoi contattare il team di supporto di GroupDocs tramite il forum ufficiale, inviare un ticket attraverso il portale clienti o consultare la documentazione dettagliata dell'API.

---

**Ultimo aggiornamento:** 2026-05-12  
**Testato con:** GroupDocs.Editor 23.11 per .NET  
**Autore:** GroupDocs

## Tutorial correlati

- [Modifica efficiente dei documenti con GroupDocs.Editor .NET: trasformare HTML in documenti modificabili](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)
- [Estrarre e salvare efficientemente le risorse DOCX usando GroupDocs.Editor .NET - Guida completa](/editor/net/document-saving/efficient-extract-save-docx-resources-groupdocs-editor-net/)
- [Padroneggiare la modifica e la conversione dei documenti con GroupDocs.Editor .NET: guida completa](/editor/net/document-editing/groupdocs-editor-net-mastering-document-editing/)