---
title: Dokument laden
linktitle: Dokument laden
second_title: GroupDocs.Editor .NET API
description: Erfahren Sie, wie Sie Dokumente programmgesteuert mit GroupDocs.Editor für .NET bearbeiten. Schritt-für-Schritt-Anleitung zum Laden von Dokumenten, Verwalten kennwortgeschützter Dateien und mehr.
weight: 13
url: /de/net/document-editing/load-document/
---
## Einführung
Das programmgesteuerte Bearbeiten von Dokumenten kann eine gewaltige Aufgabe sein, insbesondere wenn Sie mit unterschiedlichen Dateiformaten und komplexen Strukturen arbeiten. Glücklicherweise macht GroupDocs.Editor für .NET diese Aufgabe zum Kinderspiel und bietet eine robuste und benutzerfreundliche API zum Bearbeiten einer Vielzahl von Dokumenttypen. In diesem Tutorial führen wir Sie durch alles, was Sie zum Einstieg in GroupDocs.Editor für .NET benötigen, einschließlich der Voraussetzungen, des Importierens von Namespaces und einer detaillierten Schritt-für-Schritt-Anleitung zum Laden von Dokumenten mit verschiedenen Methoden.
## Voraussetzungen
Bevor wir loslegen, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:
- Visual Studio: Stellen Sie sicher, dass Visual Studio auf Ihrem Computer installiert ist.
- .NET Framework: GroupDocs.Editor für .NET unterstützt .NET Framework 2.0 oder höher. Stellen Sie sicher, dass Ihr Projekt auf ein kompatibles Framework abzielt.
-  GroupDocs.Editor für .NET: Laden Sie die neueste Version herunter von der[Download-Seite](https://releases.groupdocs.com/editor/net/).
- Grundkenntnisse in C#: Um diesem Tutorial folgen zu können, sind Kenntnisse in der C#- und .NET-Programmierung erforderlich.
## Namespaces importieren
Um GroupDocs.Editor für .NET verwenden zu können, müssen Sie die erforderlichen Namespaces in Ihr Projekt importieren. Fügen Sie oben in Ihrer C#-Datei die folgenden using-Direktiven hinzu:
```csharp
using GroupDocs.Editor.Options;
using System.IO;
```
Diese Namespaces bieten Zugriff auf die Klassen und Methoden, die für Dokumentbearbeitungsaufgaben erforderlich sind.
## Schritt 1: Dokument aus einem Dateipfad laden
Das Laden eines Dokuments aus einem Dateipfad ist unkompliziert. Diese Methode ist ideal für Dokumente, die lokal auf Ihrem Computer gespeichert sind.

```csharp
string inputPath = "Your Sample Document";
// Dokument als Datei über Pfad und ohne Ladeoptionen laden
Editor editor1 = new Editor(inputPath);
// Ressourcen entsorgen
editor1.Dispose();
System.Console.WriteLine("Document loaded successfully from file path.");
```
## Schritt 2: Dokument mit Ladeoptionen laden
Manchmal müssen Sie Dokumente laden, die eine besondere Behandlung erfordern, z. B. kennwortgeschützte Dateien. In solchen Fällen können Sie Ladeoptionen verwenden.

```csharp
string inputPath = "Your Sample Document";
//Ladeoptionen für Word-Dokumente erstellen
WordProcessingLoadOptions wordLoadOptions = new WordProcessingLoadOptions();
wordLoadOptions.Password = "some password";
// Dokument als Datei laden über Pfad und mit Ladeoptionen
Editor editor2 = new Editor(inputPath, delegate { return wordLoadOptions; });
// Ressourcen entsorgen
editor2.Dispose();
System.Console.WriteLine("Password-protected document loaded successfully.");
```
## Schritt 3: Dokument aus einem Byte-Stream laden
Das Laden eines Dokuments aus einem Bytestream ist nützlich, wenn Sie Dokumente verarbeiten müssen, die nicht als Dateien gespeichert sind, z. B. solche, die aus einer Datenbank oder einem Webdienst abgerufen wurden.

```csharp
FileStream inputStream = File.OpenRead("Your Sample Document");
// Dokument als Inhalt aus Bytestream und ohne Ladeoptionen laden
Editor editor3 = new Editor(delegate { return inputStream; });
// Ressourcen entsorgen
editor3.Dispose();
System.Console.WriteLine("Document loaded successfully from byte stream.");
```
## Schritt 4: Dokument mit Ladeoptionen aus einem Byte-Stream laden
Für Dokumente, die beim Laden aus einem Bytestream eine besondere Behandlung erfordern, können Sie das Laden des Bytestreams mit Ladeoptionen kombinieren.

```csharp
FileStream inputStream = File.OpenRead("Your Sample Document");
// Erstellen von Ladeoptionen für Tabellenkalkulationen
SpreadsheetLoadOptions sheetLoadOptions = new SpreadsheetLoadOptions();
sheetLoadOptions.OptimizeMemoryUsage = true;
// Dokument als Inhalt aus Bytestream und mit Ladeoptionen laden
Editor editor4 = new Editor(delegate { return inputStream; }, delegate { return sheetLoadOptions; });
// Ressourcen entsorgen
editor4.Dispose();
System.Console.WriteLine("Spreadsheet document loaded successfully with load options.");
```
## Abschluss
Herzlichen Glückwunsch! Sie haben erfolgreich gelernt, wie Sie Dokumente mit GroupDocs.Editor für .NET auf verschiedene Arten laden können. Egal, ob Sie mit lokalen Dateien, kennwortgeschützten Dokumenten oder Byte-Streams arbeiten, GroupDocs.Editor bietet eine flexible und leistungsstarke Lösung für Ihre Anforderungen an die Dokumentbearbeitung. Denken Sie daran, immer Ressourcen freizugeben, um optimale Leistung und Ressourcenverwaltung in Ihren Anwendungen sicherzustellen.
## Häufig gestellte Fragen
### Welche Dateiformate werden von GroupDocs.Editor für .NET unterstützt?
 GroupDocs.Editor unterstützt eine Vielzahl von Dateiformaten, darunter DOCX, XLSX, PPTX, HTML und viele mehr. Eine vollständige Liste finden Sie im[Dokumentation](https://tutorials.groupdocs.com/editor/net/).
### Wie gehe ich mit passwortgeschützten Dokumenten um?
 Sie können Ladeoptionen verwenden wie`WordProcessingLoadOptions` um beim Laden passwortgeschützter Dokumente das Passwort anzugeben.
### Kann ich GroupDocs.Editor in einer Webanwendung verwenden?
Ja, GroupDocs.Editor kann in Webanwendungen verwendet werden. Stellen Sie sicher, dass Sie Dateiströme und Ressourcenverfügung richtig handhaben, um Speicherlecks zu vermeiden.
### Wo kann ich eine temporäre Lizenz für GroupDocs.Editor erhalten?
 Eine vorläufige Lizenz erhalten Sie bei der[Seite mit der temporären Lizenz](https://purchase.groupdocs.com/temporary-license/).
### Gibt es Support, wenn ich auf Probleme stoße?
 Ja, GroupDocs bietet Support über ihre[Hilfeforum](https://forum.groupdocs.com/c/editor/20).