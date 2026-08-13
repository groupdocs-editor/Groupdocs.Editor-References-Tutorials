---
date: 2026-06-01
description: Dowiedz się, jak uzyskać liczbę stron i wyodrębnić metadane dokumentu
  przy użyciu GroupDocs.Editor dla .NET w szczegółowym samouczku krok po kroku.
keywords:
- get page count
- extract document metadata
- get document info
- find document extension
- retrieve document size
linktitle: Uzyskaj liczbę stron i wyodrębnij informacje o dokumencie
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
title: Uzyskaj liczbę stron i wyodrębnij informacje o dokumencie za pomocą GroupDocs.Editor
type: docs
url: /pl/net/document-processing/extract-document-info/
weight: 10
---

# Uzyskaj liczbę stron i wyodrębnij informacje o dokumencie za pomocą GroupDocs.Editor

## Wprowadzenie
W tym kompleksowym samouczku dowiesz się, jak **get page count** oraz wyodrębnić szczegółowe informacje o dokumencie — w tym format, rozmiar i status szyfrowania — przy użyciu GroupDocs.Editor dla .NET. Niezależnie od tego, czy tworzysz system zarządzania dokumentami, silnik raportowania czy zautomatyzowany potok konwersji, zrozumienie metadanych pliku jest pierwszym krokiem do niezawodnego przetwarzania. Przejdźmy przez cały przepływ pracy, od załadowania pliku po bezpieczne zwolnienie zasobów.

## Szybkie odpowiedzi
- **Jak mogę pobrać liczbę stron dokumentu?**  
  Wywołaj `editor.GetDocumentInfo().PageCount` po załadowaniu pliku przy użyciu `Editor`.
- **Jakie formaty plików są obsługiwane przy wyodrębnianiu metadanych?**  
  Ponad 50 formatów, w tym DOCX, XLSX, PPTX, PDF, TXT i HTML.
- **Czy mogę wyodrębnić metadane z plików chronionych hasłem?**  
  Tak — podaj hasło podczas tworzenia instancji `Editor`.
- **Czy muszę ręcznie zwalniać zasoby?**  
  Zdecydowanie; zawsze wywołuj `editor.Dispose()` lub otaczaj edytor blokiem `using`.
- **Jakiej wersji GroupDocs.Editor potrzebuję?**  
  Najnowsze stabilne wydanie (v23.12+ w momencie pisania) obsługuje wszystkie przedstawione funkcje.

## Co to jest „get page count” w GroupDocs.Editor?
`GetDocumentInfo()` jest metodą zwracającą obiekt `DocumentInfo` zawierający liczbę stron dokumentu, format, rozmiar i inne metadane. To pojedyncze wywołanie zapewnia natychmiastowy wgląd bez ręcznego parsowania pliku. Korzystając z tej metody, unikasz ładowania całego dokumentu do pamięci, co poprawia wydajność, szczególnie przy dużych plikach, i zmniejsza zużycie zasobów serwera.

## Dlaczego wyodrębniać metadane dokumentu za pomocą GroupDocs.Editor?
GroupDocs.Editor może przetwarzać **ponad 50 formatów wejściowych i wyjściowych** oraz pobierać metadane plików do **2 GB** bez ładowania całego dokumentu do pamięci. Ta wydajność zmniejsza obciążenie serwera nawet o **70 %** w porównaniu z pełnym parsowaniem dokumentu, co czyni go idealnym dla aplikacji o wysokiej przepustowości.

