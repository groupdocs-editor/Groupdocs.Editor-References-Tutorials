---
date: 2026-03-14
description: تعلم كيفية تحرير عروض PowerPoint التقديمية وأنواع المستندات الأخرى باستخدام
  GroupDocs.Editor لـ .NET. يغطي الدليل أيضًا كيفية حفظ المستند المُحرر وتحرير مستند
  Word باستخدام .NET.
linktitle: Create Document
second_title: GroupDocs.Editor .NET API
title: تحرير عرض PowerPoint باستخدام GroupDocs.Editor لـ .NET
type: docs
url: /ar/net/document-editing/create-document/
weight: 10
---

_X}}. Keep them unchanged.

Check for any other markdown elements: lists, headings, bold, links.

All good.

Now produce final content with Arabic translations and original placeholders.

# تحرير عرض PowerPoint التقديمي باستخدام GroupDocs.Editor لـ .NET

## مقدمة
إذا كنت تبحث عن طريقة موثوقة **لتحرير عرض PowerPoint** برمجياً، فإن GroupDocs.Editor لـ .NET هو الجواب. تتيح لك هذه المكتبة العمل مع صيغ Word وExcel وPowerPoint وEbook وEmail — جميعها من خلال واجهة برمجة تطبيقات واحدة سهلة الاستخدام. في هذا الدرس سنستعرض إنشاء وتحرير كل نوع من المستندات المدعومة، ونوضح لك كيفية **حفظ المستند المعدل** تدفقات، ونقدم لك نصائح عملية يمكنك تطبيقها في المشاريع الحقيقية.

## إجابات سريعة
- **ما المكتبة التي تسمح لي بتحرير ملفات PowerPoint في .NET؟** GroupDocs.Editor for .NET.  
- **هل يمكنني تحرير ملفات Word وExcel وEpub باستخدام نفس API؟** نعم، ففئة `Editor` نفسها تدعم جميع هذه الصيغ.  
- **كيف يمكنني التقاط الملف المعدل؟** قدم دالة رد نداء (callback) (مثال: `SaveNewDocument`) التي تستقبل تدفق النتيجة.  
- **هل أحتاج إلى ترخيص للاستخدام في الإنتاج؟** نعم — اشترِ ترخيصًا أو استخدم ترخيصًا تجريبيًا مؤقتًا.  
- **ما إصدارات .NET المدعومة؟** .NET Framework 4.0+، .NET Core، و .NET 5/6.

## ما هو “تحرير عرض PowerPoint” باستخدام GroupDocs.Editor؟
يعني تحرير عرض PowerPoint تحميل ملف `.pptx`، تطبيق التغييرات (مثل تعديل الشرائح أو النص أو العناصر المخفية)، ثم استرجاع الملف المحدث — كل ذلك دون الحاجة إلى تثبيت Microsoft Office.

## لماذا تستخدم GroupDocs.Editor لـ .NET؟
- **واجهة API واحدة للعديد من الصيغ** – لا حاجة للتعامل مع مكتبات منفصلة لـ Word أو Excel أو Epub.  
- **بدون اعتماد على Office** – يعمل على الخوادم، الحاويات، وخطوط أنابيب CI.  
- **تحكم دقيق** – تخصيص ترقيم الصفحات، معلومات اللغة، استخراج الخطوط، وأكثر.  
- **معالجة قائمة على التدفقات** – مثالية لخدمات السحابة حيث تتعامل مع تدفقات الذاكرة بدلاً من الملفات الفعلية.

## المتطلبات المسبقة
- Visual Studio (أي إصدار حديث).  
- .NET Framework 4.0 أو أعلى (أو .NET Core/.NET 5+).  
- مكتبة GroupDocs.Editor لـ .NET – حمّلها من [here](https://releases.groupdocs.com/editor/net/).  
- معرفة أساسية بـ C#.

## استيراد مساحات الأسماء
أولاً، استورد مساحات الأسماء التي تحتوي على الفئات الأساسية التي سنستخدمها.

```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using System.IO;
```

## الخطوة 1: إعداد التدفق
سنستخدم تدفق ذاكرة كعنصر نائب لمحتوى المستند.

```csharp
Stream memoryStream = Stream.Null;
```

## الخطوة 2: دالة رد النداء **لحفظ المستند المعدل**
عرّف دالة رد نداء تستقبل التدفق المعدل وتخزنه في `memoryStream`.

```csharp
void SaveNewDocument(Stream resultStream)
{
    memoryStream = resultStream;
}
```

## الخطوة 3: إنشاء وتحرير مستند معالجة نصية  
(هنا نقوم **بتحرير مستند Word .net**.)

### إنشاء وتحرير باستخدام الخيارات الافتراضية
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    EditableDocument defaultWordProcessingDoc = editor.Edit();
}
```

### إنشاء وتحرير باستخدام خيارات مخصصة
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

## الخطوة 4: إنشاء وتحرير مستند جدول بيانات  
(استخدم هذا **لتحرير ملف Excel .net**.)

### إنشاء وتحرير باستخدام الخيارات الافتراضية
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    EditableDocument defaultEditableSpreadsheetDocument = editor.Edit();
}
```

