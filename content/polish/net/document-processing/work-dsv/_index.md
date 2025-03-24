---
title: Praca z wartościami rozdzielonymi rozdzielanymi (DSV)
linktitle: Praca z wartościami rozdzielonymi rozdzielanymi (DSV)
second_title: Edytor GroupDocs.NET API
description: Z tego przewodnika krok po kroku dowiesz się, jak edytować pliki CSV i TSV przy użyciu programu GroupDocs.Editor dla platformy .NET. Ulepszaj swoje projekty .NET bez wysiłku.
weight: 12
url: /pl/net/document-processing/work-dsv/
---
## Wstęp
Jeśli jesteś programistą pracującym z wartościami rozdzielanymi (DSV), takimi jak pliki CSV lub TSV, wiesz, że programowa edycja tych plików może być trudnym zadaniem. Jednak dzięki GroupDocs.Editor dla .NET zadanie to staje się znacznie prostsze i wydajniejsze. W tym samouczku przeprowadzimy Cię przez proces używania programu GroupDocs.Editor dla platformy .NET do odczytywania, edytowania i zapisywania plików DSV. Podzielimy proces na łatwe do wykonania kroki, dzięki czemu możesz łatwo wdrożyć go w swoich projektach.
## Warunki wstępne
Zanim przejdziemy do samouczka, upewnij się, że spełniasz następujące wymagania wstępne:
- Visual Studio: Upewnij się, że na komputerze jest zainstalowany program Visual Studio.
-  GroupDocs.Editor dla .NET: Należy pobrać bibliotekę GroupDocs.Editor dla .NET i skorzystać z niej. Możesz go pobrać[Tutaj](https://releases.groupdocs.com/editor/net/).
- Podstawowa znajomość języka C#: W tym samouczku założono, że masz podstawową wiedzę na temat programowania w językach C# i .NET.
## Importuj przestrzenie nazw
Najpierw musisz zaimportować niezbędne przestrzenie nazw do swojego projektu. Te przestrzenie nazw udostępniają klasy i metody wymagane do pracy z programem GroupDocs.Editor dla platformy .NET.
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

## Krok 1: Uzyskaj ścieżkę do wejściowego pliku DSV
Najpierw musisz określić ścieżkę do wejściowego pliku DSV. W tym przykładzie założymy, że jest to plik CSV.
```csharp
string inputFilePath = "Your Sample Document";
```
## Krok 2: Utwórz instancję edytora
 Utwórz instancję`Editor` klasa. Ta instancja będzie używana do ładowania pliku DSV i manipulowania nim.
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## Krok 3: Utwórz opcje edycji DSV
 Następnie utwórz instancję`DelimitedTextEditOptions` i określ ogranicznik dla pliku DSV. Tutaj używamy przecinka jako separatora.
```csharp
    Options.DelimitedTextEditOptions editOptions = new DelimitedTextEditOptions(",");
    editOptions.ConvertDateTimeData = false;
    editOptions.ConvertNumericData = true;
    editOptions.TreatConsecutiveDelimitersAsOne = true;
```
## Krok 4: Utwórz instancję EditableDocument
 Stworzyć`EditableDocument` przykład za pomocą`Editor.Edit` metoda. Spowoduje to przygotowanie dokumentu do edycji.
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## Krok 5: Edytuj zawartość dokumentu
Pobierz oryginalną treść tekstową i wprowadź niezbędne modyfikacje. Dla celów demonstracyjnych zamieńmy jakiś tekst.
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("SsangYong", "Chevrolet").Replace("Kyron", "Camaro");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## Krok 6: Utwórz dokument edytowalny ze zaktualizowaną zawartością
 Stwórz nowy`EditableDocument` z zaktualizowaną zawartością.
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## Krok 7: Utwórz opcje zapisu CSV
Określ opcje zapisywania formatu CSV, w tym ogranicznik i kodowanie.
```csharp
    Options.DelimitedTextSaveOptions csvSaveOptions = new DelimitedTextSaveOptions(",");
    csvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## Krok 8: Utwórz opcje zapisu TSV
Podobnie określ opcje zapisu dla formatu TSV.
```csharp
    Options.DelimitedTextSaveOptions tsvSaveOptions = new DelimitedTextSaveOptions("\t");
    tsvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## Krok 9: Utwórz opcje zapisywania arkusza kalkulacyjnego
Jeśli chcesz zapisać dokument jako arkusz kalkulacyjny, utwórz odpowiednie opcje zapisywania.
```csharp
    Options.SpreadsheetSaveOptions cellsSaveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
```
## Krok 10: Przygotuj ścieżki zapisu
Określ ścieżki, w których będą zapisywane edytowane pliki.
```csharp
    string outputCsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".csv");
    string outputTsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".tsv");
    string outputCellsPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".xlsm");
```
## Krok 11: Zapisz edytowany dokument
Zapisz edytowany dokument w określonych ścieżkach w różnych formatach.
```csharp
    editor.Save(afterEdit, outputCsvPath, csvSaveOptions);
    editor.Save(afterEdit, outputTsvPath, tsvSaveOptions);
    editor.Save(afterEdit, outputCellsPath, cellsSaveOptions);
```
## Krok 12: Usuń instancje edytowalnego dokumentu
 Na koniec pamiętaj o pozbyciu się`EditableDocument` instancje, aby zwolnić zasoby.
```csharp
    beforeEdit.Dispose();
    afterEdit.Dispose();
}
System.Console.WriteLine("WorkingWithDsv routine has successfully finished");
```
## Wniosek
Edycja plików DSV przy użyciu programu GroupDocs.Editor dla .NET to prosty proces obejmujący utworzenie instancji edytora, ustawienie opcji edycji, modyfikację zawartości i zapisanie zmian. Ten przewodnik krok po kroku powinien pomóc w łatwej integracji tej funkcji z aplikacjami .NET. Niezależnie od tego, czy pracujesz z plikami CSV, TSV czy innymi formatami DSV, GroupDocs.Editor dla .NET zapewnia solidne i elastyczne rozwiązanie.
## Często zadawane pytania
### Czy mogę używać GroupDocs.Editor dla .NET do edycji dużych plików CSV?
Tak, GroupDocs.Editor dla .NET jest w stanie efektywnie obsługiwać duże pliki CSV.
### Czy GroupDocs.Editor dla .NET obsługuje inne formaty DSV oprócz CSV i TSV?
Tak, obsługuje różne formaty DSV, o ile określisz odpowiedni ogranicznik.
### Czy można dostosować kodowanie podczas zapisywania plików DSV?
Oczywiście możesz określić żądane kodowanie w opcjach zapisu.
### Czy mogę przekonwertować plik CSV na arkusz kalkulacyjny Excel za pomocą GroupDocs.Editor dla .NET?
Tak, możesz zapisać plik CSV jako arkusz kalkulacyjny Excel, korzystając z odpowiednich opcji zapisywania.
### Gdzie mogę znaleźć więcej dokumentacji dotyczącej GroupDocs.Editor dla .NET?
 Można znaleźć szczegółową dokumentację[Tutaj](https://tutorials.groupdocs.com/editor/net/)