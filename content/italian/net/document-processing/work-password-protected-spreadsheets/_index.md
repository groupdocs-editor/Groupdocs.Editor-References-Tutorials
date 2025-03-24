---
title: Lavora con fogli di calcolo protetti da password
linktitle: Lavora con fogli di calcolo protetti da password
second_title: API GroupDocs.Editor .NET
description: Scopri come gestire i fogli di calcolo protetti da password utilizzando GroupDocs.Editor per .NET. Questa guida dettagliata ti guida attraverso l'apertura e il salvataggio di file Excel protetti.
weight: 18
url: /it/net/document-processing/work-password-protected-spreadsheets/
---

# Lavora con fogli di calcolo protetti da password

## introduzione
Hai difficoltà a gestire fogli di calcolo protetti da password nelle tue applicazioni .NET? Se è così, sei nel posto giusto! In questa guida completa ti guideremo attraverso il processo di utilizzo di GroupDocs.Editor per .NET per gestire in modo efficiente i fogli di calcolo protetti da password. Alla fine di questo tutorial sarai ben attrezzato per aprire, modificare e salvare facilmente file Excel crittografati.
## Prerequisiti
Prima di immergerci nel codice, assicuriamoci di avere tutto ciò di cui hai bisogno per seguire:
- Conoscenza di base di C#: questo tutorial presuppone che tu abbia familiarità con la programmazione C#.
- .NET Framework: assicurati di avere .NET Framework installato sul tuo computer di sviluppo.
-  GroupDocs.Editor per .NET: scarica e installa GroupDocs.Editor per .NET da[Qui](https://releases.groupdocs.com/editor/net/).
## Importa spazi dei nomi
Per iniziare, dovrai importare gli spazi dei nomi necessari nel tuo progetto C#. Questi spazi dei nomi forniscono l'accesso alle funzionalità di GroupDocs.Editor.
```csharp
using System;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
## Passaggio 1: ottieni un percorso per il file di input
Innanzitutto, avrai bisogno di un percorso per il file di input. Per questo esempio utilizzeremo un file Excel di esempio (`Your Sample Document`) protetto da password.
```csharp
string inputFilePath = "Your Sample Document";
```
## Passaggio 2: tentativo di aprire il documento senza password
Vediamo cosa succede se proviamo ad aprire il documento senza fornire una password.
```csharp
Editor editor = new Editor(inputFilePath);
try
{
    editor.Edit();
}
catch (GroupDocs.Editor.PasswordRequiredException)
{
    Console.WriteLine("Cannot edit the document because it is password-protected. A password is required.");
}
editor.Dispose();
```
## Passaggio 3: provare a specificare una password errata
Ora specificheremo una password errata per dimostrare come risponde l'editor.
```csharp
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.Password = "incorrect_password";
editor = new Editor(inputFilePath, delegate { return loadOptions; });
try
{
    editor.Edit();
}
catch (GroupDocs.Editor.IncorrectPasswordException)
{
    Console.WriteLine("Cannot edit the document because the specified password is incorrect.");
}
editor.Dispose();
```
## Passaggio 4: aprire il file con la password corretta
Forniamo la password corretta e apriamo il file con successo.
```csharp
loadOptions.Password = "excel_password";
loadOptions.OptimizeMemoryUsage = true;
editor = new Editor(inputFilePath, delegate { return loadOptions; });
```
## Passaggio 5: crea e modifica le opzioni di modifica
Per modificare il foglio di calcolo, dobbiamo creare e modificare le opzioni di modifica.
```csharp
SpreadsheetEditOptions editOptions = new SpreadsheetEditOptions();
```
## Passaggio 6: creare un documento modificabile intermedio
 Successivamente, creiamo un intermedio`EditableDocument` che ci consente di apportare modifiche al foglio di calcolo.
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
{
    // Passaggio 7: crea opzioni di salvataggio
    SpreadsheetFormats xlsmFormat = SpreadsheetFormats.Xlsm;
    SpreadsheetSaveOptions saveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
    // Passaggio 7.1: imposta la nuova password di apertura
    saveOptions.Password = "new password";
    // Passaggio 7.2: impostare la protezione da scrittura
    saveOptions.WorksheetProtection = new WorksheetProtection(WorksheetProtectionType.All, "write password");
    // Passaggio 8: salva il documento senza modifiche
    //Passaggio 8.1: preparare il nome e il percorso del file di output
    string outputFilename = Path.GetFileNameWithoutExtension(inputFilePath) + "." + xlsmFormat.Extension;
    string outputPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename);
    // Passaggio 8.2: creazione del flusso di output
    using (FileStream outputStream = File.Create(outputPath))
    {
        // Passaggio 8.3: Salva
        editor.Save(beforeEdit, outputStream, saveOptions);
    }
}
// Passaggio 9: eliminare l'istanza dell'editor
editor.Dispose();
Console.WriteLine("Successfully handled the password-protected spreadsheet. Editor instance has been disposed: {0}", editor.IsDisposed ? "Yes" : "No");
```
## Conclusione
Congratulazioni! Hai imparato con successo come gestire i fogli di calcolo protetti da password utilizzando GroupDocs.Editor per .NET. Dal tentativo di aprire il documento senza password al salvarlo con nuove impostazioni di protezione, hai coperto tutti i passaggi essenziali. Questa conoscenza migliorerà senza dubbio la tua capacità di gestire documenti sicuri all'interno delle tue applicazioni .NET.
## Domande frequenti
### Cos'è GroupDocs.Editor per .NET?
GroupDocs.Editor per .NET è una potente API di modifica dei documenti che consente agli sviluppatori di caricare, modificare e salvare una varietà di formati di documenti all'interno delle applicazioni .NET.
### Come posso ottenere una licenza temporanea per GroupDocs.Editor?
 È possibile ottenere una licenza temporanea da[Qui](https://purchase.groupdocs.com/temporary-license/) per valutare le caratteristiche del prodotto.
### È possibile ottimizzare l'utilizzo della memoria durante la modifica di documenti di grandi dimensioni?
 Sì, puoi abilitare l'ottimizzazione della memoria impostando il file`OptimizeMemoryUsage` proprietà a`true`nelle opzioni di caricamento.
### Posso impostare password diverse per aprire e scrivere su un foglio di calcolo?
Assolutamente! È possibile impostare password separate per l'apertura del documento e per la protezione da scrittura utilizzando le opzioni di salvataggio.
### Dove posso trovare documentazione più dettagliata?
 È possibile accedere alla documentazione completa per GroupDocs.Editor per .NET[Qui](https://tutorials.groupdocs.com/editor/net/).