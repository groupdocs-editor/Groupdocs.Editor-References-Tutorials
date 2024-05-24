---
title: Erweiterte Verwendung editierbarer Dokumente
linktitle: Erweiterte Verwendung editierbarer Dokumente
second_title: GroupDocs.Editor .NET API
description: Erlernen Sie die erweiterte Verwendung von GroupDocs.Editor für .NET zum programmgesteuerten Erstellen, Bearbeiten und Extrahieren von Ressourcen aus Dokumenten.
type: docs
weight: 11
url: /de/net/document-editing/advanced-usage-of-editable-documents/
---
## Einführung
Wenn Sie ein .NET-Entwickler sind und Ihre Dokumentbearbeitungsfunktionen verbessern möchten, bietet GroupDocs.Editor für .NET eine leistungsstarke Suite an Tools. Diese umfassende Anleitung führt Sie durch die erweiterte Verwendung bearbeitbarer Dokumente mit GroupDocs.Editor und erläutert jeden Schritt im Detail, damit Sie das volle Potenzial nutzen können.
## Voraussetzungen
Bevor Sie in die erweiterten Funktionen eintauchen, stellen Sie sicher, dass Sie über Folgendes verfügen:
- Visual Studio ist auf Ihrem Entwicklungscomputer installiert.
- .NET Framework kompatibel mit GroupDocs.Editor.
-  GroupDocs.Editor für .NET-Bibliothek. Sie können[hier herunterladen](https://releases.groupdocs.com/editor/net/).
-  Eine gültige GroupDocs.Editor-Lizenz. Sie erhalten eine[Kostenlose Testphase](https://releases.groupdocs.com/) oder kaufen Sie ein[vorläufige Lizenz](https://purchase.groupdocs.com/temporary-license/).
## Namespaces importieren
Stellen Sie zunächst sicher, dass Sie die erforderlichen Namespaces in Ihr .NET-Projekt importieren:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```
## Schritt 1: Erstellen einer EditableDocument-Instanz
 Zuerst müssen Sie eine Instanz von`EditableDocument` durch Laden und Bearbeiten eines Eingabedokuments eines unterstützten Formats.
```csharp
string inputFilePath = "YourSampleDocument.docx";
Editor editor = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```
In diesem Schritt laden wir das Eingabedokument und bereiten es für die Bearbeitung vor.
## Schritt 2: Dokumentressourcen extrahieren
 Der`EditableDocument` enthält verschiedene Ressourcen, die extrahiert und manipuliert werden können. Lassen Sie uns diese aufschlüsseln:
### Schritt 2.1: Gesamtes Dokument als HTML extrahieren
Sie können eine einzelne Zeichenfolge generieren, die das gesamte Dokument mit allen seinen als HTML eingebetteten Ressourcen enthält.
```csharp
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```
Diese Zeichenfolge wird ziemlich groß sein, da sie in Base64 codierte Stylesheets, Bilder und Schriftarten enthält.
### Schritt 2.2: Alle Bilder extrahieren
Extrahieren Sie alle Bilder aus dem Dokument.
```csharp
List<IImageResource> allImages = beforeEdit.Images;
```
### Schritt 2.3: Alle Schriftarten extrahieren
Extrahieren Sie alle im Dokument verwendeten Schriftarten.
```csharp
List<FontResourceBase> allFonts = beforeEdit.Fonts;
```
### Schritt 2.4: Alle Stylesheets extrahieren
Extrahieren Sie alle Stylesheets in ein Textformat.
```csharp
List<CssText> allStylesheets = beforeEdit.Css;
```
### Schritt 2.5: Alle Ressourcen sammeln
Sammeln Sie alle Ressourcen in einem Anruf.
```csharp
List<IHtmlResource> allResources = beforeEdit.AllResources;
```
Hierzu zählen Bilder, Schriftarten und Stylesheets.
### Schritt 2.6: HTML-Markup abrufen
Holen Sie sich die HTML-Auszeichnung des Dokuments ohne eingebettete Ressourcen.
```csharp
string htmlMarkup = beforeEdit.GetContent();
```
## Schritt 3: Externe Links anpassen
Manchmal müssen Sie externe Links anpassen, damit sie auf einen benutzerdefinierten Ressourcenhandler verweisen. So geht's:
### Schritt 3.1: Benutzerdefinierte Präfixe vorbereiten
Bereiten Sie Präfixe vor, die den ursprünglichen externen Links vorangestellt werden.
```csharp
string customImagesRequesthandlerUri = "http://beispiel.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://beispiel.com/CssHandler/id=";
string customFontsRequesthandlerUri = "http://beispiel.com/FontsHandler/id=";
```
### Schritt 3.2: Präfixiertes HTML-Markup generieren
Generieren Sie HTML-Markup mit angepassten Links.
```csharp
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```
### Schritt 3.3: Nur-Text-HTML-Inhalt abrufen
Einige WYSIWYG-Editoren verarbeiten nur reines HTML-Markup ohne Header.
```csharp
string onlyBodyContent = beforeEdit.GetBodyContent();
```
### Schritt 3.4: Nur-Text-Inhalte mit Präfix
Generieren Sie Nur-Text-Inhalte mit benutzerdefinierten Bildpräfixen.
```csharp
string prefixedBodyContent = beforeEdit.GetBodyContent(customImagesRequesthandlerUri);
```
### Schritt 3.5: Stylesheets extrahieren
Extrahieren Sie im Dokument verwendete Stylesheets.
```csharp
List<string> stylesheets = beforeEdit.GetCssContent();
```
### Schritt 3.6: Präfixierte Stylesheets
Extrahieren Sie Stylesheets mit benutzerdefinierten Präfixen.
```csharp
List<string> prefixedStylesheets = beforeEdit.GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri);
```
## Schritt 4: Dokument als HTML speichern
Speichern Sie das bearbeitete Dokument inklusive seiner Ressourcen als HTML-Datei.
```csharp
string htmlFilePath = Path.Combine("output", Path.GetFileNameWithoutExtension(inputFilePath) + ".html");
beforeEdit.Save(htmlFilePath);
```
Diese Methode erstellt ein separates Verzeichnis für Ressourcen wie Stylesheets, Bilder und Schriftarten.
## Schritt 5: EditableDocument entsorgen
 EditableDocument implementiert`IDisposable` und bietet die Möglichkeit zu überprüfen, ob die Instanz entsorgt wurde.
```csharp
Console.WriteLine("EditableDocument is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");
```
### Schritt 5.1 Verarbeiten des Dispose-Ereignisses
Sie können sich auch für die Veräußerungsaktion anmelden.
```csharp
EventHandler someMethod = delegate { Console.WriteLine("Disposing event was spotted!"); };
beforeEdit.Disposed += someMethod;
```
## Schritt 6: Editierbares Dokument aus HTML erstellen
Erstellen Sie eine Instanz von EditableDocument aus einem HTML-Dokument.
### Schritt 6.1: Aus einer HTML-Datei
```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
```
### Schritt 6.2: Aus HTML-Markup
```csharp
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);
```
Diese Instanzen (afterEditFromFile und afterEditFromMarkup) sind identisch mit dem Original (beforeEdit).
## Schritt 7: Manuelle Entsorgung
Entsorgen Sie Ihre EditableDocument-Instanzen manuell.
```csharp
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```
Dadurch wird eine ordnungsgemäße Bereinigung der Ressourcen sichergestellt.
## Abschluss
GroupDocs.Editor für .NET bietet robuste Tools zum programmgesteuerten Bearbeiten von Dokumenten. Indem Sie dieser Schritt-für-Schritt-Anleitung folgen, können Sie Dokumentinhalte, Ressourcen und Ausgabeformate effizient verwalten. Egal, ob Sie Ressourcen einbetten, externe Links anpassen oder Dokumente in HTML konvertieren, GroupDocs.Editor stattet Sie mit der Funktionalität aus, die Sie für die erweiterte Dokumentbearbeitung benötigen.
## Häufig gestellte Fragen
### Welche Formate unterstützt GroupDocs.Editor?
GroupDocs.Editor unterstützt verschiedene Formate, darunter DOCX, XLSX, PPTX und mehr.
### Kann ich GroupDocs.Editor ohne Lizenz verwenden?
 Ja, Sie können es mit einem[Kostenlose Testphase](https://releases.groupdocs.com/) oder ein[vorläufige Lizenz](https://purchase.groupdocs.com/temporary-license/).
### Wie extrahiere ich bestimmte Ressourcen aus einem Dokument?
 Sie können Bilder, Schriftarten und Stylesheets mit den bereitgestellten Methoden extrahieren, wie`Images`, `Fonts` , Und`Css`.
### Ist es möglich Links in der HTML-Ausgabe anzupassen?
Ja, Sie können externe Links anpassen, indem Sie benutzerdefinierte Präfixe für Bilder, CSS und Schriftarten angeben.
### Wie speichere ich ein bearbeitetes Dokument als HTML-Datei?
 Verwenden Sie die`Save` Methode der`EditableDocument`Klasse, um das Dokument einschließlich seiner Ressourcen als HTML-Datei zu speichern.