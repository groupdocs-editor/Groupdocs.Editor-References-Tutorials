---
date: 2026-03-14
description: เรียนรู้วิธีดึงรูปภาพจากไฟล์ DOCX, แปลง DOCX เป็น HTML, และบันทึกเอกสารเป็น
  HTML ด้วย GroupDocs.Editor สำหรับ .NET.
linktitle: Extract Images from DOCX – Advanced Editable Document Usage
second_title: GroupDocs.Editor .NET API
title: ดึงรูปภาพจาก DOCX – การใช้งานเอกสารที่แก้ไขได้ขั้นสูง
type: docs
url: /th/net/document-editing/advanced-usage-of-editable-documents/
weight: 11
---

# ดึงรูปภาพจาก DOCX – การใช้งานเอกสารที่แก้ไขได้ขั้นสูง

หากคุณเป็นนักพัฒนา .NET ที่ต้องการ **extract images from DOCX** และเพิ่มศักยภาพการแก้ไขเอกสารของคุณ GroupDocs.Editor สำหรับ .NET มีชุดเครื่องมือที่ทรงพลัง คู่มือฉบับสมบูรณ์นี้จะพาคุณผ่านการใช้งานเอกสารที่แก้ไขได้ขั้นสูงด้วย GroupDocs.Editor โดยแยกแต่ละขั้นตอนอย่างละเอียดเพื่อให้คุณใช้ประโยชน์เต็มที่

## คำตอบด่วน
- **ฉันจะดึงรูปภาพจากไฟล์ DOCX ได้อย่างไร?** ใช้ `EditableDocument.Images` หลังจากโหลดเอกสารด้วย `Editor`.
- **ฉันสามารถแปลง DOCX เป็น HTML พร้อมทรัพยากรที่ฝังอยู่ได้หรือไม่?** ได้—เรียก `EditableDocument.GetEmbeddedHtml()` หรือ `GetContent()` เพื่อรับ markup HTML.
- **เมธอดใดที่บันทึกเอกสารที่แก้ไขเป็น HTML?** `EditableDocument.Save(htmlFilePath)` จะสร้างไฟล์ HTML พร้อมโฟลเดอร์ทรัพยากร
- **สามารถดึงฟอนต์จากเอกสาร Word ได้หรือไม่?** ใช้ `EditableDocument.Fonts` เพื่อดึงทรัพยากรฟอนต์ทั้งหมด
- **ฉันต้องมีไลเซนส์สำหรับการใช้งานในโปรดักชันหรือไม่?** จำเป็นต้องมีไลเซนส์ GroupDocs.Editor ที่ถูกต้อง; มีการทดลองใช้ฟรี

## **extract images from docx** คืออะไร?
การดึงรูปภาพจากไฟล์ DOCX หมายถึงการดึงรูปภาพแต่ละรูปที่ฝังอยู่ในเอกสาร Word อย่างโปรแกรมมิ่ง เพื่อให้คุณสามารถนำกลับมาใช้ใหม่ แก้ไข หรือเก็บแยกออกได้ GroupDocs.Editor เปิดเผยคอลเลกชัน `Images` บนอินสแตนซ์ `EditableDocument` ทำให้งานนี้ง่ายขึ้น

## ทำไมต้องใช้ GroupDocs.Editor สำหรับเวิร์กโฟลว์นี้?
- **การควบคุมเต็มรูปแบบ** ของทรัพยากรเอกสาร (รูปภาพ, ฟอนต์, CSS) โดยไม่ต้องจัดการ ZIP ด้วยตนเอง.  
- **การแปลงอย่างไร้รอยต่อ** จาก DOCX ไปเป็น HTML พร้อมคงรูปแบบและสไตล์.  
- **การดึงทรัพยากรอย่างง่าย** สำหรับการจัดการรูปภาพแบบกำหนดเอง, ฝังฟอนต์, หรือการส่งมอบผ่าน CDN.  
- **รูปแบบการทำลายที่แข็งแรง** รับประกันว่าไม่มีการรั่วของหน่วยความจำในบริการที่ทำงานเป็นเวลานาน.

