---
title: A szerkeszthető dokumentumok speciális használata
linktitle: A szerkeszthető dokumentumok speciális használata
second_title: GroupDocs.Editor .NET API
description: Tanulja meg a GroupDocs.Editor haladó használatát a .NET-es dokumentumokból való erőforrások programozott létrehozásához, szerkesztéséhez és kinyeréséhez.
type: docs
weight: 11
url: /hu/net/document-editing/advanced-usage-of-editable-documents/
---
## Bevezetés
Ha Ön .NET-fejlesztő, aki szeretné javítani dokumentumszerkesztési képességeit, a GroupDocs.Editor for .NET hatékony eszközkészletet kínál. Ez az átfogó útmutató végigvezeti Önt a szerkeszthető dokumentumok GroupDocs.Editor használatával haladó használatán, részletesen lebontva az egyes lépéseket, hogy biztosítsa a benne rejlő lehetőségek teljes kihasználását.
## Előfeltételek
Mielőtt belemerülne a speciális funkciókba, győződjön meg arról, hogy rendelkezik a következőkkel:
- A Visual Studio telepítve van a fejlesztőgépre.
- .NET Framework kompatibilis a GroupDocs.Editorral.
-  GroupDocs.Editor .NET könyvtárhoz. tudsz[töltse le itt](https://releases.groupdocs.com/editor/net/).
-  Érvényes GroupDocs.Editor licenc. Kaphatsz a[ingyenes próbaverzió](https://releases.groupdocs.com/) vagy vásárolni a[ideiglenes engedély](https://purchase.groupdocs.com/temporary-license/).
## Névterek importálása
Kezdésként győződjön meg róla, hogy importálja a szükséges névtereket a .NET-projektbe:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```
## 1. lépés: Szerkeszthető dokumentumpéldány létrehozása
 Először is létre kell hoznia egy példányt`EditableDocument` támogatott formátumú bemeneti dokumentum betöltésével és szerkesztésével.
```csharp
string inputFilePath = "YourSampleDocument.docx";
Editor editor = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```
Ebben a lépésben betöltjük a bemeneti dokumentumot és előkészítjük szerkesztésre.
## 2. lépés: Dokumentumforrások kibontása
 A`EditableDocument` különféle forrásokat tartalmaz, amelyek kinyerhetők és manipulálhatók. Bontsuk fel ezeket:
### 2.1. lépés: A teljes dokumentum kibontása HTML formátumban
Létrehozhat egyetlen karakterláncot, amely tartalmazza a teljes dokumentumot és annak összes erőforrását HTML formátumban.
```csharp
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```
Ez a karakterlánc elég nagy lesz, mivel stíluslapokat, képeket és base64-ben kódolt betűtípusokat tartalmaz.
### 2.2. lépés: Az összes kép kibontása
Az összes kép kibontása a dokumentumból.
```csharp
List<IImageResource> allImages = beforeEdit.Images;
```
### 2.3. lépés: Az összes betűtípus kibontása
Bontsa ki a dokumentumban használt összes betűtípust.
```csharp
List<FontResourceBase> allFonts = beforeEdit.Fonts;
```
### 2.4. lépés: Az összes stíluslap kibontása
Az összes stíluslap kibontása szöveges formátumban.
```csharp
List<CssText> allStylesheets = beforeEdit.Css;
```
### 2.5. lépés: Gyűjtsd össze az összes erőforrást
Gyűjtsön össze minden erőforrást egy hívásban.
```csharp
List<IHtmlResource> allResources = beforeEdit.AllResources;
```
Ez magában foglalja a képeket, a betűtípusokat és a stíluslapokat.
### 2.6. lépés: Szerezze be a HTML-jelölést
Szerezze be a dokumentum HTML-jelölését beágyazott erőforrások nélkül.
```csharp
string htmlMarkup = beforeEdit.GetContent();
```
## 3. lépés: A külső hivatkozások beállítása
Néha módosítania kell a külső hivatkozásokat, hogy egy egyéni erőforrás-kezelőre mutassanak. Íme, hogyan kell csinálni:
### 3.1. lépés: Készítsen egyéni előtagokat
Készítsen előtagokat, amelyek az eredeti külső hivatkozásokat hozzáfűzik.
```csharp
string customImagesRequesthandlerUri = "http://example.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://example.com/CssHandler/id=";
string customFontsRequesthandlerUri = "http://example.com/FontsHandler/id=";
```
### 3.2. lépés: Előtagolt HTML-jelölés létrehozása
Hozzon létre HTML-jelölést módosított hivatkozásokkal.
```csharp
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```
### 3.3. lépés: Szerezzen csak testet tartalmazó HTML-tartalmat
Egyes WYSIWYG-szerkesztők csak tiszta HTML-jelölést kezelnek fejlécek nélkül.
```csharp
string onlyBodyContent = beforeEdit.GetBodyContent();
```
### 3.4. lépés: Előtaggal ellátott, csak szöveges tartalom
Hozzon létre csak test tartalmat egyéni képelőtagokkal.
```csharp
string prefixedBodyContent = beforeEdit.GetBodyContent(customImagesRequesthandlerUri);
```
### 3.5. lépés: Stíluslapok kibontása
A dokumentumban használt stíluslapok kibontása.
```csharp
List<string> stylesheets = beforeEdit.GetCssContent();
```
### 3.6. lépés: Előtagozott stíluslapok
Stíluslapok kibontása egyéni előtagokkal.
```csharp
List<string> prefixedStylesheets = beforeEdit.GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri);
```
## 4. lépés: Mentse el a dokumentumot HTML-ként
Mentse el a szerkesztett dokumentumot HTML-fájlként, beleértve az erőforrásokat is.
```csharp
string htmlFilePath = Path.Combine("output", Path.GetFileNameWithoutExtension(inputFilePath) + ".html");
beforeEdit.Save(htmlFilePath);
```
Ez a módszer külön könyvtárat hoz létre az olyan erőforrások számára, mint a stíluslapok, képek és betűtípusok.
## 5. lépés: A EditableDocument megsemmisítése
 EditableDocument implementációk`IDisposable` és lehetőséget biztosít annak ellenőrzésére, hogy a példány megsemmisült-e.
```csharp
Console.WriteLine("EditableDocument is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");
```
### 5.1. lépés: Az ártalmatlanítási esemény kezelése
Feliratkozhat az ártalmatlanítási eseményre is.
```csharp
EventHandler someMethod = delegate { Console.WriteLine("Disposing event was spotted!"); };
beforeEdit.Disposed += someMethod;
```
## 6. lépés: EditableDocument létrehozása HTML-ből
Hozzon létre egy EditableDocument példányt egy HTML-dokumentumból.
### 6.1. lépés: HTML fájlból
```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
```
### 6.2. lépés: A HTML-jelölésből
```csharp
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);
```
Ezek a példányok (afterEditFromFile és afterEditFromMarkup) megegyeznek az eredetivel (beforeEdit).
## 7. lépés: Kézi ártalmatlanítás
Kézzel semmisítse meg az EditableDocument példányait.
```csharp
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```
Ez biztosítja az erőforrások megfelelő tisztítását.
## Következtetés
GroupDocs.Editor for .NET robusztus eszközöket biztosít a dokumentumok programozott szerkesztéséhez. Ennek a lépésenkénti útmutatónak a követésével hatékonyan kezelheti a dokumentumtartalmat, az erőforrásokat és a kimeneti formátumokat. Akár erőforrásokat ágyaz be, akár külső hivatkozásokat állít be, akár dokumentumokat konvertál HTML formátumba, a GroupDocs.Editor felvértezi a haladó dokumentumkezeléshez szükséges funkciókkal.
## GYIK
### Milyen formátumokat támogat a GroupDocs.Editor?
A GroupDocs.Editor különféle formátumokat támogat, beleértve a DOCX, XLSX, PPTX és egyebeket.
### Használhatom a GroupDocs.Editort licenc nélkül?
 Igen, használhatod a[ingyenes próbaverzió](https://releases.groupdocs.com/) vagy a[ideiglenes engedély](https://purchase.groupdocs.com/temporary-license/).
### Hogyan nyerhetek ki meghatározott erőforrásokat egy dokumentumból?
 Képeket, betűtípusokat és stíluslapokat bonthat ki a megadott módszerekkel, például`Images`, `Fonts` , és`Css`.
### Lehetséges a hivatkozásokat módosítani a HTML kimenetben?
Igen, módosíthatja a külső hivatkozásokat egyéni előtagok megadásával a képekhez, a CSS-hez és a betűtípusokhoz.
### Hogyan menthetek el szerkesztett dokumentumot HTML-fájlként?
 Használja a`Save` módszere a`EditableDocument`osztályt, hogy a dokumentumot HTML-fájlként mentse, beleértve az erőforrásokat is.