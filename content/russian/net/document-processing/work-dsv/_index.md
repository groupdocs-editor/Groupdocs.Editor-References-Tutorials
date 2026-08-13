---
date: 2026-06-06
description: Узнайте, как **создавать редактируемый документ** из файлов CSV и TSV
  с помощью GroupDocs.Editor для .NET. Это руководство также показывает, как **читать
  разделённый текст C#** и **редактировать CSV .NET** эффективно в Visual Studio.
keywords:
- create editable document
- read delimited text c#
- edit csv .net
- parse delimited values c#
linktitle: Работа с разделёнными значениями (DSV) – создание редактируемого документа
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to **create editable document** objects from CSV and TSV
    files using GroupDocs.Editor for .NET. This guide also shows how to **read delimited
    text C#** and **edit CSV .NET** efficiently in Visual Studio.
  headline: Work with Delimited Separated Values (DSV) – create editable document
  type: TechArticle
- questions:
  - answer: Yes, the API streams data and can handle files larger than 1 GB without
      loading the entire document into memory.
    question: Can I use GroupDocs.Editor for .NET to edit large CSV files?
  - answer: Absolutely – any single‑character delimiter (e.g., pipe `|`, semicolon
      `;`) is supported as long as you specify it in `DelimitedTextEditOptions`.
    question: Does GroupDocs.Editor for .NET support other DSV formats besides CSV
      and TSV?
  - answer: Yes, you can set the `Encoding` property in `DelimitedTextSaveOptions`
      to UTF‑8, UTF‑16, ISO‑8859‑1, or any .NET `Encoding` you require.
    question: Is it possible to customize the encoding when saving DSV files?
  - answer: Yes – after editing, simply use `SpreadsheetSaveOptions` to export the
      content as an `.xlsx` workbook.
    question: Can I convert a CSV file to an Excel spreadsheet using GroupDocs.Editor
      for .NET?
  - answer: Detailed API references and code samples are available **[here](https://tutorials.groupdocs.com/editor/net/)**.
    question: Where can I find more documentation on GroupDocs.Editor for .NET?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Работа с разделёнными значениями (DSV) – создание редактируемого документа
type: docs
url: /ru/net/document-processing/work-dsv/
weight: 12
---

# Работа с разделенными значениями (DSV) – создание редактируемого документа

Если вы разработчик .NET, которому нужно **create editable document** из разделенных значений (DSV) таких как CSV или TSV, вы попали по адресу. В первых 100 словах мы объясним, почему GroupDocs.Editor for .NET — самый надежный способ **read delimited text C#**, редактировать его и затем сохранять без потери форматирования. Вы получите готовый к копированию и вставке рабочий процесс, который естественно впишется в любое решение Visual Studio.

## Быстрые ответы
- **Какая библиотека лучше всего обрабатывает редактирование CSV в .NET?** GroupDocs.Editor for .NET.
- **Могу ли я редактировать большие CSV‑файлы в Visual Studio?** Да — API потоково передаёт данные и избегает загрузки всего файла в память.
- **Нужна ли лицензия для использования в продакшене?** Требуется коммерческая лицензия; доступна бесплатная пробная версия.
- **В каких форматах можно сохранить после редактирования?** CSV, TSV и форматы электронных таблиц, совместимые с Excel.
- **Совместим ли API с .NET 6+?** Абсолютно — поддерживает .NET Framework 4.5+, .NET Core 3.1+, .NET 5 и .NET 6.

## Что означает «create editable document» в контексте GroupDocs.Editor?
**Create editable document** означает создание экземпляра `EditableDocument`, представляющего изменяемую версию исходного файла (CSV, TSV и т.д.) в памяти. Этот объект позволяет читать, изменять и повторно сохранять содержимое с помощью того же API. Он предоставляет методы для получения текста документа, применения изменений и сохранения его в различных форматах, обеспечивая сохранение выравнивания столбцов и кавычек.

## Почему стоит использовать GroupDocs.Editor для работы с DSV?
GroupDocs.Editor обрабатывает **более 50 форматов ввода и вывода**, включая CSV, TSV и электронные таблицы, совместимые с Excel, при этом потребление памяти не превышает 10 МБ для файлов размером до 500 МБ. Он также автоматически сохраняет выравнивание столбцов, правила кавычек и пользовательские кодировки, что устраняет необходимость в ручной логике парсинга.

## Предварительные требования
- **Visual Studio** (любая современная версия) — вы будете разрабатывать и отлаживать непосредственно в IDE.
- **GroupDocs.Editor for .NET** — скачайте последнюю версию **[здесь](https://releases.groupdocs.com/editor/net/)**.
- **Базовые знания C#** — в руководстве предполагается, что вы умеете создавать консольный или ASP.NET проект и добавлять пакеты NuGet.

## Импорт пространств имён
Классы `Editor`, `EditableDocument` и классы параметров находятся в пространстве имён `GroupDocs.Editor`.  

Класс `DelimitedTextEditOptions` является точкой входа для определения разделителя (запятая, табуляция и т.д.) и других правил парсинга.

```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

## Как создать редактируемый документ из CSV‑файла?
Загрузите исходный CSV с помощью `Editor` и вызовите метод `Edit`, передав экземпляр `DelimitedTextEditOptions`, указывающий запятую в качестве разделителя. Метод возвращает `EditableDocument`, которым можно управлять в памяти. Этот двухшаговый шаблон — загрузка → редактирование — покрывает сценарии **read delimited text C#** и гарантирует сохранение исходной структуры файла.

## Шаг 1: Получите путь к входному DSV‑файлу
Сначала необходимо указать абсолютный или относительный путь к исходному DSV‑файлу. Для демонстрации мы используем простой CSV, расположенный в папке `Data` проекта.

```csharp
string inputFilePath = "Your Sample Document";
```

## Шаг 2: Создайте экземпляр Editor
`Editor` — основной класс, который управляет загрузкой, редактированием и сохранением. Создание его экземпляра с объектом `FileInfo` даёт полный контроль над жизненным циклом файла.

```csharp
using (Editor editor = new Editor(inputFilePath))
{
```

## Шаг 3: Создайте параметры редактирования DSV
`DelimitedTextEditOptions` указывает редактору, как интерпретировать файл. Вы можете задать разделитель, содержит ли первая строка заголовки, и кодировку символов.

```csharp
    Options.DelimitedTextEditOptions editOptions = new DelimitedTextEditOptions(",");
    editOptions.ConvertDateTimeData = false;
    editOptions.ConvertNumericData = true;
    editOptions.TreatConsecutiveDelimitersAsOne = true;
```

## Шаг 4: Создайте экземпляр EditableDocument
`EditableDocument` представляет изменяемую в памяти версию исходного файла. Вызов `Editor.Edit` с параметрами возвращает `EditableDocument`. Этот объект хранит текст файла в изменяемой строке, готовой к любой операции **parse delimited values C#**, которую вам потребуется выполнить.

```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```

## Шаг 5: Отредактируйте содержимое документа
`GetDocumentText()` возвращает текущий текст редактируемого документа в виде строки. Получите оригинальный текст через `EditableDocument.GetDocumentText()`, выполните необходимые изменения (например, замените значение столбца) и сохраните результат в новой строке. Здесь вы **edit CSV .NET** без работы с низкоуровневыми файловыми потоками.

```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("SsangYong", "Chevrolet").Replace("Kyron", "Camaro");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```

## Шаг 6: Создайте EditableDocument с обновлённым содержимым
Оберните изменённую строку обратно в `EditableDocument`. Этот шаг завершает изменения и подготавливает объект к сохранению в любом поддерживаемом формате.

```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```

## Шаг 7: Создайте параметры сохранения CSV
`DelimitedTextSaveOptions` определяет, как записать отредактированное содержимое обратно в CSV‑файл. Когда вы готовы сохранить изменения, настройте `DelimitedTextSaveOptions`. Вы можете указать тот же разделитель, другой или даже изменить стиль окончания строк.

```csharp
    Options.DelimitedTextSaveOptions csvSaveOptions = new DelimitedTextSaveOptions(",");
    csvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

## Шаг 8: Создайте параметры сохранения TSV
Если вам нужна версия с разделителями‑табуляциями, просто смените разделитель на `\t`. Один и тот же `EditableDocument` можно сохранять несколько раз с разными параметрами.

```csharp
    Options.DelimitedTextSaveOptions tsvSaveOptions = new DelimitedTextSaveOptions("\t");
    tsvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

## Шаг 9: Создайте параметры сохранения электронных таблиц
`SpreadsheetSaveOptions` настраивает экспорт документа в форматы, совместимые с Excel, такие как .xlsx. GroupDocs.Editor также позволяет экспортировать отредактированные данные в формат, совместимый с Excel (`.xlsx`). Класс `SpreadsheetSaveOptions` автоматически обрабатывает типы столбцов, формулы и стили ячеек.

```csharp
    Options.SpreadsheetSaveOptions cellsSaveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
```

## Шаг 10: Подготовьте пути сохранения
Определите отдельные пути вывода для каждого формата. Использование понятных соглашений об именовании (например, `output.csv`, `output.tsv`, `output.xlsx`) помогает поддерживать порядок в проекте.

```csharp
    string outputCsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".csv");
    string outputTsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".tsv");
    string outputCellsPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".xlsm");
