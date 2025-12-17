---
date: '2025-12-17'
description: เรียนรู้วิธีเพิ่มส่วนต่อท้ายให้กับชื่อไฟล์และลบข้อมูลที่เป็นความลับออกจากเอกสารโดยใช้
  GroupDocs.Redaction สำหรับ Java. เพิ่มความปลอดภัยและความเป็นส่วนตัวของเอกสารอย่างมีประสิทธิภาพ.
keywords:
- document redaction Java
- GroupDocs.Redaction tutorial
- secure document handling
title: วิธีเพิ่มส่วนต่อท้ายให้ชื่อไฟล์ขณะทำการลบข้อมูลในเอกสารด้วย Java และ GroupDocs.Redaction
type: docs
url: /th/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

# วิธีเพิ่มส่วนต่อท้ายชื่อไฟล์ขณะทำการลบข้อมูลในเอกสารด้วย Java และ GroupDocs.Redaction

การลบข้อมูลที่เป็นความลับเป็นเพียงครึ่งหนึ่งของการต่อสู้—คุณยังต้องแน่ใจว่าไฟล์ที่บันทึกแล้วแสดงอย่างชัดเจนว่าถูกประมวลผลแล้ว ในคู่มือนี้คุณจะได้เรียนรู้ **วิธีเพิ่มส่วนต่อท้ายชื่อไฟล์** เมื่อบันทึกเอกสารที่ลบข้อมูลแล้ว พร้อมกับการโหลด, การทำ annotation, และการบันทึกโดยใช้ GroupDocs.Redaction สำหรับ Java ไม่ว่าคุณจะกำลังปกป้องสัญญากฎหมาย, บันทึกทางการแพทย์, หรือรายงานทางการเงิน ขั้นตอนเหล่านี้จะทำให้กระบวนการทำงานของคุณปลอดภัยและตรวจสอบได้

## คำตอบด่วน
- **การเพิ่มส่วนต่อท้ายชื่อไฟล์ทำอะไร?**  
  มันจะต่อส่วนต่อท้ายที่กำหนดเอง (เช่น “_redacted”) ไปที่ชื่อไฟล์ผลลัพธ์เพื่อให้คุณสามารถระบุไฟล์ที่ผ่านการประมวลผลได้ทันที  
- **ฉันสามารถโหลดเอกสารจากสตรีมได้หรือไม่?**  
  ได้—GroupDocs.Redaction รองรับการโหลดจาก `InputStream` ใด ๆ เหมาะสำหรับการจัดเก็บบนคลาวด์หรือการประมวลผลในหน่วยความจำ  
- **ฉันต้องมีใบอนุญาตสำหรับฟีเจอร์นี้หรือไม่?**  
  การทดลองใช้ฟรีทำงานสำหรับการลบข้อมูลพื้นฐาน; ใบอนุญาตชั่วคราวหรือเต็มจะเปิดใช้งานตัวเลือกขั้นสูงทั้งหมด รวมถึงการจัดการส่วนต่อท้าย  
- **ฟอร์แมตใดบ้างที่รองรับ?**  
  ไลบรารีรองรับ DOCX, PDF, PPTX, XLSX และอื่น ๆ อีกมาก  
- **ต้องทำ rasterization สำหรับ PDF หรือไม่?**  
  Rasterization เป็นทางเลือก; เปิดใช้งานเมื่อคุณต้องการทำให้เอกสารแบนเพื่อความปลอดภัยเพิ่มเติม  

## การเพิ่มส่วนต่อท้ายชื่อไฟล์คืออะไร?
การต่อส่วนต่อท้ายเป็นแนวทางการตั้งชื่อที่ง่ายซึ่งบ่งบอกว่าไฟล์ได้ผ่านการลบข้อมูลแล้ว มันช่วยป้องกันการแชร์ไฟล์ต้นฉบับที่ยังไม่ได้ลบข้อมูลโดยบังเอิญและช่วยให้ pipeline อัตโนมัติดตามสถานะการประมวลผลได้

## ทำไมต้องใช้ GroupDocs.Redaction สำหรับงานนี้?
GroupDocs.Redaction ให้ API ของ Java ที่เป็น fluent ซึ่งทำให้คุณสามารถรวมการลบข้อมูลกับตัวเลือกการจัดการไฟล์—เช่น **การเพิ่มส่วนต่อท้ายชื่อไฟล์**—ได้ในเพียงไม่กี่บรรทัดของโค้ด สิ่งนี้ช่วยประหยัดเวลาในการพัฒนาและลดความเสี่ยงจากข้อผิดพลาดของมนุษย์

