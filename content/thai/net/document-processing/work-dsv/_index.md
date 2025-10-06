---
title: ทำงานกับค่าที่คั่นด้วยตัวคั่น (DSV)
linktitle: ทำงานกับค่าที่คั่นด้วยตัวคั่น (DSV)
second_title: GroupDocs.Editor .NET API
description: เรียนรู้วิธีแก้ไขไฟล์ CSV และ TSV โดยใช้ GroupDocs.Editor สำหรับ .NET พร้อมคำแนะนำทีละขั้นตอนนี้ ปรับปรุงโครงการ .NET ของคุณได้อย่างง่ายดาย
weight: 12
url: /th/net/document-processing/work-dsv/
type: docs
---
# ทำงานกับค่าที่คั่นด้วยตัวคั่น (DSV)

## การแนะนำ
หากคุณเป็นนักพัฒนาซอฟต์แวร์ที่ทำงานโดยใช้ค่าที่คั่นด้วยตัวคั่น (DSV) เช่น ไฟล์ CSV หรือ TSV คุณจะทราบดีว่าการแก้ไขไฟล์เหล่านี้โดยทางโปรแกรมอาจเป็นงานที่ยุ่งยาก อย่างไรก็ตาม ด้วย GroupDocs.Editor สำหรับ .NET งานนี้ง่ายขึ้นและมีประสิทธิภาพมากขึ้นอย่างเห็นได้ชัด ในบทช่วยสอนนี้ เราจะอธิบายวิธีใช้ GroupDocs.Editor สำหรับ .NET เพื่ออ่าน แก้ไข และบันทึกไฟล์ DSV เราจะแบ่งกระบวนการออกเป็นขั้นตอนที่ง่ายต่อการปฏิบัติตาม ซึ่งจะทำให้คุณสามารถนำไปใช้ในโครงการของคุณได้อย่างตรงไปตรงมา
## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะเจาะลึกบทช่วยสอน ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นดังต่อไปนี้:
- Visual Studio: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Visual Studio บนเครื่องของคุณ
-  GroupDocs.Editor สำหรับ .NET: คุณจะต้องดาวน์โหลดและอ้างอิงไลบรารี GroupDocs.Editor สำหรับ .NET คุณสามารถดาวน์โหลดได้[ที่นี่](https://releases.groupdocs.com/editor/net/).
- ความเข้าใจพื้นฐานของ C#: บทช่วยสอนนี้ถือว่าคุณมีความเข้าใจพื้นฐานเกี่ยวกับการพัฒนา C# และ .NET
## นำเข้าเนมสเปซ
ขั้นแรก คุณต้องนำเข้าเนมสเปซที่จำเป็นในโปรเจ็กต์ของคุณ เนมสเปซเหล่านี้มีคลาสและวิธีการที่จำเป็นในการทำงานกับ GroupDocs.Editor สำหรับ .NET
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

## ขั้นตอนที่ 1: รับเส้นทางไปยังไฟล์ DSV อินพุต
ขั้นแรก คุณต้องระบุเส้นทางไปยังไฟล์ DSV อินพุต สำหรับตัวอย่างนี้ เราจะถือว่ามันเป็นไฟล์ CSV
```csharp
string inputFilePath = "Your Sample Document";
```
## ขั้นตอนที่ 2: สร้างอินสแตนซ์ตัวแก้ไข
 สร้างอินสแตนซ์ของ`Editor` ระดับ. อินสแตนซ์นี้จะใช้ในการโหลดและจัดการไฟล์ DSV
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## ขั้นตอนที่ 3: สร้างตัวเลือกการแก้ไข DSV
 ถัดไป สร้างอินสแตนซ์ของ`DelimitedTextEditOptions` และระบุตัวคั่นสำหรับไฟล์ DSV ในที่นี้ เราใช้เครื่องหมายจุลภาคเป็นตัวคั่น
```csharp
    Options.DelimitedTextEditOptions editOptions = new DelimitedTextEditOptions(",");
    editOptions.ConvertDateTimeData = false;
    editOptions.ConvertNumericData = true;
    editOptions.TreatConsecutiveDelimitersAsOne = true;
```
## ขั้นตอนที่ 4: สร้างอินสแตนซ์เอกสารที่แก้ไขได้
 สร้าง`EditableDocument` อินสแตนซ์ที่ใช้`Editor.Edit` วิธี. นี่เป็นการเตรียมเอกสารสำหรับการแก้ไข
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## ขั้นตอนที่ 5: แก้ไขเนื้อหาเอกสาร
ดึงเนื้อหาข้อความต้นฉบับและทำการแก้ไขที่จำเป็น เพื่อวัตถุประสงค์ในการสาธิต ลองแทนที่ข้อความบางส่วน
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("SsangYong", "Chevrolet").Replace("Kyron", "Camaro");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## ขั้นตอนที่ 6: สร้างเอกสารที่แก้ไขได้พร้อมเนื้อหาที่อัปเดต
 สร้างใหม่`EditableDocument` ด้วยเนื้อหาที่อัปเดต
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## ขั้นตอนที่ 7: สร้างตัวเลือกการบันทึก CSV
ระบุตัวเลือกการบันทึกสำหรับรูปแบบ CSV รวมถึงตัวคั่นและการเข้ารหัส
```csharp
    Options.DelimitedTextSaveOptions csvSaveOptions = new DelimitedTextSaveOptions(",");
    csvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## ขั้นตอนที่ 8: สร้างตัวเลือกการบันทึก TSV
ในทำนองเดียวกัน ให้ระบุตัวเลือกการบันทึกสำหรับรูปแบบ TSV
```csharp
    Options.DelimitedTextSaveOptions tsvSaveOptions = new DelimitedTextSaveOptions("\t");
    tsvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## ขั้นตอนที่ 9: สร้างตัวเลือกการบันทึกสเปรดชีต
หากคุณต้องการบันทึกเอกสารเป็นสเปรดชีต ให้สร้างตัวเลือกการบันทึกที่เกี่ยวข้อง
```csharp
    Options.SpreadsheetSaveOptions cellsSaveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
```
## ขั้นตอนที่ 10: เตรียมเส้นทางบันทึก
กำหนดเส้นทางที่จะบันทึกไฟล์ที่แก้ไข
```csharp
    string outputCsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".csv");
    string outputTsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".tsv");
    string outputCellsPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".xlsm");
```
## ขั้นตอนที่ 11: บันทึกเอกสารที่แก้ไข
บันทึกเอกสารที่แก้ไขไปยังเส้นทางที่ระบุในรูปแบบต่างๆ
```csharp
    editor.Save(afterEdit, outputCsvPath, csvSaveOptions);
    editor.Save(afterEdit, outputTsvPath, tsvSaveOptions);
    editor.Save(afterEdit, outputCellsPath, cellsSaveOptions);
```
## ขั้นตอนที่ 12: กำจัดอินสแตนซ์เอกสารที่แก้ไขได้
 สุดท้ายนี้ ให้แน่ใจว่าได้กำจัดทิ้ง`EditableDocument` อินสแตนซ์เพื่อเพิ่มทรัพยากร
```csharp
    beforeEdit.Dispose();
    afterEdit.Dispose();
}
System.Console.WriteLine("WorkingWithDsv routine has successfully finished");
```
## บทสรุป
การแก้ไขไฟล์ DSV โดยใช้ GroupDocs.Editor สำหรับ .NET เป็นกระบวนการที่ไม่ซับซ้อนซึ่งเกี่ยวข้องกับการสร้างอินสแตนซ์ตัวแก้ไข การตั้งค่าตัวเลือกการแก้ไข การแก้ไขเนื้อหา และการบันทึกการเปลี่ยนแปลง คำแนะนำทีละขั้นตอนนี้จะช่วยให้คุณรวมฟังก์ชันการทำงานนี้เข้ากับแอปพลิเคชัน .NET ของคุณได้อย่างง่ายดาย ไม่ว่าคุณจะทำงานกับ CSV, TSV หรือรูปแบบ DSV อื่นๆ GroupDocs.Editor สำหรับ .NET มอบโซลูชันที่มีประสิทธิภาพและยืดหยุ่น
## คำถามที่พบบ่อย
### ฉันสามารถใช้ GroupDocs.Editor สำหรับ .NET เพื่อแก้ไขไฟล์ CSV ขนาดใหญ่ได้หรือไม่
ใช่ GroupDocs.Editor สำหรับ .NET สามารถจัดการไฟล์ CSV ขนาดใหญ่ได้อย่างมีประสิทธิภาพ
### GroupDocs.Editor สำหรับ .NET รองรับรูปแบบ DSV อื่นๆ นอกเหนือจาก CSV และ TSV หรือไม่
ใช่ รองรับรูปแบบ DSV ต่างๆ ตราบใดที่คุณระบุตัวคั่นที่เหมาะสม
### เป็นไปได้หรือไม่ที่จะปรับแต่งการเข้ารหัสเมื่อบันทึกไฟล์ DSV
แน่นอน คุณสามารถระบุการเข้ารหัสที่ต้องการได้ในตัวเลือกการบันทึก
### ฉันสามารถแปลงไฟล์ CSV เป็นสเปรดชีต Excel โดยใช้ GroupDocs.Editor สำหรับ .NET ได้หรือไม่
ได้ คุณสามารถบันทึกไฟล์ CSV เป็นสเปรดชีต Excel ได้โดยใช้ตัวเลือกการบันทึกที่เหมาะสม
### ฉันจะหาเอกสารเพิ่มเติมเกี่ยวกับ GroupDocs.Editor สำหรับ .NET ได้ที่ไหน
 คุณสามารถค้นหาเอกสารรายละเอียดได้[ที่นี่](https://tutorials.groupdocs.com/editor/net/)