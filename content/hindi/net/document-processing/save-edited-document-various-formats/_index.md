---
title: संपादित दस्तावेज़ को विभिन्न प्रारूपों में सहेजें
linktitle: संपादित दस्तावेज़ को विभिन्न प्रारूपों में सहेजें
second_title: GroupDocs.Editor .NET एपीआई
description: इस व्यापक चरण-दर-चरण मार्गदर्शिका में GroupDocs.Editor for .NET का उपयोग करके संपादित दस्तावेज़ों को विभिन्न प्रारूपों में सहेजना सीखें।
weight: 11
url: /hi/net/document-processing/save-edited-document-various-formats/
---
## परिचय
क्या आप .NET के लिए GroupDocs.Editor का उपयोग करके संपादित दस्तावेज़ों को विभिन्न स्वरूपों में सहेजना चाहते हैं? आप सही जगह पर आए हैं! यह व्यापक मार्गदर्शिका आपको अपने परिवेश को सेट करने से लेकर अपने संपादित दस्तावेज़ को कई स्वरूपों में सहेजने तक की पूरी प्रक्रिया से परिचित कराएगी। आइए इसमें गोता लगाएँ और दस्तावेज़ संपादन और सहेजना आसान बनाएँ!
## आवश्यक शर्तें
शुरू करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित हैं:
1.  .NET के लिए GroupDocs.Editor - से नवीनतम संस्करण डाउनलोड करें[यहाँ](https://releases.groupdocs.com/editor/net/).
2. विकास वातावरण - विजुअल स्टूडियो या कोई अन्य .NET संगत IDE.
3. .NET फ्रेमवर्क - सुनिश्चित करें कि आपके पास .NET फ्रेमवर्क 4.6.1 या उच्चतर संस्करण स्थापित है।
4. नमूना दस्तावेज़ - कार्य करने के लिए एक नमूना वर्डप्रोसेसिंग दस्तावेज़.
5. बुनियादी C# ज्ञान - C# प्रोग्रामिंग से परिचित होना आवश्यक है।
## नामस्थान आयात करें
आरंभ करने के लिए, सुनिश्चित करें कि आपने अपने C# प्रोजेक्ट में आवश्यक नामस्थान आयात किए हैं। GroupDocs.Editor कार्यक्षमता तक पहुँचने के लिए यह महत्वपूर्ण है।
```csharp
using System;
using GroupDocs.Editor.Metadata;
```
आइए इस प्रक्रिया को प्रबंधनीय चरणों में विभाजित करें। प्रत्येक भाग को समझने के लिए सावधानीपूर्वक आगे बढ़ें।
## चरण 1: इनपुट फ़ाइल का पथ प्राप्त करें
सबसे पहले, आपको अपनी इनपुट वर्डप्रोसेसिंग फ़ाइल का पथ निर्दिष्ट करना होगा। यह फ़ाइल लोड और संपादित की जाएगी।
```csharp
string inputFilePath = "Your Sample Document";
```
## चरण 2: दस्तावेज़ के लिए लोड विकल्प बनाएँ
इसके बाद, WordProcessing दस्तावेज़ों के लिए विशिष्ट लोड विकल्प बनाएँ। ये विकल्प दस्तावेज़ को लोड करने के तरीके को अनुकूलित करने में मदद करेंगे।
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
```
## चरण 3: दस्तावेज़ को विकल्पों के साथ लोड करें
 अब, दस्तावेज़ को एक में लोड करें`Editor` निर्दिष्ट लोड विकल्पों का उपयोग करके इंस्टेंस।
```csharp
using (Editor editor = new Editor(inputFilePath, delegate { return loadOptions; }))
```
## चरण 4: संपादन विकल्प बनाएँ
दस्तावेज़ के लिए संपादन विकल्प तैयार करें। ये विकल्प यह निर्धारित करेंगे कि दस्तावेज़ को संपादन के लिए कैसे खोला जाए।
```csharp
WordProcessingEditOptions editOptions = new WordProcessingEditOptions();
```
## चरण 5: संपादन के लिए दस्तावेज़ खोलें
 बनाकर संपादन के लिए दस्तावेज़ खोलें`EditableDocument`यह इंस्टेंस आपको दस्तावेज़ में परिवर्तन करने की अनुमति देगा।
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
```
## चरण 6: दस्तावेज़ सामग्री संपादित करें
अब दस्तावेज़ की सामग्री को संपादित करने का समय आ गया है। सबसे पहले, दस्तावेज़ को एकल बेस64-एन्कोडेड स्ट्रिंग के रूप में प्राप्त करें।
```csharp
string allEmbeddedInsideString = beforeEdit.GetEmbeddedHtml();
```
उदाहरण के लिए, आइए दस्तावेज़ में उपशीर्षक को संशोधित करें।
```csharp
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
```
## चरण 7: संपादित सामग्री से नया संपादन योग्य दस्तावेज़ बनाएँ
 कोई नया बनाएं`EditableDocument` संपादित सामग्री और संसाधनों से उदाहरण लें।
```csharp
using (EditableDocument afterEdit = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null))
```
## चरण 8: दस्तावेज़ को विभिन्न प्रारूपों में सहेजें
अंत में, सभी समर्थित वर्डप्रोसेसिंग प्रारूपों पर पुनरावृत्ति करें और संपादित दस्तावेज़ को प्रत्येक प्रारूप में सहेजें।
```csharp
foreach (WordProcessingFormats oneFormat in WordProcessingFormats.All)
{
    // सहेजने के विकल्प तैयार करें
    WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(oneFormat);
    // सेव पथ तैयार करें
    string savePath = Path.Combine("OutputDirectory", "MultipleOutFormats." + saveOptions.OutputFormat.Extension);
    // दस्तावेज़ सहेजें
    editor.Save(afterEdit, savePath, saveOptions);
}
```
## समापन संदेश
अंत में, आप एक संदेश प्रिंट कर सकते हैं जो यह सूचित करता है कि प्रक्रिया सफलतापूर्वक समाप्त हो गई है।
```csharp
Console.WriteLine("SavingEditedDocumentToAllFormats routine has successfully finished");
```
## निष्कर्ष
बधाई हो! आपने सफलतापूर्वक सीख लिया है कि .NET के लिए GroupDocs.Editor का उपयोग करके संपादित दस्तावेज़ों को विभिन्न स्वरूपों में कैसे सहेजा जाए। यह शक्तिशाली उपकरण कोड की कुछ पंक्तियों के साथ कई स्वरूपों में दस्तावेज़ों को हेरफेर करना और सहेजना आसान बनाता है। याद रखें, मुख्य चरणों में दस्तावेज़ लोड करना, सामग्री संपादित करना और इसे वांछित स्वरूपों में सहेजना शामिल है।
## अक्सर पूछे जाने वाले प्रश्न
### .NET के लिए GroupDocs.Editor क्या है?
GroupDocs.Editor for .NET एक शक्तिशाली एपीआई है जो आपको .NET अनुप्रयोगों का उपयोग करके विभिन्न प्रारूपों में दस्तावेज़ों को संपादित करने की अनुमति देता है।
### क्या मैं GroupDocs.Editor का निःशुल्क उपयोग कर सकता हूँ?
 हां, आप इसे निःशुल्क परीक्षण के साथ उपयोग कर सकते हैं। इसे डाउनलोड करें[यहाँ](https://releases.groupdocs.com/).
### GroupDocs.Editor द्वारा कौन से प्रारूप समर्थित हैं?
GroupDocs.Editor कई प्रकार के प्रारूपों का समर्थन करता है, जिसमें DOCX, PDF, HTML और कई अन्य शामिल हैं।
### मैं GroupDocs.Editor के लिए अस्थायी लाइसेंस कैसे प्राप्त करूं?
 आप अस्थायी लाइसेंस प्राप्त कर सकते हैं[यहाँ](https://purchase.groupdocs.com/temporary-license/).
### मुझे अधिक दस्तावेज और सहायता कहां मिल सकती है?
 विस्तृत दस्तावेज उपलब्ध है[यहाँ](https://tutorials.groupdocs.com/editor/net/) , और आप सहायता प्राप्त कर सकते हैं[यहाँ](https://forum.groupdocs.com/c/editor/20).