---
date: 2026-05-12
description: Naučte se, jak extrahovat písma a další HTML zdroje z dokumentů pomocí
  GroupDocs.Editor pro .NET. Průvodce krok za krokem pro vývojáře .NET.
keywords:
- how to extract fonts
- GroupDocs.Editor .NET
- extract HTML resources
linktitle: Uložit HTML zdroje do složky
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
title: Jak extrahovat písma a uložit HTML zdroje do složky
type: docs
url: /cs/net/document-editing/save-html-resources-to-folder/
weight: 13
---

# Jak extrahovat písma a uložit HTML zdroje do složky

## Úvod
GroupDocs.Editor pro .NET vám umožňuje **how to extract fonts** a další prostředky z dokumentu při jeho převodu do HTML. V několika řádcích C# můžete vytáhnout obrázky, stylové listy a soubory písem a uložit je do složky dle vašeho výběru. Tento tutoriál vás provede celým pracovním postupem, od inicializace editoru po uložení každého zdroje na disk.

## Rychlé odpovědi
- **What does “how to extract fonts” mean?** Jedná se o proces získávání vložených souborů písem ze zdrojového dokumentu během převodu do HTML.  
- **Which library handles this?** GroupDocs.Editor pro .NET poskytuje dedikované API pro extrahování písem, obrázků a stylových listů.  
- **Do I need a license?** K dispozici je bezplatná zkušební verze; pro produkční použití je vyžadována komerční licence.  
- **What .NET versions are supported?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.  
- **Can I target a custom folder?** Ano, můžete zadat libovolnou zapisovatelnou cestu při ukládání extrahovaných zdrojů.

## Co je “how to extract fonts”?
**How to extract fonts** odkazuje na získání původních souborů písem vložených ve zdrojovém dokumentu (např. DOCX, PPTX), aby mohly být odkazovány v generovaném HTML. To zajišťuje, že text se v prohlížečích vykreslí přesně tak, jak bylo zamýšleno, bez spoléhání se na systémová písma.

## Proč použít GroupDocs.Editor pro extrakci HTML zdrojů?
GroupDocs.Editor podporuje **50+ vstupních a výstupních formátů**—včetně DOCX, PPTX, PDF a HTML— a dokáže zpracovat dokumenty s **až 300 stránkami** bez načítání celého souboru do paměti. Jeho API extrahuje písma, obrázky a CSS v jednom průchodu, čímž snižuje dobu vývoje až o **70 %** ve srovnání s ručním parsováním.

