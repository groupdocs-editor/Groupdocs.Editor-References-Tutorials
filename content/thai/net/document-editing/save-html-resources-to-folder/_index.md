---
date: 2026-05-12
description: เรียนรู้วิธีดึงฟอนต์และทรัพยากร HTML อื่น ๆ จากเอกสารโดยใช้ GroupDocs.Editor
  for .NET คู่มือแบบขั้นตอนสำหรับนักพัฒนา .NET
keywords:
- how to extract fonts
- GroupDocs.Editor .NET
- extract HTML resources
linktitle: บันทึกทรัพยากร HTML ลงในโฟลเดอร์
schemas:
- author: GroupDocs
  dateModified: '2026-05-12'
  description: Learn how to extract fonts and other HTML resources from documents
    using GroupDocs.Editor for .NET. Step‑by‑step guide for .NET developers.
  headline: How to Extract Fonts and Save HTML Resources to Folder
  type: TechArticle
- description: Learn how to extract fonts and other HTML resources from documents
    using GroupDocs.Editor for .NET. Step‑by‑step guide for .NET developers.
  name: How to Extract Fonts and Save HTML Resources to Folder
  steps:
  - name: '**Basic Knowledge of C# and .NET** – Familiarity with C# programming language
      and .NET framework is essential to follow along with the examples.'
    text: '**Basic Knowledge of C# and .NET** – Familiarity with C# programming language
      and .NET framework is essential to follow along with the examples.'
  - name: '**GroupDocs.Editor for .NET Library** – Download and install GroupDocs.Editor
      for .NET library from the [website](https://releases.groupdocs.com/editor/net/).'
    text: '**GroupDocs.Editor for .NET Library** – Download and install GroupDocs.Editor
      for .NET library from the [website](https://releases.groupdocs.com/editor/net/).'
  - name: '**Development Environment** – Set up your preferred development environment
      such as Visual Studio or any other compatible IDE.'
    text: '**Development Environment** – Set up your preferred development environment
      such as Visual Studio or any other compatible IDE.'
  type: HowTo
- questions:
  - answer: Yes, it supports Excel, PowerPoint, PDF, HTML, and over 50 additional
      formats for both editing and resource extraction.
    question: Is GroupDocs.Editor compatible with other document formats besides Word?
  - answer: Absolutely. The API works seamlessly with ASP.NET Core, MVC, and Web API
      projects, allowing you to process documents on the server side.
    question: Can I integrate GroupDocs.Editor into a web application?
  - answer: Yes, it includes built‑in connectors for Google Drive, Dropbox, OneDrive,
      and Amazon S3, enabling direct loading and saving of documents in the cloud.
    question: Does GroupDocs.Editor provide cloud storage integration?
  - answer: A fully functional 30‑day trial can be downloaded from the GroupDocs website
      without any credit‑card requirement.
    question: Is there a free trial available for GroupDocs.Editor?
  - answer: You can reach the GroupDocs support team via the official forum, submit
      a ticket through the customer portal, or consult the detailed API documentation.
    question: How can I get technical support for extraction issues?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: วิธีดึงฟอนต์และบันทึกทรัพยากร HTML ลงในโฟลเดอร์
type: docs
url: /th/net/document-editing/save-html-resources-to-folder/
weight: 13
---

# วิธีการสกัดฟอนต์และบันทึกทรัพยากร HTML ไปยังโฟลเดอร์

## บทนำ
GroupDocs.Editor for .NET ให้คุณ **how to extract fonts** และทรัพยากรอื่น ๆ จากเอกสารขณะแปลงเป็น HTML เพียงไม่กี่บรรทัดของ C# คุณสามารถดึงรูปภาพ, Stylesheets, และไฟล์ฟอนต์ออกมา แล้วเก็บไว้ในโฟลเดอร์ที่คุณเลือก บทเรียนนี้จะพาคุณผ่านขั้นตอนทั้งหมด ตั้งแต่การเริ่มต้น Editor จนถึงการบันทึกแต่ละทรัพยากรลงดิสก์

## คำตอบสั้น
- **What does “how to extract fonts” mean?** เป็นกระบวนการดึงไฟล์ฟอนต์ที่ฝังอยู่จากเอกสารต้นฉบับระหว่างการแปลงเป็น HTML.  
- **Which library handles this?** GroupDocs.Editor for .NET มี API เฉพาะสำหรับการสกัดฟอนต์, รูปภาพ, และ Stylesheets.  
- **Do I need a license?** มีการทดลองใช้ฟรี; จำเป็นต้องมีลิขสิทธิ์เชิงพาณิชย์สำหรับการใช้งานในสภาพแวดล้อมจริง.  
- **What .NET versions are supported?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.  
- **Can I target a custom folder?** ได้, คุณสามารถระบุเส้นทางที่เขียนได้เมื่อบันทึกทรัพยากรที่สกัดออกมา.

## “how to extract fonts” คืออะไร
**How to extract fonts** หมายถึงการดึงไฟล์ฟอนต์ต้นฉบับที่ฝังอยู่ในเอกสารต้นทาง (เช่น DOCX, PPTX) เพื่อให้สามารถอ้างอิงได้โดย HTML ที่สร้างขึ้น ซึ่งทำให้ข้อความแสดงผลตรงตามที่ต้องการในเบราว์เซอร์โดยไม่ต้องพึ่งพาฟอนต์ของระบบ.

## ทำไมต้องใช้ GroupDocs.Editor สำหรับการสกัดทรัพยากร HTML
GroupDocs.Editor รองรับ **50+ input and output formats**—รวมถึง DOCX, PPTX, PDF, และ HTML—และสามารถประมวลผลเอกสารที่มี **up to 300 pages** ได้โดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ API ของมันสกัดฟอนต์, รูปภาพ, และ CSS ในขั้นตอนเดียว ลดเวลาในการพัฒนาถึง **70 %** เมื่อเทียบกับการทำการแยกวิเคราะห์ด้วยตนเอง.

## ข้อกำหนดเบื้องต้น
ก่อนเริ่มทำตามบทเรียน โปรดตรวจสอบว่าคุณมีข้อกำหนดต่อไปนี้:
1. **Basic Knowledge of C# and .NET** – ความคุ้นเคยกับภาษาโปรแกรม C# และ .NET framework เป็นสิ่งจำเป็นเพื่อทำตามตัวอย่างได้
2. **GroupDocs.Editor for .NET Library** – ดาวน์โหลดและติดตั้งไลบรารี GroupDocs.Editor for .NET จาก [website](https://releases.groupdocs.com/editor/net/).
3. **Development Environment** – ตั้งค่าสภาพแวดล้อมการพัฒนาที่คุณต้องการ เช่น Visual Studio หรือ IDE ที่เข้ากันได้อื่น ๆ

## นำเข้า Namespaces
เพื่อเริ่มต้น ให้นำเข้า Namespaces ที่จำเป็นในโปรเจกต์ C# ของคุณ:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```

## วิธีสกัดฟอนต์และบันทึกทรัพยากร HTML ไปยังโฟลเดอร์?
โหลดเอกสารต้นฉบับของคุณด้วย `Editor editor = new Editor("sample.docx", new WordProcessingLoadOptions());` จากนั้นเรียก `editor.Save("output.html", SaveOptions.Html);` หลังจากการบันทึก คอลเลกชัน `Resources` จะมีทรัพยากรที่สกัดทั้งหมด—รวมถึงฟอนต์—ที่คุณสามารถวนลูปและเขียนลงดิสก์ วิธีการแบบขั้นตอนเดียวนี้จัดการทั้งการแปลงและการสกัดทรัพยากรโดยอัตโนมัติ

## ขั้นตอนที่ 1: เริ่มต้น GroupDocs.Editor
`Editor` เป็นคลาสหลักที่ประสานการโหลดเอกสาร, การแปลง, และการสกัดทรัพยากร มันเป็นตัวแทนของเซสชันเอกสารเดียวในหน่วยความจำ.
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
ขั้นแรก ให้เริ่มต้นอ็อบเจ็กต์ `Editor` โดยระบุพาธไปยังเอกสารตัวอย่างของคุณ ในตัวอย่างนี้ เราใช้เอกสาร Word ดังนั้นเราจึงระบุ `WordProcessingLoadOptions` เป็นประเภทของเอกสาร.

## ขั้นตอนที่ 2: แก้ไขเอกสาร
`EditableDocument` เป็นตัวแทนที่สามารถแก้ไขได้ซึ่งคืนค่าจากเมธอด `Edit` ทำให้คุณสามารถจัดการเอกสารก่อนบันทึกได้.
```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
ต่อไป สร้างอ็อบเจ็กต์ `EditableDocument` โดยเรียกเมธอด `Edit` ของอ็อบเจ็กต์ `Editor` ซึ่งทำให้คุณสามารถทำการแก้ไขบนเอกสารได้.

## ขั้นตอนที่ 3: สกัดทรัพยากร
`Resources` เป็นคอลเลกชันที่จัดกลุ่มทรัพยากรที่สกัด—รูปภาพ, ฟอนต์, และ Stylesheets—เป็นรายการแยกต่างหากเพื่อความสะดวกในการจัดการ.
```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
สกัดทรัพยากรเช่นรูปภาพ, ฟอนต์, และ Stylesheets จากเอกสารและเก็บไว้ในรายการที่สอดคล้องกัน.

## ขั้นตอนที่ 4: ระบุโฟลเดอร์ปลายทาง
`outputFolder` เป็นสตริงที่กำหนดตำแหน่งที่ไฟล์ที่สกัดจะถูกเขียน คุณสามารถชี้ไปยังไดเรกทอรีที่เขียนได้บนเซิร์ฟเวอร์หรือเครื่องท้องถิ่นใด ๆ.
```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
กำหนดโฟลเดอร์ปลายทางที่ทรัพยากรที่สกัดจะถูกบันทึก คุณสามารถปรับแต่งพาธของโฟลเดอร์ตามความต้องการของคุณ.

## ขั้นตอนที่ 5: บันทึกทรัพยากร
`SaveResource` เป็นฟังก์ชันช่วยเหลือที่เขียนทรัพยากรไบนารีเดียว (รูปภาพ, ฟอนต์, หรือ Stylesheet) ไปยังระบบไฟล์.
```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
วนลูปผ่านแต่ละทรัพยากรรูปภาพ, บันทึกลงโฟลเดอร์ปลายทาง, และแสดงข้อมูลที่เกี่ยวข้องเช่นชื่อไฟล์, ประเภท, และขนาด.
```csharp
		foreach (FontResourceBase oneFont in fonts)
		{
			Console.WriteLine("Saving {0} of {1} type",
				oneFont.FilenameWithExtension, oneFont.Type.FormalName);
			oneFont.Save(Path.Combine(outputFolder, oneFont.FilenameWithExtension));
		}
```
เช่นเดียวกัน, บันทึกแต่ละทรัพยากรฟอนต์ลงโฟลเดอร์ปลายทาง.
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
สุดท้าย, บันทึกแต่ละ Stylesheet ลงโฟลเดอร์ปลายทางและเสร็จสิ้นกระบวนการแก้ไข.

## ปัญหาที่พบบ่อยและวิธีแก้
- **Missing fonts after conversion** – ตรวจสอบว่าเอกสารต้นทางฝังฟอนต์จริงหรือไม่; หากไม่, GroupDocs.Editor จะอ้างอิงฟอนต์ของระบบเท่านั้น.
- **Access denied errors** – ยืนยันว่ากระบวนการแอปพลิเคชันมีสิทธิ์เขียนไปยังโฟลเดอร์ปลายทาง.
- **Large documents cause high memory usage** – ใช้ `LoadOptions` กับ `LoadMode = LoadMode.Stream` เพื่อสตรีมไฟล์ขนาดใหญ่แทนการโหลดทั้งหมดเข้าสู่หน่วยความจำ.

## คำถามที่พบบ่อย
**Q: GroupDocs.Editor รองรับรูปแบบเอกสารอื่น ๆ นอกจาก Word หรือไม่?**  
A: ใช่, รองรับ Excel, PowerPoint, PDF, HTML, และรูปแบบเพิ่มเติมกว่า 50 รูปแบบสำหรับการแก้ไขและการสกัดทรัพยากร

**Q: ฉันสามารถรวม GroupDocs.Editor เข้าในเว็บแอปพลิเคชันได้หรือไม่?**  
A: แน่นอน. API ทำงานอย่างราบรื่นกับ ASP.NET Core, MVC, และโครงการ Web API ทำให้คุณสามารถประมวลผลเอกสารบนฝั่งเซิร์ฟเวอร์ได้

**Q: GroupDocs.Editor มีการรวมการจัดเก็บข้อมูลบนคลาวด์หรือไม่?**  
A: มี, มีคอนเนคเตอร์ในตัวสำหรับ Google Drive, Dropbox, OneDrive, และ Amazon S3 ทำให้สามารถโหลดและบันทึกเอกสารโดยตรงบนคลาวด์ได้

**Q: มีการทดลองใช้ฟรีสำหรับ GroupDocs.Editor หรือไม่?**  
A: สามารถดาวน์โหลดการทดลองใช้เต็มรูปแบบ 30‑วันจากเว็บไซต์ GroupDocs โดยไม่ต้องใช้บัตรเครดิต

**Q: ฉันจะรับการสนับสนุนด้านเทคนิคสำหรับปัญหาการสกัดได้อย่างไร?**  
A: คุณสามารถติดต่อทีมสนับสนุนของ GroupDocs ผ่านฟอรั่มอย่างเป็นทางการ, ส่งตั๋วผ่านพอร์ทัลลูกค้า, หรือศึกษาคู่มือ API อย่างละเอียด

---

**อัปเดตล่าสุด:** 2026-05-12  
**ทดสอบด้วย:** GroupDocs.Editor 23.11 for .NET  
**ผู้เขียน:** GroupDocs

## บทเรียนที่เกี่ยวข้อง
- [การแก้ไขเอกสารอย่างมีประสิทธิภาพด้วย GroupDocs.Editor .NET: แปลง HTML เป็นเอกสารที่แก้ไขได้](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)
- [สกัดและบันทึกทรัพยากร DOCX อย่างมีประสิทธิภาพโดยใช้ GroupDocs.Editor .NET - คู่มือครบถ้วน](/editor/net/document-saving/efficient-extract-save-docx-resources-groupdocs-editor-net/)
- [เชี่ยวชาญการแก้ไขและแปลงเอกสารด้วย GroupDocs.Editor .NET: คู่มือครบถ้วน](/editor/net/document-editing/groupdocs-editor-net-mastering-document-editing/)