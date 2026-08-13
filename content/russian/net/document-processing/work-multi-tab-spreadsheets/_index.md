---
date: 2026-06-06
description: Узнайте, как **сохранить каждый лист Excel** с помощью GroupDocs.Editor
  для .NET — пошаговое руководство, примеры кода и лучшие практики по разбиению файлов
  XLSX.
keywords:
- save each excel tab
- read multiple sheets
- convert excel tab pdf
- split xlsx files
linktitle: Работа с таблицами с несколькими листами
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to **save each Excel tab** using GroupDocs.Editor for .NET
    – step‑by‑step guide, code snippets, and best practices for splitting XLSX files.
  headline: How to save each Excel tab with GroupDocs.Editor .NET
  type: TechArticle
- description: Learn how to **save each Excel tab** using GroupDocs.Editor for .NET
    – step‑by‑step guide, code snippets, and best practices for splitting XLSX files.
  name: How to save each Excel tab with GroupDocs.Editor .NET
  steps:
  - name: Get a Path to the Input File
    text: First, specify the full path to the source XLSX that contains multiple tabs.
  - name: Load the Spreadsheet into the Editor Instance
    text: The `Editor` class is the entry point for all document operations in GroupDocs.Editor.
      It reads the file stream and prepares the document for editing or extraction.
  - name: Create an EditableDocument from the First Tab
    text: '`EditableDocument` represents a single, editable sheet within the workbook.
      The constructor takes the `Editor` instance and a zero‑based sheet index.'
  - name: Create an EditableDocument from the Second Tab
    text: You can repeat the same pattern for any additional sheet by changing the
      index value.
  - name: Save the First Tab to a Separate Document
    text: '`Save` writes the edited document to a file in the specified format. Call
      it on the `EditableDocument` instance, providing the output path and format
      (e.g., `SaveFormat.Xlsx`).'
  - name: Save the Second Tab to a Separate Document
    text: The same `Save` call works for the second sheet, and you can choose a different
      format such as PDF if needed.
  - name: Dispose of EditableDocument Instances
    text: '`Dispose` releases unmanaged resources held by the document, such as file
      handles, ensuring no leaks in long‑running services.'
  type: HowTo
