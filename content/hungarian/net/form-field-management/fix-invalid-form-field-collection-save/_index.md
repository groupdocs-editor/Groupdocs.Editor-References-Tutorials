---
title: Javítsa ki az érvénytelen űrlapmező-gyűjteményt, és mentse
linktitle: Javítsa ki az érvénytelen űrlapmező-gyűjteményt, és mentse
second_title: GroupDocs.Editor .NET API
description: Ismerje meg, hogyan javíthatja ki az érvénytelen űrlapmezőket a DOCX-ben a Groupdocs.Editor for .NET segítségével. Kövesse ezt az útmutatót, hogy dokumentumai hibamentesek legyenek, és biztonságosan mentse azokat.
weight: 11
url: /hu/net/form-field-management/fix-invalid-form-field-collection-save/
---
## Bevezetés
Üdvözöljük! Ha űrlapmezőkkel dolgozik dokumentumokban, és problémákba ütközik az érvénytelen űrlapmező-gyűjteményekkel kapcsolatban, akkor jó helyen jár. Ebben az oktatóanyagban belemerülünk az érvénytelen űrlapmezők javításába és a dokumentum mentésébe a Groupdocs.Editor for .NET segítségével. Lépésről lépésre végigvezetjük a folyamaton, biztosítva, hogy minden részlet birtokában legyen a zökkenőmentes működéshez. Kezdjük el!
## Előfeltételek
Mielőtt belevágnánk a kódba, néhány dolgot meg kell határoznia:
-  Groupdocs.Editor for .NET: Győződjön meg arról, hogy telepítette a Groupdocs.Editor könyvtárat a .NET-hez. Letöltheti[itt](https://releases.groupdocs.com/editor/net/).
- Fejlesztői környezet: Be kell állítania egy .NET fejlesztői környezetet, például a Visual Studio-t.
- Alapvető C# ismeretek: Ez az oktatóanyag feltételezi, hogy rendelkezik alapvető ismeretekkel a C# programozásról.
## Névterek importálása
Először is importálnia kell a szükséges névtereket a C# projektbe. Adja hozzá a következő sorokat a kódfájl elejéhez:
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System;
using System.IO;
```
## 1. lépés: Szerezze meg a bemeneti fájl elérési útját
Az első lépés a bemeneti fájl elérési útjának megadása. Ennek a fájlnak egy űrlapmezőket tartalmazó DOCX-dokumentumnak kell lennie.
```csharp
string inputFilePath = Constants.SampleLegacyFormFields_docx;
```
## 2. lépés: Hozzon létre egy adatfolyamot a fájl elérési útjából
Ezután hozzon létre egy fájlfolyamot a bemeneti dokumentum olvasásához. Ez lehetővé teszi a dokumentum betöltését a szerkesztőbe.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
```
## 3. lépés: Hozzon létre betöltési beállításokat a dokumentumhoz
Ebben a lépésben létre kell hoznia a dokumentum betöltési beállításait. Ha dokumentuma jelszóval védett, megadhatja a jelszót. Ebben a példában a dokumentum nem védett, így a jelszó figyelmen kívül marad.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
loadOptions.Password = "some_password_to_open_a_document";
```
## 4. lépés: Töltse be a dokumentumot a szerkesztőpéldányba
Most töltse be a dokumentumot a megadott beállításokkal a Szerkesztő példányba. Itt zajlanak majd a főbb műveletek a dokumentumon.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
```
## 4.1. lépés: Olvassa el a FormFieldManager példányt
 A`FormFieldManager` példány felelős a dokumentum űrlapmezőinek kezeléséért. Az űrlapmezők eléréséhez és kezeléséhez el kell olvasnia ezt a példányt.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
## 4.2. lépés: Olvassa el a FormFieldCollection-t
 A`FormFieldCollection` tartalmazza a dokumentum összes űrlapmezőjét. Ezt a gyűjteményt az érvénytelen űrlapmezők ellenőrzéséhez és kijavításához olvassa el.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
## 4.3. lépés: Érvénytelen űrlapmezők automatikus javítása
Próbálja meg automatikusan kijavítani a dokumentum érvénytelen űrlapmezőit. Ez egy előzetes lépés a nyilvánvaló problémák megoldására.
```csharp
fieldManager.FixInvalidFormFieldNames(new InvalidFormField[0]);
collection = fieldManager.FormFieldCollection;
```
## 4.4. lépés: Ellenőrizze az érvénytelen űrlapmezőket
Ellenőrizze, hogy maradt-e érvénytelen űrlapmező az automatikus javítási kísérlet után.
```csharp
bool hasInvalidFormFields = fieldManager.HasInvalidFormFields();
Console.WriteLine("FormFieldCollection contains invalid items: {0}", hasInvalidFormFields);
```
## 4.4.1. lépés: Az összes érvénytelen űrlapmezőnév lekérése
Kérje le az összes érvénytelen űrlapmező nevét. Ezeket a neveket használjuk a mezők javítására.
```csharp
var invalidFormFields = fieldManager.GetInvalidFormFieldNames();
```
## 4.4.2. lépés: Hozzon létre egyedi neveket az érvénytelen mezőknek
Minden érvénytelen űrlapmezőhöz hozzon létre egyedi nevet. Ez biztosítja, hogy ne legyenek ütközések a meglévő űrlapmezőnevekkel.
```csharp
foreach (var invalidItem in invalidFormFields)
{
    invalidItem.FixedName = string.Format("{0}_{1}", invalidItem.Name, Guid.NewGuid());
}
```
## 4.4.3. lépés: Javítsa ki az érvénytelen űrlapmezőket
Javítsa ki az érvénytelen űrlapmezőket az előző lépésben létrehozott egyedi nevek használatával.
```csharp
fieldManager.FixInvalidFormFieldNames(invalidFormFields);
collection = fieldManager.FormFieldCollection;
```
## 5. lépés: Hozzon létre dokumentummentési beállításokat
Állítsa be a dokumentum mentési beállításait. Ez magában foglalja a formátum és az esetleges további mentési beállítások megadását.
```csharp
WordProcessingFormats docFormat = WordProcessingFormats.Docx;
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(docFormat);
```
## 5.1. lépés: A memóriahasználat optimalizálása
 Ha a dokumentum nagy, és okozhat egy`OutOfMemoryException`engedélyezze a memóriaoptimalizálási lehetőséget.
```csharp
saveOptions.OptimizeMemoryUsage = true;
```
## 5.2. lépés: Védje meg a dokumentumot az írástól
Ha meg szeretné védeni a dokumentumot a módosítástól, az űrlapmezők kivételével, állítson be védelmi jelszót.
```csharp
saveOptions.Protection = new WordProcessingProtection(WordProcessingProtectionType.AllowOnlyFormFields, "write_password");
```
## 6. lépés: Mentse el a dokumentumot
Végül mentse el a dokumentumot a megadott mentési beállításokkal. Készítsen memóriafolyamot a kimeneti dokumentum mentéséhez.
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(outputStream, saveOptions);
}
Console.WriteLine("FixInvalidFormFieldCollectionAndSave routine has successfully finished");
```
## Következtetés
 És megvan! Sikeresen kijavította az érvénytelen űrlapmezőket, és elmentette a dokumentumot a Groupdocs.Editor for .NET segítségével. Ennek a lépésenkénti útmutatónak egyértelművé és kezelhetővé kellett volna tennie a folyamatot. Ha bármilyen problémába ütközik, vagy kérdése van, nézze meg a[dokumentáció](https://tutorials.groupdocs.com/editor/net/) vagy nyúlj hozzá[támogatás](https://forum.groupdocs.com/c/editor/20).
## GYIK
### Mi a teendő, ha a dokumentumom jelszóval védett?
 A jelszót a`WordProcessingLoadOptions` a dokumentum megnyitásához.
### Honnan tudhatom, hogy vannak-e érvénytelen űrlapmezők?
 Használja a`HasInvalidFormFields` módszerrel ellenőrizheti, hogy a dokumentumban vannak-e érvénytelen űrlapmezők.
### Javíthatom az űrlapmezőket a nevük megváltoztatása nélkül?
Az ütközések elkerülése érdekében ajánlatos egyedi neveket létrehozni az érvénytelen űrlapmezőknek.
### Milyen formátumokba menthetem a dokumentumot?
 A megfelelő beállítással a dokumentumot különféle formátumokban mentheti, például DOCX, PDF és egyéb formátumokban`WordProcessingFormats`.
### Hogyan optimalizálhatom a memóriahasználatot nagy dokumentumok mentése közben?
 Engedélyezze a`OptimizeMemoryUsage` opció a`WordProcessingSaveOptions` nagyméretű dokumentumok hatékony kezeléséhez.