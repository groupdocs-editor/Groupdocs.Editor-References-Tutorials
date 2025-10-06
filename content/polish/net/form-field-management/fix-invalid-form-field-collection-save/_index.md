---
title: Napraw nieprawidłowy zbiór pól formularza i zapisz
linktitle: Napraw nieprawidłowy zbiór pól formularza i zapisz
second_title: Edytor GroupDocs.NET API
description: Dowiedz się, jak naprawić nieprawidłowe pola formularza w DOCX za pomocą Groupdocs.Editor dla .NET. Postępuj zgodnie z tym przewodnikiem, aby mieć pewność, że Twoje dokumenty są wolne od błędów i bezpiecznie je zapisywać.
weight: 11
url: /pl/net/form-field-management/fix-invalid-form-field-collection-save/
type: docs
---
# Napraw nieprawidłowy zbiór pól formularza i zapisz

## Wstęp
Powitanie! Jeśli pracujesz z polami formularzy w dokumentach i napotykasz problemy z nieprawidłowymi zbiorami pól formularzy, jesteś we właściwym miejscu. W tym samouczku omówimy, jak naprawić nieprawidłowe pola formularza i zapisać dokument za pomocą Groupdocs.Editor dla .NET. Poprowadzimy Cię przez proces krok po kroku, upewniając się, że masz wszystkie szczegóły potrzebne do jego płynnego działania. Zacznijmy!
## Warunki wstępne
Zanim przejdziemy do kodu, jest kilka rzeczy, które musisz mieć na miejscu:
-  Groupdocs.Editor dla .NET: Upewnij się, że zainstalowałeś bibliotekę Groupdocs.Editor dla .NET. Możesz go pobrać[Tutaj](https://releases.groupdocs.com/editor/net/).
- Środowisko programistyczne: Należy mieć skonfigurowane środowisko programistyczne .NET, takie jak Visual Studio.
- Podstawowa znajomość języka C#: W tym samouczku założono, że masz podstawową wiedzę na temat programowania w języku C#.
## Importuj przestrzenie nazw
Najpierw musisz zaimportować niezbędne przestrzenie nazw do swojego projektu C#. Dodaj następujące wiersze na początku pliku kodu:
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System;
using System.IO;
```
## Krok 1: Uzyskaj ścieżkę pliku wejściowego
Pierwszym krokiem jest określenie ścieżki do pliku wejściowego. Plik ten powinien być dokumentem DOCX zawierającym pola formularza.
```csharp
string inputFilePath = Constants.SampleLegacyFormFields_docx;
```
## Krok 2: Utwórz strumień ze ścieżki pliku
Następnie utwórz strumień plików, aby odczytać dokument wejściowy. Umożliwi to załadowanie dokumentu do edytora.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
```
## Krok 3: Utwórz opcje ładowania dokumentu
Na tym etapie musisz utworzyć opcje ładowania dokumentu. Jeśli dokument jest chroniony hasłem, możesz określić hasło. W tym przykładzie dokument nie jest chroniony, więc hasło jest ignorowane.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
loadOptions.Password = "some_password_to_open_a_document";
```
## Krok 4: Załaduj dokument do instancji edytora
Teraz załaduj dokument z określonymi opcjami do instancji Editor. Tutaj będą miały miejsce główne operacje na dokumencie.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
```
## Krok 4.1: Przeczytaj instancję FormFieldManager
 The`FormFieldManager` instancja odpowiada za zarządzanie polami formularzy w dokumencie. Aby uzyskać dostęp do pól formularza i manipulować nimi, musisz przeczytać tę instancję.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
## Krok 4.2: Przeczytaj kolekcję FormField
 The`FormFieldCollection` zawiera wszystkie pola formularza w dokumencie. Przeczytasz tę kolekcję, aby sprawdzić i naprawić nieprawidłowe pola formularza.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
## Krok 4.3: Automatyczna naprawa nieprawidłowych pól formularza
Spróbuj automatycznie naprawić nieprawidłowe pola formularza w dokumencie. Jest to wstępny krok w celu rozwiązania oczywistych problemów.
```csharp
fieldManager.FixInvalidFormFieldNames(new InvalidFormField[0]);
collection = fieldManager.FormFieldCollection;
```
## Krok 4.4: Sprawdź, czy nie ma nieprawidłowych pól formularza
Sprawdź, czy po próbie automatycznej naprawy pozostały jakieś nieprawidłowe pola formularza.
```csharp
bool hasInvalidFormFields = fieldManager.HasInvalidFormFields();
Console.WriteLine("FormFieldCollection contains invalid items: {0}", hasInvalidFormFields);
```
## Krok 4.4.1: Uzyskaj wszystkie nieprawidłowe nazwy pól formularza
Pobierz nazwy wszystkich nieprawidłowych pól formularza. Nazwy te zostaną użyte do naprawienia pól.
```csharp
var invalidFormFields = fieldManager.GetInvalidFormFieldNames();
```
## Krok 4.4.2: Utwórz unikalne nazwy dla nieprawidłowych pól
Dla każdego nieprawidłowego pola formularza utwórz unikalną nazwę. Zapewnia to brak konfliktów z istniejącymi nazwami pól formularza.
```csharp
foreach (var invalidItem in invalidFormFields)
{
    invalidItem.FixedName = string.Format("{0}_{1}", invalidItem.Name, Guid.NewGuid());
}
```
## Krok 4.4.3: Napraw nieprawidłowe pola formularza
Napraw nieprawidłowe pola formularza, używając unikalnych nazw utworzonych w poprzednim kroku.
```csharp
fieldManager.FixInvalidFormFieldNames(invalidFormFields);
collection = fieldManager.FormFieldCollection;
```
## Krok 5: Utwórz opcje zapisywania dokumentu
Skonfiguruj opcje zapisywania dokumentu. Obejmuje to określenie formatu i wszelkich dodatkowych ustawień zapisywania.
```csharp
WordProcessingFormats docFormat = WordProcessingFormats.Docx;
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(docFormat);
```
## Krok 5.1: Zoptymalizuj wykorzystanie pamięci
 Jeśli dokument jest duży i może powodować`OutOfMemoryException`włącz opcję optymalizacji pamięci.
```csharp
saveOptions.OptimizeMemoryUsage = true;
```
## Krok 5.2: Chroń dokument przed zapisem
Aby zabezpieczyć dokument przed modyfikacją, za wyjątkiem pól formularza, należy ustawić hasło zabezpieczające.
```csharp
saveOptions.Protection = new WordProcessingProtection(WordProcessingProtectionType.AllowOnlyFormFields, "write_password");
```
## Krok 6: Zapisz dokument
Na koniec zapisz dokument z określonymi opcjami zapisywania. Przygotuj strumień pamięci do zapisania dokumentu wyjściowego.
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(outputStream, saveOptions);
}
Console.WriteLine("FixInvalidFormFieldCollectionAndSave routine has successfully finished");
```
## Wniosek
 I masz to! Pomyślnie naprawiłeś nieprawidłowe pola formularza i zapisałeś dokument za pomocą Groupdocs.Editor dla .NET. Ten przewodnik krok po kroku powinien był sprawić, że proces będzie jasny i łatwy w zarządzaniu. Jeśli napotkasz jakiekolwiek problemy lub masz pytania, nie wahaj się sprawdzić[dokumentacja](https://tutorials.groupdocs.com/editor/net/) lub skontaktuj się z nami[wsparcie](https://forum.groupdocs.com/c/editor/20).
## Często zadawane pytania
### Co się stanie, jeśli mój dokument jest chroniony hasłem?
 Hasło możesz określić w pliku`WordProcessingLoadOptions` aby otworzyć dokument.
### Skąd mam wiedzieć, czy istnieją nieprawidłowe pola formularza?
 Użyj`HasInvalidFormFields` metoda sprawdzania, czy w dokumencie nie ma nieprawidłowych pól formularza.
### Czy mogę naprawić pola formularza bez zmiany ich nazw?
Aby uniknąć konfliktów, zaleca się utworzenie unikalnych nazw dla nieprawidłowych pól formularza.
### W jakich formatach mogę zapisać dokument?
 Możesz zapisać dokument w różnych formatach, takich jak DOCX, PDF i inne, ustawiając odpowiednie`WordProcessingFormats`.
### Jak zoptymalizować wykorzystanie pamięci podczas zapisywania dużych dokumentów?
 Włącz`OptimizeMemoryUsage` opcja w`WordProcessingSaveOptions` wydajną obsługę dużych dokumentów.