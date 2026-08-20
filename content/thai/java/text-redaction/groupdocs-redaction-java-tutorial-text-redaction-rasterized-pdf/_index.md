---
date: '2026-08-20'
description: เรียนรู้วิธีทำการลบข้อมูลในข้อความด้วย GroupDocs.Redaction Java, บันทึกเป็น
  rasterized PDF, แทนที่วลีที่ตรงกันอย่างแม่นยำ, และใช้การตั้งค่า PDF แบบกำหนดเอง
keywords:
- how to redact text
- save pdf as image
- convert pdf to image
lastmod: '2026-08-20'
og_description: วิธีทำการลบข้อมูลในข้อความด้วย GroupDocs.Redaction Java คู่มือนี้จะแสดงการแทนที่วลีที่ตรงกันอย่างแม่นยำ,
  การสร้าง rasterized PDF, และการปฏิบัติตามมาตรฐาน PDF/A‑1a ในไม่กี่ขั้นตอน
og_image_alt: Guide showing GroupDocs.Redaction Java code to redact text and create
  rasterized PDF
og_title: วิธีทำการลบข้อมูลในข้อความด้วยไลบรารี GroupDocs.Redaction Java
schemas:
- author: GroupDocs
  dateModified: '2026-08-20'
  description: Learn how to redact text with GroupDocs.Redaction Java, save as rasterized
    PDF, replace exact phrases, and apply custom PDF settings.
  headline: How to redact text with GroupDocs.Redaction Java
  type: TechArticle
- description: Learn how to redact text with GroupDocs.Redaction Java, save as rasterized
    PDF, replace exact phrases, and apply custom PDF settings.
  name: How to redact text with GroupDocs.Redaction Java
  steps:
  - name: '**Sensitive data redaction** – automatically hide personal identifiers
      before sharing contracts.'
    text: '**Sensitive data redaction** – automatically hide personal identifiers
      before sharing contracts.'
  - name: '**Document archiving** – convert finalized reports to rasterized PDF/A
      for long‑term compliance.'
    text: '**Document archiving** – convert finalized reports to rasterized PDF/A
      for long‑term compliance.'
  - name: '**Bulk content update** – replace outdated terminology across hundreds
      of files with a single script.'
    text: '**Bulk content update** – replace outdated terminology across hundreds
      of files with a single script.'
  type: HowTo
- questions:
  - answer: Add the GroupDocs repository and the `groupdocs-redaction` dependency
      to your `pom.xml` as shown in the Maven Setup section.
    question: How do I install GroupDocs.Redaction in a Maven project?
  - answer: Yes, GroupDocs.Redaction supports PDF, DOCX, PPTX, and many other formats.
    question: Can I redact text from PDF files using this library?
  - answer: The `RedactorChangeLog` will return a status of `Failed`. Verify the phrase’s
      spelling and case sensitivity.
    question: What happens if the exact phrase isn’t found?
  - answer: Process them in smaller page ranges, enable rasterization only where needed,
      and always close the `Redactor` to free resources.
    question: How can I handle very large documents efficiently?
  - answer: Absolutely. Use `options.getRasterization().setPageIndex()` and `setPageCount()`
      to target the exact pages you want to rasterize.
    question: Is it possible to save rasterized PDFs with specific page ranges?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java PDF processing
title: วิธีทำการลบข้อมูลในข้อความด้วย GroupDocs.Redaction Java
type: docs
url: /th/java/text-redaction/groupdocs-redaction-java-tutorial-text-redaction-rasterized-pdf/
weight: 1
---

# วิธีทำการลบข้อความด้วย GroupDocs.Redaction Java

ในแอปพลิเคชันสมัยใหม่, **วิธีทำการลบข้อความ** ในเอกสารขณะรักษาความเร็วของกระบวนการทำงานและความสอดคล้องเป็นความท้าทายที่พบบ่อยสำหรับนักพัฒนา, ผู้ตรวจสอบ, และเจ้าหน้าที่ด้านการปฏิบัติตามกฎระเบียบ. บทแนะนำนี้จะพาคุณผ่านการใช้ GroupDocs.Redaction สำหรับ Java เพื่อค้นหาวลีที่ตรงกัน, แทนที่ด้วยชั้นทับที่ปลอดภัย, และสุดท้ายส่งออกผลลัพธ์เป็นเอกสาร PDF/A‑1a ที่แปลงเป็นภาพ—เหมาะสำหรับการเก็บถาวรหรือการแจกจ่ายทางกฎหมาย.

