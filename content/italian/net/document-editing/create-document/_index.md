---
title: Crea documento
linktitle: Crea documento
second_title: API GroupDocs.Editor .NET
description: Scopri come modificare documenti Word, Excel, PowerPoint, Ebook ed e-mail utilizzando GroupDocs.Editor per .NET con questo tutorial completo passo passo.
weight: 10
url: /it/net/document-editing/create-document/
type: docs
---
# Crea documento

## introduzione
Sei stanco dei problemi che derivano dalla modifica programmatica di diversi tipi di documenti? GroupDocs.Editor per .NET è qui per semplificare il processo. Questo potente strumento consente agli sviluppatori di modificare facilmente vari formati di documenti come Word, Excel, PowerPoint, Ebook ed e-mail. In questo tutorial, approfondiremo come utilizzare GroupDocs.Editor per .NET per creare e modificare documenti. Suddivideremo il processo in passaggi facili da seguire, rendendolo accessibile anche se sei nuovo a questo.
## Prerequisiti
Prima di iniziare, assicurati di avere quanto segue:
- Visual Studio installato sul tuo computer.
- .NET Framework (4.0 o versione successiva).
-  GroupDocs.Editor per la libreria .NET. Puoi scaricarlo da[Qui](https://releases.groupdocs.com/editor/net/).
- Conoscenza base della programmazione C#.
## Importa spazi dei nomi
Per prima cosa importiamo gli spazi dei nomi necessari. Ciò renderà accessibili le classi e i metodi richiesti nella nostra applicazione.
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using System.IO;
```
## Passaggio 1: configurazione dello streaming
Per cominciare, dobbiamo impostare un flusso di memoria che fungerà da segnaposto per il contenuto del documento.
```csharp
Stream memoryStream = Stream.Null;
```
## Passaggio 2: funzione di richiamata per salvare il documento
Successivamente, definisci una funzione di callback che salverà il nuovo flusso di documenti. Questa funzione è essenziale per gestire l'output del processo di modifica del documento.
```csharp
void SaveNewDocument(Stream resultStream)
{
    memoryStream = resultStream;
}
```
## Passaggio 3: creazione e modifica di un documento di elaborazione testi
 Ora creiamo e modifichiamo un documento Word. Inizieremo creandone uno nuovo`Editor` istanza per i documenti di elaborazione testi e modificarla con le opzioni predefinite.
### Crea e modifica con le opzioni predefinite
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    EditableDocument defaultWordProcessingDoc = editor.Edit();
}
```
### Crea e modifica con opzioni personalizzate
Per un maggiore controllo, possiamo specificare opzioni come disabilitare l'impaginazione ed estrarre i caratteri incorporati.
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    WordProcessingEditOptions wordProcessingEditOptions = new WordProcessingEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true,
        FontExtraction = FontExtractionOptions.ExtractAllEmbedded
    };
    EditableDocument editableWordProcessingDocument = editor.Edit(wordProcessingEditOptions);
}
```
## Passaggio 4: creazione e modifica di un documento di foglio di calcolo
Allo stesso modo, possiamo creare e modificare un documento Excel. Ecco come farlo.
### Crea e modifica con le opzioni predefinite
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    EditableDocument defaultEditableSpreadsheetDocument = editor.Edit();
}
```
### Crea e modifica con opzioni personalizzate
 Per indirizzare fogli di lavoro specifici o escludere quelli nascosti, utilizziamo`SpreadsheetEditOptions`.
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    SpreadsheetEditOptions spreadsheetEditOptions = new SpreadsheetEditOptions
    {
        WorksheetIndex = 0,
        ExcludeHiddenWorksheets = true
    };
    EditableDocument editableSpreadsheetDocument = editor.Edit(spreadsheetEditOptions);
}
```
## Passaggio 5: creazione e modifica di un documento di presentazione
Sono supportate anche le presentazioni PowerPoint. Vediamo come gestirli.
### Crea e modifica con le opzioni predefinite
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    EditableDocument defaultEditablePresentationDocument = editor.Edit();
}
```
### Crea e modifica con opzioni personalizzate
Puoi personalizzare le tue modifiche specificando opzioni come quale diapositiva mostrare e se includere le diapositive nascoste.
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    PresentationEditOptions presentationEditOptions = new PresentationEditOptions
    {
        ShowHiddenSlides = false,
        SlideNumber = 0
    };
    EditableDocument editablePresentationDocument = editor.Edit(presentationEditOptions);
}
```
## Passaggio 6: creazione e modifica di un documento ebook
GroupDocs.Editor consente anche di modificare formati di ebook come EPUB. Ecco come puoi gestirlo.
### Crea e modifica con le opzioni predefinite
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EditableDocument defaultEditableEbookDocument = editor.Edit();
}
```
### Crea e modifica con opzioni personalizzate
Personalizza la modifica del tuo ebook abilitando o disabilitando l'impaginazione e le informazioni sulla lingua.
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EbookEditOptions ebookEditOptions = new EbookEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true
    };
    EditableDocument editableEbookDocument = editor.Edit(ebookEditOptions);
}
```
## Passaggio 7: creazione e modifica di un documento e-mail
Infine, vedremo come modificare i documenti di posta elettronica. Ciò include formati come EML.
### Crea e modifica con le opzioni predefinite
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EditableDocument defaultEditableEmailDocument = editor.Edit();
}
```
### Crea e modifica con opzioni personalizzate
Specificare le opzioni di output del messaggio di posta per controllare il processo di modifica.
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EmailEditOptions emailEditOptions = new EmailEditOptions
    {
        MailMessageOutput = MailMessageOutput.All
    };
    EditableDocument editableEmailDocument = editor.Edit(emailEditOptions);
}
```
## Passaggio 8: finalizzazione del processo
Dopo aver modificato i documenti, è fondamentale smaltire correttamente il flusso di memoria per liberare risorse.
```csharp
memoryStream.Dispose();
System.Console.WriteLine("CreateDocument routine has successfully finished");
```
## Conclusione
GroupDocs.Editor per .NET è uno strumento versatile e potente che può semplificare l'attività di modifica di vari tipi di documenti a livello di codice. Seguendo questa guida passo passo, puoi creare e modificare documenti con facilità, siano essi file di elaborazione testi, fogli di calcolo, presentazioni, ebook o e-mail. Immergiti nella documentazione di GroupDocs.Editor per funzionalità più avanzate e opzioni di personalizzazione.
## Domande frequenti
### Quali tipi di documenti posso modificare con GroupDocs.Editor per .NET?
Puoi modificare un'ampia gamma di documenti, inclusi elaborazione testi, fogli di calcolo, presentazioni, ebook ed e-mail.
### È possibile personalizzare le opzioni di modifica?
Sì, GroupDocs.Editor per .NET consente un'ampia personalizzazione attraverso varie opzioni di modifica specifiche per ciascun tipo di documento.
### Come gestisco l'output dei documenti modificati?
È possibile utilizzare una funzione di richiamata per salvare il flusso di documenti modificato nella posizione desiderata.
### Ho bisogno di una licenza per utilizzare GroupDocs.Editor per .NET?
 Sì, puoi ottenere una licenza da[Qui](https://purchase.groupdocs.com/buy). C'è anche un'opzione per una licenza temporanea.
### Dove posso trovare documentazione più dettagliata?
 La documentazione dettagliata è disponibile su[GroupDocs.Editor per la pagina della documentazione .NET](https://tutorials.groupdocs.com/editor/net/).