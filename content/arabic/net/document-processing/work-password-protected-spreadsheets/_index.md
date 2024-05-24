---
title: العمل مع جداول البيانات المحمية بكلمة مرور
linktitle: العمل مع جداول البيانات المحمية بكلمة مرور
second_title: GroupDocs.Editor .NET API
description: تعرف على كيفية التعامل مع جداول البيانات المحمية بكلمة مرور باستخدام GroupDocs.Editor لـ .NET. يرشدك هذا الدليل التفصيلي إلى كيفية فتح ملفات Excel الآمنة.
type: docs
weight: 18
url: /ar/net/document-processing/work-password-protected-spreadsheets/
---
## مقدمة
هل تواجه صعوبة في إدارة جداول البيانات المحمية بكلمة مرور في تطبيقات .NET الخاصة بك؟ إذا كان الأمر كذلك، فأنت في المكان الصحيح! في هذا الدليل الشامل، سنرشدك خلال عملية استخدام GroupDocs.Editor لـ .NET للتعامل مع جداول البيانات المحمية بكلمة مرور بكفاءة. بحلول نهاية هذا البرنامج التعليمي، ستكون مجهزًا جيدًا لفتح ملفات Excel المشفرة وتحريرها وحفظها بسهولة.
## المتطلبات الأساسية
قبل الغوص في الكود، دعنا نتأكد من أن لديك كل ما تحتاج إلى متابعته:
- المعرفة الأساسية بـ C#: يفترض هذا البرنامج التعليمي أنك على دراية ببرمجة C#.
- .NET Framework: تأكد من تثبيت .NET Framework على جهاز التطوير الخاص بك.
-  GroupDocs.Editor لـ .NET: قم بتنزيل وتثبيت GroupDocs.Editor لـ .NET من[هنا](https://releases.groupdocs.com/editor/net/).
## استيراد مساحات الأسماء
للبدء، ستحتاج إلى استيراد مساحات الأسماء الضرورية في مشروع C# الخاص بك. توفر مساحات الأسماء هذه إمكانية الوصول إلى وظائف GroupDocs.Editor.
```csharp
using System;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
## الخطوة 1: احصل على المسار إلى ملف الإدخال
أولاً، ستحتاج إلى مسار لملف الإدخال. في هذا المثال، سنستخدم نموذجًا لملف Excel (`Your Sample Document`) محمي بكلمة مرور.
```csharp
string inputFilePath = "Your Sample Document";
```
## الخطوة 2: محاولة فتح المستند بدون كلمة مرور
دعونا نرى ما سيحدث إذا حاولنا فتح المستند دون توفير كلمة مرور.
```csharp
Editor editor = new Editor(inputFilePath);
try
{
    editor.Edit();
}
catch (GroupDocs.Editor.PasswordRequiredException)
{
    Console.WriteLine("Cannot edit the document because it is password-protected. A password is required.");
}
editor.Dispose();
```
## الخطوة 3: حاول تحديد كلمة مرور غير صحيحة
الآن، سنقوم بتحديد كلمة مرور غير صحيحة لتوضيح كيفية استجابة المحرر.
```csharp
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.Password = "incorrect_password";
editor = new Editor(inputFilePath, delegate { return loadOptions; });
try
{
    editor.Edit();
}
catch (GroupDocs.Editor.IncorrectPasswordException)
{
    Console.WriteLine("Cannot edit the document because the specified password is incorrect.");
}
editor.Dispose();
```
## الخطوة 4: افتح الملف بكلمة المرور الصحيحة
دعونا نقدم كلمة المرور الصحيحة ونفتح الملف بنجاح.
```csharp
loadOptions.Password = "excel_password";
loadOptions.OptimizeMemoryUsage = true;
editor = new Editor(inputFilePath, delegate { return loadOptions; });
```
## الخطوة 5: إنشاء وضبط خيارات التحرير
لتحرير جدول البيانات، نحتاج إلى إنشاء خيارات التحرير وضبطها.
```csharp
SpreadsheetEditOptions editOptions = new SpreadsheetEditOptions();
```
## الخطوة 6: إنشاء مستند متوسط قابل للتحرير
 بعد ذلك، نقوم بإنشاء وسيط`EditableDocument` الذي يسمح لنا بإجراء تغييرات على جدول البيانات.
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
{
    // الخطوة 7: إنشاء خيارات الحفظ
    SpreadsheetFormats xlsmFormat = SpreadsheetFormats.Xlsm;
    SpreadsheetSaveOptions saveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
    // الخطوة 7.1: تعيين كلمة مرور فتح جديدة
    saveOptions.Password = "new password";
    // الخطوة 7.2: ضبط الحماية ضد الكتابة
    saveOptions.WorksheetProtection = new WorksheetProtection(WorksheetProtectionType.All, "write password");
    // الخطوة 8: احفظ المستند دون تعديل
    //الخطوة 8.1: إعداد اسم ملف الإخراج والمسار
    string outputFilename = Path.GetFileNameWithoutExtension(inputFilePath) + "." + xlsmFormat.Extension;
    string outputPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename);
    // الخطوة 8.2: إنشاء دفق الإخراج
    using (FileStream outputStream = File.Create(outputPath))
    {
        // الخطوة 8.3: حفظ
        editor.Save(beforeEdit, outputStream, saveOptions);
    }
}
// الخطوة 9: التخلص من مثيل المحرر
editor.Dispose();
Console.WriteLine("Successfully handled the password-protected spreadsheet. Editor instance has been disposed: {0}", editor.IsDisposed ? "Yes" : "No");
```
## خاتمة
تهانينا! لقد تعلمت بنجاح كيفية التعامل مع جداول البيانات المحمية بكلمة مرور باستخدام GroupDocs.Editor لـ .NET. بدءًا من محاولة فتح المستند بدون كلمة مرور وحتى حفظه باستخدام إعدادات الحماية الجديدة، فقد قمت بتغطية كافة الخطوات الأساسية. ستعزز هذه المعرفة بلا شك قدرتك على إدارة المستندات الآمنة داخل تطبيقات .NET الخاصة بك.
## الأسئلة الشائعة
### ما هو GroupDocs.Editor لـ .NET؟
يعد GroupDocs.Editor for .NET واجهة برمجة تطبيقات قوية لتحرير المستندات تتيح للمطورين تحميل مجموعة متنوعة من تنسيقات المستندات وتحريرها وحفظها داخل تطبيقات .NET.
### كيف يمكنني الحصول على ترخيص مؤقت لـ GroupDocs.Editor؟
 يمكنك الحصول على ترخيص مؤقت من[هنا](https://purchase.groupdocs.com/temporary-license/) لتقييم ميزات المنتج.
### هل من الممكن تحسين استخدام الذاكرة أثناء تحرير المستندات الكبيرة؟
 نعم، يمكنك تمكين تحسين الذاكرة عن طريق ضبط`OptimizeMemoryUsage` الملكية ل`true`في خيارات التحميل
### هل يمكنني تعيين كلمات مرور مختلفة لفتح جدول بيانات والكتابة فيه؟
قطعاً! يمكنك تعيين كلمات مرور منفصلة لفتح المستند وللحماية ضد الكتابة باستخدام خيارات الحفظ.
### أين يمكنني العثور على وثائق أكثر تفصيلا؟
 يمكنك الوصول إلى الوثائق الشاملة الخاصة بـ GroupDocs.Editor لـ .NET[هنا](https://reference.groupdocs.com/editor/net/).