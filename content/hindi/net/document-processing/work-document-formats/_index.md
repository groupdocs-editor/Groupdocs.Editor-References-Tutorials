---
date: 2026-06-06
description: GroupDocs.Editor for .NET का उपयोग करके समर्थित दस्तावेज़ फ़ॉर्मेट की
  सूची बनाना और फ़ाइल फ़ॉर्मेट एक्सटेंशन निर्धारित करना सीखें। Step‑by‑step guide,
  code snippets, quick answers, और FAQs के साथ।
keywords:
- list supported document formats
- determine file format extension
- GroupDocs.Editor .NET
- document editing API
- supported formats guide
linktitle: समर्थित दस्तावेज़ फ़ॉर्मेट की सूची
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to list supported document formats and determine file format
    extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets,
    quick answers, and FAQs.
  headline: List Supported Document Formats with GroupDocs.Editor .NET
  type: TechArticle
- description: Learn how to list supported document formats and determine file format
    extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets,
    quick answers, and FAQs.
  name: List Supported Document Formats with GroupDocs.Editor .NET
  steps:
  - name: '**.NET development environment** – Visual Studio 2022 or any IDE that supports
      .NET 6+.'
    text: '**.NET development environment** – Visual Studio 2022 or any IDE that supports
      .NET 6+.'
  - name: '**GroupDocs.Editor for .NET library** – download from the [GroupDocs releases
      page](https://releases.groupdocs.com/editor/net/).'
    text: '**GroupDocs.Editor for .NET library** – download from the [GroupDocs releases
      page](https://releases.groupdocs.com/editor/net/).'
  - name: '**Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/)
      for unrestricted access.'
    text: '**Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/)
      for unrestricted access.'
  - name: '**Basic C# knowledge** – familiarity with namespaces, `using` statements,
      and console output.'
    text: '**Basic C# knowledge** – familiarity with namespaces, `using` statements,
      and console output.'
  - name: '**Loop Through Formats:** We iterate over all available Word‑processing
      formats.'
    text: '**Loop Through Formats:** We iterate over all available Word‑processing
      formats.'
  - name: '**Output Format Details:** For each format we print its friendly name and
      default file extension.'
    text: '**Output Format Details:** For each format we print its friendly name and
      default file extension.'
  - name: '**Loop Through Formats:** The same looping logic applies to presentations.'
    text: '**Loop Through Formats:** The same looping logic applies to presentations.'
  - name: '**Output Format Details:** The name and extension are displayed for each
      format.'
    text: '**Output Format Details:** The name and extension are displayed for each
      format.'
  - name: '**Parse Format:** `FromExtension` converts the `.xlsm` extension into its
      internal `SpreadsheetFormat` enum.'
    text: '**Parse Format:** `FromExtension` converts the `.xlsm` extension into its
      internal `SpreadsheetFormat` enum.'
  - name: '**Output Format:** The parsed format’s name is printed, confirming the
      mapping.'
    text: '**Output Format:** The parsed format’s name is printed, confirming the
      mapping.'
  type: HowTo
- questions:
  - answer: '`DocumentFormatInfo` provides metadata about supported file types, while
      `SaveOptions` configures how a document is written back to disk (format, compression,
      etc.).'
    question: What is the difference between `DocumentFormatInfo` and `SaveOptions`?
  - answer: Yes—use `DocumentFormatInfo.FromExtension("yourExt")`; if the extension
      isn’t recognized, the method returns `null`.
    question: Can I list formats for a custom file extension?
  - answer: Absolutely. Pass the password to the `Editor` constructor via `EditorSettings`
      to open encrypted documents.
    question: Does GroupDocs.Editor support password‑protected files?
  - answer: Over **30 input and output formats**, spanning Word, Excel, PowerPoint,
      HTML, and plain text.
    question: How many formats does GroupDocs.Editor actually support?
  - answer: Use the `GetEditableWordProcessingFormats()` (or Spreadsheet/Presentation
      equivalents) to retrieve formats that allow full edit capabilities.
    question: Is there a way to restrict the list to only editable formats?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: GroupDocs.Editor .NET के साथ समर्थित दस्तावेज़ फ़ॉर्मेट की सूची बनाएं
type: docs
url: /hi/net/document-processing/work-document-formats/
weight: 13
---

# समर्थित दस्तावेज़ फ़ॉर्मेट्स की सूची

GroupDocs.Editor for .NET के साथ **समर्थित दस्तावेज़ फ़ॉर्मेट्स की सूची कैसे बनाएं** पर हमारे व्यापक ट्यूटोरियल में आपका स्वागत है। चाहे आप एक दस्तावेज़‑केंद्रित वेब ऐप बना रहे हों या एंटरप्राइज़‑ग्रेड डेस्कटॉप टूल, यह जानना कि आप कौन‑से फ़ॉर्मेट्स को संपादित या परिवर्तित कर सकते हैं, अत्यंत आवश्यक है। इस गाइड में आप फ़ॉर्मेट्स की सूची बनाना, एक्सटेंशन पार्स करना, और दस्तावेज़ संपादित करना सीखेंगे—सभी स्पष्ट, उपयोगकर्ता‑मित्र व्याख्याओं और तुरंत चलाने योग्य कोड स्निपेट्स के साथ।

## त्वरित उत्तर
- **मैं सभी समर्थित फ़ॉर्मेट्स की सूची कैसे बनाऊँ?** `DocumentFormatInfo.GetSupportedWordProcessingFormats()` (या Presentation/Spreadsheet समकक्ष) का उपयोग करें और संग्रह पर इटररेट करें।  
- **क्या मैं फ़ाइल एक्सटेंशन से फ़ॉर्मेट निर्धारित कर सकता हूँ?** हाँ—`DocumentFormatInfo.FromExtension(".docx")` को कॉल करें।  
- **GroupDocs.Editor किन फ़ाइल प्रकारों का समर्थन करता है?** 30 से अधिक इनपुट और आउटपुट फ़ॉर्मेट्स, जिसमें DOCX, XLSX, PPTX, HTML, और प्लेन टेक्स्ट शामिल हैं।  
- **फ़ॉर्मेट्स की सूची बनाने के लिए क्या मुझे लाइसेंस चाहिए?** एक टेम्पररी लाइसेंस पूर्ण API अनलॉक करता है; अन्यथा ट्रायल सीमित सुविधाओं के साथ काम करता है।  
- **कौन‑से .NET संस्करण संगत हैं?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.

## “समर्थित दस्तावेज़ फ़ॉर्मेट्स की सूची” क्या है?
यह वाक्यांश प्रोग्रामेटिक रूप से उन फ़ाइल प्रकारों के संग्रह को प्राप्त करने को दर्शाता है जिन्हें GroupDocs.Editor खोल, संपादित और सहेज सकता है। यह ऑपरेशन आपको डायनामिक UI ड्रॉपडाउन बनाने या प्रोसेसिंग से पहले उपयोगकर्ता अपलोड्स को वैलिडेट करने की अनुमति देता है, जिससे केवल संगत फ़ाइलें ही आगे के संचालन के लिए एडिटर को पास की जाती हैं।

## समर्थित दस्तावेज़ फ़ॉर्मेट्स की सूची क्यों बनानी चाहिए?
GroupDocs.Editor **30+ इनपुट और आउटपुट फ़ॉर्मेट्स का समर्थन करता है** और पूरी दस्तावेज़ को मेमोरी में लोड किए बिना **2 GB** तक की फ़ाइलें संभाल सकता है। सटीक सूची को जानने से रन‑टाइम त्रुटियों से बचा जा सकता है, उपयोगकर्ता अनुभव सुधरता है, और आप “केवल संपादन योग्य Office दस्तावेज़ों की अनुमति दें” जैसे व्यावसायिक नियम लागू कर सकते हैं। यह आपको उपयोगकर्ताओं को केवल वही फ़ॉर्मेट्स दिखाने में मदद करता है जो आपका एप्लिकेशन वास्तव में समर्थन करता है।

## पूर्वापेक्षाएँ
1. **.NET विकास पर्यावरण** – Visual Studio 2022 या कोई भी IDE जो .NET 6+ को सपोर्ट करता हो।  
2. **GroupDocs.Editor for .NET लाइब्रेरी** – [GroupDocs रिलीज़ पेज](https://releases.groupdocs.com/editor/net/) से डाउनलोड करें।  
3. **टेम्पररी लाइसेंस** – अनरिस्ट्रिक्टेड एक्सेस के लिए एक [टेम्पररी लाइसेंस](https://purchase.groupdocs.com/temporary-license/) प्राप्त करें।  
4. **बेसिक C# ज्ञान** – नेमस्पेसेस, `using` स्टेटमेंट्स, और कंसोल आउटपुट की परिचितता।

## समर्थित दस्तावेज़ फ़ॉर्मेट्स की सूची कैसे बनाएं?
समर्थित फ़ॉर्मेट्स संग्रह को लोड करें और प्रत्येक फ़ॉर्मेट का नाम और फ़ाइल एक्सटेंशन प्रिंट करें। यह दो‑स्टेप पैटर्न Word Processing, Spreadsheet, और Presentation दस्तावेज़ों के लिए काम करता है। संग्रह को इटररेट करके आप UI तत्वों जैसे ड्रॉपडाउन को डायनामिक रूप से भर सकते हैं, जिससे उपयोगकर्ता केवल वही फ़ॉर्मेट्स चुन सकें जिन्हें एडिटर वास्तव में संभाल सकता है।

```csharp
// No actual code block – placeholder retained from original tutorial
```csharp
using System;
using GroupDocs.Editor.Options;
```
```

### Word Processing फ़ॉर्मेट्स की सूची बनाना
`Formats.WordProcessingFormats` एक एन्यूमरेशन है जो एडिटर द्वारा पहचाने गए प्रत्येक Word‑processing फ़ाइल प्रकार का वर्णन करता है। `All` प्रॉपर्टी इन फ़ॉर्मेट ऑब्जेक्ट्स का संग्रह लौटाती है।

```csharp
```csharp
foreach (Formats.WordProcessingFormats oneFormat in Formats.WordProcessingFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**Explanation:**  
1. **Loop Through Formats:** We iterate over all available Word‑processing formats.  
2. **Output Format Details:** For each format we print its friendly name and default file extension.

### Presentation फ़ॉर्मेट्स की सूची बनाना
`Formats.PresentationFormats` स्लाइड‑डेक फ़ाइलों के लिए भी समान रूप से काम करता है, `All` संग्रह के माध्यम से प्रत्येक समर्थित प्रेजेंटेशन टाइप को उजागर करता है।

```csharp
```csharp
foreach (Formats.PresentationFormats oneFormat in Formats.PresentationFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**Explanation:**  
1. **Loop Through Formats:** The same looping logic applies to presentations.  
2. **Output Format Details:** The name and extension are displayed for each format.

## फ़ाइल फ़ॉर्मेट एक्सटेंशन कैसे निर्धारित करें?
कभी‑कभी आपके पास केवल फ़ाइल नाम होता है और आपको संबंधित `DocumentFormat` का अनुमान लगाना पड़ता है। GroupDocs.Editor एक सरल स्टैटिक हेल्पर प्रदान करता है जो फ़ाइल एक्सटेंशन को उसके आंतरिक फ़ॉर्मेट प्रतिनिधित्व से मैप करता है, जिससे आप फ़ाइलों को एडिटर में लोड करने से पहले वैलिडेट या कनवर्ट कर सकते हैं।

### Spreadsheet फ़ॉर्मेट्स का पार्सिंग
`Formats.SpreadsheetFormats.FromExtension` फ़ाइल एक्सटेंशन स्ट्रिंग को मिलते‑जुलते स्प्रेडशीट फ़ॉर्मेट एन्‍यूम वैल्यू में बदलता है।

```csharp
```csharp
Formats.SpreadsheetFormats expectedXlsm = Formats.SpreadsheetFormats.FromExtension(".xlsm");
Console.WriteLine("Parsed Spreadsheet format is {0}", expectedXlsm.Name);
```
```

**Explanation:**  
1. **Parse Format:** `FromExtension` converts the `.xlsm` extension into its internal `SpreadsheetFormat` enum.  
2. **Output Format:** The parsed format’s name is printed, confirming the mapping.

### Textual फ़ॉर्मेट्स का पार्सिंग
इसी प्रकार, `Formats.TextualFormats.FromExtension` HTML या TXT जैसे टेक्स्टुअल फ़ाइल एक्सटेंशन को हल करता है।

```csharp
```csharp
Formats.TextualFormats expectedHtml = Formats.TextualFormats.FromExtension("html");
Console.WriteLine("Parsed Textual format is {0}", expectedHtml.Name);
```
```

**Explanation:**  
1. **Parse Format:** The `FromExtension` method resolves the `html` extension to a `TextFormat`.  
2. **Output Format:** The name of the textual format is displayed, useful for web‑based editors.

## फ़ॉर्मेट्स की पहचान करने के बाद दस्तावेज़ कैसे संपादित करें?
एक बार फ़ॉर्मेट पता चल जाने पर, दस्तावेज़ को लोड और संपादित करना एक सुसंगत पैटर्न का पालन करता है। पहले आप स्रोत फ़ाइल के पाथ के साथ एक `Editor` इंस्टेंस बनाते हैं, फिर `Edit()` को कॉल करके एक `EditableDocument` प्राप्त करते हैं। उसके बाद आप सामग्री को पढ़ सकते हैं, संशोधित कर सकते हैं, और अंत में उपयुक्त `SaveOptions` का उपयोग करके सहेज सकते हैं।

### दस्तावेज़ लोड करना
`Editor` वह कोर क्लास है जो किसी फ़ाइल के सभी संपादन ऑपरेशन्स को समेटे रहता है।

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/document.docx"))
{
    // Further steps will be covered here.
}
```
```

**Explanation:**  
1. **Initialize Editor:** Create an `Editor` instance, passing the full path of the target file.  
2. **Dispose Pattern:** The `using` statement guarantees that all unmanaged resources are released promptly.

### सामग्री निकालना
`EditableDocument.GetContent()` दस्तावेज़ का कच्चा टेक्स्ट (या वेब‑आधारित एडिटर्स के लिए HTML) लौटाता है, जिसे आप प्रदर्शित या संशोधित कर सकते हैं।

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    string content = editableDocument.GetContent();
    Console.WriteLine(content);
}
```
```

**Explanation:**  
1. **Edit Method:** `Edit()` returns an `EditableDocument` object.  
2. **Get Content:** `GetContent()` extracts the document’s raw text (or HTML for web‑based editors).  
3. **Output Content:** The content is written to the console for verification.

### परिवर्तनों को सहेजना
`SaveOptions` एडिटर को बताता है कि संपादित दस्तावेज़ को किस प्रकार और किस फ़ॉर्मेट में स्टोरेज में वापस लिखना है।

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    // Modify content here
    SaveOptions saveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docx);
    editor.Save(editableDocument, "path/to/save/document.docx", saveOptions);
}
```
```

**Explanation:**  
1. **Edit Method:** Re‑obtain the `EditableDocument` after modifications.  
2. **Modify Content:** Apply your changes to the string (not shown here).  
3. **Save Options:** Configure `SaveOptions` with the desired output format.  
4. **Save Document:** Persist the edited file back to disk.

## विभिन्न दस्तावेज़ प्रकारों के साथ कैसे काम करें?
GroupDocs.Editor Word, Spreadsheet, और Presentation हैंडलिंग को एक ही API सतह के पीछे एब्स्ट्रैक्ट करता है, जिससे प्रत्येक दस्तावेज़ परिवार के लिए नई क्लासेस सीखने की आवश्यकता के बिना संदर्भ बदलना आसान हो जाता है।

### Spreadsheet दस्तावेज़ों को संपादित करना
`SpreadsheetSaveOptions` यह निर्धारित करता है कि स्प्रेडशीट कैसे लिखी जाती है, जिसमें फ़ॉर्मेट और वैकल्पिक कंप्रेशन सेटिंग्स शामिल हैं।

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/spreadsheet.xlsx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // Modify content here
        SaveOptions saveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsx);
        editor.Save(editableDocument, "path/to/save/spreadsheet.xlsx", saveOptions);
    }
}
```
```

