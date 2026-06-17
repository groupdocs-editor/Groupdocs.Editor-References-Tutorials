---
date: '2026-04-07'
description: Naučte se upravovat soubory DOCX a převádět Word na RTF pomocí GroupDocs.Editor .NET.
  Efektivně automatizujte workflow dokumentů.
keywords:
- how to edit docx
- convert word to rtf
- convert docx to txt
- document workflow automation
- batch process word docs
- save docx as docm
title: Jak editovat DOCX a převádět formáty pomocí GroupDocs.Editor
type: docs
url: /cs/net/document-editing/groupdocs-editor-net-mastering-document-editing/
weight: 1
---

# Jak upravit DOCX a převádět formáty pomocí GroupDocs.Editor

Jednoduše spravujte a převádějte Word dokumenty ve svém .NET prostředí pomocí **GroupDocs.Editor .NET**. V tomto tutoriálu se dozvíte **jak upravit docx** soubory, převést je do formátů jako RTF, DOCM a prostý text a automatizovat svůj dokumentový workflow pro maximální produktivitu.

## Rychlé odpovědi
- **Jaká knihovna je vyžadována?** GroupDocs.Editor pro .NET (20.10+).  
- **Mohu převést DOCX na RTF?** Ano – použijte `WordProcessingSaveOptions` s `WordProcessingFormats.Rtf`.  
- **Je podpora ukládání jako TXT?** Rozhodně, pomocí `TextSaveOptions`.  
- **Potřebuji licenci?** Zkušební verze funguje pro vývoj; licence odemkne všechny funkce.  
- **Jak zvládnout mnoho souborů?** Kombinujte kód s async/await nebo Parallel.ForEach pro dávkové zpracování.

## Co je „jak upravit docx“ pomocí GroupDocs.Editor?
GroupDocs.Editor načte DOCX, zpřístupní jeho obsah jako editovatelný HTML, umožní vám tento HTML programově upravit a poté výsledek uloží zpět do libovolného podporovaného formátu. Tento přístup eliminuje potřebu Office interop a funguje na jakékoli server‑side .NET platformě.

## Proč použít GroupDocs.Editor pro automatizaci dokumentových workflow?
- **Pouze server‑side** – není vyžadována instalace Office.  
- **Více výstupních formátů** – RTF, DOCM, TXT, HTML, PDF atd.  
- **Vysoký výkon** – lehké API navržené pro dávkové scénáře.  
- **Plná kontrola** – editovat, nahrazovat nebo vkládat HTML fragmenty před uložením.

## Požadavky
- **GroupDocs.Editor** knihovna (verze 20.10 nebo novější)  
- .NET Framework 4.7.2 + nebo .NET 5/6  
- Visual Studio (jakékoli recentní vydání)  
- Základní znalost C# a povědomí o souborovém I/O  

## Instalace GroupDocs.Editor
Balíček můžete přidat pomocí .NET CLI, Package Manager Console nebo NuGet UI.

```bash
dotnet add package GroupDocs.Editor
```

```powershell
Install-Package GroupDocs.Editor
```

## Získání licence
Začněte s bezplatnou zkušební verzí nebo požádejte o dočasný licenční klíč. Pro produkční použití zakupte licenci, která odemkne neomezené zpracování.

## Jak načíst a upravit DOCX dokument
Nejprve nasměrujte editor na svůj zdrojový soubor, poté načtěte editovatelný HTML, proveďte potřebné změny a nakonec vytvořte nový `EditableDocument` z upraveného markupu.

```csharp
using (Editor editor = new Editor("YOUR_DOCUMENT_DIRECTORY/sample.docx", new Options.WordProcessingLoadOptions()))
{
    // Your document manipulation code here
}
```

### Postupný průchod kódem
1. **Define the input file path**  

```csharp
string inputFilePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
```

2. **Create the `Editor` instance**  

```csharp
using GroupDocs.Editor;
using GroupDocs.Editor.Options;

Editor editor = new Editor(inputFilePath, new Options.WordProcessingLoadOptions());
```

3. **Edit the document’s HTML**  

```csharp
EditableDocument defaultWordProcessingDoc = editor.Edit();
string allEmbeddedInsideString = defaultWordProcessingDoc.GetEmbeddedHtml();
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
```

4. **Create a new `EditableDocument` from the edited HTML**  

```csharp
EditableDocument editedDoc = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```

5. **Dispose of temporary objects**  

```csharp
editedDoc.Dispose();
defaultWordProcessingDoc.Dispose();
editor.Dispose();
```

