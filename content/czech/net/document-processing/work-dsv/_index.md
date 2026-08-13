---
date: 2026-06-06
description: Zjistěte, jak **vytvořit editovatelný dokument** z CSV a TSV souborů
  pomocí GroupDocs.Editor for .NET. Tento průvodce také ukazuje, jak **číst oddělený
  text C#** a **editovat CSV .NET** efektivně ve Visual Studio.
keywords:
- create editable document
- read delimited text c#
- edit csv .net
- parse delimited values c#
linktitle: Práce s oddělenými hodnotami (DSV) – vytvořte editovatelný dokument
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to **create editable document** objects from CSV and TSV
    files using GroupDocs.Editor for .NET. This guide also shows how to **read delimited
    text C#** and **edit CSV .NET** efficiently in Visual Studio.
  headline: Work with Delimited Separated Values (DSV) – create editable document
  type: TechArticle
- questions:
  - answer: Yes, the API streams data and can handle files larger than 1 GB without
      loading the entire document into memory.
    question: Can I use GroupDocs.Editor for .NET to edit large CSV files?
  - answer: Absolutely – any single‑character delimiter (e.g., pipe `|`, semicolon
      `;`) is supported as long as you specify it in `DelimitedTextEditOptions`.
    question: Does GroupDocs.Editor for .NET support other DSV formats besides CSV
      and TSV?
  - answer: Yes, you can set the `Encoding` property in `DelimitedTextSaveOptions`
      to UTF‑8, UTF‑16, ISO‑8859‑1, or any .NET `Encoding` you require.
    question: Is it possible to customize the encoding when saving DSV files?
  - answer: Yes – after editing, simply use `SpreadsheetSaveOptions` to export the
      content as an `.xlsx` workbook.
    question: Can I convert a CSV file to an Excel spreadsheet using GroupDocs.Editor
      for .NET?
  - answer: Detailed API references and code samples are available **[here](https://tutorials.groupdocs.com/editor/net/)**.
    question: Where can I find more documentation on GroupDocs.Editor for .NET?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Práce s oddělenými hodnotami (DSV) – vytvořte editovatelný dokument
type: docs
url: /cs/net/document-processing/work-dsv/
weight: 12
---

# Práce s oddělenými hodnotami (DSV) – vytvoření editovatelného dokumentu

Pokud jste vývojář .NET, který potřebuje **vytvořit editovatelný dokument** z oddělených hodnot (DSV) jako CSV nebo TSV, jste na správném místě. V prvních 100 slovech vysvětlíme, proč je GroupDocs.Editor pro .NET nejspolehlivějším způsobem, jak **číst oddělený text C#**, upravit jej a poté uložit zpět bez ztráty formátování. Získáte kompletní workflow připravené ke kopírování a vložení, které se přirozeně hodí do jakéhokoli řešení Visual Studio.

## Rychlé odpovědi
- **Která knihovna nejlépe zvládá úpravu CSV v .NET?** GroupDocs.Editor pro .NET.
- **Mohu upravovat velké CSV soubory ve Visual Studio?** Ano – API streamuje data a vyhýbá se načítání celého souboru do paměti.
- **Potřebuji licenci pro produkční použití?** Vyžaduje se komerční licence; k dispozici je bezplatná zkušební verze.
- **Jaké formáty mohu po úpravě exportovat?** CSV, TSV a formáty tabulek kompatibilní s Excel.
- **Je API kompatibilní s .NET 6+?** Naprosto – podporuje .NET Framework 4.5+, .NET Core 3.1+, .NET 5 a .NET 6.

## Co znamená „create editable document“ v kontextu GroupDocs.Editor?
**Create editable document** znamená vytvoření instance `EditableDocument`, která představuje mutovatelnou verzi zdrojového souboru (CSV, TSV, atd.) v paměti. Tento objekt vám umožní číst, měnit a znovu ukládat obsah pomocí stejného API. Poskytuje metody pro získání textu dokumentu, aplikaci změn a uložení v různých formátech, přičemž zachovává zarovnání sloupců a uvozovky.

## Proč používat GroupDocs.Editor pro práci s DSV?
GroupDocs.Editor zpracovává **více než 50 vstupních a výstupních formátů**, včetně CSV, TSV a tabulek kompatibilních s Excelem, přičemž spotřeba paměti zůstává pod 10 MB pro soubory až do 500 MB. Automaticky také zachovává zarovnání sloupců, pravidla uvozování a vlastní kódování, což eliminuje potřebu ručního parsování.

## Předpoklady
Předtím, než se ponoříme, ujistěte se, že máte nainstalováno:

- **Visual Studio** (jakékoli recentní vydání) – budete vyvíjet a ladit přímo v IDE.
- **GroupDocs.Editor pro .NET** – stáhněte nejnovější balíček **[zde](https://releases.groupdocs.com/editor/net/)**.
- **Základní znalost C#** – tutoriál předpokládá, že umíte vytvořit konzolový nebo ASP.NET projekt a přidat NuGet balíčky.

## Importování jmenných prostorů
Třídy `Editor`, `EditableDocument` a třídy možností se nacházejí v jmenném prostoru `GroupDocs.Editor`.

Třída `DelimitedTextEditOptions` je vstupním bodem pro definování oddělovače (čárka, tabulátor, atd.) a dalších pravidel parsování.

```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

## Jak vytvořit editovatelný dokument z CSV souboru?
Načtěte zdrojové CSV pomocí `Editor` a zavolejte metodu `Edit`, předávající instanci `DelimitedTextEditOptions`, která specifikuje čárkový oddělovač. Metoda vrátí `EditableDocument`, který můžete v paměti manipulovat. Tento dvoustupňový vzor – načíst → upravit – pokrývá scénáře **read delimited text C#** a zajišťuje, že původní struktura souboru zůstane zachována.

## Krok 1: Získání cesty k vstupnímu DSV souboru
Nejprve musíte zadat absolutní nebo relativní cestu ke zdrojovému DSV souboru. Pro demonstraci použijeme jednoduché CSV umístěné ve složce projektu `Data`.

```csharp
string inputFilePath = "Your Sample Document";
```

## Krok 2: Vytvoření instance Editoru
`Editor` je hlavní třída, která orchestruje načítání, úpravy a ukládání. Vytvořením instance s objektem `FileInfo` získáte plnou kontrolu nad životním cyklem souboru.

```csharp
using (Editor editor = new Editor(inputFilePath))
{
```

## Krok 3: Vytvoření DSV editovacích možností
`DelimitedTextEditOptions` říká editoru, jak soubor interpretovat. Můžete nastavit oddělovač, zda první řádek obsahuje hlavičky, a kódování znaků.

```csharp
    Options.DelimitedTextEditOptions editOptions = new DelimitedTextEditOptions(",");
    editOptions.ConvertDateTimeData = false;
    editOptions.ConvertNumericData = true;
    editOptions.TreatConsecutiveDelimitersAsOne = true;
```

## Krok 4: Vytvoření instance EditableDocument
`EditableDocument` představuje mutovatelnou verzi zdrojového souboru v paměti. Zavoláním `Editor.Edit` s možnostmi získáte `EditableDocument`. Tento objekt drží text souboru v mutovatelné řetězci, připravený pro jakoukoli operaci **parse delimited values C#**, kterou potřebujete.

```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```

## Krok 5: Úprava obsahu dokumentu
`GetDocumentText()` vrací aktuální text editovatelného dokumentu jako řetězec. Získejte původní text pomocí `EditableDocument.GetDocumentText()`, proveďte úpravy (např. nahraďte hodnotu ve sloupci) a výsledek uložte do nového řetězce. Zde můžete **edit CSV .NET** bez zásahu do nízkoúrovňových souborových streamů.

```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("SsangYong", "Chevrolet").Replace("Kyron", "Camaro");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```

## Krok 6: Vytvoření EditableDocument s aktualizovaným obsahem
Zabalte upravený řetězec zpět do `EditableDocument`. Tento krok finalizuje změny a připraví objekt k uložení v libovolném podporovaném formátu.

```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```

## Krok 7: Vytvoření možností uložení CSV
`DelimitedTextSaveOptions` určuje, jak zapsat upravený obsah zpět do CSV souboru. Když jste připraveni změny uložit, nakonfigurujte `DelimitedTextSaveOptions`. Můžete specifikovat stejný oddělovač, jiný, nebo dokonce změnit styl konce řádku.

```csharp
    Options.DelimitedTextSaveOptions csvSaveOptions = new DelimitedTextSaveOptions(",");
    csvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

## Krok 8: Vytvoření možností uložení TSV
Pokud potřebujete verzi oddělenou tabulátory, jednoduše přepněte oddělovač na `\t`. Stejný `EditableDocument` lze uložit vícekrát s různými možnostmi.

```csharp
    Options.DelimitedTextSaveOptions tsvSaveOptions = new DelimitedTextSaveOptions("\t");
    tsvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

## Krok 9: Vytvoření možností uložení Spreadsheet
`SpreadsheetSaveOptions` konfiguruje export dokumentu do formátů kompatibilních s Excelem, jako je .xlsx. GroupDocs.Editor také umožňuje export upravených dat do formátu kompatibilního s Excelem (`.xlsx`). Třída `SpreadsheetSaveOptions` automaticky zpracovává typy sloupců, vzorce a stylování buněk.

```csharp
    Options.SpreadsheetSaveOptions cellsSaveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
```

## Krok 10: Připravení cest pro uložení
Definujte odlišné výstupní cesty pro každý formát. Použití jasných pojmenovacích konvencí (např. `output.csv`, `output.tsv`, `output.xlsx`) pomáhá udržet projekt přehledný.

```csharp
    string outputCsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".csv");
    string outputTsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".tsv");
    string outputCellsPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".xlsm");
