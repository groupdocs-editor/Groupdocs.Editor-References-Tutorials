---
date: '2026-04-11'
description: Naučte se, jak vytvořit editovatelný dokument pomocí GroupDocs.Editor
  pro .NET a efektivně uložit dokument jako HTML.
keywords:
- create editable document
- extract images from document
- save document as html
title: Vytvořte editovatelný dokument pomocí GroupDocs.Editor .NET
type: docs
url: /cs/net/document-editing/groupdocs-editor-net-edit-manage-documents-guide/
weight: 1
---

# Vytvoření editovatelného dokumentu s GroupDocs.Editor .NET

V dnešní digitální éře je **vytvoření editovatelného dokumentu** základní požadavkem pro jakýkoli moderní pracovní postup. Ať už vytváříte kolaborativní editor, systém pro správu obsahu nebo nástroj pro automatizované generování zpráv, schopnost programově upravovat a ukládat soubory HTML může ušetřit nespočet hodin. Tento tutoriál vám ukáže, jak **vytvořit instance editovatelného dokumentu**, extrahovat zdroje a **uložit dokument jako HTML** pomocí GroupDocs.Editor pro .NET.

## Rychlé odpovědi
- **Co znamená „vytvořit editovatelný dokument“?** Znamená to načtení zdrojového souboru do objektu GroupDocs.Editor `EditableDocument`, který můžete programově upravovat.  
- **Do jakých formátů mohu konvertovat do HTML?** Word, Excel, PowerPoint a mnoho dalších formátů Office jsou podporovány.  
- **Jak extrahuji obrázky z dokumentu?** Použijte kolekci `EditableDocument.Images`.  
- **Mohu vygenerovat jeden řetězec HTML se všemi vloženými zdroji?** Ano—voláním `GetEmbeddedHtml()`.  
- **Potřebuji licenci pro produkci?** Zkušební verze funguje pro hodnocení; pro komerční použití je vyžadována trvalá licence.

## Co je „vytvořit editovatelný dokument“?
Vytvoření editovatelného dokumentu znamená načtení zdrojového souboru (například .docx) do GroupDocs.Editor, který vrací objekt `EditableDocument`. Tento objekt poskytuje HTML značkování dokumentu, obrázky, fonty a CSS, což vám umožňuje upravovat obsah, nahrazovat zdroje nebo vložit celý dokument do webové stránky.

## Proč použít GroupDocs.Editor .NET pro tento úkol?
- **Plnohodnotné API** – Zpracovává Word, Excel, PowerPoint a další.  
- **Extrahování zdrojů** – Vytahuje obrázky, fonty a stylové listy pomocí jednoduchých vlastností.  
- **Generování vloženého HTML** – Vytvoří jeden řetězec HTML, který obsahuje všechny zdroje, ideální pro e‑mail nebo jednopage aplikace.  
- **Zaměřeno na výkon** – Okamžitě uvolňujte objekty a při potřebě používejte asynchronní vzory.

## Předpoklady
- **.NET prostředí**: Nastavte své vývojové prostředí pro .NET aplikace.
- **Knihovny a závislosti**:
  - Nainstalujte GroupDocs.Editor pomocí jedné z následujících metod:
    - **.NET CLI**
      ```bash
      dotnet add package GroupDocs.Editor
      ```
    - **Package Manager**
      ```powershell
      Install-Package GroupDocs.Editor
      ```
    - **NuGet Package Manager UI**: Vyhledejte a nainstalujte nejnovější verzi.
- **Požadované znalosti**: Doporučuje se znalost programování v C# a základních konceptů práce s dokumenty.

## Nastavení GroupDocs.Editor pro .NET
### Pokyny k instalaci
Pro začátek nastavte GroupDocs.Editor ve svém projektu:
1. **Instalace pomocí .NET CLI**:
   ```bash
   dotnet add package GroupDocs.Editor
   ```
2. **Použít Package Manager**:
   - Otevřete konzoli Package Manager a spusťte:
     ```powershell
     Install-Package GroupDocs.Editor
     ```
3. **NuGet Package Manager UI**: 
   - Přejděte do NuGet, vyhledejte "GroupDocs.Editor" a nainstalujte.

