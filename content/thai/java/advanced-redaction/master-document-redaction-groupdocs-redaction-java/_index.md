---
date: '2026-02-16'
description: เรียนรู้วิธีใช้การพึ่งพา GroupDocs Maven เพื่อเพิ่มส่วนต่อท้ายให้กับชื่อไฟล์ขณะทำการลบข้อมูลในเอกสารด้วย
  Java รวมถึงการโหลดจากสตรีม การลบคำอธิบาย และตัวเลือกการบันทึก.
keywords:
- document redaction Java
- GroupDocs.Redaction tutorial
- secure document handling
title: การพึ่งพา Maven ของ GroupDocs – เพิ่มส่วนต่อท้ายให้ชื่อไฟล์ใน Java
type: docs
url: /th/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

 answer.# วิธีเพิ่มส่วนต่อท้ายให้กับชื่อไฟล์ขณะทำการลบข้อมูลในเอกสารด้วย Java และ GroupDocs.Redaction

การลบข้อมูลที่เป็นความลับเป็นเพียงครึ่งหนึ่งของการปกป้อง—คุณยังต้องทำให้ไฟล์ที่บันทึกไว้แสดงอย่างชัดเจนว่าถูกประมวลผลแล้ว **การใช้ dependency ของ groupdocs ใน Maven ทำให้เรื่องนี้ง่ายขึ้นมาก** เพียงไม่กี่บรรทัดของโค้ดคุณก็สามารถเพิ่มส่วนต่อท้ายให้กับชื่อไฟล์ผลลัพธ์ได้ ในคู่มือนี้คุณจะได้เรียนรู้วิธีเพิ่มส่วนต่อท้ายให้กับชื่อไฟล์เมื่อบันทึกเอกสารที่ถูกลบข้อมูล พร้อมกับการโหลด, การทำ annotation, และการบันทึกโดยใช้ GroupDocs.Redaction สำหรับ Java ไม่ว่าคุณจะกำลังปกป้องสัญญากฎหมาย, บันทึกทางการแพทย์, หรือรายงานการเงิน ขั้นตอนเหล่านี้จะช่วยให้กระบวนการทำงานของคุณปลอดภัยและตรวจสอบได้

## คำตอบสั้น
- **“เพิ่มส่วนต่อท้ายให้กับชื่อไฟล์” ทำอะไร?**  
  จะต่อส่วนต่อท้ายที่กำหนดเอง (เช่น “_redacted”) ไปที่ชื่อไฟล์ผลลัพธ์ เพื่อให้คุณสามารถระบุไฟล์ที่ผ่านการประมวลผลได้ทันที  
- **ฉันสามารถโหลดเอกสารจากสตรีมได้หรือไม่?**  
  ได้—GroupDocs.Redaction รองรับการโหลดจาก `InputStream` ใด ๆ เหมาะสำหรับการจัดเก็บบนคลาวด์หรือการประมวลผลในหน่วยความจำ  
- **ต้องมีลิขสิทธิ์สำหรับฟีเจอร์นี้หรือไม่?**  
  การทดลองใช้ฟรีทำงานสำหรับการลบข้อมูลพื้นฐาน; ลิขสิทธิ์ชั่วคราวหรือเต็มจะเปิดใช้งานตัวเลือกขั้นสูงทั้งหมดรวมถึงการจัดการส่วนต่อท้าย  
- **รองรับรูปแบบไฟล์ใดบ้าง?**  
  ไลบรารีรองรับ DOCX, PDF, PPTX, XLSX และอื่น ๆ อีกมาก  
- **ต้องทำ rasterization สำหรับผลลัพธ์ PDF หรือไม่?**  
  rasterization เป็นตัวเลือก; เปิดใช้งานเมื่อคุณต้องการแปลงเอกสารให้เป็นภาพเพื่อความปลอดภัยเพิ่มขึ้น

