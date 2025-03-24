---
title: ทำงานกับสเปรดชีตที่มีการป้องกันด้วยรหัสผ่าน
linktitle: ทำงานกับสเปรดชีตที่มีการป้องกันด้วยรหัสผ่าน
second_title: GroupDocs.Editor .NET API
description: เรียนรู้วิธีจัดการสเปรดชีตที่ป้องกันด้วยรหัสผ่านโดยใช้ GroupDocs.Editor สำหรับ .NET คำแนะนำโดยละเอียดนี้จะอธิบายขั้นตอนการเปิดเพื่อบันทึกไฟล์ Excel ที่ปลอดภัย
weight: 18
url: /th/net/document-processing/work-password-protected-spreadsheets/
---
## การแนะนำ
คุณกำลังประสบปัญหาในการจัดการสเปรดชีตที่มีการป้องกันด้วยรหัสผ่านในแอปพลิเคชัน .NET ของคุณหรือไม่? ถ้าเป็นเช่นนั้น คุณมาถูกที่แล้ว! ในคู่มือที่ครอบคลุมนี้ เราจะแนะนำคุณตลอดขั้นตอนการใช้ GroupDocs.Editor สำหรับ .NET เพื่อจัดการสเปรดชีตที่มีการป้องกันด้วยรหัสผ่านอย่างมีประสิทธิภาพ เมื่อสิ้นสุดบทช่วยสอนนี้ คุณจะมีความพร้อมที่จะเปิด แก้ไข และบันทึกไฟล์ Excel ที่เข้ารหัสได้อย่างง่ายดาย
## ข้อกำหนดเบื้องต้น
ก่อนที่จะเจาะลึกโค้ด เรามาตรวจสอบให้แน่ใจว่าคุณมีทุกสิ่งที่จำเป็นในการปฏิบัติตาม:
- ความรู้พื้นฐานของ C#: บทช่วยสอนนี้ถือว่าคุณคุ้นเคยกับการเขียนโปรแกรม C#
- .NET Framework: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง .NET Framework บนเครื่องพัฒนาของคุณ
-  GroupDocs.Editor สำหรับ .NET: ดาวน์โหลดและติดตั้ง GroupDocs.Editor สำหรับ .NET จาก[ที่นี่](https://releases.groupdocs.com/editor/net/).
## นำเข้าเนมสเปซ
ในการเริ่มต้น คุณจะต้องนำเข้าเนมสเปซที่จำเป็นในโปรเจ็กต์ C# ของคุณ เนมสเปซเหล่านี้ให้สิทธิ์เข้าถึงฟังก์ชันของ GroupDocs.Editor
```csharp
using System;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
## ขั้นตอนที่ 1: รับเส้นทางไปยังไฟล์อินพุต
ขั้นแรก คุณจะต้องมีเส้นทางไปยังไฟล์อินพุต สำหรับตัวอย่างนี้ เราจะใช้ไฟล์ Excel ตัวอย่าง (`Your Sample Document`) ที่มีการป้องกันด้วยรหัสผ่าน
```csharp
string inputFilePath = "Your Sample Document";
```
## ขั้นตอนที่ 2: พยายามเปิดเอกสารโดยไม่มีรหัสผ่าน
มาดูกันว่าเกิดอะไรขึ้นหากเราพยายามเปิดเอกสารโดยไม่ระบุรหัสผ่าน
```csharp
Editor editor = new Editor(inputFilePath);
try
{
    editor.Edit();
}
catch (GroupDocs.Editor.PasswordRequiredException)
{
    Console.WriteLine("Cannot edit the document because it is password-protected. A password is required.");
}
editor.Dispose();
```
## ขั้นตอนที่ 3: ลองระบุรหัสผ่านไม่ถูกต้อง
ตอนนี้ เราจะระบุรหัสผ่านที่ไม่ถูกต้องเพื่อแสดงให้เห็นว่าตัวแก้ไขตอบสนองอย่างไร
```csharp
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.Password = "incorrect_password";
editor = new Editor(inputFilePath, delegate { return loadOptions; });
try
{
    editor.Edit();
}
catch (GroupDocs.Editor.IncorrectPasswordException)
{
    Console.WriteLine("Cannot edit the document because the specified password is incorrect.");
}
editor.Dispose();
```
## ขั้นตอนที่ 4: เปิดไฟล์ด้วยรหัสผ่านที่ถูกต้อง
มาระบุรหัสผ่านที่ถูกต้องและเปิดไฟล์ได้สำเร็จ
```csharp
loadOptions.Password = "excel_password";
loadOptions.OptimizeMemoryUsage = true;
editor = new Editor(inputFilePath, delegate { return loadOptions; });
```
## ขั้นตอนที่ 5: สร้างและปรับตัวเลือกการแก้ไข
หากต้องการแก้ไขสเปรดชีต เราจำเป็นต้องสร้างและปรับตัวเลือกการแก้ไข
```csharp
SpreadsheetEditOptions editOptions = new SpreadsheetEditOptions();
```
## ขั้นตอนที่ 6: สร้างเอกสารที่แก้ไขได้ระดับกลาง
 ต่อไปเราจะสร้างสื่อกลาง`EditableDocument` ที่ช่วยให้เราสามารถเปลี่ยนแปลงสเปรดชีตได้
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
{
    // ขั้นตอนที่ 7: สร้างตัวเลือกการบันทึก
    SpreadsheetFormats xlsmFormat = SpreadsheetFormats.Xlsm;
    SpreadsheetSaveOptions saveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
    // ขั้นตอนที่ 7.1: ตั้งรหัสผ่านการเปิดใหม่
    saveOptions.Password = "new password";
    // ขั้นตอนที่ 7.2: ตั้งค่าการป้องกันการเขียน
    saveOptions.WorksheetProtection = new WorksheetProtection(WorksheetProtectionType.All, "write password");
    // ขั้นตอนที่ 8: บันทึกเอกสารโดยไม่มีการแก้ไข
    //ขั้นตอนที่ 8.1: เตรียมชื่อไฟล์เอาต์พุตและเส้นทาง
    string outputFilename = Path.GetFileNameWithoutExtension(inputFilePath) + "." + xlsmFormat.Extension;
    string outputPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename);
    // ขั้นตอนที่ 8.2: สร้างสตรีมเอาท์พุต
    using (FileStream outputStream = File.Create(outputPath))
    {
        // ขั้นตอนที่ 8.3: บันทึก
        editor.Save(beforeEdit, outputStream, saveOptions);
    }
}
// ขั้นตอนที่ 9: กำจัดอินสแตนซ์ตัวแก้ไข
editor.Dispose();
Console.WriteLine("Successfully handled the password-protected spreadsheet. Editor instance has been disposed: {0}", editor.IsDisposed ? "Yes" : "No");
```
## บทสรุป
ยินดีด้วย! คุณได้เรียนรู้วิธีจัดการสเปรดชีตที่ป้องกันด้วยรหัสผ่านโดยใช้ GroupDocs.Editor สำหรับ .NET เรียบร้อยแล้ว ตั้งแต่การพยายามเปิดเอกสารโดยไม่ต้องใช้รหัสผ่านไปจนถึงการบันทึกด้วยการตั้งค่าการป้องกันใหม่ คุณได้ครอบคลุมขั้นตอนที่จำเป็นทั้งหมดแล้ว ความรู้นี้จะช่วยเพิ่มความสามารถของคุณในการจัดการเอกสารที่ปลอดภัยภายในแอปพลิเคชัน .NET ของคุณอย่างไม่ต้องสงสัย
## คำถามที่พบบ่อย
### GroupDocs.Editor สำหรับ .NET คืออะไร
GroupDocs.Editor สำหรับ .NET เป็น API การแก้ไขเอกสารอันทรงพลังที่ช่วยให้นักพัฒนาโหลด แก้ไข และบันทึกรูปแบบเอกสารที่หลากหลายภายในแอปพลิเคชัน .NET
### ฉันจะรับใบอนุญาตชั่วคราวสำหรับ GroupDocs.Editor ได้อย่างไร
 คุณสามารถขอรับใบอนุญาตชั่วคราวได้จาก[ที่นี่](https://purchase.groupdocs.com/temporary-license/) เพื่อประเมินคุณลักษณะของผลิตภัณฑ์
### เป็นไปได้หรือไม่ที่จะปรับการใช้หน่วยความจำให้เหมาะสมในขณะที่แก้ไขเอกสารขนาดใหญ่?
 ใช่ คุณสามารถเปิดใช้งานการเพิ่มประสิทธิภาพหน่วยความจำได้โดยการตั้งค่า`OptimizeMemoryUsage` ทรัพย์สินเพื่อ`true`ในตัวเลือกการโหลด
### ฉันสามารถตั้งรหัสผ่านที่แตกต่างกันสำหรับการเปิดและเขียนลงในสเปรดชีตได้หรือไม่
อย่างแน่นอน! คุณสามารถตั้งรหัสผ่านแยกต่างหากสำหรับการเปิดเอกสารและสำหรับการป้องกันการเขียนโดยใช้ตัวเลือกการบันทึก
### ฉันจะหาเอกสารรายละเอียดเพิ่มเติมได้จากที่ไหน?
 คุณสามารถเข้าถึงเอกสารที่ครอบคลุมสำหรับ GroupDocs.Editor สำหรับ .NET[ที่นี่](https://tutorials.groupdocs.com/editor/net/).