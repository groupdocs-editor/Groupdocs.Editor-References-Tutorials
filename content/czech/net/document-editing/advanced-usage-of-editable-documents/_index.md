---
title: Pokročilé použití upravitelných dokumentů
linktitle: Pokročilé použití upravitelných dokumentů
second_title: GroupDocs.Editor .NET API
description: Naučte se pokročilé používání GroupDocs.Editor pro .NET vytváření, úpravy a extrahování zdrojů z dokumentů programově.
weight: 11
url: /cs/net/document-editing/advanced-usage-of-editable-documents/
---
## Úvod
Pokud jste vývojář .NET a chcete vylepšit své možnosti úpravy dokumentů, GroupDocs.Editor pro .NET nabízí výkonnou sadu nástrojů. Tento komplexní průvodce vás provede pokročilým používáním upravitelných dokumentů pomocí GroupDocs.Editor a podrobně rozebere každý krok, abyste zajistili, že budete moci využít jeho plný potenciál.
## Předpoklady
Než se ponoříte do pokročilých funkcí, ujistěte se, že máte následující:
- Visual Studio nainstalované na vašem vývojovém počítači.
- .NET Framework kompatibilní s GroupDocs.Editor.
-  GroupDocs.Editor pro knihovnu .NET. Můžeš[stáhněte si jej zde](https://releases.groupdocs.com/editor/net/).
-  Platná licence GroupDocs.Editor. Můžete získat a[zkušební verze zdarma](https://releases.groupdocs.com/) nebo koupit a[dočasná licence](https://purchase.groupdocs.com/temporary-license/).
## Importovat jmenné prostory
Nejprve se ujistěte, že do svého projektu .NET importujete potřebné jmenné prostory:
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
 Nejprve musíte vytvořit instanci`EditableDocument` načtením a úpravou vstupního dokumentu podporovaného formátu.
```csharp
string inputFilePath = "YourSampleDocument.docx";
Editor editor = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```
V tomto kroku načteme vstupní dokument a připravíme jej k editaci.
## Krok 2: Extrahování zdrojů dokumentů
 The`EditableDocument` obsahuje různé zdroje, které lze extrahovat a manipulovat s nimi. Pojďme si je rozebrat:
### Krok 2.1: Extrahujte celý dokument jako HTML
Můžete vygenerovat jeden řetězec, který obsahuje celý dokument se všemi jeho prostředky vloženými jako HTML.
```csharp
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```
Tento řetězec bude poměrně velký, protože obsahuje šablony stylů, obrázky a fonty zakódované v base64.
### Krok 2.2: Extrahujte všechny obrázky
Extrahujte všechny obrázky z dokumentu.
```csharp
List<IImageResource> allImages = beforeEdit.Images;
```
### Krok 2.3: Extrahujte všechna písma
Extrahujte všechna písma použitá v dokumentu.
```csharp
List<FontResourceBase> allFonts = beforeEdit.Fonts;
```
### Krok 2.4: Extrahujte všechny šablony stylů
Extrahujte všechny šablony stylů v textovém formátu.
```csharp
List<CssText> allStylesheets = beforeEdit.Css;
```
### Krok 2.5: Shromážděte všechny zdroje
Shromážděte všechny zdroje v jednom hovoru.
```csharp
List<IHtmlResource> allResources = beforeEdit.AllResources;
```
To zahrnuje obrázky, písma a šablony stylů.
### Krok 2.6: Získejte značky HTML
Získejte označení HTML dokumentu bez vložených zdrojů.
```csharp
string htmlMarkup = beforeEdit.GetContent();
```
## Krok 3: Úprava externích odkazů
Někdy je potřeba upravit externí odkazy tak, aby ukazovaly na vlastní obslužný program zdrojů. Jak na to:
### Krok 3.1: Připravte si vlastní předpony
Připravte si předpony, které předřadí původní externí odkazy.
```csharp
string customImagesRequesthandlerUri = "http://example.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://example.com/CssHandler/id=";
string customFontsRequesthandlerUri = "http://example.com/FontsHandler/id=";
```
### Krok 3.2: Vygenerujte značku HTML s předponou
Vygenerujte HTML značky s upravenými odkazy.
```csharp
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```
### Krok 3.3: Získejte obsah HTML pouze pro tělo
Některé WYSIWYG editory zpracovávají pouze čisté HTML značky bez záhlaví.
```csharp
string onlyBodyContent = beforeEdit.GetBodyContent();
```
### Krok 3.4: Obsah pouze pro tělo s předponou
Vytvářejte obsah pouze pro tělo s vlastními předponami obrázků.
```csharp
string prefixedBodyContent = beforeEdit.GetBodyContent(customImagesRequesthandlerUri);
```
### Krok 3.5: Extrahujte šablony stylů
Extrahujte šablony stylů použité v dokumentu.
```csharp
List<string> stylesheets = beforeEdit.GetCssContent();
```
### Krok 3.6: Předdefinované šablony stylů
Extrahujte šablony stylů s vlastními předponami.
```csharp
List<string> prefixedStylesheets = beforeEdit.GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri);
```
## Krok 4: Uložte dokument jako HTML
Upravený dokument uložte jako soubor HTML včetně jeho prostředků.
```csharp
string htmlFilePath = Path.Combine("output", Path.GetFileNameWithoutExtension(inputFilePath) + ".html");
beforeEdit.Save(htmlFilePath);
```
Tato metoda vytvoří samostatný adresář pro zdroje, jako jsou šablony stylů, obrázky a písma.
## Krok 5: Likvidace EditableDocumentu
 EditableDocument implementuje`IDisposable` a poskytuje možnost zkontrolovat, zda je instance vyřazena.
```csharp
Console.WriteLine("EditableDocument is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");
```
### Krok 5.1 Zpracování události likvidace
Můžete se také přihlásit k odběru likvidační akce.
```csharp
EventHandler someMethod = delegate { Console.WriteLine("Disposing event was spotted!"); };
beforeEdit.Disposed += someMethod;
```
## Krok 6: Vytvoření EditableDocument z HTML
Vytvořte instanci EditableDocument z dokumentu HTML.
### Krok 6.1: Ze souboru HTML
```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
```
### Krok 6.2: Z HTML Markup
```csharp
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);
```
Tyto instance (afterEditFromFile a afterEditFromMarkup) jsou totožné s originálem (beforeEdit).
## Krok 7: Ruční likvidace
Ručně zlikvidujte své instance EditableDocument.
```csharp
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```
To zajišťuje řádné čištění zdrojů.
## Závěr
GroupDocs.Editor pro .NET poskytuje robustní nástroje pro programovou úpravu dokumentů. Podle tohoto podrobného průvodce můžete efektivně spravovat obsah dokumentu, zdroje a výstupní formáty. Ať už vkládáte zdroje, upravujete externí odkazy nebo převádíte dokumenty do HTML, GroupDocs.Editor vás vybaví funkcemi potřebnými pro pokročilou manipulaci s dokumenty.
## FAQ
### Jaké formáty podporuje GroupDocs.Editor?
GroupDocs.Editor podporuje různé formáty včetně DOCX, XLSX, PPTX a dalších.
### Mohu používat GroupDocs.Editor bez licence?
 Ano, můžete jej použít s a[zkušební verze zdarma](https://releases.groupdocs.com/) nebo a[dočasná licence](https://purchase.groupdocs.com/temporary-license/).
### Jak extrahuji konkrétní zdroje z dokumentu?
 Obrázky, písma a šablony stylů můžete extrahovat pomocí poskytnutých metod, jako je např`Images`, `Fonts` , a`Css`.
### Je možné upravit odkazy ve výstupu HTML?
Ano, externí odkazy můžete upravit zadáním vlastních předpon pro obrázky, CSS a písma.
### Jak uložím upravený dokument jako soubor HTML?
 Použijte`Save` metoda`EditableDocument`třídy k uložení dokumentu jako souboru HTML včetně jeho prostředků.