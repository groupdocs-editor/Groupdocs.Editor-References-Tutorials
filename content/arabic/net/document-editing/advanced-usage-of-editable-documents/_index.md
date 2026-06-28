---
date: 2026-03-14
description: تعلم كيفية استخراج الصور من ملفات DOCX، وتحويل DOCX إلى HTML، وحفظ المستند
  كـ HTML باستخدام GroupDocs.Editor لـ .NET.
linktitle: Extract Images from DOCX – Advanced Editable Document Usage
second_title: GroupDocs.Editor .NET API
title: استخراج الصور من DOCX – الاستخدام المتقدم للمستند القابل للتحرير
type: docs
url: /ar/net/document-editing/advanced-usage-of-editable-documents/
weight: 11
---

.

Also ensure that markdown links remain same.

Now produce final answer.# استخراج الصور من DOCX – الاستخدام المتقدم للمستند القابل للتحرير

إذا كنت مطور .NET وتبحث عن **استخراج الصور من DOCX** وتعزيز قدرات تحرير المستندات الخاصة بك، فإن GroupDocs.Editor for .NET يقدم مجموعة قوية من الأدوات. سيوجهك هذا الدليل الشامل خلال الاستخدام المتقدم للمستندات القابلة للتحرير باستخدام GroupDocs.Editor، مع تفصيل كل خطوة بالتفصيل حتى تتمكن من استغلال إمكاناته الكاملة.

## إجابات سريعة
- **كيف يمكنني استخراج الصور من ملف DOCX؟** استخدم `EditableDocument.Images` بعد تحميل المستند باستخدام `Editor`.
- **هل يمكنني تحويل DOCX إلى HTML مع الموارد المضمنة؟** نعم—استدعِ `EditableDocument.GetEmbeddedHtml()` أو `GetContent()` للحصول على ترميز HTML.
- **ما الطريقة التي تحفظ المستند المعدل كملف HTML؟** `EditableDocument.Save(htmlFilePath)` ينشئ ملف HTML مع مجلد للموارد.
- **هل يمكن استخراج الخطوط من مستند Word؟** استخدم `EditableDocument.Fonts` لاسترجاع جميع موارد الخطوط.
- **هل أحتاج إلى ترخيص للاستخدام في الإنتاج؟** يلزم وجود ترخيص صالح لـ GroupDocs.Editor؛ يتوفر إصدار تجريبي مجاني.

## ما هو **extract images from docx**؟
استخراج الصور من ملف DOCX يعني استرجاع كل صورة مدمجة في مستند Word برمجياً بحيث يمكنك إعادة استخدامها أو تعديلها أو تخزينها بشكل منفصل. يتيح GroupDocs.Editor مجموعة `Images` على كائن `EditableDocument`، مما يجعل هذه المهمة بسيطة.

## لماذا تستخدم GroupDocs.Editor لهذا سير العمل؟
- **تحكم كامل** في موارد المستند (الصور، الخطوط، CSS) دون الحاجة إلى التعامل اليدوي مع ملفات ZIP.  
- **تحويل سلس** من DOCX إلى HTML مع الحفاظ على التخطيط والتنسيق.  
- **استخراج موارد سهل** للتعامل مع الصور المخصصة، تضمين الخطوط، أو توصيلها عبر CDN.  
- **نمط إتلاف قوي** يضمن عدم وجود تسرب للذاكرة في الخدمات التي تعمل لفترات طويلة.

