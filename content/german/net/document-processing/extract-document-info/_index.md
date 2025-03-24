---
title: Dokumentinformationen extrahieren
linktitle: Dokumentinformationen extrahieren
second_title: GroupDocs.Editor .NET API
description: Erfahren Sie in unserem ausführlichen Schritt-für-Schritt-Tutorial, wie Sie mit GroupDocs.Editor für .NET Dokumentinformationen extrahieren. Perfekt für die Verwaltung verschiedener Dokumenttypen.
weight: 10
url: /de/net/document-processing/extract-document-info/
---

# Dokumentinformationen extrahieren

## Einführung
Willkommen zu diesem umfassenden Tutorial zum Extrahieren von Dokumentinformationen mit GroupDocs.Editor für .NET. In dieser Anleitung führen wir Sie Schritt für Schritt durch den Prozess und stellen sicher, dass Sie jeden Teil klar und präzise verstehen. Egal, ob Sie ein erfahrener Entwickler sind oder gerade erst anfangen, dieses Tutorial hilft Ihnen dabei, GroupDocs.Editor nahtlos in Ihre .NET-Projekte zu integrieren, um Dokumente effizient zu verwalten und zu bearbeiten.
## Voraussetzungen
Bevor wir uns in den Code vertiefen, stellen wir sicher, dass Sie alles haben, was Sie brauchen:
- Grundkenntnisse in C#: Das Verständnis der Grundlagen der C#-Programmierung ist wichtig.
- Visual Studio: Stellen Sie sicher, dass Sie Visual Studio installiert haben.
-  GroupDocs.Editor für .NET: Sie benötigen die Bibliothek GroupDocs.Editor für .NET. Sie können sie herunterladen von[Download-Seite](https://releases.groupdocs.com/editor/net/).
## Namespaces importieren
Zu Beginn müssen Sie die erforderlichen Namespaces importieren. Dadurch können Sie auf die Klassen und Methoden zugreifen, die zum Bearbeiten von Dokumenten erforderlich sind.
```csharp
using System;
using GroupDocs.Editor.Metadata;
```
## Schritt 1: Laden Sie Ihr Dokument
Zuerst müssen Sie das Dokument laden, aus dem Sie Informationen extrahieren möchten. Dies können Sie tun, indem Sie den Dateipfad zum Dokument angeben.
```csharp
string docxInputFilePath = "YourSampleDocument.docx";
Editor editorDocx = new Editor(docxInputFilePath);
```
## Schritt 2: Dokumentinformationen abrufen
 Als nächstes rufen Sie die Dokumentinformationen ab mit dem`GetDocumentInfo` Methode. Diese Methode erfordert keine speziellen Ladeoptionen, wenn Sie sich über das Dokumentformat nicht sicher sind.
```csharp
IDocumentInfo infoDocx = editorDocx.GetDocumentInfo(null);
```
## Schritt 3: Dokumenttyp bestimmen
Jetzt müssen Sie den Dokumenttyp überprüfen, mit dem Sie arbeiten. Dies ist entscheidend, da es bestimmt, wie Sie mit dem Dokument umgehen.
```csharp
bool isSpreadsheet = infoDocx is SpreadsheetDocumentInfo;
bool isText = infoDocx is TextualDocumentInfo;
bool isWordProcessing = infoDocx is WordProcessingDocumentInfo;
Console.WriteLine($"Is '{docxInputFilePath}' a Spreadsheet: {isSpreadsheet}");
Console.WriteLine($"Is '{docxInputFilePath}' a Textual document: {isText}");
Console.WriteLine($"Is '{docxInputFilePath}' a WordProcessing document: {isWordProcessing}");
```
## Schritt 4: Detaillierte Informationen extrahieren
Wenn es sich bei dem Dokument um ein Textverarbeitungsdokument handelt, können Sie detaillierte Informationen wie Format, Erweiterung, Seitenzahl, Größe und Verschlüsselung extrahieren.
```csharp
if (isWordProcessing)
{
    WordProcessingDocumentInfo casted = (WordProcessingDocumentInfo)infoDocx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Page count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```
## Schritt 5: Wiederholen Sie den Vorgang für verschiedene Dokumenttypen
Wiederholen Sie die gleichen Schritte für andere Dokumenttypen wie Tabellenkalkulationen und Textdokumente.
```csharp
string xlsxInputFilePath = "YourSampleDocument.xlsx";
Editor editorXlsx = new Editor(xlsxInputFilePath);
IDocumentInfo infoXlsx = editorXlsx.GetDocumentInfo(null);
bool isXlsxSpreadsheet = infoXlsx is SpreadsheetDocumentInfo;
Console.WriteLine($"Is '{xlsxInputFilePath}' a Spreadsheet: {isXlsxSpreadsheet}");
if (isXlsxSpreadsheet)
{
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo)infoXlsx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Tabs count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```
## Schritt 6: Umgang mit passwortgeschützten Dokumenten
Bei passwortgeschützten Dokumenten sollten Sie zunächst versuchen, diese ohne Passwort, dann mit einem falschen Passwort und schließlich mit dem richtigen Passwort zu öffnen.
```csharp
string xlsInputFilePath = "YourSampleDocument.xls";
Editor editorXls = new Editor(xlsInputFilePath);
try
{
    IDocumentInfo infoXls = editorXls.GetDocumentInfo(null);
}
catch (PasswordRequiredException)
{
    Console.WriteLine("This document is password-protected.");
}
try
{
    IDocumentInfo infoXls = editorXls.GetDocumentInfo("incorrect_password");
}
catch (IncorrectPasswordException)
{
    Console.WriteLine("The provided password is incorrect.");
}
IDocumentInfo infoXlsValid = editorXls.GetDocumentInfo("correct_password");
bool isXlsSpreadsheet = infoXlsValid is SpreadsheetDocumentInfo;
Console.WriteLine($"Password-protected document is a Spreadsheet: {isXlsSpreadsheet}");
if (isXlsSpreadsheet)
{
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo)infoXlsValid;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Tabs count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```
## Schritt 7: Textbasierte Dokumente verarbeiten
```csharp
string xmlInputFilePath = "YourSampleDocument.xml";
Editor editorXml = new Editor(xmlInputFilePath);
IDocumentInfo infoXml = editorXml.GetDocumentInfo(null);
bool isXmlText = infoXml is TextualDocumentInfo;
Console.WriteLine($"Is '{xmlInputFilePath}' a Textual document: {isXmlText}");
if (isXmlText)
{
    TextualDocumentInfo casted = (TextualDocumentInfo)infoXml;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Encoding: {casted.Encoding}; Size: {casted.Size} bytes");
}
```
## Schritt 8: Ressourcen entsorgen
Stellen Sie abschließend sicher, dass Sie alle Ressourcen freigeben, um Speicherlecks zu verhindern.
```csharp
editorDocx.Dispose();
editorXlsx.Dispose();
editorXls.Dispose();
editorXml.Dispose();
Console.WriteLine("ExtractingDocumentInfo routine has successfully finished");
```
## Abschluss
Herzlichen Glückwunsch! Sie haben jetzt gelernt, wie Sie Dokumentinformationen mit GroupDocs.Editor für .NET extrahieren. Diese leistungsstarke Bibliothek vereinfacht die Dokumentenverwaltung und -bearbeitung und ermöglicht Ihnen die nahtlose Verarbeitung verschiedener Dokumenttypen. Egal, ob Sie mit Textverarbeitungs-, Tabellenkalkulations- oder textbasierten Dokumenten arbeiten, GroupDocs.Editor bietet eine robuste Lösung.
## Häufig gestellte Fragen
### Welche Dokumenttypen kann GroupDocs.Editor verarbeiten?
GroupDocs.Editor kann verschiedene Dokumenttypen verarbeiten, darunter Textverarbeitungs-, Tabellenkalkulations- und textbasierte Dokumente.
### Kann GroupDocs.Editor passwortgeschützte Dokumente verwalten?
Ja, GroupDocs.Editor kann passwortgeschützte Dokumente verwalten. Es kann diese Dokumente identifizieren und mit dem richtigen Passwort öffnen.
### Ist es notwendig, die Editorobjekte zu entsorgen?
Ja, es ist wichtig, Editorobjekte zu entsorgen, um Ressourcen freizugeben und Speicherlecks zu verhindern.
### Kann ich detaillierte Informationen zum Dokumentformat und zur Dokumentgröße extrahieren?
Auf jeden Fall! GroupDocs.Editor ermöglicht Ihnen das Extrahieren detaillierter Informationen wie Format, Erweiterung, Größe, Seitenzahl und Verschlüsselungsstatus.
### Wo erhalte ich Unterstützung, wenn Probleme auftreten?
 Unterstützung erhalten Sie vom[GroupDocs.Editor-Supportforum](https://forum.groupdocs.com/c/editor/20).