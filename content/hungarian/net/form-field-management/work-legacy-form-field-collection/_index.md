---
title: Dolgozzon a Legacy Form Field Collection segítségével
linktitle: Dolgozzon a Legacy Form Field Collection segítségével
second_title: GroupDocs.Editor .NET API
description: Részletes útmutatónkból megtudhatja, hogyan kezelheti a régi űrlapmezőket a GroupDocs.Editor for .NET használatával. Tökéletes a szövegmezők, jelölőnégyzetek, dátumok és egyebek kezelésére.
weight: 12
url: /hu/net/form-field-management/work-legacy-form-field-collection/
---
## Bevezetés
Üdvözöljük ebben az átfogó útmutatóban, amely arról szól, hogyan dolgozhat a régi űrlapmező-gyűjteményekkel a GroupDocs.Editor for .NET használatával. Legyen szó szövegmezőről, jelölőnégyzetről, dátummezőről vagy legördülő menüről, ez az oktatóanyag végigvezeti Önt a mezők hatékony kezelésének lépésein. Az útmutató végére alapos ismerete lesz arról, hogyan használhatja a GroupDocs.Editort a dokumentumok különböző űrlapmezőinek kezelésére. Merüljünk el!
## Előfeltételek
Mielőtt elkezdené, győződjön meg arról, hogy rendelkezik a következő előfeltételekkel:
- Visual Studio: Bármelyik legújabb verzió működik.
- .NET-keretrendszer: Győződjön meg arról, hogy telepítve van a .NET-keretrendszer.
-  GroupDocs.Editor for .NET: Töltse le a legújabb verziót[itt](https://releases.groupdocs.com/editor/net/).
- Mintadokumentum: Egy minta DOCX-fájl űrlapmezőkkel tesztelési célból.
## Névterek importálása
Először is importálja a szükséges névtereket a projektbe. Ezek a névterek elengedhetetlenek az űrlapmezők kezeléséhez szükséges osztályok és metódusok eléréséhez.
```csharp
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System.IO;
```
## 1. lépés: Szerezze meg a bemeneti fájl elérési útját
Először is meg kell adnia a bemeneti fájl elérési útját. Ebben a példában egy minta DOCX-fájlt használunk, amely különböző űrlapmezőket tartalmaz.
```csharp
string inputFilePath = "path/to/your/sample_legacy_formfields.docx";
```
## 2. lépés: Hozzon létre egy adatfolyamot a fájl elérési útjából
Ezután hozzon létre egy fájlfolyamot a dokumentum tartalmának olvasásához. Ezt az adatfolyamot fogja használni a dokumentum betöltésére a GroupDocs.Editorba.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
    // A további kód ide kerül
}
```
## 3. lépés: Hozzon létre betöltési beállításokat a dokumentumhoz
A dokumentum betöltése előtt hozzon létre betöltési beállításokat. Ezek a beállítások segítenek a különböző forgatókönyvek kezelésében, például a jelszóval védett dokumentumok kezelésében.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
// Ha a dokumentum jelszóval védett, adja meg a jelszót
loadOptions.Password = "your_password_here"; // Ha szükséges, használjon valódi jelszót
```
## 4. lépés: Töltse be a dokumentumot a szerkesztőpéldány segítségével
Most töltse be a dokumentumot a Szerkesztő példányba a korábban létrehozott fájlfolyam és betöltési beállítások használatával.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    // A további kód ide kerül
}
```
## 5. lépés: Olvassa el a FormFieldManager példányt
Az űrlapmezők kezeléséhez nyissa meg a FormFieldManager példányt a Szerkesztőből. Ez a példány lehetővé teszi a dokumentumban lévő űrlapmezőkkel való interakciót.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
## 6. lépés: Olvassa el a FormFieldCollection-t
Töltse le a FormFieldCollection fájlt a FormFieldManager alkalmazásból. Ez a gyűjtemény tartalmazza a dokumentumban található összes űrlapmezőt.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
## 7. lépés: Ismételje meg az egyes űrlapmezőket
Lapozzon végig a gyűjtemény minden űrlapmezőjén, és azonosítsa a típusukat. A típustól függően kivonhatja és módosíthatja a mező értékét.
```csharp
foreach (var formField in collection)
{
    switch (formField.Type)
    {
        case FormFieldType.Text:
            TextFormField textFormField = collection.GetFormField<TextFormField>(formField.Name);
            Console.WriteLine($"TextFormField detected, name: {formField.Name}, value: {textFormField.Value}");
            break;
        case FormFieldType.CheckBox:
            CheckBoxForm checkBoxFormField = collection.GetFormField<CheckBoxForm>(formField.Name);
            Console.WriteLine($"CheckBoxForm detected, name: {formField.Name}, value: {checkBoxFormField.Value}");
            break;
        case FormFieldType.Date:
            DateFormField dateFormField = collection.GetFormField<DateFormField>(formField.Name);
            Console.WriteLine($"DateFormField detected, name: {formField.Name}, value: {dateFormField.Value}");
            break;
        case FormFieldType.Number:
            NumberFormField numberFormField = collection.GetFormField<NumberFormField>(formField.Name);
            Console.WriteLine($"NumberFormField detected, name: {formField.Name}, value: {numberFormField.Value}");
            break;
        case FormFieldType.DropDown:
            DropDownFormField dropDownFormField = collection.GetFormField<DropDownFormField>(formField.Name);
            Console.WriteLine($"DropDownFormField detected, name: {formField.Name}, value selected: {dropDownFormField.Value[dropDownFormField.SelectedIndex]}");
            break;
    }
}
```
## 8. lépés: Következtetés
Ha követi ezeket a lépéseket, hatékonyan kezelheti és kommunikálhat a dokumentumok régi űrlapmezőivel a GroupDocs.Editor for .NET segítségével. Legyen szó szövegmezőkről, jelölőnégyzetekről, dátumokról, számokról vagy legördülő menükről, ez az útmutató világos és tömör módszert kínál az egyes típusok kezelésére.
## Következtetés
 A dokumentumokban a régi űrlapmezőkkel való munka egyszerű lehet, ha megfelelő eszközöket használ. A GroupDocs.Editor for .NET robusztus megoldást kínál ezeknek a mezőknek a hatékony kezelésére. Ennek a lépésről-lépésre szóló útmutatónak a követésével most már könnyedén kezelheti a dokumentumok különböző űrlapmezőit. Ne felejtse el felfedezni a[dokumentáció](https://tutorials.groupdocs.com/editor/net/) fejlettebb funkciókért és opciókért.
## GYIK
### 1. Használhatom a GroupDocs.Editor for .NET programot jelszóval védett dokumentumokkal?
Igen, megadhatja a jelszót a betöltési beállításokban a jelszóval védett dokumentumok kezeléséhez.
### 2. Hogyan szerezhetem be a GroupDocs.Editor ingyenes próbaverzióját .NET-hez?
 Ingyenes próbaverziót letölthet a webhelyről[itt](https://releases.groupdocs.com/).
### 3. Rendelkezésre áll a GroupDocs.Editor for .NET támogatása?
 Igen, hozzáférhet a támogatáshoz[itt](https://forum.groupdocs.com/c/editor/20).
### 4. Vásárolhatok licencet a GroupDocs.Editor for .NET számára?
 Igen, vásárolhat licencet[itt](https://purchase.groupdocs.com/buy).
### 5. Hol találom a GroupDocs.Editor for .NET dokumentációját?
 dokumentáció elérhető[itt](https://tutorials.groupdocs.com/editor/net/).