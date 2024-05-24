---
title: Pracuj ze starszą kolekcją pól formularzy
linktitle: Pracuj ze starszą kolekcją pól formularzy
second_title: Edytor GroupDocs.NET API
description: Dowiedz się, jak zarządzać starszymi polami formularzy za pomocą GroupDocs.Editor dla .NET, korzystając z naszego szczegółowego przewodnika. Idealny do obsługi pól tekstowych, pól wyboru, dat i nie tylko.
type: docs
weight: 12
url: /pl/net/form-field-management/work-legacy-form-field-collection/
---
## Wstęp
Witamy w tym obszernym przewodniku na temat pracy ze starszymi zbiorami pól formularzy przy użyciu programu GroupDocs.Editor dla platformy .NET. Niezależnie od tego, czy masz do czynienia z polami tekstowymi, polami wyboru, polami daty czy menu rozwijanymi, ten samouczek przeprowadzi Cię przez każdy krok, aby efektywnie zarządzać tymi polami. Pod koniec tego przewodnika będziesz mieć solidną wiedzę na temat korzystania z GroupDocs.Editor do obsługi różnych pól formularzy w dokumentach. Zanurzmy się!
## Warunki wstępne
Zanim zaczniemy, upewnij się, że spełniasz następujące wymagania wstępne:
- Visual Studio: każda najnowsza wersja będzie działać.
- .NET Framework: Upewnij się, że masz zainstalowaną platformę .NET Framework.
-  GroupDocs.Editor dla .NET: Pobierz najnowszą wersję[Tutaj](https://releases.groupdocs.com/editor/net/).
- Przykładowy dokument: przykładowy plik DOCX z polami formularza do celów testowych.
## Importuj przestrzenie nazw
Na początek zaimportuj niezbędne przestrzenie nazw do swojego projektu. Te przestrzenie nazw są niezbędne do uzyskania dostępu do klas i metod wymaganych do manipulowania polami formularzy.
```csharp
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System.IO;
```
## Krok 1: Uzyskaj ścieżkę pliku wejściowego
Najpierw musisz określić ścieżkę do pliku wejściowego. W tym przykładzie użyjemy przykładowego pliku DOCX zawierającego różne pola formularzy.
```csharp
string inputFilePath = "path/to/your/sample_legacy_formfields.docx";
```
## Krok 2: Utwórz strumień ze ścieżki pliku
Następnie utwórz strumień plików, aby odczytać zawartość dokumentu. Ten strumień zostanie użyty do załadowania dokumentu do GroupDocs.Editor.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
    // Tutaj zostanie umieszczony dodatkowy kod
}
```
## Krok 3: Utwórz opcje ładowania dokumentu
Przed załadowaniem dokumentu utwórz opcje ładowania. Opcje te pomogą w obsłudze różnych scenariuszy, takich jak dokumenty chronione hasłem.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
// Jeśli dokument jest chroniony hasłem, podaj hasło
loadOptions.Password = "your_password_here"; // Jeśli to konieczne, użyj rzeczywistego hasła
```
## Krok 4: Załaduj dokument z instancją edytora
Teraz załaduj dokument do instancji Editor, korzystając z utworzonego wcześniej strumienia plików i opcji ładowania.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    // Tutaj zostanie umieszczony dodatkowy kod
}
```
## Krok 5: Przeczytaj instancję FormFieldManager
Aby zarządzać polami formularzy, uzyskaj dostęp do instancji FormFieldManager z Edytora. Ta instancja umożliwia interakcję z polami formularza w dokumencie.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
## Krok 6: Przeczytaj kolekcję FormField
Pobierz FormFieldCollection z FormFieldManager. Ta kolekcja zawiera wszystkie pola formularza występujące w dokumencie.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
## Krok 7: Iteruj po każdym polu formularza
Przejdź przez każde pole formularza w kolekcji i zidentyfikuj jego typ. W zależności od typu można wyodrębnić wartość pola i manipulować nią.
```csharp
foreach (var formField in collection)
{
    switch (formField.Type)
    {
        case FormFieldType.Text:
            TextFormField textFormField = collection.GetFormField<TextFormField>(formField.Name);
            Console.WriteLine($"TextFormField detected, name: {formField.Name}, value: {textFormField.Value}");
            break;
        case FormFieldType.CheckBox:
            CheckBoxForm checkBoxFormField = collection.GetFormField<CheckBoxForm>(formField.Name);
            Console.WriteLine($"CheckBoxForm detected, name: {formField.Name}, value: {checkBoxFormField.Value}");
            break;
        case FormFieldType.Date:
            DateFormField dateFormField = collection.GetFormField<DateFormField>(formField.Name);
            Console.WriteLine($"DateFormField detected, name: {formField.Name}, value: {dateFormField.Value}");
            break;
        case FormFieldType.Number:
            NumberFormField numberFormField = collection.GetFormField<NumberFormField>(formField.Name);
            Console.WriteLine($"NumberFormField detected, name: {formField.Name}, value: {numberFormField.Value}");
            break;
        case FormFieldType.DropDown:
            DropDownFormField dropDownFormField = collection.GetFormField<DropDownFormField>(formField.Name);
            Console.WriteLine($"DropDownFormField detected, name: {formField.Name}, value selected: {dropDownFormField.Value[dropDownFormField.SelectedIndex]}");
            break;
    }
}
```
## Krok 8: Wniosek
Wykonując poniższe kroki, możesz efektywnie zarządzać polami formularzy w dokumentach i wchodzić w interakcję ze starszymi polami formularzy za pomocą programu GroupDocs.Editor dla .NET. Niezależnie od tego, czy są to pola tekstowe, pola wyboru, daty, liczby czy listy rozwijane, ten przewodnik zapewnia jasny i zwięzły sposób obsługi każdego typu.
## Wniosek
 Praca ze starszymi polami formularzy w dokumentach może być prosta, jeśli użyje się odpowiednich narzędzi. GroupDocs.Editor dla .NET zapewnia solidne rozwiązanie do efektywnego zarządzania tymi polami. Postępując zgodnie z tym przewodnikiem krok po kroku, powinno być teraz możliwe łatwe manipulowanie różnymi polami formularzy w dokumentach. Nie zapomnij zbadać[dokumentacja](https://reference.groupdocs.com/editor/net/)aby uzyskać bardziej zaawansowane funkcje i opcje.
## Często zadawane pytania
### 1. Czy mogę używać GroupDocs.Editor dla .NET z dokumentami chronionymi hasłem?
Tak, możesz określić hasło w opcjach ładowania, aby obsługiwać dokumenty chronione hasłem.
### 2. Jak uzyskać bezpłatną wersję próbną GroupDocs.Editor dla .NET?
 Możesz pobrać bezpłatną wersję próbną ze strony[Tutaj](https://releases.groupdocs.com/).
### 3. Czy dostępna jest obsługa programu GroupDocs.Editor dla platformy .NET?
 Tak, możesz uzyskać dostęp do wsparcia[Tutaj](https://forum.groupdocs.com/c/editor/20).
### 4. Czy mogę kupić licencję na GroupDocs.Editor dla .NET?
 Tak, możesz kupić licencję od[Tutaj](https://purchase.groupdocs.com/buy).
### 5. Gdzie mogę znaleźć dokumentację GroupDocs.Editor dla .NET?
Dokumentacja jest dostępna[Tutaj](https://reference.groupdocs.com/editor/net/).