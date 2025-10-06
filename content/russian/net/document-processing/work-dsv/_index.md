---
title: Работа со значениями, разделенными разделителями (DSV)
linktitle: Работа со значениями, разделенными разделителями (DSV)
second_title: GroupDocs.Editor .NET API
description: Узнайте, как редактировать файлы CSV и TSV с помощью GroupDocs.Editor для .NET, с помощью этого пошагового руководства. Улучшайте свои проекты .NET без особых усилий.
weight: 12
url: /ru/net/document-processing/work-dsv/
type: docs
---
# Работа со значениями, разделенными разделителями (DSV)

## Введение
Если вы разработчик, работающий со значениями с разделителями-разделителями (DSV), такими как файлы CSV или TSV, вы знаете, что программное редактирование этих файлов может оказаться сложной задачей. Однако с GroupDocs.Editor для .NET эта задача становится значительно проще и эффективнее. В этом руководстве мы покажем вам, как использовать GroupDocs.Editor для .NET для чтения, редактирования и сохранения файлов DSV. Мы разобьем этот процесс на простые для выполнения шаги, чтобы вы могли легко реализовать его в своих проектах.
## Предварительные условия
Прежде чем мы углубимся в руководство, убедитесь, что у вас есть следующие предварительные условия:
- Visual Studio: убедитесь, что на вашем компьютере установлена Visual Studio.
-  GroupDocs.Editor для .NET: вам потребуется загрузить библиотеку GroupDocs.Editor for .NET и указать ссылку на нее. Вы можете скачать его[здесь](https://releases.groupdocs.com/editor/net/).
- Базовые знания C#. В этом руководстве предполагается, что у вас есть базовые знания о разработке C# и .NET.
## Импортировать пространства имен
Во-первых, вам необходимо импортировать необходимые пространства имен в ваш проект. Эти пространства имен предоставляют классы и методы, необходимые для работы с GroupDocs.Editor для .NET.
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

## Шаг 1. Получите путь к входному файлу DSV
Сначала вам нужно указать путь к входному файлу DSV. В этом примере мы предположим, что это файл CSV.
```csharp
string inputFilePath = "Your Sample Document";
```
## Шаг 2. Создайте экземпляр редактора
 Создайте экземпляр`Editor` сорт. Этот экземпляр будет использоваться для загрузки файла DSV и управления им.
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## Шаг 3. Создайте параметры редактирования DSV
 Далее создайте экземпляр`DelimitedTextEditOptions` и укажите разделитель для файла DSV. Здесь мы используем запятую в качестве разделителя.
```csharp
    Options.DelimitedTextEditOptions editOptions = new DelimitedTextEditOptions(",");
    editOptions.ConvertDateTimeData = false;
    editOptions.ConvertNumericData = true;
    editOptions.TreatConsecutiveDelimitersAsOne = true;
```
## Шаг 4. Создайте экземпляр EditableDocument
 Создать`EditableDocument` экземпляр, используя`Editor.Edit` метод. Это подготавливает документ к редактированию.
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## Шаг 5. Отредактируйте содержимое документа
Получите исходное текстовое содержимое и внесите необходимые изменения. В демонстрационных целях заменим некоторый текст.
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("SsangYong", "Chevrolet").Replace("Kyron", "Camaro");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## Шаг 6. Создайте редактируемый документ с обновленным содержимым
 Создать новый`EditableDocument` с обновленным контентом.
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## Шаг 7. Создайте параметры сохранения в формате CSV.
Укажите параметры сохранения для формата CSV, включая разделитель и кодировку.
```csharp
    Options.DelimitedTextSaveOptions csvSaveOptions = new DelimitedTextSaveOptions(",");
    csvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## Шаг 8. Создайте параметры сохранения TSV.
Аналогичным образом укажите параметры сохранения для формата TSV.
```csharp
    Options.DelimitedTextSaveOptions tsvSaveOptions = new DelimitedTextSaveOptions("\t");
    tsvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## Шаг 9: Создайте параметры сохранения электронной таблицы
Если вам нужно сохранить документ в виде электронной таблицы, создайте соответствующие параметры сохранения.
```csharp
    Options.SpreadsheetSaveOptions cellsSaveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
```
## Шаг 10: Подготовьте пути сохранения
Определите пути, по которым будут сохраняться отредактированные файлы.
```csharp
    string outputCsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".csv");
    string outputTsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".tsv");
    string outputCellsPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".xlsm");
```
## Шаг 11: Сохраните отредактированный документ
Сохраните отредактированный документ по указанным путям в разных форматах.
```csharp
    editor.Save(afterEdit, outputCsvPath, csvSaveOptions);
    editor.Save(afterEdit, outputTsvPath, tsvSaveOptions);
    editor.Save(afterEdit, outputCellsPath, cellsSaveOptions);
```
## Шаг 12. Удалите экземпляры EditableDocument
 Наконец, обязательно утилизируйте`EditableDocument` экземпляры для освобождения ресурсов.
```csharp
    beforeEdit.Dispose();
    afterEdit.Dispose();
}
System.Console.WriteLine("WorkingWithDsv routine has successfully finished");
```
## Заключение
Редактирование файлов DSV с помощью GroupDocs.Editor для .NET — это простой процесс, который включает в себя создание экземпляра редактора, настройку параметров редактирования, изменение содержимого и сохранение изменений. Это пошаговое руководство поможет вам легко интегрировать эту функцию в ваши приложения .NET. Независимо от того, работаете ли вы с CSV, TSV или другими форматами DSV, GroupDocs.Editor для .NET предоставляет надежное и гибкое решение.
## Часто задаваемые вопросы
### Могу ли я использовать GroupDocs.Editor для .NET для редактирования больших файлов CSV?
Да, GroupDocs.Editor для .NET способен эффективно обрабатывать большие файлы CSV.
### Поддерживает ли GroupDocs.Editor для .NET другие форматы DSV, кроме CSV и TSV?
Да, он поддерживает различные форматы DSV, если вы укажете соответствующий разделитель.
### Можно ли настроить кодировку при сохранении файлов DSV?
Конечно, в настройках сохранения можно указать нужную кодировку.
### Могу ли я преобразовать файл CSV в электронную таблицу Excel с помощью GroupDocs.Editor для .NET?
Да, вы можете сохранить файл CSV как электронную таблицу Excel, используя соответствующие параметры сохранения.
### Где я могу найти дополнительную документацию по GroupDocs.Editor для .NET?
 Вы можете найти подробную документацию[здесь](https://tutorials.groupdocs.com/editor/net/)