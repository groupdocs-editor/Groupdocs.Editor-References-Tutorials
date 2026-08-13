---
date: 2026-06-01
description: Naučte se, jak získat počet stránek a extrahovat metadata dokumentu pomocí
  GroupDocs.Editor pro .NET v podrobném krok‑za‑krokem tutoriálu.
keywords:
- get page count
- extract document metadata
- get document info
- find document extension
- retrieve document size
linktitle: Získat počet stránek a extrahovat informace o dokumentu
schemas:
- author: GroupDocs
  dateModified: '2026-06-01'
  description: Learn how to get page count and extract document metadata using GroupDocs.Editor
    for .NET in a detailed step‑by‑step tutorial.
  headline: Get Page Count & Extract Document Info with GroupDocs.Editor
  type: TechArticle
- questions:
  - answer: GroupDocs.Editor supports Word processing, spreadsheet, presentation,
      PDF, and plain‑text files—over 50 formats in total.
    question: What document types can I extract metadata from?
  - answer: Access `DocumentInfo.Extension` after calling `GetDocumentInfo()`; it
      returns the extension without the leading dot.
    question: How do I retrieve the file extension?
  - answer: Yes—`DocumentInfo.Size` returns the size in bytes; divide by 1,048,576
      to convert to megabytes.
    question: Can I get the size of a document in megabytes?
  - answer: Absolutely—GroupDocs.Editor never writes the password to disk and disposes
      of all cryptographic objects after use.
    question: Is it safe to process password‑protected files on a server?
  - answer: You can get support from the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).
    question: Where can I find additional help if I run into issues?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Získat počet stránek a extrahovat informace o dokumentu pomocí GroupDocs.Editor
type: docs
url: /cs/net/document-processing/extract-document-info/
weight: 10
---

# Získání počtu stránek a extrakce informací o dokumentu pomocí GroupDocs.Editor

## Úvod
V tomto komplexním tutoriálu se naučíte, jak **získat počet stránek** a extrahovat podrobné informace o dokumentu — včetně formátu, velikosti a stavu šifrování — pomocí GroupDocs.Editor pro .NET. Ať už vytváříte systém pro správu dokumentů, reportingový engine nebo automatizovanou konverzní pipeline, pochopení metadat souboru je prvním krokem k spolehlivému zpracování. Projdeme celý pracovní postup, od načtení souboru až po bezpečné uvolnění prostředků.

## Rychlé odpovědi
- **Jak získám počet stránek dokumentu?**  
  Zavolejte `editor.GetDocumentInfo().PageCount` po načtení souboru pomocí `Editor`.
- **Které formáty souborů jsou podporovány pro extrakci metadat?**  
  Více než 50 formátů, včetně DOCX, XLSX, PPTX, PDF, TXT a HTML.
- **Mohu extrahovat metadata ze souborů chráněných heslem?**  
  Ano — při vytváření instance `Editor` poskytněte heslo.
- **Musím ručně uvolňovat prostředky?**  
  Rozhodně; vždy zavolejte `editor.Dispose()` nebo obalte editor do bloku `using`.
- **Jaká verze GroupDocs.Editor je vyžadována?**  
  Nejnovější stabilní vydání (v23.12+ v době psaní) podporuje všechny ukázané funkce.

## Co znamená „získat počet stránek“ v GroupDocs.Editor?
`GetDocumentInfo()` je metoda, která vrací objekt `DocumentInfo` obsahující počet stránek dokumentu, formát, velikost a další metadata. Tento jediný volání vám poskytne okamžitý přehled bez nutnosti ručního parsování souboru. Použitím této metody se vyhnete načítání celého dokumentu do paměti, což zlepšuje výkon zejména u velkých souborů a snižuje zatížení serverových prostředků.

## Proč extrahovat metadata dokumentu pomocí GroupDocs.Editor?
GroupDocs.Editor dokáže zpracovat **více než 50 vstupních a výstupních formátů** a získat metadata pro soubory až do **2 GB** bez načítání celého dokumentu do paměti. Tato efektivita snižuje zatížení serveru až o **70 %** ve srovnání s úplným parsováním dokumentu, což je ideální pro aplikace s vysokou propustností.

