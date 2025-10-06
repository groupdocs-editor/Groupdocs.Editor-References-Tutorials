---
title: บันทึกเอกสารที่แก้ไขแล้วเป็นรูปแบบต่างๆ
linktitle: บันทึกเอกสารที่แก้ไขแล้วเป็นรูปแบบต่างๆ
second_title: GroupDocs.Editor .NET API
description: เรียนรู้วิธีบันทึกเอกสารที่แก้ไขแล้วเป็นรูปแบบต่างๆ โดยใช้ GroupDocs.Editor สำหรับ .NET ในคำแนะนำทีละขั้นตอนที่ครอบคลุมนี้
weight: 11
url: /th/net/document-processing/save-edited-document-various-formats/
type: docs
---
# บันทึกเอกสารที่แก้ไขแล้วเป็นรูปแบบต่างๆ

## การแนะนำ
คุณต้องการบันทึกเอกสารที่แก้ไขแล้วเป็นรูปแบบต่างๆ โดยใช้ GroupDocs.Editor สำหรับ .NET หรือไม่? คุณมาถูกที่แล้ว! คู่มือที่ครอบคลุมนี้จะแนะนำคุณตลอดกระบวนการทั้งหมด ตั้งแต่การตั้งค่าสภาพแวดล้อมไปจนถึงการบันทึกเอกสารที่แก้ไขแล้วในรูปแบบต่างๆ มาเจาะลึกและแก้ไขเอกสารและประหยัดเงินได้ง่ายๆ เลย!
## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะเริ่ม ตรวจสอบให้แน่ใจว่าคุณมีสิ่งต่อไปนี้:
1.  GroupDocs.Editor สำหรับ .NET - ดาวน์โหลดเวอร์ชันล่าสุดจาก[ที่นี่](https://releases.groupdocs.com/editor/net/).
2. สภาพแวดล้อมการพัฒนา - Visual Studio หรือ IDE ที่รองรับ .NET อื่นๆ
3. .NET Framework - ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง .NET Framework 4.6.1 หรือสูงกว่า
4. เอกสารตัวอย่าง - ตัวอย่างเอกสาร WordProcessing ที่จะใช้งาน
5. ความรู้พื้นฐาน C# - จำเป็นต้องมีความคุ้นเคยกับการเขียนโปรแกรม C#
## นำเข้าเนมสเปซ
ในการเริ่มต้น ตรวจสอบให้แน่ใจว่าคุณนำเข้าเนมสเปซที่จำเป็นลงในโปรเจ็กต์ C# ของคุณ นี่เป็นสิ่งสำคัญสำหรับการเข้าถึงฟังก์ชัน GroupDocs.Editor
```csharp
using System;
using GroupDocs.Editor.Metadata;
```
เรามาแบ่งกระบวนการออกเป็นขั้นตอนที่สามารถจัดการได้ ปฏิบัติตามอย่างระมัดระวังเพื่อให้แน่ใจว่าคุณเข้าใจแต่ละส่วน
## ขั้นตอนที่ 1: รับเส้นทางไปยังไฟล์อินพุต
ขั้นแรก คุณต้องระบุเส้นทางไปยังไฟล์ WordProcessing อินพุตของคุณ ไฟล์นี้จะถูกโหลดและแก้ไข
```csharp
string inputFilePath = "Your Sample Document";
```
## ขั้นตอนที่ 2: สร้างตัวเลือกการโหลดสำหรับเอกสาร
จากนั้น สร้างตัวเลือกการโหลดเฉพาะสำหรับเอกสาร WordProcessing ตัวเลือกเหล่านี้จะช่วยปรับแต่งวิธีการโหลดเอกสาร
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
```
## ขั้นตอนที่ 3: โหลดเอกสารพร้อมตัวเลือก
 ตอนนี้ให้โหลดเอกสารลงในไฟล์`Editor` อินสแตนซ์โดยใช้ตัวเลือกการโหลดที่ระบุ
```csharp
using (Editor editor = new Editor(inputFilePath, delegate { return loadOptions; }))
```
## ขั้นตอนที่ 4: สร้างตัวเลือกการแก้ไข
เตรียมตัวเลือกการแก้ไขสำหรับเอกสาร ตัวเลือกเหล่านี้จะกำหนดวิธีการเปิดเอกสารเพื่อแก้ไข
```csharp
WordProcessingEditOptions editOptions = new WordProcessingEditOptions();
```
## ขั้นตอนที่ 5: เปิดเอกสารเพื่อการแก้ไข
 เปิดเอกสารเพื่อแก้ไขโดยสร้างไฟล์`EditableDocument`ตัวอย่าง. อินสแตนซ์นี้จะช่วยให้คุณสามารถเปลี่ยนแปลงเอกสารได้
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
```
## ขั้นตอนที่ 6: แก้ไขเนื้อหาเอกสาร
ถึงเวลาแก้ไขเนื้อหาของเอกสารแล้ว ขั้นแรก รับเอกสารเป็นสตริงที่เข้ารหัส base64 เดี่ยว
```csharp
string allEmbeddedInsideString = beforeEdit.GetEmbeddedHtml();
```
ตัวอย่างเช่น เรามาแก้ไขคำบรรยายในเอกสารกัน
```csharp
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
```
## ขั้นตอนที่ 7: สร้างเอกสารที่แก้ไขได้ใหม่จากเนื้อหาที่แก้ไข
 สร้างใหม่`EditableDocument` อินสแตนซ์จากเนื้อหาและทรัพยากรที่แก้ไข
```csharp
using (EditableDocument afterEdit = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null))
```
## ขั้นตอนที่ 8: บันทึกเอกสารเป็นรูปแบบต่างๆ
สุดท้าย ทำซ้ำรูปแบบ WordProcessing ที่รองรับทั้งหมด และบันทึกเอกสารที่แก้ไขแล้วในแต่ละรูปแบบ
```csharp
foreach (WordProcessingFormats oneFormat in WordProcessingFormats.All)
{
    // เตรียมตัวเลือกการบันทึก
    WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(oneFormat);
    // เตรียมเส้นทางบันทึก
    string savePath = Path.Combine("OutputDirectory", "MultipleOutFormats." + saveOptions.OutputFormat.Extension);
    // บันทึกเอกสาร
    editor.Save(afterEdit, savePath, saveOptions);
}
```
## ข้อความเสร็จสิ้น
เพื่อสรุป คุณสามารถพิมพ์ข้อความที่ระบุว่ากระบวนการเสร็จสิ้นเรียบร้อยแล้ว
```csharp
Console.WriteLine("SavingEditedDocumentToAllFormats routine has successfully finished");
```
## บทสรุป
ยินดีด้วย! คุณได้เรียนรู้วิธีบันทึกเอกสารที่แก้ไขเป็นรูปแบบต่างๆ โดยใช้ GroupDocs.Editor สำหรับ .NET เรียบร้อยแล้ว เครื่องมืออันทรงพลังนี้ทำให้ง่ายต่อการจัดการและบันทึกเอกสารในรูปแบบต่าง ๆ โดยใช้โค้ดเพียงไม่กี่บรรทัด โปรดจำไว้ว่า ขั้นตอนสำคัญเกี่ยวข้องกับการโหลดเอกสาร การแก้ไขเนื้อหา และการบันทึกในรูปแบบที่ต้องการ
## คำถามที่พบบ่อย
### GroupDocs.Editor สำหรับ .NET คืออะไร
GroupDocs.Editor สำหรับ .NET เป็น API ที่มีประสิทธิภาพซึ่งช่วยให้คุณสามารถแก้ไขเอกสารในรูปแบบต่างๆ ได้โดยใช้แอปพลิเคชัน .NET
### ฉันสามารถใช้ GroupDocs.Editor ได้ฟรีหรือไม่
 ใช่ คุณสามารถใช้งานได้แบบทดลองใช้ฟรี ดาวน์โหลดได้[ที่นี่](https://releases.groupdocs.com/).
### GroupDocs.Editor รองรับรูปแบบใดบ้าง
GroupDocs.Editor รองรับรูปแบบที่หลากหลาย รวมถึง DOCX, PDF, HTML และอื่นๆ อีกมากมาย
### ฉันจะได้รับใบอนุญาตชั่วคราวสำหรับ GroupDocs.Editor ได้อย่างไร
 คุณสามารถขอรับใบอนุญาตชั่วคราวได้[ที่นี่](https://purchase.groupdocs.com/temporary-license/).
### ฉันจะหาเอกสารและความช่วยเหลือเพิ่มเติมได้จากที่ไหน?
 มีเอกสารรายละเอียดให้[ที่นี่](https://tutorials.groupdocs.com/editor/net/) และคุณสามารถรับการสนับสนุนได้[ที่นี่](https://forum.groupdocs.com/c/editor/20).