---
title: Uložit upravený dokument do různých formátů
linktitle: Uložit upravený dokument do různých formátů
second_title: GroupDocs.Editor .NET API
description: Zjistěte, jak uložit upravené dokumenty do různých formátů pomocí GroupDocs.Editor pro .NET v tomto podrobném průvodci krok za krokem.
weight: 11
url: /cs/net/document-processing/save-edited-document-various-formats/
type: docs
---
# Uložit upravený dokument do různých formátů

## Úvod
Chcete uložit upravené dokumenty do různých formátů pomocí GroupDocs.Editor pro .NET? Jste na správném místě! Tento komplexní průvodce vás provede celým procesem, od nastavení prostředí až po uložení upraveného dokumentu v různých formátech. Ponořme se do toho a udělejme z úprav a ukládání dokumentů hračku!
## Předpoklady
Než začneme, ujistěte se, že máte následující:
1.  GroupDocs.Editor for .NET – Stáhněte si nejnovější verzi z[tady](https://releases.groupdocs.com/editor/net/).
2. Vývojové prostředí - Visual Studio nebo jakékoli jiné .NET kompatibilní IDE.
3. .NET Framework – Ujistěte se, že máte nainstalované rozhraní .NET Framework 4.6.1 nebo vyšší.
4. Ukázkový dokument – Ukázkový dokument WordProcessing, se kterým lze pracovat.
5. Základní znalost C# – je nutná znalost programování v C#.
## Importovat jmenné prostory
Nejprve se ujistěte, že jste do svého projektu C# importovali potřebné jmenné prostory. To je zásadní pro přístup k funkcím GroupDocs.Editor.
```csharp
using System;
using GroupDocs.Editor.Metadata;
```
Pojďme si tento proces rozdělit na zvládnutelné kroky. Postupujte pečlivě, abyste se ujistili, že rozumíte každé části.
## Krok 1: Získejte cestu ke vstupnímu souboru
Nejprve musíte zadat cestu k vašemu vstupnímu souboru WordProcessing. Tento soubor bude načten a upraven.
```csharp
string inputFilePath = "Your Sample Document";
```
## Krok 2: Vytvořte možnosti načtení pro dokument
Dále vytvořte možnosti načtení specifické pro dokumenty WordProcessing. Tyto možnosti vám pomohou přizpůsobit způsob načítání dokumentu.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
```
## Krok 3: Vložte dokument s možnostmi
 Nyní vložte dokument do souboru`Editor` instance pomocí zadaných možností zatížení.
```csharp
using (Editor editor = new Editor(inputFilePath, delegate { return loadOptions; }))
```
## Krok 4: Vytvořte možnosti úprav
Připravte možnosti úprav dokumentu. Tyto možnosti určují, jak se dokument otevře pro úpravy.
```csharp
WordProcessingEditOptions editOptions = new WordProcessingEditOptions();
```
## Krok 5: Otevřete dokument pro úpravy
 Otevřete dokument pro úpravy vytvořením souboru`EditableDocument`instance. Tato instance vám umožní provádět změny v dokumentu.
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
```
## Krok 6: Upravte obsah dokumentu
Nyní je čas upravit obsah dokumentu. Nejprve získejte dokument jako jeden řetězec kódovaný base64.
```csharp
string allEmbeddedInsideString = beforeEdit.GetEmbeddedHtml();
```
Upravme například podnadpis v dokumentu.
```csharp
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
```
## Krok 7: Vytvořte nový upravitelný dokument z upraveného obsahu
 Vytvoř nový`EditableDocument` instance z upraveného obsahu a zdrojů.
```csharp
using (EditableDocument afterEdit = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null))
```
## Krok 8: Uložte dokument do různých formátů
Nakonec iterujte všechny podporované formáty WordProcessing a uložte upravený dokument v každém formátu.
```csharp
foreach (WordProcessingFormats oneFormat in WordProcessingFormats.All)
{
    // Připravte možnosti uložení
    WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(oneFormat);
    // Připravte cestu k uložení
    string savePath = Path.Combine("OutputDirectory", "MultipleOutFormats." + saveOptions.OutputFormat.Extension);
    // Uložte dokument
    editor.Save(afterEdit, savePath, saveOptions);
}
```
## Zpráva o dokončení
Na závěr můžete vytisknout zprávu oznamující, že proces byl úspěšně dokončen.
```csharp
Console.WriteLine("SavingEditedDocumentToAllFormats routine has successfully finished");
```
## Závěr
Gratulujeme! Úspěšně jste se naučili ukládat upravené dokumenty do různých formátů pomocí GroupDocs.Editor pro .NET. Tento výkonný nástroj usnadňuje manipulaci a ukládání dokumentů v různých formátech pomocí pouhých několika řádků kódu. Pamatujte, že klíčové kroky zahrnují načtení dokumentu, úpravu obsahu a jeho uložení v požadovaných formátech.
## FAQ
### Co je GroupDocs.Editor pro .NET?
GroupDocs.Editor for .NET je výkonné rozhraní API, které umožňuje upravovat dokumenty v různých formátech pomocí aplikací .NET.
### Mohu používat GroupDocs.Editor zdarma?
 Ano, můžete jej použít s bezplatnou zkušební verzí. Stáhnout to[tady](https://releases.groupdocs.com/).
### Jaké formáty podporuje GroupDocs.Editor?
GroupDocs.Editor podporuje širokou škálu formátů, včetně DOCX, PDF, HTML a mnoha dalších.
### Jak získám dočasnou licenci pro GroupDocs.Editor?
 Můžete získat dočasnou licenci[tady](https://purchase.groupdocs.com/temporary-license/).
### Kde najdu další dokumentaci a podporu?
 K dispozici je podrobná dokumentace[tady](https://tutorials.groupdocs.com/editor/net/) a můžete získat podporu[tady](https://forum.groupdocs.com/c/editor/20).