---
date: 2026-06-06
description: Узнайте, как вывести список поддерживаемых форматов документов и определить
  расширение файлов с помощью GroupDocs.Editor для .NET. Пошаговое руководство с примерами
  кода, быстрыми ответами и часто задаваемыми вопросами.
keywords:
- list supported document formats
- determine file format extension
- GroupDocs.Editor .NET
- document editing API
- supported formats guide
linktitle: Список поддерживаемых форматов документов
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to list supported document formats and determine file format
    extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets,
    quick answers, and FAQs.
  headline: List Supported Document Formats with GroupDocs.Editor .NET
  type: TechArticle
- description: Learn how to list supported document formats and determine file format
    extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets,
    quick answers, and FAQs.
  name: List Supported Document Formats with GroupDocs.Editor .NET
  steps:
  - name: '**.NET development environment** – Visual Studio 2022 or any IDE that supports
      .NET 6+.'
    text: '**.NET development environment** – Visual Studio 2022 or any IDE that supports
      .NET 6+.'
  - name: '**GroupDocs.Editor for .NET library** – download from the [GroupDocs releases
      page](https://releases.groupdocs.com/editor/net/).'
    text: '**GroupDocs.Editor for .NET library** – download from the [GroupDocs releases
      page](https://releases.groupdocs.com/editor/net/).'
  - name: '**Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/)
      for unrestricted access.'
    text: '**Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/)
      for unrestricted access.'
  - name: '**Basic C# knowledge** – familiarity with namespaces, `using` statements,
      and console output.'
    text: '**Basic C# knowledge** – familiarity with namespaces, `using` statements,
      and console output.'
  - name: '**Loop Through Formats:** We iterate over all available Word‑processing
      formats.'
    text: '**Loop Through Formats:** We iterate over all available Word‑processing
      formats.'
  - name: '**Output Format Details:** For each format we print its friendly name and
      default file extension.'
    text: '**Output Format Details:** For each format we print its friendly name and
      default file extension.'
  - name: '**Loop Through Formats:** The same looping logic applies to presentations.'
    text: '**Loop Through Formats:** The same looping logic applies to presentations.'
  - name: '**Output Format Details:** The name and extension are displayed for each
      format.'
    text: '**Output Format Details:** The name and extension are displayed for each
      format.'
  - name: '**Parse Format:** `FromExtension` converts the `.xlsm` extension into its
      internal `SpreadsheetFormat` enum.'
    text: '**Parse Format:** `FromExtension` converts the `.xlsm` extension into its
      internal `SpreadsheetFormat` enum.'
  - name: '**Output Format:** The parsed format’s name is printed, confirming the
      mapping.'
    text: '**Output Format:** The parsed format’s name is printed, confirming the
      mapping.'
  type: HowTo
- questions:
  - answer: '`DocumentFormatInfo` provides metadata about supported file types, while
      `SaveOptions` configures how a document is written back to disk (format, compression,
      etc.).'
    question: What is the difference between `DocumentFormatInfo` and `SaveOptions`?
  - answer: Yes—use `DocumentFormatInfo.FromExtension("yourExt")`; if the extension
      isn’t recognized, the method returns `null`.
    question: Can I list formats for a custom file extension?
  - answer: Absolutely. Pass the password to the `Editor` constructor via `EditorSettings`
      to open encrypted documents.
    question: Does GroupDocs.Editor support password‑protected files?
  - answer: Over **30 input and output formats**, spanning Word, Excel, PowerPoint,
      HTML, and plain text.
    question: How many formats does GroupDocs.Editor actually support?
  - answer: Use the `GetEditableWordProcessingFormats()` (or Spreadsheet/Presentation
      equivalents) to retrieve formats that allow full edit capabilities.
    question: Is there a way to restrict the list to only editable formats?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Список поддерживаемых форматов документов с GroupDocs.Editor .NET
type: docs
url: /ru/net/document-processing/work-document-formats/
weight: 13
---

# Список поддерживаемых форматов документов

Добро пожаловать в наш подробный учебник о **how to list supported document formats** с GroupDocs.Editor для .NET. Независимо от того, создаёте ли вы веб‑приложение, ориентированное на документы, или корпоративный настольный инструмент, знание точных форматов, которые вы можете редактировать или конвертировать, имеет решающее значение. В этом руководстве вы узнаете, как перечислять форматы, разбирать расширения и редактировать документы — всё с понятными, человеко‑дружелюбными объяснениями и готовыми к запуску фрагментами кода.

## Быстрые ответы
- **Как перечислить все поддерживаемые форматы?** Используйте `DocumentFormatInfo.GetSupportedWordProcessingFormats()` (или эквиваленты для Presentation/Spreadsheet) и пройдитесь по коллекции.  
- **Могу ли я определить формат по расширению файла?** Да — вызовите `DocumentFormatInfo.FromExtension(".docx")`.  
- **Какие типы файлов поддерживает GroupDocs.Editor?** Более 30 форматов ввода и вывода, включая DOCX, XLSX, PPTX, HTML и обычный текст.  
- **Нужна ли лицензия для получения списка форматов?** Временная лицензия разблокирует полный API; в противном случае пробная версия работает с ограниченными возможностями.  
- **Какие версии .NET совместимы?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.

## Что означает «list supported document formats»?
Фраза относится к программному получению коллекции типов файлов, которые GroupDocs.Editor может открыть, отредактировать и сохранить. Эта операция позволяет создавать динамические выпадающие списки в пользовательском интерфейсе или проверять загружаемые пользователем файлы до их обработки, гарантируя, что только совместимые файлы передаются редактору для дальнейшего манипулирования.

## Почему нужно перечислять поддерживаемые форматы документов?
GroupDocs.Editor **поддерживает более 30 форматов ввода и вывода** и может обрабатывать файлы размером до **2 ГБ**, не загружая весь документ в память. Точное знание списка предотвращает ошибки выполнения, улучшает пользовательский опыт и позволяет применять бизнес‑правила, такие как «разрешать только редактируемые документы Office». Это также помогает показывать пользователям только те форматы, которые действительно поддерживает ваше приложение.

## Требования
1. **Среда разработки .NET** — Visual Studio 2022 или любая IDE, поддерживающая .NET 6+.  
2. **Библиотека GroupDocs.Editor для .NET** — загрузите с [страницы выпусков GroupDocs](https://releases.groupdocs.com/editor/net/).  
3. **Временная лицензия** — получите [временную лицензию](https://purchase.groupdocs.com/temporary-license/) для неограниченного доступа.  
4. **Базовые знания C#** — знакомство с пространствами имён, инструкциями `using` и выводом в консоль.

## Как перечислить поддерживаемые форматы документов?
Загрузите коллекцию поддерживаемых форматов и выведите имя и расширение каждого формата. Этот двухшаговый шаблон работает для документов Word, Spreadsheet и Presentation. Перебирая коллекцию, вы можете динамически заполнять элементы UI, такие как выпадающие списки, гарантируя, что пользователи могут выбирать только форматы, действительно поддерживаемые редактором.

```csharp
// No actual code block – placeholder retained from original tutorial
```csharp
using System;
using GroupDocs.Editor.Options;
```
```

### Перечисление форматов обработки текста
`Formats.WordProcessingFormats` — перечисление, описывающее каждый тип файлов обработки текста, распознаваемый редактором. Свойство `All` возвращает коллекцию этих объектов форматов.

```csharp
```csharp
foreach (Formats.WordProcessingFormats oneFormat in Formats.WordProcessingFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**Объяснение:**  
1. **Перебор форматов:** Мы проходим по всем доступным форматам обработки текста.  
2. **Вывод деталей формата:** Для каждого формата мы выводим его читаемое название и расширение по умолчанию.

### Перечисление форматов презентаций
`Formats.PresentationFormats` работает аналогично для файлов презентаций, предоставляя каждый поддерживаемый тип через коллекцию `All`.

```csharp
```csharp
foreach (Formats.PresentationFormats oneFormat in Formats.PresentationFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**Объяснение:**  
1. **Перебор форматов:** Та же логика перебора применяется к презентациям.  
2. **Вывод деталей формата:** Имя и расширение отображаются для каждого формата.

## Как определить расширение формата файла?
Иногда у вас есть только имя файла, и нужно определить соответствующий `DocumentFormat`. GroupDocs.Editor предлагает простой статический помощник, который сопоставляет расширение файла его внутреннему представлению формата, позволяя проверять или конвертировать файлы до их загрузки в редактор.

### Разбор форматов электронных таблиц
`Formats.SpreadsheetFormats.FromExtension` преобразует строку расширения файла в соответствующее значение перечисления формата таблицы.

```csharp
```csharp
Formats.SpreadsheetFormats expectedXlsm = Formats.SpreadsheetFormats.FromExtension(".xlsm");
Console.WriteLine("Parsed Spreadsheet format is {0}", expectedXlsm.Name);
```
```

**Объяснение:**  
1. **Разбор формата:** `FromExtension` преобразует расширение `.xlsm` во внутреннее перечисление `SpreadsheetFormat`.  
2. **Вывод формата:** Выводится имя разобранного формата, подтверждая соответствие.

### Разбор текстовых форматов
Аналогично, `Formats.TextualFormats.FromExtension` определяет текстовые расширения, такие как HTML или TXT.

```csharp
```csharp
Formats.TextualFormats expectedHtml = Formats.TextualFormats.FromExtension("html");
Console.WriteLine("Parsed Textual format is {0}", expectedHtml.Name);
```
```

**Объяснение:**  
1. **Разбор формата:** Метод `FromExtension` определяет расширение `html` как `TextFormat`.  
2. **Вывод формата:** Отображается название текстового формата, полезное для веб‑редакторов.

## Как редактировать документы после определения форматов?
После того как вы знаете формат, загрузка и редактирование документа следуют единому шаблону. Сначала создаётся экземпляр `Editor` с путём к исходному файлу, затем вызывается `Edit()`, получая `EditableDocument`. Далее можно читать, изменять и, наконец, сохранять содержимое, используя соответствующие `SaveOptions`.

### Загрузка документа
`Editor` — основной класс, инкапсулирующий все операции редактирования для данного файла.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/document.docx"))
{
    // Further steps will be covered here.
}
```
```

**Объяснение:**  
1. **Инициализация Editor:** Создайте экземпляр `Editor`, передав полный путь к целевому файлу.  
2. **Шаблон освобождения:** Оператор `using` гарантирует своевременное освобождение всех неуправляемых ресурсов.

### Извлечение содержимого
`EditableDocument.GetContent()` возвращает необработанный текст документа (или HTML для веб‑редакторов), который можно отобразить или изменить.

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    string content = editableDocument.GetContent();
    Console.WriteLine(content);
}
```
```

**Объяснение:**  
1. **Метод Edit:** `Edit()` возвращает объект `EditableDocument`.  
2. **Получить содержимое:** `GetContent()` извлекает необработанный текст документа (или HTML для веб‑редакторов).  
3. **Вывод содержимого:** Содержимое выводится в консоль для проверки.

### Сохранение изменений
`SaveOptions` указывает редактору, как и в каком формате записать отредактированный документ обратно в хранилище.

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    // Modify content here
    SaveOptions saveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docx);
    editor.Save(editableDocument, "path/to/save/document.docx", saveOptions);
}
```
```

**Объяснение:**  
1. **Метод Edit:** Снова получаем `EditableDocument` после внесения изменений.  
2. **Изменить содержимое:** Примените изменения к строке (не показано здесь).  
3. **Параметры сохранения:** Настройте `SaveOptions` с нужным форматом вывода.  
4. **Сохранить документ:** Сохраните отредактированный файл обратно на диск.

## Как работать с различными типами документов?
GroupDocs.Editor абстрагирует работу с Word, Spreadsheet и Presentation за единым API, что упрощает переключение контекстов без необходимости изучать отдельный набор классов для каждой семейства документов.

### Редактирование документов электронных таблиц
`SpreadsheetSaveOptions` определяет, как записывается таблица, включая формат и необязательные параметры сжатия.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/spreadsheet.xlsx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // Modify content here
        SaveOptions saveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsx);
        editor.Save(editableDocument, "path/to/save/spreadsheet.xlsx", saveOptions);
    }
}
```
```

