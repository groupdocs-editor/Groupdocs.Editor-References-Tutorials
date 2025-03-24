---
title: แก้ไขการรวบรวมฟิลด์แบบฟอร์ม
linktitle: แก้ไขการรวบรวมฟิลด์แบบฟอร์ม
second_title: GroupDocs.Editor .NET API
description: เพิ่มประสิทธิภาพการแก้ไขเอกสารในโครงการ .NET ด้วย Groupdocs.Editor แก้ไขคอลเลกชันฟิลด์แบบฟอร์มได้อย่างราบรื่น
weight: 10
url: /th/net/form-field-management/edit-form-field-collection/
---
## การแนะนำ
Groupdocs.Editor สำหรับ .NET ช่วยให้นักพัฒนามีชุดคุณลักษณะที่มีประสิทธิภาพสำหรับการทำงานกับรูปแบบเอกสารต่างๆ ความสามารถอย่างหนึ่งคือความสามารถในการแก้ไขคอลเลกชันฟิลด์แบบฟอร์มภายในเอกสารได้อย่างราบรื่น ไม่ว่าคุณจะอัปเดตช่องข้อความหรือใช้การป้องกันเอกสาร Groupdocs.Editor จะเพิ่มความคล่องตัวให้กับกระบวนการ เพิ่มประสิทธิภาพและประสิทธิผล
## ข้อกำหนดเบื้องต้น
ก่อนที่จะเจาะลึกบทช่วยสอน ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้:
1.  Groupdocs.Editor สำหรับแพ็คเกจ .NET: ดาวน์โหลดและติดตั้งแพ็คเกจ Groupdocs.Editor สำหรับ .NET จาก[ที่นี่](https://releases.groupdocs.com/editor/net/).
2. เอกสารตัวอย่าง: เตรียมเอกสารตัวอย่างที่มีช่องแบบฟอร์มสำหรับการทดลอง
3. ความเข้าใจพื้นฐานของ C#: ทำความคุ้นเคยกับพื้นฐานภาษาการเขียนโปรแกรม C#

## การนำเข้าเนมสเปซ
เริ่มต้นด้วยการนำเข้าเนมสเปซที่จำเป็นเพื่อเข้าถึงฟังก์ชัน Groupdocs.Editor ในโปรเจ็กต์ C# ของคุณ
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System.IO;
```
## ขั้นตอนที่ 1: รับเส้นทางไฟล์อินพุต
```csharp
string inputFilePath = Constants.SampleLegacyFormFields_docx;
```
ในขั้นตอนนี้ ให้กำหนดเส้นทางไปยังไฟล์อินพุตที่มีฟิลด์แบบฟอร์มที่คุณต้องการแก้ไข
## ขั้นตอนที่ 2: สร้าง FileStream
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
    // รหัสของคุณที่นี่
}
```
 สร้างก`FileStream` จากเส้นทางไฟล์อินพุตเพื่อเข้าถึงเนื้อหา
## ขั้นตอนที่ 3: สร้างตัวเลือกการโหลด
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
loadOptions.Password = "some_password_to_open_a_document";
```
กำหนดค่าตัวเลือกการโหลดสำหรับเอกสาร เช่น การระบุรหัสผ่านสำหรับเอกสารที่มีการป้องกันด้วยรหัสผ่าน
## ขั้นตอนที่ 4: โหลดเอกสารลงในตัวแก้ไข
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    // รหัสของคุณที่นี่
}
```
โหลดเอกสารลงในอินสแตนซ์ Editor โดยใช้ตัวเลือก FileStream และโหลดที่มีให้
## ขั้นตอนที่ 5: เข้าถึงการรวบรวมฟิลด์แบบฟอร์ม
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
ดึงข้อมูล FormFieldCollection จากอินสแตนซ์ Editor เพื่อการจัดการเพิ่มเติม
## ขั้นตอนที่ 6: อัปเดตฟิลด์แบบฟอร์ม
```csharp
TextFormField textField = collection.GetFormField<TextFormField>("Text1");
textField.LocaleId = 1029;
textField.Value = "new Value";
fieldManager.UpdateFormFiled(collection);
```
อัปเดตฟิลด์แบบฟอร์มเฉพาะตามความจำเป็น ในตัวอย่างนี้ เราแก้ไขฟิลด์แบบฟอร์มข้อความ
## ขั้นตอนที่ 7: สร้างตัวเลือกการบันทึก
```csharp
WordProcessingFormats docFormat = WordProcessingFormats.Docx;
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(docFormat);
saveOptions.OptimizeMemoryUsage = true;
saveOptions.Protection = new WordProcessingProtection(WordProcessingProtectionType.AllowOnlyFormFields, "write_password");
```
กำหนดค่าตัวเลือกการบันทึกสำหรับเอกสาร การระบุรูปแบบ การเพิ่มประสิทธิภาพหน่วยความจำ และการตั้งค่าการป้องกันเอกสาร
## ขั้นตอนที่ 8: บันทึกเอกสาร
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(outputStream, saveOptions);
}
```
บันทึกเอกสารที่แก้ไข กำหนดเอาต์พุตไปยัง MemoryStream หรือไฟล์ตามความต้องการของคุณ

## บทสรุป
Groupdocs.Editor สำหรับ .NET ช่วยให้นักพัฒนาจัดการคอลเลกชันฟิลด์แบบฟอร์มภายในเอกสารได้อย่างราบรื่น เพิ่มประสิทธิภาพเวิร์กโฟลว์ เมื่อทำตามบทช่วยสอนนี้ คุณจะได้รับทักษะที่จำเป็นในการใช้ประโยชน์จากศักยภาพสูงสุดของไลบรารีอันทรงพลังนี้ในโครงการ .NET ของคุณ

## คำถามที่พบบ่อย
### Groupdocs.Editor เข้ากันได้กับเอกสารทุกรูปแบบหรือไม่
Groupdocs.Editor รองรับรูปแบบเอกสารที่หลากหลาย รวมถึง DOCX, XLSX, PPTX และอื่นๆ โปรดดูเอกสารประกอบสำหรับรายการที่ครอบคลุม
### ฉันสามารถปกป้องเอกสารโดยใช้ Groupdocs.Editor ได้หรือไม่
ใช่ Groupdocs.Editor อนุญาตให้คุณใช้กลไกการป้องกันเอกสารที่หลากหลาย รวมถึงการป้องกันด้วยรหัสผ่านและการจำกัดสิทธิ์ในการแก้ไข
### Groupdocs.Editor มีเวอร์ชันทดลองใช้งานสำหรับการประเมินผลหรือไม่
ใช่ คุณสามารถเข้าถึง Groupdocs.Editor รุ่นทดลองใช้ฟรีเพื่อสำรวจคุณสมบัติและความสามารถของ Groupdocs.Editor ก่อนตัดสินใจซื้อ
### Groupdocs.Editor อัพเดตบ่อยแค่ไหน?
Groupdocs อัปเดตผลิตภัณฑ์เป็นประจำเพื่อรวมคุณสมบัติใหม่ การปรับปรุง และการแก้ไขข้อบกพร่อง เพื่อให้มั่นใจถึงประสิทธิภาพและความน่าเชื่อถือสูงสุด
### มีการสนับสนุนด้านเทคนิคสำหรับผู้ใช้ Groupdocs.Editor หรือไม่
ใช่ Groupdocs ให้การสนับสนุนทางเทคนิคโดยเฉพาะเพื่อช่วยเหลือผู้ใช้เกี่ยวกับปัญหาหรือข้อสงสัยใดๆ ที่พวกเขาอาจพบขณะใช้งาน Groupdocs.Editor