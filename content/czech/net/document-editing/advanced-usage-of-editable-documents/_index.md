---
date: 2026-03-14
description: Naučte se, jak extrahovat obrázky z DOCX, převést DOCX na HTML a uložit
  dokument jako HTML pomocí GroupDocs.Editor pro .NET.
linktitle: Extract Images from DOCX – Advanced Editable Document Usage
second_title: GroupDocs.Editor .NET API
title: Extrahovat obrázky z DOCX – Pokročilé využití editovatelného dokumentu
type: docs
url: /cs/net/document-editing/advanced-usage-of-editable-documents/
weight: 11
---

# Extrahovat obrázky z DOCX – Pokročilé použití editovatelného dokumentu

Pokud jste vývojář .NET a chcete **extrahovat obrázky z DOCX** a rozšířit své možnosti úprav dokumentů, GroupDocs.Editor pro .NET nabízí výkonný soubor nástrojů. Tento komplexní průvodce vás provede pokročilým používáním editovatelných dokumentů pomocí GroupDocs.Editor, podrobně rozebere každý krok, abyste mohli plně využít jeho potenciál.

## Rychlé odpovědi
- **Jak mohu extrahovat obrázky z souboru DOCX?** Použijte `EditableDocument.Images` po načtení dokumentu pomocí `Editor`.
- **Mohu převést DOCX na HTML s vloženými zdroji?** Ano—voláním `EditableDocument.GetEmbeddedHtml()` nebo `GetContent()` získáte HTML značky.
- **Jaká metoda uloží upravený dokument jako HTML?** `EditableDocument.Save(htmlFilePath)` vytvoří HTML soubor se složkou zdrojů.
- **Je možné extrahovat písma z dokumentu Word?** Použijte `EditableDocument.Fonts` k získání všech zdrojů písem.
- **Potřebuji licenci pro produkční použití?** Je vyžadována platná licence GroupDocs.Editor; je k dispozici bezplatná zkušební verze.

## Co je **extrahovat obrázky z docx**?
Extrahování obrázků z souboru DOCX znamená programově získat každý obrázek vložený v dokumentu Word, abyste jej mohli znovu použít, upravit nebo uložit samostatně. GroupDocs.Editor zpřístupňuje kolekci `Images` na instanci `EditableDocument`, což usnadňuje tento úkol.

## Proč použít GroupDocs.Editor pro tento pracovní postup?
- **Plná kontrola** nad zdroji dokumentu (obrázky, písma, CSS) bez ručního zpracování ZIP.  
- **Bezproblémová konverze** z DOCX do HTML při zachování rozvržení a stylování.  
- **Jednoduché získávání zdrojů** pro vlastní zpracování obrázků, vkládání písem nebo doručování přes CDN.  
- **Robustní vzor uvolňování** zajišťuje, že v dlouhodobě běžících službách nedochází k únikům paměti.

