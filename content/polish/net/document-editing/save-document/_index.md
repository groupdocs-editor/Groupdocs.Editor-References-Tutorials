---
title: Zapisz dokument
linktitle: Zapisz dokument
second_title: Edytor GroupDocs.NET API
description: Bez wysiłku edytuj i zapisuj dokumenty za pomocą GroupDocs.Editor dla .NET. Ten przewodnik krok po kroku upraszcza proces dla programistów.
weight: 14
url: /pl/net/document-editing/save-document/
---
## Wstęp
Czy chcesz bez wysiłku edytować i zapisywać dokumenty za pomocą GroupDocs.Editor dla .NET? Jesteś we właściwym miejscu! Ten samouczek przeprowadzi Cię przez proces krok po kroku, zapewniając łatwe zarządzanie dokumentami. Niezależnie od tego, czy jesteś doświadczonym programistą, czy początkującym, nasz przewodnik zapewni Ci wszystkie informacje potrzebne do rozpoczęcia.
## Warunki wstępne
Zanim przejdziesz do samouczka, upewnij się, że spełniasz następujące wymagania wstępne:
- Środowisko programistyczne: Visual Studio zainstalowane na Twoim komputerze.
- .NET Framework: Upewnij się, że masz .NET Framework 4.6.1 lub nowszą wersję.
-  GroupDocs.Editor dla .NET: Pobierz najnowszą wersję[Tutaj](https://releases.groupdocs.com/editor/net/).
- Podstawowa znajomość języka C#: Znajomość programowania w języku C# jest niezbędna.
## Importuj przestrzenie nazw
Aby używać GroupDocs.Editor w projekcie .NET, musisz zaimportować niezbędne przestrzenie nazw. Oto jak to zrobić:
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
Teraz, gdy mamy już skonfigurowane środowisko i zaimportowane niezbędne przestrzenie nazw, przejdźmy do kroków wymaganych do załadowania, edytowania i zapisania dokumentu przy użyciu GroupDocs.Editor dla .NET.
## Krok 1: Załaduj dokument
Najpierw musimy załadować dokument, który chcemy edytować. Dzięki GroupDocs.Editor ten proces jest prosty. Oto jak możesz to zrobić:

```csharp
string inputFilePath = "Your Sample Document";
Editor editor = new Editor(inputFilePath, delegate { return new Options.WordProcessingLoadOptions(); });
EditableDocument defaultWordProcessingDoc = editor.Edit();
```
 W tym kroku określamy ścieżkę do dokumentu, który chcemy edytować i tworzymy instancję pliku`Editor` klasa. The`Edit` Następnie wywoływana jest metoda w celu załadowania dokumentu do pliku`EditableDocument` obiekt.
## Krok 2: Zmodyfikuj dokument
Po załadowaniu dokumentu czas na wprowadzenie pewnych modyfikacji. Ponieważ nie mamy dołączonego edytora WYSIWYG, zasymulujemy proces edycji w kodzie.

```csharp
string allEmbeddedInsideString = defaultWordProcessingDoc.GetEmbeddedHtml();
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
EditableDocument editedDoc = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```
 Tutaj pobieramy osadzoną treść HTML dokumentu, dokonujemy prostej zamiany tekstu i tworzymy nowy`EditableDocument`instancję ze zmodyfikowanego kodu HTML.
## Krok 3: Zapisz dokument
Ostatnim krokiem po edycji dokumentu jest jego zapisanie. GroupDocs.Editor udostępnia wiele opcji zapisywania dokumentu w różnych formatach.
## Zapisz jako RTF
```csharp
string outputRtfPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.rtf");
WordProcessingSaveOptions rtfSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
editor.Save(editedDoc, outputRtfPath, rtfSaveOptions);
```
## Zapisz jako DOCM
```csharp
string outputDocmPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.docm");
WordProcessingSaveOptions docmSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm);
using (FileStream outputStream = File.Create(outputDocmPath))
{
    editor.Save(editedDoc, outputStream, docmSaveOptions);
}
```
## Zapisz jako zwykły tekst
```csharp
string outputTxtPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.txt");
TextSaveOptions textSaveOptions = new TextSaveOptions
{
    Encoding = System.Text.Encoding.UTF8,
    PreserveTableLayout = true
};
editor.Save(editedDoc, outputTxtPath, textSaveOptions);
```
## Krok 4: Oczyszczanie
 Na koniec ważne jest, aby pozbyć się`EditableDocument` I`Editor` instancje, aby zwolnić zasoby.
```csharp
editedDoc.Dispose();
defaultWordProcessingDoc.Dispose();
editor.Dispose();
```
Wykonując poniższe kroki, możesz efektywnie ładować, edytować i zapisywać dokumenty przy użyciu GroupDocs.Editor dla .NET. To potężne narzędzie zapewnia elastyczność i łatwość obsługi, dzięki czemu zarządzanie dokumentami jest proste.
## Wniosek
Programowe edytowanie i zapisywanie dokumentów nigdy nie było łatwiejsze dzięki GroupDocs.Editor dla .NET. Ten przewodnik przeprowadził Cię przez cały proces, od załadowania dokumentu po zapisanie go w różnych formatach. Dzięki GroupDocs.Editor masz wszechstronne i niezawodne rozwiązanie na wyciągnięcie ręki, upraszczające proces edycji dokumentów.
## Często zadawane pytania
### Jakie formaty plików obsługuje GroupDocs.Editor?
GroupDocs.Editor obsługuje różne formaty plików, w tym DOCX, RTF, TXT i wiele innych. Aby zobaczyć pełną listę, sprawdź[dokumentacja](https://tutorials.groupdocs.com/editor/net/).
### Czy mogę wypróbować GroupDocs.Editor przed zakupem?
 Tak, możesz dostać[bezpłatna wersja próbna](https://releases.groupdocs.com/) aby przetestować funkcje GroupDocs.Editor.
### Czy mogę liczyć na wsparcie, jeśli napotkam problemy?
 Absolutnie! Możesz odwiedzić[forum wsparcia](https://forum.groupdocs.com/c/editor/20) o pomoc w rozwiązaniu wszelkich napotkanych problemów.
### Jak uzyskać licencję tymczasową?
 Możesz poprosić o[licencja tymczasowa](https://purchase.groupdocs.com/temporary-license/) w celach ewaluacyjnych.
### Gdzie mogę kupić pełną wersję GroupDocs.Editor?
 Można kupić pełną wersję[Tutaj](https://purchase.groupdocs.com/buy).