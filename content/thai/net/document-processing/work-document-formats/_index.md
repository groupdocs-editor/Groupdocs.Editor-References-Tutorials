---
date: 2026-06-06
description: เรียนรู้วิธีการแสดงรายการรูปแบบเอกสารที่รองรับและกำหนดนามสกุลไฟล์โดยใช้
  GroupDocs.Editor สำหรับ .NET คู่มือขั้นตอนโดยละเอียดพร้อมตัวอย่างโค้ด คำตอบสั้น
  ๆ และคำถามที่พบบ่อย
keywords:
- list supported document formats
- determine file format extension
- GroupDocs.Editor .NET
- document editing API
- supported formats guide
linktitle: รายการรูปแบบเอกสารที่รองรับ
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to list supported document formats and determine file format
    extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets,
    quick answers, and FAQs.
  headline: List Supported Document Formats with GroupDocs.Editor .NET
  type: TechArticle
- description: Learn how to list supported document formats and determine file format
    extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets,
    quick answers, and FAQs.
  name: List Supported Document Formats with GroupDocs.Editor .NET
  steps:
  - name: '**.NET development environment** – Visual Studio 2022 or any IDE that supports
      .NET 6+.'
    text: '**.NET development environment** – Visual Studio 2022 or any IDE that supports
      .NET 6+.'
  - name: '**GroupDocs.Editor for .NET library** – download from the [GroupDocs releases
      page](https://releases.groupdocs.com/editor/net/).'
    text: '**GroupDocs.Editor for .NET library** – download from the [GroupDocs releases
      page](https://releases.groupdocs.com/editor/net/).'
  - name: '**Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/)
      for unrestricted access.'
    text: '**Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/)
      for unrestricted access.'
  - name: '**Basic C# knowledge** – familiarity with namespaces, `using` statements,
      and console output.'
    text: '**Basic C# knowledge** – familiarity with namespaces, `using` statements,
      and console output.'
  - name: '**Loop Through Formats:** We iterate over all available Word‑processing
      formats.'
    text: '**Loop Through Formats:** We iterate over all available Word‑processing
      formats.'
  - name: '**Output Format Details:** For each format we print its friendly name and
      default file extension.'
    text: '**Output Format Details:** For each format we print its friendly name and
      default file extension.'
  - name: '**Loop Through Formats:** The same looping logic applies to presentations.'
    text: '**Loop Through Formats:** The same looping logic applies to presentations.'
  - name: '**Output Format Details:** The name and extension are displayed for each
      format.'
    text: '**Output Format Details:** The name and extension are displayed for each
      format.'
  - name: '**Parse Format:** `FromExtension` converts the `.xlsm` extension into its
      internal `SpreadsheetFormat` enum.'
    text: '**Parse Format:** `FromExtension` converts the `.xlsm` extension into its
      internal `SpreadsheetFormat` enum.'
  - name: '**Output Format:** The parsed format’s name is printed, confirming the
      mapping.'
    text: '**Output Format:** The parsed format’s name is printed, confirming the
      mapping.'
  type: HowTo
- questions:
  - answer: '`DocumentFormatInfo` provides metadata about supported file types, while
      `SaveOptions` configures how a document is written back to disk (format, compression,
      etc.).'
    question: What is the difference between `DocumentFormatInfo` and `SaveOptions`?
  - answer: Yes—use `DocumentFormatInfo.FromExtension("yourExt")`; if the extension
      isn’t recognized, the method returns `null`.
    question: Can I list formats for a custom file extension?
  - answer: Absolutely. Pass the password to the `Editor` constructor via `EditorSettings`
      to open encrypted documents.
    question: Does GroupDocs.Editor support password‑protected files?
  - answer: Over **30 input and output formats**, spanning Word, Excel, PowerPoint,
      HTML, and plain text.
    question: How many formats does GroupDocs.Editor actually support?
  - answer: Use the `GetEditableWordProcessingFormats()` (or Spreadsheet/Presentation
      equivalents) to retrieve formats that allow full edit capabilities.
    question: Is there a way to restrict the list to only editable formats?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: รายการรูปแบบเอกสารที่รองรับด้วย GroupDocs.Editor .NET
type: docs
url: /th/net/document-processing/work-document-formats/
weight: 13
---

# รายการรูปแบบเอกสารที่รองรับ

ยินดีต้อนรับสู่บทแนะนำเชิงลึกของเราเกี่ยวกับ **วิธีแสดงรายการรูปแบบเอกสารที่รองรับ** ด้วย GroupDocs.Editor สำหรับ .NET ไม่ว่าคุณจะกำลังสร้างแอปเว็บที่เน้นเอกสารหรือเครื่องมือเดสก์ท็อประดับองค์กร การรู้ว่ารูปแบบใดที่คุณสามารถแก้ไขหรือแปลงได้อย่างแม่นยำเป็นสิ่งสำคัญ ในคู่มือนี้คุณจะได้ค้นพบวิธีการนับรายการรูปแบบ การแยกส่วนต่อขยายไฟล์ และการแก้ไขเอกสาร—ทั้งหมดด้วยคำอธิบายที่ชัดเจนและเป็นมิตรต่อผู้ใช้ พร้อมโค้ดตัวอย่างที่พร้อมรัน

## คำตอบด่วน
- **ฉันจะลิสต์รูปแบบที่รองรับทั้งหมดได้อย่างไร?** ใช้ `DocumentFormatInfo.GetSupportedWordProcessingFormats()` (หรือเทียบเท่าสำหรับ Presentation/Spreadsheet) และวนลูปคอลเลกชัน.  
- **ฉันสามารถกำหนดรูปแบบจากส่วนต่อขยายไฟล์ได้หรือไม่?** ใช่—เรียก `DocumentFormatInfo.FromExtension(".docx")`.  
- **GroupDocs.Editor รองรับประเภทไฟล์อะไรบ้าง?** มากกว่า 30 รูปแบบการนำเข้าและส่งออก รวมถึง DOCX, XLSX, PPTX, HTML และข้อความธรรมดา.  
- **ฉันต้องมีลิขสิทธิ์เพื่อแสดงรายการรูปแบบหรือไม่?** ลิขสิทธิ์ชั่วคราวจะปลดล็อก API ทั้งหมด; หากไม่เช่นนั้น การทดลองใช้งานจะทำงานด้วยคุณสมบัติที่จำกัด.  
- **เวอร์ชัน .NET ใดที่เข้ากันได้?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.

## “การแสดงรายการรูปแบบเอกสารที่รองรับ” คืออะไร
วลีนี้หมายถึงการดึงข้อมูลคอลเลกชันของประเภทไฟล์ที่ GroupDocs.Editor สามารถเปิด, แก้ไขและบันทึกได้โดยโปรแกรม การทำเช่นนี้ช่วยให้คุณสร้างเมนูดรอปดาวน์ UI แบบไดนามิกหรือทำการตรวจสอบไฟล์ที่ผู้ใช้อัปโหลดก่อนประมวลผล เพื่อให้แน่ใจว่าไฟล์ที่ส่งไปยังเอดิเตอร์เป็นไฟล์ที่เข้ากันได้เท่านั้น

## ทำไมต้องแสดงรายการรูปแบบเอกสารที่รองรับ
GroupDocs.Editor **รองรับรูปแบบการนำเข้าและส่งออกกว่า 30 ประเภท** และสามารถจัดการไฟล์ขนาด **สูงสุด 2 GB** โดยไม่ต้องโหลดเอกสารทั้งหมดเข้าสู่หน่วยความจำ การรู้รายการที่แน่นอนช่วยป้องกันข้อผิดพลาดขณะรัน, ปรับปรุงประสบการณ์ผู้ใช้, และทำให้คุณสามารถบังคับใช้กฎธุรกิจเช่น “อนุญาตเฉพาะเอกสาร Office ที่สามารถแก้ไขได้” นอกจากนี้ยังช่วยให้คุณแสดงเฉพาะรูปแบบที่แอปของคุณรองรับจริงต่อผู้ใช้

## ข้อกำหนดเบื้องต้น
ก่อนเริ่มทำงาน โปรดตรวจสอบว่าคุณมี:

1. **สภาพแวดล้อมการพัฒนา .NET** – Visual Studio 2022 หรือ IDE ใด ๆ ที่รองรับ .NET 6+.  
2. **ไลบรารี GroupDocs.Editor for .NET** – ดาวน์โหลดจาก [GroupDocs releases page](https://releases.groupdocs.com/editor/net/).  
3. **ลิขสิทธิ์ชั่วคราว** – รับ [temporary license](https://purchase.groupdocs.com/temporary-license/) เพื่อเข้าถึงแบบไม่จำกัด.  
4. **ความรู้พื้นฐานของ C#** – คุ้นเคยกับ namespaces, คำสั่ง `using`, และการแสดงผลบนคอนโซล.

## วิธีแสดงรายการรูปแบบเอกสารที่รองรับ?
โหลดคอลเลกชันของรูปแบบที่รองรับและพิมพ์ชื่อและส่วนต่อขยายของแต่ละรูปแบบ รูปแบบสองขั้นตอนนี้ทำงานได้กับเอกสาร Word Processing, Spreadsheet, และ Presentation โดยการวนลูปคอลเลกชันคุณสามารถเติมข้อมูลให้กับองค์ประกอบ UI เช่น ดรอปดาวน์ เพื่อให้ผู้ใช้เลือกได้เฉพาะรูปแบบที่เอดิเตอร์สามารถจัดการได้จริง

```csharp
// No actual code block – placeholder retained from original tutorial
```csharp
using System;
using GroupDocs.Editor.Options;
```
```

### การแสดงรายการรูปแบบการประมวลผลคำ
`Formats.WordProcessingFormats` เป็น enumeration ที่อธิบายทุกประเภทไฟล์การประมวลผลคำที่เอดิเตอร์รับรู้ property `All` จะคืนคอลเลกชันของอ็อบเจกต์รูปแบบเหล่านี้

```csharp
```csharp
foreach (Formats.WordProcessingFormats oneFormat in Formats.WordProcessingFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**คำอธิบาย:**  
1. **วนลูปผ่านรูปแบบ:** เรา iterate ผ่านรูปแบบการประมวลผลคำทั้งหมดที่มี.  
2. **แสดงรายละเอียดรูปแบบ:** สำหรับแต่ละรูปแบบเราพิมพ์ชื่อที่เป็นมิตรและส่วนต่อขยายไฟล์เริ่มต้น.

### การแสดงรายการรูปแบบการนำเสนอ
`Formats.PresentationFormats` ทำงานเช่นเดียวกันสำหรับไฟล์สไลด์เด็ค โดยเปิดเผยแต่ละประเภทการนำเสนอที่รองรับผ่านคอลเลกชัน `All`

```csharp
```csharp
foreach (Formats.PresentationFormats oneFormat in Formats.PresentationFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**คำอธิบาย:**  
1. **วนลูปผ่านรูปแบบ:** โลจิกการวนลูปเดียวกันใช้กับการนำเสนอ.  
2. **แสดงรายละเอียดรูปแบบ:** ชื่อและส่วนต่อขยายจะแสดงสำหรับแต่ละรูปแบบ.

## วิธีกำหนดส่วนต่อขยายรูปแบบไฟล์?
บางครั้งคุณอาจมีเพียงชื่อไฟล์และต้องสรุป `DocumentFormat` ที่สอดคล้อง GroupDocs.Editor มีตัวช่วยแบบ static ที่แมปส่วนต่อขยายไฟล์ไปยังรูปแบบภายใน ช่วยให้คุณตรวจสอบหรือแปลงไฟล์ก่อนโหลดเข้าสู่เอดิเตอร์

### การแยกรูปแบบสเปรดชีต
`Formats.SpreadsheetFormats.FromExtension` แปลงสตริงส่วนต่อขยายไฟล์เป็นค่า enum ของรูปแบบสเปรดชีตที่ตรงกัน

```csharp
```csharp
Formats.SpreadsheetFormats expectedXlsm = Formats.SpreadsheetFormats.FromExtension(".xlsm");
Console.WriteLine("Parsed Spreadsheet format is {0}", expectedXlsm.Name);
```
```

**คำอธิบาย:**  
1. **แปลงรูปแบบ:** `FromExtension` แปลงส่วนต่อขยาย `.xlsm` ให้เป็นค่า `SpreadsheetFormat` ภายใน.  
2. **แสดงรูปแบบ:** พิมพ์ชื่อของรูปแบบที่แปลงแล้วเพื่อยืนยันการแมป.

### การแยกรูปแบบข้อความ
ในทำนองเดียวกัน `Formats.TextualFormats.FromExtension` จะระบุส่วนต่อขยายไฟล์ข้อความเช่น HTML หรือ TXT

```csharp
```csharp
Formats.TextualFormats expectedHtml = Formats.TextualFormats.FromExtension("html");
Console.WriteLine("Parsed Textual format is {0}", expectedHtml.Name);
```
```

**คำอธิบาย:**  
1. **แปลงรูปแบบ:** เมธอด `FromExtension` ระบุส่วนต่อขยาย `html` ให้เป็น `TextFormat`.  
2. **แสดงรูปแบบ:** ชื่อของรูปแบบข้อความจะแสดงออกมา มีประโยชน์สำหรับเอดิเตอร์บนเว็บ.

## วิธีแก้ไขเอกสารหลังจากระบุรูปแบบแล้ว?
เมื่อคุณรู้รูปแบบแล้ว การโหลดและแก้ไขเอกสารจะทำตามรูปแบบที่สอดคล้องกัน ขั้นแรกสร้างอินสแตนซ์ `Editor` ด้วยพาธของไฟล์ต้นฉบับ จากนั้นเรียก `Edit()` เพื่อรับ `EditableDocument` จากนั้นคุณสามารถอ่าน, แก้ไขและบันทึกเนื้อหาโดยใช้ `SaveOptions` ที่เหมาะสม

### การโหลดเอกสาร
`Editor` เป็นคลาสหลักที่ห่อหุ้มการดำเนินการแก้ไขทั้งหมดสำหรับไฟล์ที่ระบุ

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/document.docx"))
{
    // Further steps will be covered here.
}
```
```

**คำอธิบาย:**  
1. **เริ่มต้น Editor:** สร้างอินสแตนซ์ `Editor` โดยส่งพาธเต็มของไฟล์เป้าหมาย.  
2. **รูปแบบการปล่อยทรัพยากร:** คำสั่ง `using` รับประกันว่าทรัพยากรที่ไม่ได้จัดการจะถูกปล่อยอย่างทันท่วงที.

### การดึงเนื้อหา
`EditableDocument.GetContent()` คืนข้อความดิบของเอกสาร (หรือ HTML สำหรับเอดิเตอร์บนเว็บ) ซึ่งคุณสามารถแสดงหรือจัดการต่อได้

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    string content = editableDocument.GetContent();
    Console.WriteLine(content);
}
```
```

**คำอธิบาย:**  
1. **เมธอด Edit:** `Edit()` คืนอ็อบเจกต์ `EditableDocument`.  
2. **ดึงเนื้อหา:** `GetContent()` สกัดข้อความดิบของเอกสาร (หรือ HTML สำหรับเอดิเตอร์บนเว็บ).  
3. **แสดงเนื้อหา:** พิมพ์เนื้อหาออกคอนโซลเพื่อยืนยัน.

### การบันทึกการเปลี่ยนแปลง
`SaveOptions` บอกเอดิเตอร์ว่าจะเขียนเอกสารที่แก้ไขกลับไปยังที่เก็บอย่างไรและในรูปแบบใด

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    // Modify content here
    SaveOptions saveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docx);
    editor.Save(editableDocument, "path/to/save/document.docx", saveOptions);
}
```
```

**คำอธิบาย:**  
1. **เมธอด Edit:** ดึง `EditableDocument` อีกครั้งหลังจากทำการแก้ไข.  
2. **แก้ไขเนื้อหา:** ปรับเปลี่ยนสตริงตามที่ต้องการ (ไม่ได้แสดงในตัวอย่าง).  
3. **ตัวเลือกการบันทึก:** กำหนด `SaveOptions` ด้วยรูปแบบเอาต์พุตที่ต้องการ.  
4. **บันทึกเอกสาร:** บันทึกไฟล์ที่แก้ไขกลับสู่ดิสก์.

## วิธีทำงานกับประเภทเอกสารที่แตกต่างกัน?
GroupDocs.Editor ทำให้การจัดการ Word, Spreadsheet, และ Presentation อยู่ใน API เดียวกัน ทำให้คุณสลับบริบทได้โดยไม่ต้องเรียนรู้ชุดคลาสใหม่สำหรับแต่ละตระกูลเอกสาร

### การแก้ไขเอกสารสเปรดชีต
`SpreadsheetSaveOptions` กำหนดวิธีการเขียนสเปรดชีต รวมถึงรูปแบบและการตั้งค่าการบีบอัดแบบเลือกได้

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/spreadsheet.xlsx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // Modify content here
        SaveOptions saveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsx);
        editor.Save(editableDocument, "path/to/save/spreadsheet.xlsx", saveOptions);
    }
}
```
```

