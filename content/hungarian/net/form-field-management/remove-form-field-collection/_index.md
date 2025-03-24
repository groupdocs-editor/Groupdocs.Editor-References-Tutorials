---
title: Űrlapmező-gyűjtemény eltávolítása
linktitle: Űrlapmező-gyűjtemény eltávolítása
second_title: GroupDocs.Editor .NET API
description: Ebből a lépésről lépésre szóló útmutatóból megtudhatja, hogyan távolíthat el űrlapmezőket Word-dokumentumokból a GroupDocs.Editor for .NET segítségével. Ideális fejlesztőknek.
weight: 13
url: /hu/net/form-field-management/remove-form-field-collection/
---

# Űrlapmező-gyűjtemény eltávolítása

## Bevezetés
Szeretné programozottan kezelni az űrlapmezőket a dokumentumokban? A GroupDocs.Editor for .NET hatékony megoldást kínál az űrlapmezők kezelésére és manipulálására különféle dokumentumformátumokban. Ebben az oktatóanyagban végigvezetjük az űrlapmező-gyűjtemények Word-dokumentumból történő eltávolításának lépésein ennek a robusztus könyvtárnak a használatával. 
## Előfeltételek
Mielőtt belemerülnénk a kódba, győződjön meg arról, hogy mindent beállított a zökkenőmentes élmény érdekében:
1. GroupDocs.Editor for .NET: Győződjön meg arról, hogy letöltötte és telepítette a GroupDocs.Editor for .NET programot. Ha nem, akkor letöltheti[itt](https://releases.groupdocs.com/editor/net/).
2. Fejlesztési környezet: Szüksége lesz egy fejlesztői környezetre, például a Visual Studiora.
3. .NET-keretrendszer: Győződjön meg arról, hogy a .NET-keretrendszer telepítve van a számítógépen.
4.  Mintadokumentum: legyen egy Word-dokumentum mintája (pl.`SampleLegacyFormFields.docx`) a módosítani kívánt űrlapmezőkkel.

## Névterek importálása
A kezdéshez importálnia kell a szükséges névtereket a .NET-projektbe. Ez lehetővé teszi a GroupDocs.Editor funkcióinak elérését.
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System.IO;
```
## 1. lépés: Töltse be a dokumentumot
Először is be kell töltenie a szerkeszteni kívánt dokumentumot. Bontsuk szét:
### 1.1. lépés: Szerezze meg a bemeneti fájl elérési útját
 Meg kell adnia a bemeneti fájl elérési útját. Ebben a példában egy mintafájlt fogunk használni, melynek neve`SampleLegacyFormFields.docx`.
```csharp
string inputFilePath = "path/to/SampleLegacyFormFields.docx";
```
### 1.2. lépés: Hozzon létre egy FileStream-et az elérési útból
 Ezután hozzon létre a`FileStream` elolvasni a dokumentumot.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
    // Folytassa a következő lépésekkel ezen belül a blokk használatával.
}
```
## 2. lépés: Állítsa be a betöltési beállításokat
dokumentum betöltésekor előfordulhat, hogy meg kell adnia a betöltési beállításokat, különösen, ha a dokumentum jelszóval védett.
### 2.1. lépés: Hozzon létre betöltési beállításokat
 Hozzon létre egy példányt a`WordProcessingLoadOptions`.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
```
### 2.2 lépés: Adja meg a jelszót (ha szükséges)
Ha dokumentuma jelszóval védett, megadhatja a jelszót.
```csharp
loadOptions.Password = "some_password_to_open_a_document";
```
## 3. lépés: Töltse be a dokumentumot a Szerkesztőbe
 Most töltse be a dokumentumot a`Editor` például a`FileStream` és`LoadOptions`.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    // Folytassa a következő lépésekkel ezen belül a blokk használatával.
}
```
## 4. lépés: Az űrlapmezők elérése és kezelése
Miután a dokumentum betöltődött, elérheti és kezelheti az űrlapmezőket.
### 4.1. lépés: Olvassa el a FormFieldManagert
 Szerezze vissza a`FormFieldManager` tól`Editor` példa.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
### 4.2. lépés: A FormFieldCollection elérése
 Szerezd meg a`FormFieldCollection` amely a dokumentum összes űrlapmezőjét tartalmazza.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
### 4.3. lépés: Távolítson el egy adott szöveges űrlapmezőt
Egy adott szöveges űrlapmező eltávolításához keresse meg a neve alapján, majd távolítsa el.
```csharp
TextFormField textField = collection.GetFormField<TextFormField>("Text1");
fieldManager.RemoveFormFiled(textField);
```
### 4.4. lépés: Több űrlapmező eltávolítása
Egyszerre több űrlapmezőt is eltávolíthat a nevük megadásával.
```csharp
textField = collection.GetFormField<TextFormField>("Text7");
CheckBoxForm checkBoxForm = collection.GetFormField<CheckBoxForm>("Check2");
fieldManager.RemoveFormFields(new IFormField[] { textField, checkBoxForm });
```
## 5. lépés: Mentse el a módosított dokumentumot
Az űrlapmezők módosítása után el kell mentenie a dokumentumot.
### 5.1. lépés: Mentési beállítások létrehozása
Adja meg a kimeneti dokumentum formátumát és mentési beállításait.
```csharp
WordProcessingFormats docFormat = WordProcessingFormats.Docx;
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(docFormat);
```
### 5.2. lépés: A memóriahasználat optimalizálása
Ha nagy dokumentumokkal foglalkozik, érdemes lehet optimalizálni a memóriahasználatot.
```csharp
saveOptions.OptimizeMemoryUsage = true;
```
### 5.3. lépés: Védelem beállítása (ha szükséges)
Írási jelszó beállításával megvédheti a dokumentumot a további szerkesztéstől.
```csharp
saveOptions.Protection = new WordProcessingProtection(WordProcessingProtectionType.AllowOnlyFormFields, "write_password");
```
### 5.4. lépés: Mentse el a dokumentumot
 Végül mentse el a dokumentumot az a`MemoryStream`.
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(outputStream, saveOptions);
}
```

## Következtetés
Gratulálunk! Sikeresen eltávolította az űrlapmezőket egy Word-dokumentumból a GroupDocs.Editor for .NET segítségével. Ez a nagy teljesítményű könyvtár megkönnyíti a dokumentumok tartalmának programozott kezelését, így időt és erőfeszítést takarít meg.
## GYIK
### Használhatom a GroupDocs.Editor for .NET programot más dokumentumformátumokkal?
Igen, a GroupDocs.Editor for .NET különféle dokumentumformátumokat támogat, beleértve a PDF-t, HTML-t és egyebeket.
### Lehetséges űrlapmezőket hozzáadni a GroupDocs.Editor for .NET segítségével?
Igen, programozottan hozzáadhat, módosíthat és eltávolíthat űrlapmezőket.
### Mi van, ha a dokumentumom nagyon nagy?
A nagy dokumentumok hatékony kezelése érdekében a mentési beállításoknál engedélyezheti a memóriaoptimalizálást.
### Használhatom a GroupDocs.Editor for .NET programot webalkalmazásban?
Teljesen! A GroupDocs.Editor for .NET webes alkalmazásokba integrálható szerveroldali dokumentumfeldolgozáshoz.
### Hol kaphatok támogatást, ha problémákba ütközöm?
 Meglátogathatja a[támogatói fórum](https://forum.groupdocs.com/c/editor/20) segítségért bármilyen kérdésben.