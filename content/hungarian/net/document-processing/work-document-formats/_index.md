---
date: 2026-06-06
description: Ismerje meg, hogyan lehet felsorolni a támogatott dokumentumformátumokat
  és meghatározni a fájlformátum kiterjesztését a GroupDocs.Editor for .NET használatával.
  Step‑by‑step guide with code snippets, quick answers, and FAQs.
keywords:
- list supported document formats
- determine file format extension
- GroupDocs.Editor .NET
- document editing API
- supported formats guide
linktitle: Támogatott dokumentumformátumok listázása
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to list supported document formats and determine file format
    extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets,
    quick answers, and FAQs.
  headline: List Supported Document Formats with GroupDocs.Editor .NET
  type: TechArticle
- description: Learn how to list supported document formats and determine file format
    extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets,
    quick answers, and FAQs.
  name: List Supported Document Formats with GroupDocs.Editor .NET
  steps:
  - name: '**.NET development environment** – Visual Studio 2022 or any IDE that supports
      .NET 6+.'
    text: '**.NET development environment** – Visual Studio 2022 or any IDE that supports
      .NET 6+.'
  - name: '**GroupDocs.Editor for .NET library** – download from the [GroupDocs releases
      page](https://releases.groupdocs.com/editor/net/).'
    text: '**GroupDocs.Editor for .NET library** – download from the [GroupDocs releases
      page](https://releases.groupdocs.com/editor/net/).'
  - name: '**Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/)
      for unrestricted access.'
    text: '**Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/)
      for unrestricted access.'
  - name: '**Basic C# knowledge** – familiarity with namespaces, `using` statements,
      and console output.'
    text: '**Basic C# knowledge** – familiarity with namespaces, `using` statements,
      and console output.'
  - name: '**Loop Through Formats:** We iterate over all available Word‑processing
      formats.'
    text: '**Loop Through Formats:** We iterate over all available Word‑processing
      formats.'
  - name: '**Output Format Details:** For each format we print its friendly name and
      default file extension.'
    text: '**Output Format Details:** For each format we print its friendly name and
      default file extension.'
  - name: '**Loop Through Formats:** The same looping logic applies to presentations.'
    text: '**Loop Through Formats:** The same looping logic applies to presentations.'
  - name: '**Output Format Details:** The name and extension are displayed for each
      format.'
    text: '**Output Format Details:** The name and extension are displayed for each
      format.'
  - name: '**Parse Format:** `FromExtension` converts the `.xlsm` extension into its
      internal `SpreadsheetFormat` enum.'
    text: '**Parse Format:** `FromExtension` converts the `.xlsm` extension into its
      internal `SpreadsheetFormat` enum.'
  - name: '**Output Format:** The parsed format’s name is printed, confirming the
      mapping.'
    text: '**Output Format:** The parsed format’s name is printed, confirming the
      mapping.'
  type: HowTo
- questions:
  - answer: '`DocumentFormatInfo` provides metadata about supported file types, while
      `SaveOptions` configures how a document is written back to disk (format, compression,
      etc.).'
    question: What is the difference between `DocumentFormatInfo` and `SaveOptions`?
  - answer: Yes—use `DocumentFormatInfo.FromExtension("yourExt")`; if the extension
      isn’t recognized, the method returns `null`.
    question: Can I list formats for a custom file extension?
  - answer: Absolutely. Pass the password to the `Editor` constructor via `EditorSettings`
      to open encrypted documents.
    question: Does GroupDocs.Editor support password‑protected files?
  - answer: Over **30 input and output formats**, spanning Word, Excel, PowerPoint,
      HTML, and plain text.
    question: How many formats does GroupDocs.Editor actually support?
  - answer: Use the `GetEditableWordProcessingFormats()` (or Spreadsheet/Presentation
      equivalents) to retrieve formats that allow full edit capabilities.
    question: Is there a way to restrict the list to only editable formats?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Támogatott dokumentumformátumok listázása a GroupDocs.Editor .NET segítségével
type: docs
url: /hu/net/document-processing/work-document-formats/
weight: 13
---

# Támogatott dokumentumformátumok listája

Üdvözöljük átfogó oktatóanyagainkban, amely **hogyan listázzuk a támogatott dokumentumformátumokat** a GroupDocs.Editor for .NET segítségével. Akár dokumentum‑központú webalkalmazást, akár vállalati szintű asztali eszközt épít, elengedhetetlen, hogy pontosan tudja, mely formátumokat szerkesztheti vagy konvertálhatja. Ebben az útmutatóban megtudja, hogyan sorolja fel a formátumokat, hogyan dolgozza fel a kiterjesztéseket, és hogyan szerkesszen dokumentumokat – mindezt világos, emberi nyelven megfogalmazott magyarázatokkal és azonnal futtatható kódrészletekkel.

## Gyors válaszok
- **Hogyan listázhatom az összes támogatott formátumot?** Használja a `DocumentFormatInfo.GetSupportedWordProcessingFormats()` (vagy a Presentation/Spreadsheet megfelelőket) és iterálja a gyűjteményt.  
- **Meg tudom határozni a formátumot egy fájl kiterjesztésből?** Igen—hívja a `DocumentFormatInfo.FromExtension(".docx")`-t.  
- **Milyen fájltípusokat támogat a GroupDocs.Editor?** Több mint 30 bemeneti és kimeneti formátum, beleértve a DOCX, XLSX, PPTX, HTML és egyszerű szöveg formátumokat.  
- **Szükségem van licencre a formátumok listázásához?** Egy ideiglenes licenc feloldja a teljes API-t; egyébként a próbaverzió korlátozott funkciókkal működik.  
- **Mely .NET verziók kompatibilisek?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.

## Mi az a „támogatott dokumentumformátumok listázása”?
A kifejezés arra utal, hogy programozott módon lekérdezzük azon fájltípusok gyűjteményét, amelyeket a GroupDocs.Editor megnyithat, szerkeszthet és menthet. Ez a művelet lehetővé teszi dinamikus UI legördülő menük létrehozását vagy a felhasználói feltöltések validálását a feldolgozás előtt, biztosítva, hogy csak kompatibilis fájlok kerüljenek az editorba a további manipulációhoz.

## Miért listázzuk a támogatott dokumentumformátumokat?
A GroupDocs.Editor **több mint 30 bemeneti és kimeneti formátumot támogat** és akár **2 GB** méretű fájlokat is kezel anélkül, hogy a teljes dokumentumot a memóriába töltené. A pontos lista ismerete megakadályozza a futásidejű hibákat, javítja a felhasználói élményt, és lehetővé teszi üzleti szabályok érvényesítését, például „csak szerkeszthető Office dokumentumok engedélyezése”. Emellett segít a felhasználók számára csak az alkalmazás által valóban támogatott formátumok megjelenítésében.

## Előfeltételek
Mielőtt elkezdené, győződjön meg róla, hogy rendelkezik:

1. **.NET fejlesztői környezet** – Visual Studio 2022 vagy bármely IDE, amely támogatja a .NET 6+.  
2. **GroupDocs.Editor for .NET könyvtár** – letöltés a [GroupDocs releases page](https://releases.groupdocs.com/editor/net/) oldalról.  
3. **Ideiglenes licenc** – szerezzen be egy [temporary license](https://purchase.groupdocs.com/temporary-license/) a korlátlan hozzáféréshez.  
4. **Alap C# ismeretek** – ismerje a névtereket, a `using` utasításokat és a konzol kimenetet.

## Hogyan listázzuk a támogatott dokumentumformátumokat?
Töltsük be a támogatott formátumok gyűjteményét, és írjuk ki minden formátum nevét és fájlkiterjesztését. Ez a kétlépéses minta a Word feldolgozási, a Táblázatkezelő és a Prezentáció dokumentumokra egyaránt működik. A gyűjtemény iterálásával dinamikusan tölthetünk fel UI elemeket, például legördülő menüket, biztosítva, hogy a felhasználók csak az editor által ténylegesen kezelhető formátumokat választhassák.

```csharp
// No actual code block – placeholder retained from original tutorial
```csharp
using System;
using GroupDocs.Editor.Options;
```
```

### Word feldolgozási formátumok listázása
A `Formats.WordProcessingFormats` egy felsorolás, amely leírja az összes Word‑feldolgozási fájltípust, amelyet az editor felismer. Az `All` tulajdonság egy gyűjteményt ad vissza ezekből a formátumobjektumokból.

```csharp
```csharp
foreach (Formats.WordProcessingFormats oneFormat in Formats.WordProcessingFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**Explanation:**  
1. **Loop Through Formats:** We iterate over all available Word‑processing formats.  
2. **Output Format Details:** For each format we print its friendly name and default file extension.

### Prezentációs formátumok listázása
A `Formats.PresentationFormats` ugyanúgy működik a diavetítési fájlok esetén, a `All` gyűjteményen keresztül teszi elérhetővé minden támogatott prezentációtípust.

```csharp
```csharp
foreach (Formats.PresentationFormats oneFormat in Formats.PresentationFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**Explanation:**  
1. **Loop Through Formats:** The same looping logic applies to presentations.  
2. **Output Format Details:** The name and extension are displayed for each format.

## Hogyan határozzuk meg a fájlformátum kiterjesztését?
Néha csak egy fájlnév áll rendelkezésre, és meg kell határozni a megfelelő `DocumentFormat`-ot. A GroupDocs.Editor egy egyszerű statikus segédfüggvényt kínál, amely a fájl kiterjesztését a belső formátumábrázolásra térképezi, lehetővé téve a fájlok validálását vagy konvertálását, mielőtt betöltené őket az editorba.

### Táblázatkezelő formátumok feldolgozása
A `Formats.SpreadsheetFormats.FromExtension` egy fájl kiterjesztés karakterláncot alakít át a megfelelő táblázatkezelő formátum enum értékre.

```csharp
```csharp
Formats.SpreadsheetFormats expectedXlsm = Formats.SpreadsheetFormats.FromExtension(".xlsm");
Console.WriteLine("Parsed Spreadsheet format is {0}", expectedXlsm.Name);
```
```

**Explanation:**  
1. **Parse Format:** `FromExtension` converts the `.xlsm` extension into its internal `SpreadsheetFormat` enum.  
2. **Output Format:** The parsed format’s name is printed, confirming the mapping.

### Szöveges formátumok feldolgozása
Hasonlóképpen, a `Formats.TextualFormats.FromExtension` feloldja a szöveges fájl kiterjesztéseket, például a HTML vagy TXT formátumokat.

```csharp
```csharp
Formats.TextualFormats expectedHtml = Formats.TextualFormats.FromExtension("html");
Console.WriteLine("Parsed Textual format is {0}", expectedHtml.Name);
```
```

**Explanation:**  
1. **Parse Format:** The `FromExtension` method resolves the `html` extension to a `TextFormat`.  
2. **Output Format:** The name of the textual format is displayed, useful for web‑based editors.

## Hogyan szerkesszünk dokumentumokat a formátumok azonosítása után?
Miután ismeri a formátumot, a dokumentum betöltése és szerkesztése egy konzisztens mintát követ. Először egy `Editor` példányt hoz létre a forrásfájl elérési útjával, majd meghívja az `Edit()` metódust, hogy egy `EditableDocument` objektumot kapjon. Innen olvashat, módosíthat és végül mentheti a tartalmat a megfelelő `SaveOptions` használatával.

### Dokumentum betöltése
Az `Editor` az a központi osztály, amely egy adott fájl összes szerkesztési műveletét magába foglalja.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/document.docx"))
{
    // Further steps will be covered here.
}
```
```

**Explanation:**  
1. **Initialize Editor:** Create an `Editor` instance, passing the full path of the target file.  
2. **Dispose Pattern:** The `using` statement guarantees that all unmanaged resources are released promptly.

### Tartalom kinyerése
A `EditableDocument.GetContent()` visszaadja a dokumentum nyers szövegét (vagy HTML‑t web‑alapú szerkesztők esetén), amelyet megjeleníthet vagy manipulálhat.

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    string content = editableDocument.GetContent();
    Console.WriteLine(content);
}
```
```

**Explanation:**  
1. **Edit Method:** `Edit()` returns an `EditableDocument` object.  
2. **Get Content:** `GetContent()` extracts the document’s raw text (or HTML for web‑based editors).  
3. **Output Content:** The content is written to the console for verification.

### Változások mentése
A `SaveOptions` megmondja az editornak, hogyan és milyen formátumban írja vissza a szerkesztett dokumentumot a tárolóba.

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    // Modify content here
    SaveOptions saveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docx);
    editor.Save(editableDocument, "path/to/save/document.docx", saveOptions);
}
```
```

**Explanation:**  
1. **Edit Method:** Re‑obtain the `EditableDocument` after modifications.  
2. **Modify Content:** Apply your changes to the string (not shown here).  
3. **Save Options:** Configure `SaveOptions` with the desired output format.  
4. **Save Document:** Persist the edited file back to disk.

## Hogyan dolgozzunk különböző dokumentumtípusokkal?
A GroupDocs.Editor a Word, Spreadsheet és Presentation kezelését ugyanazon API felületen absztrahálja, így könnyű kontextust váltani anélkül, hogy minden dokumentumcsaládhoz új osztálykészletet kellene megtanulni.

### Táblázat dokumentumok szerkesztése
A `SpreadsheetSaveOptions` meghatározza, hogyan íródik egy táblázat, beleértve a formátumot és az opcionális tömörítési beállításokat.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/spreadsheet.xlsx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // Modify content here
        SaveOptions saveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsx);
        editor.Save(editableDocument, "path/to/save/spreadsheet.xlsx", saveOptions);
    }
}
```
```

