---
title: العمل مع القيم المنفصلة المحددة (DSV)
linktitle: العمل مع القيم المنفصلة المحددة (DSV)
second_title: GroupDocs.Editor .NET API
description: تعرف على كيفية تحرير ملفات CSV وTSV باستخدام GroupDocs.Editor لـ .NET باستخدام هذا الدليل التفصيلي خطوة بخطوة. قم بتحسين مشاريع .NET الخاصة بك بسهولة.
weight: 12
url: /ar/net/document-processing/work-dsv/
type: docs
---
# العمل مع القيم المنفصلة المحددة (DSV)

## مقدمة
إذا كنت مطورًا يعمل مع القيم المنفصلة المحددة (DSV) مثل ملفات CSV أو TSV، فأنت تعلم أن تحرير هذه الملفات برمجيًا يمكن أن يكون مهمة شاقة. ومع ذلك، باستخدام GroupDocs.Editor لـ .NET، تصبح هذه المهمة أبسط وأكثر كفاءة بشكل ملحوظ. في هذا البرنامج التعليمي، سنرشدك إلى كيفية استخدام GroupDocs.Editor لـ .NET لقراءة ملفات DSV وتحريرها وحفظها. سنقوم بتقسيم العملية إلى خطوات سهلة المتابعة، مما يسهل عليك تنفيذها في مشاريعك.
## المتطلبات الأساسية
قبل أن نتعمق في البرنامج التعليمي، تأكد من أن لديك المتطلبات الأساسية التالية:
- Visual Studio: تأكد من تثبيت Visual Studio على جهازك.
-  GroupDocs.Editor لـ .NET: ستحتاج إلى تنزيل GroupDocs.Editor لمكتبة .NET والإشارة إليه. يمكنك تنزيله[هنا](https://releases.groupdocs.com/editor/net/).
- الفهم الأساسي لـ C#: يفترض هذا البرنامج التعليمي أن لديك فهمًا أساسيًا لتطوير C# و.NET.
## استيراد مساحات الأسماء
أولاً، تحتاج إلى استيراد مساحات الأسماء الضرورية في مشروعك. توفر مساحات الأسماء هذه الفئات والأساليب المطلوبة للعمل مع GroupDocs.Editor لـ .NET.
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

## الخطوة 1: احصل على المسار إلى ملف إدخال DSV
أولاً، تحتاج إلى تحديد المسار إلى ملف الإدخال DSV. في هذا المثال، سنفترض أنه ملف CSV.
```csharp
string inputFilePath = "Your Sample Document";
```
## الخطوة 2: إنشاء مثيل محرر
 إنشاء مثيل لـ`Editor` فصل. سيتم استخدام هذا المثيل لتحميل ملف DSV ومعالجته.
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## الخطوة 3: إنشاء خيارات تحرير DSV
 بعد ذلك، قم بإنشاء مثيل لـ`DelimitedTextEditOptions` وحدد المحدد لملف DSV. هنا نستخدم الفاصلة كمحدد.
```csharp
    Options.DelimitedTextEditOptions editOptions = new DelimitedTextEditOptions(",");
    editOptions.ConvertDateTimeData = false;
    editOptions.ConvertNumericData = true;
    editOptions.TreatConsecutiveDelimitersAsOne = true;
```
## الخطوة 4: إنشاء مثيل EditableDocument
 يخترع`EditableDocument` المثال باستخدام`Editor.Edit` طريقة. يؤدي هذا إلى تحضير المستند للتحرير.
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## الخطوة 5: تحرير محتوى المستند
استرداد محتوى النص الأصلي وإجراء التعديلات اللازمة. لأغراض العرض التوضيحي، دعونا نستبدل بعض النص.
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("SsangYong", "Chevrolet").Replace("Kyron", "Camaro");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## الخطوة 6: إنشاء مستند قابل للتحرير بمحتوى محدث
 إنشاء جديد`EditableDocument` مع المحتوى المحدث.
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## الخطوة 7: إنشاء خيارات حفظ CSV
حدد خيارات الحفظ لتنسيق CSV، بما في ذلك المحدد والتشفير.
```csharp
    Options.DelimitedTextSaveOptions csvSaveOptions = new DelimitedTextSaveOptions(",");
    csvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## الخطوة 8: إنشاء خيارات حفظ TSV
وبالمثل، حدد خيارات الحفظ لتنسيق TSV.
```csharp
    Options.DelimitedTextSaveOptions tsvSaveOptions = new DelimitedTextSaveOptions("\t");
    tsvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## الخطوة 9: إنشاء خيارات حفظ جدول البيانات
إذا كنت بحاجة إلى حفظ المستند كجدول بيانات، فقم بإنشاء خيارات الحفظ المقابلة.
```csharp
    Options.SpreadsheetSaveOptions cellsSaveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
```
## الخطوة 10: تحضير مسارات الحفظ
تحديد المسارات حيث سيتم حفظ الملفات المحررة.
```csharp
    string outputCsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".csv");
    string outputTsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".tsv");
    string outputCellsPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".xlsm");
```
## الخطوة 11: احفظ المستند المحرر
احفظ المستند الذي تم تحريره في المسارات المحددة بتنسيقات مختلفة.
```csharp
    editor.Save(afterEdit, outputCsvPath, csvSaveOptions);
    editor.Save(afterEdit, outputTsvPath, tsvSaveOptions);
    editor.Save(afterEdit, outputCellsPath, cellsSaveOptions);
```
## الخطوة 12: التخلص من مثيلات EditableDocument
 وأخيرا، تأكد من التخلص من`EditableDocument` حالات لتحرير الموارد.
```csharp
    beforeEdit.Dispose();
    afterEdit.Dispose();
}
System.Console.WriteLine("WorkingWithDsv routine has successfully finished");
```
## خاتمة
يعد تحرير ملفات DSV باستخدام GroupDocs.Editor لـ .NET عملية مباشرة تتضمن إنشاء نسخة محرر وتعيين خيارات التحرير وتعديل المحتوى وحفظ التغييرات. من المفترض أن يساعدك هذا الدليل التفصيلي على دمج هذه الوظيفة في تطبيقات .NET الخاصة بك بسهولة. سواء كنت تعمل باستخدام تنسيقات CSV أو TSV أو DSV أخرى، فإن GroupDocs.Editor for .NET يوفر حلاً قويًا ومرنًا.
## الأسئلة الشائعة
### هل يمكنني استخدام GroupDocs.Editor لـ .NET لتحرير ملفات CSV الكبيرة؟
نعم، GroupDocs.Editor for .NET قادر على التعامل مع ملفات CSV الكبيرة بكفاءة.
### هل يدعم GroupDocs.Editor for .NET تنسيقات DSV الأخرى إلى جانب CSV وTSV؟
نعم، فهو يدعم تنسيقات DSV المختلفة طالما قمت بتحديد المحدد المناسب.
### هل من الممكن تخصيص الترميز عند حفظ ملفات DSV؟
بالتأكيد، يمكنك تحديد الترميز المطلوب في خيارات الحفظ.
### هل يمكنني تحويل ملف CSV إلى جدول بيانات Excel باستخدام GroupDocs.Editor لـ .NET؟
نعم، يمكنك حفظ ملف CSV كجدول بيانات Excel باستخدام خيارات الحفظ المناسبة.
### أين يمكنني العثور على مزيد من الوثائق حول GroupDocs.Editor لـ .NET؟
 يمكنك العثور على وثائق مفصلة[هنا](https://tutorials.groupdocs.com/editor/net/)