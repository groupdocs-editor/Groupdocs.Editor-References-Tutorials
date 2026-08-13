---
date: 2026-06-06
description: Dowiedz się, jak wyświetlić obsługiwane formaty dokumentów i określić
  rozszerzenie formatu pliku przy użyciu GroupDocs.Editor dla .NET. Przewodnik krok
  po kroku z fragmentami kodu, szybkimi odpowiedziami i FAQ.
keywords:
- list supported document formats
- determine file format extension
- GroupDocs.Editor .NET
- document editing API
- supported formats guide
linktitle: Lista obsługiwanych formatów dokumentów
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to list supported document formats and determine file format
    extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets,
    quick answers, and FAQs.
  headline: List Supported Document Formats with GroupDocs.Editor .NET
  type: TechArticle
- description: Learn how to list supported document formats and determine file format
    extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets,
    quick answers, and FAQs.
  name: List Supported Document Formats with GroupDocs.Editor .NET
  steps:
  - name: '**.NET development environment** – Visual Studio 2022 or any IDE that supports
      .NET 6+.'
    text: '**.NET development environment** – Visual Studio 2022 or any IDE that supports
      .NET 6+.'
  - name: '**GroupDocs.Editor for .NET library** – download from the [GroupDocs releases
      page](https://releases.groupdocs.com/editor/net/).'
    text: '**GroupDocs.Editor for .NET library** – download from the [GroupDocs releases
      page](https://releases.groupdocs.com/editor/net/).'
  - name: '**Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/)
      for unrestricted access.'
    text: '**Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/)
      for unrestricted access.'
  - name: '**Basic C# knowledge** – familiarity with namespaces, `using` statements,
      and console output.'
    text: '**Basic C# knowledge** – familiarity with namespaces, `using` statements,
      and console output.'
  - name: '**Loop Through Formats:** We iterate over all available Word‑processing
      formats.'
    text: '**Loop Through Formats:** We iterate over all available Word‑processing
      formats.'
  - name: '**Output Format Details:** For each format we print its friendly name and
      default file extension.'
    text: '**Output Format Details:** For each format we print its friendly name and
      default file extension.'
  - name: '**Loop Through Formats:** The same looping logic applies to presentations.'
    text: '**Loop Through Formats:** The same looping logic applies to presentations.'
  - name: '**Output Format Details:** The name and extension are displayed for each
      format.'
    text: '**Output Format Details:** The name and extension are displayed for each
      format.'
  - name: '**Parse Format:** `FromExtension` converts the `.xlsm` extension into its
      internal `SpreadsheetFormat` enum.'
    text: '**Parse Format:** `FromExtension` converts the `.xlsm` extension into its
      internal `SpreadsheetFormat` enum.'
  - name: '**Output Format:** The parsed format’s name is printed, confirming the
      mapping.'
    text: '**Output Format:** The parsed format’s name is printed, confirming the
      mapping.'
  type: HowTo
- questions:
  - answer: '`DocumentFormatInfo` provides metadata about supported file types, while
      `SaveOptions` configures how a document is written back to disk (format, compression,
      etc.).'
    question: What is the difference between `DocumentFormatInfo` and `SaveOptions`?
  - answer: Yes—use `DocumentFormatInfo.FromExtension("yourExt")`; if the extension
      isn’t recognized, the method returns `null`.
    question: Can I list formats for a custom file extension?
  - answer: Absolutely. Pass the password to the `Editor` constructor via `EditorSettings`
      to open encrypted documents.
    question: Does GroupDocs.Editor support password‑protected files?
  - answer: Over **30 input and output formats**, spanning Word, Excel, PowerPoint,
      HTML, and plain text.
    question: How many formats does GroupDocs.Editor actually support?
  - answer: Use the `GetEditableWordProcessingFormats()` (or Spreadsheet/Presentation
      equivalents) to retrieve formats that allow full edit capabilities.
    question: Is there a way to restrict the list to only editable formats?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Lista obsługiwanych formatów dokumentów w GroupDocs.Editor .NET
type: docs
url: /pl/net/document-processing/work-document-formats/
weight: 13
---

# Lista obsługiwanych formatów dokumentów

Witamy w naszym obszernej samouczku dotyczącym **jak wyświetlić obsługiwane formaty dokumentów** z GroupDocs.Editor dla .NET. Niezależnie od tego, czy tworzysz aplikację webową skoncentrowaną na dokumentach, czy narzędzie desktopowe klasy enterprise, znajomość dokładnych formatów, które możesz edytować lub konwertować, jest niezbędna. W tym przewodniku dowiesz się, jak wyliczyć formaty, parsować rozszerzenia i edytować dokumenty — wszystko z jasnymi, przyjaznymi dla człowieka wyjaśnieniami i gotowymi do uruchomienia fragmentami kodu.

## Szybkie odpowiedzi
- **Jak wyświetlić wszystkie obsługiwane formaty?** Użyj `DocumentFormatInfo.GetSupportedWordProcessingFormats()` (lub odpowiedników dla Presentation/Spreadsheet) i iteruj kolekcję.  
- **Czy mogę określić format na podstawie rozszerzenia pliku?** Tak — wywołaj `DocumentFormatInfo.FromExtension(".docx")`.  
- **Jakie typy plików obsługuje GroupDocs.Editor?** Ponad 30 formatów wejściowych i wyjściowych, w tym DOCX, XLSX, PPTX, HTML oraz zwykły tekst.  
- **Czy potrzebuję licencji, aby wyświetlić formaty?** Tymczasowa licencja odblokowuje pełne API; w przeciwnym razie wersja próbna działa z ograniczonymi funkcjami.  
- **Które wersje .NET są kompatybilne?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.

## Co oznacza „lista obsługiwanych formatów dokumentów”?
Wyrażenie odnosi się do programowego pobierania kolekcji typów plików, które GroupDocs.Editor może otworzyć, edytować i zapisać. Ta operacja pozwala tworzyć dynamiczne listy rozwijane w interfejsie użytkownika lub weryfikować przesyłane pliki przed przetworzeniem, zapewniając, że tylko kompatybilne pliki są przekazywane do edytora w celu dalszej manipulacji.

## Dlaczego warto wyświetlać obsługiwane formaty dokumentów?
GroupDocs.Editor **obsługuje ponad 30 formatów wejściowych i wyjściowych** i może obsługiwać pliki do **2 GB** bez ładowania całego dokumentu do pamięci. Znajomość dokładnej listy zapobiega błędom w czasie wykonywania, poprawia doświadczenie użytkownika i umożliwia egzekwowanie reguł biznesowych, takich jak „zezwalaj tylko na edytowalne dokumenty Office”. Pomaga również prezentować użytkownikom wyłącznie formaty, które naprawdę obsługuje Twoja aplikacja.

## Wymagania wstępne
1. **Środowisko programistyczne .NET** – Visual Studio 2022 lub dowolne IDE obsługujące .NET 6+.  
2. **Biblioteka GroupDocs.Editor for .NET** – pobierz ze [strony wydań GroupDocs](https://releases.groupdocs.com/editor/net/).  
3. **Tymczasowa licencja** – uzyskaj [tymczasową licencję](https://purchase.groupdocs.com/temporary-license/) dla nieograniczonego dostępu.  
4. **Podstawowa znajomość C#** – znajomość przestrzeni nazw, instrukcji `using` oraz wyjścia konsoli.

## Jak wyświetlić obsługiwane formaty dokumentów?
Załaduj kolekcję obsługiwanych formatów i wypisz nazwę oraz rozszerzenie każdego formatu. Ten dwustopniowy wzorzec działa dla dokumentów Word, Spreadsheet i Presentation. Iterując kolekcję, możesz dynamicznie wypełniać elementy UI, takie jak listy rozwijane, zapewniając, że użytkownicy mogą wybierać jedynie formaty, które edytor rzeczywiście obsługuje.

```csharp
// No actual code block – placeholder retained from original tutorial
```csharp
using System;
using GroupDocs.Editor.Options;
```
```

### Wyświetlanie formatów przetwarzania tekstu
`Formats.WordProcessingFormats` jest wyliczeniem opisującym każdy typ pliku przetwarzania tekstu rozpoznawany przez edytor. Właściwość `All` zwraca kolekcję tych obiektów formatu.

```csharp
```csharp
foreach (Formats.WordProcessingFormats oneFormat in Formats.WordProcessingFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**Wyjaśnienie:**  
1. **Iteracja po formatach:** Przechodzimy po wszystkich dostępnych formatach przetwarzania tekstu.  
2. **Wyświetlanie szczegółów formatu:** Dla każdego formatu wypisujemy przyjazną nazwę i domyślne rozszerzenie pliku.

### Wyświetlanie formatów prezentacji
`Formats.PresentationFormats` działa w ten sam sposób dla plików prezentacji, udostępniając każdy obsługiwany typ prezentacji poprzez kolekcję `All`.

```csharp
```csharp
foreach (Formats.PresentationFormats oneFormat in Formats.PresentationFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**Wyjaśnienie:**  
1. **Iteracja po formatach:** Ta sama logika iteracji dotyczy prezentacji.  
2. **Wyświetlanie szczegółów formatu:** Nazwa i rozszerzenie są wyświetlane dla każdego formatu.

## Jak określić rozszerzenie formatu pliku?
Czasami masz tylko nazwę pliku i musisz wywnioskować odpowiadający mu `DocumentFormat`. GroupDocs.Editor oferuje prosty statyczny pomocnik, który mapuje rozszerzenie pliku na wewnętrzną reprezentację formatu, umożliwiając walidację lub konwersję plików przed ich załadowaniem do edytora.

### Parsowanie formatów arkuszy kalkulacyjnych
`Formats.SpreadsheetFormats.FromExtension` konwertuje ciąg rozszerzenia pliku na odpowiadającą wartość wyliczenia formatu arkusza kalkulacyjnego.

```csharp
```csharp
Formats.SpreadsheetFormats expectedXlsm = Formats.SpreadsheetFormats.FromExtension(".xlsm");
Console.WriteLine("Parsed Spreadsheet format is {0}", expectedXlsm.Name);
```
```

**Wyjaśnienie:**  
1. **Parsowanie formatu:** `FromExtension` konwertuje rozszerzenie `.xlsm` na wewnętrzne wyliczenie `SpreadsheetFormat`.  
2. **Wyświetlenie formatu:** Nazwa sparsowanego formatu jest wypisywana, potwierdzając mapowanie.

### Parsowanie formatów tekstowych
Analogicznie, `Formats.TextualFormats.FromExtension` rozwiązuje rozszerzenia plików tekstowych, takich jak HTML czy TXT.

```csharp
```csharp
Formats.TextualFormats expectedHtml = Formats.TextualFormats.FromExtension("html");
Console.WriteLine("Parsed Textual format is {0}", expectedHtml.Name);
```
```

**Wyjaśnienie:**  
1. **Parsowanie formatu:** Metoda `FromExtension` rozwiązuje rozszerzenie `html` do `TextFormat`.  
2. **Wyświetlenie formatu:** Nazwa formatu tekstowego jest wyświetlana, przydatna dla edytorów internetowych.

## Jak edytować dokumenty po zidentyfikowaniu formatów?
Gdy znasz format, ładowanie i edytowanie dokumentu odbywa się według spójnego wzorca. Najpierw tworzysz instancję `Editor` z ścieżką do pliku źródłowego, następnie wywołujesz `Edit()`, aby uzyskać `EditableDocument`. Stamtąd możesz odczytać, zmodyfikować i ostatecznie zapisać zawartość przy użyciu odpowiednich `SaveOptions`.

### Ładowanie dokumentu
`Editor` jest klasą podstawową, która kapsułkuje wszystkie operacje edycji dla danego pliku.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/document.docx"))
{
    // Further steps will be covered here.
}
```
```

**Wyjaśnienie:**  
1. **Inicjalizacja edytora:** Utwórz instancję `Editor`, przekazując pełną ścieżkę do docelowego pliku.  
2. **Wzorzec zwalniania zasobów:** Instrukcja `using` zapewnia, że wszystkie niezarządzane zasoby zostaną szybko zwolnione.

### Pobieranie zawartości
`EditableDocument.GetContent()` zwraca surowy tekst dokumentu (lub HTML dla edytorów internetowych), który możesz wyświetlić lub zmodyfikować.

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    string content = editableDocument.GetContent();
    Console.WriteLine(content);
}
```
```

**Wyjaśnienie:**  
1. **Metoda Edit:** `Edit()` zwraca obiekt `EditableDocument`.  
2. **Pobranie zawartości:** `GetContent()` wyodrębnia surowy tekst dokumentu (lub HTML dla edytorów internetowych).  
3. **Wyświetlenie zawartości:** Zawartość jest wypisywana w konsoli w celu weryfikacji.

### Zapisywanie zmian
`SaveOptions` określa edytorowi, jak i w jakim formacie zapisać edytowany dokument z powrotem do pamięci.

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    // Modify content here
    SaveOptions saveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docx);
    editor.Save(editableDocument, "path/to/save/document.docx", saveOptions);
}
```
```

**Wyjaśnienie:**  
1. **Metoda Edit:** Ponownie uzyskaj `EditableDocument` po wprowadzeniu modyfikacji.  
2. **Modyfikacja zawartości:** Zastosuj zmiany w ciągu znaków (nie pokazano tutaj).  
3. **Opcje zapisu:** Skonfiguruj `SaveOptions` z żądanym formatem wyjściowym.  
4. **Zapis dokumentu:** Zapisz zmodyfikowany plik z powrotem na dysk.

## Jak pracować z różnymi typami dokumentów?
GroupDocs.Editor abstrahuje obsługę Word, Spreadsheet i Presentation za pomocą tego samego interfejsu API, co ułatwia przełączanie kontekstów bez konieczności nauki nowego zestawu klas dla każdej rodziny dokumentów.

### Edytowanie dokumentów arkuszy kalkulacyjnych
`SpreadsheetSaveOptions` definiuje sposób zapisu arkusza kalkulacyjnego, w tym format i opcjonalne ustawienia kompresji.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/spreadsheet.xlsx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // Modify content here
        SaveOptions saveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsx);
        editor.Save(editableDocument, "path/to/save/spreadsheet.xlsx", saveOptions);
    }
}
```
```

