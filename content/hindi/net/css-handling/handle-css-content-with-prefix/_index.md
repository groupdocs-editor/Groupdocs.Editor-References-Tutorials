---
date: 2026-09-26
description: इस विस्तृत चरण‑दर‑चरण ट्यूटोरियल में GroupDocs.Editor for .NET का उपयोग
  करके css प्रीफ़िक्स को संभालना और css कंटेंट निकालना सीखें।
keywords:
- handle css prefix
- extract css content
- edit document css
- prepend url to css
lastmod: 2026-09-26
linktitle: प्रीफ़िक्स के साथ CSS कंटेंट को संभालें
og_description: GroupDocs.Editor for .NET के साथ css प्रीफ़िक्स को संभालना और css
  कंटेंट निकालना जानें। CSS संसाधनों में URLs जोड़ने और स्टाइलशीट्स प्राप्त करने के
  लिए चरण‑दर‑चरण गाइड का पालन करें।
og_image_alt: Developer guide showing css prefix handling with GroupDocs.Editor for
  .NET
og_title: GroupDocs.Editor for .NET में css प्रीफ़िक्स को कैसे संभालें
schemas:
- author: GroupDocs
  dateModified: '2026-09-26'
  description: Learn how to handle css prefix and extract css content using GroupDocs.Editor
    for .NET in this detailed step‑by‑step tutorial.
  headline: How to handle css prefix in GroupDocs.Editor for .NET
  type: TechArticle
