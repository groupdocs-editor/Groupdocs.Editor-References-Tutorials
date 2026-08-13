---
date: 2026-06-01
description: Узнайте, как получить количество страниц и извлечь метаданные документа
  с помощью GroupDocs.Editor для .NET в подробном пошаговом руководстве.
keywords:
- get page count
- extract document metadata
- get document info
- find document extension
- retrieve document size
linktitle: Получить количество страниц и извлечь информацию о документе
schemas:
- author: GroupDocs
  dateModified: '2026-06-01'
  description: Learn how to get page count and extract document metadata using GroupDocs.Editor
    for .NET in a detailed step‑by‑step tutorial.
  headline: Get Page Count & Extract Document Info with GroupDocs.Editor
  type: TechArticle
- questions:
  - answer: GroupDocs.Editor supports Word processing, spreadsheet, presentation,
      PDF, and plain‑text files—over 50 formats in total.
    question: What document types can I extract metadata from?
  - answer: Access `DocumentInfo.Extension` after calling `GetDocumentInfo()`; it
      returns the extension without the leading dot.
    question: How do I retrieve the file extension?
  - answer: Yes—`DocumentInfo.Size` returns the size in bytes; divide by 1,048,576
      to convert to megabytes.
    question: Can I get the size of a document in megabytes?
  - answer: Absolutely—GroupDocs.Editor never writes the password to disk and disposes
      of all cryptographic objects after use.
    question: Is it safe to process password‑protected files on a server?
  - answer: You can get support from the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).
    question: Where can I find additional help if I run into issues?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Получить количество страниц и извлечь информацию о документе с GroupDocs.Editor
type: docs
url: /ru/net/document-processing/extract-document-info/
weight: 10
---

# Получить количество страниц и извлечь информацию о документе с GroupDocs.Editor

## Введение
В этом всестороннем руководстве вы узнаете, как **получить количество страниц** и извлечь подробную информацию о документе — включая формат, размер и статус шифрования — с помощью GroupDocs.Editor для .NET. Независимо от того, создаёте ли вы систему управления документами, движок отчётности или автоматизированный конвейер конвертации, понимание метаданных файла — первый шаг к надёжной обработке. Давайте пройдем весь рабочий процесс, от загрузки файла до безопасного освобождения ресурсов.

## Быстрые ответы
- **Как получить количество страниц документа?**  
  Вызовите `editor.GetDocumentInfo().PageCount` после загрузки файла с помощью `Editor`.
- **Какие форматы файлов поддерживаются для извлечения метаданных?**  
  Более 50 форматов, включая DOCX, XLSX, PPTX, PDF, TXT и HTML.
- **Можно ли извлекать метаданные из файлов, защищённых паролем?**  
  Да — укажите пароль при создании экземпляра `Editor`.
- **Нужно ли вручную освобождать ресурсы?**  
  Абсолютно; всегда вызывайте `editor.Dispose()` или оборачивайте редактор в блок `using`.
- **Какая версия GroupDocs.Editor требуется?**  
  Последний стабильный релиз (v23.12+ на момент написания) поддерживает все показанные функции.

## Что такое «получить количество страниц» в GroupDocs.Editor?
`GetDocumentInfo()` — метод, возвращающий объект `DocumentInfo`, содержащий количество страниц, формат, размер и другие метаданные документа. Этот единственный вызов даёт мгновенное представление без ручного парсинга файла. Используя этот метод, вы избегаете загрузки всего документа в память, что повышает производительность, особенно для больших файлов, и снижает нагрузку на серверные ресурсы.

## Почему стоит извлекать метаданные документа с GroupDocs.Editor?
GroupDocs.Editor может обрабатывать **более 50 входных и выходных форматов** и получать метаданные файлов до **2 ГБ** без полной загрузки документа в память. Такая эффективность снижает нагрузку на сервер до **70 %** по сравнению с полным парсингом документа, что делает её идеальной для приложений с высоким пропускным способностью.

## Предварительные требования
Перед началом убедитесь, что у вас есть:

