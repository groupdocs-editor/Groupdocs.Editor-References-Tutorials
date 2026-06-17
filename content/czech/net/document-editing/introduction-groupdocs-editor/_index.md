---
date: 2026-04-11
description: Naučte se programově upravovat dokument Word pomocí GroupDocs.Editor
  pro .NET a převádět Word do RTF v tomto podrobném průvodci krok za krokem.
keywords:
- programmatically edit word document
- convert pdf to editable
- replace text in document
- convert word to rtf
- save document to stream
linktitle: Programově upravovat dokument Word pomocí GroupDocs.Editor pro .NET
second_title: GroupDocs.Editor .NET API
title: Programově editovat dokument Word pomocí GroupDocs.Editor pro .NET
type: docs
url: /cs/net/document-editing/introduction-groupdocs-editor/
weight: 12
---

# Programové úpravy Word dokumentu pomocí GroupDocs.Editor pro .NET

Pokud jste .NET vývojář, který potřebuje **programově upravovat Word dokument** – ať už chcete nahradit text, převést formáty nebo vložit výsledek do proudu – GroupDocs.Editor pro .NET je robustní, snadno použitelní knihovna, která úkol splní. V tomto tutoriálu projdeme reálným příkladem, který zahrnuje načtení souboru DOCX, úpravu jeho obsahu, převod výsledku do RTF a uložení buď na disk, nebo do paměťového proudu.

## Rychlé odpovědi
- **Co mohu upravovat?** Word, PDF, HTML, RTF a mnoho dalších formátů.  
- **Mohu nahradit text?** Ano – použijte jednoduchou náhradu řetězce nebo pokročilejší manipulaci s DOM.  
- **Jak převést PDF na editovatelné?** Načtěte PDF pomocí `Editor` a upravte vygenerované HTML.  
- **Jaký je nejjednodušší způsob uložení do proudu?** Použijte `editor.Save(editableDoc, stream, options)`.  
- **Potřebuji licenci?** Pro produkční použití je vyžadována dočasná nebo plná licence.

## Co je programové úpravy Word dokumentu?
Programové úpravy Word dokumentu znamenají použití kódu – místo uživatelského rozhraní – k otevření souboru, změně jeho obsahu (text, obrázky, styly) a zápisu upravené verze zpět do úložiště. Tento přístup umožňuje automatizované reportování, hromadné aktualizace dokumentů a generování vlastního obsahu.

## Proč používat GroupDocs.Editor pro .NET?
- **Flexibilita formátů:** Načtěte DOCX, PDF, HTML, RTF atd. a uložte do libovolného podporovaného formátu.  
- **Bez závislosti na Office:** Funguje bez nainstalovaného Microsoft Office na serveru.  
- **Přátelské ke streamům:** Ideální pro cloudové scénáře, kde čtete/zapisujete z proudu místo souborového systému.  
- **Bohaté API:** Přístup k obrázkům, fontům, CSS a dalším zdrojům pro plnohodnotné úpravy.

## Požadavky
Než se ponoříme do implementace, ujistěte se, že máte:

