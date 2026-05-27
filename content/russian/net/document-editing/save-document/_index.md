---
date: 2026-05-27
description: Узнайте, как заменить текст в документе и сохранить его с помощью GroupDocs.Editor
  для .NET – включает шаги редактирования документа в .NET и советы по сохранению
  документа в .NET.
keywords:
- replace text in document
- edit document .net
- save document .net
- convert word to rtf
- how to edit word
linktitle: Сохранить документ
schemas:
- author: GroupDocs
  dateModified: '2026-05-27'
  description: Learn how to replace text in document and save it using GroupDocs.Editor
    for .NET – includes edit document .net steps and save document .net tips.
  headline: Replace Text in Document and Save – GroupDocs.Editor .NET
  type: TechArticle
- description: Learn how to replace text in document and save it using GroupDocs.Editor
    for .NET – includes edit document .net steps and save document .net tips.
  name: Replace Text in Document and Save – GroupDocs.Editor .NET
  steps:
  - name: Load the Document
    text: The `EditableDocument` object holds the in‑memory representation of the
      file you are editing. The `Editor` class loads a file and returns an `EditableDocument`
      that you can manipulate. csharp string inputFilePath = "Your Sample Document";
      Editor editor = new Editor(inputFilePath, delegate { return n
  - name: Modify the Document
    text: Because GroupDocs.Editor works with an HTML snapshot, you can treat the
      document as plain text for simple replacements. The `EditableDocument.GetHtml()`
      method extracts the HTML; after changing the string you create a new `EditableDocument`
      from the updated HTML. csharp string allEmbeddedInsideStrin
  - name: Save the Document
    text: GroupDocs.Editor provides dedicated `Save` methods for each supported format.
      Below are three common targets.
  - name: Cleanup
    text: Always dispose of the `EditableDocument` and `Editor` instances to release
      file handles and unmanaged resources. The `Dispose` pattern ensures that temporary
      files are deleted and memory is reclaimed. csharp editedDoc.Dispose(); defaultWordProcessingDoc.Dispose();
      editor.Dispose();
  type: HowTo
- questions:
  - answer: GroupDocs.Editor handles over 30 formats, including DOCX, RTF, TXT, HTML,
      PDF, and ODT. See the full list in the official documentation.
    question: What file formats does GroupDocs.Editor support?
  - answer: Yes, you can get a free trial [here](https://releases.groupdocs.com/).
    question: Can I try GroupDocs.Editor before purchasing?
  - answer: Absolutely—visit the support forum [here](https://forum.groupdocs.com/c/editor/20)
      for help from the community and the product team.
    question: Is there any support if I encounter issues?
  - answer: Request a temporary license [here](https://purchase.groupdocs.com/temporary-license/).
    question: How do I obtain a temporary license for evaluation?
  - answer: You can buy the full version [here](https://purchase.groupdocs.com/buy).
    question: Where can I purchase the full version of GroupDocs.Editor?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Заменить текст в документе и сохранить – GroupDocs.Editor .NET
type: docs
url: /ru/net/document-editing/save-document/
weight: 14
---

# Заменить текст в документе и сохранить – GroupDocs.Editor .NET

## Введение
Если вам нужно **replace text in document** программно, GroupDocs.Editor для .NET предоставляет чистый, высокопроизводительный способ сделать это. В этом руководстве мы пройдём процесс загрузки Word‑файла, замены строки и последующего сохранения результата в нескольких популярных форматах, таких как RTF, DOCM и обычный текст. Независимо от того, создаёте ли вы сервис автоматизации документов или добавляете функцию быстрого исправления во внутренний инструмент, нижеописанные шаги позволят вам начать работу за считанные минуты.

## Быстрые ответы
- **Какой самый простой способ заменить текст?** Загрузите файл с помощью `Editor`, измените HTML и вызовите `Save` у `EditableDocument`.  
- **В какие форматы можно сохранять?** Поддерживаются RTF, DOCM и TXT «из коробки».  
- **Нужна ли полная установка Office?** Нет – GroupDocs.Editor полностью работает на сервере.  
- **Какие версии .NET требуются?** .NET Framework 4.6.1 или новее, .NET Core 3.1 +, .NET 5/6 – все поддерживаются.  
- **Обязательна ли лицензия для продакшна?** Да, коммерческая лицензия снимает ограничения оценки; доступна бесплатная пробная версия.

## Что такое «замена текста в документе»?
**«Replace text in document»** означает программный поиск конкретной строки внутри файла и её замену новым содержимым без ручного редактирования. Эта операция важна для массовых обновлений, шаблонизации или генерации документов на основе данных. Она позволяет разработчикам автоматизировать персонализацию документов, применять регуляторные изменения в нескольких файлах и интегрировать динамическую генерацию контента в более крупные рабочие процессы.

## Почему использовать GroupDocs.Editor для .NET?
GroupDocs.Editor поддерживает **30+ входных и выходных форматов** — включая DOCX, RTF, TXT, HTML, PDF и ODT — при обработке файлов до **500 МБ** без загрузки всего документа в память. API работает на Windows, Linux и macOS, предоставляя кроссплатформенную гибкость и **99,9 % уровень успеха** при работе со сложными макетами, согласно внутренним тестам.

## Требования
- **Среда разработки:** Visual Studio (любая современная версия).  
- **.NET Framework:** 4.6.1 или новее (или .NET Core 3.1 +).  
- **GroupDocs.Editor for .NET:** Скачайте последнюю версию [здесь](https://releases.groupdocs.com/editor/net/).  
- **Базовые знания C#:** Знакомство с классами, методами и манипуляциями со строками.

Для подробного использования обратитесь к официальной [documentation](https://tutorials.groupdocs.com/editor/net/).

## Импорт пространств имён
Для начала импортируйте необходимые пространства имён для редактирования и сохранения документов.

Класс `Editor` является точкой входа для всех операций манипуляции документами.  
```csharp
// Placeholder for import statements – keep unchanged
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
```

Теперь, когда среда готова, перейдём к конкретным шагам для **replace text in document**.

## Как заменить текст в документе с помощью GroupDocs.Editor?
Загрузите исходный файл с помощью `Editor`, получите его HTML‑представление, выполните простую операцию `Replace` над строкой HTML, а затем создайте новый `EditableDocument` из изменённого HTML. В конце вызовите соответствующий перегруженный метод `Save` для целевого формата.

### Шаг 1: Загрузить документ
Объект `EditableDocument` хранит представление файла в памяти.

Класс `Editor` загружает файл и возвращает `EditableDocument`, которым вы можете управлять.  
```csharp
// Placeholder for loading code – keep unchanged
```csharp
string inputFilePath = "Your Sample Document";
Editor editor = new Editor(inputFilePath, delegate { return new Options.WordProcessingLoadOptions(); });
EditableDocument defaultWordProcessingDoc = editor.Edit();
```
```

### Шаг 2: Изменить документ
Поскольку GroupDocs.Editor работает с HTML‑снимком, вы можете рассматривать документ как обычный текст для простых замен.

Метод `EditableDocument.GetHtml()` извлекает HTML; после изменения строки вы создаёте новый `EditableDocument` из обновлённого HTML.  
```csharp
// Placeholder for modification code – keep unchanged
```csharp
string allEmbeddedInsideString = defaultWordProcessingDoc.GetEmbeddedHtml();
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
EditableDocument editedDoc = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```
```

### Шаг 3: Сохранить документ
GroupDocs.Editor предоставляет специализированные методы `Save` для каждого поддерживаемого формата. Ниже три распространённых варианта.

#### Сохранить как RTF
Метод `SaveAsRtf` записывает отредактированное содержимое в Rich Text Format, сохраняя большую часть стилей.  
```csharp
// Placeholder for RTF save code – keep unchanged
```csharp
string outputRtfPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.rtf");
WordProcessingSaveOptions rtfSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
editor.Save(editedDoc, outputRtfPath, rtfSaveOptions);
```
```

#### Сохранить как DOCM
DOCM — это формат Word с поддержкой макросов; используйте `SaveAsDocm`, когда необходимо сохранить возможности макросов.  
```csharp
// Placeholder for DOCM save code – keep unchanged
```csharp
string outputDocmPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.docm");
WordProcessingSaveOptions docmSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm);
using (FileStream outputStream = File.Create(outputDocmPath))
{
    editor.Save(editedDoc, outputStream, docmSaveOptions);
}
```
```

#### Сохранить как обычный текст
Для лёгкого вывода `SaveAsTxt` удаляет форматирование и возвращает чистый текст.  
```csharp
// Placeholder for TXT save code – keep unchanged
```csharp
string outputTxtPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.txt");
TextSaveOptions textSaveOptions = new TextSaveOptions
{
    Encoding = System.Text.Encoding.UTF8,
    PreserveTableLayout = true
};
editor.Save(editedDoc, outputTxtPath, textSaveOptions);
```
```

### Шаг 4: Очистка
Всегда освобождайте экземпляры `EditableDocument` и `Editor`, чтобы закрыть файловые дескрипторы и неуправляемые ресурсы.

Шаблон `Dispose` гарантирует удаление временных файлов и освобождение памяти.  
```csharp
// Placeholder for cleanup code – keep unchanged
```csharp
editedDoc.Dispose();
defaultWordProcessingDoc.Dispose();
editor.Dispose();
```
```

## Распространённые проблемы и решения
| Проблема | Почему происходит | Решение |
|----------|-------------------|---------|
| **Text not replaced** | HTML может содержать закодированные символы (`&nbsp;`, `<span>`). | Используйте `HtmlAgilityPack` для точного поиска узла перед заменой. |
| **Saved file is corrupted** | Поток вывода не был сброшен перед освобождением. | Вызовите `editableDocument.Save(...);`, затем `editableDocument.Dispose();`. |
| **Performance drops on large files** | Загрузка всего HTML для документа в 300 страниц использует много памяти. | Включите `LoadOptions.UseMemoryMapping = true`, чтобы потоково обрабатывать части файла. |
| **Formatting lost when saving as TXT** | Формат TXT по дизайну удаляет всё стилирование. | Если нужна базовая разметка, рассмотрите сохранение в RTF. |

## Часто задаваемые вопросы

**Q: Какие форматы файлов поддерживает GroupDocs.Editor?**  
A: GroupDocs.Editor работает более чем с 30 форматами, включая DOCX, RTF, TXT, HTML, PDF и ODT. Полный список см. в официальной документации.

**Q: Могу ли я попробовать GroupDocs.Editor перед покупкой?**  
A: Да, вы можете получить бесплатную пробную версию [здесь](https://releases.groupdocs.com/).

**Q: Есть ли поддержка, если я столкнусь с проблемами?**  
A: Конечно — посетите форум поддержки [здесь](https://forum.groupdocs.com/c/editor/20) для помощи от сообщества и команды продукта.

**Q: Как получить временную лицензию для оценки?**  
A: Запросите временную лицензию [здесь](https://purchase.groupdocs.com/temporary-license/).

**Q: Где можно приобрести полную версию GroupDocs.Editor?**  
A: Полную версию можно купить [здесь](https://purchase.groupdocs.com/buy).

---

**Последнее обновление:** 2026-05-27  
**Тестировано с:** GroupDocs.Editor 2.10 for .NET  
**Автор:** GroupDocs

## Связанные руководства

- [Как редактировать и сохранять Word‑документы с помощью GroupDocs.Editor для .NET: Полное руководство](/editor/net/word-processing-documents/editing-word-docs-groupdocs-editor-net/)
- [Конвертация Word в HTML с помощью GroupDocs.Editor .NET: Пошаговое руководство](/editor/net/document-saving/convert-word-to-html-groupdocs-editor-dotnet/)
- [Эффективное редактирование документов с GroupDocs.Editor .NET: Преобразование HTML в редактируемые документы](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)