**Explanation:**  
1. **Initialize Editor:** Pass a spreadsheet file path to the `Editor` constructor.  
2. **Edit Method:** Retrieve an `EditableDocument`.  
3. **Get Content:** Print the spreadsheet’s CSV representation (or HTML).  
4. **Modify Content:** Apply any cell‑level changes you need.  
5. **Save Options:** Choose the appropriate `SpreadsheetSaveOptions`.  
6. **Save Document:** Write the updated spreadsheet back to storage.

### Presentation दस्तावेज़ों को संपादित करना
`PresentationSaveOptions` स्लाइड डेक के आउटपुट फ़ॉर्मेट को नियंत्रित करता है, जिससे आप मूल फ़ाइल प्रकार को बनाए रख सकते हैं या बदल सकते हैं।

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/presentation.pptx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // Modify content here
        SaveOptions saveOptions = new PresentationSaveOptions(PresentationFormats.Pptx);
        editor.Save(editableDocument, "path/to/save/presentation.pptx", saveOptions);
    }
}
```
```

**Explanation:**  
1. **Initialize Editor:** Load a PowerPoint file via `Editor`.  
2. **Edit Method:** Obtain an `EditableDocument`.  
3. **Get Content:** Extract slide HTML or plain text.  
4. **Modify Content:** Update titles, bullet points, or images.  
5. **Save Options:** Use `PresentationSaveOptions` to define the output format.  
6. **Save Document:** Persist the edited presentation.