**Wyjaśnienie:**  
1. **Inicjalizacja edytora:** Przekaż ścieżkę do pliku arkusza kalkulacyjnego w konstruktorze `Editor`.  
2. **Metoda Edit:** Pobierz `EditableDocument`.  
3. **Pobranie zawartości:** Wypisz reprezentację CSV arkusza (lub HTML).  
4. **Modyfikacja zawartości:** Wprowadź potrzebne zmiany na poziomie komórek.  
5. **Opcje zapisu:** Wybierz odpowiednie `SpreadsheetSaveOptions`.  
6. **Zapis dokumentu:** Zapisz zaktualizowany arkusz z powrotem w pamięci.

### Edytowanie dokumentów prezentacji
`PresentationSaveOptions` kontroluje format wyjściowy dla prezentacji, umożliwiając zachowanie lub zmianę pierwotnego typu pliku.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/presentation.pptx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // Modify content here
        SaveOptions saveOptions = new PresentationSaveOptions(PresentationFormats.Pptx);
        editor.Save(editableDocument, "path/to/save/presentation.pptx", saveOptions);
    }
}
```
```

**Wyjaśnienie:**  
1. **Inicjalizacja edytora:** Załaduj plik PowerPoint przy użyciu `Editor`.  
2. **Metoda Edit:** Uzyskaj `EditableDocument`.  
3. **Pobranie zawartości:** Wyodrębnij HTML slajdów lub zwykły tekst.  
4. **Modyfikacja zawartości:** Zaktualizuj tytuły, wypunktowania lub obrazy.  
5. **Opcje zapisu:** Użyj `PresentationSaveOptions`, aby określić format wyjściowy.  
6. **Zapis dokumentu:** Zapisz zmodyfikowaną prezentację.

