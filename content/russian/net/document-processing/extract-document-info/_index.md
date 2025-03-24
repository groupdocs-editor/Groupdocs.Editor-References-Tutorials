---
title: Извлечь информацию о документе
linktitle: Извлечь информацию о документе
second_title: GroupDocs.Editor .NET API
description: Узнайте, как извлечь информацию о документе с помощью GroupDocs.Editor для .NET, с помощью нашего подробного пошагового руководства. Идеально подходит для управления различными типами документов.
weight: 10
url: /ru/net/document-processing/extract-document-info/
---
## Введение
Добро пожаловать в это подробное руководство по извлечению информации о документе с помощью GroupDocs.Editor для .NET. В этом руководстве мы шаг за шагом проведем вас через весь процесс, убедившись, что вы понимаете каждую часть четко и кратко. Независимо от того, являетесь ли вы опытным разработчиком или только начинаете, это руководство поможет вам легко интегрировать GroupDocs.Editor в ваши проекты .NET для эффективного управления документами и манипулирования ими.
## Предварительные условия
Прежде чем углубиться в код, давайте убедимся, что у вас есть все необходимое:
- Базовые знания C#. Понимание основ программирования на C# имеет важное значение.
- Visual Studio: убедитесь, что у вас установлена Visual Studio.
-  GroupDocs.Editor для .NET: вам понадобится библиотека GroupDocs.Editor для .NET. Вы можете скачать его с сайта[страница загрузки](https://releases.groupdocs.com/editor/net/).
## Импортировать пространства имен
Для начала вам необходимо импортировать необходимые пространства имен. Это позволяет вам получить доступ к классам и методам, необходимым для управления документами.
```csharp
using System;
using GroupDocs.Editor.Metadata;
```
## Шаг 1. Загрузите документ
Сначала вам нужно загрузить документ, из которого вы хотите извлечь информацию. Это можно сделать, указав путь к документу.
```csharp
string docxInputFilePath = "YourSampleDocument.docx";
Editor editorDocx = new Editor(docxInputFilePath);
```
## Шаг 2. Получите информацию о документе
 Далее вы получите информацию о документе, используя`GetDocumentInfo` метод. Этот метод не требует каких-либо конкретных параметров загрузки, если вы не уверены в формате документа.
```csharp
IDocumentInfo infoDocx = editorDocx.GetDocumentInfo(null);
```
## Шаг 3: Определите тип документа
Теперь вам нужно проверить тип документа, с которым вы имеете дело. Это очень важно, поскольку от этого зависит, как вы будете обращаться с документом.
```csharp
bool isSpreadsheet = infoDocx is SpreadsheetDocumentInfo;
bool isText = infoDocx is TextualDocumentInfo;
bool isWordProcessing = infoDocx is WordProcessingDocumentInfo;
Console.WriteLine($"Is '{docxInputFilePath}' a Spreadsheet: {isSpreadsheet}");
Console.WriteLine($"Is '{docxInputFilePath}' a Textual document: {isText}");
Console.WriteLine($"Is '{docxInputFilePath}' a WordProcessing document: {isWordProcessing}");
```
## Шаг 4: Извлеките подробную информацию
Если документ является документом текстового процессора, вы можете извлечь подробную информацию, такую как формат, расширение, количество страниц, размер и то, зашифрован ли он.
```csharp
if (isWordProcessing)
{
    WordProcessingDocumentInfo casted = (WordProcessingDocumentInfo)infoDocx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Page count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```
## Шаг 5. Повторите действия для разных типов документов.
Повторите те же действия для других типов документов, таких как электронные таблицы и текстовые документы.
```csharp
string xlsxInputFilePath = "YourSampleDocument.xlsx";
Editor editorXlsx = new Editor(xlsxInputFilePath);
IDocumentInfo infoXlsx = editorXlsx.GetDocumentInfo(null);
bool isXlsxSpreadsheet = infoXlsx is SpreadsheetDocumentInfo;
Console.WriteLine($"Is '{xlsxInputFilePath}' a Spreadsheet: {isXlsxSpreadsheet}");
if (isXlsxSpreadsheet)
{
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo)infoXlsx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Tabs count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```
## Шаг 6. Обработка документов, защищенных паролем
Имея дело с документами, защищенными паролем, сначала следует попытаться открыть их без пароля, затем с неправильным паролем и, наконец, с правильным паролем.
```csharp
string xlsInputFilePath = "YourSampleDocument.xls";
Editor editorXls = new Editor(xlsInputFilePath);
try
{
    IDocumentInfo infoXls = editorXls.GetDocumentInfo(null);
}
catch (PasswordRequiredException)
{
    Console.WriteLine("This document is password-protected.");
}
try
{
    IDocumentInfo infoXls = editorXls.GetDocumentInfo("incorrect_password");
}
catch (IncorrectPasswordException)
{
    Console.WriteLine("The provided password is incorrect.");
}
IDocumentInfo infoXlsValid = editorXls.GetDocumentInfo("correct_password");
bool isXlsSpreadsheet = infoXlsValid is SpreadsheetDocumentInfo;
Console.WriteLine($"Password-protected document is a Spreadsheet: {isXlsSpreadsheet}");
if (isXlsSpreadsheet)
{
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo)infoXlsValid;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Tabs count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```
## Шаг 7. Обработка текстовых документов
```csharp
string xmlInputFilePath = "YourSampleDocument.xml";
Editor editorXml = new Editor(xmlInputFilePath);
IDocumentInfo infoXml = editorXml.GetDocumentInfo(null);
bool isXmlText = infoXml is TextualDocumentInfo;
Console.WriteLine($"Is '{xmlInputFilePath}' a Textual document: {isXmlText}");
if (isXmlText)
{
    TextualDocumentInfo casted = (TextualDocumentInfo)infoXml;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Encoding: {casted.Encoding}; Size: {casted.Size} bytes");
}
```
## Шаг 8: Утилизация ресурсов
Наконец, убедитесь, что вы избавились от всех ресурсов, чтобы предотвратить утечки памяти.
```csharp
editorDocx.Dispose();
editorXlsx.Dispose();
editorXls.Dispose();
editorXml.Dispose();
Console.WriteLine("ExtractingDocumentInfo routine has successfully finished");
```
## Заключение
Поздравляем! Теперь вы узнали, как извлекать информацию о документе с помощью GroupDocs.Editor для .NET. Эта мощная библиотека упрощает управление документами и манипулирование ими, позволяя беспрепятственно обрабатывать различные типы документов. Независимо от того, имеете ли вы дело с текстовым процессором, электронными таблицами или текстовыми документами, GroupDocs.Editor предоставляет надежное решение.
## Часто задаваемые вопросы
### Какие типы документов может обрабатывать GroupDocs.Editor?
GroupDocs.Editor может обрабатывать различные типы документов, включая текстовые документы, электронные таблицы и текстовые документы.
### Может ли GroupDocs.Editor управлять документами, защищенными паролем?
Да, GroupDocs.Editor может управлять документами, защищенными паролем. Он может идентифицировать и открыть эти документы при наличии правильного пароля.
### Необходимо ли удалять объекты редактора?
Да, очень важно удалять объекты Editor, чтобы освободить ресурсы и предотвратить утечки памяти.
### Могу ли я получить подробную информацию о формате и размере документа?
Абсолютно! GroupDocs.Editor позволяет извлекать подробную информацию, включая формат, расширение, размер, количество страниц и состояние шифрования.
### Где я могу получить поддержку, если у меня возникнут проблемы?
 Вы можете получить поддержку от[Форум поддержки GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).