## सामान्य समस्याएँ और समाधान
- **“Format not supported” त्रुटि:** सुनिश्चित करें कि आप नवीनतम GroupDocs.Editor संस्करण का उपयोग कर रहे हैं; यह नियमित रूप से नए Office फ़ॉर्मेट्स के समर्थन को जोड़ता है।  
- **बड़ी फ़ाइल मेमोरी खपत:** दस्तावेज़ लोड करने से पहले `EditorSettings.EnableStreaming = true` सेट करके स्ट्रीमिंग मोड सक्षम करें।  
- **लाइसेंस लागू नहीं हुआ:** सुनिश्चित करें कि टेम्पररी लाइसेंस फ़ाइल एप्लिकेशन रूट में रखी गई है या `License license = new License(); license.SetLicense("path/to/license.lic");` के माध्यम से लोड की गई है।

## अक्सर पूछे जाने वाले प्रश्न

**Q: `DocumentFormatInfo` और `SaveOptions` में क्या अंतर है?**  
A: `DocumentFormatInfo` समर्थित फ़ाइल प्रकारों के बारे में मेटाडेटा प्रदान करता है, जबकि `SaveOptions` यह कॉन्फ़िगर करता है कि दस्तावेज़ डिस्क पर कैसे लिखा जाए (फ़ॉर्मेट, कंप्रेशन, आदि)।

