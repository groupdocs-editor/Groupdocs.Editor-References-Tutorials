---
title: संपादन योग्य दस्तावेज़ों का उन्नत उपयोग
linktitle: संपादन योग्य दस्तावेज़ों का उन्नत उपयोग
second_title: GroupDocs.Editor .NET एपीआई
description: .NET के लिए GroupDocs.Editor का उन्नत उपयोग सीखें, दस्तावेज़ों से प्रोग्रामेटिक रूप से संसाधन बनाएं, संपादित करें और निकालें।
weight: 11
url: /hi/net/document-editing/advanced-usage-of-editable-documents/
type: docs
---
# संपादन योग्य दस्तावेज़ों का उन्नत उपयोग

## परिचय
यदि आप एक .NET डेवलपर हैं जो अपने दस्तावेज़ संपादन क्षमताओं को बढ़ाना चाहते हैं, तो GroupDocs.Editor for .NET टूल का एक शक्तिशाली सूट प्रदान करता है। यह व्यापक मार्गदर्शिका आपको GroupDocs.Editor का उपयोग करके संपादन योग्य दस्तावेज़ों के उन्नत उपयोग के माध्यम से ले जाएगी, यह सुनिश्चित करने के लिए प्रत्येक चरण को विस्तार से तोड़ देगी कि आप इसकी पूरी क्षमता का उपयोग कर सकते हैं।
## आवश्यक शर्तें
उन्नत कार्यक्षमताओं में उतरने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित हैं:
- आपके विकास मशीन पर Visual Studio स्थापित है।
- .NET फ्रेमवर्क GroupDocs.Editor के साथ संगत है।
-  .NET लाइब्रेरी के लिए GroupDocs.Editor. आप कर सकते हैं[यहाँ पर डाउनलोड करो](https://releases.groupdocs.com/editor/net/).
-  एक वैध GroupDocs.Editor लाइसेंस। आप प्राप्त कर सकते हैं[मुफ्त परीक्षण](https://releases.groupdocs.com/) या खरीदें[अस्थायी लाइसेंस](https://purchase.groupdocs.com/temporary-license/).
## नामस्थान आयात करें
आरंभ करने के लिए, सुनिश्चित करें कि आपने अपने .NET प्रोजेक्ट में आवश्यक नामस्थान आयात कर लिए हैं:
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
## चरण 1: संपादन योग्य दस्तावेज़ इंस्टेंस बनाना
 सबसे पहले, आपको इसका एक उदाहरण बनाना होगा`EditableDocument` किसी समर्थित प्रारूप के इनपुट दस्तावेज़ को लोड और संपादित करके।
```csharp
string inputFilePath = "YourSampleDocument.docx";
Editor editor = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```
इस चरण में, हम इनपुट दस्तावेज़ को लोड करते हैं और उसे संपादन के लिए तैयार करते हैं।
## चरण 2: दस्तावेज़ संसाधन निकालना
`EditableDocument` इसमें विभिन्न संसाधन शामिल हैं जिन्हें निकाला और हेरफेर किया जा सकता है। आइए इन्हें तोड़ते हैं:
### चरण 2.1: संपूर्ण दस्तावेज़ को HTML के रूप में निकालें
आप एक एकल स्ट्रिंग उत्पन्न कर सकते हैं जिसमें संपूर्ण दस्तावेज़ तथा उसके सभी संसाधन HTML के रूप में सन्निहित हों।
```csharp
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```
यह स्ट्रिंग काफी बड़ी होगी क्योंकि इसमें बेस64 में एनकोडेड स्टाइलशीट, छवियां और फ़ॉन्ट शामिल हैं।
### चरण 2.2: सभी छवियाँ निकालें
दस्तावेज़ से सभी छवियाँ निकालें.
```csharp
List<IImageResource> allImages = beforeEdit.Images;
```
### चरण 2.3: सभी फ़ॉन्ट निकालें
दस्तावेज़ में प्रयुक्त सभी फ़ॉन्ट निकालें.
```csharp
List<FontResourceBase> allFonts = beforeEdit.Fonts;
```
### चरण 2.4: सभी स्टाइलशीट निकालें
सभी स्टाइलशीट को पाठ्य प्रारूप में निकालें।
```csharp
List<CssText> allStylesheets = beforeEdit.Css;
```
### चरण 2.5: सभी संसाधन एकत्रित करें
सभी संसाधनों को एक कॉल में एकत्रित करें।
```csharp
List<IHtmlResource> allResources = beforeEdit.AllResources;
```
इसमें छवियाँ, फ़ॉन्ट और स्टाइलशीट शामिल हैं।
### चरण 2.6: HTML मार्कअप प्राप्त करें
एम्बेडेड संसाधनों के बिना दस्तावेज़ का HTML मार्कअप प्राप्त करें।
```csharp
string htmlMarkup = beforeEdit.GetContent();
```
## चरण 3: बाहरी लिंक समायोजित करना
कभी-कभी, आपको कस्टम रिसोर्स हैंडलर की ओर इंगित करने के लिए बाहरी लिंक को समायोजित करने की आवश्यकता होती है। इसे करने का तरीका यहां बताया गया है:
### चरण 3.1: कस्टम प्रीफ़िक्स तैयार करें
ऐसे उपसर्ग तैयार करें जो मूल बाह्य लिंक के आगे जोड़ दिए जाएं।
```csharp
string customImagesRequesthandlerUri = "http://example.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://example.com/CssHandler/id=";
string customFontsRequesthandlerUri = "http://example.com/FontsHandler/id=";
```
### चरण 3.2: प्रीफिक्स्ड HTML मार्कअप उत्पन्न करें
समायोजित लिंक के साथ HTML मार्कअप उत्पन्न करें।
```csharp
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```
### चरण 3.3: केवल बॉडी-HTML सामग्री प्राप्त करें
कुछ WYSIWYG संपादक केवल हेडर के बिना शुद्ध HTML मार्कअप को ही संभालते हैं।
```csharp
string onlyBodyContent = beforeEdit.GetBodyContent();
```
### चरण 3.4: उपसर्गित बॉडी-ओनली कंटेंट
कस्टम छवि उपसर्गों के साथ केवल मुख्य भाग की सामग्री उत्पन्न करें.
```csharp
string prefixedBodyContent = beforeEdit.GetBodyContent(customImagesRequesthandlerUri);
```
### चरण 3.5: स्टाइलशीट निकालें
दस्तावेज़ में प्रयुक्त स्टाइलशीट निकालें.
```csharp
List<string> stylesheets = beforeEdit.GetCssContent();
```
### चरण 3.6: प्रीफिक्स्ड स्टाइलशीट्स
कस्टम उपसर्गों के साथ स्टाइलशीट निकालें.
```csharp
List<string> prefixedStylesheets = beforeEdit.GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri);
```
## चरण 4: दस्तावेज़ को HTML के रूप में सहेजें
संपादित दस्तावेज़ को उसके संसाधनों सहित HTML फ़ाइल के रूप में सहेजें.
```csharp
string htmlFilePath = Path.Combine("output", Path.GetFileNameWithoutExtension(inputFilePath) + ".html");
beforeEdit.Save(htmlFilePath);
```
यह विधि स्टाइलशीट, छवियों और फ़ॉन्ट जैसे संसाधनों के लिए एक अलग निर्देशिका बनाती है।
## चरण 5: EditableDocument का निपटान
 संपादन योग्यदस्तावेज़ कार्यान्वयन`IDisposable` और यह जांचने की क्षमता प्रदान करता है कि क्या इंस्टैंस को डिस्पोज किया गया है।
```csharp
Console.WriteLine("EditableDocument is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");
```
### चरण 5.1 डिस्पोज़ इवेंट को संभालना
आप डिस्पोजिंग इवेंट की सदस्यता भी ले सकते हैं।
```csharp
EventHandler someMethod = delegate { Console.WriteLine("Disposing event was spotted!"); };
beforeEdit.Disposed += someMethod;
```
## चरण 6: HTML से संपादन योग्य दस्तावेज़ बनाना
HTML दस्तावेज़ से EditableDocument का एक उदाहरण बनाएँ।
### चरण 6.1: HTML फ़ाइल से
```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
```
### चरण 6.2: HTML मार्कअप से
```csharp
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);
```
ये उदाहरण (afterEditFromFile और afterEditFromMarkup) मूल (beforeEdit) के समान हैं।
## चरण 7: मैनुअल निपटान
अपने EditableDocument इंस्टैंस को मैन्युअल रूप से हटाएँ।
```csharp
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```
इससे संसाधनों की उचित सफाई सुनिश्चित होती है।
## निष्कर्ष
.NET के लिए GroupDocs.Editor प्रोग्रामेटिक रूप से दस्तावेज़ों को संपादित करने के लिए मज़बूत उपकरण प्रदान करता है। इस चरण-दर-चरण मार्गदर्शिका का पालन करके, आप दस्तावेज़ सामग्री, संसाधनों और आउटपुट स्वरूपों को कुशलतापूर्वक प्रबंधित कर सकते हैं। चाहे आप संसाधन एम्बेड कर रहे हों, बाहरी लिंक समायोजित कर रहे हों, या दस्तावेज़ों को HTML में परिवर्तित कर रहे हों, GroupDocs.Editor आपको उन्नत दस्तावेज़ हेरफेर के लिए आवश्यक कार्यक्षमता से लैस करता है।
## अक्सर पूछे जाने वाले प्रश्न
### GroupDocs.Editor किस प्रारूप का समर्थन करता है?
GroupDocs.Editor DOCX, XLSX, PPTX, और अधिक सहित विभिन्न प्रारूपों का समर्थन करता है।
### क्या मैं बिना लाइसेंस के GroupDocs.Editor का उपयोग कर सकता हूं?
 हाँ, आप इसका उपयोग कर सकते हैं[मुफ्त परीक्षण](https://releases.groupdocs.com/) या एक[अस्थायी लाइसेंस](https://purchase.groupdocs.com/temporary-license/).
### मैं किसी दस्तावेज़ से विशिष्ट संसाधन कैसे निकालूँ?
 आप निम्नलिखित विधियों का उपयोग करके चित्र, फ़ॉन्ट और स्टाइलशीट निकाल सकते हैं`Images`, `Fonts` , और`Css`.
### क्या HTML आउटपुट में लिंक समायोजित करना संभव है?
हां, आप छवियों, सीएसएस और फ़ॉन्ट्स के लिए कस्टम उपसर्ग निर्दिष्ट करके बाहरी लिंक को समायोजित कर सकते हैं।
### मैं संपादित दस्तावेज़ को HTML फ़ाइल के रूप में कैसे सहेजूँ?
 उपयोग`Save` की विधि`EditableDocument`दस्तावेज़ को उसके संसाधनों सहित HTML फ़ाइल के रूप में सहेजने के लिए क्लास का उपयोग करें।