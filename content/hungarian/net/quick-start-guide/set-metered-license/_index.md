---
title: Állítsa be a mért licencet
linktitle: Állítsa be a mért licencet
second_title: GroupDocs.Editor .NET API
description: Átfogó útmutatónkból megtudhatja, hogyan integrálhatja és használhatja a GroupDocs.Editor for .NET programot. Oldja fel a hatékony dokumentumszerkesztési funkciókat .NET-alkalmazásaiban.
type: docs
weight: 12
url: /hu/net/quick-start-guide/set-metered-license/
---
## Bevezetés
Üdvözöljük a GroupDocs.Editor for .NET használatáról szóló, lépésenkénti útmutatónkban! Akár tapasztalt fejlesztő vagy, akár csak kezdő, ez az oktatóanyag segít kihasználni a nagy teljesítményű könyvtárban rejlő lehetőségeket. A GroupDocs.Editor for .NET segítségével könnyedén szerkesztheti a különféle formátumú dokumentumokat .NET-alkalmazásaiban. Merüljön el, és fedezze fel, hogyan kezdheti el ezzel a robusztus eszközzel.
## Előfeltételek
Mielőtt belevágnánk a technikai részletekbe, győződjön meg arról, hogy rendelkezik a következő előfeltételekkel:
- .NET programozási alapismeretek: C# és .NET Framework ismerete.
- A Visual Studio telepítve: Győződjön meg arról, hogy a Visual Studio legújabb verziója telepítve van a számítógépen.
-  GroupDocs.Editor for .NET: Töltse le a könyvtárat a[letöltési oldal](https://releases.groupdocs.com/editor/net/).
-  Érvényes engedély: Szerezzen be ideiglenes vagy teljes licencet a[GroupDocs vásárlási oldal](https://purchase.groupdocs.com/temporary-license/).
## Névterek importálása
GroupDocs.Editor for .NET használatához importálnia kell a szükséges névtereket a projektbe. Ez a lépés kulcsfontosságú, mivel beállítja a projektet, hogy kihasználja a könyvtár funkcióit.
```csharp
using System;
using GroupDocs.Editor;
```
Bontsuk le az egyes példákat több lépésre, hogy könnyen követhető legyen.
## 1. lépés: Telepítse a GroupDocs.Editor for .NET programot
Először is telepítenie kell a GroupDocs.Editor for .NET programot a projektjébe. Ezt a Visual Studio NuGet Package Manager segítségével teheti meg.
### Telepítés a NuGet Package Manageren keresztül
1. Nyissa meg projektjét a Visual Studióban.
2.  Menj`Tools` >`NuGet Package Manager` >`Manage NuGet Packages for Solution`.
3.  Keressen rá`GroupDocs.Editor`.
4.  Kattintson`Install`.
Ez hozzáadja a szükséges hivatkozásokat a projekthez.
## 2. lépés: Állítsa be a mért licencet
A GroupDocs.Editor teljes funkcióinak feloldásához be kell állítania egy fizetős licencet. Ez lehetővé teszi az API korlátozások nélküli használatát.
### A mért licenc beállítása
1.  Szerezze be nyilvános és privát kulcsait a[GroupDocs vásárlási oldal](https://purchase.groupdocs.com/temporary-license/).
2. Adja hozzá a következő kódot a projekthez a mért licenc beállításához:
```csharp
string publicKey = "*****";
string privateKey = "*****";
Metered metered = new Metered();
metered.SetMeteredKey(publicKey, privateKey);
Console.WriteLine("License set successfully.");
```
## 3. lépés: Töltsön be és szerkesszen egy dokumentumot
Most, hogy a projekt beállítása és licence megtörtént, térjünk át a dokumentum betöltésére és szerkesztésére.
### Dokumentum betöltése
1. Adja hozzá a következő kódot a dokumentum betöltéséhez:
```csharp
string filePath = "sample.docx";
Editor editor = new Editor(filePath);
Console.WriteLine("Document loaded successfully.");
```
### A dokumentum szerkesztése
2. A dokumentum szerkesztéséhez szerkeszthető formátumba kell konvertálnia:
```csharp
EditableDocument editableDocument = editor.Edit();
string content = editableDocument.GetContent();
Console.WriteLine("Document converted to editable format.");
```
## 4. lépés: Mentse el a szerkesztett dokumentumot
A dokumentum szerkesztése után az utolsó lépés a módosítások mentése.
### A dokumentum mentése
1. A szerkesztett tartalom visszaállítása az eredeti formátumba:
```csharp
string updatedContent = "<html><body>Updated content</body></html>";
editableDocument = EditableDocument.FromMarkup(updatedContent, new WordProcessingSaveOptions());
editor.Save(editableDocument, "updated_sample.docx");
Console.WriteLine("Document saved successfully.");
```
## Következtetés
 Gratulálunk! Sikeresen integrálta és használta a GroupDocs.Editor for .NET programot az alkalmazásában. A könyvtár telepítésétől a fizetős licenc beállításáig és a dokumentumok szerkesztéséig minden lényeges lépést megtett. Ez a hatékony eszköz jelentősen leegyszerűsítheti a dokumentumszerkesztési munkafolyamatokat a .NET-alkalmazásokon belül. További információkért lásd a[GroupDocs.Editor .NET dokumentációhoz](https://reference.groupdocs.com/editor/net/).
## GYIK
### Hogyan szerezhetek GroupDocs.Editor licencet?
 Engedélyt szerezhet a[GroupDocs vásárlási oldal](https://purchase.groupdocs.com/buy) . Ideiglenes engedélyért látogasson el ide[itt](https://purchase.groupdocs.com/temporary-license/).
### Ingyenesen kipróbálhatom a GroupDocs.Editort?
 Igen, letölthet egy ingyenes próbaverziót a webhelyről[letöltési oldal](https://releases.groupdocs.com/) és kérjen ideiglenes engedélyt.
### Milyen dokumentumformátumokat támogat a GroupDocs.Editor?
 A GroupDocs.Editor különféle formátumokat támogat, beleértve a DOCX, PPTX, XLSX, TXT, HTML és egyebeket. A teljes lista megtekintéséhez ellenőrizze a[dokumentáció](https://reference.groupdocs.com/editor/net/).
### Elérhető közösségi támogatás a GroupDocs.Editor számára?
 Igen, közösségi támogatást kaphat a[GroupDocs.Editor fórum](https://forum.groupdocs.com/c/editor/20).
### Hogyan kezdhetem el a GroupDocs.Editor for .NET használatát?
 Kövesse lépésenkénti útmutatónkat a könyvtár beállításához, a licenc megszerzéséhez és a dokumentumok szerkesztésének megkezdéséhez. Részletes útmutatásért keresse fel a[dokumentáció](https://reference.groupdocs.com/editor/net/).