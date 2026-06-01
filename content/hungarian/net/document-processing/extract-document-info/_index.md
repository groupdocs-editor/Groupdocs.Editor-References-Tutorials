---
date: 2026-06-01
description: Ismerje meg, hogyan lehet oldalszámot lekérni és a dokumentum metaadatait
  kinyerni a GroupDocs.Editor for .NET segítségével egy részletes lépésről‑lépésre
  útmutatóban.
keywords:
- get page count
- extract document metadata
- get document info
- find document extension
- retrieve document size
linktitle: Oldalszám lekérése és dokumentuminformációk kinyerése
schemas:
- author: GroupDocs
  dateModified: '2026-06-01'
  description: Learn how to get page count and extract document metadata using GroupDocs.Editor
    for .NET in a detailed step‑by‑step tutorial.
  headline: Get Page Count & Extract Document Info with GroupDocs.Editor
  type: TechArticle
- questions:
  - answer: GroupDocs.Editor supports Word processing, spreadsheet, presentation,
      PDF, and plain‑text files—over 50 formats in total.
    question: What document types can I extract metadata from?
  - answer: Access `DocumentInfo.Extension` after calling `GetDocumentInfo()`; it
      returns the extension without the leading dot.
    question: How do I retrieve the file extension?
  - answer: Yes—`DocumentInfo.Size` returns the size in bytes; divide by 1,048,576
      to convert to megabytes.
    question: Can I get the size of a document in megabytes?
  - answer: Absolutely—GroupDocs.Editor never writes the password to disk and disposes
      of all cryptographic objects after use.
    question: Is it safe to process password‑protected files on a server?
  - answer: You can get support from the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).
    question: Where can I find additional help if I run into issues?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Oldalszám lekérése és dokumentuminformációk kinyerése a GroupDocs.Editor segítségével
type: docs
url: /hu/net/document-processing/extract-document-info/
weight: 10
---

# Oldalszám lekérése és dokumentuminformációk kinyerése a GroupDocs.Editor segítségével

## Bevezetés
Egy átfogó útmutatóban megtanulja, hogyan **get page count** és hogyan nyerjen ki részletes dokumentuminformációkat – beleértve a formátumot, méretet és titkosítási állapotot – a GroupDocs.Editor for .NET használatával. Akár dokumentumkezelő rendszert, jelentéskészítő motorot vagy automatizált konverziós csővezetéket épít, a fájl metaadatainak megértése az első lépés a megbízható feldolgozáshoz. Lépjünk végig a teljes munkafolyamaton, a fájl betöltésétől a források biztonságos felszabadításáig.

## Gyors válaszok
- **Hogyan tudom lekérni egy dokumentum oldalszámát?**  
  Hívja meg a `editor.GetDocumentInfo().PageCount` metódust a fájl `Editor`-rel történő betöltése után.
- **Mely fájlformátumok támogatottak a metaadatok kinyeréséhez?**  
  Több mint 50 formátum, beleértve a DOCX, XLSX, PPTX, PDF, TXT és HTML formátumokat.
- **Kinyerhetek metaadatokat jelszóval védett fájlokból?**  
  Igen – adja meg a jelszót az `Editor` példány létrehozásakor.
- **Kézzel kell felszabadítanom az erőforrásokat?**  
  Abszolút; mindig hívja meg az `editor.Dispose()` metódust, vagy helyezze az editort egy `using` blokkba.
- **Melyik GroupDocs.Editor verzió szükséges?**  
  A legújabb stabil kiadás (v23.12+ a írás időpontjában) támogatja az összes bemutatott funkciót.

