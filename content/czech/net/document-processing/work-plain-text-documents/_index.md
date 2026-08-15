---
date: 2026-08-10
description: Zjistěte, jak upravovat soubory prostého textu pomocí GroupDocs.Editor
  pro .NET. Průvodce zahrnuje načtení souboru txt, ořezání mezer, nastavení kódování
  textu a uložení výsledku.
keywords:
- edit plain text
- load txt file
- trim trailing spaces
- convert leading spaces
- set text encoding
lastmod: 2026-08-10
linktitle: Práce s dokumenty prostého textu
og_description: Zjistěte, jak upravovat soubory prostého textu pomocí GroupDocs.Editor
  pro .NET – načtěte soubor txt, ořízněte koncové mezery, převádějte úvodní mezery,
  nastavte kódování textu a uložte efektivně.
og_image_alt: Guide showing edit plain text workflow with GroupDocs.Editor for .NET
og_title: Upravujte dokumenty prostého textu pomocí GroupDocs.Editor pro .NET
schemas:
- author: GroupDocs
  dateModified: '2026-08-10'
  description: Learn how to edit plain text files using GroupDocs.Editor for .NET.
    The guide covers loading a txt file, trimming spaces, setting text encoding, and
    saving the result.
  headline: Edit plain text documents with GroupDocs.Editor for .NET
  type: TechArticle
- description: Learn how to edit plain text files using GroupDocs.Editor for .NET.
    The guide covers loading a txt file, trimming spaces, setting text encoding, and
    saving the result.
  name: Edit plain text documents with GroupDocs.Editor for .NET
  steps:
  - name: Get a path to the input TXT file
    text: First, decide whether you’ll work with a physical file path or a memory
      stream. Using a path is the most straightforward approach for local development.
  - name: Create an Editor instance
    text: '`Editor` is the main class that loads a document and provides editing capabilities.'
  - name: Create TXT editing options
    text: '`TxtEditOptions` configures how plain‑text files are parsed and edited,
      allowing you to set encoding and space‑handling rules.'
  - name: Create an EditableDocument instance
    text: '`EditableDocument` represents the in‑memory version of the loaded document,
      including its text and any associated resources.'
  - name: Edit the document content
    text: Retrieve the original text, apply any string operations you need (e.g.,
      replace, trim, change case), and store the result back into the `EditableDocument`.
  - name: Create an EditableDocument with updated content
    text: After you’ve transformed the text, instantiate a new `EditableDocument`
      that contains the edited string and the original resource collection.
  - name: Create WordProcessing save options
    text: '`WordProcessingSaveOptions` defines settings for saving the document in
      a Word‑compatible format such as DOCX or DOCM.'
  - name: Create TXT saving options
    text: '`TxtSaveOptions` specifies how the edited plain‑text file should be written,
      including encoding, line‑ending preservation, and table layout handling.'
  - name: Prepare output paths
    text: Derive the output directory from the input file path, then build the full
      filenames for the DOCX and TXT results.
  - name: Save the edited document
    text: Finally, call `editor.Save` twice—once with the WordProcessing options and
      once with the TXT options—to produce both formats in a single operation.
  type: HowTo
