---
date: 2026-06-06
description: تعرف على كيفية سرد صيغ المستندات المدعومة وتحديد امتداد صيغة الملف باستخدام
  GroupDocs.Editor لـ .NET. دليل خطوة بخطوة مع مقتطفات الكود، إجابات سريعة، وأسئلة
  شائعة.
keywords:
- list supported document formats
- determine file format extension
- GroupDocs.Editor .NET
- document editing API
- supported formats guide
linktitle: قائمة صيغ المستندات المدعومة
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to list supported document formats and determine file format
    extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets,
    quick answers, and FAQs.
  headline: List Supported Document Formats with GroupDocs.Editor .NET
  type: TechArticle
- description: Learn how to list supported document formats and determine file format
    extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets,
    quick answers, and FAQs.
  name: List Supported Document Formats with GroupDocs.Editor .NET
  steps:
  - name: '**.NET development environment** – Visual Studio 2022 or any IDE that supports
      .NET 6+.'
    text: '**.NET development environment** – Visual Studio 2022 or any IDE that supports
      .NET 6+.'
  - name: '**GroupDocs.Editor for .NET library** – download from the [GroupDocs releases
      page](https://releases.groupdocs.com/editor/net/).'
    text: '**GroupDocs.Editor for .NET library** – download from the [GroupDocs releases
      page](https://releases.groupdocs.com/editor/net/).'
  - name: '**Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/)
      for unrestricted access.'
    text: '**Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/)
      for unrestricted access.'
  - name: '**Basic C# knowledge** – familiarity with namespaces, `using` statements,
      and console output.'
    text: '**Basic C# knowledge** – familiarity with namespaces, `using` statements,
      and console output.'
  - name: '**Loop Through Formats:** We iterate over all available Word‑processing
      formats.'
    text: '**Loop Through Formats:** We iterate over all available Word‑processing
      formats.'
  - name: '**Output Format Details:** For each format we print its friendly name and
      default file extension.'
    text: '**Output Format Details:** For each format we print its friendly name and
      default file extension.'
  - name: '**Loop Through Formats:** The same looping logic applies to presentations.'
    text: '**Loop Through Formats:** The same looping logic applies to presentations.'
  - name: '**Output Format Details:** The name and extension are displayed for each
      format.'
    text: '**Output Format Details:** The name and extension are displayed for each
      format.'
  - name: '**Parse Format:** `FromExtension` converts the `.xlsm` extension into its
      internal `SpreadsheetFormat` enum.'
    text: '**Parse Format:** `FromExtension` converts the `.xlsm` extension into its
      internal `SpreadsheetFormat` enum.'
  - name: '**Output Format:** The parsed format’s name is printed, confirming the
      mapping.'
    text: '**Output Format:** The parsed format’s name is printed, confirming the
      mapping.'
  type: HowTo
- questions:
  - answer: '`DocumentFormatInfo` provides metadata about supported file types, while
      `SaveOptions` configures how a document is written back to disk (format, compression,
      etc.).'
    question: What is the difference between `DocumentFormatInfo` and `SaveOptions`?
  - answer: Yes—use `DocumentFormatInfo.FromExtension("yourExt")`; if the extension
      isn’t recognized, the method returns `null`.
    question: Can I list formats for a custom file extension?
  - answer: Absolutely. Pass the password to the `Editor` constructor via `EditorSettings`
      to open encrypted documents.
    question: Does GroupDocs.Editor support password‑protected files?
  - answer: Over **30 input and output formats**, spanning Word, Excel, PowerPoint,
      HTML, and plain text.
    question: How many formats does GroupDocs.Editor actually support?
  - answer: Use the `GetEditableWordProcessingFormats()` (or Spreadsheet/Presentation
      equivalents) to retrieve formats that allow full edit capabilities.
    question: Is there a way to restrict the list to only editable formats?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: قائمة صيغ المستندات المدعومة باستخدام GroupDocs.Editor .NET
type: docs
url: /ar/net/document-processing/work-document-formats/
weight: 13
---

# قائمة صيغ المستندات المدعومة

مرحبًا بكم في دليلنا الشامل حول **كيفية سرد صيغ المستندات المدعومة** باستخدام GroupDocs.Editor لـ .NET. سواءً كنت تبني تطبيق ويب يركز على المستندات أو أداة سطح مكتب على مستوى المؤسسات، فإن معرفة الصيغ التي يمكنك تحريرها أو تحويلها بدقة أمر أساسي. في هذا الدليل ستكتشف كيفية تعداد الصيغ، تحليل الامتدادات، وتحرير المستندات—كل ذلك مع شروحات واضحة وسهلة الفهم ومقاطع شفرة جاهزة للتنفيذ.

## الإجابات السريعة
- **كيف يمكنني سرد جميع الصيغ المدعومة؟** استخدم `DocumentFormatInfo.GetSupportedWordProcessingFormats()` (أو ما يعادلها لـ Presentation/Spreadsheet) وتكرار المجموعة.  
- **هل يمكنني تحديد صيغة من امتداد ملف؟** نعم—استدعِ `DocumentFormatInfo.FromExtension(".docx")`.  
- **ما أنواع الملفات التي يدعمها GroupDocs.Editor؟** أكثر من 30 صيغة إدخال وإخراج، بما في ذلك DOCX و XLSX و PPTX و HTML والنص العادي.  
- **هل أحتاج إلى ترخيص لسرد الصيغ؟** الترخيص المؤقت يفتح كامل الـ API؛ وإلا فإن النسخة التجريبية تعمل بميزات محدودة.  
- **ما إصدارات .NET المتوافقة؟** .NET Framework 4.6+، .NET Core 3.1+، .NET 5/6/7.

## ما هو “قائمة صيغ المستندات المدعومة”؟
تشير العبارة إلى استرجاع مجموعة أنواع الملفات التي يمكن لـ GroupDocs.Editor فتحها، تحريرها، وحفظها برمجيًا. يتيح لك هذا الإجراء بناء قوائم منسدلة ديناميكية في واجهة المستخدم أو التحقق من تحميلات المستخدمين قبل المعالجة، مما يضمن تمرير ملفات متوافقة فقط إلى المحرر للمزيد من التلاعب.

## لماذا نُدرج صيغ المستندات المدعومة؟
يُدعم GroupDocs.Editor **أكثر من 30 صيغة إدخال وإخراج** ويمكنه التعامل مع ملفات تصل إلى **2 GB** دون تحميل المستند بالكامل في الذاكرة. معرفة القائمة الدقيقة تمنع الأخطاء أثناء التشغيل، تحسن تجربة المستخدم، وتتيح لك فرض قواعد عمل مثل “السماح فقط بالمستندات القابلة للتحرير من Office”. كما تساعدك على عرض الصيغ التي يدعمها تطبيقك فعليًا للمستخدمين.

## المتطلبات المسبقة
قبل أن تبدأ، تأكد من وجود ما يلي:

1. **بيئة تطوير .NET** – Visual Studio 2022 أو أي بيئة تدعم .NET 6+.  
2. **مكتبة GroupDocs.Editor لـ .NET** – حمّلها من [صفحة إصدارات GroupDocs](https://releases.groupdocs.com/editor/net/).  
3. **ترخيص مؤقت** – احصل على [ترخيص مؤقت](https://purchase.groupdocs.com/temporary-license/) للوصول غير المحدود.  
4. **معرفة أساسية بـ C#** – الإلمام بالمساحات الاسمية، عبارات `using`، وإخراج الكونسول.

## كيفية سرد صيغ المستندات المدعومة؟
حمّل مجموعة الصيغ المدعومة واطبع اسم كل صيغة وامتداد الملف الخاص بها. يعمل هذا النمط ذو الخطوتين مع مستندات معالجة النصوص، الجداول، والعروض التقديمية. من خلال تكرار المجموعة يمكنك ملء عناصر واجهة المستخدم مثل القوائم المنسدلة ديناميكيًا، مما يضمن اختيار المستخدمين لصيغ يمكن للمحرر التعامل معها فعليًا.

```csharp
// No actual code block – placeholder retained from original tutorial
```csharp
using System;
using GroupDocs.Editor.Options;
```
```

### قائمة صيغ معالجة النصوص
`Formats.WordProcessingFormats` هي تعداد يصف كل نوع ملف معالجة نصوص يُعترف به من قبل المحرر. تُعيد الخاصية `All` مجموعة من كائنات الصيغ هذه.

```csharp
```csharp
foreach (Formats.WordProcessingFormats oneFormat in Formats.WordProcessingFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**شرح:**  
1. **التكرار عبر الصيغ:** نمر على جميع صيغ معالجة النصوص المتاحة.  
2. **إخراج تفاصيل الصيغة:** لكل صيغة نطبع اسمها الودي والامتداد الافتراضي للملف.

### قائمة صيغ العروض التقديمية
`Formats.PresentationFormats` تعمل بنفس الطريقة لملفات الشرائح، حيث تكشف كل نوع عرض تقديمي مدعوم عبر مجموعة `All`.

```csharp
```csharp
foreach (Formats.PresentationFormats oneFormat in Formats.PresentationFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**شرح:**  
1. **التكرار عبر الصيغ:** نفس منطق التكرار يُطبق على العروض التقديمية.  
2. **إخراج تفاصيل الصيغة:** يُعرض الاسم والامتداد لكل صيغة.

## كيفية تحديد امتداد صيغة الملف؟
أحيانًا يكون لديك اسم ملف فقط وتحتاج إلى استنتاج `DocumentFormat` المقابل. يقدم GroupDocs.Editor أداة ثابتة بسيطة تُحوّل امتداد الملف إلى تمثيله الداخلي، مما يسمح لك بالتحقق أو تحويل الملفات قبل تحميلها إلى المحرر.

### تحليل صيغ الجداول
`Formats.SpreadsheetFormats.FromExtension` يحول سلسلة امتداد ملف إلى قيمة تعداد صيغ الجداول المطابقة.

```csharp
```csharp
Formats.SpreadsheetFormats expectedXlsm = Formats.SpreadsheetFormats.FromExtension(".xlsm");
Console.WriteLine("Parsed Spreadsheet format is {0}", expectedXlsm.Name);
```
```

**شرح:**  
1. **تحليل الصيغة:** `FromExtension` يحول امتداد `.xlsm` إلى تعداد `SpreadsheetFormat` الداخلي.  
2. **إخراج الصيغة:** يُطبع اسم الصيغة المحللة لتأكيد التطابق.

### تحليل الصيغ النصية
وبالمثل، `Formats.TextualFormats.FromExtension` يحدد امتدادات الملفات النصية مثل HTML أو TXT.

```csharp
```csharp
Formats.TextualFormats expectedHtml = Formats.TextualFormats.FromExtension("html");
Console.WriteLine("Parsed Textual format is {0}", expectedHtml.Name);
```
```

**شرح:**  
1. **تحليل الصيغة:** طريقة `FromExtension` تُحوّل امتداد `html` إلى `TextFormat`.  
2. **إخراج الصيغة:** يُعرض اسم الصيغة النصية، وهو مفيد للمحررات القائمة على الويب.

## كيفية تحرير المستندات بعد تحديد الصيغ؟
بمجرد معرفة الصيغة، يتبع تحميل وتحرير المستند نمطًا ثابتًا. أولًا تُنشئ كائن `Editor` مع مسار الملف المصدر، ثم تستدعي `Edit()` للحصول على `EditableDocument`. من هناك يمكنك القراءة، التعديل، وأخيرًا الحفظ باستخدام `SaveOptions` المناسبة.

### تحميل مستند
`Editor` هو الفئة الأساسية التي تُغلف جميع عمليات التحرير لملف معين.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/document.docx"))
{
    // Further steps will be covered here.
}
```
```

**شرح:**  
1. **تهيئة المحرر:** إنشاء كائن `Editor` مع تمرير المسار الكامل للملف المستهدف.  
2. **نمط التخلص:** يضمن بيان `using` تحرير جميع الموارد غير المُدارة بسرعة.

### استخراج المحتوى
`EditableDocument.GetContent()` تُعيد النص الخام للمستند (أو HTML للمحررات القائمة على الويب)، ويمكنك عرضه أو معالجته.

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    string content = editableDocument.GetContent();
    Console.WriteLine(content);
}
```
```

**شرح:**  
1. **طريقة Edit:** تُعيد كائن `EditableDocument`.  
2. **الحصول على المحتوى:** `GetContent()` تستخرج النص الخام للمستند (أو HTML للمحررات القائمة على الويب).  
3. **إخراج المحتوى:** يُكتب المحتوى إلى الكونسول للتحقق.

### حفظ التغييرات
`SaveOptions` تُخبر المحرر كيف وبأي صيغة يكتب المستند المُعدل مرة أخرى إلى التخزين.

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    // Modify content here
    SaveOptions saveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docx);
    editor.Save(editableDocument, "path/to/save/document.docx", saveOptions);
}
```
```

**شرح:**  
1. **طريقة Edit:** استرجاع `EditableDocument` بعد التعديلات.  
2. **تعديل المحتوى:** تطبيق التغييرات على السلسلة (غير موضح هنا).  
3. **خيارات الحفظ:** تكوين `SaveOptions` بالصِيغة المطلوبة للإخراج.  
4. **حفظ المستند:** حفظ الملف المُعدل إلى القرص.

## كيفية العمل مع أنواع المستندات المختلفة؟
يُجرد GroupDocs.Editor التعامل مع Word، Spreadsheet، وPresentation خلف نفس واجهة الـ API، مما يسهل الانتقال بين السياقات دون الحاجة لتعلم مجموعة جديدة من الفئات لكل عائلة مستندات.

### تحرير مستندات الجداول
`SpreadsheetSaveOptions` تُحدد كيفية كتابة جدول، بما في ذلك الصيغة وإعدادات الضغط الاختيارية.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/spreadsheet.xlsx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // Modify content here
        SaveOptions saveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsx);
        editor.Save(editableDocument, "path/to/save/spreadsheet.xlsx", saveOptions);
    }
}
```
```

