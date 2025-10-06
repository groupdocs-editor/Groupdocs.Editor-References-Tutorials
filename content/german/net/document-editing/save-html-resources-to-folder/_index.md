---
title: HTML-Ressourcen im Ordner speichern
linktitle: HTML-Ressourcen im Ordner speichern
second_title: GroupDocs.Editor .NET API
description: Erfahren Sie, wie Sie mit Groupdocs.Editor für .NET HTML-Ressourcen aus Dokumenten extrahieren. Dieses umfassende Tutorial bietet Entwicklern eine Schritt-für-Schritt-Anleitung.
weight: 13
url: /de/net/document-editing/save-html-resources-to-folder/
type: docs
---
# HTML-Ressourcen im Ordner speichern

## Einführung
Groupdocs.Editor für .NET ist ein leistungsstarkes Tool, mit dem Entwickler Dokumente in ihren .NET-Anwendungen nahtlos bearbeiten und konvertieren können. Egal, ob Sie HTML-Ressourcen aus einem Dokument extrahieren oder erweiterte Bearbeitungsaufgaben ausführen müssen, Groupdocs.Editor vereinfacht den Vorgang mit seiner intuitiven API und umfassenden Dokumentation.
## Voraussetzungen
Bevor Sie mit dem Lernprogramm beginnen, stellen Sie sicher, dass Sie die folgenden Voraussetzungen erfüllen:
1. Grundkenntnisse in C# und .NET: Um den Beispielen folgen zu können, sind Kenntnisse der Programmiersprache C# und des .NET-Frameworks unbedingt erforderlich.
2.  Groupdocs.Editor für .NET-Bibliothek: Laden Sie die Groupdocs.Editor für .NET-Bibliothek herunter und installieren Sie sie von der[Webseite](https://releases.groupdocs.com/editor/net/).
3. Entwicklungsumgebung: Richten Sie Ihre bevorzugte Entwicklungsumgebung ein, beispielsweise Visual Studio oder eine andere kompatible IDE.

## Namespaces importieren
Importieren Sie zunächst die erforderlichen Namespaces in Ihr C#-Projekt:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```
##Lassen Sie uns nun den Vorgang zum Speichern von HTML-Ressourcen in einem Ordner mit Groupdocs.Editor für .NET in mehrere Schritte aufteilen:
## Schritt 1: Groupdocs.Editor initialisieren
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
 Initialisieren Sie zunächst den`Editor`Objekt, indem Sie den Pfad zu Ihrem Beispieldokument angeben. In diesem Beispiel verwenden wir ein Word-Dokument, daher geben wir`WordProcessingLoadOptions` als Dokumenttyp.
## Schritt 2: Dokument bearbeiten
```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
 Erstellen Sie als Nächstes eine`EditableDocument` Objekt durch Aufrufen des`Edit` Methode der`Editor` Objekt. Dadurch können Sie Bearbeitungsvorgänge am Dokument durchführen.
## Schritt 3: Ressourcen extrahieren
```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
Extrahieren Sie Ressourcen wie Bilder, Schriftarten und Stylesheets aus dem Dokument und speichern Sie sie in entsprechenden Listen.
## Schritt 4: Ausgabeordner angeben
```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
Definieren Sie den Ausgabeordner, in dem die extrahierten Ressourcen gespeichert werden. Sie können den Ordnerpfad nach Bedarf anpassen.
## Schritt 5: Ressourcen sparen
```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
Durchlaufen Sie jede Bildressource, speichern Sie sie im Ausgabeordner und zeigen Sie relevante Informationen wie Dateiname, Typ und Abmessungen an.
```csharp
		foreach (FontResourceBase oneFont in fonts)
		{
			Console.WriteLine("Saving {0} of {1} type",
				oneFont.FilenameWithExtension, oneFont.Type.FormalName);
			oneFont.Save(Path.Combine(outputFolder, oneFont.FilenameWithExtension));
		}
```
Speichern Sie auf ähnliche Weise jede Schriftartressource im Ausgabeordner.
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
Speichern Sie abschließend jedes Stylesheet im Ausgabeordner und schließen Sie den Bearbeitungsvorgang ab.

## Abschluss
Zusammenfassend lässt sich sagen, dass Groupdocs.Editor für .NET eine praktische Lösung für die programmgesteuerte Verwaltung und Bearbeitung von Dokumenten innerhalb von .NET-Anwendungen bietet. Mit diesem Tutorial können Sie ganz einfach HTML-Ressourcen aus Dokumenten extrahieren und den Prozess an Ihre spezifischen Anforderungen anpassen.
## Häufig gestellte Fragen
### Ist Groupdocs.Editor mit anderen Dokumentformaten außer Word kompatibel?
Ja, Groupdocs.Editor unterstützt eine breite Palette von Dokumentformaten, darunter Excel, PowerPoint, PDF und mehr.
### Kann ich Groupdocs.Editor in meine Webanwendung integrieren?
Absolut, Groupdocs.Editor bietet eine nahtlose Integration mit Webanwendungen, die auf dem .NET-Framework entwickelt wurden.
### Bietet Groupdocs.Editor Unterstützung für Cloud-Speicherdienste?
Ja, Groupdocs.Editor unterstützt die Integration mit beliebten Cloud-Speicherdiensten wie Google Drive, Dropbox und Microsoft OneDrive.
### Gibt es eine kostenlose Testversion für Groupdocs.Editor?
Ja, Sie können auf der Website eine kostenlose Testversion von Groupdocs.Editor herunterladen.
### Wie kann ich technischen Support für Groupdocs.Editor erhalten?
Für technische Hilfe und Community-Support können Sie das Groupdocs.Editor-Forum besuchen.