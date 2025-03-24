---
title: Работа с коллекцией полей устаревшей формы
linktitle: Работа с коллекцией полей устаревшей формы
second_title: GroupDocs.Editor .NET API
description: Узнайте, как управлять полями устаревшей формы с помощью GroupDocs.Editor для .NET, из нашего подробного руководства. Идеально подходит для обработки текстовых полей, флажков, дат и многого другого.
weight: 12
url: /ru/net/form-field-management/work-legacy-form-field-collection/
---

# Работа с коллекцией полей устаревшей формы

## Введение
Добро пожаловать в это подробное руководство по работе с коллекциями полей форм прежних версий с помощью GroupDocs.Editor для .NET. Независимо от того, имеете ли вы дело с текстовыми полями, флажками, полями даты или раскрывающимися меню, это руководство проведет вас через каждый шаг, чтобы эффективно управлять этими полями. К концу этого руководства вы получите четкое представление о том, как использовать GroupDocs.Editor для обработки различных полей форм в ваших документах. Давайте погрузимся!
## Предварительные условия
Прежде чем мы начнем, убедитесь, что у вас есть следующие предварительные условия:
- Visual Studio: подойдет любая последняя версия.
- .NET Framework: убедитесь, что у вас установлена .NET Framework.
-  GroupDocs.Editor для .NET: загрузите последнюю версию[здесь](https://releases.groupdocs.com/editor/net/).
- Образец документа: образец файла DOCX с полями формы для целей тестирования.
## Импортировать пространства имен
Для начала импортируйте необходимые пространства имен в свой проект. Эти пространства имен необходимы для доступа к классам и методам, необходимым для управления полями формы.
```csharp
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System.IO;
```
## Шаг 1. Получите путь к входному файлу
Сначала вам нужно указать путь к входному файлу. В этом примере мы будем использовать образец файла DOCX, который содержит различные поля формы.
```csharp
string inputFilePath = "path/to/your/sample_legacy_formfields.docx";
```
## Шаг 2. Создайте поток из пути к файлу
Затем создайте файловый поток для чтения содержимого вашего документа. Этот поток будет использоваться для загрузки документа в GroupDocs.Editor.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
    // Здесь будет размещен дополнительный код
}
```
## Шаг 3. Создайте параметры загрузки для документа
Перед загрузкой документа создайте параметры загрузки. Эти параметры помогут справиться с различными сценариями, например с документами, защищенными паролем.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
// Если документ защищен паролем, укажите пароль
loadOptions.Password = "your_password_here"; // При необходимости используйте действительный пароль
```
## Шаг 4. Загрузите документ с помощью экземпляра редактора
Теперь загрузите документ в экземпляр редактора, используя файловый поток и параметры загрузки, которые вы создали ранее.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    // Здесь будет размещен дополнительный код
}
```
## Шаг 5. Прочтите экземпляр FormFieldManager.
Для управления полями формы откройте экземпляр FormFieldManager из редактора. Этот экземпляр позволит вам взаимодействовать с полями формы в вашем документе.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
## Шаг 6. Прочтите коллекцию FormFieldCollection.
Получите FormFieldCollection из FormFieldManager. Эта коллекция содержит все поля формы, присутствующие в документе.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
## Шаг 7. Перебор каждого поля формы
Просмотрите каждое поле формы в коллекции и определите его тип. В зависимости от типа вы можете извлекать значение поля и манипулировать им.
```csharp
foreach (var formField in collection)
{
    switch (formField.Type)
    {
        case FormFieldType.Text:
            TextFormField textFormField = collection.GetFormField<TextFormField>(formField.Name);
            Console.WriteLine($"TextFormField detected, name: {formField.Name}, value: {textFormField.Value}");
            break;
        case FormFieldType.CheckBox:
            CheckBoxForm checkBoxFormField = collection.GetFormField<CheckBoxForm>(formField.Name);
            Console.WriteLine($"CheckBoxForm detected, name: {formField.Name}, value: {checkBoxFormField.Value}");
            break;
        case FormFieldType.Date:
            DateFormField dateFormField = collection.GetFormField<DateFormField>(formField.Name);
            Console.WriteLine($"DateFormField detected, name: {formField.Name}, value: {dateFormField.Value}");
            break;
        case FormFieldType.Number:
            NumberFormField numberFormField = collection.GetFormField<NumberFormField>(formField.Name);
            Console.WriteLine($"NumberFormField detected, name: {formField.Name}, value: {numberFormField.Value}");
            break;
        case FormFieldType.DropDown:
            DropDownFormField dropDownFormField = collection.GetFormField<DropDownFormField>(formField.Name);
            Console.WriteLine($"DropDownFormField detected, name: {formField.Name}, value selected: {dropDownFormField.Value[dropDownFormField.SelectedIndex]}");
            break;
    }
}
```
## Шаг 8: Заключение
Выполнив эти шаги, вы сможете эффективно управлять полями устаревших форм и взаимодействовать с ними с помощью GroupDocs.Editor для .NET. Будь то текстовые поля, флажки, даты, числа или раскрывающиеся списки, в этом руководстве представлен ясный и краткий способ работы с каждым типом.
## Заключение
 Работа с полями устаревших форм в документах может быть простой при использовании правильных инструментов. GroupDocs.Editor для .NET предоставляет надежное решение для эффективного управления этими полями. Следуя этому пошаговому руководству, вы теперь сможете легко манипулировать различными полями форм в своих документах. Не забудьте изучить[документация](https://tutorials.groupdocs.com/editor/net/)для получения более продвинутых функций и опций.
## Часто задаваемые вопросы
### 1. Могу ли я использовать GroupDocs.Editor для .NET с документами, защищенными паролем?
Да, вы можете указать пароль в параметрах загрузки для обработки документов, защищенных паролем.
### 2. Как получить бесплатную пробную версию GroupDocs.Editor для .NET?
 Вы можете скачать бесплатную пробную версию с[здесь](https://releases.groupdocs.com/).
### 3. Имеется ли какая-либо поддержка для GroupDocs.Editor для .NET?
 Да, вы можете получить доступ к поддержке[здесь](https://forum.groupdocs.com/c/editor/20).
### 4. Могу ли я приобрести лицензию на GroupDocs.Editor для .NET?
 Да, вы можете купить лицензию у[здесь](https://purchase.groupdocs.com/buy).
### 5. Где я могу найти документацию по GroupDocs.Editor для .NET?
Документация доступна[здесь](https://tutorials.groupdocs.com/editor/net/).