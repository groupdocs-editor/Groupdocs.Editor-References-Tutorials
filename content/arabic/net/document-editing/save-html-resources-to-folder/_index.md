---
title: حفظ موارد HTML إلى المجلد
linktitle: حفظ موارد HTML إلى المجلد
second_title: GroupDocs.Editor .NET API
description: تعرف على كيفية استخراج موارد HTML من المستندات باستخدام Groupdocs.Editor لـ .NET. يوفر هذا البرنامج التعليمي الشامل إرشادات خطوة بخطوة للمطورين.
weight: 13
url: /ar/net/document-editing/save-html-resources-to-folder/
type: docs
---
# حفظ موارد HTML إلى المجلد

## مقدمة
يعد Groupdocs.Editor for .NET أداة قوية تمكن المطورين من معالجة المستندات وتحويلها داخل تطبيقات .NET الخاصة بهم بسلاسة. سواء كنت بحاجة إلى استخراج موارد HTML من مستند أو تنفيذ مهام تحرير متقدمة، فإن Groupdocs.Editor يبسط العملية من خلال واجهة برمجة التطبيقات البديهية والوثائق الشاملة.
## المتطلبات الأساسية
قبل الغوص في البرنامج التعليمي، تأكد من أن لديك المتطلبات الأساسية التالية:
1. المعرفة الأساسية بـ C# و.NET: يعد الإلمام بلغة البرمجة C# وإطار عمل .NET ضروريًا للمتابعة مع الأمثلة.
2.  Groupdocs.Editor لمكتبة .NET: قم بتنزيل Groupdocs.Editor لمكتبة .NET وتثبيته من[موقع إلكتروني](https://releases.groupdocs.com/editor/net/).
3. بيئة التطوير: قم بإعداد بيئة التطوير المفضلة لديك مثل Visual Studio أو أي بيئة تطوير متكاملة أخرى متوافقة.

## استيراد مساحات الأسماء
للبدء، قم باستيراد مساحات الأسماء الضرورية في مشروع C# الخاص بك:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```
##الآن، دعنا نقسم عملية حفظ موارد HTML إلى مجلد باستخدام Groupdocs.Editor لـ .NET إلى خطوات متعددة:
## الخطوة 1: تهيئة Groupdocs.Editor
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
 أولاً، قم بتهيئة`Editor`الكائن عن طريق توفير المسار إلى نموذج المستند الخاص بك. في هذا المثال، نحن نستخدم مستند Word، لذلك نقوم بتحديده`WordProcessingLoadOptions` كنوع الوثيقة.
## الخطوة 2: تحرير المستند
```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
 بعد ذلك، قم بإنشاء`EditableDocument` كائن عن طريق استدعاء`Edit` طريقة`Editor` هدف. يتيح لك هذا إجراء عمليات التحرير على المستند.
## الخطوة 3: استخراج الموارد
```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
قم باستخراج الموارد مثل الصور والخطوط وأوراق الأنماط من المستند وقم بتخزينها في القوائم المعنية.
## الخطوة 4: تحديد مجلد الإخراج
```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
حدد مجلد الإخراج حيث سيتم حفظ الموارد المستخرجة. يمكنك تخصيص مسار المجلد وفقًا لمتطلباتك.
## الخطوة 5: حفظ الموارد
```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
قم بالمرور عبر كل مورد صورة، واحفظه في مجلد الإخراج، واعرض المعلومات ذات الصلة مثل اسم الملف، والنوع، والأبعاد.
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
أخيرًا، احفظ كل ورقة أنماط في مجلد الإخراج وأكمل عملية التحرير.

## خاتمة
في الختام، يوفر Groupdocs.Editor for .NET حلاً مناسبًا لإدارة المستندات ومعالجتها برمجيًا داخل تطبيقات .NET. باتباع هذا البرنامج التعليمي، يمكنك بسهولة استخراج موارد HTML من المستندات وتخصيص العملية وفقًا لمتطلباتك المحددة.
## الأسئلة الشائعة
### هل Groupdocs.Editor متوافق مع تنسيقات المستندات الأخرى إلى جانب Word؟
نعم، يدعم Groupdocs.Editor مجموعة واسعة من تنسيقات المستندات بما في ذلك Excel وPowerPoint وPDF والمزيد.
### هل يمكنني دمج Groupdocs.Editor في تطبيق الويب الخاص بي؟
بالتأكيد، يوفر Groupdocs.Editor تكاملًا سلسًا مع تطبيقات الويب التي تم تطويرها على إطار عمل .NET.
### هل يوفر Groupdocs.Editor الدعم لخدمات التخزين السحابية؟
نعم، يدعم Groupdocs.Editor التكامل مع خدمات التخزين السحابية الشائعة مثل Google Drive وDropbox وMicrosoft OneDrive.
### هل هناك نسخة تجريبية مجانية متاحة لـ Groupdocs.Editor؟
نعم، يمكنك الاستفادة من النسخة التجريبية المجانية من Groupdocs.Editor من موقع الويب.
### كيف يمكنني الحصول على الدعم الفني لـ Groupdocs.Editor؟
للحصول على المساعدة الفنية ودعم المجتمع، يمكنك زيارة منتدى Groupdocs.Editor.