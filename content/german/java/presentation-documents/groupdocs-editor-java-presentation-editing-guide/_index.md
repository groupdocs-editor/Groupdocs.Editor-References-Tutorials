---
date: '2026-03-17'
description: Erfahren Sie, wie Sie PPTX in Java mit GroupDocs.Editor bearbeiten und
  PPTX in PPTM konvertieren. Dieser Leitfaden führt Sie durch die programmgesteuerte
  PowerPoint‑Bearbeitung, das Ersetzen von Text und die Massenkonvertierung von PPTX‑Dateien.
keywords:
- GroupDocs.Editor for Java
- presentation editing in Java
- editing PPTX files with Java
title: Wie man PPTX in Java mit GroupDocs bearbeitet und in PPTM konvertiert
type: docs
url: /de/java/presentation-documents/groupdocs-editor-java-presentation-editing-guide/
weight: 1
---

# Wie man PPTX bearbeitet und in PPTM konvertiert in Java mit GroupDocs

In der heutigen schnelllebigen digitalen Welt fragen viele Entwickler, **wie man pptx** programmgesteuert bearbeitet. Egal, ob Sie Text ersetzen, Makros hinzufügen oder einfach **PPTX in PPTM konvertieren** möchten, dieses Tutorial zeigt Ihnen Schritt für Schritt, wie Sie diese Ziele mit GroupDocs.Editor für Java erreichen. Sie sehen, wie Sie eine Präsentation laden, Änderungen vornehmen und das Ergebnis als makro‑aktiviertes PPTM speichern – und das ganz ohne Microsoft Office auf dem Server.

## Schnelle Antworten
- **Was ist der Hauptzweck dieses Leitfadens?** Um zu demonstrieren, wie man PPTX-Dateien bearbeitet und PPTX in PPTM mit GroupDocs.Editor für Java konvertiert.  
- **Benötige ich eine Lizenz?** Ja, eine Test- oder Dauerlizenz von GroupDocs ist für den Produktionseinsatz erforderlich.  
- **Kann ich passwortgeschützte Dateien verarbeiten?** Ja – die Ladeoptionen ermöglichen die Angabe des Passworts.  
- **Welche Java-Version wird unterstützt?** Java 8 oder höher (JDK 11+ empfohlen).  
- **Ist Maven der einzige Weg, die Bibliothek hinzuzufügen?** Nein, Sie können das JAR auch direkt herunterladen.  

## Was bedeutet „convert PPTX to PPTM“?

Das Konvertieren einer PPTX-Datei in PPTM ändert das Dateiformat von einer Standard‑PowerPoint‑Präsentation zu einer makro‑aktivierten Version (PPTM). Dies ist nützlich, wenn Sie VBA‑Makros einbetten oder erweiterte Funktionen beibehalten müssen, die PPTX nicht unterstützt.

## Warum GroupDocs.Editor für Java zum Bearbeiten von PPTX verwenden?

GroupDocs.Editor bietet eine High‑Level‑API, die die Komplexität des Office Open XML‑Formats abstrahiert. Sie ermöglicht:

- Präsentationen (einschließlich passwortgeschützter) mit einem einzigen Aufruf zu laden.  
- **Programmatic PowerPoint edit**: Folien zu ändern, Text zu ersetzen und Ressourcen zu manipulieren.  
- Das Ergebnis als PPTM zu speichern und bei Bedarf ein neues Passwort anzuwenden.

All dies kann erledigt werden, ohne dass Microsoft Office auf dem Server installiert sein muss.

## Voraussetzungen

- **GroupDocs.Editor for Java** – version 25.3 oder neuer.  
- **Java Development Kit (JDK)** – 8 oder höher.  
- Eine IDE wie IntelliJ IDEA oder Eclipse.  
- Eine gültige GroupDocs‑Lizenz (kostenlose Testversion oder gekauft).  

