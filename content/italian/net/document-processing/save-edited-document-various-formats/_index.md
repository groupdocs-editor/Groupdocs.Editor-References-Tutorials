---
title: Salva il documento modificato in vari formati
linktitle: Salva il documento modificato in vari formati
second_title: API GroupDocs.Editor .NET
description: Scopri come salvare i documenti modificati in vari formati utilizzando GroupDocs.Editor per .NET in questa guida passo passo completa.
weight: 11
url: /it/net/document-processing/save-edited-document-various-formats/
---

# Salva il documento modificato in vari formati

## introduzione
Stai cercando di salvare i documenti modificati in vari formati utilizzando GroupDocs.Editor per .NET? Sei arrivato nel posto giusto! Questa guida completa ti guiderà attraverso l'intero processo, dalla configurazione del tuo ambiente al salvataggio del documento modificato in più formati. Immergiamoci e rendiamo la modifica e il salvataggio dei documenti un gioco da ragazzi!
## Prerequisiti
Prima di iniziare, assicurati di avere quanto segue:
1.  GroupDocs.Editor per .NET: scarica la versione più recente da[Qui](https://releases.groupdocs.com/editor/net/).
2. Ambiente di sviluppo: Visual Studio o qualsiasi altro IDE compatibile con .NET.
3. .NET Framework: assicurati di avere installato .NET Framework 4.6.1 o versione successiva.
4. Documento di esempio: un documento di elaborazione testi di esempio con cui lavorare.
5. Conoscenza base di C#: è richiesta familiarità con la programmazione C#.
## Importa spazi dei nomi
Per iniziare, assicurati di importare gli spazi dei nomi necessari nel tuo progetto C#. Questo è fondamentale per accedere alla funzionalità GroupDocs.Editor.
```csharp
using System;
using GroupDocs.Editor.Metadata;
```
Suddividiamo il processo in passaggi gestibili. Segui attentamente per assicurarti di comprendere ogni parte.
## Passaggio 1: ottieni un percorso per il file di input
Innanzitutto, devi specificare il percorso del file di elaborazione testi di input. Questo file verrà caricato e modificato.
```csharp
string inputFilePath = "Your Sample Document";
```
## Passaggio 2: creare opzioni di caricamento per il documento
Successivamente, crea opzioni di caricamento specifiche per i documenti di elaborazione testi. Queste opzioni aiuteranno a personalizzare il modo in cui viene caricato il documento.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
```
## Passaggio 3: caricare il documento con le opzioni
 Ora carica il documento in un file`Editor` istanza utilizzando le opzioni di caricamento specificate.
```csharp
using (Editor editor = new Editor(inputFilePath, delegate { return loadOptions; }))
```
## Passaggio 4: crea opzioni di modifica
Preparare le opzioni di modifica per il documento. Queste opzioni determineranno la modalità di apertura del documento per la modifica.
```csharp
WordProcessingEditOptions editOptions = new WordProcessingEditOptions();
```
## Passaggio 5: aprire il documento per la modifica
 Apri il documento per la modifica creando un file`EditableDocument`esempio. Questa istanza ti consentirà di apportare modifiche al documento.
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
```
## Passaggio 6: modifica il contenuto del documento
Ora è il momento di modificare il contenuto del documento. Innanzitutto, ottieni il documento come una singola stringa con codifica base64.
```csharp
string allEmbeddedInsideString = beforeEdit.GetEmbeddedHtml();
```
Ad esempio, modifichiamo il sottotitolo nel documento.
```csharp
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
```
## Passaggio 7: crea un nuovo documento modificabile dal contenuto modificato
 Creane uno nuovo`EditableDocument` istanza dal contenuto e dalle risorse modificati.
```csharp
using (EditableDocument afterEdit = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null))
```
## Passaggio 8: salva il documento in vari formati
Infine, esegui l'iterazione su tutti i formati di elaborazione testi supportati e salva il documento modificato in ciascun formato.
```csharp
foreach (WordProcessingFormats oneFormat in WordProcessingFormats.All)
{
    // Preparare le opzioni di salvataggio
    WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(oneFormat);
    // Preparare il percorso di salvataggio
    string savePath = Path.Combine("OutputDirectory", "MultipleOutFormats." + saveOptions.OutputFormat.Extension);
    // Salva il documento
    editor.Save(afterEdit, savePath, saveOptions);
}
```
## Messaggio di completamento
Per concludere è possibile stampare un messaggio che indica che il processo è terminato con successo.
```csharp
Console.WriteLine("SavingEditedDocumentToAllFormats routine has successfully finished");
```
## Conclusione
Congratulazioni! Hai imparato con successo come salvare i documenti modificati in vari formati utilizzando GroupDocs.Editor per .NET. Questo potente strumento semplifica la manipolazione e il salvataggio di documenti in più formati con solo poche righe di codice. Ricorda, i passaggi chiave riguardano il caricamento del documento, la modifica del contenuto e il salvataggio nei formati desiderati.
## Domande frequenti
### Cos'è GroupDocs.Editor per .NET?
GroupDocs.Editor per .NET è una potente API che ti consente di modificare documenti in vari formati utilizzando applicazioni .NET.
### Posso utilizzare GroupDocs.Editor gratuitamente?
 Sì, puoi usarlo con una prova gratuita. Scaricalo[Qui](https://releases.groupdocs.com/).
### Quali formati sono supportati da GroupDocs.Editor?
GroupDocs.Editor supporta un'ampia gamma di formati, inclusi DOCX, PDF, HTML e molti altri.
### Come posso ottenere una licenza temporanea per GroupDocs.Editor?
 È possibile ottenere una licenza temporanea[Qui](https://purchase.groupdocs.com/temporary-license/).
### Dove posso trovare ulteriore documentazione e supporto?
 È disponibile la documentazione dettagliata[Qui](https://tutorials.groupdocs.com/editor/net/) e puoi ottenere supporto[Qui](https://forum.groupdocs.com/c/editor/20).