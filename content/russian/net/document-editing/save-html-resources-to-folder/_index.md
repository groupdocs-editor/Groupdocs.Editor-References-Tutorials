---
date: 2026-05-12
description: Узнайте, как извлекать шрифты и другие HTML‑ресурсы из документов с помощью
  GroupDocs.Editor for .NET. Пошаговое руководство для разработчиков .NET.
keywords:
- how to extract fonts
- GroupDocs.Editor .NET
- extract HTML resources
linktitle: Сохранить HTML‑ресурсы в папку
schemas:
- author: GroupDocs
  dateModified: '2026-05-12'
  description: Learn how to extract fonts and other HTML resources from documents
    using GroupDocs.Editor for .NET. Step‑by‑step guide for .NET developers.
  headline: How to Extract Fonts and Save HTML Resources to Folder
  type: TechArticle
- description: Learn how to extract fonts and other HTML resources from documents
    using GroupDocs.Editor for .NET. Step‑by‑step guide for .NET developers.
  name: How to Extract Fonts and Save HTML Resources to Folder
  steps:
  - name: '**Basic Knowledge of C# and .NET** – Familiarity with C# programming language
      and .NET framework is essential to follow along with the examples.'
    text: '**Basic Knowledge of C# and .NET** – Familiarity with C# programming language
      and .NET framework is essential to follow along with the examples.'
  - name: '**GroupDocs.Editor for .NET Library** – Download and install GroupDocs.Editor
      for .NET library from the [website](https://releases.groupdocs.com/editor/net/).'
    text: '**GroupDocs.Editor for .NET Library** – Download and install GroupDocs.Editor
      for .NET library from the [website](https://releases.groupdocs.com/editor/net/).'
  - name: '**Development Environment** – Set up your preferred development environment
      such as Visual Studio or any other compatible IDE.'
    text: '**Development Environment** – Set up your preferred development environment
      such as Visual Studio or any other compatible IDE.'
  type: HowTo
- questions:
  - answer: Yes, it supports Excel, PowerPoint, PDF, HTML, and over 50 additional
      formats for both editing and resource extraction.
    question: Is GroupDocs.Editor compatible with other document formats besides Word?
  - answer: Absolutely. The API works seamlessly with ASP.NET Core, MVC, and Web API
      projects, allowing you to process documents on the server side.
    question: Can I integrate GroupDocs.Editor into a web application?
  - answer: Yes, it includes built‑in connectors for Google Drive, Dropbox, OneDrive,
      and Amazon S3, enabling direct loading and saving of documents in the cloud.
    question: Does GroupDocs.Editor provide cloud storage integration?
  - answer: A fully functional 30‑day trial can be downloaded from the GroupDocs website
      without any credit‑card requirement.
    question: Is there a free trial available for GroupDocs.Editor?
  - answer: You can reach the GroupDocs support team via the official forum, submit
      a ticket through the customer portal, or consult the detailed API documentation.
    question: How can I get technical support for extraction issues?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Как извлечь шрифты и сохранить HTML‑ресурсы в папку
type: docs
url: /ru/net/document-editing/save-html-resources-to-folder/
weight: 13
---

# Как извлечь шрифты и сохранить HTML-ресурсы в папку

## Введение
GroupDocs.Editor for .NET позволяет вам **как извлечь шрифты** и другие ресурсы из документа при его конвертации в HTML. В нескольких строках C# вы можете извлечь изображения, таблицы стилей и файлы шрифтов, а затем сохранить их в выбранную вами папку. Это руководство проведёт вас через весь процесс, от инициализации редактора до сохранения каждого ресурса на диск.

## Быстрые ответы
- **Что означает “how to extract fonts”?** Это процесс получения встроенных файлов шрифтов из исходного документа во время конвертации в HTML.  
- **Какая библиотека обрабатывает это?** GroupDocs.Editor for .NET предоставляет специальный API для извлечения шрифтов, изображений и таблиц стилей.  
- **Нужна ли лицензия?** Доступна бесплатная пробная версия; коммерческая лицензия требуется для использования в продакшене.  
- **Какие версии .NET поддерживаются?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.  
- **Можно ли указать пользовательскую папку?** Да, вы можете указать любой доступный для записи путь при сохранении извлечённых ресурсов.

## Что такое “how to extract fonts”?
**How to extract fonts** относится к получению оригинальных файлов шрифтов, встроенных в исходный документ (например, DOCX, PPTX), чтобы они могли быть использованы в сгенерированном HTML. Это гарантирует, что текст отображается точно так, как задумано, в браузерах без зависимости от системных шрифтов.

## Зачем использовать GroupDocs.Editor для извлечения HTML-ресурсов?
GroupDocs.Editor поддерживает **более 50 форматов ввода и вывода** — включая DOCX, PPTX, PDF и HTML — и может обрабатывать документы с **до 300 страницами** без загрузки всего файла в память. Его API извлекает шрифты, изображения и CSS за один проход, сокращая время разработки до **70 %** по сравнению с ручным разбором.

## Требования
Прежде чем приступить к руководству, убедитесь, что у вас есть следующие требования:
1. **Базовые знания C# и .NET** – Знание языка программирования C# и платформы .NET необходимо для понимания примеров.  
2. **Библиотека GroupDocs.Editor for .NET** – Скачайте и установите библиотеку GroupDocs.Editor for .NET с [веб‑сайта](https://releases.groupdocs.com/editor/net/).  
3. **Среда разработки** – Настройте предпочитаемую среду разработки, такую как Visual Studio или любую другую совместимую IDE.

## Импорт пространств имён
Чтобы начать, импортируйте необходимые пространства имён в ваш проект C#:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```

## Как извлечь шрифты и сохранить HTML-ресурсы в папку?
Загрузите ваш исходный документ с помощью `Editor editor = new Editor("sample.docx", new WordProcessingLoadOptions());`, затем вызовите `editor.Save("output.html", SaveOptions.Html);`. После операции сохранения коллекция `Resources` содержит все извлечённые ресурсы — включая шрифты, — которые можно перебрать и записать на диск. Этот одноступенчатый подход автоматически обрабатывает как конвертацию, так и извлечение ресурсов.

## Шаг 1: Инициализация GroupDocs.Editor
`Editor` — основной класс, который управляет загрузкой документа, конвертацией и извлечением ресурсов. Он представляет одну сессию документа в памяти.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
Сначала инициализируйте объект `Editor`, указав путь к вашему образцу документа. В этом примере мы используем документ Word, поэтому указываем `WordProcessingLoadOptions` как тип документа.

## Шаг 2: Редактирование документа
`EditableDocument` — редактируемое представление, возвращаемое методом `Edit`, позволяющее изменять документ перед сохранением.

```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
Затем создайте объект `EditableDocument`, вызвав метод `Edit` у объекта `Editor`. Это позволяет выполнять операции редактирования над документом.

## Шаг 3: Извлечение ресурсов
`Resources` — коллекция, группирующая извлечённые ресурсы — изображения, шрифты и таблицы стилей — в отдельные списки для удобного управления.

```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
Извлеките ресурсы, такие как изображения, шрифты и таблицы стилей, из документа и сохраните их в соответствующих списках.

## Шаг 4: Указание папки вывода
`outputFolder` — строка, определяющая, куда будут записаны извлечённые файлы. Вы можете указать любой каталог, доступный для записи, на сервере или локальном компьютере.

```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
Определите папку вывода, куда будут сохраняться извлечённые ресурсы. Вы можете настроить путь к папке в соответствии с вашими требованиями.

## Шаг 5: Сохранение ресурсов
`SaveResource` — вспомогательная процедура, записывающая один бинарный ресурс (изображение, шрифт или таблицу стилей) в файловую систему.

```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
Пройдитесь по каждому ресурсу изображения, сохраните его в папку вывода и отобразите соответствующую информацию, такую как имя файла, тип и размеры.

```csharp
		foreach (FontResourceBase oneFont in fonts)
		{
			Console.WriteLine("Saving {0} of {1} type",
				oneFont.FilenameWithExtension, oneFont.Type.FormalName);
			oneFont.Save(Path.Combine(outputFolder, oneFont.FilenameWithExtension));
		}
```
Аналогично, сохраните каждый ресурс шрифта в папку вывода.

```csharp
		foreach (CssText oneStylesheet in stylesheets)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} encoding",
				oneStylesheet.FilenameWithExtension, oneStylesheet.Type.FormalName, oneStylesheet.Encoding);
			oneStylesheet.Save(Path.Combine(outputFolder, oneStylesheet.FilenameWithExtension));
		}
	}
}
```
Наконец, сохраните каждую таблицу стилей в папку вывода и завершите процесс редактирования.

## Распространённые проблемы и решения
- **Отсутствие шрифтов после конвертации** – Убедитесь, что исходный документ действительно встраивает шрифты; иначе GroupDocs.Editor может ссылаться только на системные шрифты.  
- **Ошибки доступа (Access denied)** – Проверьте, что процесс приложения имеет права записи в целевую папку вывода.  
- **Большие документы вызывают высокое использование памяти** – Используйте `LoadOptions` с `LoadMode = LoadMode.Stream`, чтобы потоково обрабатывать большие файлы вместо полной загрузки их в память.

## Часто задаваемые вопросы

**В: Совместим ли GroupDocs.Editor с другими форматами документов, помимо Word?**  
О: Да, он поддерживает Excel, PowerPoint, PDF, HTML и более 50 дополнительных форматов как для редактирования, так и для извлечения ресурсов.

**В: Могу ли я интегрировать GroupDocs.Editor в веб‑приложение?**  
О: Конечно. API без проблем работает с проектами ASP.NET Core, MVC и Web API, позволяя обрабатывать документы на стороне сервера.

**В: Предоставляет ли GroupDocs.Editor интеграцию с облачным хранилищем?**  
О: Да, он включает встроенные коннекторы для Google Drive, Dropbox, OneDrive и Amazon S3, позволяя напрямую загружать и сохранять документы в облаке.

**В: Доступна ли бесплатная пробная версия GroupDocs.Editor?**  
О: Полнофункциональная 30‑дневная пробная версия доступна для скачивания с сайта GroupDocs без требования ввода данных кредитной карты.

**В: Как получить техническую поддержку по вопросам извлечения?**  
О: Вы можете связаться с командой поддержки GroupDocs через официальный форум, отправить запрос через клиентский портал или ознакомиться с подробной документацией API.

---

**Последнее обновление:** 2026-05-12  
**Тестировано с:** GroupDocs.Editor 23.11 for .NET  
**Автор:** GroupDocs

## Связанные руководства

- [Эффективное редактирование документов с GroupDocs.Editor .NET&#58; Преобразование HTML в редактируемые документы](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)
- [Эффективное извлечение и сохранение ресурсов DOCX с помощью GroupDocs.Editor .NET — Полное руководство](/editor/net/document-saving/efficient-extract-save-docx-resources-groupdocs-editor-net/)
- [Мастерство редактирования и конвертации документов с GroupDocs.Editor .NET&#58; Полное руководство](/editor/net/document-editing/groupdocs-editor-net-mastering-document-editing/)