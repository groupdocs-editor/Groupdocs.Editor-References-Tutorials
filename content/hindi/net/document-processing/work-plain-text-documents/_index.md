---
title: सादे पाठ दस्तावेज़ों के साथ कार्य करें
linktitle: सादे पाठ दस्तावेज़ों के साथ कार्य करें
second_title: GroupDocs.Editor .NET एपीआई
description: हमारे चरण-दर-चरण मार्गदर्शिका के साथ .NET के लिए GroupDocs.Editor का उपयोग करके सादे पाठ दस्तावेज़ों को संपादित करना सीखें। अपने .NET दस्तावेज़ संपादन प्रक्रिया को सरल बनाएं।
weight: 15
url: /hi/net/document-processing/work-plain-text-documents/
---

# सादे पाठ दस्तावेज़ों के साथ कार्य करें

## परिचय
क्या आप .NET में अपने दस्तावेज़ संपादन प्रक्रिया को सरल बनाना चाहते हैं? .NET के लिए GroupDocs.Editor से आगे न देखें! यह शक्तिशाली API आपको कई तरह के दस्तावेज़ प्रारूपों को आसानी से संपादित करने की अनुमति देता है। इस ट्यूटोरियल में, हम आपको GroupDocs.Editor for .NET का उपयोग करके सादे टेक्स्ट दस्तावेज़ों के साथ काम करने की प्रक्रिया के माध्यम से मार्गदर्शन करेंगे। अंत तक, आप एक प्रो की तरह टेक्स्ट दस्तावेज़ संपादन को संभालने के लिए सुसज्जित होंगे। गोता लगाने के लिए तैयार हैं? चलिए शुरू करते हैं!
## आवश्यक शर्तें
शुरू करने से पहले, आपको कुछ चीजें तैयार रखनी होंगी:
- .NET डेवलपमेंट एनवायरनमेंट: सुनिश्चित करें कि आपके पास एक कार्यशील .NET डेवलपमेंट एनवायरनमेंट सेट अप है। Visual Studio एक लोकप्रिय विकल्प है।
-  .NET के लिए GroupDocs.Editor: डाउनलोड करें और इंस्टॉल करें[.NET के लिए GroupDocs.Editor](https://releases.groupdocs.com/editor/net/).
- बुनियादी C# ज्ञान: C# प्रोग्रामिंग भाषा से परिचित होने से आपको उदाहरणों को समझने में मदद मिलेगी।
- टेक्स्ट एडिटर: कोई भी टेक्स्ट एडिटर काम करेगा, हालांकि विजुअल स्टूडियो कोड को इसकी विशेषताओं और उपयोग में आसानी के लिए अनुशंसित किया जाता है।
## नामस्थान आयात करें
.NET के लिए GroupDocs.Editor का उपयोग शुरू करने के लिए, आपको अपने प्रोजेक्ट में आवश्यक नामस्थान आयात करने होंगे। यह सुनिश्चित करता है कि सभी आवश्यक कक्षाएं और विधियाँ उपयोग के लिए उपलब्ध हैं।
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```
आइए इस प्रक्रिया को प्रबंधनीय चरणों में विभाजित करें। GroupDocs.Editor for .NET का उपयोग करके सादे पाठ दस्तावेज़ों को संपादित करने के प्रत्येक चरण के माध्यम से आपका मार्गदर्शन करते हुए आगे बढ़ें।
## चरण 1: इनपुट TXT फ़ाइल का पथ प्राप्त करें
सबसे पहले, आपको इनपुट TXT फ़ाइल का पथ निर्दिष्ट करना होगा। यह किसी स्थानीय फ़ाइल या फ़ाइल सामग्री वाली स्ट्रीम का पथ हो सकता है।
```csharp
string inputFilePath = "YourSampleDocument.txt";
```
## चरण 2: एक संपादक इंस्टेंस बनाएँ
 इसके बाद, इसका एक उदाहरण बनाएं`Editor` क्लास। यह क्लास दस्तावेजों को लोड करने और संपादित करने के लिए जिम्मेदार है। इस स्तर पर किसी लोड विकल्प की आवश्यकता नहीं है।
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## चरण 3: TXT संपादन विकल्प बनाएँ
अब, TXT संपादन विकल्प बनाएँ। ये विकल्प आपको यह निर्दिष्ट करने की अनुमति देते हैं कि संपादन के दौरान पाठ सामग्री को कैसे संसाधित किया जाना चाहिए।
```csharp
    TextEditOptions editOptions = new TextEditOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        RecognizeLists = true,
        LeadingSpaces = TextLeadingSpacesOptions.ConvertToIndent,
        TrailingSpaces = TextTrailingSpacesOptions.Trim
    };
