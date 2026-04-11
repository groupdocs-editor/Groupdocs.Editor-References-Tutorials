---
date: '2026-04-11'
description: Erfahren Sie, wie Sie ein bearbeitbares Dokument mit GroupDocs.Editor
  für .NET erstellen und das Dokument effizient als HTML speichern.
keywords:
- create editable document
- extract images from document
- save document as html
title: Erstellen Sie ein bearbeitbares Dokument mit GroupDocs.Editor .NET
type: docs
url: /de/net/document-editing/groupdocs-editor-net-edit-manage-documents-guide/
weight: 1
---

# Erstellen eines editierbaren Dokuments mit GroupDocs.Editor .NET

Im heutigen digitalen Zeitalter ist **das Erstellen eines editierbaren Dokuments** eine zentrale Anforderung für jeden modernen Arbeitsablauf. Egal, ob Sie einen kollaborativen Editor, ein Content‑Management‑System oder ein automatisiertes Reporting‑Tool entwickeln, die Möglichkeit, HTML‑Dateien programmgesteuert zu bearbeiten und zu speichern, kann unzählige Stunden sparen. Dieses Tutorial zeigt Ihnen, wie Sie **editierbares Dokument erstellen**, Ressourcen extrahieren und **Dokument als HTML speichern** mit GroupDocs.Editor für .NET.

## Schnelle Antworten
- **Was bedeutet „editierbares Dokument erstellen“?** Es bedeutet, dass eine Quelldatei in ein GroupDocs.Editor `EditableDocument`‑Objekt geladen wird, das Sie programmgesteuert ändern können.  
- **Welche Formate kann ich in HTML konvertieren?** Word, Excel, PowerPoint und viele andere Office‑Formate werden unterstützt.  
- **Wie extrahiere ich Bilder aus einem Dokument?** Verwenden Sie die `EditableDocument.Images`‑Sammlung.  
- **Kann ich einen einzelnen HTML‑String mit allen eingebetteten Ressourcen erzeugen?** Ja – rufen Sie `GetEmbeddedHtml()` auf.  
- **Benötige ich eine Lizenz für die Produktion?** Eine Testversion funktioniert für die Evaluierung; für den kommerziellen Einsatz ist eine permanente Lizenz erforderlich.

## Was ist „editierbares Dokument erstellen“?
Das Erstellen eines editierbaren Dokuments bedeutet, dass eine Quelldatei (z. B. eine .docx) in GroupDocs.Editor geladen wird, das ein `EditableDocument`‑Objekt zurückgibt. Dieses Objekt stellt das HTML‑Markup, Bilder, Schriftarten und CSS des Dokuments bereit, sodass Sie den Inhalt bearbeiten, Ressourcen ersetzen oder das Ganze in eine Webseite einbetten können.

## Warum GroupDocs.Editor .NET für diese Aufgabe verwenden?
- **Vollständige API** – Unterstützt Word, Excel, PowerPoint und mehr.  
- **Ressourcenauszug** – Extrahiert Bilder, Schriftarten und Stylesheets mit einfachen Eigenschaften.  
- **Einbettung von HTML** – Erzeugt einen einzelnen HTML‑String, der alle Ressourcen enthält, ideal für E‑Mails oder Single‑Page‑Apps.  
- **Leistungsorientiert** – Objekte sofort freigeben und bei Bedarf asynchrone Muster verwenden.

## Voraussetzungen
Bevor Sie GroupDocs.Editor .NET‑Funktionen implementieren, stellen Sie sicher:
- **.NET‑Umgebung**: Richten Sie Ihre Entwicklungsumgebung für .NET‑Anwendungen ein.
- **Bibliotheken & Abhängigkeiten**:
  - Installieren Sie GroupDocs.Editor mit einer dieser Methoden:
    - **.NET CLI**
      ```bash
      dotnet add package GroupDocs.Editor
      ```
    - **Package Manager**
      ```powershell
      Install-Package GroupDocs.Editor
      ```
    - **NuGet Package Manager UI**: Search and install the latest version.
- **Wissensvoraussetzungen**: Vertrautheit mit C#‑Programmierung und grundlegenden Dokumenten‑Handling‑Konzepten wird empfohlen.