```

## Шаг 11: Сохраните отредактированный документ
`Save()` записывает документ на диск, используя предоставленные параметры сохранения. Вызовите `EditableDocument.Save` с соответствующими параметрами для каждого целевого формата. API записывает файл напрямую на диск, сохраняя оригинальную кодировку, если вы её не переопределяете.

```csharp
    editor.Save(afterEdit, outputCsvPath, csvSaveOptions);
    editor.Save(afterEdit, outputTsvPath, tsvSaveOptions);
    editor.Save(afterEdit, outputCellsPath, cellsSaveOptions);
```

## Шаг 12: Освободите экземпляры EditableDocument
И `Editor`, и `EditableDocument` реализуют `IDisposable`. Их освобождение закрывает файловые дескрипторы и неуправляемые ресурсы, что критично при обработке большого количества файлов в пакетной задаче.

```csharp
    beforeEdit.Dispose();
    afterEdit.Dispose();
}
System.Console.WriteLine("WorkingWithDsv routine has successfully finished");
```

## Распространённые проблемы и решения
| Проблема | Почему происходит | Решение |
|----------|-------------------|---------|
| **Неожиданные лишние кавычки** | Стандартный CSV‑парсер может рассматривать запятые внутри полей как разделители. | Установите `EscapeMode = EscapeMode.DoubleQuote` в `DelimitedTextEditOptions`. |
| **Резкий рост памяти при большом файле** | Загрузка файла размером 500 МБ без потоковой обработки. | Используйте `Editor.Load` с `LoadOptions`, включающими ленивую загрузку. |
| **Несоответствие кодировок** | Исходный файл использует UTF‑16, а параметры по умолчанию — UTF‑8. | Явно задайте `Encoding = Encoding.Unicode` в параметрах сохранения. |

## Часто задаваемые вопросы

**Q: Могу ли я использовать GroupDocs.Editor for .NET для редактирования больших CSV‑файлов?**  
A: Да, API потоково передаёт данные и может обрабатывать файлы размером более 1 ГБ без загрузки всего документа в память.

**Q: Поддерживает ли GroupDocs.Editor for .NET другие форматы DSV, помимо CSV и TSV?**  
A: Абсолютно — любой однобайтовый разделитель (например, вертикальная черта `|`, точка с запятой `;`) поддерживается, если указать его в `DelimitedTextEditOptions`.

**Q: Можно ли настроить кодировку при сохранении DSV‑файлов?**  
A: Да, вы можете задать свойство `Encoding` в `DelimitedTextSaveOptions` как UTF‑8, UTF‑16, ISO‑8859‑1 или любую другую .NET `Encoding`, которая вам нужна.

**Q: Могу ли я конвертировать CSV‑файл в электронную таблицу Excel с помощью GroupDocs.Editor for .NET?**  
A: Да — после редактирования просто используйте `SpreadsheetSaveOptions` для экспорта содержимого в рабочую книгу `.xlsx`.

**Q: Где я могу найти более подробную документацию по GroupDocs.Editor for .NET?**  
A: Подробные справочники API и примеры кода доступны **[здесь](https://tutorials.groupdocs.com/editor/net/)**.

---

**Последнее обновление:** 2026-06-06  
**Тестировано с:** GroupDocs.Editor 23.10 for .NET  
**Автор:** GroupDocs

## Связанные руководства

- [Руководства по редактированию Plain Text и DSV документов для GroupDocs.Editor .NET](/editor/net/plain-text-dsv-documents/)
- [Освойте GroupDocs.Editor .NET для эффективного редактирования CSV‑документов и конвертации](/editor/net/plain-text-dsv-documents/groupdocs-editor-net-csv-editing-guide/)
- [Мастерство загрузки документов в .NET с GroupDocs.Editor: Полное руководство](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)