---
date: 2026-06-01
description: GroupDocs.Editor for .NET का उपयोग करके पृष्ठ गिनती प्राप्त करने और दस्तावेज़
  मेटाडेटा निकालने के बारे में विस्तृत चरण‑दर‑चरण ट्यूटोरियल में जानें।
keywords:
- get page count
- extract document metadata
- get document info
- find document extension
- retrieve document size
linktitle: पृष्ठ गिनती प्राप्त करें और दस्तावेज़ जानकारी निकालें
schemas:
- author: GroupDocs
  dateModified: '2026-06-01'
  description: Learn how to get page count and extract document metadata using GroupDocs.Editor
    for .NET in a detailed step‑by‑step tutorial.
  headline: Get Page Count & Extract Document Info with GroupDocs.Editor
  type: TechArticle
- questions:
  - answer: GroupDocs.Editor supports Word processing, spreadsheet, presentation,
      PDF, and plain‑text files—over 50 formats in total.
    question: What document types can I extract metadata from?
  - answer: Access `DocumentInfo.Extension` after calling `GetDocumentInfo()`; it
      returns the extension without the leading dot.
    question: How do I retrieve the file extension?
  - answer: Yes—`DocumentInfo.Size` returns the size in bytes; divide by 1,048,576
      to convert to megabytes.
    question: Can I get the size of a document in megabytes?
  - answer: Absolutely—GroupDocs.Editor never writes the password to disk and disposes
      of all cryptographic objects after use.
    question: Is it safe to process password‑protected files on a server?
  - answer: You can get support from the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).
    question: Where can I find additional help if I run into issues?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: GroupDocs.Editor के साथ पृष्ठ गिनती प्राप्त करें और दस्तावेज़ जानकारी निकालें
type: docs
url: /hi/net/document-processing/extract-document-info/
weight: 10
---

# पृष्ठ गिनती प्राप्त करें और GroupDocs.Editor के साथ दस्तावेज़ जानकारी निकालें

## परिचय
इस व्यापक ट्यूटोरियल में आप सीखेंगे कि **पृष्ठ गिनती** कैसे प्राप्त करें और GroupDocs.Editor for .NET का उपयोग करके विस्तृत दस्तावेज़ जानकारी—जैसे फ़ॉर्मेट, आकार, और एन्क्रिप्शन स्थिति—कैसे निकालें। चाहे आप दस्तावेज़‑प्रबंधन प्रणाली, रिपोर्टिंग इंजन, या स्वचालित रूपांतरण पाइपलाइन बना रहे हों, फ़ाइल के मेटाडेटा को समझना विश्वसनीय प्रोसेसिंग की पहली कदम है। चलिए पूरे वर्कफ़्लो को देखते हैं, फ़ाइल लोड करने से लेकर संसाधनों को सुरक्षित रूप से डिस्पोज़ करने तक।

## त्वरित उत्तर
- **मैं दस्तावेज़ की पृष्ठ गिनती कैसे प्राप्त करूँ?**  
  फ़ाइल को `Editor` के साथ लोड करने के बाद `editor.GetDocumentInfo().PageCount` को कॉल करें।  
- **मेटाडेटा निष्कर्षण के लिए कौन से फ़ाइल फ़ॉर्मेट समर्थित हैं?**  
  50 से अधिक फ़ॉर्मेट, जिसमें DOCX, XLSX, PPTX, PDF, TXT, और HTML शामिल हैं।  
- **क्या मैं पासवर्ड‑सुरक्षित फ़ाइलों से मेटाडेटा निकाल सकता हूँ?**  
  हाँ—`Editor` इंस्टेंस बनाते समय पासवर्ड प्रदान करें।  
- **क्या मुझे संसाधनों को मैन्युअल रूप से रिलीज़ करना चाहिए?**  
  बिल्कुल; हमेशा `editor.Dispose()` को कॉल करें या `using` ब्लॉक में एडिटर को रैप करें।  
