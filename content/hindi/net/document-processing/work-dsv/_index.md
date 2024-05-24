---
title: सीमांकित पृथक मान (DSV) के साथ कार्य करें
linktitle: सीमांकित पृथक मान (DSV) के साथ कार्य करें
second_title: GroupDocs.Editor .NET एपीआई
description: इस चरण-दर-चरण मार्गदर्शिका के साथ .NET के लिए GroupDocs.Editor का उपयोग करके CSV और TSV फ़ाइलों को संपादित करना सीखें। अपने .NET प्रोजेक्ट्स को आसानी से बेहतर बनाएँ।
type: docs
weight: 12
url: /hi/net/document-processing/work-dsv/
---
## परिचय
यदि आप CSV या TSV फ़ाइलों जैसे सीमांकित अलग किए गए मान (DSV) के साथ काम करने वाले डेवलपर हैं, तो आप जानते हैं कि इन फ़ाइलों को प्रोग्रामेटिक रूप से संपादित करना एक कठिन काम हो सकता है। हालाँकि, GroupDocs.Editor for .NET के साथ, यह कार्य काफी सरल और अधिक कुशल हो जाता है। इस ट्यूटोरियल में, हम आपको DSV फ़ाइलों को पढ़ने, संपादित करने और सहेजने के लिए GroupDocs.Editor for .NET का उपयोग करने का तरीका बताएंगे। हम इस प्रक्रिया को आसान चरणों में विभाजित करेंगे, जिससे आपके लिए अपनी परियोजनाओं में इसे लागू करना आसान हो जाएगा।
## आवश्यक शर्तें
इससे पहले कि हम ट्यूटोरियल में आगे बढ़ें, सुनिश्चित करें कि आपके पास निम्नलिखित पूर्वापेक्षाएँ हैं:
- विज़ुअल स्टूडियो: सुनिश्चित करें कि आपके मशीन पर विज़ुअल स्टूडियो स्थापित है।
-  .NET के लिए GroupDocs.Editor: आपको .NET लाइब्रेरी के लिए GroupDocs.Editor को डाउनलोड और संदर्भित करना होगा। आप इसे डाउनलोड कर सकते हैं[यहाँ](https://releases.groupdocs.com/editor/net/).
- C# की बुनियादी समझ: यह ट्यूटोरियल मानता है कि आपको C# और .NET विकास की बुनियादी समझ है।
## नामस्थान आयात करें
सबसे पहले, आपको अपने प्रोजेक्ट में आवश्यक नामस्थान आयात करने की आवश्यकता है। ये नामस्थान .NET के लिए GroupDocs.Editor के साथ काम करने के लिए आवश्यक कक्षाएं और विधियाँ प्रदान करते हैं।
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

## चरण 1: इनपुट DSV फ़ाइल का पथ प्राप्त करें
सबसे पहले, आपको इनपुट DSV फ़ाइल का पथ निर्दिष्ट करना होगा। इस उदाहरण के लिए, हम मान लेंगे कि यह एक CSV फ़ाइल है।
```csharp
string inputFilePath = "Your Sample Document";
```
## चरण 2: एक संपादक इंस्टेंस बनाएँ
 इसका एक उदाहरण बनाएं`Editor` क्लास. इस इंस्टेंस का उपयोग DSV फ़ाइल को लोड करने और उसमें हेरफेर करने के लिए किया जाएगा.
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## चरण 3: DSV संपादन विकल्प बनाएँ
 इसके बाद, इसका एक उदाहरण बनाएं`DelimitedTextEditOptions` और DSV फ़ाइल के लिए सीमांकक निर्दिष्ट करें। यहाँ, हम सीमांकक के रूप में अल्पविराम का उपयोग करते हैं।
```csharp
    Options.DelimitedTextEditOptions editOptions = new DelimitedTextEditOptions(",");
    editOptions.ConvertDateTimeData = false;
    editOptions.ConvertNumericData = true;
    editOptions.TreatConsecutiveDelimitersAsOne = true;
```
## चरण 4: संपादन योग्य दस्तावेज़ इंस्टेंस बनाएँ
 एक बनाएं`EditableDocument` उदाहरण का उपयोग कर`Editor.Edit` यह दस्तावेज़ को संपादन के लिए तैयार करता है।
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## चरण 5: दस्तावेज़ सामग्री संपादित करें
मूल पाठ सामग्री को पुनः प्राप्त करें और आवश्यक संशोधन करें। प्रदर्शन के उद्देश्य से, आइए कुछ पाठ बदलें।
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("SsangYong", "Chevrolet").Replace("Kyron", "Camaro");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## चरण 6: अपडेट की गई सामग्री के साथ संपादन योग्य दस्तावेज़ बनाएँ
 कोई नया बनाएं`EditableDocument` अद्यतन सामग्री के साथ.
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## चरण 7: CSV सहेजें विकल्प बनाएँ
डिलीमीटर और एनकोडिंग सहित CSV प्रारूप के लिए सहेजने के विकल्प निर्दिष्ट करें।
```csharp
    Options.DelimitedTextSaveOptions csvSaveOptions = new DelimitedTextSaveOptions(",");
    csvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## चरण 8: TSV सहेजें विकल्प बनाएँ
इसी प्रकार, TSV प्रारूप के लिए सहेजने के विकल्प निर्दिष्ट करें।
```csharp
    Options.DelimitedTextSaveOptions tsvSaveOptions = new DelimitedTextSaveOptions("\t");
    tsvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## चरण 9: स्प्रेडशीट सहेजें विकल्प बनाएँ
यदि आपको दस्तावेज़ को स्प्रेडशीट के रूप में सहेजना है, तो संगत सहेजें विकल्प बनाएँ।
```csharp
    Options.SpreadsheetSaveOptions cellsSaveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
```
## चरण 10: सेव पथ तैयार करें
उन पथों को परिभाषित करें जहां संपादित फ़ाइलें सहेजी जाएंगी.
```csharp
    string outputCsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".csv");
    string outputTsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".tsv");
    string outputCellsPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".xlsm");
```
## चरण 11: संपादित दस्तावेज़ को सहेजें
संपादित दस्तावेज़ को विभिन्न प्रारूपों में निर्दिष्ट पथों पर सहेजें।
```csharp
    editor.Save(afterEdit, outputCsvPath, csvSaveOptions);
    editor.Save(afterEdit, outputTsvPath, tsvSaveOptions);
    editor.Save(afterEdit, outputCellsPath, cellsSaveOptions);
```
## चरण 12: EditableDocument इंस्टैंस को हटाएँ
 अंत में, सुनिश्चित करें कि आप इसका निपटान कर दें`EditableDocument` संसाधनों को मुक्त करने के लिए उदाहरण।
```csharp
    beforeEdit.Dispose();
    afterEdit.Dispose();
}
System.Console.WriteLine("WorkingWithDsv routine has successfully finished");
```
## निष्कर्ष
.NET के लिए GroupDocs.Editor का उपयोग करके DSV फ़ाइलों को संपादित करना एक सीधी प्रक्रिया है जिसमें एक संपादक उदाहरण बनाना, संपादन विकल्प सेट करना, सामग्री को संशोधित करना और परिवर्तनों को सहेजना शामिल है। यह चरण-दर-चरण मार्गदर्शिका आपको इस कार्यक्षमता को अपने .NET अनुप्रयोगों में आसानी से एकीकृत करने में मदद करेगी। चाहे आप CSV, TSV या अन्य DSV प्रारूपों के साथ काम कर रहे हों, .NET के लिए GroupDocs.Editor एक मजबूत और लचीला समाधान प्रदान करता है।
## अक्सर पूछे जाने वाले प्रश्न
### क्या मैं बड़ी CSV फ़ाइलों को संपादित करने के लिए .NET के लिए GroupDocs.Editor का उपयोग कर सकता हूं?
हां, .NET के लिए GroupDocs.Editor बड़ी CSV फ़ाइलों को कुशलतापूर्वक संभालने में सक्षम है।
### क्या .NET के लिए GroupDocs.Editor CSV और TSV के अलावा अन्य DSV प्रारूपों का समर्थन करता है?
हां, यह विभिन्न DSV प्रारूपों का समर्थन करता है, बशर्ते आप उपयुक्त सीमांकक निर्दिष्ट करें।
### क्या DSV फ़ाइलों को सहेजते समय एन्कोडिंग को अनुकूलित करना संभव है?
बिल्कुल, आप सेव विकल्पों में वांछित एनकोडिंग निर्दिष्ट कर सकते हैं।
### क्या मैं .NET के लिए GroupDocs.Editor का उपयोग करके CSV फ़ाइल को Excel स्प्रेडशीट में परिवर्तित कर सकता हूं?
हां, आप उपयुक्त सेव विकल्पों का उपयोग करके CSV फ़ाइल को एक्सेल स्प्रेडशीट के रूप में सेव कर सकते हैं।
### मैं .NET के लिए GroupDocs.Editor पर अधिक दस्तावेज़ कहां पा सकता हूं?
 आप विस्तृत दस्तावेज पा सकते हैं[यहाँ](https://reference.groupdocs.com/editor/net/)