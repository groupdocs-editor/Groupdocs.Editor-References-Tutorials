---
title: Salva documento
linktitle: Salva documento
second_title: API GroupDocs.Editor .NET
description: Modifica e salva facilmente i documenti utilizzando GroupDocs.Editor per .NET. Questa guida passo passo semplifica il processo per gli sviluppatori.
weight: 14
url: /it/net/document-editing/save-document/
type: docs
---
# Salva documento

## introduzione
Stai cercando di modificare e salvare facilmente documenti utilizzando GroupDocs.Editor per .NET? Sei nel posto giusto! Questo tutorial ti guiderà attraverso il processo passo dopo passo, assicurandoti di poter gestire facilmente i tuoi documenti. Che tu sia uno sviluppatore esperto o un principiante, la nostra guida ti fornirà tutte le informazioni necessarie per iniziare.
## Prerequisiti
Prima di immergerti nel tutorial, assicurati di avere i seguenti prerequisiti:
- Ambiente di sviluppo: Visual Studio installato sul tuo computer.
- .NET Framework: assicurati di avere .NET Framework 4.6.1 o versione successiva.
-  GroupDocs.Editor per .NET: scarica la versione più recente[Qui](https://releases.groupdocs.com/editor/net/).
- Conoscenza di base del C#: la familiarità con la programmazione C# è essenziale.
## Importa spazi dei nomi
Per utilizzare GroupDocs.Editor nel tuo progetto .NET, devi importare gli spazi dei nomi necessari. Ecco come farlo:
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
Ora che abbiamo configurato il nostro ambiente e importati gli spazi dei nomi necessari, analizziamo i passaggi necessari per caricare, modificare e salvare un documento utilizzando GroupDocs.Editor per .NET.
## Passaggio 1: caricare il documento
Per prima cosa dobbiamo caricare il documento che vogliamo modificare. GroupDocs.Editor rende questo processo semplice. Ecco come puoi farlo:

```csharp
string inputFilePath = "Your Sample Document";
Editor editor = new Editor(inputFilePath, delegate { return new Options.WordProcessingLoadOptions(); });
EditableDocument defaultWordProcessingDoc = editor.Edit();
```
 In questo passaggio specifichiamo il percorso del documento che vogliamo modificare e creiamo un'istanza del file`Editor` classe. IL`Edit` viene quindi chiamato il metodo per caricare il documento in un file`EditableDocument` oggetto.
## Passaggio 2: modifica il documento
Con il documento caricato, è il momento di apportare alcune modifiche. Poiché non abbiamo un editor WYSIWYG collegato, simuleremo il processo di modifica nel codice.

```csharp
string allEmbeddedInsideString = defaultWordProcessingDoc.GetEmbeddedHtml();
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
EditableDocument editedDoc = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```
 Qui recuperiamo il contenuto HTML incorporato del documento, eseguiamo una semplice sostituzione del testo e ne creiamo uno nuovo`EditableDocument`istanza dall'HTML modificato.
## Passaggio 3: salva il documento
Dopo aver modificato il documento, il passaggio finale è salvarlo. GroupDocs.Editor fornisce più opzioni per salvare il documento in diversi formati.
## Salva come RTF
```csharp
string outputRtfPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.rtf");
WordProcessingSaveOptions rtfSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
editor.Save(editedDoc, outputRtfPath, rtfSaveOptions);
```
## Salva come DOCM
```csharp
string outputDocmPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.docm");
WordProcessingSaveOptions docmSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm);
using (FileStream outputStream = File.Create(outputDocmPath))
{
    editor.Save(editedDoc, outputStream, docmSaveOptions);
}
```
## Salva come testo normale
```csharp
string outputTxtPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.txt");
TextSaveOptions textSaveOptions = new TextSaveOptions
{
    Encoding = System.Text.Encoding.UTF8,
    PreserveTableLayout = true
};
editor.Save(editedDoc, outputTxtPath, textSaveOptions);
```
## Passaggio 4: pulizia
 Infine, è fondamentale smaltire il`EditableDocument` E`Editor` istanze per liberare risorse.
```csharp
editedDoc.Dispose();
defaultWordProcessingDoc.Dispose();
editor.Dispose();
```
Seguendo questi passaggi, puoi caricare, modificare e salvare in modo efficiente i documenti utilizzando GroupDocs.Editor per .NET. Questo potente strumento offre flessibilità e facilità d'uso, rendendo la gestione dei documenti un gioco da ragazzi.
## Conclusione
Modificare e salvare documenti a livello di codice non è mai stato così semplice con GroupDocs.Editor per .NET. Questa guida ti ha guidato attraverso l'intero processo, dal caricamento di un documento al salvataggio in vari formati. Con GroupDocs.Editor hai una soluzione versatile e solida a portata di mano, che semplifica il processo di modifica dei documenti.
## Domande frequenti
### Quali formati di file supporta GroupDocs.Editor?
GroupDocs.Editor supporta vari formati di file, inclusi DOCX, RTF, TXT e molti altri. Per un elenco completo, consulta il[documentazione](https://tutorials.groupdocs.com/editor/net/).
### Posso provare GroupDocs.Editor prima dell'acquisto?
 Sì, puoi ottenere un[prova gratuita](https://releases.groupdocs.com/) per testare le funzionalità di GroupDocs.Editor.
### È disponibile supporto in caso di problemi?
 Assolutamente! Puoi visitare il[Forum di assistenza](https://forum.groupdocs.com/c/editor/20) per assistenza in caso di problemi riscontrati.
### Come posso ottenere una licenza temporanea?
 Puoi richiedere un[licenza temporanea](https://purchase.groupdocs.com/temporary-license/) a fini di valutazione.
### Dove posso acquistare la versione completa di GroupDocs.Editor?
 Puoi acquistare la versione completa[Qui](https://purchase.groupdocs.com/buy).