## Jak převést Word na RTF
Uložení upraveného dokumentu jako RTF je jednoduché s vhodnými možnostmi uložení.

```csharp
string outputRtfPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "editedDoc.rtf");
```

```csharp
WordProcessingSaveOptions rtfSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
```

```csharp
using (Editor editor = new Editor(inputFilePath, new Options.WordProcessingLoadOptions()))
{
    editor.Save(editedDoc, outputRtfPath, rtfSaveOptions);
}
editor.Dispose();
```

## Jak uložit DOCX jako DOCM pomocí streamu
Když potřebujete formát DOCM s makry, můžete zapisovat přímo do `FileStream`.

```csharp
string outputDocmPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "editedDoc.docm");
```

```csharp
WordProcessingSaveOptions docmSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm);
```

```csharp
using (Editor editor = new Editor(inputFilePath, new Options.WordProcessingLoadOptions()))
{
    using (FileStream outputStream = File.Create(outputDocmPath))
    {
        editor.Save(editedDoc, outputStream, docmSaveOptions);
    }
}
editor.Dispose();
```

## Jak převést DOCX na TXT (prostý text)
Extrahování prostého textu je užitečné pro indexování, vyhledávání nebo e‑mailová upozornění.

```csharp
string outputTxtPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "editedDoc.txt");
```

```csharp
TextSaveOptions textSaveOptions = new TextSaveOptions()
{
    Encoding = Encoding.UTF8,
    PreserveTableLayout = true
};
```

```csharp
using (Editor editor = new Editor(inputFilePath, new Options.WordProcessingLoadOptions()))
{
    editor.Save(editedDoc, outputTxtPath, textSaveOptions);
}
editor.Dispose();
```

## Běžné případy použití a reálné scénáře
- **Automatizovaná tvorba reportů:** Převádějte analytické Word reporty do TXT pro e‑mailové rozesílání.  
- **Platformy pro kolaborativní úpravy:** Umožněte uživatelům editovat HTML fragmenty a uložit výsledek jako DOCM nebo RTF.  
- **Archivace dokumentů:** Migrujte starší DOCX soubory do DOCM pro podporu maker při zachování obsahu.  
- **Webové služby:** Streamujte konverze DOCX → PDF/RTF za běhu bez dočasných souborů.

## Tipy pro výkon při dávkovém zpracování Word dokumentů
- **Okamžitě uvolňovat:** Vždy zavolejte `Dispose()` na objektech `Editor` a dokumentu.  
- **Rozumné načítání:** Vyberte nejspecifičtější `LoadOptions`, aby se předešlo zbytečnému parsování.  
- **Bezpečné paralelizování:** Použijte `Parallel.ForEach` s oddělenými instancemi `Editor` pro každý vlákno.  
- **Vyhněte se velkým řetězcům v paměti:** Při zpracování obrovských dokumentů pracujte se streamy místo kompletních HTML řetězců.

## Často kladené otázky

**Q: Mohu upravit chráněný DOCX heslem?**  
A: Ano. Zadejte heslo pomocí `WordProcessingLoadOptions.Password` při vytváření `Editor`.

**Q: Je možné převést mnoho souborů v jednom běhu?**  
A: Rozhodně. Zabalte logiku pro jeden soubor do smyčky nebo použijte `Parallel.ForEach` pro souběžné zpracování.

**Q: Podporuje GroupDocs.Editor .NET Core?**  
A: Knihovna funguje s .NET 5, .NET 6 a .NET Core 3.1 i s plným .NET Framework.

**Q: Co se stane s makry při uložení jako DOCM?**  
A: Makra jsou zachována, když použijete formát uložení `Docm`; jsou odstraněna pro RTF/TXT.

**Q: Jak řešit „OutOfMemoryException“ během velkých dávkových úloh?**  
A: Zpracovávejte soubory v menších dávkách, okamžitě uvolňujte objekty a zvažte zvýšení limitu paměti aplikace.

## Závěr
Nyní máte kompletní, připravený workflow pro **jak upravit docx** soubory a převádět je na RTF, DOCM nebo prostý text pomocí GroupDocs.Editor .NET. Dodržením výše uvedených kroků můžete automatizovat dokumentové workflow, zpracovávat dávky a integrovat bezproblémovou konverzi formátů do jakékoli .NET aplikace.

---

**Poslední aktualizace:** 2026-04-07  
**Testováno s:** GroupDocs.Editor 20.10 (latest at time of writing)  
**Autor:** GroupDocs