- **Базовые навыки разработки на C#** — вы должны уверенно работать с Visual Studio и структурами проектов .NET.
- **Visual Studio 2022** (или более свежая версия), установленная на вашем компьютере.
- **GroupDocs.Editor for .NET** — скачайте последний пакет со [страницы загрузки](https://releases.groupdocs.com/editor/net/).

## Как загрузить ваш документ?
`Editor` — основной класс, представляющий документ и предоставляющий методы для его загрузки и манипуляций. Загрузите целевой файл, создав экземпляр `Editor` и передав путь к файлу. Редактор автоматически определяет формат, поэтому указывать параметры загрузки не требуется. Такой подход работает с любым поддерживаемым типом файла и упрощает начальную настройку.

```csharp
using System;
using GroupDocs.Editor.Metadata;
```

## Как получить информацию о документе?
`GetDocumentInfo()` возвращает объект `DocumentInfo`, содержащий метаданные такие как количество страниц, формат, размер и статус шифрования. После загрузки вызовите этот метод, чтобы получить объект. Возвращаемый `DocumentInfo` предоставляет краткий снимок характеристик файла, позволяя принимать решения без дальнейшей обработки.

```csharp
string docxInputFilePath = "YourSampleDocument.docx";
Editor editorDocx = new Editor(docxInputFilePath);
```

## Как определить тип документа?
`DocumentType` — перечисление, указывающее, является ли документ WordProcessing, Spreadsheet или Text. Знание того, является ли файл документом обработки текста, таблицей или простым текстом, влияет на последующую обработку. Используйте свойство `DocumentType` объекта `DocumentInfo`, чтобы принять решение и ветвить логику соответственно.

```csharp
IDocumentInfo infoDocx = editorDocx.GetDocumentInfo(null);
```

## Как извлечь подробную информацию для файлов обработки текста?
`WordProcessing` относится к документам типа DOCX, ODT и RTF, обрабатываемым как файлы обработки текста. Если тип документа — `WordProcessing`, вы можете прочитать дополнительные свойства, такие как **format**, **extension**, **page count**, **size** и **encryption flag**, напрямую из объекта `DocumentInfo`. Эти детали помогают адаптировать шаги обработки, например, применять специфические конвертации или проверки безопасности.

```csharp
bool isSpreadsheet = infoDocx is SpreadsheetDocumentInfo;
bool isText = infoDocx is TextualDocumentInfo;
bool isWordProcessing = infoDocx is WordProcessingDocumentInfo;
Console.WriteLine($"Is '{docxInputFilePath}' a Spreadsheet: {isSpreadsheet}");
Console.WriteLine($"Is '{docxInputFilePath}' a Textual document: {isText}");
Console.WriteLine($"Is '{docxInputFilePath}' a WordProcessing document: {isWordProcessing}");
```

## Как работать с таблицами и текстовыми документами?
`Spreadsheet` обозначает таблицы, такие как XLSX, а `Text` представляет простые текстовые документы. Для таблиц (`Spreadsheet`) и простых текстовых файлов (`Text`) объект `DocumentInfo` всё равно предоставляет основные метаданные (расширение, размер, количество страниц). Некоторые форматы могут не содержать информации о количестве страниц, в этом случае значение будет `0`. Вы всё равно можете опираться на другие метаданные для дальнейшей логики.

```csharp
if (isWordProcessing)
{
    WordProcessingDocumentInfo casted = (WordProcessingDocumentInfo)infoDocx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Page count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```

## Как работать с документами, защищёнными паролем?
`Password` — строка, передаваемая конструктору `Editor` для открытия зашифрованных файлов. Когда документ зашифрован, сначала попытайтесь открыть его без пароля. Если это не удаётся, перехватите исключение и повторите попытку с правильным паролем. Конструктор `Editor` принимает параметр `Password` для этой цели, обеспечивая бесшовную работу с защищёнными файлами.

```csharp
string xlsxInputFilePath = "YourSampleDocument.xlsx";
Editor editorXlsx = new Editor(xlsxInputFilePath);
IDocumentInfo infoXlsx = editorXlsx.GetDocumentInfo(null);
bool isXlsxSpreadsheet = infoXlsx is SpreadsheetDocumentInfo;
Console.WriteLine($"Is '{xlsxInputFilePath}' a Spreadsheet: {isXlsxSpreadsheet}");
if (isXlsxSpreadsheet)
{
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo)infoXlsx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Tabs count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```

## Как обрабатывать документы, основанные на тексте?
`DocumentInfo` предоставляет базовые метаданные, такие как размер, расширение и кодировка для текстовых файлов. Текстовые файлы (например, `.txt`, `.md`) рассматриваются как простые потоки. Вы всё ещё можете получить информацию о размере и кодировке из `DocumentInfo`, что полезно для проверки целостности файла или определения подходящего конвейера обработки.

```csharp
string xlsInputFilePath = "YourSampleDocument.xls";
Editor editorXls = new Editor(xlsInputFilePath);
try
{
    IDocumentInfo infoXls = editorXls.GetDocumentInfo(null);
}
catch (PasswordRequiredException)
{
    Console.WriteLine("This document is password-protected.");
}
try
{
    IDocumentInfo infoXls = editorXls.GetDocumentInfo("incorrect_password");
}
catch (IncorrectPasswordException)
{
    Console.WriteLine("The provided password is incorrect.");
}
IDocumentInfo infoXlsValid = editorXls.GetDocumentInfo("correct_password");
bool isXlsSpreadsheet = infoXlsValid is SpreadsheetDocumentInfo;
Console.WriteLine($"Password-protected document is a Spreadsheet: {isXlsSpreadsheet}");
if (isXlsSpreadsheet)
{
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo)infoXlsValid;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Tabs count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```

## Как правильно освобождать ресурсы?
`Editor` — основной класс, который держит неуправляемые ресурсы и должен быть освобождён после использования. Чтобы избежать утечек памяти, всегда освобождайте экземпляр `Editor` после завершения извлечения информации. Оператор `using` — самый безопасный шаблон, так как он гарантирует освобождение даже при возникновении исключения, обеспечивая чистое управление ресурсами.

```csharp
string xmlInputFilePath = "YourSampleDocument.xml";
Editor editorXml = new Editor(xmlInputFilePath);
IDocumentInfo infoXml = editorXml.GetDocumentInfo(null);
bool isXmlText = infoXml is TextualDocumentInfo;
Console.WriteLine($"Is '{xmlInputFilePath}' a Textual document: {isXmlText}");
if (isXmlText)
{
    TextualDocumentInfo casted = (TextualDocumentInfo)infoXml;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Encoding: {casted.Encoding}; Size: {casted.Size} bytes");
}
```

## Распространённые проблемы и решения
| Проблема | Причина | Решение |
|----------|---------|----------|
| **PageCount возвращает 0** | Формат не поддерживает пагинацию (например, простой текст) | Проверьте `DocumentInfo.DocumentType` перед использованием `PageCount`. |
| **Неподдерживаемый формат файла** | Расширение файла не распознано | Убедитесь, что файл относится к более чем 50 поддерживаемым форматам; обновите GroupDocs.Editor до последней версии. |
| **Исключение пароля** | Указан неверный пароль | Перехватите `PasswordProtectedException` и предложите пользователю ввести пароль повторно. |
| **Резкое увеличение памяти при больших файлах** | Загрузка очень больших PDF без потоковой передачи | Используйте `LoadOptions` с `LoadOptions.LoadMode = LoadMode.Stream` (доступно в новых релизах). |

## Часто задаваемые вопросы

**В: Какие типы документов я могу извлекать метаданные?**  
О: GroupDocs.Editor поддерживает документы обработки текста, таблицы, презентации, PDF и простые текстовые файлы — более 50 форматов в общей сложности.

**В: Как получить расширение файла?**  
О: Обратитесь к `DocumentInfo.Extension` после вызова `GetDocumentInfo()`; возвращается расширение без ведущей точки.

**В: Можно ли получить размер документа в мегабайтах?**  
О: Да — `DocumentInfo.Size` возвращает размер в байтах; разделите на 1 048 576 для преобразования в мегабайты.

**В: Безопасно ли обрабатывать файлы, защищённые паролем, на сервере?**  
О: Абсолютно — GroupDocs.Editor никогда не записывает пароль на диск и освобождает все криптографические объекты после использования.

**В: Где можно получить дополнительную помощь, если возникнут проблемы?**  
О: Вы можете получить поддержку на [форуме поддержки GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).

---

**Последнее обновление:** 2026-06-01  
**Тестировано с:** GroupDocs.Editor 23.12 for .NET  
**Автор:** GroupDocs

```csharp
editorDocx.Dispose();
editorXlsx.Dispose();
editorXls.Dispose();
editorXml.Dispose();
Console.WriteLine("ExtractingDocumentInfo routine has successfully finished");
```

## Связанные руководства

- [Мастер извлечения метаданных в .NET с GroupDocs.Editor: Полное руководство](/editor/net/advanced-features/groupdocs-editor-net-metadata-extraction-guide/)
- [Руководства по загрузке документов с GroupDocs.Editor для .NET](/editor/net/document-loading/)
- [Эффективное редактирование документов с GroupDocs.Editor .NET: Преобразование HTML в редактируемые документы](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)