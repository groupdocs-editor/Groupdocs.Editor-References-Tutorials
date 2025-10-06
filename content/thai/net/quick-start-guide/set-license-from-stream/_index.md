---
title: ตั้งค่าใบอนุญาตจากสตรีม
linktitle: ตั้งค่าใบอนุญาตจากสตรีม
second_title: GroupDocs.Editor .NET API
description: เรียนรู้วิธีใช้ Groupdocs.Editor สำหรับ .NET เพื่อแก้ไขเอกสารโดยทางโปรแกรม ปฏิบัติตามข้อครอบคลุมนี้เพื่อการบูรณาการที่ราบรื่นและคุณสมบัติขั้นสูง
weight: 11
url: /th/net/quick-start-guide/set-license-from-stream/
type: docs
---
# ตั้งค่าใบอนุญาตจากสตรีม

## การแนะนำ
คุณกำลังมองหาวิธีที่มีประสิทธิภาพในการแก้ไขเอกสารโดยทางโปรแกรมในแอปพลิเคชัน .NET ของคุณหรือไม่? ไม่ต้องมองอีกต่อไป! Groupdocs.Editor สำหรับ .NET เป็นโซลูชันการแก้ไขเอกสารที่มีประสิทธิภาพ ซึ่งช่วยให้คุณสามารถผสานรวมคุณลักษณะการแก้ไขเอกสารเข้ากับแอปพลิเคชันของคุณได้อย่างราบรื่น ไม่ว่าคุณจะจัดการเอกสาร Word, สเปรดชีต Excel หรือรูปแบบอื่นๆ คู่มือนี้จะแนะนำทุกสิ่งที่คุณจำเป็นต้องรู้เพื่อเริ่มต้นใช้งาน
## ข้อกำหนดเบื้องต้น
ก่อนที่จะดำดิ่งสู่โลกแห่งการแก้ไขเอกสารด้วย Groupdocs.Editor สำหรับ .NET ที่น่าตื่นเต้น คุณจะต้องมีข้อกำหนดเบื้องต้นบางประการเพื่อให้แน่ใจว่าการตั้งค่าจะราบรื่น:
1. .NET Framework: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง .NET Framework 4.7.1 ขึ้นไปบนเครื่องของคุณ
2.  Groupdocs.Editor สำหรับ .NET: ดาวน์โหลดและติดตั้งเวอร์ชันล่าสุดจาก[หน้าปล่อย](https://releases.groupdocs.com/editor/net/).
3. IDE: เตรียมสภาพแวดล้อมการพัฒนาแบบรวม (IDE) เช่น Visual Studio ให้พร้อม
4.  ใบอนุญาต: รับใบอนุญาตที่ถูกต้องสำหรับ Groupdocs.Editor คุณจะได้รับ[ใบอนุญาตชั่วคราว](https://purchase.groupdocs.com/temporary-license/) เพื่อวัตถุประสงค์ในการประเมินผล
## นำเข้าเนมสเปซ
หากต้องการเริ่มใช้ Groupdocs.Editor สำหรับ .NET คุณจะต้องนำเข้าเนมสเปซที่จำเป็นในโปรเจ็กต์ของคุณ สิ่งนี้จะช่วยให้แน่ใจว่าคุณมีคลาสและวิธีการที่จำเป็นทั้งหมดให้คุณใช้งานได้
```csharp
using System;
using System.IO;
using GroupDocs.Editor;
```

การตั้งค่าใบอนุญาตเป็นขั้นตอนสำคัญขั้นแรกในการใช้ Groupdocs.Editor สำหรับ .NET คำแนะนำทีละขั้นตอนเพื่อช่วยคุณตลอดกระบวนการ:
## ขั้นตอนที่ 1: ตรวจสอบไฟล์ลิขสิทธิ์
 ขั้นแรก ตรวจสอบให้แน่ใจว่าคุณได้ดาวน์โหลดไฟล์ลิขสิทธิ์จาก Groupdocs โดยปกติแล้วไฟล์ลิขสิทธิ์จะมีชื่อประมาณนี้`GroupDocs.Editor.lic`.
## ขั้นตอนที่ 2: โหลดใบอนุญาตจากสตรีม
ตอนนี้ มาโหลดใบอนุญาตโดยใช้สตรีมไฟล์กันดีกว่า เพื่อให้แน่ใจว่ามีการใช้ใบอนุญาตอย่างถูกต้องเมื่อแอปพลิเคชันของคุณเริ่มต้น
```csharp
if (File.Exists("path/to/your/GroupDocs.Editor.lic"))
{
    using (FileStream stream = File.OpenRead("path/to/your/GroupDocs.Editor.lic"))
    {
        License license = new License();
        license.SetLicense(stream);
    }
    Console.WriteLine("License set successfully.");
}
else
{
    Console.WriteLine("\nWe do not ship any license with this example. " +
                      "\nVisit the GroupDocs site to obtain either a temporary or permanent license. " +
                      "\nLearn more about licensing at https://buy.groupdocs.com/faqs/licensing -
                      "\nLearn how to request a temporary license at https://buy.groupdocs.com/temporary-license");
}
```
ตัวอย่างนี้จะตรวจสอบการมีอยู่ของไฟล์ใบอนุญาตและตั้งค่าหากพบ
## การโหลดและการแก้ไขเอกสาร
เมื่อได้รับใบอนุญาตแล้ว มาดูการโหลดและแก้ไขเอกสารกันดีกว่า โดยจะแบ่งออกเป็นขั้นตอนที่ชัดเจนและจัดการได้
## ขั้นตอนที่ 1: โหลดเอกสาร
โหลดเอกสารที่คุณต้องการแก้ไข ตัวอย่างเช่น เริ่มจากเอกสาร Word กันก่อน
```csharp
string filePath = "path/to/your/document.docx";
Editor editor = new Editor(filePath);
```
## ขั้นตอนที่ 2: แยกเนื้อหาที่แก้ไขได้
จากนั้น แยกเนื้อหาออกจากเอกสารเป็นรูปแบบที่แก้ไขได้
```csharp
EditableDocument editableDocument = editor.Edit();
string content = editableDocument.GetContent();
```
## ขั้นตอนที่ 3: แก้ไขเนื้อหา
ตอนนี้คุณสามารถแก้ไขเนื้อหาได้ตามต้องการ สำหรับตัวอย่างนี้ ลองเพิ่มข้อความต่อท้ายกัน
```csharp
string modifiedContent = content + "\nAppended text";
editableDocument.SetContent(modifiedContent);
```
## ขั้นตอนที่ 4: บันทึกเอกสารที่แก้ไข
สุดท้าย ให้บันทึกเอกสารที่แก้ไขกลับไปยังระบบไฟล์
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(editableDocument, outputStream, new WordProcessingSaveOptions());
    File.WriteAllBytes("path/to/your/modified_document.docx", outputStream.ToArray());
}
```
## การทำงานกับรูปแบบต่างๆ
Groupdocs.Editor สำหรับ .NET รองรับรูปแบบเอกสารที่หลากหลาย ต่อไปนี้เป็นคำแนะนำโดยย่อในการทำงานกับรูปแบบทั่วไปบางรูปแบบ
## การแก้ไขสเปรดชีต Excel
การแก้ไขไฟล์ Excel จะคล้ายกับเอกสาร Word ความแตกต่างที่สำคัญคือตัวเลือกการบันทึก
```csharp
string filePath = "path/to/your/spreadsheet.xlsx";
Editor editor = new Editor(filePath);
// แยกเนื้อหา
EditableDocument editableDocument = editor.Edit();
string content = editableDocument.GetContent();
// ปรับเปลี่ยนเนื้อหา
string modifiedContent = content + "\nNew data row";
editableDocument.SetContent(modifiedContent);
// บันทึกเอกสารที่แก้ไข
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(editableDocument, outputStream, new SpreadsheetSaveOptions());
    File.WriteAllBytes("path/to/your/modified_spreadsheet.xlsx", outputStream.ToArray());
}
```
## การแก้ไขเอกสาร PDF
เอกสาร PDF ต้องใช้แนวทางที่แตกต่างออกไปเล็กน้อยเนื่องจากลักษณะของเอกสาร
```csharp
string filePath = "path/to/your/document.pdf";
Editor editor = new Editor(filePath);
// แยกเนื้อหา
EditableDocument editableDocument = editor.Edit();
string content = editableDocument.GetContent();
// ปรับเปลี่ยนเนื้อหา
string modifiedContent = content + "\nAdditional text";
editableDocument.SetContent(modifiedContent);
// บันทึกเอกสารที่แก้ไข
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(editableDocument, outputStream, new PdfSaveOptions());
    File.WriteAllBytes("path/to/your/modified_document.pdf", outputStream.ToArray());
}
```
## คุณสมบัติขั้นสูง
Groupdocs.Editor สำหรับ .NET นำเสนอคุณลักษณะขั้นสูงหลายประการที่สามารถเพิ่มความสามารถในการแก้ไขเอกสารของคุณได้
## การตั้งค่าตัวเลือกการบันทึก
คุณสามารถปรับแต่งตัวเลือกการบันทึกให้เหมาะกับความต้องการของคุณได้ ตัวอย่างเช่น เมื่อบันทึกเอกสาร Word คุณสามารถระบุรูปแบบและรายละเอียดอื่นๆ ได้
```csharp
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions
{
    Format = WordProcessingFormats.Docx,
    Password = "your-password"
};
editor.Save(editableDocument, outputStream, saveOptions);
```
## การจัดการเอกสารขนาดใหญ่
สำหรับเอกสารขนาดใหญ่ ให้ลองใช้การสตรีมเพื่อจัดการเนื้อหาอย่างมีประสิทธิภาพ
```csharp
using (FileStream inputStream = File.OpenRead("path/to/large/document.docx"))
{
    Editor editor = new Editor(() => inputStream);
    EditableDocument editableDocument = editor.Edit();
    
    // ปรับเปลี่ยนเนื้อหา
    string modifiedContent = editableDocument.GetContent() + "\nAdditional content";
    editableDocument.SetContent(modifiedContent);
    
    using (MemoryStream outputStream = new MemoryStream())
    {
        editor.Save(editableDocument, outputStream, new WordProcessingSaveOptions());
        File.WriteAllBytes("path/to/modified_large_document.docx", outputStream.ToArray());
    }
}
```
## บทสรุป
 Groupdocs.Editor สำหรับ .NET เป็นเครื่องมืออเนกประสงค์และมีประสิทธิภาพซึ่งสามารถปรับปรุงกระบวนการแก้ไขเอกสารของคุณได้อย่างมาก ด้วยคุณสมบัติที่แข็งแกร่งและการรองรับรูปแบบเอกสารที่หลากหลาย การรวมไลบรารีนี้เข้ากับแอปพลิเคชัน .NET ของคุณจะช่วยเพิ่มประสิทธิภาพและความสามารถของคุณได้อย่างไม่ต้องสงสัย อย่าลืมไปสำรวจ[เอกสารประกอบ](https://tutorials.groupdocs.com/editor/net/) สำหรับข้อมูลโดยละเอียดเพิ่มเติมและสถานการณ์การใช้งานขั้นสูง
## คำถามที่พบบ่อย
### ฉันสามารถใช้ Groupdocs.Editor สำหรับ .NET โดยไม่มีใบอนุญาตได้หรือไม่
 ไม่ คุณต้องมีใบอนุญาตที่ถูกต้องเพื่อใช้ Groupdocs.Editor สำหรับ .NET อย่างไรก็ตาม คุณสามารถขอก[ใบอนุญาตชั่วคราว](https://purchase.groupdocs.com/temporary-license/) สำหรับการประเมินผล
### Groupdocs.Editor รองรับการแก้ไขไฟล์ PDF หรือไม่
ใช่ รองรับการแก้ไขไฟล์ PDF พร้อมกับรูปแบบอื่นๆ เช่น Word และ Excel
### ฉันจะรับการสนับสนุน Groupdocs.Editor สำหรับ .NET ได้อย่างไร
 ท่านสามารถเยี่ยมชมได้ที่[ฟอรั่มการสนับสนุน](https://forum.groupdocs.com/c/editor/20) สำหรับข้อสงสัยหรือปัญหาใด ๆ ที่คุณอาจพบ
### เป็นไปได้หรือไม่ที่จะป้องกันเอกสารด้วยรหัสผ่านโดยใช้ Groupdocs.Editor
ได้ คุณสามารถตั้งรหัสผ่านและตัวเลือกความปลอดภัยอื่นๆ เมื่อบันทึกเอกสารได้
### Groupdocs.Editor for .NET รองรับรูปแบบไฟล์ใดบ้าง
 รองรับรูปแบบที่หลากหลาย รวมถึง DOCX, XLSX, PDF และอื่น ๆ อีกมากมาย อ้างถึง[เอกสารประกอบ](https://tutorials.groupdocs.com/editor/net/) สำหรับรายการทั้งหมด