## Mi az a “get page count” a GroupDocs.Editor-ben?
`GetDocumentInfo()` egy metódus, amely egy `DocumentInfo` objektumot ad vissza, amely tartalmazza a dokumentum oldalszámát, formátumát, méretét és egyéb metaadatait. Ez az egyetlen hívás azonnali betekintést nyújt anélkül, hogy manuálisan elemezné a fájlt. Ennek a metódusnak a használatával elkerülheti a teljes dokumentum memóriába töltését, ami javítja a teljesítményt, különösen nagy fájlok esetén, és csökkenti a szerver erőforrás-felhasználását.

## Miért érdemes dokumentum metaadatokat kinyerni a GroupDocs.Editor-rel?
A GroupDocs.Editor képes **50+ bemeneti és kimeneti formátum** feldolgozására, és metaadatokat visszaadni akár **2 GB** méretű fájlok esetén is anélkül, hogy a teljes dokumentumot memóriába töltené. Ez a hatékonyság akár **70 %**-kal csökkenti a szerver terhelését a teljes dokumentum elemzéséhez képest, így ideálissá teszi a nagy áteresztőképességű alkalmazások számára.

## Előfeltételek
- **C# fejlesztési alapok** – kényelmesen kell tudnia dolgozni a Visual Studio-val és a .NET projektstruktúrákkal.
- **Visual Studio 2022** (vagy bármely friss verzió) telepítve a gépén.
- **GroupDocs.Editor for .NET** – töltse le a legújabb csomagot a [download page](https://releases.groupdocs.com/editor/net/) oldalról.

## Hogyan töltsük be a dokumentumot?
`Editor` a fő osztály, amely egy dokumentumot képvisel, és metódusokat biztosít annak betöltésére és manipulálására. Töltse be a célfájlt egy `Editor` példány létrehozásával és a fájl útvonalának átadásával. Az editor automatikusan felismeri a formátumot, így nem kell betöltési beállításokat megadni. Ez a megközelítés bármely támogatott fájltípusra működik, és egyszerűsíti a kezdeti beállítást.

```csharp
using System;
using GroupDocs.Editor.Metadata;
```

## Hogyan nyerjük ki a dokumentum információkat?
`GetDocumentInfo()` egy `DocumentInfo` objektumot ad vissza, amely metaadatokat tartalmaz, mint például az oldalszám, formátum, méret és titkosítási állapot. Betöltés után hívja meg ezt a metódust az objektum lekéréséhez. A visszakapott `DocumentInfo` egy tömör áttekintést nyújt a fájl jellemzőiről, lehetővé téve döntések meghozatalát további feldolgozás nélkül.

```csharp
string docxInputFilePath = "YourSampleDocument.docx";
Editor editorDocx = new Editor(docxInputFilePath);
```

## Hogyan határozzuk meg a dokumentum típusát?
`DocumentType` egy enum, amely azt jelzi, hogy a dokumentum WordProcessing, Spreadsheet vagy Text típusú. Azt tudni, hogy egy fájl Word processing dokumentum, táblázat vagy egyszerű szöveg, befolyásolja, hogyan kezeljük később. Használja a `DocumentInfo` objektum `DocumentType` tulajdonságát a döntés meghozatalához és a logika megfelelő ágaztatásához.

```csharp
IDocumentInfo infoDocx = editorDocx.GetDocumentInfo(null);
```

## Hogyan nyerjünk ki részletes információkat a Word processing fájlokhoz?
`WordProcessing` olyan dokumentumokra vonatkozik, mint a DOCX, ODT és RTF, amelyeket word processing fájlként kezelnek. Ha a dokumentum típusa `WordProcessing`, akkor további tulajdonságokat, például **format**, **extension**, **page count**, **size**, és **encryption flag** közvetlenül a `DocumentInfo` objektumból olvashat. Ezek a részletek segítenek a feldolgozási lépések testreszabásában, például specifikus konverziók vagy biztonsági ellenőrzések alkalmazásában.

```csharp
bool isSpreadsheet = infoDocx is SpreadsheetDocumentInfo;
bool isText = infoDocx is TextualDocumentInfo;
bool isWordProcessing = infoDocx is WordProcessingDocumentInfo;
Console.WriteLine($"Is '{docxInputFilePath}' a Spreadsheet: {isSpreadsheet}");
Console.WriteLine($"Is '{docxInputFilePath}' a Textual document: {isText}");
Console.WriteLine($"Is '{docxInputFilePath}' a WordProcessing document: {isWordProcessing}");
```

## Hogyan kezeljük a táblázat- és szöveges dokumentumokat?
`Spreadsheet` a táblázatfájlokat jelöli, például az XLSX-et, míg a `Text` egyszerű szöveges dokumentumokat képviseli. Táblázatok (`Spreadsheet`) és egyszerű szövegfájlok (`Text`) esetén a `DocumentInfo` objektum továbbra is alap metaadatokat (extension, size, page count) biztosít. Néhány formátum nem adja vissza az oldalszámot, ebben az esetben az érték `0` lesz. Más metaadatokra továbbra is támaszkodhat a további logikához.

```csharp
if (isWordProcessing)
{
    WordProcessingDocumentInfo casted = (WordProcessingDocumentInfo)infoDocx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Page count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```

## Hogyan dolgozzunk jelszóval védett dokumentumokkal?
`Password` egy karakterlánc, amelyet az `Editor` konstruktorának adunk át a titkosított fájlok megnyitásához. Ha egy dokumentum titkosított, először próbálja meg jelszó nélkül megnyitni. Ha ez sikertelen, fogja el a kivételt, majd próbálja újra a helyes jelszóval. Az `Editor` konstruktor elfogad egy `Password` paramétert erre a célra, lehetővé téve a védett fájlok zökkenőmentes kezelését.

```csharp
string xlsxInputFilePath = "YourSampleDocument.xlsx";
Editor editorXlsx = new Editor(xlsxInputFilePath);
IDocumentInfo infoXlsx = editorXlsx.GetDocumentInfo(null);
bool isXlsxSpreadsheet = infoXlsx is SpreadsheetDocumentInfo;
Console.WriteLine($"Is '{xlsxInputFilePath}' a Spreadsheet: {isXlsxSpreadsheet}");
if (isXlsxSpreadsheet)
{
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo)infoXlsx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Tabs count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```

## Hogyan dolgozzunk szöveges dokumentumokkal?
`DocumentInfo` alap metaadatokat biztosít, mint a méret, kiterjesztés és kódolás a szöveges fájlokhoz. A szöveges fájlok (pl. `.txt`, `.md`) egyszerű adatfolyamként vannak kezelve. A `DocumentInfo`-ból továbbra is lekérheti a méretet és a kódolási információkat, ami hasznos a fájl integritásának ellenőrzéséhez vagy a megfelelő feldolgozási csővezeték meghatározásához.

```csharp
string xlsInputFilePath = "YourSampleDocument.xls";
Editor editorXls = new Editor(xlsInputFilePath);
try
{
    IDocumentInfo infoXls = editorXls.GetDocumentInfo(null);
}
catch (PasswordRequiredException)
{
    Console.WriteLine("This document is password-protected.");
}
try
{
    IDocumentInfo infoXls = editorXls.GetDocumentInfo("incorrect_password");
}
catch (IncorrectPasswordException)
{
    Console.WriteLine("The provided password is incorrect.");
}
IDocumentInfo infoXlsValid = editorXls.GetDocumentInfo("correct_password");
bool isXlsSpreadsheet = infoXlsValid is SpreadsheetDocumentInfo;
Console.WriteLine($"Password-protected document is a Spreadsheet: {isXlsSpreadsheet}");
if (isXlsSpreadsheet)
{
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo)infoXlsValid;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Tabs count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```

## Hogyan szabadítsuk fel az erőforrásokat megfelelően?
`Editor` az elsődleges osztály, amely nem kezelt erőforrásokat tartalmaz, és használat után fel kell szabadítani. A memória szivárgások elkerülése érdekében mindig szabadítsa fel az `Editor` példányt, miután befejezte az információk kinyerését. A `using` utasítás a legbiztonságosabb minta, mivel garantálja a felszabadítást még kivétel esetén is, biztosítva a tiszta erőforrás-kezelést.

```csharp
string xmlInputFilePath = "YourSampleDocument.xml";
Editor editorXml = new Editor(xmlInputFilePath);
IDocumentInfo infoXml = editorXml.GetDocumentInfo(null);
bool isXmlText = infoXml is TextualDocumentInfo;
Console.WriteLine($"Is '{xmlInputFilePath}' a Textual document: {isXmlText}");
if (isXmlText)
{
    TextualDocumentInfo casted = (TextualDocumentInfo)infoXml;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Encoding: {casted.Encoding}; Size: {casted.Size} bytes");
}
```

## Gyakori problémák és megoldások
| Issue | Cause | Solution |
|-------|-------|----------|
| **PageCount returns 0** | A formátum nem támogatja a lapozást (pl. egyszerű szöveg) | `DocumentInfo.DocumentType` ellenőrzése, mielőtt a `PageCount`-ra támaszkodna. |
| **Unsupported file format** | A fájl kiterjesztése nem ismert | Ellenőrizze, hogy a fájl a 50+ támogatott formátum egyike-e; frissítse a GroupDocs.Editor-t a legújabb verzióra. |
| **Password exception** | Helytelen jelszó megadva | `PasswordProtectedException` elkapása és a felhasználó kérése a jelszó újra megadására. |
| **Memory spike on large files** | Nagyon nagy PDF-ek betöltése streaming nélkül | `LoadOptions` használata a `LoadOptions.LoadMode = LoadMode.Stream` beállítással (újabb kiadásokban elérhető). |

## Gyakran feltett kérdések

**Q: Milyen dokumentumtípusokból nyerhetek metaadatokat?**  
A: A GroupDocs.Editor támogatja a Word processing, táblázat, prezentáció, PDF és egyszerű szöveg fájlokat – összesen több mint 50 formátum.

**Q: Hogyan nyerjem ki a fájl kiterjesztését?**  
A: `DocumentInfo.Extension` elérése a `GetDocumentInfo()` hívása után; a pont nélküli kiterjesztést adja vissza.

**Q: Kaphatok információt a dokumentum méretéről megabájtban?**  
A: Igen – a `DocumentInfo.Size` a méretet bájtban adja vissza; a megabájtba konvertáláshoz oszd el 1 048 576-tal.

**Q: Biztonságos-e jelszóval védett fájlokat feldolgozni egy szerveren?**  
A: Abszolút – a GroupDocs.Editor soha nem írja a jelszót a lemezre, és a használat után felszabadít minden kriptográfiai objektumot.

**Q: Hol találok további segítséget, ha problémákba ütközöm?**  
A: Támogatást kaphat a [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20) oldalon.

---

**Utolsó frissítés:** 2026-06-01  
**Tesztelt verzió:** GroupDocs.Editor 23.12 for .NET  
**Szerző:** GroupDocs

```csharp
editorDocx.Dispose();
editorXlsx.Dispose();
editorXls.Dispose();
editorXml.Dispose();
Console.WriteLine("ExtractingDocumentInfo routine has successfully finished");
```

## Kapcsolódó oktatóanyagok

- [A metaadatok kinyerésének mestersége .NET-ben a GroupDocs.Editor-rel: Átfogó útmutató](/editor/net/advanced-features/groupdocs-editor-net-metadata-extraction-guide/)
- [Dokumentum betöltési oktatóanyagok a GroupDocs.Editor for .NET használatával](/editor/net/document-loading/)
- [Hatékony dokumentumszerkesztés a GroupDocs.Editor .NET-tel: HTML átalakítása szerkeszthető dokumentumokká](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)