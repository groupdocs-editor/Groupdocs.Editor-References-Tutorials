---
title: दस्तावेज़ सहेजें
linktitle: दस्तावेज़ सहेजें
second_title: GroupDocs.Editor .NET एपीआई
description: .NET के लिए GroupDocs.Editor का उपयोग करके दस्तावेज़ों को आसानी से संपादित और सहेजें। यह चरण-दर-चरण मार्गदर्शिका डेवलपर्स के लिए प्रक्रिया को सरल बनाती है।
weight: 14
url: /hi/net/document-editing/save-document/
---

# दस्तावेज़ सहेजें

## परिचय
क्या आप .NET के लिए GroupDocs.Editor का उपयोग करके दस्तावेज़ों को आसानी से संपादित और सहेजना चाहते हैं? आप सही जगह पर हैं! यह ट्यूटोरियल आपको चरण-दर-चरण प्रक्रिया के माध्यम से मार्गदर्शन करेगा, यह सुनिश्चित करते हुए कि आप अपने दस्तावेज़ों को आसानी से प्रबंधित कर सकते हैं। चाहे आप एक अनुभवी डेवलपर हों या शुरुआती, हमारा गाइड आपको आरंभ करने के लिए आवश्यक सभी जानकारी प्रदान करेगा।
## आवश्यक शर्तें
ट्यूटोरियल में शामिल होने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित पूर्वापेक्षाएँ मौजूद हैं:
- विकास वातावरण: आपके मशीन पर स्थापित विजुअल स्टूडियो.
- .NET फ्रेमवर्क: सुनिश्चित करें कि आपके पास .NET फ्रेमवर्क 4.6.1 या बाद का संस्करण है।
-  .NET के लिए GroupDocs.Editor: नवीनतम संस्करण डाउनलोड करें[यहाँ](https://releases.groupdocs.com/editor/net/).
- बुनियादी C# ज्ञान: C# प्रोग्रामिंग से परिचित होना आवश्यक है।
## नामस्थान आयात करें
अपने .NET प्रोजेक्ट में GroupDocs.Editor का उपयोग करने के लिए, आपको आवश्यक नामस्थान आयात करने होंगे। आप इसे इस प्रकार कर सकते हैं:
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
अब जबकि हमने अपना वातावरण सेट कर लिया है और आवश्यक नामस्थान आयात कर लिए हैं, तो चलिए .NET के लिए GroupDocs.Editor का उपयोग करके दस्तावेज़ को लोड करने, संपादित करने और सहेजने के लिए आवश्यक चरणों में गोता लगाते हैं।
## चरण 1: दस्तावेज़ लोड करें
सबसे पहले, हमें उस दस्तावेज़ को लोड करना होगा जिसे हम संपादित करना चाहते हैं। GroupDocs.Editor इस प्रक्रिया को सरल बनाता है। यहाँ बताया गया है कि आप इसे कैसे कर सकते हैं:

```csharp
string inputFilePath = "Your Sample Document";
Editor editor = new Editor(inputFilePath, delegate { return new Options.WordProcessingLoadOptions(); });
EditableDocument defaultWordProcessingDoc = editor.Edit();
```
 इस चरण में, हम उस दस्तावेज़ का पथ निर्दिष्ट करते हैं जिसे हम संपादित करना चाहते हैं और उसका एक उदाहरण बनाते हैं`Editor` वर्ग.`Edit` फिर दस्तावेज़ को लोड करने के लिए विधि को बुलाया जाता है`EditableDocument` वस्तु।
## चरण 2: दस्तावेज़ को संशोधित करें
दस्तावेज़ लोड होने के बाद, कुछ संशोधन करने का समय आ गया है। चूँकि हमारे पास WYSIWYG संपादक नहीं है, इसलिए हम संपादन प्रक्रिया को कोड में सिम्युलेट करेंगे।

```csharp
string allEmbeddedInsideString = defaultWordProcessingDoc.GetEmbeddedHtml();
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
EditableDocument editedDoc = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```
 यहां, हम दस्तावेज़ की एम्बेडेड HTML सामग्री को पुनः प्राप्त करते हैं, एक सरल पाठ प्रतिस्थापन करते हैं, और एक नया दस्तावेज़ बनाते हैं।`EditableDocument`संशोधित HTML से उदाहरण.
## चरण 3: दस्तावेज़ सहेजें
दस्तावेज़ को संपादित करने के बाद, अंतिम चरण उसे सहेजना है। GroupDocs.Editor दस्तावेज़ को विभिन्न प्रारूपों में सहेजने के लिए कई विकल्प प्रदान करता है।
## RTF के रूप में सहेजें
```csharp
string outputRtfPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.rtf");
WordProcessingSaveOptions rtfSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
editor.Save(editedDoc, outputRtfPath, rtfSaveOptions);
```
## DOCM के रूप में सहेजें
```csharp
string outputDocmPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.docm");
WordProcessingSaveOptions docmSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm);
using (FileStream outputStream = File.Create(outputDocmPath))
{
    editor.Save(editedDoc, outputStream, docmSaveOptions);
}
```
## सादे पाठ के रूप में सहेजें
```csharp
string outputTxtPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.txt");
TextSaveOptions textSaveOptions = new TextSaveOptions
{
    Encoding = System.Text.Encoding.UTF8,
    PreserveTableLayout = true
};
editor.Save(editedDoc, outputTxtPath, textSaveOptions);
```
## चरण 4: सफ़ाई
 अंत में, इसका निपटान करना महत्वपूर्ण है`EditableDocument` और`Editor` संसाधनों को मुक्त करने के लिए उदाहरण।
```csharp
editedDoc.Dispose();
defaultWordProcessingDoc.Dispose();
editor.Dispose();
```
इन चरणों का पालन करके, आप GroupDocs.Editor for .NET का उपयोग करके दस्तावेज़ों को कुशलतापूर्वक लोड, संपादित और सहेज सकते हैं। यह शक्तिशाली उपकरण लचीलापन और उपयोग में आसानी प्रदान करता है, जिससे दस्तावेज़ प्रबंधन आसान हो जाता है।
## निष्कर्ष
.NET के लिए GroupDocs.Editor के साथ प्रोग्रामेटिक रूप से दस्तावेज़ों को संपादित करना और सहेजना पहले से कहीं ज़्यादा आसान है। यह गाइड आपको दस्तावेज़ लोड करने से लेकर उसे विभिन्न फ़ॉर्मेट में सहेजने तक की पूरी प्रक्रिया से गुज़ारती है। GroupDocs.Editor के साथ, आपके पास अपनी उंगलियों पर एक बहुमुखी और मज़बूत समाधान है, जो दस्तावेज़ संपादन प्रक्रिया को सरल बनाता है।
## अक्सर पूछे जाने वाले प्रश्न
### GroupDocs.Editor किस फ़ाइल स्वरूप का समर्थन करता है?
GroupDocs.Editor विभिन्न फ़ाइल स्वरूपों का समर्थन करता है, जिसमें DOCX, RTF, TXT और कई अन्य शामिल हैं। पूरी सूची के लिए, देखें[प्रलेखन](https://tutorials.groupdocs.com/editor/net/).
### क्या मैं खरीदने से पहले GroupDocs.Editor आज़मा सकता हूँ?
 हाँ, आप प्राप्त कर सकते हैं[मुफ्त परीक्षण](https://releases.groupdocs.com/) GroupDocs.Editor की सुविधाओं का परीक्षण करने के लिए।
### यदि मुझे कोई समस्या आए तो क्या कोई सहायता उपलब्ध है?
 बिल्कुल! आप यहां आ सकते हैं[सहयता मंच](https://forum.groupdocs.com/c/editor/20) किसी भी समस्या के लिए सहायता हेतु हमसे संपर्क करें।
### मैं अस्थायी लाइसेंस कैसे प्राप्त कर सकता हूँ?
 आप अनुरोध कर सकते हैं[अस्थायी लाइसेंस](https://purchase.groupdocs.com/temporary-license/) मूल्यांकन प्रयोजनों के लिए।
### मैं GroupDocs.Editor का पूर्ण संस्करण कहां से खरीद सकता हूं?
 आप पूर्ण संस्करण खरीद सकते हैं[यहाँ](https://purchase.groupdocs.com/buy).