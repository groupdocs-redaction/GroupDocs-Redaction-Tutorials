---
date: '2026-11-02'
description: เรียนรู้วิธีเพิ่มส่วนต่อท้ายให้กับชื่อไฟล์ในบทแนะนำ GroupDocs redaction
  Java โดยใช้ Maven, streaming load, annotation deletion และ save options
keywords:
- groupdocs redaction java tutorial
- add suffix filename java
- document redaction workflow
- groupdocs maven dependency
- java inputstream redaction
lastmod: '2026-11-02'
og_description: เรียนรู้วิธีเพิ่มส่วนต่อท้ายให้กับชื่อไฟล์ในบทแนะนำ GroupDocs redaction
  Java. ทำตาม step‑by‑step Maven setup, streaming load, และ save options
og_image_alt: Guide showing Java code to add suffix to redacted filenames using GroupDocs
  Redaction
og_title: วิธีเพิ่มส่วนต่อท้ายให้กับชื่อไฟล์ใน GroupDocs redaction Java
schemas:
- author: GroupDocs
  dateModified: '2026-11-02'
  description: Learn how to add suffix to filename in a GroupDocs redaction Java tutorial
    using Maven, streaming load, annotation deletion, and save options.
  headline: How to add suffix to filename in GroupDocs redaction Java
  type: TechArticle
- description: Learn how to add suffix to filename in a GroupDocs redaction Java tutorial
    using Maven, streaming load, annotation deletion, and save options.
  name: How to add suffix to filename in GroupDocs redaction Java
  steps:
  - name: '1: Create InputStream'
    text: '- **Why:** Using `InputStream` allows you to handle documents stored in
      various locations—cloud buckets, databases, or in‑memory buffers—without first
      writing them to disk. This approach is essential when you need to **load document
      from stream** in micro‑service architectures.'
  - name: '1: Apply DeleteAnnotationRedaction'
    text: '- **Why:** This step ensures that any sensitive annotations (comments,
      highlights, or hidden notes) are stripped from the document, enhancing privacy
      and compliance.'
  - name: '1: Configure SaveOptions'
    text: '- **Why:** Customizing save options allows flexible output formats and
      naming conventions. Enabling `setAddSuffix(true)` **adds suffix to filename**,
      making it clear that the file has been redacted.'
  type: HowTo
