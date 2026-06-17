---
date: 2026-06-06
description: Zjistěte, jak vypsat podporované formáty dokumentů a určit příponu souboru
  pomocí GroupDocs.Editor pro .NET. Step‑by‑step guide s code snippets, quick answers
  a FAQs.
keywords:
- list supported document formats
- determine file format extension
- GroupDocs.Editor .NET
- document editing API
- supported formats guide
linktitle: Seznam podporovaných formátů dokumentů
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to list supported document formats and determine file format
    extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets,
    quick answers, and FAQs.
  headline: List Supported Document Formats with GroupDocs.Editor .NET
  type: TechArticle
- description: Learn how to list supported document formats and determine file format
    extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets,
    quick answers, and FAQs.
  name: List Supported Document Formats with GroupDocs.Editor .NET
  steps:
  - name: '**.NET development environment** – Visual Studio 2022 or any IDE that supports
      .NET 6+.'
    text: '**.NET development environment** – Visual Studio 2022 or any IDE that supports
      .NET 6+.'
  - name: '**GroupDocs.Editor for .NET library** – download from the [GroupDocs releases
      page](https://releases.groupdocs.com/editor/net/).'
    text: '**GroupDocs.Editor for .NET library** – download from the [GroupDocs releases
      page](https://releases.groupdocs.com/editor/net/).'
  - name: '**Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/)
      for unrestricted access.'
    text: '**Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/)
      for unrestricted access.'
  - name: '**Basic C# knowledge** – familiarity with namespaces, `using` statements,
      and console output.'
    text: '**Basic C# knowledge** – familiarity with namespaces, `using` statements,
      and console output.'
  - name: '**Loop Through Formats:** We iterate over all available Word‑processing
      formats.'
    text: '**Loop Through Formats:** We iterate over all available Word‑processing
      formats.'
  - name: '**Output Format Details:** For each format we print its friendly name and
      default file extension.'
    text: '**Output Format Details:** For each format we print its friendly name and
      default file extension.'
  - name: '**Loop Through Formats:** The same looping logic applies to presentations.'
    text: '**Loop Through Formats:** The same looping logic applies to presentations.'
  - name: '**Output Format Details:** The name and extension are displayed for each
      format.'
    text: '**Output Format Details:** The name and extension are displayed for each
      format.'
  - name: '**Parse Format:** `FromExtension` converts the `.xlsm` extension into its
      internal `SpreadsheetFormat` enum.'
    text: '**Parse Format:** `FromExtension` converts the `.xlsm` extension into its
      internal `SpreadsheetFormat` enum.'
  - name: '**Output Format:** The parsed format’s name is printed, confirming the
      mapping.'
    text: '**Output Format:** The parsed format’s name is printed, confirming the
      mapping.'
  type: HowTo
- questions:
  - answer: '`DocumentFormatInfo` provides metadata about supported file types, while
      `SaveOptions` configures how a document is written back to disk (format, compression,
      etc.).'
    question: What is the difference between `DocumentFormatInfo` and `SaveOptions`?
  - answer: Yes—use `DocumentFormatInfo.FromExtension("yourExt")`; if the extension
      isn’t recognized, the method returns `null`.
    question: Can I list formats for a custom file extension?
  - answer: Absolutely. Pass the password to the `Editor` constructor via `EditorSettings`
      to open encrypted documents.
    question: Does GroupDocs.Editor support password‑protected files?
  - answer: Over **30 input and output formats**, spanning Word, Excel, PowerPoint,
      HTML, and plain text.
    question: How many formats does GroupDocs.Editor actually support?
  - answer: Use the `GetEditableWordProcessingFormats()` (or Spreadsheet/Presentation
      equivalents) to retrieve formats that allow full edit capabilities.
    question: Is there a way to restrict the list to only editable formats?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Seznam podporovaných formátů dokumentů s GroupDocs.Editor .NET
type: docs
url: /cs/net/document-processing/work-document-formats/
weight: 13
---

# Seznam podporovaných formátů dokumentů

Vítejte v našem komplexním tutoriálu o **jak vypsat podporované formáty dokumentů** s GroupDocs.Editor pro .NET. Ať už vytváříte webovou aplikaci zaměřenou na dokumenty nebo podnikové desktopové řešení, je nezbytné přesně vědět, které formáty můžete upravovat nebo konvertovat. V tomto průvodci se dozvíte, jak vyjmenovat formáty, parsovat přípony a upravovat dokumenty — vše s jasnými, uživatelsky přívětivými vysvětleními a připravenými ukázkovými kódy.

## Rychlé odpovědi
- **Jak vypsat všechny podporované formáty?** Použijte `DocumentFormatInfo.GetSupportedWordProcessingFormats()` (nebo ekvivalenty pro Presentation/Spreadsheet) a projděte kolekci.  
- **Mohu určit formát z přípony souboru?** Ano — zavolejte `DocumentFormatInfo.FromExtension(".docx")`.  
- **Jaké typy souborů GroupDocs.Editor podporuje?** Více než 30 vstupních a výstupních formátů, včetně DOCX, XLSX, PPTX, HTML a prostého textu.  
- **Potřebuji licenci pro výpis formátů?** Dočasná licence odemkne celé API; jinak zkušební verze funguje s omezenými funkcemi.  
- **Které verze .NET jsou kompatibilní?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.

## Co znamená „vypsat podporované formáty dokumentů“?
Tento výraz odkazuje na programové získání kolekce typů souborů, které GroupDocs.Editor může otevřít, upravit a uložit. Tato operace vám umožní vytvořit dynamické rozbalovací nabídky UI nebo ověřit nahrané soubory uživatele před zpracováním, čímž zajistíte, že do editoru jsou předány pouze kompatibilní soubory.

## Proč vypsat podporované formáty dokumentů?
GroupDocs.Editor **podporuje více než 30 vstupních a výstupních formátů** a dokáže zpracovat soubory až do **2 GB** bez načítání celého dokumentu do paměti. Znalost přesného seznamu zabraňuje chybám za běhu, zlepšuje uživatelskou zkušenost a umožňuje vynucovat obchodní pravidla, například „povolit jen editovatelné Office dokumenty“. Také vám pomůže zobrazit uživatelům pouze formáty, které vaše aplikace skutečně podporuje.

## Předpoklady
1. **.NET vývojové prostředí** — Visual Studio 2022 nebo jakékoli IDE podporující .NET 6+.  
2. **Knihovna GroupDocs.Editor pro .NET** — stáhněte ji ze [stránky vydání GroupDocs](https://releases.groupdocs.com/editor/net/).  
3. **Dočasná licence** — získejte [dočasnou licenci](https://purchase.groupdocs.com/temporary-license/) pro neomezený přístup.  
4. **Základní znalost C#** — znalost jmenných prostorů, `using` příkazů a výstupu do konzole.

## Jak vypsat podporované formáty dokumentů?
Načtěte kolekci podporovaných formátů a vytiskněte název a příponu každého formátu. Tento dvoustupňový vzor funguje pro dokumenty Word Processing, Spreadsheet a Presentation. Iterací kolekce můžete dynamicky naplnit UI prvky, jako jsou rozbalovací seznamy, a zajistit, že uživatelé mohou vybrat jen formáty, které editor skutečně zvládne.

```csharp
// No actual code block – placeholder retained from original tutorial
```csharp
using System;
using GroupDocs.Editor.Options;
```
```

### Výpis formátů Word Processing
`Formats.WordProcessingFormats` je výčtový typ, který popisuje každý typ souboru Word‑processing rozpoznaný editorem. Vlastnost `All` vrací kolekci těchto objektů formátů.

```csharp
```csharp
foreach (Formats.WordProcessingFormats oneFormat in Formats.WordProcessingFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**Vysvětlení:**  
1. **Procházení formátů:** Procházíme všechny dostupné Word‑processing formáty.  
2. **Výpis podrobností o formátu:** Pro každý formát vytiskneme jeho přátelský název a výchozí příponu souboru.

### Výpis formátů prezentací
`Formats.PresentationFormats` funguje stejným způsobem pro soubory prezentací, a odhaluje každý podporovaný typ prezentace prostřednictvím kolekce `All`.

```csharp
```csharp
foreach (Formats.PresentationFormats oneFormat in Formats.PresentationFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**Vysvětlení:**  
1. **Procházení formátů:** Stejná logika procházení se použije i pro prezentace.  
2. **Výpis podrobností o formátu:** Název a přípona jsou vytištěny pro každý formát.

## Jak určit příponu formátu souboru?
Někdy máte jen název souboru a potřebujete odvodit odpovídající `DocumentFormat`. GroupDocs.Editor nabízí jednoduchý statický pomocník, který mapuje příponu souboru na interní reprezentaci formátu, což vám umožní ověřit nebo konvertovat soubory před jejich načtením do editoru.

### Parsování formátů tabulek
`Formats.SpreadsheetFormats.FromExtension` převádí řetězec přípony souboru na odpovídající hodnotu výčtu formátu tabulky.

```csharp
```csharp
Formats.SpreadsheetFormats expectedXlsm = Formats.SpreadsheetFormats.FromExtension(".xlsm");
Console.WriteLine("Parsed Spreadsheet format is {0}", expectedXlsm.Name);
```
```

**Vysvětlení:**  
1. **Parsování formátu:** `FromExtension` převádí příponu `.xlsm` na interní výčet `SpreadsheetFormat`.  
2. **Výpis formátu:** Název parsovaného formátu je vytištěn, čímž potvrzuje mapování.

### Parsování textových formátů
Podobně `Formats.TextualFormats.FromExtension` rozpozná textové přípony souborů, jako jsou HTML nebo TXT.

```csharp
```csharp
Formats.TextualFormats expectedHtml = Formats.TextualFormats.FromExtension("html");
Console.WriteLine("Parsed Textual format is {0}", expectedHtml.Name);
```
```

**Vysvětlení:**  
1. **Parsování formátu:** Metoda `FromExtension` rozpozná příponu `html` jako `TextFormat`.  
2. **Výpis formátu:** Název textového formátu je zobrazen, což je užitečné pro webové editory.

## Jak upravit dokumenty po určení formátů?
Jakmile znáte formát, načítání a úprava dokumentu následuje jednotný vzor. Nejprve vytvoříte instanci `Editor` s cestou k zdrojovému souboru, poté zavoláte `Edit()` pro získání `EditableDocument`. Odtud můžete číst, měnit a nakonec uložit obsah pomocí vhodných `SaveOptions`.

### Načtení dokumentu
`Editor` je hlavní třída, která zapouzdřuje všechny operace úpravy pro daný soubor.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/document.docx"))
{
    // Further steps will be covered here.
}
```
```

**Vysvětlení:**  
1. **Inicializace Editoru:** Vytvořte instanci `Editor`, předáním úplné cesty k cílovému souboru.  
2. **Vzor uvolnění:** Příkaz `using` zajišťuje, že všechny neřízené prostředky jsou rychle uvolněny.

### Extrahování obsahu
`EditableDocument.GetContent()` vrací surový text dokumentu (nebo HTML pro webové editory), který můžete zobrazit nebo manipulovat.

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    string content = editableDocument.GetContent();
    Console.WriteLine(content);
}
```
```

**Vysvětlení:**  
1. **Metoda Edit:** `Edit()` vrací objekt `EditableDocument`.  
2. **Získání obsahu:** `GetContent()` extrahuje surový text dokumentu (nebo HTML pro webové editory).  
3. **Výpis obsahu:** Obsah je vypsán do konzole pro ověření.

### Ukládání změn
`SaveOptions` určuje editoru, jak a v jakém formátu má upravený dokument zapsat zpět do úložiště.

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    // Modify content here
    SaveOptions saveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docx);
    editor.Save(editableDocument, "path/to/save/document.docx", saveOptions);
}
```
```

**Vysvětlení:**  
1. **Metoda Edit:** Znovu získat `EditableDocument` po úpravách.  
2. **Úprava obsahu:** Aplikujte své změny na řetězec (není zde ukázáno).  
3. **Možnosti uložení:** Nakonfigurujte `SaveOptions` s požadovaným výstupním formátem.  
4. **Uložení dokumentu:** Uložte upravený soubor zpět na disk.

## Jak pracovat s různými typy dokumentů?
GroupDocs.Editor abstrahuje práci s Word, Spreadsheet a Presentation za stejným rozhraním API, což usnadňuje přepínání kontextů bez nutnosti učit se novou sadu tříd pro každou rodinu dokumentů.

### Úprava tabulkových dokumentů
`SpreadsheetSaveOptions` definuje, jak je tabulka zapisována, včetně formátu a volitelných nastavení komprese.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/spreadsheet.xlsx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // Modify content here
        SaveOptions saveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsx);
        editor.Save(editableDocument, "path/to/save/spreadsheet.xlsx", saveOptions);
    }
}
```
```

