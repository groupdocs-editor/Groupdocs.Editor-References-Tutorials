---
title: HTML törzstartalom lekérése
linktitle: HTML törzstartalom lekérése
second_title: GroupDocs.Editor .NET API
description: Letöltheti a HTML törzstartalmat a GroupDocs.Editor for .NET segítségével lépésenkénti útmutatónkkal. Bővítse .NET-alkalmazásait könnyedén.
weight: 10
url: /hu/net/html-content-retrieval/retrieve-html-body-content/
---

# HTML törzstartalom lekérése

## Bevezetés
Készen áll arra, hogy forradalmasítsa a .NET-alkalmazások dokumentumszerkesztésének kezelését? Ne keressen tovább, mint a GroupDocs.Editor for .NET! Ez a hatékony eszköz lehetővé teszi a különféle dokumentumformátumok zökkenőmentes szerkesztését közvetlenül az alkalmazáson belül. Akár Word-, akár PDF- vagy HTML-kóddal dolgozik, a GroupDocs.Editor segítségével külső eszközök nélkül is könnyen szerkesztheti és kezelheti a dokumentumokat.
## Előfeltételek
Mielőtt elkezdenénk, meg kell felelnie néhány előfeltételnek:
- .NET programozási alapismeretek: A C# és a .NET keretrendszer ismerete segít a példák követésében.
-  GroupDocs.Editor for .NET: Letöltheti a[GroupDocs.Editor letöltési oldal](https://releases.groupdocs.com/editor/net/).
-  Érvényes licenc: Licenc vásárolható a[GroupDocs vásárlási oldal](https://purchase.groupdocs.com/buy) vagy kérjen a[ideiglenes engedély](https://purchase.groupdocs.com/temporary-license/).
- Integrált fejlesztői környezet (IDE): a legjobb fejlesztési élmény érdekében a Visual Studio ajánlott.
## Névterek importálása
A GroupDocs.Editor for .NET használatának megkezdéséhez importálnia kell a szükséges névtereket. Ez lehetővé teszi a dokumentumszerkesztéshez szükséges osztályok és módszerek elérését.
```csharp
using System;
using GroupDocs.Editor.Options;
```
## 1. lépés: Inicializálja a szerkesztőt
Eljárásunk első lépése az, hogy inicializáljuk a`Editor` osztályt a dokumentumával. Ez az osztály az összes szerkesztési művelet belépési pontja.

Be kell töltenie a szerkeszteni kívánt dokumentumot. Ebben a példában egy minta Word dokumentumot fogunk használni.
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
    // Folytassa a következő lépéssel
}
```
## 2. lépés: Szerkessze a dokumentumot
 Ezután a`Edit` módszere a`Editor` osztályban a dokumentum szerkeszthető változatának létrehozásához.

 Megadjuk a dokumentum szerkesztési beállításait. Ebben az esetben használjuk`WordProcessingEditOptions`.
```csharp
using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
{
    // Folytassa a következő lépéssel
}
```
## 3. lépés: Töltse le a HTML törzstartalmat
Most lekérjük a dokumentum törzs tartalmát HTML formátumban. Itt történik a varázslat!

 Használni a`GetBodyContent` módszerrel kinyerhetjük a HTML belső tartalmát`<body>` elem.
```csharp
string bodyContent = document.GetBodyContent();
Console.WriteLine("Inner content of the HTML->BODY element: {0}", bodyContent);
```

## Következtetés
Gratulálunk! Sikeresen megtanulta, hogyan kérhet le HTML törzstartalmat egy dokumentumból a GroupDocs.Editor for .NET segítségével. Ez a hatékony könyvtár leegyszerűsíti a .NET-alkalmazásokon belüli dokumentumok szerkesztését, így értékes eszközzé teszi a fejlesztők számára.
## GYIK
### Milyen fájlformátumokat támogat a GroupDocs.Editor?
GroupDocs.Editor a fájlformátumok széles skáláját támogatja, beleértve a Word dokumentumokat, PDF-eket, Excel-táblázatokat, PowerPoint-bemutatókat és HTML-fájlokat.
### Hogyan szerezhetek ideiglenes licencet a GroupDocs.Editor számára?
 Ideiglenes engedélyt kérhet a[GroupDocs ideiglenes licencoldal](https://purchase.groupdocs.com/temporary-license/).
### Van ingyenes próbaverzió a GroupDocs.Editor számára?
 Igen, letölthet egy ingyenes próbaverziót a webhelyről[GroupDocs.Editor letöltési oldal](https://releases.groupdocs.com/).
### Használhatom a GroupDocs.Editort .NET Core-al?
Igen, a GroupDocs.Editor kompatibilis a .NET Core programmal, rugalmasságot biztosítva a modern alkalmazásfejlesztéshez.
### Hol találok további példákat és dokumentációt a GroupDocs.Editorhoz?
 További példákat és részletes dokumentációt találhat a[GroupDocs.Editor dokumentációs oldal](https://tutorials.groupdocs.com/editor/net/).