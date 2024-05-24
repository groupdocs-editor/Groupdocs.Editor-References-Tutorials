---
title: ทำงานร่วมกับคอลเลกชันฟิลด์ฟอร์มดั้งเดิม
linktitle: ทำงานร่วมกับคอลเลกชันฟิลด์ฟอร์มดั้งเดิม
second_title: GroupDocs.Editor .NET API
description: เรียนรู้วิธีจัดการฟิลด์แบบฟอร์มเดิมโดยใช้ GroupDocs.Editor สำหรับ .NET พร้อมคำแนะนำโดยละเอียดของเรา เหมาะสำหรับการจัดการช่องข้อความ ช่องทำเครื่องหมาย วันที่ และอื่นๆ
type: docs
weight: 12
url: /th/net/form-field-management/work-legacy-form-field-collection/
---
## การแนะนำ
ยินดีต้อนรับสู่คู่มือที่ครอบคลุมเกี่ยวกับวิธีการทำงานกับคอลเลกชันฟิลด์แบบฟอร์มเดิมโดยใช้ GroupDocs.Editor สำหรับ .NET ไม่ว่าคุณจะจัดการกับช่องข้อความ ช่องทำเครื่องหมาย ช่องวันที่ หรือเมนูแบบเลื่อนลง บทช่วยสอนนี้จะแนะนำแต่ละขั้นตอนในการจัดการช่องเหล่านี้อย่างมีประสิทธิภาพ ในตอนท้ายของคู่มือนี้ คุณจะมีความเข้าใจที่ชัดเจนเกี่ยวกับวิธีการใช้ GroupDocs.Editor เพื่อจัดการช่องแบบฟอร์มต่างๆ ในเอกสารของคุณ มาดำน้ำกันเถอะ!
## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะเริ่ม ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นดังต่อไปนี้:
- Visual Studio: เวอร์ชันล่าสุดจะใช้งานได้
- .NET Framework: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง .NET Framework แล้ว
-  GroupDocs.Editor สำหรับ .NET: ดาวน์โหลดเวอร์ชันล่าสุด[ที่นี่](https://releases.groupdocs.com/editor/net/).
- เอกสารตัวอย่าง: ไฟล์ DOCX ตัวอย่างพร้อมช่องแบบฟอร์มสำหรับการทดสอบ
## นำเข้าเนมสเปซ
ขั้นแรก ให้นำเข้าเนมสเปซที่จำเป็นในโปรเจ็กต์ของคุณ เนมสเปซเหล่านี้จำเป็นสำหรับการเข้าถึงคลาสและวิธีการที่จำเป็นในการจัดการฟิลด์แบบฟอร์ม
```csharp
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System.IO;
```
## ขั้นตอนที่ 1: รับเส้นทางไฟล์อินพุต
ขั้นแรก คุณต้องระบุเส้นทางไปยังไฟล์อินพุตของคุณ ในตัวอย่างนี้ เราจะใช้ไฟล์ DOCX ตัวอย่างที่มีช่องแบบฟอร์มต่างๆ
```csharp
string inputFilePath = "path/to/your/sample_legacy_formfields.docx";
```
## ขั้นตอนที่ 2: สร้างสตรีมจากเส้นทางไฟล์
จากนั้น สร้างสตรีมไฟล์เพื่ออ่านเนื้อหาในเอกสารของคุณ สตรีมนี้จะใช้ในการโหลดเอกสารลงใน GroupDocs.Editor
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
    // รหัสเพิ่มเติมจะอยู่ที่นี่
}
```
## ขั้นตอนที่ 3: สร้างตัวเลือกการโหลดสำหรับเอกสาร
ก่อนที่จะโหลดเอกสาร ให้สร้างตัวเลือกการโหลด ตัวเลือกเหล่านี้จะช่วยจัดการกับสถานการณ์ต่างๆ เช่น เอกสารที่มีการป้องกันด้วยรหัสผ่าน
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
// หากเอกสารมีการป้องกันด้วยรหัสผ่าน ให้ระบุรหัสผ่าน
loadOptions.Password = "your_password_here"; // ใช้รหัสผ่านจริงหากจำเป็น
```
## ขั้นตอนที่ 4: โหลดเอกสารด้วยอินสแตนซ์ตัวแก้ไข
ตอนนี้ ให้โหลดเอกสารลงในอินสแตนซ์ Editor โดยใช้สตรีมไฟล์และตัวเลือกการโหลดที่คุณสร้างไว้ก่อนหน้านี้
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    // รหัสเพิ่มเติมจะอยู่ที่นี่
}
```
## ขั้นตอนที่ 5: อ่านอินสแตนซ์ FormFieldManager
หากต้องการจัดการช่องแบบฟอร์ม ให้เข้าถึงอินสแตนซ์ FormFieldManager จาก Editor อินสแตนซ์นี้จะช่วยให้คุณสามารถโต้ตอบกับช่องแบบฟอร์มภายในเอกสารของคุณได้
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
## ขั้นตอนที่ 6: อ่าน FormFieldCollection
ดึงข้อมูล FormFieldCollection จาก FormFieldManager คอลเลกชันนี้ประกอบด้วยฟิลด์แบบฟอร์มทั้งหมดที่มีอยู่ในเอกสาร
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
## ขั้นตอนที่ 7: วนซ้ำแต่ละช่องแบบฟอร์ม
วนซ้ำช่องแบบฟอร์มแต่ละช่องในคอลเลกชันและระบุประเภทของแบบฟอร์ม คุณสามารถแยกและจัดการค่าของฟิลด์ได้ ทั้งนี้ขึ้นอยู่กับประเภท
```csharp
foreach (var formField in collection)
{
    switch (formField.Type)
    {
        case FormFieldType.Text:
            TextFormField textFormField = collection.GetFormField<TextFormField>(formField.Name);
            Console.WriteLine($"TextFormField detected, name: {formField.Name}, value: {textFormField.Value}");
            break;
        case FormFieldType.CheckBox:
            CheckBoxForm checkBoxFormField = collection.GetFormField<CheckBoxForm>(formField.Name);
            Console.WriteLine($"CheckBoxForm detected, name: {formField.Name}, value: {checkBoxFormField.Value}");
            break;
        case FormFieldType.Date:
            DateFormField dateFormField = collection.GetFormField<DateFormField>(formField.Name);
            Console.WriteLine($"DateFormField detected, name: {formField.Name}, value: {dateFormField.Value}");
            break;
        case FormFieldType.Number:
            NumberFormField numberFormField = collection.GetFormField<NumberFormField>(formField.Name);
            Console.WriteLine($"NumberFormField detected, name: {formField.Name}, value: {numberFormField.Value}");
            break;
        case FormFieldType.DropDown:
            DropDownFormField dropDownFormField = collection.GetFormField<DropDownFormField>(formField.Name);
            Console.WriteLine($"DropDownFormField detected, name: {formField.Name}, value selected: {dropDownFormField.Value[dropDownFormField.SelectedIndex]}");
            break;
    }
}
```
## ขั้นตอนที่ 8: บทสรุป
เมื่อทำตามขั้นตอนเหล่านี้ คุณจะจัดการและโต้ตอบกับฟิลด์แบบฟอร์มเดิมในเอกสารของคุณได้อย่างมีประสิทธิภาพโดยใช้ GroupDocs.Editor สำหรับ .NET ไม่ว่าจะเป็นช่องข้อความ ช่องทำเครื่องหมาย วันที่ ตัวเลข หรือเมนูแบบเลื่อนลง คู่มือนี้ให้วิธีที่ชัดเจนและรัดกุมในการจัดการแต่ละประเภท
## บทสรุป
 การทำงานกับฟิลด์แบบฟอร์มเดิมในเอกสารสามารถทำได้อย่างตรงไปตรงมาเมื่อใช้เครื่องมือที่เหมาะสม GroupDocs.Editor สำหรับ .NET มอบโซลูชันที่มีประสิทธิภาพสำหรับการจัดการฟิลด์เหล่านี้อย่างมีประสิทธิภาพ เมื่อทำตามคำแนะนำทีละขั้นตอนนี้ คุณจะสามารถจัดการช่องแบบฟอร์มต่างๆ ในเอกสารของคุณได้อย่างง่ายดาย อย่าลืมไปสำรวจ[เอกสารประกอบ](https://reference.groupdocs.com/editor/net/)สำหรับคุณสมบัติและตัวเลือกขั้นสูงเพิ่มเติม
## คำถามที่พบบ่อย
### 1. ฉันสามารถใช้ GroupDocs.Editor สำหรับ .NET กับเอกสารที่มีการป้องกันด้วยรหัสผ่านได้หรือไม่
ได้ คุณสามารถระบุรหัสผ่านในตัวเลือกการโหลดเพื่อจัดการเอกสารที่มีการป้องกันด้วยรหัสผ่านได้
### 2. ฉันจะทดลองใช้ GroupDocs.Editor สำหรับ .NET ฟรีได้อย่างไร
 คุณสามารถดาวน์โหลดรุ่นทดลองใช้ฟรีได้จาก[ที่นี่](https://releases.groupdocs.com/).
### 3. GroupDocs.Editor สำหรับ .NET มีการสนับสนุนใดๆ หรือไม่
 ใช่ คุณสามารถเข้าถึงการสนับสนุนได้[ที่นี่](https://forum.groupdocs.com/c/editor/20).
### 4. ฉันสามารถซื้อใบอนุญาตสำหรับ GroupDocs.Editor สำหรับ .NET ได้หรือไม่
 ใช่ คุณสามารถซื้อใบอนุญาตได้จาก[ที่นี่](https://purchase.groupdocs.com/buy).
### 5. ฉันจะหาเอกสารสำหรับ GroupDocs.Editor สำหรับ .NET ได้ที่ไหน
เอกสารก็มีให้[ที่นี่](https://reference.groupdocs.com/editor/net/).