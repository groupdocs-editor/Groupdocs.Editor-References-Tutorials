---
title: العمل مع جداول البيانات متعددة علامات التبويب
linktitle: العمل مع جداول البيانات متعددة علامات التبويب
second_title: GroupDocs.Editor .NET API
description: تعرف على كيفية العمل مع جداول البيانات متعددة علامات التبويب في .NET باستخدام GroupDocs.Editor. تم تضمين دليل خطوة بخطوة وأمثلة التعليمات البرمجية وأفضل الممارسات.
type: docs
weight: 17
url: /ar/net/document-processing/work-multi-tab-spreadsheets/
---
## مقدمة
يمكن أن يكون التعامل مع جداول البيانات متعددة علامات التبويب مهمة كبيرة، خاصة عندما تحتاج إلى معالجة البيانات أو استخراجها من أوراق مختلفة داخل نفس المستند. إذا كنت تعمل مع .NET وتبحث عن حل قوي، فإن GroupDocs.Editor for .NET يعد خيارًا ممتازًا. في هذا البرنامج التعليمي، سنرشدك خلال عملية العمل مع جداول البيانات متعددة علامات التبويب باستخدام GroupDocs.Editor لـ .NET. سنغطي كل شيء بدءًا من إعداد بيئتك وحتى حفظ كل علامة تبويب كملف منفصل.
## المتطلبات الأساسية
قبل الغوص في البرنامج التعليمي، تأكد من توفر المتطلبات الأساسية التالية:
1. Visual Studio: تأكد من تثبيت Visual Studio على جهازك.
2. .NET Framework: يدعم GroupDocs.Editor لـ .NET .NET Framework 4.0 أو أعلى.
3. GroupDocs.Editor لـ .NET: قم بتنزيل وتثبيت GroupDocs.Editor لمكتبة .NET. يمكنك الحصول عليه من[صفحة التحميل](https://releases.groupdocs.com/editor/net/).
4.  الترخيص: بينما يمكنك استخدام ملف[ترخيص مؤقت](https://purchase.groupdocs.com/temporary-license/) لتجربة المكتبة، يوصى بشراء ترخيص كامل لاستخدام الإنتاج.
## استيراد مساحات الأسماء
قبل أن نبدأ البرمجة، تحتاج إلى استيراد مساحات الأسماء الضرورية. أضف ما يلي باستخدام التوجيهات إلى أعلى ملف .cs الخاص بك:
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
## 1. احصل على المسار إلى ملف الإدخال
أولاً، تحتاج إلى تحديد المسار إلى ملف جدول بيانات الإدخال الخاص بك. يجب أن يكون هذا الملف بتنسيق XLSX (OOXML) مع علامات تبويب متعددة.
```csharp
string inputFilePath = "Your Sample Document";
```
## 2. قم بتحميل جدول البيانات في مثيل المحرر
 بعد ذلك، ستقوم بتحميل جدول البيانات إلى ملف`Editor` مثال. ويتم ذلك باستخدام دفق الملفات وتحديد خيارات التحميل المناسبة لجدول البيانات.
```csharp
using (FileStream inputStream = File.OpenRead(inputFilePath))
{
    using (Editor editor = new Editor(delegate { return inputStream; }, delegate { return new SpreadsheetLoadOptions(); }))
    {
        // سيتم اتباع خطوات أخرى هنا
    }
}
```
## 3. قم بإنشاء مستند قابل للتحرير من علامة التبويب الأولى
 لتحرير علامة تبويب معينة أو معالجتها، تحتاج إلى إنشاء ملف`EditableDocument` مثيل لعلامة التبويب هذه. يتم تحديد علامة التبويب باستخدام فهرس يستند إلى 0.
```csharp
SpreadsheetEditOptions editOptions1 = new SpreadsheetEditOptions();
editOptions1.WorksheetIndex = 0; // علامة التبويب الأولى
EditableDocument firstTabBeforeEdit = editor.Edit(editOptions1);
```
## 4. قم بإنشاء مستند قابل للتحرير من علامة التبويب الثانية
 وبالمثل، قم بإنشاء`EditableDocument` لعلامة التبويب الثانية.
```csharp
SpreadsheetEditOptions editOptions2 = new SpreadsheetEditOptions();
editOptions2.WorksheetIndex = 1; // علامة التبويب الثانية
EditableDocument secondTabBeforeEdit = editor.Edit(editOptions2);
```
## 5. احفظ علامة التبويب الأولى في مستند منفصل
الآن، احفظ علامة التبويب الأولى كمستند منفصل. حدد تنسيق الحفظ ومسار الإخراج.
```csharp
SpreadsheetSaveOptions saveOptions1 = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
string outputFilename1 = Path.GetFileNameWithoutExtension(inputFilePath) + "_tab1.xlsm";
string outputPath1 = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename1);
editor.Save(firstTabBeforeEdit, outputPath1, saveOptions1);
```
## 6. احفظ علامة التبويب الثانية في مستند منفصل
كرر العملية لعلامة التبويب الثانية، ولكن هذه المرة احفظها بتنسيق مختلف.
```csharp
SpreadsheetSaveOptions saveOptions2 = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsb);
string outputFilename2 = Path.GetFileNameWithoutExtension(inputFilePath) + "_tab2.xlsb";
string outputPath2 = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename2);
editor.Save(secondTabBeforeEdit, outputPath2, saveOptions2);
```
## 7. التخلص من مثيلات الوثيقة القابلة للتحرير
 وأخيرا، تأكد من التخلص بشكل صحيح من`EditableDocument` حالات لتحرير الموارد.
```csharp
firstTabBeforeEdit.Dispose();
secondTabBeforeEdit.Dispose();
```

## خاتمة
باتباع هذه الخطوات، يمكنك بسهولة العمل مع جداول البيانات متعددة علامات التبويب في .NET باستخدام GroupDocs.Editor. تعمل هذه المكتبة القوية على تبسيط عملية تحرير الأوراق المختلفة وحفظها داخل جدول بيانات، مما يجعل مهام التطوير الخاصة بك أكثر سهولة في الإدارة. سواء كنت تتعامل مع معالجة معقدة للبيانات أو عمليات تحرير بسيطة، فإن GroupDocs.Editor for .NET يوفر الأدوات التي تحتاجها لإنجاز المهمة بكفاءة.
## الأسئلة الشائعة
### ما هو GroupDocs.Editor لـ .NET؟
يعد GroupDocs.Editor for .NET واجهة برمجة تطبيقات قوية لتحرير المستندات تسمح للمطورين بتحميل المستندات ذات التنسيقات المختلفة وتحريرها وحفظها داخل تطبيقات .NET.
### هل يمكنني تجربة GroupDocs.Editor لـ .NET قبل الشراء؟
 نعم يمكنك استخدام أ[تجربة مجانية](https://releases.groupdocs.com/) أو طلب أ[ترخيص مؤقت](https://purchase.groupdocs.com/temporary-license/) لتقييم المنتج.
### ما تنسيقات الملفات التي يدعمها GroupDocs.Editor لـ .NET؟
يدعم GroupDocs.Editor مجموعة واسعة من التنسيقات، بما في ذلك DOCX وXLSX وPPTX وPDF وغيرها الكثير.
### كيف يمكنني الحصول على الدعم لـ GroupDocs.Editor لـ .NET؟
 يمكنك الحصول على الدعم من خلال زيارة[منتدى الدعم](https://forum.groupdocs.com/c/editor/20).
### أين يمكنني شراء ترخيص كامل لـ GroupDocs.Editor لـ .NET؟
 يمكنك شراء ترخيص كامل من[صفحة الشراء](https://purchase.groupdocs.com/buy).