---
date: 2026-09-26
description: Naučte se, jak zacházet s css prefixem a extrahovat css content pomocí
  GroupDocs.Editor for .NET v tomto podrobném step‑by‑step tutoriálu.
keywords:
- handle css prefix
- extract css content
- edit document css
- prepend url to css
lastmod: 2026-09-26
linktitle: Zpracování CSS obsahu s prefixem
og_description: Objevte, jak zacházet s css prefixem a extrahovat css content s GroupDocs.Editor
  for .NET. Postupujte podle step‑by‑step průvodce, který přidá URLs před CSS resources
  a načte stylesheets.
og_image_alt: Developer guide showing css prefix handling with GroupDocs.Editor for
  .NET
og_title: Jak zacházet s css prefixem v GroupDocs.Editor for .NET
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
title: Jak zacházet s css prefixem v GroupDocs.Editor for .NET
type: docs
url: /cs/net/css-handling/handle-css-content-with-prefix/
weight: 11
---

# Jak zacházet s prefixem CSS v GroupDocs.Editor pro .NET

V tomto tutoriálu se naučíte **jak zacházet s prefixem CSS** při práci s listinami stylů uvnitř dokumentu pomocí GroupDocs.Editor pro .NET. Ať už potřebujete přidat URL před obrázky, fonty nebo jakýkoli externí zdroj, níže uvedené kroky vám přesně ukážou, jak **zacházet s prefixem CSS** a také jak **extrahovat obsah CSS** pro další zpracování. Na konci průvodce budete schopni přepsat cesty k zdrojům, získat surové řetězce CSS a integrovat je do vašeho webového workflow s jistotou.

## Rychlé odpovědi
- **Co znamená „zacházet s prefixem CSS“?** Přidání vlastního URL prefixu k externím zdrojům odkazovaným v CSS.  
- **Která metoda API vrací CSS styly?** `EditableDocument.GetCssContent(...)`.  
- **Potřebuji licenci?** K dispozici je zkušební licence; pro produkci je vyžadována komerční licence.  
- **Jaké verze .NET jsou podporovány?** .NET Framework 4.5+ a .NET Core/5/6.  
- **Mohu změnit prefix za běhu?** Ano – stačí předat jiný řetězec metodě `GetCssContent`.

## Co je zacházení s prefixem CSS?
Termín se vztahuje k přepisování URL obrázků, fontů nebo jakéhokoli externího assetu uvnitř souboru CSS tak, aby ukazovaly na místo, které ovládáte, například CDN nebo zabezpečený server. Přidáním konzistentního základního URL zaručíte, že každý zdroj se načte správně, když je dokument vykreslen v prohlížeči nebo webovém prohlížeči.

## Proč použít GroupDocs.Editor k extrahování obsahu CSS?
GroupDocs.Editor dokáže číst původní CSS vložené do dokumentů WordProcessing, vrátit surové řetězce stylů a umožnit vám s nimi manipulovat před vykreslením nebo uložením. Tím se eliminuje ruční parsování, zaručuje věrnost interní reprezentaci dokumentu a podporuje **více než 30 formátů souborů** při zpracování souborů až do **500 MB** bez načítání celého souboru do paměti.

