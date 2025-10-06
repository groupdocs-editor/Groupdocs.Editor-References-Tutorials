---
title: Сохранить документ
linktitle: Сохранить документ
second_title: GroupDocs.Editor .NET API
description: Легко редактируйте и сохраняйте документы с помощью GroupDocs.Editor для .NET. Это пошаговое руководство упрощает процесс для разработчиков.
weight: 14
url: /ru/net/document-editing/save-document/
type: docs
---
# Сохранить документ

## Введение
Вы хотите легко редактировать и сохранять документы с помощью GroupDocs.Editor для .NET? Вы находитесь в правильном месте! Это руководство шаг за шагом проведет вас через этот процесс, гарантируя, что вы сможете легко управлять своими документами. Независимо от того, являетесь ли вы опытным разработчиком или новичком, наше руководство предоставит вам всю информацию, необходимую для начала работы.
## Предварительные условия
Прежде чем приступить к изучению руководства, убедитесь, что у вас есть следующие предварительные условия:
- Среда разработки: Visual Studio, установленная на вашем компьютере.
- .NET Framework: убедитесь, что у вас установлена .NET Framework 4.6.1 или более поздняя версия.
-  GroupDocs.Editor для .NET: загрузите последнюю версию[здесь](https://releases.groupdocs.com/editor/net/).
- Базовые знания C#: Знание программирования на C# обязательно.
## Импортировать пространства имен
Чтобы использовать GroupDocs.Editor в своем проекте .NET, вам необходимо импортировать необходимые пространства имен. Вот как это сделать:
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
Теперь, когда мы настроили нашу среду и импортировали необходимые пространства имен, давайте углубимся в шаги, необходимые для загрузки, редактирования и сохранения документа с помощью GroupDocs.Editor для .NET.
## Шаг 1. Загрузите документ
Сначала нам нужно загрузить документ, который мы хотим редактировать. GroupDocs.Editor упрощает этот процесс. Вот как вы можете это сделать:

```csharp
string inputFilePath = "Your Sample Document";
Editor editor = new Editor(inputFilePath, delegate { return new Options.WordProcessingLoadOptions(); });
EditableDocument defaultWordProcessingDoc = editor.Edit();
```
 На этом этапе мы указываем путь к документу, который хотим редактировать, и создаем экземпляр`Editor` сорт.`Edit` затем вызывается метод для загрузки документа в`EditableDocument` объект.
## Шаг 2. Измените документ
Когда документ загружен, пришло время внести некоторые изменения. Поскольку у нас нет подключенного редактора WYSIWYG, мы будем моделировать процесс редактирования в коде.

```csharp
string allEmbeddedInsideString = defaultWordProcessingDoc.GetEmbeddedHtml();
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
EditableDocument editedDoc = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```
 Здесь мы извлекаем внедренное HTML-содержимое документа, выполняем простую замену текста и создаем новый`EditableDocument`экземпляр из измененного HTML.
## Шаг 3. Сохраните документ
После редактирования документа последний шаг — сохранить его. GroupDocs.Editor предоставляет несколько вариантов сохранения документа в разных форматах.
## Сохранить как RTF
```csharp
string outputRtfPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.rtf");
WordProcessingSaveOptions rtfSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
editor.Save(editedDoc, outputRtfPath, rtfSaveOptions);
```
## Сохранить как DOCM
```csharp
string outputDocmPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.docm");
WordProcessingSaveOptions docmSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm);
using (FileStream outputStream = File.Create(outputDocmPath))
{
    editor.Save(editedDoc, outputStream, docmSaveOptions);
}
```
## Сохранить как обычный текст
```csharp
string outputTxtPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.txt");
TextSaveOptions textSaveOptions = new TextSaveOptions
{
    Encoding = System.Text.Encoding.UTF8,
    PreserveTableLayout = true
};
editor.Save(editedDoc, outputTxtPath, textSaveOptions);
```
## Шаг 4: Очистка
 Наконец, очень важно избавиться от`EditableDocument` и`Editor` экземпляры для освобождения ресурсов.
```csharp
editedDoc.Dispose();
defaultWordProcessingDoc.Dispose();
editor.Dispose();
```
Выполнив эти шаги, вы сможете эффективно загружать, редактировать и сохранять документы с помощью GroupDocs.Editor для .NET. Этот мощный инструмент обеспечивает гибкость и простоту использования, упрощая управление документами.
## Заключение
Программное редактирование и сохранение документов никогда не было проще с GroupDocs.Editor для .NET. Это руководство проведет вас через весь процесс: от загрузки документа до его сохранения в различных форматах. GroupDocs.Editor — это универсальное и надежное решение, упрощающее процесс редактирования документов.
## Часто задаваемые вопросы
### Какие форматы файлов поддерживает GroupDocs.Editor?
GroupDocs.Editor поддерживает различные форматы файлов, включая DOCX, RTF, TXT и многие другие. Полный список см.[документация](https://tutorials.groupdocs.com/editor/net/).
### Могу ли я попробовать GroupDocs.Editor перед покупкой?
 Да, вы можете получить[бесплатная пробная версия](https://releases.groupdocs.com/) протестировать возможности GroupDocs.Editor.
### Доступна ли какая-либо поддержка, если у меня возникнут проблемы?
 Абсолютно! Вы можете посетить[форум поддержки](https://forum.groupdocs.com/c/editor/20) за помощь в решении любых вопросов, с которыми вы сталкиваетесь.
### Как получить временную лицензию?
 Вы можете запросить[временная лицензия](https://purchase.groupdocs.com/temporary-license/) в целях оценки.
### Где я могу приобрести полную версию GroupDocs.Editor?
 Вы можете купить полную версию[здесь](https://purchase.groupdocs.com/buy).