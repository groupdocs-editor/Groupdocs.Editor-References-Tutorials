---
date: 2026-06-01
description: เรียนรู้วิธีรับจำนวนหน้าและสกัดเมตาดาต้าเอกสารโดยใช้ GroupDocs.Editor
  สำหรับ .NET ในบทแนะนำแบบละเอียดขั้นตอนต่อขั้นตอน
keywords:
- get page count
- extract document metadata
- get document info
- find document extension
- retrieve document size
linktitle: รับจำนวนหน้าและสกัดข้อมูลเอกสาร
schemas:
- author: GroupDocs
  dateModified: '2026-06-01'
  description: Learn how to get page count and extract document metadata using GroupDocs.Editor
    for .NET in a detailed step‑by‑step tutorial.
  headline: Get Page Count & Extract Document Info with GroupDocs.Editor
  type: TechArticle
- questions:
  - answer: GroupDocs.Editor supports Word processing, spreadsheet, presentation,
      PDF, and plain‑text files—over 50 formats in total.
    question: What document types can I extract metadata from?
  - answer: Access `DocumentInfo.Extension` after calling `GetDocumentInfo()`; it
      returns the extension without the leading dot.
    question: How do I retrieve the file extension?
  - answer: Yes—`DocumentInfo.Size` returns the size in bytes; divide by 1,048,576
      to convert to megabytes.
    question: Can I get the size of a document in megabytes?
  - answer: Absolutely—GroupDocs.Editor never writes the password to disk and disposes
      of all cryptographic objects after use.
    question: Is it safe to process password‑protected files on a server?
  - answer: You can get support from the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).
    question: Where can I find additional help if I run into issues?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: รับจำนวนหน้าและสกัดข้อมูลเอกสารด้วย GroupDocs.Editor
type: docs
url: /th/net/document-processing/extract-document-info/
weight: 10
---

# รับจำนวนหน้าและสกัดข้อมูลเอกสารด้วย GroupDocs.Editor

## บทนำ
ในบทแนะนำเชิงลึกนี้ คุณจะได้เรียนรู้วิธี **รับจำนวนหน้า** และสกัดข้อมูลรายละเอียดของเอกสาร—รวมถึงรูปแบบ, ขนาด, และสถานะการเข้ารหัส—โดยใช้ GroupDocs.Editor สำหรับ .NET ไม่ว่าคุณจะกำลังสร้างระบบจัดการเอกสาร, ระบบรายงาน, หรือกระบวนการแปลงอัตโนมัติ การเข้าใจเมตาดาต้าของไฟล์เป็นขั้นตอนแรกสู่การประมวลผลที่เชื่อถือได้ เราจะเดินผ่านขั้นตอนทั้งหมด ตั้งแต่การโหลดไฟล์จนถึงการปล่อยทรัพยากรอย่างปลอดภัย

## คำตอบด่วน
- **ฉันจะดึงจำนวนหน้าของเอกสารได้อย่างไร?**  
  เรียก `editor.GetDocumentInfo().PageCount` หลังจากโหลดไฟล์ด้วย `Editor`  
- **รูปแบบไฟล์ใดบ้างที่รองรับการสกัดเมตาดาต้า?**  
  มากกว่า 50 รูปแบบ รวมถึง DOCX, XLSX, PPTX, PDF, TXT, และ HTML  
- **ฉันสามารถสกัดเมตาดาต้าจากไฟล์ที่ป้องกันด้วยรหัสผ่านได้หรือไม่?**  
  ได้—ให้รหัสผ่านเมื่อสร้างอินสแตนซ์ `Editor`  
- **ฉันต้องปล่อยทรัพยากรด้วยตนเองหรือไม่?**  
  แน่นอน; ควรเรียก `editor.Dispose()` หรือใช้บล็อก `using` กับ editor  
- **ต้องใช้เวอร์ชันใดของ GroupDocs.Editor?**  
  รุ่นที่เสถียรล่าสุด (v23.12+ ณ เวลาที่เขียน) รองรับคุณลักษณะทั้งหมดที่แสดง

