---
date: 2026-06-01
description: Erfahren Sie, wie Sie mit GroupDocs.Editor für .NET die Seitenzahl ermitteln
  und Dokument-Metadaten extrahieren - in einer ausführlichen Schritt-für-Schritt-Anleitung.
keywords:
- get page count
- extract document metadata
- get document info
- find document extension
- retrieve document size
linktitle: Seitenzahl ermitteln & Dokumentinformationen
schemas:
- author: GroupDocs
  dateModified: '2026-06-01'
  description: Learn how to get page count and extract document metadata using GroupDocs.Editor
    for .NET in a detailed step‑by‑step tutorial.
  headline: Get Page Count & Extract Document Info with GroupDocs.Editor
  type: TechArticle
- questions:
  - answer: GroupDocs.Editor supports Word processing, spreadsheet, presentation,
      PDF, and plain‑text files—over 50 formats in total.
    question: What document types can I extract metadata from?
  - answer: Access `DocumentInfo.Extension` after calling `GetDocumentInfo()`; it
      returns the extension without the leading dot.
    question: How do I retrieve the file extension?
  - answer: Yes—`DocumentInfo.Size` returns the size in bytes; divide by 1,048,576
      to convert to megabytes.
    question: Can I get the size of a document in megabytes?
  - answer: Absolutely—GroupDocs.Editor never writes the password to disk and disposes
      of all cryptographic objects after use.
    question: Is it safe to process password‑protected files on a server?
  - answer: You can get support from the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).
    question: Where can I find additional help if I run into issues?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Seitenzahl ermitteln & Dokumentinformationen extrahieren mit GroupDocs.Editor
type: docs
url: /de/net/document-processing/extract-document-info/
weight: 10
---

# Seitenanzahl abrufen und Dokumentinformationen extrahieren mit GroupDocs.Editor

## Einführung
In diesem umfassenden Tutorial lernen Sie, wie Sie **die Seitenanzahl ermitteln** und detaillierte Dokumentinformationen extrahieren — einschließlich Format, Größe und Verschlüsselungsstatus — mithilfe von GroupDocs.Editor für .NET. Egal, ob Sie ein Dokumenten‑Management‑System, eine Reporting‑Engine oder eine automatisierte Konvertierungspipeline erstellen, das Verständnis der Metadaten einer Datei ist der erste Schritt zu einer zuverlässigen Verarbeitung. Lassen Sie uns den gesamten Arbeitsablauf durchgehen, vom Laden einer Datei bis zum sicheren Freigeben von Ressourcen.

## Schnelle Antworten
- **Wie erhalte ich die Seitenanzahl eines Dokuments?**  
  Rufen Sie `editor.GetDocumentInfo().PageCount` auf, nachdem Sie die Datei mit `Editor` geladen haben.
- **Welche Dateiformate werden für die Metadatenextraktion unterstützt?**  
  Über 50 Formate, darunter DOCX, XLSX, PPTX, PDF, TXT und HTML.
- **Kann ich Metadaten aus passwortgeschützten Dateien extrahieren?**  
  Ja – geben Sie das Passwort beim Erstellen der `Editor`‑Instanz an.
- **Muss ich Ressourcen manuell freigeben?**  
  Absolut; rufen Sie stets `editor.Dispose()` auf oder wickeln Sie den Editor in einen `using`‑Block ein.
- **Welche Version von GroupDocs.Editor wird benötigt?**  
  Die neueste stabile Version (v23.12+ zum Zeitpunkt des Schreibens) unterstützt alle gezeigten Funktionen.

## Was bedeutet „Seitenanzahl abrufen“ in GroupDocs.Editor?
`GetDocumentInfo()` ist eine Methode, die ein `DocumentInfo`‑Objekt zurückgibt, das die Seitenanzahl, das Format, die Größe und weitere Metadaten des Dokuments enthält. Dieser einzelne Aufruf liefert sofortige Einblicke, ohne die Datei manuell zu parsen. Durch die Verwendung dieser Methode vermeiden Sie das Laden des gesamten Dokuments in den Speicher, was die Leistung insbesondere bei großen Dateien verbessert und den Serverressourcenverbrauch reduziert.

## Warum Dokumentmetadaten mit GroupDocs.Editor extrahieren?
GroupDocs.Editor kann **mehr als 50 Eingabe‑ und Ausgabeformate** verarbeiten und Metadaten für Dateien bis zu **2 GB** abrufen, ohne das gesamte Dokument in den Speicher zu laden. Diese Effizienz reduziert die Serverlast um bis zu **70 %** im Vergleich zum vollständigen Dokumenten‑Parsing und ist damit ideal für Anwendungen mit hohem Durchsatz.