**Q: क्या मैं कस्टम फ़ाइल एक्सटेंशन के लिए फ़ॉर्मेट्स की सूची बना सकता हूँ?**  
A: हाँ—`DocumentFormatInfo.FromExtension("yourExt")` का उपयोग करें; यदि एक्सटेंशन पहचाना नहीं जाता, तो मेथड `null` लौटाता है।

**Q: क्या GroupDocs.Editor पासवर्ड‑सुरक्षित फ़ाइलों का समर्थन करता है?**  
A: बिल्कुल। एन्क्रिप्टेड दस्तावेज़ खोलने के लिए पासवर्ड को `EditorSettings` के माध्यम से `Editor` कंस्ट्रक्टर में पास करें।

**Q: GroupDocs.Editor वास्तव में कितने फ़ॉर्मेट्स का समर्थन करता है?**  
A: **30 से अधिक इनपुट और आउटपुट फ़ॉर्मेट्स**, जो Word, Excel, PowerPoint, HTML, और प्लेन टेक्स्ट को कवर करते हैं।

**Q: क्या सूची को केवल संपादन योग्य फ़ॉर्मेट्स तक सीमित करने का कोई तरीका है?**  
A: `GetEditableWordProcessingFormats()` (या Spreadsheet/Presentation समकक्ष) का उपयोग करके उन फ़ॉर्मेट्स को प्राप्त करें जो पूर्ण संपादन क्षमताएँ प्रदान करते हैं।

