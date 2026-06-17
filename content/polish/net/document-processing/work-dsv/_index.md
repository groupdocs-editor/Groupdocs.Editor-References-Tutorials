---
date: 2026-06-06
description: Dowiedz się, jak **create editable document** objects z plików CSV i
  TSV przy użyciu GroupDocs.Editor for .NET. Ten przewodnik pokazuje również, jak
  **read delimited text C#** oraz **edit CSV .NET** efektywnie w Visual Studio.
keywords:
- create editable document
- read delimited text c#
- edit csv .net
- parse delimited values c#
linktitle: Praca z Delimited Separated Values (DSV) – tworzenie edytowalnego dokumentu
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to **create editable document** objects from CSV and TSV
    files using GroupDocs.Editor for .NET. This guide also shows how to **read delimited
    text C#** and **edit CSV .NET** efficiently in Visual Studio.
  headline: Work with Delimited Separated Values (DSV) – create editable document
  type: TechArticle
- questions:
  - answer: Yes, the API streams data and can handle files larger than 1 GB without
      loading the entire document into memory.
    question: Can I use GroupDocs.Editor for .NET to edit large CSV files?
  - answer: Absolutely – any single‑character delimiter (e.g., pipe `|`, semicolon
      `;`) is supported as long as you specify it in `DelimitedTextEditOptions`.
    question: Does GroupDocs.Editor for .NET support other DSV formats besides CSV
      and TSV?
  - answer: Yes, you can set the `Encoding` property in `DelimitedTextSaveOptions`
      to UTF‑8, UTF‑16, ISO‑8859‑1, or any .NET `Encoding` you require.
    question: Is it possible to customize the encoding when saving DSV files?
  - answer: Yes – after editing, simply use `SpreadsheetSaveOptions` to export the
      content as an `.xlsx` workbook.
    question: Can I convert a CSV file to an Excel spreadsheet using GroupDocs.Editor
      for .NET?
  - answer: Detailed API references and code samples are available **[here](https://tutorials.groupdocs.com/editor/net/)**.
    question: Where can I find more documentation on GroupDocs.Editor for .NET?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Praca z Delimited Separated Values (DSV) – tworzenie edytowalnego dokumentu
type: docs
url: /pl/net/document-processing/work-dsv/
weight: 12
---

# Praca z wartościami rozdzielonymi (DSV) – tworzenie edytowalnego dokumentu

Jeśli jesteś programistą .NET, który potrzebuje **create editable document** obiektów z wartościami rozdzielonymi (DSV) takimi jak CSV lub TSV, trafiłeś we właściwe miejsce. W pierwszych 100 słowach wyjaśnimy, dlaczego GroupDocs.Editor dla .NET jest najpewniejszym sposobem na **read delimited text C#**, edycję i ponowne zapisanie bez utraty formatowania. Otrzymasz kompletny, gotowy do kopiowania i wklejania przepływ pracy, który naturalnie wpasowuje się w każde rozwiązanie Visual Studio.

## Szybkie odpowiedzi
- **Która biblioteka najlepiej obsługuje edycję CSV w .NET?** GroupDocs.Editor for .NET.
- **Czy mogę edytować duże pliki CSV w Visual Studio?** Tak – API strumieniuje dane i unika ładowania całego pliku do pamięci.
- **Czy potrzebuję licencji do użytku produkcyjnego?** Wymagana jest licencja komercyjna; dostępna jest darmowa wersja próbna.
- **Jakie formaty mogę uzyskać po edycji?** CSV, TSV i formaty arkuszy kalkulacyjnych kompatybilne z Excel.
- **Czy API jest kompatybilne z .NET 6+?** Absolutnie – obsługuje .NET Framework 4.5+, .NET Core 3.1+, .NET 5 i .NET 6.

## Co oznacza „create editable document” w kontekście GroupDocs.Editor?
**Create editable document** oznacza wygenerowanie instancji `EditableDocument`, która reprezentuje zmienną wersję pliku źródłowego (CSV, TSV itp.) w pamięci. Ten obiekt pozwala odczytywać, modyfikować i ponownie zapisywać zawartość przy użyciu tego samego API. Udostępnia metody do pobierania tekstu dokumentu, stosowania zmian i zapisywania go w różnych formatach, zapewniając zachowanie wyrównania kolumn i cudzysłowów.

## Dlaczego używać GroupDocs.Editor do obsługi DSV?
GroupDocs.Editor obsługuje **ponad 50 formatów wejściowych i wyjściowych**, w tym CSV, TSV oraz arkusze kalkulacyjne kompatybilne z Excel, przy jednoczesnym utrzymaniu zużycia pamięci poniżej 10 MB dla plików do 500 MB. Automatycznie zachowuje wyrównanie kolumn, zasady cudzysłowów i niestandardowe kodowania, co eliminuje potrzebę ręcznej logiki parsowania.

## Wymagania wstępne
- **Visual Studio** (dowolna aktualna edycja) – będziesz rozwijać i debugować bezpośrednio w IDE.
- **GroupDocs.Editor for .NET** – pobierz najnowszy pakiet **[here](https://releases.groupdocs.com/editor/net/)**.
- **Podstawowa znajomość C#** – tutorial zakłada, że potrafisz utworzyć projekt konsolowy lub ASP.NET i dodać pakiety NuGet.

## Importowanie przestrzeni nazw
`Editor`, `EditableDocument` oraz klasy opcji znajdują się w przestrzeni nazw `GroupDocs.Editor`.

Klasa `DelimitedTextEditOptions` jest punktem wejścia do definiowania separatora (przecinek, tabulator itp.) oraz innych reguł parsowania.

```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

## Jak utworzyć edytowalny dokument z pliku CSV?
Wczytaj źródłowy CSV za pomocą `Editor` i wywołaj metodę `Edit`, przekazując instancję `DelimitedTextEditOptions` określającą separator przecinka. Metoda zwraca `EditableDocument`, który możesz manipulować w pamięci. Ten dwustopniowy wzorzec — wczytaj → edytuj — obejmuje scenariusze **read delimited text C#** i zapewnia zachowanie pierwotnej struktury pliku.

## Krok 1: Uzyskaj ścieżkę do wejściowego pliku DSV
Najpierw musisz określić absolutną lub względną ścieżkę do źródłowego pliku DSV. Dla demonstracji użyjemy prostego CSV znajdującego się w folderze `Data` projektu.

```csharp
string inputFilePath = "Your Sample Document";
```

## Krok 2: Utwórz instancję Editor
`Editor` jest klasą rdzeniową, która koordynuje wczytywanie, edycję i zapisywanie. Utworzenie jej przy użyciu obiektu `FileInfo` daje pełną kontrolę nad cyklem życia pliku.

```csharp
using (Editor editor = new Editor(inputFilePath))
{
```

## Krok 3: Utwórz opcje edycji DSV
`DelimitedTextEditOptions` informuje edytor, jak interpretować plik. Możesz ustawić separator, czy pierwszy wiersz zawiera nagłówki oraz kodowanie znaków.

```csharp
    Options.DelimitedTextEditOptions editOptions = new DelimitedTextEditOptions(",");
    editOptions.ConvertDateTimeData = false;
    editOptions.ConvertNumericData = true;
    editOptions.TreatConsecutiveDelimitersAsOne = true;
```

## Krok 4: Utwórz instancję EditableDocument
`EditableDocument` reprezentuje zmienną wersję pliku źródłowego w pamięci. Wywołanie `Editor.Edit` z opcjami zwraca `EditableDocument`. Ten obiekt przechowuje tekst pliku w zmiennym łańcuchu, gotowy do dowolnej operacji **parse delimited values C#**, której potrzebujesz.

```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```

## Krok 5: Edytuj zawartość dokumentu
`GetDocumentText()` zwraca bieżący tekst edytowalnego dokumentu jako łańcuch. Pobierz oryginalny tekst za pomocą `EditableDocument.GetDocumentText()`, wykonaj modyfikacje (np. zamień wartość w kolumnie) i zapisz wynik w nowym łańcuchu. To miejsce, w którym **edit CSV .NET** bez ingerencji w niskopoziomowe strumienie plików.

```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("SsangYong", "Chevrolet").Replace("Kyron", "Camaro");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```

## Krok 6: Utwórz EditableDocument z zaktualizowaną zawartością
Owiń zmodyfikowany łańcuch z powrotem w `EditableDocument`. Ten krok finalizuje zmiany i przygotowuje obiekt do zapisu w dowolnym obsługiwanym formacie.

```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```

## Krok 7: Utwórz opcje zapisu CSV
`DelimitedTextSaveOptions` określa, jak zapisać edytowaną zawartość z powrotem do pliku CSV. Gdy będziesz gotowy, aby zachować zmiany, skonfiguruj `DelimitedTextSaveOptions`. Możesz podać ten sam separator, inny lub nawet zmienić styl zakończenia linii.

```csharp
    Options.DelimitedTextSaveOptions csvSaveOptions = new DelimitedTextSaveOptions(",");
    csvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

## Krok 8: Utwórz opcje zapisu TSV
Jeśli potrzebujesz wersji rozdzielonej tabulatorem, po prostu zmień separator na `\t`. Ten sam `EditableDocument` może być zapisany wielokrotnie z różnymi opcjami.

```csharp
    Options.DelimitedTextSaveOptions tsvSaveOptions = new DelimitedTextSaveOptions("\t");
    tsvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

## Krok 9: Utwórz opcje zapisu arkusza kalkulacyjnego
`SpreadsheetSaveOptions` konfiguruje eksport dokumentu do formatów kompatybilnych z Excel, takich jak .xlsx. GroupDocs.Editor umożliwia również eksport edytowanych danych do formatu kompatybilnego z Excel (`.xlsx`). Klasa `SpreadsheetSaveOptions` automatycznie obsługuje typy kolumn, formuły i stylowanie komórek.

```csharp
    Options.SpreadsheetSaveOptions cellsSaveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
```

## Krok 10: Przygotuj ścieżki zapisu
Zdefiniuj odrębne ścieżki wyjściowe dla każdego formatu. Używanie przejrzystych konwencji nazewnictwa (np. `output.csv`, `output.tsv`, `output.xlsx`) pomaga utrzymać porządek w projekcie.

```csharp
    string outputCsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".csv");
    string outputTsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".tsv");
    string outputCellsPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".xlsm");
