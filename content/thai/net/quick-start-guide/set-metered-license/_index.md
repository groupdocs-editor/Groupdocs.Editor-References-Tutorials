---
title: ตั้งค่าใบอนุญาตแบบมิเตอร์
linktitle: ตั้งค่าใบอนุญาตแบบมิเตอร์
second_title: GroupDocs.Editor .NET API
description: เรียนรู้วิธีบูรณาการและใช้ GroupDocs.Editor สำหรับ .NET พร้อมคำแนะนำที่ครอบคลุมของเรา ปลดล็อกคุณสมบัติการแก้ไขเอกสารอันทรงพลังภายในแอปพลิเคชัน .NET ของคุณ
type: docs
weight: 12
url: /th/net/quick-start-guide/set-metered-license/
---
## การแนะนำ
ยินดีต้อนรับสู่คำแนะนำทีละขั้นตอนเกี่ยวกับการใช้ GroupDocs.Editor สำหรับ .NET! ไม่ว่าคุณจะเป็นนักพัฒนาที่มีประสบการณ์หรือเพิ่งเริ่มต้น บทช่วยสอนนี้จะช่วยให้คุณใช้ประโยชน์จากศักยภาพสูงสุดของไลบรารีอันทรงพลังนี้ GroupDocs.Editor สำหรับ .NET ช่วยให้คุณสามารถแก้ไขเอกสารในรูปแบบต่างๆ ภายในแอปพลิเคชัน .NET ของคุณได้อย่างง่ายดาย มาเจาะลึกและสำรวจว่าคุณสามารถเริ่มต้นใช้งานเครื่องมือที่มีประสิทธิภาพนี้ได้อย่างไร
## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะพูดถึงรายละเอียดด้านเทคนิค ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นดังต่อไปนี้:
- ความรู้พื้นฐานเกี่ยวกับการเขียนโปรแกรม .NET: ความคุ้นเคยกับ C# และ .NET Framework
- ติดตั้ง Visual Studio แล้ว: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Visual Studio เวอร์ชันล่าสุดบนเครื่องของคุณ
-  GroupDocs.Editor สำหรับ .NET: ดาวน์โหลดไลบรารีจาก[หน้าดาวน์โหลด](https://releases.groupdocs.com/editor/net/).
-  ใบอนุญาตที่ถูกต้อง: รับใบอนุญาตชั่วคราวหรือเต็มรูปแบบจาก[หน้าการซื้อ GroupDocs](https://purchase.groupdocs.com/temporary-license/).
## นำเข้าเนมสเปซ
หากต้องการใช้ GroupDocs.Editor สำหรับ .NET คุณจะต้องนำเข้าเนมสเปซที่จำเป็นในโปรเจ็กต์ของคุณ ขั้นตอนนี้มีความสำคัญเนื่องจากเป็นการตั้งค่าโปรเจ็กต์ของคุณเพื่อใช้ฟังก์ชันการทำงานของไลบรารี
```csharp
using System;
using GroupDocs.Editor;
```
เราจะแบ่งแต่ละตัวอย่างออกเป็นหลายขั้นตอนเพื่อให้แน่ใจว่าคุณสามารถปฏิบัติตามได้อย่างง่ายดาย
## ขั้นตอนที่ 1: ติดตั้ง GroupDocs.Editor สำหรับ .NET
ก่อนอื่น คุณต้องติดตั้ง GroupDocs.Editor สำหรับ .NET ในโปรเจ็กต์ของคุณ คุณสามารถทำได้ผ่าน NuGet Package Manager ใน Visual Studio
### ติดตั้งผ่าน NuGet Package Manager
1. เปิดโครงการของคุณใน Visual Studio
2.  ไปที่`Tools` -`NuGet Package Manager` -`Manage NuGet Packages for Solution`.
3.  ค้นหา`GroupDocs.Editor`.
4.  คลิกที่`Install`.
นี่จะเป็นการเพิ่มข้อมูลอ้างอิงที่จำเป็นให้กับโครงการของคุณ
## ขั้นตอนที่ 2: ตั้งค่าใบอนุญาตแบบมิเตอร์
หากต้องการปลดล็อกฟีเจอร์ทั้งหมดของ GroupDocs.Editor คุณจะต้องตั้งค่าใบอนุญาตแบบคิดค่าบริการตามปริมาณข้อมูล ซึ่งจะทำให้คุณสามารถใช้ API ได้โดยไม่มีข้อจำกัดใดๆ
### การตั้งค่าใบอนุญาตแบบมิเตอร์
1.  รับกุญแจสาธารณะและกุญแจส่วนตัวของคุณจาก[หน้าการซื้อ GroupDocs](https://purchase.groupdocs.com/temporary-license/).
2. เพิ่มรหัสต่อไปนี้ในโครงการของคุณเพื่อตั้งค่าใบอนุญาตแบบคิดค่าบริการตามปริมาณข้อมูล:
```csharp
string publicKey = "*****";
string privateKey = "*****";
Metered metered = new Metered();
metered.SetMeteredKey(publicKey, privateKey);
Console.WriteLine("License set successfully.");
```
## ขั้นตอนที่ 3: โหลดและแก้ไขเอกสาร
ตอนนี้โปรเจ็กต์ของคุณได้รับการตั้งค่าและได้รับสิทธิ์การใช้งานแล้ว มาดูการโหลดและแก้ไขเอกสารกันดีกว่า
### กำลังโหลดเอกสาร
1. เพิ่มรหัสต่อไปนี้เพื่อโหลดเอกสาร:
```csharp
string filePath = "sample.docx";
Editor editor = new Editor(filePath);
Console.WriteLine("Document loaded successfully.");
```
### การแก้ไขเอกสาร
2. หากต้องการแก้ไขเอกสาร คุณต้องแปลงเป็นรูปแบบที่แก้ไขได้:
```csharp
EditableDocument editableDocument = editor.Edit();
string content = editableDocument.GetContent();
Console.WriteLine("Document converted to editable format.");
```
## ขั้นตอนที่ 4: บันทึกเอกสารที่แก้ไข
เมื่อคุณแก้ไขเอกสารแล้ว ขั้นตอนสุดท้ายคือบันทึกการเปลี่ยนแปลงของคุณ
### กำลังบันทึกเอกสาร
1. แปลงเนื้อหาที่แก้ไขกลับไปเป็นรูปแบบดั้งเดิม:
```csharp
string updatedContent = "<html><body>Updated content</body></html>";
editableDocument = EditableDocument.FromMarkup(updatedContent, new WordProcessingSaveOptions());
editor.Save(editableDocument, "updated_sample.docx");
Console.WriteLine("Document saved successfully.");
```
## บทสรุป
 ยินดีด้วย! คุณได้รวมและใช้ GroupDocs.Editor สำหรับ .NET ในแอปพลิเคชันของคุณสำเร็จแล้ว ตั้งแต่การติดตั้งไลบรารีไปจนถึงการตั้งค่าใบอนุญาตแบบคิดค่าบริการตามปริมาณข้อมูลและการแก้ไขเอกสาร คุณได้ครอบคลุมขั้นตอนที่จำเป็นทั้งหมดแล้ว เครื่องมืออันทรงพลังนี้สามารถปรับปรุงเวิร์กโฟลว์การแก้ไขเอกสารภายในแอปพลิเคชัน .NET ของคุณได้อย่างมาก สำหรับข้อมูลเพิ่มเติม โปรดดูที่[GroupDocs.Editor สำหรับเอกสาร .NET](https://reference.groupdocs.com/editor/net/).
## คำถามที่พบบ่อย
### ฉันจะขอรับใบอนุญาต GroupDocs.Editor ได้อย่างไร
 คุณสามารถขอรับใบอนุญาตได้จาก[หน้าการซื้อ GroupDocs](https://purchase.groupdocs.com/buy) - หากต้องการใบอนุญาตชั่วคราว โปรดไปที่[ที่นี่](https://purchase.groupdocs.com/temporary-license/).
### ฉันสามารถทดลองใช้ GroupDocs.Editor ได้ฟรีหรือไม่
 ใช่ คุณสามารถดาวน์โหลดรุ่นทดลองใช้ฟรีได้จาก[หน้าดาวน์โหลด](https://releases.groupdocs.com/) และขอใบอนุญาตชั่วคราว
### GroupDocs.Editor รองรับเอกสารรูปแบบใดบ้าง
 GroupDocs.Editor รองรับรูปแบบต่างๆ รวมถึง DOCX, PPTX, XLSX, TXT, HTML และอื่นๆ สำหรับรายการทั้งหมด โปรดดูที่[เอกสารประกอบ](https://reference.groupdocs.com/editor/net/).
### มีการสนับสนุนจากชุมชนสำหรับ GroupDocs.Editor หรือไม่
 ใช่ คุณสามารถรับการสนับสนุนจากชุมชนได้จาก[ฟอรัม GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).
### ฉันจะเริ่มต้นใช้งาน GroupDocs.Editor สำหรับ .NET ได้อย่างไร
 ปฏิบัติตามคำแนะนำทีละขั้นตอนของเราเพื่อตั้งค่าไลบรารี รับใบอนุญาต และเริ่มแก้ไขเอกสาร สำหรับคำแนะนำโดยละเอียด โปรดไปที่[เอกสารประกอบ](https://reference.groupdocs.com/editor/net/).