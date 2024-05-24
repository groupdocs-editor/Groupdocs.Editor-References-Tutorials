---
title: Dokument erstellen
linktitle: Dokument erstellen
second_title: GroupDocs.Editor .NET API
description: Erfahren Sie in diesem umfassenden Schritt-für-Schritt-Tutorial, wie Sie Word-, Excel-, PowerPoint-, E-Book- und E-Mail-Dokumente mit GroupDocs.Editor für .NET bearbeiten.
type: docs
weight: 10
url: /de/net/document-editing/create-document/
---
## Einführung
Sind Sie es leid, sich mit dem programmgesteuerten Bearbeiten verschiedener Dokumenttypen herumzuschlagen? GroupDocs.Editor für .NET vereinfacht diesen Vorgang. Mit diesem leistungsstarken Tool können Entwickler verschiedene Dokumentformate wie Word, Excel, PowerPoint, E-Books und E-Mails ganz einfach bearbeiten. In diesem Tutorial erfahren Sie ausführlich, wie Sie mit GroupDocs.Editor für .NET Dokumente erstellen und bearbeiten. Wir unterteilen den Vorgang in leicht verständliche Schritte, sodass er auch für Anfänger leicht verständlich ist.
## Voraussetzungen
Bevor wir beginnen, stellen Sie sicher, dass Sie über Folgendes verfügen:
- Visual Studio ist auf Ihrem Computer installiert.
- .NET Framework (4.0 oder höher).
-  GroupDocs.Editor für .NET-Bibliothek. Sie können es herunterladen von[Hier](https://releases.groupdocs.com/editor/net/).
- Grundkenntnisse der C#-Programmierung.
## Namespaces importieren
Importieren wir zunächst die erforderlichen Namespaces. Dadurch werden die erforderlichen Klassen und Methoden in unserer Anwendung zugänglich.
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using System.IO;
```
## Schritt 1: Einrichten des Streams
Zunächst müssen wir einen Speicherstream einrichten, der als Platzhalter für den Dokumentinhalt dient.
```csharp
Stream memoryStream = Stream.Null;
```
## Schritt 2: Callback-Funktion zum Speichern des Dokuments
Definieren Sie als Nächstes eine Rückruffunktion, die den neuen Dokumentstrom speichert. Diese Funktion ist für die Handhabung der Ausgabe des Dokumentbearbeitungsprozesses von entscheidender Bedeutung.
```csharp
void SaveNewDocument(Stream resultStream)
{
    memoryStream = resultStream;
}
```
## Schritt 3: Erstellen und Bearbeiten eines Textverarbeitungsdokuments
 Lassen Sie uns nun ein Word-Dokument erstellen und bearbeiten. Wir beginnen mit der Erstellung eines neuen`Editor` Instanz für Textverarbeitungsdokumente und bearbeiten Sie sie mit den Standardoptionen.
### Erstellen und Bearbeiten mit Standardoptionen
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    EditableDocument defaultWordProcessingDoc = editor.Edit();
}
```
### Erstellen und Bearbeiten mit benutzerdefinierten Optionen
Für mehr Kontrolle können wir Optionen wie das Deaktivieren der Seitennummerierung und das Extrahieren eingebetteter Schriftarten angeben.
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    WordProcessingEditOptions wordProcessingEditOptions = new WordProcessingEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true,
        FontExtraction = FontExtractionOptions.ExtractAllEmbedded
    };
    EditableDocument editableWordProcessingDocument = editor.Edit(wordProcessingEditOptions);
}
```
## Schritt 4: Erstellen und Bearbeiten eines Tabellenkalkulationsdokuments
Auf ähnliche Weise können wir ein Excel-Dokument erstellen und bearbeiten. So geht’s:
### Erstellen und Bearbeiten mit Standardoptionen
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    EditableDocument defaultEditableSpreadsheetDocument = editor.Edit();
}
```
### Erstellen und Bearbeiten mit benutzerdefinierten Optionen
 Um bestimmte Arbeitsblätter anzusprechen oder versteckte auszuschließen, verwenden wir`SpreadsheetEditOptions`.
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    SpreadsheetEditOptions spreadsheetEditOptions = new SpreadsheetEditOptions
    {
        WorksheetIndex = 0,
        ExcludeHiddenWorksheets = true
    };
    EditableDocument editableSpreadsheetDocument = editor.Edit(spreadsheetEditOptions);
}
```
## Schritt 5: Erstellen und Bearbeiten eines Präsentationsdokuments
PowerPoint-Präsentationen werden ebenfalls unterstützt. Sehen wir uns an, wie man damit umgeht.
### Erstellen und Bearbeiten mit Standardoptionen
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    EditableDocument defaultEditablePresentationDocument = editor.Edit();
}
```
### Erstellen und Bearbeiten mit benutzerdefinierten Optionen
Sie können Ihre Bearbeitungen anpassen, indem Sie Optionen angeben, beispielsweise welche Folie angezeigt werden soll und ob ausgeblendete Folien einbezogen werden sollen.
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    PresentationEditOptions presentationEditOptions = new PresentationEditOptions
    {
        ShowHiddenSlides = false,
        SlideNumber = 0
    };
    EditableDocument editablePresentationDocument = editor.Edit(presentationEditOptions);
}
```
## Schritt 6: Erstellen und Bearbeiten eines E-Book-Dokuments
GroupDocs.Editor ermöglicht auch die Bearbeitung von E-Book-Formaten wie EPUB. So können Sie vorgehen.
### Erstellen und Bearbeiten mit Standardoptionen
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EditableDocument defaultEditableEbookDocument = editor.Edit();
}
```
### Erstellen und Bearbeiten mit benutzerdefinierten Optionen
Passen Sie die Bearbeitung Ihres E-Books an, indem Sie Seitennummerierung und Sprachinformationen aktivieren oder deaktivieren.
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EbookEditOptions ebookEditOptions = new EbookEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true
    };
    EditableDocument editableEbookDocument = editor.Edit(ebookEditOptions);
}
```
## Schritt 7: Erstellen und Bearbeiten eines E-Mail-Dokuments
Abschließend schauen wir uns an, wie man E-Mail-Dokumente bearbeitet. Dazu gehören Formate wie EML.
### Erstellen und Bearbeiten mit Standardoptionen
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EditableDocument defaultEditableEmailDocument = editor.Edit();
}
```
### Erstellen und Bearbeiten mit benutzerdefinierten Optionen
Geben Sie Ausgabeoptionen für E-Mail-Nachrichten an, um den Bearbeitungsvorgang zu steuern.
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EmailEditOptions emailEditOptions = new EmailEditOptions
    {
        MailMessageOutput = MailMessageOutput.All
    };
    EditableDocument editableEmailDocument = editor.Edit(emailEditOptions);
}
```
## Schritt 8: Abschließen des Vorgangs
Nach dem Bearbeiten der Dokumente ist es wichtig, den Speicherstrom ordnungsgemäß zu entsorgen, um Ressourcen freizugeben.
```csharp
memoryStream.Dispose();
System.Console.WriteLine("CreateDocument routine has successfully finished");
```
## Abschluss
GroupDocs.Editor für .NET ist ein vielseitiges und leistungsstarkes Tool, das die programmgesteuerte Bearbeitung verschiedener Dokumenttypen vereinfacht. Wenn Sie dieser Schritt-für-Schritt-Anleitung folgen, können Sie Dokumente ganz einfach erstellen und bearbeiten, egal ob es sich um Textverarbeitungsdateien, Tabellenkalkulationen, Präsentationen, E-Books oder E-Mails handelt. Weitere erweiterte Funktionen und Anpassungsoptionen finden Sie in der GroupDocs.Editor-Dokumentation.
## Häufig gestellte Fragen
### Welche Dokumenttypen kann ich mit GroupDocs.Editor für .NET bearbeiten?
Sie können eine breite Palette von Dokumenten bearbeiten, darunter Textverarbeitungsdokumente, Tabellenkalkulationen, Präsentationen, E-Books und E-Mails.
### Ist es möglich, die Bearbeitungsoptionen anzupassen?
Ja, GroupDocs.Editor für .NET ermöglicht eine umfassende Anpassung durch verschiedene, für jeden Dokumenttyp spezifische Bearbeitungsoptionen.
### Wie gehe ich mit der Ausgabe der bearbeiteten Dokumente um?
Sie können eine Rückruffunktion verwenden, um den bearbeiteten Dokumentstrom am gewünschten Speicherort zu speichern.
### Benötige ich eine Lizenz, um GroupDocs.Editor für .NET zu verwenden?
 Ja, Sie können eine Lizenz erhalten bei[Hier](https://purchase.groupdocs.com/buy)Es besteht auch die Möglichkeit einer temporären Lizenz.
### Wo finde ich ausführlichere Dokumentation?
 Eine ausführliche Dokumentation finden Sie auf der[GroupDocs.Editor für .NET-Dokumentationsseite](https://reference.groupdocs.com/editor/net/).