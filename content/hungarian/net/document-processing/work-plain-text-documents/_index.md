---
title: Egyszerű szöveges dokumentumok használata
linktitle: Egyszerű szöveges dokumentumok használata
second_title: GroupDocs.Editor .NET API
description: Ismerje meg, hogyan szerkeszthet egyszerű szöveges dokumentumokat a GroupDocs.Editor for .NET segítségével lépésenkénti útmutatónkkal. Egyszerűsítse a .NET-dokumentumszerkesztési folyamatot.
weight: 15
url: /hu/net/document-processing/work-plain-text-documents/
type: docs
---
# Egyszerű szöveges dokumentumok használata

## Bevezetés
Egyszerűsíteni szeretné dokumentumszerkesztési folyamatát .NET-ben? Ne keressen tovább, mint a GroupDocs.Editor for .NET! Ez a hatékony API lehetővé teszi a dokumentumformátumok széles skálájának egyszerű szerkesztését. Ebben az oktatóanyagban végigvezetjük az egyszerű szöveges dokumentumokkal való munkafolyamaton a GroupDocs.Editor for .NET használatával. A végére felkészülten kezelheti a szöveges dokumentumok szerkesztését, mint egy profi. Készen állsz a merülésre? Kezdjük el!
## Előfeltételek
Mielőtt elkezdenénk, néhány dolgot meg kell tennie:
- .NET fejlesztői környezet: Győződjön meg arról, hogy be van állítva egy működő .NET fejlesztői környezet. A Visual Studio népszerű választás.
-  GroupDocs.Editor for .NET: Töltse le és telepítse a[GroupDocs.Editor for .NET](https://releases.groupdocs.com/editor/net/).
- Alapvető C# ismeretek: A C# programozási nyelv ismerete segít a példák követésében.
- Szövegszerkesztő: Bármely szövegszerkesztő megteszi, bár a Visual Studio Code ajánlott szolgáltatásai és könnyű használhatósága miatt.
## Névterek importálása
A GroupDocs.Editor for .NET használatának megkezdéséhez importálnia kell a szükséges névtereket a projektbe. Ez biztosítja, hogy az összes szükséges osztály és metódus elérhető legyen a használatra.
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```
Bontsuk fel a folyamatot kezelhető lépésekre. Kövesse végig, ahogy végigvezetjük az egyszerű szöveges dokumentumok szerkesztésének minden szakaszán a GroupDocs.Editor for .NET használatával.
## 1. lépés: Szerezzen elérési utat a bemeneti TXT fájlhoz
Először is meg kell adnia a bemeneti TXT fájl elérési útját. Ez lehet egy helyi fájl elérési útja vagy a fájl tartalmát tartalmazó adatfolyam.
```csharp
string inputFilePath = "YourSampleDocument.txt";
```
## 2. lépés: Hozzon létre egy szerkesztőpéldányt
 Ezután hozzon létre egy példányt a`Editor` osztály. Ez az osztály felelős a dokumentumok betöltéséért és szerkesztéséért. Ebben a szakaszban nincs szükség terhelési opciókra.
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## 3. lépés: Hozzon létre TXT szerkesztési beállításokat
Most hozza létre a TXT szerkesztési beállításokat. Ezek az opciók lehetővé teszik annak megadását, hogy a szöveges tartalmat hogyan kell feldolgozni a szerkesztés során.
```csharp
    TextEditOptions editOptions = new TextEditOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        RecognizeLists = true,
        LeadingSpaces = TextLeadingSpacesOptions.ConvertToIndent,
        TrailingSpaces = TextTrailingSpacesOptions.Trim
    };
