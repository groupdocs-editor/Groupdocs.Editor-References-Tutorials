---
title: แก้ไขเอกสาร
linktitle: แก้ไขเอกสาร
second_title: GroupDocs.Editor .NET API
description: เรียนรู้การแก้ไขเอกสารอย่างง่ายดายด้วย GroupDocs.Editor สำหรับ .NET คำแนะนำทีละขั้นตอนสำหรับไฟล์การประมวลผลคำและสเปรดชีต
type: docs
weight: 11
url: /th/net/document-editing/edit-document/
---
## การแนะนำ
เคยพบว่าตัวเองยุ่งวุ่นวายกับความซับซ้อนในการแก้ไขเอกสารภายในแอปพลิเคชัน .NET ของคุณหรือไม่? อย่ากลัว! ด้วย GroupDocs.Editor สำหรับ .NET คุณจะมีพันธมิตรที่ทรงพลังในการทำให้งานนี้ง่ายขึ้น คู่มือที่ครอบคลุมนี้จะแนะนำวิธีใช้ประโยชน์จากเครื่องมือที่มีประสิทธิภาพนี้เพื่อแก้ไขเอกสารได้อย่างง่ายดาย ไม่ว่าคุณจะจัดการกับเอกสารการประมวลผลคำหรือสเปรดชีต เมื่อสิ้นสุดบทช่วยสอนนี้ คุณจะใช้งาน GroupDocs.Editor อย่างมืออาชีพได้
## ข้อกำหนดเบื้องต้น
ก่อนที่จะเข้าสู่บทช่วยสอน ตรวจสอบให้แน่ใจว่าคุณมีสิ่งต่อไปนี้:
- Visual Studio: ติดตั้งแล้วและพร้อมใช้งาน
- .NET Framework: เวอร์ชันที่เข้ากันได้ที่ติดตั้งบนระบบของคุณ
-  GroupDocs.Editor สำหรับ .NET: คุณทำได้[ดาวน์โหลดเวอร์ชันล่าสุด](https://releases.groupdocs.com/editor/net/) และได้รับ[ใบอนุญาตชั่วคราว](https://purchase.groupdocs.com/temporary-license/) หากมีความจำเป็น.
- ความรู้พื้นฐานของ C#: คู่มือนี้ถือว่าคุณมีความเข้าใจพื้นฐานเกี่ยวกับการพัฒนา C# และ .NET
## นำเข้าเนมสเปซ
ในการเริ่มต้น คุณต้องนำเข้าเนมสเปซที่จำเป็นลงในโปรเจ็กต์ของคุณ เพิ่มบรรทัดต่อไปนี้ที่ด้านบนของไฟล์ C# ของคุณ:
```csharp
using System.Collections.Generic;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.Options;
```
ตอนนี้คุณพร้อมแล้ว เรามาแบ่งขั้นตอนการแก้ไขเอกสารออกเป็นขั้นตอนที่สามารถจัดการได้
## ขั้นตอนที่ 1: โหลดเอกสารการประมวลผลคำ
ขั้นแรก มาโหลดเอกสารการประมวลผลคำกัน นี่คือที่ที่คุณชี้อินสแตนซ์ Editor ไปยังตำแหน่งของเอกสารของคุณและระบุตัวเลือกการโหลดหากจำเป็น
### 1.1 เริ่มต้นโปรแกรมแก้ไขด้วยตัวเลือกเริ่มต้น
```csharp
string inputFilePath = "Your Sample Document"; // เส้นทางไปยังเอกสารของคุณ
Editor editor1 = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
```
ข้อมูลโค้ดนี้จะเตรียมใช้งานอินสแตนซ์ Editor โดยใช้ตัวเลือกการโหลดเริ่มต้นสำหรับเอกสารการประมวลผลคำ
## ขั้นตอนที่ 2: แก้ไขเอกสาร
ตอนนี้เราสามารถดำเนินการแก้ไขเอกสารที่โหลดต่อไปได้ GroupDocs.Editor ช่วยให้คุณปรับแต่งตัวเลือกการแก้ไขให้เหมาะกับความต้องการของคุณได้
### 2.1 แก้ไขด้วยตัวเลือกเริ่มต้น
```csharp
EditableDocument defaultWordProcessingDoc = editor1.Edit();
```
การแก้ไขเอกสารด้วยตัวเลือกเริ่มต้นนั้นตรงไปตรงมาและต้องมีการกำหนดค่าเพียงเล็กน้อย
### 2.2 แก้ไขด้วยตัวเลือกแบบกำหนดเอง
เรามาเจาะลึกการกำหนดค่าขั้นสูงเพิ่มเติมโดยการระบุตัวเลือกการแก้ไขแบบกำหนดเอง
```csharp
WordProcessingEditOptions wordProcessingEditOptions1 = new WordProcessingEditOptions();
wordProcessingEditOptions1.EnablePagination = false;
wordProcessingEditOptions1.EnableLanguageInformation = true;
wordProcessingEditOptions1.FontExtraction = FontExtractionOptions.ExtractAllEmbedded;
EditableDocument version1WordProcessingDoc = editor1.Edit(wordProcessingEditOptions1);
```
ในตัวอย่างนี้ เราได้ปิดการใช้งานการแบ่งหน้า เปิดใช้งานข้อมูลภาษา และตั้งค่าการแยกแบบอักษรเพื่อแยกแบบอักษรที่ฝังทั้งหมด
### 2.3 ตัวอย่างการกำหนดค่าอื่น
คุณยังสามารถแก้ไขเอกสารด้วยชุดตัวเลือกอื่นได้:
```csharp
WordProcessingEditOptions wordProcessingEditOptions2 = new WordProcessingEditOptions(true);
wordProcessingEditOptions2.FontExtraction = FontExtractionOptions.ExtractAll;
EditableDocument version2WordProcessingDoc = editor1.Edit(wordProcessingEditOptions2);
```
ที่นี่ เราเปิดใช้งานการแบ่งหน้าและตั้งค่าการแยกแบบอักษรเพื่อแยกแบบอักษรทั้งหมด
## ขั้นตอนที่ 3: โหลดและแก้ไขสเปรดชีต
การแก้ไขสเปรดชีตทำได้ง่ายไม่แพ้กันด้วย GroupDocs.Editor
### 3.1 โหลดสเปรดชีต
```csharp
Editor editor2 = new Editor("Your Sample Document", delegate { return new SpreadsheetLoadOptions(); });
```
ซึ่งจะเริ่มต้นอินสแตนซ์ Editor สำหรับเอกสารสเปรดชีต
### 3.2 แก้ไขแท็บแรก
```csharp
SpreadsheetEditOptions sheetTab1EditOptions = new SpreadsheetEditOptions();
sheetTab1EditOptions.WorksheetIndex = 0; // ดัชนีเป็นแบบ 0 ดังนั้นนี่คือแท็บแรก
EditableDocument firstTab = editor2.Edit(sheetTab1EditOptions);
```
คุณสามารถแก้ไขแท็บแรกของสเปรดชีตได้โดยใช้ตัวเลือกที่ระบุ
### 3.3 แก้ไขแท็บที่สอง
```csharp
SpreadsheetEditOptions sheetTab2EditOptions = new SpreadsheetEditOptions();
sheetTab2EditOptions.WorksheetIndex = 1; // ดัชนีเป็นแบบ 0 ดังนั้นนี่คือแท็บที่สอง
EditableDocument secondTab = editor2.Edit(sheetTab2EditOptions);
```
ในทำนองเดียวกัน ข้อมูลโค้ดนี้จะแก้ไขแท็บที่สองของสเปรดชีต
## ขั้นตอนที่ 4: แยกเนื้อหา
เมื่อคุณแก้ไขเอกสารแล้ว คุณอาจต้องแยกเนื้อหาออกจากนั้น GroupDocs.Editor มีวิธีการต่างๆ มากมายสำหรับเรื่องนี้
### 4.1 รับเนื้อหา HTML
```csharp
string bodyContent = firstTab.GetBodyContent(); // มาร์กอัป HTML จากภายในองค์ประกอบ HTML->BODY
string allContent = firstTab.GetContent(); // มาร์กอัป HTML แบบเต็มของเอกสารทั้งหมด รวมถึงส่วนหัว HTML->HEAD และเนื้อหา
```
รหัสนี้จะแยกเนื้อหา HTML ของเอกสารที่แก้ไข
### 4.2 แยกทรัพยากร
```csharp
List<IImageResource> onlyImages = firstTab.Images;
List<IHtmlResource> allResourcesTogether = firstTab.AllResources;
```
ที่นี่ คุณสามารถแยกรูปภาพและทรัพยากร HTML อื่นๆ ทั้งหมดออกจากเอกสารได้
## ขั้นตอนที่ 5: ทำความสะอาด
อย่าลืมกำจัดอินสแตนซ์ทั้งหมดเพื่อเพิ่มทรัพยากร
```csharp
defaultWordProcessingDoc.Dispose();
version1WordProcessingDoc.Dispose();
version2WordProcessingDoc.Dispose();
firstTab.Dispose();
secondTab.Dispose();
editor1.Dispose();
editor2.Dispose();
```
การกำจัดอย่างเหมาะสมช่วยให้แน่ใจว่าไม่มีหน่วยความจำรั่วไหลหรือปัญหาด้านประสิทธิภาพในแอปพลิเคชันของคุณ
## บทสรุป
 ยินดีด้วย! ขณะนี้คุณมีความเข้าใจที่ชัดเจนเกี่ยวกับวิธีการใช้ GroupDocs.Editor สำหรับ .NET เพื่อโหลด แก้ไข และแยกเนื้อหาจากเอกสารการประมวลผลคำและสเปรดชีต เครื่องมืออันทรงพลังนี้ช่วยลดความยุ่งยากในการแก้ไขเอกสารและผสานรวมกับแอปพลิเคชัน .NET ของคุณได้อย่างราบรื่น สำหรับรายละเอียดเพิ่มเติม คุณสามารถสำรวจได้ที่[เอกสารประกอบ](https://reference.groupdocs.com/editor/net/), [ดาวน์โหลดเวอร์ชันล่าสุด](https://releases.groupdocs.com/editor/net/) หรือได้รับ[ใบอนุญาตชั่วคราว](https://purchase.groupdocs.com/temporary-license/).
## คำถามที่พบบ่อย
### ฉันสามารถแก้ไขเอกสาร PDF ด้วย GroupDocs.Editor สำหรับ .NET ได้หรือไม่
ปัจจุบัน GroupDocs.Editor สำหรับ .NET รองรับรูปแบบการประมวลผลคำ สเปรดชีต และการนำเสนอเป็นหลัก
### ฉันจะจัดการเอกสารขนาดใหญ่อย่างมีประสิทธิภาพได้อย่างไร
ใช้ตัวเลือกการแก้ไขเพื่อโหลดและประมวลผลเฉพาะส่วนที่จำเป็นของเอกสาร และให้แน่ใจว่าคุณกำจัดอินสแตนซ์อย่างเหมาะสมเพื่อจัดการหน่วยความจำ
### มีการจำกัดขนาดเอกสารที่ฉันสามารถแก้ไขได้หรือไม่
ไม่มีการจำกัดขนาดที่เข้มงวด แต่ประสิทธิภาพขึ้นอยู่กับความสามารถของระบบของคุณ
### ฉันสามารถปรับแต่งเอาต์พุต HTML เพิ่มเติมได้หรือไม่
ใช่ GroupDocs.Editor ช่วยให้ปรับแต่งเอาต์พุต HTML ได้อย่างกว้างขวางผ่านตัวเลือกและการตั้งค่าต่างๆ
### ฉันจะรับการสนับสนุนได้ที่ไหนหากฉันประสบปัญหา
 ท่านสามารถเยี่ยมชมได้ที่[ฟอรัมสนับสนุน GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20) เพื่อขอความช่วยเหลือและความช่วยเหลือ