## การเพิ่มส่วนต่อท้ายให้กับชื่อไฟล์คืออะไร?
การต่อส่วนต่อท้ายเป็นแนวปฏิบัติการตั้งชื่ออย่างง่ายที่บ่งบอกว่าไฟล์ได้ผ่านการลบข้อมูลแล้ว ช่วยป้องกันการแชร์ไฟล์ต้นฉบับที่ยังไม่ได้ลบข้อมูลโดยบังเอิญและช่วยให้ pipeline อัตโนมัติดึงสถานะการประมวลผลได้ง่ายขึ้น

## ทำไมต้องใช้ GroupDocs.Redaction สำหรับงานนี้?
GroupDocs.Redaction มี API Java ที่เป็น fluent ทำให้คุณสามารถผสานการลบข้อมูลกับตัวเลือกการจัดการไฟล์—เช่น **การเพิ่มส่วนต่อท้ายให้กับชื่อไฟล์**—ได้ในไม่กี่บรรทัดของโค้ด สิ่งนี้ช่วยลดเวลาในการพัฒนาและลดความเสี่ยงจากข้อผิดพลาดที่ทำด้วยมือ

## ข้อกำหนดเบื้องต้น

- **Java Development Kit (JDK):** เวอร์ชัน 8 หรือสูงกว่า  
- **GroupDocs.Redaction Library:** ไลบรารีหลักสำหรับงานลบข้อมูล  
- **IDE:** IntelliJ IDEA, Eclipse หรือเครื่องมือแก้ไข Java ใดก็ได้  
- **Maven:** สำหรับการจัดการ dependency  

### ความรู้เบื้องต้นที่ต้องมี
ความคุ้นเคยกับ Java I/O และแนวคิดพื้นฐานของ OOP จะทำให้ตัวอย่างต่าง ๆ เข้าใจได้ง่ายขึ้น

## การตั้งค่า GroupDocs.Redaction สำหรับ Java
### การตั้งค่า Maven
เพิ่มการกำหนดค่าต่อไปนี้ในไฟล์ `pom.xml` ของคุณเพื่อเข้าถึงไลบรารีของ GroupDocs ผ่าน Maven:

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
หรือคุณสามารถดาวน์โหลดเวอร์ชันล่าสุดได้โดยตรงจาก [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/)  

### การรับลิขสิทธิ์
1. **Free Trial:** เข้าถึงฟังก์ชันพื้นฐานโดยไม่มีข้อจำกัด  
2. **Temporary License:** รับลิขสิทธิ์ชั่วคราวเพื่อสำรวจฟีเจอร์ขั้นสูง  
3. **Purchase:** สำหรับการใช้งานระยะยาว ควรพิจารณาซื้อลิขสิทธิ์เต็มรูปแบบ  

#### การเริ่มต้นและการตั้งค่าพื้นฐาน
เพิ่ม import ที่จำเป็นลงในโปรเจกต์ของคุณ:

```java
import com.groupdocs.redaction.Redactor;
```

เมื่อทำการตั้งค่าเสร็จแล้ว คุณก็พร้อมที่จะเริ่มใช้งานฟังก์ชันการลบข้อมูลในเอกสารแล้ว

## คู่มือการทำงาน

### ฟีเจอร์ 1: โหลดเอกสารจากสตรีม
**ภาพรวม:** เรียนรู้วิธีโหลดเอกสารเข้าสู่ `InputStream` เพื่อทำการประมวลผล  

#### ขั้นตอนการทำงานแบบละเอียด
##### ขั้นตอน 1.1: สร้าง InputStream

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

- **ทำไม:** การใช้ `InputStream` ช่วยให้คุณจัดการเอกสารที่เก็บในรูปแบบต่าง ๆ ได้อย่างราบรื่น ซึ่งจำเป็นเมื่อคุณต้อง **โหลดเอกสารจากสตรีม** ในสภาพแวดล้อมคลาวด์หรือ micro‑service  

### ฟีเจอร์ 2: ลบ Annotation ด้วย Redaction
**ภาพรวม:** ลบ annotation จากเอกสารของคุณด้วย `DeleteAnnotationRedaction`  

