---
title: Arbeiten mit Nur-Text-Dokumenten
linktitle: Arbeiten mit Nur-Text-Dokumenten
second_title: GroupDocs.Editor .NET API
description: Lernen Sie mit unserer Schritt-für-Schritt-Anleitung, reine Textdokumente mit GroupDocs.Editor für .NET zu bearbeiten. Vereinfachen Sie Ihren .NET-Dokumentbearbeitungsprozess.
weight: 15
url: /de/net/document-processing/work-plain-text-documents/
---

# Arbeiten mit Nur-Text-Dokumenten

## Einführung
Möchten Sie Ihren Dokumentbearbeitungsprozess in .NET optimieren? Dann sind Sie bei GroupDocs.Editor für .NET genau richtig! Mit dieser leistungsstarken API können Sie eine Vielzahl von Dokumentformaten problemlos bearbeiten. In diesem Tutorial führen wir Sie durch den Prozess der Arbeit mit einfachen Textdokumenten mithilfe von GroupDocs.Editor für .NET. Am Ende sind Sie in der Lage, Textdokumente wie ein Profi zu bearbeiten. Bereit, loszulegen? Dann legen wir los!
## Voraussetzungen
Bevor wir beginnen, müssen Sie einige Dinge vorbereitet haben:
- .NET-Entwicklungsumgebung: Stellen Sie sicher, dass Sie eine funktionierende .NET-Entwicklungsumgebung eingerichtet haben. Visual Studio ist eine beliebte Wahl.
-  GroupDocs.Editor für .NET: Laden Sie herunter und installieren Sie den[GroupDocs.Editor für .NET](https://releases.groupdocs.com/editor/net/).
- Grundlegende C#-Kenntnisse: Wenn Sie mit der Programmiersprache C# vertraut sind, können Sie den Beispielen leichter folgen.
- Texteditor: Jeder Texteditor ist geeignet, aufgrund seiner Funktionen und Benutzerfreundlichkeit wird jedoch Visual Studio Code empfohlen.
## Namespaces importieren
Um GroupDocs.Editor für .NET verwenden zu können, müssen Sie die erforderlichen Namespaces in Ihr Projekt importieren. Dadurch wird sichergestellt, dass alle erforderlichen Klassen und Methoden zur Verwendung verfügbar sind.
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```
Lassen Sie uns den Prozess in überschaubare Schritte aufteilen. Folgen Sie uns, während wir Sie durch jede Phase der Bearbeitung von Nur-Text-Dokumenten mit GroupDocs.Editor für .NET führen.
## Schritt 1: Holen Sie sich einen Pfad zur Eingabe-TXT-Datei
Zuerst müssen Sie den Pfad zur TXT-Eingabedatei angeben. Dies kann ein Pfad zu einer lokalen Datei oder ein Stream sein, der den Dateiinhalt enthält.
```csharp
string inputFilePath = "YourSampleDocument.txt";
```
## Schritt 2: Erstellen einer Editor-Instanz
 Erstellen Sie als nächstes eine Instanz des`Editor` Klasse. Diese Klasse ist für das Laden und Bearbeiten von Dokumenten zuständig. Zu diesem Zeitpunkt sind keine Ladeoptionen erforderlich.
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## Schritt 3: TXT-Bearbeitungsoptionen erstellen
Legen Sie nun die TXT-Bearbeitungsoptionen fest. Mit diesen Optionen können Sie festlegen, wie der Textinhalt bei der Bearbeitung verarbeitet werden soll.
```csharp
    TextEditOptions editOptions = new TextEditOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        RecognizeLists = true,
        LeadingSpaces = TextLeadingSpacesOptions.ConvertToIndent,
        TrailingSpaces = TextTrailingSpacesOptions.Trim
    };
