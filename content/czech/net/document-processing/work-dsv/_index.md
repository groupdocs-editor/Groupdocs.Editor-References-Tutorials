---
title: Práce s oddělenými hodnotami (DSV)
linktitle: Práce s oddělenými hodnotami (DSV)
second_title: GroupDocs.Editor .NET API
description: Naučte se upravovat soubory CSV a TSV pomocí GroupDocs.Editor pro .NET pomocí tohoto podrobného průvodce. Vylepšete své .NET projekty bez námahy.
weight: 12
url: /cs/net/document-processing/work-dsv/
---

# Práce s oddělenými hodnotami (DSV)

## Úvod
Pokud jste vývojář pracující s oddělenými hodnotami (DSV), jako jsou soubory CSV nebo TSV, víte, že programová úprava těchto souborů může být skličující úkol. S GroupDocs.Editor pro .NET se však tento úkol výrazně zjednoduší a zefektivní. V tomto tutoriálu vás provedeme tím, jak používat GroupDocs.Editor pro .NET ke čtení, úpravě a ukládání souborů DSV. Tento proces rozdělíme do snadno pochopitelných kroků, takže jej můžete snadno implementovat do svých projektů.
## Předpoklady
Než se pustíme do výukového programu, ujistěte se, že máte následující předpoklady:
- Visual Studio: Ujistěte se, že máte na svém počítači nainstalované Visual Studio.
-  GroupDocs.Editor for .NET: Budete si muset stáhnout a odkazovat na knihovnu GroupDocs.Editor for .NET. Můžete si jej stáhnout[tady](https://releases.groupdocs.com/editor/net/).
- Základní porozumění C#: Tento tutoriál předpokládá, že máte základní znalosti o C# a vývoji .NET.
## Importovat jmenné prostory
Nejprve musíte do projektu importovat potřebné jmenné prostory. Tyto jmenné prostory poskytují třídy a metody potřebné pro práci s GroupDocs.Editor pro .NET.
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

## Krok 1: Získejte cestu ke vstupnímu souboru DSV
Nejprve musíte zadat cestu ke vstupnímu souboru DSV. V tomto příkladu budeme předpokládat, že se jedná o soubor CSV.
```csharp
string inputFilePath = "Your Sample Document";
```
## Krok 2: Vytvořte instanci editoru
 Vytvořte instanci souboru`Editor` třída. Tato instance bude použita k načtení a manipulaci se souborem DSV.
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## Krok 3: Vytvořte možnosti úprav DSV
 Dále vytvořte instanci`DelimitedTextEditOptions` a zadejte oddělovač pro soubor DSV. Zde používáme jako oddělovač čárku.
```csharp
    Options.DelimitedTextEditOptions editOptions = new DelimitedTextEditOptions(",");
    editOptions.ConvertDateTimeData = false;
    editOptions.ConvertNumericData = true;
    editOptions.TreatConsecutiveDelimitersAsOne = true;
```
## Krok 4: Vytvořte instanci EditableDocument
 Vytvořit`EditableDocument` instance pomocí`Editor.Edit` metoda. Tím se dokument připraví k úpravám.
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## Krok 5: Upravte obsah dokumentu
Načtěte původní textový obsah a proveďte potřebné úpravy. Pro demonstrační účely nahradíme část textu.
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("SsangYong", "Chevrolet").Replace("Kyron", "Camaro");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## Krok 6: Vytvořte upravitelný dokument s aktualizovaným obsahem
 Vytvoř nový`EditableDocument` s aktualizovaným obsahem.
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## Krok 7: Vytvořte možnosti uložení CSV
Zadejte možnosti uložení pro formát CSV, včetně oddělovače a kódování.
```csharp
    Options.DelimitedTextSaveOptions csvSaveOptions = new DelimitedTextSaveOptions(",");
    csvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## Krok 8: Vytvořte možnosti uložení TSV
Podobně zadejte možnosti uložení pro formát TSV.
```csharp
    Options.DelimitedTextSaveOptions tsvSaveOptions = new DelimitedTextSaveOptions("\t");
    tsvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## Krok 9: Vytvořte možnosti uložení tabulky
Pokud potřebujete uložit dokument jako tabulku, vytvořte odpovídající možnosti uložení.
```csharp
    Options.SpreadsheetSaveOptions cellsSaveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
```
## Krok 10: Připravte si cesty pro uložení
Definujte cesty, kam se budou ukládat upravené soubory.
```csharp
    string outputCsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".csv");
    string outputTsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".tsv");
    string outputCellsPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".xlsm");
```
## Krok 11: Uložte upravený dokument
Uložte upravený dokument do zadaných cest v různých formátech.
```csharp
    editor.Save(afterEdit, outputCsvPath, csvSaveOptions);
    editor.Save(afterEdit, outputTsvPath, tsvSaveOptions);
    editor.Save(afterEdit, outputCellsPath, cellsSaveOptions);
```
## Krok 12: Zlikvidujte instance EditableDocument
 Nakonec se ujistěte, že jste je zlikvidovali`EditableDocument` instance pro uvolnění zdrojů.
```csharp
    beforeEdit.Dispose();
    afterEdit.Dispose();
}
System.Console.WriteLine("WorkingWithDsv routine has successfully finished");
```
## Závěr
Úprava souborů DSV pomocí GroupDocs.Editor for .NET je jednoduchý proces, který zahrnuje vytvoření instance editoru, nastavení možností úprav, úpravu obsahu a uložení změn. Tento podrobný průvodce by vám měl pomoci snadno integrovat tuto funkci do vašich aplikací .NET. Ať už pracujete s CSV, TSV nebo jinými formáty DSV, GroupDocs.Editor pro .NET poskytuje robustní a flexibilní řešení.
## FAQ
### Mohu použít GroupDocs.Editor pro .NET k úpravě velkých souborů CSV?
Ano, GroupDocs.Editor pro .NET je schopen efektivně zpracovávat velké soubory CSV.
### Podporuje GroupDocs.Editor pro .NET jiné formáty DSV kromě CSV a TSV?
Ano, podporuje různé formáty DSV, pokud zadáte příslušný oddělovač.
### Je možné upravit kódování při ukládání souborů DSV?
Samozřejmě můžete zadat požadované kódování v možnostech uložení.
### Mohu převést soubor CSV na tabulku aplikace Excel pomocí GroupDocs.Editor pro .NET?
Ano, pomocí vhodných možností uložení můžete uložit soubor CSV jako tabulku aplikace Excel.
### Kde najdu další dokumentaci k GroupDocs.Editor pro .NET?
 Můžete najít podrobnou dokumentaci[tady](https://tutorials.groupdocs.com/editor/net/)