---
date: 2026-05-12
description: GroupDocs.Editor for .NET का उपयोग करके दस्तावेज़ों से फ़ॉन्ट और अन्य
  HTML संसाधन निकालना सीखें। .NET डेवलपर्स के लिए चरण‑दर‑चरण मार्गदर्शिका।
keywords:
- how to extract fonts
- GroupDocs.Editor .NET
- extract HTML resources
linktitle: HTML संसाधनों को फ़ोल्डर में सहेजें
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
title: फ़ॉन्ट निकालने और HTML संसाधनों को फ़ोल्डर में सहेजने का तरीका
type: docs
url: /hi/net/document-editing/save-html-resources-to-folder/
weight: 13
---

# फ़ॉन्ट निकालने और HTML संसाधनों को फ़ोल्डर में सहेजने का तरीका

## परिचय
GroupDocs.Editor for .NET आपको **फ़ॉन्ट निकालने का तरीका** और अन्य एसेट्स को एक दस्तावेज़ से निकालने देता है जबकि इसे HTML में परिवर्तित किया जाता है। कुछ ही पंक्तियों के C# कोड में आप छवियों, स्टाइलशीट्स, और फ़ॉन्ट फ़ाइलों को निकाल सकते हैं, फिर उन्हें अपनी पसंद के फ़ोल्डर में सहेज सकते हैं। यह ट्यूटोरियल आपको सम्पूर्ण कार्यप्रवाह के माध्यम से ले जाता है, एडिटर को इनिशियलाइज़ करने से लेकर प्रत्येक संसाधन को डिस्क पर सहेजने तक।

## त्वरित उत्तर
- **“फ़ॉन्ट निकालने का तरीका” क्या है?** यह HTML रूपांतरण के दौरान स्रोत दस्तावेज़ से एम्बेडेड फ़ॉन्ट फ़ाइलों को पुनः प्राप्त करने की प्रक्रिया है।  
- **कौन‑सी लाइब्रेरी इसे संभालती है?** GroupDocs.Editor for .NET फ़ॉन्ट, छवियों और स्टाइलशीट्स को निकालने के लिए एक समर्पित API प्रदान करता है।  
- **क्या मुझे लाइसेंस चाहिए?** एक मुफ्त ट्रायल उपलब्ध है; उत्पादन उपयोग के लिए एक व्यावसायिक लाइसेंस आवश्यक है।  
- **कौन‑से .NET संस्करण समर्थित हैं?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.  
- **क्या मैं कस्टम फ़ोल्डर को लक्ष्य बना सकता हूँ?** हाँ, आप निकाले गए संसाधनों को सहेजते समय कोई भी लिखने योग्य पथ निर्दिष्ट कर सकते हैं।

## “फ़ॉन्ट निकालने का तरीका” क्या है?
**फ़ॉन्ट निकालने का तरीका** से स्रोत दस्तावेज़ (जैसे DOCX, PPTX) में एम्बेडेड मूल फ़ॉन्ट फ़ाइलों को पुनः प्राप्त करने को कहा जाता है, ताकि उत्पन्न HTML द्वारा उनका संदर्भ लिया जा सके। यह सुनिश्चित करता है कि टेक्स्ट ब्राउज़र में बिल्कुल वही दिखे जैसा कि इरादा है, बिना सिस्टम फ़ॉन्ट्स पर निर्भर हुए।

## HTML संसाधन निष्कर्षण के लिए GroupDocs.Editor का उपयोग क्यों करें?
GroupDocs.Editor **50+ इनपुट और आउटपुट फ़ॉर्मैट्स**—जिसमें DOCX, PPTX, PDF, और HTML शामिल हैं—को समर्थन देता है और **300 पृष्ठों तक** के दस्तावेज़ों को पूरी फ़ाइल को मेमोरी में लोड किए बिना प्रोसेस कर सकता है। इसका API फ़ॉन्ट, छवियों और CSS को एक ही पास में निकालता है, जिससे मैन्युअल पार्सिंग की तुलना में विकास समय **70 %** तक घट जाता है।

