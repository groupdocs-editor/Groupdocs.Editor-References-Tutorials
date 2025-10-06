---
title: ทำงานกับเอกสารข้อความธรรมดา
linktitle: ทำงานกับเอกสารข้อความธรรมดา
second_title: GroupDocs.Editor .NET API
description: เรียนรู้วิธีแก้ไขเอกสารข้อความธรรมดาโดยใช้ GroupDocs.Editor สำหรับ .NET พร้อมคำแนะนำทีละขั้นตอนของเรา ลดความซับซ้อนของกระบวนการแก้ไขเอกสาร .NET ของคุณ
weight: 15
url: /th/net/document-processing/work-plain-text-documents/
type: docs
---
# ทำงานกับเอกสารข้อความธรรมดา

## การแนะนำ
คุณกำลังมองหาวิธีปรับปรุงกระบวนการแก้ไขเอกสารใน .NET หรือไม่? ไม่ต้องมองหาที่อื่นนอกจาก GroupDocs.Editor สำหรับ .NET! API อันทรงพลังนี้ช่วยให้คุณแก้ไขรูปแบบเอกสารที่หลากหลายได้อย่างง่ายดาย ในบทช่วยสอนนี้ เราจะแนะนำคุณตลอดกระบวนการทำงานกับเอกสารข้อความธรรมดาโดยใช้ GroupDocs.Editor สำหรับ .NET ในตอนท้าย คุณจะพร้อมที่จะจัดการการแก้ไขเอกสารข้อความอย่างมืออาชีพ พร้อมที่จะดำน้ำแล้วหรือยัง? มาเริ่มกันเลย!
## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะเริ่ม มีบางสิ่งที่คุณต้องเตรียม:
- สภาพแวดล้อมการพัฒนา .NET: ตรวจสอบให้แน่ใจว่าคุณได้ตั้งค่าสภาพแวดล้อมการพัฒนา .NET ที่ใช้งานได้ Visual Studio เป็นตัวเลือกยอดนิยม
-  GroupDocs.Editor สำหรับ .NET: ดาวน์โหลดและติดตั้ง[GroupDocs.Editor สำหรับ .NET](https://releases.groupdocs.com/editor/net/).
- ความรู้พื้นฐาน C#: ความคุ้นเคยกับภาษาการเขียนโปรแกรม C# จะช่วยให้คุณปฏิบัติตามตัวอย่างได้
- โปรแกรมแก้ไขข้อความ: โปรแกรมแก้ไขข้อความใดก็ได้ แม้ว่าจะแนะนำให้ใช้ Visual Studio Code เนื่องจากคุณสมบัติและความสะดวกในการใช้งาน
## นำเข้าเนมสเปซ
หากต้องการเริ่มใช้ GroupDocs.Editor สำหรับ .NET คุณจะต้องนำเข้าเนมสเปซที่จำเป็นลงในโปรเจ็กต์ของคุณ สิ่งนี้ทำให้มั่นใจได้ว่าคลาสและวิธีการที่จำเป็นทั้งหมดจะพร้อมใช้งาน
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```
เรามาแบ่งกระบวนการออกเป็นขั้นตอนที่สามารถจัดการได้ ทำตามคำแนะนำในขณะที่เราแนะนำคุณตลอดแต่ละขั้นตอนของการแก้ไขเอกสารข้อความธรรมดาโดยใช้ GroupDocs.Editor สำหรับ .NET
## ขั้นตอนที่ 1: รับเส้นทางไปยังไฟล์อินพุต TXT
ขั้นแรก คุณต้องระบุเส้นทางไปยังไฟล์ TXT อินพุต นี่อาจเป็นเส้นทางไปยังไฟล์ในเครื่องหรือสตรีมที่มีเนื้อหาไฟล์
```csharp
string inputFilePath = "YourSampleDocument.txt";
```
## ขั้นตอนที่ 2: สร้างอินสแตนซ์ตัวแก้ไข
 ถัดไป สร้างอินสแตนซ์ของ`Editor` ระดับ. ชั้นเรียนนี้มีหน้าที่โหลดและแก้ไขเอกสาร ไม่จำเป็นต้องมีตัวเลือกการโหลดในขั้นตอนนี้
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## ขั้นตอนที่ 3: สร้างตัวเลือกการแก้ไข TXT
ตอนนี้ ให้สร้างตัวเลือกการแก้ไข TXT ตัวเลือกเหล่านี้ช่วยให้คุณสามารถระบุวิธีการประมวลผลเนื้อหาข้อความในระหว่างการแก้ไข
```csharp
    TextEditOptions editOptions = new TextEditOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        RecognizeLists = true,
        LeadingSpaces = TextLeadingSpacesOptions.ConvertToIndent,
        TrailingSpaces = TextTrailingSpacesOptions.Trim
    };