## “get page count” คืออะไรใน GroupDocs.Editor?
`GetDocumentInfo()` เป็นเมธอดที่คืนค่าอ็อบเจกต์ `DocumentInfo` ซึ่งบรรจุจำนวนหน้า, รูปแบบ, ขนาด และเมตาดาต้าอื่น ๆ ของเอกสาร การเรียกครั้งเดียวนี้ให้ข้อมูลโดยตรงโดยไม่ต้องพาร์สไฟล์ด้วยตนเอง การใช้เมธอดนี้ช่วยหลีกเลี่ยงการโหลดเอกสารทั้งหมดเข้าสู่หน่วยความจำ ซึ่งช่วยเพิ่มประสิทธิภาพโดยเฉพาะไฟล์ขนาดใหญ่และลดการใช้ทรัพยากรของเซิร์ฟเวอร์

## ทำไมต้องสกัดเมตาดาต้าเอกสารด้วย GroupDocs.Editor?
GroupDocs.Editor สามารถประมวลผล **รูปแบบเข้าและออกกว่า 50 ประเภท** และสกัดเมตาดาต้าสำหรับไฟล์ขนาดสูงสุด **2 GB** โดยไม่ต้องโหลดเอกสารทั้งหมดเข้าสู่หน่วยความจำ ประสิทธิภาพนี้ช่วยลดภาระเซิร์ฟเวอร์ได้ถึง **70 %** เมื่อเทียบกับการพาร์สเอกสารเต็มรูปแบบ ทำให้เหมาะกับแอปพลิเคชันที่ต้องการประมวลผลจำนวนมาก