**Explanation:**  
1. **Initialize Editor:** Pass a spreadsheet file path to the `Editor` constructor.  
2. **Edit Method:** Retrieve an `EditableDocument`.  
3. **Get Content:** Print the spreadsheet’s CSV representation (or HTML).  
4. **Modify Content:** Apply any cell‑level changes you need.  
5. **Save Options:** Choose the appropriate `SpreadsheetSaveOptions`.  
6. **Save Document:** Write the updated spreadsheet back to storage.

### Prezentáció dokumentumok szerkesztése
A `PresentationSaveOptions` szabályozza a diavetítések kimeneti formátumát, lehetővé téve az eredeti fájltípus megőrzését vagy módosítását.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/presentation.pptx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // Modify content here
        SaveOptions saveOptions = new PresentationSaveOptions(PresentationFormats.Pptx);
        editor.Save(editableDocument, "path/to/save/presentation.pptx", saveOptions);
    }
}
```
```

**Explanation:**  
1. **Initialize Editor:** Load a PowerPoint file via `Editor`.  
2. **Edit Method:** Obtain an `EditableDocument`.  
3. **Get Content:** Extract slide HTML or plain text.  
4. **Modify Content:** Update titles, bullet points, or images.  
5. **Save Options:** Use `PresentationSaveOptions` to define the output format.  
6. **Save Document:** Persist the edited presentation.

