---
date: 2026-09-21
description: เรียนรู้วิธีแก้ไข PowerPoint โดยไม่ต้องใช้ Office ด้วย GroupDocs.Editor
  for .NET, แก้ไข Word, Excel, EPUB และบันทึก document stream ที่แก้ไข
keywords:
- edit powerpoint without office
- GroupDocs.Editor .NET
- document editing .NET
- edit presentation programmatically
lastmod: 2026-09-21
linktitle: สร้างเอกสาร
og_description: แก้ไข Powerpoint โดยไม่ต้องใช้ Office ด้วย GroupDocs.Editor for .NET.
  คู่มือนี้แสดงวิธีปรับเปลี่ยนการนำเสนอ, Word, Excel, EPUB และบันทึก document streams
  ที่แก้ไข
og_image_alt: Guide showing code to edit PowerPoint presentations without Microsoft
  Office using GroupDocs.Editor for .NET
og_title: แก้ไข Powerpoint โดยไม่ต้องใช้ Office ด้วย GroupDocs.Editor for .NET
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to edit PowerPoint without Office using GroupDocs.Editor
    for .NET, edit Word, Excel, EPUB and capture the edited document stream.
  headline: Edit powerpoint without office with GroupDocs.Editor for .NET
  type: TechArticle
- questions:
  - answer: You can edit WordProcessing, spreadsheets, presentations, ebooks, and
      emails—including PowerPoint files for the **edit powerpoint without office**
      use case.
    question: What types of documents can I edit with GroupDocs.Editor for .NET?
  - answer: Yes, each format has its own options class (e.g., `WordProcessingEditOptions`,
      `SpreadsheetEditOptions`, `PresentationEditOptions`) that let you fine‑tune
      pagination, hidden slides, worksheet selection, etc.
    question: Is it possible to customize the editing options?
  - answer: Use the callback function (`SaveNewDocument`) to capture the edited stream,
      then you can write it to disk, a database, or return it from a web API.
    question: How do I handle the output of the edited documents?
  - answer: Yes, a license is required for production. You can obtain one from the
      [GroupDocs.Editor purchase page](https://purchase.groupdocs.com/buy). A temporary
      trial license is also available.
    question: Do I need a license to use GroupDocs.Editor for .NET?
  - answer: Detailed documentation is available on the [GroupDocs.Editor for .NET
      documentation page](https://tutorials.groupdocs.com/editor/net/).
    question: Where can I find more detailed documentation?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
tags:
- edit powerpoint
- GroupDocs.Editor
- .NET document processing
title: แก้ไข Powerpoint โดยไม่ต้องใช้ Office ด้วย GroupDocs.Editor for .NET
type: docs
url: /th/net/document-editing/create-document/
weight: 10
---

# แก้ไข Powerpoint โดยไม่ใช้ Office ด้วย GroupDocs.Editor สำหรับ .NET

## บทนำ
หากคุณกำลังมองหาวิธีที่เชื่อถือได้ในการ **แก้ไข PowerPoint โดยไม่ใช้ Office** ผ่านโปรแกรม, GroupDocs.Editor สำหรับ .NET คือคำตอบ ไลบรารีนี้ช่วยให้คุณทำงานกับรูปแบบ Word, Excel, PowerPoint, Ebook, และ Email — ทั้งหมดจาก API เดียวที่ใช้งานง่าย ในบทเรียนนี้เราจะอธิบายขั้นตอนการสร้างและแก้ไขเอกสารแต่ละประเภทที่รองรับ, แสดงวิธี **บันทึกสตรีมเอกสารที่แก้ไข** และให้คำแนะนำที่สามารถนำไปใช้ในโครงการจริงได้

## คำตอบอย่างรวดเร็ว
- **ไลบรารีใดที่ทำให้ฉันแก้ไขไฟล์ PowerPoint ใน .NET ได้?** GroupDocs.Editor for .NET.  
- **ฉันสามารถแก้ไขไฟล์ Word, Excel และ Epub ด้วย API เดียวกันได้หรือไม่?** ใช่, คลาส `Editor` เดียวกันรองรับรูปแบบทั้งหมดเหล่านั้น.  
- **ฉันจะจับไฟล์ที่แก้ไขได้อย่างไร?** ให้ฟังก์ชัน callback (เช่น `SaveNewDocument`) ที่รับสตรีมผลลัพธ์.  
- **ฉันต้องการไลเซนส์สำหรับการใช้งานในโปรดักชันหรือไม่?** ใช่ — ซื้อไลเซนส์หรือใช้ไลเซนส์ทดลองชั่วคราว.  
- **เวอร์ชัน .NET ใดที่รองรับ?** .NET Framework 4.0+, .NET Core, และ .NET 5/6.

## อะไรคือการแก้ไข PowerPoint โดยไม่ใช้ Office?
การแก้ไขงานนำเสนอ PowerPoint โดยไม่ใช้ Office หมายถึงการโหลดไฟล์ `.pptx`, ทำการเปลี่ยนแปลงเช่นการแก้ไขสไลด์, ข้อความ หรือองค์ประกอบที่ซ่อนอยู่, แล้วดึงไฟล์ที่อัปเดตออกมา — ทั้งหมดโดยไม่ต้องติดตั้ง Microsoft PowerPoint บนเซิร์ฟเวอร์

## ทำไมต้องใช้ GroupDocs.Editor สำหรับ .NET?
GroupDocs.Editor รองรับ **ประเภทเอกสารหลักกว่า 5 ประเภท** (Word, Excel, PowerPoint, EPUB, Email) และสามารถประมวลผลไฟล์ขนาดสูงสุด **500 MB** ในขณะที่ใช้หน่วยความจำไม่เกิน **100 MB** ด้วยสถาปัตยกรรมแบบสตรีม ไลบรารีนี้ทำงานบน **Windows, Linux, และ macOS** ทำให้เหมาะสำหรับบริการคลาวด์‑เนทีฟ, CI pipelines, และงานที่รันในคอนเทนเนอร์

## ข้อกำหนดเบื้องต้น
- Visual Studio (รุ่นล่าสุดใดก็ได้).  
- .NET Framework 4.0 หรือสูงกว่า (หรือ .NET Core/.NET 5+).  
- GroupDocs.Editor for .NET library – [download the GroupDocs.Editor for .NET library](https://releases.groupdocs.com/editor/net/).  
- ความรู้พื้นฐานของ C#.

## นำเข้าเนมสเปซ
คลาส `Editor` อยู่ในเนมสเปซ `GroupDocs.Editor`, ส่วนคลาสตัวเลือกที่เฉพาะรูปแบบจะอยู่ในซับเนมสเปซของตนเอง  

`Editor` คือคลาสหลักที่โหลดเอกสาร, เปิดเผยการแสดงผลที่สามารถแก้ไขได้, และเขียนเนื้อหาที่แก้ไขกลับไปยังสตรีม.  

```csharp
using GroupDocs.Editor;
using GroupDocs.Editor.Options;
using System.IO;
```

```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using System.IO;
```

## ขั้นตอนที่ 1: ตั้งค่า stream
การทำงานกับสตรีมช่วยให้คุณเก็บกระบวนการทั้งหมดในหน่วยความจำ, ซึ่งเหมาะอย่างยิ่งสำหรับเว็บ API หรือฟังก์ชันแบบ serverless.  

`MemoryStream` เป็นบัฟเฟอร์ที่เบาและขยายได้ซึ่งจำลองไฟล์บนดิสก์แต่คงอยู่ใน RAM.  

```csharp
byte[] fileBytes = File.ReadAllBytes("sample.pptx");
var inputStream = new MemoryStream(fileBytes);
```

```csharp
Stream memoryStream = Stream.Null;
```

## ขั้นตอนที่ 2: ฟังก์ชัน callback เพื่อ **บันทึกเอกสารที่แก้ไข**
Callback จะรับสตรีมที่แก้ไขหลังจาก `Editor` ประมวลผลเสร็จ คุณสามารถเขียนลงดิสก์, ฐานข้อมูล, หรือส่งกลับจาก endpoint ของ API ได้.  

`SaveNewDocument` คือเมธอดที่ผู้ใช้กำหนดซึ่ง SDK จะเรียกโดยอัตโนมัติเมื่อการแก้ไขเสร็จสิ้น.  

```csharp
void SaveNewDocument(Stream editedStream)
{
    using var file = File.Create("output.pptx");
    editedStream.CopyTo(file);
}
```

```csharp
void SaveNewDocument(Stream resultStream)
{
    memoryStream = resultStream;
}
```

## ขั้นตอนที่ 3: การสร้างและแก้ไขเอกสารการประมวลผลคำ  
(ที่นี่เราจะ **แก้ไขเอกสาร Word .net**.)  

### สร้างและแก้ไขด้วยตัวเลือกเริ่มต้น
คลาส `WordProcessingEditOptions` ให้ค่าตั้งต้นที่เหมาะสมสำหรับไฟล์ DOCX.  

`WordProcessingEditOptions` กำหนดวิธีที่ตัวแก้ไขจัดการการแบ่งหน้า, การติดตามการเปลี่ยนแปลง, และออบเจ็กต์ที่ฝังอยู่.  

```csharp
var editor = new Editor(inputStream, new WordProcessingEditOptions());
var editable = editor.Edit();
editable.Replace("{Placeholder}", "Actual value");
editor.Save(SaveNewDocument);
```

```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    EditableDocument defaultWordProcessingDoc = editor.Edit();
}
```

### สร้างและแก้ไขด้วยตัวเลือกกำหนดเอง
คุณสามารถเปิดหรือปิดฟีเจอร์เฉพาะเช่นการตรวจสอบการสะกดหรือการติดตามการเปลี่ยนแปลง.  

`WordProcessingEditOptions` ให้คุณเปิดใช้งาน `EnableTrackChanges` เพื่อบันทึกการตรวจสอบ.  

```csharp
var options = new WordProcessingEditOptions
{
    EnableTrackChanges = true,
    EnableSpellCheck = false
};
var editor = new Editor(inputStream, options);
```

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
(ใช้เพื่อ **แก้ไขไฟล์ Excel .net**.)  

### สร้างและแก้ไขด้วยตัวเลือกเริ่มต้น
`SpreadsheetEditOptions` ควบคุมว่าเวิร์กชีตใดจะถูกโหลดและว่าจะประเมินสูตรหรือไม่.  

`SpreadsheetEditOptions` เลือกเวิร์กชีตแรกเป็นค่าเริ่มต้น.  

```csharp
var editor = new Editor(inputStream, new SpreadsheetEditOptions());
var editable = editor.Edit();
editable.ReplaceCell("A1", "42");
editor.Save(SaveNewDocument);
```

```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    EditableDocument defaultEditableSpreadsheetDocument = editor.Edit();
}
```

### สร้างและแก้ไขด้วยตัวเลือกกำหนดเอง
คุณสามารถระบุดัชนีเวิร์กชีตอื่นหรือปิดการประเมินสูตรเพื่อประสิทธิภาพ.  

`SpreadsheetEditOptions` ให้คุณตั้งค่า `WorksheetIndex` และ `EnableFormulaEvaluation`.  

```csharp
var options = new SpreadsheetEditOptions
{
    WorksheetIndex = 2,
    EnableFormulaEvaluation = false
};
var editor = new Editor(inputStream, options);
```

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

## ขั้นตอนที่ 5: แก้ไข Powerpoint โดยไม่ใช้ Office – การสร้างและแก้ไขเอกสารพรีเซนเทชัน
### สร้างและแก้ไขด้วยตัวเลือกเริ่มต้น
`PresentationEditOptions` กำหนดว่าจะรวมสไลด์ที่ซ่อนอยู่หรือไม่และสไลด์ใดเป็นเป้าหมายการแก้ไขเริ่มต้น.  

`PresentationEditOptions` รวมสไลด์ที่ซ่อนอยู่เป็นค่าเริ่มต้น, คุณสามารถสลับได้.  

```csharp
var editor = new Editor(inputStream, new PresentationEditOptions());
var editable = editor.Edit();
editable.ReplaceSlideText(0, "{Title}", "Quarterly Report");
editor.Save(SaveNewDocument);
```

```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    EditableDocument defaultEditablePresentationDocument = editor.Edit();
}
```

### สร้างและแก้ไขด้วยตัวเลือกกำหนดเอง
คุณสามารถเปลี่ยน `SlideNumber` เพื่อแก้ไขสไลด์เฉพาะ, หรือปิดการรวมหน้าบันทึกย่อ.  

`PresentationEditOptions` ให้คุณตั้งค่า `SlideNumber` และ `IncludeNotes`.  

```csharp
var options = new PresentationEditOptions
{
    SlideNumber = 2,
    IncludeNotes = false
};
var editor = new Editor(inputStream, options);
```

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

## ขั้นตอนที่ 6: การสร้างและแก้ไขเอกสารอีบุ๊ค  
(ที่นี่เราจะ **แก้ไขไฟล์ epub**.)  

### สร้างและแก้ไขด้วยตัวเลือกเริ่มต้น
`EbookEditOptions` จัดการการแปลงระหว่าง EPUB กับการแสดงผล HTML ภายใน.  

`EbookEditOptions` ใช้ตัวเรนเดอร์ HTML เริ่มต้นสำหรับเนื้อหา EPUB.  

```csharp
var editor = new Editor(inputStream, new EbookEditOptions());
var editable = editor.Edit();
editable.Replace("{Author}", "Jane Doe");
editor.Save(SaveNewDocument);
```

```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EditableDocument defaultEditableEbookDocument = editor.Edit();
}
```

### สร้างและแก้ไขด้วยตัวเลือกกำหนดเอง
คุณสามารถรักษา CSS ดั้งเดิมหรือบังคับให้เป็นการจัดวางแบบข้อความธรรมดา.  

`EbookEditOptions` มีแฟล็ก `PreserveCss` และ `PlainTextOnly`.  

```csharp
var options = new EbookEditOptions
{
    PreserveCss = true,
    PlainTextOnly = false
};
var editor = new Editor(inputStream, options);
```

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
### สร้างและแก้ไขด้วยตัวเลือกเริ่มต้น
`EmailEditOptions` ให้คุณจัดการเนื้อหา, หัวเรื่อง, และไฟล์แนบของไฟล์ .eml.  

`EmailEditOptions` โหลดเนื้อหาอีเมลเป็นข้อความธรรมดาสำหรับการแทนที่ง่าย.  

```csharp
var editor = new Editor(inputStream, new EmailEditOptions());
var editable = editor.Edit();
editable.Replace("{Recipient}", "john@example.com");
editor.Save(SaveNewDocument);
```

```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EditableDocument defaultEditableEmailDocument = editor.Edit();
}
```

### สร้างและแก้ไขด้วยตัวเลือกกำหนดเอง
คุณสามารถเก็บส่วนหัว MIME ดั้งเดิมหรือกำจัดเพื่อให้ได้เวอร์ชันข้อความที่สะอาด.  

`EmailEditOptions` มี `KeepHeaders` เพื่อรักษาหรือทิ้งเมตาดาต้า MIME.  

```csharp
var options = new EmailEditOptions
{
    KeepHeaders = false
};
var editor = new Editor(inputStream, options);
```

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

## ขั้นตอนที่ 8: สรุปกระบวนการ
ทำการ Dispose สตรีมเพื่อปล่อยทรัพยากรเมื่อเสร็จสิ้น การทำ Dispose อย่างเหมาะสมป้องกันการรั่วไหลของหน่วยความจำในบริการที่ทำงานต่อเนื่องเป็นเวลานาน เช่น เว็บ API หรือ background worker.  

```csharp
inputStream.Dispose();
```

```csharp
memoryStream.Dispose();
System.Console.WriteLine("CreateDocument routine has successfully finished");
```

## ข้อผิดพลาดทั่วไป & เคล็ดลับ
- **ห้ามลืมทำ Dispose สตรีม** – การเปิดไว้โดยไม่ปิดอาจทำให้เกิดการรั่วไหลของหน่วยความจำในบริการที่ทำงานต่อเนื่อง.  
- **เมื่อแก้ไข PowerPoint, ตรวจสอบให้แน่ใจว่าคุณตั้งค่า `SlideNumber` อย่างถูกต้อง**; มิฉะนั้นสไลด์แรกอาจถูกทำซ้ำ.  
- **หากต้องการเก็บชื่อไฟล์ต้นฉบับ**, ให้บันทึกไว้ก่อน callback และเปลี่ยนชื่อสตรีมผลลัพธ์หลังการแก้ไข.  
- **สำหรับเอกสารขนาดใหญ่**, พิจารณาประมวลผลเป็นชิ้นส่วนหรือใช้ `Editor` กับไฟล์ชั่วคราวเพื่อหลีกเลี่ยงการใช้หน่วยความจำสูง.  
- **เปิดการบันทึก** ผ่าน `EditorOptions` หากคุณต้องการแก้ไขปัญหาพฤติกรรมที่ไม่คาดคิดในโปรดักชัน.

## คำถามที่พบบ่อย

**Q: ฉันสามารถแก้ไขประเภทเอกสารใดบ้างด้วย GroupDocs.Editor สำหรับ .NET?**  
A: คุณสามารถแก้ไข WordProcessing, spreadsheets, presentations, ebooks, และ emails — รวมถึงไฟล์ PowerPoint สำหรับกรณีการ **แก้ไข PowerPoint โดยไม่ใช้ Office**.  

**Q: สามารถปรับแต่งตัวเลือกการแก้ไขได้หรือไม่?**  
A: ได้, แต่ละรูปแบบมีคลาสตัวเลือกของตนเอง (เช่น `WordProcessingEditOptions`, `SpreadsheetEditOptions`, `PresentationEditOptions`) ที่ให้คุณปรับแต่งการแบ่งหน้า, สไลด์ที่ซ่อน, การเลือกเวิร์กชีต ฯลฯ.  

**Q: ฉันจะจัดการกับผลลัพธ์ของเอกสารที่แก้ไขอย่างไร?**  
A: ใช้ฟังก์ชัน callback (`SaveNewDocument`) เพื่อจับสตรีมที่แก้ไข, จากนั้นคุณสามารถเขียนลงดิสก์, ฐานข้อมูล, หรือส่งกลับจากเว็บ API.  

**Q: ฉันต้องการไลเซนส์เพื่อใช้ GroupDocs.Editor สำหรับ .NET หรือไม่?**  
A: ใช่, จำเป็นต้องมีไลเซนส์สำหรับการใช้งานในโปรดักชัน คุณสามารถซื้อได้จาก [GroupDocs.Editor purchase page](https://purchase.groupdocs.com/buy). ไลเซนส์ทดลองชั่วคราวก็มีให้เช่นกัน.  

**Q: ฉันจะหาเอกสารรายละเอียดเพิ่มเติมได้จากที่ไหน?**  
A: เอกสารรายละเอียดพร้อมให้บริการบน [GroupDocs.Editor for .NET documentation page](https://tutorials.groupdocs.com/editor/net/).  

## สรุป
GroupDocs.Editor สำหรับ .NET ทำให้การ **แก้ไข Powerpoint โดยไม่ใช้ Office** และประเภทเอกสารอื่น ๆ เป็นเรื่องง่าย ด้วยการทำตามขั้นตอนข้างต้นคุณสามารถสร้าง, แก้ไข, และ **บันทึกสตรีมเอกสารที่แก้ไข** ทั้งหมดในโค้ดโดยไม่ต้องพึ่งพาการติดตั้ง Office สำรวจตัวเลือกขั้นสูงของไลบรารีเพื่อปรับประสบการณ์การแก้ไขให้ตรงกับความต้องการของธุรกิจของคุณ

---

**อัปเดตล่าสุด:** 2026-09-21  
**ทดสอบด้วย:** GroupDocs.Editor for .NET (latest release)  
**ผู้เขียน:** GroupDocs

## บทแนะนำที่เกี่ยวข้อง

- [บทแนะนำการแก้ไขเอกสารพรีเซนเทชันสำหรับ GroupDocs.Editor .NET](/editor/net/presentation-documents/)
- [สร้างเอกสารที่แก้ไขได้ด้วย GroupDocs.Editor .NET](/editor/net/document-editing/groupdocs-editor-net-edit-manage-documents-guide/)
- [โหลดเอกสารโดยไม่มีตัวเลือกใน .NET ด้วย GroupDocs.Editor – คู่มือฉบับสมบูรณ์](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)