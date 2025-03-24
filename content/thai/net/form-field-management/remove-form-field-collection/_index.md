---
title: ลบคอลเลกชันฟิลด์แบบฟอร์ม
linktitle: ลบคอลเลกชันฟิลด์แบบฟอร์ม
second_title: GroupDocs.Editor .NET API
description: เรียนรู้วิธีลบฟิลด์แบบฟอร์มออกจากเอกสาร Word โดยใช้ GroupDocs.Editor สำหรับ .NET พร้อมคำแนะนำทีละขั้นตอนนี้ เหมาะสำหรับนักพัฒนา
weight: 13
url: /th/net/form-field-management/remove-form-field-collection/
---

# ลบคอลเลกชันฟิลด์แบบฟอร์ม

## การแนะนำ
คุณต้องการจัดการฟิลด์แบบฟอร์มในเอกสารของคุณโดยทางโปรแกรมหรือไม่? GroupDocs.Editor สำหรับ .NET นำเสนอโซลูชันอันทรงพลังในการจัดการและจัดการฟิลด์แบบฟอร์มในรูปแบบเอกสารต่างๆ ในบทช่วยสอนนี้ เราจะแนะนำคุณตลอดขั้นตอนในการลบคอลเลกชันฟิลด์แบบฟอร์มออกจากเอกสาร Word โดยใช้ไลบรารีที่มีประสิทธิภาพนี้ 
## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะเจาะลึกโค้ด เรามาตรวจสอบให้แน่ใจว่าคุณได้ตั้งค่าทุกอย่างแล้วเพื่อประสบการณ์ที่ราบรื่น:
1. GroupDocs.Editor สำหรับ .NET: ตรวจสอบให้แน่ใจว่าคุณได้ดาวน์โหลดและติดตั้ง GroupDocs.Editor สำหรับ .NET แล้ว ถ้าไม่คุณสามารถดาวน์โหลดได้[ที่นี่](https://releases.groupdocs.com/editor/net/).
2. สภาพแวดล้อมการพัฒนา: คุณจะต้องมีสภาพแวดล้อมการพัฒนาเช่น Visual Studio
3. .NET Framework: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง .NET Framework บนเครื่องของคุณ
4.  เอกสารตัวอย่าง: มีตัวอย่างเอกสาร Word (เช่น`SampleLegacyFormFields.docx`) ด้วยช่องแบบฟอร์มที่คุณต้องการจัดการ

## นำเข้าเนมสเปซ
ในการเริ่มต้น คุณต้องนำเข้าเนมสเปซที่จำเป็นในโปรเจ็กต์ .NET ของคุณ ซึ่งจะช่วยให้คุณสามารถเข้าถึงฟังก์ชัน GroupDocs.Editor ได้
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System.IO;
```
## ขั้นตอนที่ 1: โหลดเอกสาร
ขั้นแรก คุณจะต้องโหลดเอกสารที่คุณต้องการแก้ไข มาทำลายมันกัน:
### ขั้นตอนที่ 1.1: รับเส้นทางไปยังไฟล์อินพุต
 คุณต้องระบุเส้นทางไปยังไฟล์อินพุตของคุณ สำหรับตัวอย่างนี้ เราจะใช้ไฟล์ตัวอย่างที่เรียกว่า`SampleLegacyFormFields.docx`.
```csharp
string inputFilePath = "path/to/SampleLegacyFormFields.docx";
```
### ขั้นตอนที่ 1.2: สร้าง FileStream จากเส้นทาง
 ต่อไปสร้างก`FileStream` เพื่ออ่านเอกสาร
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
    // ทำตามขั้นตอนถัดไปโดยใช้บล็อกนี้
}
```
## ขั้นตอนที่ 2: ตั้งค่าตัวเลือกการโหลด
เมื่อโหลดเอกสาร คุณอาจต้องระบุตัวเลือกการโหลด โดยเฉพาะอย่างยิ่งหากเอกสารของคุณมีการป้องกันด้วยรหัสผ่าน
### ขั้นตอนที่ 2.1: สร้างตัวเลือกการโหลด
 สร้างอินสแตนซ์ของ`WordProcessingLoadOptions`.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
```
### ขั้นตอนที่ 2.2: ระบุรหัสผ่าน (หากจำเป็น)
หากเอกสารของคุณมีการป้องกันด้วยรหัสผ่าน คุณสามารถระบุรหัสผ่านได้
```csharp
loadOptions.Password = "some_password_to_open_a_document";
```
## ขั้นตอนที่ 3: โหลดเอกสารลงในตัวแก้ไข
 ตอนนี้โหลดเอกสารลงใน`Editor` อินสแตนซ์ที่ใช้`FileStream` และ`LoadOptions`.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    // ทำตามขั้นตอนถัดไปโดยใช้บล็อกนี้
}
```
## ขั้นตอนที่ 4: เข้าถึงและจัดการฟิลด์แบบฟอร์ม
เมื่อโหลดเอกสารแล้ว คุณสามารถเข้าถึงและจัดการฟิลด์แบบฟอร์มได้แล้ว
### ขั้นตอนที่ 4.1: อ่าน FormFieldManager
 ดึงข้อมูล`FormFieldManager` จาก`Editor` ตัวอย่าง.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
### ขั้นตอนที่ 4.2: เข้าถึง FormFieldCollection
 รับ`FormFieldCollection` ซึ่งมีฟิลด์แบบฟอร์มทั้งหมดในเอกสาร
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
### ขั้นตอนที่ 4.3: ลบฟิลด์แบบฟอร์มข้อความเฉพาะ
หากต้องการลบฟิลด์ฟอร์มข้อความเฉพาะ ให้ค้นหาตามชื่อแล้วลบออก
```csharp
TextFormField textField = collection.GetFormField<TextFormField>("Text1");
fieldManager.RemoveFormFiled(textField);
```
### ขั้นตอนที่ 4.4: ลบฟิลด์แบบฟอร์มหลายรายการ
คุณยังสามารถลบฟิลด์แบบฟอร์มหลายรายการพร้อมกันได้โดยการระบุชื่อ
```csharp
textField = collection.GetFormField<TextFormField>("Text7");
CheckBoxForm checkBoxForm = collection.GetFormField<CheckBoxForm>("Check2");
fieldManager.RemoveFormFields(new IFormField[] { textField, checkBoxForm });
```
## ขั้นตอนที่ 5: บันทึกเอกสารที่แก้ไข
หลังจากแก้ไขฟิลด์แบบฟอร์มแล้ว คุณจะต้องบันทึกเอกสาร
### ขั้นตอนที่ 5.1: สร้างตัวเลือกการบันทึก
ระบุรูปแบบและบันทึกตัวเลือกสำหรับเอกสารเอาต์พุต
```csharp
WordProcessingFormats docFormat = WordProcessingFormats.Docx;
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(docFormat);
```
### ขั้นตอนที่ 5.2: ปรับการใช้หน่วยความจำให้เหมาะสม
หากต้องจัดการกับเอกสารขนาดใหญ่ คุณอาจต้องการปรับการใช้หน่วยความจำให้เหมาะสม
```csharp
saveOptions.OptimizeMemoryUsage = true;
```
### ขั้นตอนที่ 5.3: ตั้งค่าการป้องกัน (หากจำเป็น)
คุณสามารถป้องกันเอกสารจากการแก้ไขเพิ่มเติมได้โดยการตั้งค่ารหัสผ่านการเขียน
```csharp
saveOptions.Protection = new WordProcessingProtection(WordProcessingProtectionType.AllowOnlyFormFields, "write_password");
```
### ขั้นตอนที่ 5.4: บันทึกเอกสาร
 สุดท้าย ให้บันทึกเอกสารโดยใช้ไฟล์`MemoryStream`.
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(outputStream, saveOptions);
}
```

## บทสรุป
ยินดีด้วย! คุณได้ลบเขตข้อมูลแบบฟอร์มออกจากเอกสาร Word เรียบร้อยแล้วโดยใช้ GroupDocs.Editor สำหรับ .NET ไลบรารีอันทรงพลังนี้ทำให้การจัดการเนื้อหาเอกสารโดยทางโปรแกรมเป็นเรื่องง่าย ช่วยให้คุณประหยัดเวลาและความพยายาม
## คำถามที่พบบ่อย
### ฉันสามารถใช้ GroupDocs.Editor สำหรับ .NET กับเอกสารรูปแบบอื่นได้หรือไม่
ใช่ GroupDocs.Editor สำหรับ .NET รองรับรูปแบบเอกสารที่หลากหลาย รวมถึง PDF, HTML และอื่นๆ
### เป็นไปได้หรือไม่ที่จะเพิ่มฟิลด์แบบฟอร์มโดยใช้ GroupDocs.Editor สำหรับ .NET
ได้ คุณสามารถเพิ่ม แก้ไข และลบฟิลด์แบบฟอร์มโดยทางโปรแกรมได้
### จะเกิดอะไรขึ้นหากเอกสารของฉันมีขนาดใหญ่มาก?
คุณสามารถเปิดใช้งานการเพิ่มประสิทธิภาพหน่วยความจำในตัวเลือกการบันทึกเพื่อจัดการเอกสารขนาดใหญ่ได้อย่างมีประสิทธิภาพ
### ฉันสามารถใช้ GroupDocs.Editor สำหรับ .NET ในเว็บแอปพลิเคชันได้หรือไม่
อย่างแน่นอน! GroupDocs.Editor สำหรับ .NET สามารถรวมเข้ากับเว็บแอปพลิเคชันสำหรับการประมวลผลเอกสารฝั่งเซิร์ฟเวอร์ได้
### ฉันจะรับการสนับสนุนได้ที่ไหนหากฉันประสบปัญหา
 ท่านสามารถเยี่ยมชมได้ที่[ฟอรั่มการสนับสนุน](https://forum.groupdocs.com/c/editor/20) เพื่อช่วยเหลือในประเด็นต่างๆ