- questions:
  - answer: Yes, GroupDocs.Editor for .NET supports PDF, Word, Excel, PowerPoint,
      and many other formats.
    question: Can I use GroupDocs.Editor for .NET with other document formats?
  - answer: Absolutely! You can start your free trial on the [GroupDocs free trial
      page](https://releases.groupdocs.com/).
    question: Is there a free trial available for GroupDocs.Editor for .NET?
  - answer: You can obtain a temporary license from the [temporary license page](https://purchase.groupdocs.com/temporary-license/).
    question: How do I get a temporary license for GroupDocs.Editor for .NET?
  - answer: Detailed documentation is available on the [GroupDocs.Editor for .NET
      documentation site](https://tutorials.groupdocs.com/editor/net/).
    question: Where can I find detailed documentation for GroupDocs.Editor for .NET?
  - answer: You can get support through the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).
    question: What support options are available for GroupDocs.Editor for .NET?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
tags:
- css handling
- GroupDocs.Editor
- .NET document processing
- css prefix
- api tutorial
title: GroupDocs.Editor for .NET में css प्रीफ़िक्स को कैसे संभालें
type: docs
url: /hi/net/css-handling/handle-css-content-with-prefix/
weight: 11
---

# GroupDocs.Editor for .NET में css प्रीफ़िक्स को कैसे संभालें

इस ट्यूटोरियल में आप GroupDocs.Editor for .NET का उपयोग करके दस्तावेज़ के भीतर स्टाइलशीट्स के साथ काम करते समय **css प्रीफ़िक्स को कैसे संभालें** सीखेंगे। चाहे आपको इमेज, फ़ॉन्ट या किसी भी बाहरी संसाधन के लिए URL को प्रीफ़िक्स करना हो, नीचे दिए गए चरण आपको बिल्कुल दिखाएंगे कि **css प्रीफ़िक्स को कैसे संभालें** और साथ ही **css कंटेंट को कैसे निकालें** आगे की प्रोसेसिंग के लिए। गाइड के अंत तक आप संसाधन पथों को पुनः लिख सकेंगे, कच्चे CSS स्ट्रिंग्स को प्राप्त कर सकेंगे, और उन्हें अपने वेब वर्कफ़्लो में आत्मविश्वास के साथ एकीकृत कर सकेंगे।

## त्वरित उत्तर
- **handle css प्रीफ़िक्स का क्या मतलब है?** CSS में संदर्भित बाहरी संसाधनों के लिए एक कस्टम URL प्रीफ़िक्स जोड़ना।  
- **CSS स्टाइल्स लौटाने वाला कौन सा API मेथड है?** `EditableDocument.GetCssContent(...)`.  
- **क्या मुझे लाइसेंस चाहिए?** एक ट्रायल लाइसेंस उपलब्ध है; प्रोडक्शन के लिए एक कमर्शियल लाइसेंस आवश्यक है।  
- **कौन से .NET संस्करण समर्थित हैं?** .NET Framework 4.5+ और .NET Core/5/6।  
- **क्या मैं रनटाइम पर प्रीफ़िक्स बदल सकता हूँ?** हाँ – बस एक अलग स्ट्रिंग `GetCssContent` को पास करें।

## handle css प्रीफ़िक्स क्या है?
यह शब्द CSS फ़ाइल के भीतर इमेज, फ़ॉन्ट या किसी भी बाहरी एसेट के URL को पुनः लिखने को दर्शाता है ताकि वे आपके नियंत्रण में किसी स्थान, जैसे CDN या सुरक्षित सर्वर, की ओर संकेत करें। एक समान बेस URL को प्रीफ़िक्स करके आप सुनिश्चित करते हैं कि दस्तावेज़ ब्राउज़र या वेब‑आधारित व्यूअर में रेंडर होने पर हर संसाधन सही ढंग से लोड हो।

## css कंटेंट निकालने के लिए GroupDocs.Editor का उपयोग क्यों करें?
GroupDocs.Editor WordProcessing दस्तावेज़ों में एम्बेडेड मूल CSS को पढ़ सकता है, कच्चे स्टाइलशीट स्ट्रिंग्स को लौटाता है, और आपको उन्हें रेंडर या सेव करने से पहले संशोधित करने देता है। इससे मैन्युअल पार्सिंग समाप्त होती है, दस्तावेज़ की आंतरिक प्रतिनिधित्व की सटीकता सुनिश्चित होती है, और **30+ फ़ाइल फ़ॉर्मेट** को सपोर्ट करता है जबकि फ़ाइलों को **500 MB** तक प्रोसेस करता है बिना पूरी फ़ाइल को मेमोरी में लोड किए।

## पूर्वापेक्षाएँ
शुरू करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित पूर्वापेक्षाएँ मौजूद हैं:
- Visual Studio: आपको Visual Studio की कार्यशील इंस्टॉलेशन चाहिए।  
- .NET Framework: सुनिश्चित करें कि आपके पास .NET Framework इंस्टॉल है।  
- GroupDocs.Editor for .NET: आप इसे [GroupDocs.Editor for .NET download page](https://releases.groupdocs.com/editor/net/) से डाउनलोड कर सकते हैं।  
- Sample Document: संपादन के लिए एक नमूना दस्तावेज़ तैयार रखें।

## नेमस्पेस इम्पोर्ट करें
पहले, आवश्यक नेमस्पेस इम्पोर्ट करें ताकि हमारा कोड सुचारू रूप से चले। यह चरण हमें GroupDocs.Editor की कोर क्लासेज़ तक पहुंच देता है।

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Editor.Options;
```

## चरण 1: Editor को इनिशियलाइज़ करें
`Editor` क्लास GroupDocs.Editor में दस्तावेज़ों के साथ काम करने का एंट्री पॉइंट है। यह लोडिंग, एडिटिंग और सेविंग ऑपरेशन्स को मैनेज करता है।  
पहला चरण आपके नमूना दस्तावेज़ के साथ एक `Editor` इंस्टेंस बनाना है। यह एडिटिंग वातावरण सेट करता है।

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```

## चरण 2: दस्तावेज़ को एडिट करें
`EditableDocument` ऑब्जेक्ट फ़ाइल के एडिटेबल संस्करण को दर्शाता है और इसके आंतरिक भागों, जैसे CSS, इमेज, और HTML को एक्सपोज़ करता है।  
अगला, हम एक `EditableDocument` ऑब्जेक्ट प्राप्त करते हैं। यह ऑब्जेक्ट हमें दस्तावेज़ के आंतरिक CSS के साथ काम करने देता है।

```csharp
    using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
    {
```

## चरण 3: बाहरी प्रीफ़िक्स सेट करें
इमेज और फ़ॉन्ट के लिए URL प्रीफ़िक्स परिभाषित करें। ये प्रीफ़िक्स CSS में मिलने वाले प्रत्येक इमेज और फ़ॉन्ट रेफ़रेंस के आगे जोड़े जाएंगे।

```csharp
        string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
        string externalFontsPrefix = "http://www.mywebsite.com/fonts/id=";
```

## चरण 4: प्रीफ़िक्स के साथ css कंटेंट निकालें
`GetCssContent` CSS स्टाइलशीट स्ट्रिंग्स का संग्रह लौटाता है जिसमें पहले से ही आपके द्वारा प्रदान किए गए प्रीफ़िक्स्ड URL शामिल होते हैं।  
`GetCssContent` को कॉल करें, और आपने जो प्रीफ़िक्स अभी परिभाषित किए हैं उन्हें पास करें। यह मेथड CSS स्टाइलशीट स्ट्रिंग्स की एक सूची लौटाता है जिसमें पहले से ही प्रीफ़िक्स्ड URL होते हैं।

```csharp
        List<string> stylesheets = document.GetCssContent(externalImagesPrefix, externalFontsPrefix);
```

## चरण 5: परिणाम आउटपुट करें
पाए गए स्टाइलशीट्स की संख्या प्रिंट करें और प्रत्येक स्टाइलशीट को दिखाएँ। यह आपको यह सत्यापित करने में मदद करता है कि प्रीफ़िक्स सही ढंग से लागू हुए हैं।

```csharp
        Console.WriteLine("There are {0} stylesheets in the input document", stylesheets.Count);
        foreach (string css in stylesheets)
        {
            Console.WriteLine(css);
        }
    }
}
```

## सामान्य समस्याएँ और समाधान
- **कोई स्टाइलशीट नहीं मिली** – सुनिश्चित करें कि स्रोत दस्तावेज़ में वास्तव में CSS है (जैसे, स्टाइल्ड टेबल्स या एम्बेडेड HTML वाला Word दस्तावेज़)।  
- **गलत URL** – दोबारा जांचें कि प्रीफ़िक्स स्ट्रिंग्स आपके सर्वर रूटिंग के लिए उपयुक्त डिलिमिटर (`/` या `=`) पर समाप्त होती हैं।  
- **परफॉर्मेंस संबंधी चिंताएँ** – बहुत बड़े दस्तावेज़ों के लिए, मेमोरी उपयोग को कम रखने के लिए स्टाइलशीट्स को बैच में प्रोसेस करने पर विचार करें।

## अक्सर पूछे जाने वाले प्रश्न

**Q: क्या मैं GroupDocs.Editor for .NET को अन्य दस्तावेज़ फ़ॉर्मेट्स के साथ उपयोग कर सकता हूँ?**  
A: हाँ, GroupDocs.Editor for .NET PDF, Word, Excel, PowerPoint, और कई अन्य फ़ॉर्मेट्स को सपोर्ट करता है।

**Q: क्या GroupDocs.Editor for .NET के लिए कोई फ्री ट्रायल उपलब्ध है?**  
A: बिल्कुल! आप [GroupDocs free trial page](https://releases.groupdocs.com/) पर अपना फ्री ट्रायल शुरू कर सकते हैं।

**Q: GroupDocs.Editor for .NET के लिए अस्थायी लाइसेंस कैसे प्राप्त करें?**  
A: आप [temporary license page](https://purchase.groupdocs.com/temporary-license/) से अस्थायी लाइसेंस प्राप्त कर सकते हैं।

**Q: GroupDocs.Editor for .NET की विस्तृत दस्तावेज़ीकरण कहाँ मिल सकता है?**  
A: विस्तृत दस्तावेज़ीकरण [GroupDocs.Editor for .NET documentation site](https://tutorials.groupdocs.com/editor/net/) पर उपलब्ध है।

**Q: GroupDocs.Editor for .NET के लिए कौन से सपोर्ट विकल्प उपलब्ध हैं?**  
A: आप [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20) के माध्यम से सपोर्ट प्राप्त कर सकते हैं।

## अतिरिक्त अक्सर पूछे जाने वाले प्रश्न

**Q: CSS निकालने के बाद क्या मैं प्रीफ़िक्स बदल सकता हूँ?**  
A: हाँ। `GetCssContent` को फिर से एक अलग प्रीफ़िक्स स्ट्रिंग के साथ कॉल करें; मेथड हमेशा रनटाइम पर पास किए गए मानों का उपयोग करता है।

**Q: क्या यह पासवर्ड‑प्रोटेक्टेड दस्तावेज़ों के साथ काम करता है?**  
A: हाँ। `Editor` इंस्टेंस बनाते समय `WordProcessingLoadOptions` में पासवर्ड प्रदान करें।

**Q: क्या संशोधित CSS को दस्तावेज़ में वापस सेव करना संभव है?**  
A: GroupDocs.Editor वर्तमान में CSS तक केवल रीड‑ओनली एक्सेस प्रदान करता है। बदलावों को स्थायी करने के लिए आपको मूल स्टाइलशीट को दस्तावेज़ के अंतर्निहित XML API का उपयोग करके बदलना होगा।

---

**अंतिम अपडेट:** 2026-09-26  
**परीक्षित संस्करण:** GroupDocs.Editor 23.12 for .NET  
**लेखक:** GroupDocs

## संबंधित ट्यूटोरियल्स

- [GroupDocs.Editor .NET का उपयोग करके वर्ड डॉक्यूमेंट्स से बाहरी CSS निकालें: एक व्यापक गाइड](/editor/net/html-web-documents/extract-external-css-word-docs-groupdocs-editor-dotnet/)
- [GroupDocs.Editor .NET का उपयोग करके वर्ड डॉक्यूमेंट्स से HTML निकालें और प्रीफ़िक्स करें](/editor/net/html-web-documents/groupdocs-editor-dotnet-extract-prefix-html-word-docs/)
- [GroupDocs.Editor .NET का उपयोग करके वर्ड डॉक्यूमेंट्स में HTML कंटेंट को निकालना और संशोधित करना कैसे करें](/editor/net/html-web-documents/extract-modify-html-content-word-docs-groupdocs-editor-net/)