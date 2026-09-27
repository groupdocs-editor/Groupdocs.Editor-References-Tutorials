---
date: 2026-09-26
description: Узнайте, как работать с префиксом css и извлекать css content с помощью
  GroupDocs.Editor для .NET в этом подробном step‑by‑step tutorial.
keywords:
- handle css prefix
- extract css content
- edit document css
- prepend url to css
lastmod: 2026-09-26
linktitle: Обработка CSS Content с префиксом
og_description: Узнайте, как работать с префиксом css и извлекать css content с помощью
  GroupDocs.Editor для .NET. Следуйте step‑by‑step руководству, чтобы добавлять URLs
  к CSS resources и получать stylesheets.
og_image_alt: Developer guide showing css prefix handling with GroupDocs.Editor for
  .NET
og_title: Как работать с префиксом css в GroupDocs.Editor для .NET
schemas:
- author: GroupDocs
  dateModified: '2026-09-26'
  description: Learn how to handle css prefix and extract css content using GroupDocs.Editor
    for .NET in this detailed step‑by‑step tutorial.
  headline: How to handle css prefix in GroupDocs.Editor for .NET
  type: TechArticle
- questions:
  - answer: Yes, GroupDocs.Editor for .NET supports PDF, Word, Excel, PowerPoint,
      and many other formats.
    question: Can I use GroupDocs.Editor for .NET with other document formats?
  - answer: Absolutely! You can start your free trial on the [GroupDocs free trial
      page](https://releases.groupdocs.com/).
    question: Is there a free trial available for GroupDocs.Editor for .NET?
  - answer: You can obtain a temporary license from the [temporary license page](https://purchase.groupdocs.com/temporary-license/).
    question: How do I get a temporary license for GroupDocs.Editor for .NET?
  - answer: Detailed documentation is available on the [GroupDocs.Editor for .NET
      documentation site](https://tutorials.groupdocs.com/editor/net/).
    question: Where can I find detailed documentation for GroupDocs.Editor for .NET?
  - answer: You can get support through the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).
    question: What support options are available for GroupDocs.Editor for .NET?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
tags:
- css handling
- GroupDocs.Editor
- .NET document processing
- css prefix
- api tutorial
title: Как работать с префиксом css в GroupDocs.Editor для .NET
type: docs
url: /ru/net/css-handling/handle-css-content-with-prefix/
weight: 11
---

# Как работать с префиксом CSS в GroupDocs.Editor для .NET

В этом руководстве вы узнаете **как работать с префиксом CSS**, работая с таблицами стилей внутри документа с помощью GroupDocs.Editor для .NET. Если вам нужно добавить URL‑префикс к изображениям, шрифтам или любому внешнему ресурсу, нижеописанные шаги покажут, как **работать с префиксом CSS** и как **извлечь содержимое CSS** для дальнейшей обработки. К концу руководства вы сможете переписать пути к ресурсам, получить необработанные строки CSS и уверенно интегрировать их в ваш веб‑рабочий процесс.

## Быстрые ответы
- **Что означает “handle css prefix”?** Добавление пользовательского URL‑префикса к внешним ресурсам, указанным в CSS.  
- **Какой метод API возвращает стили CSS?** `EditableDocument.GetCssContent(...)`.  
- **Нужна ли лицензия?** Доступна пробная лицензия; для продакшн‑использования требуется коммерческая лицензия.  
- **Какие версии .NET поддерживаются?** .NET Framework 4.5+ и .NET Core/5/6.  
- **Можно ли изменить префикс во время выполнения?** Да — просто передайте другую строку в `GetCssContent`.

## Что такое префикс CSS?
Термин относится к переписыванию URL‑адресов изображений, шрифтов или любых внешних ресурсов внутри файла CSS так, чтобы они указывали на контролируемое вами место, например CDN или защищённый сервер. Добавляя единый базовый URL, вы гарантируете корректную загрузку каждого ресурса при отображении документа в браузере или веб‑просмотрщике.

## Зачем использовать GroupDocs.Editor для извлечения содержимого CSS?
GroupDocs.Editor может читать оригинальный CSS, встроенный в документы обработки текста, возвращать необработанные строки таблиц стилей и позволять вам манипулировать ими перед рендерингом или сохранением. Это устраняет необходимость ручного парсинга, гарантирует точность внутреннего представления документа и поддерживает **30+ форматов файлов**, обрабатывая файлы до **500 MB** без загрузки всего файла в память.

## Предварительные требования
Перед началом убедитесь, что у вас есть следующее:
- Visual Studio: вам понадобится рабочая установка Visual Studio.  
- .NET Framework: убедитесь, что .NET Framework установлен.  
- GroupDocs.Editor for .NET: вы можете скачать его со страницы [страница загрузки GroupDocs.Editor для .NET](https://releases.groupdocs.com/editor/net/).  
- Пример документа: подготовьте пример документа для редактирования.

## Импорт пространств имён
First, let’s import the necessary namespaces to ensure our code runs smoothly. This step gives us access to the core classes of GroupDocs.Editor.

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Editor.Options;
```

## Шаг 1: Инициализация редактора
The `Editor` class is the entry point for working with documents in GroupDocs.Editor. It manages loading, editing, and saving operations.  
The first step involves creating an `Editor` instance with your sample document. This sets up the editing environment.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```

## Шаг 2: Редактирование документа
The `EditableDocument` object represents the editable version of the file and exposes its internal parts, such as CSS, images, and HTML.  
Next, we obtain an `EditableDocument` object. This object allows us to work with the document’s internal CSS.

```csharp
    using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
    {
```

## Шаг 3: Установка внешних префиксов
Define the URL prefixes for images and fonts. These prefixes will be prepended to every image and font reference found in the CSS.

```csharp
        string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
        string externalFontsPrefix = "http://www.mywebsite.com/fonts/id=";
```

## Шаг 4: Извлечение содержимого CSS с префиксами
`GetCssContent` returns a collection of CSS stylesheet strings that already contain the prefixed URLs you supplied.  
Call `GetCssContent`, passing the prefixes you just defined. The method returns a list of CSS stylesheet strings that already contain the prefixed URLs.

```csharp
        List<string> stylesheets = document.GetCssContent(externalImagesPrefix, externalFontsPrefix);
```

## Шаг 5: Вывод результатов
Print the number of stylesheets found and display each stylesheet. This helps you verify that the prefixes were applied correctly.

```csharp
        Console.WriteLine("There are {0} stylesheets in the input document", stylesheets.Count);
        foreach (string css in stylesheets)
        {
            Console.WriteLine(css);
        }
    }
}
```

## Распространённые проблемы и решения
- **Не возвращены таблицы стилей** — Убедитесь, что исходный документ действительно содержит CSS (например, Word‑документ со стилизованными таблицами или встроенным HTML).  
- **Некорректные URL** — Проверьте, что строки префикса заканчиваются правильным разделителем (`/` или `=`) для маршрутизации вашего сервера.  
- **Проблемы с производительностью** — Для очень больших документов рассмотрите обработку таблиц стилей пакетами, чтобы избежать высокого потребления памяти.

## Часто задаваемые вопросы

**В: Могу ли я использовать GroupDocs.Editor для .NET с другими форматами документов?**  
О: Да, GroupDocs.Editor для .NET поддерживает PDF, Word, Excel, PowerPoint и многие другие форматы.

**В: Доступна ли бесплатная пробная версия GroupDocs.Editor для .NET?**  
О: Конечно! Вы можете начать бесплатную пробную версию на странице [страница бесплатной пробной версии GroupDocs](https://releases.groupdocs.com/).

**В: Как получить временную лицензию для GroupDocs.Editor для .NET?**  
О: Вы можете получить временную лицензию на странице [temporary license page](https://purchase.groupdocs.com/temporary-license/).

**В: Где найти подробную документацию по GroupDocs.Editor для .NET?**  
О: Подробная документация доступна на сайте [GroupDocs.Editor for .NET documentation site](https://tutorials.groupdocs.com/editor/net/).

**В: Какие варианты поддержки доступны для GroupDocs.Editor для .NET?**  
О: Вы можете получить поддержку через [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).

## Дополнительные часто задаваемые вопросы

**В: Могу ли я изменить префикс после извлечения CSS?**  
О: Да. Вызовите `GetCssContent` снова с другой строкой префикса; метод всегда использует переданные вами значения во время выполнения.

**В: Работает ли это с документами, защищёнными паролем?**  
О: Да. Укажите пароль в `WordProcessingLoadOptions` при создании экземпляра `Editor`.

**В: Можно ли сохранить изменённый CSS обратно в документ?**  
О: В текущей версии GroupDocs.Editor доступ к CSS только для чтения. Чтобы сохранить изменения, необходимо заменить оригинальную таблицу стилей с помощью XML‑API документа.

---

**Последнее обновление:** 2026-09-26  
**Тестировано с:** GroupDocs.Editor 23.12 for .NET  
**Автор:** GroupDocs

## Связанные руководства

- [Извлечение внешнего CSS из Word‑документов с помощью GroupDocs.Editor .NET: Полное руководство](/editor/net/html-web-documents/extract-external-css-word-docs-groupdocs-editor-dotnet/)
- [Извлечение и добавление префикса HTML из Word‑документов с помощью GroupDocs.Editor .NET](/editor/net/html-web-documents/groupdocs-editor-dotnet-extract-prefix-html-word-docs/)
- [Как извлечь и изменить HTML‑контент в Word‑документах с помощью GroupDocs.Editor .NET](/editor/net/html-web-documents/extract-modify-html-content-word-docs-groupdocs-editor-net/)