```
## Schritt 4: Erstellen Sie eine EditableDocument-Instanz
 Erstellen Sie mit den festgelegten Bearbeitungsoptionen eine`EditableDocument` Instanz. Dies stellt das Dokument in einem bearbeitbaren Format dar.
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## Schritt 5: Bearbeiten des Dokumentinhalts
Rufen Sie den ursprünglichen Textinhalt ab und nehmen Sie die gewünschten Änderungen vor. In diesem Beispiel ersetzen wir das Wort „Text“ durch „BEARBEITETER Text“.
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("text", "EDITED text");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## Schritt 6: Erstellen Sie ein bearbeitbares Dokument mit aktualisiertem Inhalt
 Nachdem Sie die erforderlichen Änderungen vorgenommen haben, erstellen Sie ein neues`EditableDocument` mit dem aktualisierten Inhalt und den Originalressourcen.
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## Schritt 7: Erstellen Sie Speicheroptionen für Textverarbeitung
Bereiten Sie die Speicheroptionen für das Textverarbeitungsformat vor. Dieses Beispiel verwendet das DOCM-Format und gibt das Gebietsschema an.
```csharp
    WordProcessingSaveOptions wordSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm)
    {
        Locale = System.Globalization.CultureInfo.GetCultureInfo("en-GB")
    };
```
## Schritt 8: TXT-Speicheroptionen erstellen
Erstellen Sie auf ähnliche Weise die Speicheroptionen für das TXT-Format. Stellen Sie sicher, dass die Kodierung auf UTF-8 eingestellt ist und das Tabellenlayout beibehalten wird.
```csharp
    TextSaveOptions txtSaveOptions = new TextSaveOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        PreserveTableLayout = true
    };
```
## Schritt 9: Ausgabepfade vorbereiten
Bereiten Sie die Pfade zum Speichern der resultierenden DOCX- und TXT-Dateien vor. Verwenden Sie den Eingabedateipfad, um das Ausgabeverzeichnis und die Dateinamen zu bestimmen.
```csharp
    string outputWordPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".docm");
    string outputTxtPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".txt");
```
## Schritt 10: Speichern Sie das bearbeitete Dokument
Speichern Sie das bearbeitete Dokument abschließend mit den angegebenen Speicheroptionen sowohl im DOCX- als auch im TXT-Format.
```csharp
    editor.Save(afterEdit, outputWordPath, wordSaveOptions);
    editor.Save(afterEdit, outputTxtPath, txtSaveOptions);
}
System.Console.WriteLine("Document editing process completed successfully!");
```
## Abschluss
 Herzlichen Glückwunsch! Sie haben erfolgreich ein reines Textdokument mit GroupDocs.Editor für .NET bearbeitet. Dieses leistungsstarke Tool vereinfacht die Dokumentbearbeitung und ermöglicht eine einfache Integration in Ihre .NET-Anwendungen. Egal, ob Sie einfache Textdateien oder komplexe Dokumentformate bearbeiten, GroupDocs.Editor bietet alles. Weitere Funktionen und Möglichkeiten finden Sie auf der[GroupDocs.Editor-Dokumentation](https://tutorials.groupdocs.com/editor/net/).
## Häufig gestellte Fragen
### Welche Dateiformate unterstützt GroupDocs.Editor für .NET?
 GroupDocs.Editor für .NET unterstützt eine Vielzahl von Dateiformaten, darunter DOCX, TXT, HTML und mehr. Überprüfen Sie die[Dokumentation](https://tutorials.groupdocs.com/editor/net/) für eine vollständige Liste.
### Wie kann ich eine kostenlose Testversion von GroupDocs.Editor für .NET erhalten?
 Sie können eine kostenlose Testversion von GroupDocs.Editor für .NET herunterladen von der[Veröffentlichungsseite](https://releases.groupdocs.com/).
### Kann ich eine temporäre Lizenz für GroupDocs.Editor für .NET erwerben?
Ja, Sie können eine vorläufige Lizenz erhalten bei der[GroupDocs-Kaufseite](https://purchase.groupdocs.com/temporary-license/).
### Wo erhalte ich Support für GroupDocs.Editor für .NET?
 Support erhalten Sie über die[GroupDocs.Editor-Supportforum](https://forum.groupdocs.com/c/editor/20).
### Gibt es eine ausführliche Dokumentation für GroupDocs.Editor für .NET?
 Ja, eine ausführliche Dokumentation ist verfügbar auf der[GroupDocs.Editor-Dokumentationsseite](https://tutorials.groupdocs.com/editor/net/).