---
title: العمل مع المستندات النصية العادية
linktitle: العمل مع المستندات النصية العادية
second_title: GroupDocs.Editor .NET API
description: تعرف على كيفية تحرير المستندات النصية العادية باستخدام GroupDocs.Editor لـ .NET من خلال دليلنا التفصيلي خطوة بخطوة. قم بتبسيط عملية تحرير مستندات .NET الخاصة بك.
weight: 15
url: /ar/net/document-processing/work-plain-text-documents/
---
## مقدمة
هل تتطلع إلى تبسيط عملية تحرير المستندات في .NET؟ لا تنظر أبعد من GroupDocs.Editor لـ .NET! تسمح لك واجهة برمجة التطبيقات القوية هذه بتحرير مجموعة واسعة من تنسيقات المستندات بسهولة. في هذا البرنامج التعليمي، سنرشدك خلال عملية التعامل مع المستندات النصية العادية باستخدام GroupDocs.Editor لـ .NET. وفي النهاية، ستكون جاهزًا للتعامل مع تحرير المستندات النصية كالمحترفين. على استعداد للغوص في؟ هيا بنا نبدأ!
## المتطلبات الأساسية
قبل أن نبدأ، هناك بعض الأشياء التي ستحتاج إلى توفرها:
- بيئة تطوير .NET: تأكد من إعداد بيئة تطوير .NET صالحة للعمل. يعد Visual Studio خيارًا شائعًا.
-  GroupDocs.Editor لـ .NET: قم بتنزيل وتثبيت[GroupDocs.Editor لـ .NET](https://releases.groupdocs.com/editor/net/).
- المعرفة الأساسية بـ C#: الإلمام بلغة البرمجة C# سيساعدك على متابعة الأمثلة.
- محرر النصوص: أي محرر نصوص سيفي بالغرض، على الرغم من أنه يوصى باستخدام Visual Studio Code لميزاته وسهولة استخدامه.
## استيراد مساحات الأسماء
لبدء استخدام GroupDocs.Editor لـ .NET، تحتاج إلى استيراد مساحات الأسماء الضرورية إلى مشروعك. وهذا يضمن أن جميع الفئات والأساليب المطلوبة متاحة للاستخدام.
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```
دعونا نقسم العملية إلى خطوات يمكن التحكم فيها. تابع معنا بينما نرشدك خلال كل مرحلة من مراحل تحرير المستندات النصية العادية باستخدام GroupDocs.Editor لـ .NET.
## الخطوة 1: احصل على المسار إلى ملف TXT للإدخال
أولاً، تحتاج إلى تحديد المسار إلى ملف الإدخال TXT. يمكن أن يكون هذا مسارًا إلى ملف محلي أو دفق يحتوي على محتوى الملف.
```csharp
string inputFilePath = "YourSampleDocument.txt";
```
## الخطوة 2: إنشاء مثيل محرر
 بعد ذلك، قم بإنشاء مثيل لـ`Editor` فصل. هذه الفئة مسؤولة عن تحميل المستندات وتحريرها. لا توجد خيارات تحميل مطلوبة في هذه المرحلة.
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## الخطوة 3: إنشاء خيارات تحرير TXT
الآن، قم بإنشاء خيارات تحرير TXT. تسمح لك هذه الخيارات بتحديد كيفية معالجة محتوى النص أثناء التحرير.
```csharp
    TextEditOptions editOptions = new TextEditOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        RecognizeLists = true,
        LeadingSpaces = TextLeadingSpacesOptions.ConvertToIndent,
        TrailingSpaces = TextTrailingSpacesOptions.Trim
    };