### Získání licence
- **Bezplatná zkušební verze a dočasná licence**:
  Začněte s bezplatnou zkušební verzí stažením z [GroupDocs vydání](https://releases.groupdocs.com/editor/net/). Pro rozšířené testování požádejte o dočasnou licenci na [stránka nákupu](https://purchase.groupdocs.com/temporary-license).

### Základní inicializace a nastavení
Zde je, jak inicializovat GroupDocs.Editor ve vaší aplikaci:
```csharp
using System;
using GroupDocs.Editor;

string inputFilePath = "YOUR_DOCUMENT_DIRECTORY"; // Replace with your actual document path
Editor editor = new Editor(inputFilePath, new WordProcessingLoadOptions());
```

## Jak vytvořit editovatelný dokument pomocí GroupDocs.Editor .NET
### Vytvoření instance EditableDocument
**Přehled**: Načtěte a upravujte dokumenty vytvořením instance `EditableDocument`.

#### Načtení dokumentu
```csharp
using GroupDocs.Editor.Options;

// Load your document with appropriate options
Editor editor = new Editor(inputFilePath, new WordProcessingLoadOptions());

// Create EditableDocument from the loaded file
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```

## Jak vygenerovat vložené html
### Generování vloženého HTML z EditableDocument
**Přehled**: Převést celý dokument na jeden vložený řetězec HTML se styly a zdroji.
```csharp
using System.Collections.Generic;
using GroupDocs.Editor.HtmlCss.Resources;

// Generate embedded HTML
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```

## Jak extrahovat obrázky z dokumentu
### Extrahování zdrojů z EditableDocument
**Přehled**: Získat obrázky, fonty, CSS a další zdroje z vašeho dokumentu.
```csharp
List<IImageResource> allImages = beforeEdit.Images;
List<FontResourceBase> allFonts = beforeEdit.Fonts;
List<CssText> allStylesheets = beforeEdit.Css;
List<IHtmlResource> allResources = beforeEdit.AllResources;
```

## Jak extrahovat fonty z dokumentu
*Stejný blok kódu výše také ukazuje, jak získat fontové zdroje pomocí `beforeEdit.Fonts`.*

## Jak získat čistý HTML obsah
### Získání HTML obsahu z EditableDocument
**Přehled**: Extrahovat čistý HTML obsah bez vložených zdrojů.
```csharp
string htmlMarkup = beforeEdit.GetContent();
```

## Jak upravit externí odkazy v HTML obsahu
### Úprava externích odkazů v HTML obsahu
**Přehled**: Upravit externí odkazy pro obrázky, CSS a fonty pomocí vlastních předpon.
```csharp
using System.Collections.Generic;

// Define custom handlers for resource URLs
string customImagesRequesthandlerUri = "http://example.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://example.com/CssHandler/id=";

// Adjust HTML content with prefixed links
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```

## Jak uložit dokument jako html
### Uložení EditableDocument jako HTML soubor
**Přehled**: Uložit upravený dokument zpět na disk ve formátu HTML.
```csharp
using System.IO;

string htmlFilePath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "document.html"); // Adjust the output path
beforeEdit.Save(htmlFilePath);
```

## Uvolňování a zpracování událostí pro EditableDocument
**Přehled**: Spravovat uvolňování zdrojů a zpracovávat události související s životním cyklem dokumentu.
```csharp
Console.WriteLine("beforeEdit variable of EditableDocument type is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");

// Subscribe to the disposing event
EventHandler someMethod = delegate {
    Console.WriteLine("Disposing event was spotted!");
};
beforeEdit.Disposed += someMethod;
```

## Jak vytvořit editovatelný dokument z HTML obsahu
### Vytvoření EditableDocument z HTML obsahu
**Přehled**: Zrekonstruovat instanci `EditableDocument` z existujícího HTML obsahu.
```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);

// Dispose resources once done
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```

## Praktické aplikace
GroupDocs.Editor .NET lze využít v mnoha reálných scénářích:
- **Kolaborativní editace**: Umožnit plynulé úpravy dokumentu více uživateli.  
- **Webové publikování**: Převést dokumenty do webových formátů pro online prohlížení a interakci.  
- **Systémy pro správu obsahu**: Integrovat s platformami CMS a umožnit dynamické aktualizace obsahu.  
- **Automatizovaná generace zpráv**: Automatizovat tvorbu a formátování zpráv z různých datových zdrojů.

## Úvahy o výkonu
Pro optimalizaci výkonu GroupDocs.Editor .NET:
- Spravovat paměť efektivně tím, že po použití okamžitě uvolníte objekty.  
- Minimalizovat dobu načítání zdrojů optimalizací cest k souborům a URL.  
- Používat asynchronní zpracování, kde je to možné, pro zlepšení odezvy aplikace.

## Časté problémy a řešení
- **Velké soubory způsobují vysokou spotřebu paměti** – Uvolněte objekty `EditableDocument` ihned po dokončení jejich zpracování.  
- **Poškozené odkazy na obrázky po konverzi** – Ujistěte se, že používáte správné URI obslužných zdrojů při volání `GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri)`.  
- **Chybějící fonty v generovaném HTML** – Ověřte, že zdrojový dokument obsahuje požadované fonty nebo že jsou dostupné na serveru.

## Často kladené otázky
**Q: Je GroupDocs.Editor .NET kompatibilní se všemi formáty dokumentů?**  
A: GroupDocs.Editor podporuje širokou škálu formátů, včetně Word, Excel, PowerPoint a mnoha dalších, což vám poskytuje flexibilitu pro různé scénáře použití.

**Q: Jak efektivně zpracovat velké soubory pomocí GroupDocs.Editor?**  
A: Používejte asynchronní API, kde jsou k dispozici, zpracovávejte soubory po částech, pokud je to možné, a vždy okamžitě uvolňujte objekty `EditableDocument` a `Editor`, aby se uvolnila paměť.

**Q: Mohu integrovat GroupDocs.Editor s řešeními cloudového úložiště?**  
A: Ano, můžete se připojit k Azure Blob Storage, Amazon S3, Google Cloud Storage nebo jakémukoli jinému poskytovateli cloudu tím, že předáte souborové streamy do konstruktoru `Editor`.

**Q: Jaké jsou licenční možnosti pro GroupDocs.Editor?**  
A: Můžete začít s bezplatnou zkušební verzí nebo požádat o dočasnou licenci pro hodnocení. Produkční nasazení vyžaduje placenou licenci.

**Q: Kde mohu získat podporu, pokud narazím na problémy?**  
A: Fórum [Fórum podpory GroupDocs](https://forum.groupdocs.com) je k dispozici pro pomoc, a můžete také přímo kontaktovat tým podpory GroupDocs.

---

**Poslední aktualizace:** 2026-04-11  
**Testováno s:** GroupDocs.Editor 23.12 for .NET  
**Autor:** GroupDocs