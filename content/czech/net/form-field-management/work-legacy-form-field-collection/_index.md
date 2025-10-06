---
title: Práce s Legacy Form Field Collection
linktitle: Práce s Legacy Form Field Collection
second_title: GroupDocs.Editor .NET API
description: Naučte se, jak spravovat starší pole formuláře pomocí GroupDocs.Editor pro .NET s naším podrobným průvodcem. Ideální pro práci s textovými poli, zaškrtávacími políčky, daty a dalšími.
weight: 12
url: /cs/net/form-field-management/work-legacy-form-field-collection/
type: docs
---
# Práce s Legacy Form Field Collection

## Úvod
Vítejte v tomto komplexním průvodci, jak pracovat se staršími kolekcemi polí formulářů pomocí GroupDocs.Editor pro .NET. Ať už máte co do činění s textovými poli, zaškrtávacími políčky, datovými poli nebo rozevíracími nabídkami, tento tutoriál vás provede každým krokem k efektivní správě těchto polí. Na konci této příručky budete dobře rozumět tomu, jak používat GroupDocs.Editor pro práci s různými poli formulářů ve vašich dokumentech. Pojďme se ponořit!
## Předpoklady
Než začneme, ujistěte se, že máte následující předpoklady:
- Visual Studio: Bude fungovat jakákoli nejnovější verze.
- .NET Framework: Ujistěte se, že máte nainstalované rozhraní .NET Framework.
-  GroupDocs.Editor pro .NET: Stáhněte si nejnovější verzi[tady](https://releases.groupdocs.com/editor/net/).
- Ukázkový dokument: Ukázkový soubor DOCX s poli formuláře pro účely testování.
## Importovat jmenné prostory
Nejprve importujte potřebné jmenné prostory do svého projektu. Tyto jmenné prostory jsou nezbytné pro přístup ke třídám a metodám potřebným k manipulaci s poli formuláře.
```csharp
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System.IO;
```
## Krok 1: Získejte cestu k vstupnímu souboru
Nejprve musíte zadat cestu k vašemu vstupnímu souboru. V tomto příkladu použijeme ukázkový soubor DOCX, který obsahuje různá pole formuláře.
```csharp
string inputFilePath = "path/to/your/sample_legacy_formfields.docx";
```
## Krok 2: Vytvořte stream z cesty k souboru
Dále vytvořte datový proud souboru pro čtení obsahu dokumentu. Tento proud bude použit k načtení dokumentu do GroupDocs.Editoru.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
    // Dodatečný kód bude uveden zde
}
```
## Krok 3: Vytvořte možnosti načtení pro dokument
Před načtením dokumentu vytvořte možnosti načtení. Tyto možnosti pomohou zvládnout různé scénáře, jako jsou dokumenty chráněné heslem.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
// Pokud je dokument chráněn heslem, zadejte heslo
loadOptions.Password = "your_password_here"; // V případě potřeby použijte skutečné heslo
```
## Krok 4: Načtěte dokument s instancí editoru
Nyní načtěte dokument do instance Editoru pomocí streamu souborů a možností načtení, které jste vytvořili dříve.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    // Dodatečný kód bude uveden zde
}
```
## Krok 5: Přečtěte si instanci FormFieldManager
Chcete-li spravovat pole formuláře, otevřete instanci FormFieldManager z Editoru. Tato instance vám umožní pracovat s poli formuláře v dokumentu.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
## Krok 6: Přečtěte si FormFieldCollection
Načtěte FormFieldCollection z FormFieldManager. Tato kolekce obsahuje všechna pole formuláře přítomná v dokumentu.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
## Krok 7: Iterujte každé pole formuláře
Projděte každé pole formuláře v kolekci a identifikujte jeho typ. V závislosti na typu můžete extrahovat a manipulovat s hodnotou pole.
```csharp
foreach (var formField in collection)
{
    switch (formField.Type)
    {
        case FormFieldType.Text:
            TextFormField textFormField = collection.GetFormField<TextFormField>(formField.Name);
            Console.WriteLine($"TextFormField detected, name: {formField.Name}, value: {textFormField.Value}");
            break;
        case FormFieldType.CheckBox:
            CheckBoxForm checkBoxFormField = collection.GetFormField<CheckBoxForm>(formField.Name);
            Console.WriteLine($"CheckBoxForm detected, name: {formField.Name}, value: {checkBoxFormField.Value}");
            break;
        case FormFieldType.Date:
            DateFormField dateFormField = collection.GetFormField<DateFormField>(formField.Name);
            Console.WriteLine($"DateFormField detected, name: {formField.Name}, value: {dateFormField.Value}");
            break;
        case FormFieldType.Number:
            NumberFormField numberFormField = collection.GetFormField<NumberFormField>(formField.Name);
            Console.WriteLine($"NumberFormField detected, name: {formField.Name}, value: {numberFormField.Value}");
            break;
        case FormFieldType.DropDown:
            DropDownFormField dropDownFormField = collection.GetFormField<DropDownFormField>(formField.Name);
            Console.WriteLine($"DropDownFormField detected, name: {formField.Name}, value selected: {dropDownFormField.Value[dropDownFormField.SelectedIndex]}");
            break;
    }
}
```
## Krok 8: Závěr
Dodržením těchto kroků můžete efektivně spravovat a pracovat se staršími poli formulářů ve vašich dokumentech pomocí GroupDocs.Editor pro .NET. Ať už se jedná o textová pole, zaškrtávací políčka, data, čísla nebo rozevírací seznamy, tato příručka poskytuje jasný a stručný způsob, jak zacházet s každým typem.
## Závěr
 Práce se staršími poli formulářů v dokumentech může být při použití správných nástrojů jednoduchá. GroupDocs.Editor pro .NET poskytuje robustní řešení pro efektivní správu těchto polí. Podle tohoto podrobného průvodce byste nyní měli být schopni snadno manipulovat s různými poli formuláře ve vašich dokumentech. Nezapomeňte prozkoumat[dokumentace](https://tutorials.groupdocs.com/editor/net/)pro pokročilejší funkce a možnosti.
## FAQ
### 1. Mohu použít GroupDocs.Editor pro .NET s dokumenty chráněnými heslem?
Ano, můžete zadat heslo v možnostech načtení pro zpracování dokumentů chráněných heslem.
### 2. Jak získám bezplatnou zkušební verzi GroupDocs.Editor pro .NET?
 Bezplatnou zkušební verzi si můžete stáhnout z[tady](https://releases.groupdocs.com/).
### 3. Je k dispozici nějaká podpora pro GroupDocs.Editor pro .NET?
 Ano, máte přístup k podpoře[tady](https://forum.groupdocs.com/c/editor/20).
### 4. Mohu si zakoupit licenci pro GroupDocs.Editor pro .NET?
 Ano, můžete si zakoupit licenci od[tady](https://purchase.groupdocs.com/buy).
### 5. Kde najdu dokumentaci k GroupDocs.Editor pro .NET?
Dokumentace je k dispozici[tady](https://tutorials.groupdocs.com/editor/net/).