---
date: 2026-06-06
description: Erfahren Sie, wie Sie **editierbare Dokumente**-Objekte aus CSV- und
  TSV-Dateien mit GroupDocs.Editor for .NET erstellen. Dieser Leitfaden zeigt außerdem,
  wie Sie **delimitierten Text in C# lesen** und **CSV in .NET bearbeiten** effizient
  in Visual Studio.
keywords:
- create editable document
- read delimited text c#
- edit csv .net
- parse delimited values c#
linktitle: Arbeiten mit durch Trennzeichen getrennten Werten (DSV) – editierbares
  Dokument erstellen
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to **create editable document** objects from CSV and TSV
    files using GroupDocs.Editor for .NET. This guide also shows how to **read delimited
    text C#** and **edit CSV .NET** efficiently in Visual Studio.
  headline: Work with Delimited Separated Values (DSV) – create editable document
  type: TechArticle
- questions:
  - answer: Yes, the API streams data and can handle files larger than 1 GB without
      loading the entire document into memory.
    question: Can I use GroupDocs.Editor for .NET to edit large CSV files?
  - answer: Absolutely – any single‑character delimiter (e.g., pipe `|`, semicolon
      `;`) is supported as long as you specify it in `DelimitedTextEditOptions`.
    question: Does GroupDocs.Editor for .NET support other DSV formats besides CSV
      and TSV?
  - answer: Yes, you can set the `Encoding` property in `DelimitedTextSaveOptions`
      to UTF‑8, UTF‑16, ISO‑8859‑1, or any .NET `Encoding` you require.
    question: Is it possible to customize the encoding when saving DSV files?
  - answer: Yes – after editing, simply use `SpreadsheetSaveOptions` to export the
      content as an `.xlsx` workbook.
    question: Can I convert a CSV file to an Excel spreadsheet using GroupDocs.Editor
      for .NET?
  - answer: Detailed API references and code samples are available **[here](https://tutorials.groupdocs.com/editor/net/)**.
    question: Where can I find more documentation on GroupDocs.Editor for .NET?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Arbeiten mit durch Trennzeichen getrennten Werten (DSV) – editierbares Dokument
  erstellen
type: docs
url: /de/net/document-processing/work-dsv/
weight: 12
---

# Arbeiten mit durch Trennzeichen getrennten Werten (DSV) – editierbares Dokument erstellen

Wenn Sie ein .NET‑Entwickler sind, der **editierbare Dokument**‑Objekte aus durch Trennzeichen getrennten Werten (DSV) wie CSV oder TSV erstellen muss, sind Sie hier genau richtig. In den ersten 100 Wörtern erklären wir, warum GroupDocs.Editor für .NET der zuverlässigste Weg ist, um **read delimited text C#** zu lesen, zu bearbeiten und anschließend ohne Verlust der Formatierung wieder zu speichern. Sie erhalten einen vollständigen, copy‑and‑paste‑bereiten Workflow, der sich nahtlos in jede Visual Studio‑Lösung einfügt.

## Schnelle Antworten
- **Welche Bibliothek verarbeitet CSV‑Bearbeitung am besten in .NET?** GroupDocs.Editor for .NET.
- **Kann ich große CSV‑Dateien in Visual Studio bearbeiten?** Ja – die API streamt Daten und vermeidet das Laden der gesamten Datei in den Speicher.
- **Benötige ich eine Lizenz für den Produktionseinsatz?** Eine kommerzielle Lizenz ist erforderlich; eine kostenlose Testversion ist verfügbar.
- **Welche Formate kann ich nach der Bearbeitung ausgeben?** CSV, TSV und Excel‑kompatible Tabellenformate.
- **Ist die API mit .NET 6+ kompatibel?** Absolut – sie unterstützt .NET Framework 4.5+, .NET Core 3.1+, .NET 5 und .NET 6.

## Was bedeutet „create editable document“ im Kontext von GroupDocs.Editor?
**Create editable document** bedeutet, eine `EditableDocument`‑Instanz zu erzeugen, die eine veränderbare Version einer Quelldatei (CSV, TSV usw.) im Speicher darstellt. Dieses Objekt ermöglicht das Lesen, Ändern und erneute Speichern des Inhalts über dieselbe API. Es stellt Methoden bereit, um den Dokumenttext abzurufen, Änderungen anzuwenden und ihn in verschiedenen Formaten wieder zu speichern, wobei Spaltenausrichtung und Anführungszeichen erhalten bleiben.

## Warum GroupDocs.Editor für die DSV‑Verarbeitung verwenden?
GroupDocs.Editor verarbeitet **mehr als 50 Eingabe‑ und Ausgabeformate**, darunter CSV, TSV und Excel‑kompatible Tabellen, und hält den Speicherverbrauch bei Dateien bis zu 500 MB unter 10 MB. Außerdem bewahrt es automatisch Spaltenausrichtung, Anführungsregeln und benutzerdefinierte Codierungen, wodurch manuelle Parsing‑Logik überflüssig wird.

## Voraussetzungen
Bevor wir beginnen, stellen Sie sicher, dass Sie Folgendes installiert haben:

- **Visual Studio** (jede aktuelle Edition) – Sie entwickeln und debuggen direkt in der IDE.
- **GroupDocs.Editor for .NET** – laden Sie das neueste Paket **[hier](https://releases.groupdocs.com/editor/net/)** herunter.
- **Basic C# knowledge** – das Tutorial geht davon aus, dass Sie ein Konsolen‑ oder ASP.NET‑Projekt erstellen und NuGet‑Pakete hinzufügen können.

## Namespaces importieren
Die Klassen `Editor`, `EditableDocument` und Optionsklassen befinden sich im Namespace `GroupDocs.Editor`.  

Die Klasse `DelimitedTextEditOptions` ist der Einstiegspunkt zur Definition des Trennzeichens (Komma, Tab usw.) und weiterer Parsing‑Regeln.

```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

## Wie erstellt man ein editierbares Dokument aus einer CSV‑Datei?
Laden Sie die Quell‑CSV mit `Editor` und rufen Sie die Methode `Edit` auf, wobei Sie eine `DelimitedTextEditOptions`‑Instanz übergeben, die ein Komma‑Trennzeichen festlegt. Die Methode gibt ein `EditableDocument` zurück, das Sie im Speicher manipulieren können. Dieses Zwei‑Schritt‑Muster – laden → bearbeiten – deckt **read delimited text C#**‑Szenarien ab und stellt sicher, dass die ursprüngliche Dateistruktur erhalten bleibt.

## Schritt 1: Pfad zur Eingabe‑DSV‑Datei erhalten
Zuerst müssen Sie den absoluten oder relativen Pfad zur Quell‑DSV‑Datei angeben. Für die Demonstration verwenden wir eine einfache CSV, die sich im `Data`‑Ordner des Projekts befindet.

```csharp
string inputFilePath = "Your Sample Document";
```

## Schritt 2: Editor‑Instanz erstellen
`Editor` ist die Kernklasse, die das Laden, Bearbeiten und Speichern steuert. Durch die Instanziierung mit einem `FileInfo`‑Objekt erhalten Sie die volle Kontrolle über den Dateilebenszyklus.

```csharp
using (Editor editor = new Editor(inputFilePath))
{
```

## Schritt 3: DSV‑Bearbeitungsoptionen erstellen
`DelimitedTextEditOptions` gibt dem Editor an, wie die Datei zu interpretieren ist. Sie können das Trennzeichen, ob die erste Zeile Header enthält, und die Zeichenkodierung festlegen.

```csharp
    Options.DelimitedTextEditOptions editOptions = new DelimitedTextEditOptions(",");
    editOptions.ConvertDateTimeData = false;
    editOptions.ConvertNumericData = true;
    editOptions.TreatConsecutiveDelimitersAsOne = true;
```

## Schritt 4: EditableDocument‑Instanz erstellen
`EditableDocument` stellt eine veränderbare In‑Memory‑Version der Quelldatei dar. Der Aufruf von `Editor.Edit` mit den Optionen liefert ein `EditableDocument`. Dieses Objekt enthält den Text der Datei in einem veränderbaren String, bereit für jede **parse delimited values C#**‑Operation, die Sie benötigen.

```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```

## Schritt 5: Dokumentinhalt bearbeiten
`GetDocumentText()` gibt den aktuellen Text des editierbaren Dokuments als Zeichenkette zurück. Rufen Sie den Originaltext über `EditableDocument.GetDocumentText()` ab, führen Sie Ihre Änderungen durch (z. B. einen Spaltenwert ersetzen) und speichern Sie das Ergebnis in einer neuen Zeichenkette. Hier können Sie **edit CSV .NET** ausführen, ohne low‑level‑Dateistreams zu berühren.

```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("SsangYong", "Chevrolet").Replace("Kyron", "Camaro");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```

## Schritt 6: EditableDocument mit aktualisiertem Inhalt erstellen
Verpacken Sie die modifizierte Zeichenkette wieder in ein `EditableDocument`. Dieser Schritt finalisiert die Änderungen und bereitet das Objekt für das Speichern in einem beliebigen unterstützten Format vor.

```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```

## Schritt 7: CSV‑Speicheroptionen erstellen
`DelimitedTextSaveOptions` legt fest, wie der bearbeitete Inhalt zurück in eine CSV‑Datei geschrieben wird. Wenn Sie bereit sind, die Änderungen zu speichern, konfigurieren Sie `DelimitedTextSaveOptions`. Sie können dasselbe Trennzeichen, ein anderes oder sogar den Zeilenende‑Stil ändern.

```csharp
    Options.DelimitedTextSaveOptions csvSaveOptions = new DelimitedTextSaveOptions(",");
    csvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

## Schritt 8: TSV‑Speicheroptionen erstellen
Falls Sie eine tab‑separierte Version benötigen, wechseln Sie einfach das Trennzeichen zu `\t`. Das gleiche `EditableDocument` kann mehrfach mit unterschiedlichen Optionen gespeichert werden.

```csharp
    Options.DelimitedTextSaveOptions tsvSaveOptions = new DelimitedTextSaveOptions("\t");
    tsvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

## Schritt 9: Spreadsheet‑Speicheroptionen erstellen
`SpreadsheetSaveOptions` konfiguriert den Export des Dokuments in Excel‑kompatible Formate wie .xlsx. GroupDocs.Editor ermöglicht zudem den Export der bearbeiteten Daten in ein Excel‑kompatibles Format (`.xlsx`). Die Klasse `SpreadsheetSaveOptions` kümmert sich automatisch um Spaltentypen, Formeln und Zellformatierung.

```csharp
    Options.SpreadsheetSaveOptions cellsSaveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
```

## Schritt 10: Speicherpfade vorbereiten
Definieren Sie eindeutige Ausgabepfade für jedes Format. Durch klare Namenskonventionen (z. B. `output.csv`, `output.tsv`, `output.xlsx`) bleibt Ihr Projekt übersichtlich.

```csharp
    string outputCsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".csv");
    string outputTsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".tsv");
    string outputCellsPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".xlsm");
