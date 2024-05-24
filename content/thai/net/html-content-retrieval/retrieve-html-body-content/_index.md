---
title: ดึงเนื้อหาเนื้อหา HTML
linktitle: ดึงเนื้อหาเนื้อหา HTML
second_title: GroupDocs.Editor .NET API
description: ดึงเนื้อหาเนื้อหา HTML โดยใช้ GroupDocs.Editor สำหรับ .NET พร้อมด้วยคำแนะนำทีละขั้นตอนของเรา ปรับปรุงแอปพลิเคชัน .NET ของคุณได้อย่างง่ายดาย
type: docs
weight: 10
url: /th/net/html-content-retrieval/retrieve-html-body-content/
---
## การแนะนำ
คุณพร้อมที่จะปฏิวัติวิธีจัดการการแก้ไขเอกสารในแอปพลิเคชัน .NET ของคุณแล้วหรือยัง? ไม่ต้องมองหาที่อื่นนอกจาก GroupDocs.Editor สำหรับ .NET! เครื่องมืออันทรงพลังนี้ช่วยให้สามารถแก้ไขรูปแบบเอกสารที่หลากหลายได้โดยตรงภายในแอปพลิเคชันของคุณได้อย่างราบรื่น ไม่ว่าคุณจะทำงานกับ Word, PDF หรือ HTML, GroupDocs.Editor ทำให้ง่ายต่อการแก้ไขและจัดการเอกสารโดยไม่ต้องใช้เครื่องมือภายนอก
## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะเริ่ม มีข้อกำหนดเบื้องต้นบางประการที่คุณต้องมี:
- ความรู้พื้นฐานเกี่ยวกับการเขียนโปรแกรม .NET: ความคุ้นเคยกับ C# และกรอบงาน .NET จะช่วยให้คุณทำตามตัวอย่างได้
-  GroupDocs.Editor สำหรับ .NET: คุณสามารถดาวน์โหลดได้จากไฟล์[หน้าดาวน์โหลด GroupDocs.Editor](https://releases.groupdocs.com/editor/net/).
-  ใบอนุญาตที่ถูกต้อง: คุณสามารถซื้อใบอนุญาตได้จาก[หน้าการซื้อ GroupDocs](https://purchase.groupdocs.com/buy) หรือขอ[ใบอนุญาตชั่วคราว](https://purchase.groupdocs.com/temporary-license/).
- สภาพแวดล้อมการพัฒนาแบบรวม (IDE): แนะนำให้ใช้ Visual Studio เพื่อประสบการณ์การพัฒนาที่ดีที่สุด
## นำเข้าเนมสเปซ
หากต้องการเริ่มต้นใช้งาน GroupDocs.Editor สำหรับ .NET คุณจะต้องนำเข้าเนมสเปซที่จำเป็น ซึ่งจะช่วยให้คุณสามารถเข้าถึงคลาสและวิธีการที่จำเป็นสำหรับการแก้ไขเอกสาร
```csharp
using System;
using GroupDocs.Editor.Options;
```
## ขั้นตอนที่ 1: เริ่มต้นตัวแก้ไข
ขั้นตอนแรกในกระบวนการของเราคือการเริ่มต้น`Editor` ชั้นเรียนด้วยเอกสารของคุณ คลาสนี้เป็นจุดเริ่มต้นสำหรับการดำเนินการแก้ไขทั้งหมด

คุณต้องโหลดเอกสารที่คุณต้องการแก้ไข สำหรับตัวอย่างนี้ เราจะใช้เอกสาร Word ตัวอย่าง
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
    // ดำเนินการต่อไปยังขั้นตอนถัดไป
}
```
## ขั้นตอนที่ 2: แก้ไขเอกสาร
 ต่อไปเราจะใช้`Edit` วิธีการของ`Editor` คลาสเพื่อสร้างเอกสารเวอร์ชันที่แก้ไขได้

 เราจะระบุตัวเลือกการแก้ไขสำหรับเอกสาร ในกรณีนี้เราจะใช้`WordProcessingEditOptions`.
```csharp
using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
{
    // ดำเนินการต่อไปยังขั้นตอนถัดไป
}
```
## ขั้นตอนที่ 3: ดึงเนื้อหาเนื้อหา HTML
ตอนนี้เราจะดึงเนื้อหาเนื้อหาของเอกสารในรูปแบบ HTML นี่คือจุดที่ความมหัศจรรย์เกิดขึ้น!

 ใช้`GetBodyContent` วิธีการเราสามารถแยกเนื้อหาภายในของ HTML ได้`<body>` องค์ประกอบ.
```csharp
string bodyContent = document.GetBodyContent();
Console.WriteLine("Inner content of the HTML->BODY element: {0}", bodyContent);
```

## บทสรุป
ยินดีด้วย! คุณได้เรียนรู้วิธีดึงเนื้อหาเนื้อหา HTML จากเอกสารโดยใช้ GroupDocs.Editor สำหรับ .NET เรียบร้อยแล้ว ไลบรารีอันทรงพลังนี้ทำให้การแก้ไขเอกสารภายในแอปพลิเคชัน .NET ของคุณง่ายขึ้น ทำให้เป็นเครื่องมืออันมีค่าสำหรับนักพัฒนา
## คำถามที่พบบ่อย
### GroupDocs.Editor รองรับไฟล์รูปแบบใดบ้าง
GroupDocs.Editor รองรับรูปแบบไฟล์ที่หลากหลาย รวมถึงเอกสาร Word, PDF, สเปรดชีต Excel, งานนำเสนอ PowerPoint และไฟล์ HTML
### ฉันจะรับใบอนุญาตชั่วคราวสำหรับ GroupDocs.Editor ได้อย่างไร
 คุณสามารถขอใบอนุญาตชั่วคราวได้จาก[หน้าสิทธิ์การใช้งานชั่วคราวของ GroupDocs](https://purchase.groupdocs.com/temporary-license/).
### GroupDocs.Editor มีรุ่นทดลองใช้ฟรีหรือไม่
 ใช่ คุณสามารถดาวน์โหลดรุ่นทดลองใช้ฟรีได้จาก[หน้าดาวน์โหลด GroupDocs.Editor](https://releases.groupdocs.com/).
### ฉันสามารถใช้ GroupDocs.Editor กับ .NET Core ได้หรือไม่
ใช่ GroupDocs.Editor เข้ากันได้กับ .NET Core ซึ่งให้ความยืดหยุ่นสำหรับการพัฒนาแอปพลิเคชันสมัยใหม่
### ฉันจะหาตัวอย่างและเอกสารประกอบเพิ่มเติมสำหรับ GroupDocs.Editor ได้จากที่ไหน
 คุณสามารถดูตัวอย่างเพิ่มเติมและเอกสารประกอบโดยละเอียดได้ที่[หน้าเอกสาร GroupDocs.Editor](https://reference.groupdocs.com/editor/net/).