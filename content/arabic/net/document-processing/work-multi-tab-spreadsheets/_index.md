---
date: 2026-06-06
description: تعلم كيفية **حفظ كل ورقة Excel** باستخدام GroupDocs.Editor for .NET –
  دليل خطوة بخطوة، مقتطفات كود، وأفضل الممارسات لتقسيم ملفات XLSX.
keywords:
- save each excel tab
- read multiple sheets
- convert excel tab pdf
- split xlsx files
linktitle: العمل مع جداول البيانات متعددة الأوراق
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to **save each Excel tab** using GroupDocs.Editor for .NET
    – step‑by‑step guide, code snippets, and best practices for splitting XLSX files.
  headline: How to save each Excel tab with GroupDocs.Editor .NET
  type: TechArticle
- description: Learn how to **save each Excel tab** using GroupDocs.Editor for .NET
    – step‑by‑step guide, code snippets, and best practices for splitting XLSX files.
  name: How to save each Excel tab with GroupDocs.Editor .NET
  steps:
  - name: Get a Path to the Input File
    text: First, specify the full path to the source XLSX that contains multiple tabs.
  - name: Load the Spreadsheet into the Editor Instance
    text: The `Editor` class is the entry point for all document operations in GroupDocs.Editor.
      It reads the file stream and prepares the document for editing or extraction.
  - name: Create an EditableDocument from the First Tab
    text: '`EditableDocument` represents a single, editable sheet within the workbook.
      The constructor takes the `Editor` instance and a zero‑based sheet index.'
  - name: Create an EditableDocument from the Second Tab
    text: You can repeat the same pattern for any additional sheet by changing the
      index value.
  - name: Save the First Tab to a Separate Document
    text: '`Save` writes the edited document to a file in the specified format. Call
      it on the `EditableDocument` instance, providing the output path and format
      (e.g., `SaveFormat.Xlsx`).'
  - name: Save the Second Tab to a Separate Document
    text: The same `Save` call works for the second sheet, and you can choose a different
      format such as PDF if needed.
  - name: Dispose of EditableDocument Instances
    text: '`Dispose` releases unmanaged resources held by the document, such as file
      handles, ensuring no leaks in long‑running services.'
  type: HowTo
