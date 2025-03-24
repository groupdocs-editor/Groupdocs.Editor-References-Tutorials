---
title: สร้างเอกสาร
linktitle: สร้างเอกสาร
second_title: GroupDocs.Editor .NET API
description: เรียนรู้วิธีแก้ไขเอกสาร Word, Excel, PowerPoint, Ebook และอีเมลโดยใช้ GroupDocs.Editor สำหรับ .NET พร้อมบทช่วยสอนทีละขั้นตอนที่ครอบคลุมนี้
weight: 10
url: /th/net/document-editing/create-document/
---
## การแนะนำ
คุณเบื่อกับความยุ่งยากที่มาพร้อมกับการแก้ไขเอกสารประเภทต่างๆ โดยทางโปรแกรมหรือไม่? GroupDocs.Editor สำหรับ .NET อยู่ที่นี่เพื่อทำให้กระบวนการง่ายขึ้น เครื่องมืออันทรงพลังนี้ช่วยให้นักพัฒนาสามารถแก้ไขรูปแบบเอกสารต่าง ๆ เช่น Word, Excel, PowerPoint, Ebooks และอีเมลได้อย่างง่ายดาย ในบทช่วยสอนนี้ เราจะเจาะลึกถึงวิธีใช้ GroupDocs.Editor สำหรับ .NET เพื่อสร้างและแก้ไขเอกสาร เราจะแบ่งกระบวนการออกเป็นขั้นตอนที่ปฏิบัติตามได้ง่าย ซึ่งทำให้สามารถเข้าถึงได้แม้ว่าคุณจะยังใหม่กับสิ่งนี้ก็ตาม
## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะเริ่ม ตรวจสอบให้แน่ใจว่าคุณมีสิ่งต่อไปนี้:
- ติดตั้ง Visual Studio บนเครื่องของคุณแล้ว
- .NET Framework (4.0 หรือสูงกว่า)
-  GroupDocs.Editor สำหรับไลบรารี .NET คุณสามารถดาวน์โหลดได้จาก[ที่นี่](https://releases.groupdocs.com/editor/net/).
- ความรู้พื้นฐานเกี่ยวกับการเขียนโปรแกรม C#
## นำเข้าเนมสเปซ
ขั้นแรก เรามานำเข้าเนมสเปซที่จำเป็นกันก่อน สิ่งนี้จะทำให้คลาสและวิธีการที่จำเป็นสามารถเข้าถึงได้ในแอปพลิเคชันของเรา
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using System.IO;
```
## ขั้นตอนที่ 1: การตั้งค่าสตรีม
ขั้นแรก เราต้องตั้งค่าสตรีมหน่วยความจำที่จะทำหน้าที่เป็นตัวยึดตำแหน่งสำหรับเนื้อหาเอกสาร
```csharp
Stream memoryStream = Stream.Null;
```
## ขั้นตอนที่ 2: ฟังก์ชั่นการโทรกลับเพื่อบันทึกเอกสาร
ถัดไป กำหนดฟังก์ชันการโทรกลับที่จะบันทึกสตรีมเอกสารใหม่ ฟังก์ชันนี้จำเป็นสำหรับการจัดการผลลัพธ์ของกระบวนการแก้ไขเอกสาร
```csharp
void SaveNewDocument(Stream resultStream)
{
    memoryStream = resultStream;
}
```
## ขั้นตอนที่ 3: การสร้างและแก้ไขเอกสาร WordProcessing
 ตอนนี้เรามาสร้างและแก้ไขเอกสาร Word กันดีกว่า เราจะเริ่มต้นด้วยการสร้างใหม่`Editor` อินสแตนซ์สำหรับเอกสาร WordProcessing และแก้ไขด้วยตัวเลือกเริ่มต้น
### สร้างและแก้ไขด้วยตัวเลือกเริ่มต้น
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    EditableDocument defaultWordProcessingDoc = editor.Edit();
}
```
### สร้างและแก้ไขด้วยตัวเลือกแบบกำหนดเอง
เพื่อการควบคุมที่มากขึ้น เราสามารถระบุตัวเลือกต่างๆ เช่น การปิดใช้งานการแบ่งหน้าและการแยกแบบอักษรที่ฝังไว้
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    WordProcessingEditOptions wordProcessingEditOptions = new WordProcessingEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true,
        FontExtraction = FontExtractionOptions.ExtractAllEmbedded
    };
    EditableDocument editableWordProcessingDocument = editor.Edit(wordProcessingEditOptions);
}
```
## ขั้นตอนที่ 4: การสร้างและแก้ไขเอกสารสเปรดชีต
ในทำนองเดียวกัน เราสามารถสร้างและแก้ไขเอกสาร Excel ได้ นี่คือวิธีการที่คุณทำ
### สร้างและแก้ไขด้วยตัวเลือกเริ่มต้น
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    EditableDocument defaultEditableSpreadsheetDocument = editor.Edit();
}
```
### สร้างและแก้ไขด้วยตัวเลือกแบบกำหนดเอง
 ในการกำหนดเป้าหมายแผ่นงานเฉพาะหรือยกเว้นแผ่นงานที่ซ่อนอยู่เราใช้`SpreadsheetEditOptions`.
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    SpreadsheetEditOptions spreadsheetEditOptions = new SpreadsheetEditOptions
    {
        WorksheetIndex = 0,
        ExcludeHiddenWorksheets = true
    };
    EditableDocument editableSpreadsheetDocument = editor.Edit(spreadsheetEditOptions);
}
```
## ขั้นตอนที่ 5: การสร้างและแก้ไขเอกสารการนำเสนอ
รองรับการนำเสนอ PowerPoint ด้วย มาดูวิธีจัดการพวกมันกัน
### สร้างและแก้ไขด้วยตัวเลือกเริ่มต้น
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    EditableDocument defaultEditablePresentationDocument = editor.Edit();
}
```
### สร้างและแก้ไขด้วยตัวเลือกแบบกำหนดเอง
คุณสามารถปรับแต่งการแก้ไขได้โดยการระบุตัวเลือก เช่น สไลด์ที่จะแสดง และจะรวมสไลด์ที่ซ่อนไว้หรือไม่
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    PresentationEditOptions presentationEditOptions = new PresentationEditOptions
    {
        ShowHiddenSlides = false,
        SlideNumber = 0
    };
    EditableDocument editablePresentationDocument = editor.Edit(presentationEditOptions);
}
```
## ขั้นตอนที่ 6: การสร้างและแก้ไขเอกสาร Ebook
GroupDocs.Editor ยังอนุญาตให้แก้ไขรูปแบบ Ebook เช่น EPUB ได้ด้วย นี่คือวิธีที่คุณสามารถจัดการกับมันได้
### สร้างและแก้ไขด้วยตัวเลือกเริ่มต้น
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EditableDocument defaultEditableEbookDocument = editor.Edit();
}
```
### สร้างและแก้ไขด้วยตัวเลือกแบบกำหนดเอง
ปรับแต่งการแก้ไข Ebook ของคุณโดยเปิดหรือปิดใช้ข้อมูลการแบ่งหน้าและภาษา
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EbookEditOptions ebookEditOptions = new EbookEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true
    };
    EditableDocument editableEbookDocument = editor.Edit(ebookEditOptions);
}
```
## ขั้นตอนที่ 7: การสร้างและแก้ไขเอกสารอีเมล
สุดท้ายนี้ เราจะดูวิธีแก้ไขเอกสารอีเมล ซึ่งรวมถึงรูปแบบเช่น EML
### สร้างและแก้ไขด้วยตัวเลือกเริ่มต้น
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EditableDocument defaultEditableEmailDocument = editor.Edit();
}
```
### สร้างและแก้ไขด้วยตัวเลือกแบบกำหนดเอง
ระบุตัวเลือกเอาต์พุตข้อความเมลเพื่อควบคุมกระบวนการแก้ไข
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EmailEditOptions emailEditOptions = new EmailEditOptions
    {
        MailMessageOutput = MailMessageOutput.All
    };
    EditableDocument editableEmailDocument = editor.Edit(emailEditOptions);
}
```
## ขั้นตอนที่ 8: การสิ้นสุดกระบวนการ
หลังจากแก้ไขเอกสารแล้ว สิ่งสำคัญคือต้องกำจัดสตรีมหน่วยความจำอย่างเหมาะสมเพื่อเพิ่มพื้นที่ว่างทรัพยากร
```csharp
memoryStream.Dispose();
System.Console.WriteLine("CreateDocument routine has successfully finished");
```
## บทสรุป
GroupDocs.Editor สำหรับ .NET เป็นเครื่องมืออเนกประสงค์และมีประสิทธิภาพที่ช่วยลดความยุ่งยากในการแก้ไขเอกสารประเภทต่างๆ โดยทางโปรแกรม ด้วยการทำตามคำแนะนำทีละขั้นตอนนี้ คุณสามารถสร้างและแก้ไขเอกสารได้อย่างง่ายดาย ไม่ว่าจะเป็นไฟล์ประมวลผลคำ สเปรดชีต งานนำเสนอ ebooks หรืออีเมล เจาะลึกเอกสาร GroupDocs.Editor เพื่อดูคุณสมบัติขั้นสูงและตัวเลือกการปรับแต่งเพิ่มเติม
## คำถามที่พบบ่อย
### ฉันสามารถแก้ไขเอกสารประเภทใดด้วย GroupDocs.Editor สำหรับ .NET ได้บ้าง
คุณสามารถแก้ไขเอกสารได้หลากหลาย รวมถึงการประมวลผลคำ สเปรดชีต การนำเสนอ ebooks และอีเมล
### เป็นไปได้ไหมที่จะปรับแต่งตัวเลือกการแก้ไข?
ใช่ GroupDocs.Editor สำหรับ .NET ช่วยให้สามารถปรับแต่งได้อย่างกว้างขวางผ่านตัวเลือกการแก้ไขที่หลากหลายสำหรับเอกสารแต่ละประเภทโดยเฉพาะ
### ฉันจะจัดการกับผลลัพธ์ของเอกสารที่แก้ไขได้อย่างไร?
คุณสามารถใช้ฟังก์ชันโทรกลับเพื่อบันทึกสตรีมเอกสารที่แก้ไขแล้วไปยังตำแหน่งที่คุณต้องการ
### ฉันต้องมีใบอนุญาตเพื่อใช้ GroupDocs.Editor สำหรับ .NET หรือไม่
 ใช่ คุณสามารถขอรับใบอนุญาตได้จาก[ที่นี่](https://purchase.groupdocs.com/buy)- นอกจากนี้ยังมีตัวเลือกสำหรับใบอนุญาตชั่วคราว
### ฉันจะหาเอกสารรายละเอียดเพิ่มเติมได้จากที่ไหน?
 เอกสารรายละเอียดมีอยู่ที่[GroupDocs.Editor สำหรับหน้าเอกสารประกอบ .NET](https://tutorials.groupdocs.com/editor/net/).