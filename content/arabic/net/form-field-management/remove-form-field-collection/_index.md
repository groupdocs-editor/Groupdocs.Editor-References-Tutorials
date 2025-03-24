---
title: إزالة مجموعة حقول النموذج
linktitle: إزالة مجموعة حقول النموذج
second_title: GroupDocs.Editor .NET API
description: تعرف على كيفية إزالة حقول النموذج من مستندات Word باستخدام GroupDocs.Editor لـ .NET باستخدام هذا الدليل التفصيلي خطوة بخطوة. مثالية للمطورين.
weight: 13
url: /ar/net/form-field-management/remove-form-field-collection/
---

# إزالة مجموعة حقول النموذج

## مقدمة
هل تتطلع إلى إدارة حقول النموذج في مستنداتك برمجياً؟ يقدم GroupDocs.Editor for .NET حلاً قويًا للتعامل مع حقول النماذج ومعالجتها بتنسيقات المستندات المختلفة. في هذا البرنامج التعليمي، سنرشدك خلال خطوات إزالة مجموعات حقول النموذج من مستند Word باستخدام هذه المكتبة القوية. 
## المتطلبات الأساسية
قبل أن نتعمق في التعليمات البرمجية، دعونا نتأكد من إعداد كل شيء للحصول على تجربة سلسة:
1. GroupDocs.Editor لـ .NET: تأكد من تنزيل GroupDocs.Editor لـ .NET وتثبيته. إذا لم يكن الأمر كذلك، يمكنك تنزيله[هنا](https://releases.groupdocs.com/editor/net/).
2. بيئة التطوير: ستحتاج إلى بيئة تطوير مثل Visual Studio.
3. .NET Framework: تأكد من تثبيت .NET Framework على جهازك.
4.  نموذج مستند: احصل على نموذج مستند Word (على سبيل المثال،`SampleLegacyFormFields.docx`) مع حقول النموذج التي تريد معالجتها.

## استيراد مساحات الأسماء
للبدء، تحتاج إلى استيراد مساحات الأسماء الضرورية في مشروع .NET الخاص بك. سيسمح لك هذا بالوصول إلى وظائف GroupDocs.Editor.
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System.IO;
```
## الخطوة 1: قم بتحميل المستند
أولاً، ستحتاج إلى تحميل المستند الذي تريد تحريره. دعونا نقسمها:
### الخطوة 1.1: احصل على المسار إلى ملف الإدخال
 تحتاج إلى تحديد المسار إلى ملف الإدخال الخاص بك. في هذا المثال، سوف نستخدم ملف عينة يسمى`SampleLegacyFormFields.docx`.
```csharp
string inputFilePath = "path/to/SampleLegacyFormFields.docx";
```
### الخطوة 1.2: إنشاء FileStream من المسار
 بعد ذلك، قم بإنشاء`FileStream` لقراءة الوثيقة.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
    // تابع إلى الخطوات التالية ضمن كتلة الاستخدام هذه.
}
```
## الخطوة 2: ضبط خيارات التحميل
عند تحميل المستند، قد تحتاج إلى تحديد خيارات التحميل، خاصةً إذا كان مستندك محميًا بكلمة مرور.
### الخطوة 2.1: إنشاء خيارات التحميل
 إنشاء مثيل ل`WordProcessingLoadOptions`.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
```
### الخطوة 2.2: تحديد كلمة المرور (إذا لزم الأمر)
إذا كان مستندك محميًا بكلمة مرور، فيمكنك تحديد كلمة المرور.
```csharp
loadOptions.Password = "some_password_to_open_a_document";
```
## الخطوة 3: قم بتحميل المستند في المحرر
 الآن قم بتحميل المستند إلى ملف`Editor` المثال باستخدام`FileStream` و`LoadOptions`.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    // تابع إلى الخطوات التالية ضمن كتلة الاستخدام هذه.
}
```
## الخطوة 4: الوصول إلى حقول النموذج وإدارتها
بعد تحميل المستند، يمكنك الآن الوصول إلى حقول النموذج ومعالجتها.
### الخطوة 4.1: اقرأ ملف FormFieldManager
 استرداد`FormFieldManager` من`Editor` مثال.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
### الخطوة 4.2: الوصول إلى FormFieldCollection
 احصل على ال`FormFieldCollection` الذي يحتوي على كافة حقول النموذج في الوثيقة.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
### الخطوة 4.3: إزالة حقل نموذج نصي محدد
لإزالة حقل نموذج نصي محدد، حدد موقعه حسب اسمه ثم قم بإزالته.
```csharp
TextFormField textField = collection.GetFormField<TextFormField>("Text1");
fieldManager.RemoveFormFiled(textField);
```
### الخطوة 4.4: إزالة حقول النماذج المتعددة
يمكنك أيضًا إزالة حقول نماذج متعددة مرة واحدة عن طريق تحديد أسمائها.
```csharp
textField = collection.GetFormField<TextFormField>("Text7");
CheckBoxForm checkBoxForm = collection.GetFormField<CheckBoxForm>("Check2");
fieldManager.RemoveFormFields(new IFormField[] { textField, checkBoxForm });
```
## الخطوة 5: احفظ المستند المعدل
بعد تعديل حقول النموذج، تحتاج إلى حفظ المستند.
### الخطوة 5.1: إنشاء خيارات الحفظ
حدد خيارات التنسيق والحفظ للمستند الناتج.
```csharp
WordProcessingFormats docFormat = WordProcessingFormats.Docx;
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(docFormat);
```
### الخطوة 5.2: تحسين استخدام الذاكرة
إذا كنت تتعامل مع مستندات كبيرة، فقد ترغب في تحسين استخدام الذاكرة.
```csharp
saveOptions.OptimizeMemoryUsage = true;
```
### الخطوة 5.3: ضبط الحماية (إذا لزم الأمر)
يمكنك حماية المستند من المزيد من التحرير عن طريق تعيين كلمة مرور للكتابة.
```csharp
saveOptions.Protection = new WordProcessingProtection(WordProcessingProtectionType.AllowOnlyFormFields, "write_password");
```
### الخطوة 5.4: احفظ المستند
 أخيرًا، احفظ المستند باستخدام ملف`MemoryStream`.
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(outputStream, saveOptions);
}
```

## خاتمة
تهانينا! لقد نجحت في إزالة حقول النموذج من مستند Word باستخدام GroupDocs.Editor لـ .NET. تعمل هذه المكتبة القوية على تسهيل التعامل مع محتوى المستند برمجيًا، مما يوفر لك الوقت والجهد.
## الأسئلة الشائعة
### هل يمكنني استخدام GroupDocs.Editor لـ .NET مع تنسيقات المستندات الأخرى؟
نعم، يدعم GroupDocs.Editor for .NET تنسيقات المستندات المختلفة، بما في ذلك PDF وHTML والمزيد.
### هل من الممكن إضافة حقول النموذج باستخدام GroupDocs.Editor لـ .NET؟
نعم، يمكنك إضافة حقول النموذج وتعديلها وإزالتها برمجيًا.
### ماذا لو كانت وثيقتي كبيرة جدًا؟
يمكنك تمكين تحسين الذاكرة في خيارات الحفظ للتعامل مع المستندات الكبيرة بكفاءة.
### هل يمكنني استخدام GroupDocs.Editor لـ .NET في تطبيق ويب؟
قطعاً! يمكن دمج GroupDocs.Editor for .NET في تطبيقات الويب لمعالجة المستندات من جانب الخادم.
### أين يمكنني الحصول على الدعم إذا واجهت مشاكل؟
 يمكنك زيارة[منتدى الدعم](https://forum.groupdocs.com/c/editor/20) للمساعدة في أي مشاكل.