**Объяснение:**  
1. **Инициализация Editor:** Передайте путь к файлу электронной таблицы в конструктор `Editor`.  
2. **Метод Edit:** Получите `EditableDocument`.  
3. **Получить содержимое:** Выведите CSV‑представление таблицы (или HTML).  
4. **Изменить содержимое:** Примените необходимые изменения на уровне ячеек.  
5. **Параметры сохранения:** Выберите соответствующий `SpreadsheetSaveOptions`.  
6. **Сохранить документ:** Запишите обновлённую таблицу обратно в хранилище.

### Редактирование документов презентаций
`PresentationSaveOptions` управляет форматом вывода для наборов слайдов, позволяя сохранять оригинальный тип файла или менять его.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/presentation.pptx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // Modify content here
        SaveOptions saveOptions = new PresentationSaveOptions(PresentationFormats.Pptx);
        editor.Save(editableDocument, "path/to/save/presentation.pptx", saveOptions);
    }
}
```
```

**Объяснение:**  
1. **Инициализация Editor:** Загрузите файл PowerPoint через `Editor`.  
2. **Метод Edit:** Получите `EditableDocument`.  
3. **Получить содержимое:** Извлеките HTML слайдов или обычный текст.  
4. **Изменить содержимое:** Обновите заголовки, маркеры или изображения.  
5. **Параметры сохранения:** Используйте `PresentationSaveOptions` для определения формата вывода.  
6. **Сохранить документ:** Сохраните отредактированную презентацию.

