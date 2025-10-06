---
title: Odebrat kolekci polí formuláře
linktitle: Odebrat kolekci polí formuláře
second_title: GroupDocs.Editor .NET API
description: V tomto podrobném průvodci se dozvíte, jak odstranit pole formuláře z dokumentů aplikace Word pomocí GroupDocs.Editor for .NET. Ideální pro vývojáře.
weight: 13
url: /cs/net/form-field-management/remove-form-field-collection/
type: docs
---
# Odebrat kolekci polí formuláře

## Úvod
Chcete spravovat pole formuláře ve svých dokumentech programově? GroupDocs.Editor for .NET nabízí výkonné řešení pro manipulaci a manipulaci s poli formulářů v různých formátech dokumentů. V tomto kurzu vás provedeme kroky k odstranění kolekcí polí formuláře z dokumentu aplikace Word pomocí této robustní knihovny. 
## Předpoklady
Než se ponoříme do kódu, ujistěte se, že máte vše nastaveno pro hladký průběh:
1. GroupDocs.Editor pro .NET: Ujistěte se, že jste si stáhli a nainstalovali GroupDocs.Editor pro .NET. Pokud ne, můžete si jej stáhnout[tady](https://releases.groupdocs.com/editor/net/).
2. Vývojové prostředí: Budete potřebovat vývojové prostředí, jako je Visual Studio.
3. .NET Framework: Ujistěte se, že máte na svém počítači nainstalované rozhraní .NET Framework.
4.  Vzorový dokument: Mějte vzorový dokument Word (např.`SampleLegacyFormFields.docx`) s poli formuláře, se kterými chcete manipulovat.

## Importovat jmenné prostory
Chcete-li začít, musíte do svého projektu .NET importovat potřebné jmenné prostory. To vám umožní přístup k funkcím GroupDocs.Editor.
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System.IO;
```
## Krok 1: Vložte dokument
Nejprve musíte načíst dokument, který chcete upravit. Pojďme si to rozebrat:
### Krok 1.1: Získejte cestu ke vstupnímu souboru
 Musíte zadat cestu ke svému vstupnímu souboru. Pro tento příklad použijeme ukázkový soubor s názvem`SampleLegacyFormFields.docx`.
```csharp
string inputFilePath = "path/to/SampleLegacyFormFields.docx";
```
### Krok 1.2: Vytvořte FileStream z cesty
 Dále vytvořte a`FileStream` k přečtení dokumentu.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
    // Pokračujte dalšími kroky v rámci tohoto bloku pomocí.
}
```
## Krok 2: Nastavte možnosti načítání
Při načítání dokumentu může být nutné zadat možnosti načítání, zejména pokud je dokument chráněn heslem.
### Krok 2.1: Vytvořte možnosti načtení
 Vytvořte instanci`WordProcessingLoadOptions`.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
```
### Krok 2.2: Zadejte heslo (v případě potřeby)
Pokud je váš dokument chráněn heslem, můžete heslo zadat.
```csharp
loadOptions.Password = "some_password_to_open_a_document";
```
## Krok 3: Načtěte dokument do Editoru
 Nyní vložte dokument do`Editor` instance pomocí`FileStream` a`LoadOptions`.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    // Pokračujte dalšími kroky v rámci tohoto bloku pomocí.
}
```
## Krok 4: Přístup k polím formuláře a jejich správa
Po načtení dokumentu můžete nyní přistupovat k polím formuláře a manipulovat s nimi.
### Krok 4.1: Přečtěte si FormFieldManager
 Získat`FormFieldManager` z`Editor` instance.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
### Krok 4.2: Přístup k FormFieldCollection
 Dostaň`FormFieldCollection` který obsahuje všechna pole formuláře v dokumentu.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
### Krok 4.3: Odeberte specifické textové pole formuláře
Chcete-li odebrat konkrétní textové pole formuláře, vyhledejte jej podle názvu a poté jej odeberte.
```csharp
TextFormField textField = collection.GetFormField<TextFormField>("Text1");
fieldManager.RemoveFormFiled(textField);
```
### Krok 4.4: Odeberte více polí formuláře
Můžete také odstranit více polí formuláře najednou zadáním jejich názvů.
```csharp
textField = collection.GetFormField<TextFormField>("Text7");
CheckBoxForm checkBoxForm = collection.GetFormField<CheckBoxForm>("Check2");
fieldManager.RemoveFormFields(new IFormField[] { textField, checkBoxForm });
```
## Krok 5: Uložte upravený dokument
Po úpravě polí formuláře je třeba dokument uložit.
### Krok 5.1: Vytvořte možnosti uložení
Určete formát a možnosti uložení pro výstupní dokument.
```csharp
WordProcessingFormats docFormat = WordProcessingFormats.Docx;
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(docFormat);
```
### Krok 5.2: Optimalizujte využití paměti
Pokud pracujete s velkými dokumenty, možná budete chtít optimalizovat využití paměti.
```csharp
saveOptions.OptimizeMemoryUsage = true;
```
### Krok 5.3: Nastavte ochranu (v případě potřeby)
Nastavením hesla pro zápis můžete dokument chránit před dalšími úpravami.
```csharp
saveOptions.Protection = new WordProcessingProtection(WordProcessingProtectionType.AllowOnlyFormFields, "write_password");
```
### Krok 5.4: Uložte dokument
 Nakonec dokument uložte pomocí a`MemoryStream`.
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(outputStream, saveOptions);
}
```

## Závěr
Gratulujeme! Úspěšně jste odstranili pole formuláře z dokumentu aplikace Word pomocí GroupDocs.Editor pro .NET. Tato výkonná knihovna usnadňuje programovou manipulaci s obsahem dokumentů, což vám šetří čas a námahu.
## FAQ
### Mohu použít GroupDocs.Editor pro .NET s jinými formáty dokumentů?
Ano, GroupDocs.Editor pro .NET podporuje různé formáty dokumentů, včetně PDF, HTML a dalších.
### Je možné přidat pole formuláře pomocí GroupDocs.Editor pro .NET?
Ano, pole formuláře můžete přidávat, upravovat a odebírat programově.
### Co když je můj dokument velmi velký?
Chcete-li efektivně zpracovávat velké dokumenty, můžete povolit optimalizaci paměti v možnostech ukládání.
### Mohu použít GroupDocs.Editor pro .NET ve webové aplikaci?
Absolutně! GroupDocs.Editor for .NET lze integrovat do webových aplikací pro zpracování dokumentů na straně serveru.
### Kde mohu získat podporu, pokud narazím na problémy?
 Můžete navštívit[Fórum podpory](https://forum.groupdocs.com/c/editor/20) za pomoc s případnými problémy.