## ข้อกำหนดเบื้องต้น
- **พื้นฐานการพัฒนา C#** – คุณควรคุ้นเคยกับ Visual Studio และโครงสร้างโครงการ .NET  
- **Visual Studio 2022** (หรือเวอร์ชันล่าสุดใดก็ได้) ที่ติดตั้งบนเครื่องของคุณ  
- **GroupDocs.Editor for .NET** – ดาวน์โหลดแพคเกจล่าสุดจาก [download page](https://releases.groupdocs.com/editor/net/)

## วิธีโหลดเอกสารของคุณ?
`Editor` เป็นคลาสหลักที่แทนเอกสารและให้เมธอดสำหรับการโหลดและจัดการ โหลดไฟล์เป้าหมายโดยสร้างอินสแตนซ์ `Editor` และส่งพาธไฟล์เข้าไป ตัว editor จะตรวจจับรูปแบบโดยอัตโนมัติ ดังนั้นคุณไม่จำเป็นต้องระบุตัวเลือกการโหลด วิธีนี้ทำงานกับไฟล์ที่รองรับทุกประเภทและทำให้การตั้งค่าเริ่มต้นง่ายขึ้น

```csharp
using System;
using GroupDocs.Editor.Metadata;
```

## วิธีดึงข้อมูลเอกสาร?
`GetDocumentInfo()` คืนค่าอ็อบเจกต์ `DocumentInfo` ที่บรรจุเมตาดาต้า เช่น จำนวนหน้า, รูปแบบ, ขนาด, และสถานะการเข้ารหัส หลังจากโหลดไฟล์แล้ว ให้เรียกเมธอดนี้เพื่อดึงอ็อบเจกต์ที่ได้ `DocumentInfo` จะให้ภาพรวมสั้น ๆ ของคุณลักษณะไฟล์ ช่วยให้คุณตัดสินใจได้โดยไม่ต้องประมวลผลต่อ

```csharp
string docxInputFilePath = "YourSampleDocument.docx";
Editor editorDocx = new Editor(docxInputFilePath);
```

## วิธีกำหนดประเภทเอกสาร?
`DocumentType` เป็น enum ที่บ่งบอกว่าเอกสารเป็น WordProcessing, Spreadsheet หรือ Text การรู้ประเภทไฟล์ช่วยกำหนดวิธีการจัดการต่อไป ใช้คุณสมบัติ `DocumentType` ของอ็อบเจกต์ `DocumentInfo` เพื่อทำการตัดสินใจและแยกสาขาโลจิกตามประเภท

```csharp
IDocumentInfo infoDocx = editorDocx.GetDocumentInfo(null);
```

## วิธีสกัดข้อมูลรายละเอียดสำหรับไฟล์ประมวลผลคำ?
`WordProcessing` หมายถึงเอกสารเช่น DOCX, ODT, และ RTF ที่จัดการเป็นไฟล์ประมวลผลคำ หาก `DocumentType` เป็น `WordProcessing` คุณสามารถอ่านคุณสมบัติเพิ่มเติมเช่น **format**, **extension**, **page count**, **size**, และ **encryption flag** ได้โดยตรงจากอ็อบเจกต์ `DocumentInfo` รายละเอียดเหล่านี้ช่วยปรับขั้นตอนการประมวลผล เช่น การแปลงเฉพาะหรือการตรวจสอบความปลอดภัย

```csharp
bool isSpreadsheet = infoDocx is SpreadsheetDocumentInfo;
bool isText = infoDocx is TextualDocumentInfo;
bool isWordProcessing = infoDocx is WordProcessingDocumentInfo;
Console.WriteLine($"Is '{docxInputFilePath}' a Spreadsheet: {isSpreadsheet}");
Console.WriteLine($"Is '{docxInputFilePath}' a Textual document: {isText}");
Console.WriteLine($"Is '{docxInputFilePath}' a WordProcessing document: {isWordProcessing}");
```

## วิธีจัดการสเปรดชีตและเอกสารข้อความ?
`Spreadsheet` หมายถึงไฟล์สเปรดชีตเช่น XLSX ส่วน `Text` แทนไฟล์ข้อความธรรมดา สำหรับสเปรดชีต (`Spreadsheet`) และไฟล์ข้อความ (`Text`) อ็อบเจกต์ `DocumentInfo` ยังให้เมตาดาต้าแกนหลัก (extension, size, page count) บางรูปแบบอาจไม่แสดงจำนวนหน้า ซึ่งค่าจะเป็น `0` คุณยังสามารถอ้างอิงเมตาดาต้าอื่น ๆ เพื่อใช้ในโลจิกต่อไปได้

```csharp
if (isWordProcessing)
{
    WordProcessingDocumentInfo casted = (WordProcessingDocumentInfo)infoDocx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Page count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```

## วิธีทำงานกับเอกสารที่ป้องกันด้วยรหัสผ่าน?
`Password` เป็นสตริงที่ส่งให้คอนสตรัคเตอร์ `Editor` เพื่อเปิดไฟล์ที่เข้ารหัส เมื่อเอกสารถูกเข้ารหัส ให้ลองเปิดโดยไม่ระบุรหัสผ่านก่อน หากล้มเหลว ให้ดักจับข้อยกเว้นแล้วลองใหม่ด้วยรหัสผ่านที่ถูกต้อง คอนสตรัคเตอร์ `Editor` ยอมรับพารามิเตอร์ `Password` เพื่อรองรับการจัดการไฟล์ที่ป้องกันอย่างราบรื่น

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

## วิธีประมวลผลเอกสารแบบข้อความ?
`DocumentInfo` ให้เมตาดาต้าเบื้องต้นเช่น ขนาด, ส่วนขยาย, และการเข้ารหัสสำหรับไฟล์ข้อความ ไฟล์ข้อความ (เช่น `.txt`, `.md`) ถูกจัดการเป็นสตรีมง่าย ๆ คุณยังคงสามารถดึงข้อมูลขนาดและการเข้ารหัสจาก `DocumentInfo` ซึ่งมีประโยชน์ในการตรวจสอบความสมบูรณ์ของไฟล์หรือกำหนดสายการประมวลผลที่เหมาะสม

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

## วิธีปล่อยทรัพยากรอย่างถูกต้อง?
`Editor` เป็นคลาสหลักที่ถือทรัพยากรที่ไม่ได้จัดการโดย .NET และต้องปล่อยหลังการใช้งาน เพื่อป้องกันการรั่วไหลของหน่วยความจำ ควรปล่อยอินสแตนซ์ `Editor` เสมอหลังจากดึงข้อมูลเสร็จ การใช้คำสั่ง `using` เป็นรูปแบบที่ปลอดภัยที่สุด เพราะมันรับประกันการปล่อยทรัพยากรแม้เกิดข้อยกเว้น ทำให้การจัดการทรัพยากรเป็นระเบียบ

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

## ปัญหาทั่วไปและวิธีแก้ไข
| ปัญหา | สาเหตุ | วิธีแก้ไข |
|-------|-------|----------|
| **PageCount returns 0** | รูปแบบไม่รองรับการแบ่งหน้า (เช่น plain text) | ตรวจสอบ `DocumentInfo.DocumentType` ก่อนพึ่งพา `PageCount`. |
| **Unsupported file format** | ส่วนขยายไฟล์ไม่ถูกจดจำ | ตรวจสอบว่าไฟล์เป็นหนึ่งในรูปแบบที่รองรับกว่า 50 รูปแบบ; อัปเดต GroupDocs.Editor เป็นเวอร์ชันล่าสุด. |
| **Password exception** | รหัสผ่านที่ให้ไม่ถูกต้อง | ดักจับ `PasswordProtectedException` แล้วแจ้งผู้ใช้ให้ใส่รหัสผ่านใหม่. |
| **Memory spike on large files** | โหลด PDF ขนาดใหญ่มากโดยไม่ใช้การสตรีม | ใช้ `LoadOptions` กับ `LoadOptions.LoadMode = LoadMode.Stream` (มีในรุ่นใหม่กว่า). |

## คำถามที่พบบ่อย

**Q: ฉันสามารถสกัดเมตาดาต้าจากประเภทเอกสารใดได้บ้าง?**  
A: GroupDocs.Editor รองรับไฟล์ประมวลผลคำ, สเปรดชีต, พรีเซนเทชัน, PDF, และไฟล์ข้อความธรรมดา—รวมกว่า 50 รูปแบบทั้งหมด.

**Q: ฉันจะดึงส่วนขยายไฟล์ได้อย่างไร?**  
A: เข้าถึง `DocumentInfo.Extension` หลังจากเรียก `GetDocumentInfo()`; จะคืนค่าส่วนขยายโดยไม่มีจุดนำหน้า.

**Q: ฉันสามารถรับขนาดของเอกสารเป็นเมกะไบต์ได้หรือไม่?**  
A: ได้—`DocumentInfo.Size` คืนค่าขนาดเป็นไบต์; หารด้วย 1,048,576 เพื่อแปลงเป็นเมกะไบต์.

**Q: การประมวลผลไฟล์ที่ป้องกันด้วยรหัสผ่านบนเซิร์ฟเวอร์ปลอดภัยหรือไม่?**  
A: แน่นอน—GroupDocs.Editor ไม่เคยเขียนรหัสผ่านลงดิสก์และทำลายอ็อบเจกต์การเข้ารหัสทั้งหมดหลังการใช้งาน.

**Q: ฉันจะหาแนวทางช่วยเหลือเพิ่มเติมได้จากที่ไหนหากเจอปัญหา?**  
A: คุณสามารถรับการสนับสนุนจาก [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).

---

**อัปเดตล่าสุด:** 2026-06-01  
**ทดสอบกับ:** GroupDocs.Editor 23.12 for .NET  
**ผู้เขียน:** GroupDocs

```csharp
editorDocx.Dispose();
editorXlsx.Dispose();
editorXls.Dispose();
editorXml.Dispose();
Console.WriteLine("ExtractingDocumentInfo routine has successfully finished");
```

## บทแนะนำที่เกี่ยวข้อง

- [คู่มือการสกัดเมตาดาต้าอย่างครบถ้วนใน .NET ด้วย GroupDocs.Editor: A Comprehensive Guide](/editor/net/advanced-features/groupdocs-editor-net-metadata-extraction-guide/)
- [บทแนะนำการโหลดเอกสารด้วย GroupDocs.Editor สำหรับ .NET](/editor/net/document-loading/)
- [การแก้ไขเอกสารอย่างมีประสิทธิภาพด้วย GroupDocs.Editor .NET: แปลง HTML เป็นเอกสารที่แก้ไขได้](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)