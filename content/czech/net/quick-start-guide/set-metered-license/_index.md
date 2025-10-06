---
title: Nastavte měřenou licenci
linktitle: Nastavte měřenou licenci
second_title: GroupDocs.Editor .NET API
description: Naučte se, jak integrovat a používat GroupDocs.Editor pro .NET pomocí našeho komplexního průvodce. Odemkněte výkonné funkce pro úpravu dokumentů ve svých aplikacích .NET.
weight: 12
url: /cs/net/quick-start-guide/set-metered-license/
type: docs
---
# Nastavte měřenou licenci

## Úvod
Vítejte v našem podrobném průvodci používáním GroupDocs.Editor pro .NET! Ať už jste zkušený vývojář nebo teprve začínáte, tento tutoriál vám pomůže využít plný potenciál této výkonné knihovny. GroupDocs.Editor pro .NET vám umožňuje bez námahy upravovat dokumenty různých formátů ve vašich aplikacích .NET. Pojďme se ponořit a prozkoumat, jak můžete začít s tímto robustním nástrojem.
## Předpoklady
Než přejdeme k technickým detailům, ujistěte se, že máte následující předpoklady:
- Základní znalost programování .NET: Znalost C# a .NET Framework.
- Nainstalované Visual Studio: Ujistěte se, že máte na svém počítači nainstalovanou nejnovější verzi sady Visual Studio.
-  GroupDocs.Editor pro .NET: Stáhněte si knihovnu z[stránka ke stažení](https://releases.groupdocs.com/editor/net/).
-  Platná licence: Získejte dočasnou nebo plnou licenci od[Nákupní stránka GroupDocs](https://purchase.groupdocs.com/temporary-license/).
## Importovat jmenné prostory
Chcete-li používat GroupDocs.Editor pro .NET, budete muset do projektu importovat potřebné jmenné prostory. Tento krok je zásadní, protože nastavuje váš projekt tak, aby využíval funkce knihovny.
```csharp
using System;
using GroupDocs.Editor;
```
Pojďme si každý příklad rozdělit do několika kroků, abyste se ujistili, že je budete snadno sledovat.
## Krok 1: Nainstalujte GroupDocs.Editor pro .NET
Nejprve musíte do svého projektu nainstalovat GroupDocs.Editor for .NET. Můžete to udělat prostřednictvím NuGet Package Manager v sadě Visual Studio.
### Nainstalujte přes NuGet Package Manager
1. Otevřete projekt v sadě Visual Studio.
2.  Jít do`Tools` >`NuGet Package Manager` >`Manage NuGet Packages for Solution`.
3.  Hledat`GroupDocs.Editor`.
4.  Klikněte na`Install`.
Tím do svého projektu přidáte potřebné tutorials.
## Krok 2: Nastavte měřenou licenci
Chcete-li odemknout všechny funkce aplikace GroupDocs.Editor, budete muset nastavit měřenou licenci. To vám umožňuje používat API bez jakýchkoli omezení.
### Nastavení měřené licence
1.  Získejte své veřejné a soukromé klíče z[Nákupní stránka GroupDocs](https://purchase.groupdocs.com/temporary-license/).
2. Chcete-li nastavit měřenou licenci, přidejte do svého projektu následující kód:
```csharp
string publicKey = "*****";
string privateKey = "*****";
Metered metered = new Metered();
metered.SetMeteredKey(publicKey, privateKey);
Console.WriteLine("License set successfully.");
```
## Krok 3: Načtěte a upravte dokument
Nyní, když je váš projekt nastaven a licencován, přejděme k načítání a úpravám dokumentu.
### Načítání dokumentu
1. Chcete-li načíst dokument, přidejte následující kód:
```csharp
string filePath = "sample.docx";
Editor editor = new Editor(filePath);
Console.WriteLine("Document loaded successfully.");
```
### Úprava dokumentu
2. Chcete-li dokument upravit, musíte jej převést do upravitelného formátu:
```csharp
EditableDocument editableDocument = editor.Edit();
string content = editableDocument.GetContent();
Console.WriteLine("Document converted to editable format.");
```
## Krok 4: Uložte upravený dokument
Po úpravě dokumentu je posledním krokem uložení změn.
### Uložení dokumentu
1. Převeďte upravený obsah zpět do původního formátu:
```csharp
string updatedContent = "<html><body>Updated content</body></html>";
editableDocument = EditableDocument.FromMarkup(updatedContent, new WordProcessingSaveOptions());
editor.Save(editableDocument, "updated_sample.docx");
Console.WriteLine("Document saved successfully.");
```
## Závěr
 Gratulujeme! Úspěšně jste integrovali a používali GroupDocs.Editor pro .NET ve své aplikaci. Od instalace knihovny po nastavení měřené licence a úpravy dokumentů jste probrali všechny základní kroky. Tento výkonný nástroj může výrazně zefektivnit vaše pracovní postupy při úpravě dokumentů ve vašich aplikacích .NET. Další informace naleznete v části[GroupDocs.Editor pro dokumentaci .NET](https://tutorials.groupdocs.com/editor/net/).
## FAQ
### Jak získám licenci GroupDocs.Editor?
 Licenci můžete získat od[Nákupní stránka GroupDocs](https://purchase.groupdocs.com/buy) . Chcete-li získat dočasnou licenci, navštivte[tady](https://purchase.groupdocs.com/temporary-license/).
### Mohu vyzkoušet GroupDocs.Editor zdarma?
 Ano, můžete si stáhnout bezplatnou zkušební verzi z[stránka ke stažení](https://releases.groupdocs.com/) a požádat o dočasnou licenci.
### Jaké formáty dokumentů podporuje GroupDocs.Editor?
 GroupDocs.Editor podporuje různé formáty včetně DOCX, PPTX, XLSX, TXT, HTML a dalších. Úplný seznam naleznete na[dokumentace](https://tutorials.groupdocs.com/editor/net/).
### Je pro GroupDocs.Editor k dispozici nějaká podpora komunity?
 Ano, můžete získat podporu komunity od[Fórum GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).
### Jak mohu začít s GroupDocs.Editor pro .NET?
 Postupujte podle našeho podrobného průvodce nastavením knihovny, získáním licence a zahájením úprav dokumentů. Podrobné pokyny naleznete na[dokumentace](https://tutorials.groupdocs.com/editor/net/).