## Typowe problemy i rozwiązania
- **Błąd „Format nieobsługiwany”**: Upewnij się, że używasz najnowszej wersji GroupDocs.Editor; regularnie dodaje wsparcie dla nowszych formatów Office.  
- **Wysokie zużycie pamięci przy dużych plikach**: Włącz tryb strumieniowy, ustawiając `EditorSettings.EnableStreaming = true` przed załadowaniem dokumentu.  
- **Licencja nie została zastosowana**: Upewnij się, że plik tymczasowej licencji znajduje się w katalogu głównym aplikacji lub jest ładowany za pomocą `License license = new License(); license.SetLicense("path/to/license.lic");`.

## Najczęściej zadawane pytania

**Q: Jaka jest różnica między `DocumentFormatInfo` a `SaveOptions`?**  
A: `DocumentFormatInfo` dostarcza metadane o obsługiwanych typach plików, natomiast `SaveOptions` konfiguruje sposób zapisu dokumentu na dysk (format, kompresja itp.).

**Q: Czy mogę wyświetlić formaty dla własnego rozszerzenia pliku?**  
A: Tak — użyj `DocumentFormatInfo.FromExtension("yourExt")`; jeśli rozszerzenie nie jest rozpoznane, metoda zwraca `null`.

**Q: Czy GroupDocs.Editor obsługuje pliki zabezpieczone hasłem?**  
A: Zdecydowanie tak. Przekaż hasło do konstruktora `Editor` za pomocą `EditorSettings`, aby otworzyć zaszyfrowane dokumenty.