#### ขั้นตอนการทำงานแบบละเอียด
##### ขั้นตอน 2.1: ใช้ DeleteAnnotationRedaction

```java
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply the DeleteAnnotationRedaction to remove annotations from the document
    redactor.apply(new DeleteAnnotationRedaction());
}
```

- **ทำไม:** ขั้นตอนนี้ทำให้แน่ใจว่า annotation ที่อาจมีข้อมูลสำคัญถูกลบออกไป เพิ่มความเป็นส่วนตัวของเอกสาร  

### ฟีเจอร์ 3: บันทึกเอกสารพร้อมตัวเลือก
**ภาพรวม:** เรียนรู้วิธีบันทึกเอกสารที่ผ่านการประมวลผลด้วยตัวเลือกต่าง ๆ เช่น rasterization และ **การเพิ่มส่วนต่อท้ายให้กับชื่อไฟล์**  

#### ขั้นตอนการทำงานแบบละเอียด
##### ขั้นตอน 3.1: กำหนดค่า SaveOptions

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

- **ทำไม:** การปรับแต่งตัวเลือกการบันทึกทำให้คุณเลือกรูปแบบผลลัพธ์และแนวปฏิบัติการตั้งชื่อได้อย่างยืดหยุ่น การเปิด `setAddSuffix(true)` **จะเพิ่มส่วนต่อท้ายให้กับชื่อไฟล์** ทำให้เห็นชัดว่าไฟล์นั้นถูกลบข้อมูลแล้ว  

## ภาพรวมของ groupdocs maven dependency
**groupdocs maven dependency** นำ Redaction SDK ทั้งหมดเข้ามาในโปรเจกต์ของคุณด้วยรายการ `<dependency>` เพียงรายการเดียว มันจัดการ dependency ที่เป็น transitive, ทำให้ไลบรารีเป็นเวอร์ชันล่าสุดเสมอ และทำให้การอัตโนมัติของการสร้างโปรเจกต์ง่ายขึ้น โดยการประกาศ dependency ใน `pom.xml` คุณจะไม่ต้องจัดการ JAR ด้วยตนเองและมั่นใจได้ว่าเข้ากันได้กับแพตช์ความปลอดภัยล่าสุด

## ทำไมการเพิ่มส่วนต่อท้ายจึงสำคัญ
- **Auditability:** ทีมงานสามารถมองเห็นไฟล์ที่ปลอดภัยต่อการแจกจ่ายได้ทันที  
- **Automation:** สคริปต์สามารถกรองไฟล์ตามส่วนต่อท้าย ป้องกันการประมวลผลไฟล์ต้นฉบับโดยบังเอิญ  
- **Compliance:** กฎระเบียบหลายฉบับกำหนดให้ต้องมีการระบุชัดเจนว่าเอกสารถูกทำความสะอาดแล้ว  

## การประยุกต์ใช้ในเชิงปฏิบัติ
สำรวจกรณีการใช้งานจริงต่อไปนี้:
1. **Legal Document Redaction:** ปกป้องสัญญาก่อนส่งให้ลูกค้า  
2. **Medical Record Handling:** ปกป้องข้อมูลระบุตัวผู้ป่วย  
3. **Financial Reporting:** รักษาความลับของตัวเลขสำคัญ  
4. **CRM Integration:** ลบข้อมูลลูกค้าอัตโนมัติก่อนส่งออก  
5. **Collaboration Tools:** ทำให้ร่างที่แชร์ไม่เปิดเผยคอมเมนต์ที่ซ่อนอยู่  

## การพิจารณาประสิทธิภาพ
### การเพิ่มประสิทธิภาพ
- ใช้การสตรีม (`load document from stream`) เพื่อลดการโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ  
- ปิดอินสแตนซ์ `Redactor` อย่างทันท่วงทีเพื่อคืนทรัพยากร  

