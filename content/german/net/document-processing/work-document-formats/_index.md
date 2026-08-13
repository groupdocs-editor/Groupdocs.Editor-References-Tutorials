---
date: 2026-06-06
description: Erfahren Sie, wie Sie unterstützte Dokumentformate auflisten und die
  Dateiformaterweiterung mit GroupDocs.Editor für .NET bestimmen. Schritt‑für‑Schritt‑Anleitung
  mit Code‑Beispielen, schnellen Antworten und FAQs.
keywords:
- list supported document formats
- determine file format extension
- GroupDocs.Editor .NET
- document editing API
- supported formats guide
linktitle: Unterstützte Dokumentformate auflisten
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to list supported document formats and determine file format
    extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets,
    quick answers, and FAQs.
  headline: List Supported Document Formats with GroupDocs.Editor .NET
  type: TechArticle
- description: Learn how to list supported document formats and determine file format
    extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets,
    quick answers, and FAQs.
  name: List Supported Document Formats with GroupDocs.Editor .NET
  steps:
  - name: '**.NET development environment** – Visual Studio 2022 or any IDE that supports
      .NET 6+.'
    text: '**.NET development environment** – Visual Studio 2022 or any IDE that supports
      .NET 6+.'
  - name: '**GroupDocs.Editor for .NET library** – download from the [GroupDocs releases
      page](https://releases.groupdocs.com/editor/net/).'
    text: '**GroupDocs.Editor for .NET library** – download from the [GroupDocs releases
      page](https://releases.groupdocs.com/editor/net/).'
  - name: '**Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/)
      for unrestricted access.'
    text: '**Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/)
      for unrestricted access.'
  - name: '**Basic C# knowledge** – familiarity with namespaces, `using` statements,
      and console output.'
    text: '**Basic C# knowledge** – familiarity with namespaces, `using` statements,
      and console output.'
  - name: '**Loop Through Formats:** We iterate over all available Word‑processing
      formats.'
    text: '**Loop Through Formats:** We iterate over all available Word‑processing
      formats.'
  - name: '**Output Format Details:** For each format we print its friendly name and
      default file extension.'
    text: '**Output Format Details:** For each format we print its friendly name and
      default file extension.'
  - name: '**Loop Through Formats:** The same looping logic applies to presentations.'
    text: '**Loop Through Formats:** The same looping logic applies to presentations.'
  - name: '**Output Format Details:** The name and extension are displayed for each
      format.'
    text: '**Output Format Details:** The name and extension are displayed for each
      format.'
  - name: '**Parse Format:** `FromExtension` converts the `.xlsm` extension into its
      internal `SpreadsheetFormat` enum.'
    text: '**Parse Format:** `FromExtension` converts the `.xlsm` extension into its
      internal `SpreadsheetFormat` enum.'
  - name: '**Output Format:** The parsed format’s name is printed, confirming the
      mapping.'
    text: '**Output Format:** The parsed format’s name is printed, confirming the
      mapping.'
  type: HowTo
- questions:
  - answer: '`DocumentFormatInfo` provides metadata about supported file types, while
      `SaveOptions` configures how a document is written back to disk (format, compression,
      etc.).'
    question: What is the difference between `DocumentFormatInfo` and `SaveOptions`?
  - answer: Yes—use `DocumentFormatInfo.FromExtension("yourExt")`; if the extension
      isn’t recognized, the method returns `null`.
    question: Can I list formats for a custom file extension?
  - answer: Absolutely. Pass the password to the `Editor` constructor via `EditorSettings`
      to open encrypted documents.
    question: Does GroupDocs.Editor support password‑protected files?
  - answer: Over **30 input and output formats**, spanning Word, Excel, PowerPoint,
      HTML, and plain text.
    question: How many formats does GroupDocs.Editor actually support?
  - answer: Use the `GetEditableWordProcessingFormats()` (or Spreadsheet/Presentation
      equivalents) to retrieve formats that allow full edit capabilities.
    question: Is there a way to restrict the list to only editable formats?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Unterstützte Dokumentformate auflisten mit GroupDocs.Editor .NET
type: docs
url: /de/net/document-processing/work-document-formats/
weight: 13
---

# Liste unterstützter Dokumentformate

Willkommen zu unserem umfassenden Tutorial, wie man **unterstützte Dokumentformate** mit GroupDocs.Editor für .NET auflistet. Egal, ob Sie eine dokumenten‑zentrierte Web‑App oder ein Enterprise‑Desktop‑Tool bauen, es ist entscheidend zu wissen, welche Formate Sie bearbeiten oder konvertieren können. In diesem Leitfaden erfahren Sie, wie Sie Formate enumerieren, Erweiterungen parsen und Dokumente bearbeiten – alles mit klaren, benutzerfreundlichen Erklärungen und sofort ausführbaren Code‑Snippets.

## Schnelle Antworten
- **Wie liste ich alle unterstützten Formate auf?** Verwenden Sie `DocumentFormatInfo.GetSupportedWordProcessingFormats()` (bzw. die entsprechenden Methoden für Präsentationen/Tabellen) und iterieren Sie über die Sammlung.  
- **Kann ich ein Format anhand einer Dateierweiterung bestimmen?** Ja – rufen Sie `DocumentFormatInfo.FromExtension(".docx")` auf.  
- **Welche Dateitypen unterstützt GroupDocs.Editor?** Mehr als 30 Eingabe‑ und Ausgabeformate, darunter DOCX, XLSX, PPTX, HTML und Nur‑Text.  
- **Benötige ich eine Lizenz, um Formate aufzulisten?** Eine temporäre Lizenz schaltet die komplette API frei; andernfalls funktioniert eine Testversion mit eingeschränkten Funktionen.  
- **Welche .NET‑Versionen sind kompatibel?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.

## Was bedeutet „unterstützte Dokumentformate auflisten“?
Der Ausdruck bezieht sich darauf, programmgesteuert die Sammlung von Dateitypen abzurufen, die GroupDocs.Editor öffnen, bearbeiten und speichern kann. Dieser Vorgang ermöglicht es Ihnen, dynamische UI‑Dropdowns zu erstellen oder Benutzer‑Uploads vor der Verarbeitung zu validieren, sodass nur kompatible Dateien an den Editor übergeben werden.

## Warum unterstützte Dokumentformate auflisten?
GroupDocs.Editor **unterstützt über 30 Eingabe‑ und Ausgabeformate** und kann Dateien bis zu **2 GB** verarbeiten, ohne das gesamte Dokument in den Speicher zu laden. Das genaue Wissen um die unterstützten Formate verhindert Laufzeitfehler, verbessert die Benutzererfahrung und erlaubt Ihnen, Geschäftsregeln wie „nur editierbare Office‑Dokumente zulassen“ durchzusetzen. Zudem können Sie Benutzern nur die Formate anzeigen, die Ihre Anwendung tatsächlich unterstützt.

## Voraussetzungen
Bevor Sie beginnen, stellen Sie sicher, dass Sie Folgendes haben:

1. **.NET‑Entwicklungsumgebung** – Visual Studio 2022 oder jede IDE, die .NET 6+ unterstützt.  
2. **GroupDocs.Editor für .NET‑Bibliothek** – herunterladen von der [GroupDocs releases page](https://releases.groupdocs.com/editor/net/).  
3. **Temporäre Lizenz** – erhalten Sie eine [temporary license](https://purchase.groupdocs.com/temporary-license/) für uneingeschränkten Zugriff.  
4. **Grundkenntnisse in C#** – Vertrautheit mit Namespaces, `using`‑Anweisungen und Konsolenausgabe.

## Wie listet man unterstützte Dokumentformate auf?
Laden Sie die Sammlung der unterstützten Formate und geben Sie für jedes Format den Namen und die Dateierweiterung aus. Dieses zweistufige Muster funktioniert für Word‑Processing, Tabellen‑ und Präsentationsdokumente. Durch das Durchlaufen der Sammlung können Sie UI‑Elemente wie Dropdowns dynamisch befüllen, sodass Benutzer nur Formate auswählen können, die der Editor tatsächlich handhaben kann.

```csharp
// No actual code block – placeholder retained from original tutorial
```csharp
using System;
using GroupDocs.Editor.Options;
```
```

### Auflisten von Word‑Processing‑Formaten
`Formats.WordProcessingFormats` ist eine Aufzählung, die jeden vom Editor erkannten Word‑Processing‑Dateityp beschreibt. Die Eigenschaft `All` liefert eine Sammlung dieser Formatobjekte.

```csharp
```csharp
foreach (Formats.WordProcessingFormats oneFormat in Formats.WordProcessingFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**Erklärung:**  
1. **Durchlaufen der Formate:** Wir iterieren über alle verfügbaren Word‑Processing‑Formate.  
2. **Ausgabe der Formatinformationen:** Für jedes Format geben wir den benutzerfreundlichen Namen und die Standard‑Dateierweiterung aus.

### Auflisten von Präsentationsformaten
`Formats.PresentationFormats` funktioniert auf dieselbe Weise für Folien‑Dateien und stellt jeden unterstützten Präsentationstyp über die Sammlung `All` bereit.

```csharp
```csharp
foreach (Formats.PresentationFormats oneFormat in Formats.PresentationFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**Erklärung:**  
1. **Durchlaufen der Formate:** Die gleiche Schleifenlogik gilt für Präsentationen.  
2. **Ausgabe der Formatinformationen:** Name und Erweiterung werden für jedes Format angezeigt.

## Wie bestimmt man die Dateiformat‑Erweiterung?
Manchmal haben Sie nur einen Dateinamen und müssen das zugehörige `DocumentFormat` ableiten. GroupDocs.Editor bietet einen einfachen statischen Helfer, der eine Dateierweiterung ihrer internen Format‑Repräsentation zuordnet, sodass Sie Dateien vor dem Laden in den Editor validieren oder konvertieren können.

### Parsen von Tabellenformaten
`Formats.SpreadsheetFormats.FromExtension` wandelt einen Dateierweiterungs‑String in den passenden Tabellen‑Format‑Enum‑Wert um.

```csharp
```csharp
Formats.SpreadsheetFormats expectedXlsm = Formats.SpreadsheetFormats.FromExtension(".xlsm");
Console.WriteLine("Parsed Spreadsheet format is {0}", expectedXlsm.Name);
```
```

**Erklärung:**  
1. **Format parsen:** `FromExtension` konvertiert die Erweiterung `.xlsm` in das interne `SpreadsheetFormat`‑Enum.  
2. **Ausgabe des Formats:** Der Name des geparsten Formats wird ausgegeben, um die Zuordnung zu bestätigen.

### Parsen von Textformaten
Analog dazu löst `Formats.TextualFormats.FromExtension` textbasierte Dateierweiterungen wie HTML oder TXT auf.

```csharp
```csharp
Formats.TextualFormats expectedHtml = Formats.TextualFormats.FromExtension("html");
Console.WriteLine("Parsed Textual format is {0}", expectedHtml.Name);
```
```

**Erklärung:**  
1. **Format parsen:** Die Methode `FromExtension` ordnet die Erweiterung `html` einem `TextFormat` zu.  
2. **Ausgabe des Formats:** Der Name des Textformats wird angezeigt, was für web‑basierte Editoren nützlich ist.

## Wie bearbeitet man Dokumente nach der Formatbestimmung?
Sobald Sie das Format kennen, folgt das Laden und Bearbeiten eines Dokuments einem konsistenten Muster. Zuerst erstellen Sie eine `Editor`‑Instanz mit dem Pfad zur Quelldatei, dann rufen Sie `Edit()` auf, um ein `EditableDocument` zu erhalten. Von dort aus können Sie den Inhalt lesen, ändern und schließlich mit passenden `SaveOptions` speichern.

### Laden eines Dokuments
`Editor` ist die Kernklasse, die alle Bearbeitungsoperationen für eine gegebene Datei kapselt.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/document.docx"))
{
    // Further steps will be covered here.
}
```
```

**Erklärung:**  
1. **Editor initialisieren:** Erstellen Sie eine `Editor`‑Instanz und übergeben Sie den vollständigen Pfad der Zieldatei.  
2. **Dispose‑Muster:** Die `using`‑Anweisung stellt sicher, dass alle nicht verwalteten Ressourcen sofort freigegeben werden.

### Extrahieren von Inhalt
`EditableDocument.GetContent()` liefert den Rohtext des Dokuments (oder HTML für web‑basierte Editoren), den Sie anzeigen oder manipulieren können.

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    string content = editableDocument.GetContent();
    Console.WriteLine(content);
}
```
```

**Erklärung:**  
1. **Edit‑Methode:** `Edit()` gibt ein `EditableDocument`‑Objekt zurück.  
2. **Inhalt holen:** `GetContent()` extrahiert den Rohtext des Dokuments (oder HTML für web‑basierte Editoren).  
3. **Inhalt ausgeben:** Der Inhalt wird zur Überprüfung in die Konsole geschrieben.

### Änderungen speichern
`SaveOptions` gibt dem Editor vor, wie und in welchem Format das bearbeitete Dokument zurück in den Speicher geschrieben wird.

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    // Modify content here
    SaveOptions saveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docx);
    editor.Save(editableDocument, "path/to/save/document.docx", saveOptions);
}
```
```

**Erklärung:**  
1. **Edit‑Methode erneut aufrufen:** Holen Sie das `EditableDocument` nach den Änderungen erneut.  
2. **Inhalt ändern:** Nehmen Sie Ihre Änderungen am String vor (hier nicht gezeigt).  
3. **Speicheroptionen:** Konfigurieren Sie `SaveOptions` mit dem gewünschten Ausgabeformat.  
4. **Dokument speichern:** Persistieren Sie die bearbeitete Datei wieder auf dem Datenträger.

## Wie arbeitet man mit verschiedenen Dokumenttypen?
GroupDocs.Editor abstrahiert die Behandlung von Word, Tabellen und Präsentationen hinter derselben API‑Oberfläche, sodass Sie den Kontext wechseln können, ohne für jede Dokumentfamilie neue Klassen lernen zu müssen.

### Bearbeiten von Tabellendokumenten
`SpreadsheetSaveOptions` definiert, wie eine Tabelle geschrieben wird, einschließlich Format und optionaler Komprimierungseinstellungen.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/spreadsheet.xlsx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // Modify content here
        SaveOptions saveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsx);
        editor.Save(editableDocument, "path/to/save/spreadsheet.xlsx", saveOptions);
    }
}
```
```

