---
date: 2026-03-14
description: Lernen Sie, wie Sie PowerPoint-Präsentationen und andere Dokumenttypen
  mit GroupDocs.Editor für .NET bearbeiten. Der Leitfaden behandelt außerdem, wie
  Sie das bearbeitete Dokument speichern und Word-Dokumente in .NET bearbeiten.
linktitle: Create Document
second_title: GroupDocs.Editor .NET API
title: PowerPoint-Präsentation mit GroupDocs.Editor für .NET bearbeiten
type: docs
url: /de/net/document-editing/create-document/
weight: 10
---

# PowerPoint-Präsentation bearbeiten mit GroupDocs.Editor für .NET

## Einführung
Wenn Sie nach einer zuverlässigen Möglichkeit suchen, **PowerPoint-Präsentation bearbeiten** Dateien programmgesteuert zu bearbeiten, ist GroupDocs.Editor für .NET die Antwort. Diese Bibliothek ermöglicht Ihnen die Arbeit mit Word-, Excel-, PowerPoint-, Ebook- und E‑Mail-Formaten – alles über eine einzige, einfach zu nutzende API. In diesem Tutorial führen wir Sie durch das Erstellen und Bearbeiten jedes unterstützten Dokumenttyps, zeigen Ihnen, wie Sie **bearbeitetes Dokument speichern**‑Streams speichern, und geben Ihnen praktische Tipps, die Sie in realen Projekten anwenden können.

## Schnelle Antworten
- **Welche Bibliothek ermöglicht mir das Bearbeiten von PowerPoint-Dateien in .NET?** GroupDocs.Editor für .NET.  
- **Kann ich Word-, Excel- und Epub-Dateien mit derselben API bearbeiten?** Ja, die gleiche `Editor`‑Klasse unterstützt all diese Formate.  
- **Wie erfasse ich die bearbeitete Datei?** Stellen Sie eine Callback‑Funktion bereit (z. B. `SaveNewDocument`), die den Ergebnis‑Stream empfängt.  
- **Benötige ich eine Lizenz für den Produktionseinsatz?** Ja – erwerben Sie eine Lizenz oder nutzen Sie eine temporäre Testlizenz.  
- **Welche .NET‑Versionen werden unterstützt?** .NET Framework 4.0+, .NET Core und .NET 5/6.

## Was bedeutet „PowerPoint-Präsentation bearbeiten“ mit GroupDocs.Editor?
Das Bearbeiten einer PowerPoint‑Präsentation bedeutet, eine `.pptx`‑Datei zu laden, Änderungen vorzunehmen (wie das Modifizieren von Folien, Text oder versteckten Elementen) und anschließend die aktualisierte Datei abzurufen – und das alles, ohne dass Microsoft Office installiert sein muss.

## Warum GroupDocs.Editor für .NET verwenden?
- **Einzelne API für viele Formate** – Keine Notwendigkeit, separate Bibliotheken für Word, Excel oder Epub zu jonglieren.  
- **Keine Office‑Abhängigkeit** – Funktioniert auf Servern, in Containern und CI‑Pipelines.  
- **Feinkörnige Kontrolle** – Paginierung, Sprachinformationen, Schriftart‑Extraktion und mehr anpassen.  
- **Stream‑basierte Verarbeitung** – Ideal für Cloud‑Dienste, bei denen Sie mit Memory‑Streams statt physischen Dateien arbeiten.

## Voraussetzungen
- Visual Studio (irgendeine aktuelle Edition).  
- .NET Framework 4.0 oder höher (oder .NET Core/.NET 5+).  
- GroupDocs.Editor für .NET Bibliothek – laden Sie sie von [hier](https://releases.groupdocs.com/editor/net/) herunter.  
- Grundkenntnisse in C#.

## Namespaces importieren
Zuerst importieren Sie die Namespaces, die die Kernklassen enthalten, die wir verwenden werden.

```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using System.IO;
```

## Schritt 1: Stream einrichten
Wir verwenden einen Memory‑Stream als Platzhalter für den Dokumentinhalt.

```csharp
Stream memoryStream = Stream.Null;
```

## Schritt 2: Callback‑Funktion zum **bearbeitetes Dokument speichern**
Definieren Sie einen Callback, der den bearbeiteten Stream empfängt und ihn in `memoryStream` speichert.

```csharp
void SaveNewDocument(Stream resultStream)
{
    memoryStream = resultStream;
}
```

## Schritt 3: Erstellen und Bearbeiten eines WordProcessing-Dokuments  
(Hier **Word-Dokument .net bearbeiten**.)

### Erstellen und Bearbeiten mit Standardoptionen
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    EditableDocument defaultWordProcessingDoc = editor.Edit();
}
```

### Erstellen und Bearbeiten mit benutzerdefinierten Optionen
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    WordProcessingEditOptions wordProcessingEditOptions = new WordProcessingEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true,
        FontExtraction = FontExtractionOptions.ExtractAllEmbedded
    };
    EditableDocument editableWordProcessingDocument = editor.Edit(wordProcessingEditOptions);
}
```

## Schritt 4: Erstellen und Bearbeiten eines Spreadsheet-Dokuments  
(Verwenden Sie dies, um **Excel-Datei .net bearbeiten**.)