## Předpoklady
Předtím, než se ponoříte do tutoriálu, ujistěte se, že máte následující předpoklady:
1. **Basic Knowledge of C# and .NET** – Znalost programovacího jazyka C# a .NET frameworku je nezbytná pro sledování příkladů.  
2. **GroupDocs.Editor for .NET Library** – Stáhněte a nainstalujte knihovnu GroupDocs.Editor pro .NET z [webové stránky](https://releases.groupdocs.com/editor/net/).  
3. **Development Environment** – Nastavte své preferované vývojové prostředí, například Visual Studio nebo jiné kompatibilní IDE.

## Importovat jmenné prostory
Pro zahájení importujte potřebné jmenné prostory ve vašem C# projektu:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```

## Jak extrahovat písma a uložit HTML zdroje do složky?
Načtěte svůj zdrojový dokument pomocí `Editor editor = new Editor("sample.docx", new WordProcessingLoadOptions());` a poté zavolejte `editor.Save("output.html", SaveOptions.Html);`. Po operaci uložení obsahuje kolekce `Resources` všechny extrahované prostředky—včetně písem—které můžete iterovat a zapisovat na disk. Tento jednoprostý přístup automaticky zvládá jak konverzi, tak extrakci zdrojů.

## Krok 1: Inicializovat GroupDocs.Editor
`Editor` je hlavní třída, která koordinuje načítání dokumentu, konverzi a extrakci zdrojů. Representuje jediné sezení dokumentu v paměti.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
Nejprve inicializujte objekt `Editor` zadáním cesty k vašemu ukázkovému dokumentu. V tomto příkladu používáme Word dokument, takže specifikujeme `WordProcessingLoadOptions` jako typ dokumentu.

## Krok 2: Upravit dokument
`EditableDocument` je editovatelná reprezentace vrácená metodou `Edit`, která vám umožňuje manipulovat s dokumentem před uložením.

```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
Dále vytvořte objekt `EditableDocument` voláním metody `Edit` objektu `Editor`. To vám umožní provádět úpravy dokumentu.

## Krok 3: Extrahovat zdroje
`Resources` je kolekce, která seskupuje extrahované prostředky—obrázky, písma a stylové listy—do samostatných seznamů pro snadnou manipulaci.

```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
Extrahujte zdroje jako obrázky, písma a stylové listy z dokumentu a uložte je do příslušných seznamů.

## Krok 4: Specifikovat výstupní složku
`outputFolder` je řetězec, který určuje, kam budou extrahované soubory zapsány. Můžete jej nasměrovat na libovolný zapisovatelný adresář na serveru nebo lokálním počítači.

```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
Definujte výstupní složku, kam budou extrahované zdroje uloženy. Cestu složky můžete přizpůsobit podle svých požadavků.

## Krok 5: Uložit zdroje
`SaveResource` je pomocná rutina, která zapisuje jeden binární zdroj (obrázek, písmo nebo stylový list) do souborového systému.

```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
Projděte každý obrazový zdroj, uložte jej do výstupní složky a zobrazte relevantní informace, jako je název souboru, typ a rozměry.

```csharp
		foreach (FontResourceBase oneFont in fonts)
		{
			Console.WriteLine("Saving {0} of {1} type",
				oneFont.FilenameWithExtension, oneFont.Type.FormalName);
			oneFont.Save(Path.Combine(outputFolder, oneFont.FilenameWithExtension));
		}
```
Podobně uložte každý zdroj písma do výstupní složky.

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
Nakonec uložte každý stylový list do výstupní složky a dokončete proces úprav.

## Časté problémy a řešení
- **Missing fonts after conversion** – Ujistěte se, že zdrojový dokument skutečně vkládá písma; jinak GroupDocs.Editor může odkazovat jen na systémová písma.  
- **Access denied errors** – Ověřte, že proces aplikace má oprávnění k zápisu do cílové výstupní složky.  
- **Large documents cause high memory usage** – Použijte `LoadOptions` s `LoadMode = LoadMode.Stream` pro streamování velkých souborů místo jejich úplného načtení do paměti.

## Často kladené otázky

**Q: Je GroupDocs.Editor kompatibilní s jinými formáty dokumentů kromě Wordu?**  
A: Ano, podporuje Excel, PowerPoint, PDF, HTML a více než 50 dalších formátů jak pro úpravy, tak pro extrakci zdrojů.

**Q: Mohu integrovat GroupDocs.Editor do webové aplikace?**  
A: Rozhodně. API funguje hladce s ASP.NET Core, MVC a projekty Web API, což vám umožní zpracovávat dokumenty na straně serveru.

**Q: Poskytuje GroupDocs.Editor integraci s cloudovým úložištěm?**  
A: Ano, zahrnuje vestavěné konektory pro Google Drive, Dropbox, OneDrive a Amazon S3, což umožňuje přímé načítání a ukládání dokumentů v cloudu.

**Q: Je k dispozici bezplatná zkušební verze GroupDocs.Editor?**  
A: Plně funkční 30‑denní zkušební verzi lze stáhnout z webu GroupDocs bez požadavku na kreditní kartu.

**Q: Jak mohu získat technickou podporu pro problémy s extrakcí?**  
A: Můžete kontaktovat tým podpory GroupDocs přes oficiální fórum, odeslat ticket přes zákaznický portál nebo si prostudovat podrobnou dokumentaci API.

---

**Poslední aktualizace:** 2026-05-12  
**Testováno s:** GroupDocs.Editor 23.11 for .NET  
**Autor:** GroupDocs

## Související tutoriály

- [Efektivní úprava dokumentů s GroupDocs.Editor .NET&#58; Transform HTML to Editable Documents](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)
- [Efektivně extrahovat a uložit DOCX zdroje pomocí GroupDocs.Editor .NET - Kompletní průvodce](/editor/net/document-saving/efficient-extract-save-docx-resources-groupdocs-editor-net/)
- [Mistrovství v úpravě a konverzi dokumentů s GroupDocs.Editor .NET&#58; Kompletní průvodce](/editor/net/document-editing/groupdocs-editor-net-mastering-document-editing/)