## Předpoklady
Before we get started, make sure you have the following prerequisites in place:
- Visual Studio: Budete potřebovat funkční instalaci Visual Studio.  
- .NET Framework: Ujistěte se, že máte nainstalovaný .NET Framework.  
- GroupDocs.Editor for .NET: Můžete si jej stáhnout ze [stránky pro stažení GroupDocs.Editor for .NET](https://releases.groupdocs.com/editor/net/).  
- Sample Document: Mějte připravený ukázkový dokument k úpravě.

## Importovat jmenné prostory
First, let’s import the necessary namespaces to ensure our code runs smoothly. This step gives us access to the core classes of GroupDocs.Editor.

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Editor.Options;
```

## Krok 1: Inicializovat Editor
The `Editor` class is the entry point for working with documents in GroupDocs.Editor. It manages loading, editing, and saving operations.  
The first step involves creating an `Editor` instance with your sample document. This sets up the editing environment.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```

## Krok 2: Upravit dokument
The `EditableDocument` object represents the editable version of the file and exposes its internal parts, such as CSS, images, and HTML.  
Next, we obtain an `EditableDocument` object. This object allows us to work with the document’s internal CSS.

```csharp
    using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
    {
```

## Krok 3: Nastavit externí prefixy
Define the URL prefixes for images and fonts. These prefixes will be prepended to every image and font reference found in the CSS.

```csharp
        string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
        string externalFontsPrefix = "http://www.mywebsite.com/fonts/id=";
```

## Krok 4: Extrahovat obsah CSS s prefixy
`GetCssContent` vrací kolekci řetězců CSS stylových listů, které již obsahují vámi zadané prefixované URL.  
Zavolejte `GetCssContent` a předávejte prefixy, které jste právě definovali. Metoda vrátí seznam řetězců CSS stylových listů, které již obsahují prefixované URL.

```csharp
        List<string> stylesheets = document.GetCssContent(externalImagesPrefix, externalFontsPrefix);
```

## Krok 5: Výstup výsledků
Print the number of stylesheets found and display each stylesheet. This helps you verify that the prefixes were applied correctly.

```csharp
        Console.WriteLine("There are {0} stylesheets in the input document", stylesheets.Count);
        foreach (string css in stylesheets)
        {
            Console.WriteLine(css);
        }
    }
}
```

## Časté problémy a řešení
- **Nebyly vráceny žádné stylové listy** – Ujistěte se, že zdrojový dokument skutečně obsahuje CSS (např. Word dokument s formátovanými tabulkami nebo vloženým HTML).  
- **Nesprávné URL** – Dvakrát zkontrolujte, že řetězce prefixů končí vhodným oddělovačem (`/` nebo `=`) pro směrování na vašem serveru.  
- **Obavy o výkon** – U velmi velkých dokumentů zvažte zpracování stylových listů po dávkách, aby nedošlo k vysokému využití paměti.

## Často kladené otázky

**Q: Mohu použít GroupDocs.Editor pro .NET s jinými formáty dokumentů?**  
A: Ano, GroupDocs.Editor pro .NET podporuje PDF, Word, Excel, PowerPoint a mnoho dalších formátů.

**Q: Je k dispozici bezplatná zkušební verze pro GroupDocs.Editor pro .NET?**  
A: Rozhodně! Můžete zahájit svou bezplatnou zkušební verzi na [stránce s bezplatnou zkušební verzí GroupDocs](https://releases.groupdocs.com/).

**Q: Jak získám dočasnou licenci pro GroupDocs.Editor pro .NET?**  
A: Dočasnou licenci můžete získat na [stránce s dočasnou licencí](https://purchase.groupdocs.com/temporary-license/).

**Q: Kde najdu podrobnou dokumentaci pro GroupDocs.Editor pro .NET?**  
A: Podrobná dokumentace je k dispozici na [webu s dokumentací GroupDocs.Editor pro .NET](https://tutorials.groupdocs.com/editor/net/).

**Q: Jaké možnosti podpory jsou k dispozici pro GroupDocs.Editor pro .NET?**  
A: Podporu můžete získat prostřednictvím [fóra podpory GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).

## Další často kladené otázky

**Q: Mohu změnit prefix po extrahování CSS?**  
A: Ano. Znovu zavolejte `GetCssContent` s jiným řetězcem prefixu; metoda vždy použije hodnoty, které předáte za běhu.

**Q: Funguje to s dokumenty chráněnými heslem?**  
A: Ano. Zadejte heslo v `WordProcessingLoadOptions` při vytváření instance `Editor`.

**Q: Je možné uložit upravené CSS zpět do dokumentu?**  
A: GroupDocs.Editor v současnosti poskytuje pouze přístup pro čtení k CSS. Pro zachování změn byste museli nahradit původní stylový list pomocí podkladových XML API dokumentu.

---

**Poslední aktualizace:** 2026-09-26  
**Testováno s:** GroupDocs.Editor 23.12 pro .NET  
**Autor:** GroupDocs

## Související tutoriály

- [Extrahovat externí CSS z Word dokumentů pomocí GroupDocs.Editor .NET&#58; Komplexní průvodce](/editor/net/html-web-documents/extract-external-css-word-docs-groupdocs-editor-dotnet/)
- [Extrahovat a přidat prefix HTML z Word dokumentů pomocí GroupDocs.Editor .NET](/editor/net/html-web-documents/groupdocs-editor-dotnet-extract-prefix-html-word-docs/)
- [Jak extrahovat a upravit HTML obsah ve Word dokumentech pomocí GroupDocs.Editor .NET](/editor/net/html-web-documents/extract-modify-html-content-word-docs-groupdocs-editor-net/)