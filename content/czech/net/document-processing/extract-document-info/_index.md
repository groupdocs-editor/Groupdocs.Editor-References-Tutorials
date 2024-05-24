---
title: Extrahujte informace o dokumentu
linktitle: Extrahujte informace o dokumentu
second_title: GroupDocs.Editor .NET API
description: Naučte se, jak extrahovat informace o dokumentu pomocí GroupDocs.Editor pro .NET s naším podrobným, podrobným návodem. Ideální pro správu různých typů dokumentů.
type: docs
weight: 10
url: /cs/net/document-processing/extract-document-info/
---
## Úvod
Vítejte v tomto komplexním tutoriálu o extrahování informací o dokumentu pomocí GroupDocs.Editor pro .NET. V této příručce vás provedeme procesem krok za krokem, přičemž se ujistíme, že každé části rozumíte jasně a stručně. Ať už jste zkušený vývojář nebo teprve začínáte, tento tutoriál vám pomůže bezproblémově integrovat GroupDocs.Editor do vašich projektů .NET, abyste mohli efektivně spravovat a manipulovat s dokumenty.
## Předpoklady
Než se ponoříte do kódu, ujistěte se, že máte vše, co potřebujete:
- Základní znalost C#: Pochopení základů programování v C# je nezbytné.
- Visual Studio: Ujistěte se, že máte nainstalované Visual Studio.
-  GroupDocs.Editor pro .NET: Budete potřebovat knihovnu GroupDocs.Editor pro .NET. Můžete si jej stáhnout z[stránka ke stažení](https://releases.groupdocs.com/editor/net/).
## Importovat jmenné prostory
Chcete-li začít, budete muset importovat potřebné jmenné prostory. To vám umožní přístup ke třídám a metodám potřebným pro manipulaci s dokumenty.
```csharp
using System;
using GroupDocs.Editor.Metadata;
```
## Krok 1: Vložte svůj dokument
Nejprve musíte načíst dokument, ze kterého chcete extrahovat informace. To lze provést zadáním cesty souboru k dokumentu.
```csharp
string docxInputFilePath = "YourSampleDocument.docx";
Editor editorDocx = new Editor(docxInputFilePath);
```
## Krok 2: Načtěte informace o dokumentu
 Dále získáte informace o dokumentu pomocí`GetDocumentInfo` metoda. Pokud si nejste jisti formátem dokumentu, tato metoda nevyžaduje žádné specifické možnosti načítání.
```csharp
IDocumentInfo infoDocx = editorDocx.GetDocumentInfo(null);
```
## Krok 3: Určete typ dokumentu
Nyní musíte zkontrolovat typ dokumentu, se kterým máte co do činění. To je zásadní, protože určuje, jak budete s dokumentem nakládat.
```csharp
bool isSpreadsheet = infoDocx is SpreadsheetDocumentInfo;
bool isText = infoDocx is TextualDocumentInfo;
bool isWordProcessing = infoDocx is WordProcessingDocumentInfo;
Console.WriteLine($"Is '{docxInputFilePath}' a Spreadsheet: {isSpreadsheet}");
Console.WriteLine($"Is '{docxInputFilePath}' a Textual document: {isText}");
Console.WriteLine($"Is '{docxInputFilePath}' a WordProcessing document: {isWordProcessing}");
```
## Krok 4: Extrahujte podrobné informace
Pokud je dokument textovým dokumentem, můžete extrahovat podrobné informace, jako je formát, přípona, počet stránek, velikost a zda je zašifrován.
```csharp
if (isWordProcessing)
{
    WordProcessingDocumentInfo casted = (WordProcessingDocumentInfo)infoDocx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Page count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```
## Krok 5: Opakujte pro různé typy dokumentů
Opakujte stejné kroky pro další typy dokumentů, jako jsou tabulky a textové dokumenty.
```csharp
string xlsxInputFilePath = "YourSampleDocument.xlsx";
Editor editorXlsx = new Editor(xlsxInputFilePath);
IDocumentInfo infoXlsx = editorXlsx.GetDocumentInfo(null);
bool isXlsxSpreadsheet = infoXlsx is SpreadsheetDocumentInfo;
Console.WriteLine($"Is '{xlsxInputFilePath}' a Spreadsheet: {isXlsxSpreadsheet}");
if (isXlsxSpreadsheet)
{
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo)infoXlsx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Tabs count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```
## Krok 6: Práce s dokumenty chráněnými heslem
Při práci s dokumenty chráněnými heslem byste se měli nejprve pokusit je otevřít bez hesla, poté s nesprávným heslem a nakonec se správným heslem.
```csharp
string xlsInputFilePath = "YourSampleDocument.xls";
Editor editorXls = new Editor(xlsInputFilePath);
try
{
    IDocumentInfo infoXls = editorXls.GetDocumentInfo(null);
}
catch (PasswordRequiredException)
{
    Console.WriteLine("This document is password-protected.");
}
try
{
    IDocumentInfo infoXls = editorXls.GetDocumentInfo("incorrect_password");
}
catch (IncorrectPasswordException)
{
    Console.WriteLine("The provided password is incorrect.");
}
IDocumentInfo infoXlsValid = editorXls.GetDocumentInfo("correct_password");
bool isXlsSpreadsheet = infoXlsValid is SpreadsheetDocumentInfo;
Console.WriteLine($"Password-protected document is a Spreadsheet: {isXlsSpreadsheet}");
if (isXlsSpreadsheet)
{
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo)infoXlsValid;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Tabs count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```
## Krok 7: Práce s textovými dokumenty
```csharp
string xmlInputFilePath = "YourSampleDocument.xml";
Editor editorXml = new Editor(xmlInputFilePath);
IDocumentInfo infoXml = editorXml.GetDocumentInfo(null);
bool isXmlText = infoXml is TextualDocumentInfo;
Console.WriteLine($"Is '{xmlInputFilePath}' a Textual document: {isXmlText}");
if (isXmlText)
{
    TextualDocumentInfo casted = (TextualDocumentInfo)infoXml;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Encoding: {casted.Encoding}; Size: {casted.Size} bytes");
}
```
## Krok 8: Zlikvidujte zdroje
Nakonec se ujistěte, že jste zlikvidovali všechny prostředky, abyste zabránili úniku paměti.
```csharp
editorDocx.Dispose();
editorXlsx.Dispose();
editorXls.Dispose();
editorXml.Dispose();
Console.WriteLine("ExtractingDocumentInfo routine has successfully finished");
```
## Závěr
Gratulujeme! Nyní jste se naučili, jak extrahovat informace o dokumentu pomocí GroupDocs.Editor pro .NET. Tato výkonná knihovna zjednodušuje správu a manipulaci s dokumenty a umožňuje bezproblémovou manipulaci s různými typy dokumentů. Ať už pracujete s textovými, tabulkovými nebo textovými dokumenty, GroupDocs.Editor poskytuje robustní řešení.
## FAQ
### Jaké typy dokumentů dokáže GroupDocs.Editor zpracovat?
GroupDocs.Editor dokáže zpracovávat různé typy dokumentů včetně textových dokumentů, tabulek a textových dokumentů.
### Může GroupDocs.Editor spravovat dokumenty chráněné heslem?
Ano, GroupDocs.Editor může spravovat dokumenty chráněné heslem. Dokáže identifikovat a otevřít tyto dokumenty se správným heslem.
### Je nutné zlikvidovat objekty Editoru?
Ano, je důležité zlikvidovat objekty Editoru, aby se uvolnily prostředky a zabránilo se únikům paměti.
### Mohu získat podrobné informace o formátu a velikosti dokumentu?
Absolutně! GroupDocs.Editor umožňuje extrahovat podrobné informace včetně formátu, rozšíření, velikosti, počtu stránek a stavu šifrování.
### Kde mohu získat podporu, pokud narazím na problémy?
 Můžete získat podporu od[Fórum podpory GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).