**Erklärung:**  
1. **Editor initialisieren:** Pfad zu einer Tabellendatei an den `Editor`‑Konstruktor übergeben.  
2. **Edit‑Methode:** Ein `EditableDocument` abrufen.  
3. **Inhalt holen:** Die CSV‑Darstellung (oder HTML) der Tabelle ausgeben.  
4. **Inhalt ändern:** Zell‑Level‑Änderungen vornehmen.  
5. **Speicheroptionen:** Die passenden `SpreadsheetSaveOptions` auswählen.  
6. **Dokument speichern:** Die aktualisierte Tabelle zurück in den Speicher schreiben.

### Bearbeiten von Präsentationsdokumenten
`PresentationSaveOptions` steuert das Ausgabeformat für Folien‑Decks und ermöglicht es Ihnen, den ursprünglichen Dateityp beizubehalten oder zu ändern.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/presentation.pptx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // Modify content here
        SaveOptions saveOptions = new PresentationSaveOptions(PresentationFormats.Pptx);
        editor.Save(editableDocument, "path/to/save/presentation.pptx", saveOptions);
    }
}
```
```

**Erklärung:**  
1. **Editor initialisieren:** Laden Sie eine PowerPoint‑Datei über `Editor`.  
2. **Edit‑Methode:** Ein `EditableDocument` erhalten.  
3. **Inhalt holen:** Folien‑HTML oder Nur‑Text extrahieren.  
4. **Inhalt ändern:** Titel, Aufzählungen oder Bilder aktualisieren.  
5. **Speicheroptionen:** `PresentationSaveOptions` verwenden, um das Ausgabeformat festzulegen.  
6. **Dokument speichern:** Die bearbeitete Präsentation persistieren.