```

## Schritt 11: Bearbeitetes Dokument speichern
`Save()` schreibt das Dokument mit den angegebenen Speicheroptionen auf die Festplatte. Rufen Sie `EditableDocument.Save` mit den jeweiligen Optionen für jedes Zielformat auf. Die API schreibt die Datei direkt auf die Festplatte und bewahrt die ursprüngliche Kodierung, sofern Sie sie nicht überschreiben.

```csharp
    editor.Save(afterEdit, outputCsvPath, csvSaveOptions);
    editor.Save(afterEdit, outputTsvPath, tsvSaveOptions);
    editor.Save(afterEdit, outputCellsPath, cellsSaveOptions);
```

## Schritt 12: EditableDocument‑Instanzen freigeben
Sowohl `Editor` als auch `EditableDocument` implementieren `IDisposable`. Durch das Freigeben werden Dateihandles und nicht verwaltete Ressourcen freigegeben, was bei der Verarbeitung vieler Dateien in einem Batch‑Job entscheidend ist.

```csharp
    beforeEdit.Dispose();
    afterEdit.Dispose();
}
System.Console.WriteLine("WorkingWithDsv routine has successfully finished");
```

## Häufige Probleme und Lösungen
| Problem | Warum es passiert | Lösung |
|-------|----------------|-----|
| **Unerwartete zusätzliche Anführungszeichen** | Der Standard‑CSV‑Parser kann eingebettete Kommas als Trennzeichen behandeln. | Set `EscapeMode = EscapeMode.DoubleQuote` in `DelimitedTextEditOptions`. |
| **Großer Speicherverbrauch bei großen Dateien** | Laden einer 500 MB‑Datei ohne Streaming. | Use `Editor.Load` with `LoadOptions` that enable lazy loading. |
| **Kodierungsabweichung** | Die Quelldatei verwendet UTF‑16, während die Optionen standardmäßig UTF‑8 nutzen. | Explicitly set `Encoding = Encoding.Unicode` in save options. |

## Häufig gestellte Fragen

**Q: Kann ich GroupDocs.Editor für .NET verwenden, um große CSV‑Dateien zu bearbeiten?**  
A: Ja, die API streamt Daten und kann Dateien größer als 1 GB verarbeiten, ohne das gesamte Dokument in den Speicher zu laden.

**Q: Unterstützt GroupDocs.Editor für .NET andere DSV‑Formate neben CSV und TSV?**  
A: Absolut – jedes ein‑Zeichen‑Trennzeichen (z. B. Pipe `|`, Semikolon `;`) wird unterstützt, solange Sie es in `DelimitedTextEditOptions` angeben.

**Q: Ist es möglich, die Kodierung beim Speichern von DSV‑Dateien anzupassen?**  
A: Ja, Sie können die Eigenschaft `Encoding` in `DelimitedTextSaveOptions` auf UTF‑8, UTF‑16, ISO‑8859‑1 oder jede andere .NET‑`Encoding` setzen, die Sie benötigen.

**Q: Kann ich eine CSV‑Datei mit GroupDocs.Editor für .NET in eine Excel‑Tabelle konvertieren?**  
A: Ja – nach der Bearbeitung verwenden Sie einfach `SpreadsheetSaveOptions`, um den Inhalt als `.xlsx`‑Arbeitsmappe zu exportieren.

**Q: Wo finde ich weitere Dokumentation zu GroupDocs.Editor für .NET?**  
A: Detaillierte API‑Referenzen und Code‑Beispiele sind **[hier](https://tutorials.groupdocs.com/editor/net/)** verfügbar.

**Zuletzt aktualisiert:** 2026-06-06  
**Getestet mit:** GroupDocs.Editor 23.10 für .NET  
**Autor:** GroupDocs

## Verwandte Tutorials

- [Tutorials zum Bearbeiten von Klartext‑ und DSV‑Dokumenten für GroupDocs.Editor .NET](/editor/net/plain-text-dsv-documents/)
- [GroupDocs.Editor .NET meistern für effizientes CSV‑Dokumenten‑Editing und -Konvertierung](/editor/net/plain-text-dsv-documents/groupdocs-editor-net-csv-editing-guide/)
- [Dokumenten‑Laden in .NET mit GroupDocs.Editor meistern: Ein umfassender Leitfaden](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)