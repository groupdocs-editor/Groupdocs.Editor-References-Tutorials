---
title: HTML संसाधनों को फ़ोल्डर में सहेजें
linktitle: HTML संसाधनों को फ़ोल्डर में सहेजें
second_title: GroupDocs.Editor .NET एपीआई
description: .NET के लिए Groupdocs.Editor का उपयोग करके दस्तावेज़ों से HTML संसाधन निकालने का तरीका जानें। यह व्यापक ट्यूटोरियल डेवलपर्स के लिए चरण-दर-चरण मार्गदर्शन प्रदान करता है।
weight: 13
url: /hi/net/document-editing/save-html-resources-to-folder/
type: docs
---
# HTML संसाधनों को फ़ोल्डर में सहेजें

## परिचय
.NET के लिए Groupdocs.Editor एक शक्तिशाली उपकरण है जो डेवलपर्स को उनके .NET अनुप्रयोगों के भीतर दस्तावेजों को सहजता से हेरफेर करने और परिवर्तित करने में सक्षम बनाता है। चाहे आपको किसी दस्तावेज़ से HTML संसाधन निकालने की आवश्यकता हो या उन्नत संपादन कार्य करने हों, Groupdocs.Editor अपने सहज API और व्यापक दस्तावेज़ीकरण के साथ प्रक्रिया को सरल बनाता है।
## आवश्यक शर्तें
ट्यूटोरियल में शामिल होने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित पूर्वापेक्षाएँ हैं:
1. C# और .NET का बुनियादी ज्ञान: उदाहरणों के साथ-साथ C# प्रोग्रामिंग भाषा और .NET फ्रेमवर्क से परिचित होना आवश्यक है।
2.  .NET लाइब्रेरी के लिए Groupdocs.Editor: .NET लाइब्रेरी के लिए Groupdocs.Editor को डाउनलोड और इंस्टॉल करें[वेबसाइट](https://releases.groupdocs.com/editor/net/).
3. विकास परिवेश: अपना पसंदीदा विकास परिवेश सेट करें जैसे कि विजुअल स्टूडियो या कोई अन्य संगत IDE.

## नामस्थान आयात करें
आरंभ करने के लिए, अपने C# प्रोजेक्ट में आवश्यक नामस्थान आयात करें:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```
##अब, आइए .NET के लिए Groupdocs.Editor का उपयोग करके HTML संसाधनों को फ़ोल्डर में सहेजने की प्रक्रिया को कई चरणों में विभाजित करें:
## चरण 1: Groupdocs.Editor को आरंभ करें
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
 सबसे पहले, आरंभ करें`Editor`अपने सैंपल डॉक्यूमेंट का पथ प्रदान करके ऑब्जेक्ट को चुनें। इस उदाहरण में, हम एक वर्ड डॉक्यूमेंट का उपयोग कर रहे हैं, इसलिए हम निर्दिष्ट करते हैं`WordProcessingLoadOptions` दस्तावेज़ प्रकार के रूप में.
## चरण 2: दस्तावेज़ संपादित करें
```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
 इसके बाद, एक बनाएं`EditableDocument` ऑब्जेक्ट को कॉल करके`Edit` की विधि`Editor` यह आपको दस्तावेज़ पर संपादन कार्य करने की अनुमति देता है।
## चरण 3: संसाधन निकालें
```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
दस्तावेज़ से छवियाँ, फ़ॉन्ट और स्टाइलशीट जैसे संसाधन निकालें और उन्हें संबंधित सूचियों में संग्रहीत करें।
## चरण 4: आउटपुट फ़ोल्डर निर्दिष्ट करें
```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
आउटपुट फ़ोल्डर को परिभाषित करें जहाँ निकाले गए संसाधन सहेजे जाएँगे। आप अपनी आवश्यकता के अनुसार फ़ोल्डर पथ को अनुकूलित कर सकते हैं।
## चरण 5: संसाधन बचाएँ
```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
प्रत्येक छवि संसाधन को लूप करें, उसे आउटपुट फ़ोल्डर में सहेजें, तथा फ़ाइल नाम, प्रकार और आयाम जैसी प्रासंगिक जानकारी प्रदर्शित करें।
```csharp
		foreach (FontResourceBase oneFont in fonts)
		{
			Console.WriteLine("Saving {0} of {1} type",
				oneFont.FilenameWithExtension, oneFont.Type.FormalName);
			oneFont.Save(Path.Combine(outputFolder, oneFont.FilenameWithExtension));
		}
```
इसी प्रकार, प्रत्येक फ़ॉन्ट संसाधन को आउटपुट फ़ोल्डर में सहेजें।
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
अंत में, प्रत्येक स्टाइलशीट को आउटपुट फ़ोल्डर में सहेजें और संपादन प्रक्रिया पूरी करें।

## निष्कर्ष
निष्कर्ष में, .NET के लिए Groupdocs.Editor .NET अनुप्रयोगों के भीतर प्रोग्रामेटिक रूप से दस्तावेज़ों को प्रबंधित करने और हेरफेर करने के लिए एक सुविधाजनक समाधान प्रदान करता है। इस ट्यूटोरियल का पालन करके, आप आसानी से दस्तावेज़ों से HTML संसाधन निकाल सकते हैं और अपनी विशिष्ट आवश्यकताओं के अनुसार प्रक्रिया को अनुकूलित कर सकते हैं।
## अक्सर पूछे जाने वाले प्रश्न
### क्या Groupdocs.Editor Word के अलावा अन्य दस्तावेज़ प्रारूपों के साथ संगत है?
हां, Groupdocs.Editor एक्सेल, पावरपॉइंट, पीडीएफ, और अधिक सहित दस्तावेज़ प्रारूपों की एक विस्तृत श्रृंखला का समर्थन करता है।
### क्या मैं Groupdocs.Editor को अपने वेब एप्लिकेशन में एकीकृत कर सकता हूँ?
बिल्कुल, Groupdocs.Editor .NET फ्रेमवर्क पर विकसित वेब अनुप्रयोगों के साथ सहज एकीकरण प्रदान करता है।
### क्या Groupdocs.Editor क्लाउड स्टोरेज सेवाओं के लिए समर्थन प्रदान करता है?
हां, Groupdocs.Editor लोकप्रिय क्लाउड स्टोरेज सेवाओं जैसे गूगल ड्राइव, ड्रॉपबॉक्स और माइक्रोसॉफ्ट वनड्राइव के साथ एकीकरण का समर्थन करता है।
### क्या Groupdocs.Editor के लिए कोई निःशुल्क परीक्षण उपलब्ध है?
हां, आप वेबसाइट से Groupdocs.Editor का निःशुल्क परीक्षण प्राप्त कर सकते हैं।
### मैं Groupdocs.Editor के लिए तकनीकी सहायता कैसे प्राप्त कर सकता हूं?
तकनीकी सहायता और सामुदायिक समर्थन के लिए, आप Groupdocs.Editor फ़ोरम पर जा सकते हैं।