**Vysvětlení:**  
1. **Inicializace Editoru:** Předat cestu k souboru tabulky konstruktoru `Editor`.  
2. **Metoda Edit:** Získat `EditableDocument`.  
3. **Získání obsahu:** Vytisknout CSV reprezentaci tabulky (nebo HTML).  
4. **Úprava obsahu:** Proveďte požadované změny na úrovni buněk.  
5. **Možnosti uložení:** Vyberte vhodné `SpreadsheetSaveOptions`.  
6. **Uložení dokumentu:** Zapište aktualizovanou tabulku zpět do úložiště.

### Úprava prezentačních dokumentů
`PresentationSaveOptions` řídí výstupní formát pro sady snímků, což vám umožní zachovat nebo změnit původní typ souboru.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/presentation.pptx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // Modify content here
        SaveOptions saveOptions = new PresentationSaveOptions(PresentationFormats.Pptx);
        editor.Save(editableDocument, "path/to/save/presentation.pptx", saveOptions);
    }
}
```
```

**Vysvětlení:**  
1. **Inicializace Editoru:** Načtěte soubor PowerPoint pomocí `Editor`.  
2. **Metoda Edit:** Získat `EditableDocument`.  
3. **Získání obsahu:** Extrahovat HTML snímků nebo prostý text.  
4. **Úprava obsahu:** Aktualizovat nadpisy, odrážky nebo obrázky.  
5. **Možnosti uložení:** Použijte `PresentationSaveOptions` k definování výstupního formátu.  
6. **Uložení dokumentu:** Uložit upravenou prezentaci.

