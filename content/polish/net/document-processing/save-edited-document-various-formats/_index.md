---
title: Zapisz edytowany dokument w różnych formatach
linktitle: Zapisz edytowany dokument w różnych formatach
second_title: Edytor GroupDocs.NET API
description: Z tego obszernego przewodnika krok po kroku dowiesz się, jak zapisywać edytowane dokumenty w różnych formatach przy użyciu programu GroupDocs.Editor dla platformy .NET.
weight: 11
url: /pl/net/document-processing/save-edited-document-various-formats/
---
## Wstęp
Czy chcesz zapisywać edytowane dokumenty w różnych formatach za pomocą GroupDocs.Editor dla .NET? Trafiłeś we właściwe miejsce! Ten obszerny przewodnik przeprowadzi Cię przez cały proces, od konfiguracji środowiska po zapisanie edytowanego dokumentu w wielu formatach. Zanurzmy się i sprawmy, że edytowanie i zapisywanie dokumentów będzie proste!
## Warunki wstępne
Zanim zaczniemy, upewnij się, że masz następujące elementy:
1.  GroupDocs.Editor dla .NET — pobierz najnowszą wersję z[Tutaj](https://releases.groupdocs.com/editor/net/).
2. Środowisko programistyczne - Visual Studio lub dowolne inne IDE kompatybilne z .NET.
3. .NET Framework — upewnij się, że masz zainstalowany program .NET Framework 4.6.1 lub nowszy.
4. Przykładowy dokument — przykładowy dokument WordProcessing, z którym można pracować.
5. Podstawowa znajomość języka C# – wymagana jest znajomość programowania w języku C#.
## Importuj przestrzenie nazw
Na początek upewnij się, że zaimportowałeś niezbędne przestrzenie nazw do projektu C#. Ma to kluczowe znaczenie dla uzyskania dostępu do funkcjonalności GroupDocs.Editor.
```csharp
using System;
using GroupDocs.Editor.Metadata;
```
Podzielmy proces na łatwe do wykonania etapy. Postępuj zgodnie ze wskazówkami, aby upewnić się, że rozumiesz każdą część.
## Krok 1: Uzyskaj ścieżkę do pliku wejściowego
Najpierw musisz określić ścieżkę do wejściowego pliku WordProcessing. Ten plik zostanie załadowany i edytowany.
```csharp
string inputFilePath = "Your Sample Document";
```
## Krok 2: Utwórz opcje ładowania dokumentu
Następnie utwórz opcje ładowania specyficzne dla dokumentów WordProcessing. Opcje te pomogą dostosować sposób ładowania dokumentu.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
```
## Krok 3: Załaduj dokument z opcjami
 Teraz załaduj dokument do pliku`Editor` instancję przy użyciu określonych opcji ładowania.
```csharp
using (Editor editor = new Editor(inputFilePath, delegate { return loadOptions; }))
```
## Krok 4: Utwórz opcje edycji
Przygotuj opcje edycji dokumentu. Opcje te określają sposób otwierania dokumentu do edycji.
```csharp
WordProcessingEditOptions editOptions = new WordProcessingEditOptions();
```
## Krok 5: Otwórz dokument do edycji
 Otwórz dokument do edycji, tworząc plik`EditableDocument`instancja. Ta instancja umożliwi Ci dokonanie zmian w dokumencie.
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
```
## Krok 6: Edytuj zawartość dokumentu
Teraz czas na edycję treści dokumentu. Najpierw pobierz dokument jako pojedynczy ciąg znaków zakodowany w formacie base64.
```csharp
string allEmbeddedInsideString = beforeEdit.GetEmbeddedHtml();
```
Na przykład zmodyfikujmy podtytuł w dokumencie.
```csharp
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
```
## Krok 7: Utwórz nowy edytowalny dokument na podstawie edytowanej treści
 Stwórz nowy`EditableDocument` instancję z edytowanej treści i zasobów.
```csharp
using (EditableDocument afterEdit = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null))
```
## Krok 8: Zapisz dokument w różnych formatach
Na koniec wykonaj iterację po wszystkich obsługiwanych formatach WordProcessing i zapisz edytowany dokument w każdym formacie.
```csharp
foreach (WordProcessingFormats oneFormat in WordProcessingFormats.All)
{
    // Przygotuj opcje zapisu
    WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(oneFormat);
    // Przygotuj ścieżkę zapisu
    string savePath = Path.Combine("OutputDirectory", "MultipleOutFormats." + saveOptions.OutputFormat.Extension);
    // Zapisz dokument
    editor.Save(afterEdit, savePath, saveOptions);
}
```
## Wiadomość o zakończeniu
Na zakończenie możesz wydrukować komunikat informujący o pomyślnym zakończeniu procesu.
```csharp
Console.WriteLine("SavingEditedDocumentToAllFormats routine has successfully finished");
```
## Wniosek
Gratulacje! Pomyślnie nauczyłeś się zapisywać edytowane dokumenty w różnych formatach przy użyciu GroupDocs.Editor dla .NET. To potężne narzędzie ułatwia manipulowanie dokumentami i zapisywanie ich w wielu formatach za pomocą zaledwie kilku linijek kodu. Pamiętaj, że kluczowe kroki obejmują załadowanie dokumentu, edycję treści i zapisanie go w żądanych formatach.
## Często zadawane pytania
### Co to jest GroupDocs.Editor dla .NET?
GroupDocs.Editor dla .NET to potężne API, które umożliwia edycję dokumentów w różnych formatach przy użyciu aplikacji .NET.
### Czy mogę korzystać z GroupDocs.Editor za darmo?
 Tak, możesz z niego korzystać w ramach bezpłatnego okresu próbnego. Pobierz to[Tutaj](https://releases.groupdocs.com/).
### Jakie formaty są obsługiwane przez GroupDocs.Editor?
GroupDocs.Editor obsługuje szeroką gamę formatów, w tym DOCX, PDF, HTML i wiele innych.
### Jak uzyskać tymczasową licencję na GroupDocs.Editor?
 Możesz uzyskać licencję tymczasową[Tutaj](https://purchase.groupdocs.com/temporary-license/).
### Gdzie mogę znaleźć więcej dokumentacji i wsparcia?
 Dostępna jest szczegółowa dokumentacja[Tutaj](https://tutorials.groupdocs.com/editor/net/) i możesz uzyskać wsparcie[Tutaj](https://forum.groupdocs.com/c/editor/20).