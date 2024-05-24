---
title: حفظ المستند
linktitle: حفظ المستند
second_title: GroupDocs.Editor .NET API
description: قم بتحرير المستندات وحفظها بسهولة باستخدام GroupDocs.Editor لـ .NET. يعمل هذا الدليل التفصيلي على تبسيط العملية للمطورين.
type: docs
weight: 14
url: /ar/net/document-editing/save-document/
---
## مقدمة
هل تتطلع إلى تحرير المستندات وحفظها بسهولة باستخدام GroupDocs.Editor لـ .NET؟ أنت في المكان الصحيح! سيرشدك هذا البرنامج التعليمي خلال العملية خطوة بخطوة، مما يضمن أنه يمكنك إدارة مستنداتك بسهولة. سواء كنت مطورًا متمرسًا أو مبتدئًا، سيزودك دليلنا بجميع المعلومات التي تحتاجها للبدء.
## المتطلبات الأساسية
قبل الغوص في البرنامج التعليمي، تأكد من توفر المتطلبات الأساسية التالية:
- بيئة التطوير: Visual Studio مثبت على جهازك.
- .NET Framework: تأكد من أن لديك .NET Framework 4.6.1 أو إصدار أحدث.
-  GroupDocs.Editor لـ .NET: قم بتنزيل أحدث إصدار[هنا](https://releases.groupdocs.com/editor/net/).
- المعرفة الأساسية بـ C#: الإلمام ببرمجة C# أمر ضروري.
## استيراد مساحات الأسماء
لاستخدام GroupDocs.Editor في مشروع .NET الخاص بك، تحتاج إلى استيراد مساحات الأسماء الضرورية. إليك كيفية القيام بذلك:
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
الآن بعد أن قمنا بإعداد بيئتنا واستيراد مساحات الأسماء الضرورية، فلنتعمق في الخطوات المطلوبة لتحميل مستند وتحريره وحفظه باستخدام GroupDocs.Editor لـ .NET.
## الخطوة 1: قم بتحميل المستند
أولاً، نحتاج إلى تحميل المستند الذي نريد تحريره. يجعل GroupDocs.Editor هذه العملية واضحة ومباشرة. وإليك كيف يمكنك القيام بذلك:

```csharp
string inputFilePath = "Your Sample Document";
Editor editor = new Editor(inputFilePath, delegate { return new Options.WordProcessingLoadOptions(); });
EditableDocument defaultWordProcessingDoc = editor.Edit();
```
 في هذه الخطوة، نحدد المسار إلى المستند الذي نريد تحريره وإنشاء مثيل له`Editor` فصل. ال`Edit` يتم بعد ذلك استدعاء الطريقة لتحميل المستند في ملف`EditableDocument` هدف.
## الخطوة 2: تعديل الوثيقة
بعد تحميل المستند، حان الوقت لإجراء بعض التعديلات. وبما أننا لا نمتلك محرر WYSIWYG مرفقًا، فسنقوم بمحاكاة عملية التحرير في التعليمات البرمجية.

```csharp
string allEmbeddedInsideString = defaultWordProcessingDoc.GetEmbeddedHtml();
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
EditableDocument editedDoc = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```
 هنا، نقوم باسترداد محتوى HTML المضمن للمستند، وإجراء استبدال بسيط للنص، وإنشاء نص جديد`EditableDocument`مثيل من HTML المعدل.
## الخطوة 3: احفظ المستند
بعد تحرير المستند، الخطوة الأخيرة هي حفظه. يوفر GroupDocs.Editor خيارات متعددة لحفظ المستند بتنسيقات مختلفة.
## حفظ باسم RTF
```csharp
string outputRtfPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.rtf");
WordProcessingSaveOptions rtfSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
editor.Save(editedDoc, outputRtfPath, rtfSaveOptions);
```
## حفظ باسم DOCM
```csharp
string outputDocmPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.docm");
WordProcessingSaveOptions docmSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm);
using (FileStream outputStream = File.Create(outputDocmPath))
{
    editor.Save(editedDoc, outputStream, docmSaveOptions);
}
```
## حفظ كنص عادي
```csharp
string outputTxtPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.txt");
TextSaveOptions textSaveOptions = new TextSaveOptions
{
    Encoding = System.Text.Encoding.UTF8,
    PreserveTableLayout = true
};
editor.Save(editedDoc, outputTxtPath, textSaveOptions);
```
## الخطوة 4: التنظيف
 أخيرًا، من الضروري التخلص من`EditableDocument` و`Editor` حالات لتحرير الموارد.
```csharp
editedDoc.Dispose();
defaultWordProcessingDoc.Dispose();
editor.Dispose();
```
باتباع هذه الخطوات، يمكنك تحميل المستندات وتحريرها وحفظها بكفاءة باستخدام GroupDocs.Editor لـ .NET. توفر هذه الأداة القوية المرونة وسهولة الاستخدام، مما يجعل إدارة المستندات أمرًا سهلاً.
## خاتمة
لم يكن تحرير المستندات وحفظها برمجيًا أسهل من أي وقت مضى مع GroupDocs.Editor for .NET. يرشدك هذا الدليل خلال العملية بأكملها، بدءًا من تحميل المستند وحتى حفظه بتنسيقات مختلفة. مع GroupDocs.Editor، لديك حل قوي ومتعدد الاستخدامات في متناول يدك، مما يبسط عملية تحرير المستندات.
## الأسئلة الشائعة
### ما هي تنسيقات الملفات التي يدعمها GroupDocs.Editor؟
يدعم GroupDocs.Editor العديد من تنسيقات الملفات، بما في ذلك DOCX وRTF وTXT وغيرها الكثير. للحصول على القائمة الكاملة، قم بمراجعة[توثيق](https://reference.groupdocs.com/editor/net/).
### هل يمكنني تجربة GroupDocs.Editor قبل الشراء؟
 نعم يمكنك الحصول على[تجربة مجانية](https://releases.groupdocs.com/) لاختبار ميزات GroupDocs.Editor.
### هل هناك أي دعم متاح إذا واجهت مشاكل؟
 قطعاً! يمكنك زيارة[منتدى الدعم](https://forum.groupdocs.com/c/editor/20) للمساعدة في أي مشاكل تواجهها.
### كيف أحصل على ترخيص مؤقت؟
 يمكنك طلب أ[ترخيص مؤقت](https://purchase.groupdocs.com/temporary-license/) لأغراض التقييم.
### أين يمكنني شراء الإصدار الكامل من GroupDocs.Editor؟
 يمكنك شراء النسخة الكاملة[هنا](https://purchase.groupdocs.com/buy).