**คำอธิบาย:**  
1. **เริ่มต้น Editor:** ส่งพาธไฟล์สเปรดชีตให้กับคอนสตรัคเตอร์ `Editor`.  
2. **เมธอด Edit:** ดึง `EditableDocument`.  
3. **ดึงเนื้อหา:** พิมพ์การแสดงผล CSV ของสเปรดชีต (หรือ HTML).  
4. **แก้ไขเนื้อหา:** ทำการเปลี่ยนแปลงระดับเซลล์ตามต้องการ.  
5. **ตัวเลือกการบันทึก:** เลือก `SpreadsheetSaveOptions` ที่เหมาะสม.  
6. **บันทึกเอกสาร:** เขียนสเปรดชีตที่อัปเดตกลับสู่ที่เก็บ.

### การแก้ไขเอกสารการนำเสนอ
`PresentationSaveOptions` ควบคุมรูปแบบเอาต์พุตสำหรับสไลด์เด็ค ให้คุณคงหรือเปลี่ยนประเภทไฟล์ต้นฉบับได้

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/presentation.pptx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // Modify content here
        SaveOptions saveOptions = new PresentationSaveOptions(PresentationFormats.Pptx);
        editor.Save(editableDocument, "path/to/save/presentation.pptx", saveOptions);
    }
}
```
```