### Erstellen und Bearbeiten mit Standardoptionen
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    EditableDocument defaultEditableSpreadsheetDocument = editor.Edit();
}
```

### Erstellen und Bearbeiten mit benutzerdefinierten Optionen
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    SpreadsheetEditOptions spreadsheetEditOptions = new SpreadsheetEditOptions
    {
        WorksheetIndex = 0,
        ExcludeHiddenWorksheets = true
    };
    EditableDocument editableSpreadsheetDocument = editor.Edit(spreadsheetEditOptions);
}
```

## Schritt 5: **PowerPoint-Präsentation bearbeiten** – Erstellen und Bearbeiten eines Präsentationsdokuments
### Erstellen und Bearbeiten mit Standardoptionen
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    EditableDocument defaultEditablePresentationDocument = editor.Edit();
}
```

### Erstellen und Bearbeiten mit benutzerdefinierten Optionen
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    PresentationEditOptions presentationEditOptions = new PresentationEditOptions
    {
        ShowHiddenSlides = false,
        SlideNumber = 0
    };
    EditableDocument editablePresentationDocument = editor.Edit(presentationEditOptions);
}
```

## Schritt 6: Erstellen und Bearbeiten eines Ebook-Dokuments  
(Hier **epub-Datei bearbeiten**.)

### Erstellen und Bearbeiten mit Standardoptionen
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EditableDocument defaultEditableEbookDocument = editor.Edit();
}
```

### Erstellen und Bearbeiten mit benutzerdefinierten Optionen
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EbookEditOptions ebookEditOptions = new EbookEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true
    };
    EditableDocument editableEbookDocument = editor.Edit(ebookEditOptions);
}
```

## Schritt 7: Erstellen und Bearbeiten eines E‑Mail‑Dokuments
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EditableDocument defaultEditableEmailDocument = editor.Edit();
}
```

### Erstellen und Bearbeiten mit benutzerdefinierten Optionen
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EmailEditOptions emailEditOptions = new EmailEditOptions
    {
        MailMessageOutput = MailMessageOutput.All
    };
    EditableDocument editableEmailDocument = editor.Edit(emailEditOptions);
}
```

## Schritt 8: Prozess abschließen
Entsorgen Sie den Stream, um Ressourcen freizugeben, sobald Sie fertig sind.

```csharp
memoryStream.Dispose();
System.Console.WriteLine("CreateDocument routine has successfully finished");
```

## Häufige Fallstricke & Tipps
- **Vergessen Sie niemals, den Stream zu entsorgen** – lässt man ihn offen, kann das in langlaufenden Diensten zu Speicherlecks führen.  
- **Beim Bearbeiten von PowerPoint stellen Sie sicher, dass `SlideNumber` korrekt gesetzt ist**; sonst kann die erste Folie dupliziert werden.  
- **Wenn Sie den ursprünglichen Dateinamen beibehalten müssen**, speichern Sie ihn vor dem Callback und benennen Sie den Ausgabestream nach dem Bearbeiten um.  
- **Bei großen Dokumenten** sollten Sie die Verarbeitung in Chunks erwägen oder `Editor` mit einer temporären Datei verwenden, um hohen Speicherverbrauch zu vermeiden.

## Häufig gestellte Fragen

**F: Welche Dokumenttypen kann ich mit GroupDocs.Editor für .NET bearbeiten?**  
A: Sie können WordProcessing-, Tabellenkalkulations-, Präsentations-, Ebook- und E‑Mail-Dokumente bearbeiten – einschließlich PowerPoint‑Dateien für den Anwendungsfall **PowerPoint-Präsentation bearbeiten**.

**F: Ist es möglich, die Bearbeitungsoptionen anzupassen?**  
A: Ja, jedes Format hat seine eigene Optionsklasse (z. B. `WordProcessingEditOptions`, `SpreadsheetEditOptions`, `PresentationEditOptions`), die Ihnen ermöglicht, Paginierung, versteckte Folien, Arbeitsblatt‑Auswahl usw. fein abzustimmen.

**F: Wie gehe ich mit der Ausgabe der bearbeiteten Dokumente um?**  
A: Verwenden Sie die Callback‑Funktion (`SaveNewDocument`), um den bearbeiteten Stream zu erfassen, dann können Sie ihn auf die Festplatte, in eine Datenbank schreiben oder von einer Web‑API zurückgeben.

**F: Benötige ich eine Lizenz, um GroupDocs.Editor für .NET zu verwenden?**  
A: Ja, für den Produktionseinsatz ist eine Lizenz erforderlich. Sie können eine Lizenz von [hier](https://purchase.groupdocs.com/buy) erhalten. Eine temporäre Testlizenz ist ebenfalls verfügbar.

**F: Wo finde ich ausführlichere Dokumentation?**  
A: Detaillierte Dokumentation ist auf der [GroupDocs.Editor für .NET Dokumentationsseite](https://tutorials.groupdocs.com/editor/net/) verfügbar.

## Fazit
GroupDocs.Editor für .NET macht es einfach, **PowerPoint-Präsentationen** zu bearbeiten und eine breite Palette anderer Dokumenttypen. Wenn Sie den obigen Schritten folgen, können Sie Dokumente erstellen, ändern und **bearbeitete Dokumente**‑Streams vollständig im Code speichern, ohne auf Office‑Installationen angewiesen zu sein. Erkunden Sie die erweiterten Optionen der Bibliothek, um das Bearbeitungserlebnis an Ihre spezifischen Geschäftsanforderungen anzupassen.

---

**Zuletzt aktualisiert:** 2026-03-14  
**Getestet mit:** GroupDocs.Editor für .NET (neueste Version)  
**Autor:** GroupDocs