---
title: Correggi la raccolta di campi modulo non validi e salva
linktitle: Correggi la raccolta di campi modulo non validi e salva
second_title: API GroupDocs.Editor .NET
description: Scopri come correggere i campi modulo non validi in DOCX utilizzando Groupdocs.Editor per .NET. Segui questa guida per assicurarti che i tuoi documenti siano privi di errori e salvarli in modo sicuro.
weight: 11
url: /it/net/form-field-management/fix-invalid-form-field-collection-save/
type: docs
---
# Correggi la raccolta di campi modulo non validi e salva

## introduzione
Benvenuto! Se lavori con i campi modulo nei documenti e riscontri problemi con raccolte di campi modulo non valide, sei nel posto giusto. In questo tutorial, approfondiremo come correggere i campi del modulo non validi e salvare il documento utilizzando Groupdocs.Editor per .NET. Ti guideremo attraverso il processo passo dopo passo, assicurandoti di avere tutti i dettagli necessari per farlo funzionare senza problemi. Iniziamo!
## Prerequisiti
Prima di addentrarci nel codice, ci sono alcune cose che devi avere a posto:
-  Groupdocs.Editor per .NET: assicurati di aver installato la libreria Groupdocs.Editor per .NET. Puoi scaricarlo[Qui](https://releases.groupdocs.com/editor/net/).
- Ambiente di sviluppo: è necessario disporre di un ambiente di sviluppo .NET configurato, ad esempio Visual Studio.
- Conoscenza di base di C#: questo tutorial presuppone che tu abbia una conoscenza di base della programmazione C#.
## Importa spazi dei nomi
Innanzitutto, devi importare gli spazi dei nomi necessari nel tuo progetto C#. Aggiungi le seguenti righe all'inizio del file di codice:
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System;
using System.IO;
```
## Passaggio 1: ottenere il percorso del file di input
Il primo passo è specificare il percorso del file di input. Questo file dovrebbe essere un documento DOCX contenente campi modulo.
```csharp
string inputFilePath = Constants.SampleLegacyFormFields_docx;
```
## Passaggio 2: crea uno stream dal percorso file
Successivamente, crea un flusso di file per leggere il documento di input. Ciò ti consentirà di caricare il documento nell'editor.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
```
## Passaggio 3: creare opzioni di caricamento per il documento
In questo passaggio, devi creare opzioni di caricamento per il tuo documento. Se il documento è protetto da password, è possibile specificare la password. In questo esempio il documento non è protetto, quindi la password viene ignorata.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
loadOptions.Password = "some_password_to_open_a_document";
```
## Passaggio 4: caricare il documento nell'istanza dell'editor
Ora carica il documento con le opzioni specificate nell'istanza dell'editor. È qui che si svolgeranno le principali operazioni sul documento.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
```
## Passaggio 4.1: leggere l'istanza di FormFieldManager
 IL`FormFieldManager` l'istanza è responsabile della gestione dei campi del modulo nel documento. Dovrai leggere questa istanza per accedere e manipolare i campi del modulo.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
## Passaggio 4.2: leggere FormFieldCollection
 IL`FormFieldCollection` contiene tutti i campi del modulo nel documento. Leggerai questa raccolta per verificare e correggere i campi del modulo non validi.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
## Passaggio 4.3: correzione automatica dei campi del modulo non validi
Tentare di correggere automaticamente eventuali campi modulo non validi nel documento. Questo è un passo preliminare per affrontare questioni evidenti.
```csharp
fieldManager.FixInvalidFormFieldNames(new InvalidFormField[0]);
collection = fieldManager.FormFieldCollection;
```
## Passaggio 4.4: verificare la presenza di campi modulo non validi
Controlla se sono rimasti campi del modulo non validi dopo il tentativo di correzione automatica.
```csharp
bool hasInvalidFormFields = fieldManager.HasInvalidFormFields();
Console.WriteLine("FormFieldCollection contains invalid items: {0}", hasInvalidFormFields);
```
## Passaggio 4.4.1: Ottieni tutti i nomi dei campi modulo non validi
Recupera i nomi di tutti i campi del modulo non validi. Questi nomi verranno utilizzati per correggere i campi.
```csharp
var invalidFormFields = fieldManager.GetInvalidFormFieldNames();
```
## Passaggio 4.4.2: creare nomi univoci per i campi non validi
Per ogni campo modulo non valido, crea un nome univoco. Ciò garantisce che non vi siano conflitti con i nomi dei campi del modulo esistenti.
```csharp
foreach (var invalidItem in invalidFormFields)
{
    invalidItem.FixedName = string.Format("{0}_{1}", invalidItem.Name, Guid.NewGuid());
}
```
## Passaggio 4.4.3: correggere i campi del modulo non validi
Correggi i campi del modulo non validi utilizzando i nomi univoci creati nel passaggio precedente.
```csharp
fieldManager.FixInvalidFormFieldNames(invalidFormFields);
collection = fieldManager.FormFieldCollection;
```
## Passaggio 5: crea le opzioni di salvataggio del documento
Configura le opzioni per salvare il documento. Ciò include la specifica del formato e di eventuali impostazioni di salvataggio aggiuntive.
```csharp
WordProcessingFormats docFormat = WordProcessingFormats.Docx;
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(docFormat);
```
## Passaggio 5.1: ottimizzare l'utilizzo della memoria
 Se il tuo documento è di grandi dimensioni e potrebbe causare un`OutOfMemoryException`abilitare l'opzione di ottimizzazione della memoria.
```csharp
saveOptions.OptimizeMemoryUsage = true;
```
## Passaggio 5.2: proteggere il documento dalla scrittura
Per proteggere il documento da eventuali modifiche, ad eccezione dei campi del modulo, impostare una password di protezione.
```csharp
saveOptions.Protection = new WordProcessingProtection(WordProcessingProtectionType.AllowOnlyFormFields, "write_password");
```
## Passaggio 6: salva il documento
Infine, salva il documento con le opzioni di salvataggio specificate. Preparare un flusso di memoria per salvare il documento di output.
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(outputStream, saveOptions);
}
Console.WriteLine("FixInvalidFormFieldCollectionAndSave routine has successfully finished");
```
## Conclusione
 E il gioco è fatto! Hai corretto con successo i campi del modulo non validi e salvato il documento utilizzando Groupdocs.Editor per .NET. Questa guida passo passo avrebbe dovuto rendere il processo chiaro e gestibile. Se riscontri problemi o hai domande, non esitare a controllare il[documentazione](https://tutorials.groupdocs.com/editor/net/) o contattare[supporto](https://forum.groupdocs.com/c/editor/20).
## Domande frequenti
### Cosa succede se il mio documento è protetto da password?
 È possibile specificare la password nel file`WordProcessingLoadOptions` per aprire il documento.
### Come faccio a sapere se ci sono campi modulo non validi?
 Usa il`HasInvalidFormFields` metodo per verificare la presenza di eventuali campi modulo non validi nel documento.
### Posso correggere i campi del modulo senza cambiarne i nomi?
Si consiglia di creare nomi univoci per i campi del modulo non validi per evitare conflitti.
### In quali formati posso salvare il documento?
 Puoi salvare il documento in vari formati come DOCX, PDF e altri impostando il formato appropriato`WordProcessingFormats`.
### Come posso ottimizzare l'utilizzo della memoria salvando documenti di grandi dimensioni?
 Abilita il`OptimizeMemoryUsage` opzione nel`WordProcessingSaveOptions` per gestire documenti di grandi dimensioni in modo efficiente.