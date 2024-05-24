---
title: إصلاح مجموعة حقول النموذج غير الصالحة وحفظها
linktitle: إصلاح مجموعة حقول النموذج غير الصالحة وحفظها
second_title: GroupDocs.Editor .NET API
description: تعرف على كيفية إصلاح حقول النموذج غير الصالحة في DOCX باستخدام Groupdocs.Editor لـ .NET. اتبع هذا الدليل للتأكد من أن مستنداتك خالية من الأخطاء وحفظها بشكل آمن.
type: docs
weight: 11
url: /ar/net/form-field-management/fix-invalid-form-field-collection-save/
---
## مقدمة
مرحباً! إذا كنت تعمل مع حقول النماذج في المستندات وتواجه مشكلات تتعلق بمجموعات حقول النماذج غير الصالحة، فأنت في المكان الصحيح. في هذا البرنامج التعليمي، سنتعمق في كيفية إصلاح حقول النموذج غير الصالحة وحفظ المستند باستخدام Groupdocs.Editor لـ .NET. سنقوم بإرشادك خلال العملية خطوة بخطوة، مما يضمن حصولك على جميع التفاصيل التي تحتاجها لجعلها تعمل بسلاسة. هيا بنا نبدأ!
## المتطلبات الأساسية
قبل أن ننتقل إلى الكود، هناك بعض الأشياء التي يجب أن تكون لديك:
-  Groupdocs.Editor لـ .NET: تأكد من تثبيت مكتبة Groupdocs.Editor لـ .NET. يمكنك تنزيله[هنا](https://releases.groupdocs.com/editor/net/).
- بيئة التطوير: يجب أن يكون لديك بيئة تطوير .NET، مثل Visual Studio.
- المعرفة الأساسية بـ C#: يفترض هذا البرنامج التعليمي أن لديك فهمًا أساسيًا لبرمجة C#.
## استيراد مساحات الأسماء
أولاً، تحتاج إلى استيراد مساحات الأسماء الضرورية في مشروع C# الخاص بك. أضف الأسطر التالية في بداية ملف التعليمات البرمجية الخاص بك:
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System;
using System.IO;
```
## الخطوة 1: الحصول على مسار ملف الإدخال
الخطوة الأولى هي تحديد المسار إلى ملف الإدخال الخاص بك. يجب أن يكون هذا الملف مستند DOCX يحتوي على حقول النموذج.
```csharp
string inputFilePath = Constants.SampleLegacyFormFields_docx;
```
## الخطوة 2: إنشاء دفق من مسار الملف
بعد ذلك، قم بإنشاء دفق ملف لقراءة مستند الإدخال. سيسمح لك ذلك بتحميل المستند في المحرر.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
```
## الخطوة 3: إنشاء خيارات التحميل للمستند
في هذه الخطوة، تحتاج إلى إنشاء خيارات التحميل للمستند الخاص بك. إذا كان مستندك محميًا بكلمة مرور، فيمكنك تحديد كلمة المرور. في هذا المثال، المستند غير محمي، لذلك يتم تجاهل كلمة المرور.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
loadOptions.Password = "some_password_to_open_a_document";
```
## الخطوة 4: قم بتحميل المستند في مثيل المحرر
الآن، قم بتحميل المستند بالخيارات المحددة في نسخة المحرر. هذا هو المكان الذي ستتم فيه العمليات الرئيسية على المستند.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
```
## الخطوة 4.1: اقرأ مثيل FormFieldManager
 ال`FormFieldManager` المثيل مسؤول عن إدارة حقول النموذج في المستند. ستحتاج إلى قراءة هذا المثيل للوصول إلى حقول النموذج ومعالجتها.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
## الخطوة 4.2: اقرأ ملف FormFieldCollection
 ال`FormFieldCollection` يحتوي على كافة حقول النموذج في الوثيقة. ستقرأ هذه المجموعة للتحقق من حقول النماذج غير الصالحة وإصلاحها.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
## الخطوة 4.3: الإصلاح التلقائي لحقول النموذج غير الصالحة
حاول الإصلاح التلقائي لأي حقول نموذج غير صالحة في المستند. هذه خطوة أولية لمعالجة المشكلات الواضحة.
```csharp
fieldManager.FixInvalidFormFieldNames(new InvalidFormField[0]);
collection = fieldManager.FormFieldCollection;
```
## الخطوة 4.4: التحقق من وجود حقول نموذج غير صالحة
تحقق مما إذا كانت هناك أية حقول نموذج غير صالحة متبقية بعد محاولة الإصلاح التلقائي.
```csharp
bool hasInvalidFormFields = fieldManager.HasInvalidFormFields();
Console.WriteLine("FormFieldCollection contains invalid items: {0}", hasInvalidFormFields);
```
## الخطوة 4.4.1: احصل على جميع أسماء حقول النموذج غير الصالحة
استرداد أسماء جميع حقول النموذج غير الصالحة. سيتم استخدام هذه الأسماء لإصلاح الحقول.
```csharp
var invalidFormFields = fieldManager.GetInvalidFormFieldNames();
```
## الخطوة 4.4.2: إنشاء أسماء فريدة للحقول غير الصالحة
لكل حقل نموذج غير صالح، قم بإنشاء اسم فريد. وهذا يضمن عدم وجود تعارضات مع أسماء حقول النموذج الموجودة.
```csharp
foreach (var invalidItem in invalidFormFields)
{
    invalidItem.FixedName = string.Format("{0}_{1}", invalidItem.Name, Guid.NewGuid());
}
```
## الخطوة 4.4.3: إصلاح حقول النموذج غير الصالحة
قم بإصلاح حقول النموذج غير الصالحة باستخدام الأسماء الفريدة التي تم إنشاؤها في الخطوة السابقة.
```csharp
fieldManager.FixInvalidFormFieldNames(invalidFormFields);
collection = fieldManager.FormFieldCollection;
```
## الخطوة 5: إنشاء خيارات حفظ المستند
قم بإعداد الخيارات لحفظ المستند. يتضمن ذلك تحديد التنسيق وأي إعدادات حفظ إضافية.
```csharp
WordProcessingFormats docFormat = WordProcessingFormats.Docx;
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(docFormat);
```
## الخطوة 5.1: تحسين استخدام الذاكرة
 إذا كان المستند الخاص بك كبيرًا وقد يتسبب في حدوث خطأ`OutOfMemoryException`، قم بتمكين خيار تحسين الذاكرة.
```csharp
saveOptions.OptimizeMemoryUsage = true;
```
## الخطوة 5.2: حماية المستند من الكتابة
لحماية المستند من التعديل، باستثناء حقول النموذج، قم بتعيين كلمة مرور الحماية.
```csharp
saveOptions.Protection = new WordProcessingProtection(WordProcessingProtectionType.AllowOnlyFormFields, "write_password");
```
## الخطوة 6: احفظ المستند
وأخيرًا، احفظ المستند باستخدام خيارات الحفظ المحددة. قم بإعداد دفق ذاكرة لحفظ مستند الإخراج.
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(outputStream, saveOptions);
}
Console.WriteLine("FixInvalidFormFieldCollectionAndSave routine has successfully finished");
```
## خاتمة
 وهناك لديك! لقد نجحت في إصلاح حقول النموذج غير الصالحة وحفظت مستندك باستخدام Groupdocs.Editor لـ .NET. كان من المفترض أن يجعل هذا الدليل التفصيلي العملية واضحة وسهلة الإدارة. إذا واجهت أي مشاكل أو لديك أسئلة، فلا تتردد في التحقق من[توثيق](https://reference.groupdocs.com/editor/net/) أو الوصول إلى[يدعم](https://forum.groupdocs.com/c/editor/20).
## الأسئلة الشائعة
### ماذا لو كانت وثيقتي محمية بكلمة مرور؟
 يمكنك تحديد كلمة المرور في`WordProcessingLoadOptions` لفتح المستند.
### كيف أعرف إذا كانت هناك حقول نموذج غير صالحة؟
 استخدم ال`HasInvalidFormFields` طريقة للتحقق من وجود أي حقول نموذج غير صالحة في المستند.
### هل يمكنني إصلاح حقول النموذج دون تغيير أسمائها؟
يوصى بإنشاء أسماء فريدة لحقول النماذج غير الصالحة لتجنب التعارضات.
### ما هي التنسيقات التي يمكنني حفظ المستند بها؟
 يمكنك حفظ المستند بتنسيقات مختلفة مثل DOCX وPDF والمزيد عن طريق ضبط الإعداد المناسب`WordProcessingFormats`.
### كيف يمكنني تحسين استخدام الذاكرة مع حفظ المستندات الكبيرة؟
 تمكين`OptimizeMemoryUsage` الخيار في`WordProcessingSaveOptions` للتعامل مع المستندات الكبيرة بكفاءة.