```

## Krok 11: Uložení upraveného dokumentu
`Save()` zapíše dokument na disk pomocí poskytnutých možností uložení. Zavolejte `EditableDocument.Save` s odpovídajícími možnostmi pro každý cílový formát. API zapisuje soubor přímo na disk, zachovává původní kódování, pokud jej nepřepíšete.

```csharp
    editor.Save(afterEdit, outputCsvPath, csvSaveOptions);
    editor.Save(afterEdit, outputTsvPath, tsvSaveOptions);
    editor.Save(afterEdit, outputCellsPath, cellsSaveOptions);
```

## Krok 12: Uvolnění instancí EditableDocument
Jak `Editor`, tak `EditableDocument` implementují `IDisposable`. Uvolnění jejich prostředků uvolní souborové handle a neřízené zdroje, což je klíčové při zpracování mnoha souborů v dávkovém úkolu.

```csharp
    beforeEdit.Dispose();
    afterEdit.Dispose();
}
System.Console.WriteLine("WorkingWithDsv routine has successfully finished");
```

## Časté problémy a řešení
| Problém | Proč se to děje | Řešení |
|-------|----------------|-----|
| **Neočekávané nadbytečné uvozovky** | Výchozí CSV parser může považovat vložené čárky za oddělovače. | Nastavte `EscapeMode = EscapeMode.DoubleQuote` v `DelimitedTextEditOptions`. |
| **Náraz paměti při velkém souboru** | Načítání 500 MB souboru bez streamování. | Použijte `Editor.Load` s `LoadOptions`, které povolují lazy loading. |
| **Neshoda kódování** | Zdrojový soubor používá UTF‑16, ale možnosti mají výchozí UTF‑8. | Explicitně nastavte `Encoding = Encoding.Unicode` v možnostech uložení. |

## Často kladené otázky

**Q: Mohu použít GroupDocs.Editor pro .NET k úpravě velkých CSV souborů?**  
A: Ano, API streamuje data a dokáže zpracovat soubory větší než 1 GB bez načítání celého dokumentu do paměti.

**Q: Podporuje GroupDocs.Editor pro .NET další DSV formáty kromě CSV a TSV?**  
A: Naprosto – jakýkoli jednoslovní oddělovač (např. svislítko `|`, středník `;`) je podporován, pokud jej specifikujete v `DelimitedTextEditOptions`.

**Q: Je možné přizpůsobit kódování při ukládání DSV souborů?**  
A: Ano, můžete nastavit vlastnost `Encoding` v `DelimitedTextSaveOptions` na UTF‑8, UTF‑16, ISO‑8859‑1 nebo libovolné .NET `Encoding`, které potřebujete.

**Q: Mohu převést CSV soubor na Excel tabulku pomocí GroupDocs.Editor pro .NET?**  
A: Ano – po úpravě jednoduše použijte `SpreadsheetSaveOptions` k exportu obsahu jako `.xlsx` sešitu.

**Q: Kde najdu další dokumentaci k GroupDocs.Editor pro .NET?**  
A: Podrobné reference API a ukázkové kódy jsou k dispozici **[zde](https://tutorials.groupdocs.com/editor/net/)**.

**Poslední aktualizace:** 2026-06-06  
**Testováno s:** GroupDocs.Editor 23.10 pro .NET  
**Autor:** GroupDocs

## Související tutoriály

- [Tutoriály pro úpravu prostého textu a DSV dokumentů v GroupDocs.Editor .NET](/editor/net/plain-text-dsv-documents/)
- [Mistrovství GroupDocs.Editor .NET pro efektivní úpravu CSV dokumentů a konverzi](/editor/net/plain-text-dsv-documents/groupdocs-editor-net-csv-editing-guide/)
- [Mistrovství načítání dokumentů v .NET s GroupDocs.Editor: komplexní průvodce](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)