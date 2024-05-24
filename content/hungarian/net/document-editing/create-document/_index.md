---
title: Dokumentum létrehozása
linktitle: Dokumentum létrehozása
second_title: GroupDocs.Editor .NET API
description: Ezzel az átfogó, lépésenkénti oktatóanyaggal megtudhatja, hogyan szerkeszthet Word, Excel, PowerPoint, Ebook és E-mail dokumentumokat a GroupDocs.Editor for .NET segítségével.
type: docs
weight: 10
url: /hu/net/document-editing/create-document/
---
## Bevezetés
Eleged van a különféle dokumentumtípusok programozott szerkesztésével járó fáradságból? A GroupDocs.Editor for .NET azért van itt, hogy leegyszerűsítse a folyamatot. Ezzel a hatékony eszközzel a fejlesztők könnyedén szerkeszthetnek különféle dokumentumformátumokat, például Word, Excel, PowerPoint, e-könyveket és e-maileket. Ebben az oktatóanyagban részletesen elmerülünk a GroupDocs.Editor for .NET használatával dokumentumok létrehozására és szerkesztésére. A folyamatot könnyen követhető lépésekre bontjuk, így akkor is elérhetővé tesszük, ha még nem ismeri ezt.
## Előfeltételek
Mielőtt elkezdené, győződjön meg arról, hogy rendelkezik az alábbiakkal:
- A Visual Studio telepítve van a gépedre.
- .NET-keretrendszer (4.0 vagy újabb).
-  GroupDocs.Editor .NET könyvtárhoz. Letöltheti innen[itt](https://releases.groupdocs.com/editor/net/).
- C# programozási alapismeretek.
## Névterek importálása
Először is importáljuk a szükséges névtereket. Ezzel elérhetővé teszi a szükséges osztályokat és metódusokat az alkalmazásunkban.
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using System.IO;
```
## 1. lépés: Az adatfolyam beállítása
Először is be kell állítanunk egy memóriafolyamot, amely a dokumentumtartalom helyőrzőjeként fog működni.
```csharp
Stream memoryStream = Stream.Null;
```
## 2. lépés: Visszahívási funkció a dokumentum mentéséhez
Ezután határozzon meg egy visszahívási funkciót, amely elmenti az új dokumentumfolyamot. Ez a funkció elengedhetetlen a dokumentumszerkesztési folyamat kimenetének kezeléséhez.
```csharp
void SaveNewDocument(Stream resultStream)
{
    memoryStream = resultStream;
}
```
## 3. lépés: Szövegfeldolgozási dokumentum létrehozása és szerkesztése
 Most hozzunk létre és szerkesszünk egy Word-dokumentumot. Kezdjük egy új létrehozásával`Editor` példányt a WordProcessing dokumentumokhoz, és szerkessze az alapértelmezett beállításokkal.
### Létrehozása és szerkesztése az alapértelmezett beállításokkal
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    EditableDocument defaultWordProcessingDoc = editor.Edit();
}
```
### Létrehozása és szerkesztése egyéni beállításokkal
A nagyobb szabályozás érdekében megadhatunk olyan beállításokat, mint például a lapozás letiltása és a beágyazott betűtípusok kibontása.
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    WordProcessingEditOptions wordProcessingEditOptions = new WordProcessingEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true,
        FontExtraction = FontExtractionOptions.ExtractAllEmbedded
    };
    EditableDocument editableWordProcessingDocument = editor.Edit(wordProcessingEditOptions);
}
```
## 4. lépés: Táblázatdokumentum létrehozása és szerkesztése
Hasonlóképpen készíthetünk és szerkeszthetünk Excel-dokumentumot. Íme, hogyan kell csinálni.
### Létrehozása és szerkesztése az alapértelmezett beállításokkal
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    EditableDocument defaultEditableSpreadsheetDocument = editor.Edit();
}
```
### Létrehozása és szerkesztése egyéni beállításokkal
 Adott munkalapok célzásához vagy rejtett munkalapok kizárásához használjuk`SpreadsheetEditOptions`.
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    SpreadsheetEditOptions spreadsheetEditOptions = new SpreadsheetEditOptions
    {
        WorksheetIndex = 0,
        ExcludeHiddenWorksheets = true
    };
    EditableDocument editableSpreadsheetDocument = editor.Edit(spreadsheetEditOptions);
}
```
## 5. lépés: Prezentációs dokumentum létrehozása és szerkesztése
A PowerPoint prezentációk szintén támogatottak. Lássuk, hogyan kezeljük őket.
### Létrehozása és szerkesztése az alapértelmezett beállításokkal
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    EditableDocument defaultEditablePresentationDocument = editor.Edit();
}
```
### Létrehozása és szerkesztése egyéni beállításokkal
A szerkesztéseket testreszabhatja az olyan opciók megadásával, mint például, hogy melyik diát jelenítse meg, és hogy tartalmazzon-e rejtett diákat.
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    PresentationEditOptions presentationEditOptions = new PresentationEditOptions
    {
        ShowHiddenSlides = false,
        SlideNumber = 0
    };
    EditableDocument editablePresentationDocument = editor.Edit(presentationEditOptions);
}
```
## 6. lépés: E-könyv-dokumentum létrehozása és szerkesztése
A GroupDocs.Editor lehetővé teszi az e-könyv formátumok, például az EPUB szerkesztését is. Így kezelheti.
### Létrehozása és szerkesztése az alapértelmezett beállításokkal
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EditableDocument defaultEditableEbookDocument = editor.Edit();
}
```
### Létrehozása és szerkesztése egyéni beállításokkal
Szabja személyre e-könyveinek szerkesztését az oldalszámozás és a nyelvi információk engedélyezésével vagy letiltásával.
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EbookEditOptions ebookEditOptions = new EbookEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true
    };
    EditableDocument editableEbookDocument = editor.Edit(ebookEditOptions);
}
```
## 7. lépés: E-mail dokumentum létrehozása és szerkesztése
Végül megnézzük, hogyan lehet szerkeszteni az e-mail dokumentumokat. Ez magában foglalja az olyan formátumokat, mint az EML.
### Létrehozása és szerkesztése az alapértelmezett beállításokkal
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EditableDocument defaultEditableEmailDocument = editor.Edit();
}
```
### Létrehozása és szerkesztése egyéni beállításokkal
Adja meg az e-mail üzenetek kimeneti beállításait a szerkesztési folyamat szabályozásához.
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EmailEditOptions emailEditOptions = new EmailEditOptions
    {
        MailMessageOutput = MailMessageOutput.All
    };
    EditableDocument editableEmailDocument = editor.Edit(emailEditOptions);
}
```
## 8. lépés: A folyamat lezárása
dokumentumok szerkesztése után kulcsfontosságú a memóriafolyam megfelelő ártalmatlanítása az erőforrások felszabadítása érdekében.
```csharp
memoryStream.Dispose();
System.Console.WriteLine("CreateDocument routine has successfully finished");
```
## Következtetés
A GroupDocs.Editor for .NET egy sokoldalú és hatékony eszköz, amely leegyszerűsíti a különféle dokumentumtípusok programozott szerkesztését. Ennek a lépésenkénti útmutatónak a követésével könnyedén hozhat létre és szerkeszthet dokumentumokat, legyenek azok WordProcessing-fájlok, táblázatok, prezentációk, e-könyvek vagy e-mailek. Merüljön el a GroupDocs.Editor dokumentációjában a fejlettebb szolgáltatásokért és testreszabási lehetőségekért.
## GYIK
### Milyen típusú dokumentumokat szerkeszthetek a GroupDocs.Editor for .NET segítségével?
Sokféle dokumentumot szerkeszthet, beleértve a Word Processing-ot, a táblázatokat, a prezentációkat, az e-könyveket és az e-maileket.
### Lehetséges a szerkesztési beállítások testreszabása?
Igen, a GroupDocs.Editor for .NET széleskörű testreszabást tesz lehetővé az egyes dokumentumtípusokra jellemző különféle szerkesztési beállítások révén.
### Hogyan kezelhetem a szerkesztett dokumentumok kimenetét?
visszahívási funkció segítségével a szerkesztett dokumentumfolyamot a kívánt helyre mentheti.
### Szükségem van licencre a GroupDocs.Editor for .NET használatához?
 Igen, kaphat engedélyt[itt](https://purchase.groupdocs.com/buy). Lehetőség van ideiglenes engedélyre is.
### Hol találok részletesebb dokumentációt?
 A részletes dokumentáció elérhető a[GroupDocs.Editor for .NET dokumentációs oldal](https://reference.groupdocs.com/editor/net/).