## अतिरिक्त संसाधन
- लाइब्रेरी डाउनलोड करें [GroupDocs रिलीज़ पेज](https://releases.groupdocs.com/editor/net/) से।  
- पूर्ण फीचर एक्सेस के लिए एक [टेम्पररी लाइसेंस](https://purchase.groupdocs.com/temporary-license/) प्राप्त करें।  
- उत्पाद को एक [फ्री ट्रायल](https://releases.groupdocs.com/) के साथ आज़माएँ।  
- विस्तृत उपयोग उदाहरण देखें [GroupDocs.Editor दस्तावेज़ीकरण](https://tutorials.groupdocs.com/editor/net/) में।  
- समुदाय से मदद प्राप्त करें [सपोर्ट फ़ोरम](https://forum.groupdocs.com/c/editor/20) पर।

## निष्कर्ष
इस गाइड का पालन करके अब आप जानते हैं कि **समर्थित दस्तावेज़ फ़ॉर्मेट्स की सूची कैसे बनाएं**, **फ़ाइल एक्सटेंशन से फ़ॉर्मेट कैसे निर्धारित करें**, और **दस्तावेज़ कैसे संपादित करें** Word, Spreadsheet, और Presentation प्रकारों में GroupDocs.Editor for .NET का उपयोग करके। इन स्निपेट्स को अपने प्रोजेक्ट्स में शामिल करें ताकि आप मजबूत, फ़ॉर्मेट‑सचेत एप्लिकेशन बना सकें जो अंतिम उपयोगकर्ताओं को खुश करें और रन‑टाइम त्रुटियों को कम करें।

**अंतिम अपडेट:** 2026-06-06  
**परीक्षित संस्करण:** GroupDocs.Editor 23.9 for .NET  
**लेखक:** GroupDocs

## संबंधित ट्यूटोरियल्स

- [GroupDocs.Editor के साथ .NET में दस्तावेज़ लोडिंग में महारत: एक व्यापक गाइड](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)  
- [GroupDocs.Editor के साथ .NET में दस्तावेज़ संपादन में महारत: एक व्यापक गाइड](/editor/net/document-editing/master-document-editing-dotnet-groupdocs-editor/)  
- [GroupDocs.Editor .NET का उपयोग करके Word को HTML में बदलना: चरण‑दर‑चरण गाइड](/editor/net/document-saving/convert-word-to-html-groupdocs-editor-dotnet/)