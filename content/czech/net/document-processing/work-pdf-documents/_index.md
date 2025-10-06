---
title: Práce s dokumenty PDF
linktitle: Práce s dokumenty PDF
second_title: GroupDocs.Editor .NET API
description: V tomto kurzu se dozvíte, jak upravovat dokumenty PDF pomocí GroupDocs.Editor pro .NET. Upravujte obsah, manipulujte s velkými soubory a bezpečně ukládejte své úpravy.
weight: 14
url: /cs/net/document-processing/work-pdf-documents/
type: docs
---
# Práce s dokumenty PDF

## Úvod
Hledáte komplexního průvodce pro manipulaci a úpravu dokumentů PDF pomocí GroupDocs.Editor pro .NET? Jste na správném místě! V tomto tutoriálu vás provedeme celým procesem, od nastavení projektu až po uložení upraveného dokumentu PDF. Ať už jste zkušený vývojář nebo teprve začínáte, tato příručka vám bude užitečná a snadno se budete řídit. Pojďme se ponořit!
## Předpoklady
Než začneme, budete potřebovat několik věcí:
1. Vývojové prostředí .NET: Ujistěte se, že máte nastavené vývojové prostředí .NET. Může to být Visual Studio nebo jakékoli jiné preferované IDE.
2. GroupDocs.Editor pro .NET: Stáhněte a nainstalujte knihovnu GroupDocs.Editor pro .NET. Můžete to získat z[stránka vydání](https://releases.groupdocs.com/editor/net/).
3. Základní porozumění C#: Znalost programování v C# bude prospěšná, protože tento tutoriál zahrnuje psaní a porozumění kódu C#.
## Importovat jmenné prostory
Před napsáním jakéhokoli kódu se ujistěte, že máte do projektu importovány potřebné jmenné prostory:
```csharp
using System;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Reflection;
```
## Krok 1: Získejte cestu ke vstupnímu souboru
Nejprve musíte zadat cestu k dokumentu PDF. Pro tento tutoriál budeme předpokládat, že máte vzorový soubor PDF.
```csharp
string inputFilePath = "Your Sample Document.pdf";
```
## Krok 2: Vytvořte stream z cesty
Dále vytvořte datový proud souboru ze zadané cesty. Tento proud bude použit ke čtení dokumentu PDF.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
```
## Krok 3: Vytvořte možnosti načtení pro dokument
Chcete-li načíst dokument PDF, musíte určit možnosti načtení. Pokud je váš PDF chráněn heslem, můžete heslo zadat zde.
```csharp
Options.PdfLoadOptions loadOptions = new PdfLoadOptions();
// Pokud je dokument chráněn heslem
loadOptions.Password = "your_password";
```
## Krok 4: Načtěte dokument do instance editoru
Nyní použijte možnosti toku souboru a načtení k načtení dokumentu do souboru`Editor` instance.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    var documentInfo = editor.GetDocumentInfo(null);
```
## Krok 5: Vytvořte možnosti úprav
Nastavte možnosti úprav dokumentu. V tomto případě povolíme režim stránkování.
```csharp
Options.PdfEditOptions editOptions = new PdfEditOptions();
editOptions.EnablePagination = true;
```
## Krok 6: Vytvořte přechodný upravitelný dokument
Vytvořte přechodný upravitelný dokument pomocí instance editoru a možností úprav.
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
{
    // Extrahujte textový obsah jako značku HTML
    string originalContent = beforeEdit.GetContent();
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## Krok 7: Upravte obsah
Podle potřeby upravte obsah dokumentu. Zde jednoduše nahrazujeme slovo v dokumentu.
```csharp
string editedContent = originalContent.Replace("document", "edited document");
```
## Krok 8: Vytvořte nový upravitelný dokument s upraveným obsahem
 Vytvoř nový`EditableDocument` instance s upraveným obsahem a zdroji.
```csharp
using (EditableDocument afterEdit = EditableDocument.FromMarkup(editedContent, allResources))
{
    string originalContent3 = afterEdit.GetContent();
```
## Krok 9: Vytvořte možnosti uložení dokumentu
Určete možnosti uložení pro dokument PDF. Můžete také nastavit heslo pro výstupní dokument.
```csharp
FixedLayoutFormats docmFormat = FixedLayoutFormats.Pdf;
Options.PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.Password = "output_password";
saveOptions.OptimizeMemoryUsage = true;
```
## Krok 10: Uložte upravený dokument
Nakonec upravený dokument uložte do zadané výstupní cesty.
```csharp
string outputFilename = Path.GetFileNameWithoutExtension(inputFilePath) + "." + docmFormat.Extension;
string outputPath = Path.Combine("OutputDirectoryPath", outputFilename);
using (FileStream outputStream = File.Create(outputPath))
{
    editor.Save(afterEdit, outputStream, saveOptions);
}
```

## Závěr
Tady to máš! Podle těchto kroků můžete úspěšně upravovat dokumenty PDF pomocí GroupDocs.Editor pro .NET. Tato výkonná knihovna usnadňuje manipulaci a programové ukládání souborů PDF. Ať už provádíte jednoduché nahrazování textu nebo složitější úpravy, GroupDocs.Editor pro .NET vás pokryje.
## FAQ
### Mohu použít GroupDocs.Editor pro .NET k úpravě jiných formátů dokumentů?
Ano, GroupDocs.Editor pro .NET podporuje různé formáty dokumentů včetně Wordu, Excelu, PowerPointu a dalších.
### Jak mohu získat bezplatnou zkušební verzi GroupDocs.Editor pro .NET?
 Můžete si stáhnout bezplatnou zkušební verzi z[Bezplatná zkušební stránka GroupDocs.Editor](https://releases.groupdocs.com/).
### Je možné zpracovávat velké PDF dokumenty s GroupDocs.Editor pro .NET?
Ano, GroupDocs.Editor for .NET obsahuje možnosti pro optimalizaci využití paměti, takže je vhodný pro zpracování velkých dokumentů.
### Jak získám podporu, pokud narazím na problémy?
 Pro podporu můžete navštívit[Fórum podpory GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).
### Mohu dokument PDF při ukládání zašifrovat?
Ano, můžete nastavit heslo pro šifrování dokumentu PDF během procesu ukládání pomocí`PdfSaveOptions.Password` vlastnictví.