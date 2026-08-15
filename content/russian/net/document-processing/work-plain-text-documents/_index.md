---
date: 2026-08-10
description: Узнайте, как редактировать plain text файлы с помощью GroupDocs.Editor
  for .NET. Руководство охватывает загрузку txt файла, удаление пробелов, установку
  text encoding и сохранение результата.
keywords:
- edit plain text
- load txt file
- trim trailing spaces
- convert leading spaces
- set text encoding
lastmod: 2026-08-10
linktitle: Работа с plain text документами
og_description: Узнайте, как редактировать plain text файлы с помощью GroupDocs.Editor
  for .NET – загрузка txt файла, удаление конечных пробелов, конвертация начальных
  пробелов, установка text encoding и эффективное сохранение.
og_image_alt: Guide showing edit plain text workflow with GroupDocs.Editor for .NET
og_title: Редактировать plain text документы с помощью GroupDocs.Editor for .NET
schemas:
- author: GroupDocs
  dateModified: '2026-08-10'
  description: Learn how to edit plain text files using GroupDocs.Editor for .NET.
    The guide covers loading a txt file, trimming spaces, setting text encoding, and
    saving the result.
  headline: Edit plain text documents with GroupDocs.Editor for .NET
  type: TechArticle
- description: Learn how to edit plain text files using GroupDocs.Editor for .NET.
    The guide covers loading a txt file, trimming spaces, setting text encoding, and
    saving the result.
  name: Edit plain text documents with GroupDocs.Editor for .NET
  steps:
  - name: Get a path to the input TXT file
    text: First, decide whether you’ll work with a physical file path or a memory
      stream. Using a path is the most straightforward approach for local development.
  - name: Create an Editor instance
    text: '`Editor` is the main class that loads a document and provides editing capabilities.'
  - name: Create TXT editing options
    text: '`TxtEditOptions` configures how plain‑text files are parsed and edited,
      allowing you to set encoding and space‑handling rules.'
  - name: Create an EditableDocument instance
    text: '`EditableDocument` represents the in‑memory version of the loaded document,
      including its text and any associated resources.'
  - name: Edit the document content
    text: Retrieve the original text, apply any string operations you need (e.g.,
      replace, trim, change case), and store the result back into the `EditableDocument`.
  - name: Create an EditableDocument with updated content
    text: After you’ve transformed the text, instantiate a new `EditableDocument`
      that contains the edited string and the original resource collection.
  - name: Create WordProcessing save options
    text: '`WordProcessingSaveOptions` defines settings for saving the document in
      a Word‑compatible format such as DOCX or DOCM.'
  - name: Create TXT saving options
    text: '`TxtSaveOptions` specifies how the edited plain‑text file should be written,
      including encoding, line‑ending preservation, and table layout handling.'
  - name: Prepare output paths
    text: Derive the output directory from the input file path, then build the full
      filenames for the DOCX and TXT results.
  - name: Save the edited document
    text: Finally, call `editor.Save` twice—once with the WordProcessing options and
      once with the TXT options—to produce both formats in a single operation.
  type: HowTo