**คำอธิบาย:**  
1. **เริ่มต้น Editor:** โหลดไฟล์ PowerPoint ผ่าน `Editor`.  
2. **เมธอด Edit:** รับ `EditableDocument`.  
3. **ดึงเนื้อหา:** สกัด HTML ของสไลด์หรือข้อความธรรมดา.  
4. **แก้ไขเนื้อหา:** ปรับหัวข้อ, รายการหัวข้อย่อย หรือรูปภาพ.  
5. **ตัวเลือกการบันทึก:** ใช้ `PresentationSaveOptions` เพื่อกำหนดรูปแบบเอาต์พุต.  
6. **บันทึกเอกสาร:** บันทึกการนำเสนอที่แก้ไขแล้ว

## ปัญหาทั่วไปและวิธีแก้
- **ข้อผิดพลาด “Format not supported”:** ตรวจสอบว่าคุณใช้เวอร์ชันล่าสุดของ GroupDocs.Editor; เวอร์ชันใหม่มักเพิ่มการสนับสนุนรูปแบบ Office ที่อัปเดต.  
- **การใช้หน่วยความจำสูงสำหรับไฟล์ขนาดใหญ่:** เปิดโหมดสตรีมมิ่งโดยตั้งค่า `EditorSettings.EnableStreaming = true` ก่อนโหลดเอกสาร.  
- **ลิขสิทธิ์ไม่ทำงาน:** ตรวจสอบว่าไฟล์ลิขสิทธิ์ชั่วคราวอยู่ในโฟลเดอร์รากของแอปหรือโหลดผ่าน `License license = new License(); license.SetLicense("path/to/license.lic");`.

