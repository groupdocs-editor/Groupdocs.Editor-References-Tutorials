---
title: Dokument speichern
linktitle: Dokument speichern
second_title: GroupDocs.Editor .NET API
description: Bearbeiten und speichern Sie Dokumente mühelos mit GroupDocs.Editor für .NET. Diese Schritt-für-Schritt-Anleitung vereinfacht den Vorgang für Entwickler.
type: docs
weight: 14
url: /de/net/document-editing/save-document/
---
## Einführung
Möchten Sie mühelos Dokumente mit GroupDocs.Editor für .NET bearbeiten und speichern? Dann sind Sie hier richtig! Dieses Tutorial führt Sie Schritt für Schritt durch den Vorgang und stellt sicher, dass Sie Ihre Dokumente problemlos verwalten können. Egal, ob Sie ein erfahrener Entwickler oder ein Anfänger sind, unser Leitfaden bietet Ihnen alle Informationen, die Sie für den Einstieg benötigen.
## Voraussetzungen
Bevor Sie mit dem Lernprogramm beginnen, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:
- Entwicklungsumgebung: Visual Studio auf Ihrem Computer installiert.
- .NET Framework: Stellen Sie sicher, dass Sie .NET Framework 4.6.1 oder höher haben.
-  GroupDocs.Editor für .NET: Laden Sie die neueste Version herunter[Hier](https://releases.groupdocs.com/editor/net/).
- Grundlegende C#-Kenntnisse: Kenntnisse in der C#-Programmierung sind unbedingt erforderlich.
## Namespaces importieren
Um GroupDocs.Editor in Ihrem .NET-Projekt zu verwenden, müssen Sie die erforderlichen Namespaces importieren. So gehen Sie dabei vor:
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
Nachdem wir nun unsere Umgebung eingerichtet und die erforderlichen Namespaces importiert haben, stürzen wir uns auf die Schritte, die zum Laden, Bearbeiten und Speichern eines Dokuments mit GroupDocs.Editor für .NET erforderlich sind.
## Schritt 1: Dokument laden
Zuerst müssen wir das Dokument laden, das wir bearbeiten möchten. GroupDocs.Editor macht diesen Vorgang unkompliziert. So können Sie es tun:

```csharp
string inputFilePath = "Your Sample Document";
Editor editor = new Editor(inputFilePath, delegate { return new Options.WordProcessingLoadOptions(); });
EditableDocument defaultWordProcessingDoc = editor.Edit();
```
 In diesem Schritt geben wir den Pfad zum Dokument an, das wir bearbeiten möchten, und erstellen eine Instanz des`Editor` Klasse. Die`Edit` wird dann die -Methode aufgerufen, um das Dokument in ein`EditableDocument` Objekt.
## Schritt 2: Ändern des Dokuments
Nachdem das Dokument geladen wurde, ist es an der Zeit, einige Änderungen vorzunehmen. Da wir keinen WYSIWYG-Editor angeschlossen haben, simulieren wir den Bearbeitungsprozess im Code.

```csharp
string allEmbeddedInsideString = defaultWordProcessingDoc.GetEmbeddedHtml();
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
EditableDocument editedDoc = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```
 Hier holen wir uns den eingebetteten HTML-Inhalt des Dokuments, führen eine einfache Textersetzung durch und erstellen ein neues`EditableDocument`Instanz aus dem geänderten HTML.
## Schritt 3: Speichern Sie das Dokument
Nach der Bearbeitung des Dokuments besteht der letzte Schritt darin, es zu speichern. GroupDocs.Editor bietet mehrere Optionen zum Speichern des Dokuments in verschiedenen Formaten.
## Als RTF speichern
```csharp
string outputRtfPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.rtf");
WordProcessingSaveOptions rtfSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
editor.Save(editedDoc, outputRtfPath, rtfSaveOptions);
```
## Als DOCM speichern
```csharp
string outputDocmPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.docm");
WordProcessingSaveOptions docmSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm);
using (FileStream outputStream = File.Create(outputDocmPath))
{
    editor.Save(editedDoc, outputStream, docmSaveOptions);
}
```
## Als Nur-Text speichern
```csharp
string outputTxtPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.txt");
TextSaveOptions textSaveOptions = new TextSaveOptions
{
    Encoding = System.Text.Encoding.UTF8,
    PreserveTableLayout = true
};
editor.Save(editedDoc, outputTxtPath, textSaveOptions);
```
## Schritt 4: Bereinigen
 Schließlich ist es wichtig, die`EditableDocument` Und`Editor` Instanzen, um Ressourcen freizugeben.
```csharp
editedDoc.Dispose();
defaultWordProcessingDoc.Dispose();
editor.Dispose();
```
Wenn Sie diese Schritte befolgen, können Sie Dokumente mit GroupDocs.Editor für .NET effizient laden, bearbeiten und speichern. Dieses leistungsstarke Tool bietet Flexibilität und Benutzerfreundlichkeit und macht die Dokumentenverwaltung zum Kinderspiel.
## Abschluss
Das programmgesteuerte Bearbeiten und Speichern von Dokumenten war mit GroupDocs.Editor für .NET noch nie so einfach. Diese Anleitung führt Sie durch den gesamten Prozess, vom Laden eines Dokuments bis zum Speichern in verschiedenen Formaten. Mit GroupDocs.Editor haben Sie eine vielseitige und robuste Lösung zur Hand, die den Dokumentbearbeitungsprozess vereinfacht.
## Häufig gestellte Fragen
### Welche Dateiformate unterstützt GroupDocs.Editor?
GroupDocs.Editor unterstützt verschiedene Dateiformate, darunter DOCX, RTF, TXT und viele mehr. Eine vollständige Liste finden Sie unter[Dokumentation](https://reference.groupdocs.com/editor/net/).
### Kann ich GroupDocs.Editor vor dem Kauf ausprobieren?
 Ja, Sie können eine[Kostenlose Testphase](https://releases.groupdocs.com/) um die Funktionen von GroupDocs.Editor zu testen.
### Gibt es Support, wenn ich auf Probleme stoße?
 Auf jeden Fall! Sie können die[Hilfeforum](https://forum.groupdocs.com/c/editor/20) für Hilfe bei allen auftretenden Problemen.
### Wie erhalte ich eine vorläufige Lizenz?
 Sie können eine[vorläufige Lizenz](https://purchase.groupdocs.com/temporary-license/) zu Auswertungszwecken.
### Wo kann ich die Vollversion von GroupDocs.Editor kaufen?
 Sie können die Vollversion kaufen[Hier](https://purchase.groupdocs.com/buy).