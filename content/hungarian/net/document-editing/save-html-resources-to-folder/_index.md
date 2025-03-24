---
title: Mentse a HTML-forrásokat mappába
linktitle: Mentse a HTML-forrásokat mappába
second_title: GroupDocs.Editor .NET API
description: Ismerje meg, hogyan bonthat ki HTML-forrásokat dokumentumokból a Groupdocs.Editor for .NET segítségével. Ez az átfogó oktatóanyag lépésről lépésre nyújt útmutatást a fejlesztőknek.
weight: 13
url: /hu/net/document-editing/save-html-resources-to-folder/
---
## Bevezetés
Groupdocs.Editor for .NET egy hatékony eszköz, amellyel a fejlesztők zökkenőmentesen kezelhetik és konvertálhatják a dokumentumokat .NET-alkalmazásaikon belül. Akár HTML-forrásokat kell kivonnia egy dokumentumból, akár speciális szerkesztési feladatokat kell végrehajtania, a Groupdocs.Editor leegyszerűsíti a folyamatot intuitív API-jával és kiterjedt dokumentációjával.
## Előfeltételek
Mielőtt belevágna az oktatóanyagba, győződjön meg arról, hogy rendelkezik a következő előfeltételekkel:
1. Alapvető C# és .NET ismeretek: A C# programozási nyelv és a .NET keretrendszer ismerete elengedhetetlen a példák mellett.
2.  Groupdocs.Editor for .NET Library: Töltse le és telepítse a Groupdocs.Editor for .NET könyvtárat a[weboldal](https://releases.groupdocs.com/editor/net/).
3. Fejlesztési környezet: Állítsa be a kívánt fejlesztői környezetet, például a Visual Studio-t vagy bármely más kompatibilis IDE-t.

## Névterek importálása
A kezdéshez importálja a szükséges névtereket a C# projektbe:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```
##Most bontsuk le a HTML-erőforrások mappába mentésének folyamatát a Groupdocs.Editor for .NET segítségével több lépésre:
## 1. lépés: Inicializálja a Groupdocs.Editor programot
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
 Először inicializálja a`Editor`objektumot úgy, hogy megadja a mintadokumentum elérési útját. Ebben a példában Word-dokumentumot használunk, ezért megadjuk`WordProcessingLoadOptions` mint a dokumentum típusa.
## 2. lépés: Dokumentum szerkesztése
```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
 Ezután hozzon létre egy`EditableDocument` objektumot a`Edit` módszere a`Editor` tárgy. Ezzel szerkesztési műveleteket hajthat végre a dokumentumon.
## 3. lépés: Erőforrások kibontása
```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
Kivonja a dokumentumból az olyan erőforrásokat, mint a képek, betűtípusok és stíluslapok, és tárolja azokat a megfelelő listákban.
## 4. lépés: Adja meg a kimeneti mappát
```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
Határozza meg a kimeneti mappát, ahová a kibontott erőforrások mentésre kerülnek. A mappa elérési útját igény szerint testreszabhatja.
## 5. lépés: Mentse el az erőforrásokat
```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
Lapozzon át minden képforráson, mentse el a kimeneti mappába, és jelenítse meg a releváns információkat, például a fájlnevet, a típust és a méreteket.
```csharp
		foreach (FontResourceBase oneFont in fonts)
		{
			Console.WriteLine("Saving {0} of {1} type",
				oneFont.FilenameWithExtension, oneFont.Type.FormalName);
			oneFont.Save(Path.Combine(outputFolder, oneFont.FilenameWithExtension));
		}
```
Hasonlóképpen mentse el az egyes betűkészlet-erőforrásokat a kimeneti mappába.
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
Végül mentse az egyes stíluslapokat a kimeneti mappába, és fejezze be a szerkesztési folyamatot.

## Következtetés
Összefoglalva, a Groupdocs.Editor for .NET kényelmes megoldást kínál a dokumentumok programozott kezelésére és manipulálására .NET-alkalmazásokon belül. Ennek az oktatóanyagnak a követésével könnyedén kivonhatja a HTML-forrásokat a dokumentumokból, és testreszabhatja a folyamatot sajátos igényei szerint.
## GYIK
### A Groupdocs.Editor kompatibilis a Word mellett más dokumentumformátumokkal?
Igen, a Groupdocs.Editor a dokumentumformátumok széles skáláját támogatja, beleértve az Excelt, a PowerPointot, a PDF-et és egyebeket.
### Integrálhatom a Groupdocs.Editort a webalkalmazásomba?
Természetesen a Groupdocs.Editor zökkenőmentes integrációt kínál a .NET keretrendszeren fejlesztett webalkalmazásokkal.
### A Groupdocs.Editor támogatja a felhőalapú tárolási szolgáltatásokat?
Igen, a Groupdocs.Editor támogatja az integrációt olyan népszerű felhőalapú tárolási szolgáltatásokkal, mint a Google Drive, a Dropbox és a Microsoft OneDrive.
### Van ingyenes próbaverzió a Groupdocs.Editor számára?
Igen, igénybe veheti a Groupdocs.Editor ingyenes próbaverzióját a webhelyről.
### Hogyan kaphatok technikai támogatást a Groupdocs.Editorhoz?
Technikai segítségért és közösségi támogatásért keresse fel a Groupdocs.Editor fórumot.