## Wymagania wstępne
- **Podstawy programowania w C#** – powinieneś być zaznajomiony z Visual Studio i strukturami projektów .NET.
- **Visual Studio 2022** (lub dowolna nowsza wersja) zainstalowane na twoim komputerze.
- **GroupDocs.Editor for .NET** – pobierz najnowszy pakiet ze [strony pobierania](https://releases.groupdocs.com/editor/net/).

## Jak załadować dokument?
`Editor` jest główną klasą reprezentującą dokument i udostępnia metodę ładowania oraz manipulacji nim. Załaduj docelowy plik, tworząc instancję `Editor` i przekazując ścieżkę do pliku. Edytor automatycznie wykrywa format, więc nie musisz podawać opcji ładowania. To podejście działa dla każdego obsługiwanego typu pliku i upraszcza początkową konfigurację.

```csharp
using System;
using GroupDocs.Editor.Metadata;
```

## Jak pobrać informacje o dokumencie?
`GetDocumentInfo()` zwraca obiekt `DocumentInfo` zawierający metadane takie jak liczba stron, format, rozmiar i status szyfrowania. Po załadowaniu wywołaj tę metodę, aby uzyskać obiekt. Zwrócony `DocumentInfo` dostarcza zwięzły podgląd cech pliku, umożliwiając podejmowanie decyzji bez dalszego przetwarzania.

```csharp
string docxInputFilePath = "YourSampleDocument.docx";
Editor editorDocx = new Editor(docxInputFilePath);
```

## Jak określić typ dokumentu?
`DocumentType` jest wyliczeniem wskazującym, czy dokument jest WordProcessing, Spreadsheet czy Text. Wiedza, czy plik jest dokumentem przetwarzania tekstu, arkuszem kalkulacyjnym czy zwykłym tekstem, wpływa na późniejsze przetwarzanie. Użyj właściwości `DocumentType` obiektu `DocumentInfo`, aby podjąć tę decyzję i odpowiednio rozgałęzić logikę.

```csharp
IDocumentInfo infoDocx = editorDocx.GetDocumentInfo(null);
```

## Jak wyodrębnić szczegółowe informacje dla plików przetwarzania tekstu?
`WordProcessing` odnosi się do dokumentów takich jak DOCX, ODT i RTF obsługiwanych jako pliki przetwarzania tekstu. Jeśli typ dokumentu to `WordProcessing`, możesz odczytać dodatkowe właściwości, takie jak **format**, **extension**, **page count**, **size** i **encryption flag** bezpośrednio z obiektu `DocumentInfo`. Szczegóły te pomagają dostosować kroki przetwarzania, np. stosując konkretne konwersje lub kontrole bezpieczeństwa.

```csharp
bool isSpreadsheet = infoDocx is SpreadsheetDocumentInfo;
bool isText = infoDocx is TextualDocumentInfo;
bool isWordProcessing = infoDocx is WordProcessingDocumentInfo;
Console.WriteLine($"Is '{docxInputFilePath}' a Spreadsheet: {isSpreadsheet}");
Console.WriteLine($"Is '{docxInputFilePath}' a Textual document: {isText}");
Console.WriteLine($"Is '{docxInputFilePath}' a WordProcessing document: {isWordProcessing}");
```

## Jak obsługiwać arkusze kalkulacyjne i dokumenty tekstowe?
`Spreadsheet` oznacza pliki arkuszy kalkulacyjnych, takie jak XLSX, natomiast `Text` reprezentuje dokumenty zwykłego tekstu. Dla arkuszy (`Spreadsheet`) i plików tekstowych (`Text`) obiekt `DocumentInfo` nadal dostarcza podstawowe metadane (extension, size, page count). Niektóre formaty mogą nie udostępniać liczby stron, w takim przypadku wartość będzie `0`. Nadal możesz polegać na innych metadanych w dalszej logice.

```csharp
if (isWordProcessing)
{
    WordProcessingDocumentInfo casted = (WordProcessingDocumentInfo)infoDocx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Page count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```

## Jak pracować z dokumentami chronionymi hasłem?
`Password` jest ciągiem znaków przekazywanym do konstruktora `Editor` w celu otwarcia zaszyfrowanych plików. Gdy dokument jest zaszyfrowany, najpierw spróbuj otworzyć go bez hasła. Jeśli to się nie powiedzie, przechwyć wyjątek i spróbuj ponownie z właściwym hasłem. Konstruktor `Editor` przyjmuje parametr `Password` w tym celu, umożliwiając płynne obsługiwanie chronionych plików.

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

## Jak przetwarzać dokumenty tekstowe?
`DocumentInfo` dostarcza podstawowe metadane, takie jak rozmiar, rozszerzenie i kodowanie dla plików tekstowych. Pliki tekstowe (np. `.txt`, `.md`) są traktowane jako proste strumienie. Nadal możesz pobrać informacje o rozmiarze i kodowaniu z `DocumentInfo`, co jest przydatne przy weryfikacji integralności pliku lub określaniu odpowiednich potoków przetwarzania.

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

## Jak prawidłowo zwolnić zasoby?
`Editor` jest główną klasą, która posiada niezarządzane zasoby i musi być zwolniona po użyciu. Aby uniknąć wycieków pamięci, zawsze zwalniaj instancję `Editor` po zakończeniu wyodrębniania informacji. Instrukcja `using` jest najbezpieczniejszym wzorcem, ponieważ zapewnia zwolnienie zasobów nawet w przypadku wystąpienia wyjątku, zapewniając czyste zarządzanie zasobami.

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

## Typowe problemy i rozwiązania
| Problem | Przyczyna | Rozwiązanie |
|-------|-------|----------|
| **PageCount returns 0** | Format nie obsługuje paginacji (np. zwykły tekst) | Sprawdź `DocumentInfo.DocumentType` przed poleganiem na `PageCount`. |
| **Unsupported file format** | Rozszerzenie pliku nie zostało rozpoznane | Zweryfikuj, że plik jest jednym z ponad 50 obsługiwanych formatów; zaktualizuj GroupDocs.Editor do najnowszej wersji. |
| **Password exception** | Podano nieprawidłowe hasło | Przechwyć `PasswordProtectedException` i poproś użytkownika o ponowne wprowadzenie hasła. |
| **Memory spike on large files** | Ładowanie bardzo dużych plików PDF bez strumieniowania | Użyj `LoadOptions` z `LoadOptions.LoadMode = LoadMode.Stream` (dostępne w nowszych wersjach). |

## Często zadawane pytania

**Q: Jakie typy dokumentów mogę wyodrębnić metadane?**  
A: GroupDocs.Editor obsługuje dokumenty przetwarzania tekstu, arkusze kalkulacyjne, prezentacje, PDF oraz pliki zwykłego tekstu — ponad 50 formatów w sumie.

**Q: Jak pobrać rozszerzenie pliku?**  
A: Uzyskaj `DocumentInfo.Extension` po wywołaniu `GetDocumentInfo()`; zwraca rozszerzenie bez wiodącej kropki.

**Q: Czy mogę uzyskać rozmiar dokumentu w megabajtach?**  
A: Tak — `DocumentInfo.Size` zwraca rozmiar w bajtach; podziel przez 1 048 576, aby przeliczyć na megabajty.

**Q: Czy bezpieczne jest przetwarzanie plików chronionych hasłem na serwerze?**  
A: Zdecydowanie — GroupDocs.Editor nigdy nie zapisuje hasła na dysku i zwalnia wszystkie obiekty kryptograficzne po użyciu.

**Q: Gdzie mogę znaleźć dodatkową pomoc, jeśli napotkam problemy?**  
A: Możesz uzyskać wsparcie na [forum wsparcia GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).

---

**Ostatnia aktualizacja:** 2026-06-01  
**Testowano z:** GroupDocs.Editor 23.12 for .NET  
**Autor:** GroupDocs

```csharp
editorDocx.Dispose();
editorXlsx.Dispose();
editorXls.Dispose();
editorXml.Dispose();
Console.WriteLine("ExtractingDocumentInfo routine has successfully finished");
```

## Powiązane samouczki

- [Mistrzowskie wyodrębnianie metadanych w .NET z GroupDocs.Editor: Kompletny przewodnik](/editor/net/advanced-features/groupdocs-editor-net-metadata-extraction-guide/)
- [Samouczki ładowania dokumentów z GroupDocs.Editor dla .NET](/editor/net/document-loading/)
- [Efektywna edycja dokumentów z GroupDocs.Editor .NET: Transformacja HTML do edytowalnych dokumentów](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)