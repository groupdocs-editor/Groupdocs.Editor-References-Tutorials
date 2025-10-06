---
title: Práce s tabulkami chráněnými heslem
linktitle: Práce s tabulkami chráněnými heslem
second_title: GroupDocs.Editor .NET API
description: Naučte se pracovat s tabulkami chráněnými heslem pomocí GroupDocs.Editor pro .NET. Tento podrobný průvodce vás provede otevřením a uložením zabezpečených souborů Excel.
weight: 18
url: /cs/net/document-processing/work-password-protected-spreadsheets/
type: docs
---
# Práce s tabulkami chráněnými heslem

## Úvod
Máte potíže se správou tabulek chráněných heslem ve svých aplikacích .NET? Pokud ano, jste na správném místě! V tomto komplexním průvodci vás provedeme procesem používání GroupDocs.Editoru pro .NET k efektivnímu zpracování tabulek chráněných heslem. Na konci tohoto tutoriálu budete dobře vybaveni k snadnému otevírání, úpravám a ukládání šifrovaných souborů aplikace Excel.
## Předpoklady
Než se ponoříte do kódu, ujistěte se, že máte vše, co potřebujete:
- Základní znalost C#: Tento tutoriál předpokládá, že jste obeznámeni s programováním v C#.
- .NET Framework: Ujistěte se, že máte na vývojovém počítači nainstalovaný .NET Framework.
-  GroupDocs.Editor pro .NET: Stáhněte a nainstalujte GroupDocs.Editor pro .NET z[tady](https://releases.groupdocs.com/editor/net/).
## Importovat jmenné prostory
Chcete-li začít, budete muset do svého projektu C# importovat potřebné jmenné prostory. Tyto jmenné prostory poskytují přístup k funkcím GroupDocs.Editoru.
```csharp
using System;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
## Krok 1: Získejte cestu ke vstupnímu souboru
Nejprve budete potřebovat cestu ke vstupnímu souboru. Pro tento příklad použijeme vzorový soubor Excel (`Your Sample Document`), který je chráněn heslem.
```csharp
string inputFilePath = "Your Sample Document";
```
## Krok 2: Pokuste se otevřít dokument bez hesla
Podívejme se, co se stane, když se pokusíme otevřít dokument bez zadání hesla.
```csharp
Editor editor = new Editor(inputFilePath);
try
{
    editor.Edit();
}
catch (GroupDocs.Editor.PasswordRequiredException)
{
    Console.WriteLine("Cannot edit the document because it is password-protected. A password is required.");
}
editor.Dispose();
```
## Krok 3: Zkuste zadat nesprávné heslo
Nyní zadáme nesprávné heslo, abychom ukázali, jak editor reaguje.
```csharp
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.Password = "incorrect_password";
editor = new Editor(inputFilePath, delegate { return loadOptions; });
try
{
    editor.Edit();
}
catch (GroupDocs.Editor.IncorrectPasswordException)
{
    Console.WriteLine("Cannot edit the document because the specified password is incorrect.");
}
editor.Dispose();
```
## Krok 4: Otevřete soubor se správným heslem
Zadejte správné heslo a soubor úspěšně otevřete.
```csharp
loadOptions.Password = "excel_password";
loadOptions.OptimizeMemoryUsage = true;
editor = new Editor(inputFilePath, delegate { return loadOptions; });
```
## Krok 5: Vytvořte a upravte možnosti úprav
Pro úpravu tabulky musíme vytvořit a upravit možnosti úprav.
```csharp
SpreadsheetEditOptions editOptions = new SpreadsheetEditOptions();
```
## Krok 6: Vytvořte Intermediate EditableDocument
 Dále vytvoříme meziprodukt`EditableDocument` což nám umožňuje provádět změny v tabulce.
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
{
    // Krok 7: Vytvořte možnosti uložení
    SpreadsheetFormats xlsmFormat = SpreadsheetFormats.Xlsm;
    SpreadsheetSaveOptions saveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
    // Krok 7.1: Nastavte nové heslo pro otevření
    saveOptions.Password = "new password";
    // Krok 7.2: Nastavte ochranu proti zápisu
    saveOptions.WorksheetProtection = new WorksheetProtection(WorksheetProtectionType.All, "write password");
    // Krok 8: Uložte dokument bez úprav
    //Krok 8.1: Připravte název výstupního souboru a cestu
    string outputFilename = Path.GetFileNameWithoutExtension(inputFilePath) + "." + xlsmFormat.Extension;
    string outputPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename);
    // Krok 8.2: Vytvořte výstupní proud
    using (FileStream outputStream = File.Create(outputPath))
    {
        // Krok 8.3: Uložit
        editor.Save(beforeEdit, outputStream, saveOptions);
    }
}
// Krok 9: Zlikvidujte instanci editoru
editor.Dispose();
Console.WriteLine("Successfully handled the password-protected spreadsheet. Editor instance has been disposed: {0}", editor.IsDisposed ? "Yes" : "No");
```
## Závěr
Gratulujeme! Úspěšně jste se naučili, jak zacházet s tabulkami chráněnými heslem pomocí GroupDocs.Editor pro .NET. Od pokusu o otevření dokumentu bez hesla až po jeho uložení s novým nastavením ochrany jste probrali všechny základní kroky. Tyto znalosti nepochybně rozšíří vaši schopnost spravovat zabezpečené dokumenty ve vašich aplikacích .NET.
## FAQ
### Co je GroupDocs.Editor pro .NET?
GroupDocs.Editor for .NET je výkonné rozhraní API pro úpravu dokumentů, které umožňuje vývojářům načítat, upravovat a ukládat různé formáty dokumentů v rámci aplikací .NET.
### Jak mohu získat dočasnou licenci pro GroupDocs.Editor?
 Dočasnou licenci můžete získat od[tady](https://purchase.groupdocs.com/temporary-license/) zhodnotit vlastnosti produktu.
### Je možné optimalizovat využití paměti při úpravě velkých dokumentů?
 Ano, optimalizaci paměti můžete povolit nastavením`OptimizeMemoryUsage` majetek do`true` možnostech zatížení.
### Mohu nastavit různá hesla pro otevírání a zápis do tabulky?
Absolutně! Pomocí možností uložení můžete nastavit samostatná hesla pro otevření dokumentu a pro ochranu proti zápisu.
### Kde najdu podrobnější dokumentaci?
 Máte přístup ke komplexní dokumentaci pro GroupDocs.Editor pro .NET[tady](https://tutorials.groupdocs.com/editor/net/).