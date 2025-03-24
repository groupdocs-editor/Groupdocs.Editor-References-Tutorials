---
title: แยกข้อมูลเอกสาร
linktitle: แยกข้อมูลเอกสาร
second_title: GroupDocs.Editor .NET API
description: เรียนรู้วิธีดึงข้อมูลเอกสารโดยใช้ GroupDocs.Editor สำหรับ .NET พร้อมบทช่วยสอนแบบละเอียดทีละขั้นตอนของเรา เหมาะสำหรับการจัดการเอกสารประเภทต่างๆ
weight: 10
url: /th/net/document-processing/extract-document-info/
---

# แยกข้อมูลเอกสาร

## การแนะนำ
ยินดีต้อนรับสู่บทช่วยสอนที่ครอบคลุมเกี่ยวกับการดึงข้อมูลเอกสารโดยใช้ GroupDocs.Editor สำหรับ .NET ในคู่มือนี้ เราจะแนะนำคุณตลอดกระบวนการทีละขั้นตอน เพื่อให้แน่ใจว่าคุณเข้าใจแต่ละส่วนอย่างชัดเจนและรัดกุม ไม่ว่าคุณจะเป็นนักพัฒนาที่มีประสบการณ์หรือเพิ่งเริ่มต้น บทช่วยสอนนี้จะช่วยให้คุณผสานรวม GroupDocs.Editor เข้ากับโปรเจ็กต์ .NET ของคุณได้อย่างราบรื่น เพื่อจัดการและจัดการเอกสารอย่างมีประสิทธิภาพ
## ข้อกำหนดเบื้องต้น
ก่อนที่จะเจาะลึกโค้ด โปรดตรวจสอบให้แน่ใจว่าคุณมีทุกสิ่งที่คุณต้องการ:
- ความรู้พื้นฐานของ C#: การทำความเข้าใจพื้นฐานของการเขียนโปรแกรม C# เป็นสิ่งสำคัญ
- Visual Studio: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Visual Studio แล้ว
-  GroupDocs.Editor สำหรับ .NET: คุณจะต้องมี GroupDocs.Editor สำหรับไลบรารี .NET คุณสามารถดาวน์โหลดได้จาก[หน้าดาวน์โหลด](https://releases.groupdocs.com/editor/net/).
## นำเข้าเนมสเปซ
ในการเริ่มต้น คุณจะต้องนำเข้าเนมสเปซที่จำเป็น สิ่งนี้ช่วยให้คุณเข้าถึงคลาสและวิธีการที่จำเป็นในการจัดการเอกสาร
```csharp
using System;
using GroupDocs.Editor.Metadata;
```
## ขั้นตอนที่ 1: โหลดเอกสารของคุณ
ขั้นแรก คุณต้องโหลดเอกสารที่คุณต้องการดึงข้อมูลออกมา ซึ่งสามารถทำได้โดยระบุเส้นทางของไฟล์ไปยังเอกสาร
```csharp
string docxInputFilePath = "YourSampleDocument.docx";
Editor editorDocx = new Editor(docxInputFilePath);
```
## ขั้นตอนที่ 2: ดึงข้อมูลเอกสาร
 จากนั้น คุณจะดึงข้อมูลเอกสารโดยใช้`GetDocumentInfo` วิธี. วิธีนี้ไม่ต้องใช้ตัวเลือกการโหลดเฉพาะใดๆ หากคุณไม่แน่ใจเกี่ยวกับรูปแบบเอกสาร
```csharp
IDocumentInfo infoDocx = editorDocx.GetDocumentInfo(null);
```
## ขั้นตอนที่ 3: กำหนดประเภทเอกสาร
ตอนนี้คุณต้องตรวจสอบประเภทของเอกสารที่คุณกำลังติดต่อด้วย นี่เป็นสิ่งสำคัญเนื่องจากเป็นตัวกำหนดวิธีที่คุณจะจัดการเอกสาร
```csharp
bool isSpreadsheet = infoDocx is SpreadsheetDocumentInfo;
bool isText = infoDocx is TextualDocumentInfo;
bool isWordProcessing = infoDocx is WordProcessingDocumentInfo;
Console.WriteLine($"Is '{docxInputFilePath}' a Spreadsheet: {isSpreadsheet}");
Console.WriteLine($"Is '{docxInputFilePath}' a Textual document: {isText}");
Console.WriteLine($"Is '{docxInputFilePath}' a WordProcessing document: {isWordProcessing}");
```
## ขั้นตอนที่ 4: แยกข้อมูลโดยละเอียด
หากเอกสารนั้นเป็นเอกสารการประมวลผลคำ คุณสามารถดึงข้อมูลโดยละเอียด เช่น รูปแบบ นามสกุล จำนวนหน้า ขนาด และดูว่ามีการเข้ารหัสหรือไม่
```csharp
if (isWordProcessing)
{
    WordProcessingDocumentInfo casted = (WordProcessingDocumentInfo)infoDocx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Page count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```
## ขั้นตอนที่ 5: ทำซ้ำสำหรับเอกสารประเภทต่างๆ
ทำซ้ำขั้นตอนเดียวกันสำหรับเอกสารประเภทอื่นๆ เช่น เอกสารสเปรดชีตและข้อความ
```csharp
string xlsxInputFilePath = "YourSampleDocument.xlsx";
Editor editorXlsx = new Editor(xlsxInputFilePath);
IDocumentInfo infoXlsx = editorXlsx.GetDocumentInfo(null);
bool isXlsxSpreadsheet = infoXlsx is SpreadsheetDocumentInfo;
Console.WriteLine($"Is '{xlsxInputFilePath}' a Spreadsheet: {isXlsxSpreadsheet}");
if (isXlsxSpreadsheet)
{
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo)infoXlsx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Tabs count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```
## ขั้นตอนที่ 6: จัดการเอกสารที่ป้องกันด้วยรหัสผ่าน
เมื่อต้องจัดการกับเอกสารที่มีการป้องกันด้วยรหัสผ่าน คุณควรพยายามเปิดเอกสารโดยไม่มีรหัสผ่านก่อน จากนั้นจึงเปิดด้วยรหัสผ่านที่ไม่ถูกต้อง และสุดท้ายด้วยรหัสผ่านที่ถูกต้อง
```csharp
string xlsInputFilePath = "YourSampleDocument.xls";
Editor editorXls = new Editor(xlsInputFilePath);
try
{
    IDocumentInfo infoXls = editorXls.GetDocumentInfo(null);
}
catch (PasswordRequiredException)
{
    Console.WriteLine("This document is password-protected.");
}
try
{
    IDocumentInfo infoXls = editorXls.GetDocumentInfo("incorrect_password");
}
catch (IncorrectPasswordException)
{
    Console.WriteLine("The provided password is incorrect.");
}
IDocumentInfo infoXlsValid = editorXls.GetDocumentInfo("correct_password");
bool isXlsSpreadsheet = infoXlsValid is SpreadsheetDocumentInfo;
Console.WriteLine($"Password-protected document is a Spreadsheet: {isXlsSpreadsheet}");
if (isXlsSpreadsheet)
{
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo)infoXlsValid;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Tabs count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```
## ขั้นตอนที่ 7: จัดการเอกสารที่เป็นข้อความ
```csharp
string xmlInputFilePath = "YourSampleDocument.xml";
Editor editorXml = new Editor(xmlInputFilePath);
IDocumentInfo infoXml = editorXml.GetDocumentInfo(null);
bool isXmlText = infoXml is TextualDocumentInfo;
Console.WriteLine($"Is '{xmlInputFilePath}' a Textual document: {isXmlText}");
if (isXmlText)
{
    TextualDocumentInfo casted = (TextualDocumentInfo)infoXml;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Encoding: {casted.Encoding}; Size: {casted.Size} bytes");
}
```
## ขั้นตอนที่ 8: กำจัดทรัพยากร
สุดท้ายนี้ ตรวจสอบให้แน่ใจว่าคุณได้กำจัดทรัพยากรทั้งหมดเพื่อป้องกันการรั่วไหลของหน่วยความจำ
```csharp
editorDocx.Dispose();
editorXlsx.Dispose();
editorXls.Dispose();
editorXml.Dispose();
Console.WriteLine("ExtractingDocumentInfo routine has successfully finished");
```
## บทสรุป
ยินดีด้วย! ตอนนี้คุณได้เรียนรู้วิธีแยกข้อมูลเอกสารโดยใช้ GroupDocs.Editor สำหรับ .NET แล้ว ไลบรารีอันทรงพลังนี้ช่วยลดความยุ่งยากในการจัดการและจัดการเอกสาร ช่วยให้คุณจัดการเอกสารประเภทต่าง ๆ ได้อย่างราบรื่น ไม่ว่าคุณจะจัดการกับการประมวลผลคำ สเปรดชีต หรือเอกสารแบบข้อความ GroupDocs.Editor ก็มีโซลูชันที่มีประสิทธิภาพ
## คำถามที่พบบ่อย
### GroupDocs.Editor รองรับเอกสารประเภทใดบ้าง
GroupDocs.Editor สามารถจัดการเอกสารได้หลายประเภท รวมถึงการประมวลผลคำ สเปรดชีต และเอกสารแบบข้อความ
### GroupDocs.Editor สามารถจัดการเอกสารที่มีการป้องกันด้วยรหัสผ่านได้หรือไม่
ใช่ GroupDocs.Editor สามารถจัดการเอกสารที่มีการป้องกันด้วยรหัสผ่านได้ สามารถระบุและเปิดเอกสารเหล่านี้ด้วยรหัสผ่านที่ถูกต้อง
### จำเป็นต้องกำจัดออบเจ็กต์ Editor หรือไม่?
ใช่ การกำจัดออบเจ็กต์ Editor เพื่อเพิ่มทรัพยากรและป้องกันหน่วยความจำรั่วเป็นสิ่งสำคัญ
### ฉันสามารถดึงข้อมูลโดยละเอียดเกี่ยวกับรูปแบบและขนาดเอกสารได้หรือไม่
อย่างแน่นอน! GroupDocs.Editor ช่วยให้คุณสามารถดึงข้อมูลโดยละเอียด รวมถึงรูปแบบ นามสกุล ขนาด จำนวนหน้า และสถานะการเข้ารหัส
### ฉันจะรับการสนับสนุนได้ที่ไหนหากฉันประสบปัญหา
 คุณสามารถรับการสนับสนุนจาก[ฟอรัมสนับสนุน GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).