```

## Krok 11: Zapisz edytowany dokument
`Save()` zapisuje dokument na dysku przy użyciu podanych opcji zapisu. Wywołaj `EditableDocument.Save` z odpowiednimi opcjami dla każdego docelowego formatu. API zapisuje plik bezpośrednio na dysku, zachowując oryginalne kodowanie, chyba że je nadpiszesz.

```csharp
    editor.Save(afterEdit, outputCsvPath, csvSaveOptions);
    editor.Save(afterEdit, outputTsvPath, tsvSaveOptions);
    editor.Save(afterEdit, outputCellsPath, cellsSaveOptions);
```

## Krok 12: Usuń instancje EditableDocument
Zarówno `Editor`, jak i `EditableDocument` implementują `IDisposable`. Ich usunięcie zwalnia uchwyty plików i zasoby niezarządzane, co jest kluczowe przy przetwarzaniu wielu plików w zadaniu wsadowym.

```csharp
    beforeEdit.Dispose();
    afterEdit.Dispose();
}
System.Console.WriteLine("WorkingWithDsv routine has successfully finished");
```

## Częste problemy i rozwiązania
| Problem | Dlaczego się pojawia | Rozwiązanie |
|---------|----------------------|-------------|
| **Nieoczekiwane dodatkowe cudzysłowy** | Domyślny parser CSV może traktować wbudowane przecinki jako separatory. | Ustaw `EscapeMode = EscapeMode.DoubleQuote` w `DelimitedTextEditOptions`. |
| **Wzrost zużycia pamięci przy dużym pliku** | Ładowanie pliku 500 MB bez strumieniowania. | Użyj `Editor.Load` z `LoadOptions`, które włączają leniwe ładowanie. |
| **Niezgodność kodowania** | Plik źródłowy używa UTF‑16, ale opcje domyślnie ustawione są na UTF‑8. | Jawnie ustaw `Encoding = Encoding.Unicode` w opcjach zapisu. |

## Najczęściej zadawane pytania

**Q: Czy mogę używać GroupDocs.Editor dla .NET do edycji dużych plików CSV?**  
A: Tak, API strumieniuje dane i może obsługiwać pliki większe niż 1 GB bez ładowania całego dokumentu do pamięci.

**Q: Czy GroupDocs.Editor dla .NET obsługuje inne formaty DSV poza CSV i TSV?**  
A: Absolutnie – każdy jednopunktowy separator (np. pionowa kreska `|`, średnik `;`) jest obsługiwany, o ile zostanie określony w `DelimitedTextEditOptions`.

**Q: Czy można dostosować kodowanie przy zapisywaniu plików DSV?**  
A: Tak, możesz ustawić właściwość `Encoding` w `DelimitedTextSaveOptions` na UTF‑8, UTF‑16, ISO‑8859‑1 lub dowolne kodowanie .NET, którego potrzebujesz.

**Q: Czy mogę przekonwertować plik CSV na arkusz Excel przy użyciu GroupDocs.Editor dla .NET?**  
A: Tak – po edycji wystarczy użyć `SpreadsheetSaveOptions`, aby wyeksportować zawartość jako skoroszyt `.xlsx`.

**Q: Gdzie mogę znaleźć więcej dokumentacji na temat GroupDocs.Editor dla .NET?**  
A: Szczegółowe odniesienia API i przykłady kodu są dostępne **[here](https://tutorials.groupdocs.com/editor/net/)**.

---

**Ostatnia aktualizacja:** 2026-06-06  
**Testowano z:** GroupDocs.Editor 23.10 for .NET  
**Autor:** GroupDocs

## Powiązane samouczki

- [Samouczki edycji tekstu zwykłego i dokumentów DSV dla GroupDocs.Editor .NET](/editor/net/plain-text-dsv-documents/)
- [Opanuj GroupDocs.Editor .NET dla efektywnej edycji i konwersji dokumentów CSV](/editor/net/plain-text-dsv-documents/groupdocs-editor-net-csv-editing-guide/)
- [Mistrzostwo ładowania dokumentów w .NET z GroupDocs.Editor: Kompletny przewodnik](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)