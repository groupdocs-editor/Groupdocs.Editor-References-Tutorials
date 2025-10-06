---
title: Abrufen von HTML-Inhalten mit Präfix
linktitle: Abrufen von HTML-Inhalten mit Präfix
second_title: GroupDocs.Editor .NET API
description: Erfahren Sie, wie Sie mit GroupDocs.Editor für .NET HTML-Inhalte aus Dokumenten mit benutzerdefinierten Präfixen für Bilder und Stylesheets abrufen. Schritt-für-Schritt-Anleitung enthalten.
weight: 11
url: /de/net/html-content-retrieval/retrieve-html-content-with-prefix/
type: docs
---
# Abrufen von HTML-Inhalten mit Präfix

## Einführung
Willkommen zu unserem Schritt-für-Schritt-Tutorial zum Abrufen von HTML-Inhalten aus einem Dokument mithilfe von GroupDocs.Editor für .NET. Egal, ob Sie ein erfahrener Entwickler sind oder gerade erst anfangen, diese Anleitung führt Sie auf leicht verständliche Weise durch den Prozess. Wir behandeln alles, was Sie wissen müssen, vom Einrichten Ihrer Umgebung bis zur erfolgreichen Ausführung des Codes. Tauchen Sie ein!
## Voraussetzungen
Bevor wir beginnen, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:
1.  GroupDocs.Editor für .NET: Laden Sie die neueste Version herunter von der[Download-Seite](https://releases.groupdocs.com/editor/net/).
2. Entwicklungsumgebung: Visual Studio oder eine andere bevorzugte .NET-Entwicklungsumgebung.
3. Grundkenntnisse in C#: Wenn Sie mit der C#-Programmierung vertraut sind, können Sie den Beispielen leichter folgen.
4. Zu bearbeitendes Dokument: Halten Sie zum Testen ein Beispieldokument bereit, beispielsweise ein Word-Dokument.
5. .NET Framework: Stellen Sie sicher, dass .NET Framework auf Ihrem Computer installiert ist.
Nun, da Sie alles bereit haben, können wir loslegen!
## Namespaces importieren
Zuerst müssen Sie die erforderlichen Namespaces in Ihr C#-Projekt importieren. Diese Namespaces stellen die Klassen und Methoden bereit, die für die Arbeit mit GroupDocs.Editor für .NET erforderlich sind.
```csharp
using System;
using GroupDocs.Editor.Options;
```
Nachdem die Namespaces importiert wurden, können wir mit der Einrichtung des Editors fortfahren.
## Schritt 1: Initialisieren des Editors
 Zunächst müssen Sie den`Editor`Klasse mit Ihrem Dokument. In diesem Schritt müssen Sie das zu bearbeitende Dokument angeben und die erforderlichen Ladeoptionen bereitstellen.
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
    // Weitere Schritte werden hier hinzugefügt
}
```
 In diesem Beispiel laden wir ein Word-Dokument. Sie können ersetzen`"Your Sample Document"` durch den Pfad zu Ihrem Dokument.
## Schritt 2: Bearbeiten Sie das Dokument
 Als nächstes müssen wir das Dokument zum Bearbeiten öffnen. Dies geschieht über das`Edit` Methode der`Editor` Klasse, die erfordert`WordProcessingEditOptions` als Argument.
```csharp
using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
{
    // Weitere Schritte werden hier hinzugefügt
}
```
 Der`EditableDocument` Instanz stellt das Dokument in einem editierbaren Format dar. Jetzt können wir den HTML-Inhalt abrufen.
## Schritt 3: Benutzerdefinierte Präfixe definieren
Um benutzerdefinierte Präfixe für Bilder und CSS hinzuzufügen, müssen wir die Präfixe als Zeichenfolgen definieren. Dieser Schritt stellt sicher, dass der HTML-Inhalt die angegebenen Präfixe für externe Ressourcen enthält.
```csharp
string externalImagesPrefix = "http://www.meinewebsite.com/images/id=";
string externalCssPrefix = "http://www.meinewebsite.com/css/id=";
```
Sie können die URLs durch die gewünschten Präfixe ersetzen. Diese Präfixe werden im nächsten Schritt verwendet, um die HTML-Ausgabe anzupassen.
## Schritt 4: HTML-Inhalt abrufen
Nachdem wir nun unsere Präfixe festgelegt haben, können wir den HTML-Inhalt aus dem Dokument abrufen.`GetContent` Methode der`EditableDocument` Klasse ermöglicht es uns, das Bild und die CSS-Präfixe anzugeben.
```csharp
string prefixedHtmlContent = document.GetContent(externalImagesPrefix, externalCssPrefix);
Console.WriteLine("HTML content of the input document with custom image and stylesheet prefixes: {0}", prefixedHtmlContent);
```
Dieser Codeausschnitt holt den HTML-Inhalt mit den benutzerdefinierten Präfixen und gibt ihn auf der Konsole aus. Sie können diesen HTML-Inhalt nach Bedarf weiterverarbeiten oder speichern.
## Abschluss
Und da haben Sie es! Indem Sie diese Schritte befolgen, können Sie mit GroupDocs.Editor für .NET ganz einfach HTML-Inhalte aus einem Dokument abrufen, komplett mit benutzerdefinierten Präfixen für Bilder und Stylesheets. Dieses leistungsstarke Tool vereinfacht die Dokumentbearbeitung, sodass Sie sich auf die nahtlose Integration der Dokumentbearbeitung in Ihre .NET-Anwendungen konzentrieren können.
 Ausführlichere Informationen finden Sie im[GroupDocs.Editor für .NET-Dokumentation](https://tutorials.groupdocs.com/editor/net/) Wenn Sie Fragen haben oder weitere Hilfe benötigen, wenden Sie sich bitte an[Hilfeforum](https://forum.groupdocs.com/c/editor/20).
## Häufig gestellte Fragen
### Welche Dokumenttypen kann ich mit GroupDocs.Editor für .NET bearbeiten?
GroupDocs.Editor unterstützt verschiedene Dokumentformate, darunter Word, Excel, PowerPoint, PDF und mehr.
### Wie erhalte ich eine kostenlose Testversion von GroupDocs.Editor für .NET?
 Sie erhalten eine kostenlose Testversion von[GroupDocs-Website](https://releases.groupdocs.com/).
### Kann ich den HTML-Inhalt weiter anpassen?
Ja, Sie können den abgerufenen HTML-Inhalt vor dem Rendern oder Speichern nach Bedarf ändern.
### Ist es möglich, GroupDocs.Editor für .NET mit anderen .NET-Sprachen zu verwenden?
Ja, Sie können es mit jeder .NET-kompatiblen Sprache wie VB.NET oder F# verwenden.
### Wie erhalte ich eine temporäre Lizenz für GroupDocs.Editor für .NET?
 Eine vorläufige Lizenz erhalten Sie bei der[Kaufseite](https://purchase.groupdocs.com/temporary-license/).