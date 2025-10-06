---
title: Zaawansowane wykorzystanie edytowalnych dokumentów
linktitle: Zaawansowane wykorzystanie edytowalnych dokumentów
second_title: Edytor GroupDocs.NET API
description: Poznaj zaawansowane wykorzystanie programu GroupDocs.Editor dla platformy .NET do programowego tworzenia, edytowania i wyodrębniania zasobów z dokumentów.
weight: 11
url: /pl/net/document-editing/advanced-usage-of-editable-documents/
type: docs
---
# Zaawansowane wykorzystanie edytowalnych dokumentów

## Wstęp
Jeśli jesteś programistą .NET i chcesz ulepszyć swoje możliwości edycji dokumentów, GroupDocs.Editor dla .NET oferuje potężny zestaw narzędzi. Ten obszerny przewodnik przeprowadzi Cię przez zaawansowane korzystanie z edytowalnych dokumentów przy użyciu programu GroupDocs.Editor, szczegółowo opisując każdy krok, aby upewnić się, że możesz wykorzystać jego pełny potencjał.
## Warunki wstępne
Zanim zagłębisz się w zaawansowane funkcje, upewnij się, że posiadasz następujące elementy:
- Program Visual Studio zainstalowany na komputerze programistycznym.
- .NET Framework kompatybilny z GroupDocs.Editor.
-  GroupDocs.Editor dla biblioteki .NET. Możesz[Pobierz to tutaj](https://releases.groupdocs.com/editor/net/).
-  Ważna licencja GroupDocs.Editor. Możesz dostać[bezpłatna wersja próbna](https://releases.groupdocs.com/) lub kup A[licencja tymczasowa](https://purchase.groupdocs.com/temporary-license/).
## Importuj przestrzenie nazw
Na początek upewnij się, że zaimportowałeś niezbędne przestrzenie nazw do projektu .NET:
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
## Krok 1: Tworzenie instancji EditableDocument
 Najpierw musisz utworzyć instancję`EditableDocument` ładując i edytując dokument wejściowy w obsługiwanym formacie.
```csharp
string inputFilePath = "YourSampleDocument.docx";
Editor editor = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```
Na tym etapie ładujemy dokument wejściowy i przygotowujemy go do edycji.
## Krok 2: Wyodrębnianie zasobów dokumentów
 The`EditableDocument` zawiera różne zasoby, które można wydobywać i manipulować. Podzielmy je na części:
### Krok 2.1: Wyodrębnij cały dokument jako HTML
Można wygenerować pojedynczy ciąg znaków zawierający cały dokument ze wszystkimi zasobami osadzonymi w formacie HTML.
```csharp
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```
Ten ciąg będzie dość duży, ponieważ zawiera arkusze stylów, obrazy i czcionki zakodowane w base64.
### Krok 2.2: Wyodrębnij wszystkie obrazy
Wyodrębnij wszystkie obrazy z dokumentu.
```csharp
List<IImageResource> allImages = beforeEdit.Images;
```
### Krok 2.3: Wyodrębnij wszystkie czcionki
Wyodrębnij wszystkie czcionki użyte w dokumencie.
```csharp
List<FontResourceBase> allFonts = beforeEdit.Fonts;
```
### Krok 2.4: Wyodrębnij wszystkie arkusze stylów
Wyodrębnij wszystkie arkusze stylów w formacie tekstowym.
```csharp
List<CssText> allStylesheets = beforeEdit.Css;
```
### Krok 2.5: Zbierz wszystkie zasoby
Zbierz wszystkie zasoby w jednym połączeniu.
```csharp
List<IHtmlResource> allResources = beforeEdit.AllResources;
```
Dotyczy to obrazów, czcionek i arkuszy stylów.
### Krok 2.6: Uzyskaj znaczniki HTML
Uzyskaj znaczniki HTML dokumentu bez osadzonych zasobów.
```csharp
string htmlMarkup = beforeEdit.GetContent();
```
## Krok 3: Dostosowywanie linków zewnętrznych
Czasami trzeba dostosować linki zewnętrzne, aby wskazywały niestandardową procedurę obsługi zasobów. Oto jak to zrobić:
### Krok 3.1: Przygotuj niestandardowe prefiksy
Przygotuj przedrostki, które będą dołączane do oryginalnych linków zewnętrznych.
```csharp
string customImagesRequesthandlerUri = "http://przykład.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://przykład.com/CssHandler/id=";
string customFontsRequesthandlerUri = "http://przykład.com/FontsHandler/id=";
```
### Krok 3.2: Wygeneruj prefiksowane znaczniki HTML
Wygeneruj znaczniki HTML z dostosowanymi linkami.
```csharp
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```
### Krok 3.3: Uzyskaj treść HTML zawierającą wyłącznie treść
Niektóre edytory WYSIWYG obsługują tylko czyste znaczniki HTML bez nagłówków.
```csharp
string onlyBodyContent = beforeEdit.GetBodyContent();
```
### Krok 3.4: Treść zawierająca tylko treść z prefiksem
Generuj samą treść z niestandardowymi przedrostkami obrazów.
```csharp
string prefixedBodyContent = beforeEdit.GetBodyContent(customImagesRequesthandlerUri);
```
### Krok 3.5: Wyodrębnij arkusze stylów
Wyodrębnij arkusze stylów użyte w dokumencie.
```csharp
List<string> stylesheets = beforeEdit.GetCssContent();
```
### Krok 3.6: Przedrostki arkuszy stylów
Wyodrębnij arkusze stylów z niestandardowymi przedrostkami.
```csharp
List<string> prefixedStylesheets = beforeEdit.GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri);
```
## Krok 4: Zapisz dokument jako HTML
Zapisz edytowany dokument jako plik HTML wraz z jego zasobami.
```csharp
string htmlFilePath = Path.Combine("output", Path.GetFileNameWithoutExtension(inputFilePath) + ".html");
beforeEdit.Save(htmlFilePath);
```
Ta metoda tworzy oddzielny katalog dla zasobów, takich jak arkusze stylów, obrazy i czcionki.
## Krok 5: Pozbycie się edytowalnego dokumentu
 Implementacje EditableDocument`IDisposable` i zapewnia możliwość sprawdzenia, czy instancja została usunięta.
```csharp
Console.WriteLine("EditableDocument is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");
```
### Krok 5.1 Obsługa zdarzenia Dispose
Możesz także zapisać się na wydarzenie utylizacji.
```csharp
EventHandler someMethod = delegate { Console.WriteLine("Disposing event was spotted!"); };
beforeEdit.Disposed += someMethod;
```
## Krok 6: Tworzenie edytowalnego dokumentu z HTML
Utwórz instancję EditableDocument z dokumentu HTML.
### Krok 6.1: Z pliku HTML
```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
```
### Krok 6.2: Ze znaczników HTML
```csharp
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);
```
Te instancje (afterEditFromFile i afterEditFromMarkup) są identyczne z oryginałem (przed Edit).
## Krok 7: Ręczna utylizacja
Ręcznie usuń instancje EditableDocument.
```csharp
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```
Zapewnia to właściwe oczyszczenie zasobów.
## Wniosek
GroupDocs.Editor dla .NET zapewnia niezawodne narzędzia do programowej edycji dokumentów. Postępując zgodnie z tym szczegółowym przewodnikiem, możesz efektywnie zarządzać zawartością dokumentu, zasobami i formatami wyjściowymi. Niezależnie od tego, czy osadzasz zasoby, dostosowujesz linki zewnętrzne, czy konwertujesz dokumenty do formatu HTML, GroupDocs.Editor zapewnia funkcjonalność potrzebną do zaawansowanej manipulacji dokumentami.
## Często zadawane pytania
### Jakie formaty obsługuje GroupDocs.Editor?
GroupDocs.Editor obsługuje różne formaty, w tym DOCX, XLSX, PPTX i inne.
### Czy mogę używać GroupDocs.Editor bez licencji?
 Tak, możesz go używać z[bezpłatna wersja próbna](https://releases.groupdocs.com/) lub[licencja tymczasowa](https://purchase.groupdocs.com/temporary-license/).
### Jak wyodrębnić określone zasoby z dokumentu?
 Możesz wyodrębnić obrazy, czcionki i arkusze stylów, korzystając z dostarczonych metod, takich jak`Images`, `Fonts` , I`Css`.
### Czy można dostosować linki w wynikach HTML?
Tak, możesz dostosować linki zewnętrzne, określając niestandardowe przedrostki obrazów, CSS i czcionek.
### Jak zapisać edytowany dokument jako plik HTML?
 Użyj`Save` metoda`EditableDocument`class, aby zapisać dokument jako plik HTML wraz z jego zasobami.