Sie können eine Testlizenz von der [GroupDocs-Website](https://purchase.groupdocs.com/temporary-license) erhalten.

## Einrichtung von GroupDocs.Editor für Java

Sie können die Bibliothek zu Ihrem Projekt über Maven hinzufügen oder das JAR direkt herunterladen.

### Verwendung von Maven
Fügen Sie die folgende Konfiguration in Ihre `pom.xml`‑Datei ein:

```xml
<repositories>
   <repository>
      <id>repository.groupdocs.com</id>
      <name>GroupDocs Repository</name>
      <url>https://releases.groupdocs.com/editor/java/</url>
   </repository>
</repositories>

<dependencies>
   <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-editor</artifactId>
      <version>25.3</version>
   </dependency>
</dependencies>
```

### Direkter Download
Alternativ laden Sie das neueste JAR von der offiziellen Release‑Seite herunter: [GroupDocs.Editor for Java releases](https://releases.groupdocs.com/editor/java/).

Sobald die Bibliothek in Ihrem Klassenpfad ist, können Sie eine `Editor`‑Instanz erstellen:

```java
import com.groupdocs.editor.Editor;
// Initialize GroupDocs.Editor (example setup)
Editor editor = new Editor();
```

## Wie man PPTX bearbeitet (und in PPTM konvertiert)

### Feature 1: Laden einer Präsentation (einschließlich passwortgeschützter Dateien)

#### Überblick
Das Laden einer Präsentation ist der erste Schritt, bevor Sie **PPTX in PPTM konvertieren** oder deren Inhalt bearbeiten können.

#### Schritt‑für‑Schritt‑Implementierung

**1. Pfad zu Ihrer Datei festlegen**  
Legen Sie den Speicherort der PPTX fest, mit der Sie arbeiten möchten:

```java
String inputFilePath = "YOUR_DOCUMENT_DIRECTORY/sample_pptx.pptx";
```

**2. InputStream erstellen**  
Öffnen Sie die Datei als Stream:

```java
import java.io.FileInputStream;
import java.io.InputStream;

InputStream fs = new FileInputStream(inputFilePath);
```

**3. Ladeoptionen festlegen**  
Falls die Datei geschützt ist, geben Sie das Passwort an:

```java
import com.groupdocs.editor.options.PresentationLoadOptions;

PresentationLoadOptions loadOptions = new PresentationLoadOptions();
loadOptions.setPassword("some_password_to_open_a_document");
```

**4. Präsentation laden**  
Verwenden Sie die `Editor`‑Klasse mit dem Stream und den Optionen:

```java
Editor editor = new Editor(fs, loadOptions);
```

**Pro Tipp:** Schließen Sie den `InputStream` immer in einem `finally`‑Block oder verwenden Sie try‑with‑resources, um Ressourcenlecks zu vermeiden.

### Feature 2: Bearbeiten einer bestimmten Folie (edit pptx java)

#### Überblick
Zielen Sie auf eine einzelne Folie für Änderungen – ideal für das **edit pptx java**‑Szenario.

#### Schritt‑für‑Schritt‑Implementierung

**1. Bearbeitungsoptionen festlegen**  
Wählen Sie die zu bearbeitende Folie (0‑basierter Index):

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.options.PresentationEditOptions;

PresentationEditOptions editOptions = new PresentationEditOptions();
editOptions.setSlideNumber(0); // Edit the first slide
editOptions.setShowHiddenSlides(true);
```

**2. Editable Document erhalten**  
Rufen Sie die bearbeitbare Darstellung der Folie ab:

```java
import com.groupdocs.editor.EditableDocument;

EditableDocument beforeEdit = editor.edit(editOptions);
```

**3. HTML‑Inhalt und Ressourcen extrahieren**  
Sie können nun mit dem HTML‑Markup der Folie und deren eingebetteten Ressourcen arbeiten:

```java
String originalContent = beforeEdit.getContent();
List<IHtmlResource> allResources = beforeEdit.getAllResources();
```

### Feature 3: Inhalt einer Präsentationsfolie ändern

#### Überblick
Ersetzen Sie Text oder fügen Sie neues HTML direkt in das Folien‑Markup ein.

#### Schritt‑für‑Schritt‑Implementierung

**1. Text ersetzen**  
Für eine einfache Textsubstitution:

```java
String editedContent = beforeEdit.getContent().replace("New text", "edited text");
```

**2. Neues Editable Document erstellen**  
Packen Sie das modifizierte Markup wieder in ein `EditableDocument`:

```java
EditableDocument afterEdit = EditableDocument.fromMarkup(editedContent, allResources);
```

### Feature 4: Speichern einer bearbeiteten Präsentation (convert PPTX to PPTM)

#### Überblick
Speichern Sie schließlich das bearbeitete Folien-Set als PPTM‑Datei, optional mit einem Passwort geschützt.

#### Schritt‑für‑Schritt‑Implementierung

**1. Save‑Optionen initialisieren**  
Geben Sie das PPTM‑Format und ein neues Passwort an:

```java
import com.groupdocs.editor.options.PresentationSaveOptions;
import com.groupdocs.editor.formats.PresentationFormats;

PresentationSaveOptions saveOptions = new PresentationSaveOptions(PresentationFormats.Pptm);
saveOptions.setPassword("password");
```

**2. Ausgabestream vorbereiten**  
Legen Sie fest, wohin die resultierende Datei geschrieben wird:

```java
import java.io.ByteArrayOutputStream;
import java.io.FileOutputStream;

String outputPath = "YOUR_OUTPUT_DIRECTORY/sample_out.pptm";
ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
```

**3. Das bearbeitete Dokument speichern**  
Schreiben Sie die aktualisierte Präsentation in den Ausgabestream:

```java
editor.save(afterEdit, outputStream, saveOptions);
```

**4. In Datei schreiben**  
Speichern Sie den Stream auf der Festplatte:

```java
try (FileOutputStream outputFile = new FileOutputStream(outputPath)) {
    outputStream.writeTo(outputFile);
}
```

**Tipp:** Nach dem Speichern können Sie die Datei öffnen, um in PowerPoint zu prüfen, ob das makro‑aktivierte Format wie erwartet funktioniert.

## Text in PPTX‑Folien ersetzen

Das obige Snippet (`replace text pptx`) zeigt eine einfache Methode, um jede Zeichenkette im HTML einer Folie zu ersetzen. Für komplexere Szenarien – z. B. das Aktualisieren von Platzhaltern über mehrere Folien hinweg – können Sie über jedes `EditableDocument` iterieren und dieselbe `replace`‑Logik anwenden.

## Mehrfachkonvertierung von PPTX‑Dateien

Wenn Sie **pptx‑Dateien in großen Mengen** in PPTM (oder ein anderes Format) konvertieren müssen, verpacken Sie die Schritte Laden‑Bearbeiten‑Speichern in einer Schleife, die über ein Verzeichnis von PPTX‑Dateien iteriert. Die Wiederverwendung einer einzelnen `Editor`‑Instanz reduziert den Overhead und beschleunigt die Batch‑Verarbeitung.

## Praktische Anwendungen

GroupDocs.Editor Java API glänzt in realen Szenarien wie:

- **Corporate training:** Schnell Decks mit neuen Richtlinien aktualisieren.  
- **Marketing campaigns:** Makro‑aktivierte Präsentationen für interaktive Demos erzeugen.  
- **Education:** Die Erstellung von Vorlesungsfolien automatisieren, die VBA‑Makros für Quizze enthalten.  

## Leistungsüberlegungen

Wenn Sie große PPTX‑Dateien verarbeiten:

- Erhöhen Sie die JVM‑Heap‑Größe (`-Xmx2g` oder höher), um `OutOfMemoryError` zu vermeiden.  
- Verwenden Sie dieselbe `Editor`‑Instanz für die Batch‑Verarbeitung, um Overhead zu reduzieren.  
- Halten Sie die Bibliothek aktuell; neuere Releases enthalten Leistungsoptimierungen.

## Häufig gestellte Fragen

**Q: Kann ich ein PPTX in PPTM konvertieren, ohne die Folien zu bearbeiten?**  
A: Ja. Laden Sie das PPTX mit `PresentationLoadOptions` und speichern Sie es anschließend mit `PresentationSaveOptions` im PPTM‑Format – Zwischenschritte zur Bearbeitung sind nicht erforderlich.

**Q: Unterstützt die Bibliothek andere PowerPoint‑Formate (PPT, PPSX usw.)?**  
A: GroupDocs.Editor kann PPT, PPTX, PPSX und PPTM Formate laden und speichern. Verwenden Sie beim Speichern das passende `PresentationFormats`‑Enum.

**Q: Wie gehe ich mit einer Präsentation um, die kein Passwort hat, ich aber trotzdem eines für die Ausgabe setzen möchte?**  
A: Geben Sie das gewünschte Passwort nur in `PresentationSaveOptions` an; in `PresentationLoadOptions` muss es nicht gesetzt werden.

**Q: Ist es möglich, mehrere Folien in einem Vorgang zu bearbeiten?**  
A: Ja. Iterieren Sie über die Folienzahlen, rufen jedes `EditableDocument` ab, wenden Änderungen an und kombinieren die Ergebnisse vor dem Speichern.

**Q: Was ist, wenn ich eine neue Folie hinzufügen möchte, anstatt eine vorhandene zu bearbeiten?**  
A: Erstellen Sie eine neue Folie mit der API des Editors (z. B. `PresentationEditOptions.setSlideNumber(-1)` zum Anhängen) und fügen Sie anschließend das gewünschte Markup ein.

**Q: Wie kann ich eine Mehrfachkonvertierung von pptx zu pptm in einem einzigen Service durchführen?**  
A: Durchlaufen Sie Ihr Quellverzeichnis, laden Sie jedes PPTX mit derselben `Editor`‑Instanz und rufen Sie `save` mit `PresentationSaveOptions(PresentationFormats.Pptm)` auf. Denken Sie daran, Streams zeitnah zu schließen.

## Fazit

Durch das Befolgen dieses Leitfadens wissen Sie jetzt, **wie man pptx**‑Dateien **bearbeitet** und **PPTX in PPTM** mit GroupDocs.Editor für Java **konvertiert**. Sie können Präsentationen laden, einzelne Folien ändern, Text ersetzen und das Ergebnis als makro‑aktivierte PPTM‑Datei speichern – alles programmgesteuert und sicher.

**Nächste Schritte:**  
- Experimentieren Sie mit dem Hinzufügen von VBA‑Makros zur PPTM‑Datei.  
- Erkunden Sie die Mehrfachkonvertierung mehrerer Präsentationen in einem einzigen Java‑Service.  
- Lesen Sie die vollständige GroupDocs.Editor‑Dokumentation für erweiterte Funktionen wie Bildverarbeitung und benutzerdefiniertes Styling.

---

**Zuletzt aktualisiert:** 2026-03-17  
**Getestet mit:** GroupDocs.Editor 25.3 für Java  
**Autor:** GroupDocs