## Häufige Probleme und Lösungen
- **„Format not supported“-Fehler:** Stellen Sie sicher, dass Sie die neueste Version von GroupDocs.Editor verwenden; sie fügt regelmäßig Unterstützung für neuere Office‑Formate hinzu.  
- **Hoher Speicherverbrauch bei großen Dateien:** Aktivieren Sie den Streaming‑Modus, indem Sie `EditorSettings.EnableStreaming = true` setzen, bevor Sie das Dokument laden.  
- **Lizenz nicht angewendet:** Vergewissern Sie sich, dass die temporäre Lizenzdatei im Anwendungsverzeichnis liegt oder über `License license = new License(); license.SetLicense("path/to/license.lic");` geladen wird.

## Häufig gestellte Fragen

**F: Was ist der Unterschied zwischen `DocumentFormatInfo` und `SaveOptions`?**  
A: `DocumentFormatInfo` liefert Metadaten zu unterstützten Dateitypen, während `SaveOptions` konfiguriert, wie ein Dokument zurück auf die Festplatte geschrieben wird (Format, Kompression usw.).

**F: Kann ich Formate für eine benutzerdefinierte Dateierweiterung auflisten?**  
A: Ja – verwenden Sie `DocumentFormatInfo.FromExtension("yourExt")`; wird die Erweiterung nicht erkannt, liefert die Methode `null`.