## คำตอบอย่างรวดเร็ว
- **คลาสหลักสำหรับการลบข้อความคืออะไร?** `Redactor`  
- **ฉันสามารถแทนที่วลีด้วยชั้นทับสีได้หรือไม่?** ใช่, โดยใช้ `ExactPhraseRedaction` และ `ReplacementOptions`.  
- **ฉันจะสร้าง PDF ที่แปลงเป็นภาพได้อย่างไร?** เปิดการแปลงเป็นภาพผ่าน `SaveOptions.getRasterization().setEnabled(true)`.  
- **ระดับการปฏิบัติตาม PDF ที่ใช้ในตัวอย่างคืออะไร?** `PdfComplianceLevel.PdfA1a`.  
- **ฉันต้องการใบอนุญาตสำหรับการใช้งานในสภาพแวดล้อมการผลิตหรือไม่?** จำเป็นต้องมีใบอนุญาต GroupDocs.Redaction ที่ถูกต้องสำหรับการใช้งานในสภาพแวดล้อมการผลิต.

## “วิธีทำการลบข้อความ” ใน Java คืออะไร?
`Redaction` คือการลบหรือทำให้ข้อมูลที่ละเอียดอ่อนจากไฟล์เป็นถาวรเพื่อไม่ให้สามารถกู้คืนหรืออ่านได้ในภายหลัง. ด้วย GroupDocs.Redaction คุณสามารถค้นหาวลีที่ตรงกันโดยโปรแกรม เช่น หมายเลขประกันสังคมหรือรหัสโครงการที่เป็นความลับ, และแทนที่ด้วยชั้นทับสีแดง, กล่องสีดำ, หรือองค์ประกอบภาพใด ๆ ที่กำหนดเอง, เพื่อรับประกันว่าข้อมูลต้นฉบับจะไม่สามารถกู้คืนได้.

## ทำไมต้องใช้ GroupDocs.Redaction สำหรับ Java?
GroupDocs.Redaction รองรับ **รูปแบบไฟล์เข้าและออกกว่า 30 แบบ** (PDF, DOCX, PPTX, XLSX, HTML, และประเภทภาพ) และสามารถประมวลผลเอกสารหลายร้อยหน้าโดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ. อัลกอริทึมการจับคู่วลีที่ตรงกันของมันลดผลบวกเท็จได้มากกว่า > 95 % เมื่อเทียบกับการค้นหาคำหลักทั่วไป, และเครื่องมือแปลงเป็นภาพในตัวช่วยให้คุณสร้างไฟล์ PDF/A‑1a ที่เป็นภาพทั้งหมดสำหรับการเก็บรักษาระยะยาว.

## ข้อกำหนดเบื้องต้น
- **GroupDocs.Redaction for Java** (v24.9 หรือใหม่กว่า).  
- **Java Development Kit (JDK) 8+**.  
- IDE เช่น IntelliJ IDEA, Eclipse, หรือ NetBeans.  
- Maven สำหรับการจัดการ dependencies.  

### ไลบรารีและ dependencies ที่จำเป็น
- GroupDocs.Redaction for Java – เพิ่ม repository และ dependency ลงใน `pom.xml` ของคุณ (ดูส่วนการตั้งค่า Maven).  
- ตัวเลือก: เฟรมเวิร์กการบันทึกใด ๆ ที่คุณต้องการ (SLF4J, Log4j, ฯลฯ).

### ความรู้ที่ต้องมี
- พื้นฐานไวยากรณ์ Java และการทำ I/O กับไฟล์.  
- ความคุ้นเคยกับโครงสร้าง `pom.xml` ของ Maven.

## การตั้งค่า GroupDocs.Redaction สำหรับ Java
### การตั้งค่า Maven
เพิ่ม repository ของ GroupDocs และ dependency `groupdocs-redaction` ลงในไฟล์ `pom.xml` ของคุณ:

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
- **Free trial** – ทดลองใช้ API โดยไม่ต้องมีคีย์ใบอนุญาต.  
- **Temporary license** – ใช้สำหรับการประเมินผลระยะยาว.  
- **Full license** – จำเป็นสำหรับสภาพแวดล้อมการผลิต.

### การเริ่มต้นและตั้งค่าเบื้องต้น
The `Redactor` class คือจุดเริ่มต้นสำหรับการดำเนินการลบข้อความทั้งหมด. มันโหลดเอกสาร, ใช้กฎการลบข้อความ, และบันทึกผลลัพธ์.

```java
import com.groupdocs.redaction.Redactor;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
```

