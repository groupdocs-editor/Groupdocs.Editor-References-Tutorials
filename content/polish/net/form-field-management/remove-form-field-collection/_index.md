---
title: Usuń kolekcję pól formularza
linktitle: Usuń kolekcję pól formularza
second_title: Edytor GroupDocs.NET API
description: Z tego przewodnika krok po kroku dowiesz się, jak usuwać pola formularzy z dokumentów programu Word za pomocą programu GroupDocs.Editor dla platformy .NET. Idealny dla programistów.
weight: 13
url: /pl/net/form-field-management/remove-form-field-collection/
---

# Usuń kolekcję pól formularza

## Wstęp
Czy chcesz programowo zarządzać polami formularzy w swoich dokumentach? GroupDocs.Editor dla .NET oferuje zaawansowane rozwiązanie do obsługi i manipulowania polami formularzy w różnych formatach dokumentów. W tym samouczku przeprowadzimy Cię przez kroki usuwania kolekcji pól formularzy z dokumentu programu Word przy użyciu tej niezawodnej biblioteki. 
## Warunki wstępne
Zanim zagłębimy się w kod, upewnijmy się, że wszystko jest skonfigurowane tak, aby zapewnić płynne działanie:
1. GroupDocs.Editor dla .NET: Upewnij się, że pobrałeś i zainstalowałeś GroupDocs.Editor dla .NET. Jeśli nie, możesz go pobrać[Tutaj](https://releases.groupdocs.com/editor/net/).
2. Środowisko programistyczne: będziesz potrzebować środowiska programistycznego, takiego jak Visual Studio.
3. .NET Framework: Upewnij się, że na komputerze jest zainstalowana platforma .NET Framework.
4.  Przykładowy dokument: Przygotuj przykładowy dokument programu Word (np.`SampleLegacyFormFields.docx`) z polami formularza, którymi chcesz manipulować.

## Importuj przestrzenie nazw
Aby rozpocząć, musisz zaimportować niezbędne przestrzenie nazw do swojego projektu .NET. Umożliwi to dostęp do funkcjonalności GroupDocs.Editor.
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System.IO;
```
## Krok 1: Załaduj dokument
Najpierw musisz załadować dokument, który chcesz edytować. Rozbijmy to:
### Krok 1.1: Uzyskaj ścieżkę do pliku wejściowego
 Musisz określić ścieżkę do pliku wejściowego. W tym przykładzie użyjemy przykładowego pliku o nazwie`SampleLegacyFormFields.docx`.
```csharp
string inputFilePath = "path/to/SampleLegacyFormFields.docx";
```
### Krok 1.2: Utwórz strumień plików ze ścieżki
 Następnie utwórz plik`FileStream` przeczytać dokument.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
    // Przejdź do kolejnych kroków w ramach tego bloku.
}
```
## Krok 2: Ustaw opcje ładowania
Podczas ładowania dokumentu może być konieczne określenie opcji ładowania, szczególnie jeśli dokument jest chroniony hasłem.
### Krok 2.1: Utwórz opcje ładowania
 Utwórz instancję`WordProcessingLoadOptions`.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
```
### Krok 2.2: Podaj hasło (jeśli to konieczne)
Jeśli dokument jest chroniony hasłem, możesz określić hasło.
```csharp
loadOptions.Password = "some_password_to_open_a_document";
```
## Krok 3: Załaduj dokument do edytora
 Teraz załaduj dokument do`Editor` przykład za pomocą`FileStream` I`LoadOptions`.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    // Przejdź do kolejnych kroków w ramach tego bloku.
}
```
## Krok 4: Uzyskaj dostęp do pól formularza i zarządzaj nimi
Po załadowaniu dokumentu możesz teraz uzyskać dostęp do pól formularza i manipulować nimi.
### Krok 4.1: Przeczytaj menedżera FormFieldManager
 Odzyskaj`FormFieldManager` z`Editor` instancja.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
### Krok 4.2: Uzyskaj dostęp do FormFieldCollection
 Uzyskać`FormFieldCollection` który zawiera wszystkie pola formularza w dokumencie.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
### Krok 4.3: Usuń określone pole formularza tekstowego
Aby usunąć określone pole formularza tekstowego, zlokalizuj je po nazwie, a następnie usuń.
```csharp
TextFormField textField = collection.GetFormField<TextFormField>("Text1");
fieldManager.RemoveFormFiled(textField);
```
### Krok 4.4: Usuń wiele pól formularza
Możesz także usunąć wiele pól formularza jednocześnie, podając ich nazwy.
```csharp
textField = collection.GetFormField<TextFormField>("Text7");
CheckBoxForm checkBoxForm = collection.GetFormField<CheckBoxForm>("Check2");
fieldManager.RemoveFormFields(new IFormField[] { textField, checkBoxForm });
```
## Krok 5: Zapisz zmodyfikowany dokument
Po modyfikacji pól formularza należy zapisać dokument.
### Krok 5.1: Utwórz opcje zapisu
Określ format i opcje zapisu dokumentu wyjściowego.
```csharp
WordProcessingFormats docFormat = WordProcessingFormats.Docx;
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(docFormat);
```
### Krok 5.2: Zoptymalizuj wykorzystanie pamięci
Jeśli masz do czynienia z dużymi dokumentami, możesz zoptymalizować wykorzystanie pamięci.
```csharp
saveOptions.OptimizeMemoryUsage = true;
```
### Krok 5.3: Ustaw ochronę (w razie potrzeby)
Możesz zabezpieczyć dokument przed dalszą edycją, ustawiając hasło zapisu.
```csharp
saveOptions.Protection = new WordProcessingProtection(WordProcessingProtectionType.AllowOnlyFormFields, "write_password");
```
### Krok 5.4: Zapisz dokument
 Na koniec zapisz dokument za pomocą pliku a`MemoryStream`.
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(outputStream, saveOptions);
}
```

## Wniosek
Gratulacje! Pomyślnie usunąłeś pola formularza z dokumentu programu Word za pomocą programu GroupDocs.Editor dla .NET. Ta potężna biblioteka ułatwia programowe manipulowanie zawartością dokumentu, oszczędzając czas i wysiłek.
## Często zadawane pytania
### Czy mogę używać programu GroupDocs.Editor for .NET z dokumentami w innych formatach?
Tak, GroupDocs.Editor dla .NET obsługuje różne formaty dokumentów, w tym PDF, HTML i inne.
### Czy można dodawać pola formularzy za pomocą GroupDocs.Editor dla .NET?
Tak, możesz programowo dodawać, modyfikować i usuwać pola formularzy.
### Co się stanie, jeśli mój dokument jest bardzo duży?
Możesz włączyć optymalizację pamięci w opcjach zapisywania, aby wydajnie obsługiwać duże dokumenty.
### Czy mogę używać GroupDocs.Editor for .NET w aplikacji internetowej?
Absolutnie! GroupDocs.Editor dla .NET można zintegrować z aplikacjami internetowymi w celu przetwarzania dokumentów po stronie serwera.
### Gdzie mogę uzyskać pomoc, jeśli napotkam problemy?
 Możesz odwiedzić[forum wsparcia](https://forum.groupdocs.com/c/editor/20) o pomoc w każdej kwestii.