- questions:
  - answer: Hidden sheets are treated like any other sheet; you can access them by
      index and save them, but you may need to set `EditableDocument.IsVisible = true`
      before saving if you want them visible in the output.
    question: What if my workbook contains hidden sheets?
  - answer: Yes, specify `SaveFormat.Pdf` when calling `Save` on the `EditableDocument`.
      The library preserves layout, images, and charts during conversion.
    question: Can I convert an Excel tab directly to PDF?
  - answer: Absolutely. Use `SaveFormat.Csv` for each `EditableDocument` to generate
      plain‑text CSV representations of each sheet.
    question: Is it possible to split a workbook into CSV files instead of XLSX?
  - answer: It does. Provide the password via `LoadOptions.Password` when creating
      the `Editor` instance.
    question: Does GroupDocs.Editor support password‑protected Excel files?
  - answer: The official documentation and sample projects on the [download page](https://releases.groupdocs.com/editor/net/)
      contain additional use‑cases.
    question: Where can I find more examples of working with spreadsheets?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Как сохранить каждый лист Excel с помощью GroupDocs.Editor .NET
type: docs
url: /ru/net/document-processing/work-multi-tab-spreadsheets/
weight: 17
---

# Работа с многостраничными электронными таблицами

## Введение
Если вам нужно **сохранить каждую вкладку Excel** как отдельный файл, GroupDocs.Editor для .NET делает это без усилий. Независимо от того, извлекаете ли вы финансовые отчёты, создаёте листы для отдельных отделов или конвертируете вкладки в PDF, этот учебник проведёт вас через весь процесс — от настройки окружения до освобождения ресурсов — чтобы вы могли автоматизировать работу с несколькими листами с уверенностью.

## Быстрые ответы
- **Может ли GroupDocs.Editor разделить XLSX на отдельные файлы?** Да, вы можете загрузить книгу и экспортировать каждый лист отдельно.  
- **В каких форматах можно сохранять каждую вкладку?** XLSX, CSV, PDF, HTML и другие — поддерживается более 30 форматов вывода.  
- **Нужна ли лицензия для этой функции?** Временная лицензия подходит для тестирования; для продакшн‑использования требуется полная лицензия.  
- **Поддерживается ли .NET Core?** Абсолютно — библиотека работает с .NET Framework 4.0+ и .NET Core/5/6+.  
- **Сколько вкладок можно обрабатывать одновременно?** GroupDocs.Editor может работать с книгами, содержащими более 500 листов, без загрузки всего файла в память.

## Что означает «сохранить каждую вкладку Excel»?
**«Сохранить каждую вкладку Excel»** означает извлечение каждого листа из многостраничной книги и запись каждого в отдельный автономный документ (например, отдельные файлы XLSX или PDF). Такой подход упрощает последующую обработку, отчётность и распространение, предоставляя вам файл для каждого листа, который затем можно делиться, архивировать или дальше преобразовывать независимо.

## Почему стоит использовать GroupDocs.Editor для этой задачи?
GroupDocs.Editor поддерживает **более 30 форматов ввода и вывода** и может обрабатывать электронные таблицы с **до 1 000 листов**, при этом экономя память за счёт потоковой передачи данных вместо загрузки всего файла. API также сохраняет стили ячеек, формулы и встроенные изображения, гарантируя, что каждая экспортированная вкладка выглядит точно так же, как оригинал.

## Предварительные требования
Прежде чем приступать, убедитесь, что у вас есть:

1. **Visual Studio** — любой современный выпуск (Community, Professional или Enterprise).  
2. **.NET Framework 4.0+** — или .NET Core/5/6, если вы предпочитаете кроссплатформенный рантайм.  
3. **GroupDocs.Editor for .NET** — скачайте его со [страницы загрузки](https://releases.groupdocs.com/editor/net/).  
4. **Лицензия** — [временная лицензия](https://purchase.groupdocs.com/temporary-license/) подходит для тестирования; для продакшн‑использования приобретите полную лицензию.  
5. **Бесплатный пробный период** — вы также можете попробовать библиотеку через страницу [бесплатного пробного периода](https://releases.groupdocs.com/).  
6. **Поддержка** — если возникнут проблемы, посетите [форум поддержки](https://forum.groupdocs.com/c/editor/20) или рассмотрите [страницу покупки](https://purchase.groupdocs.com/buy) для полной лицензии.

## Импорт пространств имён
Перед тем как начать писать код, необходимо импортировать нужные пространства имён. Добавьте следующие директивы using в начало вашего файла `.cs`:

```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```

## Как сохранить каждую вкладку Excel в отдельный файл?
Загрузите книгу, создайте `EditableDocument` для каждого листа и вызовите `Save` с нужным форматом. Этот процесс изолирует каждую вкладку, позволяет выбрать отдельный путь вывода и автоматически освобождает ресурсы. Ниже представлен пошаговый рабочий процесс с объяснениями каждого вызова API и рекомендациями по лучшим практикам, чтобы избежать распространённых проблем.

### Шаг 1: Получить путь к входному файлу
Сначала укажите полный путь к исходному файлу XLSX, содержащему несколько вкладок.

```csharp
string inputFilePath = "Your Sample Document";
```

### Шаг 2: Загрузить электронную таблицу в экземпляр Editor
Класс `Editor` является точкой входа для всех операций с документами в GroupDocs.Editor. Он читает поток файла и подготавливает документ для редактирования или извлечения.

```csharp
using (FileStream inputStream = File.OpenRead(inputFilePath))
{
    using (Editor editor = new Editor(delegate { return inputStream; }, delegate { return new SpreadsheetLoadOptions(); }))
    {
        // Further steps will go here
    }
}
```

### Шаг 3: Создать EditableDocument из первой вкладки
`EditableDocument` представляет один редактируемый лист в книге. Конструктор принимает экземпляр `Editor` и индекс листа, начинающийся с нуля.

```csharp
SpreadsheetEditOptions editOptions1 = new SpreadsheetEditOptions();
editOptions1.WorksheetIndex = 0; // First tab
EditableDocument firstTabBeforeEdit = editor.Edit(editOptions1);
```

### Шаг 4: Создать EditableDocument из второй вкладки
Вы можете повторить тот же шаблон для любого другого листа, изменив значение индекса.

```csharp
SpreadsheetEditOptions editOptions2 = new SpreadsheetEditOptions();
editOptions2.WorksheetIndex = 1; // Second tab
EditableDocument secondTabBeforeEdit = editor.Edit(editOptions2);
```

### Шаг 5: Сохранить первую вкладку в отдельный документ
`Save` записывает отредактированный документ в файл в указанном формате. Вызовите его у экземпляра `EditableDocument`, указав путь вывода и формат (например, `SaveFormat.Xlsx`).

```csharp
SpreadsheetSaveOptions saveOptions1 = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
string outputFilename1 = Path.GetFileNameWithoutExtension(inputFilePath) + "_tab1.xlsm";
string outputPath1 = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename1);
editor.Save(firstTabBeforeEdit, outputPath1, saveOptions1);
```

### Шаг 6: Сохранить вторую вкладку в отдельный документ
Тот же вызов `Save` работает для второго листа, и при необходимости вы можете выбрать другой формат, например PDF.

```csharp
SpreadsheetSaveOptions saveOptions2 = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsb);
string outputFilename2 = Path.GetFileNameWithoutExtension(inputFilePath) + "_tab2.xlsb";
string outputPath2 = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename2);
editor.Save(secondTabBeforeEdit, outputPath2, saveOptions2);
```

### Шаг 7: Освободить экземпляры EditableDocument
`Dispose` освобождает неуправляемые ресурсы, связанные с документом, такие как файловые дескрипторы, гарантируя отсутствие утечек в длительно работающих сервисах.

```csharp
firstTabBeforeEdit.Dispose();
secondTabBeforeEdit.Dispose();
```

## Распространённые проблемы и решения
- **Ошибка «Файл заблокирован»** — Убедитесь, что вызываете `Dispose()` у каждого `EditableDocument` и у экземпляра `Editor`, либо оберните их в конструкции `using`.  
- **Отсутствие стилей после экспорта** — Убедитесь, что сохраняете в формат, поддерживающий стили (например, XLSX или PDF). CSV по‑умолчанию теряет форматирование.  
- **Большие книги вызывают медленную работу** — Используйте опцию потоковой загрузки (`LoadOptions.Streaming = true`), чтобы снизить потребление памяти.

## Часто задаваемые вопросы

**Q: Что если моя книга содержит скрытые листы?**  
A: Скрытые листы обрабатываются как любые другие; вы можете получить к ним доступ по индексу и сохранить, но возможно понадобится установить `EditableDocument.IsVisible = true` перед сохранением, если хотите, чтобы они были видимыми в результате.

**Q: Можно ли напрямую конвертировать вкладку Excel в PDF?**  
A: Да, укажите `SaveFormat.Pdf` при вызове `Save` у `EditableDocument`. Библиотека сохраняет макет, изображения и диаграммы при конвертации.

**Q: Возможно ли разделить книгу на CSV‑файлы вместо XLSX?**  
A: Абсолютно. Используйте `SaveFormat.Csv` для каждого `EditableDocument`, чтобы получить текстовые CSV‑представления каждого листа.

**Q: Поддерживает ли GroupDocs.Editor Excel‑файлы, защищённые паролем?**  
A: Да. Укажите пароль через `LoadOptions.Password` при создании экземпляра `Editor`.

**Q: Где я могу найти больше примеров работы с электронными таблицами?**  
A: Официальная документация и примеры проектов на [странице загрузки](https://releases.groupdocs.com/editor/net/) содержат дополнительные сценарии использования.

## Заключение
Следуя этим шагам, вы сможете **сохранить каждую вкладку Excel** как отдельный документ, конвертировать вкладки в PDF или разбить большие книги на управляемые части — всё это с надёжной, высокопроизводительной библиотекой GroupDocs.Editor для .NET. Эта возможность упрощает конвейеры отчётности, автоматизирует извлечение данных и уменьшает ручную работу с электронными таблицами.

---

**Последнее обновление:** 2026-06-06  
**Тестировано с:** GroupDocs.Editor 23.11 for .NET  
**Автор:** GroupDocs  

---

## Связанные руководства

- [Мастерство извлечения вкладок электронных таблиц в .NET с GroupDocs.Editor](/editor/net/spreadsheet-documents/mastering-spreadsheet-tab-extraction-dotnet-groupdocs-editor/)
- [Защита паролем файлов Excel с помощью GroupDocs.Editor для .NET | Управление безопасностью электронных таблиц](/editor/net/spreadsheet-documents/groupdocs-editor-net-password-excel-files/)
- [Мастерство загрузки документов в .NET с GroupDocs.Editor: Полное руководство](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)