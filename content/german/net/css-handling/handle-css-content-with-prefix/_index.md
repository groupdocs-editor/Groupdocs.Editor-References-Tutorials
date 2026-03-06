---
date: 2026-03-06
description: Erfahren Sie, wie Sie CSS‑Inhalte mit Präfix verarbeiten und CSS‑Inhalte
  mit GroupDocs.Editor für .NET extrahieren, in diesem detaillierten Schritt‑für‑Schritt‑Tutorial.
linktitle: Handle CSS Content with Prefix
second_title: GroupDocs.Editor .NET API
title: CSS-Inhalt mit Präfix verarbeiten
type: docs
url: /de/net/css-handling/handle-css-content-with-prefix/
weight: 11
---

# CSS-Inhalt mit Präfix verarbeiten

In diesem Tutorial erfahren Sie **wie man css prefix handhabt**, wenn Sie mit Stylesheets innerhalb eines Dokuments mithilfe von GroupDocs.Editor für .NET arbeiten. Egal, ob Sie einer URL ein Präfix für Bilder, Schriftarten oder andere externe Ressourcen voranstellen müssen – die nachfolgenden Schritte zeigen Ihnen genau, **wie man css prefix handhabt** und auch, **wie man css content extrahiert** für weitere Verarbeitung.

## Schnelle Antworten
- **Was bedeutet „handle css prefix“?** Hinzufügen eines benutzerdefinierten URL‑Präfixes zu externen Ressourcen, die in CSS referenziert werden.  
- **Welche API‑Methode gibt CSS‑Stile zurück?** `EditableDocument.GetCssContent(...)`.  
- **Benötige ich eine Lizenz?** Eine Testlizenz ist verfügbar; für den Produktionseinsatz ist eine kommerzielle Lizenz erforderlich.  
- **Welche .NET‑Versionen werden unterstützt?** .NET Framework 4.5+ und .NET Core/5/6.  
- **Kann ich das Präfix zur Laufzeit ändern?** Ja – übergeben Sie einfach einen anderen String an `GetCssContent`.

## Was ist **handle css prefix**?
Ein Präfix auf CSS‑Ressourcen anzuwenden, überschreibt die Pfade von Bildern, Schriftarten oder anderen Assets, sodass sie auf einen Ort zeigen, den Sie kontrollieren (z. B. ein CDN oder einen gesicherten Server). Das ist besonders nützlich, wenn Sie ein Dokument exportieren und alle externen Verweise von einer Web‑Anwendung aus erreichbar sein müssen.

## Warum GroupDocs.Editor zum **extract css content** verwenden?
GroupDocs.Editor kann das ursprüngliche CSS, das in Word‑Processing‑Dokumenten eingebettet ist, auslesen, Ihnen die rohen Stylesheet‑Strings bereitstellen und Ihnen ermöglichen, diese vor dem Rendern oder Speichern zu manipulieren. Das eliminiert manuelles Parsen und stellt sicher, dass das extrahierte CSS der internen Darstellung des Dokuments entspricht.

