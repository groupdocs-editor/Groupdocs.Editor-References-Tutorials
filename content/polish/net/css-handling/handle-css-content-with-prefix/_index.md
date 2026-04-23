---
date: 2026-03-06
description: Dowiedz się, jak obsługiwać zawartość CSS z prefiksem i wyodrębniać zawartość
  CSS przy użyciu GroupDocs.Editor dla .NET w tym szczegółowym, krok po kroku, poradniku.
linktitle: Handle CSS Content with Prefix
second_title: GroupDocs.Editor .NET API
title: Obsłuż zawartość CSS z prefiksem
type: docs
url: /pl/net/css-handling/handle-css-content-with-prefix/
weight: 11
---

# Obsługa zawartości CSS z prefiksem

W tym samouczku odkryjesz **jak obsługiwać prefiks CSS** podczas pracy z arkuszami stylów w dokumencie przy użyciu GroupDocs.Editor dla .NET. Niezależnie od tego, czy musisz dodać prefiks URL do obrazów, czcionek lub dowolnych zasobów zewnętrznych, poniższe kroki pokażą Ci dokładnie, jak **obsługiwać prefiks CSS** oraz jak **wyodrębnić zawartość CSS** do dalszego przetwarzania.

## Quick Answers
- **Co oznacza „obsługa prefiksu CSS”?** Dodanie własnego prefiksu URL do zewnętrznych zasobów odwoływanych w CSS.
- **Która metoda API zwraca style CSS?** `EditableDocument.GetCssContent(...)`.
- **Czy potrzebna jest licencja?** Dostępna jest licencja próbna; licencja komercyjna jest wymagana w środowisku produkcyjnym.
- **Jakie wersje .NET są obsługiwane?** .NET Framework 4.5+ oraz .NET Core/5/6.
- **Czy mogę zmienić prefiks w czasie działania?** Tak – wystarczy przekazać inny ciąg znaków do `GetCssContent`.

## What is **handle css prefix**?
Zastosowanie prefiksu do zasobów CSS przepisuje ścieżki obrazów, czcionek lub innych elementów tak, aby wskazywały na lokalizację, którą kontrolujesz (np. CDN lub zabezpieczony serwer). Jest to szczególnie przydatne, gdy eksportujesz dokument i potrzebujesz, aby wszystkie odwołania zewnętrzne były dostępne z aplikacji internetowej.

## Why use GroupDocs.Editor to **extract css content**?
GroupDocs.Editor może odczytać oryginalny CSS osadzony w dokumentach przetwarzania tekstu, udostępnić surowe ciągi arkuszy stylów i pozwolić na ich manipulację przed renderowaniem lub zapisem. Eliminuje to potrzebę ręcznego parsowania i zapewnia, że wyodrębniony CSS odpowiada wewnętrznej reprezentacji dokumentu.

## Prerequisites
Before we get started, make sure you have the following prerequisites in place:
- Visual Studio: Potrzebujesz działającej instalacji Visual Studio.  
- .NET Framework: Upewnij się, że masz zainstalowany .NET Framework.  
- GroupDocs.Editor for .NET: Możesz go pobrać [here](https://releases.groupdocs.com/editor/net/).  
- Sample Document: Przygotuj przykładowy dokument do edycji.

## Import Namespaces
First, let’s import the necessary namespaces to ensure our code runs smoothly. This step gives us access to the core classes of GroupDocs.Editor.

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Editor.Options;
```

## Step 1: Initialize the Editor
The first step involves creating an `Editor` instance with your sample document. This sets up the editing environment.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```

## Step 2: Edit the Document
Next, we obtain an `EditableDocument` object. This object represents the editable version of the file and allows us to work with its internal parts.

```csharp
    using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
    {
```

## Step 3: Set External Prefixes
Define the URL prefixes for images and fonts. These prefixes will be prepended to every image and font reference found in the CSS.

```csharp
        string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
        string externalFontsPrefix = "http://www.mywebsite.com/fonts/id=";
```

## Step 4: **Extract CSS content** with the Prefixes
Call `GetCssContent`, passing the prefixes you just defined. The method returns a list of CSS stylesheet strings that already contain the prefixed URLs.

```csharp
        List<string> stylesheets = document.GetCssContent(externalImagesPrefix, externalFontsPrefix);
```

## Step 5: Output the Results
Print the number of stylesheets found and display each stylesheet. This helps you verify that the prefixes were applied correctly.

```csharp
        Console.WriteLine("There are {0} stylesheets in the input document", stylesheets.Count);
        foreach (string css in stylesheets)
        {
            Console.WriteLine(css);
        }
    }
}
```

## Common Issues and Solutions
- **Brak zwróconych arkuszy stylów** – Upewnij się, że dokument źródłowy rzeczywiście zawiera CSS (np. dokument Word z formatowanymi tabelami lub osadzonym HTML).  
- **Nieprawidłowe URL** – Sprawdź, czy ciągi prefiksu kończą się odpowiednim separatorem (`/` lub `=`) zgodnie z routingiem Twojego serwera.  
- **Problemy z wydajnością** – W przypadku bardzo dużych dokumentów rozważ przetwarzanie arkuszy stylów w partiach, aby uniknąć wysokiego zużycia pamięci.

## Conclusion
Handling CSS content with a prefix using GroupDocs.Editor for .NET is straightforward and powerful. By following these steps you can **handle css prefix**, retrieve the raw CSS via **extract css content**, and seamlessly integrate external resources into your web workflow. Explore other GroupDocs.Editor features such as HTML conversion, image extraction, and document merging to get even more value out of the API.

## FAQ's
### Can I use GroupDocs.Editor for .NET with other document formats?
Yes, GroupDocs.Editor for .NET supports various document formats including PDF, Word, Excel, and more.

### Is there a free trial available for GroupDocs.Editor for .NET?
Absolutely! You can start your free trial [here](https://releases.groupdocs.com/).

### How do I get a temporary license for GroupDocs.Editor for .NET?
You can obtain a temporary license [here](https://purchase.groupdocs.com/temporary-license/).

### Where can I find detailed documentation for GroupDocs.Editor for .NET?
Detailed documentation is available [here](https://tutorials.groupdocs.com/editor/net/).

### What support options are available for GroupDocs.Editor for .NET?
You can get support [here](https://forum.groupdocs.com/c/editor/20).

## Additional Frequently Asked Questions

**Q: Can I change the prefix after extracting the CSS?**  
A: Yes. Call `GetCssContent` again with a different prefix string; the method always uses the values you pass at runtime.

**Q: Does this work with password‑protected documents?**  
A: Yes. Provide the password in `WordProcessingLoadOptions` when creating the `Editor` instance.

**Q: Is it possible to save the modified CSS back into the document?**  
A: GroupDocs.Editor currently provides read‑only access to CSS. To persist changes you would need to replace the original stylesheet using the document’s underlying XML APIs.

---

**Last Updated:** 2026-03-06  
**Tested With:** GroupDocs.Editor 23.12 for .NET  
**Author:** GroupDocs