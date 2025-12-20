---
date: '2025-12-20'
description: เรียนรู้วิธีแก้ไขเอกสาร Excel และ Word ใน Java ด้วย GroupDocs.Editor.
  ทำให้การสร้างรายงานอัตโนมัติ, ดึงฟอนต์ที่ฝังไว้, และเพิ่มประสิทธิภาพการทำงาน.
keywords:
- GroupDocs Editor Java
- Java document editing
- Word document automation in Java
title: วิธีแก้ไขไฟล์ Excel และ Word ใน Java ด้วย GroupDocs.Editor
type: docs
url: /th/java/document-editing/java-groupdocs-editor-master-document-editing/
weight: 1
---

# วิธีแก้ไขไฟล์ Excel และ Word ใน Java ด้วย GroupDocs.Editor

ในแอปพลิเคชัน Java สมัยใหม่ ความสามารถในการ **แก้ไขไฟล์ Excel** อย่างอัตโนมัติเป็นสิ่งที่เปลี่ยนเกมสำหรับธุรกิจที่ต้องการสร้างรายงานอัตโนมัติ, ปรับปรุงสเปรดชีตแบบเรียลไทม์, หรือปรับแต่งเทมเพลตให้เหมาะกับผู้ใช้แต่ละคน บทเรียนนี้จะแสดงขั้นตอนการแก้ไขเอกสาร Excel และ Word ด้วย GroupDocs.Editor พร้อมทั้งครอบคลุมเทคนิคการเพิ่มประสิทธิภาพ Java และวิธีดึงฟอนต์ที่ฝังอยู่เมื่อจำเป็น

## บทนำ
ในโลกดิจิทัลที่เปลี่ยนแปลงอย่างรวดเร็ว การจัดการและแก้ไขเอกสารอย่างมีประสิทธิภาพเป็นสิ่งสำคัญสำหรับธุรกิจและบุคคล ไม่ว่าคุณจะทำการสร้างรายงานอัตโนมัติหรือปรับแต่งเทมเพลตแบบเรียลไทม์ การเชี่ยวชาญการจัดการเอกสารสามารถเพิ่มผลผลิตได้อย่างมาก คู่มือนี้จะพาคุณผ่านการใช้ GroupDocs.Editor สำหรับ Java เพื่อโหลด, แก้ไข, และบันทึกไฟล์ Word และ Excel อย่างมั่นใจ

**สิ่งที่คุณจะได้เรียนรู้**
- วิธีโหลดและแก้ไขเอกสารประมวลผลคำด้วยตัวเลือกเริ่มต้นและตัวเลือกกำหนดเอง  
- วิธี **แก้ไขไฟล์ Excel** โดยกำหนดเป้าหมายที่แท็บเฉพาะ  
- การใช้งานจริง เช่น การสร้างรายงานอัตโนมัติและการปรับแต่งเทมเพลต  
- เคล็ดลับการเพิ่มประสิทธิภาพ Java เพื่อให้แอปพลิเคชันของคุณตอบสนองได้ดี  

พร้อมที่จะก้าวเข้าสู่โลกของการแก้ไขเอกสารอัตโนมัติหรือยัง? เริ่มกันเลย!

## คำตอบสั้น
- **ไลบรารีใดที่ทำให้สามารถแก้ไขไฟล์ Excel ใน Java ได้?** GroupDocs.Editor สำหรับ Java  
- **ฉันสามารถแก้ไขแท็บ Excel เฉพาะโดยไม่ต้องโหลดทั้งเวิร์กบุ๊กได้หรือไม่?** ได้, โดยใช้ `SpreadsheetEditOptions.setWorksheetIndex()`  
- **ฉันจะดึงฟอนต์ที่ฝังอยู่ทั้งหมดจากเอกสาร Word อย่างไร?** ตั้งค่า `FontExtractionOptions.ExtractAllEmbedded` ใน `WordProcessingEditOptions`  
- **แนวทางปฏิบัติที่ดีที่สุดสำหรับการเพิ่มประสิทธิภาพ Java เมื่อจัดการไฟล์ขนาดใหญ่คืออะไร?** ทำลาย (dispose) วัตถุ `EditableDocument` และ `Editor` ทันทีและใช้ตัวเลือกการโหลดซ้ำเมื่อเป็นไปได้  
- **ต้องมีลิขสิทธิ์สำหรับการใช้งานในโปรดักชันหรือไม่?** แนะนำให้ใช้ลิขสิทธิ์เต็มของ GroupDocs.Editor สำหรับการใช้งานในโปรดักชัน  

