---
title: บันทึกทรัพยากร HTML ลงในโฟลเดอร์
linktitle: บันทึกทรัพยากร HTML ลงในโฟลเดอร์
second_title: GroupDocs.Editor .NET API
description: เรียนรู้วิธีแยกทรัพยากร HTML ออกจากเอกสารโดยใช้ Groupdocs.Editor สำหรับ .NET บทช่วยสอนที่ครอบคลุมนี้ให้คำแนะนำทีละขั้นตอนสำหรับนักพัฒนา
weight: 13
url: /th/net/document-editing/save-html-resources-to-folder/
---
## การแนะนำ
Groupdocs.Editor สำหรับ .NET เป็นเครื่องมืออันทรงพลังที่ช่วยให้นักพัฒนาสามารถจัดการและแปลงเอกสารภายในแอปพลิเคชัน .NET ของตนได้อย่างราบรื่น ไม่ว่าคุณจะต้องการแยกทรัพยากร HTML ออกจากเอกสารหรือดำเนินการแก้ไขขั้นสูง Groupdocs.Editor จะทำให้กระบวนการง่ายขึ้นด้วย API ที่ใช้งานง่ายและเอกสารประกอบที่ครอบคลุม
## ข้อกำหนดเบื้องต้น
ก่อนที่จะเข้าสู่บทช่วยสอน ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้:
1. ความรู้พื้นฐานเกี่ยวกับ C# และ .NET: ความคุ้นเคยกับภาษาการเขียนโปรแกรม C# และกรอบงาน .NET เป็นสิ่งสำคัญที่ต้องปฏิบัติตามพร้อมกับตัวอย่าง
2.  Groupdocs.Editor สำหรับ .NET Library: ดาวน์โหลดและติดตั้ง Groupdocs.Editor สำหรับ .NET Library จาก[เว็บไซต์](https://releases.groupdocs.com/editor/net/).
3. สภาพแวดล้อมการพัฒนา: ตั้งค่าสภาพแวดล้อมการพัฒนาที่คุณต้องการ เช่น Visual Studio หรือ IDE อื่น ๆ ที่เข้ากันได้

## นำเข้าเนมสเปซ
ในการเริ่มต้น ให้นำเข้าเนมสเปซที่จำเป็นในโปรเจ็กต์ C# ของคุณ:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```
##ตอนนี้ เราจะแบ่งขั้นตอนการบันทึกทรัพยากร HTML ลงในโฟลเดอร์โดยใช้ Groupdocs.Editor สำหรับ .NET ออกเป็นหลายขั้นตอน:
## ขั้นตอนที่ 1: เริ่มต้น Groupdocs.Editor
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
 ขั้นแรกให้เริ่มต้น`Editor`วัตถุโดยระบุเส้นทางไปยังเอกสารตัวอย่างของคุณ ในตัวอย่างนี้ เรากำลังใช้เอกสาร Word ดังนั้นเราจึงระบุ`WordProcessingLoadOptions` เป็นประเภทเอกสาร
## ขั้นตอนที่ 2: แก้ไขเอกสาร
```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
 ต่อไปให้สร้างไฟล์`EditableDocument` วัตถุโดยการเรียก`Edit` วิธีการของ`Editor` วัตถุ. ซึ่งช่วยให้คุณสามารถดำเนินการแก้ไขเอกสารได้
## ขั้นตอนที่ 3: แยกทรัพยากร
```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
แยกทรัพยากร เช่น รูปภาพ แบบอักษร และสไตล์ชีตออกจากเอกสารและจัดเก็บไว้ในรายการตามลำดับ
## ขั้นตอนที่ 4: ระบุโฟลเดอร์เอาท์พุต
```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
กำหนดโฟลเดอร์เอาท์พุตที่จะบันทึกทรัพยากรที่แตกออกมา คุณสามารถปรับแต่งเส้นทางโฟลเดอร์ได้ตามความต้องการของคุณ
## ขั้นตอนที่ 5: บันทึกทรัพยากร
```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
วนซ้ำทรัพยากรรูปภาพแต่ละรายการ บันทึกลงในโฟลเดอร์เอาต์พุต และแสดงข้อมูลที่เกี่ยวข้อง เช่น ชื่อไฟล์ ประเภท และขนาด
```csharp
		foreach (FontResourceBase oneFont in fonts)
		{
			Console.WriteLine("Saving {0} of {1} type",
				oneFont.FilenameWithExtension, oneFont.Type.FormalName);
			oneFont.Save(Path.Combine(outputFolder, oneFont.FilenameWithExtension));
		}
```
ในทำนองเดียวกัน บันทึกทรัพยากรแบบอักษรแต่ละรายการลงในโฟลเดอร์ผลลัพธ์
```csharp
		foreach (CssText oneStylesheet in stylesheets)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} encoding",
				oneStylesheet.FilenameWithExtension, oneStylesheet.Type.FormalName, oneStylesheet.Encoding);
			oneStylesheet.Save(Path.Combine(outputFolder, oneStylesheet.FilenameWithExtension));
		}
	}
}
```
สุดท้าย ให้บันทึกแต่ละสไตล์ชีตลงในโฟลเดอร์เอาท์พุตและดำเนินการแก้ไขให้เสร็จสิ้น

## บทสรุป
โดยสรุป Groupdocs.Editor สำหรับ .NET มอบโซลูชันที่สะดวกสำหรับการจัดการและจัดการเอกสารโดยทางโปรแกรมภายในแอปพลิเคชัน .NET เมื่อทำตามบทช่วยสอนนี้ คุณสามารถแยกทรัพยากร HTML ออกจากเอกสารได้อย่างง่ายดาย และปรับแต่งกระบวนการตามความต้องการเฉพาะของคุณ
## คำถามที่พบบ่อย
### Groupdocs.Editor เข้ากันได้กับรูปแบบเอกสารอื่นนอกเหนือจาก Word หรือไม่
ใช่ Groupdocs.Editor รองรับรูปแบบเอกสารที่หลากหลาย รวมถึง Excel, PowerPoint, PDF และอื่นๆ
### ฉันสามารถรวม Groupdocs.Editor เข้ากับเว็บแอปพลิเคชันของฉันได้หรือไม่
Groupdocs.Editor นำเสนอการบูรณาการอย่างราบรื่นกับเว็บแอปพลิเคชันที่พัฒนาบนเฟรมเวิร์ก .NET
### Groupdocs.Editor ให้การสนับสนุนบริการจัดเก็บข้อมูลบนคลาวด์หรือไม่
ใช่ Groupdocs.Editor รองรับการทำงานร่วมกับบริการจัดเก็บข้อมูลบนคลาวด์ยอดนิยม เช่น Google Drive, Dropbox และ Microsoft OneDrive
### Groupdocs.Editor มีรุ่นทดลองใช้ฟรีหรือไม่
ใช่ คุณสามารถทดลองใช้ Groupdocs.Editor ฟรีได้จากเว็บไซต์
### ฉันจะรับการสนับสนุนด้านเทคนิคสำหรับ Groupdocs.Editor ได้อย่างไร
หากต้องการความช่วยเหลือด้านเทคนิคและการสนับสนุนชุมชน คุณสามารถไปที่ฟอรัม Groupdocs.Editor