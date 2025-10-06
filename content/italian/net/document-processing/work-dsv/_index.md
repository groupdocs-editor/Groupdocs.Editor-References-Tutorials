---
title: Utilizzare valori separati delimitati (DSV)
linktitle: Utilizzare valori separati delimitati (DSV)
second_title: API GroupDocs.Editor .NET
description: Scopri come modificare file CSV e TSV utilizzando GroupDocs.Editor per .NET con questa guida passo passo. Migliora i tuoi progetti .NET senza sforzo.
weight: 12
url: /it/net/document-processing/work-dsv/
type: docs
---
# Utilizzare valori separati delimitati (DSV)

## introduzione
Se sei uno sviluppatore che lavora con valori separati delimitati (DSV) come file CSV o TSV, sai che la modifica di questi file a livello di codice può essere un compito arduo. Tuttavia, con GroupDocs.Editor per .NET, questa attività diventa notevolmente più semplice ed efficiente. In questo tutorial ti spiegheremo come utilizzare GroupDocs.Editor per .NET per leggere, modificare e salvare file DSV. Suddivideremo il processo in passaggi facili da seguire, rendendolo semplice da implementare nei tuoi progetti.
## Prerequisiti
Prima di immergerci nel tutorial, assicurati di avere i seguenti prerequisiti:
- Visual Studio: assicurati di avere Visual Studio installato sul tuo computer.
-  GroupDocs.Editor per .NET: dovrai scaricare e fare riferimento alla libreria GroupDocs.Editor per .NET. Puoi scaricarlo[Qui](https://releases.groupdocs.com/editor/net/).
- Comprensione di base di C#: questa esercitazione presuppone una conoscenza di base dello sviluppo C# e .NET.
## Importa spazi dei nomi
Innanzitutto, devi importare gli spazi dei nomi necessari nel tuo progetto. Questi spazi dei nomi forniscono le classi e i metodi necessari per lavorare con GroupDocs.Editor per .NET.
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

## Passaggio 1: ottenere un percorso per il file DSV di input
Innanzitutto è necessario specificare il percorso del file DSV di input. Per questo esempio, supponiamo che si tratti di un file CSV.
```csharp
string inputFilePath = "Your Sample Document";
```
## Passaggio 2: crea un'istanza dell'editor
 Crea un'istanza di`Editor` classe. Questa istanza verrà utilizzata per caricare e manipolare il file DSV.
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## Passaggio 3: crea le opzioni di modifica DSV
 Successivamente, crea un'istanza di`DelimitedTextEditOptions` e specificare il delimitatore per il file DSV. Qui utilizziamo una virgola come delimitatore.
```csharp
    Options.DelimitedTextEditOptions editOptions = new DelimitedTextEditOptions(",");
    editOptions.ConvertDateTimeData = false;
    editOptions.ConvertNumericData = true;
    editOptions.TreatConsecutiveDelimitersAsOne = true;
```
## Passaggio 4: crea un'istanza di documento modificabile
 Creare un`EditableDocument` istanza utilizzando il file`Editor.Edit` metodo. Questo prepara il documento per la modifica.
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## Passaggio 5: modifica il contenuto del documento
Recupera il contenuto del testo originale e apporta le modifiche necessarie. A scopo dimostrativo, sostituiamo del testo.
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("SsangYong", "Chevrolet").Replace("Kyron", "Camaro");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## Passaggio 6: crea un documento modificabile con contenuto aggiornato
 Creane uno nuovo`EditableDocument` con il contenuto aggiornato.
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## Passaggio 7: crea opzioni di salvataggio CSV
Specificare le opzioni di salvataggio per il formato CSV, inclusi delimitatore e codifica.
```csharp
    Options.DelimitedTextSaveOptions csvSaveOptions = new DelimitedTextSaveOptions(",");
    csvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## Passaggio 8: crea le opzioni di salvataggio TSV
Allo stesso modo, specifica le opzioni di salvataggio per il formato TSV.
```csharp
    Options.DelimitedTextSaveOptions tsvSaveOptions = new DelimitedTextSaveOptions("\t");
    tsvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## Passaggio 9: crea le opzioni di salvataggio del foglio di calcolo
Se devi salvare il documento come foglio di calcolo, crea le opzioni di salvataggio corrispondenti.
```csharp
    Options.SpreadsheetSaveOptions cellsSaveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
```
## Passaggio 10: preparare i percorsi di salvataggio
Definire i percorsi in cui verranno salvati i file modificati.
```csharp
    string outputCsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".csv");
    string outputTsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".tsv");
    string outputCellsPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".xlsm");
```
## Passaggio 11: salva il documento modificato
Salva il documento modificato nei percorsi specificati in diversi formati.
```csharp
    editor.Save(afterEdit, outputCsvPath, csvSaveOptions);
    editor.Save(afterEdit, outputTsvPath, tsvSaveOptions);
    editor.Save(afterEdit, outputCellsPath, cellsSaveOptions);
```
## Passaggio 12: eliminare le istanze di documento modificabile
 Infine, assicurati di smaltire il`EditableDocument` istanze per liberare risorse.
```csharp
    beforeEdit.Dispose();
    afterEdit.Dispose();
}
System.Console.WriteLine("WorkingWithDsv routine has successfully finished");
```
## Conclusione
La modifica dei file DSV utilizzando GroupDocs.Editor per .NET è un processo semplice che prevede la creazione di un'istanza dell'editor, l'impostazione delle opzioni di modifica, la modifica del contenuto e il salvataggio delle modifiche. Questa guida dettagliata dovrebbe aiutarti a integrare facilmente questa funzionalità nelle tue applicazioni .NET. Che tu stia lavorando con CSV, TSV o altri formati DSV, GroupDocs.Editor per .NET fornisce una soluzione solida e flessibile.
## Domande frequenti
### Posso utilizzare GroupDocs.Editor for .NET per modificare file CSV di grandi dimensioni?
Sì, GroupDocs.Editor per .NET è in grado di gestire file CSV di grandi dimensioni in modo efficiente.
### GroupDocs.Editor per .NET supporta altri formati DSV oltre a CSV e TSV?
Sì, supporta vari formati DSV purché si specifichi il delimitatore appropriato.
### È possibile personalizzare la codifica durante il salvataggio dei file DSV?
Assolutamente sì, puoi specificare la codifica desiderata nelle opzioni di salvataggio.
### Posso convertire un file CSV in un foglio di calcolo Excel utilizzando GroupDocs.Editor per .NET?
Sì, puoi salvare un file CSV come foglio di calcolo Excel utilizzando le opzioni di salvataggio appropriate.
### Dove posso trovare ulteriore documentazione su GroupDocs.Editor per .NET?
 Puoi trovare documentazione dettagliata[Qui](https://tutorials.groupdocs.com/editor/net/)