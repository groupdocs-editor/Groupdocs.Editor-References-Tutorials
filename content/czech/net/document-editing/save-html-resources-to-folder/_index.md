---
title: Uložte zdroje HTML do složky
linktitle: Uložte zdroje HTML do složky
second_title: GroupDocs.Editor .NET API
description: Naučte se, jak extrahovat zdroje HTML z dokumentů pomocí Groupdocs.Editor pro .NET. Tento komplexní tutoriál poskytuje vývojářům podrobné pokyny.
weight: 13
url: /cs/net/document-editing/save-html-resources-to-folder/
type: docs
---
# Uložte zdroje HTML do složky

## Úvod
Groupdocs.Editor for .NET je výkonný nástroj, který umožňuje vývojářům bezproblémově manipulovat a převádět dokumenty v rámci jejich aplikací .NET. Ať už potřebujete extrahovat HTML zdroje z dokumentu nebo provádět pokročilé editační úlohy, Groupdocs.Editor zjednodušuje proces pomocí intuitivního API a rozsáhlé dokumentace.
## Předpoklady
Než se pustíte do výukového programu, ujistěte se, že máte následující předpoklady:
1. Základní znalost C# a .NET: Znalost programovacího jazyka C# a .NET frameworku je nezbytná pro následování příkladů.
2.  Knihovna Groupdocs.Editor for .NET: Stáhněte a nainstalujte knihovnu Groupdocs.Editor for .NET z[webová stránka](https://releases.groupdocs.com/editor/net/).
3. Vývojové prostředí: Nastavte si preferované vývojové prostředí, jako je Visual Studio nebo jakékoli jiné kompatibilní IDE.

## Importovat jmenné prostory
Chcete-li začít, importujte potřebné jmenné prostory do svého projektu C#:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```
##Nyní si rozdělíme proces ukládání zdrojů HTML do složky pomocí Groupdocs.Editor pro .NET do několika kroků:
## Krok 1: Inicializujte Groupdocs.Editor
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
 Nejprve inicializujte`Editor`objekt poskytnutím cesty k vašemu vzorovému dokumentu. V tomto příkladu používáme dokument aplikace Word, takže specifikujeme`WordProcessingLoadOptions` jako typ dokumentu.
## Krok 2: Upravte dokument
```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
 Dále vytvořte`EditableDocument` objekt voláním`Edit` metoda`Editor` objekt. To vám umožní provádět úpravy dokumentu.
## Krok 3: Extrahujte zdroje
```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
Extrahujte zdroje, jako jsou obrázky, písma a šablony stylů, z dokumentu a uložte je do příslušných seznamů.
## Krok 4: Zadejte výstupní složku
```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
Definujte výstupní složku, kam se budou ukládat extrahované zdroje. Cestu ke složce můžete upravit podle svých požadavků.
## Krok 5: Uložte zdroje
```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
Projděte každý zdroj obrázku, uložte jej do výstupní složky a zobrazte relevantní informace, jako je název souboru, typ a rozměry.
```csharp
		foreach (FontResourceBase oneFont in fonts)
		{
			Console.WriteLine("Saving {0} of {1} type",
				oneFont.FilenameWithExtension, oneFont.Type.FormalName);
			oneFont.Save(Path.Combine(outputFolder, oneFont.FilenameWithExtension));
		}
```
Podobně uložte každý prostředek písem do výstupní složky.
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
Nakonec uložte každou šablonu stylů do výstupní složky a dokončete proces úprav.

## Závěr
Na závěr, Groupdocs.Editor pro .NET poskytuje pohodlné řešení pro správu a manipulaci s dokumenty programově v aplikacích .NET. Podle tohoto návodu můžete snadno extrahovat zdroje HTML z dokumentů a přizpůsobit proces podle vašich konkrétních požadavků.
## FAQ
### Je Groupdocs.Editor kompatibilní s jinými formáty dokumentů kromě Wordu?
Ano, Groupdocs.Editor podporuje širokou škálu formátů dokumentů včetně Excelu, PowerPointu, PDF a dalších.
### Mohu integrovat Groupdocs.Editor do své webové aplikace?
Rozhodně, Groupdocs.Editor nabízí bezproblémovou integraci s webovými aplikacemi vyvinutými na .NET frameworku.
### Poskytuje Groupdocs.Editor podporu pro služby cloudového úložiště?
Ano, Groupdocs.Editor podporuje integraci s oblíbenými službami cloudového úložiště, jako je Disk Google, Dropbox a Microsoft OneDrive.
### Je k dispozici bezplatná zkušební verze pro Groupdocs.Editor?
Ano, můžete využít bezplatnou zkušební verzi Groupdocs.Editor z webu.
### Jak mohu získat technickou podporu pro Groupdocs.Editor?
Pro technickou pomoc a podporu komunity můžete navštívit fórum Groupdocs.Editor.