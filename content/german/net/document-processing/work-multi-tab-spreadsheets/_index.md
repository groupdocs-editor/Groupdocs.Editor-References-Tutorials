---
title: Arbeiten mit Tabellenkalkulationen mit mehreren Registerkarten
linktitle: Arbeiten mit Tabellenkalkulationen mit mehreren Registerkarten
second_title: GroupDocs.Editor .NET API
description: Erfahren Sie, wie Sie mit GroupDocs.Editor mit Tabellenkalkulationen mit mehreren Registerkarten in .NET arbeiten. Schritt-für-Schritt-Anleitung, Codebeispiele und bewährte Methoden inklusive.
weight: 17
url: /de/net/document-processing/work-multi-tab-spreadsheets/
---
## Einführung
Die Handhabung von Tabellen mit mehreren Registerkarten kann eine ziemliche Aufgabe sein, insbesondere wenn Sie Daten aus verschiedenen Tabellenblättern innerhalb desselben Dokuments bearbeiten oder extrahieren müssen. Wenn Sie mit .NET arbeiten und nach einer robusten Lösung suchen, ist GroupDocs.Editor für .NET eine ausgezeichnete Wahl. In diesem Tutorial führen wir Sie durch den Prozess der Arbeit mit Tabellen mit mehreren Registerkarten unter Verwendung von GroupDocs.Editor für .NET. Wir behandeln alles, vom Einrichten Ihrer Umgebung bis zum Speichern jeder Registerkarte als separate Datei.
## Voraussetzungen
Bevor Sie mit dem Lernprogramm beginnen, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:
1. Visual Studio: Stellen Sie sicher, dass Visual Studio auf Ihrem Computer installiert ist.
2. .NET Framework: GroupDocs.Editor für .NET unterstützt .NET Framework 4.0 oder höher.
3. GroupDocs.Editor für .NET: Laden Sie die Bibliothek GroupDocs.Editor für .NET herunter und installieren Sie sie. Sie erhalten sie von der[Download-Seite](https://releases.groupdocs.com/editor/net/).
4.  Lizenz: Sie können zwar eine[vorläufige Lizenz](https://purchase.groupdocs.com/temporary-license/) Um die Bibliothek auszuprobieren, wird empfohlen, eine Volllizenz für den Produktionseinsatz zu erwerben.
## Namespaces importieren
Bevor wir mit dem Codieren beginnen, müssen Sie die erforderlichen Namespaces importieren. Fügen Sie oben in Ihrer CS-Datei die folgenden using-Direktiven hinzu:
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
## 1. Holen Sie sich einen Pfad zur Eingabedatei
Zuerst müssen Sie den Pfad zu Ihrer Eingabetabellendatei angeben. Diese Datei sollte eine XLSX-Datei (OOXML) mit mehreren Registerkarten sein.
```csharp
string inputFilePath = "Your Sample Document";
```
## 2. Laden Sie die Tabelle in die Editor-Instanz
 Als nächstes laden Sie die Tabelle in ein`Editor` Instanz. Dies geschieht mithilfe eines Dateistreams und der Angabe der entsprechenden Ladeoptionen für eine Tabelle.
```csharp
using (FileStream inputStream = File.OpenRead(inputFilePath))
{
    using (Editor editor = new Editor(delegate { return inputStream; }, delegate { return new SpreadsheetLoadOptions(); }))
    {
        // Weitere Schritte folgen hier
    }
}
```
## 3. Erstellen Sie ein bearbeitbares Dokument auf der ersten Registerkarte
 Um eine bestimmte Registerkarte zu bearbeiten oder zu manipulieren, müssen Sie eine`EditableDocument` Instanz für diese Registerkarte. Die Registerkarte wird mit einem 0-basierten Index angegeben.
```csharp
SpreadsheetEditOptions editOptions1 = new SpreadsheetEditOptions();
editOptions1.WorksheetIndex = 0; // Erste Registerkarte
EditableDocument firstTabBeforeEdit = editor.Edit(editOptions1);
```
## 4. Erstellen Sie ein bearbeitbares Dokument auf der zweiten Registerkarte
 Erstellen Sie auf ähnliche Weise eine`EditableDocument` für die zweite Registerkarte.
```csharp
SpreadsheetEditOptions editOptions2 = new SpreadsheetEditOptions();
editOptions2.WorksheetIndex = 1; // Zweite Registerkarte
EditableDocument secondTabBeforeEdit = editor.Edit(editOptions2);
```
## 5. Speichern Sie die erste Registerkarte in einem separaten Dokument
Speichern Sie nun die erste Registerkarte als separates Dokument. Geben Sie das Speicherformat und den Ausgabepfad an.
```csharp
SpreadsheetSaveOptions saveOptions1 = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
string outputFilename1 = Path.GetFileNameWithoutExtension(inputFilePath) + "_tab1.xlsm";
string outputPath1 = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename1);
editor.Save(firstTabBeforeEdit, outputPath1, saveOptions1);
```
## 6. Speichern Sie die zweite Registerkarte in einem separaten Dokument
Wiederholen Sie den Vorgang für die zweite Registerkarte, speichern Sie sie dieses Mal jedoch in einem anderen Format.
```csharp
SpreadsheetSaveOptions saveOptions2 = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsb);
string outputFilename2 = Path.GetFileNameWithoutExtension(inputFilePath) + "_tab2.xlsb";
string outputPath2 = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename2);
editor.Save(secondTabBeforeEdit, outputPath2, saveOptions2);
```
## 7. EditableDocument-Instanzen entsorgen
 Stellen Sie abschließend sicher, dass Sie das`EditableDocument` Instanzen, um Ressourcen freizugeben.
```csharp
firstTabBeforeEdit.Dispose();
secondTabBeforeEdit.Dispose();
```

## Abschluss
Wenn Sie diese Schritte befolgen, können Sie mithilfe von GroupDocs.Editor problemlos mit Tabellen mit mehreren Registerkarten in .NET arbeiten. Diese leistungsstarke Bibliothek vereinfacht das Bearbeiten und Speichern verschiedener Blätter in einer Tabelle und macht Ihre Entwicklungsaufgaben leichter handhabbar. Ob Sie mit komplexen Datenmanipulationen oder einfachen Bearbeitungen zu tun haben, GroupDocs.Editor für .NET bietet die Tools, die Sie benötigen, um die Arbeit effizient zu erledigen.
## Häufig gestellte Fragen
### Was ist GroupDocs.Editor für .NET?
GroupDocs.Editor für .NET ist eine leistungsstarke API zur Dokumentbearbeitung, die es Entwicklern ermöglicht, Dokumente verschiedener Formate in .NET-Anwendungen zu laden, zu bearbeiten und zu speichern.
### Kann ich GroupDocs.Editor für .NET vor dem Kauf ausprobieren?
 Ja, Sie können ein[Kostenlose Testphase](https://releases.groupdocs.com/) oder fordern Sie ein[vorläufige Lizenz](https://purchase.groupdocs.com/temporary-license/) um das Produkt zu bewerten.
### Welche Dateiformate werden von GroupDocs.Editor für .NET unterstützt?
GroupDocs.Editor unterstützt eine Vielzahl von Formaten, darunter DOCX, XLSX, PPTX, PDF und viele mehr.
### Wie erhalte ich Unterstützung für GroupDocs.Editor für .NET?
 Sie erhalten Unterstützung unter[Hilfeforum](https://forum.groupdocs.com/c/editor/20).
### Wo kann ich eine Volllizenz für GroupDocs.Editor für .NET kaufen?
 Sie können eine Volllizenz erwerben bei der[Kaufseite](https://purchase.groupdocs.com/buy).