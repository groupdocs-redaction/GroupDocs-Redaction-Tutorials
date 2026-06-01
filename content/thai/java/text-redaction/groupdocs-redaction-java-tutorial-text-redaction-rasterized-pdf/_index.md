---
date: '2026-02-26'
description: เรียนรู้วิธีการลบข้อความโดยใช้ GroupDocs.Redaction Java และบันทึกเป็น
  PDF แบบเรสเตอร์ไลซ์พร้อมการแทนที่วลีที่แม่นยำและการตั้งค่า PDF แบบกำหนดเอง
keywords:
- GroupDocs.Redaction Java
- text redaction Java
- rasterized PDF conversion
title: วิธีลบข้อมูลข้อความด้วย GroupDocs.Redaction Java
type: docs
url: /th/java/text-redaction/groupdocs-redaction-java-tutorial-text-redaction-rasterized-pdf/
weight: 1
---

, fine.

Now produce final content.

# วิธีลบข้อความด้วย GroupDocs.Redaction Java

ในโลกที่ขับเคลื่อนด้วยข้อมูลในปัจจุบัน **วิธีลบข้อความ** ในเอกสารอย่างปลอดภัยและมีประสิทธิภาพเป็นความกังวลหลักของนักพัฒนาและเจ้าหน้าที่ด้านการปฏิบัติตามกฎระเบียบ ไม่ว่าคุณจะต้องซ่อนข้อมูลส่วนบุคคล รายละเอียดลูกค้าที่เป็นความลับ หรือรหัสโครงการภายใน GroupDocs.Redaction สำหรับ Java จะมอบวิธีที่เชื่อถือได้ในการค้นหาวลีที่ตรงกันและแทนที่ด้วยการซ้อนทับที่ปลอดภัย บทเรียนนี้ยังแสดงให้คุณเห็น **วิธีบันทึกเป็น PDF ที่แรสเตอร์ไลซ์** โดยเปลี่ยนแต่ละหน้าเป็น PDF แบบภาพที่สอดคล้องกับมาตรฐานการเก็บรักษาเอกสาร

## คำตอบสั้น
- **คลาสหลักสำหรับการลบข้อมูลคืออะไร?** `Redactor`  
- **ฉันสามารถแทนที่วลีด้วยการซ้อนทับสีได้หรือไม่?** ได้ โดยใช้ `ExactPhraseRedaction` และ `ReplacementOptions`  
- **ฉันจะสร้าง PDF ที่แรสเตอร์ไลซ์ได้อย่างไร?** เปิดการแรสเตอร์ไลซ์ผ่าน `SaveOptions.getRasterization().setEnabled(true)`  
- **ระดับการปฏิบัติตามมาตรฐาน PDF ที่ใช้ในตัวอย่างคืออะไร?** `PdfComplianceLevel.PdfA1a`  
- **ฉันต้องมีใบอนุญาตสำหรับการใช้งานในผลิตภัณฑ์หรือไม่?** จำเป็นต้องมีใบอนุญาต GroupDocs.Redaction ที่ถูกต้องสำหรับการใช้งานในสภาพแวดล้อมการผลิต

## “how to redact text” คืออะไรใน Java?
การลบข้อมูล (Redaction) คือกระบวนการลบหรือทำให้ข้อมูลที่ละเอียดอ่อนจากไฟล์เป็นแบบถาวร ด้วย GroupDocs.Redaction คุณสามารถค้นหาวลีที่ตรงกัน—เช่น ชื่อหรือรหัส—และแทนที่ด้วยการซ้อนทับสีแดง กล่องสีดำ หรือองค์ประกอบภาพที่กำหนดเอง เพื่อให้ข้อมูลต้นฉบับไม่สามารถกู้คืนได้

## ทำไมต้องใช้ GroupDocs.Redaction สำหรับ Java?
- **การจับคู่วลีที่ตรงกัน** ช่วยลดผลบวกเท็จ  
- **การแรสเตอร์ไลซ์ในตัว** ทำให้คุณสร้าง PDF/A‑compatible ที่เป็นภาพเท่านั้นสำหรับการเก็บรักษาระยะยาว  
- **การสนับสนุนหลายรูปแบบ** ทำงานกับ DOCX, PDF, PPTX และอื่น ๆ ทำให้คุณใช้โค้ดเดียวกันกับประเภทเอกสารต่าง ๆ  
- **API ที่เน้นประสิทธิภาพ** ช่วยประมวลผลชุดเอกสารขนาดใหญ่พร้อมการใช้หน่วยความจำน้อย

