---
date: 2026-06-01
description: تعلم كيفية الحصول على عدد الصفحات واستخراج بيانات تعريف المستند باستخدام
  GroupDocs.Editor لـ .NET في دليل تفصيلي خطوة بخطوة.
keywords:
- get page count
- extract document metadata
- get document info
- find document extension
- retrieve document size
linktitle: احصل على عدد الصفحات واستخراج معلومات المستند
schemas:
- author: GroupDocs
  dateModified: '2026-06-01'
  description: Learn how to get page count and extract document metadata using GroupDocs.Editor
    for .NET in a detailed step‑by‑step tutorial.
  headline: Get Page Count & Extract Document Info with GroupDocs.Editor
  type: TechArticle
- questions:
  - answer: GroupDocs.Editor supports Word processing, spreadsheet, presentation,
      PDF, and plain‑text files—over 50 formats in total.
    question: What document types can I extract metadata from?
  - answer: Access `DocumentInfo.Extension` after calling `GetDocumentInfo()`; it
      returns the extension without the leading dot.
    question: How do I retrieve the file extension?
  - answer: Yes—`DocumentInfo.Size` returns the size in bytes; divide by 1,048,576
      to convert to megabytes.
    question: Can I get the size of a document in megabytes?
  - answer: Absolutely—GroupDocs.Editor never writes the password to disk and disposes
      of all cryptographic objects after use.
    question: Is it safe to process password‑protected files on a server?
  - answer: You can get support from the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).
    question: Where can I find additional help if I run into issues?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: احصل على عدد الصفحات واستخراج معلومات المستند باستخدام GroupDocs.Editor
type: docs
url: /ar/net/document-processing/extract-document-info/
weight: 10
---

# احصل على عدد الصفحات واستخراج معلومات المستند باستخدام GroupDocs.Editor

## مقدمة
في هذا الدرس الشامل ستتعلم كيفية **get page count** واستخراج معلومات مفصلة عن المستند — بما في ذلك التنسيق والحجم وحالة التشفير — باستخدام GroupDocs.Editor لـ .NET. سواءً كنت تبني نظام إدارة مستندات، أو محرك تقارير، أو خط أنابيب تحويل تلقائي، فإن فهم بيانات التعريف للملف هو الخطوة الأولى نحو معالجة موثوقة. دعنا نستعرض سير العمل بالكامل، من تحميل الملف إلى التخلص الآمن من الموارد.

## إجابات سريعة
- **كيف يمكنني استرجاع عدد الصفحات لمستند؟**  
  استدعِ `editor.GetDocumentInfo().PageCount` بعد تحميل الملف باستخدام `Editor`.
- **ما هي صيغ الملفات المدعومة لاستخراج بيانات التعريف؟**  
  أكثر من 50 صيغة، بما في ذلك DOCX، XLSX، PPTX، PDF، TXT، وHTML.
- **هل يمكنني استخراج بيانات التعريف من الملفات المحمية بكلمة مرور؟**  
  نعم — قدم كلمة المرور عند إنشاء كائن `Editor`.
- **هل أحتاج إلى تحرير الموارد يدويًا؟**  
  بالطبع؛ يجب دائمًا استدعاء `editor.Dispose()` أو وضع المحرر داخل كتلة `using`.
- **ما هو إصدار GroupDocs.Editor المطلوب؟**  
  أحدث إصدار ثابت (v23.12+ في وقت الكتابة) يدعم جميع الميزات المعروضة.

## ما هو “get page count” في GroupDocs.Editor؟
`GetDocumentInfo()` هي طريقة تُعيد كائن `DocumentInfo` يحتوي على عدد صفحات المستند، التنسيق، الحجم، وغيرها من بيانات التعريف. هذه الاستدعاءة الواحدة تمنحك نظرة فورية دون الحاجة إلى تحليل الملف يدويًا. باستخدام هذه الطريقة تتجنب تحميل المستند بالكامل في الذاكرة، مما يحسن الأداء خاصةً للملفات الكبيرة ويقلل استهلاك موارد الخادم.

## لماذا استخراج بيانات تعريف المستند باستخدام GroupDocs.Editor؟
يمكن لـ GroupDocs.Editor معالجة **أكثر من 50 صيغة إدخال وإخراج** واسترجاع بيانات التعريف للملفات حتى **2 GB** دون تحميل المستند بالكامل في الذاكرة. هذه الكفاءة تقلل حمل الخادم بنسبة تصل إلى **70 %** مقارنةً بتحليل المستند بالكامل، مما يجعلها مثالية للتطبيقات ذات الإنتاجية العالية.

