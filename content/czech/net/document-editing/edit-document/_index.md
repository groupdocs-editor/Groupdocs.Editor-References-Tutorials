---
title: Upravit dokument
linktitle: Upravit dokument
second_title: GroupDocs.Editor .NET API
description: Naučte se snadno upravovat dokumenty s GroupDocs.Editor pro .NET. Podrobný průvodce pro textové a tabulkové soubory.
weight: 11
url: /cs/net/document-editing/edit-document/
---
## Úvod
Zapletli jste se někdy do složitých úprav dokumentů ve vašich aplikacích .NET? Neboj se! S GroupDocs.Editor pro .NET máte mocného spojence, který vám tento úkol zjednoduší. Tento komplexní průvodce vás provede tím, jak využít tento robustní nástroj k snadné úpravě dokumentů. Ať už se zabýváte textovými dokumenty nebo tabulkami, na konci tohoto tutoriálu budete GroupDocs.Editor procházet jako profesionál.
## Předpoklady
Než se pustíte do výukového programu, ujistěte se, že máte následující:
- Visual Studio: Nainstalované a připravené k použití.
- .NET Framework: Kompatibilní verze nainstalovaná ve vašem systému.
-  GroupDocs.Editor pro .NET: Můžete[stáhněte si nejnovější verzi](https://releases.groupdocs.com/editor/net/) a získat a[dočasná licence](https://purchase.groupdocs.com/temporary-license/) V případě potřeby.
- Základní znalost C#: Tato příručka předpokládá, že máte základní znalosti o vývoji C# a .NET.
## Importovat jmenné prostory
Chcete-li začít, musíte do projektu importovat potřebné jmenné prostory. Přidejte následující řádky na začátek souboru C#:
```csharp
using System.Collections.Generic;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.Options;
```
Nyní, když máte vše nastaveno, pojďme si proces úpravy dokumentu rozdělit na zvládnutelné kroky.
## Krok 1: Načtěte dokument pro zpracování textu
Nejprve načteme dokument Word Processing. Zde nasměrujete instanci Editoru na umístění vašeho dokumentu a v případě potřeby určíte jakékoli možnosti načtení.
### 1.1 Inicializujte editor s výchozími možnostmi
```csharp
string inputFilePath = "Your Sample Document"; // Cesta k vašemu dokumentu
Editor editor1 = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
```
Tento fragment kódu inicializuje instanci Editoru pomocí výchozích možností načtení pro dokument textového zpracování.
## Krok 2: Upravte dokument
Nyní můžeme přistoupit k úpravě načteného dokumentu. GroupDocs.Editor umožňuje upravit možnosti úprav tak, aby vyhovovaly vašim potřebám.
### 2.1 Upravit s výchozími možnostmi
```csharp
EditableDocument defaultWordProcessingDoc = editor1.Edit();
```
Úprava dokumentu s výchozími možnostmi je přímočará a vyžaduje minimální konfiguraci.
### 2.2 Upravit pomocí vlastních možností
Pojďme se ponořit do pokročilejších konfigurací zadáním vlastních možností úprav.
```csharp
WordProcessingEditOptions wordProcessingEditOptions1 = new WordProcessingEditOptions();
wordProcessingEditOptions1.EnablePagination = false;
wordProcessingEditOptions1.EnableLanguageInformation = true;
wordProcessingEditOptions1.FontExtraction = FontExtractionOptions.ExtractAllEmbedded;
EditableDocument version1WordProcessingDoc = editor1.Edit(wordProcessingEditOptions1);
```
tomto úryvku jsme zakázali stránkování, povolili jazykové informace a nastavili extrakci písem pro extrahování všech vložených písem.
### 2.3 Jiný příklad konfigurace
Dokument můžete také upravit pomocí jiné sady možností:
```csharp
WordProcessingEditOptions wordProcessingEditOptions2 = new WordProcessingEditOptions(true);
wordProcessingEditOptions2.FontExtraction = FontExtractionOptions.ExtractAll;
EditableDocument version2WordProcessingDoc = editor1.Edit(wordProcessingEditOptions2);
```
Zde jsme povolili stránkování a nastavili extrakci písem pro extrahování všech písem.
## Krok 3: Načtěte a upravte tabulku
Úpravy tabulek jsou s GroupDocs.Editor stejně přímočaré.
### 3.1 Vložte tabulku
```csharp
Editor editor2 = new Editor("Your Sample Document", delegate { return new SpreadsheetLoadOptions(); });
```
Tím se inicializuje instance Editoru pro tabulkový dokument.
### 3.2 Upravte první kartu
```csharp
SpreadsheetEditOptions sheetTab1EditOptions = new SpreadsheetEditOptions();
sheetTab1EditOptions.WorksheetIndex = 0; // Index je založen na 0, takže toto je první karta
EditableDocument firstTab = editor2.Edit(sheetTab1EditOptions);
```
Pomocí zadaných možností můžete upravit první kartu tabulky.
### 3.3 Upravte druhou záložku
```csharp
SpreadsheetEditOptions sheetTab2EditOptions = new SpreadsheetEditOptions();
sheetTab2EditOptions.WorksheetIndex = 1; // Index je založen na 0, takže toto je druhá karta
EditableDocument secondTab = editor2.Edit(sheetTab2EditOptions);
```
Podobně tento fragment kódu upravuje druhou kartu tabulky.
## Krok 4: Extrahování obsahu
Jakmile dokument upravíte, možná budete muset extrahovat jeho obsah. GroupDocs.Editor k tomu poskytuje různé metody.
### 4.1 Získání obsahu HTML
```csharp
string bodyContent = firstTab.GetBodyContent(); // Označení HTML z prvku HTML->BODY
string allContent = firstTab.GetContent(); // Plné HTML značení všech dokumentů, včetně HTML->HEAD hlavičky a jejího obsahu
```
Tento kód extrahuje obsah HTML upravovaného dokumentu.
### 4.2 Extrahovat zdroje
```csharp
List<IImageResource> onlyImages = firstTab.Images;
List<IHtmlResource> allResourcesTogether = firstTab.AllResources;
```
Zde můžete z dokumentu extrahovat obrázky a všechny další zdroje HTML.
## Krok 5: Vyčistěte
Nezapomeňte zlikvidovat všechny instance, abyste uvolnili zdroje.
```csharp
defaultWordProcessingDoc.Dispose();
version1WordProcessingDoc.Dispose();
version2WordProcessingDoc.Dispose();
firstTab.Dispose();
secondTab.Dispose();
editor1.Dispose();
editor2.Dispose();
```
Správná likvidace zajišťuje, že ve vaší aplikaci nedochází k únikům paměti nebo problémům s výkonem.
## Závěr
 Gratulujeme! Nyní dobře rozumíte tomu, jak používat GroupDocs.Editor pro .NET k načítání, úpravám a extrahování obsahu z dokumentů textového procesoru a tabulek. Tento výkonný nástroj zjednodušuje úlohy úpravy dokumentů a hladce se integruje s vašimi aplikacemi .NET. Pro další podrobnosti můžete prozkoumat[dokumentace](https://tutorials.groupdocs.com/editor/net/), [stáhněte si nejnovější verzi](https://releases.groupdocs.com/editor/net/) nebo získat a[dočasná licence](https://purchase.groupdocs.com/temporary-license/).
## FAQ
### Mohu upravovat dokumenty PDF pomocí GroupDocs.Editor pro .NET?
současné době GroupDocs.Editor for .NET primárně podporuje formáty Word Processing, Spreadsheet a Presentation.
### Jak efektivně zpracovávat velké dokumenty?
Využijte možnosti úprav k načtení a zpracování pouze nezbytných částí dokumentu a zajistěte správnou likvidaci instancí pro správu paměti.
### Existuje omezení velikosti dokumentu, kterou mohu upravovat?
Neexistují žádná přísná omezení velikosti, ale výkon závisí na možnostech vašeho systému.
### Mohu dále upravit výstup HTML?
Ano, GroupDocs.Editor umožňuje rozsáhlé přizpůsobení výstupu HTML pomocí různých možností a nastavení.
### Kde mohu získat podporu, pokud narazím na problémy?
 Můžete navštívit[Fórum podpory GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20) za pomoc a pomoc.