**Q: Ile formatów rzeczywiście obsługuje GroupDocs.Editor?**  
A: Ponad **30 formatów wejściowych i wyjściowych**, obejmujących Word, Excel, PowerPoint, HTML oraz zwykły tekst.

**Q: Czy istnieje sposób, aby ograniczyć listę tylko do formatów edytowalnych?**  
A: Użyj `GetEditableWordProcessingFormats()` (lub odpowiedników dla Spreadsheet/Presentation), aby pobrać formaty umożliwiające pełne możliwości edycji.

## Dodatkowe zasoby
- Pobierz bibliotekę ze [strony wydań GroupDocs](https://releases.groupdocs.com/editor/net/).  
- Uzyskaj [tymczasową licencję](https://purchase.groupdocs.com/temporary-license/) dla pełnego dostępu do funkcji.  
- Wypróbuj produkt z [bezpłatną wersją próbną](https://releases.groupdocs.com/).  
- Zapoznaj się ze szczegółowymi przykładami użycia w [dokumentacji GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/).  
- Uzyskaj pomoc od społeczności na [forum wsparcia](https://forum.groupdocs.com/c/editor/20).

## Podsumowanie
Stosując się do tego przewodnika, teraz wiesz, jak **wyświetlić obsługiwane formaty dokumentów**, **określić format pliku na podstawie jego rozszerzenia** oraz **edytować dokumenty** w typach Word, Spreadsheet i Presentation przy użyciu GroupDocs.Editor dla .NET. Włącz te fragmenty kodu do własnych projektów, aby budować solidne aplikacje świadome formatów, które zachwycą użytkowników końcowych i zredukują błędy w czasie wykonywania.

---

**Ostatnia aktualizacja:** 2026-06-06  
**Testowano z:** GroupDocs.Editor 23.9 for .NET  
**Autor:** GroupDocs

## Powiązane samouczki

- [Opanowanie ładowania dokumentów w .NET z GroupDocs.Editor: Kompletny przewodnik](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)
- [Mistrzowska edycja dokumentów w .NET z GroupDocs.Editor: Kompletny przewodnik](/editor/net/document-editing/master-document-editing-dotnet-groupdocs-editor/)
- [Konwersja Word do HTML przy użyciu GroupDocs.Editor .NET: Przewodnik krok po kroku](/editor/net/document-saving/convert-word-to-html-groupdocs-editor-dotnet/)