## คำถามที่พบบ่อย

**Q: ความแตกต่างระหว่าง `DocumentFormatInfo` กับ `SaveOptions` คืออะไร?**  
A: `DocumentFormatInfo` ให้ข้อมูลเมตาดาต้าเกี่ยวกับประเภทไฟล์ที่รองรับ, ในขณะที่ `SaveOptions` กำหนดวิธีการบันทึกเอกสารกลับสู่ดิสก์ (รูปแบบ, การบีบอัด ฯลฯ).

**Q: ฉันสามารถแสดงรายการรูปแบบสำหรับส่วนต่อขยายไฟล์ที่กำหนดเองได้หรือไม่?**  
A: ได้—ใช้ `DocumentFormatInfo.FromExtension("yourExt")`; หากส่วนต่อขยายไม่ถูกจดจำเมธอดจะคืนค่า `null`.

**Q: GroupDocs.Editor รองรับไฟล์ที่มีการป้องกันด้วยรหัสผ่านหรือไม่?**  
A: แน่นอน. ส่งรหัสผ่านไปยังคอนสตรัคเตอร์ `Editor` ผ่าน `EditorSettings` เพื่อเปิดไฟล์ที่เข้ารหัส.

**Q: GroupDocs.Editor รองรับรูปแบบไฟล์กี่ประเภท?**  
A: มากกว่า **30 รูปแบบการนำเข้าและส่งออก**, ครอบคลุม Word, Excel, PowerPoint, HTML และข้อความธรรมดา.