## Předpoklady
- **Základy vývoje v C#** — měli byste být zvyklí na Visual Studio a strukturu .NET projektů.
- **Visual Studio 2022** (nebo jakákoli novější verze) nainstalované na vašem počítači.
- **GroupDocs.Editor pro .NET** — stáhněte nejnovější balíček ze [stránky ke stažení](https://releases.groupdocs.com/editor/net/).

## Jak načíst váš dokument?
`Editor` je hlavní třída, která představuje dokument a poskytuje metody pro jeho načtení a manipulaci. Načtěte cílový soubor vytvořením instance `Editor` a předáním cesty k souboru. Editor automaticky rozpozná formát, takže není nutné zadávat možnosti načtení. Tento přístup funguje pro jakýkoli podporovaný typ souboru a zjednodušuje počáteční nastavení.

```csharp
using System;
using GroupDocs.Editor.Metadata;
```

## Jak získat informace o dokumentu?
`GetDocumentInfo()` vrací objekt `DocumentInfo` obsahující metadata jako počet stránek, formát, velikost a stav šifrování. Po načtení zavolejte tuto metodu pro získání objektu. Vrácený `DocumentInfo` vám poskytne stručný přehled o vlastnostech souboru, což vám umožní učinit rozhodnutí bez dalšího zpracování.

```csharp
string docxInputFilePath = "YourSampleDocument.docx";
Editor editorDocx = new Editor(docxInputFilePath);
```

## Jak určit typ dokumentu?
`DocumentType` je výčtový typ (enum), který udává, zda je dokument WordProcessing, Spreadsheet nebo Text. Vědět, zda je soubor dokumentem pro zpracování textu, tabulkovým listem nebo prostým textem, ovlivňuje, jak s ním později zacházíte. Použijte vlastnost `DocumentType` objektu `DocumentInfo` k tomuto rozhodnutí a podle toho rozvětvěte logiku.

```csharp
IDocumentInfo infoDocx = editorDocx.GetDocumentInfo(null);
```

## Jak extrahovat podrobné informace pro soubory WordProcessing?
`WordProcessing` označuje dokumenty jako DOCX, ODT a RTF, které jsou zpracovávány jako soubory pro zpracování textu. Pokud je typ dokumentu `WordProcessing`, můžete přímo z objektu `DocumentInfo` číst další vlastnosti jako **formát**, **příponu**, **počet stránek**, **velikost** a **příznak šifrování**. Tyto podrobnosti vám pomohou přizpůsobit kroky zpracování, například aplikovat konkrétní konverze nebo bezpečnostní kontroly.

```csharp
bool isSpreadsheet = infoDocx is SpreadsheetDocumentInfo;
bool isText = infoDocx is TextualDocumentInfo;
bool isWordProcessing = infoDocx is WordProcessingDocumentInfo;
Console.WriteLine($"Is '{docxInputFilePath}' a Spreadsheet: {isSpreadsheet}");
Console.WriteLine($"Is '{docxInputFilePath}' a Textual document: {isText}");
Console.WriteLine($"Is '{docxInputFilePath}' a WordProcessing document: {isWordProcessing}");
```

## Jak zacházet s tabulkovými a textovými dokumenty?
`Spreadsheet` označuje tabulkové soubory jako XLSX, zatímco `Text` představuje prosté textové dokumenty. Pro tabulky (`Spreadsheet`) a prosté textové soubory (`Text`) objekt `DocumentInfo` stále poskytuje základní metadata (přípona, velikost, počet stránek). Některé formáty nemusí poskytovat počet stránek, v takovém případě bude hodnota `0`. Stále se můžete spolehnout na ostatní metadata pro následnou logiku.

```csharp
if (isWordProcessing)
{
    WordProcessingDocumentInfo casted = (WordProcessingDocumentInfo)infoDocx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Page count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```

## Jak pracovat se soubory chráněnými heslem?
`Password` je řetězec předávaný konstruktoru `Editor` pro otevření šifrovaných souborů. Když je dokument šifrován, nejprve se pokuste otevřít jej bez hesla. Pokud selže, zachyťte výjimku a poté opakujte pokus s správným heslem. Konstruktor `Editor` přijímá parametr `Password` pro tento účel, což umožňuje plynulé zpracování chráněných souborů.

```csharp
string xlsxInputFilePath = "YourSampleDocument.xlsx";
Editor editorXlsx = new Editor(xlsxInputFilePath);
IDocumentInfo infoXlsx = editorXlsx.GetDocumentInfo(null);
bool isXlsxSpreadsheet = infoXlsx is SpreadsheetDocumentInfo;
Console.WriteLine($"Is '{xlsxInputFilePath}' a Spreadsheet: {isXlsxSpreadsheet}");
if (isXlsxSpreadsheet)
{
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo)infoXlsx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Tabs count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```

## Jak zpracovat dokumenty založené na textu?
`DocumentInfo` poskytuje základní metadata jako velikost, příponu a kódování pro textové soubory. Textové soubory (např. `.txt`, `.md`) jsou zpracovány jako jednoduché proudy. Stále můžete získat informace o velikosti a kódování z `DocumentInfo`, což je užitečné pro ověření integrity souboru nebo určení vhodných zpracovatelských pipeline.

```csharp
string xlsInputFilePath = "YourSampleDocument.xls";
Editor editorXls = new Editor(xlsInputFilePath);
try
{
    IDocumentInfo infoXls = editorXls.GetDocumentInfo(null);
}
catch (PasswordRequiredException)
{
    Console.WriteLine("This document is password-protected.");
}
try
{
    IDocumentInfo infoXls = editorXls.GetDocumentInfo("incorrect_password");
}
catch (IncorrectPasswordException)
{
    Console.WriteLine("The provided password is incorrect.");
}
IDocumentInfo infoXlsValid = editorXls.GetDocumentInfo("correct_password");
bool isXlsSpreadsheet = infoXlsValid is SpreadsheetDocumentInfo;
Console.WriteLine($"Password-protected document is a Spreadsheet: {isXlsSpreadsheet}");
if (isXlsSpreadsheet)
{
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo)infoXlsValid;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Tabs count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```

## Jak správně uvolnit prostředky?
`Editor` je hlavní třída, která drží neřízené prostředky a musí být po použití uvolněna. Aby se předešlo únikům paměti, vždy po dokončení extrakce informací uvolněte instanci `Editor`. Použití příkazu `using` je nejbezpečnější vzor, protože zaručuje uvolnění i při výskytu výjimky, což zajišťuje čisté řízení prostředků.

```csharp
string xmlInputFilePath = "YourSampleDocument.xml";
Editor editorXml = new Editor(xmlInputFilePath);
IDocumentInfo infoXml = editorXml.GetDocumentInfo(null);
bool isXmlText = infoXml is TextualDocumentInfo;
Console.WriteLine($"Is '{xmlInputFilePath}' a Textual document: {isXmlText}");
if (isXmlText)
{
    TextualDocumentInfo casted = (TextualDocumentInfo)infoXml;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Encoding: {casted.Encoding}; Size: {casted.Size} bytes");
}
```

## Časté problémy a řešení
| Problém | Příčina | Řešení |
|-------|-------|----------|
| **PageCount vrací 0** | Formát nepodporuje stránkování (např. prostý text) | Zkontrolujte `DocumentInfo.DocumentType` před spoleháním na `PageCount`. |
| **Nepodporovaný formát souboru** | Přípona souboru nebyla rozpoznána | Ověřte, že soubor je jedním z více než 50 podporovaných formátů; aktualizujte GroupDocs.Editor na nejnovější verzi. |
| **Výjimka hesla** | Bylo zadáno nesprávné heslo | Zachyťte `PasswordProtectedException` a vyzvěte uživatele k opětovnému zadání hesla. |
| **Náraz paměti u velkých souborů** | Načítání velmi velkých PDF bez streamování | Použijte `LoadOptions` s `LoadOptions.LoadMode = LoadMode.Stream` (k dispozici v novějších verzích). |

## Často kladené otázky

**Q: Z jakých typů dokumentů mohu extrahovat metadata?**  
A: GroupDocs.Editor podporuje soubory pro zpracování textu, tabulky, prezentace, PDF a prostý text — celkem více než 50 formátů.

**Q: Jak získám příponu souboru?**  
A: Přistupte k `DocumentInfo.Extension` po zavolání `GetDocumentInfo()`; vrací příponu bez úvodní tečky.

**Q: Mohu získat velikost dokumentu v megabajtech?**  
A: Ano — `DocumentInfo.Size` vrací velikost v bajtech; vydělte 1 048 576 pro převod na megabajty.

**Q: Je bezpečné zpracovávat soubory chráněné heslem na serveru?**  
A: Rozhodně — GroupDocs.Editor nikdy neukládá heslo na disk a po použití uvolní všechny kryptografické objekty.

**Q: Kde mohu najít další pomoc, pokud narazím na problémy?**  
A: Podporu můžete získat na [fóru podpory GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).

**Poslední aktualizace:** 2026-06-01  
**Testováno s:** GroupDocs.Editor 23.12 for .NET  
**Autor:** GroupDocs

```csharp
editorDocx.Dispose();
editorXlsx.Dispose();
editorXls.Dispose();
editorXml.Dispose();
Console.WriteLine("ExtractingDocumentInfo routine has successfully finished");
```

## Související tutoriály

- [Mistrovská extrakce metadat v .NET s GroupDocs.Editor: Komplexní průvodce](/editor/net/advanced-features/groupdocs-editor-net-metadata-extraction-guide/)
- [Tutoriály načítání dokumentů s GroupDocs.Editor pro .NET](/editor/net/document-loading/)
- [Efektivní úprava dokumentů s GroupDocs.Editor .NET: Převod HTML na editovatelné dokumenty](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)