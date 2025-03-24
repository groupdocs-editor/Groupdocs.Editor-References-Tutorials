---
title: Práce s dokumenty ve formátu prostého textu
linktitle: Práce s dokumenty ve formátu prostého textu
second_title: GroupDocs.Editor .NET API
description: Naučte se upravovat dokumenty ve formátu prostého textu pomocí GroupDocs.Editor pro .NET pomocí našeho podrobného průvodce. Zjednodušte si proces úprav dokumentů .NET.
weight: 15
url: /cs/net/document-processing/work-plain-text-documents/
---

# Práce s dokumenty ve formátu prostého textu

## Úvod
Chcete zefektivnit proces úpravy dokumentů v .NET? Nehledejte nic jiného než GroupDocs.Editor pro .NET! Toto výkonné rozhraní API vám umožňuje snadno upravovat širokou škálu formátů dokumentů. V tomto tutoriálu vás provedeme procesem práce s dokumenty ve formátu prostého textu pomocí GroupDocs.Editor pro .NET. Nakonec budete připraveni zvládnout úpravy textových dokumentů jako profesionál. Jste připraveni se ponořit? Začněme!
## Předpoklady
Než začneme, je třeba mít připraveno několik věcí:
- Vývojové prostředí .NET: Ujistěte se, že máte nastavené funkční vývojové prostředí .NET. Visual Studio je oblíbenou volbou.
-  GroupDocs.Editor pro .NET: Stáhněte a nainstalujte[GroupDocs.Editor pro .NET](https://releases.groupdocs.com/editor/net/).
- Základní znalost C#: Znalost programovacího jazyka C# vám pomůže postupovat podle příkladů.
- Textový editor: Postačí jakýkoli textový editor, ačkoli Visual Studio Code je doporučeno pro jeho funkce a snadné použití.
## Importovat jmenné prostory
Chcete-li začít používat GroupDocs.Editor pro .NET, musíte do projektu importovat potřebné jmenné prostory. Tím je zajištěno, že jsou k dispozici všechny požadované třídy a metody.
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```
Pojďme si tento proces rozdělit na zvládnutelné kroky. Následujte, jak vás provedeme každou fází úpravy dokumentů ve formátu prostého textu pomocí GroupDocs.Editor pro .NET.
## Krok 1: Získejte cestu k vstupnímu souboru TXT
Nejprve musíte zadat cestu ke vstupnímu souboru TXT. Může to být cesta k místnímu souboru nebo stream obsahující obsah souboru.
```csharp
string inputFilePath = "YourSampleDocument.txt";
```
## Krok 2: Vytvořte instanci editoru
 Dále vytvořte instanci souboru`Editor` třída. Tato třída je zodpovědná za načítání a úpravy dokumentů. V této fázi nejsou vyžadovány žádné možnosti zatížení.
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## Krok 3: Vytvořte možnosti úprav TXT
Nyní vytvořte možnosti úprav TXT. Tyto volby vám umožňují určit, jak má být textový obsah zpracován během úprav.
```csharp
    TextEditOptions editOptions = new TextEditOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        RecognizeLists = true,
        LeadingSpaces = TextLeadingSpacesOptions.ConvertToIndent,
        TrailingSpaces = TextTrailingSpacesOptions.Trim
    };
```
## Krok 4: Vytvořte instanci EditableDocument
 S nastavenými možnostmi úprav vytvořte soubor`EditableDocument` instance. To představuje dokument v upravitelném formátu.
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## Krok 5: Upravte obsah dokumentu
Získejte původní textový obsah a proveďte požadované úpravy. V tomto příkladu nahradíme slovo „text“ slovem „UPRAVENÝ text“.
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("text", "EDITED text");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## Krok 6: Vytvořte upravitelný dokument s aktualizovaným obsahem
 Po provedení nezbytných úprav vytvořte nový`EditableDocument` s aktualizovaným obsahem a původními zdroji.
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## Krok 7: Vytvořte možnosti uložení WordProcessing
Připravte si možnosti uložení pro formát WordProcessing. Tento příklad používá formát DOCM a určuje národní prostředí.
```csharp
    WordProcessingSaveOptions wordSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm)
    {
        Locale = System.Globalization.CultureInfo.GetCultureInfo("en-GB")
    };
```
## Krok 8: Vytvořte možnosti ukládání TXT
Podobně vytvořte možnosti uložení pro formát TXT. Ujistěte se, že je kódování nastaveno na UTF-8 a zachovejte rozložení tabulky.
```csharp
    TextSaveOptions txtSaveOptions = new TextSaveOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        PreserveTableLayout = true
    };
```
## Krok 9: Připravte výstupní cesty
Připravte cesty pro uložení výsledných souborů DOCX a TXT. Pomocí cesty vstupního souboru určete výstupní adresář a názvy souborů.
```csharp
    string outputWordPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".docm");
    string outputTxtPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".txt");
```
## Krok 10: Uložte upravený dokument
Nakonec uložte upravený dokument ve formátu DOCX i TXT pomocí zadaných možností uložení.
```csharp
    editor.Save(afterEdit, outputWordPath, wordSaveOptions);
    editor.Save(afterEdit, outputTxtPath, txtSaveOptions);
}
System.Console.WriteLine("Document editing process completed successfully!");
```
## Závěr
 Gratulujeme! Úspěšně jste upravili dokument ve formátu prostého textu pomocí GroupDocs.Editor pro .NET. Tento výkonný nástroj zjednodušuje úpravy dokumentů a usnadňuje integraci do vašich aplikací .NET. Ať už zpracováváte jednoduché textové soubory nebo složité formáty dokumentů, GroupDocs.Editor vás pokryje. Prozkoumejte další funkce a možnosti na[GroupDocs.Editor dokumentace](https://tutorials.groupdocs.com/editor/net/).
## FAQ
### Jaké formáty souborů podporuje GroupDocs.Editor for .NET?
 GroupDocs.Editor pro .NET podporuje širokou škálu formátů souborů, včetně DOCX, TXT, HTML a dalších. Zkontrolovat[dokumentace](https://tutorials.groupdocs.com/editor/net/) pro úplný seznam.
### Jak mohu získat bezplatnou zkušební verzi GroupDocs.Editor pro .NET?
 Můžete si stáhnout bezplatnou zkušební verzi GroupDocs.Editor pro .NET z webu[stránka vydání](https://releases.groupdocs.com/).
### Mohu si zakoupit dočasnou licenci pro GroupDocs.Editor pro .NET?
Ano, můžete získat dočasnou licenci od[Nákupní stránka GroupDocs](https://purchase.groupdocs.com/temporary-license/).
### Kde mohu získat podporu pro GroupDocs.Editor pro .NET?
 Podpora je k dispozici prostřednictvím[Fórum podpory GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).
### Je k dispozici podrobná dokumentace pro GroupDocs.Editor pro .NET?
 Ano, podrobná dokumentace je k dispozici na[Stránka dokumentace GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/).