## วิธีทำการลบข้อความ – ตัวอย่างวลีที่ตรงกัน
Redactor คือคลาสหลักที่โหลดเอกสารและใช้กฎการลบข้อความ. ExactPhraseRedaction กำหนดกฎที่ตรงกับสตริงเฉพาะ. ตัวอย่างนี้แสดงการโหลดไฟล์, สร้างกฎ ExactPhraseRedaction, และดำเนินการลบข้อความในขั้นตอนเดียว, ให้กระบวนการทำงานที่กระชับสำหรับนักพัฒนาในขณะที่รับประกันว่าข้อมูลต้นฉบับจะถูกทำให้มืดลงอย่างถาวร.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.ReplacementOptions;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
```

## วิธีบันทึกเป็น PDF ที่แปลงเป็นภาพ
SaveOptions คืออ็อบเจกต์การกำหนดค่าที่ควบคุมวิธีการบันทึกเอกสาร. โดยการเปิดฟีเจอร์ rasterization และเลือกการปฏิบัติตาม PDF/A‑1a, คุณสามารถสร้าง PDF ที่เป็นภาพเท่านั้นโดยแต่ละหน้าถูกแปลงเป็นบิตแมพ, ตรงตามมาตรฐานการเก็บถาวรและป้องกันการสกัดข้อความ.

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

## การประยุกต์ใช้งานจริง
1. **Sensitive data redaction** – ซ่อนตัวระบุส่วนบุคคลโดยอัตโนมัติก่อนแชร์สัญญา.  
2. **Document archiving** – แปลงรายงานที่เสร็จสมบูรณ์เป็น PDF/A ที่แปลงเป็นภาพสำหรับการปฏิบัติตามระยะยาว.  
3. **Bulk content update** – แทนที่คำศัพท์ที่ล้าสมัยในหลายร้อยไฟล์ด้วยสคริปต์เดียว.

## ข้อควรพิจารณาด้านประสิทธิภาพ
- **ปิด `Redactor`** หลังจากแต่ละการดำเนินการเพื่อปล่อยไฟล์แฮนด์เดิลและหน่วยความจำ.  
- **การประมวลผลแบบชุด** – โหลดรายการไฟล์และวนลูปผ่านไฟล์เหล่านั้น, ใช้ `Redactor` ตัวเดียวซ้ำเมื่อเป็นไปได้.  
- **ตรวจสอบทรัพยากร** – ใช้เครื่องมือ profiling ของ Java เพื่อติดตามการใช้ CPU และ heap ระหว่างการลบข้อความขนาดใหญ่.

## คำถามที่พบบ่อย

**Q: ฉันจะติดตั้ง GroupDocs.Redaction ในโครงการ Maven อย่างไร?**  
A: เพิ่ม repository ของ GroupDocs และ dependency `groupdocs-redaction` ลงใน `pom.xml` ของคุณตามที่แสดงในส่วนการตั้งค่า Maven.

**Q: ฉันสามารถลบข้อความจากไฟล์ PDF ด้วยไลบรารีนี้ได้หรือไม่?**  
A: ใช่, GroupDocs.Redaction รองรับ PDF, DOCX, PPTX, และรูปแบบอื่น ๆ มากมาย.

**Q: จะเกิดอะไรขึ้นหากไม่พบวลีที่ตรงกัน?**  
A: `RedactorChangeLog` จะคืนสถานะเป็น `Failed`. ตรวจสอบการสะกดและความแตกต่างของตัวพิมพ์ของวลี.

**Q: ฉันจะจัดการกับเอกสารขนาดใหญ่อย่างมีประสิทธิภาพได้อย่างไร?**  
A: ประมวลผลเป็นช่วงหน้าที่เล็กลง, เปิด rasterization เฉพาะที่จำเป็น, และปิด `Redactor` เสมอเพื่อปล่อยทรัพยากร.

**Q: สามารถบันทึก PDF ที่แปลงเป็นภาพโดยกำหนดช่วงหน้าที่เฉพาะได้หรือไม่?**  
A: แน่นอน. ใช้ `options.getRasterization().setPageIndex()` และ `setPageCount()` เพื่อกำหนดหน้าที่ต้องการแปลงเป็นภาพ.

## สรุป
คุณมีคู่มือครบวงจรจากต้นจนจบเกี่ยวกับ **วิธีทำการลบข้อความ** ด้วย GroupDocs.Redaction Java และ **การบันทึกเป็น PDF ที่แปลงเป็นภาพ**. ด้วยการทำตามขั้นตอนเหล่านี้, คุณสามารถปกป้องข้อมูลที่ละเอียดอ่อนได้, ปฏิบัติตามมาตรฐานการปฏิบัติตามที่เข้มงวด, และทำให้บริการ Java ของคุณทำงานได้อย่างมีประสิทธิภาพในระดับใหญ่.

**ขั้นตอนต่อไป**  
- ศึกษา API อย่างลึกซึ้งโดยสำรวจ [official documentation](https://docs.groupdocs.com/redaction/java/).  
- ทดลองใช้ประเภทการลบข้อความอื่น ๆ เช่น `RegexRedaction` และ `ImageRedaction`.  
- เข้าร่วมชุมชนใน [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) เพื่อรับเคล็ดลับและแนวปฏิบัติที่ดีที่สุด.

---

**อัปเดตล่าสุด:** 2026-08-20  
**ทดสอบด้วย:** GroupDocs.Redaction Java 24.9  
**ผู้เขียน:** GroupDocs

```java
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.options.PdfComplianceLevel;
```

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

## บทแนะนำที่เกี่ยวข้อง

- [วิธีทำการลบข้อความด้วย GroupDocs.Redaction สำหรับ Java](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction/)
- [บทแนะนำการลบข้อความใน Java: คู่มือกับ GroupDocs.Redaction](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction-guide/)