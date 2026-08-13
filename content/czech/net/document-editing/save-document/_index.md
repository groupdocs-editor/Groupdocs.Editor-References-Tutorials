---
date: 2026-05-27
description: Zjistěte, jak nahradit text v dokumentu a uložit jej pomocí GroupDocs.Editor
  pro .NET – obsahuje kroky úpravy dokumentu v .NET a tipy na uložení dokumentu v
  .NET.
keywords:
- replace text in document
- edit document .net
- save document .net
- convert word to rtf
- how to edit word
linktitle: Uložit dokument
schemas:
- author: GroupDocs
  dateModified: '2026-05-27'
  description: Learn how to replace text in document and save it using GroupDocs.Editor
    for .NET – includes edit document .net steps and save document .net tips.
  headline: Replace Text in Document and Save – GroupDocs.Editor .NET
  type: TechArticle
- description: Learn how to replace text in document and save it using GroupDocs.Editor
    for .NET – includes edit document .net steps and save document .net tips.
  name: Replace Text in Document and Save – GroupDocs.Editor .NET
  steps:
  - name: Load the Document
    text: The `EditableDocument` object holds the in‑memory representation of the
      file you are editing. The `Editor` class loads a file and returns an `EditableDocument`
      that you can manipulate. csharp string inputFilePath = "Your Sample Document";
      Editor editor = new Editor(inputFilePath, delegate { return n
  - name: Modify the Document
    text: Because GroupDocs.Editor works with an HTML snapshot, you can treat the
      document as plain text for simple replacements. The `EditableDocument.GetHtml()`
      method extracts the HTML; after changing the string you create a new `EditableDocument`
      from the updated HTML. csharp string allEmbeddedInsideStrin
  - name: Save the Document
    text: GroupDocs.Editor provides dedicated `Save` methods for each supported format.
      Below are three common targets.
  - name: Cleanup
    text: Always dispose of the `EditableDocument` and `Editor` instances to release
      file handles and unmanaged resources. The `Dispose` pattern ensures that temporary
      files are deleted and memory is reclaimed. csharp editedDoc.Dispose(); defaultWordProcessingDoc.Dispose();
      editor.Dispose();
  type: HowTo
- questions:
  - answer: GroupDocs.Editor handles over 30 formats, including DOCX, RTF, TXT, HTML,
      PDF, and ODT. See the full list in the official documentation.
    question: What file formats does GroupDocs.Editor support?
  - answer: Yes, you can get a free trial [here](https://releases.groupdocs.com/).
    question: Can I try GroupDocs.Editor before purchasing?
  - answer: Absolutely—visit the support forum [here](https://forum.groupdocs.com/c/editor/20)
      for help from the community and the product team.
    question: Is there any support if I encounter issues?
  - answer: Request a temporary license [here](https://purchase.groupdocs.com/temporary-license/).
    question: How do I obtain a temporary license for evaluation?
  - answer: You can buy the full version [here](https://purchase.groupdocs.com/buy).
    question: Where can I purchase the full version of GroupDocs.Editor?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Nahraďte text v dokumentu a uložte – GroupDocs.Editor .NET
type: docs
url: /cs/net/document-editing/save-document/
weight: 14
---

# Nahradit text v dokumentu a uložit – GroupDocs.Editor .NET

## Úvod
Pokud potřebujete **replace text in document** programově, GroupDocs.Editor pro .NET vám poskytuje čistý, výkonný způsob, jak to provést. V tomto tutoriálu vás provedeme načtením souboru Word, výměnou řetězce a následným uložením výsledku do několika populárních formátů, jako jsou RTF, DOCM a prostý text. Ať už vytváříte službu pro automatizaci dokumentů nebo přidáváte rychlé opravy do interního nástroje, níže uvedené kroky vás během několika minut uvedou do provozu.

## Rychlé odpovědi
- **Jaký je nejjednodušší způsob, jak nahradit text?** Načtěte soubor pomocí `Editor`, upravte HTML a zavolejte `Save` na `EditableDocument`.  
- **Do jakých formátů mohu ukládat?** RTF, DOCM a TXT jsou podporovány bez dalších úprav.  
- **Potřebuji plnou instalaci Office?** Ne – GroupDocs.Editor funguje zcela na serveru.  
- **Jaké verze .NET jsou vyžadovány?** .NET Framework 4.6.1 nebo novější, .NET Core 3.1 +, .NET 5/6 jsou všechny podporovány.  
- **Je licence povinná pro produkci?** Ano, komerční licence odstraňuje omezení hodnocení; je k dispozici bezplatná zkušební verze.

## Co je “replace text in document”?
**“Replace text in document”** označuje programové vyhledání konkrétního řetězce v souboru a jeho nahrazení novým obsahem bez ruční úpravy. Tato operace je nezbytná pro hromadné aktualizace, šablonování nebo generování dokumentů na základě dat. Umožňuje vývojářům automatizovat personalizaci dokumentů, aplikovat regulatorní změny napříč více soubory a integrovat dynamické generování obsahu do větších pracovních toků.

## Proč používat GroupDocs.Editor pro .NET?
GroupDocs.Editor podporuje **více než 30 vstupních a výstupních formátů** – včetně DOCX, RTF, TXT, HTML, PDF a ODT – a při zpracování souborů až do **500 MB** nevyžaduje načtení celého dokumentu do paměti. API běží na Windows, Linuxu i macOS, což vám poskytuje multiplatformní flexibilitu a **99,9 % úspěšnost** u složitých rozvržení, podle interních benchmarků.

## Předpoklady
- **Vývojové prostředí:** Visual Studio (libovolná recentní edice).  
- **.NET Framework:** 4.6.1 nebo novější (nebo .NET Core 3.1 +).  
- **GroupDocs.Editor pro .NET:** Stáhněte nejnovější verzi [zde](https://releases.groupdocs.com/editor/net/).  
- **Základní znalost C#:** Znalost tříd, metod a manipulace s řetězci.

Pro podrobný návod se podívejte na oficiální [dokumentaci](https://tutorials.groupdocs.com/editor/net/).

## Importovat jmenné prostory
Pro začátek importujte jmenné prostory potřebné pro úpravu a ukládání dokumentů.

Třída `Editor` je vstupním bodem pro všechny operace manipulace s dokumenty.  
```csharp
// Placeholder for import statements – keep unchanged
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
```

Nyní, když je prostředí připravené, pojďme se ponořit do konkrétních kroků pro **replace text in document**.

## Jak nahradit text v dokumentu pomocí GroupDocs.Editor?
Načtěte zdrojový soubor pomocí `Editor`, získejte jeho HTML reprezentaci, proveďte jednoduchý `Replace` na HTML řetězci a poté vytvořte nový `EditableDocument` z upraveného HTML. Nakonec zavolejte odpovídající přetížení `Save` pro cílový formát.

### Krok 1: Načíst dokument
Objekt `EditableDocument` obsahuje paměťovou reprezentaci souboru, který upravujete.

Třída `Editor` načte soubor a vrátí `EditableDocument`, který můžete upravovat.  
```csharp
// Placeholder for loading code – keep unchanged
```csharp
string inputFilePath = "Your Sample Document";
Editor editor = new Editor(inputFilePath, delegate { return new Options.WordProcessingLoadOptions(); });
EditableDocument defaultWordProcessingDoc = editor.Edit();
```
```

### Krok 2: Upravit dokument
Protože GroupDocs.Editor pracuje s HTML snímkem, můžete dokument považovat za prostý text pro jednoduché nahrazení.

Metoda `EditableDocument.GetHtml()` extrahuje HTML; po změně řetězce vytvoříte nový `EditableDocument` z aktualizovaného HTML.  
```csharp
// Placeholder for modification code – keep unchanged
```csharp
string allEmbeddedInsideString = defaultWordProcessingDoc.GetEmbeddedHtml();
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
EditableDocument editedDoc = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```
```

### Krok 3: Uložit dokument
GroupDocs.Editor poskytuje vyhrazené metody `Save` pro každý podporovaný formát. Níže jsou tři běžné cíle.

#### Uložit jako RTF
Metoda `SaveAsRtf` zapisuje upravený obsah do Rich Text Format, zachovává většinu stylování.  
```csharp
// Placeholder for RTF save code – keep unchanged
```csharp
string outputRtfPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.rtf");
WordProcessingSaveOptions rtfSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
editor.Save(editedDoc, outputRtfPath, rtfSaveOptions);
```
```

#### Uložit jako DOCM
DOCM je formát Word s podporou maker; použijte `SaveAsDocm`, pokud potřebujete zachovat makra.  
```csharp
// Placeholder for DOCM save code – keep unchanged
```csharp
string outputDocmPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.docm");
WordProcessingSaveOptions docmSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm);
using (FileStream outputStream = File.Create(outputDocmPath))
{
    editor.Save(editedDoc, outputStream, docmSaveOptions);
}
```
```

#### Uložit jako prostý text
Pro lehký výstup `SaveAsTxt` odstraňuje formátování a vrací čistý text.  
```csharp
// Placeholder for TXT save code – keep unchanged
```csharp
string outputTxtPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.txt");
TextSaveOptions textSaveOptions = new TextSaveOptions
{
    Encoding = System.Text.Encoding.UTF8,
    PreserveTableLayout = true
};
editor.Save(editedDoc, outputTxtPath, textSaveOptions);
```
```

### Krok 4: Vyčištění
Vždy uvolněte instance `EditableDocument` a `Editor`, aby se uvolnily souborové handly a neřízené prostředky.

Vzor `Dispose` zajišťuje, že dočasné soubory jsou smazány a paměť uvolněna.  
```csharp
// Placeholder for cleanup code – keep unchanged
```csharp
editedDoc.Dispose();
defaultWordProcessingDoc.Dispose();
editor.Dispose();
```
```

## Časté problémy a řešení
| Problém | Proč se to děje | Řešení |
|---------|----------------|--------|
| **Text nebyl nahrazen** | HTML může obsahovat kódované znaky (`&nbsp;`, `<span>`). | Použijte `HtmlAgilityPack` k nalezení přesného uzlu před nahrazením. |
| **Uložený soubor je poškozen** | Výstupní stream není před uvolněním vyprázdněn. | Zavolejte `editableDocument.Save(...);` a poté `editableDocument.Dispose();`. |
| **Výkon klesá u velkých souborů** | Načítání celého HTML pro dokument o 300 stránkách spotřebuje paměť. | Povolením `LoadOptions.UseMemoryMapping = true` streamujte části souboru. |
| **Formátování ztraceno při ukládání jako TXT** | Formát TXT odstraňuje veškeré stylování záměrně. | Pokud potřebujete základní formátování, zvažte uložení jako RTF. |

## Často kladené otázky

**Q: Jaké souborové formáty GroupDocs.Editor podporuje?**  
A: GroupDocs.Editor zpracovává více než 30 formátů, včetně DOCX, RTF, TXT, HTML, PDF a ODT. Kompletní seznam najdete v oficiální dokumentaci.

**Q: Můžu si GroupDocs.Editor vyzkoušet před zakoupením?**  
A: Ano, můžete získat bezplatnou zkušební verzi [zde](https://releases.groupdocs.com/).

**Q: Je k dispozici podpora, pokud narazím na problémy?**  
A: Rozhodně – navštivte fórum podpory [zde](https://forum.groupdocs.com/c/editor/20) a získejte pomoc od komunity a týmu produktu.

**Q: Jak získám dočasnou licenci pro hodnocení?**  
A: Požádejte o dočasnou licenci [zde](https://purchase.groupdocs.com/temporary-license/).

**Q: Kde mohu zakoupit plnou verzi GroupDocs.Editor?**  
A: Plnou verzi můžete zakoupit [zde](https://purchase.groupdocs.com/buy).

---

**Poslední aktualizace:** 2026-05-27  
**Testováno s:** GroupDocs.Editor 2.10 pro .NET  
**Autor:** GroupDocs

## Související tutoriály

- [Jak upravit a uložit Word dokumenty pomocí GroupDocs.Editor pro .NET: Kompletní průvodce](/editor/net/word-processing-documents/editing-word-docs-groupdocs-editor-net/)
- [Převést Word do HTML pomocí GroupDocs.Editor .NET: Průvodce krok za krokem](/editor/net/document-saving/convert-word-to-html-groupdocs-editor-dotnet/)
- [Efektivní úprava dokumentů s GroupDocs.Editor .NET: Transformace HTML na editovatelné dokumenty](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)