**Q: มีวิธีใดที่จะจำกัดรายการให้แสดงเฉพาะรูปแบบที่แก้ไขได้เท่านั้นหรือไม่?**  
A: ใช้ `GetEditableWordProcessingFormats()` (หรือเทียบเท่าสำหรับ Spreadsheet/Presentation) เพื่อดึงรูปแบบที่ให้ความสามารถการแก้ไขเต็มรูปแบบ.

## แหล่งข้อมูลเพิ่มเติม
- ดาวน์โหลดไลบรารีจาก [GroupDocs releases page](https://releases.groupdocs.com/editor/net/).  
- รับ [temporary license](https://purchase.groupdocs.com/temporary-license/) เพื่อเข้าถึงคุณสมบัติเต็มรูปแบบ.  
- ทดลองผลิตภัณฑ์ด้วย [free trial](https://releases.groupdocs.com/).  
- สำรวจตัวอย่างการใช้งานโดยละเอียดใน [GroupDocs.Editor documentation](https://tutorials.groupdocs.com/editor/net/).  
- ขอความช่วยเหลือจากชุมชนได้ที่ [support forum](https://forum.groupdocs.com/c/editor/20).

## สรุป
โดยทำตามคู่มือนี้คุณจะรู้วิธี **แสดงรายการรูปแบบเอกสารที่รองรับ**, **กำหนดรูปแบบไฟล์จากส่วนต่อขยาย**, และ **แก้ไขเอกสาร** ทั้งในประเภท Word, Spreadsheet, และ Presentation ด้วย GroupDocs.Editor สำหรับ .NET. นำโค้ดตัวอย่างเหล่านี้ไปใช้ในโปรเจกต์ของคุณเพื่อสร้างแอปพลิเคชันที่ตระหนักรูปแบบไฟล์, ลดข้อผิดพลาดขณะรัน, และมอบประสบการณ์ที่ดีให้กับผู้ใช้

---

**อัปเดตล่าสุด:** 2026-06-06  
**ทดสอบกับ:** GroupDocs.Editor 23.9 for .NET  
**ผู้เขียน:** GroupDocs

## บทแนะนำที่เกี่ยวข้อง

- [การทำความเข้าใจการโหลดเอกสารใน .NET ด้วย GroupDocs.Editor: คู่มือเชิงลึก](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)
- [การทำความเข้าใจการแก้ไขเอกสารใน .NET ด้วย GroupDocs.Editor: คู่มือเชิงลึก](/editor/net/document-editing/master-document-editing-dotnet-groupdocs-editor/)
- [แปลง Word เป็น HTML ด้วย GroupDocs.Editor .NET: คู่มือขั้นตอนต่อขั้นตอน](/editor/net/document-saving/convert-word-to-html-groupdocs-editor-dotnet/)