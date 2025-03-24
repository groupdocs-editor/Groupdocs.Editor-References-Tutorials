---
title: Utwórz dokument
linktitle: Utwórz dokument
second_title: Edytor GroupDocs.NET API
description: Dowiedz się, jak edytować dokumenty Word, Excel, PowerPoint, Ebook i e-mail za pomocą GroupDocs.Editor dla .NET, dzięki temu kompleksowemu samouczkowi krok po kroku.
weight: 10
url: /pl/net/document-editing/create-document/
---
## Wstęp
Czy jesteś zmęczony problemami związanymi z programową edycją różnych typów dokumentów? GroupDocs.Editor dla .NET jest tutaj, aby uprościć ten proces. To potężne narzędzie umożliwia programistom łatwą edycję różnych formatów dokumentów, takich jak Word, Excel, PowerPoint, e-booki i e-maile. W tym samouczku szczegółowo omówimy sposób używania programu GroupDocs.Editor dla platformy .NET do tworzenia i edytowania dokumentów. Podzielimy ten proces na łatwe do wykonania kroki, dzięki czemu będzie dostępny nawet dla nowicjuszy.
## Warunki wstępne
Zanim zaczniemy, upewnij się, że masz następujące elementy:
- Program Visual Studio zainstalowany na Twoim komputerze.
- .NET Framework (4.0 lub nowszy).
-  GroupDocs.Editor dla biblioteki .NET. Można go pobrać z[Tutaj](https://releases.groupdocs.com/editor/net/).
- Podstawowa znajomość programowania w języku C#.
## Importuj przestrzenie nazw
Najpierw zaimportujmy niezbędne przestrzenie nazw. Dzięki temu wymagane klasy i metody będą dostępne w naszej aplikacji.
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using System.IO;
```
## Krok 1: Konfiguracja strumienia
Na początek musimy skonfigurować strumień pamięci, który będzie pełnił funkcję obiektu zastępczego dla zawartości dokumentu.
```csharp
Stream memoryStream = Stream.Null;
```
## Krok 2: Funkcja wywołania zwrotnego w celu zapisania dokumentu
Następnie zdefiniuj funkcję wywołania zwrotnego, która zapisze nowy strumień dokumentów. Funkcja ta jest niezbędna do obsługi wyników procesu edycji dokumentu.
```csharp
void SaveNewDocument(Stream resultStream)
{
    memoryStream = resultStream;
}
```
## Krok 3: Tworzenie i edytowanie dokumentu WordProcessing
 Teraz utwórzmy i edytujmy dokument programu Word. Zaczniemy od utworzenia nowego`Editor` instancję dla dokumentów WordProcessing i edytuj ją przy użyciu opcji domyślnych.
### Twórz i edytuj za pomocą opcji domyślnych
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    EditableDocument defaultWordProcessingDoc = editor.Edit();
}
```
### Twórz i edytuj za pomocą opcji niestandardowych
Aby uzyskać większą kontrolę, możemy określić opcje, takie jak wyłączenie paginacji i wyodrębnianie osadzonych czcionek.
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    WordProcessingEditOptions wordProcessingEditOptions = new WordProcessingEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true,
        FontExtraction = FontExtractionOptions.ExtractAllEmbedded
    };
    EditableDocument editableWordProcessingDocument = editor.Edit(wordProcessingEditOptions);
}
```
## Krok 4: Tworzenie i edytowanie dokumentu arkusza kalkulacyjnego
Podobnie możemy tworzyć i edytować dokument Excel. Oto jak to zrobić.
### Twórz i edytuj za pomocą opcji domyślnych
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    EditableDocument defaultEditableSpreadsheetDocument = editor.Edit();
}
```
### Twórz i edytuj za pomocą opcji niestandardowych
 Aby kierować reklamy na określone arkusze lub wykluczać ukryte, używamy`SpreadsheetEditOptions`.
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    SpreadsheetEditOptions spreadsheetEditOptions = new SpreadsheetEditOptions
    {
        WorksheetIndex = 0,
        ExcludeHiddenWorksheets = true
    };
    EditableDocument editableSpreadsheetDocument = editor.Edit(spreadsheetEditOptions);
}
```
## Krok 5: Tworzenie i edytowanie dokumentu prezentacji
Obsługiwane są także prezentacje programu PowerPoint. Zobaczmy, jak sobie z nimi poradzić.
### Twórz i edytuj za pomocą opcji domyślnych
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    EditableDocument defaultEditablePresentationDocument = editor.Edit();
}
```
### Twórz i edytuj za pomocą opcji niestandardowych
Możesz dostosować swoje zmiany, określając opcje, takie jak slajd do wyświetlenia i czy uwzględnić slajdy ukryte.
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    PresentationEditOptions presentationEditOptions = new PresentationEditOptions
    {
        ShowHiddenSlides = false,
        SlideNumber = 0
    };
    EditableDocument editablePresentationDocument = editor.Edit(presentationEditOptions);
}
```
## Krok 6: Tworzenie i edytowanie dokumentu e-booka
GroupDocs.Editor umożliwia także edycję formatów e-booków, takich jak EPUB. Oto jak możesz sobie z tym poradzić.
### Twórz i edytuj za pomocą opcji domyślnych
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EditableDocument defaultEditableEbookDocument = editor.Edit();
}
```
### Twórz i edytuj za pomocą opcji niestandardowych
Dostosuj edycję swojego e-booka, włączając lub wyłączając informacje o paginacji i języku.
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EbookEditOptions ebookEditOptions = new EbookEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true
    };
    EditableDocument editableEbookDocument = editor.Edit(ebookEditOptions);
}
```
## Krok 7: Tworzenie i edytowanie dokumentu e-mail
Na koniec przyjrzymy się, jak edytować dokumenty e-mailowe. Obejmuje to formaty takie jak EML.
### Twórz i edytuj za pomocą opcji domyślnych
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EditableDocument defaultEditableEmailDocument = editor.Edit();
}
```
### Twórz i edytuj za pomocą opcji niestandardowych
Określ opcje wyjściowe wiadomości e-mail, aby kontrolować proces edycji.
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EmailEditOptions emailEditOptions = new EmailEditOptions
    {
        MailMessageOutput = MailMessageOutput.All
    };
    EditableDocument editableEmailDocument = editor.Edit(emailEditOptions);
}
```
## Krok 8: Zakończenie procesu
Po edycji dokumentów bardzo ważne jest prawidłowe pozbycie się strumienia pamięci, aby zwolnić zasoby.
```csharp
memoryStream.Dispose();
System.Console.WriteLine("CreateDocument routine has successfully finished");
```
## Wniosek
GroupDocs.Editor dla .NET to wszechstronne i potężne narzędzie, które może uprościć zadanie programowej edycji różnych typów dokumentów. Postępując zgodnie z tym szczegółowym przewodnikiem, możesz z łatwością tworzyć i edytować dokumenty, niezależnie od tego, czy są to pliki WordProcessing, arkusze kalkulacyjne, prezentacje, książki elektroniczne czy wiadomości e-mail. Zapoznaj się z dokumentacją GroupDocs.Editor, aby poznać bardziej zaawansowane funkcje i opcje dostosowywania.
## Często zadawane pytania
### Jakie typy dokumentów mogę edytować za pomocą GroupDocs.Editor dla .NET?
Możesz edytować szeroką gamę dokumentów, w tym WordProcessing, arkusze kalkulacyjne, prezentacje, e-booki i e-maile.
### Czy można dostosować opcje edycji?
Tak, GroupDocs.Editor dla .NET umożliwia szerokie dostosowywanie poprzez różne opcje edycji specyficzne dla każdego typu dokumentu.
### Jak postępować z wydrukiem edytowanych dokumentów?
Możesz użyć funkcji wywołania zwrotnego, aby zapisać edytowany strumień dokumentów w wybranej lokalizacji.
### Czy potrzebuję licencji, aby używać GroupDocs.Editor dla .NET?
 Tak, możesz uzyskać licencję od[Tutaj](https://purchase.groupdocs.com/buy). Istnieje również możliwość uzyskania licencji tymczasowej.
### Gdzie mogę znaleźć bardziej szczegółową dokumentację?
 Szczegółowa dokumentacja dostępna jest na stronie[Strona dokumentacji GroupDocs.Editor dla platformy .NET](https://tutorials.groupdocs.com/editor/net/).