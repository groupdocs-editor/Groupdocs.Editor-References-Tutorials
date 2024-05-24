---
title: Einführung in GroupDocs.Editor für .NET
linktitle: Einführung in GroupDocs.Editor für .NET
second_title: GroupDocs.Editor .NET API
description: Erfahren Sie in dieser ausführlichen Schritt-für-Schritt-Anleitung, wie Sie mit GroupDocs.Editor für .NET Dokumente programmgesteuert bearbeiten.
type: docs
weight: 12
url: /de/net/document-editing/introduction-groupdocs-editor/
---
## Einführung 
Wenn Sie Entwickler sind und Dokumentbearbeitungsfunktionen nahtlos in Ihre .NET-Anwendungen integrieren möchten, ist GroupDocs.Editor für .NET ein leistungsstarkes Tool, das Sie in Betracht ziehen sollten. Diese vielseitige Bibliothek ermöglicht Ihnen das programmgesteuerte Laden, Bearbeiten und Speichern verschiedener Dokumentformate. Egal, ob Sie Word-Dokumente, PDFs oder HTML-Dateien verarbeiten müssen, GroupDocs.Editor vereinfacht den Prozess und macht ihn effizient und unkompliziert. In diesem Tutorial erkunden wir die Grundlagen der Verwendung von GroupDocs.Editor für .NET und führen Sie Schritt für Schritt durch ein praktisches Beispiel.
## Voraussetzungen
Bevor wir mit der Implementierung beginnen, stellen Sie sicher, dass Sie die folgenden Voraussetzungen erfüllen:
- Entwicklungsumgebung: Visual Studio 2017 oder höher.
- .NET Framework: .NET Framework 4.6.1 oder höher.
-  GroupDocs.Editor für .NET: Sie können[herunterladen](https://releases.groupdocs.com/editor/net/) es von der Site.
-  Lizenz: Eine gültige Lizenz oder eine[vorläufige Lizenz](https://purchase.groupdocs.com/temporary-license/) von GroupDocs.
## Namespaces importieren
Um GroupDocs.Editor für .NET verwenden zu können, müssen Sie die erforderlichen Namespaces importieren. Diese Namespaces bieten Zugriff auf die Klassen und Methoden, die für die Dokumentbearbeitung erforderlich sind.
```csharp
using System;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```

In diesem Abschnitt unterteilen wir den Prozess in überschaubare Schritte und stellen sicher, dass Sie jeden Teil des Arbeitsablaufs verstehen.
## Schritt 1: Holen Sie sich einen Pfad zur Eingabedatei
Zuerst müssen Sie den Pfad zu dem Dokument angeben, das Sie bearbeiten möchten. Nehmen wir für dieses Beispiel an, Sie haben eine DOCX-Datei mit dem Namen „Ihr Beispieldokument.docx“.
```csharp
string inputFilePath = "Your Sample Document.docx";
```
## Schritt 2: Instanziieren des Editorobjekts
 Erstellen Sie als nächstes eine Instanz des`Editor` Klasse durch Laden der Eingabedatei. Dieser Schritt initialisiert das Dokument für die weitere Verarbeitung.
```csharp
using (GroupDocs.Editor.Editor editor = new Editor(inputFilePath))
{
    //Nachfolgende Schritte werden in diesem Block verschachtelt
}
```
## Schritt 3: Öffnen Sie das Dokument zum Bearbeiten
 Um das Dokument zu bearbeiten, besorgen Sie sich eine Zwischen`EditableDocument` Instanz. Mit diesem Objekt können Sie den Dokumentinhalt und die zugehörigen Ressourcen bearbeiten.
```csharp
EditableDocument beforeEdit = editor.Edit();
```
## Schritt 4: Dokumentinhalte und Ressourcen abrufen
Extrahieren Sie den Hauptinhalt, Bilder, Schriftarten und Stylesheets aus dem bearbeitbaren Dokument. Diese Informationen sind für alle Änderungen unerlässlich.
```csharp
string content = beforeEdit.GetContent();
var images = beforeEdit.Images;
var fonts = beforeEdit.Fonts;
var stylesheets = beforeEdit.Css;
```
### Schritt 4.1: Dokument als einzelne Base64-codierte Zeichenfolge abrufen
Sie können den gesamten Dokumentinhalt auch als einzelne Base64-codierte Zeichenfolge abrufen, die alle Ressourcen enthält.
```csharp
string allEmbeddedInsideString = beforeEdit.GetEmbeddedHtml();
```
### Schritt 4.2: Inhalt bearbeiten
Lassen Sie uns zu Demonstrationszwecken den Dokumentinhalt ändern, indem wir einen bestimmten Text ersetzen.
```csharp
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
```
## Schritt 5: Erstellen Sie eine neue EditableDocument-Instanz
 Nachdem Sie den Inhalt bearbeitet haben, erstellen Sie eine neue`EditableDocument` Instanz mit dem geänderten Inhalt.
```csharp
EditableDocument afterEdit = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```
## Schritt 6: Speichern Sie das bearbeitete Dokument
Speichern Sie nun das bearbeitete Dokument im gewünschten Ausgabeformat. In diesem Beispiel speichern wir es als RTF-Datei.
### Schritt 6.1: Bereiten Sie den Ausgabepfad vor
Geben Sie den Pfad an, in dem Sie das Ausgabedokument speichern möchten.
```csharp
string outputPath = Path.Combine("Output Directory Path", Path.GetFileNameWithoutExtension(inputFilePath) + ".rtf");
```
### Schritt 6.2: Speicheroptionen vorbereiten
Definieren Sie die Speicheroptionen und geben Sie das Format an, in dem Sie das Dokument speichern möchten.
```csharp
Options.WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
```
### Schritt 6.3: Unter Pfad speichern
Speichern Sie das bearbeitete Dokument im angegebenen Pfad.
```csharp
editor.Save(afterEdit, outputPath, saveOptions);
```
### Schritt 6.4: In einem Stream speichern
Alternativ können Sie das Ausgabedokument in einem beliebigen beschreibbaren Stream speichern.
```csharp
using (MemoryStream ms = new MemoryStream())
{
    editor.Save(afterEdit, ms, saveOptions);
}
```
## Schritt 7: Entsorgen Sie die Editor- und EditableDocument-Instanzen
 Zum Schluss säubern Sie, indem Sie das`EditableDocument` Instanzen und die`Editor` Objekt, um Ressourcen freizugeben.
```csharp
beforeEdit.Dispose();
afterEdit.Dispose();
editor.Dispose();
```

## Abschluss
GroupDocs.Editor für .NET macht es unglaublich einfach, Dokumentbearbeitungsfunktionen in Ihre Anwendungen zu integrieren. Wenn Sie die in diesem Tutorial beschriebenen Schritte befolgen, können Sie Dokumente mit minimalem Aufwand programmgesteuert laden, bearbeiten und speichern. Egal, ob Sie Word-Dokumente, PDFs oder andere Formate verarbeiten müssen, GroupDocs.Editor bietet eine robuste Lösung für Ihre Anforderungen an die Dokumentverarbeitung.
## Häufig gestellte Fragen
### Kann ich PDF-Dateien mit GroupDocs.Editor für .NET bearbeiten?
Ja, GroupDocs.Editor für .NET unterstützt das Bearbeiten von PDF-Dateien sowie vielen anderen Formaten wie DOCX, HTML und mehr.
### Wie erhalte ich eine temporäre Lizenz für GroupDocs.Editor für .NET?
 Eine vorläufige Lizenz erhalten Sie bei der[GroupDocs-Website](https://purchase.groupdocs.com/temporary-license/).
### Welche Dateiformate werden von GroupDocs.Editor für .NET unterstützt?
GroupDocs.Editor für .NET unterstützt verschiedene Formate, darunter unter anderem DOCX, PDF, HTML und RTF.
### Ist es möglich, GroupDocs.Editor in den Cloud-Speicher zu integrieren?
Ja, Sie können GroupDocs.Editor in verschiedene Cloud-Speicherlösungen integrieren, um Ihre Dokumente zu verwalten.
### Wo finde ich die Dokumentation für GroupDocs.Editor für .NET?
Die Dokumentation ist verfügbar[Hier](https://reference.groupdocs.com/editor/net/).