- Visual Studio 2017 nebo novější.  
- .NET Framework 4.6.1 nebo novější.  
- GroupDocs.Editor pro .NET – můžete jej [stáhnout](https://releases.groupdocs.com/editor/net/) ze stránky.  
- Platnou licenci nebo [dočasnou licenci](https://purchase.groupdocs.com/temporary-license/) od GroupDocs.

## Importovat jmenné prostory
Pro zahájení používání GroupDocs.Editor pro .NET importujte požadované jmenné prostory:

```csharp
using System;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```

V následujících sekcích rozdělíme pracovní postup na malé kroky, abyste mohli snadno sledovat.

## Krok 1: Získat cestu k vstupnímu souboru
Zadejte umístění Word souboru, který chcete upravit. V tomto příkladu předpokládáme DOCX pojmenovaný **Your Sample Document.docx**.

```csharp
string inputFilePath = "Your Sample Document.docx";
```

## Krok 2: Vytvořit objekt Editor
Vytvořte instanci `Editor` předáním vstupní cesty. Tím se načte dokument a připraví k úpravám.

```csharp
using (GroupDocs.Editor.Editor editor = new Editor(inputFilePath))
{
    // Subsequent steps will be nested inside this block
}
```

## Krok 3: Otevřít dokument pro úpravy
Získejte `EditableDocument`, který vám poskytne přístup k HTML reprezentaci dokumentu a jeho zdrojům.

```csharp
EditableDocument beforeEdit = editor.Edit();
```

## Krok 4: Získat obsah dokumentu a zdroje
Můžete získat surové HTML, obrázky, fonty a CSS. To je užitečné, když potřebujete přímo manipulovat s markupem.

```csharp
string content = beforeEdit.GetContent();
var images = beforeEdit.Images;
var fonts = beforeEdit.Fonts;
var stylesheets = beforeEdit.Css;
```

### Krok 4.1: Získat dokument jako jediný Base64‑kódovaný řetězec
Pokud dáváte přednost jedinému řetězci, který obsahuje všechny vložené zdroje, zavolejte `GetEmbeddedHtml()`.

```csharp
string allEmbeddedInsideString = beforeEdit.GetEmbeddedHtml();
```

### Krok 4.2: Upravit obsah
Nahraďme slovo **Subtitle** slovem **Edited subtitle** pro demonstraci jednoduché náhrady textu.

```csharp
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
```

## Krok 5: Vytvořit novou instanci EditableDocument
Po úpravě markupu jej zabalte zpět do objektu `EditableDocument`.

```csharp
EditableDocument afterEdit = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```

## Krok 6: Uložit upravený dokument
Uložíme výsledek jako RTF soubor, ukážeme jak cestu v souborovém systému, tak možnost paměťového proudu.

### Krok 6.1: Připravit výstupní cestu
Definujte, kam má být RTF zapsán.

```csharp
string outputPath = Path.Combine("Output Directory Path", Path.GetFileNameWithoutExtension(inputFilePath) + ".rtf");
```

### Krok 6.2: Připravit možnosti uložení
Vyberte formát RTF pomocí `WordProcessingSaveOptions`.

```csharp
Options.WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
```

### Krok 6.3: Uložit na cestu
Zapište upravený dokument do souborového systému.

```csharp
editor.Save(afterEdit, outputPath, saveOptions);
```

### Krok 6.4: Uložit do proudu
Pokud potřebujete výsledek v paměti (např. pro nahrání do cloudového úložiště), použijte `MemoryStream`.

```csharp
using (MemoryStream ms = new MemoryStream())
{
    editor.Save(afterEdit, ms, saveOptions);
}
```

## Krok 7: Uvolnit instance Editor a EditableDocument
Uvolněte prostředky okamžitě, aby nedocházelo k únikům paměti.

```csharp
beforeEdit.Dispose();
afterEdit.Dispose();
editor.Dispose();
```

## Běžné případy použití a tipy
- **Převést PDF na editovatelné:** Načtěte PDF pomocí `Editor`, upravte vygenerované HTML a poté uložte zpět do PDF nebo jiného formátu.  
- **Nahradit text v dokumentu:** Použijte `string.Replace` pro jednoduché případy nebo manipulujte s DOM pro složitější scénáře.  
- **Převést Word na RTF:** Jak bylo ukázáno výše, nastavte `WordProcessingFormats.Rtf` v možnostech uložení.  
- **Uložit dokument do proudu:** Ideální pro webová API, která vracejí soubory přímo klientovi.  
- **Načíst dokument pro úpravy:** Vždy zabalte `Editor` do bloku `using`, aby bylo zajištěno správné uvolnění.

## Často kladené otázky

**Q: Mohu upravovat PDF soubory pomocí GroupDocs.Editor pro .NET?**  
A: Ano, GroupDocs.Editor podporuje úpravy PDF souborů převodem na mezilehlou HTML reprezentaci.

**Q: Jak získám dočasnou licenci pro GroupDocs.Editor pro .NET?**  
A: Dočasnou licenci můžete získat na [webu GroupDocs](https://purchase.groupdocs.com/temporary-license/).

**Q: Jaké souborové formáty jsou podporovány GroupDocs.Editor pro .NET?**  
A: Jsou podporovány DOCX, PDF, HTML, RTF a mnoho dalších formátů.

**Q: Je možné integrovat GroupDocs.Editor s cloudovým úložištěm?**  
A: Rozhodně – můžete číst/zapisovat proudy z Azure Blob, Amazon S3, Google Cloud Storage atd.

**Q: Kde mohu najít dokumentaci pro GroupDocs.Editor pro .NET?**  
A: Dokumentace je dostupná [zde](https://tutorials.groupdocs.com/editor/net/).

---

**Poslední aktualizace:** 2026-04-11  
**Testováno s:** GroupDocs.Editor 23.12 pro .NET  
**Autor:** GroupDocs