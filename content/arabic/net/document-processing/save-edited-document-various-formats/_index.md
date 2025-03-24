---
title: حفظ المستند المحرر بتنسيقات مختلفة
linktitle: حفظ المستند المحرر بتنسيقات مختلفة
second_title: GroupDocs.Editor .NET API
description: تعرف على كيفية حفظ المستندات التي تم تحريرها بتنسيقات مختلفة باستخدام GroupDocs.Editor لـ .NET في هذا الدليل الشامل خطوة بخطوة.
weight: 11
url: /ar/net/document-processing/save-edited-document-various-formats/
---
## مقدمة
هل تتطلع إلى حفظ المستندات التي تم تحريرها بتنسيقات مختلفة باستخدام GroupDocs.Editor لـ .NET؟ لقد جئت إلى المكان المناسب! سيرشدك هذا الدليل الشامل خلال العملية بأكملها، بدءًا من إعداد بيئتك وحتى حفظ المستند الذي تم تحريره بتنسيقات متعددة. هيا بنا نتعمق ونجعل تحرير المستندات وحفظها أمرًا سهلاً!
## المتطلبات الأساسية
قبل أن نبدأ، تأكد من أن لديك ما يلي:
1.  GroupDocs.Editor for .NET - قم بتنزيل أحدث إصدار من[هنا](https://releases.groupdocs.com/editor/net/).
2. بيئة التطوير - Visual Studio أو أي بيئة تطوير متكاملة أخرى متوافقة مع .NET.
3. .NET Framework - تأكد من تثبيت .NET Framework 4.6.1 أو أعلى.
4. نموذج مستند - نموذج مستند WordProcessing للعمل معه.
5. المعرفة الأساسية بـ C# - الإلمام ببرمجة C# مطلوب.
## استيراد مساحات الأسماء
للبدء، تأكد من استيراد مساحات الأسماء الضرورية إلى مشروع C# الخاص بك. يعد هذا أمرًا بالغ الأهمية للوصول إلى وظيفة GroupDocs.Editor.
```csharp
using System;
using GroupDocs.Editor.Metadata;
```
دعونا نقسم العملية إلى خطوات يمكن التحكم فيها. تابع بعناية للتأكد من أنك تفهم كل جزء.
## الخطوة 1: احصل على المسار إلى ملف الإدخال
أولاً، تحتاج إلى تحديد المسار إلى ملف WordProcessing الذي تم إدخاله. سيتم تحميل هذا الملف وتحريره.
```csharp
string inputFilePath = "Your Sample Document";
```
## الخطوة 2: إنشاء خيارات التحميل للمستند
بعد ذلك، قم بإنشاء خيارات التحميل الخاصة بمستندات WordProcessing. ستساعد هذه الخيارات في تخصيص كيفية تحميل المستند.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
```
## الخطوة 3: قم بتحميل المستند بالخيارات
 الآن، قم بتحميل المستند إلى ملف`Editor` مثيل باستخدام خيارات التحميل المحددة.
```csharp
using (Editor editor = new Editor(inputFilePath, delegate { return loadOptions; }))
```
## الخطوة 4: إنشاء خيارات التحرير
قم بإعداد خيارات التحرير للمستند. ستحدد هذه الخيارات كيفية فتح المستند للتحرير.
```csharp
WordProcessingEditOptions editOptions = new WordProcessingEditOptions();
```
## الخطوة 5: افتح المستند للتحرير
 افتح المستند للتحرير عن طريق إنشاء ملف`EditableDocument`مثال. سيسمح لك هذا المثيل بإجراء تغييرات على المستند.
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
```
## الخطوة 6: تحرير محتوى المستند
حان الوقت الآن لتحرير محتوى المستند. أولاً، احصل على المستند كسلسلة واحدة مشفرة بـ base64.
```csharp
string allEmbeddedInsideString = beforeEdit.GetEmbeddedHtml();
```
على سبيل المثال، دعونا نعدل العنوان الفرعي في المستند.
```csharp
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
```
## الخطوة 7: إنشاء مستند جديد قابل للتحرير من المحتوى المحرر
 إنشاء جديد`EditableDocument` مثال من المحتوى والموارد المحررة.
```csharp
using (EditableDocument afterEdit = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null))
```
## الخطوة 8: حفظ المستند بتنسيقات مختلفة
وأخيرًا، قم بالتكرار على كافة تنسيقات WordProcessing المدعومة واحفظ المستند الذي تم تحريره بكل تنسيق.
```csharp
foreach (WordProcessingFormats oneFormat in WordProcessingFormats.All)
{
    // قم بإعداد خيارات الحفظ
    WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(oneFormat);
    // تحضير مسار الحفظ
    string savePath = Path.Combine("OutputDirectory", "MultipleOutFormats." + saveOptions.OutputFormat.Extension);
    // احفظ المستند
    editor.Save(afterEdit, savePath, saveOptions);
}
```
## رسالة الإنجاز
وفي الختام، يمكنك طباعة رسالة تشير إلى انتهاء العملية بنجاح.
```csharp
Console.WriteLine("SavingEditedDocumentToAllFormats routine has successfully finished");
```
## خاتمة
تهانينا! لقد تعلمت بنجاح كيفية حفظ المستندات التي تم تحريرها بتنسيقات مختلفة باستخدام GroupDocs.Editor لـ .NET. تسهل هذه الأداة القوية التعامل مع المستندات وحفظها بتنسيقات متعددة باستخدام بضعة أسطر فقط من التعليمات البرمجية. تذكر أن الخطوات الأساسية تتضمن تحميل المستند وتحرير المحتوى وحفظه بالتنسيقات المطلوبة.
## الأسئلة الشائعة
### ما هو GroupDocs.Editor لـ .NET؟
يعد GroupDocs.Editor for .NET واجهة برمجة تطبيقات قوية تسمح لك بتحرير المستندات بتنسيقات مختلفة باستخدام تطبيقات .NET.
### هل يمكنني استخدام GroupDocs.Editor مجانًا؟
 نعم، يمكنك استخدامه مع النسخة التجريبية المجانية. تنزيله[هنا](https://releases.groupdocs.com/).
### ما هي التنسيقات التي يدعمها GroupDocs.Editor؟
يدعم GroupDocs.Editor مجموعة واسعة من التنسيقات، بما في ذلك DOCX وPDF وHTML وغيرها الكثير.
### كيف يمكنني الحصول على ترخيص مؤقت لـ GroupDocs.Editor؟
 يمكنك الحصول على ترخيص مؤقت[هنا](https://purchase.groupdocs.com/temporary-license/).
### أين يمكنني العثور على المزيد من الوثائق والدعم؟
 الوثائق التفصيلية متاحة[هنا](https://tutorials.groupdocs.com/editor/net/) ، ويمكنك الحصول على الدعم[هنا](https://forum.groupdocs.com/c/editor/20).