- **GroupDocs.Editor का कौन सा संस्करण आवश्यक है?**  
  लेख लिखते समय उपलब्ध नवीनतम स्थिर रिलीज़ (v23.12+ ) सभी दिखाए गए फीचर्स को सपोर्ट करती है।

## GroupDocs.Editor में “पृष्ठ गिनती प्राप्त करें” क्या है?
`GetDocumentInfo()` एक मेथड है जो `DocumentInfo` ऑब्जेक्ट लौटाता है जिसमें दस्तावेज़ की पृष्ठ गिनती, फ़ॉर्मेट, आकार, और अन्य मेटाडेटा शामिल होते हैं। यह एकल कॉल आपको फ़ाइल को मैन्युअल रूप से पार्स किए बिना तुरंत जानकारी देता है। इस मेथड का उपयोग करके आप पूरे दस्तावेज़ को मेमोरी में लोड करने से बचते हैं, जिससे बड़े फ़ाइलों के लिए प्रदर्शन बेहतर होता है और सर्वर संसाधनों की खपत कम होती है।

## GroupDocs.Editor के साथ दस्तावेज़ मेटाडेटा क्यों निकालें?
GroupDocs.Editor **50+ इनपुट और आउटपुट फ़ॉर्मेट** को प्रोसेस कर सकता है और **2 GB** तक की फ़ाइलों के मेटाडेटा को पूरे दस्तावेज़ को मेमोरी में लोड किए बिना प्राप्त कर सकता है। यह दक्षता पूर्ण‑दस्तावेज़ पार्सिंग की तुलना में सर्वर लोड को **70 %** तक कम करती है, जिससे यह उच्च‑थ्रूपुट एप्लिकेशनों के लिए आदर्श बनता है।

