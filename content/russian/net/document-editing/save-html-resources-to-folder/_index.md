---
title: Сохранить HTML-ресурсы в папку
linktitle: Сохранить HTML-ресурсы в папку
second_title: GroupDocs.Editor .NET API
description: Узнайте, как извлекать ресурсы HTML из документов с помощью Groupdocs.Editor для .NET. Это подробное руководство содержит пошаговые инструкции для разработчиков.
weight: 13
url: /ru/net/document-editing/save-html-resources-to-folder/
---
## Введение
Groupdocs.Editor для .NET — это мощный инструмент, который позволяет разработчикам легко манипулировать и конвертировать документы в своих приложениях .NET. Если вам нужно извлечь HTML-ресурсы из документа или выполнить сложные задачи редактирования, Groupdocs.Editor упрощает процесс благодаря интуитивно понятному API и обширной документации.
## Предварительные условия
Прежде чем приступить к изучению руководства, убедитесь, что у вас есть следующие предварительные условия:
1. Базовые знания C# и .NET. Знакомство с языком программирования C# и платформой .NET необходимо для выполнения примеров.
2.  Groupdocs.Editor для библиотеки .NET: загрузите и установите Groupdocs.Editor для библиотеки .NET с сайта[Веб-сайт](https://releases.groupdocs.com/editor/net/).
3. Среда разработки: настройте предпочтительную среду разработки, например Visual Studio или любую другую совместимую среду разработки.

## Импортировать пространства имен
Для начала импортируйте необходимые пространства имен в свой проект C#:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```
##Теперь давайте разобьем процесс сохранения HTML-ресурсов в папку с помощью Groupdocs.Editor for .NET на несколько этапов:
## Шаг 1. Инициализируйте Groupdocs.Editor
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
 Сначала инициализируйте`Editor`объект, указав путь к образцу документа. В этом примере мы используем документ Word, поэтому указываем`WordProcessingLoadOptions` как тип документа.
## Шаг 2: Редактировать документ
```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
 Далее создайте`EditableDocument` объект, вызвав`Edit` метод`Editor` объект. Это позволяет выполнять операции редактирования документа.
## Шаг 3: Извлеките ресурсы
```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
Извлекайте из документа такие ресурсы, как изображения, шрифты и таблицы стилей, и сохраняйте их в соответствующих списках.
## Шаг 4. Укажите выходную папку
```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
Определите выходную папку, в которой будут сохранены извлеченные ресурсы. Вы можете настроить путь к папке в соответствии с вашими требованиями.
## Шаг 5: Сохраните ресурсы
```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
Прокрутите каждый ресурс изображения, сохраните его в выходной папке и отобразите соответствующую информацию, такую как имя файла, тип и размеры.
```csharp
		foreach (FontResourceBase oneFont in fonts)
		{
			Console.WriteLine("Saving {0} of {1} type",
				oneFont.FilenameWithExtension, oneFont.Type.FormalName);
			oneFont.Save(Path.Combine(outputFolder, oneFont.FilenameWithExtension));
		}
```
Аналогичным образом сохраните каждый ресурс шрифта в выходной папке.
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
Наконец, сохраните каждую таблицу стилей в выходной папке и завершите процесс редактирования.

## Заключение
В заключение, Groupdocs.Editor для .NET предоставляет удобное решение для программного управления и манипулирования документами в приложениях .NET. Следуя этому руководству, вы сможете легко извлекать ресурсы HTML из документов и настроить процесс в соответствии с вашими конкретными требованиями.
## Часто задаваемые вопросы
### Совместим ли Groupdocs.Editor с другими форматами документов, кроме Word?
Да, Groupdocs.Editor поддерживает широкий спектр форматов документов, включая Excel, PowerPoint, PDF и другие.
### Могу ли я интегрировать Groupdocs.Editor в свое веб-приложение?
Безусловно, Groupdocs.Editor предлагает бесшовную интеграцию с веб-приложениями, разработанными на платформе .NET.
### Предоставляет ли Groupdocs.Editor поддержку служб облачного хранения?
Да, Groupdocs.Editor поддерживает интеграцию с популярными облачными сервисами хранения, такими как Google Drive, Dropbox и Microsoft OneDrive.
### Доступна ли бесплатная пробная версия Groupdocs.Editor?
Да, вы можете воспользоваться бесплатной пробной версией Groupdocs.Editor с веб-сайта.
### Как я могу получить техническую поддержку для Groupdocs.Editor?
Для получения технической помощи и поддержки сообщества вы можете посетить форум Groupdocs.Editor.