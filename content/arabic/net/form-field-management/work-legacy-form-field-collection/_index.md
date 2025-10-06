---
title: العمل مع مجموعة حقول النموذج القديم
linktitle: العمل مع مجموعة حقول النموذج القديم
second_title: GroupDocs.Editor .NET API
description: تعرف على كيفية إدارة حقول النماذج القديمة باستخدام GroupDocs.Editor لـ .NET من خلال دليلنا التفصيلي. مثالي للتعامل مع حقول النص ومربعات الاختيار والتواريخ والمزيد.
weight: 12
url: /ar/net/form-field-management/work-legacy-form-field-collection/
type: docs
---
# العمل مع مجموعة حقول النموذج القديم

## مقدمة
مرحبًا بك في هذا الدليل الشامل حول كيفية التعامل مع مجموعات حقول النماذج القديمة باستخدام GroupDocs.Editor لـ .NET. سواء كنت تتعامل مع حقول نصية، أو خانات اختيار، أو حقول تاريخ، أو قوائم منسدلة، فإن هذا البرنامج التعليمي سيرشدك خلال كل خطوة لإدارة هذه الحقول بكفاءة. بحلول نهاية هذا الدليل، سيكون لديك فهم قوي لكيفية استخدام GroupDocs.Editor للتعامل مع حقول النماذج المختلفة في مستنداتك. دعونا الغوص في!
## المتطلبات الأساسية
قبل أن نبدأ، تأكد من توفر المتطلبات الأساسية التالية:
- Visual Studio: أي إصدار حديث سيعمل.
- .NET Framework: تأكد من تثبيت .NET Framework.
-  GroupDocs.Editor لـ .NET: قم بتنزيل أحدث إصدار[هنا](https://releases.groupdocs.com/editor/net/).
- نموذج مستند: نموذج ملف DOCX يحتوي على حقول النموذج لأغراض الاختبار.
## استيراد مساحات الأسماء
للبدء، قم باستيراد مساحات الأسماء الضرورية في مشروعك. تعد مساحات الأسماء هذه ضرورية للوصول إلى الفئات والأساليب المطلوبة لمعالجة حقول النموذج.
```csharp
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System.IO;
```
## الخطوة 1: الحصول على مسار ملف الإدخال
أولاً، تحتاج إلى تحديد المسار إلى ملف الإدخال الخاص بك. في هذا المثال، سنستخدم نموذج ملف DOCX يحتوي على حقول نماذج متنوعة.
```csharp
string inputFilePath = "path/to/your/sample_legacy_formfields.docx";
```
## الخطوة 2: إنشاء دفق من مسار الملف
بعد ذلك، قم بإنشاء دفق ملف لقراءة محتوى المستند الخاص بك. سيتم استخدام هذا الدفق لتحميل المستند في GroupDocs.Editor.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
    // سيتم وضع رمز إضافي هنا
}
```
## الخطوة 3: إنشاء خيارات التحميل للمستند
قبل تحميل المستند، قم بإنشاء خيارات التحميل. ستساعد هذه الخيارات في التعامل مع سيناريوهات مختلفة، مثل المستندات المحمية بكلمة مرور.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
// إذا كان المستند محميًا بكلمة مرور، فحدد كلمة المرور
loadOptions.Password = "your_password_here"; // استخدم كلمة مرور فعلية إذا لزم الأمر
```
## الخطوة 4: قم بتحميل المستند بمثيل المحرر
الآن، قم بتحميل المستند إلى نسخة المحرر باستخدام دفق الملف وخيارات التحميل التي قمت بإنشائها مسبقًا.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    // سيتم وضع رمز إضافي هنا
}
```
## الخطوة 5: اقرأ مثيل FormFieldManager
لإدارة حقول النموذج، قم بالوصول إلى مثيل FormFieldManager من المحرر. سيسمح لك هذا المثيل بالتفاعل مع حقول النموذج داخل وثيقتك.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
## الخطوة 6: اقرأ ملف FormFieldCollection
استرداد FormFieldCollection من FormFieldManager. تحتوي هذه المجموعة على كافة حقول النموذج الموجودة في المستند.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
## الخطوة 7: التكرار خلال كل حقل نموذج
قم بالمراجعة خلال كل حقل نموذج في المجموعة وحدد نوعه. اعتمادًا على النوع، يمكنك استخراج قيمة الحقل ومعالجتها.
```csharp
foreach (var formField in collection)
{
    switch (formField.Type)
    {
        case FormFieldType.Text:
            TextFormField textFormField = collection.GetFormField<TextFormField>(formField.Name);
            Console.WriteLine($"TextFormField detected, name: {formField.Name}, value: {textFormField.Value}");
            break;
        case FormFieldType.CheckBox:
            CheckBoxForm checkBoxFormField = collection.GetFormField<CheckBoxForm>(formField.Name);
            Console.WriteLine($"CheckBoxForm detected, name: {formField.Name}, value: {checkBoxFormField.Value}");
            break;
        case FormFieldType.Date:
            DateFormField dateFormField = collection.GetFormField<DateFormField>(formField.Name);
            Console.WriteLine($"DateFormField detected, name: {formField.Name}, value: {dateFormField.Value}");
            break;
        case FormFieldType.Number:
            NumberFormField numberFormField = collection.GetFormField<NumberFormField>(formField.Name);
            Console.WriteLine($"NumberFormField detected, name: {formField.Name}, value: {numberFormField.Value}");
            break;
        case FormFieldType.DropDown:
            DropDownFormField dropDownFormField = collection.GetFormField<DropDownFormField>(formField.Name);
            Console.WriteLine($"DropDownFormField detected, name: {formField.Name}, value selected: {dropDownFormField.Value[dropDownFormField.SelectedIndex]}");
            break;
    }
}
```
## الخطوة 8: الاستنتاج
باتباع هذه الخطوات، يمكنك إدارة حقول النماذج القديمة والتفاعل معها بشكل فعال في مستنداتك باستخدام GroupDocs.Editor for .NET. سواء كانت حقول نصية أو مربعات اختيار أو تواريخ أو أرقام أو قوائم منسدلة، يوفر هذا الدليل طريقة واضحة وموجزة للتعامل مع كل نوع.
## خاتمة
 يمكن أن يكون العمل مع حقول النماذج القديمة في المستندات أمرًا سهلاً عند استخدام الأدوات المناسبة. يوفر GroupDocs.Editor for .NET حلاً قويًا لإدارة هذه الحقول بكفاءة. باتباع هذا الدليل التفصيلي، من المفترض أن تكون الآن قادرًا على التعامل مع حقول النماذج المختلفة في مستنداتك بسهولة. لا تنسى استكشاف[توثيق](https://tutorials.groupdocs.com/editor/net/)لمزيد من الميزات والخيارات المتقدمة.
## الأسئلة الشائعة
### 1. هل يمكنني استخدام GroupDocs.Editor لـ .NET مع المستندات المحمية بكلمة مرور؟
نعم، يمكنك تحديد كلمة المرور في خيارات التحميل للتعامل مع المستندات المحمية بكلمة مرور.
### 2. كيف يمكنني الحصول على نسخة تجريبية مجانية من GroupDocs.Editor لـ .NET؟
 يمكنك تنزيل نسخة تجريبية مجانية من[هنا](https://releases.groupdocs.com/).
### 3. هل يتوفر أي دعم لـ GroupDocs.Editor لـ .NET؟
 نعم، يمكنك الوصول إلى الدعم[هنا](https://forum.groupdocs.com/c/editor/20).
### 4. هل يمكنني شراء ترخيص GroupDocs.Editor لـ .NET؟
 نعم، يمكنك شراء ترخيص من[هنا](https://purchase.groupdocs.com/buy).
### 5. أين يمكنني العثور على الوثائق الخاصة بـ GroupDocs.Editor لـ .NET؟
الوثائق متاحة[هنا](https://tutorials.groupdocs.com/editor/net/).