**F: Unterstützt GroupDocs.Editor passwortgeschützte Dateien?**  
A: Absolut. Übergeben Sie das Passwort im `Editor`‑Konstruktor über `EditorSettings`, um verschlüsselte Dokumente zu öffnen.

**F: Wie viele Formate unterstützt GroupDocs.Editor tatsächlich?**  
A: Über **30 Eingabe‑ und Ausgabeformate**, darunter Word, Excel, PowerPoint, HTML und Nur‑Text.

**F: Gibt es eine Möglichkeit, die Liste auf nur editierbare Formate zu beschränken?**  
A: Verwenden Sie `GetEditableWordProcessingFormats()` (bzw. die entsprechenden Methoden für Tabellen/Präsentationen), um Formate abzurufen, die volle Bearbeitungsfunktionen erlauben.

## Zusätzliche Ressourcen
- Laden Sie die Bibliothek von der [GroupDocs releases page](https://releases.groupdocs.com/editor/net/) herunter.  
- Holen Sie sich eine [temporary license](https://purchase.groupdocs.com/temporary-license/) für den vollen Funktionsumfang.  
- Testen Sie das Produkt mit einer [free trial](https://releases.groupdocs.com/).  
- Erkunden Sie detaillierte Anwendungsbeispiele in der [GroupDocs.Editor documentation](https://tutorials.groupdocs.com/editor/net/).  
- Holen Sie sich Hilfe von der Community im [support forum](https://forum.groupdocs.com/c/editor/20).

## Fazit
Indem Sie diesem Leitfaden folgen, wissen Sie jetzt, wie Sie **unterstützte Dokumentformate auflisten**, **ein Dateiformat anhand seiner Erweiterung bestimmen** und **Dokumente** für Word, Tabellen und Präsentationen mit GroupDocs.Editor für .NET bearbeiten können. Integrieren Sie diese Snippets in Ihre eigenen Projekte, um robuste, format‑bewusste Anwendungen zu bauen, die End‑User begeistern und Laufzeitfehler reduzieren.

---

**Last Updated:** 2026-06-06  
**Tested With:** GroupDocs.Editor 23.9 for .NET  
**Author:** GroupDocs

## Verwandte Tutorials

- [Mastering Document Loading in .NET with GroupDocs.Editor: A Comprehensive Guide](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)
- [Master Document Editing in .NET with GroupDocs.Editor: A Comprehensive Guide](/editor/net/document-editing/master-document-editing-dotnet-groupdocs-editor/)
- [Convert Word to HTML Using GroupDocs.Editor .NET: A Step‑By‑Step Guide](/editor/net/document-saving/convert-word-to-html-groupdocs-editor-dotnet/)