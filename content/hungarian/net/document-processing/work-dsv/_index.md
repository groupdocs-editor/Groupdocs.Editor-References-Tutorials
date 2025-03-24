---
title: Munka elválasztott értékekkel (DSV)
linktitle: Munka elválasztott értékekkel (DSV)
second_title: GroupDocs.Editor .NET API
description: Ebből a lépésről lépésre szóló útmutatóból megtudhatja, hogyan szerkeszthet CSV- és TSV-fájlokat a GroupDocs.Editor for .NET használatával. Javítsa .NET-projektjeit könnyedén.
weight: 12
url: /hu/net/document-processing/work-dsv/
---

# Munka elválasztott értékekkel (DSV)

## Bevezetés
Ha Ön olyan fejlesztő, aki elválasztott értékekkel (DSV), például CSV- vagy TSV-fájlokkal dolgozik, tudja, hogy ezeknek a fájloknak a programozott szerkesztése ijesztő feladat lehet. A GroupDocs.Editor for .NET segítségével azonban ez a feladat lényegesen egyszerűbbé és hatékonyabbá válik. Ebben az oktatóanyagban végigvezetjük, hogyan használhatja a GroupDocs.Editor for .NET programot DSV-fájlok olvasásához, szerkesztéséhez és mentéséhez. A folyamatot könnyen követhető lépésekre bontjuk, így Ön könnyen megvalósíthatja projektjeit.
## Előfeltételek
Mielőtt belevágnánk az oktatóanyagba, győződjön meg arról, hogy rendelkezik a következő előfeltételekkel:
- Visual Studio: Győződjön meg arról, hogy a Visual Studio telepítve van a gépen.
-  GroupDocs.Editor for .NET: Le kell töltenie és hivatkoznia kell a GroupDocs.Editor for .NET könyvtárra. Letöltheti[itt](https://releases.groupdocs.com/editor/net/).
- C# alapvető ismerete: Ez az oktatóanyag feltételezi, hogy rendelkezik a C# és a .NET fejlesztés alapvető ismereteivel.
## Névterek importálása
Először is importálnia kell a szükséges névtereket a projektbe. Ezek a névterek biztosítják a GroupDocs.Editor for .NET használatához szükséges osztályokat és metódusokat.
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

## 1. lépés: Szerezze meg a bemeneti DSV-fájl elérési útját
Először is meg kell adnia a bemeneti DSV-fájl elérési útját. Ebben a példában feltételezzük, hogy ez egy CSV-fájl.
```csharp
string inputFilePath = "Your Sample Document";
```
## 2. lépés: Hozzon létre egy szerkesztőpéldányt
 Hozzon létre egy példányt a`Editor` osztály. Ez a példány a DSV-fájl betöltésére és kezelésére szolgál.
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## 3. lépés: Hozzon létre DSV szerkesztési beállításokat
 Ezután hozzon létre egy példányt a`DelimitedTextEditOptions` és adja meg a DSV-fájl határolóját. Itt vesszőt használunk elválasztóként.
```csharp
    Options.DelimitedTextEditOptions editOptions = new DelimitedTextEditOptions(",");
    editOptions.ConvertDateTimeData = false;
    editOptions.ConvertNumericData = true;
    editOptions.TreatConsecutiveDelimitersAsOne = true;
```
## 4. lépés: Hozzon létre egy EditableDocument példányt
 Hozzon létre egy`EditableDocument` például a`Editor.Edit` módszer. Ez előkészíti a dokumentumot szerkesztésre.
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## 5. lépés: Szerkessze a dokumentum tartalmát
Keresse ki az eredeti szöveges tartalmat, és végezze el a szükséges módosításokat. Bemutatás céljából cseréljünk ki néhány szöveget.
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("SsangYong", "Chevrolet").Replace("Kyron", "Camaro");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## 6. lépés: Hozzon létre egy szerkeszthető dokumentumot frissített tartalommal
 Újat csinálni`EditableDocument` a frissített tartalommal.
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## 7. lépés: Hozzon létre CSV mentési beállításokat
Adja meg a CSV formátum mentési beállításait, beleértve a határolót és a kódolást.
```csharp
    Options.DelimitedTextSaveOptions csvSaveOptions = new DelimitedTextSaveOptions(",");
    csvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## 8. lépés: Hozzon létre TSV mentési beállításokat
Hasonlóképpen adja meg a TSV formátum mentési beállításait.
```csharp
    Options.DelimitedTextSaveOptions tsvSaveOptions = new DelimitedTextSaveOptions("\t");
    tsvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## 9. lépés: Hozzon létre Táblázat mentési opciókat
Ha a dokumentumot táblázatként kell mentenie, hozza létre a megfelelő mentési beállításokat.
```csharp
    Options.SpreadsheetSaveOptions cellsSaveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
```
## 10. lépés: Készítse elő a mentési útvonalakat
Határozza meg a szerkesztett fájlok mentési útvonalait.
```csharp
    string outputCsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".csv");
    string outputTsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".tsv");
    string outputCellsPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".xlsm");
```
## 11. lépés: Mentse el a szerkesztett dokumentumot
Mentse el a szerkesztett dokumentumot a megadott útvonalakra különböző formátumokban.
```csharp
    editor.Save(afterEdit, outputCsvPath, csvSaveOptions);
    editor.Save(afterEdit, outputTsvPath, tsvSaveOptions);
    editor.Save(afterEdit, outputCellsPath, cellsSaveOptions);
```
## 12. lépés: Dobja ki az EditableDocument Példányokat
 Végül mindenképpen dobja ki a`EditableDocument` példányokat az erőforrások felszabadítására.
```csharp
    beforeEdit.Dispose();
    afterEdit.Dispose();
}
System.Console.WriteLine("WorkingWithDsv routine has successfully finished");
```
## Következtetés
DSV-fájlok szerkesztése a GroupDocs.Editor for .NET használatával egy egyszerű folyamat, amely magában foglalja egy szerkesztőpéldány létrehozását, a szerkesztési beállítások megadását, a tartalom módosítását és a módosítások mentését. Ez a lépésenkénti útmutató segít abban, hogy ezt a funkciót könnyedén integrálja .NET-alkalmazásaiba. Akár CSV-vel, TSV-vel vagy más DSV-formátummal dolgozik, a GroupDocs.Editor for .NET robusztus és rugalmas megoldást kínál.
## GYIK
### Használhatom a GroupDocs.Editor for .NET programot nagy CSV-fájlok szerkesztéséhez?
Igen, a GroupDocs.Editor for .NET képes hatékonyan kezelni a nagy CSV-fájlokat.
### A GroupDocs.Editor for .NET támogatja a CSV-n és a TSV-n kívül más DSV-formátumokat is?
Igen, támogatja a különböző DSV formátumokat mindaddig, amíg megadja a megfelelő határolót.
### Testreszabható a kódolás DSV fájlok mentésekor?
Természetesen a kívánt kódolást megadhatja a mentési beállításokban.
### Átalakíthatok egy CSV-fájlt Excel-táblázattá a GroupDocs.Editor for .NET segítségével?
Igen, a megfelelő mentési beállítások használatával elmenthet egy CSV-fájlt Excel-táblázatként.
### Hol találok további dokumentációt a GroupDocs.Editor for .NET-hez?
 Részletes dokumentációt találhat[itt](https://tutorials.groupdocs.com/editor/net/)