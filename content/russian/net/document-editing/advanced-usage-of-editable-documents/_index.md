---
title: Расширенное использование редактируемых документов
linktitle: Расширенное использование редактируемых документов
second_title: GroupDocs.Editor .NET API
description: Изучите расширенные возможности использования GroupDocs.Editor для .NET для создания, редактирования и извлечения ресурсов из документов программным способом.
weight: 11
url: /ru/net/document-editing/advanced-usage-of-editable-documents/
type: docs
---
# Расширенное использование редактируемых документов

## Введение
Если вы разработчик .NET и хотите расширить свои возможности редактирования документов, GroupDocs.Editor для .NET предлагает мощный набор инструментов. Это подробное руководство познакомит вас с расширенными возможностями использования редактируемых документов с помощью GroupDocs.Editor, подробно разбив каждый шаг, чтобы вы могли использовать весь его потенциал.
## Предварительные условия
Прежде чем углубляться в расширенные функции, убедитесь, что у вас есть следующее:
- Visual Studio установлена на вашей машине разработки.
- .NET Framework, совместимая с GroupDocs.Editor.
-  GroupDocs.Editor для библиотеки .NET. Ты можешь[скачай это здесь](https://releases.groupdocs.com/editor/net/).
-  Действующая лицензия GroupDocs.Editor. Вы можете получить[бесплатная пробная версия](https://releases.groupdocs.com/) или купить[временная лицензия](https://purchase.groupdocs.com/temporary-license/).
## Импортировать пространства имен
Для начала убедитесь, что вы импортировали необходимые пространства имен в свой проект .NET:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```
## Шаг 1. Создание экземпляра EditableDocument
 Сначала вам нужно создать экземпляр`EditableDocument` путем загрузки и редактирования входного документа поддерживаемого формата.
```csharp
string inputFilePath = "YourSampleDocument.docx";
Editor editor = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```
На этом этапе мы загружаем входной документ и подготавливаем его к редактированию.
## Шаг 2. Извлечение ресурсов документа
`EditableDocument` содержит различные ресурсы, которые можно извлекать и манипулировать ими. Давайте разберем их:
### Шаг 2.1. Извлеките весь документ в формате HTML
Вы можете создать одну строку, содержащую весь документ со всеми его ресурсами, внедренными в виде HTML.
```csharp
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```
Эта строка будет довольно большой, поскольку она включает таблицы стилей, изображения и шрифты, закодированные в base64.
### Шаг 2.2: Извлеките все изображения
Извлеките все изображения из документа.
```csharp
List<IImageResource> allImages = beforeEdit.Images;
```
### Шаг 2.3: Извлеките все шрифты
Извлеките все шрифты, используемые в документе.
```csharp
List<FontResourceBase> allFonts = beforeEdit.Fonts;
```
### Шаг 2.4: Извлеките все таблицы стилей
Извлеките все таблицы стилей в текстовом формате.
```csharp
List<CssText> allStylesheets = beforeEdit.Css;
```
### Шаг 2.5: Соберите все ресурсы
Соберите все ресурсы за один звонок.
```csharp
List<IHtmlResource> allResources = beforeEdit.AllResources;
```
Сюда входят изображения, шрифты и таблицы стилей.
### Шаг 2.6: Получите HTML-разметку
Получите HTML-разметку документа без встроенных ресурсов.
```csharp
string htmlMarkup = beforeEdit.GetContent();
```
## Шаг 3. Настройка внешних ссылок
Иногда вам необходимо настроить внешние ссылки, чтобы они указывали на собственный обработчик ресурсов. Вот как это сделать:
### Шаг 3.1. Подготовьте пользовательские префиксы
Подготовьте префиксы, которые будут добавлять оригинальные внешние ссылки.
```csharp
string customImagesRequesthandlerUri = "http://example.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://example.com/CssHandler/id=";
string customFontsRequesthandlerUri = "http://example.com/FontsHandler/id=";
```
### Шаг 3.2. Создание префиксной HTML-разметки
Создайте HTML-разметку с настроенными ссылками.
```csharp
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```
### Шаг 3.3: Получите HTML-контент только для тела
Некоторые редакторы WYSIWYG обрабатывают только чистую HTML-разметку без заголовков.
```csharp
string onlyBodyContent = beforeEdit.GetBodyContent();
```
### Шаг 3.4. Содержимое только с префиксом
Создавайте только основной контент с настраиваемыми префиксами изображений.
```csharp
string prefixedBodyContent = beforeEdit.GetBodyContent(customImagesRequesthandlerUri);
```
### Шаг 3.5: Извлечение таблиц стилей
Извлеките таблицы стилей, используемые в документе.
```csharp
List<string> stylesheets = beforeEdit.GetCssContent();
```
### Шаг 3.6: Таблицы стилей с префиксами
Извлекайте таблицы стилей с пользовательскими префиксами.
```csharp
List<string> prefixedStylesheets = beforeEdit.GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri);
```
## Шаг 4. Сохраните документ в формате HTML.
Сохраните отредактированный документ как HTML-файл, включая его ресурсы.
```csharp
string htmlFilePath = Path.Combine("output", Path.GetFileNameWithoutExtension(inputFilePath) + ".html");
beforeEdit.Save(htmlFilePath);
```
Этот метод создает отдельный каталог для таких ресурсов, как таблицы стилей, изображения и шрифты.
## Шаг 5. Удаление EditableDocument
 EditableDocument реализует`IDisposable` и предоставляет возможность проверить, удален ли экземпляр.
```csharp
Console.WriteLine("EditableDocument is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");
```
### Шаг 5.1. Обработка события удаления
Вы также можете подписаться на событие утилизации.
```csharp
EventHandler someMethod = delegate { Console.WriteLine("Disposing event was spotted!"); };
beforeEdit.Disposed += someMethod;
```
## Шаг 6. Создание EditableDocument из HTML
Создайте экземпляр EditableDocument из HTML-документа.
### Шаг 6.1: Из HTML-файла
```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
```
### Шаг 6.2: Из HTML-разметки
```csharp
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);
```
Эти экземпляры (afterEditFromFile и afterEditFromMarkup) идентичны оригиналу (beforeEdit).
## Шаг 7: Утилизация вручную
Вручную удалите экземпляры EditableDocument.
```csharp
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```
Это обеспечивает правильную очистку ресурсов.
## Заключение
GroupDocs.Editor для .NET предоставляет надежные инструменты для программного редактирования документов. Следуя этому пошаговому руководству, вы сможете эффективно управлять содержимым документа, ресурсами и форматами вывода. Независимо от того, встраиваете ли вы ресурсы, настраиваете внешние ссылки или конвертируете документы в HTML, GroupDocs.Editor предоставляет вам функциональные возможности, необходимые для расширенного манипулирования документами.
## Часто задаваемые вопросы
### Какие форматы поддерживает GroupDocs.Editor?
GroupDocs.Editor поддерживает различные форматы, включая DOCX, XLSX, PPTX и другие.
### Могу ли я использовать GroupDocs.Editor без лицензии?
 Да, вы можете использовать его с[бесплатная пробная версия](https://releases.groupdocs.com/) или[временная лицензия](https://purchase.groupdocs.com/temporary-license/).
### Как извлечь определенные ресурсы из документа?
 Вы можете извлекать изображения, шрифты и таблицы стилей, используя предоставленные методы, такие как`Images`, `Fonts` , и`Css`.
### Можно ли настроить ссылки в выводе HTML?
Да, вы можете настроить внешние ссылки, указав собственные префиксы для изображений, CSS и шрифтов.
### Как сохранить отредактированный документ в виде HTML-файла?
 Использовать`Save` метод`EditableDocument`class для сохранения документа в виде HTML-файла, включая его ресурсы.