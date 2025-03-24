---
title: Lavora con documenti di solo testo
linktitle: Lavora con documenti di solo testo
second_title: API GroupDocs.Editor .NET
description: Impara a modificare documenti di testo semplice utilizzando GroupDocs.Editor per .NET con la nostra guida passo passo. Semplifica il processo di modifica dei documenti .NET.
weight: 15
url: /it/net/document-processing/work-plain-text-documents/
---

# Lavora con documenti di solo testo

## introduzione
Stai cercando di semplificare il processo di modifica dei documenti in .NET? Non cercare oltre GroupDocs.Editor per .NET! Questa potente API ti consente di modificare facilmente un'ampia varietà di formati di documenti. In questo tutorial ti guideremo attraverso il processo di lavoro con documenti di testo semplice utilizzando GroupDocs.Editor per .NET. Alla fine, sarai in grado di gestire la modifica dei documenti di testo come un professionista. Pronti a tuffarvi? Iniziamo!
## Prerequisiti
Prima di iniziare, ci sono alcune cose che dovrai avere a posto:
- Ambiente di sviluppo .NET: assicurati di avere configurato un ambiente di sviluppo .NET funzionante. Visual Studio è una scelta popolare.
-  GroupDocs.Editor per .NET: scarica e installa il file[GroupDocs.Editor per .NET](https://releases.groupdocs.com/editor/net/).
- Conoscenza di base di C#: la familiarità con il linguaggio di programmazione C# ti aiuterà a seguire gli esempi.
- Editor di testo: va bene qualsiasi editor di testo, anche se Visual Studio Code è consigliato per le sue funzionalità e facilità d'uso.
## Importa spazi dei nomi
Per iniziare a utilizzare GroupDocs.Editor per .NET, devi importare gli spazi dei nomi necessari nel tuo progetto. Ciò garantisce che tutte le classi e i metodi richiesti siano disponibili per l'uso.
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```
Suddividiamo il processo in passaggi gestibili. Seguici mentre ti guidiamo attraverso ogni fase della modifica di documenti di testo normale utilizzando GroupDocs.Editor per .NET.
## Passaggio 1: ottieni un percorso per il file TXT di input
Innanzitutto, è necessario specificare il percorso del file TXT di input. Può trattarsi del percorso di un file locale o di un flusso contenente il contenuto del file.
```csharp
string inputFilePath = "YourSampleDocument.txt";
```
## Passaggio 2: crea un'istanza dell'editor
 Successivamente, crea un'istanza di`Editor` classe. Questa classe è responsabile del caricamento e della modifica dei documenti. In questa fase non sono richieste opzioni di caricamento.
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## Passaggio 3: crea opzioni di modifica TXT
Ora crea le opzioni di modifica TXT. Queste opzioni consentono di specificare come deve essere elaborato il contenuto testuale durante la modifica.
```csharp
    TextEditOptions editOptions = new TextEditOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        RecognizeLists = true,
        LeadingSpaces = TextLeadingSpacesOptions.ConvertToIndent,
        TrailingSpaces = TextTrailingSpacesOptions.Trim
    };
```
## Passaggio 4: crea un'istanza di documento modificabile
 Con le opzioni di modifica impostate, crea un file`EditableDocument` esempio. Questo rappresenta il documento in un formato modificabile.
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## Passaggio 5: modifica il contenuto del documento
Recupera il contenuto del testo originale e apporta le modifiche desiderate. Per questo esempio, sostituiremo la parola "testo" con "testo EDITATO".
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("text", "EDITED text");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## Passaggio 6: crea un documento modificabile con contenuto aggiornato
 Dopo aver apportato le modifiche necessarie, creane uno nuovo`EditableDocument` con il contenuto aggiornato e le risorse originali.
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## Passaggio 7: crea le opzioni di salvataggio dell'elaborazione testi
Preparare le opzioni di salvataggio per il formato di elaborazione testi. Questo esempio utilizza il formato DOCM e specifica la locale.
```csharp
    WordProcessingSaveOptions wordSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm)
    {
        Locale = System.Globalization.CultureInfo.GetCultureInfo("en-GB")
    };
```
## Passaggio 8: crea opzioni di salvataggio TXT
Allo stesso modo, crea le opzioni di salvataggio per il formato TXT. Assicurati che la codifica sia impostata su UTF-8 e preserva il layout della tabella.
```csharp
    TextSaveOptions txtSaveOptions = new TextSaveOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        PreserveTableLayout = true
    };
```
## Passaggio 9: preparare i percorsi di output
Preparare i percorsi per il salvataggio dei file DOCX e TXT risultanti. Utilizzare il percorso del file di input per determinare la directory di output e i nomi dei file.
```csharp
    string outputWordPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".docm");
    string outputTxtPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".txt");
```
## Passaggio 10: salva il documento modificato
Infine, salva il documento modificato in entrambi i formati DOCX e TXT utilizzando le opzioni di salvataggio specificate.
```csharp
    editor.Save(afterEdit, outputWordPath, wordSaveOptions);
    editor.Save(afterEdit, outputTxtPath, txtSaveOptions);
}
System.Console.WriteLine("Document editing process completed successfully!");
```
## Conclusione
 Congratulazioni! Hai modificato con successo un documento di testo normale utilizzando GroupDocs.Editor per .NET. Questo potente strumento semplifica la modifica dei documenti, facilitandone l'integrazione nelle applicazioni .NET. Che tu stia gestendo semplici file di testo o formati di documenti complessi, GroupDocs.Editor è quello che fa per te. Esplora ulteriori funzionalità e capacità visitando il[Documentazione di GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/).
## Domande frequenti
### Quali formati di file supporta GroupDocs.Editor per .NET?
 GroupDocs.Editor per .NET supporta un'ampia gamma di formati di file, inclusi DOCX, TXT, HTML e altri. Controlla il[documentazione](https://tutorials.groupdocs.com/editor/net/) per un elenco completo.
### Come posso ottenere una prova gratuita di GroupDocs.Editor per .NET?
 È possibile scaricare una versione di prova gratuita di GroupDocs.Editor per .NET dal sito[pagina delle uscite](https://releases.groupdocs.com/).
### Posso acquistare una licenza temporanea per GroupDocs.Editor per .NET?
Sì, puoi ottenere una licenza temporanea da[Pagina di acquisto di GroupDocs](https://purchase.groupdocs.com/temporary-license/).
### Dove posso ottenere supporto per GroupDocs.Editor per .NET?
 Il supporto è disponibile tramite il[Forum di supporto GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).
### È disponibile una documentazione dettagliata per GroupDocs.Editor per .NET?
 Sì, la documentazione dettagliata è disponibile sul[Pagina della documentazione di GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/).