## ข้อกำหนดเบื้องต้น
ก่อนเริ่มทำงาน ให้ตรวจสอบว่าคุณมีสิ่งต่อไปนี้:

- **GroupDocs.Redaction สำหรับ Java** (เวอร์ชัน 24.9 หรือใหม่กว่า)  
- **Java Development Kit (JDK) 8+**  
- IDE เช่น IntelliJ IDEA, Eclipse หรือ NetBeans  
- Maven สำหรับการจัดการ dependencies  

### ไลบรารีและการพึ่งพาที่จำเป็น
- **GroupDocs.Redaction สำหรับ Java** – เพิ่ม repository และ dependency ลงใน `pom.xml` ของคุณ (ดูโค้ดบล็อกด้านล่าง)  
- **Optional**: ไลบรารี logging ใด ๆ ที่คุณต้องการ  

### ความรู้ที่ต้องมีล่วงหน้า
- ไวยากรณ์พื้นฐานของ Java และการทำงานกับไฟล์ I/O  
- ความคุ้นเคยกับโครงสร้างของ `pom.xml` ของ Maven  

## การตั้งค่า GroupDocs.Redaction สำหรับ Java
### การตั้งค่า Maven
เพิ่ม repository และ dependency ลงในไฟล์ `pom.xml` ของคุณ:

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
หรือคุณสามารถดาวน์โหลดเวอร์ชันล่าสุดโดยตรงจาก [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/)  

### การรับใบอนุญาต
- **Free Trial** – ทดลองใช้ API โดยไม่ต้องมีคีย์ใบอนุญาต  
- **Temporary License** – ใช้สำหรับการประเมินผลระยะยาว  
- **Full License** – จำเป็นสำหรับสภาพแวดล้อมการผลิต  

### การเริ่มต้นและการตั้งค่าพื้นฐาน
โค้ดต่อไปนี้เป็นตัวอย่างขั้นต่ำสำหรับสร้างอินสแตนซ์ `Redactor` ที่ชี้ไปยังไฟล์ DOCX ตัวอย่าง:

```java
import com.groupdocs.redaction.Redactor;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
```

## วิธีลบข้อความ – ตัวอย่างวลีที่ตรงกัน
### ขั้นตอนที่ 1: นำเข้าคลาสที่จำเป็น
การนำเข้าต่อไปนี้ทำให้คุณเข้าถึงเอนจินการลบข้อมูลและตัวเลือกการแทนที่:

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.ReplacementOptions;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
```

### ขั้นตอนที่ 2: สร้างและใช้การลบข้อมูล
โค้ดส่วนนี้ค้นหาวลี **“John Doe”** และแทนที่ด้วยการซ้อนทับสีแดง:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
try {
    RedactorChangeLog result = redactor.apply(new ExactPhraseRedaction(
        "John Doe", new ReplacementOptions(java.awt.Color.RED)));
    
    if (result.getStatus() != RedactionStatus.Failed) {
        // Successfully redacted the text
    }
} finally { 
    redactor.close(); 
}
```

**ทำไมเรื่องนี้สำคัญ:** `ReplacementOptions` ให้คุณควบคุมสไตล์การแสดงผลของการลบข้อมูล เพื่อให้เนื้อหาที่ซ่อนไม่สามารถกู้คืนได้โดยการคัดลอก‑วางหรือ OCR  

## วิธีบันทึกเป็น PDF ที่แรสเตอร์ไลซ์
### ขั้นตอนที่ 1: นำเข้าคลาส SaveOptions
คลาสเหล่านี้ช่วยให้คุณกำหนดค่าการส่งออก PDF รวมถึงการแรสเตอร์ไลซ์และระดับการปฏิบัติตามมาตรฐาน:

```java
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.options.PdfComplianceLevel;
```

