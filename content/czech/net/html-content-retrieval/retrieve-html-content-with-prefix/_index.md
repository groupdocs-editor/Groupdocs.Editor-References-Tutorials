---
title: Načíst obsah HTML s předponou
linktitle: Načíst obsah HTML s předponou
second_title: GroupDocs.Editor .NET API
description: Naučte se, jak načíst obsah HTML z dokumentů pomocí GroupDocs.Editor pro .NET s vlastními předponami pro obrázky a šablony stylů. Včetně průvodce krok za krokem.
type: docs
weight: 11
url: /cs/net/html-content-retrieval/retrieve-html-content-with-prefix/
---
## Úvod
Vítejte v našem podrobném návodu, jak načíst obsah HTML z dokumentu pomocí GroupDocs.Editor pro .NET. Ať už jste zkušený vývojář nebo teprve začínáte, tato příručka vás provede procesem snadno pochopitelným způsobem. Pokryjeme vše, co potřebujete vědět, od nastavení vašeho prostředí až po úspěšné spuštění kódu. Pojďme se ponořit!
## Předpoklady
Než začneme, ujistěte se, že máte splněny následující předpoklady:
1.  GroupDocs.Editor pro .NET: Stáhněte si nejnovější verzi z[stránka ke stažení](https://releases.groupdocs.com/editor/net/).
2. Vývojové prostředí: Visual Studio nebo jakékoli jiné preferované vývojové prostředí .NET.
3. Základní znalost C#: Znalost programování v C# vám pomůže postupovat podle příkladů.
4. Dokument k úpravě: Připravte si vzorový dokument k testování, například dokument aplikace Word.
5. .NET Framework: Ujistěte se, že máte na svém počítači nainstalované rozhraní .NET Framework.
Nyní, když máte vše připraveno, můžeme začít!
## Importovat jmenné prostory
Nejprve musíte importovat potřebné jmenné prostory do vašeho projektu C#. Tyto jmenné prostory poskytují třídy a metody potřebné pro práci s GroupDocs.Editor pro .NET.
```csharp
using System;
using GroupDocs.Editor.Options;
```
S importovanými jmennými prostory můžeme přejít k nastavení editoru.
## Krok 1: Inicializujte editor
 Chcete-li začít, musíte inicializovat`Editor`třídy s vaším dokumentem. Tento krok zahrnuje zadání dokumentu, který chcete upravit, a poskytnutí nezbytných možností načtení.
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
    // Zde budou přidány další kroky
}
```
 V tomto příkladu načítáme dokument aplikace Word. Můžete vyměnit`"Your Sample Document"` s cestou k vašemu dokumentu.
## Krok 2: Upravte dokument
 Dále musíme otevřít dokument pro úpravy. To se provádí pomocí`Edit` metoda`Editor` třídy, která vyžaduje`WordProcessingEditOptions` jako argument.
```csharp
using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
{
    // Zde budou přidány další kroky
}
```
 The`EditableDocument` instance představuje dokument v upravitelném formátu. Nyní jsme připraveni načíst obsah HTML.
## Krok 3: Definujte vlastní předpony
Chcete-li přidat vlastní předpony pro obrázky a CSS, musíme předpony definovat jako řetězce. Tento krok zajistí, že obsah HTML bude mít zadané předpony pro externí zdroje.
```csharp
string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
string externalCssPrefix = "http://www.mywebsite.com/css/id=";
```
Adresy URL můžete nahradit požadovanými předponami. Tyto předpony budou použity v dalším kroku k přizpůsobení výstupu HTML.
## Krok 4: Načtěte obsah HTML
Nyní, když máme nastavené předpony, můžeme z dokumentu načíst obsah HTML. The`GetContent` metoda`EditableDocument` třída nám umožňuje specifikovat předpony obrázku a CSS.
```csharp
string prefixedHtmlContent = document.GetContent(externalImagesPrefix, externalCssPrefix);
Console.WriteLine("HTML content of the input document with custom image and stylesheet prefixes: {0}", prefixedHtmlContent);
```
Tento fragment kódu načte obsah HTML s vlastními předponami a vytiskne jej do konzoly. Tento obsah HTML můžete podle potřeby dále zpracovat nebo uložit.
## Závěr
A tady to máte! Podle těchto kroků můžete snadno načíst obsah HTML z dokumentu pomocí GroupDocs.Editor pro .NET, doplněný vlastními předponami pro obrázky a šablony stylů. Tento výkonný nástroj zjednodušuje manipulaci s dokumenty a umožňuje vám soustředit se na bezproblémovou integraci úprav dokumentů do vašich aplikací .NET.
 Pro podrobnější informace se podívejte na[GroupDocs.Editor pro dokumentaci .NET](https://reference.groupdocs.com/editor/net/) . Pokud máte nějaké dotazy nebo potřebujete další pomoc, neváhejte se obrátit na[Fórum podpory](https://forum.groupdocs.com/c/editor/20).
## FAQ
### Jaké typy dokumentů mohu upravovat pomocí GroupDocs.Editor pro .NET?
GroupDocs.Editor podporuje různé formáty dokumentů včetně Wordu, Excelu, PowerPointu, PDF a dalších.
### Jak získám bezplatnou zkušební verzi GroupDocs.Editor pro .NET?
 Můžete získat bezplatnou zkušební verzi od[Web GroupDocs](https://releases.groupdocs.com/).
### Mohu obsah HTML dále přizpůsobit?
Ano, načtený obsah HTML můžete před vykreslením nebo uložením upravit podle potřeby.
### Je možné použít GroupDocs.Editor pro .NET s jinými jazyky .NET?
Ano, můžete jej použít s jakýmkoli jazykem kompatibilním s .NET, jako je VB.NET nebo F#.
### Jak získám dočasnou licenci pro GroupDocs.Editor pro .NET?
 Dočasnou licenci můžete získat od[nákupní stránku](https://purchase.groupdocs.com/temporary-license/).