```
## 4. lépés: Hozzon létre egy EditableDocument példányt
 A beállított szerkesztési beállításokkal hozzon létre egy`EditableDocument` példa. Ez a dokumentumot szerkeszthető formátumban jeleníti meg.
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## 5. lépés: Szerkessze a dokumentum tartalmát
Töltse le az eredeti szöveges tartalmat, és végezze el a kívánt módosításokat. Ebben a példában a "szöveg" szót a "SZERKESZTETT szövegre" cseréljük.
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("text", "EDITED text");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## 6. lépés: Hozzon létre egy szerkeszthető dokumentumot frissített tartalommal
 A szükséges módosítások elvégzése után hozzon létre egy újat`EditableDocument` a frissített tartalommal és az eredeti forrásokkal.
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## 7. lépés: Hozza létre a WordProcessing mentési beállításait
Készítse elő a mentési beállításokat a WordProcessing formátumhoz. Ez a példa a DOCM formátumot használja, és megadja a területi beállítást.
```csharp
    WordProcessingSaveOptions wordSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm)
    {
        Locale = System.Globalization.CultureInfo.GetCultureInfo("en-GB")
    };
```
## 8. lépés: Hozzon létre TXT mentési beállításokat
Hasonlóképpen hozza létre a TXT formátum mentési beállításait. Győződjön meg arról, hogy a kódolás UTF-8-ra van állítva, és őrizze meg a táblázat elrendezését.
```csharp
    TextSaveOptions txtSaveOptions = new TextSaveOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        PreserveTableLayout = true
    };
```
## 9. lépés: Készítse elő a kimeneti útvonalakat
Készítse elő az elérési útvonalakat az eredményül kapott DOCX és TXT fájlok mentéséhez. Használja a bemeneti fájl elérési útját a kimeneti könyvtár és a fájlnevek meghatározásához.
```csharp
    string outputWordPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".docm");
    string outputTxtPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".txt");
```
## 10. lépés: Mentse el a szerkesztett dokumentumot
Végül mentse a szerkesztett dokumentumot DOCX és TXT formátumban is a megadott mentési beállításokkal.
```csharp
    editor.Save(afterEdit, outputWordPath, wordSaveOptions);
    editor.Save(afterEdit, outputTxtPath, txtSaveOptions);
}
System.Console.WriteLine("Document editing process completed successfully!");
```
## Következtetés
 Gratulálunk! Sikeresen szerkesztett egy egyszerű szöveges dokumentumot a GroupDocs.Editor for .NET segítségével. Ez a hatékony eszköz leegyszerűsíti a dokumentumok szerkesztését, így könnyen integrálható a .NET-alkalmazásokba. Függetlenül attól, hogy egyszerű szöveges fájlokat vagy összetett dokumentumformátumokat kezel, a GroupDocs.Editor mindent megtalál. Fedezzen fel további funkciókat és képességeket, ha felkeresi a[GroupDocs.Editor dokumentáció](https://tutorials.groupdocs.com/editor/net/).
## GYIK
### Milyen fájlformátumokat támogat a GroupDocs.Editor for .NET?
 A GroupDocs.Editor for .NET a fájlformátumok széles skáláját támogatja, beleértve a DOCX, TXT, HTML és egyebeket. Ellenőrizd a[dokumentáció](https://tutorials.groupdocs.com/editor/net/) a teljes listáért.
### Hogyan szerezhetem be a GroupDocs.Editor ingyenes próbaverzióját .NET-hez?
 Letöltheti a GroupDocs.Editor .NET-hez készült ingyenes próbaverzióját a webhelyről[kiadások oldala](https://releases.groupdocs.com/).
### Vásárolhatok ideiglenes licencet a GroupDocs.Editor for .NET számára?
Igen, ideiglenes engedélyt kaphat a[GroupDocs vásárlási oldal](https://purchase.groupdocs.com/temporary-license/).
### Hol kaphatok támogatást a GroupDocs.Editor for .NET-hez?
 A támogatás a következőn keresztül érhető el[GroupDocs.Editor támogatási fórum](https://forum.groupdocs.com/c/editor/20).
### Elérhető-e részletes dokumentáció a GroupDocs.Editor for .NET-hez?
 Igen, a részletes dokumentáció elérhető a[GroupDocs.Editor dokumentációs oldal](https://tutorials.groupdocs.com/editor/net/).