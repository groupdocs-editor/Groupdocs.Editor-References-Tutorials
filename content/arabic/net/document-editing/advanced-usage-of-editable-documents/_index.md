---
title: الاستخدام المتقدم للمستندات القابلة للتحرير
linktitle: الاستخدام المتقدم للمستندات القابلة للتحرير
second_title: GroupDocs.Editor .NET API
description: تعرف على الاستخدام المتقدم لـ GroupDocs.Editor لإنشاء الموارد من المستندات وتحريرها واستخراجها من المستندات برمجيًا.
weight: 11
url: /ar/net/document-editing/advanced-usage-of-editable-documents/
---
## مقدمة
إذا كنت أحد مطوري .NET وتتطلع إلى تحسين قدرات تحرير المستندات لديك، فإن GroupDocs.Editor for .NET يقدم مجموعة قوية من الأدوات. سيرشدك هذا الدليل الشامل خلال الاستخدام المتقدم للمستندات القابلة للتحرير باستخدام GroupDocs.Editor، مع تفصيل كل خطوة بالتفصيل لضمان قدرتك على الاستفادة من إمكاناتها الكاملة.
## المتطلبات الأساسية
قبل الغوص في الوظائف المتقدمة، تأكد من أن لديك ما يلي:
- تم تثبيت Visual Studio على جهاز التطوير الخاص بك.
- .NET Framework متوافق مع GroupDocs.Editor.
-  GroupDocs.Editor لمكتبة .NET. أنت تستطيع[قم بتنزيله هنا](https://releases.groupdocs.com/editor/net/).
-  ترخيص GroupDocs.Editor صالح. يمكنك الحصول على[تجربة مجانية](https://releases.groupdocs.com/) أو شراء أ[ترخيص مؤقت](https://purchase.groupdocs.com/temporary-license/).
## استيراد مساحات الأسماء
للبدء، تأكد من استيراد مساحات الأسماء الضرورية في مشروع .NET الخاص بك:
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
## الخطوة 1: إنشاء مثيل مستند قابل للتحرير
 أولاً، تحتاج إلى إنشاء مثيل لـ`EditableDocument` عن طريق تحميل وتحرير مستند إدخال بتنسيق مدعوم.
```csharp
string inputFilePath = "YourSampleDocument.docx";
Editor editor = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```
في هذه الخطوة، نقوم بتحميل مستند الإدخال ونجهزه للتحرير.
## الخطوة 2: استخراج موارد الوثيقة
 ال`EditableDocument` يحتوي على موارد مختلفة يمكن استخراجها ومعالجتها. دعونا نحلل هذه الأمور:
### الخطوة 2.1: استخراج المستند بأكمله بصيغة HTML
يمكنك إنشاء سلسلة واحدة تحتوي على المستند بأكمله مع تضمين جميع موارده بتنسيق HTML.
```csharp
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```
ستكون هذه السلسلة كبيرة جدًا لأنها تتضمن أوراق الأنماط والصور والخطوط المشفرة في base64.
### الخطوة 2.2: استخراج جميع الصور
استخراج كافة الصور من الوثيقة.
```csharp
List<IImageResource> allImages = beforeEdit.Images;
```
### الخطوة 2.3: استخراج كافة الخطوط
استخراج كافة الخطوط المستخدمة في الوثيقة.
```csharp
List<FontResourceBase> allFonts = beforeEdit.Fonts;
```
### الخطوة 2.4: استخراج كافة أوراق الأنماط
قم باستخراج كافة أوراق الأنماط بتنسيق نصي.
```csharp
List<CssText> allStylesheets = beforeEdit.Css;
```
### الخطوة 2.5: جمع كل الموارد
جمع كل الموارد في مكالمة واحدة.
```csharp
List<IHtmlResource> allResources = beforeEdit.AllResources;
```
يتضمن ذلك الصور والخطوط وأوراق الأنماط.
### الخطوة 2.6: الحصول على ترميز HTML
احصل على ترميز HTML للمستند بدون موارد مضمنة.
```csharp
string htmlMarkup = beforeEdit.GetContent();
```
## الخطوة 3: ضبط الروابط الخارجية
في بعض الأحيان، تحتاج إلى ضبط الروابط الخارجية للإشارة إلى معالج موارد مخصص. هيريس كيفية القيام بذلك:
### الخطوة 3.1: إعداد البادئات المخصصة
قم بإعداد البادئات التي ستسبق الروابط الخارجية الأصلية.
```csharp
string customImagesRequesthandlerUri = "http://example.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://example.com/CssHandler/id=";
string customFontsRequesthandlerUri = "http://example.com/FontsHandler/id=";
```
### الخطوة 3.2: إنشاء علامة HTML مسبوقة
قم بإنشاء علامات HTML باستخدام الروابط المعدلة.
```csharp
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```
### الخطوة 3.3: الحصول على محتوى HTML للنص الأساسي فقط
يتعامل بعض محرري WYSIWYG فقط مع ترميز HTML الخالص بدون رؤوس.
```csharp
string onlyBodyContent = beforeEdit.GetBodyContent();
```
### الخطوة 3.4: محتوى النص الأساسي فقط
أنشئ محتوى نصيًا فقط ببادئات صور مخصصة.
```csharp
string prefixedBodyContent = beforeEdit.GetBodyContent(customImagesRequesthandlerUri);
```
### الخطوة 3.5: استخراج أوراق الأنماط
استخراج أوراق الأنماط المستخدمة في الوثيقة.
```csharp
List<string> stylesheets = beforeEdit.GetCssContent();
```
### الخطوة 3.6: أوراق الأنماط المسبقة
استخراج أوراق الأنماط مع البادئات المخصصة.
```csharp
List<string> prefixedStylesheets = beforeEdit.GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri);
```
## الخطوة 4: احفظ المستند بتنسيق HTML
احفظ المستند الذي تم تحريره كملف HTML، بما في ذلك موارده.
```csharp
string htmlFilePath = Path.Combine("output", Path.GetFileNameWithoutExtension(inputFilePath) + ".html");
beforeEdit.Save(htmlFilePath);
```
تقوم هذه الطريقة بإنشاء دليل منفصل للموارد مثل أوراق الأنماط والصور والخطوط.
## الخطوة 5: التخلص من EditableDocument
 تنفذ EditableDocument`IDisposable` ويوفر القدرة على التحقق مما إذا تم التخلص من المثيل.
```csharp
Console.WriteLine("EditableDocument is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");
```
### الخطوة 5.1 التعامل مع حدث التخلص
يمكنك أيضًا الاشتراك في حدث التخلص.
```csharp
EventHandler someMethod = delegate { Console.WriteLine("Disposing event was spotted!"); };
beforeEdit.Disposed += someMethod;
```
## الخطوة 6: إنشاء مستند قابل للتحرير من HTML
قم بإنشاء مثيل لـ EditableDocument من مستند HTML.
### الخطوة 6.1: من ملف HTML
```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
```
### الخطوة 6.2: من ترميز HTML
```csharp
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);
```
هذه الحالات (afterEditFromFile وafterEditFromMarkup) مطابقة للنسخة الأصلية (beforeEdit).
## الخطوة 7: التخلص اليدوي
تخلص يدويًا من مثيلات EditableDocument الخاصة بك.
```csharp
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```
وهذا يضمن التنظيف السليم للموارد.
## خاتمة
يوفر GroupDocs.Editor for .NET أدوات قوية لتحرير المستندات برمجيًا. باتباع هذا الدليل المفصّل خطوة بخطوة، يمكنك إدارة محتوى المستند والموارد وتنسيقات الإخراج بكفاءة. سواء كنت تقوم بتضمين الموارد، أو تعديل الروابط الخارجية، أو تحويل المستندات إلى HTML، فإن GroupDocs.Editor يزودك بالوظائف اللازمة لمعالجة المستندات المتقدمة.
## الأسئلة الشائعة
### ما هي التنسيقات التي يدعمها GroupDocs.Editor؟
يدعم GroupDocs.Editor العديد من التنسيقات بما في ذلك DOCX وXLSX وPPTX والمزيد.
### هل يمكنني استخدام GroupDocs.Editor بدون ترخيص؟
 نعم يمكنك استخدامه مع[تجربة مجانية](https://releases.groupdocs.com/) أو أ[ترخيص مؤقت](https://purchase.groupdocs.com/temporary-license/).
### كيف يمكنني استخراج موارد محددة من مستند؟
 يمكنك استخراج الصور والخطوط وأوراق الأنماط باستخدام الطرق المتوفرة مثل`Images`, `Fonts` ، و`Css`.
### هل من الممكن ضبط الروابط في مخرجات HTML؟
نعم، يمكنك ضبط الروابط الخارجية عن طريق تحديد بادئات مخصصة للصور وCSS والخطوط.
### كيف يمكنني حفظ مستند تم تحريره كملف HTML؟
 استخدم ال`Save` طريقة`EditableDocument`فئة لحفظ المستند كملف HTML، بما في ذلك موارده.