## Předpoklady
- Visual Studio nainstalovaný na vašem vývojovém počítači.  
- .NET Framework kompatibilní s GroupDocs.Editor.  
- Knihovna GroupDocs.Editor pro .NET. Můžete ji [stáhnout zde](https://releases.groupdocs.com/editor/net/).  
- Platná licence GroupDocs.Editor. Můžete získat [bezplatnou zkušební verzi](https://releases.groupdocs.com/) nebo zakoupit [dočasnou licenci](https://purchase.groupdocs.com/temporary-license/).

## Importovat jmenné prostory
Nejprve se ujistěte, že ve svém .NET projektu importujete potřebné jmenné prostory:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```

## Krok 1: Vytvoření instance EditableDocument
Nejprve musíte vytvořit instanci `EditableDocument` načtením a úpravou vstupního dokumentu podporovaného formátu.

```csharp
string inputFilePath = "YourSampleDocument.docx";
Editor editor = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```

V tomto kroku načteme vstupní dokument a připravíme jej k úpravám.

## Jak **extrahovat obrázky z DOCX**?
Níže se ponoříme do možností získávání zdrojů, počínaje nejčastější potřebou—získáním všech obrázků z Word souboru.

## Krok 2: Získávání zdrojů dokumentu
`EditableDocument` obsahuje různé zdroje, které lze získat a manipulovat s nimi. Pojďme si je rozdělit:

### Krok 2.1: Získat celý dokument jako HTML
Můžete vygenerovat jeden řetězec, který obsahuje celý dokument se všemi jeho zdroji vloženými jako HTML.

```csharp
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```

Tento řetězec bude poměrně velký, protože zahrnuje styly, obrázky a písma kódované v base64.

### Krok 2.2: Získat všechny obrázky *(primární klíčové slovo v akci)*
Získat všechny obrázky z dokumentu—toto je jádro **extrahovat obrázky z docx**.

```csharp
List<IImageResource> allImages = beforeEdit.Images;
```

### Krok 2.3: Získat všechna písma *(sekundární klíčové slovo)*
Pokud také potřebujete **extrahovat písma z Wordu**, použijte následující volání:

```csharp
List<FontResourceBase> allFonts = beforeEdit.Fonts;
```

### Krok 2.4: Získat všechny styly
Získat všechny styly v textovém formátu.

```csharp
List<CssText> allStylesheets = beforeEdit.Css;
```

### Krok 2.5: Shromáždit všechny zdroje
Shromáždit všechny zdroje jedním voláním.

```csharp
List<IHtmlResource> allResources = beforeEdit.AllResources;
```

To zahrnuje obrázky, písma a styly.

### Krok 2.6: Získat HTML značky
Získat HTML značky dokumentu bez vložených zdrojů.

```csharp
string htmlMarkup = beforeEdit.GetContent();
```

## Jak **převést docx na html** s vlastním zpracováním?
Někdy je potřeba upravit externí odkazy, aby směřovaly na vaše vlastní obslužné programy zdrojů.

## Krok 3: Úprava externích odkazů
### Krok 3.1: Připravit vlastní předpony
Připravte předpony, které budou připojeny před původní externí odkazy.

```csharp
string customImagesRequesthandlerUri = "http://example.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://example.com/CssHandler/id=";
string customFontsRequesthandlerUri = "http://example.com/FontsHandler/id=";
```

### Krok 3.2: Vygenerovat HTML značky s předponou
Vygenerujte HTML značky s upravenými odkazy.

```csharp
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```

### Krok 3.3: Získat obsah HTML pouze s tělem
Některé WYSIWYG editory zpracovávají pouze čisté HTML značky bez hlaviček.

```csharp
string onlyBodyContent = beforeEdit.GetBodyContent();
```

### Krok 3.4: Obsah pouze s tělem s předponou
Vygenerujte obsah pouze s tělem s vlastními předponami obrázků.

```csharp
string prefixedBodyContent = beforeEdit.GetBodyContent(customImagesRequesthandlerUri);
```

### Krok 3.5: Získat styly
Získat styly použité v dokumentu.

```csharp
List<string> stylesheets = beforeEdit.GetCssContent();
```

### Krok 3.6: Styly s předponou
Získat styly s vlastními předponami.

```csharp
List<string> prefixedStylesheets = beforeEdit.GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri);
```

## Jak **uložit dokument jako html** správně?
## Krok 4: Uložit dokument jako HTML
Uložte upravený dokument jako HTML soubor, včetně jeho zdrojů.

```csharp
string htmlFilePath = Path.Combine("output", Path.GetFileNameWithoutExtension(inputFilePath) + ".html");
beforeEdit.Save(htmlFilePath);
```

Tato metoda vytvoří samostatný adresář pro zdroje jako styly, obrázky a písma.

## Krok 5: Uvolnění EditableDocument
`EditableDocument` implementuje `IDisposable` a poskytuje možnost zkontrolovat, zda je instance uvolněna.

```csharp
Console.WriteLine("EditableDocument is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");
```

### Krok 5.1 Zpracování události Dispose
Můžete se také přihlásit k události disposing.

```csharp
EventHandler someMethod = delegate { Console.WriteLine("Disposing event was spotted!"); };
beforeEdit.Disposed += someMethod;
```

## Krok 6: Vytvoření EditableDocument z HTML
Vytvořte instanci `EditableDocument` z HTML dokumentu.

### Krok 6.1: Z HTML souboru

```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
```

### Krok 6.2: Z HTML značek

```csharp
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);
```

Tyto instance (`afterEditFromFile` a `afterEditFromMarkup`) jsou identické s originálem (`beforeEdit`).

## Krok 7: Manuální uvolnění
Manuálně uvolněte své instance `EditableDocument`.

```csharp
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```

To zajišťuje řádné vyčištění zdrojů.

## Časté problémy a řešení
- **Obrázky se po extrakci nezobrazují:** Ověřte, že dokument skutečně obsahuje vložené obrázky a že přistupujete k `beforeEdit.Images` po volání `Edit`.  
- **Písma chybí ve výstupu HTML:** Ujistěte se, že voláte `GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri)`, aby byly URL písem správně vloženy.  
- **Velké HTML řetězce způsobují tlak na paměť:** Použijte `GetContent()` pro značky bez vložených zdrojů a poskytujte obrázky/CSS ze samostatných souborů.

## Často kladené otázky
**Q: Jaké formáty GroupDocs.Editor podporuje?**  
A: GroupDocs.Editor podporuje DOCX, XLSX, PPTX a mnoho dalších populárních kancelářských formátů.

**Q: Mohu používat GroupDocs.Editor bez licence?**  
A: Ano, můžete jej používat s [bezplatnou zkušební verzí](https://releases.groupdocs.com/) nebo s [dočasnou licencí](https://purchase.groupdocs.com/temporary-license/).

**Q: Jak mohu extrahovat konkrétní zdroje z dokumentu?**  
A: Použijte kolekce `Images`, `Fonts` a `Css` na instanci `EditableDocument`.

**Q: Je možné upravit odkazy ve výstupu HTML?**  
A: Ano, předávejte vlastní URI předpony do `GetContent` nebo `GetBodyContent`, aby se přepsaly odkazy na obrázky, CSS a písma.

**Q: Jak uložit upravený dokument jako HTML soubor?**  
A: Zavolejte metodu `Save` na instanci `EditableDocument` a zadejte cestu k souboru končící na `.html`.

---

**Poslední aktualizace:** 2026-03-14  
**Testováno s:** GroupDocs.Editor pro .NET (nejnovější verze)  
**Autor:** GroupDocs