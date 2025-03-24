---
title: Ungültige Formularfeldsammlung korrigieren und speichern
linktitle: Ungültige Formularfeldsammlung korrigieren und speichern
second_title: GroupDocs.Editor .NET API
description: Erfahren Sie, wie Sie ungültige Formularfelder in DOCX mit Groupdocs.Editor für .NET korrigieren. Folgen Sie dieser Anleitung, um sicherzustellen, dass Ihre Dokumente fehlerfrei sind und sicher gespeichert werden.
weight: 11
url: /de/net/form-field-management/fix-invalid-form-field-collection-save/
---
## Einführung
Willkommen! Wenn Sie mit Formularfeldern in Dokumenten arbeiten und Probleme mit ungültigen Formularfeldsammlungen haben, sind Sie hier richtig. In diesem Tutorial erfahren Sie, wie Sie ungültige Formularfelder reparieren und Ihr Dokument mit Groupdocs.Editor für .NET speichern. Wir führen Sie Schritt für Schritt durch den Prozess und stellen sicher, dass Sie alle Details haben, die Sie benötigen, damit alles reibungslos funktioniert. Lassen Sie uns anfangen!
## Voraussetzungen
Bevor wir uns in den Code stürzen, müssen einige Dinge bereitstehen:
-  Groupdocs.Editor für .NET: Stellen Sie sicher, dass Sie die Groupdocs.Editor-Bibliothek für .NET installiert haben. Sie können sie herunterladen[Hier](https://releases.groupdocs.com/editor/net/).
- Entwicklungsumgebung: Sie sollten eine .NET-Entwicklungsumgebung wie Visual Studio eingerichtet haben.
- Grundkenntnisse in C#: Dieses Tutorial setzt voraus, dass Sie über Grundkenntnisse der C#-Programmierung verfügen.
## Namespaces importieren
Zuerst müssen Sie die erforderlichen Namespaces in Ihr C#-Projekt importieren. Fügen Sie am Anfang Ihrer Codedatei die folgenden Zeilen hinzu:
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System;
using System.IO;
```
## Schritt 1: Den Eingabedateipfad abrufen
Der erste Schritt besteht darin, den Pfad zu Ihrer Eingabedatei anzugeben. Diese Datei sollte ein DOCX-Dokument mit Formularfeldern sein.
```csharp
string inputFilePath = Constants.SampleLegacyFormFields_docx;
```
## Schritt 2: Erstellen Sie einen Stream aus dem Dateipfad
Erstellen Sie als Nächstes einen Dateistream zum Lesen des Eingabedokuments. Dadurch können Sie das Dokument in den Editor laden.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
```
## Schritt 3: Ladeoptionen für das Dokument erstellen
In diesem Schritt müssen Sie Ladeoptionen für Ihr Dokument erstellen. Wenn Ihr Dokument kennwortgeschützt ist, können Sie das Kennwort angeben. In diesem Beispiel ist das Dokument nicht geschützt, daher wird das Kennwort ignoriert.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
loadOptions.Password = "some_password_to_open_a_document";
```
## Schritt 4: Laden Sie das Dokument in die Editor-Instanz
Laden Sie nun das Dokument mit den angegebenen Optionen in die Editor-Instanz. Hier finden die wichtigsten Operationen am Dokument statt.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
```
## Schritt 4.1: Lesen der FormFieldManager-Instanz
 Der`FormFieldManager` Instanz ist für die Verwaltung der Formularfelder im Dokument verantwortlich. Sie müssen diese Instanz lesen, um auf die Formularfelder zuzugreifen und sie zu bearbeiten.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
## Schritt 4.2: Lesen der FormFieldCollection
 Der`FormFieldCollection` enthält alle Formularfelder im Dokument. Sie lesen diese Sammlung, um ungültige Formularfelder zu überprüfen und zu korrigieren.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
## Schritt 4.3: Ungültige Formularfelder automatisch korrigieren
Versuchen Sie, alle ungültigen Formularfelder im Dokument automatisch zu korrigieren. Dies ist ein erster Schritt, um offensichtliche Probleme zu beheben.
```csharp
fieldManager.FixInvalidFormFieldNames(new InvalidFormField[0]);
collection = fieldManager.FormFieldCollection;
```
## Schritt 4.4: Auf ungültige Formularfelder prüfen
Überprüfen Sie, ob nach dem automatischen Korrekturversuch noch ungültige Formularfelder vorhanden sind.
```csharp
bool hasInvalidFormFields = fieldManager.HasInvalidFormFields();
Console.WriteLine("FormFieldCollection contains invalid items: {0}", hasInvalidFormFields);
```
## Schritt 4.4.1: Alle ungültigen Formularfeldnamen abrufen
Rufen Sie die Namen aller ungültigen Formularfelder ab. Diese Namen werden verwendet, um die Felder zu korrigieren.
```csharp
var invalidFormFields = fieldManager.GetInvalidFormFieldNames();
```
## Schritt 4.4.2: Eindeutige Namen für ungültige Felder erstellen
Vergeben Sie für jedes ungültige Formularfeld einen eindeutigen Namen. So stellen Sie sicher, dass es nicht zu Konflikten mit vorhandenen Formularfeldnamen kommt.
```csharp
foreach (var invalidItem in invalidFormFields)
{
    invalidItem.FixedName = string.Format("{0}_{1}", invalidItem.Name, Guid.NewGuid());
}
```
## Schritt 4.4.3: Ungültige Formularfelder korrigieren
Korrigieren Sie die ungültigen Formularfelder mit den im vorherigen Schritt erstellten eindeutigen Namen.
```csharp
fieldManager.FixInvalidFormFieldNames(invalidFormFields);
collection = fieldManager.FormFieldCollection;
```
## Schritt 5: Optionen zum Speichern von Dokumenten erstellen
Richten Sie Optionen zum Speichern des Dokuments ein. Dazu gehört das Festlegen des Formats und aller zusätzlichen Speichereinstellungen.
```csharp
WordProcessingFormats docFormat = WordProcessingFormats.Docx;
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(docFormat);
```
## Schritt 5.1: Speichernutzung optimieren
 Wenn Ihr Dokument groß ist und möglicherweise`OutOfMemoryException`aktivieren Sie die Option zur Speicheroptimierung.
```csharp
saveOptions.OptimizeMemoryUsage = true;
```
## Schritt 5.2: Dokument vor Schreibzugriff schützen
Um das Dokument (mit Ausnahme der Formularfelder) vor Änderungen zu schützen, legen Sie ein Schutzkennwort fest.
```csharp
saveOptions.Protection = new WordProcessingProtection(WordProcessingProtectionType.AllowOnlyFormFields, "write_password");
```
## Schritt 6: Speichern Sie das Dokument
Speichern Sie das Dokument abschließend mit den angegebenen Speicheroptionen. Bereiten Sie einen Speicherstream zum Speichern des Ausgabedokuments vor.
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(outputStream, saveOptions);
}
Console.WriteLine("FixInvalidFormFieldCollectionAndSave routine has successfully finished");
```
## Abschluss
 Und da haben Sie es! Sie haben erfolgreich ungültige Formularfelder korrigiert und Ihr Dokument mit Groupdocs.Editor für .NET gespeichert. Diese Schritt-für-Schritt-Anleitung sollte den Vorgang klar und handhabbar gemacht haben. Wenn Sie auf Probleme stoßen oder Fragen haben, können Sie gerne die[Dokumentation](https://tutorials.groupdocs.com/editor/net/) oder wenden Sie sich an[Unterstützung](https://forum.groupdocs.com/c/editor/20).
## Häufig gestellte Fragen
### Was ist, wenn mein Dokument passwortgeschützt ist?
 Sie können das Passwort im`WordProcessingLoadOptions` , um das Dokument zu öffnen.
### Wie erkenne ich, ob es ungültige Formularfelder gibt?
 Verwenden Sie die`HasInvalidFormFields` Methode, um zu prüfen, ob im Dokument ungültige Formularfelder vorhanden sind.
### Kann ich Formularfelder reparieren, ohne ihre Namen zu ändern?
Es wird empfohlen, für ungültige Formularfelder eindeutige Namen zu erstellen, um Konflikte zu vermeiden.
### In welchen Formaten kann ich das Dokument speichern?
 Sie können das Dokument in verschiedenen Formaten wie DOCX, PDF und mehr speichern, indem Sie die entsprechenden`WordProcessingFormats`.
### Wie kann ich die Speichernutzung beim Speichern großer Dokumente optimieren?
 Aktivieren Sie die`OptimizeMemoryUsage` im`WordProcessingSaveOptions` um große Dokumente effizient zu verarbeiten.