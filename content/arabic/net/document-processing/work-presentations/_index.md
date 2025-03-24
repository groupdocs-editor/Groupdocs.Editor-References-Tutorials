---
title: العمل مع العروض التقديمية
linktitle: العمل مع العروض التقديمية
second_title: GroupDocs.Editor .NET API
description: تعلم كيفية تحرير عروض PowerPoint التقديمية باستخدام GroupDocs.Editor لـ .NET. اتبع هذا الدليل التفصيلي خطوة بخطوة لتبسيط عملية تحرير المستندات الخاصة بك.
weight: 16
url: /ar/net/document-processing/work-presentations/
---

# العمل مع العروض التقديمية

## مقدمة
في العصر الرقمي الحالي، تعد الإدارة الفعالة للمستندات وتحريرها أمرًا بالغ الأهمية. سواء كنت مطورًا أو شخصًا يتعامل بشكل متكرر مع العروض التقديمية، فإن معرفة كيفية العمل باستخدام الأدوات التي تبسط هذه العمليات يمكن أن توفر لك الوقت والجهد. إحدى هذه الأدوات هي GroupDocs.Editor for .NET، وهي واجهة برمجة تطبيقات قوية تتيح لك تحرير المستندات، بما في ذلك العروض التقديمية، برمجيًا. سيرشدك هذا البرنامج التعليمي خلال خطوات العمل مع العروض التقديمية باستخدام GroupDocs.Editor لـ .NET، بدءًا من إعداد البيئة الخاصة بك ووصولاً إلى تحرير ملفات العرض التقديمي وحفظها.
## المتطلبات الأساسية
قبل الغوص في البرنامج التعليمي، تأكد من أن لديك المتطلبات الأساسية التالية:
1. Visual Studio: بيئة تطوير متكاملة مناسبة لتطوير .NET.
2.  GroupDocs.Editor لـ .NET: يمكنك تنزيله من[موقع إلكتروني](https://releases.groupdocs.com/editor/net/).
3. .NET Framework: تأكد من تثبيت إصدار متوافق.
4. نموذج ملف PPTX: نموذج ملف PowerPoint للاختبار.
5. المعرفة الأساسية بـ C#: الإلمام ببرمجة C# سيكون مفيدًا.
## استيراد مساحات الأسماء
للبدء، قم باستيراد مساحات الأسماء الضرورية في مشروع C# الخاص بك. ستوفر مساحات الأسماء هذه إمكانية الوصول إلى الفئات والأساليب المطلوبة لتحرير العروض التقديمية.
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```
## الخطوة 1: الحصول على مسار ملف الإدخال
أولاً، تحتاج إلى تحديد المسار إلى ملف العرض التقديمي المدخل الخاص بك. سيتم استخدام هذا الملف لأغراض التحرير.
```csharp
string inputFilePath = "YourSampleDocument.pptx";
```
## الخطوة 2: إنشاء دفق الملفات
بعد ذلك، قم بإنشاء دفق ملف من المسار المحدد. سيتم استخدام هذا الدفق لتحميل العرض التقديمي في المحرر.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
```
## الخطوة 3: إنشاء خيارات التحميل
تحتاج إلى إنشاء خيارات تحميل خاصة بالعروض التقديمية. تتضمن هذه الخطوة التعامل مع الملفات المحمية بكلمة مرور، إن أمكن.

```csharp
PresentationLoadOptions loadOptions = new PresentationLoadOptions
{
    Password = "some_password_to_open_a_document"
};
```
## الخطوة 4: قم بتحميل المستند في المحرر
بعد أن أصبحت خيارات دفق الملف والتحميل جاهزة، قم بتحميل العرض التقديمي في نسخة المحرر.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
```
## الخطوة 5: إنشاء خيارات التحرير
قم بإعداد خيارات التحرير، مثل الشريحة المحددة التي تريد تحريرها وما إذا كنت تريد إظهار الشرائح المخفية أم لا.
حدد فهرس الشريحة التي تريد تحريرها. لاحظ أن الفهرس يعتمد على الصفر، وبالتالي فإن الشريحة الأولى هي الفهرس 0.
```csharp
PresentationEditOptions editOptions = new PresentationEditOptions
{
    SlideNumber = 0, // الشريحة الأولى
    ShowHiddenSlides = true
};
```
## الخطوة 6: إنشاء مستند قابل للتحرير
قم بإنشاء مستند متوسط قابل للتحرير باستخدام المحرر وخيارات التحرير المحددة.
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
{
```
## الخطوة 7: استخراج المحتوى والموارد
قم باستخراج المحتوى النصي كعلامة HTML واسترجاع جميع الموارد من المستند الأصلي.
```csharp
string originalContent = beforeEdit.GetContent();
```
## الخطوة 7.1: استخراج الموارد
استرداد كافة الموارد، مثل الصور والأنماط.
```csharp
List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## الخطوة 8: تعديل المحتوى
قم بتعديل المحتوى حسب الحاجة. على سبيل المثال، استبدال نص معين في محتوى HTML.
```csharp
string editedContent = originalContent.Replace("New text", "edited text");
```
## الخطوة 9: إنشاء مستند جديد قابل للتحرير
 إنشاء مثيل جديد ل`EditableDocument` مع المحتوى المحرر ونفس الموارد.
```csharp
using (EditableDocument afterEdit = EditableDocument.FromMarkup(editedContent, allResources))
{
```
## الخطوة 10: إنشاء خيارات الحفظ
قم بإعداد الخيارات لحفظ المستند الذي تم تحريره، بما في ذلك التنسيق والتشفير.
```csharp
PresentationSaveOptions saveOptions = new PresentationSaveOptions(PresentationFormats.Pptm)
{
    Password = "password"
};
```
## الخطوة 11: احفظ المستند المحرر
وأخيرًا، احفظ العرض التقديمي المحرر في الموقع المطلوب.

```csharp
string outputFilename = Path.GetFileNameWithoutExtension(inputFilePath) + "." + saveOptions.OutputFormat.Extension;
string outputPath = Path.Combine("YourOutputDirectory", outputFilename);
```
## الخطوة 11.1: إنشاء دفق الملفات للحفظ
قم بإنشاء دفق ملف لحفظ العرض التقديمي الذي تم تحريره.
```csharp
using (FileStream outputStream = File.Create(outputPath))
{
```
## الخطوة 11.2: احفظ المستند
احفظ المستند باستخدام مثيل المحرر.
```csharp
editor.Save(afterEdit, outputStream, saveOptions);
```
```csharp
}
}
}
System.Console.WriteLine("Working with presentations routine has successfully finished");
```
## خاتمة
يعد العمل مع العروض التقديمية باستخدام GroupDocs.Editor لـ .NET أمرًا مباشرًا وفعالاً. باتباع هذا الدليل التفصيلي، يمكنك بسهولة تحرير ملفات PowerPoint وحفظها برمجيًا. سواء كنت تقوم بأتمتة سير عمل المستندات أو دمج تحرير العرض التقديمي في تطبيقاتك، فإن GroupDocs.Editor يوفر الأدوات التي تحتاجها لإنجاز المهمة.
## الأسئلة الشائعة
### هل يستطيع GroupDocs.Editor لـ .NET التعامل مع العروض التقديمية المحمية بكلمة مرور؟
نعم انها تستطيع. يمكنك تحديد كلمة المرور في خيارات التحميل لفتح العروض التقديمية المحمية بكلمة مرور وتحريرها.
### ما التنسيقات التي يدعمها GroupDocs.Editor لـ .NET لحفظ العروض التقديمية؟
يدعم GroupDocs.Editor العديد من التنسيقات بما في ذلك PPTX وPPTM والمزيد. يمكنك تحديد التنسيق المطلوب في خيارات الحفظ.
### هل من الممكن تحرير شرائح متعددة في وقت واحد؟
حاليًا، يسمح لك GroupDocs.Editor بتحرير شريحة واحدة في كل مرة. يمكنك تكرار الشرائح وتطبيق التعديلات بشكل فردي إذا لزم الأمر.
### هل يمكنني استخدام GroupDocs.Editor لـ .NET في تطبيق ويب؟
نعم، يمكن دمج GroupDocs.Editor for .NET في تطبيقات الويب لتوفير إمكانيات تحرير المستندات.
### أين يمكنني العثور على مزيد من الوثائق التفصيلية والدعم؟
 يمكنك العثور على وثائق مفصلة[هنا](https://tutorials.groupdocs.com/editor/net/) . للحصول على الدعم، قم بزيارة[منتدى الدعم](https://forum.groupdocs.com/c/editor/20).