## Časté problémy a řešení
- **Chyba „Formát není podporován“:** Ověřte, že používáte nejnovější verzi GroupDocs.Editor; pravidelně přidává podporu pro novější formáty Office.  
- **Vysoká spotřeba paměti u velkých souborů:** Aktivujte režim streamování nastavením `EditorSettings.EnableStreaming = true` před načtením dokumentu.  
- **Licence nebyla použita:** Ujistěte se, že soubor dočasné licence je umístěn v kořenovém adresáři aplikace nebo načten pomocí `License license = new License(); license.SetLicense("path/to/license.lic");`.

## Často kladené otázky

**Q: Jaký je rozdíl mezi `DocumentFormatInfo` a `SaveOptions`?**  
A: `DocumentFormatInfo` poskytuje metadata o podporovaných typech souborů, zatímco `SaveOptions` konfiguruje, jak je dokument zapsán zpět na disk (formát, komprese atd.).

**Q: Mohu vypsat formáty pro vlastní příponu souboru?**  
A: Ano — použijte `DocumentFormatInfo.FromExtension("yourExt")`; pokud přípona není rozpoznána, metoda vrátí `null`.

**Q: Podporuje GroupDocs.Editor soubory chráněné heslem?**  
A: Ano. Heslo předáte konstruktoru `Editor` prostřednictvím `EditorSettings`, aby se otevřely šifrované dokumenty.