## ข้อกำหนดเบื้องต้น
ก่อนเริ่ม, โปรดตรวจสอบว่าคุณมีสิ่งต่อไปนี้:

### ไลบรารีและการพึ่งพาที่จำเป็น
- **GroupDocs.Editor สำหรับ Java** (เวอร์ชัน 25.3 หรือใหม่กว่า)  
- **Java Development Kit (JDK)** 8 หรือสูงกว่า  

### ความต้องการการตั้งค่าสภาพแวดล้อม
- IDE เช่น IntelliJ IDEA หรือ Eclipse  
- ความคุ้นเคยพื้นฐานกับแนวคิดการเขียนโปรแกรม Java  

## การตั้งค่า GroupDocs.Editor สำหรับ Java
เพื่อรวม GroupDocs.Editor ในโปรเจกต์ของคุณ, ทำตามขั้นตอนต่อไปนี้:

**Maven**  
เพิ่มโค้ดต่อไปนี้ในไฟล์ `pom.xml` ของคุณ:
```xml
<repositories>
   <repository>
      <id>repository.groupdocs.com</id>
      <name>GroupDocs Repository</name>
      <url>https://releases.groupdocs.com/editor/java/</url>
   </repository>
</repositories>

<dependencies>
   <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-editor</artifactId>
      <version>25.3</version>
   </dependency>
</dependencies>
```

