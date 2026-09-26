---
date: 2026-09-26
description: Dowiedz się, jak obsługiwać prefiks CSS i wyodrębniać zawartość CSS przy
  użyciu GroupDocs.Editor dla .NET w tym szczegółowym przewodniku krok po kroku.
keywords:
- handle css prefix
- extract css content
- edit document css
- prepend url to css
lastmod: 2026-09-26
linktitle: Obsługa zawartości CSS z prefiksem
og_description: Odkryj, jak obsługiwać prefiks CSS i wyodrębniać zawartość CSS przy
  użyciu GroupDocs.Editor dla .NET. Postępuj zgodnie z przewodnikiem krok po kroku,
  aby dodawać prefiksy do adresów URL zasobów CSS i pobierać arkusze stylów.
og_image_alt: Developer guide showing css prefix handling with GroupDocs.Editor for
  .NET
og_title: Jak obsługiwać prefiks CSS w GroupDocs.Editor dla .NET
schemas:
- author: GroupDocs
  dateModified: '2026-09-26'
  description: Learn how to handle css prefix and extract css content using GroupDocs.Editor
    for .NET in this detailed step‑by‑step tutorial.
  headline: How to handle css prefix in GroupDocs.Editor for .NET
  type: TechArticle
- questions:
  - answer: Yes, GroupDocs.Editor for .NET supports PDF, Word, Excel, PowerPoint,
      and many other formats.
    question: Can I use GroupDocs.Editor for .NET with other document formats?
  - answer: Absolutely! You can start your free trial on the [GroupDocs free trial
      page](https://releases.groupdocs.com/).
    question: Is there a free trial available for GroupDocs.Editor for .NET?
  - answer: You can obtain a temporary license from the [temporary license page](https://purchase.groupdocs.com/temporary-license/).
    question: How do I get a temporary license for GroupDocs.Editor for .NET?
  - answer: Detailed documentation is available on the [GroupDocs.Editor for .NET
      documentation site](https://tutorials.groupdocs.com/editor/net/).
    question: Where can I find detailed documentation for GroupDocs.Editor for .NET?
  - answer: You can get support through the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).
    question: What support options are available for GroupDocs.Editor for .NET?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
tags:
- css handling
- GroupDocs.Editor
- .NET document processing
- css prefix
- api tutorial
title: Jak obsługiwać prefiks CSS w GroupDocs.Editor dla .NET
type: docs
url: /pl/net/css-handling/handle-css-content-with-prefix/
weight: 11
---

# Jak obsługiwać prefiks CSS w GroupDocs.Editor dla .NET

W tym samouczku dowiesz się **jak obsługiwać prefiks CSS** podczas pracy z arkuszami stylów wewnątrz dokumentu przy użyciu GroupDocs.Editor dla .NET. Niezależnie od tego, czy musisz dodać prefiks URL do obrazów, czcionek lub dowolnego zasobu zewnętrznego, poniższe kroki pokażą Ci dokładnie, jak **obsługiwać prefiks CSS** oraz jak **wyodrębnić zawartość CSS** do dalszego przetwarzania. Po zakończeniu przewodnika będziesz w stanie przepisować ścieżki zasobów, pobierać surowe ciągi CSS i integrować je z Twoim przepływem pracy w sieci z pewnością.

## Szybkie odpowiedzi
- **Co oznacza „obsługiwać prefiks CSS”?** Dodanie własnego prefiksu URL do zewnętrznych zasobów odwoływanych w CSS.  
- **Która metoda API zwraca style CSS?** `EditableDocument.GetCssContent(...)`.  
- **Czy potrzebna jest licencja?** Dostępna jest licencja próbna; licencja komercyjna jest wymagana w środowisku produkcyjnym.  
- **Jakie wersje .NET są obsługiwane?** .NET Framework 4.5+ oraz .NET Core/5/6.  
- **Czy mogę zmienić prefiks w czasie działania?** Tak – po prostu przekaż inny ciąg do `GetCssContent`.

## Co to jest obsługa prefiksu CSS?
Termin odnosi się do przepisywania adresów URL obrazów, czcionek lub dowolnych zewnętrznych zasobów w pliku CSS, aby wskazywały na lokalizację kontrolowaną przez Ciebie, taką jak CDN lub bezpieczny serwer. Dodając spójny bazowy URL jako prefiks, zapewniasz, że każdy zasób ładuje się prawidłowo, gdy dokument jest renderowany w przeglądarce lub przeglądarce internetowej.

## Dlaczego używać GroupDocs.Editor do wyodrębniania zawartości CSS?
GroupDocs.Editor może odczytać oryginalny CSS osadzony w dokumentach WordProcessing, zwrócić surowe ciągi arkuszy stylów i umożliwić ich manipulację przed renderowaniem lub zapisem. Eliminuje to ręczne parsowanie, zapewnia wierność wewnętrznej reprezentacji dokumentu i obsługuje **ponad 30 formatów plików**, przetwarzając pliki do **500 MB** bez ładowania całego pliku do pamięci.

## Wymagania wstępne
Zanim zaczniemy, upewnij się, że spełniasz następujące wymagania:
- Visual Studio: Potrzebujesz działającej instalacji Visual Studio.  
- .NET Framework: Upewnij się, że masz zainstalowany .NET Framework.  
- GroupDocs.Editor for .NET: Możesz go pobrać ze [strony pobierania GroupDocs.Editor for .NET](https://releases.groupdocs.com/editor/net/).  
- Przykładowy dokument: Przygotuj przykładowy dokument do edycji.

## Importowanie przestrzeni nazw
Najpierw zaimportujmy niezbędne przestrzenie nazw, aby nasz kod działał płynnie. Ten krok daje dostęp do podstawowych klas GroupDocs.Editor.

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Editor.Options;
```

## Krok 1: Inicjalizacja edytora
Klasa `Editor` jest punktem wejścia do pracy z dokumentami w GroupDocs.Editor. Zarządza operacjami ładowania, edycji i zapisu.  
Pierwszy krok polega na utworzeniu instancji `Editor` z Twoim przykładowym dokumentem. To konfiguruje środowisko edycji.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```

## Krok 2: Edycja dokumentu
Obiekt `EditableDocument` reprezentuje edytowalną wersję pliku i udostępnia jego wewnętrzne części, takie jak CSS, obrazy i HTML.  
Następnie uzyskujemy obiekt `EditableDocument`. Ten obiekt pozwala nam pracować z wewnętrznym CSS dokumentu.

```csharp
    using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
    {
```

## Krok 3: Ustawienie zewnętrznych prefiksów
Zdefiniuj prefiksy URL dla obrazów i czcionek. Te prefiksy będą dodawane do każdego odwołania do obrazu i czcionki znalezionego w CSS.

```csharp
        string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
        string externalFontsPrefix = "http://www.mywebsite.com/fonts/id=";
```

## Krok 4: Wyodrębnienie zawartości CSS z prefiksami
`GetCssContent` zwraca kolekcję ciągów arkuszy stylów CSS, które już zawierają podane przez Ciebie prefiksy URL.  
Wywołaj `GetCssContent`, przekazując prefiksy, które właśnie zdefiniowałeś. Metoda zwraca listę ciągów arkuszy stylów CSS, które już zawierają prefiksy URL.

```csharp
        List<string> stylesheets = document.GetCssContent(externalImagesPrefix, externalFontsPrefix);
```

## Krok 5: Wyświetlenie wyników
Wypisz liczbę znalezionych arkuszy stylów i wyświetl każdy z nich. To pomaga zweryfikować, że prefiksy zostały zastosowane prawidłowo.

```csharp
        Console.WriteLine("There are {0} stylesheets in the input document", stylesheets.Count);
        foreach (string css in stylesheets)
        {
            Console.WriteLine(css);
        }
    }
}
```

## Typowe problemy i rozwiązania
- **Brak zwróconych arkuszy stylów** – Upewnij się, że dokument źródłowy rzeczywiście zawiera CSS (np. dokument Word z formatowanymi tabelami lub osadzonym HTML).  
- **Nieprawidłowe URL** – Sprawdź, czy ciągi prefiksów kończą się odpowiednim separatorem (`/` lub `=`) dla routingu Twojego serwera.  
- **Problemy z wydajnością** – W przypadku bardzo dużych dokumentów rozważ przetwarzanie arkuszy stylów w partiach, aby uniknąć wysokiego zużycia pamięci.

## Najczęściej zadawane pytania

**Q: Czy mogę używać GroupDocs.Editor dla .NET z innymi formatami dokumentów?**  
A: Tak, GroupDocs.Editor dla .NET obsługuje PDF, Word, Excel, PowerPoint i wiele innych formatów.

**Q: Czy dostępna jest darmowa wersja próbna GroupDocs.Editor dla .NET?**  
A: Oczywiście! Możesz rozpocząć darmową wersję próbną na [stronie darmowej wersji próbnej GroupDocs](https://releases.groupdocs.com/).

**Q: Jak uzyskać tymczasową licencję dla GroupDocs.Editor dla .NET?**  
A: Tymczasową licencję możesz uzyskać ze [strony tymczasowej licencji](https://purchase.groupdocs.com/temporary-license/).

**Q: Gdzie mogę znaleźć szczegółową dokumentację GroupDocs.Editor dla .NET?**  
A: Szczegółowa dokumentacja jest dostępna na [stronie dokumentacji GroupDocs.Editor dla .NET](https://tutorials.groupdocs.com/editor/net/).

**Q: Jakie opcje wsparcia są dostępne dla GroupDocs.Editor dla .NET?**  
A: Wsparcie możesz uzyskać poprzez [forum wsparcia GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).

## Dodatkowe często zadawane pytania

**Q: Czy mogę zmienić prefiks po wyodrębnieniu CSS?**  
A: Tak. Wywołaj ponownie `GetCssContent` z innym ciągiem prefiksu; metoda zawsze używa wartości przekazanych w czasie działania.

**Q: Czy to działa z dokumentami zabezpieczonymi hasłem?**  
A: Tak. Podaj hasło w `WordProcessingLoadOptions` przy tworzeniu instancji `Editor`.

**Q: Czy można zapisać zmodyfikowany CSS z powrotem do dokumentu?**  
A: GroupDocs.Editor obecnie zapewnia dostęp tylko do odczytu CSS. Aby zachować zmiany, trzeba zastąpić oryginalny arkusz stylów przy użyciu podstawowych interfejsów XML dokumentu.

---

**Ostatnia aktualizacja:** 2026-09-26  
**Testowano z:** GroupDocs.Editor 23.12 for .NET  
**Autor:** GroupDocs

## Powiązane samouczki

- [Wyodrębnij zewnętrzny CSS z dokumentów Word przy użyciu GroupDocs.Editor .NET: Kompletny przewodnik](/editor/net/html-web-documents/extract-external-css-word-docs-groupdocs-editor-dotnet/)
- [Wyodrębnij i dodaj prefiks HTML z dokumentów Word przy użyciu GroupDocs.Editor .NET](/editor/net/html-web-documents/groupdocs-editor-dotnet-extract-prefix-html-word-docs/)
- [Jak wyodrębnić i zmodyfikować zawartość HTML w dokumentach Word przy użyciu GroupDocs.Editor .NET](/editor/net/html-web-documents/extract-modify-html-content-word-docs-groupdocs-editor-net/)