**شرح:**  
1. **تهيئة المحرر:** تمرير مسار ملف جدول إلى مُنشئ `Editor`.  
2. **طريقة Edit:** استرجاع `EditableDocument`.  
3. **الحصول على المحتوى:** طباعة تمثيل CSV للجدول (أو HTML).  
4. **تعديل المحتوى:** تطبيق أي تغييرات على مستوى الخلايا.  
5. **خيارات الحفظ:** اختيار `SpreadsheetSaveOptions` المناسب.  
6. **حفظ المستند:** كتابة الجدول المُحدَّث إلى التخزين.

### تحرير مستندات العروض التقديمية
`PresentationSaveOptions` تتحكم في صيغة الإخراج لملفات الشرائح، مما يتيح لك الحفاظ على النوع الأصلي أو تغييره.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/presentation.pptx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // Modify content here
        SaveOptions saveOptions = new PresentationSaveOptions(PresentationFormats.Pptx);
        editor.Save(editableDocument, "path/to/save/presentation.pptx", saveOptions);
    }
}
```
```

**شرح:**  
1. **تهيئة المحرر:** تحميل ملف PowerPoint عبر `Editor`.  
2. **طريقة Edit:** الحصول على `EditableDocument`.  
3. **الحصول على المحتوى:** استخراج HTML الشرائح أو النص العادي.  
4. **تعديل المحتوى:** تحديث العناوين، القوائم النقطية، أو الصور.  
5. **خيارات الحفظ:** استخدام `PresentationSaveOptions` لتحديد صيغة الإخراج.  
6. **حفظ المستند:** حفظ العرض التقديمي المُعدل.