## Gyakori problémák és megoldások
- **„Format not supported” error:** Verify you’re using the latest GroupDocs.Editor version; it adds support for newer Office formats regularly.  
- **Large file memory consumption:** Enable streaming mode by setting `EditorSettings.EnableStreaming = true` before loading the document.  
- **License not applied:** Ensure the temporary license file is placed in the application root or loaded via `License license = new License(); license.SetLicense("path/to/license.lic");`.

## Gyakran ismételt kérdések

**Q: Mi a különbség a `DocumentFormatInfo` és a `SaveOptions` között?**  
A: A `DocumentFormatInfo` metaadatokat szolgáltat a támogatott fájltípusokról, míg a `SaveOptions` konfigurálja, hogyan írja vissza a dokumentumot a lemezre (formátum, tömörítés stb.).

**Q: Listázhatok formátumokat egy egyedi fájlkiterjesztéshez?**  
A: Igen—használja a `DocumentFormatInfo.FromExtension("yourExt")`‑t; ha a kiterjesztést nem ismeri fel, a metódus `null`‑t ad vissza.

**Q: Támogatja a GroupDocs.Editor a jelszóval védett fájlokat?**  
A: Teljes mértékben. A jelszót az `Editor` konstruktorába az `EditorSettings`‑en keresztül adhatja meg a titkosított dokumentumok megnyitásához.

