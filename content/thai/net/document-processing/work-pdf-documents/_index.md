---
title: ทำงานกับเอกสาร PDF
linktitle: ทำงานกับเอกสาร PDF
second_title: GroupDocs.Editor .NET API
description: เรียนรู้วิธีแก้ไขเอกสาร PDF โดยใช้ GroupDocs.Editor สำหรับ .NET ด้วยบทช่วยสอนนี้ แก้ไขเนื้อหา จัดการไฟล์ขนาดใหญ่ และบันทึกการแก้ไขของคุณอย่างปลอดภัย
weight: 14
url: /th/net/document-processing/work-pdf-documents/
---
## การแนะนำ
คุณกำลังมองหาคำแนะนำที่ครอบคลุมในการจัดการและแก้ไขเอกสาร PDF โดยใช้ GroupDocs.Editor สำหรับ .NET หรือไม่? คุณอยู่ในสถานที่ที่เหมาะสม! ในบทช่วยสอนนี้ เราจะแนะนำคุณตลอดกระบวนการทั้งหมด ตั้งแต่การตั้งค่าโปรเจ็กต์ไปจนถึงการบันทึกเอกสาร PDF ที่แก้ไขแล้ว ไม่ว่าคุณจะเป็นนักพัฒนาที่มีประสบการณ์หรือเพิ่งเริ่มต้น คุณจะพบว่าคู่มือนี้มีประโยชน์และง่ายต่อการปฏิบัติตาม มาดำน้ำกันเถอะ!
## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะเริ่ม มีบางสิ่งที่คุณต้องการ:
1. สภาพแวดล้อมการพัฒนา .NET: ตรวจสอบให้แน่ใจว่าคุณได้ตั้งค่าสภาพแวดล้อมการพัฒนา .NET แล้ว นี่อาจเป็น Visual Studio หรือ IDE ที่ต้องการอื่นๆ
2. GroupDocs.Editor สำหรับ .NET: ดาวน์โหลดและติดตั้งไลบรารี GroupDocs.Editor สำหรับ .NET คุณสามารถรับได้จาก[หน้าปล่อย](https://releases.groupdocs.com/editor/net/).
3. ความเข้าใจพื้นฐานของ C#: ความคุ้นเคยกับการเขียนโปรแกรม C# จะเป็นประโยชน์ เนื่องจากบทช่วยสอนนี้เกี่ยวข้องกับการเขียนและทำความเข้าใจโค้ด C#
## นำเข้าเนมสเปซ
ก่อนที่จะเขียนโค้ดใดๆ ตรวจสอบให้แน่ใจว่าคุณได้นำเข้าเนมสเปซที่จำเป็นในโครงการของคุณแล้ว:
```csharp
using System;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Reflection;
```
## ขั้นตอนที่ 1: รับเส้นทางไปยังไฟล์อินพุต
ขั้นแรก คุณต้องระบุเส้นทางไปยังเอกสาร PDF ของคุณ สำหรับบทช่วยสอนนี้ เราจะถือว่าคุณมีไฟล์ PDF ตัวอย่าง
```csharp
string inputFilePath = "Your Sample Document.pdf";
```
## ขั้นตอนที่ 2: สร้างสตรีมจากเส้นทาง
ถัดไป สร้างสตรีมไฟล์จากเส้นทางที่คุณระบุ สตรีมนี้จะใช้ในการอ่านเอกสาร PDF
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
```
## ขั้นตอนที่ 3: สร้างตัวเลือกการโหลดสำหรับเอกสาร
หากต้องการโหลดเอกสาร PDF คุณต้องระบุตัวเลือกการโหลด หาก PDF ของคุณมีการป้องกันด้วยรหัสผ่าน คุณสามารถระบุรหัสผ่านได้ที่นี่
```csharp
Options.PdfLoadOptions loadOptions = new PdfLoadOptions();
// หากเอกสารมีการป้องกันด้วยรหัสผ่าน
loadOptions.Password = "your_password";
```
## ขั้นตอนที่ 4: โหลดเอกสารลงในอินสแตนซ์ตัวแก้ไข
ตอนนี้ ให้ใช้ตัวเลือกสตรีมไฟล์และโหลดเพื่อโหลดเอกสารลงในไฟล์`Editor` ตัวอย่าง.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    var documentInfo = editor.GetDocumentInfo(null);
```
## ขั้นตอนที่ 5: สร้างตัวเลือกการแก้ไข
ตั้งค่าตัวเลือกการแก้ไขสำหรับเอกสาร ในกรณีนี้ เราจะเปิดใช้งานโหมดการแบ่งหน้า
```csharp
Options.PdfEditOptions editOptions = new PdfEditOptions();
editOptions.EnablePagination = true;
```
## ขั้นตอนที่ 6: สร้างเอกสารที่แก้ไขได้ระดับกลาง
สร้างเอกสารที่แก้ไขได้ระดับกลางโดยใช้อินสแตนซ์ตัวแก้ไขและตัวเลือกการแก้ไข
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
{
    // แยกเนื้อหาที่เป็นข้อความเป็นมาร์กอัป HTML
    string originalContent = beforeEdit.GetContent();
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## ขั้นตอนที่ 7: แก้ไขเนื้อหา
แก้ไขเนื้อหาของเอกสารตามความจำเป็น ที่นี่ เราเพียงแค่แทนที่คำในเอกสาร
```csharp
string editedContent = originalContent.Replace("document", "edited document");
```
## ขั้นตอนที่ 8: สร้างเอกสารที่แก้ไขได้ใหม่พร้อมเนื้อหาที่แก้ไข
 สร้างใหม่`EditableDocument` อินสแตนซ์ที่มีเนื้อหาและทรัพยากรที่แก้ไขแล้ว
```csharp
using (EditableDocument afterEdit = EditableDocument.FromMarkup(editedContent, allResources))
{
    string originalContent3 = afterEdit.GetContent();
```
## ขั้นตอนที่ 9: สร้างตัวเลือกการบันทึกเอกสาร
ระบุตัวเลือกการบันทึกสำหรับเอกสาร PDF คุณยังสามารถตั้งรหัสผ่านสำหรับเอกสารเอาต์พุตได้
```csharp
FixedLayoutFormats docmFormat = FixedLayoutFormats.Pdf;
Options.PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.Password = "output_password";
saveOptions.OptimizeMemoryUsage = true;
```
## ขั้นตอนที่ 10: บันทึกเอกสารที่แก้ไข
สุดท้าย ให้บันทึกเอกสารที่แก้ไขไปยังเส้นทางเอาต์พุตที่ระบุ
```csharp
string outputFilename = Path.GetFileNameWithoutExtension(inputFilePath) + "." + docmFormat.Extension;
string outputPath = Path.Combine("OutputDirectoryPath", outputFilename);
using (FileStream outputStream = File.Create(outputPath))
{
    editor.Save(afterEdit, outputStream, saveOptions);
}
```

## บทสรุป
ได้แล้ว! เมื่อทำตามขั้นตอนเหล่านี้ คุณจะแก้ไขเอกสาร PDF ได้สำเร็จโดยใช้ GroupDocs.Editor สำหรับ .NET ไลบรารีอันทรงพลังนี้ทำให้ง่ายต่อการจัดการและบันทึกไฟล์ PDF โดยทางโปรแกรม ไม่ว่าคุณจะทำการแทนที่ข้อความธรรมดาหรือแก้ไขที่ซับซ้อนมากขึ้น GroupDocs.Editor สำหรับ .NET ก็พร้อมให้ความช่วยเหลือ
## คำถามที่พบบ่อย
### ฉันสามารถใช้ GroupDocs.Editor สำหรับ .NET เพื่อแก้ไขรูปแบบเอกสารอื่นๆ ได้หรือไม่
ใช่ GroupDocs.Editor สำหรับ .NET รองรับรูปแบบเอกสารที่หลากหลาย รวมถึง Word, Excel, PowerPoint และอื่นๆ
### ฉันจะทดลองใช้ GroupDocs.Editor สำหรับ .NET ได้ฟรีได้อย่างไร
 คุณสามารถดาวน์โหลดรุ่นทดลองใช้ฟรีได้จาก[GroupDocs.Editor หน้าทดลองใช้ฟรี](https://releases.groupdocs.com/).
### เป็นไปได้ไหมที่จะจัดการเอกสาร PDF ขนาดใหญ่ด้วย GroupDocs.Editor สำหรับ .NET
ใช่ GroupDocs.Editor สำหรับ .NET มีตัวเลือกเพื่อเพิ่มประสิทธิภาพการใช้หน่วยความจำ ทำให้เหมาะสำหรับการจัดการเอกสารขนาดใหญ่
### ฉันจะได้รับความช่วยเหลือได้อย่างไรหากฉันประสบปัญหา
 สำหรับการสนับสนุนคุณสามารถเยี่ยมชมที่[ฟอรัมสนับสนุน GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).
### ฉันสามารถเข้ารหัสเอกสาร PDF ในขณะที่บันทึกได้หรือไม่
ได้ คุณสามารถตั้งรหัสผ่านเพื่อเข้ารหัสเอกสาร PDF ในระหว่างขั้นตอนการบันทึกโดยใช้`PdfSaveOptions.Password` คุณสมบัติ.