- questions:
  - answer: Yes, the library supports PDFs, DOCX, PPTX, XLSX, and many other formats.
    question: Can I redact PDF documents using GroupDocs.Redaction?
  - answer: Use streaming (`load document from stream`) and close resources promptly
      to keep memory usage low.
    question: What is the best way to handle large files with GroupDocs.Redaction?
  - answer: The API automatically adds a default suffix (e.g., “_redacted”). For custom
      suffixes, rename the output file after saving.
    question: Is it possible to customize the suffix text?
  - answer: Visit the [Temporary License page](https://purchase.groupdocs.com/temporary-license/)
      and follow the instructions.
    question: How do I obtain a temporary license for GroupDocs.Redaction?
  - answer: Join the [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33)
      for expert assistance.
    question: Where can I get help if I encounter issues?
  type: FAQPage
tags:
- groupdocs redaction
- java tutorial
- maven dependency
- document redaction
title: วิธีเพิ่มส่วนต่อท้ายให้กับชื่อไฟล์ใน GroupDocs redaction Java
type: docs
url: /th/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

# วิธีเพิ่มส่วนต่อท้ายชื่อไฟล์ใน GroupDocs redaction Java

ใน **groupdocs redaction java tutorial** คุณจะได้เรียนรู้วิธีเพิ่มส่วนต่อท้ายโดยอัตโนมัติให้กับชื่อไฟล์ผลลัพธ์เมื่อทำการลบข้อมูลในเอกสารด้วย GroupDocs.Redaction การเพิ่มส่วนต่อท้ายช่วยขจัดการตั้งชื่อด้วยตนเอง ลดความเสี่ยงของการรั่วไหลของไฟล์ที่ไม่ได้ลบข้อมูล และเข้ากันได้อย่างลงตัวกับสายงาน CI/CD ที่พึ่งพาการตั้งชื่อ คำแนะนำนี้จะพาคุณผ่านการตั้งค่า Maven, การโหลดเอกสารแบบสตรีม, การลบ annotation, และการกำหนดค่า save options — ทั้งหมดด้วยโค้ดที่กระชับและพร้อมใช้งานในสภาพแวดล้อมการผลิต

## คำตอบสั้น
- **“add suffix to filename” ทำอะไร?**  
  เมื่อคุณเปิดใช้งานตัวเลือกส่วนต่อท้าย SDK จะเพิ่มสตริงที่กำหนดไว้ล่วงหน้า (ค่าเริ่มต้นคือ “_redacted”) ไปยังชื่อฐานของไฟล์ผลลัพธ์ก่อนส่วนขยาย ทำให้เห็นได้ชัดเจนทันทีว่าไฟล์ใดถูกประมวลผล ช่วยป้องกันการแจกจ่ายไฟล์ต้นฉบับโดยบังเอิญ และทำให้การทำงานอัตโนมัติที่อิงการตั้งชื่อเป็นเรื่องง่ายขึ้น  
- **ฉันสามารถโหลดเอกสารจากสตรีมได้หรือไม่?**  
  ได้ — GroupDocs.Redaction รองรับการโหลดจาก `InputStream` ใดก็ได้ เหมาะสำหรับการจัดเก็บบนคลาวด์หรือการประมวลผลในหน่วยความจำ  
- **ฉันต้องมีใบอนุญาตสำหรับฟีเจอร์นี้หรือไม่?**  
  การทดลองใช้ฟรีทำงานสำหรับการลบข้อมูลพื้นฐาน; ใบอนุญาตชั่วคราวหรือเต็มจะเปิดใช้งานตัวเลือกขั้นสูงทั้งหมดรวมถึงการจัดการส่วนต่อท้าย  
- **ฟอร์แมตใดบ้างที่รองรับ?**  
  ไลบรารีรองรับ DOCX, PDF, PPTX, XLSX และอื่น ๆ อีกหลายรูปแบบ  
- **ต้องใช้ rasterization สำหรับการส่งออก PDF หรือไม่?**  
  rasterization เป็นตัวเลือก; เปิดใช้งานเมื่อคุณต้องการทำให้เอกสารเป็นแบบแบนเพื่อความปลอดภัยเพิ่มขึ้น  

## “add suffix to filename” ทำอะไร?

เมื่อคุณเปิดใช้งานตัวเลือกส่วนต่อท้าย SDK จะเพิ่มสตริงที่กำหนดไว้ล่วงหน้า (ค่าเริ่มต้นคือ “_redacted”) ไปยังชื่อฐานของไฟล์ผลลัพธ์ก่อนส่วนขยาย ทำให้เห็นได้ชัดเจนทันทีว่าไฟล์ใดถูกประมวลผล ช่วยป้องกันการแจกจ่ายไฟล์ต้นฉบับโดยบังเอิญ และทำให้การทำงานอัตโนมัติที่อิงการตั้งชื่อเป็นเรื่องง่ายขึ้น  

## ทำไมต้องใช้ GroupDocs.Redaction สำหรับงานนี้?

GroupDocs.Redaction มี API Java ที่มีประสิทธิภาพสูงรวมการกระทำลบข้อมูลกับตัวเลือกการจัดการไฟล์ที่ยืดหยุ่น เช่น การเพิ่มส่วนต่อท้ายอัตโนมัติ, การสนับสนุนสตรีม, และการประมวลผลเป็นชุด รองรับมากกว่า 50 ฟอร์แมตเข้าและออก และสามารถประมวลผลเอกสารหลายร้อยหน้าโดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ ทำให้ใช้หน่วยความจำน้อยและทำงานเร็ว  

## ข้อกำหนดเบื้องต้น

- **Java Development Kit (JDK):** เวอร์ชัน 8 หรือสูงกว่า  
- **GroupDocs.Redaction Library:** ไลบรารีหลักสำหรับงานลบข้อมูล  
- **IDE:** IntelliJ IDEA, Eclipse หรือเครื่องมือแก้ไขที่รองรับ Java ใดก็ได้  
- **Maven:** สำหรับการจัดการ dependencies  

### ความรู้ที่ต้องมี
ความคุ้นเคยกับ Java I/O และแนวคิดพื้นฐานของ OOP จะทำให้ตัวอย่างง่ายต่อการทำตาม  

## การตั้งค่า GroupDocs.Redaction สำหรับ Java

### การตั้งค่า Maven
ใส่การกำหนดค่าต่อไปนี้ในไฟล์ `pom.xml` ของคุณเพื่อเข้าถึงไลบรารี GroupDocs ผ่าน Maven:

```xml
<repositories>
   <repository>
      <id>repository.groupdocs.com</id>
      <name>GroupDocs Repository</name>
      <url>https://releases.groupdocs.com/redaction/java/</url>
   </repository>
</repositories>

<dependencies>
   <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-redaction</artifactId>
      <version>24.9</version>
   </dependency>
</dependencies>
```

### ดาวน์โหลดโดยตรง
คุณสามารถดาวน์โหลดเวอร์ชันล่าสุดโดยตรงจาก [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/)  

### การรับใบอนุญาต
1. **ทดลองใช้ฟรี:** เข้าถึงฟังก์ชันพื้นฐานโดยไม่มีข้อจำกัด  
2. **ใบอนุญาตชั่วคราว:** รับใบอนุญาตชั่วคราวเพื่อสำรวจฟีเจอร์ขั้นสูง  
3. **การซื้อ:** สำหรับการใช้งานระยะยาว พิจารณาซื้อใบอนุญาตเต็ม  

#### การเริ่มต้นและตั้งค่าเบื้องต้น
เพิ่ม import ที่จำเป็นเพื่อเริ่มโครงการของคุณ:

```java
import com.groupdocs.redaction.Redactor;
```

ด้วยการตั้งค่านี้ คุณพร้อมที่จะนำฟังก์ชันการลบข้อมูลเอกสารไปใช้  

## คู่มือการใช้งาน

### ฟีเจอร์ 1: โหลดเอกสารจากสตรีม
**ภาพรวม:** เรียนรู้วิธีโหลดเอกสารเข้าสู่ `InputStream` เพื่อประมวลผล  

`InputStream` เป็นคลาส Java I/O ที่แทนสตรีมของไบต์ ทำให้คุณสามารถอ่านข้อมูลจากไฟล์, การเชื่อมต่อเครือข่าย หรือแหล่งอื่น ๆ ได้โดยไม่ต้องโหลดเนื้อหาทั้งหมดเข้าสู่หน่วยความจำ  

#### ขั้นตอน 1.1: สร้าง inputstream

```java
import java.io.FileInputStream;
import java.io.InputStream;

try (InputStream stream = new FileInputStream("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    final Redactor redactor = new Redactor(stream);
    try {
        // Document is now loaded and ready for further processing
    } finally {
        redactor.close();
    }
}
```

- **ทำไม:** การใช้ `InputStream` ช่วยให้คุณจัดการเอกสารที่เก็บอยู่ในตำแหน่งต่าง ๆ — bucket ของคลาวด์, ฐานข้อมูล, หรือบัฟเฟอร์ในหน่วยความจำ — โดยไม่ต้องเขียนลงดิสก์ก่อน วิธีนี้สำคัญเมื่อคุณต้อง **load document from stream** ในสถาปัตยกรรมไมโครเซอร์วิส  

### ฟีเจอร์ 2: ใช้การลบ annotation redaction
**ภาพรวม:** ลบ annotation จากเอกสารของคุณด้วย `DeleteAnnotationRedaction`  

`DeleteAnnotationRedaction` เป็นการดำเนินการลบข้อมูลที่ลบ annotation ทั้งหมด เช่น คอมเมนต์, ไฮไลท์, และโน้ตจากเอกสาร  

#### ขั้นตอน 2.1: ใช้ deleteannotationredaction

```java
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply the DeleteAnnotationRedaction to remove annotations from the document
    redactor.apply(new DeleteAnnotationRedaction());
}
```

- **ทำไม:** ขั้นตอนนี้ทำให้แน่ใจว่า annotation ที่อาจมีข้อมูลสำคัญ (คอมเมนต์, ไฮไลท์ หรือโน้ตที่ซ่อนอยู่) ถูกลบออกจากเอกสาร เพิ่มความเป็นส่วนตัวและความสอดคล้องตามมาตรฐาน  

### ฟีเจอร์ 3: บันทึกเอกสารด้วยตัวเลือก
**ภาพรวม:** เรียนรู้วิธีบันทึกเอกสารที่ประมวลผลด้วยตัวเลือกเฉพาะ เช่น rasterization และ **add suffix filename java**  

`SaveOptions` รวมการตั้งค่าที่ควบคุมวิธีการเขียนเอกสารที่ลบข้อมูลแล้ว รวมถึงฟอร์แมต, rasterization, และการตั้งชื่อ  

#### ขั้นตอน 3.1: กำหนดค่า saveoptions

```java
import java.io.ByteArrayOutputStream;
import com.groupdocs.redaction.options.SaveOptions;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply necessary redactions before saving
    redactor.apply(new DeleteAnnotationRedaction());
    try (ByteArrayOutputStream bA = new ByteArrayOutputStream()) {
        SaveOptions options = new SaveOptions();
        options.setRasterizeToPDF(true);  // Option to rasterize document to PDF format
        options.setAddSuffix(true);      // Option to add a suffix to the saved file name
        redactor.save(bA, options.getRasterization());
    }
}
```

- **ทำไม:** การปรับแต่ง save options ทำให้คุณเลือกฟอร์แมตและการตั้งชื่อได้อย่างยืดหยุ่น การเปิด `setAddSuffix(true)` **adds suffix to filename** ทำให้ไฟล์ที่บันทึกชัดเจนว่าเป็นไฟล์ที่ลบข้อมูลแล้ว  

## วิธีเพิ่ม suffix filename java เมื่อบันทึกเอกสาร?

คลาส `Redactor` เป็นคอมโพเนนต์หลักที่โหลดเอกสารและใช้การลบข้อมูล `SaveOptions` กำหนดวิธีการบันทึกเอกสารที่ลบข้อมูล รวมถึงฟอร์แมต, rasterization, และการตั้งชื่อ สร้างอินสแตนซ์ `Redactor` แล้วใช้การลบข้อมูลที่ต้องการ จากนั้นกำหนดวัตถุ `SaveOptions` ด้วย `setAddSuffix(true)` เรียก `redactor.save(outputPath, options)` SDK จะเพิ่ม “_redacted” (หรือส่วนต่อท้ายที่กำหนด) ไปยังชื่อไฟล์โดยอัตโนมัติ ไม่ต้องเปลี่ยนชื่อไฟล์ด้วยตนเอง  

## ภาพรวมการพึ่งพา Maven ของ GroupDocs

**groupdocs maven dependency** นำ SDK Redaction ทั้งหมดเข้ามาในโครงการของคุณด้วยรายการ `<dependency>` เพียงรายการเดียว มันจัดการ dependencies ที่ตามมา, ทำให้ไลบรารีเป็นเวอร์ชันล่าสุด, และทำให้การอัตโนมัติการสร้างเป็นเรื่องง่าย โดยการประกาศ dependency ใน `pom.xml` คุณจะหลีกเลี่ยงการจัดการ JAR ด้วยตนเองและรับประกันความเข้ากันได้กับแพตช์ความปลอดภัยล่าสุด  

## ทำไมการเพิ่มส่วนต่อท้ายถึงสำคัญ

การเพิ่มส่วนต่อท้ายให้การยืนยันด้วยสายตาว่าไฟล์ได้ผ่านการประมวลผลแล้ว ซึ่งสำคัญต่อการตรวจสอบ, เวิร์กโฟลว์อัตโนมัติ, และการปฏิบัติตามกฎระเบียบ มันทำให้สคริปต์กรองไฟล์ที่ลบข้อมูลได้ง่าย ป้องกันการแจกจ่ายไฟล์ต้นฉบับโดยบังเอิญ และสอดคล้องกับมาตรฐานอุตสาหกรรมหลายแห่งที่ต้องการการติดป้ายชัดเจนบนเอกสารที่ทำความสะอาด  

## การประยุกต์ใช้ในทางปฏิบัติ

1. **การลบข้อมูลในเอกสารกฎหมาย:** ปกป้องสัญญาก่อนแชร์ให้ลูกค้า  
2. **การจัดการบันทึกการแพทย์:** ปกป้องข้อมูลผู้ป่วยขณะรักษาข้อมูลคลินิก  
3. **การรายงานทางการเงิน:** รักษาตัวเลขสำคัญให้เป็นความลับระหว่างการตรวจสอบภายนอก  
4. **การผสานรวม CRM:** ลบข้อมูลลูกค้าโดยอัตโนมัติก่อนส่งออกไปยังเครื่องมือของบุคคลที่สาม  
5. **เครื่องมือร่วมมือ:** ทำให้ร่างที่แชร์ไม่เปิดเผยคอมเมนต์หรือเมตาดาต้าที่ซ่อนอยู่  

## การพิจารณาด้านประสิทธิภาพ

### การเพิ่มประสิทธิภาพ
- ใช้การสตรีม (`load document from stream`) เพื่อหลีกเลี่ยงการโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ  
- ปิดอินสแตนซ์ `Redactor` ทันทีหลังใช้งานเพื่อคืนทรัพยากร  

### แนวทางการใช้ทรัพยากร
- ตรวจสอบการใช้ CPU และหน่วยความจำระหว่างการรันแบบแบตช์  
- แนะนำให้ใช้ `ByteArrayOutputStream` สำหรับการบันทึกในหน่วยความจำเมื่อไฟล์มีขนาดปานกลาง  

### แนวปฏิบัติที่ดีที่สุดสำหรับการจัดการหน่วยความจำใน Java
- ใช้ซ้ำออบเจกต์ `Redactor` เมื่อประมวลผลหลายไฟล์ประเภทเดียวกัน  
- เรียก `close()` ภายในบล็อก `try‑with‑resources` เพื่อป้องกันการรั่วไหล  

## ปัญหาทั่วไปและวิธีแก้

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|-------|-----|
| **Suffix not appearing** | `setAddSuffix(false)` หรือไม่ได้เรียก | ตรวจสอบให้แน่ใจว่า `options.setAddSuffix(true)` ถูกตั้งค่าก่อน `save()` |
| **OutOfMemoryError on large DOCX** | โหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ | เปลี่ยนไปใช้การโหลดด้วย `InputStream` (ดู Feature 1) |
| **Annotations still visible** | ไม่ได้ทำการลบข้อมูลก่อนบันทึก | เรียก `redactor.apply(new DeleteAnnotationRedaction())` ก่อน `save()` |
| **PDF rasterization not applied** | `setRasterizeToPDF(false)` หรือไม่ได้ตั้งค่า | ตั้งค่า `options.setRasterizeToPDF(true)` เมื่อจำเป็นต้องได้ PDF แบบแบน |

## คำถามที่พบบ่อย

**Q: ฉันสามารถลบข้อมูลในเอกสาร PDF ด้วย GroupDocs.Redaction ได้หรือไม่?**  
A: ได้, ไลบรารีรองรับ PDF, DOCX, PPTX, XLSX และฟอร์แมตอื่น ๆ อีกหลายรูปแบบ  

**Q: วิธีที่ดีที่สุดในการจัดการไฟล์ขนาดใหญ่กับ GroupDocs.Redaction คืออะไร?**  
A: ใช้การสตรีม (`load document from stream`) และปิดทรัพยากรโดยเร็วเพื่อรักษาการใช้หน่วยความจำให้ต่ำ  

**Q: สามารถกำหนดข้อความส่วนต่อท้ายเองได้หรือไม่?**  
A: API จะเพิ่มส่วนต่อท้ายเริ่มต้น (เช่น “_redacted”) ให้โดยอัตโนมัติ หากต้องการส่วนต่อท้ายแบบกำหนดเอง ให้เปลี่ยนชื่อไฟล์หลังจากบันทึก  

**Q: จะขอใบอนุญาตชั่วคราวสำหรับ GroupDocs.Redaction ได้อย่างไร?**  
A: เยี่ยมชมหน้า [Temporary License page](https://purchase.groupdocs.com/temporary-license/) แล้วทำตามขั้นตอนที่ระบุ  

**Q: จะหาความช่วยเหลือเมื่อเจอปัญหาได้จากที่ไหน?**  
A: เข้าร่วม [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) เพื่อรับคำแนะนำจากผู้เชี่ยวชาญ  

## แหล่งข้อมูล
- **Documentation:** สำรวจคู่มือโดยละเอียดที่ [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/)  
- **API reference:** ดูรายละเอียด API อย่างครบถ้วนบน [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java)  
- **Download:** ดาวน์โหลดเวอร์ชันล่าสุดจาก [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/)  
- **GitHub repository:** มีส่วนร่วมหรือสำรวจซอร์สโค้ดที่ [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  

**Last Updated:** 2026-11-02  
**Tested With:** GroupDocs.Redaction 24.9 for Java  
**Author:** GroupDocs  

## บทแนะนำที่เกี่ยวข้อง

- [Convert Word to PDF and Save Redacted Documents with GroupDocs.Redaction Java](/redaction/java/document-saving/)
- [Preview Document Pages Java Loading with GroupDocs.Redaction](/redaction/java/document-loading/)
- [Advanced Redaction Techniques for GroupDocs.Redaction Java](/redaction/java/advanced-redaction/)