## المتطلبات المسبقة
- تثبيت Visual Studio على جهاز التطوير الخاص بك.  
- .NET Framework متوافق مع GroupDocs.Editor.  
- مكتبة GroupDocs.Editor for .NET. يمكنك [تنزيلها هنا](https://releases.groupdocs.com/editor/net/).  
- ترخيص صالح لـ GroupDocs.Editor. يمكنك الحصول على [إصدار تجريبي مجاني](https://releases.groupdocs.com/) أو شراء [ترخيص مؤقت](https://purchase.groupdocs.com/temporary-license/).

## استيراد مساحات الأسماء
لبدء العمل، تأكد من استيراد مساحات الأسماء الضرورية في مشروع .NET الخاص بك:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```

## الخطوة 1: إنشاء كائن EditableDocument
أولاً، تحتاج إلى إنشاء مثال من `EditableDocument` عن طريق تحميل وتحرير مستند إدخال بصيغة مدعومة.

```csharp
string inputFilePath = "YourSampleDocument.docx";
Editor editor = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```

في هذه الخطوة، نقوم بتحميل مستند الإدخال وتحضيره للتحرير.

## كيف **استخراج الصور من DOCX**؟
فيما يلي نستعرض قدرات استخراج الموارد، بدءًا من الحاجة الأكثر شيوعًا—استخراج جميع الصور من ملف Word.

## الخطوة 2: استخراج موارد المستند
يحتوي `EditableDocument` على موارد مختلفة يمكن استخراجها ومعالجتها. دعنا نفصلها:

### الخطوة 2.1: استخراج المستند بالكامل كـ HTML
يمكنك إنشاء سلسلة واحدة تحتوي على المستند بالكامل مع جميع موارده المدمجة كـ HTML.

```csharp
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```

ستكون هذه السلسلة كبيرة الحجم لأنها تشمل ملفات الأنماط، الصور، والخطوط المشفرة بصيغة base64.

### الخطوة 2.2: استخراج جميع الصور *(الكلمة المفتاحية الأساسية في الفعل)*
استخراج جميع الصور من المستند—هذا هو جوهر **extract images from docx**.

```csharp
List<IImageResource> allImages = beforeEdit.Images;
```

### الخطوة 2.3: استخراج جميع الخطوط *(الكلمة المفتاحية الثانوية)*
إذا كنت بحاجة أيضًا إلى **استخراج الخطوط من word**، استخدم الاستدعاء التالي:

```csharp
List<FontResourceBase> allFonts = beforeEdit.Fonts;
```

### الخطوة 2.4: استخراج جميع ملفات الأنماط
استخراج جميع ملفات الأنماط بصيغة نصية.

```csharp
List<CssText> allStylesheets = beforeEdit.Css;
```

### الخطوة 2.5: جمع جميع الموارد
جمع جميع الموارد في استدعاء واحد.

```csharp
List<IHtmlResource> allResources = beforeEdit.AllResources;
```

يتضمن ذلك الصور، الخطوط، وملفات الأنماط.

### الخطوة 2.6: الحصول على ترميز HTML
احصل على ترميز HTML للمستند بدون الموارد المدمجة.

```csharp
string htmlMarkup = beforeEdit.GetContent();
```

## كيف **تحويل docx إلى html** مع معالجة مخصصة؟
أحيانًا تحتاج إلى تعديل الروابط الخارجية لتشير إلى معالجات الموارد الخاصة بك.

## الخطوة 3: تعديل الروابط الخارجية
### الخطوة 3.1: إعداد البادئات المخصصة
إعداد البادئات التي ستضاف قبل الروابط الخارجية الأصلية.

```csharp
string customImagesRequesthandlerUri = "http://example.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://example.com/CssHandler/id=";
string customFontsRequesthandlerUri = "http://example.com/FontsHandler/id=";
```

### الخطوة 3.2: إنشاء ترميز HTML مع بادئات
إنشاء ترميز HTML مع روابط معدلة.

```csharp
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```

### الخطوة 3.3: الحصول على محتوى HTML للجسم فقط
بعض محررات WYSIWYG تتعامل فقط مع ترميز HTML النقي بدون رؤوس.

```csharp
string onlyBodyContent = beforeEdit.GetBodyContent();
```

### الخطوة 3.4: محتوى الجسم فقط مع بادئات
إنشاء محتوى للجسم فقط مع بادئات صور مخصصة.

```csharp
string prefixedBodyContent = beforeEdit.GetBodyContent(customImagesRequesthandlerUri);
```

### الخطوة 3.5: استخراج ملفات الأنماط
استخراج ملفات الأنماط المستخدمة في المستند.

```csharp
List<string> stylesheets = beforeEdit.GetCssContent();
```

### الخطوة 3.6: ملفات الأنماط مع بادئات
استخراج ملفات الأنماط مع بادئات مخصصة.

```csharp
List<string> prefixedStylesheets = beforeEdit.GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri);
```

## كيف **حفظ المستند كـ html** بشكل صحيح؟
## الخطوة 4: حفظ المستند كـ HTML
احفظ المستند المعدل كملف HTML، مع تضمين موارده.

```csharp
string htmlFilePath = Path.Combine("output", Path.GetFileNameWithoutExtension(inputFilePath) + ".html");
beforeEdit.Save(htmlFilePath);
```

تنشئ هذه الطريقة دليلًا منفصلًا للموارد مثل ملفات الأنماط، الصور، والخطوط.

## الخطوة 5: إتلاف EditableDocument
`EditableDocument` يطبق `IDisposable` ويوفر القدرة على التحقق مما إذا كان الكائن قد تم إتلافه.

```csharp
Console.WriteLine("EditableDocument is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");
```

### الخطوة 5.1 معالجة حدث الإتلاف
يمكنك أيضًا الاشتراك في حدث الإتلاف.

```csharp
EventHandler someMethod = delegate { Console.WriteLine("Disposing event was spotted!"); };
beforeEdit.Disposed += someMethod;
```

## الخطوة 6: إنشاء EditableDocument من HTML
إنشاء مثال من `EditableDocument` من مستند HTML.

### الخطوة 6.1: من ملف HTML

```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
```

### الخطوة 6.2: من ترميز HTML

```csharp
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);
```

هذه الأمثلة (`afterEditFromFile` و `afterEditFromMarkup`) هي نفسها الأصل (`beforeEdit`).

## الخطوة 7: الإتلاف اليدوي
قم بإتلاف كائنات `EditableDocument` يدويًا.

```csharp
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```

هذا يضمن تنظيف الموارد بشكل صحيح.

## المشكلات الشائعة والحلول
- **عدم ظهور الصور بعد الاستخراج:** تأكد من أن المستند يحتوي فعليًا على صور مدمجة وأنك تصل إلى `beforeEdit.Images` بعد استدعاء `Edit`.  
- **غياب الخطوط في مخرجات HTML:** تأكد من استدعاء `GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri)` لتضمين عناوين URL للخطوط بشكل صحيح.  
- **سلاسل HTML الكبيرة تسبب ضغطًا على الذاكرة:** استخدم `GetContent()` للحصول على الترميز بدون موارد مدمجة وقدّم الصور/CSS من ملفات منفصلة.

## الأسئلة المتكررة

**س: ما الصيغ التي يدعمها GroupDocs.Editor؟**  
ج: يدعم GroupDocs.Editor صيغ DOCX، XLSX، PPTX، والعديد من صيغ المكاتب الشائعة الأخرى.

**س: هل يمكنني استخدام GroupDocs.Editor بدون ترخيص؟**  
ج: نعم، يمكنك استخدامه مع [إصدار تجريبي مجاني](https://releases.groupdocs.com/) أو [ترخيص مؤقت](https://purchase.groupdocs.com/temporary-license/).

**س: كيف يمكنني استخراج موارد محددة من مستند؟**  
ج: استخدم مجموعات `Images`، `Fonts`، و `Css` على كائن `EditableDocument`.

**س: هل يمكن تعديل الروابط في مخرجات HTML؟**  
ج: نعم، مرّر بادئات URI مخصصة إلى `GetContent` أو `GetBodyContent` لإعادة كتابة روابط الصور، CSS، والخطوط.

**س: كيف أحفظ مستندًا معدلًا كملف HTML؟**  
ج: استدعِ طريقة `Save` على كائن `EditableDocument`، مع توفير مسار ملف ينتهي بـ `.html`.

---

**آخر تحديث:** 2026-03-14  
**تم الاختبار مع:** GroupDocs.Editor for .NET (أحدث إصدار)  
**المؤلف:** GroupDocs