## Voraussetzungen
Bevor wir beginnen, stellen Sie sicher, dass Sie die folgenden Voraussetzungen erfüllt haben:
- Visual Studio: Sie benötigen eine funktionierende Installation von Visual Studio.  
- .NET Framework: Stellen Sie sicher, dass das .NET Framework installiert ist.  
- GroupDocs.Editor für .NET: Sie können es [hier](https://releases.groupdocs.com/editor/net/) herunterladen.  
- Beispiel‑Dokument: Haben Sie ein Beispiel‑Dokument zum Bearbeiten bereit.

## Namespaces importieren
Zuerst importieren wir die notwendigen Namespaces, damit unser Code reibungslos läuft. Dieser Schritt gibt uns Zugriff auf die Kernklassen von GroupDocs.Editor.

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Editor.Options;
```

## Schritt 1: Editor initialisieren
Der erste Schritt besteht darin, eine `Editor`‑Instanz mit Ihrem Beispiel‑Dokument zu erstellen. Dadurch wird die Bearbeitungsumgebung eingerichtet.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```

## Schritt 2: Dokument bearbeiten
Als Nächstes erhalten wir ein `EditableDocument`‑Objekt. Dieses Objekt repräsentiert die bearbeitbare Version der Datei und ermöglicht den Zugriff auf deren interne Teile.

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

## Schritt 4: **Extract CSS content** mit den Präfixen
Rufen Sie `GetCssContent` auf und übergeben Sie die gerade definierten Präfixe. Die Methode liefert eine Liste von CSS‑Stylesheet‑Strings, die bereits die vorangestellten URLs enthalten.

```csharp
        List<string> stylesheets = document.GetCssContent(externalImagesPrefix, externalFontsPrefix);
```

## Schritt 5: Ergebnisse ausgeben
Geben Sie die Anzahl gefundener Stylesheets aus und zeigen Sie jedes Stylesheet an. So können Sie überprüfen, dass die Präfixe korrekt angewendet wurden.

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
- **Falsche URLs** – Überprüfen Sie, dass die Präfix‑Strings mit dem passenden Trennzeichen (`/` oder `=`) für Ihre Server‑Routing‑Logik enden.  
- **Performance‑Bedenken** – Bei sehr großen Dokumenten sollten Sie die Stylesheets in Batches verarbeiten, um hohen Speicherverbrauch zu vermeiden.

## Fazit
Der Umgang mit CSS‑Inhalt und einem Präfix mithilfe von GroupDocs.Editor für .NET ist unkompliziert und leistungsfähig. Durch Befolgen dieser Schritte können Sie **css prefix handhaben**, das rohe CSS via **extract css content** abrufen und externe Ressourcen nahtlos in Ihren Web‑Workflow integrieren. Erkunden Sie weitere GroupDocs.Editor‑Funktionen wie HTML‑Konvertierung, Bild‑Extraktion und Dokument‑Zusammenführung, um noch mehr Nutzen aus der API zu ziehen.

## FAQ
### Kann ich GroupDocs.Editor für .NET mit anderen Dokumentformaten verwenden?
Ja, GroupDocs.Editor für .NET unterstützt verschiedene Dokumentformate, darunter PDF, Word, Excel und mehr.

### Ist eine kostenlose Testversion für GroupDocs.Editor für .NET verfügbar?
Absolut! Sie können Ihre kostenlose Testversion [hier](https://releases.groupdocs.com/) starten.

### Wie erhalte ich eine temporäre Lizenz für GroupDocs.Editor für .NET?
Sie können eine temporäre Lizenz [hier](https://purchase.groupdocs.com/temporary-license/) erhalten.

### Wo finde ich detaillierte Dokumentation für GroupDocs.Editor für .NET?
Detaillierte Dokumentation ist [hier](https://tutorials.groupdocs.com/editor/net/) verfügbar.

### Welche Support‑Optionen gibt es für GroupDocs.Editor für .NET?
Support erhalten Sie [hier](https://forum.groupdocs.com/c/editor/20).

## Weitere häufig gestellte Fragen

**Q: Kann ich das Präfix ändern, nachdem ich das CSS extrahiert habe?**  
**A:** Ja. Rufen Sie `GetCssContent` erneut mit einem anderen Präfix‑String auf; die Methode verwendet stets die zur Laufzeit übergebenen Werte.

**Q: Funktioniert das mit passwortgeschützten Dokumenten?**  
**A:** Ja. Geben Sie das Passwort in `WordProcessingLoadOptions` an, wenn Sie die `Editor`‑Instanz erstellen.

**Q: Ist es möglich, das modifizierte CSS wieder im Dokument zu speichern?**  
**A:** GroupDocs.Editor bietet derzeit nur Lesezugriff auf CSS. Um Änderungen zu persistieren, müssten Sie das ursprüngliche Stylesheet über die zugrunde liegenden XML‑APIs des Dokuments ersetzen.

---

**Zuletzt aktualisiert:** 2026-03-06  
**Getestet mit:** GroupDocs.Editor 23.12 für .NET  
**Autor:** GroupDocs