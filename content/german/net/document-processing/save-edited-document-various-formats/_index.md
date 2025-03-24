---
title: Bearbeitetes Dokument in verschiedenen Formaten speichern
linktitle: Bearbeitetes Dokument in verschiedenen Formaten speichern
second_title: GroupDocs.Editor .NET API
description: Erfahren Sie in dieser umfassenden Schritt-für-Schritt-Anleitung, wie Sie bearbeitete Dokumente mit GroupDocs.Editor für .NET in verschiedenen Formaten speichern.
weight: 11
url: /de/net/document-processing/save-edited-document-various-formats/
---

# Bearbeitetes Dokument in verschiedenen Formaten speichern

## Einführung
Möchten Sie bearbeitete Dokumente mit GroupDocs.Editor für .NET in verschiedenen Formaten speichern? Dann sind Sie hier richtig! Diese umfassende Anleitung führt Sie durch den gesamten Prozess, vom Einrichten Ihrer Umgebung bis zum Speichern Ihres bearbeiteten Dokuments in mehreren Formaten. Lassen Sie uns eintauchen und das Bearbeiten und Speichern von Dokumenten zum Kinderspiel machen!
## Voraussetzungen
Bevor wir beginnen, stellen Sie sicher, dass Sie über Folgendes verfügen:
1.  GroupDocs.Editor für .NET - Laden Sie die neueste Version herunter von[Hier](https://releases.groupdocs.com/editor/net/).
2. Entwicklungsumgebung – Visual Studio oder eine andere .NET-kompatible IDE.
3. .NET Framework – Stellen Sie sicher, dass Sie .NET Framework 4.6.1 oder höher installiert haben.
4. Beispieldokument – Ein Beispieldokument aus der Textverarbeitung zum Arbeiten.
5. Grundlegende C#-Kenntnisse – Vertrautheit mit der C#-Programmierung ist erforderlich.
## Namespaces importieren
Stellen Sie zunächst sicher, dass Sie die erforderlichen Namespaces in Ihr C#-Projekt importieren. Dies ist für den Zugriff auf die GroupDocs.Editor-Funktionalität von entscheidender Bedeutung.
```csharp
using System;
using GroupDocs.Editor.Metadata;
```
Lassen Sie uns den Prozess in überschaubare Schritte unterteilen. Folgen Sie ihnen sorgfältig, um sicherzustellen, dass Sie jeden Teil verstehen.
## Schritt 1: Holen Sie sich einen Pfad zur Eingabedatei
Zuerst müssen Sie den Pfad zu Ihrer Eingabe-Textverarbeitungsdatei angeben. Diese Datei wird geladen und bearbeitet.
```csharp
string inputFilePath = "Your Sample Document";
```
## Schritt 2: Ladeoptionen für das Dokument erstellen
Erstellen Sie als Nächstes Ladeoptionen speziell für WordProcessing-Dokumente. Mit diesen Optionen können Sie anpassen, wie das Dokument geladen wird.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
```
## Schritt 3: Laden Sie das Dokument mit Optionen
 Laden Sie nun das Dokument in ein`Editor` -Instanz unter Verwendung der angegebenen Ladeoptionen.
```csharp
using (Editor editor = new Editor(inputFilePath, delegate { return loadOptions; }))
```
## Schritt 4: Bearbeitungsoptionen erstellen
Bereiten Sie Bearbeitungsoptionen für das Dokument vor. Diese Optionen bestimmen, wie das Dokument zum Bearbeiten geöffnet wird.
```csharp
WordProcessingEditOptions editOptions = new WordProcessingEditOptions();
```
## Schritt 5: Dokument zum Bearbeiten öffnen
 Öffnen Sie das Dokument zur Bearbeitung, indem Sie eine`EditableDocument`Instanz. Diese Instanz ermöglicht es Ihnen, Änderungen am Dokument vorzunehmen.
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
```
## Schritt 6: Bearbeiten des Dokumentinhalts
Jetzt ist es an der Zeit, den Inhalt des Dokuments zu bearbeiten. Holen Sie sich zunächst das Dokument als einzelne base64-codierte Zeichenfolge.
```csharp
string allEmbeddedInsideString = beforeEdit.GetEmbeddedHtml();
```
Lassen Sie uns beispielsweise den Untertitel im Dokument ändern.
```csharp
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
```
## Schritt 7: Neues editierbares Dokument aus bearbeitetem Inhalt erstellen
 Erstelle eine neue`EditableDocument` Instanz aus den bearbeiteten Inhalten und Ressourcen.
```csharp
using (EditableDocument afterEdit = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null))
```
## Schritt 8: Dokument in verschiedenen Formaten speichern
Zum Schluss durchlaufen Sie alle unterstützten Textverarbeitungsformate und speichern das bearbeitete Dokument in jedem Format.
```csharp
foreach (WordProcessingFormats oneFormat in WordProcessingFormats.All)
{
    // Speicheroptionen vorbereiten
    WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(oneFormat);
    // Speicherpfad vorbereiten
    string savePath = Path.Combine("OutputDirectory", "MultipleOutFormats." + saveOptions.OutputFormat.Extension);
    // Speichern des Dokuments
    editor.Save(afterEdit, savePath, saveOptions);
}
```
## Abschlussmeldung
Zum Abschluss können Sie eine Meldung ausdrucken, dass der Vorgang erfolgreich beendet wurde.
```csharp
Console.WriteLine("SavingEditedDocumentToAllFormats routine has successfully finished");
```
## Abschluss
Herzlichen Glückwunsch! Sie haben erfolgreich gelernt, wie Sie bearbeitete Dokumente mit GroupDocs.Editor für .NET in verschiedenen Formaten speichern. Dieses leistungsstarke Tool erleichtert das Bearbeiten und Speichern von Dokumenten in mehreren Formaten mit nur wenigen Codezeilen. Denken Sie daran, dass die wichtigsten Schritte das Laden des Dokuments, das Bearbeiten des Inhalts und das Speichern in den gewünschten Formaten sind.
## Häufig gestellte Fragen
### Was ist GroupDocs.Editor für .NET?
GroupDocs.Editor für .NET ist eine leistungsstarke API, mit der Sie Dokumente in verschiedenen Formaten mit .NET-Anwendungen bearbeiten können.
### Kann ich GroupDocs.Editor kostenlos nutzen?
 Ja, Sie können es mit einer kostenlosen Testversion verwenden. Laden Sie es herunter[Hier](https://releases.groupdocs.com/).
### Welche Formate werden von GroupDocs.Editor unterstützt?
GroupDocs.Editor unterstützt eine Vielzahl von Formaten, darunter DOCX, PDF, HTML und viele mehr.
### Wie erhalte ich eine temporäre Lizenz für GroupDocs.Editor?
 Sie können eine temporäre Lizenz erhalten[Hier](https://purchase.groupdocs.com/temporary-license/).
### Wo finde ich weitere Dokumentation und Support?
 Detaillierte Dokumentation ist verfügbar[Hier](https://tutorials.groupdocs.com/editor/net/) , und Sie können Unterstützung erhalten[Hier](https://forum.groupdocs.com/c/editor/20).