```
## ขั้นตอนที่ 4: สร้างอินสแตนซ์เอกสารที่แก้ไขได้
 ด้วยการตั้งค่าตัวเลือกการแก้ไข ให้สร้าง`EditableDocument` ตัวอย่าง. นี่แสดงถึงเอกสารในรูปแบบที่แก้ไขได้
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## ขั้นตอนที่ 5: แก้ไขเนื้อหาเอกสาร
ดึงเนื้อหาข้อความต้นฉบับและทำการแก้ไขตามที่คุณต้องการ สำหรับตัวอย่างนี้ เราจะแทนที่คำว่า "ข้อความ" ด้วย "ข้อความที่แก้ไขแล้ว"
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("text", "EDITED text");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## ขั้นตอนที่ 6: สร้างเอกสารที่แก้ไขได้พร้อมเนื้อหาที่อัปเดต
 หลังจากทำการแก้ไขที่จำเป็นแล้ว ให้สร้างใหม่`EditableDocument` ด้วยเนื้อหาที่อัปเดตและแหล่งข้อมูลดั้งเดิม
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## ขั้นตอนที่ 7: สร้างตัวเลือกการบันทึกการประมวลผล Word
เตรียมตัวเลือกการบันทึกสำหรับรูปแบบ WordProcessing ตัวอย่างนี้ใช้รูปแบบ DOCM และระบุสถานที่
```csharp
    WordProcessingSaveOptions wordSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm)
    {
        Locale = System.Globalization.CultureInfo.GetCultureInfo("en-GB")
    };
```
## ขั้นตอนที่ 8: สร้างตัวเลือกการบันทึก TXT
ในทำนองเดียวกัน ให้สร้างตัวเลือกการบันทึกสำหรับรูปแบบ TXT ตรวจสอบให้แน่ใจว่าตั้งค่าการเข้ารหัสเป็น UTF-8 และคงเค้าโครงตารางไว้
```csharp
    TextSaveOptions txtSaveOptions = new TextSaveOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        PreserveTableLayout = true
    };
```
## ขั้นตอนที่ 9: เตรียมเส้นทางเอาต์พุต
เตรียมเส้นทางสำหรับบันทึกไฟล์ DOCX และ TXT ที่เป็นผลลัพธ์ ใช้เส้นทางไฟล์อินพุตเพื่อกำหนดไดเร็กทอรีเอาต์พุตและชื่อไฟล์
```csharp
    string outputWordPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".docm");
    string outputTxtPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".txt");
```
## ขั้นตอนที่ 10: บันทึกเอกสารที่แก้ไข
สุดท้าย ให้บันทึกเอกสารที่แก้ไขทั้งในรูปแบบ DOCX และ TXT โดยใช้ตัวเลือกการบันทึกที่ระบุ
```csharp
    editor.Save(afterEdit, outputWordPath, wordSaveOptions);
    editor.Save(afterEdit, outputTxtPath, txtSaveOptions);
}
System.Console.WriteLine("Document editing process completed successfully!");
```
## บทสรุป
 ยินดีด้วย! คุณแก้ไขเอกสารข้อความธรรมดาได้สำเร็จโดยใช้ GroupDocs.Editor สำหรับ .NET เครื่องมืออันทรงพลังนี้ช่วยลดความยุ่งยากในการแก้ไขเอกสาร ทำให้ง่ายต่อการรวมเข้ากับแอปพลิเคชัน .NET ของคุณ ไม่ว่าคุณจะจัดการไฟล์ข้อความธรรมดาหรือรูปแบบเอกสารที่ซับซ้อน GroupDocs.Editor ก็ช่วยคุณได้ สำรวจคุณสมบัติและความสามารถเพิ่มเติมโดยไปที่[เอกสาร GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/).
## คำถามที่พบบ่อย
### GroupDocs.Editor for .NET รองรับรูปแบบไฟล์ใดบ้าง
 GroupDocs.Editor สำหรับ .NET รองรับรูปแบบไฟล์ที่หลากหลาย รวมถึง DOCX, TXT, HTML และอื่นๆ ตรวจสอบ[เอกสารประกอบ](https://tutorials.groupdocs.com/editor/net/) สำหรับรายการทั้งหมด
### ฉันจะทดลองใช้ GroupDocs.Editor สำหรับ .NET ได้ฟรีได้อย่างไร
 คุณสามารถดาวน์โหลด GroupDocs.Editor สำหรับ .NET รุ่นทดลองใช้ฟรีได้จาก[หน้าเผยแพร่](https://releases.groupdocs.com/).
### ฉันสามารถซื้อใบอนุญาตชั่วคราวสำหรับ GroupDocs.Editor สำหรับ .NET ได้หรือไม่
ใช่ คุณสามารถขอรับใบอนุญาตชั่วคราวได้จาก[หน้าการซื้อ GroupDocs](https://purchase.groupdocs.com/temporary-license/).
### ฉันจะรับการสนับสนุนสำหรับ GroupDocs.Editor สำหรับ .NET ได้ที่ไหน
 การสนับสนุนสามารถใช้ได้ผ่านทาง[ฟอรัมสนับสนุน GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).
### มีเอกสารโดยละเอียดสำหรับ GroupDocs.Editor สำหรับ .NET หรือไม่
 ใช่ เอกสารรายละเอียดมีอยู่ที่[หน้าเอกสาร GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/).