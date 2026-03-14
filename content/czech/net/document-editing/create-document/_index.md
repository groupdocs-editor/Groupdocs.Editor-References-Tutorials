---
date: 2026-03-14
description: Naučte se, jak upravovat prezentace PowerPoint a další typy dokumentů
  pomocí GroupDocs.Editor pro .NET. Průvodce také popisuje, jak uložit upravený dokument
  a upravovat Word dokument v .NET.
linktitle: Create Document
second_title: GroupDocs.Editor .NET API
title: Upravte prezentaci PowerPoint pomocí GroupDocs.Editor pro .NET
type: docs
url: /cs/net/document-editing/create-document/
weight: 10
---

Docs

Make sure bold formatting stays.

Now produce final markdown with all translations.

Check we didn't miss any shortcodes: there are none besides {{CODE_BLOCK_X}} placeholders. No Hugo shortcodes. Ensure we kept all code block placeholders.

Now produce final answer.# Upravit prezentaci PowerPoint pomocí GroupDocs.Editor pro .NET

## Úvod
Pokud hledáte spolehlivý způsob, jak programově **upravit prezentaci PowerPoint** soubory, GroupDocs.Editor pro .NET je odpovědí. Tato knihovna vám umožňuje pracovat s formáty Word, Excel, PowerPoint, Ebook a Email – vše z jediné, snadno použitelné API. V tomto tutoriálu vás provedeme vytvářením a úpravou každého podporovaného typu dokumentu, ukážeme vám, jak **uložit upravený dokument** jako stream, a poskytneme praktické tipy, které můžete použít v reálných projektech.

## Rychlé odpovědi
- **Která knihovna mi umožní upravovat soubory PowerPoint v .NET?** GroupDocs.Editor pro .NET.  
- **Mohu upravovat soubory Word, Excel a Epub pomocí stejného API?** Ano, stejná třída `Editor` podporuje všechny tyto formáty.  
- **Jak zachytím upravený soubor?** Poskytněte funkci zpětného volání (např. `SaveNewDocument`), která přijímá výstupní stream.  
- **Potřebuji licenci pro produkční použití?** Ano – zakupte licenci nebo použijte dočasnou zkušební licenci.  
- **Které verze .NET jsou podporovány?** .NET Framework 4.0+, .NET Core a .NET 5/6.

## Co znamená „upravit prezentaci PowerPoint“ pomocí GroupDocs.Editor?
Úprava prezentace PowerPoint znamená načtení souboru `.pptx`, provedení změn (např. úpravu snímků, textu nebo skrytých prvků) a následné získání aktualizovaného souboru – vše bez nutnosti mít nainstalovaný Microsoft Office.

## Proč používat GroupDocs.Editor pro .NET?
- **Jedno API pro mnoho formátů** – Není potřeba přepínat mezi samostatnými knihovnami pro Word, Excel nebo Epub.  
- **Žádná závislost na Office** – Funguje na serverech, kontejnerech a v CI pipelinech.  
- **Detailní kontrola** – Přizpůsobte stránkování, informace o jazyce, extrakci fontů a další.  
- **Zpracování založené na streamech** – Ideální pro cloudové služby, kde pracujete s paměťovými streamy místo fyzických souborů.

## Požadavky
- Visual Studio (jakékoli recentní vydání).  
- .NET Framework 4.0 nebo vyšší (nebo .NET Core/.NET 5+).  
- Knihovna GroupDocs.Editor pro .NET – stáhněte ji z [here](https://releases.groupdocs.com/editor/net/).  
- Základní znalost C#.

## Importovat jmenné prostory
Nejprve importujte jmenné prostory, které obsahují základní třídy, jež budeme používat.

```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using System.IO;
```

## Krok 1: Nastavení streamu
Použijeme paměťový stream jako zástupný objekt pro obsah dokumentu.

```csharp
Stream memoryStream = Stream.Null;
```

## Krok 2: Funkce zpětného volání pro **uložení upraveného dokumentu**
Definujte funkci zpětného volání, která přijímá upravený stream a ukládá jej do `memoryStream`.

```csharp
void SaveNewDocument(Stream resultStream)
{
    memoryStream = resultStream;
}
```

## Krok 3: Vytvoření a úprava dokumentu WordProcessing  
(Zde **upravujeme Word dokument .net**.)

### Vytvořit a upravit s výchozími možnostmi
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    EditableDocument defaultWordProcessingDoc = editor.Edit();
}
```

### Vytvořit a upravit s vlastními možnostmi
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    WordProcessingEditOptions wordProcessingEditOptions = new WordProcessingEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true,
        FontExtraction = FontExtractionOptions.ExtractAllEmbedded
    };
    EditableDocument editableWordProcessingDocument = editor.Edit(wordProcessingEditOptions);
}
```

## Krok 4: Vytvoření a úprava tabulkového dokumentu  
(Použijte to k **úpravě Excel souboru .net**.)

