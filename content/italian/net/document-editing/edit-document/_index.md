---
title: Modifica documento
linktitle: Modifica documento
second_title: API GroupDocs.Editor .NET
description: Impara a modificare i documenti senza sforzo con GroupDocs.Editor per .NET. Guida passo passo per file di elaborazione testi e fogli di calcolo.
weight: 11
url: /it/net/document-editing/edit-document/
---
## introduzione
Ti sei mai trovato intrappolato nella complessità della modifica dei documenti nelle tue applicazioni .NET? Non aver paura! Con GroupDocs.Editor per .NET, hai un potente alleato per semplificare questo compito. Questa guida completa ti spiegherà come sfruttare questo robusto strumento per modificare facilmente i documenti. Che tu abbia a che fare con documenti di elaborazione testi o fogli di calcolo, alla fine di questo tutorial navigherai GroupDocs.Editor come un professionista.
## Prerequisiti
Prima di immergerti nel tutorial, assicurati di avere quanto segue:
- Visual Studio: installato e pronto all'uso.
- .NET Framework: una versione compatibile installata sul sistema.
-  GroupDocs.Editor per .NET: puoi[scaricare l'ultima versione](https://releases.groupdocs.com/editor/net/) e ottenere a[licenza temporanea](https://purchase.groupdocs.com/temporary-license/) se necessario.
- Conoscenza di base di C#: questa guida presuppone una conoscenza di base dello sviluppo C# e .NET.
## Importa spazi dei nomi
Per iniziare, devi importare gli spazi dei nomi necessari nel tuo progetto. Aggiungi le seguenti righe nella parte superiore del file C#:
```csharp
using System.Collections.Generic;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.Options;
```
Ora che è tutto pronto, suddividiamo il processo di modifica del documento in passaggi gestibili.
## Passaggio 1: caricare un documento di elaborazione testi
Innanzitutto, carichiamo un documento di elaborazione testi. Qui è dove indirizzi l'istanza dell'editor alla posizione del tuo documento e specifichi eventuali opzioni di caricamento, se necessario.
### 1.1 Inizializzare l'editor con le opzioni predefinite
```csharp
string inputFilePath = "Your Sample Document"; // Percorso del documento
Editor editor1 = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
```
Questo frammento di codice inizializza l'istanza dell'editor utilizzando le opzioni di caricamento predefinite per un documento di elaborazione testi.
## Passaggio 2: modifica il documento
Ora possiamo procedere con la modifica del documento caricato. GroupDocs.Editor ti consente di personalizzare le opzioni di modifica in base alle tue esigenze.
### 2.1 Modifica con opzioni predefinite
```csharp
EditableDocument defaultWordProcessingDoc = editor1.Edit();
```
La modifica del documento con le opzioni predefinite è semplice e richiede una configurazione minima.
### 2.2 Modifica con opzioni personalizzate
Entriamo nelle configurazioni più avanzate specificando le opzioni di modifica personalizzate.
```csharp
WordProcessingEditOptions wordProcessingEditOptions1 = new WordProcessingEditOptions();
wordProcessingEditOptions1.EnablePagination = false;
wordProcessingEditOptions1.EnableLanguageInformation = true;
wordProcessingEditOptions1.FontExtraction = FontExtractionOptions.ExtractAllEmbedded;
EditableDocument version1WordProcessingDoc = editor1.Edit(wordProcessingEditOptions1);
```
In questo frammento abbiamo disabilitato l'impaginazione, abilitato le informazioni sulla lingua e impostato l'estrazione dei caratteri per estrarre tutti i caratteri incorporati.
### 2.3 Un altro esempio di configurazione
Puoi anche modificare il documento con un diverso set di opzioni:
```csharp
WordProcessingEditOptions wordProcessingEditOptions2 = new WordProcessingEditOptions(true);
wordProcessingEditOptions2.FontExtraction = FontExtractionOptions.ExtractAll;
EditableDocument version2WordProcessingDoc = editor1.Edit(wordProcessingEditOptions2);
```
Qui abbiamo abilitato l'impaginazione e impostato l'estrazione dei caratteri per estrarre tutti i caratteri.
## Passaggio 3: carica e modifica un foglio di calcolo
La modifica dei fogli di calcolo è altrettanto semplice con GroupDocs.Editor.
### 3.1 Caricare il foglio di calcolo
```csharp
Editor editor2 = new Editor("Your Sample Document", delegate { return new SpreadsheetLoadOptions(); });
```
Ciò inizializza un'istanza dell'editor per un documento di foglio di calcolo.
### 3.2 Modifica la prima scheda
```csharp
SpreadsheetEditOptions sheetTab1EditOptions = new SpreadsheetEditOptions();
sheetTab1EditOptions.WorksheetIndex = 0; // L'indice è a base 0, quindi questa è la prima scheda
EditableDocument firstTab = editor2.Edit(sheetTab1EditOptions);
```
Puoi modificare la prima scheda del foglio di calcolo utilizzando le opzioni specificate.
### 3.3 Modifica la seconda scheda
```csharp
SpreadsheetEditOptions sheetTab2EditOptions = new SpreadsheetEditOptions();
sheetTab2EditOptions.WorksheetIndex = 1; // L'indice è in base 0, quindi questa è la seconda scheda
EditableDocument secondTab = editor2.Edit(sheetTab2EditOptions);
```
Allo stesso modo, questo snippet di codice modifica la seconda scheda del foglio di calcolo.
## Passaggio 4: estrazione del contenuto
Una volta modificato il documento, potrebbe essere necessario estrarne il contenuto. GroupDocs.Editor fornisce vari metodi per questo.
### 4.1 Ottieni contenuto HTML
```csharp
string bodyContent = firstTab.GetBodyContent(); // Markup HTML dall'interno dell'elemento HTML->BODY
string allContent = firstTab.GetContent(); // Markup HTML completo di tutto il documento, inclusa l'intestazione HTML->HEAD e il suo contenuto
```
Questo codice estrae il contenuto HTML del documento modificato.
### 4.2 Estrarre risorse
```csharp
List<IImageResource> onlyImages = firstTab.Images;
List<IHtmlResource> allResourcesTogether = firstTab.AllResources;
```
Qui puoi estrarre le immagini e tutte le altre risorse HTML dal documento.
## Passaggio 5: pulizia
Non dimenticare di eliminare tutte le istanze per liberare risorse.
```csharp
defaultWordProcessingDoc.Dispose();
version1WordProcessingDoc.Dispose();
version2WordProcessingDoc.Dispose();
firstTab.Dispose();
secondTab.Dispose();
editor1.Dispose();
editor2.Dispose();
```
Lo smaltimento corretto garantisce che non vi siano perdite di memoria o problemi di prestazioni nell'applicazione.
## Conclusione
 Congratulazioni! Ora hai una conoscenza approfondita di come utilizzare GroupDocs.Editor per .NET per caricare, modificare ed estrarre contenuto da documenti di elaborazione testi e fogli di calcolo. Questo potente strumento semplifica le attività di modifica dei documenti e si integra perfettamente con le tue applicazioni .NET. Per ulteriori dettagli, puoi esplorare il[documentazione](https://tutorials.groupdocs.com/editor/net/), [scaricare l'ultima versione](https://releases.groupdocs.com/editor/net/) o ottenere a[licenza temporanea](https://purchase.groupdocs.com/temporary-license/).
## Domande frequenti
### Posso modificare documenti PDF con GroupDocs.Editor per .NET?
Attualmente GroupDocs.Editor per .NET supporta principalmente i formati di elaborazione testi, fogli di calcolo e presentazioni.
### Come posso gestire in modo efficiente documenti di grandi dimensioni?
Utilizza le opzioni di modifica per caricare ed elaborare solo le parti necessarie del documento e assicurati di eliminare correttamente le istanze per gestire la memoria.
### Esiste un limite alla dimensione del documento che posso modificare?
Non esistono limiti di dimensione rigidi, ma le prestazioni dipendono dalle capacità del tuo sistema.
### Posso personalizzare ulteriormente l'output HTML?
Sì, GroupDocs.Editor consente un'ampia personalizzazione dell'output HTML attraverso varie opzioni e impostazioni.
### Dove posso ottenere supporto se riscontro problemi?
 Puoi visitare il[Forum di supporto GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20) per aiuto e assistenza.