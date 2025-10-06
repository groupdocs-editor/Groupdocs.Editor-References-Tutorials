---
title: Работа с обычными текстовыми документами
linktitle: Работа с обычными текстовыми документами
second_title: GroupDocs.Editor .NET API
description: Научитесь редактировать обычные текстовые документы с помощью GroupDocs.Editor для .NET с помощью нашего пошагового руководства. Упростите процесс редактирования документов .NET.
weight: 15
url: /ru/net/document-processing/work-plain-text-documents/
type: docs
---
# Работа с обычными текстовыми документами

## Введение
Вы хотите упростить процесс редактирования документов в .NET? Не ищите ничего, кроме GroupDocs.Editor для .NET! Этот мощный API позволяет с легкостью редактировать документы самых разных форматов. В этом руководстве мы покажем вам процесс работы с обычными текстовыми документами с помощью GroupDocs.Editor для .NET. К концу вы будете готовы профессионально редактировать текстовые документы. Готовы погрузиться? Давайте начнем!
## Предварительные условия
Прежде чем мы начнем, вам необходимо подготовить несколько вещей:
- Среда разработки .NET. Убедитесь, что у вас настроена работающая среда разработки .NET. Visual Studio — популярный выбор.
-  GroupDocs.Editor для .NET: загрузите и установите[GroupDocs.Editor для .NET](https://releases.groupdocs.com/editor/net/).
- Базовые знания C#. Знакомство с языком программирования C# поможет вам следовать примерам.
- Текстовый редактор: подойдет любой текстовый редактор, но рекомендуется использовать Visual Studio Code из-за его функций и простоты использования.
## Импортировать пространства имен
Чтобы начать использовать GroupDocs.Editor для .NET, вам необходимо импортировать необходимые пространства имен в ваш проект. Это гарантирует, что все необходимые классы и методы доступны для использования.
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```
Давайте разобьем процесс на управляемые этапы. Следуйте инструкциям, пока мы проведем вас через каждый этап редактирования текстовых документов с помощью GroupDocs.Editor для .NET.
## Шаг 1. Получите путь к входному файлу TXT
Сначала вам нужно указать путь к входному файлу TXT. Это может быть путь к локальному файлу или потоку, содержащему содержимое файла.
```csharp
string inputFilePath = "YourSampleDocument.txt";
```
## Шаг 2. Создайте экземпляр редактора
 Далее создайте экземпляр`Editor` сорт. Этот класс отвечает за загрузку и редактирование документов. На этом этапе никакие параметры загрузки не требуются.
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## Шаг 3. Создайте параметры редактирования TXT
Теперь создайте параметры редактирования TXT. Эти параметры позволяют указать, как текстовое содержимое должно обрабатываться во время редактирования.
```csharp
    TextEditOptions editOptions = new TextEditOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        RecognizeLists = true,
        LeadingSpaces = TextLeadingSpacesOptions.ConvertToIndent,
        TrailingSpaces = TextTrailingSpacesOptions.Trim
    };
```
## Шаг 4. Создайте экземпляр EditableDocument
 Установив параметры редактирования, создайте`EditableDocument` пример. Это представляет документ в редактируемом формате.
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## Шаг 5. Отредактируйте содержимое документа
Получите исходное текстовое содержимое и внесите необходимые изменения. В этом примере мы заменим слово «текст» на «ОТРЕДАКТИРОВАННЫЙ текст».
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("text", "EDITED text");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## Шаг 6. Создайте редактируемый документ с обновленным содержимым
 После внесения необходимых правок создайте новый`EditableDocument` с обновленным контентом и оригинальными ресурсами.
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## Шаг 7. Создайте параметры сохранения WordProcessing
Подготовьте варианты сохранения для формата WordProcessing. В этом примере используется формат DOCM и указывается языковой стандарт.
```csharp
    WordProcessingSaveOptions wordSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm)
    {
        Locale = System.Globalization.CultureInfo.GetCultureInfo("en-GB")
    };
```
## Шаг 8. Создайте параметры сохранения TXT
Аналогичным образом создайте параметры сохранения для формата TXT. Убедитесь, что установлена кодировка UTF-8, и сохраните макет таблицы.
```csharp
    TextSaveOptions txtSaveOptions = new TextSaveOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        PreserveTableLayout = true
    };
```
## Шаг 9: Подготовьте пути вывода
Подготовьте пути для сохранения полученных файлов DOCX и TXT. Используйте путь к входному файлу, чтобы определить выходной каталог и имена файлов.
```csharp
    string outputWordPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".docm");
    string outputTxtPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".txt");
```
## Шаг 10: Сохраните отредактированный документ
Наконец, сохраните отредактированный документ в форматах DOCX и TXT, используя указанные параметры сохранения.
```csharp
    editor.Save(afterEdit, outputWordPath, wordSaveOptions);
    editor.Save(afterEdit, outputTxtPath, txtSaveOptions);
}
System.Console.WriteLine("Document editing process completed successfully!");
```
## Заключение
 Поздравляем! Вы успешно отредактировали простой текстовый документ с помощью GroupDocs.Editor для .NET. Этот мощный инструмент упрощает редактирование документов, упрощая его интеграцию в ваши .NET-приложения. Независимо от того, работаете ли вы с простыми текстовыми файлами или сложными форматами документов, GroupDocs.Editor поможет вам. Узнайте больше о функциях и возможностях, посетив[Документация GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/).
## Часто задаваемые вопросы
### Какие форматы файлов поддерживает GroupDocs.Editor для .NET?
 GroupDocs.Editor для .NET поддерживает широкий спектр форматов файлов, включая DOCX, TXT, HTML и другие. Проверить[документация](https://tutorials.groupdocs.com/editor/net/) для полного списка.
### Как я могу получить бесплатную пробную версию GroupDocs.Editor для .NET?
 Вы можете загрузить бесплатную пробную версию GroupDocs.Editor для .NET с сайта[страница релизов](https://releases.groupdocs.com/).
### Могу ли я приобрести временную лицензию на GroupDocs.Editor для .NET?
Да, вы можете получить временную лицензию в[Страница покупки GroupDocs](https://purchase.groupdocs.com/temporary-license/).
### Где я могу получить поддержку GroupDocs.Editor для .NET?
 Поддержка доступна через[Форум поддержки GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).
### Есть ли подробная документация по GroupDocs.Editor для .NET?
 Да, подробная документация доступна на сайте[Страница документации GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/).