---
title: A szerkesztett dokumentum mentése különböző formátumokba
linktitle: A szerkesztett dokumentum mentése különböző formátumokba
second_title: GroupDocs.Editor .NET API
description: Ebből az átfogó, lépésenkénti útmutatóból megtudhatja, hogyan mentheti el a szerkesztett dokumentumokat különböző formátumokba a GroupDocs.Editor for .NET segítségével.
weight: 11
url: /hu/net/document-processing/save-edited-document-various-formats/
---
## Bevezetés
Különféle formátumokba szeretné menteni a szerkesztett dokumentumokat a GroupDocs.Editor for .NET segítségével? Jó helyre jöttél! Ez az átfogó útmutató végigvezeti a teljes folyamaton, a környezet beállításától a szerkesztett dokumentum többféle formátumban történő mentéséig. Merüljünk el, és tegyük gyerekjátékká a dokumentumszerkesztést és a mentést!
## Előfeltételek
Mielőtt elkezdené, győződjön meg arról, hogy rendelkezik az alábbiakkal:
1.  GroupDocs.Editor for .NET – Töltse le a legújabb verziót innen[itt](https://releases.groupdocs.com/editor/net/).
2. Fejlesztői környezet – Visual Studio vagy bármely más .NET-kompatibilis IDE.
3. .NET-keretrendszer – Győződjön meg arról, hogy telepítve van a .NET-keretrendszer 4.6.1-es vagy újabb verziója.
4. Mintadokumentum – Minta Word Processing dokumentum, amellyel dolgozni.
5. Alapszintű C# ismeretek - C# programozás ismerete szükséges.
## Névterek importálása
A kezdéshez feltétlenül importálja a szükséges névtereket a C# projektbe. Ez döntő fontosságú a GroupDocs.Editor funkcióinak eléréséhez.
```csharp
using System;
using GroupDocs.Editor.Metadata;
```
Bontsuk fel a folyamatot kezelhető lépésekre. Gondosan kövesse, hogy minden részt megértsen.
## 1. lépés: Szerezzen elérési utat a bemeneti fájlhoz
Először is meg kell adnia a bemeneti WordProcessing fájl elérési útját. Ez a fájl betöltődik és szerkeszthető.
```csharp
string inputFilePath = "Your Sample Document";
```
## 2. lépés: Hozzon létre betöltési beállításokat a dokumentumhoz
Ezután hozza létre a WordProcessing dokumentumokra jellemző betöltési beállításokat. Ezek a beállítások segítenek testreszabni a dokumentum betöltésének módját.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
```
## 3. lépés: Töltse be a dokumentumot az opciókkal
 Most töltse be a dokumentumot egy`Editor` példányt a megadott betöltési beállítások használatával.
```csharp
using (Editor editor = new Editor(inputFilePath, delegate { return loadOptions; }))
```
## 4. lépés: Szerkesztési beállítások létrehozása
Készítse elő a dokumentum szerkesztési beállításait. Ezek a beállítások határozzák meg, hogy a dokumentum hogyan nyílik meg szerkesztésre.
```csharp
WordProcessingEditOptions editOptions = new WordProcessingEditOptions();
```
## 5. lépés: Nyissa meg a dokumentumot szerkesztésre
 Nyissa meg a dokumentumot szerkesztésre egy`EditableDocument`példa. Ez a példány lehetővé teszi a dokumentum módosítását.
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
```
## 6. lépés: Szerkessze a dokumentum tartalmát
Itt az ideje, hogy szerkessze a dokumentum tartalmát. Először szerezze be a dokumentumot egyetlen base64 kódolású karakterláncként.
```csharp
string allEmbeddedInsideString = beforeEdit.GetEmbeddedHtml();
```
Például módosítsuk az alcímet a dokumentumban.
```csharp
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
```
## 7. lépés: Hozzon létre új szerkeszthető dokumentumot a szerkesztett tartalomból
 Újat csinálni`EditableDocument` példányt a szerkesztett tartalomból és forrásokból.
```csharp
using (EditableDocument afterEdit = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null))
```
## 8. lépés: Mentse el a dokumentumot különböző formátumokba
Végül ismételje meg az összes támogatott WordProcessing formátumot, és mentse el a szerkesztett dokumentumot minden formátumban.
```csharp
foreach (WordProcessingFormats oneFormat in WordProcessingFormats.All)
{
    // Készítse elő a mentési lehetőségeket
    WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(oneFormat);
    // Készítse elő a mentési útvonalat
    string savePath = Path.Combine("OutputDirectory", "MultipleOutFormats." + saveOptions.OutputFormat.Extension);
    // Mentse el a dokumentumot
    editor.Save(afterEdit, savePath, saveOptions);
}
```
## Befejezési üzenet
Befejezésül kinyomtathat egy üzenetet, amely jelzi, hogy a folyamat sikeresen befejeződött.
```csharp
Console.WriteLine("SavingEditedDocumentToAllFormats routine has successfully finished");
```
## Következtetés
Gratulálunk! Sikeresen megtanulta, hogyan mentheti a szerkesztett dokumentumokat különböző formátumokba a GroupDocs.Editor for .NET segítségével. Ezzel a hatékony eszközzel egyszerűen kezelheti és mentheti a dokumentumokat többféle formátumban, mindössze néhány sornyi kóddal. Ne feledje, hogy a legfontosabb lépések közé tartozik a dokumentum betöltése, a tartalom szerkesztése és a kívánt formátumba mentés.
## GYIK
### Mi az a GroupDocs.Editor for .NET?
A GroupDocs.Editor for .NET egy hatékony API, amely lehetővé teszi a dokumentumok különböző formátumú szerkesztését .NET-alkalmazások segítségével.
### Használhatom ingyenesen a GroupDocs.Editort?
 Igen, ingyenes próbaverzióval használhatod. Töltsd le[itt](https://releases.groupdocs.com/).
### Milyen formátumokat támogat a GroupDocs.Editor?
A GroupDocs.Editor a formátumok széles skáláját támogatja, beleértve a DOCX-et, PDF-et, HTML-t és még sok mást.
### Hogyan szerezhetek ideiglenes licencet a GroupDocs.Editor számára?
 Kaphat ideiglenes engedélyt[itt](https://purchase.groupdocs.com/temporary-license/).
### Hol találok további dokumentációt és támogatást?
 A részletes dokumentáció elérhető[itt](https://tutorials.groupdocs.com/editor/net/) , és támogatást kaphat[itt](https://forum.groupdocs.com/c/editor/20).