```
## चरण 4: संपादन योग्य दस्तावेज़ इंस्टेंस बनाएँ
 संपादन विकल्प सेट करके, एक बनाएं`EditableDocument` यह दस्तावेज़ को संपादन योग्य प्रारूप में प्रस्तुत करता है।
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## चरण 5: दस्तावेज़ सामग्री संपादित करें
मूल पाठ सामग्री को पुनः प्राप्त करें और अपनी इच्छानुसार संपादन करें। इस उदाहरण के लिए, हम "पाठ" शब्द को "संपादित पाठ" से बदल देंगे।
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("text", "EDITED text");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## चरण 6: अपडेट की गई सामग्री के साथ संपादन योग्य दस्तावेज़ बनाएँ
 आवश्यक संपादन करने के बाद, एक नया बनाएं`EditableDocument` अद्यतन सामग्री और मूल संसाधनों के साथ।
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## चरण 7: वर्डप्रोसेसिंग सेव विकल्प बनाएँ
WordProcessing प्रारूप के लिए सहेजें विकल्प तैयार करें। यह उदाहरण DOCM प्रारूप का उपयोग करता है और लोकेल निर्दिष्ट करता है।
```csharp
    WordProcessingSaveOptions wordSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm)
    {
        Locale = System.Globalization.CultureInfo.GetCultureInfo("en-GB")
    };
```
## चरण 8: TXT सेविंग विकल्प बनाएं
इसी तरह, TXT फ़ॉर्मेट के लिए सेविंग विकल्प बनाएँ। सुनिश्चित करें कि एन्कोडिंग UTF-8 पर सेट है और टेबल लेआउट को सुरक्षित रखें।
```csharp
    TextSaveOptions txtSaveOptions = new TextSaveOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        PreserveTableLayout = true
    };
```
## चरण 9: आउटपुट पथ तैयार करें
परिणामी DOCX और TXT फ़ाइलों को सहेजने के लिए पथ तैयार करें। आउटपुट निर्देशिका और फ़ाइल नाम निर्धारित करने के लिए इनपुट फ़ाइल पथ का उपयोग करें।
```csharp
    string outputWordPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".docm");
    string outputTxtPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".txt");
```
## चरण 10: संपादित दस्तावेज़ को सहेजें
अंत में, निर्दिष्ट सहेजें विकल्पों का उपयोग करके संपादित दस्तावेज़ को DOCX और TXT दोनों प्रारूपों में सहेजें।
```csharp
    editor.Save(afterEdit, outputWordPath, wordSaveOptions);
    editor.Save(afterEdit, outputTxtPath, txtSaveOptions);
}
System.Console.WriteLine("Document editing process completed successfully!");
```
## निष्कर्ष
 बधाई हो! आपने .NET के लिए GroupDocs.Editor का उपयोग करके एक सादे टेक्स्ट दस्तावेज़ को सफलतापूर्वक संपादित किया है। यह शक्तिशाली उपकरण दस्तावेज़ संपादन को सरल बनाता है, जिससे आपके .NET अनुप्रयोगों में एकीकृत करना आसान हो जाता है। चाहे आप साधारण टेक्स्ट फ़ाइलें या जटिल दस्तावेज़ प्रारूप संभाल रहे हों, GroupDocs.Editor ने आपको कवर किया है। पर जाकर अधिक सुविधाएँ और क्षमताएँ देखें[GroupDocs.Editor दस्तावेज़ीकरण](https://tutorials.groupdocs.com/editor/net/).
## अक्सर पूछे जाने वाले प्रश्न
### GroupDocs.Editor for .NET किस फ़ाइल स्वरूप का समर्थन करता है?
 .NET के लिए GroupDocs.Editor कई तरह के फ़ाइल स्वरूपों का समर्थन करता है, जिसमें DOCX, TXT, HTML और बहुत कुछ शामिल है।[प्रलेखन](https://tutorials.groupdocs.com/editor/net/) पूरी सूची के लिए यहां क्लिक करें.
### मैं .NET के लिए GroupDocs.Editor का निःशुल्क परीक्षण कैसे प्राप्त कर सकता हूं?
 आप .NET के लिए GroupDocs.Editor का निःशुल्क परीक्षण यहाँ से डाउनलोड कर सकते हैं[विज्ञप्ति पृष्ठ](https://releases.groupdocs.com/).
### क्या मैं .NET के लिए GroupDocs.Editor का अस्थायी लाइसेंस खरीद सकता हूँ?
हां, आप अस्थायी लाइसेंस प्राप्त कर सकते हैं[ग्रुपडॉक्स खरीद पृष्ठ](https://purchase.groupdocs.com/temporary-license/).
### मुझे .NET के लिए GroupDocs.Editor का समर्थन कहां मिल सकता है?
 सहायता निम्नलिखित माध्यम से उपलब्ध है[GroupDocs.Editor सहायता मंच](https://forum.groupdocs.com/c/editor/20).
### क्या .NET के लिए GroupDocs.Editor के लिए विस्तृत दस्तावेज उपलब्ध है?
 हां, विस्तृत दस्तावेज उपलब्ध है[GroupDocs.Editor दस्तावेज़न पृष्ठ](https://tutorials.groupdocs.com/editor/net/).