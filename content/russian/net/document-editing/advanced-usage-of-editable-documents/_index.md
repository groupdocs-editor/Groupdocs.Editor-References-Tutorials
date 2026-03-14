---
date: 2026-03-14
description: Узнайте, как извлекать изображения из DOCX, конвертировать DOCX в HTML
  и сохранять документ в формате HTML с помощью GroupDocs.Editor для .NET.
linktitle: Extract Images from DOCX – Advanced Editable Document Usage
second_title: GroupDocs.Editor .NET API
title: Извлечение изображений из DOCX — Продвинутое использование редактируемого документа
type: docs
url: /ru/net/document-editing/advanced-usage-of-editable-documents/
weight: 11
---

# Извлечение изображений из DOCX – расширенное использование редактируемых документов

Если вы разработчик .NET и хотите **извлечь изображения из DOCX** и расширить возможности редактирования документов, GroupDocs.Editor for .NET предлагает мощный набор инструментов. Это подробное руководство проведёт вас через расширенное использование редактируемых документов с помощью GroupDocs.Editor, подробно разбирая каждый шаг, чтобы вы могли полностью раскрыть его потенциал.

## Быстрые ответы
- **Как извлечь изображения из файла DOCX?** Используйте `EditableDocument.Images` после загрузки документа с помощью `Editor`.
- **Можно ли конвертировать DOCX в HTML с встроенными ресурсами?** Да — вызовите `EditableDocument.GetEmbeddedHtml()` или `GetContent()` для получения HTML‑разметки.
- **Каким методом сохранить отредактированный документ как HTML?** `EditableDocument.Save(htmlFilePath)` создаёт HTML‑файл с папкой ресурсов.
- **Можно ли извлечь шрифты из документа Word?** Используйте `EditableDocument.Fonts` для получения всех шрифтовых ресурсов.
- **Нужна ли лицензия для использования в продакшене?** Требуется действующая лицензия GroupDocs.Editor; доступна бесплатная пробная версия.

## Что такое **extract images from docx**?
Извлечение изображений из файла DOCX означает программное получение каждой картинки, встроенной в документ Word, чтобы вы могли повторно использовать, изменять или хранить их отдельно. GroupDocs.Editor предоставляет коллекцию `Images` в экземпляре `EditableDocument`, что делает эту задачу простой.

## Почему стоит использовать GroupDocs.Editor для этого процесса?
- **Полный контроль** над ресурсами документа (изображения, шрифты, CSS) без ручного обращения с ZIP‑архивами.  
- **Бесшовная конверсия** из DOCX в HTML с сохранением макета и стилей.  
- **Лёгкое извлечение ресурсов** для пользовательской обработки изображений, внедрения шрифтов или доставки через CDN.  
- **Надёжный паттерн освобождения** гарантирует отсутствие утечек памяти в длительно работающих сервисах.

