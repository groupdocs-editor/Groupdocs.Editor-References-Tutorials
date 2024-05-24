---
title: Arbeiten mit durch Trennzeichen getrennten Werten (DSV)
linktitle: Arbeiten mit durch Trennzeichen getrennten Werten (DSV)
second_title: GroupDocs.Editor .NET API
description: Erfahren Sie in dieser Schritt-für-Schritt-Anleitung, wie Sie CSV- und TSV-Dateien mit GroupDocs.Editor für .NET bearbeiten. Verbessern Sie Ihre .NET-Projekte mühelos.
type: docs
weight: 12
url: /de/net/document-processing/work-dsv/
---
## Einführung
Wenn Sie als Entwickler mit durch Trennzeichen getrennten Werten (DSV) wie CSV- oder TSV-Dateien arbeiten, wissen Sie, dass das programmgesteuerte Bearbeiten dieser Dateien eine gewaltige Aufgabe sein kann. Mit GroupDocs.Editor für .NET wird diese Aufgabe jedoch deutlich einfacher und effizienter. In diesem Tutorial zeigen wir Ihnen Schritt für Schritt, wie Sie mit GroupDocs.Editor für .NET DSV-Dateien lesen, bearbeiten und speichern. Wir unterteilen den Vorgang in leicht verständliche Schritte, sodass Sie ihn problemlos in Ihre Projekte integrieren können.
## Voraussetzungen
Bevor wir mit dem Tutorial beginnen, stellen Sie sicher, dass Sie die folgenden Voraussetzungen erfüllen:
- Visual Studio: Stellen Sie sicher, dass Visual Studio auf Ihrem Computer installiert ist.
-  GroupDocs.Editor für .NET: Sie müssen die Bibliothek GroupDocs.Editor für .NET herunterladen und referenzieren. Sie können sie herunterladen[Hier](https://releases.groupdocs.com/editor/net/).
- Grundlegende Kenntnisse in C#: Dieses Tutorial setzt voraus, dass Sie über grundlegende Kenntnisse in C# und .NET-Entwicklung verfügen.
## Namespaces importieren
Zuerst müssen Sie die erforderlichen Namespaces in Ihr Projekt importieren. Diese Namespaces stellen die Klassen und Methoden bereit, die für die Arbeit mit GroupDocs.Editor für .NET erforderlich sind.
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

## Schritt 1: Pfad zur DSV-Eingabedatei abrufen
Zuerst müssen Sie den Pfad zur DSV-Eingabedatei angeben. Für dieses Beispiel gehen wir davon aus, dass es sich um eine CSV-Datei handelt.
```csharp
string inputFilePath = "Your Sample Document";
```
## Schritt 2: Erstellen einer Editor-Instanz
 Erstellen Sie eine Instanz des`Editor` Klasse. Diese Instanz wird zum Laden und Bearbeiten der DSV-Datei verwendet.
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## Schritt 3: DSV-Bearbeitungsoptionen erstellen
 Erstellen Sie als nächstes eine Instanz von`DelimitedTextEditOptions` und geben Sie das Trennzeichen für die DSV-Datei an. Hier verwenden wir ein Komma als Trennzeichen.
```csharp
    Options.DelimitedTextEditOptions editOptions = new DelimitedTextEditOptions(",");
    editOptions.ConvertDateTimeData = false;
    editOptions.ConvertNumericData = true;
    editOptions.TreatConsecutiveDelimitersAsOne = true;
```
## Schritt 4: Erstellen Sie eine EditableDocument-Instanz
 Erstelle ein`EditableDocument` Instanz mit dem`Editor.Edit` -Methode. Dadurch wird das Dokument für die Bearbeitung vorbereitet.
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## Schritt 5: Bearbeiten des Dokumentinhalts
Rufen Sie den ursprünglichen Textinhalt ab und nehmen Sie die erforderlichen Änderungen vor. Lassen Sie uns zu Demonstrationszwecken einen Teil des Textes ersetzen.
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("SsangYong", "Chevrolet").Replace("Kyron", "Camaro");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## Schritt 6: Erstellen Sie ein bearbeitbares Dokument mit aktualisiertem Inhalt
 Erstelle eine neue`EditableDocument` mit dem aktualisierten Inhalt.
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## Schritt 7: CSV-Speicheroptionen erstellen
Geben Sie die Speicheroptionen für das CSV-Format an, einschließlich Trennzeichen und Kodierung.
```csharp
    Options.DelimitedTextSaveOptions csvSaveOptions = new DelimitedTextSaveOptions(",");
    csvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## Schritt 8: TSV-Speicheroptionen erstellen
Geben Sie auf ähnliche Weise die Speicheroptionen für das TSV-Format an.
```csharp
    Options.DelimitedTextSaveOptions tsvSaveOptions = new DelimitedTextSaveOptions("\t");
    tsvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## Schritt 9: Optionen zum Speichern der Tabellenkalkulation erstellen
Wenn Sie das Dokument als Tabellenkalkulation speichern müssen, erstellen Sie die entsprechenden Speicheroptionen.
```csharp
    Options.SpreadsheetSaveOptions cellsSaveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
```
## Schritt 10: Speicherpfade vorbereiten
Definieren Sie die Pfade, in denen die bearbeiteten Dateien gespeichert werden.
```csharp
    string outputCsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".csv");
    string outputTsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".tsv");
    string outputCellsPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".xlsm");
```
## Schritt 11: Speichern Sie das bearbeitete Dokument
Speichern Sie das bearbeitete Dokument in verschiedenen Formaten in den angegebenen Pfaden.
```csharp
    editor.Save(afterEdit, outputCsvPath, csvSaveOptions);
    editor.Save(afterEdit, outputTsvPath, tsvSaveOptions);
    editor.Save(afterEdit, outputCellsPath, cellsSaveOptions);
```
## Schritt 12: EditableDocument-Instanzen entsorgen
 Entsorgen Sie abschließend die`EditableDocument` Instanzen, um Ressourcen freizugeben.
```csharp
    beforeEdit.Dispose();
    afterEdit.Dispose();
}
System.Console.WriteLine("WorkingWithDsv routine has successfully finished");
```
## Abschluss
Das Bearbeiten von DSV-Dateien mit GroupDocs.Editor für .NET ist ein unkomplizierter Vorgang, der das Erstellen einer Editorinstanz, das Festlegen von Bearbeitungsoptionen, das Ändern des Inhalts und das Speichern der Änderungen umfasst. Diese Schritt-für-Schritt-Anleitung soll Ihnen dabei helfen, diese Funktionalität problemlos in Ihre .NET-Anwendungen zu integrieren. Unabhängig davon, ob Sie mit CSV, TSV oder anderen DSV-Formaten arbeiten, bietet GroupDocs.Editor für .NET eine robuste und flexible Lösung.
## Häufig gestellte Fragen
### Kann ich GroupDocs.Editor für .NET zum Bearbeiten großer CSV-Dateien verwenden?
Ja, GroupDocs.Editor für .NET kann große CSV-Dateien effizient verarbeiten.
### Unterstützt GroupDocs.Editor für .NET andere DSV-Formate außer CSV und TSV?
Ja, es unterstützt verschiedene DSV-Formate, solange Sie das entsprechende Trennzeichen angeben.
### Ist es möglich, die Kodierung beim Speichern von DSV-Dateien anzupassen?
Natürlich können Sie in den Speicheroptionen die gewünschte Kodierung angeben.
### Kann ich mit GroupDocs.Editor für .NET eine CSV-Datei in eine Excel-Tabelle konvertieren?
Ja, Sie können eine CSV-Datei als Excel-Tabelle speichern, indem Sie die entsprechenden Speicheroptionen verwenden.
### Wo finde ich weitere Dokumentation zu GroupDocs.Editor für .NET?
 Eine ausführliche Dokumentation finden Sie[Hier](https://reference.groupdocs.com/editor/net/)