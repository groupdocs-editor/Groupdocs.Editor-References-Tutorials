---
title: Utilizzo avanzato di documenti modificabili
linktitle: Utilizzo avanzato di documenti modificabili
second_title: API GroupDocs.Editor .NET
description: Scopri l'utilizzo avanzato di GroupDocs.Editor per .NET creando, modificando ed estraendo risorse dai documenti a livello di codice.
weight: 11
url: /it/net/document-editing/advanced-usage-of-editable-documents/
---
## introduzione
Se sei uno sviluppatore .NET che desidera migliorare le proprie capacità di modifica dei documenti, GroupDocs.Editor per .NET offre una potente suite di strumenti. Questa guida completa ti guiderà attraverso l'utilizzo avanzato di documenti modificabili utilizzando GroupDocs.Editor, analizzando ogni passaggio in dettaglio per assicurarti di poter sfruttare tutto il suo potenziale.
## Prerequisiti
Prima di immergerti nelle funzionalità avanzate, assicurati di avere quanto segue:
- Visual Studio installato nel computer di sviluppo.
- .NET Framework compatibile con GroupDocs.Editor.
-  GroupDocs.Editor per la libreria .NET. Puoi[scaricalo qui](https://releases.groupdocs.com/editor/net/).
-  Una licenza GroupDocs.Editor valida. Puoi ottenere un[prova gratuita](https://releases.groupdocs.com/) o acquistare un[licenza temporanea](https://purchase.groupdocs.com/temporary-license/).
## Importa spazi dei nomi
Per iniziare, assicurati di importare gli spazi dei nomi necessari nel tuo progetto .NET:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```
## Passaggio 1: creazione di un'istanza di documento modificabile
 Per prima cosa devi creare un'istanza di`EditableDocument` caricando e modificando un documento di input di un formato supportato.
```csharp
string inputFilePath = "YourSampleDocument.docx";
Editor editor = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```
In questo passaggio carichiamo il documento di input e lo prepariamo per la modifica.
## Passaggio 2: estrazione delle risorse del documento
 IL`EditableDocument` contiene varie risorse che possono essere estratte e manipolate. Analizziamoli:
### Passaggio 2.1: estrarre l'intero documento come HTML
Puoi generare una singola stringa che contiene l'intero documento con tutte le sue risorse incorporate come HTML.
```csharp
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```
Questa stringa sarà piuttosto grande poiché include fogli di stile, immagini e caratteri codificati in base64.
### Passaggio 2.2: estrai tutte le immagini
Estrai tutte le immagini dal documento.
```csharp
List<IImageResource> allImages = beforeEdit.Images;
```
### Passaggio 2.3: Estrai tutti i caratteri
Estrai tutti i caratteri utilizzati nel documento.
```csharp
List<FontResourceBase> allFonts = beforeEdit.Fonts;
```
### Passaggio 2.4: estrazione di tutti i fogli di stile
Estrai tutti i fogli di stile in formato testuale.
```csharp
List<CssText> allStylesheets = beforeEdit.Css;
```
### Passaggio 2.5: raccogliere tutte le risorse
Raccogli tutte le risorse in un'unica chiamata.
```csharp
List<IHtmlResource> allResources = beforeEdit.AllResources;
```
Ciò include immagini, caratteri e fogli di stile.
### Passaggio 2.6: ottenere il markup HTML
Ottieni il markup HTML del documento senza risorse incorporate.
```csharp
string htmlMarkup = beforeEdit.GetContent();
```
## Passaggio 3: regolazione dei collegamenti esterni
A volte è necessario modificare i collegamenti esterni in modo che puntino a un gestore di risorse personalizzato. Ecco come farlo:
### Passaggio 3.1: preparare prefissi personalizzati
Preparare i prefissi che anteporranno i collegamenti esterni originali.
```csharp
string customImagesRequesthandlerUri = "http://esempio.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://esempio.com/CssHandler/id=";
string customFontsRequesthandlerUri = "http://esempio.com/FontsHandler/id=";
```
### Passaggio 3.2: generazione di markup HTML con prefisso
Genera markup HTML con collegamenti modificati.
```csharp
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```
### Passaggio 3.3: ottenere contenuto HTML solo corpo
Alcuni editor WYSIWYG gestiscono solo markup HTML puro senza intestazioni.
```csharp
string onlyBodyContent = beforeEdit.GetBodyContent();
```
### Passaggio 3.4: contenuto solo corpo con prefisso
Genera contenuti solo per il corpo con prefissi di immagine personalizzati.
```csharp
string prefixedBodyContent = beforeEdit.GetBodyContent(customImagesRequesthandlerUri);
```
### Passaggio 3.5: estrazione dei fogli di stile
Estrai i fogli di stile utilizzati nel documento.
```csharp
List<string> stylesheets = beforeEdit.GetCssContent();
```
### Passaggio 3.6: Fogli di stile con prefisso
Estrai fogli di stile con prefissi personalizzati.
```csharp
List<string> prefixedStylesheets = beforeEdit.GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri);
```
## Passaggio 4: salva il documento come HTML
Salva il documento modificato come file HTML, incluse le sue risorse.
```csharp
string htmlFilePath = Path.Combine("output", Path.GetFileNameWithoutExtension(inputFilePath) + ".html");
beforeEdit.Save(htmlFilePath);
```
Questo metodo crea una directory separata per risorse come fogli di stile, immagini e caratteri.
## Passaggio 5: eliminazione di EditableDocument
 Implementa EditableDocument`IDisposable` e offre la possibilità di verificare se l'istanza è stata eliminata.
```csharp
Console.WriteLine("EditableDocument is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");
```
### Passaggio 5.1 Gestione dell'evento di eliminazione
Puoi anche iscriverti all'evento di smaltimento.
```csharp
EventHandler someMethod = delegate { Console.WriteLine("Disposing event was spotted!"); };
beforeEdit.Disposed += someMethod;
```
## Passaggio 6: creazione di un documento modificabile da HTML
Crea un'istanza di EditableDocument da un documento HTML.
### Passaggio 6.1: dal file HTML
```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
```
### Passaggio 6.2: dal markup HTML
```csharp
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);
```
Queste istanze (afterEditFromFile e afterEditFromMarkup) sono identiche all'originale (beforeEdit).
## Passaggio 7: smaltimento manuale
Elimina manualmente le tue istanze EditableDocument.
```csharp
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```
Ciò garantisce una corretta pulizia delle risorse.
## Conclusione
GroupDocs.Editor per .NET fornisce strumenti robusti per la modifica dei documenti a livello di codice. Seguendo questa guida passo passo, puoi gestire in modo efficiente il contenuto dei documenti, le risorse e i formati di output. Che tu stia incorporando risorse, modificando collegamenti esterni o convertendo documenti in HTML, GroupDocs.Editor ti fornisce le funzionalità necessarie per la manipolazione avanzata dei documenti.
## Domande frequenti
### Quali formati supporta GroupDocs.Editor?
GroupDocs.Editor supporta vari formati tra cui DOCX, XLSX, PPTX e altri.
### Posso utilizzare GroupDocs.Editor senza licenza?
 Sì, puoi usarlo con a[prova gratuita](https://releases.groupdocs.com/) o a[licenza temporanea](https://purchase.groupdocs.com/temporary-license/).
### Come posso estrarre risorse specifiche da un documento?
 Puoi estrarre immagini, caratteri e fogli di stile utilizzando i metodi forniti come`Images`, `Fonts` , E`Css`.
### È possibile modificare i collegamenti nell'output HTML?
Sì, puoi modificare i collegamenti esterni specificando prefissi personalizzati per immagini, CSS e caratteri.
### Come posso salvare un documento modificato come file HTML?
 Usa il`Save` metodo del`EditableDocument`class per salvare il documento come file HTML, incluse le sue risorse.