- questions:
  - answer: Hidden sheets are treated like any other sheet; you can access them by
      index and save them, but you may need to set `EditableDocument.IsVisible = true`
      before saving if you want them visible in the output.
    question: What if my workbook contains hidden sheets?
  - answer: Yes, specify `SaveFormat.Pdf` when calling `Save` on the `EditableDocument`.
      The library preserves layout, images, and charts during conversion.
    question: Can I convert an Excel tab directly to PDF?
  - answer: Absolutely. Use `SaveFormat.Csv` for each `EditableDocument` to generate
      plain‑text CSV representations of each sheet.
    question: Is it possible to split a workbook into CSV files instead of XLSX?
  - answer: It does. Provide the password via `LoadOptions.Password` when creating
      the `Editor` instance.
    question: Does GroupDocs.Editor support password‑protected Excel files?
  - answer: The official documentation and sample projects on the [download page](https://releases.groupdocs.com/editor/net/)
      contain additional use‑cases.
    question: Where can I find more examples of working with spreadsheets?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: كيفية حفظ كل ورقة Excel باستخدام GroupDocs.Editor .NET
type: docs
url: /ar/net/document-processing/work-multi-tab-spreadsheets/
weight: 17
---

# العمل مع جداول متعددة الألسنة

## مقدمة
إذا كنت بحاجة إلى **حفظ كل ورقة Excel** كملف مستقل، فإن GroupDocs.Editor for .NET يجعل العملية سهلة. سواء كنت تستخرج تقارير مالية، أو تُنشئ أوراق عمل لكل قسم، أو تحول الأوراق إلى PDF، فإن هذا الدرس يرشّحك عبر سير العمل بالكامل—من إعداد البيئة إلى تحرير الموارد—حتى تتمكن من أتمتة معالجة الجداول المتعددة بثقة.

## إجابات سريعة
- **هل يمكن لـ GroupDocs.Editor تقسيم ملف XLSX إلى ملفات منفصلة؟** نعم، يمكنك تحميل المصنف وتصدير كل ورقة على حدة.  
- **ما الصيغ التي يمكن حفظ كل ورقة بها؟** XLSX، CSV، PDF، HTML، وأكثر – يدعم أكثر من 30 صيغة إخراج.  
- **هل أحتاج إلى ترخيص لهذه الميزة؟** الترخيص المؤقت يكفي للاختبار؛ الترخيص الكامل مطلوب للإنتاج.  
- **هل .NET Core مدعوم؟** بالتأكيد – المكتبة تعمل مع .NET Framework 4.0+ و .NET Core/5/6+.  
- **كم عدد الأوراق التي يمكن معالجتها في آن واحد؟** يمكن لـ GroupDocs.Editor التعامل مع مصنفات تحتوي على أكثر من 500 ورقة دون تحميل الملف بالكامل إلى الذاكرة.

## ما هو “save each excel tab”؟
**“Save each Excel tab”** يعني استخراج كل ورقة عمل من مصنف متعدد الأوراق وكتابة كل واحدة في مستند مستقل خاص بها (مثل ملفات XLSX أو PDF منفصلة). يسهّل هذا النهج معالجة البيانات لاحقًا، وإعداد التقارير، والتوزيع من خلال توفير ملف لكل ورقة، يمكن بعد ذلك مشاركته أو أرشفته أو تحويله بشكل مستقل.

## لماذا نستخدم GroupDocs.Editor لهذه المهمة؟
يدعم GroupDocs.Editor **أكثر من 30 صيغة إدخال وإخراج** ويمكنه معالجة جداول البيانات التي تحتوي على **حتى 1,000 ورقة** مع الحفاظ على استهلاك الذاكرة منخفضًا عبر بث البيانات بدلاً من تحميل الملف بالكامل. كما أن الـ API يحافظ على أنماط الخلايا، والصيغ، والصور المدمجة، مما يضمن أن كل ورقة مُصدرة تبدو مطابقة للأصل.

## المتطلبات المسبقة
قبل الغوص في التفاصيل، تأكد من وجود ما يلي:

1. **Visual Studio** – أي إصدار حديث (Community أو Professional أو Enterprise).  
2. **.NET Framework 4.0+** – أو .NET Core/5/6 إذا كنت تفضّل بيئة التشغيل متعددة المنصات.  
3. **GroupDocs.Editor for .NET** – حمّله من [صفحة التحميل](https://releases.groupdocs.com/editor/net/).  
4. **License** – الترخيص [المؤقت](https://purchase.groupdocs.com/temporary-license/) يكفي للاختبار؛ اشترِ ترخيصًا كاملاً للاستخدام في الإنتاج.  
5. **Free trial** – يمكنك أيضًا تجربة المكتبة عبر صفحة [التجربة المجانية](https://releases.groupdocs.com/).  
6. **Support** – إذا واجهت مشاكل، قم بزيارة [منتدى الدعم](https://forum.groupdocs.com/c/editor/20) أو انظر إلى [صفحة الشراء](https://purchase.groupdocs.com/buy) للحصول على ترخيص كامل.

## استيراد مساحات الأسماء
قبل أن نبدأ بالبرمجة، تحتاج إلى استيراد مساحات الأسماء الضرورية. أضف توجيهات `using` التالية إلى أعلى ملف `.cs` الخاص بك:

```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```

## كيفية حفظ كل ورقة Excel كملف منفصل؟
حمّل المصنف، أنشئ `EditableDocument` لكل ورقة، واستدعِ `Save` بالصيغ المطلوبة. يعزل هذا العملية كل ورقة، يتيح لك اختيار مسار إخراج مميز، ويحرّر الموارد تلقائيًا. أدناه سير العمل خطوة بخطوة الذي ستتّبعه، مع شرح لكل استدعاء API ونصائح أفضل الممارسات لتجنب المشكلات الشائعة.

### الخطوة 1: الحصول على مسار ملف الإدخال
أولاً، حدد المسار الكامل لملف XLSX المصدر الذي يحتوي على عدة أوراق.

```csharp
string inputFilePath = "Your Sample Document";
```

### الخطوة 2: تحميل جدول البيانات إلى كائن Editor
فئة `Editor` هي نقطة الدخول لجميع عمليات المستندات في GroupDocs.Editor. تقوم بقراءة تدفق الملف وتجهّز المستند للتحرير أو الاستخراج.

```csharp
using (FileStream inputStream = File.OpenRead(inputFilePath))
{
    using (Editor editor = new Editor(delegate { return inputStream; }, delegate { return new SpreadsheetLoadOptions(); }))
    {
        // Further steps will go here
    }
}
```

### الخطوة 3: إنشاء EditableDocument من الورقة الأولى
`EditableDocument` تمثل ورقة واحدة قابلة للتحرير داخل المصنف. يأخذ المُنشئ كائن `Editor` ورقم فهرس الورقة بدءًا من الصفر.

```csharp
SpreadsheetEditOptions editOptions1 = new SpreadsheetEditOptions();
editOptions1.WorksheetIndex = 0; // First tab
EditableDocument firstTabBeforeEdit = editor.Edit(editOptions1);
```

### الخطوة 4: إنشاء EditableDocument من الورقة الثانية
يمكنك تكرار النمط نفسه لأي ورقة إضافية عن طريق تغيير قيمة الفهرس.

```csharp
SpreadsheetEditOptions editOptions2 = new SpreadsheetEditOptions();
editOptions2.WorksheetIndex = 1; // Second tab
EditableDocument secondTabBeforeEdit = editor.Edit(editOptions2);
```

### الخطوة 5: حفظ الورقة الأولى كوثيقة منفصلة
`Save` يكتب المستند المُعدّل إلى ملف بالصّيغة المحددة. استدعِه على كائن `EditableDocument`، مع توفير مسار الإخراج والصيغة (مثال: `SaveFormat.Xlsx`).

```csharp
SpreadsheetSaveOptions saveOptions1 = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
string outputFilename1 = Path.GetFileNameWithoutExtension(inputFilePath) + "_tab1.xlsm";
string outputPath1 = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename1);
editor.Save(firstTabBeforeEdit, outputPath1, saveOptions1);
```

### الخطوة 6: حفظ الورقة الثانية كوثيقة منفصلة
نفس استدعاء `Save` يعمل للورقة الثانية، ويمكنك اختيار صيغة مختلفة مثل PDF إذا لزم الأمر.

```csharp
SpreadsheetSaveOptions saveOptions2 = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsb);
string outputFilename2 = Path.GetFileNameWithoutExtension(inputFilePath) + "_tab2.xlsb";
string outputPath2 = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename2);
editor.Save(secondTabBeforeEdit, outputPath2, saveOptions2);
```

### الخطوة 7: تحرير كائنات EditableDocument
`Dispose` يحرّر الموارد غير المُدارة التي يحتفظ بها المستند، مثل مقابض الملفات، مما يضمن عدم حدوث تسريبات في الخدمات طويلة التشغيل.

```csharp
firstTabBeforeEdit.Dispose();
secondTabBeforeEdit.Dispose();
```

## المشكلات الشائعة والحلول
- **خطأ “File is locked”** – تأكد من استدعاء `Dispose()` على كل `EditableDocument` وعلى كائن `Editor`، أو غلفهم بعبارات `using`.  
- **غياب الأنماط بعد التصدير** – تأكد من أنك تحفظ إلى صيغة تدعم الأنماط (مثل XLSX أو PDF). CSV سيفقد التنسيق بطبيعة الحال.  
- **المصنفات الكبيرة تسبب بطء الأداء** – استخدم خيارات التحميل المتدفقة (`LoadOptions.Streaming = true`) للحفاظ على استهلاك الذاكرة منخفضًا.

## الأسئلة المتكررة

**س: ماذا لو كان المصنف يحتوي على أوراق مخفية؟**  
ج: تُعامل الأوراق المخفية كأي ورقة أخرى؛ يمكنك الوصول إليها عبر الفهرس وحفظها، لكن قد تحتاج إلى تعيين `EditableDocument.IsVisible = true` قبل الحفظ إذا أردت ظهورها في النتيجة.

**س: هل يمكنني تحويل ورقة Excel مباشرة إلى PDF؟**  
ج: نعم، حدد `SaveFormat.Pdf` عند استدعاء `Save` على `EditableDocument`. المكتبة تحافظ على التخطيط، والصور، والرسوم البيانية أثناء التحويل.

**س: هل يمكن تقسيم المصنف إلى ملفات CSV بدلاً من XLSX؟**  
ج: بالتأكيد. استخدم `SaveFormat.Csv` لكل `EditableDocument` لإنشاء تمثيلات CSV نصية لكل ورقة.

**س: هل يدعم GroupDocs.Editor ملفات Excel المحمية بكلمة مرور؟**  
ج: نعم. قدّم كلمة المرور عبر `LoadOptions.Password` عند إنشاء كائن `Editor`.

**س: أين يمكنني العثور على المزيد من الأمثلة للعمل مع جداول البيانات؟**  
ج: الوثائق الرسمية ومشاريع العينة على [صفحة التحميل](https://releases.groupdocs.com/editor/net/) تحتوي على حالات استخدام إضافية.

## الخاتمة
باتباع هذه الخطوات، يمكنك **حفظ كل ورقة Excel** كوثيقة مستقلة، تحويل الأوراق إلى PDF، أو تقسيم المصنفات الكبيرة إلى أجزاء قابلة للإدارة—كل ذلك باستخدام مكتبة GroupDocs.Editor for .NET ذات الأداء العالي والموثوقية. تُسهل هذه القدرة خطوط إعداد التقارير، وتُؤتمت استخراج البيانات، وتقلل من التعامل اليدوي مع جداول البيانات.

**آخر تحديث:** 2026-06-06  
**تم الاختبار مع:** GroupDocs.Editor 23.11 for .NET  
**المؤلف:** GroupDocs  

## دروس ذات صلة

- [إتقان استخراج أوراق جداول البيانات في .NET باستخدام GroupDocs.Editor](/editor/net/spreadsheet-documents/mastering-spreadsheet-tab-extraction-dotnet-groupdocs-editor/)
- [حماية ملفات Excel بكلمة مرور باستخدام GroupDocs.Editor for .NET | إدارة جداول البيانات الآمنة](/editor/net/spreadsheet-documents/groupdocs-editor-net-password-excel-files/)
- [إتقان تحميل المستندات في .NET باستخدام GroupDocs.Editor: دليل شامل](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)