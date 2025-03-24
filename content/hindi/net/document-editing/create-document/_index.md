---
title: दस्तावेज़ बनाएँ
linktitle: दस्तावेज़ बनाएँ
second_title: GroupDocs.Editor .NET एपीआई
description: इस व्यापक चरण-दर-चरण ट्यूटोरियल के साथ .NET के लिए GroupDocs.Editor का उपयोग करके Word, Excel, PowerPoint, Ebook और ईमेल दस्तावेज़ों को संपादित करना सीखें।
weight: 10
url: /hi/net/document-editing/create-document/
---

# दस्तावेज़ बनाएँ

## परिचय
क्या आप प्रोग्रामेटिक रूप से विभिन्न दस्तावेज़ प्रकारों को संपादित करने में आने वाली परेशानी से थक गए हैं? .NET के लिए GroupDocs.Editor प्रक्रिया को सरल बनाने के लिए यहाँ है। यह शक्तिशाली उपकरण डेवलपर्स को Word, Excel, PowerPoint, Ebooks और Emails जैसे विभिन्न दस्तावेज़ स्वरूपों को आसानी से संपादित करने की अनुमति देता है। इस ट्यूटोरियल में, हम दस्तावेज़ बनाने और संपादित करने के लिए .NET के लिए GroupDocs.Editor का उपयोग करने के तरीके के बारे में विस्तार से जानेंगे। हम प्रक्रिया को आसान-से-अनुसरण चरणों में विभाजित करेंगे, ताकि यह तब भी सुलभ हो, जब आप इसके लिए नए हों।
## आवश्यक शर्तें
शुरू करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित हैं:
- आपके मशीन पर Visual Studio स्थापित है.
- .NET फ्रेमवर्क (4.0 या उच्चतर)।
-  .NET लाइब्रेरी के लिए GroupDocs.Editor। आप इसे यहाँ से डाउनलोड कर सकते हैं[यहाँ](https://releases.groupdocs.com/editor/net/).
- C# प्रोग्रामिंग का बुनियादी ज्ञान.
## नामस्थान आयात करें
सबसे पहले, आइए आवश्यक नेमस्पेस को आयात करें। इससे हमारे एप्लिकेशन में आवश्यक क्लासेस और मेथड्स सुलभ हो जाएंगे।
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using System.IO;
```
## चरण 1: स्ट्रीम सेट अप करना
आरंभ करने के लिए, हमें एक मेमोरी स्ट्रीम सेट अप करना होगा जो दस्तावेज़ सामग्री के लिए हमारे प्लेसहोल्डर के रूप में कार्य करेगी।
```csharp
Stream memoryStream = Stream.Null;
```
## चरण 2: दस्तावेज़ को सहेजने के लिए कॉलबैक फ़ंक्शन
इसके बाद, एक कॉलबैक फ़ंक्शन परिभाषित करें जो नए दस्तावेज़ स्ट्रीम को सहेजेगा। यह फ़ंक्शन दस्तावेज़ संपादन प्रक्रिया के आउटपुट को संभालने के लिए आवश्यक है।
```csharp
void SaveNewDocument(Stream resultStream)
{
    memoryStream = resultStream;
}
```
## चरण 3: वर्डप्रोसेसिंग दस्तावेज़ बनाना और संपादित करना
 अब, चलिए एक वर्ड डॉक्यूमेंट बनाते हैं और उसे संपादित करते हैं। हम एक नया डॉक्यूमेंट बनाकर शुरुआत करेंगे`Editor` वर्डप्रोसेसिंग दस्तावेज़ों के लिए उदाहरण बनाएँ और इसे डिफ़ॉल्ट विकल्पों के साथ संपादित करें।
### डिफ़ॉल्ट विकल्पों के साथ बनाएँ और संपादित करें
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    EditableDocument defaultWordProcessingDoc = editor.Edit();
}
```
### कस्टम विकल्पों के साथ बनाएँ और संपादित करें
अधिक नियंत्रण के लिए, हम पृष्ठांकन अक्षम करने और एम्बेडेड फ़ॉन्ट निकालने जैसे विकल्प निर्दिष्ट कर सकते हैं।
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    WordProcessingEditOptions wordProcessingEditOptions = new WordProcessingEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true,
        FontExtraction = FontExtractionOptions.ExtractAllEmbedded
    };
    EditableDocument editableWordProcessingDocument = editor.Edit(wordProcessingEditOptions);
}
```
## चरण 4: स्प्रेडशीट दस्तावेज़ बनाना और संपादित करना
इसी तरह, हम एक एक्सेल दस्तावेज़ बना और संपादित कर सकते हैं। यहाँ बताया गया है कि आप यह कैसे कर सकते हैं।
### डिफ़ॉल्ट विकल्पों के साथ बनाएँ और संपादित करें
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    EditableDocument defaultEditableSpreadsheetDocument = editor.Edit();
}
```
### कस्टम विकल्पों के साथ बनाएँ और संपादित करें
 विशिष्ट कार्यपत्रकों को लक्षित करने या छुपे हुए कार्यपत्रकों को बाहर करने के लिए, हम उपयोग करते हैं`SpreadsheetEditOptions`.
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    SpreadsheetEditOptions spreadsheetEditOptions = new SpreadsheetEditOptions
    {
        WorksheetIndex = 0,
        ExcludeHiddenWorksheets = true
    };
    EditableDocument editableSpreadsheetDocument = editor.Edit(spreadsheetEditOptions);
}
```
## चरण 5: प्रस्तुति दस्तावेज़ बनाना और संपादित करना
पावरपॉइंट प्रेजेंटेशन भी समर्थित हैं। आइए देखें कि उन्हें कैसे हैंडल किया जाए।
### डिफ़ॉल्ट विकल्पों के साथ बनाएँ और संपादित करें
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    EditableDocument defaultEditablePresentationDocument = editor.Edit();
}
```
### कस्टम विकल्पों के साथ बनाएँ और संपादित करें
आप विकल्प निर्दिष्ट करके अपने संपादन को अनुकूलित कर सकते हैं, जैसे कि कौन सी स्लाइड दिखानी है और छिपी हुई स्लाइडें शामिल करनी हैं या नहीं।
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    PresentationEditOptions presentationEditOptions = new PresentationEditOptions
    {
        ShowHiddenSlides = false,
        SlideNumber = 0
    };
    EditableDocument editablePresentationDocument = editor.Edit(presentationEditOptions);
}
```
## चरण 6: ईबुक दस्तावेज़ बनाना और संपादित करना
GroupDocs.Editor EPUB जैसे ईबुक प्रारूपों को संपादित करने की भी अनुमति देता है। यहां बताया गया है कि आप इसे कैसे संभाल सकते हैं।
### डिफ़ॉल्ट विकल्पों के साथ बनाएँ और संपादित करें
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EditableDocument defaultEditableEbookDocument = editor.Edit();
}
```
### कस्टम विकल्पों के साथ बनाएँ और संपादित करें
पृष्ठांकन और भाषा संबंधी जानकारी को सक्षम या अक्षम करके अपने ईबुक संपादन को अनुकूलित करें।
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EbookEditOptions ebookEditOptions = new EbookEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true
    };
    EditableDocument editableEbookDocument = editor.Edit(ebookEditOptions);
}
```
## चरण 7: ईमेल दस्तावेज़ बनाना और संपादित करना
अंत में, हम देखेंगे कि ईमेल दस्तावेज़ों को कैसे संपादित किया जाता है। इसमें EML जैसे प्रारूप शामिल हैं।
### डिफ़ॉल्ट विकल्पों के साथ बनाएँ और संपादित करें
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EditableDocument defaultEditableEmailDocument = editor.Edit();
}
```
### कस्टम विकल्पों के साथ बनाएँ और संपादित करें
संपादन प्रक्रिया को नियंत्रित करने के लिए मेल संदेश आउटपुट विकल्प निर्दिष्ट करें।
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EmailEditOptions emailEditOptions = new EmailEditOptions
    {
        MailMessageOutput = MailMessageOutput.All
    };
    EditableDocument editableEmailDocument = editor.Edit(emailEditOptions);
}
```
## चरण 8: प्रक्रिया को अंतिम रूप देना
दस्तावेजों को संपादित करने के बाद, संसाधनों को मुक्त करने के लिए मेमोरी स्ट्रीम का उचित तरीके से निपटान करना महत्वपूर्ण है।
```csharp
memoryStream.Dispose();
System.Console.WriteLine("CreateDocument routine has successfully finished");
```
## निष्कर्ष
.NET के लिए GroupDocs.Editor एक बहुमुखी और शक्तिशाली उपकरण है जो विभिन्न दस्तावेज़ प्रकारों को प्रोग्रामेटिक रूप से संपादित करने के कार्य को सरल बना सकता है। इस चरण-दर-चरण मार्गदर्शिका का पालन करके, आप आसानी से दस्तावेज़ बना और संपादित कर सकते हैं, चाहे वे WordProcessing फ़ाइलें, स्प्रेडशीट, प्रस्तुतियाँ, ईबुक या ईमेल हों। अधिक उन्नत सुविधाओं और अनुकूलन विकल्पों के लिए GroupDocs.Editor दस्तावेज़ में गोता लगाएँ।
## अक्सर पूछे जाने वाले प्रश्न
### .NET के लिए मैं GroupDocs.Editor के साथ किस प्रकार के दस्तावेज़ों को संपादित कर सकता हूँ?
आप वर्डप्रोसेसिंग, स्प्रेडशीट, प्रस्तुतीकरण, ई-बुक और ईमेल सहित दस्तावेजों की एक विस्तृत श्रृंखला को संपादित कर सकते हैं।
### क्या संपादन विकल्पों को अनुकूलित करना संभव है?
हां, .NET के लिए GroupDocs.Editor प्रत्येक दस्तावेज़ प्रकार के लिए विशिष्ट विभिन्न संपादन विकल्पों के माध्यम से व्यापक अनुकूलन की अनुमति देता है।
### मैं संपादित दस्तावेजों के आउटपुट को कैसे संभालूँ?
आप संपादित दस्तावेज़ स्ट्रीम को अपने इच्छित स्थान पर सहेजने के लिए कॉलबैक फ़ंक्शन का उपयोग कर सकते हैं।
### क्या मुझे .NET के लिए GroupDocs.Editor का उपयोग करने के लिए लाइसेंस की आवश्यकता है?
 हां, आप यहां से लाइसेंस प्राप्त कर सकते हैं[यहाँ](https://purchase.groupdocs.com/buy)इसमें अस्थायी लाइसेंस का विकल्प भी है।
### मैं अधिक विस्तृत दस्तावेज कहां पा सकता हूं?
 विस्तृत दस्तावेज यहां उपलब्ध है[.NET प्रलेखन पृष्ठ के लिए GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/).