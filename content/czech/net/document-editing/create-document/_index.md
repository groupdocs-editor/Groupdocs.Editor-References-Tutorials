---
title: Vytvořit dokument
linktitle: Vytvořit dokument
second_title: GroupDocs.Editor .NET API
description: Naučte se upravovat dokumenty Word, Excel, PowerPoint, e-knihy a e-maily pomocí GroupDocs.Editor pro .NET s tímto komplexním výukovým programem krok za krokem.
weight: 10
url: /cs/net/document-editing/create-document/
type: docs
---
# Vytvořit dokument

## Úvod
Už vás nebaví problémy, které přináší programová úprava různých typů dokumentů? GroupDocs.Editor pro .NET je zde pro zjednodušení procesu. Tento výkonný nástroj umožňuje vývojářům snadno upravovat různé formáty dokumentů, jako je Word, Excel, PowerPoint, e-knihy a e-maily. V tomto tutoriálu se ponoříme hluboko do toho, jak používat GroupDocs.Editor pro .NET k vytváření a úpravám dokumentů. Tento proces rozdělíme do snadno pochopitelných kroků, díky kterým bude přístupný, i když jste v tom nováčkem.
## Předpoklady
Než začneme, ujistěte se, že máte následující:
- Visual Studio nainstalované na vašem počítači.
- .NET Framework (4.0 nebo vyšší).
-  GroupDocs.Editor pro knihovnu .NET. Můžete si jej stáhnout z[tady](https://releases.groupdocs.com/editor/net/).
- Základní znalost programování v C#.
## Importovat jmenné prostory
Nejprve importujme potřebné jmenné prostory. Tím zpřístupníte požadované třídy a metody v naší aplikaci.
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using System.IO;
```
## Krok 1: Nastavení streamu
Nejprve musíme nastavit paměťový stream, který bude sloužit jako náš zástupný symbol pro obsah dokumentu.
```csharp
Stream memoryStream = Stream.Null;
```
## Krok 2: Funkce zpětného volání pro uložení dokumentu
Dále definujte funkci zpětného volání, která uloží nový proud dokumentů. Tato funkce je nezbytná pro zpracování výstupu procesu úpravy dokumentu.
```csharp
void SaveNewDocument(Stream resultStream)
{
    memoryStream = resultStream;
}
```
## Krok 3: Vytvoření a úprava dokumentu WordProcessing
 Nyní vytvoříme a upravíme dokument aplikace Word. Začneme vytvořením nového`Editor` instance pro dokumenty WordProcessing a upravte ji pomocí výchozích možností.
### Vytvořit a upravit s výchozími možnostmi
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    EditableDocument defaultWordProcessingDoc = editor.Edit();
}
```
### Vytvářejte a upravujte pomocí vlastních možností
Pro větší kontrolu můžeme zadat možnosti, jako je zakázání stránkování a extrahování vložených písem.
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    WordProcessingEditOptions wordProcessingEditOptions = new WordProcessingEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true,
        FontExtraction = FontExtractionOptions.ExtractAllEmbedded
    };
    EditableDocument editableWordProcessingDocument = editor.Edit(wordProcessingEditOptions);
}
```
## Krok 4: Vytvoření a úprava dokumentu tabulky
Podobně můžeme vytvořit a upravit dokument Excel. Zde je návod, jak to udělat.
### Vytvořit a upravit s výchozími možnostmi
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    EditableDocument defaultEditableSpreadsheetDocument = editor.Edit();
}
```
### Vytvářejte a upravujte pomocí vlastních možností
 Chcete-li cílit na konkrétní listy nebo vyloučit skryté, používáme`SpreadsheetEditOptions`.
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    SpreadsheetEditOptions spreadsheetEditOptions = new SpreadsheetEditOptions
    {
        WorksheetIndex = 0,
        ExcludeHiddenWorksheets = true
    };
    EditableDocument editableSpreadsheetDocument = editor.Edit(spreadsheetEditOptions);
}
```
## Krok 5: Vytvoření a úprava prezentačního dokumentu
Podporovány jsou také prezentace v PowerPointu. Pojďme se podívat, jak s nimi zacházet.
### Vytvořit a upravit s výchozími možnostmi
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    EditableDocument defaultEditablePresentationDocument = editor.Edit();
}
```
### Vytvářejte a upravujte pomocí vlastních možností
Úpravy můžete přizpůsobit zadáním voleb, jako je, který snímek se má zobrazit a zda zahrnout skryté snímky.
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    PresentationEditOptions presentationEditOptions = new PresentationEditOptions
    {
        ShowHiddenSlides = false,
        SlideNumber = 0
    };
    EditableDocument editablePresentationDocument = editor.Edit(presentationEditOptions);
}
```
## Krok 6: Vytvoření a úprava dokumentu elektronické knihy
GroupDocs.Editor také umožňuje upravovat formáty elektronických knih, jako je EPUB. Zde je návod, jak to můžete zvládnout.
### Vytvořit a upravit s výchozími možnostmi
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EditableDocument defaultEditableEbookDocument = editor.Edit();
}
```
### Vytvářejte a upravujte pomocí vlastních možností
Přizpůsobte si úpravy své e-knihy povolením nebo zakázáním stránkování a informací o jazyce.
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EbookEditOptions ebookEditOptions = new EbookEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true
    };
    EditableDocument editableEbookDocument = editor.Edit(ebookEditOptions);
}
```
## Krok 7: Vytvoření a úprava e-mailového dokumentu
Nakonec se podíváme na to, jak upravovat e-mailové dokumenty. To zahrnuje formáty jako EML.
### Vytvořit a upravit s výchozími možnostmi
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EditableDocument defaultEditableEmailDocument = editor.Edit();
}
```
### Vytvářejte a upravujte pomocí vlastních možností
Určete možnosti výstupu e-mailové zprávy pro řízení procesu úprav.
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EmailEditOptions emailEditOptions = new EmailEditOptions
    {
        MailMessageOutput = MailMessageOutput.All
    };
    EditableDocument editableEmailDocument = editor.Edit(emailEditOptions);
}
```
## Krok 8: Dokončení procesu
Po úpravě dokumentů je důležité správně zlikvidovat paměťový tok, aby se uvolnily zdroje.
```csharp
memoryStream.Dispose();
System.Console.WriteLine("CreateDocument routine has successfully finished");
```
## Závěr
GroupDocs.Editor for .NET je všestranný a výkonný nástroj, který může zjednodušit úlohu programové úpravy různých typů dokumentů. Podle tohoto podrobného průvodce můžete snadno vytvářet a upravovat dokumenty, ať už se jedná o soubory WordProcessing, tabulky, prezentace, e-knihy nebo e-maily. Ponořte se do dokumentace GroupDocs.Editor, kde najdete pokročilejší funkce a možnosti přizpůsobení.
## FAQ
### Jaké typy dokumentů mohu upravovat pomocí GroupDocs.Editor pro .NET?
Můžete upravovat širokou škálu dokumentů, včetně WordProcessing, tabulek, prezentací, e-knih a e-mailů.
### Je možné upravit možnosti úprav?
Ano, GroupDocs.Editor pro .NET umožňuje rozsáhlé přizpůsobení prostřednictvím různých možností úprav specifických pro každý typ dokumentu.
### Jak naložím s výstupem upravených dokumentů?
Pomocí funkce zpětného volání můžete uložit upravený tok dokumentů na požadované místo.
### Potřebuji licenci k používání GroupDocs.Editor pro .NET?
 Ano, můžete získat licenci od[tady](https://purchase.groupdocs.com/buy). Existuje také možnost dočasné licence.
### Kde najdu podrobnější dokumentaci?
 Podrobná dokumentace je k dispozici na[Stránka dokumentace GroupDocs.Editor pro .NET](https://tutorials.groupdocs.com/editor/net/).