## Распространённые проблемы и решения
- **Ошибка «Format not supported»:** Убедитесь, что используете последнюю версию GroupDocs.Editor; она регулярно добавляет поддержку новых форматов Office.  
- **Большое потребление памяти файлом:** Включите режим потоковой передачи, установив `EditorSettings.EnableStreaming = true` перед загрузкой документа.  
- **Лицензия не применена:** Убедитесь, что файл временной лицензии находится в корне приложения или загружен через `License license = new License(); license.SetLicense("path/to/license.lic");`.

## Часто задаваемые вопросы

**Q: В чём разница между `DocumentFormatInfo` и `SaveOptions`?**  
A: `DocumentFormatInfo` предоставляет метаданные о поддерживаемых типах файлов, тогда как `SaveOptions` настраивает, как документ будет записан обратно на диск (формат, сжатие и т.д.).

**Q: Можно ли вывести список форматов для пользовательского расширения файла?**  
A: Да — используйте `DocumentFormatInfo.FromExtension("yourExt")`; если расширение не распознано, метод вернёт `null`.

**Q: Поддерживает ли GroupDocs.Editor файлы, защищённые паролем?**  
A: Абсолютно. Передайте пароль в конструктор `Editor` через `EditorSettings`, чтобы открыть зашифрованные документы.

