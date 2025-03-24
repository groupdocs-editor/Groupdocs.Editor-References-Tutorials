---
title: Arbeiten mit XML-Dokumenten
linktitle: Arbeiten mit XML-Dokumenten
second_title: GroupDocs.Editor .NET API
description: Erfahren Sie in unserer Schritt-für-Schritt-Anleitung, wie Sie XML-Dokumente mit GroupDocs.Editor für .NET effizient bearbeiten. Dabei werden alle wichtigen Schritte und Optionen behandelt.
weight: 20
url: /de/net/document-processing/work-xml-documents/
---

# Arbeiten mit XML-Dokumenten

## Einführung
In der heutigen digitalen Welt ist die effiziente Verwaltung und Bearbeitung von XML-Dokumenten für Entwickler und Unternehmen gleichermaßen von entscheidender Bedeutung. GroupDocs.Editor für .NET bietet eine leistungsstarke und vielseitige Lösung zum programmgesteuerten Bearbeiten von XML-Dateien. Dieses Tutorial führt Sie durch den Prozess der Arbeit mit XML-Dokumenten mithilfe von GroupDocs.Editor für .NET und erläutert jeden Schritt, um ihn einfach und verständlich zu machen.
## Voraussetzungen
Bevor wir uns in die einzelnen Schritte stürzen, stellen wir sicher, dass Sie alles haben, was Sie für den Einstieg benötigen.
1. Entwicklungsumgebung: Stellen Sie sicher, dass Sie eine Entwicklungsumgebung eingerichtet haben. Visual Studio wird dringend empfohlen.
2. .NET Framework: GroupDocs.Editor für .NET unterstützt mehrere .NET-Frameworks. Stellen Sie sicher, dass Ihr Projekt auf eine der unterstützten Versionen abzielt.
3.  GroupDocs.Editor für .NET: Laden Sie GroupDocs.Editor für .NET herunter und installieren Sie es von der[Download-Seite](https://releases.groupdocs.com/editor/net/).
4.  Lizenz: Sie können zwar eine temporäre Lizenz von[Hier](https://purchase.groupdocs.com/temporary-license/) , wird empfohlen, für den vollen Funktionsumfang eine Volllizenz von der[Kaufseite](https://purchase.groupdocs.com/buy).
5. Beispiel-XML-Datei: Halten Sie eine Beispiel-XML-Datei bereit, die Sie bearbeiten möchten.
## Namespaces importieren
Bevor Sie mit dem Code beginnen, müssen Sie die erforderlichen Namespaces importieren. Diese ermöglichen Ihnen den Zugriff auf die von GroupDocs.Editor für .NET bereitgestellten Funktionen.
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.HtmlCss.Serialization;
using GroupDocs.Editor.Options;
```
## 1. Laden Sie die XML-Eingabedatei
Der erste Schritt besteht darin, Ihre XML-Eingabedatei zu laden. Diese dient als das Dokument, das Sie bearbeiten möchten.
```csharp
string inputFilePath = "Your Sample Document.xml";
```
## 2. Erstellen Sie eine Editor-Instanz
 Erstellen Sie als nächstes eine Instanz des`Editor` Klasse. Diese Klasse ist die Kernkomponente, die die Bearbeitung Ihres Dokuments übernimmt.
```csharp
using (Editor editor = new Editor(inputFilePath))
{
    // Fahren Sie mit den folgenden Schritten innerhalb dieses Using-Blocks fort
}
```
## 3. XML-Bearbeitungsoptionen einrichten
Konfigurieren Sie die XML-Bearbeitungsoptionen nach Ihren Anforderungen. Diese Optionen bestimmen, wie der XML-Inhalt verarbeitet wird.
```csharp
XmlEditOptions editOptions = new XmlEditOptions
{
    AttributeValuesQuoteType = QuoteType.DoubleQuote,
    RecognizeEmails = true,
    RecognizeUris = true,
    TrimTrailingWhitespaces = true
};
```
## 4. Erstellen Sie eine bearbeitbare Dokumentinstanz
 Generieren Sie ein`EditableDocument` Instanz, die das XML-Dokument in einer editierbaren Form darstellt.
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
{
    // Fahren Sie mit der Bearbeitung des Dokuments fort
}
```
## 5. Bearbeiten Sie den Dokumentinhalt
Sie können nun den Inhalt Ihres XML-Dokuments nach Bedarf ändern, zum Beispiel Text im Dokument ersetzen.
```csharp
string originalTextContent = beforeEdit.GetContent();
string updatedTextContent = originalTextContent.Replace("John", "Samuel");
List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## 6. Erstellen Sie ein bearbeitbares Dokument mit aktualisiertem Inhalt
 Nachdem Sie die erforderlichen Änderungen vorgenommen haben, erstellen Sie ein neues`EditableDocument` Instanz mit dem aktualisierten Inhalt.
```csharp
using (EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources))
{
    // Vorbereiten des Speicherns des Dokuments
}
```
## 7. Konfigurieren Sie Speicheroptionen für verschiedene Formate
Mit GroupDocs.Editor können Sie das bearbeitete Dokument in verschiedenen Formaten speichern. Hier richten wir Optionen zum Speichern in den Formaten DOCX und TXT ein.
```csharp
WordProcessingSaveOptions wordSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docx);
TextSaveOptions txtSaveOptions = new TextSaveOptions
{
    Encoding = System.Text.Encoding.UTF8
};
```
## 8. Ausgabepfade vorbereiten
Geben Sie die Pfade an, in denen die bearbeiteten Dokumente gespeichert werden.
```csharp
string outputWordPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".docx");
string outputTxtPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".txt");
```
## 9. Speichern Sie das bearbeitete Dokument
Speichern Sie das bearbeitete Dokument abschließend mit den zuvor konfigurierten Speicheroptionen in den angegebenen Pfaden.
```csharp
editor.Save(afterEdit, outputWordPath, wordSaveOptions);
editor.Save(afterEdit, outputTxtPath, txtSaveOptions);
```
## 10. Schließen Sie den Vorgang ab
Drucken Sie nach Abschluss eine Bestätigungsnachricht auf der Konsole.
```csharp
System.Console.WriteLine("WorkingWithXml routine has successfully finished");
```
## Abschluss
Das Arbeiten mit XML-Dokumenten mit GroupDocs.Editor für .NET ist unkompliziert und effizient. Indem Sie die in diesem Handbuch beschriebenen Schritte befolgen, können Sie XML-Dateien problemlos programmgesteuert laden, bearbeiten und speichern. Ganz gleich, ob Sie kleine Textersetzungen oder umfangreiche Inhaltsänderungen vornehmen müssen, GroupDocs.Editor für .NET bietet die erforderlichen Tools und die Flexibilität, um Ihre Anforderungen bei der Dokumentbearbeitung zu erfüllen.
## Häufig gestellte Fragen
### Was ist GroupDocs.Editor für .NET?
GroupDocs.Editor für .NET ist eine Bibliothek, die es Entwicklern ermöglicht, verschiedene Dokumentformate, einschließlich XML, programmgesteuert in .NET-Anwendungen zu bearbeiten.
### Kann ich GroupDocs.Editor kostenlos nutzen?
 GroupDocs.Editor bietet eine kostenlose Testversion an, auf die Sie zugreifen können[Hier](https://releases.groupdocs.com/). Für die volle Funktionalität müssen Sie eine Lizenz erwerben.
### Wie erhalte ich Unterstützung für GroupDocs.Editor für .NET?
 Unterstützung erhalten Sie vom[GroupDocs.Editor-Supportforum](https://forum.groupdocs.com/c/editor/20).
### In welche Dateiformate kann ich XML mit GroupDocs.Editor konvertieren?
Sie können XML mit den entsprechenden Speicheroptionen in mehrere Formate konvertieren, darunter DOCX und TXT.
### Gibt es eine temporäre Lizenz zum Testen?
 Ja, Sie können eine temporäre Lizenz zu Testzwecken erhalten bei[Hier](https://purchase.groupdocs.com/temporary-license/).