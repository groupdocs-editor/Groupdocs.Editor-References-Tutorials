---
title: Dokumentum mentése
linktitle: Dokumentum mentése
second_title: GroupDocs.Editor .NET API
description: Könnyedén szerkesztheti és mentheti a dokumentumokat a GroupDocs.Editor for .NET segítségével. Ez a lépésenkénti útmutató leegyszerűsíti a folyamatot a fejlesztők számára.
type: docs
weight: 14
url: /hu/net/document-editing/save-document/
---
## Bevezetés
Könnyedén szeretne dokumentumokat szerkeszteni és menteni a GroupDocs.Editor for .NET segítségével? Jó helyen jársz! Ez az oktatóanyag lépésről lépésre végigvezeti a folyamaton, így biztosítva, hogy könnyedén kezelhesse dokumentumait. Akár tapasztalt fejlesztő, akár kezdő, útmutatónk minden információt megad, amelyre szüksége van a kezdéshez.
## Előfeltételek
Mielőtt belevágna az oktatóanyagba, győződjön meg arról, hogy a következő előfeltételeket teljesítette:
- Fejlesztési környezet: A Visual Studio telepítve van a gépre.
- .NET-keretrendszer: Győződjön meg arról, hogy rendelkezik a .NET-keretrendszer 4.6.1-es vagy újabb verziójával.
-  GroupDocs.Editor for .NET: Töltse le a legújabb verziót[itt](https://releases.groupdocs.com/editor/net/).
- Alapvető C# ismeretek: A C# programozás ismerete elengedhetetlen.
## Névterek importálása
GroupDocs.Editor használatához a .NET-projektben importálnia kell a szükséges névtereket. Íme, hogyan kell csinálni:
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
Most, hogy beállítottuk a környezetünket és importáltuk a szükséges névtereket, vessünk egy pillantást a dokumentumok betöltéséhez, szerkesztéséhez és mentéséhez szükséges lépésekbe a GroupDocs.Editor for .NET segítségével.
## 1. lépés: Töltse be a dokumentumot
Először is be kell töltenünk a szerkeszteni kívánt dokumentumot. A GroupDocs.Editor ezt a folyamatot egyszerűvé teszi. A következőképpen teheti meg:

```csharp
string inputFilePath = "Your Sample Document";
Editor editor = new Editor(inputFilePath, delegate { return new Options.WordProcessingLoadOptions(); });
EditableDocument defaultWordProcessingDoc = editor.Edit();
```
 Ebben a lépésben megadjuk a szerkeszteni kívánt dokumentum elérési útját, és létrehozzuk a példányt`Editor` osztály. A`Edit` metódus hívódik meg a dokumentum betöltéséhez egy`EditableDocument` tárgy.
## 2. lépés: Módosítsa a dokumentumot
Miután a dokumentum betöltődött, ideje néhány módosítást végrehajtani. Mivel nincs WYSIWYG szerkesztőnk, a szerkesztési folyamatot kódban szimuláljuk.

```csharp
string allEmbeddedInsideString = defaultWordProcessingDoc.GetEmbeddedHtml();
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
EditableDocument editedDoc = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```
 Itt lekérjük a dokumentum beágyazott HTML-tartalmát, végrehajtunk egy egyszerű szövegcserét, és létrehozunk egy újat`EditableDocument`példányt a módosított HTML-ből.
## 3. lépés: Mentse el a dokumentumot
A dokumentum szerkesztése után az utolsó lépés a mentés. A GroupDocs.Editor többféle lehetőséget kínál a dokumentum különböző formátumokban történő mentésére.
## Mentés RTF-ként
```csharp
string outputRtfPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.rtf");
WordProcessingSaveOptions rtfSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
editor.Save(editedDoc, outputRtfPath, rtfSaveOptions);
```
## Mentés DOCM-ként
```csharp
string outputDocmPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.docm");
WordProcessingSaveOptions docmSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm);
using (FileStream outputStream = File.Create(outputDocmPath))
{
    editor.Save(editedDoc, outputStream, docmSaveOptions);
}
```
## Mentés egyszerű szövegként
```csharp
string outputTxtPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.txt");
TextSaveOptions textSaveOptions = new TextSaveOptions
{
    Encoding = System.Text.Encoding.UTF8,
    PreserveTableLayout = true
};
editor.Save(editedDoc, outputTxtPath, textSaveOptions);
```
## 4. lépés: Tisztítás
 Végül nagyon fontos, hogy megsemmisítsék a`EditableDocument` és`Editor` példányokat az erőforrások felszabadítására.
```csharp
editedDoc.Dispose();
defaultWordProcessingDoc.Dispose();
editor.Dispose();
```
Ha követi ezeket a lépéseket, hatékonyan tölthet be, szerkeszthet és menthet dokumentumokat a GroupDocs.Editor for .NET segítségével. Ez a hatékony eszköz rugalmasságot és egyszerű használatot biztosít, így a dokumentumkezelés gyerekjáték.
## Következtetés
A dokumentumok programozott szerkesztése és mentése még soha nem volt ilyen egyszerű a GroupDocs.Editor for .NET segítségével. Ez az útmutató végigvezeti Önt a teljes folyamaton, a dokumentum betöltésétől a különféle formátumokban történő mentéséig. A GroupDocs.Editor segítségével sokoldalú és robusztus megoldást kaphat, amely leegyszerűsíti a dokumentumszerkesztési folyamatot.
## GYIK
### Milyen fájlformátumokat támogat a GroupDocs.Editor?
 GroupDocs.Editor különféle fájlformátumokat támogat, beleértve a DOCX, RTF, TXT és még sok más formátumot. A teljes lista megtekintéséhez nézze meg a[dokumentáció](https://reference.groupdocs.com/editor/net/).
### Kipróbálhatom a GroupDocs.Editort vásárlás előtt?
 Igen, kaphat a[ingyenes próbaverzió](https://releases.groupdocs.com/) hogy tesztelje a GroupDocs.Editor szolgáltatásait.
### Van-e valamilyen támogatás, ha problémákkal szembesülök?
 Teljesen! Meglátogathatja a[támogatói fórum](https://forum.groupdocs.com/c/editor/20) segítségért bármilyen felmerülő problémához.
### Hogyan szerezhetek ideiglenes engedélyt?
 Kérheti a[ideiglenes engedély](https://purchase.groupdocs.com/temporary-license/) értékelési célokra.
### Hol vásárolhatom meg a GroupDocs.Editor teljes verzióját?
 Megvásárolhatja a teljes verziót[itt](https://purchase.groupdocs.com/buy).