**Q: Hány formátumot támogat valójában a GroupDocs.Editor?**  
A: Több mint **30 bemeneti és kimeneti formátum**, beleértve a Word, Excel, PowerPoint, HTML és egyszerű szöveg formátumokat.

**Q: Van mód a listát csak a szerkeszthető formátumokra korlátozni?**  
A: Használja a `GetEditableWordProcessingFormats()` (vagy Spreadsheet/Presentation megfelelőket) metódust, hogy lekérje azokat a formátumokat, amelyek teljes szerkesztési képességet biztosítanak.

## További források
- Töltse le a könyvtárat a [GroupDocs releases page](https://releases.groupdocs.com/editor/net/) oldalról.  
- Szerezzen be egy [temporary license](https://purchase.groupdocs.com/temporary-license/) teljes funkciókhoz.  
- Próbálja ki a terméket egy [free trial](https://releases.groupdocs.com/) segítségével.  
- Tekintse meg a részletes használati példákat a [GroupDocs.Editor documentation](https://tutorials.groupdocs.com/editor/net/) oldalon.  
- Kérjen segítséget a közösségtől a [support forum](https://forum.groupdocs.com/c/editor/20) fórumon.

## Következtetés
Az útmutató követésével most már tudja, hogyan **listázhatja a támogatott dokumentumformátumokat**, **határozza meg a fájlformátumot a kiterjesztés alapján**, és **szerkesszen dokumentumokat** a Word, Spreadsheet és Presentation típusokban a GroupDocs.Editor for .NET használatával. Integrálja ezeket a kódrészleteket saját projektjeibe, hogy robusztus, formátum‑tudatos alkalmazásokat építsen, amelyek örömet szereznek a végfelhasználóknak és csökkentik a futásidejű hibákat.

**Last Updated:** 2026-06-06  
**Tested With:** GroupDocs.Editor 23.9 for .NET  
**Author:** GroupDocs

## Kapcsolódó oktatóanyagok

- [Mastering Document Loading in .NET with GroupDocs.Editor: A Comprehensive Guide](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)  
- [Master Document Editing in .NET with GroupDocs.Editor: A Comprehensive Guide](/editor/net/document-editing/master-document-editing-dotnet-groupdocs-editor/)  
- [Convert Word to HTML Using GroupDocs.Editor .NET: A Step‑By‑Step Guide](/editor/net/document-saving/convert-word-to-html-groupdocs-editor-dotnet/)