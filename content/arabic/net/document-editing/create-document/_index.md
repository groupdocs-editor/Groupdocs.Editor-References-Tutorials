---
title: إنشاء مستند
linktitle: إنشاء مستند
second_title: GroupDocs.Editor .NET API
description: تعرف على كيفية تحرير مستندات Word وExcel وPowerPoint والكتب الإلكترونية والبريد الإلكتروني باستخدام GroupDocs.Editor لـ .NET باستخدام هذا البرنامج التعليمي الشامل خطوة بخطوة.
weight: 10
url: /ar/net/document-editing/create-document/
type: docs
---
# إنشاء مستند

## مقدمة
هل سئمت من المتاعب التي تأتي مع تحرير أنواع مختلفة من المستندات برمجياً؟ يتوفر GroupDocs.Editor لـ .NET لتبسيط العملية. تسمح هذه الأداة القوية للمطورين بتحرير تنسيقات المستندات المختلفة مثل Word وExcel وPowerPoint والكتب الإلكترونية ورسائل البريد الإلكتروني بسهولة. في هذا البرنامج التعليمي، سنتعمق في كيفية استخدام GroupDocs.Editor لـ .NET لإنشاء المستندات وتحريرها. سنقوم بتقسيم العملية إلى خطوات سهلة المتابعة، مما يجعلها في متناول الجميع حتى لو كنت جديدًا في هذا الأمر.
## المتطلبات الأساسية
قبل أن نبدأ، تأكد من أن لديك ما يلي:
- تم تثبيت Visual Studio على جهازك.
- .NET Framework (4.0 أو أعلى).
-  GroupDocs.Editor لمكتبة .NET. يمكنك تنزيله من[هنا](https://releases.groupdocs.com/editor/net/).
- المعرفة الأساسية ببرمجة C#.
## استيراد مساحات الأسماء
أولاً، لنستورد مساحات الأسماء الضرورية. سيؤدي ذلك إلى إتاحة الوصول إلى الفئات والأساليب المطلوبة في تطبيقنا.
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using System.IO;
```
## الخطوة 1: إعداد الدفق
للبدء، نحتاج إلى إعداد دفق الذاكرة الذي سيكون بمثابة العنصر النائب لمحتوى المستند.
```csharp
Stream memoryStream = Stream.Null;
```
## الخطوة 2: وظيفة رد الاتصال لحفظ المستند
بعد ذلك، حدد وظيفة رد الاتصال التي ستحفظ دفق المستند الجديد. هذه الوظيفة ضرورية للتعامل مع مخرجات عملية تحرير المستندات.
```csharp
void SaveNewDocument(Stream resultStream)
{
    memoryStream = resultStream;
}
```
## الخطوة 3: إنشاء وتحرير مستند معالجة الكلمات
 الآن، لنقم بإنشاء مستند Word وتحريره. سنبدأ بإنشاء جديد`Editor` مثيل لمستندات WordProcessing وتحريرها باستخدام الخيارات الافتراضية.
### إنشاء وتحرير باستخدام الخيارات الافتراضية
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    EditableDocument defaultWordProcessingDoc = editor.Edit();
}
```
### إنشاء وتحرير باستخدام خيارات مخصصة
لمزيد من التحكم، يمكننا تحديد خيارات مثل تعطيل ترقيم الصفحات واستخراج الخطوط المضمنة.
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    WordProcessingEditOptions wordProcessingEditOptions = new WordProcessingEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true,
        FontExtraction = FontExtractionOptions.ExtractAllEmbedded
    };
    EditableDocument editableWordProcessingDocument = editor.Edit(wordProcessingEditOptions);
}
```
## الخطوة 4: إنشاء وتحرير مستند جدول البيانات
وبالمثل، يمكننا إنشاء وتحرير مستند Excel. وإليك كيف يمكنك أن تفعل ذلك.
### إنشاء وتحرير باستخدام الخيارات الافتراضية
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    EditableDocument defaultEditableSpreadsheetDocument = editor.Edit();
}
```
### إنشاء وتحرير باستخدام خيارات مخصصة
 لاستهداف أوراق عمل محددة أو استبعاد الأوراق المخفية، نستخدم`SpreadsheetEditOptions`.
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    SpreadsheetEditOptions spreadsheetEditOptions = new SpreadsheetEditOptions
    {
        WorksheetIndex = 0,
        ExcludeHiddenWorksheets = true
    };
    EditableDocument editableSpreadsheetDocument = editor.Edit(spreadsheetEditOptions);
}
```
## الخطوة 5: إنشاء وتحرير مستند العرض التقديمي
كما يتم دعم عروض PowerPoint التقديمية. دعونا نرى كيفية التعامل معها.
### إنشاء وتحرير باستخدام الخيارات الافتراضية
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    EditableDocument defaultEditablePresentationDocument = editor.Edit();
}
```
### إنشاء وتحرير باستخدام خيارات مخصصة
يمكنك تخصيص تعديلاتك عن طريق تحديد خيارات مثل الشريحة التي سيتم عرضها وما إذا كنت تريد تضمين الشرائح المخفية أم لا.
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    PresentationEditOptions presentationEditOptions = new PresentationEditOptions
    {
        ShowHiddenSlides = false,
        SlideNumber = 0
    };
    EditableDocument editablePresentationDocument = editor.Edit(presentationEditOptions);
}
```
## الخطوة 6: إنشاء وتحرير مستند الكتاب الإلكتروني
يسمح GroupDocs.Editor أيضًا بتحرير تنسيقات الكتب الإلكترونية مثل EPUB. وإليك كيف يمكنك التعامل معها.
### إنشاء وتحرير باستخدام الخيارات الافتراضية
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EditableDocument defaultEditableEbookDocument = editor.Edit();
}
```
### إنشاء وتحرير باستخدام خيارات مخصصة
قم بتخصيص تحرير كتابك الإلكتروني عن طريق تمكين أو تعطيل معلومات ترقيم الصفحات واللغة.
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EbookEditOptions ebookEditOptions = new EbookEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true
    };
    EditableDocument editableEbookDocument = editor.Edit(ebookEditOptions);
}
```
## الخطوة 7: إنشاء وتحرير مستند البريد الإلكتروني
وأخيرا، سننظر في كيفية تحرير مستندات البريد الإلكتروني. يتضمن ذلك تنسيقات مثل EML.
### إنشاء وتحرير باستخدام الخيارات الافتراضية
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EditableDocument defaultEditableEmailDocument = editor.Edit();
}
```
### إنشاء وتحرير باستخدام خيارات مخصصة
حدد خيارات إخراج رسالة البريد للتحكم في عملية التحرير.
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EmailEditOptions emailEditOptions = new EmailEditOptions
    {
        MailMessageOutput = MailMessageOutput.All
    };
    EditableDocument editableEmailDocument = editor.Edit(emailEditOptions);
}
```
## الخطوة 8: الانتهاء من العملية
بعد تحرير المستندات، من الضروري التخلص من تدفق الذاكرة بشكل صحيح لتحرير الموارد.
```csharp
memoryStream.Dispose();
System.Console.WriteLine("CreateDocument routine has successfully finished");
```
## خاتمة
يعد GroupDocs.Editor for .NET أداة متعددة الاستخدامات وقوية يمكنها تبسيط مهمة تحرير أنواع المستندات المختلفة برمجيًا. باتباع هذا الدليل التفصيلي، يمكنك إنشاء المستندات وتحريرها بسهولة، سواء كانت ملفات معالجة Word، أو جداول بيانات، أو عروض تقديمية، أو كتب إلكترونية، أو رسائل بريد إلكتروني. تعمق في وثائق GroupDocs.Editor للحصول على المزيد من الميزات المتقدمة وخيارات التخصيص.
## الأسئلة الشائعة
### ما أنواع المستندات التي يمكنني تحريرها باستخدام GroupDocs.Editor لـ .NET؟
يمكنك تحرير مجموعة واسعة من المستندات، بما في ذلك معالجة الكلمات وجداول البيانات والعروض التقديمية والكتب الإلكترونية ورسائل البريد الإلكتروني.
### هل من الممكن تخصيص خيارات التحرير؟
نعم، يسمح GroupDocs.Editor for .NET بالتخصيص الشامل من خلال خيارات التحرير المتنوعة الخاصة بكل نوع مستند.
### كيف أتعامل مع مخرجات المستندات المحررة؟
يمكنك استخدام وظيفة رد الاتصال لحفظ دفق المستند الذي تم تحريره في الموقع المطلوب.
### هل أحتاج إلى ترخيص لاستخدام GroupDocs.Editor لـ .NET؟
 نعم يمكنك الحصول على ترخيص من[هنا](https://purchase.groupdocs.com/buy). هناك أيضًا خيار للحصول على ترخيص مؤقت.
### أين يمكنني العثور على وثائق أكثر تفصيلا؟
 الوثائق التفصيلية متاحة على[GroupDocs.Editor لصفحة وثائق .NET](https://tutorials.groupdocs.com/editor/net/).