## المشكلات الشائعة والحلول
- **خطأ “الصيغة غير مدعومة”:** تأكد من أنك تستخدم أحدث نسخة من GroupDocs.Editor؛ فهي تُضيف دعمًا لصيغ Office الأحدث بانتظام.  
- **استهلاك الذاكرة للملفات الكبيرة:** فعّل وضع البث عبر تعيين `EditorSettings.EnableStreaming = true` قبل تحميل المستند.  
- **الترخيص غير مُطبق:** تأكد من وضع ملف الترخيص المؤقت في جذر التطبيق أو تحميله عبر `License license = new License(); license.SetLicense("path/to/license.lic");`.

## الأسئلة المتكررة

**س: ما الفرق بين `DocumentFormatInfo` و `SaveOptions`؟**  
ج: `DocumentFormatInfo` تُوفر بيانات تعريفية حول صيغ الملفات المدعومة، بينما `SaveOptions` تُحدد كيفية كتابة المستند إلى القرص (الصيغة، الضغط، إلخ).

**س: هل يمكنني سرد صيغ لامتداد ملف مخصص؟**  
ج: نعم—استخدم `DocumentFormatInfo.FromExtension("yourExt")`؛ إذا لم يُعترف بالامتداد، تُعيد الطريقة `null`.

**س: هل يدعم GroupDocs.Editor الملفات المحمية بكلمة مرور؟**  
ج: بالتأكيد. مرّر كلمة المرور إلى مُنشئ `Editor` عبر `EditorSettings` لفتح المستندات المشفرة.

