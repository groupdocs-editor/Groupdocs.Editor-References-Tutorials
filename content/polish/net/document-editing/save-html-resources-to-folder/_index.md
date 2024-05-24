---
title: Zapisz zasoby HTML w folderze
linktitle: Zapisz zasoby HTML w folderze
second_title: Edytor GroupDocs.NET API
description: Dowiedz się, jak wyodrębnić zasoby HTML z dokumentów za pomocą Groupdocs.Editor dla .NET. Ten kompleksowy samouczek zawiera szczegółowe wskazówki dla programistów.
type: docs
weight: 13
url: /pl/net/document-editing/save-html-resources-to-folder/
---
## Wstęp
Groupdocs.Editor dla .NET to potężne narzędzie, które umożliwia programistom płynne manipulowanie i konwertowanie dokumentów w aplikacjach .NET. Niezależnie od tego, czy chcesz wyodrębnić zasoby HTML z dokumentu, czy wykonać zaawansowane zadania edycyjne, Groupdocs.Editor upraszcza ten proces dzięki intuicyjnemu interfejsowi API i obszernej dokumentacji.
## Warunki wstępne
Przed przystąpieniem do samouczka upewnij się, że spełniasz następujące wymagania wstępne:
1. Podstawowa znajomość C# i .NET: Znajomość języka programowania C# i frameworku .NET jest niezbędna do śledzenia przykładów.
2.  Biblioteka Groupdocs.Editor dla .NET: Pobierz i zainstaluj bibliotekę Groupdocs.Editor dla .NET z[strona internetowa](https://releases.groupdocs.com/editor/net/).
3. Środowisko programistyczne: Skonfiguruj preferowane środowisko programistyczne, takie jak Visual Studio lub dowolne inne kompatybilne IDE.

## Importuj przestrzenie nazw
Aby rozpocząć, zaimportuj niezbędne przestrzenie nazw do swojego projektu C#:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```
##Teraz podzielmy proces zapisywania zasobów HTML w folderze przy użyciu Groupdocs.Editor dla .NET na kilka kroków:
## Krok 1: Zainicjuj Groupdocs.Editor
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
 Najpierw zainicjuj`Editor`obiekt, podając ścieżkę do przykładowego dokumentu. W tym przykładzie używamy dokumentu programu Word, więc określamy`WordProcessingLoadOptions` jako typ dokumentu.
## Krok 2: Edytuj dokument
```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
 Następnie utwórz plik`EditableDocument` obiekt, wywołując metodę`Edit` metoda`Editor` obiekt. Umożliwia to wykonywanie operacji edycyjnych na dokumencie.
## Krok 3: Wyodrębnij zasoby
```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
Wyodrębnij z dokumentu zasoby, takie jak obrazy, czcionki i arkusze stylów, i przechowuj je na odpowiednich listach.
## Krok 4: Określ folder wyjściowy
```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
Zdefiniuj folder wyjściowy, w którym zostaną zapisane wyodrębnione zasoby. Możesz dostosować ścieżkę folderu zgodnie ze swoimi wymaganiami.
## Krok 5: Oszczędzaj zasoby
```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
Przeglądaj w pętli każdy zasób obrazu, zapisz go w folderze wyjściowym i wyświetl odpowiednie informacje, takie jak nazwa pliku, typ i wymiary.
```csharp
		foreach (FontResourceBase oneFont in fonts)
		{
			Console.WriteLine("Saving {0} of {1} type",
				oneFont.FilenameWithExtension, oneFont.Type.FormalName);
			oneFont.Save(Path.Combine(outputFolder, oneFont.FilenameWithExtension));
		}
```
Podobnie zapisz każdy zasób czcionki w folderze wyjściowym.
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
Na koniec zapisz każdy arkusz stylów w folderze wyjściowym i zakończ proces edycji.

## Wniosek
Podsumowując, Groupdocs.Editor dla .NET zapewnia wygodne rozwiązanie do programowego zarządzania dokumentami i manipulowania nimi w aplikacjach .NET. Postępując zgodnie z tym samouczkiem, możesz łatwo wyodrębnić zasoby HTML z dokumentów i dostosować proces do swoich konkretnych wymagań.
## Często zadawane pytania
### Czy Groupdocs.Editor jest kompatybilny z innymi formatami dokumentów oprócz Worda?
Tak, Groupdocs.Editor obsługuje szeroką gamę formatów dokumentów, w tym Excel, PowerPoint, PDF i inne.
### Czy mogę zintegrować Groupdocs.Editor z moją aplikacją internetową?
Absolutnie Groupdocs.Editor oferuje bezproblemową integrację z aplikacjami internetowymi opracowanymi na platformie .NET.
### Czy Groupdocs.Editor zapewnia obsługę usług przechowywania w chmurze?
Tak, Groupdocs.Editor obsługuje integrację z popularnymi usługami przechowywania w chmurze, takimi jak Google Drive, Dropbox i Microsoft OneDrive.
### Czy dostępna jest bezpłatna wersja próbna programu Groupdocs.Editor?
Tak, możesz skorzystać z bezpłatnej wersji próbnej Groupdocs.Editor na stronie internetowej.
### Jak mogę uzyskać pomoc techniczną dla Groupdocs.Editor?
Aby uzyskać pomoc techniczną i wsparcie społeczności, możesz odwiedzić forum Groupdocs.Editor.