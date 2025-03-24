---
title: Dokument bearbeiten
linktitle: Dokument bearbeiten
second_title: GroupDocs.Editor .NET API
description: Lernen Sie, mit GroupDocs.Editor für .NET mühelos Dokumente zu bearbeiten. Schritt-für-Schritt-Anleitung für Textverarbeitungs- und Tabellenkalkulationsdateien.
weight: 11
url: /de/net/document-editing/edit-document/
---
## Einführung
Haben Sie sich schon einmal mit der Komplexität der Dokumentbearbeitung in Ihren .NET-Anwendungen herumgeschlagen? Keine Angst! Mit GroupDocs.Editor für .NET haben Sie einen leistungsstarken Verbündeten, der diese Aufgabe vereinfacht. Diese umfassende Anleitung zeigt Ihnen, wie Sie dieses robuste Tool nutzen können, um Dokumente mühelos zu bearbeiten. Egal, ob Sie mit Textverarbeitungsdokumenten oder Tabellenkalkulationen arbeiten, am Ende dieses Tutorials werden Sie GroupDocs.Editor wie ein Profi bedienen können.
## Voraussetzungen
Bevor Sie mit dem Lernprogramm beginnen, stellen Sie sicher, dass Sie über Folgendes verfügen:
- Visual Studio: Installiert und einsatzbereit.
- .NET Framework: Eine kompatible Version ist auf Ihrem System installiert.
-  GroupDocs.Editor für .NET: Sie können[Laden Sie die neueste Version herunter](https://releases.groupdocs.com/editor/net/) und erhalten Sie eine[vorläufige Lizenz](https://purchase.groupdocs.com/temporary-license/) wenn benötigt.
- Grundkenntnisse in C#: Dieses Handbuch setzt voraus, dass Sie über grundlegende Kenntnisse der C#- und .NET-Entwicklung verfügen.
## Namespaces importieren
Um zu beginnen, müssen Sie die erforderlichen Namespaces in Ihr Projekt importieren. Fügen Sie oben in Ihrer C#-Datei die folgenden Zeilen hinzu:
```csharp
using System.Collections.Generic;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.Options;
```
Nachdem Sie nun alles eingerichtet haben, unterteilen wir den Dokumentbearbeitungsprozess in überschaubare Schritte.
## Schritt 1: Laden Sie ein Textverarbeitungsdokument
Lassen Sie uns zunächst ein Textverarbeitungsdokument laden. Hier zeigen Sie der Editor-Instanz den Speicherort Ihres Dokuments an und geben bei Bedarf alle Ladeoptionen an.
### 1.1 Initialisieren Sie den Editor mit Standardoptionen
```csharp
string inputFilePath = "Your Sample Document"; // Pfad zu Ihrem Dokument
Editor editor1 = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
```
Dieser Codeausschnitt initialisiert die Editorinstanz mit Standardladeoptionen für ein Textverarbeitungsdokument.
## Schritt 2: Bearbeiten Sie das Dokument
Jetzt können wir mit der Bearbeitung des geladenen Dokuments fortfahren. GroupDocs.Editor ermöglicht es Ihnen, die Bearbeitungsoptionen an Ihre Bedürfnisse anzupassen.
### 2.1 Bearbeiten mit Standardoptionen
```csharp
EditableDocument defaultWordProcessingDoc = editor1.Edit();
```
Das Bearbeiten des Dokuments mit den Standardoptionen ist unkompliziert und erfordert nur minimale Konfiguration.
### 2.2 Bearbeiten mit benutzerdefinierten Optionen
Lassen Sie uns in erweiterte Konfigurationen eintauchen, indem Sie benutzerdefinierte Bearbeitungsoptionen angeben.
```csharp
WordProcessingEditOptions wordProcessingEditOptions1 = new WordProcessingEditOptions();
wordProcessingEditOptions1.EnablePagination = false;
wordProcessingEditOptions1.EnableLanguageInformation = true;
wordProcessingEditOptions1.FontExtraction = FontExtractionOptions.ExtractAllEmbedded;
EditableDocument version1WordProcessingDoc = editor1.Edit(wordProcessingEditOptions1);
```
In diesem Snippet haben wir die Paginierung deaktiviert, Sprachinformationen aktiviert und die Schriftartenextraktion so eingestellt, dass alle eingebetteten Schriftarten extrahiert werden.
### 2.3 Ein weiteres Konfigurationsbeispiel
Sie können das Dokument auch mit anderen Optionen bearbeiten:
```csharp
WordProcessingEditOptions wordProcessingEditOptions2 = new WordProcessingEditOptions(true);
wordProcessingEditOptions2.FontExtraction = FontExtractionOptions.ExtractAll;
EditableDocument version2WordProcessingDoc = editor1.Edit(wordProcessingEditOptions2);
```
Hier haben wir die Seitennummerierung aktiviert und die Schriftartenextraktion so eingestellt, dass alle Schriftarten extrahiert werden.
## Schritt 3: Laden und Bearbeiten einer Tabelle
Das Bearbeiten von Tabellenkalkulationen ist mit GroupDocs.Editor ebenso unkompliziert.
### 3.1 Laden Sie die Tabelle
```csharp
Editor editor2 = new Editor("Your Sample Document", delegate { return new SpreadsheetLoadOptions(); });
```
Dies initialisiert eine Editor-Instanz für ein Tabellenkalkulationsdokument.
### 3.2 Bearbeiten der ersten Registerkarte
```csharp
SpreadsheetEditOptions sheetTab1EditOptions = new SpreadsheetEditOptions();
sheetTab1EditOptions.WorksheetIndex = 0; // Der Index ist 0-basiert, dies ist also die erste Registerkarte
EditableDocument firstTab = editor2.Edit(sheetTab1EditOptions);
```
Sie können die erste Registerkarte der Tabelle mit den angegebenen Optionen bearbeiten.
### 3.3 Bearbeiten der zweiten Registerkarte
```csharp
SpreadsheetEditOptions sheetTab2EditOptions = new SpreadsheetEditOptions();
sheetTab2EditOptions.WorksheetIndex = 1; // Der Index ist 0-basiert, daher ist dies die zweite Registerkarte
EditableDocument secondTab = editor2.Edit(sheetTab2EditOptions);
```
In ähnlicher Weise bearbeitet dieser Codeausschnitt die zweite Registerkarte der Tabelle.
## Schritt 4: Inhalt extrahieren
Nachdem Sie Ihr Dokument bearbeitet haben, müssen Sie möglicherweise dessen Inhalt extrahieren. GroupDocs.Editor bietet hierfür verschiedene Methoden.
### 4.1 HTML-Inhalte abrufen
```csharp
string bodyContent = firstTab.GetBodyContent(); // HTML-Markup aus dem HTML->BODY-Element
string allContent = firstTab.GetContent(); // Vollständige HTML-Auszeichnung des gesamten Dokuments, einschließlich HTML->HEAD-Header und dessen Inhalt
```
Dieser Code extrahiert den HTML-Inhalt des bearbeiteten Dokuments.
### 4.2 Ressourcen extrahieren
```csharp
List<IImageResource> onlyImages = firstTab.Images;
List<IHtmlResource> allResourcesTogether = firstTab.AllResources;
```
Hier können Sie Bilder und alle anderen HTML-Ressourcen aus dem Dokument extrahieren.
## Schritt 5: Aufräumen
Vergessen Sie nicht, alle Instanzen zu löschen, um Ressourcen freizugeben.
```csharp
defaultWordProcessingDoc.Dispose();
version1WordProcessingDoc.Dispose();
version2WordProcessingDoc.Dispose();
firstTab.Dispose();
secondTab.Dispose();
editor1.Dispose();
editor2.Dispose();
```
Durch die ordnungsgemäße Entsorgung wird sichergestellt, dass in Ihrer Anwendung keine Speicherlecks oder Leistungsprobleme auftreten.
## Abschluss
 Herzlichen Glückwunsch! Sie haben jetzt ein solides Verständnis dafür, wie Sie mit GroupDocs.Editor für .NET Inhalte aus Textverarbeitungsdokumenten und Tabellenkalkulationen laden, bearbeiten und extrahieren können. Dieses leistungsstarke Tool vereinfacht die Dokumentbearbeitung und lässt sich nahtlos in Ihre .NET-Anwendungen integrieren. Weitere Einzelheiten finden Sie im[Dokumentation](https://tutorials.groupdocs.com/editor/net/), [Laden Sie die neueste Version herunter](https://releases.groupdocs.com/editor/net/) oder erhalten Sie eine[vorläufige Lizenz](https://purchase.groupdocs.com/temporary-license/).
## Häufig gestellte Fragen
### Kann ich PDF-Dokumente mit GroupDocs.Editor für .NET bearbeiten?
Derzeit unterstützt GroupDocs.Editor für .NET hauptsächlich die Formate Textverarbeitung, Tabellenkalkulation und Präsentation.
### Wie gehe ich effizient mit großen Dokumenten um?
Nutzen Sie die Bearbeitungsoptionen, um nur die erforderlichen Teile des Dokuments zu laden und zu verarbeiten, und stellen Sie sicher, dass Sie Instanzen ordnungsgemäß entsorgen, um den Speicher zu verwalten.
### Gibt es eine Begrenzung für die Dokumentgröße, die ich bearbeiten kann?
Es gibt keine strikten Größenbeschränkungen, aber die Leistung hängt von den Fähigkeiten Ihres Systems ab.
### Kann ich die HTML-Ausgabe weiter anpassen?
Ja, GroupDocs.Editor ermöglicht eine umfassende Anpassung der HTML-Ausgabe durch verschiedene Optionen und Einstellungen.
### Wo erhalte ich Unterstützung, wenn Probleme auftreten?
 Besuchen Sie die[GroupDocs.Editor-Supportforum](https://forum.groupdocs.com/c/editor/20) für Hilfe und Unterstützung.