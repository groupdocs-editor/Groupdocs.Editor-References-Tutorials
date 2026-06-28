---
date: 2026-03-14
description: Scopri come estrarre immagini da DOCX, convertire DOCX in HTML e salvare
  il documento come HTML utilizzando GroupDocs.Editor per .NET.
linktitle: Extract Images from DOCX – Advanced Editable Document Usage
second_title: GroupDocs.Editor .NET API
title: Estrai immagini da DOCX – Utilizzo avanzato di documenti modificabili
type: docs
url: /it/net/document-editing/advanced-usage-of-editable-documents/
weight: 11
---

 for .NET (latest release)  
**Author:** GroupDocs

Translate:

"**Ultimo aggiornamento:** 2026-03-14  
**Testato con:** GroupDocs.Editor per .NET (ultima release)  
**Autore:** GroupDocs"

Make sure markdown formatting preserved.

Now produce final content with all translations. Ensure placeholders unchanged. Ensure no extra spaces that could affect count? Should be fine.

Let's assemble.# Estrarre immagini da DOCX – Utilizzo avanzato di Documenti modificabili

Se sei uno sviluppatore .NET che desidera **estrarre immagini da DOCX** e migliorare le tue capacità di modifica dei documenti, GroupDocs.Editor per .NET offre una potente suite di strumenti. Questa guida completa ti accompagnerà nell'uso avanzato dei documenti modificabili con GroupDocs.Editor, suddividendo ogni passaggio in dettaglio così potrai sfruttarne appieno il potenziale.

## Risposte rapide
- **Come posso estrarre immagini da un file DOCX?** Usa `EditableDocument.Images` dopo aver caricato il documento con `Editor`.
- **Posso convertire DOCX in HTML con risorse incorporate?** Sì—chiama `EditableDocument.GetEmbeddedHtml()` o `GetContent()` per il markup HTML.
- **Quale metodo salva il documento modificato come HTML?** `EditableDocument.Save(htmlFilePath)` crea un file HTML con una cartella delle risorse.
- **È possibile estrarre i font da un documento Word?** Usa `EditableDocument.Fonts` per recuperare tutte le risorse dei font.
- **È necessaria una licenza per l'uso in produzione?** È richiesta una licenza valida di GroupDocs.Editor; è disponibile una prova gratuita.

## Cos'è **estrarre immagini da docx**?
Estrarre immagini da un file DOCX significa recuperare programmaticamente ogni immagine incorporata nel documento Word in modo da poterla riutilizzare, modificare o archiviare separatamente. GroupDocs.Editor espone la collezione `Images` su un'istanza `EditableDocument`, rendendo questo compito semplice.

## Perché usare GroupDocs.Editor per questo flusso di lavoro?
- **Controllo completo** sulle risorse del documento (immagini, font, CSS) senza gestione manuale dello ZIP.  
- **Conversione senza interruzioni** da DOCX a HTML mantenendo layout e stile.  
- **Facile estrazione delle risorse** per la gestione personalizzata delle immagini, l'incorporamento dei font o la consegna tramite CDN.  
- **Modello di smaltimento robusto** garantisce l'assenza di perdite di memoria nei servizi a lungo termine.