**Q: Сколько форматов действительно поддерживает GroupDocs.Editor?**  
A: Более **30 форматов ввода и вывода**, охватывающих Word, Excel, PowerPoint, HTML и обычный текст.

**Q: Есть ли способ ограничить список только редактируемыми форматами?**  
A: Используйте `GetEditableWordProcessingFormats()` (или эквиваленты для Spreadsheet/Presentation), чтобы получить форматы, позволяющие полное редактирование.

## Дополнительные ресурсы
- Скачайте библиотеку с [страницы выпусков GroupDocs](https://releases.groupdocs.com/editor/net/).  
- Получите [временную лицензию](https://purchase.groupdocs.com/temporary-license/) для полного доступа к функциям.  
- Попробуйте продукт с [бесплатной пробной версией](https://releases.groupdocs.com/).  
- Изучите подробные примеры использования в [документации GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/).  
- Получите помощь от сообщества на [форуме поддержки](https://forum.groupdocs.com/c/editor/20).

## Заключение
Следуя этому руководству, вы теперь знаете, как **перечислять поддерживаемые форматы документов**, **определять формат файла по его расширению** и **редактировать документы** в форматах Word, Spreadsheet и Presentation с помощью GroupDocs.Editor для .NET. Внедрите эти фрагменты кода в свои проекты, чтобы создавать надёжные, ориентированные на форматы приложения, радующие конечных пользователей и снижающие количество ошибок выполнения.

---

**Последнее обновление:** 2026-06-06  
**Тестировано с:** GroupDocs.Editor 23.9 for .NET  
**Автор:** GroupDocs

## Связанные руководства

- [Освоение загрузки документов в .NET с GroupDocs.Editor: Полное руководство](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)  
- [Мастер‑редактирование документов в .NET с GroupDocs.Editor: Полное руководство](/editor/net/document-editing/master-document-editing-dotnet-groupdocs-editor/)  
- [Конвертация Word в HTML с помощью GroupDocs.Editor .NET: Пошаговое руководство](/editor/net/document-saving/convert-word-to-html-groupdocs-editor-dotnet/)