## المتطلبات المسبقة
- **C# development basics** – يجب أن تكون مرتاحًا مع Visual Studio وهياكل مشاريع .NET.
- **Visual Studio 2022** (أو أي نسخة حديثة) مثبتة على جهازك.
- **GroupDocs.Editor for .NET** – قم بتنزيل أحدث حزمة من [صفحة التحميل](https://releases.groupdocs.com/editor/net/).

## كيف تقوم بتحميل المستند الخاص بك؟
`Editor` هو الفئة الرئيسية التي تمثل مستندًا وتوفر طرقًا لتحميله ومعالجته. قم بتحميل الملف المستهدف بإنشاء مثيل `Editor` وتمرير مسار الملف. يكتشف المحرر التنسيق تلقائيًا، لذا لا تحتاج إلى تحديد خيارات التحميل. هذا النهج يعمل مع أي نوع ملف مدعوم ويسهل الإعداد الأولي.

```csharp
using System;
using GroupDocs.Editor.Metadata;
```

## كيف تسترجع معلومات المستند؟
`GetDocumentInfo()` تُعيد كائن `DocumentInfo` يحتوي على بيانات تعريف مثل عدد الصفحات، التنسيق، الحجم، وحالة التشفير. بعد التحميل، استدعِ هذه الطريقة للحصول على الكائن. الـ `DocumentInfo` المُرجع يمنحك لمحة مختصرة عن خصائص الملف، مما يتيح لك اتخاذ قرارات دون الحاجة إلى مزيد من المعالجة.

```csharp
string docxInputFilePath = "YourSampleDocument.docx";
Editor editorDocx = new Editor(docxInputFilePath);
```

## كيف تحدد نوع المستند؟
`DocumentType` هو تعداد (enum) يوضح ما إذا كان المستند WordProcessing أو Spreadsheet أو Text. معرفة ما إذا كان الملف مستند معالجة كلمات، أو جدول بيانات، أو نصًا عاديًا يؤثر على طريقة التعامل معه لاحقًا. استخدم خاصية `DocumentType` لكائن `DocumentInfo` لاتخاذ هذا القرار وتفرع المنطق وفقًا لذلك.

```csharp
IDocumentInfo infoDocx = editorDocx.GetDocumentInfo(null);
```

## كيف تستخرج معلومات مفصلة لملفات معالجة الكلمات؟
`WordProcessing` يشير إلى المستندات مثل DOCX وODT وRTF التي تُعامل كملفات معالجة كلمات. إذا كان نوع المستند `WordProcessing`، يمكنك قراءة خصائص إضافية مثل **format**، **extension**، **page count**، **size**، و**encryption flag** مباشرةً من كائن `DocumentInfo`. هذه التفاصيل تساعدك على تخصيص خطوات المعالجة، مثل تطبيق تحويلات محددة أو فحوصات أمان.

```csharp
bool isSpreadsheet = infoDocx is SpreadsheetDocumentInfo;
bool isText = infoDocx is TextualDocumentInfo;
bool isWordProcessing = infoDocx is WordProcessingDocumentInfo;
Console.WriteLine($"Is '{docxInputFilePath}' a Spreadsheet: {isSpreadsheet}");
Console.WriteLine($"Is '{docxInputFilePath}' a Textual document: {isText}");
Console.WriteLine($"Is '{docxInputFilePath}' a WordProcessing document: {isWordProcessing}");
```

## كيف تتعامل مع مستندات الجداول والنصوص؟
`Spreadsheet` يرمز إلى ملفات الجداول مثل XLSX، بينما `Text` يمثل المستندات النصية العادية. بالنسبة لملفات الجداول (`Spreadsheet`) والملفات النصية العادية (`Text`)، لا يزال كائن `DocumentInfo` يوفر بيانات تعريف أساسية (الامتداد، الحجم، عدد الصفحات). قد لا تعرض بعض الصيغ عدد الصفحات، وفي هذه الحالة ستكون القيمة `0`. يمكنك الاعتماد على بيانات التعريف الأخرى للمنطق اللاحق.

```csharp
if (isWordProcessing)
{
    WordProcessingDocumentInfo casted = (WordProcessingDocumentInfo)infoDocx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Page count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```

## كيف تتعامل مع المستندات المحمية بكلمة مرور؟
`Password` هو سلسلة تُمرَّر إلى مُنشئ `Editor` لفتح الملفات المشفرة. عندما يكون المستند مشفرًا، حاول أولاً فتحه بدون كلمة مرور. إذا فشل ذلك، امسك الاستثناء ثم أعد المحاولة باستخدام كلمة المرور الصحيحة. مُنشئ `Editor` يقبل معامل `Password` لهذا الغرض، مما يتيح التعامل السلس مع الملفات المحمية.

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

## كيف تعالج المستندات النصية؟
`DocumentInfo` يوفر بيانات تعريف أساسية مثل الحجم، الامتداد، والترميز للملفات النصية. تُعامل ملفات النص (مثل `.txt`، `.md`) كتيارات بسيطة. لا يزال بإمكانك استرجاع معلومات الحجم والترميز من `DocumentInfo`، وهو مفيد للتحقق من سلامة الملف أو تحديد خطوط المعالجة المناسبة.

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

## كيف تتخلص من الموارد بشكل صحيح؟
`Editor` هو الفئة الأساسية التي تحتفظ بموارد غير مُدارة ويجب تحريرها بعد الاستخدام. لتجنب تسرب الذاكرة، يجب دائمًا تحرير مثيل `Editor` بعد الانتهاء من استخراج المعلومات. عبارة `using` هي الأنماط الأكثر أمانًا لأنها تضمن تحرير الموارد حتى في حال حدوث استثناء، مما يضمن إدارة موارد نظيفة.

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

## المشكلات الشائعة والحلول
| المشكلة | السبب | الحل |
|-------|-------|----------|
| **PageCount returns 0** | الصيغة لا تدعم الترميز (مثل النص العادي) | تحقق من `DocumentInfo.DocumentType` قبل الاعتماد على `PageCount`. |
| **Unsupported file format** | امتداد الملف غير معروف | تحقق من أن الملف أحد الصيغ الـ 50+ المدعومة؛ وقم بتحديث GroupDocs.Editor إلى أحدث إصدار. |
| **Password exception** | تم توفير كلمة مرور خاطئة | امسك `PasswordProtectedException` واطلب من المستخدم إعادة إدخال كلمة المرور. |
| **Memory spike on large files** | تحميل ملفات PDF كبيرة جدًا دون التدفق | استخدم `LoadOptions` مع `LoadOptions.LoadMode = LoadMode.Stream` (متاح في الإصدارات الأحدث). |

## الأسئلة المتكررة

**Q: ما هي أنواع المستندات التي يمكنني استخراج بيانات التعريف منها؟**  
A: GroupDocs.Editor يدعم ملفات معالجة الكلمات، وجداول البيانات، والعروض التقديمية، وPDF، والملفات النصية العادية — أكثر من 50 صيغة إجمالاً.

**Q: كيف يمكنني استرجاع امتداد الملف؟**  
A: يمكنك الوصول إلى `DocumentInfo.Extension` بعد استدعاء `GetDocumentInfo()`؛ فهو يُعيد الامتداد بدون النقطة الأولى.

**Q: هل يمكنني الحصول على حجم المستند بالميغابايت؟**  
A: نعم — `DocumentInfo.Size` يُعيد الحجم بالبايت؛ قسِّمه على 1,048,576 للتحويل إلى ميغابايت.

**Q: هل من الآمن معالجة الملفات المحمية بكلمة مرور على الخادم؟**  
A: بالطبع — GroupDocs.Editor لا يكتب كلمة المرور إلى القرص ويُفرغ جميع الكائنات التشفيرية بعد الاستخدام.

**Q: أين يمكنني العثور على مساعدة إضافية إذا واجهت مشاكل؟**  
A: يمكنك الحصول على الدعم من [منتدى دعم GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).

---

**آخر تحديث:** 2026-06-01  
**تم الاختبار مع:** GroupDocs.Editor 23.12 for .NET  
**المؤلف:** GroupDocs

```csharp
editorDocx.Dispose();
editorXlsx.Dispose();
editorXls.Dispose();
editorXml.Dispose();
Console.WriteLine("ExtractingDocumentInfo routine has successfully finished");
```

## الدروس ذات الصلة

- [استخراج بيانات التعريف المتقدم في .NET باستخدام GroupDocs.Editor: دليل شامل](/editor/net/advanced-features/groupdocs-editor-net-metadata-extraction-guide/)
- [دروس تحميل المستندات باستخدام GroupDocs.Editor لـ .NET](/editor/net/document-loading/)
- [تحرير المستندات بكفاءة باستخدام GroupDocs.Editor .NET: تحويل HTML إلى مستندات قابلة للتحرير](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)