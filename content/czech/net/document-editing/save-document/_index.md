---
title: Uložit dokument
linktitle: Uložit dokument
second_title: GroupDocs.Editor .NET API
description: Bez námahy upravujte a ukládejte dokumenty pomocí GroupDocs.Editor pro .NET. Tento průvodce krok za krokem zjednodušuje vývojářům proces.
weight: 14
url: /cs/net/document-editing/save-document/
type: docs
---
# Uložit dokument

## Úvod
Chcete snadno upravovat a ukládat dokumenty pomocí GroupDocs.Editor pro .NET? Jste na správném místě! Tento tutoriál vás provede procesem krok za krokem a zajistí vám snadnou správu dokumentů. Ať už jste zkušený vývojář nebo začátečník, náš průvodce vám poskytne všechny informace, které potřebujete, abyste mohli začít.
## Předpoklady
Než se pustíte do výukového programu, ujistěte se, že máte splněny následující předpoklady:
- Vývojové prostředí: Visual Studio nainstalované na vašem počítači.
- .NET Framework: Ujistěte se, že máte .NET Framework 4.6.1 nebo novější.
-  GroupDocs.Editor pro .NET: Stáhněte si nejnovější verzi[tady](https://releases.groupdocs.com/editor/net/).
- Základní znalost C#: Znalost programování v C# je nezbytná.
## Importovat jmenné prostory
Chcete-li použít GroupDocs.Editor ve svém projektu .NET, musíte importovat potřebné jmenné prostory. Postup je následující:
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
Nyní, když máme nastavené prostředí a importované potřebné jmenné prostory, pojďme se vrhnout na kroky potřebné k načtení, úpravě a uložení dokumentu pomocí GroupDocs.Editor pro .NET.
## Krok 1: Vložte dokument
Nejprve musíme načíst dokument, který chceme upravit. GroupDocs.Editor tento proces zjednodušuje. Můžete to udělat takto:

```csharp
string inputFilePath = "Your Sample Document";
Editor editor = new Editor(inputFilePath, delegate { return new Options.WordProcessingLoadOptions(); });
EditableDocument defaultWordProcessingDoc = editor.Edit();
```
 V tomto kroku zadáme cestu k dokumentu, který chceme upravit, a vytvoříme jeho instanci`Editor` třída. The`Edit` pak je volána metoda k načtení dokumentu do souboru`EditableDocument` objekt.
## Krok 2: Upravte dokument
Po načtení dokumentu je čas provést některé úpravy. Protože nemáme připojený WYSIWYG editor, budeme proces úprav simulovat v kódu.

```csharp
string allEmbeddedInsideString = defaultWordProcessingDoc.GetEmbeddedHtml();
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
EditableDocument editedDoc = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```
 Zde načteme vložený obsah HTML dokumentu, provedeme jednoduchou náhradu textu a vytvoříme nový`EditableDocument`instance z upraveného HTML.
## Krok 3: Uložte dokument
Po úpravě dokumentu je posledním krokem jeho uložení. GroupDocs.Editor poskytuje několik možností pro uložení dokumentu v různých formátech.
## Uložit jako RTF
```csharp
string outputRtfPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.rtf");
WordProcessingSaveOptions rtfSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
editor.Save(editedDoc, outputRtfPath, rtfSaveOptions);
```
## Uložit jako DOCM
```csharp
string outputDocmPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.docm");
WordProcessingSaveOptions docmSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm);
using (FileStream outputStream = File.Create(outputDocmPath))
{
    editor.Save(editedDoc, outputStream, docmSaveOptions);
}
```
## Uložit jako prostý text
```csharp
string outputTxtPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.txt");
TextSaveOptions textSaveOptions = new TextSaveOptions
{
    Encoding = System.Text.Encoding.UTF8,
    PreserveTableLayout = true
};
editor.Save(editedDoc, outputTxtPath, textSaveOptions);
```
## Krok 4: Vyčištění
 V neposlední řadě je důležité je zlikvidovat`EditableDocument` a`Editor` instance pro uvolnění zdrojů.
```csharp
editedDoc.Dispose();
defaultWordProcessingDoc.Dispose();
editor.Dispose();
```
Pomocí následujících kroků můžete efektivně načítat, upravovat a ukládat dokumenty pomocí GroupDocs.Editor pro .NET. Tento výkonný nástroj poskytuje flexibilitu a snadné použití, díky čemuž je správa dokumentů hračkou.
## Závěr
Úpravy a ukládání dokumentů pomocí programu nebylo nikdy snazší s GroupDocs.Editor pro .NET. Tento průvodce vás provede celým procesem, od načtení dokumentu až po jeho uložení v různých formátech. S GroupDocs.Editor máte na dosah všestranné a robustní řešení, které zjednodušuje proces úprav dokumentů.
## FAQ
### Jaké formáty souborů podporuje GroupDocs.Editor?
GroupDocs.Editor podporuje různé formáty souborů, včetně DOCX, RTF, TXT a mnoha dalších. Pro úplný seznam se podívejte na[dokumentace](https://tutorials.groupdocs.com/editor/net/).
### Mohu GroupDocs.Editor před zakoupením vyzkoušet?
 Ano, můžete získat a[zkušební verze zdarma](https://releases.groupdocs.com/) k testování funkcí GroupDocs.Editoru.
### Je k dispozici nějaká podpora v případě problémů?
 Absolutně! Můžete navštívit[Fórum podpory](https://forum.groupdocs.com/c/editor/20) o pomoc s jakýmikoli problémy, se kterými se setkáte.
### Jak získám dočasnou licenci?
 Můžete požádat a[dočasná licence](https://purchase.groupdocs.com/temporary-license/) pro účely hodnocení.
### Kde si mohu zakoupit plnou verzi GroupDocs.Editoru?
 Můžete si koupit plnou verzi[tady](https://purchase.groupdocs.com/buy).