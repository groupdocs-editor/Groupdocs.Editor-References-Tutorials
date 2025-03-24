---
title: Arbeiten mit kennwortgeschützten Tabellen
linktitle: Arbeiten mit kennwortgeschützten Tabellen
second_title: GroupDocs.Editor .NET API
description: Erfahren Sie, wie Sie mit GroupDocs.Editor für .NET kennwortgeschützte Tabellenkalkulationen verwalten. Diese ausführliche Anleitung führt Sie durch das Öffnen und Speichern sicherer Excel-Dateien.
weight: 18
url: /de/net/document-processing/work-password-protected-spreadsheets/
---

# Arbeiten mit kennwortgeschützten Tabellen

## Einführung
Haben Sie Probleme, passwortgeschützte Tabellen in Ihren .NET-Anwendungen zu verwalten? Wenn ja, sind Sie hier richtig! In dieser umfassenden Anleitung führen wir Sie durch den Prozess der Verwendung von GroupDocs.Editor für .NET, um passwortgeschützte Tabellen effizient zu verwalten. Am Ende dieses Tutorials sind Sie bestens gerüstet, um verschlüsselte Excel-Dateien problemlos zu öffnen, zu bearbeiten und zu speichern.
## Voraussetzungen
Bevor wir uns in den Code vertiefen, stellen wir sicher, dass Sie alles haben, was Sie zum Mitmachen brauchen:
- Grundkenntnisse in C#: Dieses Tutorial setzt voraus, dass Sie mit der C#-Programmierung vertraut sind.
- .NET Framework: Stellen Sie sicher, dass das .NET Framework auf Ihrem Entwicklungscomputer installiert ist.
-  GroupDocs.Editor für .NET: Laden Sie GroupDocs.Editor für .NET herunter und installieren Sie es von[Hier](https://releases.groupdocs.com/editor/net/).
## Namespaces importieren
Um zu beginnen, müssen Sie die erforderlichen Namespaces in Ihr C#-Projekt importieren. Diese Namespaces bieten Zugriff auf die Funktionen von GroupDocs.Editor.
```csharp
using System;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
## Schritt 1: Holen Sie sich einen Pfad zur Eingabedatei
Zunächst benötigen Sie einen Pfad zur Eingabedatei. Für dieses Beispiel verwenden wir eine Excel-Beispieldatei (`Your Sample Document`), das passwortgeschützt ist.
```csharp
string inputFilePath = "Your Sample Document";
```
## Schritt 2: Versuchen Sie, das Dokument ohne Kennwort zu öffnen
Sehen wir uns an, was passiert, wenn wir versuchen, das Dokument ohne Eingabe eines Kennworts zu öffnen.
```csharp
Editor editor = new Editor(inputFilePath);
try
{
    editor.Edit();
}
catch (GroupDocs.Editor.PasswordRequiredException)
{
    Console.WriteLine("Cannot edit the document because it is password-protected. A password is required.");
}
editor.Dispose();
```
## Schritt 3: Geben Sie ein falsches Passwort ein
Jetzt geben wir ein falsches Passwort ein, um zu demonstrieren, wie der Editor reagiert.
```csharp
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.Password = "incorrect_password";
editor = new Editor(inputFilePath, delegate { return loadOptions; });
try
{
    editor.Edit();
}
catch (GroupDocs.Editor.IncorrectPasswordException)
{
    Console.WriteLine("Cannot edit the document because the specified password is incorrect.");
}
editor.Dispose();
```
## Schritt 4: Öffnen Sie die Datei mit dem richtigen Passwort
Geben wir das richtige Passwort ein und öffnen die Datei erfolgreich.
```csharp
loadOptions.Password = "excel_password";
loadOptions.OptimizeMemoryUsage = true;
editor = new Editor(inputFilePath, delegate { return loadOptions; });
```
## Schritt 5: Bearbeitungsoptionen erstellen und anpassen
Um die Tabelle zu bearbeiten, müssen wir die Bearbeitungsoptionen erstellen und anpassen.
```csharp
SpreadsheetEditOptions editOptions = new SpreadsheetEditOptions();
```
## Schritt 6: Erstellen Sie ein vorläufiges bearbeitbares Dokument
 Als nächstes erstellen wir ein Zwischenprodukt`EditableDocument` Dadurch können wir Änderungen an der Tabelle vornehmen.
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
{
    // Schritt 7: Speicheroptionen erstellen
    SpreadsheetFormats xlsmFormat = SpreadsheetFormats.Xlsm;
    SpreadsheetSaveOptions saveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
    // Schritt 7.1: Neues Eröffnungspasswort festlegen
    saveOptions.Password = "new password";
    // Schritt 7.2: Schreibschutz einrichten
    saveOptions.WorksheetProtection = new WorksheetProtection(WorksheetProtectionType.All, "write password");
    // Schritt 8: Speichern Sie das Dokument ohne Änderungen
    //Schritt 8.1: Ausgabedateinamen und -pfad vorbereiten
    string outputFilename = Path.GetFileNameWithoutExtension(inputFilePath) + "." + xlsmFormat.Extension;
    string outputPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename);
    // Schritt 8.2: Ausgabestream erstellen
    using (FileStream outputStream = File.Create(outputPath))
    {
        // Schritt 8.3: Speichern
        editor.Save(beforeEdit, outputStream, saveOptions);
    }
}
// Schritt 9: Entsorgen Sie die Editor-Instanz
editor.Dispose();
Console.WriteLine("Successfully handled the password-protected spreadsheet. Editor instance has been disposed: {0}", editor.IsDisposed ? "Yes" : "No");
```
## Abschluss
Herzlichen Glückwunsch! Sie haben erfolgreich gelernt, wie Sie mit passwortgeschützten Tabellenkalkulationen mithilfe von GroupDocs.Editor für .NET umgehen. Vom Versuch, das Dokument ohne Passwort zu öffnen, bis zum Speichern mit neuen Schutzeinstellungen haben Sie alle wesentlichen Schritte durchlaufen. Dieses Wissen wird zweifellos Ihre Fähigkeit verbessern, sichere Dokumente in Ihren .NET-Anwendungen zu verwalten.
## Häufig gestellte Fragen
### Was ist GroupDocs.Editor für .NET?
GroupDocs.Editor für .NET ist eine leistungsstarke API zur Dokumentbearbeitung, die es Entwicklern ermöglicht, eine Vielzahl von Dokumentformaten in .NET-Anwendungen zu laden, zu bearbeiten und zu speichern.
### Wie kann ich eine temporäre Lizenz für GroupDocs.Editor erhalten?
 Eine vorläufige Lizenz erhalten Sie bei[Hier](https://purchase.groupdocs.com/temporary-license/) um die Eigenschaften des Produkts zu bewerten.
### Ist es möglich, die Speichernutzung beim Bearbeiten großer Dokumente zu optimieren?
 Ja, Sie können die Speicheroptimierung aktivieren, indem Sie die`OptimizeMemoryUsage` Eigentum an`true`in den Ladeoptionen.
### Kann ich zum Öffnen und Schreiben in eine Tabelle unterschiedliche Passwörter festlegen?
Auf jeden Fall! Du kannst in den Speicheroptionen separate Passwörter für das Öffnen des Dokuments und für den Schreibschutz festlegen.
### Wo finde ich ausführlichere Dokumentation?
 Sie können auf die umfassende Dokumentation für GroupDocs.Editor für .NET zugreifen[Hier](https://tutorials.groupdocs.com/editor/net/).