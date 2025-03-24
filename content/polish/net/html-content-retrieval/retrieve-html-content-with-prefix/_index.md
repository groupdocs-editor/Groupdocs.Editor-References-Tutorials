---
title: Pobierz treść HTML z prefiksem
linktitle: Pobierz treść HTML z prefiksem
second_title: Edytor GroupDocs.NET API
description: Dowiedz się, jak pobierać zawartość HTML z dokumentów za pomocą narzędzia GroupDocs.Editor dla platformy .NET z niestandardowymi przedrostkami obrazów i arkuszy stylów. W zestawie instrukcja krok po kroku.
weight: 11
url: /pl/net/html-content-retrieval/retrieve-html-content-with-prefix/
---

# Pobierz treść HTML z prefiksem

## Wstęp
Witamy w naszym samouczku krok po kroku dotyczącym pobierania zawartości HTML z dokumentu za pomocą programu GroupDocs.Editor dla platformy .NET. Niezależnie od tego, czy jesteś doświadczonym programistą, czy dopiero zaczynasz, ten przewodnik w łatwy do zrozumienia sposób przeprowadzi Cię przez ten proces. Omówimy wszystko, co musisz wiedzieć, od skonfigurowania środowiska po pomyślne wykonanie kodu. Zanurzmy się!
## Warunki wstępne
Zanim zaczniemy, upewnij się, że masz następujące wymagania wstępne:
1.  GroupDocs.Editor dla .NET: Pobierz najnowszą wersję z[strona pobierania](https://releases.groupdocs.com/editor/net/).
2. Środowisko programistyczne: Visual Studio lub inne preferowane środowisko programistyczne .NET.
3. Podstawowa znajomość języka C#: Znajomość programowania w języku C# pomoże Ci śledzić przykłady.
4. Dokument do edycji: Przygotuj przykładowy dokument do testowania, na przykład dokument programu Word.
5. .NET Framework: Upewnij się, że na komputerze jest zainstalowana platforma .NET Framework.
Teraz, gdy już wszystko masz gotowe, zaczynajmy!
## Importuj przestrzenie nazw
Najpierw musisz zaimportować niezbędne przestrzenie nazw do swojego projektu C#. Te przestrzenie nazw udostępniają klasy i metody wymagane do pracy z programem GroupDocs.Editor dla platformy .NET.
```csharp
using System;
using GroupDocs.Editor.Options;
```
Po zaimportowaniu przestrzeni nazw możemy przejść do konfiguracji edytora.
## Krok 1: Zainicjuj edytor
 Aby rozpocząć, musisz zainicjować plik`Editor`zajęcia ze swoim dokumentem. Ten krok obejmuje określenie dokumentu, który chcesz edytować i podanie niezbędnych opcji ładowania.
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
    // Dalsze kroki zostaną dodane tutaj
}
```
 W tym przykładzie ładujemy dokument Word. Możesz wymienić`"Your Sample Document"` ze ścieżką do dokumentu.
## Krok 2: Edytuj dokument
 Następnie musimy otworzyć dokument do edycji. Odbywa się to za pomocą`Edit` metoda`Editor` klasa, która wymaga`WordProcessingEditOptions` jako argument.
```csharp
using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
{
    // Dalsze kroki zostaną dodane tutaj
}
```
 The`EditableDocument` instancja reprezentuje dokument w edytowalnym formacie. Teraz jesteśmy gotowi do pobrania zawartości HTML.
## Krok 3: Zdefiniuj niestandardowe prefiksy
Aby dodać niestandardowe przedrostki do obrazów i CSS, musimy zdefiniować przedrostki jako ciągi znaków. Ten krok zapewnia, że treść HTML będzie miała określone przedrostki dla zasobów zewnętrznych.
```csharp
string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
string externalCssPrefix = "http://www.mywebsite.com/css/id=";
```
Możesz zastąpić adresy URL żądanymi prefiksami. Te przedrostki zostaną użyte w następnym kroku w celu dostosowania wyniku HTML.
## Krok 4: Pobierz zawartość HTML
Teraz, gdy mamy już ustawione przedrostki, możemy pobrać treść HTML z dokumentu. The`GetContent` metoda`EditableDocument` class pozwala nam określić obraz i prefiksy CSS.
```csharp
string prefixedHtmlContent = document.GetContent(externalImagesPrefix, externalCssPrefix);
Console.WriteLine("HTML content of the input document with custom image and stylesheet prefixes: {0}", prefixedHtmlContent);
```
Ten fragment kodu pobiera treść HTML z niestandardowymi przedrostkami i drukuje ją na konsoli. W razie potrzeby możesz dalej przetwarzać lub zapisywać tę treść HTML.
## Wniosek
I masz to! Wykonując poniższe kroki, możesz łatwo pobrać zawartość HTML z dokumentu za pomocą programu GroupDocs.Editor dla .NET, wraz z niestandardowymi przedrostkami obrazów i arkuszy stylów. To potężne narzędzie upraszcza manipulowanie dokumentami, umożliwiając skupienie się na płynnej integracji edycji dokumentów z aplikacjami .NET.
 Aby uzyskać bardziej szczegółowe informacje, zapoznaj się z[GroupDocs.Editor dla dokumentacji .NET](https://tutorials.groupdocs.com/editor/net/) . Jeśli masz jakieś pytania lub potrzebujesz dalszej pomocy, skontaktuj się z nami pod adresem[forum wsparcia](https://forum.groupdocs.com/c/editor/20).
## Często zadawane pytania
### Jakie typy dokumentów mogę edytować za pomocą GroupDocs.Editor dla .NET?
GroupDocs.Editor obsługuje różne formaty dokumentów, w tym Word, Excel, PowerPoint, PDF i inne.
### Jak uzyskać bezpłatną wersję próbną GroupDocs.Editor dla .NET?
 Możesz uzyskać bezpłatną wersję próbną od[Witryna GroupDocs](https://releases.groupdocs.com/).
### Czy mogę bardziej dostosować treść HTML?
Tak, możesz w razie potrzeby zmodyfikować pobraną treść HTML przed jej wyrenderowaniem lub zapisaniem.
### Czy można używać GroupDocs.Editor dla .NET z innymi językami .NET?
Tak, możesz go używać z dowolnym językiem zgodnym z .NET, takim jak VB.NET lub F#.
### Jak uzyskać tymczasową licencję na GroupDocs.Editor dla .NET?
 Możesz uzyskać tymczasową licencję od[strona zakupu](https://purchase.groupdocs.com/temporary-license/).