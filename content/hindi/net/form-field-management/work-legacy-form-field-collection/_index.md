---
title: लीगेसी फ़ॉर्म फ़ील्ड संग्रह के साथ कार्य करें
linktitle: लीगेसी फ़ॉर्म फ़ील्ड संग्रह के साथ कार्य करें
second_title: GroupDocs.Editor .NET एपीआई
description: हमारे विस्तृत गाइड के साथ .NET के लिए GroupDocs.Editor का उपयोग करके लीगेसी फ़ॉर्म फ़ील्ड को प्रबंधित करना सीखें। टेक्स्ट फ़ील्ड, चेकबॉक्स, दिनांक और बहुत कुछ संभालने के लिए बिल्कुल सही।
weight: 12
url: /hi/net/form-field-management/work-legacy-form-field-collection/
---
## परिचय
.NET के लिए GroupDocs.Editor का उपयोग करके लीगेसी फ़ॉर्म फ़ील्ड संग्रह के साथ काम करने के तरीके पर इस व्यापक गाइड में आपका स्वागत है। चाहे आप टेक्स्ट फ़ील्ड, चेकबॉक्स, दिनांक फ़ील्ड या ड्रॉपडाउन मेनू से निपट रहे हों, यह ट्यूटोरियल आपको इन फ़ील्ड को कुशलतापूर्वक प्रबंधित करने के लिए प्रत्येक चरण से गुज़रने में मदद करेगा। इस गाइड के अंत तक, आपको अपने दस्तावेज़ों में विभिन्न फ़ॉर्म फ़ील्ड को संभालने के लिए GroupDocs.Editor का उपयोग करने के तरीके के बारे में ठोस समझ हो जाएगी। आइए शुरू करते हैं!
## आवश्यक शर्तें
शुरू करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित पूर्वापेक्षाएँ हैं:
- विजुअल स्टूडियो: कोई भी नवीनतम संस्करण काम करेगा।
- .NET फ्रेमवर्क: सुनिश्चित करें कि आपके पास .NET फ्रेमवर्क स्थापित है।
-  .NET के लिए GroupDocs.Editor: नवीनतम संस्करण डाउनलोड करें[यहाँ](https://releases.groupdocs.com/editor/net/).
- नमूना दस्तावेज़: परीक्षण प्रयोजनों के लिए फ़ॉर्म फ़ील्ड के साथ एक नमूना DOCX फ़ाइल।
## नामस्थान आयात करें
सबसे पहले, अपने प्रोजेक्ट में ज़रूरी नेमस्पेस को इंपोर्ट करें। फॉर्म फ़ील्ड में बदलाव करने के लिए ज़रूरी क्लास और मेथड तक पहुँचने के लिए ये नेमस्पेस ज़रूरी हैं।
```csharp
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System.IO;
```
## चरण 1: इनपुट फ़ाइल पथ प्राप्त करें
सबसे पहले, आपको अपनी इनपुट फ़ाइल का पथ निर्दिष्ट करना होगा। इस उदाहरण में, हम एक नमूना DOCX फ़ाइल का उपयोग करेंगे जिसमें विभिन्न फ़ॉर्म फ़ील्ड शामिल हैं।
```csharp
string inputFilePath = "path/to/your/sample_legacy_formfields.docx";
```
## चरण 2: फ़ाइल पथ से स्ट्रीम बनाएँ
इसके बाद, अपने दस्तावेज़ की सामग्री को पढ़ने के लिए एक फ़ाइल स्ट्रीम बनाएँ। इस स्ट्रीम का उपयोग दस्तावेज़ को GroupDocs.Editor में लोड करने के लिए किया जाएगा।
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
    // अतिरिक्त कोड यहाँ जाएगा
}
```
## चरण 3: दस्तावेज़ के लिए लोड विकल्प बनाएँ
दस्तावेज़ लोड करने से पहले, लोड विकल्प बनाएँ। ये विकल्प अलग-अलग परिदृश्यों को संभालने में मदद करेंगे, जैसे कि पासवर्ड से सुरक्षित दस्तावेज़।
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
// यदि दस्तावेज़ पासवर्ड से सुरक्षित है, तो पासवर्ड निर्दिष्ट करें
loadOptions.Password = "your_password_here"; // यदि आवश्यक हो तो वास्तविक पासवर्ड का उपयोग करें
```
## चरण 4: एडिटर इंस्टेंस के साथ दस्तावेज़ लोड करें
अब, आपके द्वारा पहले बनाए गए फ़ाइल स्ट्रीम और लोड विकल्पों का उपयोग करके दस्तावेज़ को संपादक इंस्टेंस में लोड करें।
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    // अतिरिक्त कोड यहाँ जाएगा
}
```
## चरण 5: FormFieldManager इंस्टेंस पढ़ें
फ़ॉर्म फ़ील्ड प्रबंधित करने के लिए, संपादक से FormFieldManager इंस्टेंस तक पहुँचें। यह इंस्टेंस आपको अपने दस्तावेज़ के भीतर फ़ॉर्म फ़ील्ड के साथ इंटरैक्ट करने की अनुमति देगा।
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
## चरण 6: फ़ॉर्म फ़ील्ड संग्रह पढ़ें
FormFieldManager से FormFieldCollection प्राप्त करें। इस संग्रह में दस्तावेज़ में मौजूद सभी फ़ॉर्म फ़ील्ड शामिल हैं।
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
## चरण 7: प्रत्येक फ़ॉर्म फ़ील्ड के माध्यम से पुनरावृति करें
संग्रह में प्रत्येक फ़ॉर्म फ़ील्ड के माध्यम से लूप करें और उसके प्रकार की पहचान करें। प्रकार के आधार पर, आप फ़ील्ड के मान को निकाल सकते हैं और उसमें बदलाव कर सकते हैं।
```csharp
foreach (var formField in collection)
{
    switch (formField.Type)
    {
        case FormFieldType.Text:
            TextFormField textFormField = collection.GetFormField<TextFormField>(formField.Name);
            Console.WriteLine($"TextFormField detected, name: {formField.Name}, value: {textFormField.Value}");
            break;
        case FormFieldType.CheckBox:
            CheckBoxForm checkBoxFormField = collection.GetFormField<CheckBoxForm>(formField.Name);
            Console.WriteLine($"CheckBoxForm detected, name: {formField.Name}, value: {checkBoxFormField.Value}");
            break;
        case FormFieldType.Date:
            DateFormField dateFormField = collection.GetFormField<DateFormField>(formField.Name);
            Console.WriteLine($"DateFormField detected, name: {formField.Name}, value: {dateFormField.Value}");
            break;
        case FormFieldType.Number:
            NumberFormField numberFormField = collection.GetFormField<NumberFormField>(formField.Name);
            Console.WriteLine($"NumberFormField detected, name: {formField.Name}, value: {numberFormField.Value}");
            break;
        case FormFieldType.DropDown:
            DropDownFormField dropDownFormField = collection.GetFormField<DropDownFormField>(formField.Name);
            Console.WriteLine($"DropDownFormField detected, name: {formField.Name}, value selected: {dropDownFormField.Value[dropDownFormField.SelectedIndex]}");
            break;
    }
}
```
## चरण 8: निष्कर्ष
इन चरणों का पालन करके, आप GroupDocs.Editor for .NET का उपयोग करके अपने दस्तावेज़ों में लीगेसी फ़ॉर्म फ़ील्ड को प्रभावी ढंग से प्रबंधित और इंटरैक्ट कर सकते हैं। चाहे वह टेक्स्ट फ़ील्ड हो, चेकबॉक्स हो, दिनांक हो, संख्या हो या ड्रॉपडाउन हो, यह गाइड प्रत्येक प्रकार को संभालने का एक स्पष्ट और संक्षिप्त तरीका प्रदान करता है।
## निष्कर्ष
 सही टूल का उपयोग करके दस्तावेज़ों में लीगेसी फ़ॉर्म फ़ील्ड के साथ काम करना आसान हो सकता है। .NET के लिए GroupDocs.Editor इन फ़ील्ड को कुशलतापूर्वक प्रबंधित करने के लिए एक मज़बूत समाधान प्रदान करता है। इस चरण-दर-चरण मार्गदर्शिका का पालन करके, अब आप अपने दस्तावेज़ों में विभिन्न फ़ॉर्म फ़ील्ड को आसानी से मैनिपुलेट करने में सक्षम होंगे।[प्रलेखन](https://tutorials.groupdocs.com/editor/net/)अधिक उन्नत सुविधाओं और विकल्पों के लिए.
## अक्सर पूछे जाने वाले प्रश्न
### 1. क्या मैं पासवर्ड-संरक्षित दस्तावेज़ों के साथ .NET के लिए GroupDocs.Editor का उपयोग कर सकता हूँ?
हां, आप पासवर्ड-संरक्षित दस्तावेज़ों को संभालने के लिए लोड विकल्पों में पासवर्ड निर्दिष्ट कर सकते हैं।
### 2. मैं .NET के लिए GroupDocs.Editor का निःशुल्क परीक्षण कैसे प्राप्त कर सकता हूँ?
 आप यहां से निःशुल्क परीक्षण डाउनलोड कर सकते हैं[यहाँ](https://releases.groupdocs.com/).
### 3. क्या .NET के लिए GroupDocs.Editor के लिए कोई समर्थन उपलब्ध है?
 हां, आप सहायता प्राप्त कर सकते हैं[यहाँ](https://forum.groupdocs.com/c/editor/20).
### 4. क्या मैं .NET के लिए GroupDocs.Editor का लाइसेंस खरीद सकता हूं?
 हां, आप यहां से लाइसेंस खरीद सकते हैं[यहाँ](https://purchase.groupdocs.com/buy).
### 5. मैं .NET के लिए GroupDocs.Editor के दस्तावेज़ कहां पा सकता हूं?
दस्तावेज़ उपलब्ध है[यहाँ](https://tutorials.groupdocs.com/editor/net/).