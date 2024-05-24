---
title: Práce s vícetabulkovými tabulkami
linktitle: Práce s vícetabulkovými tabulkami
second_title: GroupDocs.Editor .NET API
description: Naučte se pracovat s vícekartovými tabulkami v .NET pomocí GroupDocs.Editor. Součástí je podrobný průvodce, příklady kódu a osvědčené postupy.
type: docs
weight: 17
url: /cs/net/document-processing/work-multi-tab-spreadsheets/
---
## Úvod
Manipulace s tabulkami s více kartami může být docela náročný úkol, zvláště když potřebujete manipulovat nebo extrahovat data z různých listů ve stejném dokumentu. Pokud pracujete s .NET a hledáte robustní řešení, GroupDocs.Editor pro .NET je vynikající volbou. V tomto tutoriálu vás provedeme procesem práce s vícekartovými tabulkami pomocí GroupDocs.Editor pro .NET. Pokryjeme vše od nastavení prostředí až po uložení každé karty jako samostatného souboru.
## Předpoklady
Než se pustíte do výukového programu, ujistěte se, že máte splněny následující předpoklady:
1. Visual Studio: Ujistěte se, že máte na svém počítači nainstalované Visual Studio.
2. .NET Framework: GroupDocs.Editor pro .NET podporuje rozhraní .NET Framework 4.0 nebo vyšší.
3. GroupDocs.Editor pro .NET: Stáhněte a nainstalujte knihovnu GroupDocs.Editor pro .NET. Můžete to získat z[stránka ke stažení](https://releases.groupdocs.com/editor/net/).
4.  Licence: I když můžete použít a[dočasná licence](https://purchase.groupdocs.com/temporary-license/) pro vyzkoušení knihovny se doporučuje zakoupit plnou licenci pro produkční použití.
## Importovat jmenné prostory
Než začneme kódovat, musíte importovat potřebné jmenné prostory. Na začátek souboru .cs přidejte následující pomocí direktiv:
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
## 1. Získejte cestu ke vstupnímu souboru
Nejprve musíte zadat cestu ke vstupnímu souboru tabulky. Tento soubor by měl být XLSX (OOXML) s více kartami.
```csharp
string inputFilePath = "Your Sample Document";
```
## 2. Načtěte tabulku do instance editoru
 Dále načtete tabulku do souboru`Editor` instance. To se provádí pomocí datového proudu souboru a určením vhodných možností načtení pro tabulku.
```csharp
using (FileStream inputStream = File.OpenRead(inputFilePath))
{
    using (Editor editor = new Editor(delegate { return inputStream; }, delegate { return new SpreadsheetLoadOptions(); }))
    {
        // Další kroky budou směřovat sem
    }
}
```
## 3. Vytvořte EditableDocument z první záložky
 Chcete-li upravit nebo upravit konkrétní kartu, musíte ji vytvořit`EditableDocument` například pro tuto kartu. Karta je určena pomocí indexu založeného na nule.
```csharp
SpreadsheetEditOptions editOptions1 = new SpreadsheetEditOptions();
editOptions1.WorksheetIndex = 0; // První záložka
EditableDocument firstTabBeforeEdit = editor.Edit(editOptions1);
```
## 4. Vytvořte EditableDocument z druhé záložky
 Podobně vytvořte`EditableDocument` pro druhou záložku.
```csharp
SpreadsheetEditOptions editOptions2 = new SpreadsheetEditOptions();
editOptions2.WorksheetIndex = 1; // Druhá záložka
EditableDocument secondTabBeforeEdit = editor.Edit(editOptions2);
```
## 5. Uložte první záložku do samostatného dokumentu
Nyní uložte první kartu jako samostatný dokument. Zadejte formát uložení a výstupní cestu.
```csharp
SpreadsheetSaveOptions saveOptions1 = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
string outputFilename1 = Path.GetFileNameWithoutExtension(inputFilePath) + "_tab1.xlsm";
string outputPath1 = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename1);
editor.Save(firstTabBeforeEdit, outputPath1, saveOptions1);
```
## 6. Uložte druhou kartu do samostatného dokumentu
Opakujte postup pro druhou kartu, ale tentokrát ji uložte v jiném formátu.
```csharp
SpreadsheetSaveOptions saveOptions2 = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsb);
string outputFilename2 = Path.GetFileNameWithoutExtension(inputFilePath) + "_tab2.xlsb";
string outputPath2 = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename2);
editor.Save(secondTabBeforeEdit, outputPath2, saveOptions2);
```
## 7. Zlikvidujte EditableDocument instance
 Nakonec se ujistěte, že jste je správně zlikvidovali`EditableDocument` instance pro uvolnění zdrojů.
```csharp
firstTabBeforeEdit.Dispose();
secondTabBeforeEdit.Dispose();
```

## Závěr
Podle těchto kroků můžete snadno pracovat s vícekartovými tabulkami v .NET pomocí GroupDocs.Editor. Tato výkonná knihovna zjednodušuje proces úprav a ukládání různých listů v tabulkovém procesoru, díky čemuž jsou vaše vývojářské úkoly lépe zvládnutelné. Ať už máte co do činění se složitou manipulací s daty nebo jednoduchými úpravami, GroupDocs.Editor for .NET poskytuje nástroje, které potřebujete k efektivnímu provedení práce.
## FAQ
### Co je GroupDocs.Editor pro .NET?
GroupDocs.Editor for .NET je výkonné rozhraní API pro úpravu dokumentů, které umožňuje vývojářům načítat, upravovat a ukládat dokumenty různých formátů v rámci aplikací .NET.
### Mohu GroupDocs.Editor for .NET vyzkoušet před zakoupením?
 Ano, můžete použít a[zkušební verze zdarma](https://releases.groupdocs.com/) nebo požádat a[dočasná licence](https://purchase.groupdocs.com/temporary-license/) hodnotit produkt.
### Jaké formáty souborů podporuje GroupDocs.Editor pro .NET?
GroupDocs.Editor podporuje širokou škálu formátů, včetně DOCX, XLSX, PPTX, PDF a mnoha dalších.
### Jak získám podporu pro GroupDocs.Editor pro .NET?
 Podporu můžete získat návštěvou stránky[Fórum podpory](https://forum.groupdocs.com/c/editor/20).
### Kde si mohu koupit plnou licenci pro GroupDocs.Editor pro .NET?
 Plnou licenci si můžete zakoupit od[nákupní stránku](https://purchase.groupdocs.com/buy).