---
date: 2026-05-12
description: Erfahren Sie, wie Sie Schriftarten und andere HTML‑Ressourcen aus Dokumenten
  mit GroupDocs.Editor für .NET extrahieren. Schritt‑für‑Schritt‑Anleitung für .NET‑Entwickler.
keywords:
- how to extract fonts
- GroupDocs.Editor .NET
- extract HTML resources
linktitle: HTML‑Ressourcen in Ordner speichern
schemas:
- author: GroupDocs
  dateModified: '2026-05-12'
  description: Learn how to extract fonts and other HTML resources from documents
    using GroupDocs.Editor for .NET. Step‑by‑step guide for .NET developers.
  headline: How to Extract Fonts and Save HTML Resources to Folder
  type: TechArticle
- description: Learn how to extract fonts and other HTML resources from documents
    using GroupDocs.Editor for .NET. Step‑by‑step guide for .NET developers.
  name: How to Extract Fonts and Save HTML Resources to Folder
  steps:
  - name: '**Basic Knowledge of C# and .NET** – Familiarity with C# programming language
      and .NET framework is essential to follow along with the examples.'
    text: '**Basic Knowledge of C# and .NET** – Familiarity with C# programming language
      and .NET framework is essential to follow along with the examples.'
  - name: '**GroupDocs.Editor for .NET Library** – Download and install GroupDocs.Editor
      for .NET library from the [website](https://releases.groupdocs.com/editor/net/).'
    text: '**GroupDocs.Editor for .NET Library** – Download and install GroupDocs.Editor
      for .NET library from the [website](https://releases.groupdocs.com/editor/net/).'
  - name: '**Development Environment** – Set up your preferred development environment
      such as Visual Studio or any other compatible IDE.'
    text: '**Development Environment** – Set up your preferred development environment
      such as Visual Studio or any other compatible IDE.'
  type: HowTo
- questions:
  - answer: Yes, it supports Excel, PowerPoint, PDF, HTML, and over 50 additional
      formats for both editing and resource extraction.
    question: Is GroupDocs.Editor compatible with other document formats besides Word?
  - answer: Absolutely. The API works seamlessly with ASP.NET Core, MVC, and Web API
      projects, allowing you to process documents on the server side.
    question: Can I integrate GroupDocs.Editor into a web application?
  - answer: Yes, it includes built‑in connectors for Google Drive, Dropbox, OneDrive,
      and Amazon S3, enabling direct loading and saving of documents in the cloud.
    question: Does GroupDocs.Editor provide cloud storage integration?
  - answer: A fully functional 30‑day trial can be downloaded from the GroupDocs website
      without any credit‑card requirement.
    question: Is there a free trial available for GroupDocs.Editor?
  - answer: You can reach the GroupDocs support team via the official forum, submit
      a ticket through the customer portal, or consult the detailed API documentation.
    question: How can I get technical support for extraction issues?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Wie man Schriftarten extrahiert und HTML‑Ressourcen in einen Ordner speichert
type: docs
url: /de/net/document-editing/save-html-resources-to-folder/
weight: 13
---

# Wie man Schriftarten extrahiert und HTML-Ressourcen in einen Ordner speichert

## Einführung
GroupDocs.Editor für .NET ermöglicht es Ihnen, **wie man Schriftarten extrahiert** und andere Ressourcen aus einem Dokument zu extrahieren, während es in HTML konvertiert wird. In wenigen Zeilen C# können Sie Bilder, Stylesheets und Schriftdateien herausziehen und sie in einem Ordner Ihrer Wahl speichern. Dieses Tutorial führt Sie durch den gesamten Arbeitsablauf, von der Initialisierung des Editors bis zum Speichern jeder Ressource auf der Festplatte.

## Schnelle Antworten
- **Was bedeutet „wie man Schriftarten extrahiert“?** Es ist der Prozess, eingebettete Schriftdateien aus einem Quelldokument während der HTML-Konvertierung abzurufen.  
- **Welche Bibliothek übernimmt das?** GroupDocs.Editor für .NET bietet eine dedizierte API zum Extrahieren von Schriftarten, Bildern und Stylesheets.  
- **Benötige ich eine Lizenz?** Eine kostenlose Testversion ist verfügbar; für den Produktionseinsatz ist eine kommerzielle Lizenz erforderlich.  
- **Welche .NET-Versionen werden unterstützt?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.  
- **Kann ich einen benutzerdefinierten Ordner angeben?** Ja, Sie geben beim Speichern der extrahierten Ressourcen einen beliebigen beschreibbaren Pfad an.

## Was bedeutet „wie man Schriftarten extrahiert“?
**Wie man Schriftarten extrahiert** bezieht sich auf das Abrufen der ursprünglichen Schriftdateien, die in einem Quelldokument (z. B. DOCX, PPTX) eingebettet sind, damit sie vom erzeugten HTML referenziert werden können. Dies stellt sicher, dass Text in Browsern exakt wie beabsichtigt dargestellt wird, ohne auf Systemschriftarten zurückzugreifen.

## Warum GroupDocs.Editor für die Extraktion von HTML-Ressourcen verwenden?
GroupDocs.Editor unterstützt **mehr als 50 Eingabe- und Ausgabeformate** – darunter DOCX, PPTX, PDF und HTML – und kann Dokumente mit **bis zu 300 Seiten** verarbeiten, ohne die gesamte Datei in den Speicher zu laden. Seine API extrahiert Schriftarten, Bilder und CSS in einem einzigen Durchlauf und reduziert die Entwicklungszeit im Vergleich zur manuellen Analyse um bis zu **70 %**.

## Voraussetzungen
Bevor Sie in das Tutorial einsteigen, stellen Sie sicher, dass Sie die folgenden Voraussetzungen erfüllen:
1. **Grundkenntnisse in C# und .NET** – Vertrautheit mit der Programmiersprache C# und dem .NET-Framework ist erforderlich, um den Beispielen folgen zu können.  
2. **GroupDocs.Editor für .NET Bibliothek** – Laden Sie die GroupDocs.Editor für .NET Bibliothek von der [Website](https://releases.groupdocs.com/editor/net/) herunter und installieren Sie sie.  
3. **Entwicklungsumgebung** – Richten Sie Ihre bevorzugte Entwicklungsumgebung ein, z. B. Visual Studio oder eine andere kompatible IDE.

## Namespaces importieren
Um loszulegen, importieren Sie die notwendigen Namespaces in Ihrem C#‑Projekt:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```

## Wie man Schriftarten extrahiert und HTML-Ressourcen in einen Ordner speichert?
Laden Sie Ihr Quelldokument mit `Editor editor = new Editor("sample.docx", new WordProcessingLoadOptions());` und rufen Sie anschließend `editor.Save("output.html", SaveOptions.Html);` auf. Nach dem Speichervorgang enthält die `Resources`‑Sammlung alle extrahierten Assets – einschließlich Schriftarten –, die Sie iterieren und auf die Festplatte schreiben können. Dieser Ein‑Schritt‑Ansatz erledigt sowohl die Konvertierung als auch die Ressourcenaus extraction automatisch.

## Schritt 1: GroupDocs.Editor initialisieren
`Editor` ist die Kernklasse, die das Laden, die Konvertierung und die Ressourcenaus extraction von Dokumenten orchestriert. Sie repräsentiert eine einzelne Dokumentsitzung im Speicher.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
Zuerst initialisieren Sie das `Editor`‑Objekt, indem Sie den Pfad zu Ihrem Beispieldokument angeben. In diesem Beispiel verwenden wir ein Word‑Dokument, daher geben wir `WordProcessingLoadOptions` als Dokumenttyp an.

## Schritt 2: Dokument bearbeiten
`EditableDocument` ist die bearbeitbare Darstellung, die von der `Edit`‑Methode zurückgegeben wird und es Ihnen ermöglicht, das Dokument vor dem Speichern zu manipulieren.

```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
Als Nächstes erstellen Sie ein `EditableDocument`‑Objekt, indem Sie die `Edit`‑Methode des `Editor`‑Objekts aufrufen. Dadurch können Sie Bearbeitungsvorgänge am Dokument durchführen.

## Schritt 3: Ressourcen extrahieren
`Resources` ist eine Sammlung, die extrahierte Assets – Bilder, Schriftarten und Stylesheets – in separate Listen gruppiert, um die Handhabung zu erleichtern.

```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
Extrahieren Sie Ressourcen wie Bilder, Schriftarten und Stylesheets aus dem Dokument und speichern Sie sie in den jeweiligen Listen.

## Schritt 4: Ausgabeverzeichnis angeben
`outputFolder` ist ein String, der definiert, wohin die extrahierten Dateien geschrieben werden. Sie können ihn auf jedes beschreibbare Verzeichnis auf dem Server oder dem lokalen Rechner verweisen.

```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
Definieren Sie das Ausgabeverzeichnis, in dem die extrahierten Ressourcen gespeichert werden. Sie können den Ordnerpfad nach Ihren Anforderungen anpassen.

## Schritt 5: Ressourcen speichern
`SaveResource` ist eine Hilfsroutine, die eine einzelne binäre Ressource (Bild, Schriftart oder Stylesheet) in das Dateisystem schreibt.

```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
Durchlaufen Sie jede Bildressource, speichern Sie sie im Ausgabeverzeichnis und zeigen Sie relevante Informationen wie Dateiname, Typ und Abmessungen an.

```csharp
		foreach (FontResourceBase oneFont in fonts)
		{
			Console.WriteLine("Saving {0} of {1} type",
				oneFont.FilenameWithExtension, oneFont.Type.FormalName);
			oneFont.Save(Path.Combine(outputFolder, oneFont.FilenameWithExtension));
		}
```
Speichern Sie analog jede Schriftartressource im Ausgabeverzeichnis.

```csharp
		foreach (CssText oneStylesheet in stylesheets)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} encoding",
				oneStylesheet.FilenameWithExtension, oneStylesheet.Type.FormalName, oneStylesheet.Encoding);
			oneStylesheet.Save(Path.Combine(outputFolder, oneStylesheet.FilenameWithExtension));
		}
	}
}
```
Abschließend speichern Sie jedes Stylesheet im Ausgabeverzeichnis und schließen den Bearbeitungsprozess ab.

## Häufige Probleme und Lösungen
- **Fehlende Schriftarten nach der Konvertierung** – Stellen Sie sicher, dass das Quelldokument die Schriftarten tatsächlich einbettet; andernfalls kann GroupDocs.Editor nur Systemschriftarten referenzieren.  
- **Zugriff verweigert-Fehler** – Vergewissern Sie sich, dass der Anwendungsprozess Schreibrechte für das Zielausgabeverzeichnis hat.  
- **Große Dokumente verursachen hohen Speicherverbrauch** – Verwenden Sie `LoadOptions` mit `LoadMode = LoadMode.Stream`, um große Dateien zu streamen, anstatt sie vollständig in den Speicher zu laden.

## Häufig gestellte Fragen

**Q: Ist GroupDocs.Editor mit anderen Dokumentformaten außer Word kompatibel?**  
A: Ja, es unterstützt Excel, PowerPoint, PDF, HTML und über 50 weitere Formate sowohl für die Bearbeitung als auch für die Ressourcenaus extraction.

**Q: Kann ich GroupDocs.Editor in eine Webanwendung integrieren?**  
A: Absolut. Die API funktioniert nahtlos mit ASP.NET Core, MVC und Web‑API‑Projekten und ermöglicht die serverseitige Verarbeitung von Dokumenten.

**Q: Bietet GroupDocs.Editor eine Cloud‑Speicher‑Integration?**  
A: Ja, es enthält integrierte Connectoren für Google Drive, Dropbox, OneDrive und Amazon S3, sodass Dokumente direkt in der Cloud geladen und gespeichert werden können.

**Q: Gibt es eine kostenlose Testversion von GroupDocs.Editor?**  
A: Eine voll funktionsfähige 30‑tägige Testversion kann von der GroupDocs‑Website ohne Angabe einer Kreditkarte heruntergeladen werden.

**Q: Wie kann ich technischen Support für Extraktionsprobleme erhalten?**  
A: Sie können das GroupDocs‑Support‑Team über das offizielle Forum erreichen, ein Ticket über das Kundenportal einreichen oder die ausführliche API‑Dokumentation konsultieren.

---

**Zuletzt aktualisiert:** 2026-05-12  
**Getestet mit:** GroupDocs.Editor 23.11 für .NET  
**Autor:** GroupDocs

## Verwandte Tutorials

- [Effizientes Dokumenten-Editing mit GroupDocs.Editor .NET: HTML in bearbeitbare Dokumente umwandeln](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)
- [Effizientes Extrahieren und Speichern von DOCX-Ressourcen mit GroupDocs.Editor .NET – Komplettanleitung](/editor/net/document-saving/efficient-extract-save-docx-resources-groupdocs-editor-net/)
- [Meisterhaftes Dokumenten-Editing und -Konvertierung mit GroupDocs.Editor .NET: Eine Komplettanleitung](/editor/net/document-editing/groupdocs-editor-net-mastering-document-editing/)