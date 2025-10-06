---
title: บันทึกเอกสาร
linktitle: บันทึกเอกสาร
second_title: GroupDocs.Editor .NET API
description: แก้ไขและบันทึกเอกสารได้อย่างง่ายดายโดยใช้ GroupDocs.Editor สำหรับ .NET คำแนะนำทีละขั้นตอนนี้ทำให้กระบวนการสำหรับนักพัฒนาง่ายขึ้น
weight: 14
url: /th/net/document-editing/save-document/
type: docs
---
# บันทึกเอกสาร

## การแนะนำ
คุณต้องการแก้ไขและบันทึกเอกสารอย่างง่ายดายโดยใช้ GroupDocs.Editor สำหรับ .NET หรือไม่? คุณอยู่ในสถานที่ที่เหมาะสม! บทช่วยสอนนี้จะแนะนำคุณตลอดกระบวนการทีละขั้นตอน เพื่อให้มั่นใจว่าคุณสามารถจัดการเอกสารของคุณได้อย่างง่ายดาย ไม่ว่าคุณจะเป็นนักพัฒนาที่มีประสบการณ์หรือมือใหม่ คู่มือของเราจะให้ข้อมูลทั้งหมดที่คุณต้องการในการเริ่มต้น
## ข้อกำหนดเบื้องต้น
ก่อนที่จะเข้าสู่บทช่วยสอน ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้:
- สภาพแวดล้อมการพัฒนา: ติดตั้ง Visual Studio บนเครื่องของคุณ
- .NET Framework: ตรวจสอบให้แน่ใจว่าคุณมี .NET Framework 4.6.1 หรือใหม่กว่า
-  GroupDocs.Editor สำหรับ .NET: ดาวน์โหลดเวอร์ชันล่าสุด[ที่นี่](https://releases.groupdocs.com/editor/net/).
- ความรู้พื้นฐาน C#: ความคุ้นเคยกับการเขียนโปรแกรม C# เป็นสิ่งจำเป็น
## นำเข้าเนมสเปซ
หากต้องการใช้ GroupDocs.Editor ในโปรเจ็กต์ .NET คุณต้องนำเข้าเนมสเปซที่จำเป็น นี่คือวิธีการ:
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
ตอนนี้เราได้ตั้งค่าสภาพแวดล้อมและนำเข้าเนมสเปซที่จำเป็นแล้ว เรามาเจาะลึกขั้นตอนที่จำเป็นในการโหลด แก้ไข และบันทึกเอกสารโดยใช้ GroupDocs.Editor สำหรับ .NET กัน
## ขั้นตอนที่ 1: โหลดเอกสาร
ขั้นแรก เราต้องโหลดเอกสารที่เราต้องการแก้ไข GroupDocs.Editor ทำให้กระบวนการนี้ตรงไปตรงมา ต่อไปนี้คือวิธีที่คุณสามารถทำได้:

```csharp
string inputFilePath = "Your Sample Document";
Editor editor = new Editor(inputFilePath, delegate { return new Options.WordProcessingLoadOptions(); });
EditableDocument defaultWordProcessingDoc = editor.Edit();
```
 ในขั้นตอนนี้ เราระบุเส้นทางไปยังเอกสารที่เราต้องการแก้ไขและสร้างอินสแตนซ์ของ`Editor` ระดับ. ที่`Edit` จากนั้นจึงเรียกเมธอดนี้ให้โหลดเอกสารลงในไฟล์`EditableDocument` วัตถุ.
## ขั้นตอนที่ 2: แก้ไขเอกสาร
เมื่อโหลดเอกสารแล้ว ก็ถึงเวลาทำการแก้ไขบางอย่าง เนื่องจากเราไม่มีโปรแกรมแก้ไขแบบ WYSIWYG แนบมา เราจะจำลองกระบวนการแก้ไขในรูปแบบโค้ด

```csharp
string allEmbeddedInsideString = defaultWordProcessingDoc.GetEmbeddedHtml();
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
EditableDocument editedDoc = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```
 ที่นี่ เราจะดึงเนื้อหา HTML ที่ฝังไว้ของเอกสาร ดำเนินการแทนที่ข้อความอย่างง่าย และสร้างข้อความใหม่`EditableDocument`อินสแตนซ์จาก HTML ที่แก้ไข
## ขั้นตอนที่ 3: บันทึกเอกสาร
หลังจากแก้ไขเอกสารแล้ว ขั้นตอนสุดท้ายคือการบันทึก GroupDocs.Editor มีตัวเลือกมากมายสำหรับการบันทึกเอกสารในรูปแบบต่างๆ
## บันทึกเป็น RTF
```csharp
string outputRtfPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.rtf");
WordProcessingSaveOptions rtfSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
editor.Save(editedDoc, outputRtfPath, rtfSaveOptions);
```
## บันทึกเป็น DOCM
```csharp
string outputDocmPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.docm");
WordProcessingSaveOptions docmSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm);
using (FileStream outputStream = File.Create(outputDocmPath))
{
    editor.Save(editedDoc, outputStream, docmSaveOptions);
}
```
## บันทึกเป็นข้อความธรรมดา
```csharp
string outputTxtPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.txt");
TextSaveOptions textSaveOptions = new TextSaveOptions
{
    Encoding = System.Text.Encoding.UTF8,
    PreserveTableLayout = true
};
editor.Save(editedDoc, outputTxtPath, textSaveOptions);
```
## ขั้นตอนที่ 4: การล้างข้อมูล
 สุดท้ายนี้ สิ่งสำคัญคือต้องกำจัดทิ้ง`EditableDocument` และ`Editor` อินสแตนซ์เพื่อเพิ่มทรัพยากร
```csharp
editedDoc.Dispose();
defaultWordProcessingDoc.Dispose();
editor.Dispose();
```
เมื่อทำตามขั้นตอนเหล่านี้ คุณจะสามารถโหลด แก้ไข และบันทึกเอกสารโดยใช้ GroupDocs.Editor for .NET ได้อย่างมีประสิทธิภาพ เครื่องมืออันทรงพลังนี้มอบความยืดหยุ่นและความสะดวกในการใช้งาน ทำให้การจัดการเอกสารเป็นเรื่องง่าย
## บทสรุป
การแก้ไขและบันทึกเอกสารโดยทางโปรแกรมได้ง่ายกว่าที่เคยด้วย GroupDocs.Editor สำหรับ .NET คู่มือนี้จะอธิบายคุณตลอดกระบวนการทั้งหมด ตั้งแต่การโหลดเอกสารไปจนถึงการบันทึกในรูปแบบต่างๆ ด้วย GroupDocs.Editor คุณจะมีโซลูชันที่หลากหลายและมีประสิทธิภาพเพียงปลายนิ้วสัมผัส ซึ่งทำให้กระบวนการแก้ไขเอกสารง่ายขึ้น
## คำถามที่พบบ่อย
### GroupDocs.Editor รองรับไฟล์รูปแบบใดบ้าง
GroupDocs.Editor รองรับไฟล์หลากหลายรูปแบบ รวมถึง DOCX, RTF, TXT และอื่นๆ อีกมากมาย สำหรับรายการทั้งหมด โปรดดูที่[เอกสารประกอบ](https://tutorials.groupdocs.com/editor/net/).
### ฉันสามารถลองใช้ GroupDocs.Editor ก่อนซื้อได้หรือไม่
 ใช่ คุณจะได้รับ[ทดลองฟรี](https://releases.groupdocs.com/) เพื่อทดสอบคุณสมบัติของ GroupDocs.Editor
### มีการสนับสนุนใด ๆ หรือไม่หากฉันประสบปัญหา?
 อย่างแน่นอน! ท่านสามารถเยี่ยมชมได้ที่[ฟอรั่มการสนับสนุน](https://forum.groupdocs.com/c/editor/20) เพื่อช่วยเหลือในทุกปัญหาที่คุณพบ
### ฉันจะขอรับใบอนุญาตชั่วคราวได้อย่างไร
 คุณสามารถขอ[ใบอนุญาตชั่วคราว](https://purchase.groupdocs.com/temporary-license/) เพื่อวัตถุประสงค์ในการประเมินผล
### ฉันจะซื้อ GroupDocs.Editor เวอร์ชันเต็มได้ที่ไหน
 คุณสามารถซื้อเวอร์ชันเต็มได้[ที่นี่](https://purchase.groupdocs.com/buy).