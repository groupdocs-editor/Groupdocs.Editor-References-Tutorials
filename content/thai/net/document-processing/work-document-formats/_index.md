---
title: ทำงานกับรูปแบบเอกสาร
linktitle: ทำงานกับรูปแบบเอกสาร
second_title: GroupDocs.Editor .NET API
description: เรียนรู้วิธีใช้ GroupDocs.Editor สำหรับ .NET เพื่อแก้ไขรูปแบบเอกสารต่างๆ โดยทางโปรแกรม คำแนะนำทีละขั้นตอนพร้อมตัวอย่างเพื่อการผสานรวมที่ราบรื่น
weight: 13
url: /th/net/document-processing/work-document-formats/
type: docs
---
# ทำงานกับรูปแบบเอกสาร

## การแนะนำ
ยินดีต้อนรับสู่คำแนะนำเชิงลึกเกี่ยวกับการใช้ GroupDocs.Editor สำหรับ .NET! หากคุณเป็นนักพัฒนาที่ต้องการปรับปรุงแอปพลิเคชันของคุณด้วยความสามารถในการแก้ไขเอกสาร คุณมาถูกที่แล้ว บทความนี้จะแนะนำทุกสิ่งที่คุณจำเป็นต้องรู้ ตั้งแต่ข้อกำหนดเบื้องต้นไปจนถึงตัวอย่างเชิงปฏิบัติ เพื่อช่วยให้คุณเริ่มต้นใช้งานไลบรารีอันทรงพลังนี้
## ข้อกำหนดเบื้องต้น
ก่อนที่จะเจาะลึกตัวอย่างและฟังก์ชันการทำงานของ GroupDocs.Editor สำหรับ .NET มีข้อกำหนดเบื้องต้นบางประการที่คุณต้องมี:
1. ความเข้าใจพื้นฐานของ .NET: ความคุ้นเคยกับ .NET Framework หรือ .NET Core เป็นสิ่งจำเป็น
2. สภาพแวดล้อมการพัฒนา: Visual Studio หรือ .NET IDE อื่น ๆ ที่เหมาะสม
3.  GroupDocs.Editor สำหรับ .NET Library: ดาวน์โหลดไลบรารีจากไฟล์[หน้าเผยแพร่ GroupDocs](https://releases.groupdocs.com/editor/net/).
4.  ใบอนุญาตชั่วคราว: รับ[ใบอนุญาตชั่วคราว](https://purchase.groupdocs.com/temporary-license/) เพื่อคุณสมบัติที่ครบครัน
## นำเข้าเนมสเปซ
หากต้องการเริ่มต้นใช้งาน GroupDocs.Editor สำหรับ .NET คุณจะต้องนำเข้าเนมสเปซที่จำเป็นลงในโปรเจ็กต์ของคุณ สิ่งนี้จะช่วยให้คุณสามารถเข้าถึงชั้นเรียนและวิธีการทั้งหมดที่ห้องสมุดจัดให้
```csharp
using System;
using GroupDocs.Editor.Options;
```

## ขั้นตอนที่ 1: การทำงานกับรูปแบบเอกสาร
GroupDocs.Editor รองรับรูปแบบเอกสารที่หลากหลาย มาดูกันว่าคุณสามารถแสดงรายการรูปแบบการประมวลผลคำและการนำเสนอที่รองรับทั้งหมดได้อย่างไร
### แสดงรายการรูปแบบการประมวลผลคำ
```csharp
foreach (Formats.WordProcessingFormats oneFormat in Formats.WordProcessingFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
คำอธิบาย:
1. รูปแบบวนซ้ำ: เราวนซ้ำผ่านรูปแบบการประมวลผลคำที่มีอยู่ทั้งหมด
2. รายละเอียดรูปแบบผลลัพธ์: สำหรับแต่ละรูปแบบ เราจะพิมพ์ชื่อและนามสกุลของมัน
### รูปแบบการนำเสนอรายการ
```csharp
foreach (Formats.PresentationFormats oneFormat in Formats.PresentationFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
คำอธิบาย:
1. รูปแบบวนซ้ำ: เช่นเดียวกับรูปแบบการประมวลผลคำ เราวนซ้ำทุกรูปแบบการนำเสนอ
2. รายละเอียดรูปแบบผลลัพธ์: พิมพ์ชื่อและนามสกุลของแต่ละรูปแบบ
## ขั้นตอนที่ 2: แยกวิเคราะห์รูปแบบจากส่วนขยาย
บางครั้ง คุณจำเป็นต้องกำหนดรูปแบบตามนามสกุลไฟล์ GroupDocs.Editor ทำให้สิ่งนี้เป็นเรื่องง่าย
### การแยกวิเคราะห์รูปแบบสเปรดชีต
```csharp
Formats.SpreadsheetFormats expectedXlsm = Formats.SpreadsheetFormats.FromExtension(".xlsm");
Console.WriteLine("Parsed Spreadsheet format is {0}", expectedXlsm.Name);
```
คำอธิบาย:
1. รูปแบบการแยกวิเคราะห์: เราใช้`FromExtension` วิธีการแยกวิเคราะห์รูปแบบจากไฟล์`.xlsm` ส่วนขยาย.
2. รูปแบบผลลัพธ์: พิมพ์ชื่อของรูปแบบที่แยกวิเคราะห์
### การแยกวิเคราะห์รูปแบบข้อความ
```csharp
Formats.TextualFormats expectedHtml = Formats.TextualFormats.FromExtension("html");
Console.WriteLine("Parsed Textual format is {0}", expectedHtml.Name);
```
คำอธิบาย:
1.  รูปแบบการแยกวิเคราะห์: The`FromExtension` วิธีการใช้ในการแยกวิเคราะห์รูปแบบจากไฟล์`html` ส่วนขยาย.
2. รูปแบบผลลัพธ์: พิมพ์ชื่อของรูปแบบข้อความที่แยกวิเคราะห์
## ขั้นตอนที่ 3: การแก้ไขเอกสาร
ตอนนี้เราได้เห็นวิธีการทำงานกับรูปแบบแล้ว เรามาเจาะลึกการแก้ไขเอกสารโดยใช้ GroupDocs.Editor กันดีกว่า
### กำลังโหลดเอกสาร
หากต้องการแก้ไขเอกสาร คุณต้องโหลดเอกสารก่อน
```csharp
using (Editor editor = new Editor("path/to/your/document.docx"))
{
    // ขั้นตอนเพิ่มเติมจะกล่าวถึงที่นี่
}
```
คำอธิบาย:
1.  เริ่มต้นตัวแก้ไข: สร้างอินสแตนซ์ของ`Editor` คลาสเพื่อระบุเส้นทางไปยังเอกสารของคุณ
2.  รูปแบบการกำจัด: ใช้`using` คำแถลงเพื่อให้แน่ใจว่าทรัพยากรถูกกำจัดอย่างเหมาะสม
### กำลังแยกเนื้อหา
เมื่อโหลดเอกสารแล้ว คุณสามารถแยกเนื้อหาเพื่อแก้ไขได้
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    string content = editableDocument.GetContent();
    Console.WriteLine(content);
}
```
คำอธิบาย:
1.  วิธีการแก้ไข: โทร`Edit` วิธีการรับไฟล์`EditableDocument`.
2.  รับเนื้อหา: การใช้งาน`GetContent` เพื่อดึงเนื้อหาของเอกสารเป็นสตริง
3. เนื้อหาเอาท์พุต: พิมพ์เนื้อหาไปยังคอนโซล
### กำลังบันทึกการเปลี่ยนแปลง
หลังจากแก้ไข ให้บันทึกการเปลี่ยนแปลงของคุณกลับไปยังเอกสาร
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    // แก้ไขเนื้อหาที่นี่
    SaveOptions saveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docx);
    editor.Save(editableDocument, "path/to/save/document.docx", saveOptions);
}
```
คำอธิบาย:
1.  วิธีการแก้ไข: โทร`Edit` วิธีการรับไฟล์`EditableDocument`.
2. แก้ไขเนื้อหา: แก้ไขเนื้อหาตามต้องการ (ไม่แสดงในตัวอย่างนี้)
3.  บันทึกตัวเลือก: สร้าง`SaveOptions` การระบุรูปแบบ
4.  บันทึกเอกสาร: ใช้`Save` วิธีการบันทึกเอกสารที่แก้ไข
## ขั้นตอนที่ 4: การทำงานกับเอกสารประเภทต่างๆ
GroupDocs.Editor รองรับเอกสารหลายประเภท ต่อไปนี้เป็นวิธีทำงานร่วมกับพวกเขา:
### การแก้ไขเอกสารสเปรดชีต
```csharp
using (Editor editor = new Editor("path/to/your/spreadsheet.xlsx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // แก้ไขเนื้อหาที่นี่
        SaveOptions saveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsx);
        editor.Save(editableDocument, "path/to/save/spreadsheet.xlsx", saveOptions);
    }
}
```
คำอธิบาย:
1.  เริ่มต้นตัวแก้ไข: สร้าง`Editor` อินสแตนซ์สำหรับสเปรดชีต
2.  วิธีการแก้ไข: โทร`Edit` เพื่อรับ`EditableDocument`.
3. รับเนื้อหา: ดึงและพิมพ์เนื้อหา
4. แก้ไขเนื้อหา: ทำการเปลี่ยนแปลงที่จำเป็น
5. ตัวเลือกการบันทึก: ระบุตัวเลือกการบันทึกสำหรับสเปรดชีต
6. บันทึกเอกสาร: บันทึกเอกสารที่แก้ไข
### การแก้ไขเอกสารการนำเสนอ
```csharp
using (Editor editor = new Editor("path/to/your/presentation.pptx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // แก้ไขเนื้อหาที่นี่
        SaveOptions saveOptions = new PresentationSaveOptions(PresentationFormats.Pptx);
        editor.Save(editableDocument, "path/to/save/presentation.pptx", saveOptions);
    }
}
```
คำอธิบาย:
1.  เริ่มต้นตัวแก้ไข: สร้าง`Editor` ตัวอย่างสำหรับการนำเสนอ
2.  วิธีการแก้ไข: โทร`Edit` เพื่อรับ`EditableDocument`.
3. รับเนื้อหา: ดึงและพิมพ์เนื้อหา
4. แก้ไขเนื้อหา: ทำการเปลี่ยนแปลงที่จำเป็น
5. ตัวเลือกการบันทึก: ระบุตัวเลือกการบันทึกสำหรับการนำเสนอ
6. บันทึกเอกสาร: บันทึกเอกสารที่แก้ไข
## บทสรุป
GroupDocs.Editor สำหรับ .NET มอบวิธีการที่มีประสิทธิภาพและยืดหยุ่นในการแก้ไขรูปแบบเอกสารต่างๆ โดยทางโปรแกรม ด้วยการทำตามคำแนะนำนี้ คุณสามารถรวมฟังก์ชันการแก้ไขเอกสารเข้ากับแอปพลิเคชัน .NET ของคุณได้อย่างมีประสิทธิภาพ เพิ่มขีดความสามารถ และมอบคุณค่าที่มากขึ้นให้กับผู้ใช้ของคุณ
## คำถามที่พบบ่อย
### GroupDocs.Editor สำหรับ .NET คืออะไร
GroupDocs.Editor สำหรับ .NET เป็นไลบรารีที่มีประสิทธิภาพซึ่งช่วยให้นักพัฒนาสามารถแก้ไขรูปแบบเอกสารต่างๆ โดยใช้โปรแกรมภายในแอปพลิเคชัน .NET ของตนได้
### ฉันจะเริ่มต้นใช้งาน GroupDocs.Editor สำหรับ .NET ได้อย่างไร
คุณต้องดาวน์โหลดไลบรารี รับใบอนุญาตชั่วคราว และตั้งค่าสภาพแวดล้อมการพัฒนาของคุณด้วยเนมสเปซที่จำเป็น
### รองรับเอกสารรูปแบบใดบ้าง?
GroupDocs.Editor รองรับการประมวลผลคำ สเปรดชีต การนำเสนอ และรูปแบบข้อความ และอื่นๆ อีกมากมาย
### ฉันสามารถใช้ GroupDocs.Editor ได้ฟรีหรือไม่
 คุณสามารถใช้ก[ทดลองฟรี](https://releases.groupdocs.com/) ด้วยคุณสมบัติที่จำกัดหรือได้รับ[ใบอนุญาตชั่วคราว](https://purchase.groupdocs.com/temporary-license/) เพื่อการเข้าถึงอย่างเต็มรูปแบบ
### ฉันจะหาแหล่งข้อมูลเพิ่มเติมและการสนับสนุนได้จากที่ไหน?
 เยี่ยมชม[เอกสาร GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/) สำหรับข้อมูลโดยละเอียดหรือตรวจสอบของพวกเขา[ฟอรั่มการสนับสนุน](https://forum.groupdocs.com/c/editor/20) เพื่อขอความช่วยเหลือ