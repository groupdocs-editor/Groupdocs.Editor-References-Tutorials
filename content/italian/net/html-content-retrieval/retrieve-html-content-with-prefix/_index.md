---
title: Recupera contenuto HTML con prefisso
linktitle: Recupera contenuto HTML con prefisso
second_title: API GroupDocs.Editor .NET
description: Scopri come recuperare contenuto HTML dai documenti utilizzando GroupDocs.Editor per .NET con prefissi personalizzati per immagini e fogli di stile. Guida passo passo inclusa.
weight: 11
url: /it/net/html-content-retrieval/retrieve-html-content-with-prefix/
type: docs
---
# Recupera contenuto HTML con prefisso

## introduzione
Benvenuto nel nostro tutorial passo passo su come recuperare contenuto HTML da un documento utilizzando GroupDocs.Editor per .NET. Che tu sia uno sviluppatore esperto o che tu abbia appena iniziato, questa guida ti guiderà attraverso il processo in modo facile da seguire. Tratteremo tutto ciò che devi sapere, dalla configurazione del tuo ambiente all'esecuzione corretta del codice. Immergiamoci!
## Prerequisiti
Prima di iniziare, assicurati di disporre dei seguenti prerequisiti:
1.  GroupDocs.Editor per .NET: scarica la versione più recente da[pagina di download](https://releases.groupdocs.com/editor/net/).
2. Ambiente di sviluppo: Visual Studio o qualsiasi altro ambiente di sviluppo .NET preferito.
3. Conoscenza di base di C#: la familiarità con la programmazione C# ti aiuterà a seguire gli esempi.
4. Documento da modificare: tieni pronto un documento di esempio per il test, ad esempio un documento Word.
5. .NET Framework: assicurati di avere .NET Framework installato sul tuo computer.
Ora che hai tutto pronto, cominciamo!
## Importa spazi dei nomi
Innanzitutto, devi importare gli spazi dei nomi necessari nel tuo progetto C#. Questi spazi dei nomi forniscono le classi e i metodi necessari per lavorare con GroupDocs.Editor per .NET.
```csharp
using System;
using GroupDocs.Editor.Options;
```
Una volta importati gli spazi dei nomi, possiamo passare alla configurazione dell'editor.
## Passaggio 1: inizializzare l'editor
 Per iniziare è necessario inizializzare il file`Editor`classe con il tuo documento. Questo passaggio prevede la specifica del documento che desideri modificare e la fornitura delle opzioni di caricamento necessarie.
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
    // Ulteriori passaggi verranno aggiunti qui
}
```
 In questo esempio stiamo caricando un documento Word. Puoi sostituire`"Your Sample Document"` con il percorso del documento.
## Passaggio 2: modifica il documento
 Successivamente, dobbiamo aprire il documento per la modifica. Questo viene fatto utilizzando il`Edit` metodo del`Editor` classe, che richiede`WordProcessingEditOptions` come argomento.
```csharp
using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
{
    // Ulteriori passaggi verranno aggiunti qui
}
```
 IL`EditableDocument` L'istanza rappresenta il documento in un formato modificabile. Ora siamo pronti per recuperare il contenuto HTML.
## Passaggio 3: definire i prefissi personalizzati
Per aggiungere prefissi personalizzati per immagini e CSS, dobbiamo definire i prefissi come stringhe. Questo passaggio garantisce che il contenuto HTML avrà i prefissi specificati per le risorse esterne.
```csharp
string externalImagesPrefix = "http://www.ilmiosito.com/images/id=";
string externalCssPrefix = "http://www.ilmiosito.com/css/id=";
```
Puoi sostituire gli URL con i prefissi desiderati. Questi prefissi verranno utilizzati nel passaggio successivo per personalizzare l'output HTML.
## Passaggio 4: recupera il contenuto HTML
Ora che abbiamo impostato i nostri prefissi, possiamo recuperare il contenuto HTML dal documento. IL`GetContent` metodo del`EditableDocument` class ci consente di specificare l'immagine e i prefissi CSS.
```csharp
string prefixedHtmlContent = document.GetContent(externalImagesPrefix, externalCssPrefix);
Console.WriteLine("HTML content of the input document with custom image and stylesheet prefixes: {0}", prefixedHtmlContent);
```
Questo frammento di codice recupera il contenuto HTML con i prefissi personalizzati e lo stampa sulla console. È possibile elaborare o salvare ulteriormente questo contenuto HTML secondo necessità.
## Conclusione
E il gioco è fatto! Seguendo questi passaggi, puoi recuperare facilmente il contenuto HTML da un documento utilizzando GroupDocs.Editor per .NET, completo di prefissi personalizzati per immagini e fogli di stile. Questo potente strumento semplifica la manipolazione dei documenti, consentendoti di concentrarti sull'integrazione perfetta della modifica dei documenti nelle tue applicazioni .NET.
 Per informazioni più dettagliate, consultare il[GroupDocs.Editor per la documentazione .NET](https://tutorials.groupdocs.com/editor/net/) . Se hai domande o hai bisogno di ulteriore assistenza, non esitare a contattare il[Forum di assistenza](https://forum.groupdocs.com/c/editor/20).
## Domande frequenti
### Quali tipi di documenti posso modificare con GroupDocs.Editor per .NET?
GroupDocs.Editor supporta vari formati di documenti tra cui Word, Excel, PowerPoint, PDF e altri.
### Come posso ottenere una prova gratuita di GroupDocs.Editor per .NET?
 Puoi ottenere una prova gratuita da[Sito web di GroupDocs](https://releases.groupdocs.com/).
### Posso personalizzare ulteriormente il contenuto HTML?
Sì, puoi modificare il contenuto HTML recuperato secondo necessità prima di visualizzarlo o salvarlo.
### È possibile utilizzare GroupDocs.Editor per .NET con altri linguaggi .NET?
Sì, puoi usarlo con qualsiasi linguaggio compatibile con .NET come VB.NET o F#.
### Come posso ottenere una licenza temporanea per GroupDocs.Editor per .NET?
 Puoi ottenere una licenza temporanea da[pagina di acquisto](https://purchase.groupdocs.com/temporary-license/).