### ขั้นตอนที่ 2: กำหนดค่าและใช้ตัวเลือกการบันทึก
หลังจากทำการลบข้อมูลแล้ว คุณสามารถส่งออกเอกสารเป็น PDF ที่แรสเตอร์ไลซ์ ตัวอย่างด้านล่างทำการแรสเตอร์ไลซ์เฉพาะหน้า 5 และบังคับให้เป็น PDF/A‑1a:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
try {
    SaveOptions options = new SaveOptions();

    // Enable rasterization for converting pages into images.
    options.getRasterization().setEnabled(true);
    
    // Set the starting page and count for rasterization.
    options.getRasterization().setPageIndex(5);
    options.getRasterization().setPageCount(1);

    // Define PDF compliance level.
    options.getRasterization().setCompliance(PdfComplianceLevel.PdfA1a);

    // Append a suffix to avoid filename conflicts.
    options.setAddSuffix(true);

    // Save the document with these configurations.
    redactor.save(options);
} finally { 
    redactor.close(); 
}
```

**ประเด็นสำคัญ:** การแรสเตอร์ไลซ์ PDF **ทำให้แต่ละหน้ากลายเป็นภาพ** ซึ่งลบเลเยอร์ข้อความที่ซ่อนอยู่และทำให้เอกสารไม่สามารถแก้ไขได้—เหมาะสำหรับการเก็บรักษาทางกฎหมาย  

## การประยุกต์ใช้งานจริง
1. **การลบข้อมูลที่ละเอียดอ่อน** – ซ่อนตัวระบุส่วนบุคคลโดยอัตโนมัติก่อนแชร์สัญญา  
2. **การเก็บรักษาเอกสาร** – แปลงรายงานที่เสร็จสมบูรณ์เป็น PDF/A ที่แรสเตอร์ไลซ์สำหรับการปฏิบัติตามระยะยาว  
3. **การอัปเดตเนื้อหาแบบกลุ่ม** – แทนที่คำศัพท์ที่ล้าสมัยในหลายร้อยไฟล์ด้วยสคริปต์เดียว  

## ข้อควรพิจารณาด้านประสิทธิภาพ
- **ปิด `Redactor`** หลังจากแต่ละการดำเนินการเพื่อปล่อยไฟล์แฮนด์เดิลและหน่วยความจำ  
- **การประมวลผลเป็นชุด** – โหลดรายการไฟล์และวนลูปผ่านไฟล์เหล่านั้น โดยใช้อินสแตนซ์ `Redactor` เดียวเมื่อเป็นไปได้  
- **ตรวจสอบทรัพยากร** – ใช้เครื่องมือ profiling ของ Java เพื่อติดตามการใช้ CPU และ heap ระหว่างการลบข้อมูลขนาดใหญ่  

## คำถามที่พบบ่อย

**Q: ฉันจะติดตั้ง GroupDocs.Redaction ในโครงการ Maven อย่างไร?**  
A: เพิ่ม repository ของ GroupDocs และ dependency `groupdocs-redaction` ลงใน `pom.xml` ตามที่แสดงในส่วนการตั้งค่า Maven  

**Q: ฉันสามารถลบข้อความจากไฟล์ PDF ด้วยไลบรารีนี้ได้หรือไม่?**  
A: ได้, GroupDocs.Redaction รองรับ PDF, DOCX, PPTX และรูปแบบอื่น ๆ อีกหลายประเภท  

**Q: จะเกิดอะไรขึ้นหากไม่พบวลีที่ตรงกัน?**  
A: `RedactorChangeLog` จะคืนสถานะ `Failed` ตรวจสอบการสะกดและความไวต่อกรณีของวลี  

**Q: ฉันจะจัดการกับเอกสารขนาดใหญ่อย่างมีประสิทธิภาพได้อย่างไร?**  
A: แบ่งการประมวลผลเป็นช่วงหน้าที่เล็กลง, เปิดการแรสเตอร์ไลซ์เฉพาะที่จำเป็น, และปิด `Redactor` เสมอเพื่อปล่อยทรัพยากร  

**Q: สามารถบันทึก PDF ที่แรสเตอร์ไลซ์โดยกำหนดช่วงหน้าที่เฉพาะได้หรือไม่?**  
A: แน่นอน ใช้ `options.getRasterization().setPageIndex()` และ `setPageCount()` เพื่อระบุหน้าที่ต้องการแรสเตอร์ไลซ์  

## สรุป
คุณได้มีคู่มือครบวงจร **วิธีลบข้อความ** ด้วย GroupDocs.Redaction Java และ **วิธีบันทึกเป็น PDF ที่แรสเตอร์ไลซ์** แล้ว ด้วยการทำตามขั้นตอนเหล่านี้ คุณสามารถปกป้องข้อมูลที่ละเอียดอ่อน, ปฏิบัติตามข้อกำหนด, และรักษาประสิทธิภาพสูงในงานผลิต

**ขั้นตอนต่อไป**  
- ศึกษา API อย่างละเอียดโดยสำรวจ [official documentation](https://docs.groupdocs.com/redaction/java/)  
- ทดลองใช้ประเภทการลบข้อมูลอื่น ๆ (เช่น `RegexRedaction`, `ImageRedaction`)  
- เข้าร่วมชุมชนใน [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) เพื่อรับเคล็ดลับและแนวทางปฏิบัติที่ดีที่สุด  

---

**Last Updated:** 2026-02-26  
**Tested With:** GroupDocs.Redaction Java 24.9  
**Author:** GroupDocs