### แนวทางการใช้ทรัพยากร
- ตรวจสอบการใช้ CPU และหน่วยความจำระหว่างการทำงานแบบ batch  
- แนะนำให้ใช้ `ByteArrayOutputStream` สำหรับการบันทึกในหน่วยความจำเมื่อไฟล์มีขนาดปานกลาง  

### แนวทางปฏิบัติที่ดีที่สุดสำหรับการจัดการหน่วยความจำใน Java
- ใช้ `Redactor` ซ้ำเมื่อประมวลผลหลายไฟล์ที่เป็นประเภทเดียวกัน  
- เรียก `close()` ภายในบล็อก `try‑with‑resources` เพื่อป้องกันการรั่วไหล  

## ปัญหาที่พบบ่อยและวิธีแก้
| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|--------|--------|
| **ส่วนต่อท้ายไม่แสดง** | `setAddSuffix(false)` หรือไม่ได้เรียก | ตรวจสอบให้แน่ใจว่าได้ตั้ง `options.setAddSuffix(true)` ก่อนเรียก `save()` |
| **OutOfMemoryError กับ DOCX ขนาดใหญ่** | โหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ | เปลี่ยนเป็นการโหลดด้วย `InputStream` (ดูฟีเจอร์ 1) |
| **Annotations ยังคงปรากฏ** | Redaction ไม่ได้ทำก่อนบันทึก | เรียก `redactor.apply(new DeleteAnnotationRedaction())` ก่อน `save()` |
| **PDF rasterization ไม่ทำงาน** | `setRasterizeToPDF(false)` หรือไม่ได้ตั้งค่า | ตั้ง `options.setRasterizeToPDF(true)` เมื่อจำเป็นต้องได้ PDF ที่แบนลงเป็นภาพ |

## คำถามที่พบบ่อย

**Q: สามารถลบข้อมูลในไฟล์ PDF ด้วย GroupDocs.Redaction ได้หรือไม่?**  
A: ได้, ไลบรารีรองรับ PDF, DOCX, PPTX, XLSX และรูปแบบอื่น ๆ อีกหลายประเภท  

**Q: วิธีที่ดีที่สุดในการจัดการไฟล์ขนาดใหญ่กับ GroupDocs.Redaction คืออะไร?**  
A: ใช้การสตรีม (`load document from stream`) และปิดทรัพยากรโดยเร็วเพื่อให้การใช้หน่วยความจำน้อยที่สุด  

**Q: สามารถกำหนดข้อความส่วนต่อท้ายเองได้หรือไม่?**  
A: API จะเพิ่มส่วนต่อท้ายเริ่มต้น (เช่น “_redacted”) ให้โดยอัตโนมัติ หากต้องการส่วนต่อท้ายแบบกำหนดเอง คุณสามารถเปลี่ยนชื่อไฟล์ผลลัพธ์หลังจากบันทึกได้  

**Q: จะขอรับลิขสิทธิ์ชั่วคราวสำหรับ GroupDocs.Redaction ได้อย่างไร?**  
A: เยี่ยมชมหน้า [Temporary License page](https://purchase.groupdocs.com/temporary-license/) แล้วทำตามขั้นตอนที่ระบุ  

**Q: หากพบปัญหา จะขอรับความช่วยเหลือได้จากที่ไหน?**  
A: เข้าร่วม [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) เพื่อรับคำแนะนำจากผู้เชี่ยวชาญ  

## แหล่งข้อมูล
- **Documentation:** ค้นหาคู่มือโดยละเอียดได้ที่ [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/)  
- **API Reference:** ดูรายละเอียด API อย่างครบถ้วนที่ [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java)  
- **Download:** ดาวน์โหลดเวอร์ชันล่าสุดจาก [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/)  
- **GitHub Repository:** มีส่วนร่วมหรือสำรวจซอร์สโค้ดได้ที่ [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  

---

**อัปเดตล่าสุด:** 2026-02-16  
**ทดสอบกับ:** GroupDocs.Redaction 24.9 for Java  
**ผู้เขียน:** GroupDocs