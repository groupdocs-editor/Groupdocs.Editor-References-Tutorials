---
date: 2026-09-26
description: Erfahren Sie, wie Sie das css‑Präfix handhaben und css‑Inhalte mit GroupDocs.Editor
  für .NET in diesem ausführlichen Schritt‑für‑Schritt‑Tutorial extrahieren.
keywords:
- handle css prefix
- extract css content
- edit document css
- prepend url to css
lastmod: 2026-09-26
linktitle: CSS‑Inhalt mit Präfix verarbeiten
og_description: Entdecken Sie, wie Sie das css‑Präfix handhaben und css‑Inhalte mit
  GroupDocs.Editor für .NET extrahieren. Folgen Sie einer Schritt‑für‑Schritt‑Anleitung,
  um URLs zu CSS‑Ressourcen vorzuhängen und Stylesheets abzurufen.
og_image_alt: Developer guide showing css prefix handling with GroupDocs.Editor for
  .NET
og_title: Wie man das css‑Präfix in GroupDocs.Editor für .NET handhabt
schemas:
- author: GroupDocs
  dateModified: '2026-09-26'
  description: Learn how to handle css prefix and extract css content using GroupDocs.Editor
    for .NET in this detailed step‑by‑step tutorial.
  headline: How to handle css prefix in GroupDocs.Editor for .NET
  type: TechArticle