## Предварительные требования
- Установленная Visual Studio на вашей машине разработки.  
- .NET Framework, совместимый с GroupDocs.Editor.  
- Библиотека GroupDocs.Editor for .NET. Вы можете [скачать её здесь](https://releases.groupdocs.com/editor/net/).  
- Действительная лицензия GroupDocs.Editor. Вы можете получить [бесплатную пробную версию](https://releases.groupdocs.com/) или приобрести [временную лицензию](https://purchase.groupdocs.com/temporary-license/).

## Импорт пространств имён
Для начала убедитесь, что импортировали необходимые пространства имён в ваш .NET‑проект:

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

## Шаг 1: Создание экземпляра EditableDocument
Сначала необходимо создать экземпляр `EditableDocument`, загрузив и открыв входной документ поддерживаемого формата.

```csharp
string inputFilePath = "YourSampleDocument.docx";
Editor editor = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```

На этом этапе мы загружаем входной документ и подготавливаем его к редактированию.

## Как **extract images from DOCX**?
Далее мы рассматриваем возможности извлечения ресурсов, начиная с самой распространённой задачи — получения всех изображений из файла Word.

## Шаг 2: Извлечение ресурсов документа
`EditableDocument` содержит различные ресурсы, которые можно извлекать и обрабатывать. Разберём их по порядку:

### Шаг 2.1: Извлечение всего документа в виде HTML
Можно сгенерировать одну строку, содержащую весь документ со всеми ресурсами, встроенными в HTML.

```csharp
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```

Эта строка будет довольно большой, так как включает таблицы стилей, изображения и шрифты, закодированные в base64.

### Шаг 2.2: Извлечение всех изображений *(ключевое слово действия)*
Извлеките все изображения из документа — это основа **extract images from docx**.

```csharp
List<IImageResource> allImages = beforeEdit.Images;
```

### Шаг 2.3: Извлечение всех шрифтов *(вторичное ключевое слово)*
Если также нужно **extract fonts from word**, используйте следующий вызов:

```csharp
List<FontResourceBase> allFonts = beforeEdit.Fonts;
```

### Шаг 2.4: Извлечение всех таблиц стилей
Извлеките все таблицы стилей в текстовом формате.

```csharp
List<CssText> allStylesheets = beforeEdit.Css;
```

### Шаг 2.5: Сбор всех ресурсов
Соберите все ресурсы одним вызовом.

```csharp
List<IHtmlResource> allResources = beforeEdit.AllResources;
```

Это включает изображения, шрифты и таблицы стилей.

### Шаг 2.6: Получение HTML‑разметки
Получите HTML‑разметку документа без встроенных ресурсов.

```csharp
string htmlMarkup = beforeEdit.GetContent();
```

## Как **convert docx to html** с пользовательской обработкой?
Иногда требуется изменить внешние ссылки, чтобы они указывали на ваши собственные обработчики ресурсов.

## Шаг 3: Корректировка внешних ссылок
### Шаг 3.1: Подготовка пользовательских префиксов
Подготовьте префиксы, которые будут добавляться к оригинальным внешним ссылкам.

```csharp
string customImagesRequesthandlerUri = "http://example.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://example.com/CssHandler/id=";
string customFontsRequesthandlerUri = "http://example.com/FontsHandler/id=";
```

### Шаг 3.2: Генерация HTML‑разметки с префиксами
Сгенерируйте HTML‑разметку с изменёнными ссылками.

```csharp
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```

### Шаг 3.3: Получение только тела HTML
Некоторые WYSIWYG‑редакторы работают только с чистой HTML‑разметкой без заголовков.

```csharp
string onlyBodyContent = beforeEdit.GetBodyContent();
```

### Шаг 3.4: Тело HTML с префиксами
Сгенерируйте содержимое только тела с пользовательскими префиксами для изображений.

```csharp
string prefixedBodyContent = beforeEdit.GetBodyContent(customImagesRequesthandlerUri);
```

### Шаг 3.5: Извлечение таблиц стилей
Извлеките таблицы стилей, используемые в документе.

```csharp
List<string> stylesheets = beforeEdit.GetCssContent();
```

### Шаг 3.6: Таблицы стилей с префиксами
Извлеките таблицы стилей с пользовательскими префиксами.

```csharp
List<string> prefixedStylesheets = beforeEdit.GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri);
```

## Как **save document as html** правильно?
## Шаг 4: Сохранение документа как HTML
Сохраните отредактированный документ в виде HTML‑файла, включая его ресурсы.

```csharp
string htmlFilePath = Path.Combine("output", Path.GetFileNameWithoutExtension(inputFilePath) + ".html");
beforeEdit.Save(htmlFilePath);
```

Этот метод создаёт отдельный каталог для ресурсов, таких как таблицы стилей, изображения и шрифты.

## Шаг 5: Освобождение EditableDocument
`EditableDocument` реализует `IDisposable` и предоставляет возможность проверить, был ли объект освобождён.

```csharp
Console.WriteLine("EditableDocument is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");
```

### Шаг 5.1 Обработка события Dispose
Вы также можете подписаться на событие освобождения.

```csharp
EventHandler someMethod = delegate { Console.WriteLine("Disposing event was spotted!"); };
beforeEdit.Disposed += someMethod;
```

## Шаг 6: Создание EditableDocument из HTML
Создайте экземпляр `EditableDocument` из HTML‑документа.

### Шаг 6.1: Из HTML‑файла

```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
```

### Шаг 6.2: Из HTML‑разметки

```csharp
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);
```

Эти экземпляры (`afterEditFromFile` и `afterEditFromMarkup`) идентичны оригинальному (`beforeEdit`).

## Шаг 7: Ручное освобождение
Ручное освобождение ваших экземпляров `EditableDocument`.

```csharp
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```

Это гарантирует корректную очистку ресурсов.

## Распространённые проблемы и решения
- **Изображения не отображаются после извлечения:** Убедитесь, что документ действительно содержит встроенные изображения и что вы обращаетесь к `beforeEdit.Images` после вызова `Edit`.  
- **Шрифты отсутствуют в HTML‑выводе:** Убедитесь, что вызываете `GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri)`, чтобы правильно внедрить URL‑адреса шрифтов.  
- **Большие HTML‑строки вызывают нагрузку на память:** Используйте `GetContent()` для разметки без встроенных ресурсов и обслуживайте изображения/CSS из отдельных файлов.

## Часто задаваемые вопросы

**В: Какие форматы поддерживает GroupDocs.Editor?**  
О: GroupDocs.Editor поддерживает DOCX, XLSX, PPTX и многие другие популярные офисные форматы.

**В: Можно ли использовать GroupDocs.Editor без лицензии?**  
О: Да, вы можете использовать его с [бесплатной пробной версией](https://releases.groupdocs.com/) или [временной лицензией](https://purchase.groupdocs.com/temporary-license/).

**В: Как извлечь конкретные ресурсы из документа?**  
О: Используйте коллекции `Images`, `Fonts` и `Css` у экземпляра `EditableDocument`.

**В: Можно ли изменить ссылки в HTML‑выводе?**  
О: Да, передайте пользовательские URI‑префиксы в `GetContent` или `GetBodyContent`, чтобы переписать ссылки на изображения, CSS и шрифты.

**В: Как сохранить отредактированный документ как HTML‑файл?**  
О: Вызовите метод `Save` у экземпляра `EditableDocument`, указав путь к файлу, заканчивающийся на `.html`.

---

**Последнее обновление:** 2026-03-14  
**Тестировано с:** GroupDocs.Editor for .NET (последний релиз)  
**Автор:** GroupDocs