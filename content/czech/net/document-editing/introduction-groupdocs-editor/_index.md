---
title: Úvod do GroupDocs.Editoru pro .NET
linktitle: Úvod do GroupDocs.Editoru pro .NET
second_title: GroupDocs.Editor .NET API
description: Naučte se, jak používat GroupDocs.Editor pro .NET k programové úpravě dokumentů pomocí tohoto podrobného průvodce krok za krokem.
weight: 12
url: /cs/net/document-editing/introduction-groupdocs-editor/
type: docs
---
# Úvod do GroupDocs.Editoru pro .NET

## Úvod 
Pokud jste vývojář, který chce bezproblémově integrovat možnosti úprav dokumentů do vašich aplikací .NET, GroupDocs.Editor for .NET je výkonný nástroj, který je třeba zvážit. Tato všestranná knihovna umožňuje programově načítat, upravovat a ukládat různé formáty dokumentů. Ať už potřebujete zpracovávat dokumenty aplikace Word, soubory PDF nebo soubory HTML, GroupDocs.Editor tento proces zjednodušuje a činí jej efektivním a přímočarým. V tomto tutoriálu prozkoumáme základy používání GroupDocs.Editor pro .NET a provedeme vás praktickým příkladem krok za krokem.
## Předpoklady
Než se pustíme do implementace, ujistěte se, že máte následující předpoklady:
- Vývojové prostředí: Visual Studio 2017 nebo novější.
- .NET Framework: .NET Framework 4.6.1 nebo novější.
-  GroupDocs.Editor pro .NET: Můžete[stažení](https://releases.groupdocs.com/editor/net/) to z webu.
-  Licence: Platná licence nebo a[dočasná licence](https://purchase.groupdocs.com/temporary-license/) z GroupDocs.
## Importovat jmenné prostory
Chcete-li začít používat GroupDocs.Editor pro .NET, musíte importovat potřebné jmenné prostory. Tyto jmenné prostory budou poskytovat přístup ke třídám a metodám potřebným pro úpravy dokumentů.
```csharp
using System;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```

V této části rozdělíme proces do zvládnutelných kroků, abychom zajistili, že porozumíte každé části pracovního postupu.
## Krok 1: Získejte cestu ke vstupnímu souboru
Nejprve musíte zadat cestu k dokumentu, který chcete upravit. Pro tento příklad předpokládejme, že máte soubor DOCX s názvem „Váš vzorový dokument.docx“.
```csharp
string inputFilePath = "Your Sample Document.docx";
```
## Krok 2: Vytvořte instanci objektu editoru
 Dále vytvořte instanci souboru`Editor` třídy načtením vstupního souboru. Tento krok inicializuje dokument pro další zpracování.
```csharp
using (GroupDocs.Editor.Editor editor = new Editor(inputFilePath))
{
    //Následné kroky budou vnořeny do tohoto bloku
}
```
## Krok 3: Otevřete dokument pro úpravy
 Chcete-li dokument upravit, získejte prostředníka`EditableDocument` instance. Tento objekt vám umožňuje manipulovat s obsahem dokumentu a souvisejícími prostředky.
```csharp
EditableDocument beforeEdit = editor.Edit();
```
## Krok 4: Načtěte obsah dokumentu a zdroje
Extrahujte hlavní obsah, obrázky, písma a šablony stylů z upravitelného dokumentu. Tyto informace jsou nezbytné pro provedení jakýchkoli úprav.
```csharp
string content = beforeEdit.GetContent();
var images = beforeEdit.Images;
var fonts = beforeEdit.Fonts;
var stylesheets = beforeEdit.Css;
```
### Krok 4.1: Získejte dokument jako jeden řetězec kódovaný Base64
Můžete také získat celý obsah dokumentu jako jeden řetězec kódovaný base64, který zahrnuje všechny zdroje.
```csharp
string allEmbeddedInsideString = beforeEdit.GetEmbeddedHtml();
```
### Krok 4.2: Upravte obsah
Pro demonstrační účely upravme obsah dokumentu nahrazením konkrétního textu.
```csharp
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
```
## Krok 5: Vytvořte novou instanci EditableDocument
 Po úpravě obsahu vytvořte nový`EditableDocument` instance využívající upravený obsah.
```csharp
EditableDocument afterEdit = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```
## Krok 6: Uložte upravený dokument
Nyní uložte upravený dokument do požadovaného výstupního formátu. V tomto příkladu jej uložíme jako soubor RTF.
### Krok 6.1: Připravte výstupní cestu
Zadejte cestu, kam chcete uložit výstupní dokument.
```csharp
string outputPath = Path.Combine("Output Directory Path", Path.GetFileNameWithoutExtension(inputFilePath) + ".rtf");
```
### Krok 6.2: Připravte možnosti ukládání
Definujte možnosti uložení a určete formát, ve kterém chcete dokument uložit.
```csharp
Options.WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
```
### Krok 6.3: Uložit do Path
Uložte upravený dokument do zadané cesty.
```csharp
editor.Save(afterEdit, outputPath, saveOptions);
```
### Krok 6.4: Uložit do streamu
Případně můžete výstupní dokument uložit do libovolného zapisovatelného streamu.
```csharp
using (MemoryStream ms = new MemoryStream())
{
    editor.Save(afterEdit, ms, saveOptions);
}
```
## Krok 7: Zlikvidujte editor a instance EditableDocument
 Nakonec vyčistěte likvidací`EditableDocument` instance a`Editor` protestovat proti uvolnění zdrojů.
```csharp
beforeEdit.Dispose();
afterEdit.Dispose();
editor.Dispose();
```

## Závěr
GroupDocs.Editor pro .NET neuvěřitelně snadno integruje možnosti úprav dokumentů do vašich aplikací. Podle kroků uvedených v tomto kurzu můžete načítat, upravovat a ukládat dokumenty programově s minimálním úsilím. Ať už potřebujete pracovat s dokumenty Word, PDF nebo jinými formáty, GroupDocs.Editor nabízí robustní řešení pro vaše potřeby zpracování dokumentů.
## FAQ
### Mohu upravovat soubory PDF pomocí GroupDocs.Editor pro .NET?
Ano, GroupDocs.Editor pro .NET podporuje úpravy souborů PDF spolu s mnoha dalšími formáty, jako je DOCX, HTML a další.
### Jak získám dočasnou licenci pro GroupDocs.Editor pro .NET?
 Dočasnou licenci můžete získat od[Web GroupDocs](https://purchase.groupdocs.com/temporary-license/).
### Jaké formáty souborů podporuje GroupDocs.Editor pro .NET?
GroupDocs.Editor pro .NET podporuje různé formáty, mimo jiné DOCX, PDF, HTML a RTF.
### Je možné integrovat GroupDocs.Editor s cloudovým úložištěm?
Ano, můžete integrovat GroupDocs.Editor s různými řešeními cloudového úložiště pro správu vašich dokumentů.
### Kde najdu dokumentaci k GroupDocs.Editor pro .NET?
Dokumentace je k dispozici[tady](https://tutorials.groupdocs.com/editor/net/).