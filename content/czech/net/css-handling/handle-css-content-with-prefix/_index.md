---
date: 2026-03-06
description: Naučte se, jak pracovat s obsahem CSS s prefixem a jak extrahovat obsah
  CSS pomocí GroupDocs.Editor pro .NET v tomto podrobném tutoriálu krok za krokem.
linktitle: Handle CSS Content with Prefix
second_title: GroupDocs.Editor .NET API
title: Zpracovat CSS obsah s předponou
type: docs
url: /cs/net/css-handling/handle-css-content-with-prefix/
weight: 11
---

# Zpracování CSS obsahu s prefixem

V tomto tutoriálu se dozvíte **jak zpracovat css prefix** při práci se styly v dokumentu pomocí GroupDocs.Editor pro .NET. Ať už potřebujete přidat URL předponu k obrázkům, fontům nebo jakémukoli externímu zdroji, níže uvedené kroky vám přesně ukážou, jak **zpracovat css prefix** a také jak **extrahovat css obsah** pro další zpracování.

## Rychlé odpovědi
- **Co znamená “handle css prefix”?** Přidání vlastní URL předpony k externím zdrojům odkazovaným v CSS.
- **Která metoda API vrací CSS styly?** `EditableDocument.GetCssContent(...)`.
- **Potřebuji licenci?** K dispozici je zkušební licence; pro produkční nasazení je vyžadována komerční licence.
- **Jaké verze .NET jsou podporovány?** .NET Framework 4.5+ a .NET Core/5/6.
- **Mohu změnit předponu za běhu?** Ano – stačí předat jiný řetězec metodě `GetCssContent`.

## Co je **handle css prefix**?
Aplikace předpony na CSS zdroje přepíše cesty k obrázkům, fontům nebo dalším assetům tak, aby ukazovaly na místo, které ovládáte (např. CDN nebo zabezpečený server). To je zvláště užitečné, když exportujete dokument a potřebujete, aby všechny externí odkazy byly přístupné z webové aplikace.

## Proč použít GroupDocs.Editor k **extrahování css obsahu**?
GroupDocs.Editor dokáže načíst původní CSS vložené v dokumentech WordProcessing, poskytnout vám surové řetězce stylových listů a umožnit jejich manipulaci před vykreslením nebo uložením. Tím se eliminuje potřeba ručního parsování a zajišťuje, že extrahované CSS odpovídá interní reprezentaci dokumentu.

## Předpoklady
Než začneme, ujistěte se, že máte připravené následující předpoklady:
- Visual Studio: Budete potřebovat funkční instalaci Visual Studio.  
- .NET Framework: Zajistěte, že máte nainstalovaný .NET Framework.  
- GroupDocs.Editor pro .NET: Můžete si jej stáhnout [zde](https://releases.groupdocs.com/editor/net/).  
- Vzorkový dokument: Mějte připravený vzorový dokument k úpravě.

## Import Namespaces
Nejprve importujte potřebné jmenné prostory, aby náš kód běžel hladce. Tento krok nám poskytuje přístup k hlavním třídám GroupDocs.Editor.

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Editor.Options;
```

## Krok 1: Inicializace editoru
Prvním krokem je vytvoření instance `Editor` s vaším vzorovým dokumentem. Tím se nastaví prostředí pro úpravy.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```

## Krok 2: Úprava dokumentu
Dále získáme objekt `EditableDocument`. Tento objekt představuje editovatelnou verzi souboru a umožňuje nám pracovat s jeho interními částmi.

```csharp
    using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
    {
```

## Krok 3: Nastavení externích předpon
Definujte URL předpony pro obrázky a fonty. Tyto předpony budou přidány před každý odkaz na obrázek a font nalezený v CSS.

```csharp
        string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
        string externalFontsPrefix = "http://www.mywebsite.com/fonts/id=";
```

## Krok 4: **Extrahování CSS obsahu** s předponami
Zavolejte `GetCssContent` a předávejte definované předpony. Metoda vrátí seznam řetězců CSS stylových listů, které již obsahují předponované URL.

```csharp
        List<string> stylesheets = document.GetCssContent(externalImagesPrefix, externalFontsPrefix);
```

## Krok 5: Výstup výsledků
Vytiskněte počet nalezených stylových listů a zobrazte každý z nich. To vám pomůže ověřit, že předpony byly aplikovány správně.

```csharp
        Console.WriteLine("There are {0} stylesheets in the input document", stylesheets.Count);
        foreach (string css in stylesheets)
        {
            Console.WriteLine(css);
        }
    }
}
```

## Časté problémy a řešení
- **Nebyly vráceny žádné stylové listy** – Ujistěte se, že zdrojový dokument skutečně obsahuje CSS (např. Word dokument se stylovanými tabulkami nebo vloženým HTML).  
- **Nesprávné URL** – Zkontrolujte, že řetězce předpon končí vhodným oddělovačem (`/` nebo `=`) podle routování vašeho serveru.  
- **Obavy o výkon** – U velmi velkých dokumentů zvažte zpracování stylových listů po dávkách, aby nedošlo k vysoké spotřebě paměti.

## Závěr
Zpracování CSS obsahu s předponou pomocí GroupDocs.Editor pro .NET je jednoduché a výkonné. Dodržením těchto kroků můžete **zpracovat css prefix**, získat surové CSS pomocí **extrahování css obsahu** a hladce integrovat externí zdroje do vašeho webového workflow. Prozkoumejte další funkce GroupDocs.Editor, jako je konverze do HTML, extrakce obrázků a slučování dokumentů, a získejte ještě větší hodnotu z API.

## Často kladené otázky
### Mohu použít GroupDocs.Editor pro .NET s jinými formáty dokumentů?
Ano, GroupDocs.Editor pro .NET podporuje různé formáty dokumentů včetně PDF, Word, Excel a dalších.

### Je k dispozici bezplatná zkušební verze GroupDocs.Editor pro .NET?
Rozhodně! Svou bezplatnou zkušební verzi můžete zahájit [zde](https://releases.groupdocs.com/).

### Jak získám dočasnou licenci pro GroupDocs.Editor pro .NET?
Dočasnou licenci můžete získat [zde](https://purchase.groupdocs.com/temporary-license/).

### Kde najdu podrobnou dokumentaci k GroupDocs.Editor pro .NET?
Podrobná dokumentace je dostupná [zde](https://tutorials.groupdocs.com/editor/net/).

### Jaké možnosti podpory jsou k dispozici pro GroupDocs.Editor pro .NET?
Podporu můžete získat [zde](https://forum.groupdocs.com/c/editor/20).

## Další často kladené otázky

**Q: Mohu změnit předponu po extrahování CSS?**  
A: Ano. Znovu zavolejte `GetCssContent` s jiným řetězcem předpony; metoda vždy použije hodnoty, které předáte za běhu.

**Q: Funguje to i s dokumenty chráněnými heslem?**  
A: Ano. Heslo zadejte v `WordProcessingLoadOptions` při vytváření instance `Editor`.

**Q: Je možné uložit upravené CSS zpět do dokumentu?**  
A: GroupDocs.Editor v současnosti poskytuje pouze read‑only přístup k CSS. Pro trvalé uložení změn musíte nahradit původní stylový list pomocí podkladových XML API dokumentu.

---

**Poslední aktualizace:** 2026-03-06  
**Testováno s:** GroupDocs.Editor 23.12 pro .NET  
**Autor:** GroupDocs