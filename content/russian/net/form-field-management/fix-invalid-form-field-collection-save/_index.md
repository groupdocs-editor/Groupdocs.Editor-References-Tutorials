---
title: Исправить неверный сбор полей формы и сохранить
linktitle: Исправить неверный сбор полей формы и сохранить
second_title: GroupDocs.Editor .NET API
description: Узнайте, как исправить недопустимые поля формы в DOCX с помощью Groupdocs.Editor для .NET. Следуйте этому руководству, чтобы обеспечить отсутствие ошибок в ваших документах и надежно их сохранить.
type: docs
weight: 11
url: /ru/net/form-field-management/fix-invalid-form-field-collection-save/
---
## Введение
Добро пожаловать! Если вы работаете с полями форм в документах и сталкиваетесь с проблемами, связанными с недопустимыми коллекциями полей форм, вы попали по адресу. В этом уроке мы углубимся в то, как исправить недопустимые поля формы и сохранить документ с помощью Groupdocs.Editor для .NET. Мы проведем вас через весь процесс шаг за шагом, гарантируя, что у вас есть все детали, необходимые для бесперебойной работы. Давайте начнем!
## Предварительные условия
Прежде чем мы перейдем к коду, вам необходимо кое-что предусмотреть:
-  Groupdocs.Editor для .NET: убедитесь, что у вас установлена библиотека Groupdocs.Editor для .NET. Вы можете скачать его[здесь](https://releases.groupdocs.com/editor/net/).
- Среда разработки. У вас должна быть настроена среда разработки .NET, например Visual Studio.
- Базовые знания C#. В этом руководстве предполагается, что у вас есть базовые знания программирования на C#.
## Импортировать пространства имен
Сначала вам необходимо импортировать необходимые пространства имен в ваш проект C#. Добавьте следующие строки в начало файла кода:
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System;
using System.IO;
```
## Шаг 1. Получите путь к входному файлу
Первый шаг — указать путь к входному файлу. Этот файл должен представлять собой документ DOCX, содержащий поля формы.
```csharp
string inputFilePath = Constants.SampleLegacyFormFields_docx;
```
## Шаг 2. Создайте поток из пути к файлу
Затем создайте файловый поток для чтения входного документа. Это позволит вам загрузить документ в редактор.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
```
## Шаг 3. Создайте параметры загрузки для документа
На этом этапе вам необходимо создать параметры загрузки для вашего документа. Если ваш документ защищен паролем, вы можете указать пароль. В этом примере документ не защищен, поэтому пароль игнорируется.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
loadOptions.Password = "some_password_to_open_a_document";
```
## Шаг 4. Загрузите документ в экземпляр редактора.
Теперь загрузите документ с указанными параметрами в экземпляр редактора. Именно здесь будут происходить основные операции над документом.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
```
## Шаг 4.1. Прочтите экземпляр FormFieldManager.
`FormFieldManager` Экземпляр отвечает за управление полями формы в документе. Вам потребуется прочитать этот экземпляр, чтобы получить доступ к полям формы и манипулировать ими.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
## Шаг 4.2. Прочтите коллекцию FormFieldCollection.
`FormFieldCollection` содержит все поля формы в документе. Вы прочитаете эту подборку, чтобы проверить и исправить недопустимые поля формы.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
## Шаг 4.3. Автоматическое исправление недопустимых полей формы
Попытайтесь автоматически исправить все недопустимые поля формы в документе. Это предварительный шаг для решения очевидных проблем.
```csharp
fieldManager.FixInvalidFormFieldNames(new InvalidFormField[0]);
collection = fieldManager.FormFieldCollection;
```
## Шаг 4.4. Проверьте наличие недопустимых полей формы
Проверьте, остались ли недействительные поля формы после попытки автоматического исправления.
```csharp
bool hasInvalidFormFields = fieldManager.HasInvalidFormFields();
Console.WriteLine("FormFieldCollection contains invalid items: {0}", hasInvalidFormFields);
```
## Шаг 4.4.1. Получите все недопустимые имена полей формы
Получите имена всех недопустимых полей формы. Эти имена будут использоваться для исправления полей.
```csharp
var invalidFormFields = fieldManager.GetInvalidFormFieldNames();
```
## Шаг 4.4.2. Создайте уникальные имена для недопустимых полей
Для каждого недопустимого поля формы создайте уникальное имя. Это гарантирует отсутствие конфликтов с существующими именами полей формы.
```csharp
foreach (var invalidItem in invalidFormFields)
{
    invalidItem.FixedName = string.Format("{0}_{1}", invalidItem.Name, Guid.NewGuid());
}
```
## Шаг 4.4.3: Исправьте неверные поля формы
Исправьте недопустимые поля формы, используя уникальные имена, созданные на предыдущем шаге.
```csharp
fieldManager.FixInvalidFormFieldNames(invalidFormFields);
collection = fieldManager.FormFieldCollection;
```
## Шаг 5. Создайте параметры сохранения документа
Настройте параметры сохранения документа. Сюда входит указание формата и любые дополнительные настройки сохранения.
```csharp
WordProcessingFormats docFormat = WordProcessingFormats.Docx;
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(docFormat);
```
## Шаг 5.1: Оптимизируйте использование памяти
 Если ваш документ большой и может вызвать`OutOfMemoryException`включите опцию оптимизации памяти.
```csharp
saveOptions.OptimizeMemoryUsage = true;
```
## Шаг 5.2. Защитите документ от записи
Чтобы защитить документ от изменения, за исключением полей формы, установите пароль защиты.
```csharp
saveOptions.Protection = new WordProcessingProtection(WordProcessingProtectionType.AllowOnlyFormFields, "write_password");
```
## Шаг 6: Сохраните документ
Наконец, сохраните документ с указанными параметрами сохранения. Подготовьте поток памяти для сохранения выходного документа.
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(outputStream, saveOptions);
}
Console.WriteLine("FixInvalidFormFieldCollectionAndSave routine has successfully finished");
```
## Заключение
 И вот оно! Вы успешно исправили недопустимые поля формы и сохранили документ с помощью Groupdocs.Editor для .NET. Это пошаговое руководство должно было сделать процесс понятным и управляемым. Если у вас возникнут какие-либо проблемы или вопросы, не стесняйтесь проверить[документация](https://reference.groupdocs.com/editor/net/) или обратитесь к[поддерживать](https://forum.groupdocs.com/c/editor/20).
## Часто задаваемые вопросы
### Что делать, если мой документ защищен паролем?
 Вы можете указать пароль в`WordProcessingLoadOptions` чтобы открыть документ.
### Как узнать, есть ли недопустимые поля формы?
 Использовать`HasInvalidFormFields` метод для проверки наличия недопустимых полей формы в документе.
### Можно ли исправить поля формы, не меняя их названия?
Во избежание конфликтов рекомендуется создавать уникальные имена для недопустимых полей формы.
### В каких форматах можно сохранить документ?
 Вы можете сохранить документ в различных форматах, таких как DOCX, PDF и других, установив соответствующий`WordProcessingFormats`.
### Как оптимизировать использование памяти при сохранении больших документов?
 Включите`OptimizeMemoryUsage` вариант в`WordProcessingSaveOptions` для эффективной обработки больших документов.