**Q: Kolik formátů GroupDocs.Editor skutečně podporuje?**  
A: Více než **30 vstupních a výstupních formátů**, zahrnujících Word, Excel, PowerPoint, HTML a prostý text.

**Q: Existuje způsob, jak omezit seznam jen na editovatelné formáty?**  
A: Použijte `GetEditableWordProcessingFormats()` (nebo ekvivalenty pro Spreadsheet/Presentation) k získání formátů, které umožňují plnou editaci.

## Další zdroje
- Stáhněte knihovnu ze [stránky vydání GroupDocs](https://releases.groupdocs.com/editor/net/).  
- Získejte [dočasnou licenci](https://purchase.groupdocs.com/temporary-license/) pro plný přístup k funkcím.  
- Vyzkoušejte produkt s [bezplatnou zkušební verzí](https://releases.groupdocs.com/).  
- Prozkoumejte podrobné příklady použití v [dokumentaci GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/).  
- Získejte pomoc od komunity na [fóru podpory](https://forum.groupdocs.com/c/editor/20).

## Závěr
Po přečtení tohoto průvodce nyní víte, jak **vypsat podporované formáty dokumentů**, **určit formát souboru z jeho přípony** a **upravit dokumenty** napříč typy Word, Spreadsheet a Presentation pomocí GroupDocs.Editor pro .NET. Začleňte tyto úryvky do svých projektů a vytvořte robustní aplikace, které jsou si vědomy formátů, potěší koncové uživatele a sníží chyby za běhu.

---

**Last Updated:** 2026-06-06  
**Tested With:** GroupDocs.Editor 23.9 for .NET  
**Author:** GroupDocs

## Související tutoriály

- [Mistrovství načítání dokumentů v .NET s GroupDocs.Editor: Kompletní průvodce](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)
- [Mistrovství úpravy dokumentů v .NET s GroupDocs.Editor: Kompletní průvodce](/editor/net/document-editing/master-document-editing-dotnet-groupdocs-editor/)
- [Převod Wordu do HTML pomocí GroupDocs.Editor .NET: Průvodce krok za krokem](/editor/net/document-saving/convert-word-to-html-groupdocs-editor-dotnet/)