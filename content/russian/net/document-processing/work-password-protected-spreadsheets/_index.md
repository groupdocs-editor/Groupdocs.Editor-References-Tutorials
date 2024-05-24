---
title: Работа с электронными таблицами, защищенными паролем
linktitle: Работа с электронными таблицами, защищенными паролем
second_title: GroupDocs.Editor .NET API
description: Узнайте, как работать с электронными таблицами, защищенными паролем, с помощью GroupDocs.Editor для .NET. Это подробное руководство поможет вам сохранить защищенные файлы Excel.
type: docs
weight: 18
url: /ru/net/document-processing/work-password-protected-spreadsheets/
---
## Введение
Вам сложно управлять электронными таблицами, защищенными паролем, в ваших приложениях .NET? Если да, то вы находитесь в правильном месте! В этом подробном руководстве мы познакомим вас с процессом использования GroupDocs.Editor для .NET для эффективной обработки электронных таблиц, защищенных паролем. К концу этого руководства вы будете готовы с легкостью открывать, редактировать и сохранять зашифрованные файлы Excel.
## Предварительные условия
Прежде чем углубиться в код, давайте убедимся, что у вас есть все необходимое:
- Базовые знания C#. В этом руководстве предполагается, что вы знакомы с программированием на C#.
- .NET Framework: убедитесь, что на вашем компьютере разработки установлена .NET Framework.
-  GroupDocs.Editor для .NET: Загрузите и установите GroupDocs.Editor для .NET с сайта[здесь](https://releases.groupdocs.com/editor/net/).
## Импортировать пространства имен
Для начала вам необходимо импортировать необходимые пространства имен в проект C#. Эти пространства имен предоставляют доступ к функциям GroupDocs.Editor.
```csharp
using System;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
## Шаг 1. Получите путь к входному файлу
Во-первых, вам понадобится путь к входному файлу. В этом примере мы будем использовать образец файла Excel (`Your Sample Document`), защищенный паролем.
```csharp
string inputFilePath = "Your Sample Document";
```
## Шаг 2. Попытайтесь открыть документ без пароля
Давайте посмотрим, что произойдет, если мы попытаемся открыть документ без указания пароля.
```csharp
Editor editor = new Editor(inputFilePath);
try
{
    editor.Edit();
}
catch (GroupDocs.Editor.PasswordRequiredException)
{
    Console.WriteLine("Cannot edit the document because it is password-protected. A password is required.");
}
editor.Dispose();
```
## Шаг 3. Попробуйте указать неправильный пароль.
Теперь мы укажем неверный пароль, чтобы продемонстрировать реакцию редактора.
```csharp
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.Password = "incorrect_password";
editor = new Editor(inputFilePath, delegate { return loadOptions; });
try
{
    editor.Edit();
}
catch (GroupDocs.Editor.IncorrectPasswordException)
{
    Console.WriteLine("Cannot edit the document because the specified password is incorrect.");
}
editor.Dispose();
```
## Шаг 4. Откройте файл с правильным паролем.
Давайте введем правильный пароль и успешно откроем файл.
```csharp
loadOptions.Password = "excel_password";
loadOptions.OptimizeMemoryUsage = true;
editor = new Editor(inputFilePath, delegate { return loadOptions; });
```
## Шаг 5. Создайте и настройте параметры редактирования
Чтобы редактировать электронную таблицу, нам нужно создать и настроить параметры редактирования.
```csharp
SpreadsheetEditOptions editOptions = new SpreadsheetEditOptions();
```
## Шаг 6. Создайте промежуточный редактируемый документ
 Далее создаем промежуточный`EditableDocument` это позволяет нам вносить изменения в электронную таблицу.
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
{
    // Шаг 7: Создайте параметры сохранения
    SpreadsheetFormats xlsmFormat = SpreadsheetFormats.Xlsm;
    SpreadsheetSaveOptions saveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
    // Шаг 7.1: Установите новый пароль для открытия
    saveOptions.Password = "new password";
    // Шаг 7.2: Установите защиту от записи
    saveOptions.WorksheetProtection = new WorksheetProtection(WorksheetProtectionType.All, "write password");
    // Шаг 8. Сохраните документ без изменений.
    //Шаг 8.1: Подготовьте имя и путь выходного файла
    string outputFilename = Path.GetFileNameWithoutExtension(inputFilePath) + "." + xlsmFormat.Extension;
    string outputPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename);
    // Шаг 8.2: Создайте выходной поток
    using (FileStream outputStream = File.Create(outputPath))
    {
        // Шаг 8.3: Сохранить
        editor.Save(beforeEdit, outputStream, saveOptions);
    }
}
// Шаг 9. Удалите экземпляр редактора
editor.Dispose();
Console.WriteLine("Successfully handled the password-protected spreadsheet. Editor instance has been disposed: {0}", editor.IsDisposed ? "Yes" : "No");
```
## Заключение
Поздравляем! Вы успешно научились работать с электронными таблицами, защищенными паролем, с помощью GroupDocs.Editor для .NET. От попытки открыть документ без пароля до сохранения его с новыми настройками защиты — вы выполнили все основные шаги. Эти знания, несомненно, улучшат ваши возможности управления защищенными документами в ваших приложениях .NET.
## Часто задаваемые вопросы
### Что такое GroupDocs.Editor для .NET?
GroupDocs.Editor для .NET — это мощный API для редактирования документов, который позволяет разработчикам загружать, редактировать и сохранять документы различных форматов в приложениях .NET.
### Как получить временную лицензию на GroupDocs.Editor?
 Вы можете получить временную лицензию[здесь](https://purchase.groupdocs.com/temporary-license/) оценить возможности продукта.
### Можно ли оптимизировать использование памяти при редактировании больших документов?
 Да, вы можете включить оптимизацию памяти, установив`OptimizeMemoryUsage` собственность`true`в опциях загрузки.
### Могу ли я установить разные пароли для открытия и записи в таблицу?
Абсолютно! Вы можете установить отдельные пароли для открытия документа и для защиты от записи, используя параметры сохранения.
### Где я могу найти более подробную документацию?
 Вы можете получить доступ к полной документации по GroupDocs.Editor для .NET.[здесь](https://reference.groupdocs.com/editor/net/).