## Prerequisiti
- Visual Studio installato sulla tua macchina di sviluppo.  
- .NET Framework compatibile con GroupDocs.Editor.  
- Libreria GroupDocs.Editor per .NET. Puoi [scaricarla qui](https://releases.groupdocs.com/editor/net/).  
- Una licenza valida di GroupDocs.Editor. Puoi ottenere una [prova gratuita](https://releases.groupdocs.com/) o acquistare una [licenza temporanea](https://purchase.groupdocs.com/temporary-license/).

## Importare gli spazi dei nomi
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

## Passo 1: Creare un'istanza di EditableDocument
Prima, devi creare un'istanza di `EditableDocument` caricando e modificando un documento di input in un formato supportato.

```csharp
string inputFilePath = "YourSampleDocument.docx";
Editor editor = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```

In questo passaggio, carichiamo il documento di input e lo prepariamo per la modifica.

## Come **estrarre immagini da DOCX**?
Di seguito approfondiamo le capacità di estrazione delle risorse, iniziando dalla necessità più comune—ottenere tutte le immagini da un file Word.

## Passo 2: Estrarre le risorse del documento
L'`EditableDocument` contiene varie risorse che possono essere estratte e manipolate. Analizziamole:

### Passo 2.1: Estrarre l'intero documento come HTML
Puoi generare una singola stringa che contiene l'intero documento con tutte le sue risorse incorporate come HTML.

```csharp
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```

### Passo 2.2: Estrarre tutte le immagini *(parola chiave primaria in azione)*
Estrai tutte le immagini dal documento—questo è il fulcro di **estrarre immagini da docx**.

```csharp
List<IImageResource> allImages = beforeEdit.Images;
```

### Passo 2.3: Estrarre tutti i font *(parola chiave secondaria)*
Se hai anche bisogno di **estrarre i font da Word**, usa la seguente chiamata:

```csharp
List<FontResourceBase> allFonts = beforeEdit.Fonts;
```

### Passo 2.4: Estrarre tutti i fogli di stile
Estrai tutti i fogli di stile in formato testuale.

```csharp
List<CssText> allStylesheets = beforeEdit.Css;
```

### Passo 2.5: Raccogliere tutte le risorse
Raccogli tutte le risorse in una singola chiamata.

```csharp
List<IHtmlResource> allResources = beforeEdit.AllResources;
```

Questo include immagini, font e fogli di stile.

### Passo 2.6: Ottenere il markup HTML
Ottieni il markup HTML del documento senza risorse incorporate.

```csharp
string htmlMarkup = beforeEdit.GetContent();
```

## Come **convertire docx in html** con gestione personalizzata?
A volte è necessario regolare i collegamenti esterni affinché puntino ai tuoi gestori di risorse.

## Passo 3: Regolare i collegamenti esterni
### Passo 3.1: Preparare prefissi personalizzati
Prepara i prefissi che verranno aggiunti ai collegamenti esterni originali.

```csharp
string customImagesRequesthandlerUri = "http://example.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://example.com/CssHandler/id=";
string customFontsRequesthandlerUri = "http://example.com/FontsHandler/id=";
```

### Passo 3.2: Generare markup HTML con prefisso
Genera il markup HTML con i collegamenti regolati.

```csharp
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```

### Passo 3.3: Ottenere contenuto HTML solo corpo
Alcuni editor WYSIWYG gestiscono solo markup HTML puro senza intestazioni.

```csharp
string onlyBodyContent = beforeEdit.GetBodyContent();
```

### Passo 3.4: Contenuto solo corpo con prefisso
Genera contenuto solo corpo con prefissi immagine personalizzati.

```csharp
string prefixedBodyContent = beforeEdit.GetBodyContent(customImagesRequesthandlerUri);
```

### Passo 3.5: Estrarre i fogli di stile
Estrai i fogli di stile utilizzati nel documento.

```csharp
List<string> stylesheets = beforeEdit.GetCssContent();
```

### Passo 3.6: Fogli di stile con prefisso
Estrai i fogli di stile con prefissi personalizzati.

```csharp
List<string> prefixedStylesheets = beforeEdit.GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri);
```

## Come **salvare il documento come html** correttamente?
## Passo 4: Salvare il documento come HTML
Salva il documento modificato come file HTML, includendo le sue risorse.

```csharp
string htmlFilePath = Path.Combine("output", Path.GetFileNameWithoutExtension(inputFilePath) + ".html");
beforeEdit.Save(htmlFilePath);
```

Questo metodo crea una directory separata per le risorse come fogli di stile, immagini e font.

## Passo 5: Smaltimento di EditableDocument
`EditableDocument` implementa `IDisposable` e fornisce la possibilità di verificare se l'istanza è stata smaltita.

```csharp
Console.WriteLine("EditableDocument is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");
```

### Passo 5.1 Gestione dell'evento Dispose
Puoi anche iscriverti all'evento di smaltimento.

```csharp
EventHandler someMethod = delegate { Console.WriteLine("Disposing event was spotted!"); };
beforeEdit.Disposed += someMethod;
```

## Passo 6: Creare EditableDocument da HTML
Crea un'istanza di `EditableDocument` da un documento HTML.

### Passo 6.1: Da file HTML

```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
```

### Passo 6.2: Da markup HTML

```csharp
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);
```

Queste istanze (`afterEditFromFile` e `afterEditFromMarkup`) sono identiche all'originale (`beforeEdit`).

## Passo 7: Smaltimento manuale
Smaltisci manualmente le tue istanze di `EditableDocument`.

```csharp
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```

Ciò garantisce una corretta pulizia delle risorse.

## Problemi comuni e soluzioni
- **Immagini non visualizzate dopo l'estrazione:** Verifica che il documento contenga effettivamente immagini incorporate e che tu stia accedendo a `beforeEdit.Images` dopo aver chiamato `Edit`.  
- **Font mancanti nell'output HTML:** Assicurati di chiamare `GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri)` per incorporare correttamente gli URL dei font.  
- **Stringhe HTML grandi che causano pressione sulla memoria:** Usa `GetContent()` per il markup senza risorse incorporate e servi immagini/CSS da file separati.

## Domande frequenti
**D: Quali formati supporta GroupDocs.Editor?**  
R: GroupDocs.Editor supporta DOCX, XLSX, PPTX e molti altri formati office popolari.

**D: Posso usare GroupDocs.Editor senza licenza?**  
R: Sì, puoi usarlo con una [prova gratuita](https://releases.groupdocs.com/) o una [licenza temporanea](https://purchase.groupdocs.com/temporary-license/).

**D: Come estraggo risorse specifiche da un documento?**  
R: Usa le collezioni `Images`, `Fonts` e `Css` sull'istanza `EditableDocument`.

**D: È possibile regolare i collegamenti nell'output HTML?**  
R: Sì, passa prefissi URI personalizzati a `GetContent` o `GetBodyContent` per riscrivere i collegamenti a immagini, CSS e font.

**D: Come salvo un documento modificato come file HTML?**  
R: Chiama il metodo `Save` sull'istanza `EditableDocument`, fornendo un percorso file che termina con `.html`.

---

**Ultimo aggiornamento:** 2026-03-14  
**Testato con:** GroupDocs.Editor per .NET (ultima release)  
**Autore:** GroupDocs