### إنشاء وتحرير باستخدام خيارات مخصصة
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

## الخطوة 5: **تحرير عرض PowerPoint** – إنشاء وتحرير مستند عرض تقديمي
هذا هو جوهر تركيز كلمة البحث الأساسية.

### إنشاء وتحرير باستخدام الخيارات الافتراضية
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    EditableDocument defaultEditablePresentationDocument = editor.Edit();
}
```

### إنشاء وتحرير باستخدام خيارات مخصصة
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

## الخطوة 6: إنشاء وتحرير مستند Ebook  
(هنا نقوم **بتحرير ملف epub**.)

### إنشاء وتحرير باستخدام الخيارات الافتراضية
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EditableDocument defaultEditableEbookDocument = editor.Edit();
}
```

### إنشاء وتحرير باستخدام خيارات مخصصة
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

## الخطوة 7: إنشاء وتحرير مستند بريد إلكتروني
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EditableDocument defaultEditableEmailDocument = editor.Edit();
}
```

### إنشاء وتحرير باستخدام خيارات مخصصة
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

## الخطوة 8: إنهاء العملية
قم بتحرير التدفق لتفريغ الموارد بمجرد الانتهاء.

```csharp
memoryStream.Dispose();
System.Console.WriteLine("CreateDocument routine has successfully finished");
```

## الأخطاء الشائعة والنصائح
- **لا تنسَ أبدًا تحرير التدفق** – تركه مفتوحًا قد يسبب تسربًا للذاكرة في الخدمات طويلة التشغيل.  
- **عند تحرير PowerPoint، تأكد من ضبط `SlideNumber` بشكل صحيح**؛ وإلا قد يتكرر الشريحة الأولى.  
- **إذا كنت بحاجة للحفاظ على اسم الملف الأصلي**، احفظه قبل رد النداء وأعد تسمية تدفق الإخراج بعد التحرير.  
- **للملفات الكبيرة**، فكر في معالجتها على أجزاء أو استخدم `Editor` مع ملف مؤقت لتجنب استهلاك عالي للذاكرة.

## الأسئلة المتكررة

**س: ما أنواع المستندات التي يمكنني تحريرها باستخدام GroupDocs.Editor لـ .NET؟**  
ج: يمكنك تحرير معالجة النصوص، جداول البيانات، العروض التقديمية، الكتب الإلكترونية، والبريد الإلكتروني — بما في ذلك ملفات PowerPoint لحالة الاستخدام **تحرير عرض PowerPoint**.

**س: هل يمكن تخصيص خيارات التحرير؟**  
ج: نعم، كل صيغة لها فئة خيارات خاصة بها (مثال: `WordProcessingEditOptions`، `SpreadsheetEditOptions`، `PresentationEditOptions`) التي تتيح لك ضبط ترقيم الصفحات، الشرائح المخفية، اختيار ورقة العمل، إلخ.

**س: كيف أتعامل مع مخرجات المستندات المعدلة؟**  
ج: استخدم دالة رد النداء (`SaveNewDocument`) لالتقاط التدفق المعدل، ثم يمكنك كتابته إلى القرص، قاعدة بيانات، أو إرجاعه من واجهة برمجة تطبيقات ويب.

**س: هل أحتاج إلى ترخيص لاستخدام GroupDocs.Editor لـ .NET؟**  
ج: نعم، الترخيص مطلوب للإنتاج. يمكنك الحصول عليه من [here](https://purchase.groupdocs.com/buy). كما يتوفر ترخيص تجريبي مؤقت.

**س: أين يمكنني العثور على وثائق أكثر تفصيلاً؟**  
ج: الوثائق التفصيلية متوفرة على صفحة [GroupDocs.Editor for .NET documentation page](https://tutorials.groupdocs.com/editor/net/).

## الخاتمة
يُسهل GroupDocs.Editor لـ .NET عملية **تحرير عرض PowerPoint** والعديد من أنواع المستندات الأخرى. باتباع الخطوات أعلاه يمكنك إنشاء وتعديل و**حفظ المستند المعدل** بالكامل عبر الشيفرة، دون الاعتماد على تثبيتات Office. استكشف الخيارات المتقدمة للمكتبة لتخصيص تجربة التحرير وفقًا لاحتياجات عملك الخاصة.

---

**آخر تحديث:** 2026-03-14  
**تم الاختبار مع:** GroupDocs.Editor for .NET (أحدث إصدار)  
**المؤلف:** GroupDocs