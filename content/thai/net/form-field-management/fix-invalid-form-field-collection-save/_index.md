---
title: แก้ไขการรวบรวมและบันทึกฟิลด์แบบฟอร์มที่ไม่ถูกต้อง
linktitle: แก้ไขการรวบรวมและบันทึกฟิลด์แบบฟอร์มที่ไม่ถูกต้อง
second_title: GroupDocs.Editor .NET API
description: เรียนรู้วิธีแก้ไขช่องแบบฟอร์มที่ไม่ถูกต้องใน DOCX โดยใช้ Groupdocs.Editor สำหรับ .NET ปฏิบัติตามคำแนะนำนี้เพื่อให้แน่ใจว่าเอกสารของคุณปราศจากข้อผิดพลาดและบันทึกไว้อย่างปลอดภัย
weight: 11
url: /th/net/form-field-management/fix-invalid-form-field-collection-save/
---
## การแนะนำ
ยินดีต้อนรับ! หากคุณกำลังทำงานกับช่องแบบฟอร์มในเอกสารและประสบปัญหาเกี่ยวกับคอลเลกชันช่องแบบฟอร์มที่ไม่ถูกต้อง แสดงว่าคุณมาถูกที่แล้ว ในบทช่วยสอนนี้ เราจะเจาะลึกวิธีแก้ไขฟิลด์แบบฟอร์มที่ไม่ถูกต้อง และบันทึกเอกสารของคุณโดยใช้ Groupdocs.Editor สำหรับ .NET เราจะแนะนำคุณตลอดกระบวนการทีละขั้นตอน เพื่อให้มั่นใจว่าคุณมีรายละเอียดทั้งหมดที่จำเป็นเพื่อให้ทำงานได้อย่างราบรื่น มาเริ่มกันเลย!
## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะพูดถึงโค้ด มีบางสิ่งที่คุณต้องมี:
-  Groupdocs.Editor สำหรับ .NET: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้งไลบรารี Groupdocs.Editor สำหรับ .NET แล้ว คุณสามารถดาวน์โหลดได้[ที่นี่](https://releases.groupdocs.com/editor/net/).
- สภาพแวดล้อมการพัฒนา: คุณควรตั้งค่าสภาพแวดล้อมการพัฒนา .NET เช่น Visual Studio
- ความรู้พื้นฐานของ C#: บทช่วยสอนนี้ถือว่าคุณมีความเข้าใจพื้นฐานเกี่ยวกับการเขียนโปรแกรม C#
## นำเข้าเนมสเปซ
ขั้นแรก คุณต้องนำเข้าเนมสเปซที่จำเป็นในโปรเจ็กต์ C# ของคุณ เพิ่มบรรทัดต่อไปนี้ที่จุดเริ่มต้นของไฟล์โค้ดของคุณ:
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System;
using System.IO;
```
## ขั้นตอนที่ 1: รับเส้นทางไฟล์อินพุต
ขั้นตอนแรกคือการระบุเส้นทางไปยังไฟล์อินพุตของคุณ ไฟล์นี้ควรเป็นเอกสาร DOCX ที่มีฟิลด์แบบฟอร์ม
```csharp
string inputFilePath = Constants.SampleLegacyFormFields_docx;
```
## ขั้นตอนที่ 2: สร้างสตรีมจากเส้นทางไฟล์
ถัดไป สร้างสตรีมไฟล์เพื่ออ่านเอกสารอินพุต ซึ่งจะช่วยให้คุณสามารถโหลดเอกสารลงในเครื่องมือแก้ไขได้
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
```
## ขั้นตอนที่ 3: สร้างตัวเลือกการโหลดสำหรับเอกสาร
ในขั้นตอนนี้ คุณจะต้องสร้างตัวเลือกการโหลดสำหรับเอกสารของคุณ หากเอกสารของคุณมีการป้องกันด้วยรหัสผ่าน คุณสามารถระบุรหัสผ่านได้ ในตัวอย่างนี้ เอกสารไม่ได้รับการป้องกัน ดังนั้นรหัสผ่านจึงถูกละเว้น
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
loadOptions.Password = "some_password_to_open_a_document";
```
## ขั้นตอนที่ 4: โหลดเอกสารลงในอินสแตนซ์ตัวแก้ไข
ตอนนี้ ให้โหลดเอกสารพร้อมตัวเลือกที่ระบุลงในอินสแตนซ์ตัวแก้ไข นี่คือที่ที่การดำเนินการหลักในเอกสารจะเกิดขึ้น
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
```
## ขั้นตอนที่ 4.1: อ่านอินสแตนซ์ FormFieldManager
 ที่`FormFieldManager` อินสแตนซ์มีหน้าที่จัดการฟิลด์แบบฟอร์มในเอกสาร คุณจะต้องอ่านอินสแตนซ์นี้เพื่อเข้าถึงและจัดการช่องแบบฟอร์ม
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
## ขั้นตอนที่ 4.2: อ่าน FormFieldCollection
 ที่`FormFieldCollection` มีช่องแบบฟอร์มทั้งหมดในเอกสาร คุณจะอ่านคอลเลกชันนี้เพื่อตรวจสอบและแก้ไขช่องแบบฟอร์มที่ไม่ถูกต้อง
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
## ขั้นตอนที่ 4.3: แก้ไขฟิลด์แบบฟอร์มที่ไม่ถูกต้องโดยอัตโนมัติ
พยายามแก้ไขช่องแบบฟอร์มที่ไม่ถูกต้องในเอกสารโดยอัตโนมัติ นี่เป็นขั้นตอนเบื้องต้นในการแก้ไขปัญหาที่ชัดเจน
```csharp
fieldManager.FixInvalidFormFieldNames(new InvalidFormField[0]);
collection = fieldManager.FormFieldCollection;
```
## ขั้นตอนที่ 4.4: ตรวจสอบฟิลด์แบบฟอร์มที่ไม่ถูกต้อง
ตรวจสอบว่ามีช่องแบบฟอร์มที่ไม่ถูกต้องเหลืออยู่หรือไม่หลังจากพยายามแก้ไขอัตโนมัติ
```csharp
bool hasInvalidFormFields = fieldManager.HasInvalidFormFields();
Console.WriteLine("FormFieldCollection contains invalid items: {0}", hasInvalidFormFields);
```
## ขั้นตอนที่ 4.4.1: รับชื่อฟิลด์แบบฟอร์มที่ไม่ถูกต้องทั้งหมด
ดึงข้อมูลชื่อของเขตข้อมูลแบบฟอร์มที่ไม่ถูกต้องทั้งหมด ชื่อเหล่านี้จะถูกนำมาใช้เพื่อแก้ไขฟิลด์
```csharp
var invalidFormFields = fieldManager.GetInvalidFormFieldNames();
```
## ขั้นตอนที่ 4.4.2: สร้างชื่อเฉพาะสำหรับฟิลด์ที่ไม่ถูกต้อง
สำหรับแต่ละฟิลด์แบบฟอร์มที่ไม่ถูกต้อง ให้สร้างชื่อที่ไม่ซ้ำกัน เพื่อให้แน่ใจว่าไม่มีข้อขัดแย้งกับชื่อฟิลด์แบบฟอร์มที่มีอยู่
```csharp
foreach (var invalidItem in invalidFormFields)
{
    invalidItem.FixedName = string.Format("{0}_{1}", invalidItem.Name, Guid.NewGuid());
}
```
## ขั้นตอนที่ 4.4.3: แก้ไขฟิลด์แบบฟอร์มที่ไม่ถูกต้อง
แก้ไขช่องแบบฟอร์มที่ไม่ถูกต้องโดยใช้ชื่อเฉพาะที่สร้างในขั้นตอนก่อนหน้า
```csharp
fieldManager.FixInvalidFormFieldNames(invalidFormFields);
collection = fieldManager.FormFieldCollection;
```
## ขั้นตอนที่ 5: สร้างตัวเลือกการบันทึกเอกสาร
ตั้งค่าตัวเลือกสำหรับการบันทึกเอกสาร ซึ่งรวมถึงการระบุรูปแบบและการตั้งค่าการบันทึกเพิ่มเติม
```csharp
WordProcessingFormats docFormat = WordProcessingFormats.Docx;
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(docFormat);
```
## ขั้นตอนที่ 5.1: ปรับการใช้หน่วยความจำให้เหมาะสม
 หากเอกสารของคุณมีขนาดใหญ่และอาจทำให้เกิดการ`OutOfMemoryException`ให้เปิดใช้งานตัวเลือกการเพิ่มประสิทธิภาพหน่วยความจำ
```csharp
saveOptions.OptimizeMemoryUsage = true;
```
## ขั้นตอนที่ 5.2: ป้องกันเอกสารจากการเขียน
หากต้องการป้องกันไม่ให้แก้ไขเอกสาร ยกเว้นช่องแบบฟอร์ม ให้ตั้งรหัสผ่านป้องกัน
```csharp
saveOptions.Protection = new WordProcessingProtection(WordProcessingProtectionType.AllowOnlyFormFields, "write_password");
```
## ขั้นตอนที่ 6: บันทึกเอกสาร
สุดท้าย ให้บันทึกเอกสารด้วยตัวเลือกการบันทึกที่ระบุ เตรียมสตรีมหน่วยความจำสำหรับบันทึกเอกสารเอาต์พุต
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(outputStream, saveOptions);
}
Console.WriteLine("FixInvalidFormFieldCollectionAndSave routine has successfully finished");
```
## บทสรุป
 และคุณก็ได้แล้ว! คุณได้แก้ไขช่องแบบฟอร์มที่ไม่ถูกต้องและบันทึกเอกสารของคุณโดยใช้ Groupdocs.Editor สำหรับ .NET เรียบร้อยแล้ว คำแนะนำทีละขั้นตอนนี้ควรทำให้กระบวนการมีความชัดเจนและสามารถจัดการได้ หากคุณพบปัญหาใดๆ หรือมีคำถาม โปรดตรวจสอบได้ที่[เอกสารประกอบ](https://tutorials.groupdocs.com/editor/net/) หรือติดต่อไปที่[สนับสนุน](https://forum.groupdocs.com/c/editor/20).
## คำถามที่พบบ่อย
### จะเกิดอะไรขึ้นหากเอกสารของฉันมีการป้องกันด้วยรหัสผ่าน?
 คุณสามารถระบุรหัสผ่านได้ใน`WordProcessingLoadOptions` เพื่อเปิดเอกสาร
### ฉันจะรู้ได้อย่างไรว่ามีฟิลด์แบบฟอร์มที่ไม่ถูกต้อง?
 ใช้`HasInvalidFormFields` วิธีการตรวจสอบฟิลด์แบบฟอร์มที่ไม่ถูกต้องในเอกสาร
### ฉันสามารถแก้ไขฟิลด์แบบฟอร์มโดยไม่ต้องเปลี่ยนชื่อได้หรือไม่
ขอแนะนำให้สร้างชื่อที่ไม่ซ้ำกันสำหรับช่องแบบฟอร์มที่ไม่ถูกต้องเพื่อหลีกเลี่ยงความขัดแย้ง
### ฉันสามารถบันทึกเอกสารในรูปแบบใดได้บ้าง
 คุณสามารถบันทึกเอกสารในรูปแบบต่างๆ เช่น DOCX, PDF และอื่นๆ ได้โดยการตั้งค่าที่เหมาะสม`WordProcessingFormats`.
### ฉันจะเพิ่มประสิทธิภาพการใช้หน่วยความจำในขณะที่บันทึกเอกสารขนาดใหญ่ได้อย่างไร
 เปิดใช้งาน`OptimizeMemoryUsage` ตัวเลือกใน`WordProcessingSaveOptions` เพื่อจัดการเอกสารขนาดใหญ่ได้อย่างมีประสิทธิภาพ