---
title: दस्तावेज़ प्रारूपों के साथ कार्य करें
linktitle: दस्तावेज़ प्रारूपों के साथ कार्य करें
second_title: GroupDocs.Editor .NET एपीआई
description: .NET के लिए GroupDocs.Editor का उपयोग करके विभिन्न दस्तावेज़ स्वरूपों को प्रोग्रामेटिक रूप से संपादित करना सीखें। सहज एकीकरण के लिए उदाहरणों के साथ चरण-दर-चरण मार्गदर्शिका।
weight: 13
url: /hi/net/document-processing/work-document-formats/
type: docs
---
# दस्तावेज़ प्रारूपों के साथ कार्य करें

## परिचय
.NET के लिए GroupDocs.Editor का उपयोग करने के बारे में हमारी गहन मार्गदर्शिका में आपका स्वागत है! यदि आप एक डेवलपर हैं और अपने एप्लिकेशन को दस्तावेज़ संपादन क्षमताओं के साथ बेहतर बनाना चाहते हैं, तो आप सही जगह पर आए हैं। यह लेख आपको इस शक्तिशाली लाइब्रेरी के साथ काम करने के लिए आवश्यक सभी चीज़ों से परिचित कराएगा, जिसमें पूर्वापेक्षाओं से लेकर व्यावहारिक उदाहरण तक शामिल हैं।
## आवश्यक शर्तें
.NET के लिए GroupDocs.Editor के उदाहरणों और कार्यात्मकताओं में गोता लगाने से पहले, आपके पास कुछ पूर्व-आवश्यकताएँ होनी चाहिए:
1. .NET की बुनियादी समझ: .NET फ्रेमवर्क या .NET कोर से परिचित होना आवश्यक है।
2. विकास वातावरण: विजुअल स्टूडियो या कोई अन्य उपयुक्त .NET IDE.
3.  .NET लाइब्रेरी के लिए GroupDocs.Editor: लाइब्रेरी को यहाँ से डाउनलोड करें[ग्रुपडॉक्स ने पेज जारी किया](https://releases.groupdocs.com/editor/net/).
4.  अस्थायी लाइसेंस: प्राप्त करें[अस्थायी लाइसेंस](https://purchase.groupdocs.com/temporary-license/) पूर्ण सुविधाओं के लिए.
## नामस्थान आयात करें
.NET के लिए GroupDocs.Editor के साथ आरंभ करने के लिए, आपको अपने प्रोजेक्ट में आवश्यक नामस्थान आयात करने होंगे। इससे यह सुनिश्चित होगा कि आपके पास लाइब्रेरी द्वारा प्रदान की गई सभी कक्षाओं और विधियों तक पहुँच है।
```csharp
using System;
using GroupDocs.Editor.Options;
```

## चरण 1: दस्तावेज़ प्रारूपों के साथ कार्य करना
GroupDocs.Editor कई तरह के दस्तावेज़ प्रारूपों का समर्थन करता है। आइए देखें कि आप सभी समर्थित वर्ड प्रोसेसिंग और प्रेजेंटेशन प्रारूपों को कैसे सूचीबद्ध कर सकते हैं।
### वर्ड प्रोसेसिंग प्रारूपों की सूची बनाना
```csharp
foreach (Formats.WordProcessingFormats oneFormat in Formats.WordProcessingFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
स्पष्टीकरण:
1. प्रारूपों के माध्यम से लूप करें: हम सभी उपलब्ध वर्ड प्रोसेसिंग प्रारूपों के माध्यम से लूप करते हैं।
2. आउटपुट प्रारूप विवरण: प्रत्येक प्रारूप के लिए, हम उसका नाम और एक्सटेंशन प्रिंट करते हैं।
### लिस्टिंग प्रस्तुति प्रारूप
```csharp
foreach (Formats.PresentationFormats oneFormat in Formats.PresentationFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
स्पष्टीकरण:
1. लूप थ्रू फॉर्मेट: वर्ड प्रोसेसिंग फॉर्मेट के समान, हम सभी प्रेजेंटेशन फॉर्मेट के माध्यम से लूप करते हैं।
2. आउटपुट प्रारूप विवरण: प्रत्येक प्रारूप का नाम और एक्सटेंशन प्रिंट करें।
## चरण 2: एक्सटेंशन से प्रारूपों को पार्स करना
कभी-कभी, आपको फ़ाइल एक्सटेंशन के आधार पर प्रारूप निर्धारित करने की आवश्यकता होती है। GroupDocs.Editor इसे आसान बनाता है।
### स्प्रेडशीट प्रारूपों का पार्सिंग
```csharp
Formats.SpreadsheetFormats expectedXlsm = Formats.SpreadsheetFormats.FromExtension(".xlsm");
Console.WriteLine("Parsed Spreadsheet format is {0}", expectedXlsm.Name);
```
स्पष्टीकरण:
1. पार्स प्रारूप: हम उपयोग करते हैं`FromExtension` प्रारूप को पार्स करने की विधि`.xlsm` विस्तार।
2. आउटपुट प्रारूप: पार्स किए गए प्रारूप का नाम प्रिंट करें.
### पाठ्य प्रारूपों का पार्सिंग
```csharp
Formats.TextualFormats expectedHtml = Formats.TextualFormats.FromExtension("html");
Console.WriteLine("Parsed Textual format is {0}", expectedHtml.Name);
```
स्पष्टीकरण:
1.  पार्स प्रारूप:`FromExtension` विधि का उपयोग प्रारूप को पार्स करने के लिए किया जाता है`html` विस्तार।
2. आउटपुट प्रारूप: पार्स किए गए पाठ्य प्रारूप का नाम प्रिंट करें।
## चरण 3: दस्तावेज़ों का संपादन
अब जब हमने देखा है कि प्रारूपों के साथ कैसे काम करना है, तो आइए GroupDocs.Editor का उपयोग करके दस्तावेज़ों को संपादित करना शुरू करें।
### दस्तावेज़ लोड करना
किसी दस्तावेज़ को संपादित करने के लिए, आपको पहले उसे लोड करना होगा।
```csharp
using (Editor editor = new Editor("path/to/your/document.docx"))
{
    // आगे के चरणों को यहां कवर किया जाएगा।
}
```
स्पष्टीकरण:
1.  संपादक आरंभ करें: का एक उदाहरण बनाएँ`Editor` क्लास, आपके दस्तावेज़ का पथ प्रदान करता है.
2.  डिस्पोज़ पैटर्न: का उपयोग करें`using` यह सुनिश्चित करने के लिए कि संसाधनों का उचित तरीके से निपटान किया जाए, वक्तव्य जारी किया गया।
### सामग्री निकालना
एक बार दस्तावेज़ लोड हो जाने पर, आप संपादन के लिए इसकी सामग्री निकाल सकते हैं।
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    string content = editableDocument.GetContent();
    Console.WriteLine(content);
}
```
स्पष्टीकरण:
1.  संपादन विधि: कॉल करें`Edit` पाने की विधि`EditableDocument`.
2.  सामग्री प्राप्त करें: उपयोग करें`GetContent` दस्तावेज़ की सामग्री को स्ट्रिंग के रूप में पुनः प्राप्त करने के लिए.
3. आउटपुट सामग्री: सामग्री को कंसोल पर प्रिंट करें।
### बचत परिवर्तन
संपादन के बाद, अपने परिवर्तनों को दस्तावेज़ में वापस सहेजें.
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    // सामग्री यहाँ संशोधित करें
    SaveOptions saveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docx);
    editor.Save(editableDocument, "path/to/save/document.docx", saveOptions);
}
```
स्पष्टीकरण:
1.  संपादन विधि: कॉल करें`Edit` पाने की विधि`EditableDocument`.
2. सामग्री संशोधित करें: आवश्यकतानुसार सामग्री संशोधित करें (इस स्निपेट में नहीं दिखाया गया है).
3.  सहेजें विकल्प: बनाएँ`SaveOptions` प्रारूप निर्दिष्ट करना.
4.  दस्तावेज़ सहेजें: का उपयोग करें`Save` संपादित दस्तावेज़ को सहेजने की विधि.
## चरण 4: विभिन्न दस्तावेज़ प्रकारों के साथ कार्य करना
GroupDocs.Editor विभिन्न दस्तावेज़ प्रकारों का समर्थन करता है। उनके साथ काम करने का तरीका यहां बताया गया है:
### स्प्रेडशीट दस्तावेज़ों का संपादन
```csharp
using (Editor editor = new Editor("path/to/your/spreadsheet.xlsx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // सामग्री यहाँ संशोधित करें
        SaveOptions saveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsx);
        editor.Save(editableDocument, "path/to/save/spreadsheet.xlsx", saveOptions);
    }
}
```
स्पष्टीकरण:
1.  संपादक आरंभ करें: एक बनाएँ`Editor` एक स्प्रेडशीट के लिए उदाहरण.
2.  संपादन विधि: कॉल`Edit` पाने के लिए`EditableDocument`.
3. सामग्री प्राप्त करें: सामग्री को पुनः प्राप्त करें और प्रिंट करें।
4. सामग्री संशोधित करें: आवश्यक परिवर्तन करें.
5. सहेजें विकल्प: स्प्रेडशीट के लिए सहेजें विकल्प निर्दिष्ट करें.
6. दस्तावेज़ सहेजें: संशोधित दस्तावेज़ सहेजें.
### प्रस्तुति दस्तावेज़ों का संपादन
```csharp
using (Editor editor = new Editor("path/to/your/presentation.pptx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // सामग्री यहाँ संशोधित करें
        SaveOptions saveOptions = new PresentationSaveOptions(PresentationFormats.Pptx);
        editor.Save(editableDocument, "path/to/save/presentation.pptx", saveOptions);
    }
}
```
स्पष्टीकरण:
1.  संपादक आरंभ करें: एक बनाएँ`Editor` एक प्रस्तुति के लिए उदाहरण.
2.  संपादन विधि: कॉल`Edit` पाने के लिए`EditableDocument`.
3. सामग्री प्राप्त करें: सामग्री को पुनः प्राप्त करें और प्रिंट करें।
4. सामग्री संशोधित करें: आवश्यक परिवर्तन करें.
5. सहेजें विकल्प: प्रस्तुतियों के लिए सहेजें विकल्प निर्दिष्ट करें।
6. दस्तावेज़ सहेजें: संशोधित दस्तावेज़ सहेजें.
## निष्कर्ष
GroupDocs.Editor for .NET विभिन्न दस्तावेज़ स्वरूपों को प्रोग्रामेटिक रूप से संपादित करने का एक मज़बूत और लचीला तरीका प्रदान करता है। इस गाइड का पालन करके, आप अपने .NET अनुप्रयोगों में दस्तावेज़ संपादन कार्यक्षमताओं को कुशलतापूर्वक एकीकृत कर सकते हैं, उनकी क्षमताओं को बढ़ा सकते हैं और अपने उपयोगकर्ताओं को अधिक मूल्य प्रदान कर सकते हैं।
## अक्सर पूछे जाने वाले प्रश्न
### .NET के लिए GroupDocs.Editor क्या है?
GroupDocs.Editor for .NET एक शक्तिशाली लाइब्रेरी है जो डेवलपर्स को अपने .NET अनुप्रयोगों के भीतर प्रोग्रामेटिक रूप से विभिन्न दस्तावेज़ प्रारूपों को संपादित करने की अनुमति देती है।
### मैं .NET के लिए GroupDocs.Editor के साथ कैसे आरंभ करूं?
आपको लाइब्रेरी डाउनलोड करनी होगी, अस्थायी लाइसेंस प्राप्त करना होगा, तथा आवश्यक नेमस्पेस के साथ अपना विकास वातावरण स्थापित करना होगा।
### कौन से दस्तावेज़ प्रारूप समर्थित हैं?
GroupDocs.Editor वर्ड प्रोसेसिंग, स्प्रेडशीट, प्रेजेंटेशन और टेक्स्टुअल प्रारूपों का समर्थन करता है।
### क्या मैं GroupDocs.Editor का निःशुल्क उपयोग कर सकता हूँ?
 आप एक का उपयोग कर सकते हैं[मुफ्त परीक्षण](https://releases.groupdocs.com/) सीमित सुविधाओं के साथ या प्राप्त करें[अस्थायी लाइसेंस](https://purchase.groupdocs.com/temporary-license/) पूर्ण पहुँच के लिए.
### मुझे और अधिक संसाधन और सहायता कहां मिल सकती है?
 दौरा करना[GroupDocs.Editor दस्तावेज़ीकरण](https://tutorials.groupdocs.com/editor/net/) विस्तृत जानकारी के लिए, या उनकी जाँच करें[सहयता मंच](https://forum.groupdocs.com/c/editor/20) मदद के लिए।