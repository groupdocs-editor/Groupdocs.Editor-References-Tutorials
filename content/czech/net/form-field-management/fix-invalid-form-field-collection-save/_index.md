---
title: Opravte neplatnou kolekci polí formuláře a uložte
linktitle: Opravte neplatnou kolekci polí formuláře a uložte
second_title: GroupDocs.Editor .NET API
description: Přečtěte si, jak opravit neplatná pole formuláře v DOCX pomocí Groupdocs.Editor pro .NET. Postupujte podle tohoto průvodce, abyste se ujistili, že vaše dokumenty jsou bez chyb a bezpečně je uložte.
weight: 11
url: /cs/net/form-field-management/fix-invalid-form-field-collection-save/
---

# Opravte neplatnou kolekci polí formuláře a uložte

## Úvod
Vítejte! Pokud pracujete s poli formuláře v dokumentech a potýkáte se s problémy s neplatnými kolekcemi polí formuláře, jste na správném místě. V tomto tutoriálu se ponoříme do toho, jak opravit neplatná pole formuláře a uložit dokument pomocí Groupdocs.Editor pro .NET. Provedeme vás procesem krok za krokem a zajistíme, že budete mít všechny podrobnosti, které potřebujete k bezproblémovému fungování. Začněme!
## Předpoklady
Než se pustíme do kódu, je potřeba mít připraveno několik věcí:
-  Groupdocs.Editor pro .NET: Ujistěte se, že jste nainstalovali knihovnu Groupdocs.Editor pro .NET. Můžete si jej stáhnout[tady](https://releases.groupdocs.com/editor/net/).
- Vývojové prostředí: Měli byste mít nastavené vývojové prostředí .NET, jako je Visual Studio.
- Základní znalost C#: Tento tutoriál předpokládá, že máte základní znalosti o programování v C#.
## Importovat jmenné prostory
Nejprve musíte importovat potřebné jmenné prostory do vašeho projektu C#. Na začátek souboru kódu přidejte následující řádky:
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System;
using System.IO;
```
## Krok 1: Získejte cestu k vstupnímu souboru
Prvním krokem je zadat cestu k vašemu vstupnímu souboru. Tento soubor by měl být dokument DOCX obsahující pole formuláře.
```csharp
string inputFilePath = Constants.SampleLegacyFormFields_docx;
```
## Krok 2: Vytvořte stream z cesty k souboru
Dále vytvořte proud souboru pro čtení vstupního dokumentu. To vám umožní načíst dokument do editoru.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
```
## Krok 3: Vytvořte možnosti načtení pro dokument
V tomto kroku musíte pro dokument vytvořit možnosti načtení. Pokud je váš dokument chráněn heslem, můžete heslo zadat. V tomto příkladu dokument není chráněn, takže heslo je ignorováno.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
loadOptions.Password = "some_password_to_open_a_document";
```
## Krok 4: Načtěte dokument do instance editoru
Nyní načtěte dokument se zadanými možnostmi do instance Editoru. Zde budou probíhat hlavní operace s dokumentem.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
```
## Krok 4.1: Přečtěte si instanci FormFieldManager
 The`FormFieldManager` instance je odpovědná za správu polí formuláře v dokumentu. Chcete-li získat přístup k polím formuláře a manipulovat s nimi, budete si muset tuto instanci přečíst.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
## Krok 4.2: Přečtěte si FormFieldCollection
 The`FormFieldCollection` obsahuje všechna pole formuláře v dokumentu. Tuto sbírku si přečtete, abyste zkontrolovali a opravili neplatná pole formuláře.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
## Krok 4.3: Automaticky opravit neplatná pole formuláře
Pokuste se automaticky opravit všechna neplatná pole formuláře v dokumentu. Toto je předběžný krok k řešení zjevných problémů.
```csharp
fieldManager.FixInvalidFormFieldNames(new InvalidFormField[0]);
collection = fieldManager.FormFieldCollection;
```
## Krok 4.4: Zkontrolujte neplatná pole formuláře
Zkontrolujte, zda po pokusu o automatickou opravu nezůstala nějaká neplatná pole formuláře.
```csharp
bool hasInvalidFormFields = fieldManager.HasInvalidFormFields();
Console.WriteLine("FormFieldCollection contains invalid items: {0}", hasInvalidFormFields);
```
## Krok 4.4.1: Získejte všechny neplatné názvy polí formuláře
Načtěte názvy všech neplatných polí formuláře. Tyto názvy budou použity k opravě polí.
```csharp
var invalidFormFields = fieldManager.GetInvalidFormFieldNames();
```
## Krok 4.4.2: Vytvořte jedinečné názvy pro neplatná pole
Pro každé neplatné pole formuláře vytvořte jedinečný název. Tím je zajištěno, že nedochází ke konfliktům s existujícími názvy polí formuláře.
```csharp
foreach (var invalidItem in invalidFormFields)
{
    invalidItem.FixedName = string.Format("{0}_{1}", invalidItem.Name, Guid.NewGuid());
}
```
## Krok 4.4.3: Opravte neplatná pole formuláře
Opravte neplatná pole formuláře pomocí jedinečných názvů vytvořených v předchozím kroku.
```csharp
fieldManager.FixInvalidFormFieldNames(invalidFormFields);
collection = fieldManager.FormFieldCollection;
```
## Krok 5: Vytvořte možnosti uložení dokumentu
Nastavte možnosti pro uložení dokumentu. To zahrnuje specifikaci formátu a případných dalších nastavení ukládání.
```csharp
WordProcessingFormats docFormat = WordProcessingFormats.Docx;
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(docFormat);
```
## Krok 5.1: Optimalizujte využití paměti
 Pokud je váš dokument velký a může způsobit`OutOfMemoryException`povolte možnost optimalizace paměti.
```csharp
saveOptions.OptimizeMemoryUsage = true;
```
## Krok 5.2: Chraňte dokument před zápisem
Chcete-li chránit dokument před změnami, s výjimkou polí formuláře, nastavte heslo ochrany.
```csharp
saveOptions.Protection = new WordProcessingProtection(WordProcessingProtectionType.AllowOnlyFormFields, "write_password");
```
## Krok 6: Uložte dokument
Nakonec uložte dokument se zadanými možnostmi uložení. Připravte paměťový proud pro uložení výstupního dokumentu.
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(outputStream, saveOptions);
}
Console.WriteLine("FixInvalidFormFieldCollectionAndSave routine has successfully finished");
```
## Závěr
 A tady to máte! Úspěšně jste opravili neplatná pole formuláře a uložili dokument pomocí Groupdocs.Editor pro .NET. Tento průvodce krok za krokem by měl tento proces objasnit a zvládnout. Pokud narazíte na nějaké problémy nebo máte dotazy, neváhejte se podívat na[dokumentace](https://tutorials.groupdocs.com/editor/net/) nebo oslovit[Podpěra, podpora](https://forum.groupdocs.com/c/editor/20).
## FAQ
### Co když je můj dokument chráněn heslem?
 Heslo můžete zadat v`WordProcessingLoadOptions` k otevření dokumentu.
### Jak zjistím, zda jsou pole formuláře neplatná?
 Použijte`HasInvalidFormFields` metoda pro kontrolu případných neplatných polí formuláře v dokumentu.
### Mohu opravit pole formuláře, aniž bych změnil jejich názvy?
Doporučuje se vytvořit jedinečné názvy pro neplatná pole formuláře, abyste předešli konfliktům.
### V jakých formátech mohu dokument uložit?
 Dokument můžete uložit v různých formátech, jako je DOCX, PDF a další, nastavením příslušného`WordProcessingFormats`.
### Jak mohu optimalizovat využití paměti při ukládání velkých dokumentů?
 Povolit`OptimizeMemoryUsage` možnost v`WordProcessingSaveOptions` pro efektivní zpracování velkých dokumentů.