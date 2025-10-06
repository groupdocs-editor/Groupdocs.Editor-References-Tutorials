---
title: Rimuovi raccolta campi modulo
linktitle: Rimuovi raccolta campi modulo
second_title: API GroupDocs.Editor .NET
description: Scopri come rimuovere i campi modulo dai documenti Word utilizzando GroupDocs.Editor per .NET con questa guida passo passo. Ideale per gli sviluppatori.
weight: 13
url: /it/net/form-field-management/remove-form-field-collection/
type: docs
---
# Rimuovi raccolta campi modulo

## introduzione
Stai cercando di gestire i campi modulo nei tuoi documenti a livello di codice? GroupDocs.Editor per .NET offre una potente soluzione per gestire e manipolare i campi modulo in vari formati di documento. In questo tutorial ti guideremo attraverso i passaggi per rimuovere raccolte di campi modulo da un documento Word utilizzando questa solida libreria. 
## Prerequisiti
Prima di immergerci nel codice, assicuriamoci di aver impostato tutto per un'esperienza fluida:
1. GroupDocs.Editor per .NET: assicurati di aver scaricato e installato GroupDocs.Editor per .NET. In caso contrario, puoi scaricarlo[Qui](https://releases.groupdocs.com/editor/net/).
2. Ambiente di sviluppo: avrai bisogno di un ambiente di sviluppo come Visual Studio.
3. .NET Framework: assicurati di avere .NET Framework installato sul tuo computer.
4.  Documento di esempio: disporre di un documento Word di esempio (ad es.`SampleLegacyFormFields.docx`) con i campi del modulo che desideri manipolare.

## Importa spazi dei nomi
Per iniziare, devi importare gli spazi dei nomi necessari nel tuo progetto .NET. Ciò ti consentirà di accedere alle funzionalità di GroupDocs.Editor.
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System.IO;
```
## Passaggio 1: caricare il documento
Innanzitutto, dovrai caricare il documento che desideri modificare. Analizziamolo:
### Passaggio 1.1: ottenere il percorso del file di input
 È necessario specificare il percorso del file di input. Per questo esempio, utilizzeremo un file di esempio chiamato`SampleLegacyFormFields.docx`.
```csharp
string inputFilePath = "path/to/SampleLegacyFormFields.docx";
```
### Passaggio 1.2: creare un FileStream dal percorso
 Successivamente, crea un file`FileStream` per leggere il documento.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
    // Continua con i passaggi successivi all'interno di questo blocco utilizzando.
}
```
## Passaggio 2: imposta le opzioni di caricamento
Durante il caricamento del documento, potrebbe essere necessario specificare le opzioni di caricamento, soprattutto se il documento è protetto da password.
### Passaggio 2.1: creazione delle opzioni di caricamento
 Crea un'istanza di`WordProcessingLoadOptions`.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
```
### Passaggio 2.2: specificare la password (se necessario)
Se il documento è protetto da password, è possibile specificare la password.
```csharp
loadOptions.Password = "some_password_to_open_a_document";
```
## Passaggio 3: carica il documento nell'editor
 Ora carica il documento nel file`Editor` istanza utilizzando il file`FileStream` E`LoadOptions`.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    // Continua con i passaggi successivi all'interno di questo blocco utilizzando.
}
```
## Passaggio 4: accedi e gestisci i campi del modulo
Con il documento caricato, ora puoi accedere e manipolare i campi del modulo.
### Passaggio 4.1: leggere il FormFieldManager
 Recupera il`FormFieldManager` dal`Editor` esempio.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
### Passaggio 4.2: accedere a FormFieldCollection
 Ottenere il`FormFieldCollection` che contiene tutti i campi modulo nel documento.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
### Passaggio 4.3: rimuovere un campo modulo di testo specifico
Per rimuovere un campo modulo di testo specifico, individualo tramite il suo nome e quindi rimuovilo.
```csharp
TextFormField textField = collection.GetFormField<TextFormField>("Text1");
fieldManager.RemoveFormFiled(textField);
```
### Passaggio 4.4: rimuovere più campi modulo
Puoi anche rimuovere più campi modulo contemporaneamente specificandone i nomi.
```csharp
textField = collection.GetFormField<TextFormField>("Text7");
CheckBoxForm checkBoxForm = collection.GetFormField<CheckBoxForm>("Check2");
fieldManager.RemoveFormFields(new IFormField[] { textField, checkBoxForm });
```
## Passaggio 5: salva il documento modificato
Dopo aver modificato i campi del modulo, è necessario salvare il documento.
### Passaggio 5.1: creazione delle opzioni di salvataggio
Specificare il formato e le opzioni di salvataggio per il documento di output.
```csharp
WordProcessingFormats docFormat = WordProcessingFormats.Docx;
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(docFormat);
```
### Passaggio 5.2: ottimizzare l'utilizzo della memoria
Se hai a che fare con documenti di grandi dimensioni, potresti voler ottimizzare l'utilizzo della memoria.
```csharp
saveOptions.OptimizeMemoryUsage = true;
```
### Passaggio 5.3: impostazione della protezione (se necessario)
È possibile proteggere il documento da ulteriori modifiche impostando una password di scrittura.
```csharp
saveOptions.Protection = new WordProcessingProtection(WordProcessingProtectionType.AllowOnlyFormFields, "write_password");
```
### Passaggio 5.4: salvare il documento
 Infine, salva il documento utilizzando a`MemoryStream`.
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(outputStream, saveOptions);
}
```

## Conclusione
Congratulazioni! Hai rimosso con successo i campi modulo da un documento Word utilizzando GroupDocs.Editor per .NET. Questa potente libreria semplifica la manipolazione del contenuto dei documenti a livello di codice, risparmiando tempo e fatica.
## Domande frequenti
### Posso utilizzare GroupDocs.Editor for .NET con altri formati di documenti?
Sì, GroupDocs.Editor per .NET supporta vari formati di documenti, inclusi PDF, HTML e altri.
### È possibile aggiungere campi modulo utilizzando GroupDocs.Editor per .NET?
Sì, puoi aggiungere, modificare e rimuovere i campi del modulo a livello di codice.
### Cosa succede se il mio documento è molto grande?
È possibile abilitare l'ottimizzazione della memoria nelle opzioni di salvataggio per gestire documenti di grandi dimensioni in modo efficiente.
### Posso utilizzare GroupDocs.Editor per .NET in un'applicazione web?
Assolutamente! GroupDocs.Editor per .NET può essere integrato in applicazioni web per l'elaborazione di documenti lato server.
### Dove posso ottenere supporto se riscontro problemi?
 Puoi visitare il[Forum di assistenza](https://forum.groupdocs.com/c/editor/20) per assistenza su eventuali problemi.