## पूर्वापेक्षाएँ
ट्यूटोरियल में आगे बढ़ने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित पूर्वापेक्षाएँ हैं:
1. **C# और .NET का मूलभूत ज्ञान** – C# प्रोग्रामिंग भाषा और .NET फ्रेमवर्क की परिचितता उदाहरणों के साथ आगे बढ़ने के लिए आवश्यक है।  
2. **GroupDocs.Editor for .NET लाइब्रेरी** – GroupDocs.Editor for .NET लाइब्रेरी को [website](https://releases.groupdocs.com/editor/net/) से डाउनलोड और इंस्टॉल करें।  
3. **डेवलपमेंट एनवायरनमेंट** – Visual Studio या किसी अन्य संगत IDE जैसे अपने पसंदीदा डेवलपमेंट एनवायरनमेंट को सेट अप करें।

## नेमस्पेस इम्पोर्ट करें
शुरू करने के लिए, अपने C# प्रोजेक्ट में आवश्यक नेमस्पेस इम्पोर्ट करें:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```

## फ़ॉन्ट निकालने और HTML संसाधनों को फ़ोल्डर में सहेजने का तरीका?
अपने स्रोत दस्तावेज़ को `Editor editor = new Editor("sample.docx", new WordProcessingLoadOptions());` के साथ लोड करें और फिर `editor.Save("output.html", SaveOptions.Html);` को कॉल करें। सहेजने के बाद, `Resources` संग्रह में सभी निकाले गए एसेट्स—फ़ॉन्ट सहित—शामिल होते हैं, जिन्हें आप इटररेट करके डिस्क पर लिख सकते हैं। यह एक‑स्टेप दृष्टिकोण स्वचालित रूप से रूपांतरण और संसाधन निष्कर्षण दोनों को संभालता है।

## चरण 1: GroupDocs.Editor को इनिशियलाइज़ करें
`Editor` वह कोर क्लास है जो दस्तावेज़ लोडिंग, रूपांतरण, और संसाधन निष्कर्षण को व्यवस्थित करता है। यह मेमोरी में एकल दस्तावेज़ सत्र का प्रतिनिधित्व करता है।

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
सबसे पहले, `Editor` ऑब्जेक्ट को अपने सैंपल दस्तावेज़ का पथ प्रदान करके इनिशियलाइज़ करें। इस उदाहरण में, हम एक Word दस्तावेज़ का उपयोग कर रहे हैं, इसलिए हम `WordProcessingLoadOptions` को दस्तावेज़ प्रकार के रूप में निर्दिष्ट करते हैं।

## चरण 2: दस्तावेज़ संपादित करें
`EditableDocument` वह संपादन योग्य प्रतिनिधित्व है जो `Edit` मेथड द्वारा लौटाया जाता है, जिससे आप सहेजने से पहले दस्तावेज़ को संशोधित कर सकते हैं।

```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
अगला, `Editor` ऑब्जेक्ट के `Edit` मेथड को कॉल करके एक `EditableDocument` ऑब्जेक्ट बनाएं। यह आपको दस्तावेज़ पर संपादन ऑपरेशन करने की अनुमति देता है।

## चरण 3: संसाधनों को निकालें
`Resources` एक संग्रह है जो निकाले गए एसेट्स—छवियों, फ़ॉन्ट्स, और स्टाइलशीट्स—को आसान हैंडलिंग के लिए अलग-अलग सूचियों में समूहित करता है।

```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
दस्तावेज़ से छवियों, फ़ॉन्ट्स और स्टाइलशीट्स जैसे संसाधनों को निकालें और उन्हें संबंधित सूचियों में संग्रहीत करें।

## चरण 4: आउटपुट फ़ोल्डर निर्दिष्ट करें
`outputFolder` एक स्ट्रिंग है जो निर्धारित करती है कि निकाली गई फ़ाइलें कहाँ लिखी जाएँगी। आप इसे सर्वर या स्थानीय मशीन पर किसी भी लिखने योग्य डायरेक्टरी की ओर इंगित कर सकते हैं।

```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
निकाले गए संसाधनों को सहेजने के लिए आउटपुट फ़ोल्डर को परिभाषित करें। आप अपनी आवश्यकता के अनुसार फ़ोल्डर पथ को कस्टमाइज़ कर सकते हैं।

## चरण 5: संसाधनों को सहेजें
`SaveResource` एक हेल्पर रूटीन है जो एकल बाइनरी संसाधन (छवि, फ़ॉन्ट, या स्टाइलशीट) को फ़ाइल सिस्टम में लिखता है।

```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
प्रत्येक इमेज रिसोर्स पर लूप करें, इसे आउटपुट फ़ोल्डर में सहेजें, और फ़ाइलनाम, प्रकार, और आयाम जैसी संबंधित जानकारी प्रदर्शित करें।

```csharp
		foreach (FontResourceBase oneFont in fonts)
		{
			Console.WriteLine("Saving {0} of {1} type",
				oneFont.FilenameWithExtension, oneFont.Type.FormalName);
			oneFont.Save(Path.Combine(outputFolder, oneFont.FilenameWithExtension));
		}
```
इसी प्रकार, प्रत्येक फ़ॉन्ट रिसोर्स को आउटपुट फ़ोल्डर में सहेजें।

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
अंत में, प्रत्येक स्टाइलशीट को आउटपुट फ़ोल्डर में सहेजें और संपादन प्रक्रिया को पूर्ण करें।

## सामान्य समस्याएँ और समाधान
- **रूपांतरण के बाद फ़ॉन्ट्स गायब** – सुनिश्चित करें कि स्रोत दस्तावेज़ वास्तव में फ़ॉन्ट्स को एम्बेड करता है; अन्यथा, GroupDocs.Editor केवल सिस्टम फ़ॉन्ट्स को संदर्भित कर सकता है।  
- **एक्सेस डिनाइड त्रुटियाँ** – सत्यापित करें कि एप्लिकेशन प्रक्रिया को लक्ष्य आउटपुट फ़ोल्डर पर लिखने की अनुमति है।  
- **बड़े दस्तावेज़ उच्च मेमोरी उपयोग का कारण बनते हैं** – बड़े फ़ाइलों को पूरी तरह मेमोरी में लोड करने के बजाय स्ट्रीम करने के लिए `LoadOptions` को `LoadMode = LoadMode.Stream` के साथ उपयोग करें।

## अक्सर पूछे जाने वाले प्रश्न

**प्र: क्या GroupDocs.Editor Word के अलावा अन्य दस्तावेज़ फ़ॉर्मैट्स के साथ संगत है?**  
A: हाँ, यह Excel, PowerPoint, PDF, HTML, और 50 से अधिक अतिरिक्त फ़ॉर्मैट्स को संपादन और संसाधन निष्कर्षण दोनों के लिए समर्थन देता है।

**प्र: क्या मैं GroupDocs.Editor को वेब एप्लिकेशन में इंटीग्रेट कर सकता हूँ?**  
A: बिल्कुल। API ASP.NET Core, MVC, और Web API प्रोजेक्ट्स के साथ सहजता से काम करता है, जिससे आप सर्वर साइड पर दस्तावेज़ प्रोसेस कर सकते हैं।

**प्र: क्या GroupDocs.Editor क्लाउड स्टोरेज इंटीग्रेशन प्रदान करता है?**  
A: हाँ, इसमें Google Drive, Dropbox, OneDrive, और Amazon S3 के लिए बिल्ट‑इन कनेक्टर्स शामिल हैं, जिससे क्लाउड में दस्तावेज़ों को सीधे लोड और सहेजा जा सकता है।

**प्र: क्या GroupDocs.Editor के लिए कोई मुफ्त ट्रायल उपलब्ध है?**  
A: एक पूरी तरह कार्यात्मक 30‑दिन का ट्रायल GroupDocs वेबसाइट से बिना किसी क्रेडिट‑कार्ड की आवश्यकता के डाउनलोड किया जा सकता है।

**प्र: निष्कर्षण समस्याओं के लिए तकनीकी समर्थन कैसे प्राप्त कर सकता हूँ?**  
A: आप आधिकारिक फ़ोरम के माध्यम से GroupDocs सपोर्ट टीम से संपर्क कर सकते हैं, ग्राहक पोर्टल के माध्यम से टिकट सबमिट कर सकते हैं, या विस्तृत API दस्तावेज़ीकरण देख सकते हैं।

---

**अंतिम अपडेट:** 2026-05-12  
**परीक्षित संस्करण:** GroupDocs.Editor 23.11 for .NET  
**लेखक:** GroupDocs

## संबंधित ट्यूटोरियल

- [GroupDocs.Editor .NET के साथ कुशल दस्तावेज़ संपादन: HTML को संपादन योग्य दस्तावेज़ में बदलना](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)
- [GroupDocs.Editor .NET का उपयोग करके DOCX संसाधनों को कुशलतापूर्वक निकालें और सहेजें - पूर्ण गाइड](/editor/net/document-saving/efficient-extract-save-docx-resources-groupdocs-editor-net/)
- [GroupDocs.Editor .NET के साथ दस्तावेज़ संपादन और रूपांतरण में महारत: एक पूर्ण गाइड](/editor/net/document-editing/groupdocs-editor-net-mastering-document-editing/)