## Einrichtung von GroupDocs.Editor für .NET
### Installationsanleitung
Um zu beginnen, richten Sie GroupDocs.Editor in Ihrem Projekt ein:
1. **Installation über .NET CLI**:
   ```bash
   dotnet add package GroupDocs.Editor
   ```
2. **Verwendung des Package Managers**:
   - Open the Package Manager Console and run:
     ```powershell
     Install-Package GroupDocs.Editor
     ```
3. **NuGet Package Manager UI**: 
   - Navigate to NuGet, search for "GroupDocs.Editor", and install.

### Lizenzbeschaffung
- **Kostenlose Testversion & temporäre Lizenz**: Beginnen Sie mit einer kostenlosen Testversion, indem Sie sie von [GroupDocs releases](https://releases.groupdocs.com/editor/net/) herunterladen. Für erweitertes Testen beantragen Sie eine temporäre Lizenz auf der [Kaufseite](https://purchase.groupdocs.com/temporary-license).

### Grundlegende Initialisierung und Einrichtung
So initialisieren Sie GroupDocs.Editor in Ihrer Anwendung:
```csharp
using System;
using GroupDocs.Editor;

string inputFilePath = "YOUR_DOCUMENT_DIRECTORY"; // Replace with your actual document path
Editor editor = new Editor(inputFilePath, new WordProcessingLoadOptions());
```

## Wie man ein editierbares Dokument mit GroupDocs.Editor .NET erstellt
### Erstellen einer EditableDocument‑Instanz
**Übersicht**: Laden und bearbeiten Sie Dokumente, indem Sie eine `EditableDocument`‑Instanz erstellen.

#### Laden eines Dokuments
```csharp
using GroupDocs.Editor.Options;

// Load your document with appropriate options
Editor editor = new Editor(inputFilePath, new WordProcessingLoadOptions());

// Create EditableDocument from the loaded file
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```

## Wie man eingebettetes HTML generiert
### Erzeugen von eingebettetem HTML aus EditableDocument
**Übersicht**: Konvertieren Sie ein komplettes Dokument in einen einzelnen eingebetteten HTML‑String mit Stylesheets und Ressourcen.
```csharp
using System.Collections.Generic;
using GroupDocs.Editor.HtmlCss.Resources;

// Generate embedded HTML
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```

## Wie man Bilder aus einem Dokument extrahiert
### Extrahieren von Ressourcen aus EditableDocument
**Übersicht**: Rufen Sie Bilder, Schriftarten, CSS und andere Ressourcen aus Ihrem Dokument ab.
```csharp
List<IImageResource> allImages = beforeEdit.Images;
List<FontResourceBase> allFonts = beforeEdit.Fonts;
List<CssText> allStylesheets = beforeEdit.Css;
List<IHtmlResource> allResources = beforeEdit.AllResources;
```

## Wie man Schriftarten aus einem Dokument extrahiert
*Der gleiche Codeblock oben zeigt auch, wie Sie Schriftart‑Ressourcen über `beforeEdit.Fonts` abrufen können.*

## Wie man reinen HTML‑Inhalt erhält
### Abrufen von HTML‑Inhalt aus EditableDocument
**Übersicht**: Extrahieren Sie reinen HTML‑Inhalt ohne eingebettete Ressourcen.
```csharp
string htmlMarkup = beforeEdit.GetContent();
```

## Wie man externe Links im HTML‑Inhalt anpasst
### Anpassen externer Links im HTML‑Inhalt
**Übersicht**: Ändern Sie externe Links für Bilder, CSS und Schriftarten mithilfe benutzerdefinierter Präfixe.
```csharp
using System.Collections.Generic;

// Define custom handlers for resource URLs
string customImagesRequesthandlerUri = "http://example.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://example.com/CssHandler/id=";

// Adjust HTML content with prefixed links
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```

## Wie man ein Dokument als HTML speichert
### Speichern von EditableDocument als HTML‑Datei
**Übersicht**: Speichern Sie das bearbeitete Dokument wieder auf dem Datenträger im HTML‑Format.
```csharp
using System.IO;

string htmlFilePath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "document.html"); // Adjust the output path
beforeEdit.Save(htmlFilePath);
```

## Freigabe und Ereignisbehandlung für EditableDocument
**Übersicht**: Verwalten Sie die Ressourcenfreigabe und behandeln Sie Ereignisse im Zusammenhang mit dem Dokumentlebenszyklus.
```csharp
Console.WriteLine("beforeEdit variable of EditableDocument type is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");

// Subscribe to the disposing event
EventHandler someMethod = delegate {
    Console.WriteLine("Disposing event was spotted!");
};
beforeEdit.Disposed += someMethod;
```

## Wie man ein editierbares Dokument aus HTML‑Inhalt erstellt
### Erstellen von EditableDocument aus HTML‑Inhalt
**Übersicht**: Rekonstruieren Sie eine `EditableDocument`‑Instanz aus vorhandenem HTML‑Inhalt.
```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);

// Dispose resources once done
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```

## Praktische Anwendungen
GroupDocs.Editor .NET kann in zahlreichen realen Szenarien eingesetzt werden:
- **Kollaboratives Bearbeiten**: Ermöglicht nahtloses Dokumenten‑Editing durch mehrere Benutzer.  
- **Web‑Veröffentlichung**: Konvertiert Dokumente in web‑freundliche Formate für die Online‑Ansicht und Interaktion.  
- **Content‑Management‑Systeme**: Integriert sich in CMS‑Plattformen, um dynamische Inhaltsaktualisierungen zu ermöglichen.  
- **Automatisierte Berichtserstellung**: Automatisiert die Erstellung und Formatierung von Berichten aus verschiedenen Datenquellen.

## Leistungsüberlegungen
Um die Leistung von GroupDocs.Editor .NET zu optimieren:
- Verwalten Sie den Speicher effizient, indem Sie Objekte nach Gebrauch sofort freigeben.
- Minimieren Sie die Ladezeiten von Ressourcen, indem Sie Dateipfade und URLs optimieren.
- Verwenden Sie asynchrone Verarbeitung, wo möglich, um die Anwendungs‑Reaktionsfähigkeit zu verbessern.

## Häufige Probleme und Lösungen
- **Große Dateien verursachen hohen Speicherverbrauch** – Geben Sie `EditableDocument`‑Objekte sofort frei, sobald Sie die Verarbeitung abgeschlossen haben.  
- **Defekte Bildlinks nach der Konvertierung** – Stellen Sie sicher, dass Sie die korrekten Resource‑Handler‑URIs beim Aufruf von `GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri)` verwenden.  
- **Fehlende Schriftarten im generierten HTML** – Prüfen Sie, ob das Quelldokument die erforderlichen Schriftarten einbettet oder ob sie auf dem Server verfügbar sind.

## Häufig gestellte Fragen
**Q: Ist GroupDocs.Editor .NET mit allen Dokumentformaten kompatibel?**  
A: GroupDocs.Editor unterstützt eine breite Palette von Formaten, einschließlich Word, Excel, PowerPoint und vielen anderen, und bietet Ihnen Flexibilität für verschiedene Anwendungsfälle.

**Q: Wie gehe ich effizient mit großen Dateien um, wenn ich GroupDocs.Editor verwende?**  
A: Verwenden Sie nach Möglichkeit asynchrone APIs, verarbeiten Sie Dateien in Teilen, wenn möglich, und geben Sie `EditableDocument`‑ und `Editor`‑Objekte stets sofort frei, um Speicher freizugeben.

**Q: Kann ich GroupDocs.Editor in Cloud‑Speicher‑Lösungen integrieren?**  
A: Ja, Sie können Azure Blob Storage, Amazon S3, Google Cloud Storage oder einen anderen Cloud‑Anbieter anbinden, indem Sie die Dateistreams in den `Editor`‑Konstruktor übergeben.

**Q: Welche Lizenzierungsoptionen gibt es für GroupDocs.Editor?**  
A: Sie können mit einer kostenlosen Testversion beginnen oder eine temporäre Lizenz für die Evaluierung beantragen. Für den Produktionseinsatz ist eine kostenpflichtige Lizenz erforderlich.

**Q: Wo kann ich Unterstützung erhalten, wenn ich auf Probleme stoße?**  
A: Das [GroupDocs Support Forum](https://forum.groupdocs.com) steht für Hilfe zur Verfügung, und Sie können auch das GroupDocs‑Support‑Team direkt kontaktieren.

---

**Zuletzt aktualisiert:** 2026-04-11  
**Getestet mit:** GroupDocs.Editor 23.12 for .NET  
**Autor:** GroupDocs  

---