**س: كم عدد الصيغ التي يدعمها GroupDocs.Editor فعليًا؟**  
ج: أكثر من **30 صيغة إدخال وإخراج**، تشمل Word و Excel و PowerPoint و HTML والنص العادي.

**س: هل هناك طريقة لتقييد القائمة لتشمل فقط الصيغ القابلة للتحرير؟**  
ج: استخدم `GetEditableWordProcessingFormats()` (أو ما يعادلها لـ Spreadsheet/Presentation) لاسترجاع الصيغ التي تسمح بقدرات تحرير كاملة.

## موارد إضافية
- حمّل المكتبة من [صفحة إصدارات GroupDocs](https://releases.groupdocs.com/editor/net/).  
- احصل على [ترخيص مؤقت](https://purchase.groupdocs.com/temporary-license/) للوصول الكامل للميزات.  
- جرّب المنتج عبر [نسخة تجريبية مجانية](https://releases.groupdocs.com/).  
- استكشف أمثلة الاستخدام التفصيلية في [توثيق GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/).  
- احصل على المساعدة من المجتمع عبر [منتدى الدعم](https://forum.groupdocs.com/c/editor/20).

## الخاتمة
باتباعك لهذا الدليل، أصبحت الآن تعرف **كيفية سرد صيغ المستندات المدعومة**، **تحديد صيغة ملف من امتداده**، و**تحرير المستندات** عبر صيغ Word، Spreadsheet، وPresentation باستخدام GroupDocs.Editor لـ .NET. أدمج هذه المقاطع في مشاريعك لبناء تطبيقات قوية تدرك الصيغ وتُسعد المستخدمين وتقلل الأخطاء أثناء التشغيل.

---

**آخر تحديث:** 2026-06-06  
**تم الاختبار مع:** GroupDocs.Editor 23.9 لـ .NET  
**المؤلف:** GroupDocs

## الدروس ذات الصلة

- [إتقان تحميل المستندات في .NET باستخدام GroupDocs.Editor: دليل شامل](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)
- [إتقان تحرير المستندات في .NET باستخدام GroupDocs.Editor: دليل شامل](/editor/net/document-editing/master-document-editing-dotnet-groupdocs-editor/)
- [تحويل Word إلى HTML باستخدام GroupDocs.Editor .NET: دليل خطوة بخطوة](/editor/net/document-saving/convert-word-to-html-groupdocs-editor-dotnet/)