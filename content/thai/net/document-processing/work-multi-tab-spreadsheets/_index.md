---
title: ทำงานกับสเปรดชีตแบบหลายแท็บ
linktitle: ทำงานกับสเปรดชีตแบบหลายแท็บ
second_title: GroupDocs.Editor .NET API
description: เรียนรู้วิธีทำงานกับสเปรดชีตแบบหลายแท็บใน .NET โดยใช้ GroupDocs.Editor รวมคำแนะนำทีละขั้นตอน ตัวอย่างโค้ด และแนวทางปฏิบัติที่ดีที่สุด
weight: 17
url: /th/net/document-processing/work-multi-tab-spreadsheets/
---
## การแนะนำ
การจัดการสเปรดชีตแบบหลายแท็บอาจเป็นงานที่ค่อนข้างยาก โดยเฉพาะอย่างยิ่งเมื่อคุณต้องการจัดการหรือแยกข้อมูลจากชีตต่างๆ ภายในเอกสารเดียวกัน หากคุณกำลังทำงานกับ .NET และกำลังมองหาโซลูชันที่มีประสิทธิภาพ GroupDocs.Editor สำหรับ .NET เป็นตัวเลือกที่ยอดเยี่ยม ในบทช่วยสอนนี้ เราจะแนะนำคุณตลอดกระบวนการทำงานกับสเปรดชีตแบบหลายแท็บโดยใช้ GroupDocs.Editor สำหรับ .NET เราจะครอบคลุมทุกอย่างตั้งแต่การตั้งค่าสภาพแวดล้อมของคุณไปจนถึงการบันทึกแต่ละแท็บเป็นไฟล์แยกต่างหาก
## ข้อกำหนดเบื้องต้น
ก่อนที่จะเข้าสู่บทช่วยสอน ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้:
1. Visual Studio: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Visual Studio บนเครื่องของคุณ
2. .NET Framework: GroupDocs.Editor สำหรับ .NET รองรับ .NET Framework 4.0 หรือสูงกว่า
3. GroupDocs.Editor สำหรับ .NET: ดาวน์โหลดและติดตั้งไลบรารี GroupDocs.Editor สำหรับ .NET คุณสามารถรับได้จาก[หน้าดาวน์โหลด](https://releases.groupdocs.com/editor/net/).
4.  ใบอนุญาต: ในขณะที่คุณสามารถใช้ไฟล์[ใบอนุญาตชั่วคราว](https://purchase.groupdocs.com/temporary-license/) หากต้องการลองใช้ห้องสมุด ขอแนะนำให้ซื้อใบอนุญาตฉบับสมบูรณ์สำหรับการใช้งานจริง
## นำเข้าเนมสเปซ
ก่อนที่เราจะเริ่มเขียนโค้ด คุณต้องนำเข้าเนมสเปซที่จำเป็นก่อน เพิ่มคำสั่งต่อไปนี้ที่ด้านบนของไฟล์ .cs ของคุณ:
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
## 1. รับเส้นทางไปยังไฟล์อินพุต
ขั้นแรก คุณต้องระบุเส้นทางไปยังไฟล์สเปรดชีตอินพุตของคุณ ไฟล์นี้ควรเป็น XLSX (OOXML) ที่มีหลายแท็บ
```csharp
string inputFilePath = "Your Sample Document";
```
## 2. โหลดสเปรดชีตลงในอินสแตนซ์ของตัวแก้ไข
 ต่อไป คุณจะโหลดสเปรดชีตลงใน`Editor` ตัวอย่าง. ซึ่งทำได้โดยใช้สตรีมไฟล์และระบุตัวเลือกการโหลดที่เหมาะสมสำหรับสเปรดชีต
```csharp
using (FileStream inputStream = File.OpenRead(inputFilePath))
{
    using (Editor editor = new Editor(delegate { return inputStream; }, delegate { return new SpreadsheetLoadOptions(); }))
    {
        // ขั้นตอนต่อไปจะไปที่นี่
    }
}
```
## 3. สร้างเอกสารที่แก้ไขได้จากแท็บแรก
 หากต้องการแก้ไขหรือจัดการแท็บใดแท็บหนึ่ง คุณจะต้องสร้าง`EditableDocument` อินสแตนซ์สำหรับแท็บนั้น แท็บถูกระบุโดยใช้ดัชนีแบบ 0
```csharp
SpreadsheetEditOptions editOptions1 = new SpreadsheetEditOptions();
editOptions1.WorksheetIndex = 0; // แท็บแรก
EditableDocument firstTabBeforeEdit = editor.Edit(editOptions1);
```
## 4. สร้างเอกสารที่แก้ไขได้จากแท็บที่สอง
 ในทำนองเดียวกัน ให้สร้างไฟล์`EditableDocument` สำหรับแท็บที่สอง
```csharp
SpreadsheetEditOptions editOptions2 = new SpreadsheetEditOptions();
editOptions2.WorksheetIndex = 1; // แท็บที่สอง
EditableDocument secondTabBeforeEdit = editor.Edit(editOptions2);
```
## 5. บันทึกแท็บแรกลงในเอกสารแยกต่างหาก
ตอนนี้ ให้บันทึกแท็บแรกเป็นเอกสารแยกต่างหาก ระบุรูปแบบการบันทึกและเส้นทางเอาต์พุต
```csharp
SpreadsheetSaveOptions saveOptions1 = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
string outputFilename1 = Path.GetFileNameWithoutExtension(inputFilePath) + "_tab1.xlsm";
string outputPath1 = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename1);
editor.Save(firstTabBeforeEdit, outputPath1, saveOptions1);
```
## 6. บันทึกแท็บที่สองลงในเอกสารแยกต่างหาก
ทำซ้ำขั้นตอนสำหรับแท็บที่สอง แต่คราวนี้ให้บันทึกในรูปแบบอื่น
```csharp
SpreadsheetSaveOptions saveOptions2 = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsb);
string outputFilename2 = Path.GetFileNameWithoutExtension(inputFilePath) + "_tab2.xlsb";
string outputPath2 = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename2);
editor.Save(secondTabBeforeEdit, outputPath2, saveOptions2);
```
## 7. กำจัดอินสแตนซ์เอกสารที่แก้ไขได้
 สุดท้ายนี้ ตรวจสอบให้แน่ใจว่าคุณกำจัดทิ้งอย่างถูกต้อง`EditableDocument` อินสแตนซ์เพื่อเพิ่มทรัพยากร
```csharp
firstTabBeforeEdit.Dispose();
secondTabBeforeEdit.Dispose();
```

## บทสรุป
เมื่อทำตามขั้นตอนเหล่านี้ คุณจะทำงานกับสเปรดชีตแบบหลายแท็บใน .NET โดยใช้ GroupDocs.Editor ได้อย่างง่ายดาย ไลบรารีอันทรงพลังนี้ทำให้กระบวนการแก้ไขและบันทึกชีตต่างๆ ภายในสเปรดชีตง่ายขึ้น ทำให้งานการพัฒนาของคุณสามารถจัดการได้ง่ายขึ้น ไม่ว่าคุณจะจัดการกับการจัดการข้อมูลที่ซับซ้อนหรือการแก้ไขแบบง่ายๆ GroupDocs.Editor สำหรับ .NET ก็มีเครื่องมือที่คุณต้องการเพื่อให้งานสำเร็จลุล่วงได้อย่างมีประสิทธิภาพ
## คำถามที่พบบ่อย
### GroupDocs.Editor สำหรับ .NET คืออะไร
GroupDocs.Editor สำหรับ .NET เป็น API การแก้ไขเอกสารที่มีประสิทธิภาพซึ่งช่วยให้นักพัฒนาโหลด แก้ไข และบันทึกเอกสารในรูปแบบต่างๆ ภายในแอปพลิเคชัน .NET
### ฉันสามารถลองใช้ GroupDocs.Editor สำหรับ .NET ก่อนซื้อได้หรือไม่
 ใช่ คุณสามารถใช้[ทดลองฟรี](https://releases.groupdocs.com/) หรือขอ[ใบอนุญาตชั่วคราว](https://purchase.groupdocs.com/temporary-license/) เพื่อประเมินผลิตภัณฑ์
### GroupDocs.Editor สำหรับ .NET รองรับไฟล์รูปแบบใดบ้าง
GroupDocs.Editor รองรับรูปแบบที่หลากหลาย รวมถึง DOCX, XLSX, PPTX, PDF และอื่นๆ อีกมากมาย
### ฉันจะรับการสนับสนุนสำหรับ GroupDocs.Editor สำหรับ .NET ได้อย่างไร
 คุณสามารถรับการสนับสนุนได้โดยไปที่[ฟอรั่มการสนับสนุน](https://forum.groupdocs.com/c/editor/20).
### ฉันจะซื้อใบอนุญาตฉบับเต็มสำหรับ GroupDocs.Editor สำหรับ .NET ได้ที่ไหน
 คุณสามารถซื้อใบอนุญาตฉบับสมบูรณ์ได้จาก[หน้าซื้อ](https://purchase.groupdocs.com/buy).