- questions:
  - answer: The library supports 50+ formats, including DOCX, TXT, HTML, PDF, and
      markdown, allowing you to edit and convert between them seamlessly.
    question: What file formats does GroupDocs.Editor for .NET support?
  - answer: Download the trial from the [releases page](https://releases.groupdocs.com/).
    question: How can I get a free trial of GroupDocs.Editor for .NET?
  - answer: Yes, temporary licenses are available through the [GroupDocs purchase
      page](https://purchase.groupdocs.com/temporary-license/).
    question: Can I purchase a temporary license for testing?
  - answer: The official support forum is the best place – visit the [GroupDocs.Editor
      support forum](https://forum.groupdocs.com/c/editor/20).
    question: Where can I find support if I run into issues?
  - answer: Absolutely. The full reference is on the [GroupDocs.Editor documentation
      page](https://tutorials.groupdocs.com/editor/net/).
    question: Is there detailed documentation for advanced scenarios?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
tags:
- edit plain text
- GroupDocs.Editor
- C# document processing
- plain text editing
- txt file handling
title: Редактировать plain text документы с помощью GroupDocs.Editor for .NET
type: docs
url: /ru/net/document-processing/work-plain-text-documents/
weight: 15
---

# Редактировать простые текстовые документы с помощью GroupDocs.Editor для .NET

## Введение
Если вам нужно **редактировать простой текст** быстро и надёжно в .NET‑приложении, GroupDocs.Editor для .NET — это инструмент, который делает всю тяжёлую работу. Этот API поддерживает более 30 форматов документов, может обрабатывать файлы размером до 500 МБ и позволяет манипулировать текстом без загрузки всего файла в память. В этом руководстве вы узнаете, как загрузить txt‑файл, удалить конечные пробелы, преобразовать начальные пробелы, установить правильную кодировку и, наконец, сохранить отредактированное содержимое обратно на диск. Готовы приступить? Давайте начнём!

## Быстрые ответы
- **Какой первый шаг для редактирования txt‑файла?** Загрузите файл с помощью `Editor`, используя имеющийся путь или поток.  
- **Могу ли я изменить кодировку файла во время редактирования?** Да — `TxtSaveOptions` позволяют указать UTF‑8, UTF‑16 или любую пользовательскую кодировку.  
- **Как удалить лишние пробелы в конце каждой строки?** Получите текст, вызовите `TrimEnd()` для каждой строки и запишите его обратно.  
- **Можно ли бесплатно попробовать GroupDocs.Editor?** Полнофункциональная 30‑дневная пробная версия доступна на странице релизов.  
- **Какие версии .NET поддерживаются?** .NET Framework 4.6+, .NET Core 3.1+, и .NET 5/6/7.

## Что такое редактирование простого текста?
**Редактирование простого текста** означает программное изменение символов внутри простого `.txt`‑файла — добавление, удаление или пере‑форматирование текста — при сохранении исходной кодировки файла и стиля разрывов строк. Это может включать такие задачи, как удаление пробелов, нормализация разрывов строк, обновление значений конфигурации или вставка сгенерированного контента. Операция должна сохранять возможность чтения файла любым стандартным текстовым редактором и поддерживать любые существующие метаданные, такие как маркеры BOM.

## Почему стоит использовать GroupDocs.Editor для редактирования простого текста?
GroupDocs.Editor обрабатывает файлы в потоковом режиме, что означает возможность редактировать лог‑файл размером 300 МБ, используя менее 50 МБ ОЗУ. Библиотека поддерживает **более 50 форматов ввода и вывода**, автоматически определяет стили разрывов строк (CR, LF, CRLF) и предоставляет встроенные опции для **удаления конечных пробелов** и **преобразования начальных пробелов** без необходимости писать собственные парсеры.

## Предварительные требования
- **Среда разработки .NET** — Visual Studio 2022 или VS Code с расширением C#.  
- **GroupDocs.Editor для .NET** — загрузите со страницы релизов [GroupDocs.Editor for .NET](https://releases.groupdocs.com/editor/net/).  
- **Базовые знания C#** — вы должны быть уверены в работе с вводом‑выводом файлов и манипуляциями со строками.  
- **Текстовый редактор (необязательно)** — для просмотра исходных файлов; рекомендуется VS Code.  
- Для подробного использования см. [документацию](https://tutorials.groupdocs.com/editor/net/).  
- Вы также можете просмотреть общую [страницу релизов](https://releases.groupdocs.com/).

## Как редактировать простой текст пошагово
Загрузите файл, отредактируйте его содержимое и сохраните обратно — всё это менее чем в десяти строках кода. Ниже приведённые разделы проведут вас через каждый этап с понятными объяснениями.

### Шаг 1: Получить путь к входному TXT‑файлу
Сначала решите, будете ли вы работать с физическим путём к файлу или с потоковой памятью. Использование пути — самый простой подход для локальной разработки.

```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

### Шаг 2: Создать экземпляр Editor
`Editor` — основной класс, который загружает документ и предоставляет возможности редактирования.

```csharp
string inputFilePath = "YourSampleDocument.txt";
```

### Шаг 3: Создать параметры редактирования TXT
`TxtEditOptions` настраивает способ разбора и редактирования простых текстовых файлов, позволяя задать кодировку и правила обработки пробелов.

```csharp
using (Editor editor = new Editor(inputFilePath))
{
```

### Шаг 4: Создать экземпляр EditableDocument
`EditableDocument` представляет собой версию загруженного документа в памяти, включая его текст и любые связанные ресурсы.

```csharp
    TextEditOptions editOptions = new TextEditOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        RecognizeLists = true,
        LeadingSpaces = TextLeadingSpacesOptions.ConvertToIndent,
        TrailingSpaces = TextTrailingSpacesOptions.Trim
    };
```

### Шаг 5: Отредактировать содержимое документа
Получите оригинальный текст, примените необходимые операции со строками (например, замену, обрезку, изменение регистра) и сохраните результат обратно в `EditableDocument`.

```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```

### Шаг 6: Создать EditableDocument с обновлённым содержимым
После преобразования текста создайте новый `EditableDocument`, содержащий отредактированную строку и исходную коллекцию ресурсов.

```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("text", "EDITED text");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```

### Шаг 7: Создать параметры сохранения WordProcessing
`WordProcessingSaveOptions` определяет настройки для сохранения документа в совместимом с Word формате, таком как DOCX или DOCM.

```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```

### Шаг 8: Создать параметры сохранения TXT
`TxtSaveOptions` указывает, как должен быть записан отредактированный простой текстовый файл, включая кодировку, сохранение разрывов строк и обработку табличного макета.

```csharp
    WordProcessingSaveOptions wordSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm)
    {
        Locale = System.Globalization.CultureInfo.GetCultureInfo("en-GB")
    };
```

### Шаг 9: Подготовить пути вывода
Получите каталог вывода из пути входного файла, затем сформируйте полные имена файлов для результатов DOCX и TXT.

```csharp
    TextSaveOptions txtSaveOptions = new TextSaveOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        PreserveTableLayout = true
    };
```

### Шаг 10: Сохранить отредактированный документ
Наконец, вызовите `editor.Save` дважды — один раз с параметрами WordProcessing и один раз с параметрами TXT, чтобы создать оба формата за одну операцию.

```csharp
    string outputWordPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".docm");
    string outputTxtPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".txt");
```

## Распространённые проблемы и решения
- **Оставшиеся конечные пробелы после редактирования** — убедитесь, что `TxtEditOptions.TrimTrailingSpaces` установлен в `true` перед загрузкой документа.  
- **Неправильная кодировка в сохранённом файле** — проверьте, что `TxtSaveOptions.Encoding` соответствует требуемой кодовой странице (например, `Encoding.UTF8`).  
- **Большие файлы вызывают OutOfMemoryException** — используйте потоковый API (`Editor.Load(Stream)`) вместо загрузки по пути к файлу, чтобы снизить использование памяти.  

## Часто задаваемые вопросы

**В: Какие форматы файлов поддерживает GroupDocs.Editor для .NET?**  
О: Библиотека поддерживает более 50 форматов, включая DOCX, TXT, HTML, PDF и markdown, позволяя без проблем редактировать и конвертировать их между собой.

**В: Как получить бесплатную пробную версию GroupDocs.Editor для .NET?**  
О: Скачайте пробную версию со [страницы релизов](https://releases.groupdocs.com/).

**В: Можно ли приобрести временную лицензию для тестирования?**  
О: Да, временные лицензии доступны на [странице покупки GroupDocs](https://purchase.groupdocs.com/temporary-license/).

**В: Где можно получить поддержку, если возникнут проблемы?**  
О: Официальный форум поддержки — лучший вариант; посетите [форум поддержки GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).

**В: Есть ли подробная документация для продвинутых сценариев?**  
О: Конечно. Полная справка доступна на [странице документации GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/).

## Заключение
Теперь вы освоили, как **редактировать простой текст** с помощью GroupDocs.Editor для .NET — загрузка txt‑файла, удаление пробелов, преобразование начальных пробелов, установка правильной кодировки и сохранение результата как в форматах TXT, так и DOCX. Эта возможность позволяет автоматизировать очистку лог‑файлов, генерировать конфигурационные файлы «на лету» или создавать собственные конвейеры обработки текста без необходимости изобретать колесо заново. Исследуйте дополнительные функции, такие как пакетная обработка и конвертация документов, посетив официальную документацию.

**Последнее обновление:** 2026-08-10  
**Тестировано с:** GroupDocs.Editor 23.11 for .NET  
**Автор:** GroupDocs  

```csharp
    editor.Save(afterEdit, outputWordPath, wordSaveOptions);
    editor.Save(afterEdit, outputTxtPath, txtSaveOptions);
}
System.Console.WriteLine("Document editing process completed successfully!");
```

## Связанные руководства

- [Руководства по загрузке документов с GroupDocs.Editor для .NET](/editor/net/document-loading/)
- [Руководства по сохранению и экспорту документов для GroupDocs.Editor .NET](/editor/net/document-saving/)
- [Руководства по редактированию простого текста и DSV‑документов для GroupDocs.Editor .NET](/editor/net/plain-text-dsv-documents/)