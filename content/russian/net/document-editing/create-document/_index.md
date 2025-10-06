---
title: Создать документ
linktitle: Создать документ
second_title: GroupDocs.Editor .NET API
description: Узнайте, как редактировать документы Word, Excel, PowerPoint, электронные книги и электронную почту с помощью GroupDocs.Editor для .NET, с помощью этого подробного пошагового руководства.
weight: 10
url: /ru/net/document-editing/create-document/
type: docs
---
# Создать документ

## Введение
Вы устали от хлопот, связанных с программным редактированием различных типов документов? GroupDocs.Editor для .NET призван упростить этот процесс. Этот мощный инструмент позволяет разработчикам с легкостью редактировать документы различных форматов, такие как Word, Excel, PowerPoint, электронные книги и электронные письма. В этом руководстве мы подробно рассмотрим, как использовать GroupDocs.Editor для .NET для создания и редактирования документов. Мы разобьем этот процесс на простые шаги, которые сделают его доступным, даже если вы новичок в этом.
## Предварительные условия
Прежде чем мы начнем, убедитесь, что у вас есть следующее:
- Visual Studio установлена на вашем компьютере.
- .NET Framework (4.0 или выше).
-  GroupDocs.Editor для библиотеки .NET. Вы можете скачать его с[здесь](https://releases.groupdocs.com/editor/net/).
- Базовые знания программирования на C#.
## Импортировать пространства имен
Сначала давайте импортируем необходимые пространства имен. Это сделает необходимые классы и методы доступными в нашем приложении.
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using System.IO;
```
## Шаг 1. Настройка потока
Для начала нам нужно настроить поток памяти, который будет служить заполнителем для содержимого документа.
```csharp
Stream memoryStream = Stream.Null;
```
## Шаг 2. Функция обратного вызова для сохранения документа
Затем определите функцию обратного вызова, которая сохранит новый поток документов. Эта функция необходима для обработки результатов процесса редактирования документа.
```csharp
void SaveNewDocument(Stream resultStream)
{
    memoryStream = resultStream;
}
```
## Шаг 3. Создание и редактирование документа WordProcessing
 Теперь давайте создадим и отредактируем документ Word. Начнем с создания нового`Editor` экземпляр для документов WordProcessing и отредактируйте его с параметрами по умолчанию.
### Создание и редактирование с параметрами по умолчанию
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    EditableDocument defaultWordProcessingDoc = editor.Edit();
}
```
### Создание и редактирование с использованием пользовательских параметров
Для большего контроля мы можем указать такие параметры, как отключение нумерации страниц и извлечение встроенных шрифтов.
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    WordProcessingEditOptions wordProcessingEditOptions = new WordProcessingEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true,
        FontExtraction = FontExtractionOptions.ExtractAllEmbedded
    };
    EditableDocument editableWordProcessingDocument = editor.Edit(wordProcessingEditOptions);
}
```
## Шаг 4. Создание и редактирование табличного документа
Точно так же мы можем создавать и редактировать документ Excel. Вот как это сделать.
### Создание и редактирование с параметрами по умолчанию
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    EditableDocument defaultEditableSpreadsheetDocument = editor.Edit();
}
```
### Создание и редактирование с использованием пользовательских параметров
 Чтобы настроить таргетинг на определенные листы или исключить скрытые, мы используем`SpreadsheetEditOptions`.
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    SpreadsheetEditOptions spreadsheetEditOptions = new SpreadsheetEditOptions
    {
        WorksheetIndex = 0,
        ExcludeHiddenWorksheets = true
    };
    EditableDocument editableSpreadsheetDocument = editor.Edit(spreadsheetEditOptions);
}
```
## Шаг 5. Создание и редактирование документа презентации
Презентации PowerPoint также поддерживаются. Давайте посмотрим, как с ними справиться.
### Создание и редактирование с параметрами по умолчанию
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    EditableDocument defaultEditablePresentationDocument = editor.Edit();
}
```
### Создание и редактирование с использованием пользовательских параметров
Вы можете настроить свои изменения, указав такие параметры, как показ слайдов и необходимость включения скрытых слайдов.
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    PresentationEditOptions presentationEditOptions = new PresentationEditOptions
    {
        ShowHiddenSlides = false,
        SlideNumber = 0
    };
    EditableDocument editablePresentationDocument = editor.Edit(presentationEditOptions);
}
```
## Шаг 6. Создание и редактирование документа электронной книги
GroupDocs.Editor также позволяет редактировать форматы электронных книг, такие как EPUB. Вот как вы можете справиться с этим.
### Создание и редактирование с параметрами по умолчанию
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EditableDocument defaultEditableEbookDocument = editor.Edit();
}
```
### Создание и редактирование с использованием пользовательских параметров
Настройте редактирование электронной книги, включив или отключив информацию о нумерации страниц и языке.
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EbookEditOptions ebookEditOptions = new EbookEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true
    };
    EditableDocument editableEbookDocument = editor.Edit(ebookEditOptions);
}
```
## Шаг 7. Создание и редактирование электронного документа
Наконец, мы рассмотрим, как редактировать документы электронной почты. Сюда входят такие форматы, как EML.
### Создание и редактирование с параметрами по умолчанию
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EditableDocument defaultEditableEmailDocument = editor.Edit();
}
```
### Создание и редактирование с использованием пользовательских параметров
Укажите параметры вывода почтового сообщения, чтобы контролировать процесс редактирования.
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EmailEditOptions emailEditOptions = new EmailEditOptions
    {
        MailMessageOutput = MailMessageOutput.All
    };
    EditableDocument editableEmailDocument = editor.Edit(emailEditOptions);
}
```
## Шаг 8: Завершение процесса
После редактирования документов очень важно правильно распорядиться потоком памяти, чтобы освободить ресурсы.
```csharp
memoryStream.Dispose();
System.Console.WriteLine("CreateDocument routine has successfully finished");
```
## Заключение
GroupDocs.Editor для .NET — это универсальный и мощный инструмент, который может упростить задачу программного редактирования различных типов документов. Следуя этому пошаговому руководству, вы сможете с легкостью создавать и редактировать документы, будь то файлы WordProcessing, электронные таблицы, презентации, электронные книги или электронные письма. Ознакомьтесь с документацией GroupDocs.Editor, чтобы узнать о более продвинутых функциях и возможностях настройки.
## Часто задаваемые вопросы
### Какие типы документов я могу редактировать с помощью GroupDocs.Editor для .NET?
Вы можете редактировать широкий спектр документов, включая WordProcessing, электронные таблицы, презентации, электронные книги и электронные письма.
### Можно ли настроить параметры редактирования?
Да, GroupDocs.Editor для .NET обеспечивает широкие возможности настройки с помощью различных параметров редактирования, специфичных для каждого типа документа.
### Как мне обработать вывод отредактированных документов?
Вы можете использовать функцию обратного вызова, чтобы сохранить отредактированный поток документов в нужном месте.
### Нужна ли мне лицензия для использования GroupDocs.Editor для .NET?
 Да, вы можете получить лицензию от[здесь](https://purchase.groupdocs.com/buy). Также есть возможность получить временную лицензию.
### Где я могу найти более подробную документацию?
 Подробная документация доступна на сайте[Страница документации GroupDocs.Editor для .NET](https://tutorials.groupdocs.com/editor/net/).