- questions:
  - answer: The library supports 50+ formats, including DOCX, TXT, HTML, PDF, and
      markdown, allowing you to edit and convert between them seamlessly.
    question: What file formats does GroupDocs.Editor for .NET support?
  - answer: Download the trial from the [releases page](https://releases.groupdocs.com/).
    question: How can I get a free trial of GroupDocs.Editor for .NET?
  - answer: Yes, temporary licenses are available through the [GroupDocs purchase
      page](https://purchase.groupdocs.com/temporary-license/).
    question: Can I purchase a temporary license for testing?
  - answer: The official support forum is the best place – visit the [GroupDocs.Editor
      support forum](https://forum.groupdocs.com/c/editor/20).
    question: Where can I find support if I run into issues?
  - answer: Absolutely. The full reference is on the [GroupDocs.Editor documentation
      page](https://tutorials.groupdocs.com/editor/net/).
    question: Is there detailed documentation for advanced scenarios?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
tags:
- edit plain text
- GroupDocs.Editor
- C# document processing
- plain text editing
- txt file handling
title: Upravujte dokumenty prostého textu pomocí GroupDocs.Editor pro .NET
type: docs
url: /cs/net/document-processing/work-plain-text-documents/
weight: 15
---

# Upravit dokumenty prostého textu pomocí GroupDocs.Editor pro .NET

## Úvod
Pokud potřebujete **edit plain text** rychle a spolehlivě v .NET aplikaci, GroupDocs.Editor pro .NET je nástroj, který odlehčí těžkou práci. Toto API podporuje více než 30 formátů dokumentů, dokáže zpracovat soubory až do 500 MB a umožňuje manipulovat s textem, aniž byste načítali celý soubor do paměti. V tomto tutoriálu se naučíte, jak načíst txt soubor, oříznout koncové mezery, převést úvodní mezery, nastavit správné kódování a nakonec uložit upravený obsah zpět na disk. Připraveni na praktické cvičení? Pojďme na to!

## Rychlé odpovědi
- **Jaký je první krok při úpravě txt souboru?** Načtěte soubor pomocí `Editor` s použitím cesty nebo proudu, který máte.  
- **Mohu během úprav změnit kódování souboru?** Ano – `TxtSaveOptions` vám umožní specifikovat UTF‑8, UTF‑16 nebo libovolné vlastní kódování.  
- **Jak odstraním nadbytečné mezery na konci každého řádku?** Získejte text, zavolejte `TrimEnd()` na každém řádku a zapište jej zpět.  
- **Je GroupDocs.Editor zdarma k vyzkoušení?** Plně funkční 30‑denní zkušební verze je k dispozici na stránce vydání.  
- **Které verze .NET jsou podporovány?** .NET Framework 4.6+, .NET Core 3.1+ a .NET 5/6/7.

## Co je úprava prostého textu?
**Edit plain text** znamená programově měnit znaky uvnitř jednoduchého `.txt` souboru – přidávat, odstraňovat nebo přeformátovávat text – při zachování původního kódování souboru a stylu konců řádků. Může zahrnovat úkoly jako ořezávání bílých znaků, normalizaci konců řádků, aktualizaci konfiguračních hodnot nebo vkládání generovaného obsahu. Operace by měla zachovat čitelnost souboru v jakémkoli standardním textovém editoru a udržet existující metadata, jako jsou BOM značky.

## Proč používat GroupDocs.Editor pro úpravu prostého textu?
GroupDocs.Editor zpracovává soubory ve streamovacím režimu, což znamená, že může upravit 300 MB log soubor s využitím méně než 50 MB RAM. Knihovna podporuje **50+ vstupních a výstupních formátů**, automaticky detekuje styly konců řádků (CR, LF, CRLF) a poskytuje vestavěné možnosti pro **ořezání koncových mezer** a **převod úvodních mezer** bez nutnosti psát vlastní parsery.

## Požadavky
- **.NET vývojové prostředí** – Visual Studio 2022 nebo VS Code s rozšířením C#.  
- **GroupDocs.Editor pro .NET** – stáhněte ze stránky [GroupDocs.Editor for .NET](https://releases.groupdocs.com/editor/net/) releases.  
- **Základní znalost C#** – měli byste být zdatní v práci se soubory (I/O) a manipulaci s řetězci.  
- **Textový editor (volitelně)** – pro prohlížení zdrojových souborů; doporučujeme VS Code.  
- Pro podrobné použití viz [dokumentaci](https://tutorials.groupdocs.com/editor/net/).  
- Můžete také procházet obecnou [stránku vydání](https://releases.groupdocs.com/).

## Jak upravit prostý text krok za krokem
Načtěte soubor, upravte jeho obsah a uložte jej zpět – vše v méně než deseti řádcích kódu. Následující sekce vás provede každým krokem s jasnými vysvětleními.

### Krok 1: Získat cestu k vstupnímu TXT souboru
Nejprve se rozhodněte, zda budete pracovat s fyzickou cestou k souboru nebo s paměťovým proudem. Použití cesty je nejjednodušší přístup pro lokální vývoj.

```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

### Krok 2: Vytvořit instanci Editoru
`Editor` je hlavní třída, která načítá dokument a poskytuje možnosti úprav.

```csharp
string inputFilePath = "YourSampleDocument.txt";
```

### Krok 3: Vytvořit možnosti úpravy TXT
`TxtEditOptions` konfiguruje, jak jsou prosté textové soubory parsovány a upravovány, což vám umožní nastavit kódování a pravidla pro zacházení s mezerami.

```csharp
using (Editor editor = new Editor(inputFilePath))
{
```

### Krok 4: Vytvořit instanci EditableDocument
`EditableDocument` představuje verzi načteného dokumentu v paměti, včetně jeho textu a všech souvisejících zdrojů.

```csharp
    TextEditOptions editOptions = new TextEditOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        RecognizeLists = true,
        LeadingSpaces = TextLeadingSpacesOptions.ConvertToIndent,
        TrailingSpaces = TextTrailingSpacesOptions.Trim
    };
```

### Krok 5: Upravit obsah dokumentu
Získejte původní text, aplikujte potřebné operace s řetězci (např. replace, trim, změna velikosti písmen) a výsledek uložte zpět do `EditableDocument`.

```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```

### Krok 6: Vytvořit EditableDocument s aktualizovaným obsahem
Po transformaci textu vytvořte novou instanci `EditableDocument`, která obsahuje upravený řetězec a původní kolekci zdrojů.

```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("text", "EDITED text");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```

### Krok 7: Vytvořit nastavení uložení WordProcessing
`WordProcessingSaveOptions` definuje nastavení pro uložení dokumentu ve formátu kompatibilním s Wordem, jako je DOCX nebo DOCM.

```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```

### Krok 8: Vytvořit nastavení uložení TXT
`TxtSaveOptions` určuje, jak má být upravený prostý textový soubor zapsán, včetně kódování, zachování konců řádků a zpracování rozvržení tabulek.

```csharp
    WordProcessingSaveOptions wordSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm)
    {
        Locale = System.Globalization.CultureInfo.GetCultureInfo("en-GB")
    };
```

### Krok 9: Připravit výstupní cesty
Odvoďte výstupní adresář ze vstupní cesty souboru a poté vytvořte úplná jména souborů pro výsledky DOCX a TXT.

```csharp
    TextSaveOptions txtSaveOptions = new TextSaveOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        PreserveTableLayout = true
    };
```

### Krok 10: Uložit upravený dokument
Nakonec zavolejte `editor.Save` dvakrát – jednou s nastavením WordProcessing a podruhé s nastavením TXT, abyste vytvořili oba formáty v jedné operaci.

```csharp
    string outputWordPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".docm");
    string outputTxtPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".txt");
```

## Časté problémy a řešení
- **Koncové mezery zůstávají po úpravě** – ujistěte se, že `TxtEditOptions.TrimTrailingSpaces` je nastaven na `true` před načtením dokumentu.  
- **Nesprávné kódování v uloženém souboru** – ověřte, že `TxtSaveOptions.Encoding` odpovídá požadované znakové sadě (např. `Encoding.UTF8`).  
- **Velké soubory způsobují OutOfMemoryException** – použijte streaming API (`Editor.Load(Stream)`) místo načítání ze souborové cesty, aby se udržela nízká spotřeba paměti.  

## Často kladené otázky

**Q: Jaké formáty souborů GroupDocs.Editor pro .NET podporuje?**  
A: Knihovna podporuje více než 50 formátů, včetně DOCX, TXT, HTML, PDF a markdown, což vám umožní je snadno upravovat a převádět mezi nimi.

**Q: Jak získat bezplatnou zkušební verzi GroupDocs.Editor pro .NET?**  
A: Stáhněte zkušební verzi ze [stránky vydání](https://releases.groupdocs.com/).

**Q: Mohu zakoupit dočasnou licenci pro testování?**  
A: Ano, dočasné licence jsou k dispozici na [stránce nákupu GroupDocs](https://purchase.groupdocs.com/temporary-license/).

**Q: Kde mohu najít podporu, pokud narazím na problémy?**  
A: Oficiální fórum podpory je nejlepší místo – navštivte [fórum podpory GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).

**Q: Existuje podrobná dokumentace pro pokročilé scénáře?**  
A: Ano. Kompletní reference je na [stránce dokumentace GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/).

## Závěr
Nyní ovládáte, jak **edit plain text** soubory pomocí GroupDocs.Editor pro .NET – načíst txt soubor, oříznout mezery, převést úvodní mezery, nastavit správné kódování a uložit výsledek jak ve formátu TXT, tak DOCX. Tato schopnost vám umožní automatizovat čištění log souborů, generovat konfigurační soubory za běhu nebo vytvářet vlastní textové zpracovatelské pipeline bez nutnosti vymýšlet vše od začátku. Prozkoumejte další funkce, jako je dávkové zpracování a konverze dokumentů, na oficiální dokumentaci.

---

**Poslední aktualizace:** 2026-08-10  
**Testováno s:** GroupDocs.Editor 23.11 for .NET  
**Autor:** GroupDocs  

```csharp
    editor.Save(afterEdit, outputWordPath, wordSaveOptions);
    editor.Save(afterEdit, outputTxtPath, txtSaveOptions);
}
System.Console.WriteLine("Document editing process completed successfully!");
```

## Související tutoriály

- [Tutoriály načítání dokumentů s GroupDocs.Editor pro .NET](/editor/net/document-loading/)
- [Tutoriály ukládání a exportu dokumentů pro GroupDocs.Editor .NET](/editor/net/document-saving/)
- [Tutoriály úpravy prostého textu a DSV dokumentů pro GroupDocs.Editor .NET](/editor/net/plain-text-dsv-documents/)