## ข้อกำหนดเบื้องต้น
- ติดตั้ง Visual Studio บนเครื่องพัฒนาของคุณ.  
- .NET Framework ที่เข้ากันได้กับ GroupDocs.Editor.  
- ไลบรารี GroupDocs.Editor สำหรับ .NET คุณสามารถ [ดาวน์โหลดได้ที่นี่](https://releases.groupdocs.com/editor/net/).  
- ไลเซนส์ GroupDocs.Editor ที่ถูกต้อง คุณสามารถรับ [การทดลองใช้ฟรี](https://releases.groupdocs.com/) หรือซื้อ [ไลเซนส์ชั่วคราว](https://purchase.groupdocs.com/temporary-license/).

## นำเข้า Namespaces
To begin, ensure you import the necessary namespaces in your .NET project:

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

## ขั้นตอนที่ 1: การสร้างอินสแตนซ์ EditableDocument
First, you need to create an instance of `EditableDocument` by loading and editing an input document of a supported format.

```csharp
string inputFilePath = "YourSampleDocument.docx";
Editor editor = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```

ในขั้นตอนนี้ เราโหลดเอกสารอินพุตและเตรียมพร้อมสำหรับการแก้ไข.

## วิธีการ **extract images from DOCX**?
Below we dive into the resource extraction capabilities, starting with the most common need—getting all images out of a Word file.

## ขั้นตอนที่ 2: การดึงทรัพยากรของเอกสาร
The `EditableDocument` contains various resources that can be extracted and manipulated. Let's break these down:

### ขั้นตอน 2.1: ดึงเอกสารทั้งหมดเป็น HTML
You can generate a single string that contains the entire document with all its resources embedded as HTML.

```csharp
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```

สตริงนี้จะค่อนข้างใหญ่เนื่องจากรวม stylesheet, รูปภาพ, และฟอนต์ที่เข้ารหัสเป็น base64.

### ขั้นตอน 2.2: ดึงรูปภาพทั้งหมด *(primary keyword in action)*
```csharp
List<IImageResource> allImages = beforeEdit.Images;
```

### ขั้นตอน 2.3: ดึงฟอนต์ทั้งหมด *(secondary keyword)*
หากคุณต้องการ **extract fonts from word** ด้วย ให้ใช้คำเรียกต่อไปนี้:

```csharp
List<FontResourceBase> allFonts = beforeEdit.Fonts;
```

### ขั้นตอน 2.4: ดึง Stylesheets ทั้งหมด
ดึง Stylesheets ทั้งหมดในรูปแบบข้อความ.

```csharp
List<CssText> allStylesheets = beforeEdit.Css;
```

### ขั้นตอน 2.5: รวบรวมทรัพยากรทั้งหมด
รวบรวมทรัพยากรทั้งหมดด้วยการเรียกครั้งเดียว.

```csharp
List<IHtmlResource> allResources = beforeEdit.AllResources;
```

ซึ่งรวมถึงรูปภาพ, ฟอนต์, และ Stylesheets.

### ขั้นตอน 2.6: รับ HTML Markup
รับ HTML markup ของเอกสารโดยไม่มีทรัพยากรที่ฝังอยู่.

```csharp
string htmlMarkup = beforeEdit.GetContent();
```

## วิธีการ **convert docx to html** ด้วยการจัดการแบบกำหนดเอง?
บางครั้งคุณอาจต้องปรับลิงก์ภายนอกให้ชี้ไปยังตัวจัดการทรัพยากรของคุณเอง.

## ขั้นตอนที่ 3: การปรับลิงก์ภายนอก
### ขั้นตอน 3.1: เตรียม Prefix ที่กำหนดเอง
เตรียม prefix ที่จะต่อหน้าลิงก์ภายนอกเดิม.

```csharp
string customImagesRequesthandlerUri = "http://example.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://example.com/CssHandler/id=";
string customFontsRequesthandlerUri = "http://example.com/FontsHandler/id=";
```

### ขั้นตอน 3.2: สร้าง HTML Markup ที่มี Prefix
สร้าง HTML markup พร้อมลิงก์ที่ปรับแล้ว.

```csharp
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```

### ขั้นตอน 3.3: รับเนื้อหา HTML เฉพาะ Body
บาง WYSIWYG editor จะจัดการเฉพาะ HTML markup ที่ไม่มีส่วนหัว.

```csharp
string onlyBodyContent = beforeEdit.GetBodyContent();
```

### ขั้นตอน 3.4: เนื้อหา Body‑Only ที่มี Prefix
สร้างเนื้อหาเฉพาะ body พร้อม prefix รูปภาพที่กำหนดเอง.

```csharp
string prefixedBodyContent = beforeEdit.GetBodyContent(customImagesRequesthandlerUri);
```

### ขั้นตอน 3.5: ดึง Stylesheets
ดึง Stylesheets ที่ใช้ในเอกสาร.

```csharp
List<string> stylesheets = beforeEdit.GetCssContent();
```

### ขั้นตอน 3.6: Stylesheets ที่มี Prefix
ดึง Stylesheets พร้อม prefix ที่กำหนดเอง.

```csharp
List<string> prefixedStylesheets = beforeEdit.GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri);
```

## วิธีการ **save document as html** อย่างถูกต้อง?
## ขั้นตอนที่ 4: บันทึกเอกสารเป็น HTML
Save the edited document as an HTML file, including its resources.

```csharp
string htmlFilePath = Path.Combine("output", Path.GetFileNameWithoutExtension(inputFilePath) + ".html");
beforeEdit.Save(htmlFilePath);
```

เมธอดนี้จะสร้างไดเรกทอรีแยกสำหรับทรัพยากร เช่น stylesheets, รูปภาพ, และฟอนต์.

## ขั้นตอนที่ 5: การทำลาย EditableDocument
`EditableDocument` implements `IDisposable` and provides the ability to check if the instance is disposed.

```csharp
Console.WriteLine("EditableDocument is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");
```

### ขั้นตอน 5.1 การจัดการเหตุการณ์ Dispose
คุณยังสามารถสมัครรับเหตุการณ์ disposing ได้.

```csharp
EventHandler someMethod = delegate { Console.WriteLine("Disposing event was spotted!"); };
beforeEdit.Disposed += someMethod;
```

## ขั้นตอนที่ 6: การสร้าง EditableDocument จาก HTML
Create an instance of `EditableDocument` from an HTML document.

### ขั้นตอน 6.1: จากไฟล์ HTML
```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
```

### ขั้นตอน 6.2: จาก HTML Markup
```csharp
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);
```

อินสแตนซ์เหล่านี้ (`afterEditFromFile` และ `afterEditFromMarkup`) จะเหมือนกับต้นฉบับ (`beforeEdit`).

## ขั้นตอนที่ 7: การทำลายด้วยตนเอง
Manually dispose of your `EditableDocument` instances.

```csharp
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```

ซึ่งจะทำให้การทำความสะอาดทรัพยากรเป็นไปอย่างเหมาะสม.

## ปัญหาที่พบบ่อยและวิธีแก้
- **รูปภาพไม่แสดงหลังการดึง:** ตรวจสอบว่าเอกสารมีรูปภาพฝังอยู่จริงและคุณกำลังเข้าถึง `beforeEdit.Images` หลังจากเรียก `Edit`.  
- **ฟอนต์หายไปในผลลัพธ์ HTML:** ตรวจสอบว่าคุณเรียก `GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri)` เพื่อฝัง URL ของฟอนต์อย่างถูกต้อง.  
- **สตริง HTML ขนาดใหญ่ทำให้ความดันหน่วยความจำ:** ใช้ `GetContent()` สำหรับ markup ที่ไม่มีทรัพยากรฝังอยู่และให้บริการรูปภาพ/CSS จากไฟล์แยก.

## คำถามที่พบบ่อย
**Q: GroupDocs.Editor รองรับรูปแบบไฟล์อะไรบ้าง?**  
A: GroupDocs.Editor รองรับ DOCX, XLSX, PPTX, และรูปแบบสำนักงานยอดนิยมอื่น ๆ อีกหลายรูปแบบ.

**Q: ฉันสามารถใช้ GroupDocs.Editor ได้โดยไม่มีไลเซนส์หรือไม่?**  
A: ใช่, คุณสามารถใช้ได้ด้วย [การทดลองใช้ฟรี](https://releases.groupdocs.com/) หรือ [ไลเซนส์ชั่วคราว](https://purchase.groupdocs.com/temporary-license/).

**Q: ฉันจะดึงทรัพยากรเฉพาะจากเอกสารได้อย่างไร?**  
A: ใช้คอลเลกชัน `Images`, `Fonts`, และ `Css` บนอินสแตนซ์ `EditableDocument`.

**Q: สามารถปรับลิงก์ในผลลัพธ์ HTML ได้หรือไม่?**  
A: ได้, ส่ง prefix URI ที่กำหนดเองไปยัง `GetContent` หรือ `GetBodyContent` เพื่อเขียนลิงก์รูปภาพ, CSS, และฟอนต์ใหม่.

**Q: ฉันจะบันทึกเอกสารที่แก้ไขเป็นไฟล์ HTML อย่างไร?**  
A: เรียกเมธอด `Save` บนอินสแตนซ์ `EditableDocument` โดยระบุเส้นทางไฟล์ที่ลงท้ายด้วย `.html`.

**อัปเดตล่าสุด:** 2026-03-14  
**ทดสอบกับ:** GroupDocs.Editor สำหรับ .NET (รุ่นล่าสุด)  
**ผู้เขียน:** GroupDocs