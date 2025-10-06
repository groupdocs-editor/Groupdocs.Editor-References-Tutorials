---
title: Pracuj z dokumentami zwykłego tekstu
linktitle: Pracuj z dokumentami zwykłego tekstu
second_title: Edytor GroupDocs.NET API
description: Dowiedz się, jak edytować dokumenty w postaci zwykłego tekstu za pomocą programu GroupDocs.Editor dla platformy .NET, korzystając z naszego przewodnika krok po kroku. Uprość proces edycji dokumentów .NET.
weight: 15
url: /pl/net/document-processing/work-plain-text-documents/
type: docs
---
# Pracuj z dokumentami zwykłego tekstu

## Wstęp
Chcesz usprawnić proces edycji dokumentów w .NET? Nie szukaj dalej niż GroupDocs.Editor dla .NET! Ten potężny interfejs API pozwala z łatwością edytować szeroką gamę formatów dokumentów. W tym samouczku przeprowadzimy Cię przez proces pracy z dokumentami w formacie zwykłego tekstu przy użyciu programu GroupDocs.Editor dla platformy .NET. Na koniec będziesz w stanie poradzić sobie z edycją dokumentów tekstowych jak profesjonalista. Gotowy do nurkowania? Zacznijmy!
## Warunki wstępne
Zanim zaczniemy, musisz przygotować kilka rzeczy:
- Środowisko programistyczne .NET: Upewnij się, że masz skonfigurowane działające środowisko programistyczne .NET. Visual Studio to popularny wybór.
-  GroupDocs.Editor dla .NET: Pobierz i zainstaluj[Edytor GroupDocs dla .NET](https://releases.groupdocs.com/editor/net/).
- Podstawowa znajomość języka C#: Znajomość języka programowania C# pomoże Ci postępować zgodnie z przykładami.
- Edytor tekstu: wystarczy dowolny edytor tekstu, chociaż zaleca się korzystanie z programu Visual Studio Code ze względu na jego funkcje i łatwość użycia.
## Importuj przestrzenie nazw
Aby rozpocząć korzystanie z GroupDocs.Editor dla .NET, musisz zaimportować niezbędne przestrzenie nazw do swojego projektu. Dzięki temu wszystkie wymagane klasy i metody są dostępne do użycia.
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```
Podzielmy proces na łatwe do wykonania etapy. Postępuj zgodnie z instrukcjami, które poprowadzą Cię przez każdy etap edytowania dokumentów w formacie zwykłego tekstu przy użyciu programu GroupDocs.Editor dla platformy .NET.
## Krok 1: Uzyskaj ścieżkę do wejściowego pliku TXT
Najpierw musisz określić ścieżkę do wejściowego pliku TXT. Może to być ścieżka do pliku lokalnego lub strumień zawierający zawartość pliku.
```csharp
string inputFilePath = "YourSampleDocument.txt";
```
## Krok 2: Utwórz instancję edytora
 Następnie utwórz instancję`Editor` klasa. Klasa ta odpowiada za ładowanie i edycję dokumentów. Na tym etapie nie są wymagane żadne opcje ładowania.
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## Krok 3: Utwórz opcje edycji TXT
Teraz utwórz opcje edycji TXT. Opcje te pozwalają określić, w jaki sposób treść tekstowa ma być przetwarzana podczas edycji.
```csharp
    TextEditOptions editOptions = new TextEditOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        RecognizeLists = true,
        LeadingSpaces = TextLeadingSpacesOptions.ConvertToIndent,
        TrailingSpaces = TextTrailingSpacesOptions.Trim
    };
```
## Krok 4: Utwórz instancję EditableDocument
 Po ustawieniu opcji edycji utwórz plik`EditableDocument` instancja. Oznacza dokument w formacie edytowalnym.
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## Krok 5: Edytuj zawartość dokumentu
Pobierz oryginalną treść tekstową i wprowadź żądane zmiany. W tym przykładzie zastąpimy słowo „tekst” słowem „EDYTOWANY tekst”.
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("text", "EDITED text");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## Krok 6: Utwórz dokument edytowalny ze zaktualizowaną zawartością
 Po dokonaniu niezbędnych zmian utwórz nowy`EditableDocument` ze zaktualizowaną zawartością i oryginalnymi zasobami.
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## Krok 7: Utwórz opcje zapisywania edytora tekstu
Przygotuj opcje zapisu dla formatu WordProcessing. W tym przykładzie zastosowano format DOCM i określono ustawienia regionalne.
```csharp
    WordProcessingSaveOptions wordSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm)
    {
        Locale = System.Globalization.CultureInfo.GetCultureInfo("en-GB")
    };
```
## Krok 8: Utwórz opcje zapisywania TXT
Podobnie utwórz opcje zapisu dla formatu TXT. Upewnij się, że kodowanie jest ustawione na UTF-8 i zachowaj układ tabeli.
```csharp
    TextSaveOptions txtSaveOptions = new TextSaveOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        PreserveTableLayout = true
    };
```
## Krok 9: Przygotuj ścieżki wyjściowe
Przygotuj ścieżki do zapisania wynikowych plików DOCX i TXT. Użyj ścieżki pliku wejściowego, aby określić katalog wyjściowy i nazwy plików.
```csharp
    string outputWordPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".docm");
    string outputTxtPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".txt");
```
## Krok 10: Zapisz edytowany dokument
Na koniec zapisz edytowany dokument w formatach DOCX i TXT, korzystając z określonych opcji zapisywania.
```csharp
    editor.Save(afterEdit, outputWordPath, wordSaveOptions);
    editor.Save(afterEdit, outputTxtPath, txtSaveOptions);
}
System.Console.WriteLine("Document editing process completed successfully!");
```
## Wniosek
 Gratulacje! Pomyślnie edytowałeś dokument w formacie zwykłego tekstu za pomocą GroupDocs.Editor dla .NET. To potężne narzędzie upraszcza edycję dokumentów, ułatwiając integrację z aplikacjami .NET. Niezależnie od tego, czy obsługujesz proste pliki tekstowe, czy złożone formaty dokumentów, GroupDocs.Editor poradzi sobie z tym. Odkryj więcej funkcji i możliwości, odwiedzając witrynę[Dokumentacja GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/).
## Często zadawane pytania
### Jakie formaty plików obsługuje GroupDocs.Editor dla .NET?
 GroupDocs.Editor dla .NET obsługuje szeroką gamę formatów plików, w tym DOCX, TXT, HTML i inne. Sprawdź[dokumentacja](https://tutorials.groupdocs.com/editor/net/) aby uzyskać pełną listę.
### Jak mogę uzyskać bezpłatną wersję próbną GroupDocs.Editor dla .NET?
 Możesz pobrać bezpłatną wersję próbną GroupDocs.Editor dla .NET z witryny[strona z wydaniami](https://releases.groupdocs.com/).
### Czy mogę kupić tymczasową licencję na GroupDocs.Editor dla .NET?
Tak, możesz uzyskać tymczasową licencję od[Strona zakupu GroupDocs](https://purchase.groupdocs.com/temporary-license/).
### Gdzie mogę uzyskać pomoc dotyczącą GroupDocs.Editor dla platformy .NET?
 Wsparcie jest dostępne poprzez[Forum pomocy technicznej GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).
### Czy dostępna jest szczegółowa dokumentacja programu GroupDocs.Editor dla platformy .NET?
 Tak, szczegółowa dokumentacja jest dostępna na stronie[Strona dokumentacji GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/).