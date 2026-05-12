---
date: 2026-05-12
description: Dowiedz się, jak wyodrębnić czcionki i inne zasoby HTML z dokumentów
  przy użyciu GroupDocs.Editor for .NET. Przewodnik krok po kroku dla programistów
  .NET.
keywords:
- how to extract fonts
- GroupDocs.Editor .NET
- extract HTML resources
linktitle: Zapisz zasoby HTML do folderu
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
title: Jak wyodrębnić czcionki i zapisać zasoby HTML do folderu
type: docs
url: /pl/net/document-editing/save-html-resources-to-folder/
weight: 13
---

# Jak wyodrębnić czcionki i zapisać zasoby HTML do folderu

## Wprowadzenie
GroupDocs.Editor for .NET pozwala **wyodrębnić czcionki** i inne zasoby z dokumentu podczas konwertowania go do HTML. W kilku linijkach C# możesz wyciągnąć obrazy, arkusze stylów i pliki czcionek, a następnie zapisać je w wybranym folderze. Ten samouczek przeprowadzi Cię przez cały przepływ pracy, od inicjalizacji edytora po zapisanie każdego zasobu na dysku.

## Szybkie odpowiedzi
- **Co oznacza „wyodrębnić czcionki”?** To proces pobierania osadzonych plików czcionek ze źródłowego dokumentu podczas konwersji do HTML.  
- **Która biblioteka obsługuje to?** GroupDocs.Editor for .NET udostępnia dedykowane API do wyodrębniania czcionek, obrazów i arkuszy stylów.  
- **Czy potrzebna jest licencja?** Dostępna jest bezpłatna wersja próbna; licencja komercyjna jest wymagana do użytku produkcyjnego.  
- **Jakie wersje .NET są wspierane?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.  
- **Czy mogę wskazać własny folder?** Tak, możesz podać dowolną ścieżkę zapisu przy zapisywaniu wyodrębnionych zasobów.

## Co to jest „wyodrębnić czcionki”?
**Wyodrębnianie czcionek** odnosi się do pobierania oryginalnych plików czcionek osadzonych w źródłowym dokumencie (np. DOCX, PPTX), aby mogły być odwoływane przez wygenerowany HTML. Zapewnia to, że tekst jest renderowany dokładnie tak, jak zamierzono w przeglądarkach, bez polegania na czcionkach systemowych.

## Dlaczego używać GroupDocs.Editor do wyodrębniania zasobów HTML?
GroupDocs.Editor obsługuje **ponad 50 formatów wejściowych i wyjściowych** — w tym DOCX, PPTX, PDF i HTML — i może przetwarzać dokumenty **do 300 stron** bez ładowania całego pliku do pamięci. Jego API wyodrębnia czcionki, obrazy i CSS w jednym przebiegu, skracając czas programowania nawet o **70 %** w porównaniu z ręcznym parsowaniem.

