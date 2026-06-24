---
date: 2026-05-12
description: تعلم كيفية استخراج الخطوط وغيرها من موارد HTML من المستندات باستخدام
  GroupDocs.Editor لـ .NET. دليل خطوة بخطوة لمطوري .NET.
keywords:
- how to extract fonts
- GroupDocs.Editor .NET
- extract HTML resources
linktitle: حفظ موارد HTML في مجلد
schemas:
- author: GroupDocs
  dateModified: '2026-05-12'
  description: Learn how to extract fonts and other HTML resources from documents
    using GroupDocs.Editor for .NET. Step‑by‑step guide for .NET developers.
  headline: How to Extract Fonts and Save HTML Resources to Folder
  type: TechArticle
- description: Learn how to extract fonts and other HTML resources from documents
    using GroupDocs.Editor for .NET. Step‑by‑step guide for .NET developers.
  name: How to Extract Fonts and Save HTML Resources to Folder
  steps:
  - name: '**Basic Knowledge of C# and .NET** – Familiarity with C# programming language
      and .NET framework is essential to follow along with the examples.'
    text: '**Basic Knowledge of C# and .NET** – Familiarity with C# programming language
      and .NET framework is essential to follow along with the examples.'
  - name: '**GroupDocs.Editor for .NET Library** – Download and install GroupDocs.Editor
      for .NET library from the [website](https://releases.groupdocs.com/editor/net/).'
    text: '**GroupDocs.Editor for .NET Library** – Download and install GroupDocs.Editor
      for .NET library from the [website](https://releases.groupdocs.com/editor/net/).'
  - name: '**Development Environment** – Set up your preferred development environment
      such as Visual Studio or any other compatible IDE.'
    text: '**Development Environment** – Set up your preferred development environment
      such as Visual Studio or any other compatible IDE.'
  type: HowTo
- questions:
  - answer: Yes, it supports Excel, PowerPoint, PDF, HTML, and over 50 additional
      formats for both editing and resource extraction.
    question: Is GroupDocs.Editor compatible with other document formats besides Word?
  - answer: Absolutely. The API works seamlessly with ASP.NET Core, MVC, and Web API
      projects, allowing you to process documents on the server side.
    question: Can I integrate GroupDocs.Editor into a web application?
  - answer: Yes, it includes built‑in connectors for Google Drive, Dropbox, OneDrive,
      and Amazon S3, enabling direct loading and saving of documents in the cloud.
    question: Does GroupDocs.Editor provide cloud storage integration?
  - answer: A fully functional 30‑day trial can be downloaded from the GroupDocs website
      without any credit‑card requirement.
    question: Is there a free trial available for GroupDocs.Editor?
  - answer: You can reach the GroupDocs support team via the official forum, submit
      a ticket through the customer portal, or consult the detailed API documentation.
    question: How can I get technical support for extraction issues?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: كيفية استخراج الخطوط وحفظ موارد HTML في مجلد
type: docs
url: /ar/net/document-editing/save-html-resources-to-folder/
weight: 13
---

# كيفية استخراج الخطوط وحفظ موارد HTML في مجلد

## مقدمة
GroupDocs.Editor for .NET يتيح لك **how to extract fonts** وغيرها من الأصول من مستند أثناء تحويله إلى HTML. في بضع أسطر من C# يمكنك استخراج الصور، أوراق الأنماط، وملفات الخطوط، ثم تخزينها في مجلد تختاره. هذا البرنامج التعليمي يشرح لك سير العمل بالكامل، من تهيئة المحرر إلى حفظ كل مورد على القرص.

## إجابات سريعة
- **ماذا يعني “how to extract fonts”؟** إنها العملية التي تسترجع ملفات الخط المدمجة من المستند المصدر أثناء تحويل HTML.  
- **أي مكتبة تتعامل مع ذلك؟** GroupDocs.Editor for .NET توفر API مخصص لاستخراج الخطوط، الصور، وأوراق الأنماط.  
- **هل أحتاج إلى ترخيص؟** يتوفر نسخة تجريبية مجانية؛ يلزم الحصول على ترخيص تجاري للاستخدام في الإنتاج.  
- **ما إصدارات .NET المدعومة؟** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.  
- **هل يمكنني استهداف مجلد مخصص؟** نعم، يمكنك تحديد أي مسار قابل للكتابة عند حفظ الموارد المستخرجة.

## ما هو “how to extract fonts”؟
**How to extract fonts** تشير إلى استرجاع ملفات الخط الأصلية المدمجة في مستند مصدر (مثل DOCX، PPTX) بحيث يمكن الإشارة إليها في HTML المُولد. هذا يضمن عرض النص بدقة كما هو مقصود في المتصفحات دون الاعتماد على خطوط النظام.

## لماذا تستخدم GroupDocs.Editor لاستخراج موارد HTML؟
GroupDocs.Editor يدعم **أكثر من 50 تنسيقًا للإدخال والإخراج** — بما في ذلك DOCX، PPTX، PDF، وHTML — ويمكنه معالجة المستندات التي تصل إلى **300 صفحة** دون تحميل الملف بالكامل في الذاكرة. API الخاص به يستخرج الخطوط، الصور، وCSS في خطوة واحدة، مما يقلل وقت التطوير حتى **70 %** مقارنةً بالتحليل اليدوي.

## المتطلبات المسبقة
قبل الغوص في البرنامج التعليمي، تأكد من أن لديك المتطلبات المسبقة التالية:
1. **معرفة أساسية بـ C# و .NET** – الإلمام بلغة برمجة C# وإطار عمل .NET ضروري لمتابعة الأمثلة.  
2. **مكتبة GroupDocs.Editor for .NET** – قم بتحميل وتثبيت مكتبة GroupDocs.Editor for .NET من [الموقع الإلكتروني](https://releases.groupdocs.com/editor/net/).  
3. **بيئة التطوير** – قم بإعداد بيئة التطوير المفضلة لديك مثل Visual Studio أو أي بيئة تطوير متكاملة أخرى متوافقة.

## استيراد مساحات الأسماء
لبدء العمل، استورد مساحات الأسماء الضرورية في مشروع C# الخاص بك:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```

## كيفية استخراج الخطوط وحفظ موارد HTML في مجلد؟
حمّل المستند المصدر باستخدام `Editor editor = new Editor("sample.docx", new WordProcessingLoadOptions());` ثم استدعِ `editor.Save("output.html", SaveOptions.Html);`. بعد عملية الحفظ، تحتوي مجموعة `Resources` على جميع الأصول المستخرجة — بما في ذلك الخطوط — والتي يمكنك تكرارها وكتابتها إلى القرص. هذه الطريقة ذات الخطوة الواحدة تتعامل تلقائيًا مع كل من التحويل واستخراج الموارد.

## الخطوة 1: تهيئة GroupDocs.Editor
`Editor` هو الفئة الأساسية التي تنسق تحميل المستند، التحويل، واستخراج الموارد. تمثل جلسة مستند واحدة في الذاكرة.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
أولاً، قم بتهيئة كائن `Editor` عن طريق توفير المسار إلى المستند النموذجي الخاص بك. في هذا المثال، نستخدم مستند Word، لذا نحدد `WordProcessingLoadOptions` كنوع المستند.

## الخطوة 2: تحرير المستند
`EditableDocument` هو التمثيل القابل للتحرير الذي تُعيده طريقة `Edit`، مما يتيح لك تعديل المستند قبل الحفظ.

```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
بعد ذلك، أنشئ كائن `EditableDocument` عن طريق استدعاء طريقة `Edit` لكائن `Editor`. هذا يتيح لك إجراء عمليات تحرير على المستند.

## الخطوة 3: استخراج الموارد
`Resources` هي مجموعة تُجَمّع الأصول المستخرجة — الصور، الخطوط، وأوراق الأنماط — في قوائم منفصلة لتسهيل التعامل.

```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
استخرج الموارد مثل الصور، الخطوط، وأوراق الأنماط من المستند وخزنها في القوائم الخاصة بها.

## الخطوة 4: تحديد مجلد الإخراج
`outputFolder` هو سلسلة تحدد مكان كتابة الملفات المستخرجة. يمكنك توجيهها إلى أي دليل قابل للكتابة على الخادم أو الجهاز المحلي.

```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
حدد مجلد الإخراج حيث سيتم حفظ الموارد المستخرجة. يمكنك تخصيص مسار المجلد وفقًا لمتطلباتك.

## الخطوة 5: حفظ الموارد
`SaveResource` هي روتين مساعد يكتب موردًا ثنائيًا واحدًا (صورة، خط، أو ورقة نمط) إلى نظام الملفات.

```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
تكرار عبر كل مورد صورة، حفظه في مجلد الإخراج، وعرض المعلومات ذات الصلة مثل اسم الملف، النوع، والأبعاد.

```csharp
		foreach (FontResourceBase oneFont in fonts)
		{
			Console.WriteLine("Saving {0} of {1} type",
				oneFont.FilenameWithExtension, oneFont.Type.FormalName);
			oneFont.Save(Path.Combine(outputFolder, oneFont.FilenameWithExtension));
		}
```
وبالمثل، احفظ كل مورد خط في مجلد الإخراج.

```csharp
		foreach (CssText oneStylesheet in stylesheets)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} encoding",
				oneStylesheet.FilenameWithExtension, oneStylesheet.Type.FormalName, oneStylesheet.Encoding);
			oneStylesheet.Save(Path.Combine(outputFolder, oneStylesheet.FilenameWithExtension));
		}
	}
}
```
أخيرًا، احفظ كل ورقة نمط في مجلد الإخراج وأكمل عملية التحرير.

## المشكلات الشائعة والحلول
- **الخطوط المفقودة بعد التحويل** – تأكد من أن المستند المصدر يضم الخطوط فعليًا؛ وإلا، لا يمكن لـ GroupDocs.Editor إلا الإشارة إلى خطوط النظام.  
- **أخطاء رفض الوصول** – تحقق من أن عملية التطبيق لديها أذونات كتابة إلى مجلد الإخراج المستهدف.  
- **المستندات الكبيرة تسبب استهلاكًا عاليًا للذاكرة** – استخدم `LoadOptions` مع `LoadMode = LoadMode.Stream` لتدفق الملفات الكبيرة بدلاً من تحميلها بالكامل في الذاكرة.

## الأسئلة المتكررة
**س: هل GroupDocs.Editor متوافق مع صيغ مستندات أخرى غير Word؟**  
ج: نعم، يدعم Excel، PowerPoint، PDF، HTML، وأكثر من 50 صيغة إضافية لكل من التحرير واستخراج الموارد.

**س: هل يمكنني دمج GroupDocs.Editor في تطبيق ويب؟**  
ج: بالتأكيد. الـ API يعمل بسلاسة مع مشاريع ASP.NET Core، MVC، وWeb API، مما يتيح لك معالجة المستندات على جانب الخادم.

**س: هل يوفر GroupDocs.Editor تكاملًا مع التخزين السحابي؟**  
ج: نعم، يتضمن موصلات مدمجة لـ Google Drive، Dropbox، OneDrive، وAmazon S3، مما يتيح تحميل وحفظ المستندات مباشرةً في السحابة.

**س: هل هناك نسخة تجريبية مجانية متاحة لـ GroupDocs.Editor؟**  
ج: يمكن تنزيل نسخة تجريبية كاملة الوظائف لمدة 30 يومًا من موقع GroupDocs دون الحاجة إلى بطاقة ائتمان.

**س: كيف يمكنني الحصول على دعم فني لمشكلات الاستخراج؟**  
ج: يمكنك التواصل مع فريق دعم GroupDocs عبر المنتدى الرسمي، أو تقديم تذكرة عبر بوابة العملاء، أو الاطلاع على وثائق الـ API التفصيلية.

---

**آخر تحديث:** 2026-05-12  
**تم الاختبار مع:** GroupDocs.Editor 23.11 for .NET  
**المؤلف:** GroupDocs

## دروس ذات صلة

- [تحرير المستندات بكفاءة باستخدام GroupDocs.Editor .NET: تحويل HTML إلى مستندات قابلة للتحرير](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)
- [استخراج وحفظ موارد DOCX بكفاءة باستخدام GroupDocs.Editor .NET - دليل كامل](/editor/net/document-saving/efficient-extract-save-docx-resources-groupdocs-editor-net/)
- [إتقان تحرير وتحويل المستندات باستخدام GroupDocs.Editor .NET: دليل كامل](/editor/net/document-editing/groupdocs-editor-net-mastering-document-editing/)