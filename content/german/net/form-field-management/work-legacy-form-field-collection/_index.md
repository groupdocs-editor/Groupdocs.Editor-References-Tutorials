---
title: Arbeiten mit der Legacy-Formularfeldsammlung
linktitle: Arbeiten mit der Legacy-Formularfeldsammlung
second_title: GroupDocs.Editor .NET API
description: Erfahren Sie in unserem ausführlichen Handbuch, wie Sie mit GroupDocs.Editor für .NET ältere Formularfelder verwalten. Perfekt für die Handhabung von Textfeldern, Kontrollkästchen, Daten und mehr.
weight: 12
url: /de/net/form-field-management/work-legacy-form-field-collection/
type: docs
---
# Arbeiten mit der Legacy-Formularfeldsammlung

## Einführung
Willkommen zu dieser umfassenden Anleitung zum Arbeiten mit älteren Formularfeldsammlungen mithilfe von GroupDocs.Editor für .NET. Egal, ob Sie mit Textfeldern, Kontrollkästchen, Datumsfeldern oder Dropdown-Menüs arbeiten, dieses Tutorial führt Sie Schritt für Schritt durch die effiziente Verwaltung dieser Felder. Am Ende dieser Anleitung verfügen Sie über ein solides Verständnis für die Verwendung von GroupDocs.Editor zur Handhabung verschiedener Formularfelder in Ihren Dokumenten. Lassen Sie uns loslegen!
## Voraussetzungen
Bevor wir beginnen, stellen Sie sicher, dass Sie die folgenden Voraussetzungen erfüllen:
- Visual Studio: Jede aktuelle Version funktioniert.
- .NET Framework: Stellen Sie sicher, dass Sie .NET Framework installiert haben.
-  GroupDocs.Editor für .NET: Laden Sie die neueste Version herunter[Hier](https://releases.groupdocs.com/editor/net/).
- Beispieldokument: Eine Beispiel-DOCX-Datei mit Formularfeldern zu Testzwecken.
## Namespaces importieren
Importieren Sie zunächst die erforderlichen Namespaces in Ihr Projekt. Diese Namespaces sind für den Zugriff auf die Klassen und Methoden, die zur Bearbeitung von Formularfeldern erforderlich sind, unerlässlich.
```csharp
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System.IO;
```
## Schritt 1: Den Eingabedateipfad abrufen
Zuerst müssen Sie den Pfad zu Ihrer Eingabedatei angeben. In diesem Beispiel verwenden wir eine Beispiel-DOCX-Datei, die verschiedene Formularfelder enthält.
```csharp
string inputFilePath = "path/to/your/sample_legacy_formfields.docx";
```
## Schritt 2: Erstellen Sie einen Stream aus dem Dateipfad
Erstellen Sie als Nächstes einen Dateistream, um den Inhalt Ihres Dokuments zu lesen. Dieser Stream wird verwendet, um das Dokument in den GroupDocs.Editor zu laden.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
    // Hier kommt zusätzlicher Code rein
}
```
## Schritt 3: Ladeoptionen für das Dokument erstellen
Erstellen Sie vor dem Laden des Dokuments Ladeoptionen. Diese Optionen helfen bei der Handhabung verschiedener Szenarien, beispielsweise kennwortgeschützter Dokumente.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
// Wenn das Dokument passwortgeschützt ist, geben Sie das Passwort an
loadOptions.Password = "your_password_here"; // Verwenden Sie bei Bedarf ein aktuelles Passwort
```
## Schritt 4: Laden Sie das Dokument mit der Editor-Instanz
Laden Sie nun das Dokument in die Editorinstanz, indem Sie den Dateistream und die Ladeoptionen verwenden, die Sie zuvor erstellt haben.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    // Hier kommt zusätzlicher Code rein
}
```
## Schritt 5: Lesen Sie die FormFieldManager-Instanz
Um Formularfelder zu verwalten, greifen Sie über den Editor auf die Instanz FormFieldManager zu. Mit dieser Instanz können Sie mit den Formularfeldern in Ihrem Dokument interagieren.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
## Schritt 6: Lesen der FormFieldCollection
Rufen Sie die FormFieldCollection aus dem FormFieldManager ab. Diese Sammlung enthält alle im Dokument vorhandenen Formularfelder.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
## Schritt 7: Durch jedes Formularfeld iterieren
Durchlaufen Sie jedes Formularfeld in der Sammlung und ermitteln Sie seinen Typ. Abhängig vom Typ können Sie den Wert des Felds extrahieren und bearbeiten.
```csharp
foreach (var formField in collection)
{
    switch (formField.Type)
    {
        case FormFieldType.Text:
            TextFormField textFormField = collection.GetFormField<TextFormField>(formField.Name);
            Console.WriteLine($"TextFormField detected, name: {formField.Name}, value: {textFormField.Value}");
            break;
        case FormFieldType.CheckBox:
            CheckBoxForm checkBoxFormField = collection.GetFormField<CheckBoxForm>(formField.Name);
            Console.WriteLine($"CheckBoxForm detected, name: {formField.Name}, value: {checkBoxFormField.Value}");
            break;
        case FormFieldType.Date:
            DateFormField dateFormField = collection.GetFormField<DateFormField>(formField.Name);
            Console.WriteLine($"DateFormField detected, name: {formField.Name}, value: {dateFormField.Value}");
            break;
        case FormFieldType.Number:
            NumberFormField numberFormField = collection.GetFormField<NumberFormField>(formField.Name);
            Console.WriteLine($"NumberFormField detected, name: {formField.Name}, value: {numberFormField.Value}");
            break;
        case FormFieldType.DropDown:
            DropDownFormField dropDownFormField = collection.GetFormField<DropDownFormField>(formField.Name);
            Console.WriteLine($"DropDownFormField detected, name: {formField.Name}, value selected: {dropDownFormField.Value[dropDownFormField.SelectedIndex]}");
            break;
    }
}
```
## Schritt 8: Fazit
Wenn Sie diese Schritte befolgen, können Sie mit GroupDocs.Editor für .NET ältere Formularfelder in Ihren Dokumenten effektiv verwalten und mit ihnen interagieren. Ob Textfelder, Kontrollkästchen, Daten, Zahlen oder Dropdown-Listen – dieser Leitfaden bietet eine klare und prägnante Möglichkeit, mit jedem Typ umzugehen.
## Abschluss
 Das Arbeiten mit alten Formularfeldern in Dokumenten kann mit den richtigen Tools unkompliziert sein. GroupDocs.Editor für .NET bietet eine robuste Lösung für die effiziente Verwaltung dieser Felder. Wenn Sie dieser Schritt-für-Schritt-Anleitung folgen, sollten Sie nun in der Lage sein, verschiedene Formularfelder in Ihren Dokumenten problemlos zu bearbeiten. Vergessen Sie nicht, die[Dokumentation](https://tutorials.groupdocs.com/editor/net/)für erweiterte Funktionen und Optionen.
## Häufig gestellte Fragen
### 1. Kann ich GroupDocs.Editor für .NET mit passwortgeschützten Dokumenten verwenden?
Ja, Sie können für den Umgang mit passwortgeschützten Dokumenten das Passwort in den Ladeoptionen angeben.
### 2. Wie erhalte ich eine kostenlose Testversion von GroupDocs.Editor für .NET?
 Sie können eine kostenlose Testversion herunterladen unter[Hier](https://releases.groupdocs.com/).
### 3. Gibt es Support für GroupDocs.Editor für .NET?
 Ja, Sie können Support in Anspruch nehmen[Hier](https://forum.groupdocs.com/c/editor/20).
### 4. Kann ich eine Lizenz für GroupDocs.Editor für .NET erwerben?
 Ja, Sie können eine Lizenz kaufen bei[Hier](https://purchase.groupdocs.com/buy).
### 5. Wo finde ich die Dokumentation für GroupDocs.Editor für .NET?
Die Dokumentation ist verfügbar[Hier](https://tutorials.groupdocs.com/editor/net/).