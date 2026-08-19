---
date: 2026-05-12
description: Ismerje meg, hogyan vonhat ki betűtípusokat és egyéb HTML erőforrásokat
  a dokumentumokból a GroupDocs.Editor for .NET használatával. Lépésről‑lépésre útmutató
  .NET fejlesztőknek.
keywords:
- how to extract fonts
- GroupDocs.Editor .NET
- extract HTML resources
linktitle: HTML erőforrások mentése mappába
schemas:
- author: GroupDocs
  dateModified: '2026-05-12'
  description: Learn how to extract fonts and other HTML resources from documents
    using GroupDocs.Editor for .NET. Step‑by‑step guide for .NET developers.
  headline: How to Extract Fonts and Save HTML Resources to Folder
  type: TechArticle
- description: Learn how to extract fonts and other HTML resources from documents
    using GroupDocs.Editor for .NET. Step‑by‑step guide for .NET developers.
  name: How to Extract Fonts and Save HTML Resources to Folder
  steps:
  - name: '**Basic Knowledge of C# and .NET** – Familiarity with C# programming language
      and .NET framework is essential to follow along with the examples.'
    text: '**Basic Knowledge of C# and .NET** – Familiarity with C# programming language
      and .NET framework is essential to follow along with the examples.'
  - name: '**GroupDocs.Editor for .NET Library** – Download and install GroupDocs.Editor
      for .NET library from the [website](https://releases.groupdocs.com/editor/net/).'
    text: '**GroupDocs.Editor for .NET Library** – Download and install GroupDocs.Editor
      for .NET library from the [website](https://releases.groupdocs.com/editor/net/).'
  - name: '**Development Environment** – Set up your preferred development environment
      such as Visual Studio or any other compatible IDE.'
    text: '**Development Environment** – Set up your preferred development environment
      such as Visual Studio or any other compatible IDE.'
  type: HowTo
- questions:
  - answer: Yes, it supports Excel, PowerPoint, PDF, HTML, and over 50 additional
      formats for both editing and resource extraction.
    question: Is GroupDocs.Editor compatible with other document formats besides Word?
  - answer: Absolutely. The API works seamlessly with ASP.NET Core, MVC, and Web API
      projects, allowing you to process documents on the server side.
    question: Can I integrate GroupDocs.Editor into a web application?
  - answer: Yes, it includes built‑in connectors for Google Drive, Dropbox, OneDrive,
      and Amazon S3, enabling direct loading and saving of documents in the cloud.
    question: Does GroupDocs.Editor provide cloud storage integration?
  - answer: A fully functional 30‑day trial can be downloaded from the GroupDocs website
      without any credit‑card requirement.
    question: Is there a free trial available for GroupDocs.Editor?
  - answer: You can reach the GroupDocs support team via the official forum, submit
      a ticket through the customer portal, or consult the detailed API documentation.
    question: How can I get technical support for extraction issues?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Hogyan vonjunk ki betűtípusokat és mentsük el a HTML erőforrásokat mappába
type: docs
url: /hu/net/document-editing/save-html-resources-to-folder/
weight: 13
---

# Hogyan lehet betűtípusokat kinyerni és HTML erőforrásokat mappába menteni

## Bevezetés
A GroupDocs.Editor for .NET lehetővé teszi, hogy **betűtípusok kinyerését** és egyéb eszközöket egy dokumentumból HTML-re konvertálás közben. Néhány C# sorral ki tudja nyerni a képeket, stíluslapokat és betűtípus fájlokat, majd a kívánt mappába menteni őket. Ez az útmutató végigvezeti Önt a teljes munkafolyamaton, a szerkesztő inicializálásától az egyes erőforrások lemezre mentéséig.

## Gyors válaszok
- **Mit jelent a „betűtípusok kinyerése”?** Ez a beágyazott betűtípusfájlok lekérésének folyamata egy forrásdokumentumból HTML konverzió során.  
- **Melyik könyvtár kezeli ezt?** A GroupDocs.Editor for .NET dedikált API-t biztosít a betűtípusok, képek és stíluslapok kinyeréséhez.  
- **Szükségem van licencre?** Elérhető egy ingyenes próba, a kereskedelmi licenc szükséges a termelési használathoz.  
- **Mely .NET verziók támogatottak?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.  
- **Célzott mappa megadható?** Igen, megadhat bármely írható útvonalat a kinyert erőforrások mentésekor.

## Mi az a „betűtípusok kinyerése”?
**Betűtípusok kinyerése** arra utal, hogy a forrásdokumentumba (pl. DOCX, PPTX) beágyazott eredeti betűtípusfájlokat lekérjük, hogy a generált HTML hivatkozhasson rájuk. Ez biztosítja, hogy a szöveg a böngészőkben pontosan úgy jelenjen meg, ahogy szándékolták, anélkül, hogy a rendszer betűtípusaira támaszkodna.

## Miért használja a GroupDocs.Editor-t HTML erőforrás kinyeréshez?
A GroupDocs.Editor **50+ bemeneti és kimeneti formátumot** támogat — beleértve a DOCX, PPTX, PDF és HTML formátumokat — és képes **legfeljebb 300 oldalas** dokumentumokat feldolgozni anélkül, hogy a teljes fájlt a memóriába töltené. API-ja egyetlen lépésben nyeri ki a betűtípusokat, képeket és CSS-t, ezzel a manuális feldolgozáshoz képest akár **70 %**-kal csökkentve a fejlesztési időt.

## Előfeltételek
Mielőtt belemerülne az útmutatóba, győződjön meg róla, hogy rendelkezik a következő előfeltételekkel:
1. **Alapvető C# és .NET ismeretek** – A C# programozási nyelv és a .NET keretrendszer ismerete elengedhetetlen a példák követéséhez.  
2. **GroupDocs.Editor for .NET könyvtár** – Töltse le és telepítse a GroupDocs.Editor for .NET könyvtárat a [weboldalról](https://releases.groupdocs.com/editor/net/).  
3. **Fejlesztői környezet** – Állítsa be a kedvenc fejlesztői környezetét, például a Visual Studio-t vagy bármely más kompatibilis IDE-t.

## Névterek importálása
A kezdéshez importálja a szükséges névtereket a C# projektjébe:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```

## Hogyan nyerjen ki betűtípusokat és mentse az HTML erőforrásokat egy mappába?
Töltse be a forrásdokumentumot a `Editor editor = new Editor("sample.docx", new WordProcessingLoadOptions());` kóddal, majd hívja meg a `editor.Save("output.html", SaveOptions.Html);` metódust. A mentés művelet után a `Resources` gyűjtemény tartalmazza az összes kinyert eszközt — beleértve a betűtípusokat is — amelyeket végigjárhat és lemezre írhat. Ez az egylépéses megközelítés automatikusan kezeli a konverziót és az erőforrások kinyerését.

## 1. lépés: A GroupDocs.Editor inicializálása
`Editor` az a központi osztály, amely a dokumentum betöltését, konvertálását és az erőforrások kinyerését irányítja. Egyetlen dokumentum munkamenetet képvisel a memóriában.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
Először inicializálja az `Editor` objektumot a mintadokumentum elérési útjának megadásával. Ebben a példában egy Word dokumentumot használunk, ezért a `WordProcessingLoadOptions`-t adjuk meg dokumentumtípusként.

## 2. lépés: Dokumentum szerkesztése
`EditableDocument` a szerkeszthető reprezentáció, amelyet az `Edit` metódus ad vissza, lehetővé téve a dokumentum mentés előtti módosítását.

```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
Ezután hozza létre az `EditableDocument` objektumot az `Editor` objektum `Edit` metódusának meghívásával. Ez lehetővé teszi a dokumentum szerkesztési műveleteinek végrehajtását.

## 3. lépés: Erőforrások kinyerése
`Resources` egy gyűjtemény, amely a kinyert eszközöket — képeket, betűtípusokat és stíluslapokat — külön listákba csoportosítja a könnyű kezelés érdekében.

```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
Kinyerheti a dokumentumból a képeket, betűtípusokat és stíluslapokat, és a megfelelő listákban tárolhatja őket.

## 4. lépés: Kimeneti mappa megadása
`outputFolder` egy karakterlánc, amely meghatározza, hová lesznek írva a kinyert fájlok. Bármely írható könyvtárra mutathatja a szerveren vagy a helyi gépen.

```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
Határozza meg a kimeneti mappát, ahová a kinyert erőforrások mentésre kerülnek. A mappa útvonalát igénye szerint testre szabhatja.

## 5. lépés: Erőforrások mentése
`SaveResource` egy segédeljárás, amely egyetlen bináris erőforrást (képet, betűtípust vagy stíluslapot) ír a fájlrendszerbe.

```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
Iteráljon minden képerny erőforráson, mentse azt a kimeneti mappába, és jelenítse meg a releváns információkat, például a fájlnevet, típust és méreteket.

```csharp
		foreach (FontResourceBase oneFont in fonts)
		{
			Console.WriteLine("Saving {0} of {1} type",
				oneFont.FilenameWithExtension, oneFont.Type.FormalName);
			oneFont.Save(Path.Combine(outputFolder, oneFont.FilenameWithExtension));
		}
```
Hasonlóan, mentse minden betűtípus erőforrást a kimeneti mappába.

```csharp
		foreach (CssText oneStylesheet in stylesheets)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} encoding",
				oneStylesheet.FilenameWithExtension, oneStylesheet.Type.FormalName, oneStylesheet.Encoding);
			oneStylesheet.Save(Path.Combine(outputFolder, oneStylesheet.FilenameWithExtension));
		}
	}
}
```
Végül mentse minden stíluslapot a kimeneti mappába, és fejezze be a szerkesztési folyamatot.

## Gyakori problémák és megoldások
- **Hiányzó betűtípusok a konverzió után** – Győződjön meg arról, hogy a forrásdokumentum ténylegesen beágyazza a betűtípusokat; ellenkező esetben a GroupDocs.Editor csak a rendszer betűtípusaira hivatkozhat.  
- **Hozzáférés megtagadva hibák** – Ellenőrizze, hogy az alkalmazás folyamatnak van-e írási jogosultsága a cél kimeneti mappához.  
- **Nagy dokumentumok magas memóriahasználatot okoznak** – Használja a `LoadOptions`-t a `LoadMode = LoadMode.Stream` beállítással, hogy nagy fájlokat streamelje ahelyett, hogy teljesen betöltené őket a memóriába.

## Gyakran ismételt kérdések

**Q: A GroupDocs.Editor kompatibilis más dokumentumformátumokkal is a Word mellett?**  
A: Igen, támogatja az Excelt, PowerPointot, PDF-et, HTML-t, valamint több mint 50 további formátumot a szerkesztéshez és az erőforrások kinyeréséhez.

**Q: Integrálhatom a GroupDocs.Editor-t egy webalkalmazásba?**  
A: Teljes mértékben. Az API zökkenőmentesen működik az ASP.NET Core, MVC és Web API projektekben, lehetővé téve a dokumentumok szerveroldali feldolgozását.

**Q: A GroupDocs.Editor felhő tároló integrációt kínál?**  
A: Igen, beépített csatlakozókat tartalmaz a Google Drive, Dropbox, OneDrive és Amazon S3 szolgáltatásokhoz, így közvetlenül betöltheti és mentheti a dokumentumokat a felhőben.

**Q: Elérhető ingyenes próba a GroupDocs.Editor-hez?**  
A: Egy teljes funkcionalitású 30‑napos próba letölthető a GroupDocs weboldaláról, hitelkártya megadása nélkül.

**Q: Hogyan kaphatok technikai támogatást a kinyerési problémákhoz?**  
A: A GroupDocs támogatási csapatot elérheti a hivatalos fórumon, benyújthat egy jegyet az ügyfélportálon keresztül, vagy tanulmányozhatja a részletes API dokumentációt.

---

**Utoljára frissítve:** 2026-05-12  
**Tesztelve:** GroupDocs.Editor 23.11 for .NET  
**Szerző:** GroupDocs

## Kapcsolódó útmutatók

- [Hatékony dokumentumszerkesztés a GroupDocs.Editor .NET&#58; HTML átalakítása szerkeszthető dokumentumokká](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)
- [Hatékony DOCX erőforrások kinyerése és mentése a GroupDocs.Editor .NET használatával – Teljes útmutató](/editor/net/document-saving/efficient-extract-save-docx-resources-groupdocs-editor-net/)
- [A dokumentumszerkesztés és konvertálás mestersége a GroupDocs.Editor .NET&#58; Teljes útmutató](/editor/net/document-editing/groupdocs-editor-net-mastering-document-editing/)