### Vytvořit a upravit s výchozími možnostmi
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    EditableDocument defaultEditableSpreadsheetDocument = editor.Edit();
}
```

### Vytvořit a upravit s vlastními možnostmi
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    SpreadsheetEditOptions spreadsheetEditOptions = new SpreadsheetEditOptions
    {
        WorksheetIndex = 0,
        ExcludeHiddenWorksheets = true
    };
    EditableDocument editableSpreadsheetDocument = editor.Edit(spreadsheetEditOptions);
}
```

## Krok 5: **Upravit prezentaci PowerPoint** – Vytvoření a úprava prezentačního dokumentu
Toto je jádro našeho hlavního klíčového slova.

### Vytvořit a upravit s výchozími možnostmi
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    EditableDocument defaultEditablePresentationDocument = editor.Edit();
}
```

### Vytvořit a upravit s vlastními možnostmi
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    PresentationEditOptions presentationEditOptions = new PresentationEditOptions
    {
        ShowHiddenSlides = false,
        SlideNumber = 0
    };
    EditableDocument editablePresentationDocument = editor.Edit(presentationEditOptions);
}
```

## Krok 6: Vytvoření a úprava Ebook dokumentu  
(Zde **upravujeme epub soubor**.)

### Vytvořit a upravit s výchozími možnostmi
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EditableDocument defaultEditableEbookDocument = editor.Edit();
}
```

### Vytvořit a upravit s vlastními možnostmi
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EbookEditOptions ebookEditOptions = new EbookEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true
    };
    EditableDocument editableEbookDocument = editor.Edit(ebookEditOptions);
}
```

## Krok 7: Vytvoření a úprava Email dokumentu
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EditableDocument defaultEditableEmailDocument = editor.Edit();
}
```

### Vytvořit a upravit s vlastními možnostmi
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EmailEditOptions emailEditOptions = new EmailEditOptions
    {
        MailMessageOutput = MailMessageOutput.All
    };
    EditableDocument editableEmailDocument = editor.Edit(emailEditOptions);
}
```

## Krok 8: Dokončení procesu
Uvolněte stream, aby se uvolnily prostředky, jakmile budete hotovi.

```csharp
memoryStream.Dispose();
System.Console.WriteLine("CreateDocument routine has successfully finished");
```

## Časté úskalí a tipy
- **Nikdy nezapomeňte uvolnit stream** – ponechání otevřeného může způsobit úniky paměti v dlouhodobě běžících službách.  
- **Při úpravě PowerPointu se ujistěte, že nastavujete `SlideNumber` správně**; jinak se může první snímek duplikovat.  
- **Pokud potřebujete zachovat původní název souboru**, uložte jej před voláním zpětné funkce a po úpravě přejmenujte výstupní stream.  
- **U velkých dokumentů** zvažte zpracování po částech nebo použití `Editor` s dočasným souborem, aby nedošlo k vysoké spotřebě paměti.

## Často kladené otázky

**Q: Jaké typy dokumentů mohu upravovat pomocí GroupDocs.Editor pro .NET?**  
A: Můžete upravovat WordProcessing, tabulky, prezentace, ebooky a emaily – včetně souborů PowerPoint pro případ **upravit prezentaci PowerPoint**.

**Q: Je možné přizpůsobit možnosti úprav?**  
A: Ano, každý formát má svou vlastní třídu možností (např. `WordProcessingEditOptions`, `SpreadsheetEditOptions`, `PresentationEditOptions`), která vám umožní detailně nastavit stránkování, skryté snímky, výběr listu atd.

**Q: Jak zacházet s výstupem upravených dokumentů?**  
A: Použijte funkci zpětného volání (`SaveNewDocument`) k zachycení upraveného streamu, poté jej můžete zapsat na disk, do databáze nebo vrátit z webového API.

**Q: Potřebuji licenci pro použití GroupDocs.Editor pro .NET?**  
A: Ano, licence je vyžadována pro produkční použití. Můžete ji získat na [here](https://purchase.groupdocs.com/buy). Dočasná zkušební licence je také k dispozici.

**Q: Kde najdu podrobnější dokumentaci?**  
A: Podrobná dokumentace je k dispozici na stránce [GroupDocs.Editor for .NET documentation page](https://tutorials.groupdocs.com/editor/net/).

## Závěr
GroupDocs.Editor pro .NET usnadňuje **úpravu prezentací PowerPoint** a širokou škálu dalších typů dokumentů. Dodržením výše uvedených kroků můžete vytvářet, měnit a **ukládat upravené dokumenty** jako streamy kompletně v kódu, aniž byste se spolehli na instalaci Office. Prozkoumejte pokročilé možnosti knihovny, abyste si přizpůsobili zážitek z úprav podle konkrétních obchodních potřeb.

---

**Poslední aktualizace:** 2026-03-14  
**Testováno s:** GroupDocs.Editor for .NET (latest release)  
**Autor:** GroupDocs