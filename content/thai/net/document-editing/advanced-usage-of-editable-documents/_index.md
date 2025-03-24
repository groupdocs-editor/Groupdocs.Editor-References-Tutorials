---
title: การใช้งานขั้นสูงของเอกสารที่แก้ไขได้
linktitle: การใช้งานขั้นสูงของเอกสารที่แก้ไขได้
second_title: GroupDocs.Editor .NET API
description: เรียนรู้การใช้งานขั้นสูงของ GroupDocs.Editor สำหรับ .NET ในการสร้าง แก้ไข และแยกทรัพยากรออกจากเอกสารโดยทางโปรแกรม
weight: 11
url: /th/net/document-editing/advanced-usage-of-editable-documents/
---
## การแนะนำ
หากคุณเป็นนักพัฒนา .NET ที่ต้องการปรับปรุงความสามารถในการแก้ไขเอกสาร GroupDocs.Editor สำหรับ .NET มีชุดเครื่องมืออันทรงพลัง คู่มือที่ครอบคลุมนี้จะแนะนำการใช้งานขั้นสูงของเอกสารที่แก้ไขได้โดยใช้ GroupDocs.Editor โดยแจกแจงรายละเอียดแต่ละขั้นตอนเพื่อให้แน่ใจว่าคุณสามารถใช้ศักยภาพของเอกสารได้อย่างเต็มที่
## ข้อกำหนดเบื้องต้น
ก่อนที่จะเจาะลึกฟังก์ชันการทำงานขั้นสูง ตรวจสอบให้แน่ใจว่าคุณมีสิ่งต่อไปนี้:
- ติดตั้ง Visual Studio บนเครื่องพัฒนาของคุณ
- .NET Framework เข้ากันได้กับ GroupDocs.Editor
-  GroupDocs.Editor สำหรับไลบรารี .NET คุณสามารถ[ดาวน์โหลดได้ที่นี่](https://releases.groupdocs.com/editor/net/).
-  ใบอนุญาต GroupDocs.Editor ที่ถูกต้อง คุณจะได้รับ[ทดลองฟรี](https://releases.groupdocs.com/) หรือซื้อก[ใบอนุญาตชั่วคราว](https://purchase.groupdocs.com/temporary-license/).
## นำเข้าเนมสเปซ
ในการเริ่มต้น ตรวจสอบให้แน่ใจว่าคุณนำเข้าเนมสเปซที่จำเป็นในโปรเจ็กต์ .NET ของคุณ:
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
## ขั้นตอนที่ 1: การสร้างอินสแตนซ์เอกสารที่แก้ไขได้
 ก่อนอื่นคุณต้องสร้างอินสแตนซ์ของ`EditableDocument` โดยการโหลดและแก้ไขเอกสารอินพุตในรูปแบบที่รองรับ
```csharp
string inputFilePath = "YourSampleDocument.docx";
Editor editor = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```
ในขั้นตอนนี้ เราจะโหลดเอกสารอินพุตและเตรียมพร้อมสำหรับการแก้ไข
## ขั้นตอนที่ 2: แยกทรัพยากรเอกสาร
 ที่`EditableDocument` มีทรัพยากรต่าง ๆ ที่สามารถแยกและจัดการได้ มาทำลายสิ่งเหล่านี้กัน:
### ขั้นตอนที่ 2.1: แยกเอกสารทั้งหมดเป็น HTML
คุณสามารถสร้างสตริงเดียวที่มีทั้งเอกสารโดยมีทรัพยากรทั้งหมดฝังอยู่เป็น HTML
```csharp
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```
สตริงนี้จะค่อนข้างใหญ่เนื่องจากมีสไตล์ชีต รูปภาพ และแบบอักษรที่เข้ารหัสใน base64
### ขั้นตอนที่ 2.2: แยกรูปภาพทั้งหมด
แยกรูปภาพทั้งหมดออกจากเอกสาร
```csharp
List<IImageResource> allImages = beforeEdit.Images;
```
### ขั้นตอนที่ 2.3: แยกแบบอักษรทั้งหมด
แยกแบบอักษรทั้งหมดที่ใช้ในเอกสาร
```csharp
List<FontResourceBase> allFonts = beforeEdit.Fonts;
```
### ขั้นตอนที่ 2.4: แยกสไตล์ชีททั้งหมด
แยกสไตล์ชีตทั้งหมดในรูปแบบข้อความ
```csharp
List<CssText> allStylesheets = beforeEdit.Css;
```
### ขั้นตอนที่ 2.5: รวบรวมทรัพยากรทั้งหมด
รวบรวมทรัพยากรทั้งหมดในการโทรครั้งเดียว
```csharp
List<IHtmlResource> allResources = beforeEdit.AllResources;
```
ซึ่งรวมถึงรูปภาพ แบบอักษร และสไตล์ชีท
### ขั้นตอนที่ 2.6: รับมาร์กอัป HTML
รับมาร์กอัป HTML ของเอกสารโดยไม่มีทรัพยากรแบบฝัง
```csharp
string htmlMarkup = beforeEdit.GetContent();
```
## ขั้นตอนที่ 3: การปรับลิงค์ภายนอก
บางครั้ง คุณจำเป็นต้องปรับลิงก์ภายนอกให้ชี้ไปที่ตัวจัดการทรัพยากรแบบกำหนดเอง ต่อไปนี้เป็นวิธีดำเนินการ:
### ขั้นตอนที่ 3.1: เตรียมคำนำหน้าแบบกำหนดเอง
เตรียมคำนำหน้าที่จะนำหน้าลิงก์ภายนอกต้นฉบับ
```csharp
string customImagesRequesthandlerUri = "http://example.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://example.com/CssHandler/id = ";
string customFontsRequesthandlerUri = "http://example.com/FontsHandler/id=";
```
### ขั้นตอนที่ 3.2: สร้างมาร์กอัป HTML คำนำหน้า
สร้างมาร์กอัป HTML พร้อมลิงก์ที่ปรับเปลี่ยน
```csharp
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```
### ขั้นตอนที่ 3.3: รับเนื้อหา HTML เฉพาะเนื้อหา
โปรแกรมแก้ไขแบบ WYSIWYG บางตัวจัดการเฉพาะมาร์กอัป HTML ล้วนๆ โดยไม่มีส่วนหัว
```csharp
string onlyBodyContent = beforeEdit.GetBodyContent();
```
### ขั้นตอนที่ 3.4: คำนำหน้าเนื้อหาเฉพาะเนื้อหา
สร้างเนื้อหาเฉพาะเนื้อหาด้วยคำนำหน้ารูปภาพที่กำหนดเอง
```csharp
string prefixedBodyContent = beforeEdit.GetBodyContent(customImagesRequesthandlerUri);
```
### ขั้นตอนที่ 3.5: แยกสไตล์ชีท
แยกสไตล์ชีทที่ใช้ในเอกสาร
```csharp
List<string> stylesheets = beforeEdit.GetCssContent();
```
### ขั้นตอนที่ 3.6: คำนำหน้าสไตล์ชีต
แยกสไตล์ชีทด้วยคำนำหน้าที่กำหนดเอง
```csharp
List<string> prefixedStylesheets = beforeEdit.GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri);
```
## ขั้นตอนที่ 4: บันทึกเอกสารเป็น HTML
บันทึกเอกสารที่แก้ไขเป็นไฟล์ HTML รวมถึงทรัพยากรด้วย
```csharp
string htmlFilePath = Path.Combine("output", Path.GetFileNameWithoutExtension(inputFilePath) + ".html");
beforeEdit.Save(htmlFilePath);
```
เมธอดนี้จะสร้างไดเร็กทอรีแยกต่างหากสำหรับทรัพยากร เช่น สไตล์ชีต รูปภาพ และแบบอักษร
## ขั้นตอนที่ 5: การกำจัดเอกสารที่แก้ไขได้
 เอกสารที่แก้ไขได้นำไปใช้`IDisposable` และให้ความสามารถในการตรวจสอบว่าอินสแตนซ์ถูกกำจัดหรือไม่
```csharp
Console.WriteLine("EditableDocument is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");
```
### ขั้นตอนที่ 5.1 การจัดการเหตุการณ์การกำจัด
คุณยังสามารถสมัครรับเหตุการณ์การกำจัดได้
```csharp
EventHandler someMethod = delegate { Console.WriteLine("Disposing event was spotted!"); };
beforeEdit.Disposed += someMethod;
```
## ขั้นตอนที่ 6: การสร้างเอกสารที่แก้ไขได้จาก HTML
สร้างอินสแตนซ์ของ EditableDocument จากเอกสาร HTML
### ขั้นตอนที่ 6.1: จากไฟล์ HTML
```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
```
### ขั้นตอนที่ 6.2: จากมาร์กอัป HTML
```csharp
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);
```
อินสแตนซ์เหล่านี้ (afterEditFromFile และ afterEditFromMarkup) จะเหมือนกับอินสแตนซ์ดั้งเดิม (beforeEdit)
## ขั้นตอนที่ 7: การกำจัดด้วยตนเอง
กำจัดอินสแตนซ์ EditableDocument ของคุณด้วยตนเอง
```csharp
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```
สิ่งนี้ทำให้มั่นใจได้ถึงการล้างทรัพยากรอย่างเหมาะสม
## บทสรุป
GroupDocs.Editor สำหรับ .NET มีเครื่องมือที่มีประสิทธิภาพสำหรับการแก้ไขเอกสารโดยทางโปรแกรม ด้วยการทำตามคำแนะนำทีละขั้นตอนนี้ คุณสามารถจัดการเนื้อหาเอกสาร ทรัพยากร และรูปแบบเอาต์พุตได้อย่างมีประสิทธิภาพ ไม่ว่าคุณจะฝังทรัพยากร ปรับลิงก์ภายนอก หรือแปลงเอกสารเป็น HTML GroupDocs.Editor จะทำให้คุณมีฟังก์ชันที่จำเป็นสำหรับการจัดการเอกสารขั้นสูง
## คำถามที่พบบ่อย
### GroupDocs.Editor รองรับรูปแบบใดบ้าง
GroupDocs.Editor รองรับรูปแบบต่างๆ รวมถึง DOCX, XLSX, PPTX และอื่นๆ
### ฉันสามารถใช้ GroupDocs.Editor โดยไม่มีใบอนุญาตได้หรือไม่
 ใช่ คุณสามารถใช้มันกับ[ทดลองฟรี](https://releases.groupdocs.com/) หรือก[ใบอนุญาตชั่วคราว](https://purchase.groupdocs.com/temporary-license/).
### ฉันจะแยกทรัพยากรเฉพาะออกจากเอกสารได้อย่างไร
 คุณสามารถแยกรูปภาพ แบบอักษร และสไตล์ชีทได้โดยใช้วิธีการที่ให้ไว้ เช่น`Images`, `Fonts` , และ`Css`.
### เป็นไปได้หรือไม่ที่จะปรับลิงก์ในเอาต์พุต HTML?
ได้ คุณสามารถปรับลิงก์ภายนอกได้โดยการระบุคำนำหน้าแบบกำหนดเองสำหรับรูปภาพ, CSS และแบบอักษร
### ฉันจะบันทึกเอกสารที่แก้ไขแล้วเป็นไฟล์ HTML ได้อย่างไร
 ใช้`Save` วิธีการของ`EditableDocument`คลาสเพื่อบันทึกเอกสารเป็นไฟล์ HTML รวมถึงทรัพยากรด้วย