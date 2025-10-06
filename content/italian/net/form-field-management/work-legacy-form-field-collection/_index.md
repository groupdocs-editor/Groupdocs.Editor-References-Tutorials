---
title: Lavora con la raccolta di campi modulo legacy
linktitle: Lavora con la raccolta di campi modulo legacy
second_title: API GroupDocs.Editor .NET
description: Scopri come gestire i campi del modulo legacy utilizzando GroupDocs.Editor per .NET con la nostra guida dettagliata. Perfetto per gestire campi di testo, caselle di controllo, date e altro.
weight: 12
url: /it/net/form-field-management/work-legacy-form-field-collection/
type: docs
---
# Lavora con la raccolta di campi modulo legacy

## introduzione
Benvenuti in questa guida completa su come lavorare con raccolte di campi modulo legacy utilizzando GroupDocs.Editor per .NET. Che tu abbia a che fare con campi di testo, caselle di controllo, campi data o menu a discesa, questo tutorial ti guiderà attraverso ogni passaggio per gestire questi campi in modo efficiente. Al termine di questa guida avrai una solida conoscenza di come utilizzare GroupDocs.Editor per gestire vari campi modulo nei tuoi documenti. Immergiamoci!
## Prerequisiti
Prima di iniziare, assicurati di possedere i seguenti prerequisiti:
- Visual Studio: qualsiasi versione recente funzionerà.
- .NET Framework: assicurati di avere .NET Framework installato.
-  GroupDocs.Editor per .NET: scarica la versione più recente[Qui](https://releases.groupdocs.com/editor/net/).
- Documento di esempio: un file DOCX di esempio con campi modulo a scopo di test.
## Importa spazi dei nomi
Per cominciare, importa gli spazi dei nomi necessari nel tuo progetto. Questi spazi dei nomi sono essenziali per accedere alle classi e ai metodi richiesti per manipolare i campi del modulo.
```csharp
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System.IO;
```
## Passaggio 1: ottenere il percorso del file di input
Innanzitutto, devi specificare il percorso del file di input. In questo esempio utilizzeremo un file DOCX di esempio che contiene vari campi modulo.
```csharp
string inputFilePath = "path/to/your/sample_legacy_formfields.docx";
```
## Passaggio 2: crea uno stream dal percorso file
Successivamente, crea un flusso di file per leggere il contenuto del tuo documento. Questo flusso verrà utilizzato per caricare il documento in GroupDocs.Editor.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
    // Il codice aggiuntivo andrà qui
}
```
## Passaggio 3: creare opzioni di caricamento per il documento
Prima di caricare il documento, crea le opzioni di caricamento. Queste opzioni aiuteranno a gestire diversi scenari, come i documenti protetti da password.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
// Se il documento è protetto da password, specificare la password
loadOptions.Password = "your_password_here"; // Se necessario, utilizzare una password effettiva
```
## Passaggio 4: caricare il documento con l'istanza dell'editor
Ora carica il documento nell'istanza dell'editor utilizzando il flusso di file e le opzioni di caricamento create in precedenza.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    // Il codice aggiuntivo andrà qui
}
```
## Passaggio 5: leggere l'istanza di FormFieldManager
Per gestire i campi del modulo, accedi all'istanza FormFieldManager dall'editor. Questa istanza ti consentirà di interagire con i campi del modulo all'interno del tuo documento.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
## Passaggio 6: leggere FormFieldCollection
Recupera FormFieldCollection da FormFieldManager. Questa raccolta contiene tutti i campi modulo presenti nel documento.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
## Passaggio 7: scorrere ciascun campo del modulo
Scorri ogni campo del modulo nella raccolta e identificane il tipo. A seconda del tipo, puoi estrarre e manipolare il valore del campo.
```csharp
foreach (var formField in collection)
{
    switch (formField.Type)
    {
        case FormFieldType.Text:
            TextFormField textFormField = collection.GetFormField<TextFormField>(formField.Name);
            Console.WriteLine($"TextFormField detected, name: {formField.Name}, value: {textFormField.Value}");
            break;
        case FormFieldType.CheckBox:
            CheckBoxForm checkBoxFormField = collection.GetFormField<CheckBoxForm>(formField.Name);
            Console.WriteLine($"CheckBoxForm detected, name: {formField.Name}, value: {checkBoxFormField.Value}");
            break;
        case FormFieldType.Date:
            DateFormField dateFormField = collection.GetFormField<DateFormField>(formField.Name);
            Console.WriteLine($"DateFormField detected, name: {formField.Name}, value: {dateFormField.Value}");
            break;
        case FormFieldType.Number:
            NumberFormField numberFormField = collection.GetFormField<NumberFormField>(formField.Name);
            Console.WriteLine($"NumberFormField detected, name: {formField.Name}, value: {numberFormField.Value}");
            break;
        case FormFieldType.DropDown:
            DropDownFormField dropDownFormField = collection.GetFormField<DropDownFormField>(formField.Name);
            Console.WriteLine($"DropDownFormField detected, name: {formField.Name}, value selected: {dropDownFormField.Value[dropDownFormField.SelectedIndex]}");
            break;
    }
}
```
## Passaggio 8: conclusione
Seguendo questi passaggi, puoi gestire e interagire in modo efficace con i campi modulo legacy nei tuoi documenti utilizzando GroupDocs.Editor per .NET. Che si tratti di campi di testo, caselle di controllo, date, numeri o menu a discesa, questa guida fornisce un modo chiaro e conciso per gestire ogni tipo.
## Conclusione
 Lavorare con i campi modulo legacy nei documenti può essere semplice se si utilizzano gli strumenti giusti. GroupDocs.Editor per .NET fornisce una soluzione solida per gestire questi campi in modo efficiente. Seguendo questa guida passo passo, ora dovresti essere in grado di manipolare facilmente vari campi modulo nei tuoi documenti. Non dimenticare di esplorare il[documentazione](https://tutorials.groupdocs.com/editor/net/)per funzionalità e opzioni più avanzate.
## Domande frequenti
### 1. Posso utilizzare GroupDocs.Editor for .NET con documenti protetti da password?
Sì, puoi specificare la password nelle opzioni di caricamento per gestire i documenti protetti da password.
### 2. Come posso ottenere una prova gratuita di GroupDocs.Editor per .NET?
 È possibile scaricare una versione di prova gratuita da[Qui](https://releases.groupdocs.com/).
### 3. È disponibile supporto per GroupDocs.Editor per .NET?
 Sì, puoi accedere al supporto[Qui](https://forum.groupdocs.com/c/editor/20).
### 4. Posso acquistare una licenza per GroupDocs.Editor per .NET?
 Sì, puoi acquistare una licenza da[Qui](https://purchase.groupdocs.com/buy).
### 5. Dove posso trovare la documentazione per GroupDocs.Editor per .NET?
La documentazione è disponibile[Qui](https://tutorials.groupdocs.com/editor/net/).