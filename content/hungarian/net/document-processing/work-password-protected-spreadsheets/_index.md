---
title: Dolgozzon jelszóval védett táblázatokkal
linktitle: Dolgozzon jelszóval védett táblázatokkal
second_title: GroupDocs.Editor .NET API
description: Ismerje meg, hogyan kezelheti a jelszóval védett táblázatokat a GroupDocs.Editor for .NET segítségével. Ez a részletes útmutató végigvezeti a biztonságos Excel-fájlok megnyitásán.
weight: 18
url: /hu/net/document-processing/work-password-protected-spreadsheets/
type: docs
---
# Dolgozzon jelszóval védett táblázatokkal

## Bevezetés
Nehezen kezeli a jelszóval védett táblázatokat .NET-alkalmazásaiban? Ha igen, akkor jó helyen jársz! Ebben az átfogó útmutatóban végigvezetjük a GroupDocs.Editor for .NET használatának folyamatán a jelszóval védett táblázatok hatékony kezeléséhez. Az oktatóanyag végére jól felkészült lesz a titkosított Excel-fájlok egyszerű megnyitására, szerkesztésére és mentésére.
## Előfeltételek
Mielőtt belemerülnénk a kódba, győződjünk meg arról, hogy rendelkezik mindennel, ami a követéshez szükséges:
- Alapvető C# ismerete: Ez az oktatóanyag feltételezi, hogy ismeri a C# programozást.
- .NET-keretrendszer: Győződjön meg arról, hogy a .NET-keretrendszer telepítve van a fejlesztőgépen.
-  GroupDocs.Editor for .NET: Töltse le és telepítse a GroupDocs.Editor for .NET programot innen:[itt](https://releases.groupdocs.com/editor/net/).
## Névterek importálása
A kezdéshez importálnia kell a szükséges névtereket a C# projektbe. Ezek a névterek hozzáférést biztosítanak a GroupDocs.Editor funkcióihoz.
```csharp
using System;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
## 1. lépés: Szerezzen elérési utat a bemeneti fájlhoz
Először is szüksége lesz egy elérési útra a bemeneti fájlhoz. Ebben a példában egy minta Excel fájlt fogunk használni (`Your Sample Document`), amely jelszóval védett.
```csharp
string inputFilePath = "Your Sample Document";
```
## 2. lépés: Próbálja meg megnyitni a dokumentumot jelszó nélkül
Nézzük meg, mi történik, ha jelszó megadása nélkül próbáljuk megnyitni a dokumentumot.
```csharp
Editor editor = new Editor(inputFilePath);
try
{
    editor.Edit();
}
catch (GroupDocs.Editor.PasswordRequiredException)
{
    Console.WriteLine("Cannot edit the document because it is password-protected. A password is required.");
}
editor.Dispose();
```
## 3. lépés: Próbáljon meg helytelen jelszót megadni
Most helytelen jelszót adunk meg annak bemutatására, hogyan reagál a szerkesztő.
```csharp
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.Password = "incorrect_password";
editor = new Editor(inputFilePath, delegate { return loadOptions; });
try
{
    editor.Edit();
}
catch (GroupDocs.Editor.IncorrectPasswordException)
{
    Console.WriteLine("Cannot edit the document because the specified password is incorrect.");
}
editor.Dispose();
```
## 4. lépés: Nyissa meg a fájlt a megfelelő jelszóval
Adjuk meg a helyes jelszót, és nyissa meg sikeresen a fájlt.
```csharp
loadOptions.Password = "excel_password";
loadOptions.OptimizeMemoryUsage = true;
editor = new Editor(inputFilePath, delegate { return loadOptions; });
```
## 5. lépés: Szerkesztési beállítások létrehozása és módosítása
A táblázat szerkesztéséhez létre kell hoznunk és módosítanunk kell a szerkesztési beállításokat.
```csharp
SpreadsheetEditOptions editOptions = new SpreadsheetEditOptions();
```
## 6. lépés: Hozzon létre egy köztes szerkeszthető dokumentumot
 Ezután létrehozunk egy közteset`EditableDocument` amely lehetővé teszi számunkra, hogy módosítsuk a táblázatot.
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
{
    // 7. lépés: Hozzon létre mentési beállításokat
    SpreadsheetFormats xlsmFormat = SpreadsheetFormats.Xlsm;
    SpreadsheetSaveOptions saveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
    // 7.1. lépés: Állítson be új nyitó jelszót
    saveOptions.Password = "new password";
    // 7.2. lépés: Állítsa be az írásvédelmet
    saveOptions.WorksheetProtection = new WorksheetProtection(WorksheetProtectionType.All, "write password");
    // 8. lépés: Mentse el a dokumentumot módosítás nélkül
    //8.1. lépés: Készítse elő a kimeneti fájl nevét és elérési útját
    string outputFilename = Path.GetFileNameWithoutExtension(inputFilePath) + "." + xlsmFormat.Extension;
    string outputPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename);
    // 8.2. lépés: Kimeneti adatfolyam létrehozása
    using (FileStream outputStream = File.Create(outputPath))
    {
        // 8.3. lépés: Mentés
        editor.Save(beforeEdit, outputStream, saveOptions);
    }
}
// 9. lépés: Dobja ki a szerkesztőpéldányt
editor.Dispose();
Console.WriteLine("Successfully handled the password-protected spreadsheet. Editor instance has been disposed: {0}", editor.IsDisposed ? "Yes" : "No");
```
## Következtetés
Gratulálunk! Sikeresen megtanulta a jelszóval védett táblázatok kezelését a GroupDocs.Editor for .NET segítségével. A dokumentum jelszó nélküli megnyitásának kísérletétől az új védelmi beállításokkal történő mentéséig minden lényeges lépést megtett. Ez a tudás kétségtelenül javítja a biztonságos dokumentumok kezelésének képességét a .NET-alkalmazásokon belül.
## GYIK
### Mi az a GroupDocs.Editor for .NET?
A GroupDocs.Editor for .NET egy hatékony dokumentumszerkesztő API, amely lehetővé teszi a fejlesztők számára, hogy különféle dokumentumformátumokat töltsenek be, szerkesszenek és mentsenek a .NET-alkalmazásokon belül.
### Hogyan szerezhetek ideiglenes licencet a GroupDocs.Editor számára?
 Ideiglenes jogosítványt szerezhet be[itt](https://purchase.groupdocs.com/temporary-license/) hogy értékelje a termék tulajdonságait.
### Lehetséges-e optimalizálni a memóriahasználatot nagy dokumentumok szerkesztése közben?
 Igen, engedélyezheti a memóriaoptimalizálást a`OptimizeMemoryUsage` tulajdonát`true` betöltési lehetőségek között.
### Beállíthatok különböző jelszavakat a táblázat megnyitásához és írásához?
Teljesen! A mentési opciók segítségével külön jelszavakat állíthat be a dokumentum megnyitásához és az írásvédelemhez.
### Hol találok részletesebb dokumentációt?
 Hozzáférhet a GroupDocs.Editor for .NET átfogó dokumentációjához[itt](https://tutorials.groupdocs.com/editor/net/).