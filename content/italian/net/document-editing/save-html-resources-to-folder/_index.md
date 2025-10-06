---
title: Salva le risorse HTML nella cartella
linktitle: Salva le risorse HTML nella cartella
second_title: API GroupDocs.Editor .NET
description: Scopri come estrarre risorse HTML dai documenti utilizzando Groupdocs.Editor per .NET. Questo tutorial completo fornisce una guida passo passo per gli sviluppatori.
weight: 13
url: /it/net/document-editing/save-html-resources-to-folder/
type: docs
---
# Salva le risorse HTML nella cartella

## introduzione
Groupdocs.Editor per .NET è un potente strumento che consente agli sviluppatori di manipolare e convertire documenti all'interno delle loro applicazioni .NET senza problemi. Che tu abbia bisogno di estrarre risorse HTML da un documento o eseguire attività di modifica avanzate, Groupdocs.Editor semplifica il processo con la sua API intuitiva e un'ampia documentazione.
## Prerequisiti
Prima di immergerti nel tutorial, assicurati di possedere i seguenti prerequisiti:
1. Conoscenza di base di C# e .NET: la familiarità con il linguaggio di programmazione C# e il framework .NET è essenziale da seguire insieme agli esempi.
2.  Groupdocs.Editor per la libreria .NET: scarica e installa Groupdocs.Editor per la libreria .NET dalla[sito web](https://releases.groupdocs.com/editor/net/).
3. Ambiente di sviluppo: configura il tuo ambiente di sviluppo preferito come Visual Studio o qualsiasi altro IDE compatibile.

## Importa spazi dei nomi
Per iniziare, importa gli spazi dei nomi necessari nel tuo progetto C#:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```
##Ora, suddividiamo il processo di salvataggio delle risorse HTML in una cartella utilizzando Groupdocs.Editor per .NET in più passaggi:
## Passaggio 1: inizializza Groupdocs.Editor
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
 Innanzitutto, inizializza il file`Editor`oggetto fornendo il percorso del documento di esempio. In questo esempio stiamo utilizzando un documento Word, quindi specifichiamo`WordProcessingLoadOptions` come tipo di documento.
## Passaggio 2: modifica il documento
```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
 Successivamente, crea un file`EditableDocument` oggetto chiamando il`Edit` metodo del`Editor` oggetto. Ciò consente di eseguire operazioni di modifica sul documento.
## Passaggio 3: estrazione delle risorse
```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
Estrai risorse come immagini, caratteri e fogli di stile dal documento e archiviali nei rispettivi elenchi.
## Passaggio 4: specificare la cartella di output
```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
Definire la cartella di output in cui verranno salvate le risorse estratte. Puoi personalizzare il percorso della cartella secondo le tue esigenze.
## Passaggio 5: salva risorse
```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
Sfoglia ciascuna risorsa immagine, salvala nella cartella di output e visualizza le informazioni pertinenti come nome file, tipo e dimensioni.
```csharp
		foreach (FontResourceBase oneFont in fonts)
		{
			Console.WriteLine("Saving {0} of {1} type",
				oneFont.FilenameWithExtension, oneFont.Type.FormalName);
			oneFont.Save(Path.Combine(outputFolder, oneFont.FilenameWithExtension));
		}
```
Allo stesso modo, salva ogni risorsa di carattere nella cartella di output.
```csharp
		foreach (CssText oneStylesheet in stylesheets)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} encoding",
				oneStylesheet.FilenameWithExtension, oneStylesheet.Type.FormalName, oneStylesheet.Encoding);
			oneStylesheet.Save(Path.Combine(outputFolder, oneStylesheet.FilenameWithExtension));
		}
	}
}
```
Infine, salva ciascun foglio di stile nella cartella di output e completa il processo di modifica.

## Conclusione
In conclusione, Groupdocs.Editor per .NET fornisce una soluzione conveniente per la gestione e la manipolazione dei documenti a livello di codice all'interno delle applicazioni .NET. Seguendo questo tutorial, puoi facilmente estrarre risorse HTML dai documenti e personalizzare il processo in base alle tue esigenze specifiche.
## Domande frequenti
### Groupdocs.Editor è compatibile con altri formati di documenti oltre a Word?
Sì, Groupdocs.Editor supporta un'ampia gamma di formati di documenti tra cui Excel, PowerPoint, PDF e altri.
### Posso integrare Groupdocs.Editor nella mia applicazione web?
Assolutamente, Groupdocs.Editor offre una perfetta integrazione con le applicazioni web sviluppate sul framework .NET.
### Groupdocs.Editor fornisce supporto per i servizi di archiviazione cloud?
Sì, Groupdocs.Editor supporta l'integrazione con i più diffusi servizi di archiviazione cloud come Google Drive, Dropbox e Microsoft OneDrive.
### È disponibile una prova gratuita per Groupdocs.Editor?
Sì, puoi usufruire di una prova gratuita di Groupdocs.Editor dal sito web.
### Come posso ottenere supporto tecnico per Groupdocs.Editor?
Per assistenza tecnica e supporto della community, è possibile visitare il forum Groupdocs.Editor.