## पूर्वापेक्षाएँ
- **C# विकास मूलभूत** – आपको Visual Studio और .NET प्रोजेक्ट संरचनाओं में सहज होना चाहिए।  
- **Visual Studio 2022** (या कोई भी नवीनतम संस्करण) आपके मशीन पर स्थापित होना चाहिए।  
- **GroupDocs.Editor for .NET** – नवीनतम पैकेज [download page](https://releases.groupdocs.com/editor/net/) से डाउनलोड करें।

## अपना दस्तावेज़ कैसे लोड करें?
`Editor` मुख्य क्लास है जो दस्तावेज़ का प्रतिनिधित्व करता है और इसे लोड करने व संशोधित करने के लिए मेथड्स प्रदान करता है। फ़ाइल पाथ पास करके `Editor` इंस्टेंस बनाकर लक्ष्य फ़ाइल लोड करें। एडिटर स्वचालित रूप से फ़ॉर्मेट का पता लगाता है, इसलिए आपको लोड विकल्प निर्दिष्ट करने की आवश्यकता नहीं है। यह तरीका किसी भी समर्थित फ़ाइल प्रकार के लिए काम करता है और प्रारंभिक सेटअप को सरल बनाता है।

```csharp
using System;
using GroupDocs.Editor.Metadata;
```

## दस्तावेज़ जानकारी कैसे प्राप्त करें?
`GetDocumentInfo()` एक `DocumentInfo` ऑब्जेक्ट लौटाता है जिसमें पृष्ठ गिनती, फ़ॉर्मेट, आकार, और एन्क्रिप्शन स्थिति जैसी मेटाडेटा शामिल होती है। लोड करने के बाद इस मेथड को कॉल करके ऑब्जेक्ट प्राप्त करें। लौटाया गया `DocumentInfo` फ़ाइल की विशेषताओं का संक्षिप्त स्नैपशॉट देता है, जिससे आप आगे की प्रोसेसिंग के बिना निर्णय ले सकते हैं।

```csharp
string docxInputFilePath = "YourSampleDocument.docx";
Editor editorDocx = new Editor(docxInputFilePath);
```

## दस्तावेज़ प्रकार कैसे निर्धारित करें?
`DocumentType` एक enum है जो दर्शाता है कि दस्तावेज़ WordProcessing, Spreadsheet, या Text है। यह जानना कि फ़ाइल Word प्रोसेसिंग दस्तावेज़, स्प्रेडशीट, या साधारण टेक्स्ट है, बाद में इसे कैसे हैंडल किया जाए, को प्रभावित करता है। इस निर्णय के लिए `DocumentInfo` ऑब्जेक्ट की `DocumentType` प्रॉपर्टी का उपयोग करें और तदनुसार लॉजिक को शाखा दें।

```csharp
IDocumentInfo infoDocx = editorDocx.GetDocumentInfo(null);
```

## Word Processing फ़ाइलों के लिए विस्तृत जानकारी कैसे निकालें?
`WordProcessing` उन दस्तावेज़ों को दर्शाता है जैसे DOCX, ODT, और RTF जो वर्ड प्रोसेसिंग फ़ाइलों के रूप में संभाले जाते हैं। यदि दस्तावेज़ प्रकार `WordProcessing` है, तो आप **फ़ॉर्मेट**, **एक्सटेंशन**, **पृष्ठ गिनती**, **आकार**, और **एन्क्रिप्शन फ़्लैग** जैसी अतिरिक्त प्रॉपर्टीज़ सीधे `DocumentInfo` ऑब्जेक्ट से पढ़ सकते हैं। ये विवरण आपको प्रोसेसिंग स्टेप्स को अनुकूलित करने में मदद करते हैं, जैसे विशिष्ट रूपांतरण या सुरक्षा जांच लागू करना।

```csharp
bool isSpreadsheet = infoDocx is SpreadsheetDocumentInfo;
bool isText = infoDocx is TextualDocumentInfo;
bool isWordProcessing = infoDocx is WordProcessingDocumentInfo;
Console.WriteLine($"Is '{docxInputFilePath}' a Spreadsheet: {isSpreadsheet}");
Console.WriteLine($"Is '{docxInputFilePath}' a Textual document: {isText}");
Console.WriteLine($"Is '{docxInputFilePath}' a WordProcessing document: {isWordProcessing}");
```

## स्प्रेडशीट और टेक्स्टुअल दस्तावेज़ों को कैसे हैंडल करें?
`Spreadsheet` स्प्रेडशीट फ़ाइलों जैसे XLSX को दर्शाता है, जबकि `Text` साधारण‑टेक्स्ट दस्तावेज़ों को दर्शाता है। स्प्रेडशीट (`Spreadsheet`) और साधारण‑टेक्स्ट फ़ाइलों (`Text`) के लिए `DocumentInfo` ऑब्जेक्ट अभी भी मुख्य मेटाडेटा (एक्सटेंशन, आकार, पृष्ठ गिनती) प्रदान करता है। कुछ फ़ॉर्मेट पृष्ठ गिनती नहीं दिखा सकते हैं, ऐसे में मान `0` होगा। आप फिर भी अन्य मेटाडेटा पर निर्भर रह सकते हैं डाउनस्ट्रीम लॉजिक के लिए।

```csharp
if (isWordProcessing)
{
    WordProcessingDocumentInfo casted = (WordProcessingDocumentInfo)infoDocx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Page count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```

## पासवर्ड‑सुरक्षित दस्तावेज़ों के साथ कैसे काम करें?
`Password` एक स्ट्रिंग है जो एन्क्रिप्टेड फ़ाइलों को खोलने के लिए `Editor` कंस्ट्रक्टर में पास की जाती है। जब दस्तावेज़ एन्क्रिप्टेड हो, तो पहले बिना पासवर्ड के खोलने का प्रयास करें। यदि विफल हो, तो एक्सेप्शन को कैच करें और सही पासवर्ड के साथ पुनः प्रयास करें। इस उद्देश्य के लिए `Editor` कंस्ट्रक्टर `Password` पैरामीटर स्वीकार करता है, जिससे संरक्षित फ़ाइलों को सहजता से हैंडल किया जा सके।

```csharp
string xlsxInputFilePath = "YourSampleDocument.xlsx";
Editor editorXlsx = new Editor(xlsxInputFilePath);
IDocumentInfo infoXlsx = editorXlsx.GetDocumentInfo(null);
bool isXlsxSpreadsheet = infoXlsx is SpreadsheetDocumentInfo;
Console.WriteLine($"Is '{xlsxInputFilePath}' a Spreadsheet: {isXlsxSpreadsheet}");
if (isXlsxSpreadsheet)
{
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo)infoXlsx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Tabs count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```

## टेक्स्ट‑आधारित दस्तावेज़ों को कैसे प्रोसेस करें?
`DocumentInfo` टेक्स्ट फ़ाइलों के लिए आकार, एक्सटेंशन, और एन्कोडिंग जैसी बुनियादी मेटाडेटा प्रदान करता है। टेक्स्ट फ़ाइलें (जैसे `.txt`, `.md`) को सरल स्ट्रीम के रूप में ट्रीट किया जाता है। आप अभी भी `DocumentInfo` से आकार और एन्कोडिंग जानकारी प्राप्त कर सकते हैं, जो फ़ाइल इंटेग्रिटी वैलिडेट करने या उपयुक्त प्रोसेसिंग पाइपलाइन निर्धारित करने में उपयोगी है।

```csharp
string xlsInputFilePath = "YourSampleDocument.xls";
Editor editorXls = new Editor(xlsInputFilePath);
try
{
    IDocumentInfo infoXls = editorXls.GetDocumentInfo(null);
}
catch (PasswordRequiredException)
{
    Console.WriteLine("This document is password-protected.");
}
try
{
    IDocumentInfo infoXls = editorXls.GetDocumentInfo("incorrect_password");
}
catch (IncorrectPasswordException)
{
    Console.WriteLine("The provided password is incorrect.");
}
IDocumentInfo infoXlsValid = editorXls.GetDocumentInfo("correct_password");
bool isXlsSpreadsheet = infoXlsValid is SpreadsheetDocumentInfo;
Console.WriteLine($"Password-protected document is a Spreadsheet: {isXlsSpreadsheet}");
if (isXlsSpreadsheet)
{
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo)infoXlsValid;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Tabs count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```

## संसाधनों को सही तरीके से कैसे डिस्पोज़ करें?
`Editor` मुख्य क्लास है जो अनमैनेज्ड रिसोर्सेज़ रखता है और उपयोग के बाद डिस्पोज़ किया जाना चाहिए। मेमोरी लीक से बचने के लिए, जानकारी निकालने के बाद हमेशा `Editor` इंस्टेंस को डिस्पोज़ करें। `using` स्टेटमेंट सबसे सुरक्षित पैटर्न है क्योंकि यह एक्सेप्शन होने पर भी डिस्पोज़ सुनिश्चित करता है, जिससे साफ़ रिसोर्स मैनेजमेंट होता है।

```csharp
string xmlInputFilePath = "YourSampleDocument.xml";
Editor editorXml = new Editor(xmlInputFilePath);
IDocumentInfo infoXml = editorXml.GetDocumentInfo(null);
bool isXmlText = infoXml is TextualDocumentInfo;
Console.WriteLine($"Is '{xmlInputFilePath}' a Textual document: {isXmlText}");
if (isXmlText)
{
    TextualDocumentInfo casted = (TextualDocumentInfo)infoXml;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Encoding: {casted.Encoding}; Size: {casted.Size} bytes");
}
```

## सामान्य समस्याएँ और समाधान
| समस्या | कारण | समाधान |
|-------|-------|----------|
| **PageCount 0 लौटाता है** | फ़ॉर्मेट पेजिनेशन का समर्थन नहीं करता (जैसे, साधारण टेक्स्ट) | `PageCount` पर निर्भर होने से पहले `DocumentInfo.DocumentType` जांचें। |
| **असमर्थित फ़ाइल फ़ॉर्मेट** | फ़ाइल एक्सटेंशन पहचाना नहीं गया | फ़ाइल 50+ समर्थित फ़ॉर्मेट में से एक है यह सत्यापित करें; GroupDocs.Editor को नवीनतम संस्करण में अपडेट करें। |
| **पासवर्ड एक्सेप्शन** | गलत पासवर्ड प्रदान किया गया | `PasswordProtectedException` को कैच करें और उपयोगकर्ता को पासवर्ड पुनः दर्ज करने के लिए प्रॉम्प्ट करें। |
| **बड़ी फ़ाइलों पर मेमोरी स्पाइक** | बहुत बड़ी PDFs को स्ट्रीमिंग के बिना लोड करना | `LoadOptions` के साथ `LoadOptions.LoadMode = LoadMode.Stream` का उपयोग करें (नए रिलीज़ में उपलब्ध)। |

## अक्सर पूछे जाने वाले प्रश्न

**प्र: मैं किन दस्तावेज़ प्रकारों से मेटाडेटा निकाल सकता हूँ?**  
उ: GroupDocs.Editor वर्ड प्रोसेसिंग, स्प्रेडशीट, प्रेजेंटेशन, PDF, और साधारण‑टेक्स्ट फ़ाइलों को सपोर्ट करता है—कुल मिलाकर 50 से अधिक फ़ॉर्मेट।

**प्र: मैं फ़ाइल एक्सटेंशन कैसे प्राप्त करूँ?**  
उ: `GetDocumentInfo()` कॉल करने के बाद `DocumentInfo.Extension` एक्सेस करें; यह अग्रणी डॉट के बिना एक्सटेंशन लौटाता है।

**प्र: क्या मैं दस्तावेज़ का आकार मेगाबाइट में प्राप्त कर सकता हूँ?**  
उ: हाँ—`DocumentInfo.Size` बाइट्स में आकार लौटाता है; मेगाबाइट में बदलने के लिए 1,048,576 से विभाजित करें।

**प्र: क्या सर्वर पर पासवर्ड‑सुरक्षित फ़ाइलों को प्रोसेस करना सुरक्षित है?**  
उ: बिल्कुल—GroupDocs.Editor पासवर्ड को डिस्क पर कभी नहीं लिखता और उपयोग के बाद सभी क्रिप्टोग्राफिक ऑब्जेक्ट्स को डिस्पोज़ कर देता है।

**प्र: यदि मुझे समस्याएँ आती हैं तो अतिरिक्त सहायता कहाँ मिल सकती है?**  
उ: आप [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20) से सहायता प्राप्त कर सकते हैं।

**अंतिम अपडेट:** 2026-06-01  
**परीक्षण किया गया:** GroupDocs.Editor 23.12 for .NET  
**लेखक:** GroupDocs

```csharp
editorDocx.Dispose();
editorXlsx.Dispose();
editorXls.Dispose();
editorXml.Dispose();
Console.WriteLine("ExtractingDocumentInfo routine has successfully finished");
```

## संबंधित ट्यूटोरियल

- [GroupDocs.Editor के साथ .NET में मेटाडेटा निष्कर्षण में महारत: एक व्यापक गाइड](/editor/net/advanced-features/groupdocs-editor-net-metadata-extraction-guide/)
- [GroupDocs.Editor for .NET के साथ दस्तावेज़ लोडिंग ट्यूटोरियल](/editor/net/document-loading/)
- [GroupDocs.Editor .NET के साथ कुशल दस्तावेज़ संपादन: HTML को संपादन योग्य दस्तावेज़ में बदलें](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)