---
title: फ़ॉर्म फ़ील्ड संग्रह निकालें
linktitle: फ़ॉर्म फ़ील्ड संग्रह निकालें
second_title: GroupDocs.Editor .NET एपीआई
description: इस चरण-दर-चरण मार्गदर्शिका के साथ .NET के लिए GroupDocs.Editor का उपयोग करके Word दस्तावेज़ों से फ़ॉर्म फ़ील्ड निकालना सीखें। डेवलपर्स के लिए आदर्श।
type: docs
weight: 13
url: /hi/net/form-field-management/remove-form-field-collection/
---
## परिचय
क्या आप अपने दस्तावेज़ों में फ़ॉर्म फ़ील्ड को प्रोग्रामेटिक रूप से प्रबंधित करना चाहते हैं? .NET के लिए GroupDocs.Editor विभिन्न दस्तावेज़ स्वरूपों में फ़ॉर्म फ़ील्ड को संभालने और हेरफेर करने के लिए एक शक्तिशाली समाधान प्रदान करता है। इस ट्यूटोरियल में, हम आपको इस मज़बूत लाइब्रेरी का उपयोग करके Word दस्तावेज़ से फ़ॉर्म फ़ील्ड संग्रह को हटाने के चरणों के माध्यम से मार्गदर्शन करेंगे। 
## आवश्यक शर्तें
इससे पहले कि हम कोड में उतरें, आइए सुनिश्चित करें कि आपके पास सुचारू अनुभव के लिए सब कुछ सेट है:
1. .NET के लिए GroupDocs.Editor: सुनिश्चित करें कि आपने .NET के लिए GroupDocs.Editor डाउनलोड और इंस्टॉल किया है। यदि नहीं, तो आप इसे डाउनलोड कर सकते हैं[यहाँ](https://releases.groupdocs.com/editor/net/).
2. विकास परिवेश: आपको विजुअल स्टूडियो जैसे विकास परिवेश की आवश्यकता होगी।
3. .NET फ्रेमवर्क: सुनिश्चित करें कि आपके मशीन पर .NET फ्रेमवर्क स्थापित है।
4.  नमूना दस्तावेज़: एक नमूना वर्ड दस्तावेज़ रखें (उदाहरण के लिए,`SampleLegacyFormFields.docx`) को उन फॉर्म फ़ील्ड्स के साथ जोड़ें जिन्हें आप बदलना चाहते हैं।

## नामस्थान आयात करें
आरंभ करने के लिए, आपको अपने .NET प्रोजेक्ट में आवश्यक नामस्थान आयात करने की आवश्यकता है। इससे आप GroupDocs.Editor कार्यक्षमताओं तक पहुँच सकेंगे।
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System.IO;
```
## चरण 1: दस्तावेज़ लोड करें
सबसे पहले, आपको वह दस्तावेज़ लोड करना होगा जिसे आप संपादित करना चाहते हैं। आइए इसे विस्तार से समझते हैं:
### चरण 1.1: इनपुट फ़ाइल का पथ प्राप्त करें
 आपको अपनी इनपुट फ़ाइल का पथ निर्दिष्ट करना होगा। इस उदाहरण के लिए, हम एक नमूना फ़ाइल का उपयोग करेंगे जिसका नाम है`SampleLegacyFormFields.docx`.
```csharp
string inputFilePath = "path/to/SampleLegacyFormFields.docx";
```
### चरण 1.2: पथ से फ़ाइलस्ट्रीम बनाएँ
 इसके बाद, एक बनाएं`FileStream` दस्तावेज़ को पढ़ने के लिए.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
    // इस using ब्लॉक के भीतर अगले चरणों पर आगे बढ़ें।
}
```
## चरण 2: लोड विकल्प सेट करें
दस्तावेज़ लोड करते समय, आपको लोड विकल्प निर्दिष्ट करने की आवश्यकता हो सकती है, खासकर यदि आपका दस्तावेज़ पासवर्ड-संरक्षित है।
### चरण 2.1: लोड विकल्प बनाएँ
 इसका एक उदाहरण बनाएं`WordProcessingLoadOptions`.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
```
### चरण 2.2: पासवर्ड निर्दिष्ट करें (यदि आवश्यक हो)
यदि आपका दस्तावेज़ पासवर्ड-संरक्षित है, तो आप पासवर्ड निर्दिष्ट कर सकते हैं।
```csharp
loadOptions.Password = "some_password_to_open_a_document";
```
## चरण 3: दस्तावेज़ को संपादक में लोड करें
 अब, दस्तावेज़ को लोड करें`Editor` उदाहरण का उपयोग कर`FileStream` और`LoadOptions`.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    // इस using ब्लॉक के भीतर अगले चरणों पर आगे बढ़ें।
}
```
## चरण 4: फ़ॉर्म फ़ील्ड तक पहुँचें और उन्हें प्रबंधित करें
दस्तावेज़ लोड होने के बाद, अब आप फ़ॉर्म फ़ील्ड तक पहुंच सकते हैं और उनमें बदलाव कर सकते हैं।
### चरण 4.1: फॉर्म फ़ील्ड मैनेजर पढ़ें
 पुनः प्राप्त करें`FormFieldManager` से`Editor` उदाहरण।
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
### चरण 4.2: फॉर्म फ़ील्ड संग्रह तक पहुँचें
 लाओ`FormFieldCollection` जिसमें दस्तावेज़ के सभी फ़ॉर्म फ़ील्ड शामिल हैं.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
### चरण 4.3: एक विशिष्ट टेक्स्ट फ़ॉर्म फ़ील्ड निकालें
किसी विशिष्ट टेक्स्ट फ़ॉर्म फ़ील्ड को हटाने के लिए, उसे उसके नाम से ढूंढें और फिर हटा दें.
```csharp
TextFormField textField = collection.GetFormField<TextFormField>("Text1");
fieldManager.RemoveFormFiled(textField);
```
### चरण 4.4: एकाधिक फ़ॉर्म फ़ील्ड हटाएं
आप एक साथ कई फ़ॉर्म फ़ील्ड को उनके नाम निर्दिष्ट करके हटा भी सकते हैं.
```csharp
textField = collection.GetFormField<TextFormField>("Text7");
CheckBoxForm checkBoxForm = collection.GetFormField<CheckBoxForm>("Check2");
fieldManager.RemoveFormFields(new IFormField[] { textField, checkBoxForm });
```
## चरण 5: संशोधित दस्तावेज़ सहेजें
फ़ॉर्म फ़ील्ड को संशोधित करने के बाद, आपको दस्तावेज़ को सहेजना होगा।
### चरण 5.1: सहेजें विकल्प बनाएँ
आउटपुट दस्तावेज़ के लिए प्रारूप और सहेजें विकल्प निर्दिष्ट करें।
```csharp
WordProcessingFormats docFormat = WordProcessingFormats.Docx;
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(docFormat);
```
### चरण 5.2: मेमोरी उपयोग को अनुकूलित करें
यदि आप बड़े दस्तावेज़ों पर काम कर रहे हैं, तो आप मेमोरी उपयोग को अनुकूलित करना चाहेंगे।
```csharp
saveOptions.OptimizeMemoryUsage = true;
```
### चरण 5.3: सुरक्षा सेट करें (यदि आवश्यक हो)
आप लेखन पासवर्ड सेट करके दस्तावेज़ को आगे संपादन से सुरक्षित कर सकते हैं।
```csharp
saveOptions.Protection = new WordProcessingProtection(WordProcessingProtectionType.AllowOnlyFormFields, "write_password");
```
### चरण 5.4: दस्तावेज़ सहेजें
 अंत में, दस्तावेज़ को सेव करें`MemoryStream`.
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(outputStream, saveOptions);
}
```

## निष्कर्ष
बधाई हो! आपने .NET के लिए GroupDocs.Editor का उपयोग करके Word दस्तावेज़ से फ़ॉर्म फ़ील्ड को सफलतापूर्वक हटा दिया है। यह शक्तिशाली लाइब्रेरी प्रोग्रामेटिक रूप से दस्तावेज़ सामग्री में हेरफेर करना आसान बनाती है, जिससे आपका समय और प्रयास बचता है।
## अक्सर पूछे जाने वाले प्रश्न
### क्या मैं अन्य दस्तावेज़ प्रारूपों के साथ .NET के लिए GroupDocs.Editor का उपयोग कर सकता हूं?
हां, .NET के लिए GroupDocs.Editor पीडीएफ, HTML, और अधिक सहित विभिन्न दस्तावेज़ प्रारूपों का समर्थन करता है।
### क्या .NET के लिए GroupDocs.Editor का उपयोग करके फ़ॉर्म फ़ील्ड जोड़ना संभव है?
हां, आप प्रोग्रामेटिक रूप से फ़ॉर्म फ़ील्ड जोड़, संशोधित और हटा सकते हैं.
### यदि मेरा दस्तावेज़ बहुत बड़ा है तो क्या होगा?
आप बड़े दस्तावेज़ों को कुशलतापूर्वक संभालने के लिए सेव विकल्पों में मेमोरी ऑप्टिमाइज़ेशन सक्षम कर सकते हैं।
### क्या मैं वेब अनुप्रयोग में .NET के लिए GroupDocs.Editor का उपयोग कर सकता हूँ?
बिल्कुल! .NET के लिए GroupDocs.Editor सर्वर-साइड दस्तावेज़ प्रसंस्करण के लिए वेब अनुप्रयोगों में एकीकृत किया जा सकता है।
### यदि मुझे कोई समस्या आती है तो मुझे सहायता कहां से मिल सकती है?
 आप यहां जा सकते हैं[सहयता मंच](https://forum.groupdocs.com/c/editor/20) किसी भी समस्या में सहायता के लिए.