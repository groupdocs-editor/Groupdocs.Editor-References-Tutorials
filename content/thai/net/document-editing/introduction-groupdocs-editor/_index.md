---
title: ข้อมูลเบื้องต้นเกี่ยวกับ GroupDocs.Editor สำหรับ .NET
linktitle: ข้อมูลเบื้องต้นเกี่ยวกับ GroupDocs.Editor สำหรับ .NET
second_title: GroupDocs.Editor .NET API
description: เรียนรู้วิธีใช้ GroupDocs.Editor สำหรับ .NET เพื่อแก้ไขเอกสารโดยทางโปรแกรมพร้อมคำแนะนำทีละขั้นตอนโดยละเอียดนี้
weight: 12
url: /th/net/document-editing/introduction-groupdocs-editor/
---

# ข้อมูลเบื้องต้นเกี่ยวกับ GroupDocs.Editor สำหรับ .NET

## การแนะนำ 
หากคุณเป็นนักพัฒนาที่ต้องการรวมความสามารถในการแก้ไขเอกสารเข้ากับแอปพลิเคชัน .NET ของคุณได้อย่างราบรื่น GroupDocs.Editor สำหรับ .NET คือเครื่องมืออันทรงประสิทธิภาพที่ควรพิจารณา ไลบรารีอเนกประสงค์นี้ช่วยให้คุณสามารถโหลด แก้ไข และบันทึกรูปแบบเอกสารต่างๆ โดยทางโปรแกรม ไม่ว่าคุณจะต้องการจัดการเอกสาร Word, PDF หรือไฟล์ HTML GroupDocs.Editor จะทำให้กระบวนการง่ายขึ้น ทำให้มีประสิทธิภาพและตรงไปตรงมา ในบทช่วยสอนนี้ เราจะสำรวจพื้นฐานของการใช้ GroupDocs.Editor สำหรับ .NET ซึ่งจะแนะนำคุณตลอดตัวอย่างการใช้งานจริงทีละขั้นตอน
## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะเจาะลึกเรื่องการนำไปใช้งาน ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้:
- สภาพแวดล้อมการพัฒนา: Visual Studio 2017 หรือใหม่กว่า
- .NET Framework: .NET Framework 4.6.1 หรือใหม่กว่า
-  GroupDocs.Editor สำหรับ .NET: คุณทำได้[ดาวน์โหลด](https://releases.groupdocs.com/editor/net/) จากเว็บไซต์
-  ใบอนุญาต: ใบอนุญาตที่ถูกต้องหรือ[ใบอนุญาตชั่วคราว](https://purchase.groupdocs.com/temporary-license/) จาก GroupDocs
## นำเข้าเนมสเปซ
หากต้องการเริ่มใช้ GroupDocs.Editor สำหรับ .NET คุณจะต้องนำเข้าเนมสเปซที่จำเป็น เนมสเปซเหล่านี้จะให้การเข้าถึงคลาสและวิธีการที่จำเป็นสำหรับการแก้ไขเอกสาร
```csharp
using System;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```

ในส่วนนี้ เราจะแบ่งกระบวนการออกเป็นขั้นตอนที่สามารถจัดการได้ เพื่อให้แน่ใจว่าคุณเข้าใจแต่ละส่วนของขั้นตอนการทำงาน
## ขั้นตอนที่ 1: รับเส้นทางไปยังไฟล์อินพุต
ขั้นแรก คุณต้องระบุเส้นทางไปยังเอกสารที่คุณต้องการแก้ไข สำหรับตัวอย่างนี้ สมมติว่าคุณมีไฟล์ DOCX ชื่อ "Your Sample Document.docx"
```csharp
string inputFilePath = "Your Sample Document.docx";
```
## ขั้นตอนที่ 2: สร้างอินสแตนซ์ของวัตถุตัวแก้ไข
 ถัดไป สร้างอินสแตนซ์ของ`Editor` คลาสโดยการโหลดไฟล์อินพุต ขั้นตอนนี้จะเริ่มต้นเอกสารเพื่อการประมวลผลต่อไป
```csharp
using (GroupDocs.Editor.Editor editor = new Editor(inputFilePath))
{
    //ขั้นตอนต่อไปจะฝังอยู่ในบล็อกนี้
}
```
## ขั้นตอนที่ 3: เปิดเอกสารสำหรับการแก้ไข
 หากต้องการแก้ไขเอกสารให้ขอรับสื่อกลาง`EditableDocument` ตัวอย่าง. ออบเจ็กต์นี้ช่วยให้คุณสามารถจัดการเนื้อหาเอกสารและทรัพยากรที่เกี่ยวข้องได้
```csharp
EditableDocument beforeEdit = editor.Edit();
```
## ขั้นตอนที่ 4: ดึงเนื้อหาเอกสารและทรัพยากร
แยกเนื้อหาหลัก รูปภาพ แบบอักษร และสไตล์ชีตออกจากเอกสารที่แก้ไขได้ ข้อมูลนี้จำเป็นสำหรับการแก้ไขใดๆ
```csharp
string content = beforeEdit.GetContent();
var images = beforeEdit.Images;
var fonts = beforeEdit.Fonts;
var stylesheets = beforeEdit.Css;
```
### ขั้นตอนที่ 4.1: รับเอกสารเป็นสตริงที่เข้ารหัส Base64 เดี่ยว
คุณยังสามารถรับเนื้อหาเอกสารทั้งหมดเป็นสตริงที่เข้ารหัส base64 เดียว ซึ่งรวมถึงรีซอร์สทั้งหมด
```csharp
string allEmbeddedInsideString = beforeEdit.GetEmbeddedHtml();
```
### ขั้นตอนที่ 4.2: แก้ไขเนื้อหา
เพื่อวัตถุประสงค์ในการสาธิต ให้ปรับเปลี่ยนเนื้อหาเอกสารโดยการแทนที่ข้อความที่ระบุ
```csharp
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
```
## ขั้นตอนที่ 5: สร้างอินสแตนซ์เอกสารที่แก้ไขได้ใหม่
 หลังจากแก้ไขเนื้อหาแล้ว ให้สร้างเนื้อหาใหม่`EditableDocument` อินสแตนซ์ที่ใช้เนื้อหาที่แก้ไข
```csharp
EditableDocument afterEdit = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```
## ขั้นตอนที่ 6: บันทึกเอกสารที่แก้ไข
ตอนนี้ ให้บันทึกเอกสารที่แก้ไขแล้วเป็นรูปแบบผลลัพธ์ที่ต้องการ ในตัวอย่างนี้ เราจะบันทึกเป็นไฟล์ RTF
### ขั้นตอนที่ 6.1: เตรียมเส้นทางเอาต์พุต
ระบุเส้นทางที่คุณต้องการบันทึกเอกสารเอาต์พุต
```csharp
string outputPath = Path.Combine("Output Directory Path", Path.GetFileNameWithoutExtension(inputFilePath) + ".rtf");
```
### ขั้นตอนที่ 6.2: เตรียมตัวเลือกการบันทึก
กำหนดตัวเลือกการบันทึก โดยระบุรูปแบบที่คุณต้องการบันทึกเอกสาร
```csharp
Options.WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
```
### ขั้นตอนที่ 6.3: บันทึกไปยังพาธ
บันทึกเอกสารที่แก้ไขไปยังเส้นทางที่ระบุ
```csharp
editor.Save(afterEdit, outputPath, saveOptions);
```
### ขั้นตอนที่ 6.4: บันทึกไปยังสตรีม
หรือคุณสามารถบันทึกเอกสารเอาต์พุตลงในสตรีมที่สามารถเขียนได้
```csharp
using (MemoryStream ms = new MemoryStream())
{
    editor.Save(afterEdit, ms, saveOptions);
}
```
## ขั้นตอนที่ 7: กำจัดอินสแตนซ์ของตัวแก้ไขและเอกสารที่แก้ไขได้
 สุดท้ายให้ทำความสะอาดโดยการกำจัดทิ้ง`EditableDocument` กรณีและ`Editor` คัดค้านการเพิ่มทรัพยากร
```csharp
beforeEdit.Dispose();
afterEdit.Dispose();
editor.Dispose();
```

## บทสรุป
GroupDocs.Editor สำหรับ .NET ช่วยให้การรวมความสามารถในการแก้ไขเอกสารเข้ากับแอปพลิเคชันของคุณเป็นเรื่องง่ายอย่างเหลือเชื่อ ด้วยการทำตามขั้นตอนที่ระบุไว้ในบทช่วยสอนนี้ คุณสามารถโหลด แก้ไข และบันทึกเอกสารโดยทางโปรแกรมได้โดยใช้ความพยายามเพียงเล็กน้อย ไม่ว่าคุณจะต้องการจัดการเอกสาร Word, PDF หรือรูปแบบอื่นๆ GroupDocs.Editor นำเสนอโซลูชันที่มีประสิทธิภาพสำหรับความต้องการในการประมวลผลเอกสารของคุณ
## คำถามที่พบบ่อย
### ฉันสามารถแก้ไขไฟล์ PDF โดยใช้ GroupDocs.Editor สำหรับ .NET ได้หรือไม่
ใช่ GroupDocs.Editor สำหรับ .NET รองรับการแก้ไขไฟล์ PDF พร้อมกับรูปแบบอื่นๆ มากมาย เช่น DOCX, HTML และอื่นๆ
### ฉันจะได้รับใบอนุญาตชั่วคราวสำหรับ GroupDocs.Editor สำหรับ .NET ได้อย่างไร
 คุณสามารถขอรับใบอนุญาตชั่วคราวได้จาก[เว็บไซต์กรุ๊ปดอคส์](https://purchase.groupdocs.com/temporary-license/).
### GroupDocs.Editor สำหรับ .NET รองรับไฟล์รูปแบบใดบ้าง
GroupDocs.Editor สำหรับ .NET รองรับรูปแบบต่างๆ รวมถึง DOCX, PDF, HTML และ RTF และอื่นๆ อีกมากมาย
### เป็นไปได้หรือไม่ที่จะผสานรวม GroupDocs.Editor เข้ากับพื้นที่เก็บข้อมูลบนคลาวด์
ได้ คุณสามารถผสานรวม GroupDocs.Editor เข้ากับโซลูชันพื้นที่เก็บข้อมูลบนคลาวด์ต่างๆ เพื่อจัดการเอกสารของคุณได้
### ฉันจะหาเอกสารสำหรับ GroupDocs.Editor สำหรับ .NET ได้ที่ไหน
เอกสารก็มีให้[ที่นี่](https://tutorials.groupdocs.com/editor/net/).