- questions:
  - answer: Yes, GroupDocs.Editor for .NET supports PDF, Word, Excel, PowerPoint,
      and many other formats.
    question: Can I use GroupDocs.Editor for .NET with other document formats?
  - answer: Absolutely! You can start your free trial on the [GroupDocs free trial
      page](https://releases.groupdocs.com/).
    question: Is there a free trial available for GroupDocs.Editor for .NET?
  - answer: You can obtain a temporary license from the [temporary license page](https://purchase.groupdocs.com/temporary-license/).
    question: How do I get a temporary license for GroupDocs.Editor for .NET?
  - answer: Detailed documentation is available on the [GroupDocs.Editor for .NET
      documentation site](https://tutorials.groupdocs.com/editor/net/).
    question: Where can I find detailed documentation for GroupDocs.Editor for .NET?
  - answer: You can get support through the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).
    question: What support options are available for GroupDocs.Editor for .NET?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
tags:
- css handling
- GroupDocs.Editor
- .NET document processing
- css prefix
- api tutorial
title: Wie man das css‑Präfix in GroupDocs.Editor für .NET handhabt
type: docs
url: /de/net/css-handling/handle-css-content-with-prefix/
weight: 11
---

# Wie man CSS‑Präfix in GroupDocs.Editor für .NET handhabt

In diesem Tutorial lernen Sie **wie man CSS‑Präfix handhabt**, wenn Sie mit Stylesheets innerhalb eines Dokuments mit GroupDocs.Editor für .NET arbeiten. Egal, ob Sie einer URL zu Bildern, Schriftarten oder anderen externen Ressourcen voranstellen müssen, die nachfolgenden Schritte zeigen Ihnen genau, wie Sie **CSS‑Präfix handhaben** und außerdem, wie Sie **CSS‑Inhalt extrahieren** für die weitere Verarbeitung. Am Ende des Leitfadens können Sie Ressourcenpfade umschreiben, die rohen CSS‑Zeichenketten abrufen und sie mit Zuversicht in Ihren Web‑Workflow integrieren.

## Schnelle Antworten
- **Was bedeutet “CSS‑Präfix handhaben”?** Hinzufügen eines benutzerdefinierten URL‑Präfixes zu externen Ressourcen, die in CSS referenziert werden.  
- **Welche API‑Methode gibt CSS‑Stile zurück?** `EditableDocument.GetCssContent(...)`.  
- **Benötige ich eine Lizenz?** Eine Testlizenz ist verfügbar; für die Produktion ist eine kommerzielle Lizenz erforderlich.  
- **Welche .NET‑Versionen werden unterstützt?** .NET Framework 4.5+ und .NET Core/5/6.  
- **Kann ich das Präfix zur Laufzeit ändern?** Ja – übergeben Sie einfach einen anderen String an `GetCssContent`.

## Was bedeutet das Handhaben von CSS‑Präfix?
Der Begriff bezieht sich auf das Umschreiben der URLs von Bildern, Schriftarten oder anderen externen Assets innerhalb einer CSS‑Datei, sodass sie auf einen von Ihnen kontrollierten Ort zeigen, z. B. ein CDN oder einen sicheren Server. Durch das Voranstellen einer konsistenten Basis‑URL stellen Sie sicher, dass jede Ressource korrekt geladen wird, wenn das Dokument in einem Browser oder einem webbasierten Viewer gerendert wird.

## Warum GroupDocs.Editor zum Extrahieren von CSS‑Inhalt verwenden?
GroupDocs.Editor kann das originale, in Word‑Verarbeitungsdokumenten eingebettete CSS lesen, die rohen Stylesheet‑Zeichenketten zurückgeben und Ihnen ermöglichen, diese vor dem Rendern oder Speichern zu manipulieren. Das eliminiert manuelles Parsen, gewährleistet die Treue zur internen Dokumentrepräsentation und unterstützt **30+ Dateiformate**, während Dateien bis zu **500 MB** verarbeitet werden, ohne die gesamte Datei in den Speicher zu laden.

## Voraussetzungen
Bevor wir beginnen, stellen Sie sicher, dass Sie die folgenden Voraussetzungen erfüllt haben:
- Visual Studio: Sie benötigen eine funktionierende Installation von Visual Studio.  
- .NET Framework: Stellen Sie sicher, dass das .NET Framework installiert ist.  
- GroupDocs.Editor for .NET: Sie können es von der [GroupDocs.Editor for .NET download page](https://releases.groupdocs.com/editor/net/) herunterladen.  
- Sample Document: Haben Sie ein Beispieldokument zum Bearbeiten bereit.

## Namespaces importieren
Zuerst importieren wir die notwendigen Namespaces, um sicherzustellen, dass unser Code reibungslos läuft. Dieser Schritt gibt uns Zugriff auf die Kernklassen von GroupDocs.Editor.

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Editor.Options;
```

## Schritt 1: Editor initialisieren
Die Klasse `Editor` ist der Einstiegspunkt für die Arbeit mit Dokumenten in GroupDocs.Editor. Sie verwaltet Ladevorgänge, Bearbeitungen und Speicheroperationen.  
Der erste Schritt besteht darin, eine `Editor`‑Instanz mit Ihrem Beispieldokument zu erstellen. Dadurch wird die Bearbeitungsumgebung eingerichtet.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```

## Schritt 2: Dokument bearbeiten
Das Objekt `EditableDocument` stellt die bearbeitbare Version der Datei dar und gibt interne Teile wie CSS, Bilder und HTML frei.  
Als Nächstes erhalten wir ein `EditableDocument`‑Objekt. Dieses Objekt ermöglicht es uns, mit dem internen CSS des Dokuments zu arbeiten.

```csharp
    using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
    {
```

## Schritt 3: Externe Präfixe festlegen
Definieren Sie die URL‑Präfixe für Bilder und Schriftarten. Diese Präfixe werden jedem Bild‑ und Schriftart‑Verweis im CSS vorangestellt.

```csharp
        string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
        string externalFontsPrefix = "http://www.mywebsite.com/fonts/id=";
```

## Schritt 4: CSS‑Inhalt mit den Präfixen extrahieren
`GetCssContent` gibt eine Sammlung von CSS‑Stylesheet‑Zeichenketten zurück, die bereits die von Ihnen angegebenen Präfix‑URLs enthalten.  
Rufen Sie `GetCssContent` auf und übergeben Sie die gerade definierten Präfixe. Die Methode gibt eine Liste von CSS‑Stylesheet‑Zeichenketten zurück, die bereits die präfixierten URLs enthalten.

```csharp
        List<string> stylesheets = document.GetCssContent(externalImagesPrefix, externalFontsPrefix);
```

## Schritt 5: Ergebnisse ausgeben
Geben Sie die Anzahl gefundener Stylesheets aus und zeigen Sie jedes Stylesheet an. Dies hilft Ihnen zu überprüfen, dass die Präfixe korrekt angewendet wurden.

```csharp
        Console.WriteLine("There are {0} stylesheets in the input document", stylesheets.Count);
        foreach (string css in stylesheets)
        {
            Console.WriteLine(css);
        }
    }
}
```

## Häufige Probleme und Lösungen
- **Keine Stylesheets zurückgegeben** – Stellen Sie sicher, dass das Quell‑Dokument tatsächlich CSS enthält (z. B. ein Word‑Dokument mit formatierten Tabellen oder eingebettetem HTML).  
- **Falsche URLs** – Überprüfen Sie, ob die Präfix‑Zeichenketten mit dem passenden Trennzeichen (`/` oder `=`) für Ihre Server‑Routing‑Logik enden.  
- **Leistungsbedenken** – Bei sehr großen Dokumenten sollten Sie die Verarbeitung der Stylesheets in Batches erwägen, um hohen Speicherverbrauch zu vermeiden.

## Häufig gestellte Fragen

**Q: Kann ich GroupDocs.Editor für .NET mit anderen Dokumentformaten verwenden?**  
A: Ja, GroupDocs.Editor für .NET unterstützt PDF, Word, Excel, PowerPoint und viele weitere Formate.

**Q: Gibt es eine kostenlose Testversion für GroupDocs.Editor für .NET?**  
A: Auf jeden Fall! Sie können Ihre kostenlose Testversion auf der [GroupDocs free trial page](https://releases.groupdocs.com/) starten.

**Q: Wie erhalte ich eine temporäre Lizenz für GroupDocs.Editor für .NET?**  
A: Sie können eine temporäre Lizenz von der [temporary license page](https://purchase.groupdocs.com/temporary-license/) erhalten.

**Q: Wo finde ich detaillierte Dokumentation für GroupDocs.Editor für .NET?**  
A: Detaillierte Dokumentation ist verfügbar auf der [GroupDocs.Editor for .NET documentation site](https://tutorials.groupdocs.com/editor/net/).

**Q: Welche Support‑Optionen stehen für GroupDocs.Editor für .NET zur Verfügung?**  
A: Sie können Unterstützung über das [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20) erhalten.

## Weitere häufig gestellte Fragen

**Q: Kann ich das Präfix nach dem Extrahieren des CSS ändern?**  
A: Ja. Rufen Sie `GetCssContent` erneut mit einem anderen Präfix‑String auf; die Methode verwendet stets die zur Laufzeit übergebenen Werte.

**Q: Funktioniert das mit passwortgeschützten Dokumenten?**  
A: Ja. Geben Sie das Passwort in `WordProcessingLoadOptions` an, wenn Sie die `Editor`‑Instanz erstellen.

**Q: Ist es möglich, das modifizierte CSS wieder im Dokument zu speichern?**  
A: GroupDocs.Editor bietet derzeit nur Lese‑Zugriff auf CSS. Um Änderungen zu übernehmen, müssten Sie das ursprüngliche Stylesheet über die zugrunde liegenden XML‑APIs des Dokuments ersetzen.

---

**Zuletzt aktualisiert:** 2026-09-26  
**Getestet mit:** GroupDocs.Editor 23.12 für .NET  
**Autor:** GroupDocs

## Verwandte Tutorials

- [Externe CSS aus Word‑Dokumenten mit GroupDocs.Editor .NET&#58; Ein umfassender Leitfaden](/editor/net/html-web-documents/extract-external-css-word-docs-groupdocs-editor-dotnet/)
- [HTML aus Word‑Dokumenten extrahieren & Präfix hinzufügen mit GroupDocs.Editor .NET](/editor/net/html-web-documents/groupdocs-editor-dotnet-extract-prefix-html-word-docs/)
- [Wie man HTML‑Inhalt in Word‑Dokumenten extrahiert und ändert mit GroupDocs.Editor .NET](/editor/net/html-web-documents/extract-modify-html-content-word-docs-groupdocs-editor-net/)