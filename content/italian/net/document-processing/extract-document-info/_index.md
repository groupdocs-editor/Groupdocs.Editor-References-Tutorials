---
title: Estrai informazioni sul documento
linktitle: Estrai informazioni sul documento
second_title: API GroupDocs.Editor .NET
description: Scopri come estrarre le informazioni sui documenti utilizzando GroupDocs.Editor per .NET con il nostro tutorial dettagliato passo dopo passo. Perfetto per gestire vari tipi di documenti.
weight: 10
url: /it/net/document-processing/extract-document-info/
type: docs
---
# Estrai informazioni sul documento

## introduzione
Benvenuti in questo tutorial completo sull'estrazione delle informazioni sui documenti utilizzando GroupDocs.Editor per .NET. In questa guida ti guideremo attraverso il processo passo dopo passo, assicurandoci che tu comprenda ogni parte in modo chiaro e conciso. Che tu sia uno sviluppatore esperto o che tu abbia appena iniziato, questo tutorial ti aiuterà a integrare perfettamente GroupDocs.Editor nei tuoi progetti .NET per gestire e manipolare i documenti in modo efficiente.
## Prerequisiti
Prima di immergerti nel codice, assicuriamoci di avere tutto ciò di cui hai bisogno:
- Conoscenza di base di C#: comprendere le basi della programmazione C# è essenziale.
- Visual Studio: assicurati di avere Visual Studio installato.
-  GroupDocs.Editor per .NET: avrai bisogno della libreria GroupDocs.Editor per .NET. Puoi scaricarlo da[pagina di download](https://releases.groupdocs.com/editor/net/).
## Importa spazi dei nomi
Per iniziare, dovrai importare gli spazi dei nomi necessari. Ciò consente di accedere alle classi e ai metodi necessari per manipolare i documenti.
```csharp
using System;
using GroupDocs.Editor.Metadata;
```
## Passaggio 1: carica il documento
Innanzitutto, devi caricare il documento da cui desideri estrarre le informazioni. Questo può essere fatto fornendo il percorso del file al documento.
```csharp
string docxInputFilePath = "YourSampleDocument.docx";
Editor editorDocx = new Editor(docxInputFilePath);
```
## Passaggio 2: recuperare le informazioni sul documento
 Successivamente, recupererai le informazioni sul documento utilizzando il file`GetDocumentInfo` metodo. Questo metodo non richiede opzioni di caricamento specifiche se non sei sicuro del formato del documento.
```csharp
IDocumentInfo infoDocx = editorDocx.GetDocumentInfo(null);
```
## Passaggio 3: determinare il tipo di documento
Ora devi verificare il tipo di documento con cui hai a che fare. Questo è fondamentale in quanto determina come gestirai il documento.
```csharp
bool isSpreadsheet = infoDocx is SpreadsheetDocumentInfo;
bool isText = infoDocx is TextualDocumentInfo;
bool isWordProcessing = infoDocx is WordProcessingDocumentInfo;
Console.WriteLine($"Is '{docxInputFilePath}' a Spreadsheet: {isSpreadsheet}");
Console.WriteLine($"Is '{docxInputFilePath}' a Textual document: {isText}");
Console.WriteLine($"Is '{docxInputFilePath}' a WordProcessing document: {isWordProcessing}");
```
## Passaggio 4: estrazione di informazioni dettagliate
Se il documento è un documento di elaborazione testi, puoi estrarre informazioni dettagliate come formato, estensione, numero di pagine, dimensioni e se è crittografato.
```csharp
if (isWordProcessing)
{
    WordProcessingDocumentInfo casted = (WordProcessingDocumentInfo)infoDocx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Page count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```
## Passaggio 5: ripetere per diversi tipi di documenti
Ripeti gli stessi passaggi per altri tipi di documenti come fogli di calcolo e documenti di testo.
```csharp
string xlsxInputFilePath = "YourSampleDocument.xlsx";
Editor editorXlsx = new Editor(xlsxInputFilePath);
IDocumentInfo infoXlsx = editorXlsx.GetDocumentInfo(null);
bool isXlsxSpreadsheet = infoXlsx is SpreadsheetDocumentInfo;
Console.WriteLine($"Is '{xlsxInputFilePath}' a Spreadsheet: {isXlsxSpreadsheet}");
if (isXlsxSpreadsheet)
{
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo)infoXlsx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Tabs count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```
## Passaggio 6: gestire i documenti protetti da password
Quando hai a che fare con documenti protetti da password, dovresti prima provare ad aprirli senza password, poi con una password errata e infine con la password corretta.
```csharp
string xlsInputFilePath = "YourSampleDocument.xls";
Editor editorXls = new Editor(xlsInputFilePath);
try
{
    IDocumentInfo infoXls = editorXls.GetDocumentInfo(null);
}
catch (PasswordRequiredException)
{
    Console.WriteLine("This document is password-protected.");
}
try
{
    IDocumentInfo infoXls = editorXls.GetDocumentInfo("incorrect_password");
}
catch (IncorrectPasswordException)
{
    Console.WriteLine("The provided password is incorrect.");
}
IDocumentInfo infoXlsValid = editorXls.GetDocumentInfo("correct_password");
bool isXlsSpreadsheet = infoXlsValid is SpreadsheetDocumentInfo;
Console.WriteLine($"Password-protected document is a Spreadsheet: {isXlsSpreadsheet}");
if (isXlsSpreadsheet)
{
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo)infoXlsValid;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Tabs count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```
## Passaggio 7: gestire documenti basati su testo
```csharp
string xmlInputFilePath = "YourSampleDocument.xml";
Editor editorXml = new Editor(xmlInputFilePath);
IDocumentInfo infoXml = editorXml.GetDocumentInfo(null);
bool isXmlText = infoXml is TextualDocumentInfo;
Console.WriteLine($"Is '{xmlInputFilePath}' a Textual document: {isXmlText}");
if (isXmlText)
{
    TextualDocumentInfo casted = (TextualDocumentInfo)infoXml;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Encoding: {casted.Encoding}; Size: {casted.Size} bytes");
}
```
## Passaggio 8: smaltire le risorse
Infine, assicurati di smaltire tutte le risorse per evitare perdite di memoria.
```csharp
editorDocx.Dispose();
editorXlsx.Dispose();
editorXls.Dispose();
editorXml.Dispose();
Console.WriteLine("ExtractingDocumentInfo routine has successfully finished");
```
## Conclusione
Congratulazioni! Ora hai imparato come estrarre le informazioni sui documenti utilizzando GroupDocs.Editor per .NET. Questa potente libreria semplifica la gestione e la manipolazione dei documenti, consentendoti di gestire diversi tipi di documenti senza problemi. Che tu abbia a che fare con elaborazione testi, fogli di calcolo o documenti basati su testo, GroupDocs.Editor fornisce una soluzione solida.
## Domande frequenti
### Quali tipi di documenti può gestire GroupDocs.Editor?
GroupDocs.Editor può gestire vari tipi di documenti tra cui elaborazione testi, fogli di calcolo e documenti basati su testo.
### GroupDocs.Editor può gestire documenti protetti da password?
Sì, GroupDocs.Editor può gestire documenti protetti da password. Può identificare e aprire questi documenti fornendo la password corretta.
### È necessario disfarsi degli oggetti Editor?
Sì, è fondamentale eliminare gli oggetti Editor per liberare risorse e prevenire perdite di memoria.
### Posso estrarre informazioni dettagliate sul formato e sulle dimensioni del documento?
Assolutamente! GroupDocs.Editor ti consente di estrarre informazioni dettagliate tra cui formato, estensione, dimensione, conteggio delle pagine e stato di crittografia.
### Dove posso ottenere supporto se riscontro problemi?
 Puoi ottenere supporto da[Forum di supporto GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).