```
## الخطوة 4: إنشاء مثيل EditableDocument
 مع تعيين خيارات التحرير، قم بإنشاء`EditableDocument` مثال. يمثل هذا المستند بتنسيق قابل للتحرير.
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## الخطوة 5: تحرير محتوى المستند
استرجع محتوى النص الأصلي وقم بإجراء التعديلات المطلوبة. في هذا المثال، سنستبدل كلمة "نص" بكلمة "نص محرر".
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("text", "EDITED text");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## الخطوة 6: إنشاء مستند قابل للتحرير بمحتوى محدث
 بعد إجراء التعديلات اللازمة، قم بإنشاء ملف جديد`EditableDocument` مع المحتوى المحدث والموارد الأصلية.
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## الخطوة 7: إنشاء خيارات حفظ معالجة الكلمات
قم بإعداد خيارات الحفظ لتنسيق WordProcessing. يستخدم هذا المثال تنسيق DOCM ويحدد اللغة.
```csharp
    WordProcessingSaveOptions wordSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm)
    {
        Locale = System.Globalization.CultureInfo.GetCultureInfo("en-GB")
    };
```
## الخطوة 8: إنشاء خيارات حفظ TXT
وبالمثل، قم بإنشاء خيارات الحفظ لتنسيق TXT. تأكد من ضبط التشفير على UTF-8 واحتفظ بتخطيط الجدول.
```csharp
    TextSaveOptions txtSaveOptions = new TextSaveOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        PreserveTableLayout = true
    };
```
## الخطوة 9: إعداد مسارات الإخراج
قم بإعداد المسارات لحفظ ملفات DOCX وTXT الناتجة. استخدم مسار ملف الإدخال لتحديد دليل الإخراج وأسماء الملفات.
```csharp
    string outputWordPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".docm");
    string outputTxtPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".txt");
```
## الخطوة 10: احفظ المستند المحرر
أخيرًا، احفظ المستند الذي تم تحريره بتنسيقي DOCX وTXT باستخدام خيارات الحفظ المحددة.
```csharp
    editor.Save(afterEdit, outputWordPath, wordSaveOptions);
    editor.Save(afterEdit, outputTxtPath, txtSaveOptions);
}
System.Console.WriteLine("Document editing process completed successfully!");
```
## خاتمة
 تهانينا! لقد قمت بتحرير مستند نص عادي بنجاح باستخدام GroupDocs.Editor لـ .NET. تعمل هذه الأداة القوية على تبسيط عملية تحرير المستندات، مما يجعل من السهل دمجها في تطبيقات .NET الخاصة بك. سواء كنت تتعامل مع ملفات نصية بسيطة أو تنسيقات مستندات معقدة، فإن GroupDocs.Editor يلبي احتياجاتك. اكتشف المزيد من الميزات والإمكانيات من خلال زيارة[وثائق GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/).
## الأسئلة الشائعة
### ما هي تنسيقات الملفات التي يدعمها GroupDocs.Editor لـ .NET؟
 يدعم GroupDocs.Editor for .NET نطاقًا واسعًا من تنسيقات الملفات، بما في ذلك DOCX وTXT وHTML والمزيد. افحص ال[توثيق](https://tutorials.groupdocs.com/editor/net/) للحصول على قائمة كاملة.
### كيف يمكنني الحصول على نسخة تجريبية مجانية من GroupDocs.Editor لـ .NET؟
 يمكنك تنزيل نسخة تجريبية مجانية من GroupDocs.Editor لـ .NET من[صفحة الإصدارات](https://releases.groupdocs.com/).
### هل يمكنني شراء ترخيص مؤقت لـ GroupDocs.Editor لـ .NET؟
نعم يمكنك الحصول على ترخيص مؤقت من[صفحة شراء GroupDocs](https://purchase.groupdocs.com/temporary-license/).
### أين يمكنني الحصول على الدعم لـ GroupDocs.Editor لـ .NET؟
 الدعم متاح من خلال[منتدى دعم GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).
### هل تتوفر وثائق تفصيلية لـ GroupDocs.Editor لـ .NET؟
 نعم، الوثائق التفصيلية متاحة على[صفحة وثائق GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/).