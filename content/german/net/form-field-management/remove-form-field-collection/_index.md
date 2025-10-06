---
title: Formularfeldsammlung entfernen
linktitle: Formularfeldsammlung entfernen
second_title: GroupDocs.Editor .NET API
description: Erfahren Sie in dieser Schritt-für-Schritt-Anleitung, wie Sie mit GroupDocs.Editor für .NET Formularfelder aus Word-Dokumenten entfernen. Ideal für Entwickler.
weight: 13
url: /de/net/form-field-management/remove-form-field-collection/
type: docs
---
# Formularfeldsammlung entfernen

## Einführung
Möchten Sie Formularfelder in Ihren Dokumenten programmgesteuert verwalten? GroupDocs.Editor für .NET bietet eine leistungsstarke Lösung zum Verarbeiten und Bearbeiten von Formularfeldern in verschiedenen Dokumentformaten. In diesem Tutorial führen wir Sie durch die Schritte zum Entfernen von Formularfeldsammlungen aus einem Word-Dokument mithilfe dieser robusten Bibliothek. 
## Voraussetzungen
Bevor wir uns in den Code vertiefen, stellen wir sicher, dass Sie alles für ein reibungsloses Erlebnis eingerichtet haben:
1. GroupDocs.Editor für .NET: Stellen Sie sicher, dass Sie GroupDocs.Editor für .NET heruntergeladen und installiert haben. Wenn nicht, können Sie es herunterladen[Hier](https://releases.groupdocs.com/editor/net/).
2. Entwicklungsumgebung: Sie benötigen eine Entwicklungsumgebung wie Visual Studio.
3. .NET Framework: Stellen Sie sicher, dass .NET Framework auf Ihrem Computer installiert ist.
4.  Beispieldokument: Halten Sie ein Beispiel-Word-Dokument bereit (z. B.`SampleLegacyFormFields.docx`) mit Formularfeldern, die Sie bearbeiten möchten.

## Namespaces importieren
Um zu beginnen, müssen Sie die erforderlichen Namespaces in Ihr .NET-Projekt importieren. Dadurch können Sie auf die Funktionen von GroupDocs.Editor zugreifen.
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System.IO;
```
## Schritt 1: Dokument laden
Zuerst müssen Sie das Dokument laden, das Sie bearbeiten möchten. Lassen Sie uns das im Einzelnen erklären:
### Schritt 1.1: Den Pfad zur Eingabedatei abrufen
 Sie müssen den Pfad zu Ihrer Eingabedatei angeben. Für dieses Beispiel verwenden wir eine Beispieldatei namens`SampleLegacyFormFields.docx`.
```csharp
string inputFilePath = "path/to/SampleLegacyFormFields.docx";
```
### Schritt 1.2: Erstellen Sie einen FileStream aus dem Pfad
 Erstellen Sie als Nächstes eine`FileStream` um das Dokument zu lesen.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
    // Fahren Sie mit den nächsten Schritten innerhalb dieses Using-Blocks fort.
}
```
## Schritt 2: Ladeoptionen festlegen
Beim Laden des Dokuments müssen Sie möglicherweise Ladeoptionen angeben, insbesondere wenn Ihr Dokument kennwortgeschützt ist.
### Schritt 2.1: Ladeoptionen erstellen
 Erstellen Sie eine Instanz von`WordProcessingLoadOptions`.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
```
### Schritt 2.2: Passwort festlegen (falls erforderlich)
Wenn Ihr Dokument passwortgeschützt ist, können Sie das Passwort angeben.
```csharp
loadOptions.Password = "some_password_to_open_a_document";
```
## Schritt 3: Laden Sie das Dokument in den Editor
 Laden Sie nun das Dokument in den`Editor` Instanz mit dem`FileStream` Und`LoadOptions`.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    // Fahren Sie mit den nächsten Schritten innerhalb dieses Using-Blocks fort.
}
```
## Schritt 4: Auf Formularfelder zugreifen und diese verwalten
Nachdem das Dokument geladen wurde, können Sie nun auf die Formularfelder zugreifen und diese bearbeiten.
### Schritt 4.1: Lesen des FormFieldManagers
 Abrufen der`FormFieldManager` von dem`Editor` Beispiel.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
### Schritt 4.2: Zugriff auf FormFieldCollection
 Bekommen das`FormFieldCollection` das alle Formularfelder im Dokument enthält.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
### Schritt 4.3: Entfernen eines bestimmten Textformularfelds
Um ein bestimmtes Textformularfeld zu entfernen, suchen Sie es anhand seines Namens und entfernen Sie es.
```csharp
TextFormField textField = collection.GetFormField<TextFormField>("Text1");
fieldManager.RemoveFormFiled(textField);
```
### Schritt 4.4: Mehrere Formularfelder entfernen
Sie können auch mehrere Formularfelder auf einmal entfernen, indem Sie ihre Namen angeben.
```csharp
textField = collection.GetFormField<TextFormField>("Text7");
CheckBoxForm checkBoxForm = collection.GetFormField<CheckBoxForm>("Check2");
fieldManager.RemoveFormFields(new IFormField[] { textField, checkBoxForm });
```
## Schritt 5: Speichern Sie das geänderte Dokument
Nachdem Sie die Formularfelder geändert haben, müssen Sie das Dokument speichern.
### Schritt 5.1: Speicheroptionen erstellen
Geben Sie das Format und die Speicheroptionen für das Ausgabedokument an.
```csharp
WordProcessingFormats docFormat = WordProcessingFormats.Docx;
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(docFormat);
```
### Schritt 5.2: Speichernutzung optimieren
Wenn Sie mit großen Dokumenten arbeiten, möchten Sie möglicherweise die Speichernutzung optimieren.
```csharp
saveOptions.OptimizeMemoryUsage = true;
```
### Schritt 5.3: Schutz einrichten (falls erforderlich)
Durch die Festlegung eines Schreibkennworts können Sie das Dokument vor weiterer Bearbeitung schützen.
```csharp
saveOptions.Protection = new WordProcessingProtection(WordProcessingProtectionType.AllowOnlyFormFields, "write_password");
```
### Schritt 5.4: Speichern Sie das Dokument
 Speichern Sie das Dokument abschließend mit einem`MemoryStream`.
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(outputStream, saveOptions);
}
```

## Abschluss
Herzlichen Glückwunsch! Sie haben erfolgreich Formularfelder aus einem Word-Dokument mithilfe von GroupDocs.Editor für .NET entfernt. Diese leistungsstarke Bibliothek erleichtert die programmgesteuerte Bearbeitung von Dokumentinhalten und spart Ihnen Zeit und Mühe.
## Häufig gestellte Fragen
### Kann ich GroupDocs.Editor für .NET mit anderen Dokumentformaten verwenden?
Ja, GroupDocs.Editor für .NET unterstützt verschiedene Dokumentformate, darunter PDF, HTML und mehr.
### Ist es möglich, mit GroupDocs.Editor für .NET Formularfelder hinzuzufügen?
Ja, Sie können Formularfelder programmgesteuert hinzufügen, ändern und entfernen.
### Was ist, wenn mein Dokument sehr groß ist?
Um große Dokumente effizient zu verarbeiten, können Sie in den Speicheroptionen die Speicheroptimierung aktivieren.
### Kann ich GroupDocs.Editor für .NET in einer Webanwendung verwenden?
Auf jeden Fall! GroupDocs.Editor für .NET kann zur serverseitigen Dokumentverarbeitung in Webanwendungen integriert werden.
### Wo erhalte ich Unterstützung, wenn Probleme auftreten?
 Besuchen Sie die[Hilfeforum](https://forum.groupdocs.com/c/editor/20) für Hilfe bei allen Problemen.