## Prerequisites
Zanim zanurzysz się w samouczek, upewnij się, że masz następujące wymagania wstępne:
1. **Podstawowa znajomość C# i .NET** – Znajomość języka programowania C# oraz frameworka .NET jest niezbędna, aby nadążać za przykładami.  
2. **Biblioteka GroupDocs.Editor for .NET** – Pobierz i zainstaluj bibliotekę GroupDocs.Editor for .NET z [strony internetowej](https://releases.groupdocs.com/editor/net/).  
3. **Środowisko programistyczne** – Skonfiguruj preferowane środowisko programistyczne, takie jak Visual Studio lub inne kompatybilne IDE.

## Importowanie przestrzeni nazw
Aby rozpocząć, zaimportuj niezbędne przestrzenie nazw w swoim projekcie C#:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```

## Jak wyodrębnić czcionki i zapisać zasoby HTML do folderu?
Załaduj swój dokument źródłowy przy użyciu `Editor editor = new Editor("sample.docx", new WordProcessingLoadOptions());`, a następnie wywołaj `editor.Save("output.html", SaveOptions.Html);`. Po operacji zapisu kolekcja `Resources` zawiera wszystkie wyodrębnione zasoby — w tym czcionki — które możesz iterować i zapisywać na dysku. To jednoczesne podejście obsługuje zarówno konwersję, jak i wyodrębnianie zasobów automatycznie.

## Krok 1: Inicjalizacja GroupDocs.Editor
`Editor` jest klasą podstawową, która koordynuje ładowanie dokumentu, konwersję i wyodrębnianie zasobów. Reprezentuje pojedynczą sesję dokumentu w pamięci.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
Najpierw zainicjalizuj obiekt `Editor`, podając ścieżkę do przykładowego dokumentu. W tym przykładzie używamy dokumentu Word, więc określamy `WordProcessingLoadOptions` jako typ dokumentu.

## Krok 2: Edycja dokumentu
`EditableDocument` jest edytowalną reprezentacją zwracaną przez metodę `Edit`, umożliwiającą manipulację dokumentem przed zapisaniem.

```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
Następnie utwórz obiekt `EditableDocument`, wywołując metodę `Edit` obiektu `Editor`. Pozwala to na wykonywanie operacji edycyjnych na dokumencie.

## Krok 3: Wyodrębnianie zasobów
`Resources` jest kolekcją, która grupuje wyodrębnione zasoby — obrazy, czcionki i arkusze stylów — w oddzielne listy ułatwiające obsługę.

```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
Wyodrębnij zasoby, takie jak obrazy, czcionki i arkusze stylów, z dokumentu i przechowaj je w odpowiednich listach.

## Krok 4: Określenie folderu wyjściowego
`outputFolder` jest ciągiem znaków określającym, gdzie zostaną zapisane wyodrębnione pliki. Możesz wskazać dowolny zapisywalny katalog na serwerze lub komputerze lokalnym.

```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
Zdefiniuj folder wyjściowy, w którym zostaną zapisane wyodrębnione zasoby. Możesz dostosować ścieżkę folderu zgodnie z własnymi wymaganiami.

## Krok 5: Zapis zasobów
`SaveResource` jest pomocniczą procedurą, która zapisuje pojedynczy zasób binarny (obraz, czcionkę lub arkusz stylów) w systemie plików.

```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
Iteruj po każdym zasobie obrazu, zapisz go do folderu wyjściowego i wyświetl odpowiednie informacje, takie jak nazwa pliku, typ i wymiary.

```csharp
		foreach (FontResourceBase oneFont in fonts)
		{
			Console.WriteLine("Saving {0} of {1} type",
				oneFont.FilenameWithExtension, oneFont.Type.FormalName);
			oneFont.Save(Path.Combine(outputFolder, oneFont.FilenameWithExtension));
		}
```
Podobnie, zapisz każdy zasób czcionki do folderu wyjściowego.

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
Na koniec zapisz każdy arkusz stylów do folderu wyjściowego i zakończ proces edycji.

## Częste problemy i rozwiązania
- **Brak czcionek po konwersji** – Upewnij się, że dokument źródłowy rzeczywiście osadza czcionki; w przeciwnym razie GroupDocs.Editor może odwoływać się tylko do czcionek systemowych.  
- **Błędy odmowy dostępu** – Sprawdź, czy proces aplikacji ma uprawnienia do zapisu w docelowym folderze wyjściowym.  
- **Duże dokumenty powodują wysokie zużycie pamięci** – Użyj `LoadOptions` z `LoadMode = LoadMode.Stream`, aby strumieniowo przetwarzać duże pliki zamiast ładować je w całości do pamięci.

## Najczęściej zadawane pytania

**Q:** Czy GroupDocs.Editor jest kompatybilny z innymi formatami dokumentów oprócz Word?  
**A:** Tak, obsługuje Excel, PowerPoint, PDF, HTML oraz ponad 50 dodatkowych formatów zarówno do edycji, jak i wyodrębniania zasobów.

**Q:** Czy mogę zintegrować GroupDocs.Editor z aplikacją webową?  
**A:** Oczywiście. API działa bezproblemowo z projektami ASP.NET Core, MVC i Web API, umożliwiając przetwarzanie dokumentów po stronie serwera.

**Q:** Czy GroupDocs.Editor zapewnia integrację z przechowywaniem w chmurze?  
**A:** Tak, zawiera wbudowane łączniki do Google Drive, Dropbox, OneDrive i Amazon S3, umożliwiając bezpośrednie ładowanie i zapisywanie dokumentów w chmurze.

**Q:** Czy dostępna jest bezpłatna wersja próbna GroupDocs.Editor?  
**A:** W pełni funkcjonalna 30‑dniowa wersja próbna może być pobrana ze strony GroupDocs bez wymogu podania karty kredytowej.

**Q:** Jak mogę uzyskać wsparcie techniczne w kwestii problemów z wyodrębnianiem?  
**A:** Możesz skontaktować się z zespołem wsparcia GroupDocs poprzez oficjalne forum, zgłosić zgłoszenie w portalu klienta lub skonsultować się ze szczegółową dokumentacją API.

---

**Ostatnia aktualizacja:** 2026-05-12  
**Testowano z:** GroupDocs.Editor 23.11 for .NET  
**Autor:** GroupDocs

## Powiązane samouczki

- [Efektywna edycja dokumentów przy użyciu GroupDocs.Editor .NET&#58; Przekształcanie HTML w edytowalne dokumenty](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)
- [Efektywne wyodrębnianie i zapisywanie zasobów DOCX przy użyciu GroupDocs.Editor .NET – kompletny przewodnik](/editor/net/document-saving/efficient-extract-save-docx-resources-groupdocs-editor-net/)
- [Mistrzostwo w edycji i konwersji dokumentów z GroupDocs.Editor .NET&#58; kompletny przewodnik](/editor/net/document-editing/groupdocs-editor-net-mastering-document-editing/)