**ดาวน์โหลดโดยตรง**  
หรือดาวน์โหลดไลบรารีจาก [GroupDocs.Editor for Java releases](https://releases.groupdocs.com/editor/java/)  

### การรับลิขสิทธิ์
- **ทดลองใช้ฟรี** – เริ่มสำรวจฟีเจอร์โดยไม่ต้องผูกมัด  
- **ลิขสิทธิ์ชั่วคราว** – ขยายระยะเวลาการประเมินตามต้องการ  
- **ลิขสิทธิ์เต็ม** – แนะนำสำหรับการใช้งานในโปรดักชันเพื่อเปิดใช้งานคุณสมบัติทั้งหมด  

## วิธีแก้ไขเอกสาร Word ใน Java
ต่อไปนี้คือสามวิธีที่พบบ่อยในการทำงานกับไฟล์ Word

### โหลดและแก้ไขเอกสารประมวลผลคำด้วยตัวเลือกเริ่มต้น
**ภาพรวม:** โหลดไฟล์ DOCX ด้วยการตั้งค่าเริ่มต้นและรับอินสแตนซ์ที่สามารถแก้ไขได้
```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.EditableDocument;
import com.groupdocs.editor.options.WordProcessingLoadOptions;

String inputFilePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
Editor editor1 = new Editor(inputFilePath, new WordProcessingLoadOptions());
EditableDocument defaultWordProcessingDoc = editor1.edit();

// Manipulate the document as needed
defaultWordProcessingDoc.dispose();
editor1.dispose();
```
**พารามิเตอร์สำคัญ**
- `inputFilePath` – เส้นทางไปยังไฟล์ Word ของคุณ  
- `WordProcessingLoadOptions()` – โหลดเอกสารด้วยตัวเลือกเริ่มต้น  

### แก้ไขเอกสารประมวลผลคำด้วยตัวเลือกกำหนดเอง
**ภาพรวม:** ปิดการแบ่งหน้า, เปิดการดึงข้อมูลภาษา, และดึงฟอนต์ที่ฝังอยู่ทั้งหมด
```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.EditableDocument;
import com.groupdocs.editor.options.WordProcessingEditOptions;
import com.groupdocs.editor.options.FontExtractionOptions;

String inputFilePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
Editor editor1 = new Editor(inputFilePath, new WordProcessingLoadOptions());

WordProcessingEditOptions options = new WordProcessingEditOptions();
options.setEnablePagination(false);
options.setEnableLanguageInformation(true);
options.setFontExtraction(FontExtractionOptions.ExtractAllEmbedded);

EditableDocument editableDoc = editor1.edit(options);

// Manipulate the document as needed
editableDoc.dispose();
editor1.dispose();
```
**ตัวเลือกการกำหนดค่า**
- `setEnablePagination(false)` – ปิดการแบ่งหน้าเพื่อเร่งการแก้ไข  
- `setEnableLanguageInformation(true)` – ดึงข้อมูลเมตาดาต้าภาษา  
- `setFontExtraction(FontExtractionOptions.ExtractAllEmbedded)` – **ดึงฟอนต์ที่ฝังอยู่** เพื่อความแม่นยำเต็มรูปแบบ  

### แก้ไขเอกสารประมวลผลคำด้วยการกำหนดค่าอื่น
**ภาพรวม:** เปิดข้อมูลภาษาในขณะเดียวกันกับการดึงฟอนต์ที่ฝังอยู่โดยใช้คอนสตรัคเตอร์สั้น
```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.EditableDocument;
import com.groupdocs.editor.options.WordProcessingEditOptions;

String inputFilePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
Editor editor1 = new Editor(inputFilePath, new WordProcessingLoadOptions());

WordProcessingEditOptions options = new WordProcessingEditOptions(true);
options.setFontExtraction(FontExtractionOptions.ExtractAll);

EditableDocument editableDoc = editor1.edit(options);

// Manipulate the document as needed
editableDoc.dispose();
editor1.dispose();
```

## วิธีแก้ไขไฟล์ Excel ใน Java
GroupDocs.Editor ให้คุณกำหนดเป้าหมายที่แผ่นงานแต่ละแผ่น, ซึ่งเหมาะอย่างยิ่งสำหรับสถานการณ์ **แก้ไขไฟล์ Excel** ที่คุณต้องการแก้ไขเพียงแท็บเดียว

### โหลดและแก้ไขเอกสารสเปรดชีต (แท็บแรก)
**ภาพรวม:** แก้ไขแผ่นงานแรก (ดัชนี 0) ของไฟล์ Excel
```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.EditableDocument;
import com.groupdocs.editor.options.SpreadsheetLoadOptions;
import com.groupdocs.editor.options.SpreadsheetEditOptions;

String inputFilePath = "YOUR_DOCUMENT_DIRECTORY/sample.xlsx";
Editor editor2 = new Editor(inputFilePath, new SpreadsheetLoadOptions());

SpreadsheetEditOptions options = new SpreadsheetEditOptions();
options.setWorksheetIndex(0); // Access the first tab (index 0)

EditableDocument editableDoc = editor2.edit(options);

// Manipulate the document as needed
editableDoc.dispose();
editor2.dispose();
```

### โหลดและแก้ไขเอกสารสเปรดชีต (แท็บที่สอง)
**ภาพรวม:** แก้ไขแผ่นงานที่สอง (ดัชนี 1) ของเวิร์กบุ๊กเดียวกัน
```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.EditableDocument;
import com.groupdocs.editor.options.SpreadsheetLoadOptions;
import com.groupdocs.editor.options.SpreadsheetEditOptions;

String inputFilePath = "YOUR_DOCUMENT_DIRECTORY/sample.xlsx";
Editor editor2 = new Editor(inputFilePath, new SpreadsheetLoadOptions());

SpreadsheetEditOptions options = new SpreadsheetEditOptions();
options.setWorksheetIndex(1); // Access the second tab (index 1)

EditableDocument editableDoc = editor2.edit(options);

// Manipulate the document as needed
editableDoc.dispose();
editor2.dispose();
```

## การใช้งานจริง
- **การสร้างรายงานอัตโนมัติ** – สร้างรายงานประสิทธิภาพรายเดือนโดยเติมเทมเพลต Excel ผ่านโค้ด  
- **การปรับแต่งเทมเพลต** – แก้ไขสัญญา Word หรือใบแจ้งหนี้แบบเรียลไทม์ตามข้อมูลผู้ใช้  
- **การรวมข้อมูล** – รวมข้อมูลจากหลายสเปรดชีตโดยไม่ต้องโหลดเวิร์กบุ๊กทั้งหมดเข้าสู่หน่วยความจำ, ช่วยเพิ่ม **การเพิ่มประสิทธิภาพ Java**  
- **การบูรณาการกับ CRM** – อัปเดตเอกสารลูกค้าในระบบ CRM อัตโนมัติ  

## พิจารณาด้านประสิทธิภาพ
เพื่อให้แอปพลิเคชัน Java ของคุณตอบสนองได้ดีเมื่อทำงานกับเอกสารขนาดใหญ่:

1. **ทำลายวัตถุโดยเร็ว** – เรียก `dispose()` บน `EditableDocument` และ `Editor` ทันทีที่เสร็จงาน  
2. **ใช้ตัวเลือกการโหลดซ้ำ** – สร้างอินสแตนซ์เดียวของ `WordProcessingLoadOptions` หรือ `SpreadsheetLoadOptions` แล้วส่งต่อให้หลาย editor  
3. **กำหนดเป้าหมายที่แผ่นงานเฉพาะ** – การแก้ไขเฉพาะแท็บที่ต้องการช่วยลดการใช้หน่วยความจำ (ดูตัวอย่าง **แก้ไขไฟล์ Excel** ด้านบน)  
4. **หลีกเลี่ยงการแบ่งหน้าไม่จำเป็น** – ปิดการแบ่งหน้า (`setEnablePagination(false)`) จะทำให้การประมวลผลไฟล์ Word ขนาดใหญ่เร็วขึ้น  

## สรุป
ตอนนี้คุณมีพื้นฐานที่มั่นคงสำหรับ **การแก้ไขไฟล์ Excel** และ Word ใน Java ด้วย GroupDocs.Editor การใช้ตัวเลือกการโหลดและแก้ไขที่กำหนดเอง, การดึงฟอนต์ที่ฝังอยู่, และการปฏิบัติตามแนวทางเพิ่มประสิทธิภาพ จะช่วยให้คุณสร้างเวิร์กโฟลว์เอกสารอัตโนมัติที่แข็งแรงและขยายได้

**ขั้นตอนต่อไป**
- ทดลองใช้ `WordProcessingEditOptions` ต่าง ๆ เพื่อปรับแต่งประสบการณ์การแก้ไขของคุณ  
- สำรวจฟีเจอร์เพิ่มเติมของ GroupDocs.Editor เช่น การแปลงไฟล์หรือการป้องกันเอกสาร  
- ผสานตรรกะการแก้ไขเข้ากับบริการหรือสถาปัตยกรรมไมโครเซอร์วิสของคุณ  

## คำถามที่พบบ่อย

**Q: GroupDocs.Editor รองรับฟอร์แมต Word ทุกประเภทหรือไม่?**  
A: ใช่, รองรับ DOCX, DOCM, DOC และฟอร์แมต Word ที่ใช้กันทั่วไปอื่น ๆ  

**Q: ฉันสามารถแก้ไขไฟล์ Excel โดยไม่ต้องโหลดเวิร์กบุ๊กทั้งหมดเข้าสู่หน่วยความจำได้หรือไม่?**  
A: แน่นอน. โดยตั้งค่า `SpreadsheetEditOptions.setWorksheetIndex()` คุณจะแก้ไขเฉพาะแท็บที่เลือก, เหมาะสำหรับงาน **แก้ไขไฟล์ Excel**  

**Q: ฉันจะดึงฟอนต์ที่ฝังอยู่ทั้งหมดจากเอกสาร Word อย่างไร?**  
A: ใช้ `WordProcessingEditOptions.setFontExtraction(FontExtractionOptions.ExtractAllEmbedded)` ตามตัวอย่างในส่วนตัวเลือกกำหนดเอง  

**Q: แนวทางปฏิบัติที่ดีที่สุดสำหรับการเพิ่มประสิทธิภาพ Java เมื่อจัดการเอกสารขนาดใหญ่คืออะไร?**  
A: ทำลายวัตถุ `EditableDocument` และ `Editor` อย่างรวดเร็ว, กำหนดเป้าหมายที่แผ่นงานเฉพาะ, และปิดการแบ่งหน้าถ้าไม่จำเป็น  

**Q: จำเป็นต้องมีลิขสิทธิ์สำหรับการใช้งานในโปรดักชันหรือไม่?**  
A: ใช่, จำเป็นต้องมีลิขสิทธิ์เต็มของ GroupDocs.Editor สำหรับการใช้งานในโปรดักชันเพื่อเปิดใช้งานทุกฟีเจอร์และรับการสนับสนุน  

---

**อัปเดตล่าสุด:** 2025-12-20  
**ทดสอบกับ:** GroupDocs.Editor 25.3 for Java  
**ผู้เขียน:** GroupDocs