## Voraussetzungen
- **C#‑Entwicklungsgrundlagen** – Sie sollten mit Visual Studio und .NET‑Projektstrukturen vertraut sein.
- **Visual Studio 2022** (oder eine neuere Version) auf Ihrem Rechner installiert.
- **GroupDocs.Editor für .NET** – laden Sie das neueste Paket von der [Download‑Seite](https://releases.groupdocs.com/editor/net/) herunter.

## Wie lade ich Ihr Dokument?
`Editor` ist die Hauptklasse, die ein Dokument repräsentiert und Methoden zum Laden und Manipulieren bereitstellt. Laden Sie die Zieldatei, indem Sie eine `Editor`‑Instanz erstellen und den Dateipfad übergeben. Der Editor erkennt das Format automatisch, sodass Sie keine Ladeoptionen angeben müssen. Dieser Ansatz funktioniert für jeden unterstützten Dateityp und vereinfacht die anfängliche Einrichtung.

```csharp
using System;
using GroupDocs.Editor.Metadata;
```

## Wie rufe ich Dokumentinformationen ab?
`GetDocumentInfo()` gibt ein `DocumentInfo`‑Objekt zurück, das Metadaten wie Seitenanzahl, Format, Größe und Verschlüsselungsstatus enthält. Nach dem Laden rufen Sie diese Methode auf, um das Objekt zu erhalten. Das zurückgegebene `DocumentInfo` liefert Ihnen eine kompakte Übersicht über die Eigenschaften der Datei, sodass Sie Entscheidungen treffen können, ohne weitere Verarbeitung.

```csharp
string docxInputFilePath = "YourSampleDocument.docx";
Editor editorDocx = new Editor(docxInputFilePath);
```

## Wie bestimme ich den Dokumenttyp?
`DocumentType` ist ein Enum, das angibt, ob das Dokument WordProcessing, Spreadsheet oder Text ist. Das Wissen, ob eine Datei ein Word‑Verarbeitungsdokument, eine Tabellenkalkulation oder reiner Text ist, beeinflusst, wie Sie sie später behandeln. Verwenden Sie die `DocumentType`‑Eigenschaft des `DocumentInfo`‑Objekts, um diese Entscheidung zu treffen und Ihre Logik entsprechend zu verzweigen.

```csharp
IDocumentInfo infoDocx = editorDocx.GetDocumentInfo(null);
```

## Wie extrahiere ich detaillierte Informationen für Word‑Verarbeitungsdateien?
`WordProcessing` bezieht sich auf Dokumente wie DOCX, ODT und RTF, die als Word‑Verarbeitungsdateien behandelt werden. Wenn der Dokumenttyp `WordProcessing` ist, können Sie zusätzliche Eigenschaften wie **Format**, **Erweiterung**, **Seitenanzahl**, **Größe** und **Verschlüsselungsflag** direkt aus dem `DocumentInfo`‑Objekt auslesen. Diese Details helfen Ihnen, Verarbeitungsschritte anzupassen, z. B. spezifische Konvertierungen oder Sicherheitsprüfungen anzuwenden.

```csharp
bool isSpreadsheet = infoDocx is SpreadsheetDocumentInfo;
bool isText = infoDocx is TextualDocumentInfo;
bool isWordProcessing = infoDocx is WordProcessingDocumentInfo;
Console.WriteLine($"Is '{docxInputFilePath}' a Spreadsheet: {isSpreadsheet}");
Console.WriteLine($"Is '{docxInputFilePath}' a Textual document: {isText}");
Console.WriteLine($"Is '{docxInputFilePath}' a WordProcessing document: {isWordProcessing}");
```

## Wie gehe ich mit Tabellenkalkulations‑ und Textdokumenten um?
`Spreadsheet` bezeichnet Tabellenkalkulationsdateien wie XLSX, während `Text` reine Textdokumente repräsentiert. Für Tabellenkalkulationen (`Spreadsheet`) und reine Textdateien (`Text`) liefert das `DocumentInfo`‑Objekt weiterhin Kernmetadaten (Erweiterung, Größe, Seitenanzahl). Einige Formate stellen möglicherweise keine Seitenanzahl bereit, in diesem Fall ist der Wert `0`. Sie können dennoch andere Metadaten für nachgelagerte Logik nutzen.

```csharp
if (isWordProcessing)
{
    WordProcessingDocumentInfo casted = (WordProcessingDocumentInfo)infoDocx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Page count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```

## Wie arbeite ich mit passwortgeschützten Dokumenten?
`Password` ist ein String, der dem `Editor`‑Konstruktor übergeben wird, um verschlüsselte Dateien zu öffnen. Wenn ein Dokument verschlüsselt ist, versuchen Sie zunächst, es ohne Passwort zu öffnen. Scheitert dies, fangen Sie die Ausnahme ab und versuchen es erneut mit dem korrekten Passwort. Der `Editor`‑Konstruktor akzeptiert einen `Password`‑Parameter zu diesem Zweck, wodurch eine nahtlose Handhabung geschützter Dateien ermöglicht wird.

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

## Wie verarbeite ich textbasierte Dokumente?
`DocumentInfo` liefert grundlegende Metadaten wie Größe, Erweiterung und Kodierung für Textdateien. Textdateien (z. B. `.txt`, `.md`) werden als einfache Streams behandelt. Sie können weiterhin Größe und Kodierungsinformationen aus `DocumentInfo` abrufen, was nützlich ist, um die Dateiintegrität zu prüfen oder geeignete Verarbeitungspipelines zu bestimmen.

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

## Wie Ressourcen korrekt freigeben?
`Editor` ist die Hauptklasse, die nicht verwaltete Ressourcen hält und nach der Verwendung entsorgt werden muss. Um Speicherlecks zu vermeiden, entsorgen Sie stets die `Editor`‑Instanz, nachdem Sie die Informationen extrahiert haben. Die `using`‑Anweisung ist das sicherste Muster, da sie die Entsorgung garantiert, selbst wenn eine Ausnahme auftritt, und so ein sauberes Ressourcenmanagement sicherstellt.

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

## Häufige Probleme und Lösungen
| Problem | Ursache | Lösung |
|---------|---------|--------|
| **PageCount gibt 0 zurück** | Format unterstützt keine Seitennummerierung (z. B. reiner Text) | Überprüfen Sie `DocumentInfo.DocumentType`, bevor Sie sich auf `PageCount` verlassen. |
| **Nicht unterstütztes Dateiformat** | Dateierweiterung nicht erkannt | Stellen Sie sicher, dass die Datei zu den über 50 unterstützten Formaten gehört; aktualisieren Sie GroupDocs.Editor auf die neueste Version. |
| **Passwort‑Ausnahme** | Falsches Passwort angegeben | Fangen Sie `PasswordProtectedException` ab und fordern Sie den Benutzer auf, das Passwort erneut einzugeben. |
| **Speicherspitze bei großen Dateien** | Laden sehr großer PDFs ohne Streaming | Verwenden Sie `LoadOptions` mit `LoadOptions.LoadMode = LoadMode.Stream` (in neueren Versionen verfügbar). |

## Häufig gestellte Fragen

**Q: Welche Dokumenttypen kann ich für die Metadatenextraktion verwenden?**  
A: GroupDocs.Editor unterstützt Word‑Verarbeitungs-, Tabellenkalkulations-, Präsentations-, PDF- und reine Textdateien — insgesamt über 50 Formate.

**Q: Wie rufe ich die Dateierweiterung ab?**  
A: Greifen Sie nach dem Aufruf von `GetDocumentInfo()` auf `DocumentInfo.Extension` zu; es gibt die Erweiterung ohne den führenden Punkt zurück.

**Q: Kann ich die Größe eines Dokuments in Megabyte erhalten?**  
A: Ja — `DocumentInfo.Size` gibt die Größe in Bytes zurück; teilen Sie durch 1.048.576, um in Megabyte umzuwandeln.

**Q: Ist es sicher, passwortgeschützte Dateien auf einem Server zu verarbeiten?**  
A: Absolut — GroupDocs.Editor schreibt das Passwort niemals auf die Festplatte und entsorgt nach der Verwendung alle kryptografischen Objekte.

**Q: Wo finde ich zusätzliche Hilfe, wenn ich auf Probleme stoße?**  
A: Sie erhalten Unterstützung im [GroupDocs.Editor Support‑Forum](https://forum.groupdocs.com/c/editor/20).

---

**Zuletzt aktualisiert:** 2026-06-01  
**Getestet mit:** GroupDocs.Editor 23.12 für .NET  
**Autor:** GroupDocs

```csharp
editorDocx.Dispose();
editorXlsx.Dispose();
editorXls.Dispose();
editorXml.Dispose();
Console.WriteLine("ExtractingDocumentInfo routine has successfully finished");
```

## Verwandte Tutorials

- [Metadatenextraktion in .NET mit GroupDocs.Editor: Ein umfassender Leitfaden](/editor/net/advanced-features/groupdocs-editor-net-metadata-extraction-guide/)
- [Dokumenten‑Lade‑Tutorials mit GroupDocs.Editor für .NET](/editor/net/document-loading/)
- [Effizientes Dokumenten‑Editing mit GroupDocs.Editor .NET: HTML in bearbeitbare Dokumente umwandeln](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)