## ข้อกำหนดเบื้องต้น

- **Java Development Kit (JDK):** เวอร์ชัน 8 หรือสูงกว่า  
- **GroupDocs.Redaction Library:** ไลบรารีหลักสำหรับงานลบข้อมูล  
- **IDE:** IntelliJ IDEA, Eclipse หรือเครื่องมือแก้ไขที่รองรับ Java ใ ๆ  
- **Maven:** สำหรับการจัดการ dependencies  

### ความรู้เบื้องต้นที่ต้องมี
ความคุ้นเคยกับ Java I/O และแนวคิดเชิงวัตถุพื้นฐานจะทำให้ตัวอย่างง่ายต่อการทำตาม

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
หรือคุณสามารถดาวน์โหลดเวอร์ชันล่าสุดโดยตรงจาก [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### การรับใบอนุญาต
1. **Free Trial:** เข้าถึงฟังก์ชันพื้นฐานโดยไม่มีข้อจำกัด.  
2. **Temporary License:** รับใบอนุญาตชั่วคราวเพื่อสำรวจฟีเจอร์ขั้นสูง.  
3. **Purchase:** สำหรับการใช้งานระยะยาว พิจารณาซื้อใบอนุญาตเต็ม.

#### การเริ่มต้นและตั้งค่าพื้นฐาน
เริ่มต้นโปรเจคของคุณโดยเพิ่มการนำเข้า (import) ที่จำเป็น:

```java
import com.groupdocs.redaction.Redactor;
```

ด้วยการตั้งค่านี้ คุณพร้อมที่จะดำเนินการฟังก์ชันการลบข้อมูลในเอกสารแล้ว

## คู่มือการทำงาน

### ฟีเจอร์ 1: โหลดเอกสารจากสตรีม
**ภาพรวม:** เรียนรู้วิธีโหลดเอกสารเข้าสู่ `InputStream` เพื่อการประมวลผล.

#### การดำเนินการตามขั้นตอน
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

- **ทำไม:** การใช้ `InputStream` ช่วยให้คุณจัดการเอกสารที่เก็บในรูปแบบต่าง ๆ ได้อย่างราบรื่น ซึ่งจำเป็นเมื่อคุณต้อง **load document from stream** ในสภาพแวดล้อมคลาวด์หรือไมโครเซอร์วิส

### ฟีเจอร์ 2: ใช้การลบ Annotation Redaction
**ภาพรวม:** ลบ annotation จากเอกสารของคุณโดยใช้ `DeleteAnnotationRedaction`.

#### การดำเนินการตามขั้นตอน
##### ขั้นตอน 2.1: ใช้ DeleteAnnotationRedaction

```java
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply the DeleteAnnotationRedaction to remove annotations from the document
    redactor.apply(new DeleteAnnotationRedaction());
}
```

- **ทำไม:** ขั้นตอนนี้ทำให้แน่ใจว่า annotation ที่เป็นข้อมูลสำคัญทั้งหมดถูกลบออก เพิ่มความเป็นส่วนตัวของเอกสาร

### ฟีเจอร์ 3: บันทึกเอกสารพร้อมตัวเลือก
**ภาพรวม:** เรียนรู้วิธีบันทึกเอกสารที่ผ่านการประมวลผลพร้อมตัวเลือกเฉพาะ เช่น rasterization และ **การเพิ่มส่วนต่อท้ายชื่อไฟล์**.

#### การดำเนินการตามขั้นตอน
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

- **ทำไม:** การปรับแต่งตัวเลือกการบันทึกทำให้คุณสามารถกำหนดรูปแบบผลลัพธ์และรูปแบบการตั้งชื่อได้อย่างยืดหยุ่น การเปิดใช้งาน `setAddSuffix(true)` **adds suffix to filename** ทำให้ไฟล์ชัดเจนว่าถูกลบข้อมูลแล้ว

## ทำไมการเพิ่มส่วนต่อท้ายจึงสำคัญ
- **การตรวจสอบ:** ทีมงานสามารถระบุไฟล์ที่ปลอดภัยต่อการแจกจ่ายได้ทันที  
- **การอัตโนมัติ:** สคริปต์สามารถกรองไฟล์ตามส่วนต่อท้าย ป้องกันการประมวลผลไฟล์ต้นฉบับโดยบังเอิญ  
- **การปฏิบัติตามกฎระเบียบ:** กฎระเบียบหลายฉบับต้องการการติดฉลากที่ชัดเจนสำหรับเอกสารที่ทำความสะอาดแล้ว  

## การประยุกต์ใช้ในทางปฏิบัติ
สำรวจกรณีการใช้งานจริงต่อไปนี้:
1. **การลบข้อมูลในเอกสารทางกฎหมาย:** ปกป้องสัญญาก่อนแชร์ให้ลูกค้า.  
. **การจัดการบันทึกทางการแพทย์:** ปกป้องตัวระบุผู้ป่วย.  
3. **การรายงานทางการเงิน:** รักษาตัวเลขสำคัญให้เป็นความลับ.  
4. **การรวมกับ CRM:** ลบข้อมูลลูกค้าโดยอัตโนมัติก่อนส่งออก.  
5. **เครื่องมือการทำงานร่วมกัน:** ทำให้แน่ใจว่าร่างที่แชร์ไม่เปิดเผยคอมเมนต์ที่ซ่อนอยู่.  

## พิจารณาด้านประสิทธิภาพ
### การเพิ่มประสิทธิภาพ
- ใช้การสตรีม (`load document from stream`) เพื่อหลีกเลี่ยงการโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ.  
- ปิดอินสแตนซ์ `Redactor` อย่างรวดเร็วเพื่อปลดปล่อยทรัพยากร  

### แนวทางการใช้ทรัพยากร
- ตรวจสอบการใช้ CPU และหน่วยความจำระหว่างการรันแบบแบตช์.  
- แนะนำให้ใช้ `ByteArrayOutputStream` สำหรับการบันทึกในหน่วยความจำเมื่อทำงานกับไฟล์ขนาดปานกลาง.  

### แนวทางปฏิบัติที่ดีที่สุดสำหรับการจัดการหน่วยความจำใน Java
- ใช้วัตถุ `Redactor` ซ้ำเมื่อประมวลผลหลายไฟล์ที่เป็นประเภทเดียวกัน.  
- เรียก `close()` ในบล็อก `finally` หรือใช้ try‑with‑resources เพื่อป้องกันการรั่วไหล.  

## ปัญหาทั่วไปและวิธีแก้
| Issue | Cause | Fix |
|-------|-------|-----|
| **ส่วนต่อท้ายไม่แสดง** | `setAddSuffix(false)` หรือการเรียกที่หายไป | ตรวจสอบให้แน่ใจว่าได้ตั้งค่า `options.setAddSuffix(true)` ก่อนเรียก `save()` |
| **OutOfMemoryError กับ DOCX ขนาดใหญ่** | โหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ | เปลี่ยนเป็นการโหลดด้วย `InputStream` (ดูฟีเจอร์ 1) |
| **Annotations ยังมองเห็นได้** | ไม่ได้ทำการลบข้อมูลก่อนบันทึก | เรียก `redactor.apply(new DeleteAnnotationRedaction())` ก่อน `save()` |
| **PDF rasterization ไม่ทำงาน** | `setRasterizeToPDF(false)` หรือไม่ได้ตั้งค่า | ตั้งค่า `options.setRasterizeToPDF(true)` เมื่อคุณต้องการ PDF ที่แบน |

## คำถามที่พบบ่อย

**Q: Can I redact PDF documents using GroupDocs.Redaction?**  
A: Yes, the library supports PDFs, DOCX, PPTX, XLSX, and many other formats.  

**Q: What is the best way to handle large files with GroupDocs.Redaction?**  
A: Use streaming (`load document from stream`) and close resources promptly to keep memory usage low.  

**Q: Is it possible to customize the suffix text?**  
A: The API automatically adds a default suffix (e.g., “_redacted”). For custom suffixes, you can rename the output file after saving.  

**Q: How do I obtain a temporary license for GroupDocs.Redaction?**  
A: Visit the [Temporary License page](https://purchase.groupdocs.com/temporary-license/) and follow the instructions.  

**Q: Where can I get help if I encounter issues?**  
A: Join the [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) for expert assistance.  

## แหล่งข้อมูล
- **Documentation:** สำรวจคู่มือโดยละเอียดที่ [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/).  
- **API Reference:** เข้าถึงรายละเอียด API อย่างครบถ้วนที่ [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java).  
- **Download:** ดาวน์โหลดเวอร์ชันล่าสุดจาก [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/).  
- **GitHub Repository:** มีส่วนร่วมหรือสำรวจซอร์สโค้ดที่ [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).  

---

**Last Updated:** 2025-12-17  
**Tested With:** GroupDocs.Redaction 24.9 for Java  
**Author:** GroupDocs