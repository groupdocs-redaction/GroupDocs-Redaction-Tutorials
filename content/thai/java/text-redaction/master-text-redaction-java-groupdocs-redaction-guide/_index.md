---
date: '2026-08-20'
description: ค้นพบวิธีการลบข้อมูลในข้อความโดยใช้ regex กับ Java และ GroupDocs.Redaction.
  บทเรียนขั้นตอนต่อขั้นตอนนี้จะแสดงวิธีการใช้ regex, การกำหนดค่า save options, และการปกป้องข้อมูลที่ละเอียดอ่อน
keywords:
- how to redact text
- mask credit card numbers
- remove social security numbers
- redact pdf java
lastmod: '2026-08-20'
og_description: เรียนรู้วิธีลบข้อมูลในข้อความด้วย Java โดยใช้ GroupDocs.Redaction.
  คู่มือนี้อธิบายการลบข้อมูลด้วย regex, การกำหนดค่า save‑option, และเคล็ดลับ performance
  สำหรับการปกป้องข้อมูลที่ละเอียดอ่อน
og_image_alt: Guide showing Java code to redact text using GroupDocs.Redaction
og_title: วิธีลบข้อมูลในข้อความด้วย Java และ GroupDocs.Redaction
schemas:
- author: GroupDocs
  dateModified: '2026-08-20'
  description: Discover how to redact text using regex in Java with GroupDocs.Redaction.
    This step‑by‑step tutorial shows you how to apply regex, configure save options,
    and protect sensitive data.
  headline: 'How to redact text in Java with GroupDocs.Redaction: A complete guide'
  type: TechArticle
- description: Discover how to redact text using regex in Java with GroupDocs.Redaction.
    This step‑by‑step tutorial shows you how to apply regex, configure save options,
    and protect sensitive data.
  name: 'How to redact text in Java with GroupDocs.Redaction: A complete guide'
  steps:
  - name: import required classes
    text: 'The following imports give you access to the redaction API:'
  - name: initialize redactor and apply regex pattern
    text: '`RegexRedaction` represents a redaction rule based on a regular‑expression
      pattern. The pattern you provide determines which text fragments are replaced.
      - **Regex explanation**: The pattern `\b\d{3}-\d{2}-\d{4}\b` matches U.S. Social
      Security numbers (three digits, a dash, two digits, a dash, four '
  - name: configure save options
    text: '`SaveOptions` controls how the redacted file is written. Adding a suffix
      makes it clear which files have been processed, while preserving the original
      format avoids unwanted conversion. - **Save options**: `setAddSuffix(true)`
      automatically appends “_redacted” to the output filename, preventing acci'
  - name: customize additional save settings
    text: 'You can further tailor the output—such as preserving metadata or flattening
      annotations—by adjusting the `SaveOptions` object. - **Key configuration**:
      Setting `setPreserveMetadata(true)` retains original document properties, which
      is often required for compliance audits.'
  type: HowTo
- questions:
  - answer: It automatically appends a suffix (e.g., `_redacted`) to the output filename,
      making it obvious which files have been processed.
    question: What is the purpose of `setAddSuffix(true)` in SaveOptions?
  - answer: Absolutely. Any valid Java regular expression can be supplied to `RegexRedaction`
      to target emails, phone numbers, custom IDs, etc.
    question: Can I use regex patterns other than numbers for text redaction?
  - answer: Wrap the redaction logic in a try‑catch block, log the exception, and
      always close the `Redactor` in a finally clause to release resources.
    question: How should I handle errors during redaction?
  - answer: Yes. GroupDocs.Redaction works with PDF, DOCX, PPTX, and many other formats.
    question: Is PDF redaction supported?
  - answer: Use batch processing, keep regex patterns simple, and monitor memory usage
      with profiling tools.
    question: What are best practices for large‑scale redaction projects?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java document processing
- regex redaction
- PDF redaction
title: 'วิธีทำการลบข้อมูลในข้อความด้วย Java และ GroupDocs.Redaction: คู่มือฉบับสมบูรณ์'
type: docs
url: /th/java/text-redaction/master-text-redaction-java-groupdocs-redaction-guide/
weight: 1
---

# วิธีลบข้อความใน Java ด้วย GroupDocs.Redaction: คู่มือฉบับสมบูรณ์

ในโลกดิจิทัลที่เคลื่อนที่อย่างรวดเร็วในวันนี้, **วิธีลบข้อความ** ในเอกสารเป็นคำถามที่นักพัฒนาหลายคนต้องเผชิญ ไม่ว่าคุณจะกำลังปกป้องข้อมูลส่วนบุคคล, ปฏิบัติตามกฎระเบียบ, หรือเพียงแค่ทำความสะอาดร่างเอกสาร, คู่มือนี้จะพาคุณผ่านการใช้ GroupDocs.Redaction สำหรับ Java เพื่อ **ใช้การลบข้อความโดยอิง regex อย่างรวดเร็วและปลอดภัย** คุณจะได้เรียนรู้ว่าการลบข้อความสำคัญอย่างไร, วิธีตั้งค่าห้องสมุด, และเคล็ดลับการปฏิบัติที่ดีที่สุดสำหรับการประมวลผลที่มีประสิทธิภาพสูง

## คำตอบด่วน
- **วัตถุประสงค์หลักของ GroupDocs.Redaction คืออะไร?** มันให้ API ที่เชื่อถือได้สำหรับค้นหาและซ่อนข้อความที่เป็นความลับในรูปแบบเอกสารมากกว่า 50 แบบ.  
- **ฉันจะใช้ regex สำหรับการลบข้อความอย่างไร?** สร้างอ็อบเจกต์ `RegexRedaction` ด้วยแพทเทิร์นของคุณและส่งให้เมธอด `Redactor.apply()`.  
- **ฉันต้องมีลิขสิทธิ์หรือไม่?** การทดลองใช้ฟรีทำงานสำหรับการพัฒนา; ลิขสิทธิ์แบบชำระเงินจะเปิดใช้งานฟีเจอร์ทั้งหมดสำหรับการผลิต.  
- **ฉันสามารถลบข้อความใน PDF ได้เช่นเดียวกับไฟล์ DOCX หรือไม่?** ได้—GroupDocs.Redaction รองรับ PDF, DOCX, PPTX และรูปแบบอื่น ๆ อีกหลายรูปแบบ.  
- **วิธีที่ดีที่สุดในการปรับปรุงประสิทธิภาพคืออะไร?** ปิดอินสแตนซ์ `Redactor` อย่างรวดเร็ว, ทำให้แพทเทิร์น regex เรียบง่าย, และประมวลผลไฟล์เป็นชุด.

## การลบข้อความคืออะไรและทำไมจึงสำคัญ?
การลบข้อความจะลบหรือทำให้ข้อมูลที่เป็นความลับจากเอกสารหายไปอย่างถาวร, ทำให้มั่นใจว่าข้อมูลที่เป็นความลับ—เช่นหมายเลขประกันสังคม, รายละเอียดบัตรเครดิต, หรือบันทึกทางการแพทย์—ไม่สามารถกู้คืนหรือดูได้โดยบุคคลที่ไม่ได้รับอนุญาต มันทำงานโดยการเขียนทับอักขระเดิมหรือแทนที่ด้วยหน้ากาก, ดังนั้นเนื้อหาที่ซ่อนอยู่ไม่สามารถดึงออกโดยการคัดลอก‑วางหรือเครื่องมือ OCR ได้ สิ่งนี้ช่วยให้ปฏิบัติตามกฎระเบียบความเป็นส่วนตัวและปกป้องบุคคลจากการขโมยข้อมูลส่วนบุคคลหรือการละเมิดข้อมูล

## ทำไมต้องใช้ regex สำหรับการลบข้อความ?
Regular expressions ช่วยให้คุณกำหนดแพทเทิร์นที่ยืดหยุ่นซึ่งตรงกับรูปแบบข้อมูลที่หลากหลาย (เช่นหมายเลขโทรศัพท์, หมายเลขบัตรเครดิต) การใช้ regex กับ GroupDocs.Redaction ให้คุณควบคุมอย่างแม่นยำว่าอะไรจะถูกซ่อน, พร้อมกับทำให้การนำไปใช้สั้นกระชับและดูแลรักษาได้ง่าย

## ข้อกำหนดเบื้องต้น
- **Java Development Kit (JDK)** ที่ติดตั้ง (Java 8 หรือใหม่กว่า).  
- ความคุ้นเคยพื้นฐานกับไวยากรณ์ Java และ regular expressions.  
- IDE เช่น **IntelliJ IDEA** หรือ **Eclipse** เพื่อรันและดีบักโค้ด.  

## การตั้งค่า GroupDocs.Redaction สำหรับ Java
ขั้นแรก, เพิ่มไลบรารีลงในโปรเจกต์ของคุณ.

### การตั้งค่า Maven
หากคุณใช้ Maven, แทรกส่วนต่อไปนี้ลงในไฟล์ `pom.xml` ของคุณ:

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
หรือคุณสามารถดาวน์โหลด JAR ล่าสุดจาก [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### การเริ่มต้นพื้นฐาน
`Redactor` เป็นคลาสหลักที่เปิดเอกสาร, ใช้กฎการลบข้อความ, และเขียนผลลัพธ์ออก.

เมื่อไลบรารีพร้อมใช้งาน, คุณสามารถเริ่มลบข้อความในเอกสารได้:

```java
// Import the necessary classes from GroupDocs.Redaction
import com.groupdocs.redaction.Redactor;

public class RedactionExample {
    public static void main(String[] args) {
        // Initialize the redactor with your document path
        final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
        // Ensure you close resources after operations
        try { /* Your code here */ } finally { redactor.close(); }
    }
}
```

## วิธีลบข้อความโดยใช้ regex ใน Java?
กระบวนการนี้รวมถึงการโหลดไฟล์ต้นทางเข้าสู่อินสแตนซ์ `Redactor`, สร้างกฎ `RegexRedaction` ที่กำหนดแพทเทิร์นที่ต้องการจับ, ใช้กฎด้วย `redactor.apply()`, และสุดท้ายบันทึกเอกสารที่แก้ไขโดยใช้ `SaveOptions`. ด้วยการทำตามขั้นตอนเหล่านี้คุณจะสามารถค้นหาและซ่อนสตริงที่เป็นความลับได้อย่างเชื่อถือในรูปแบบที่รองรับ.

คลาส `Redactor` เป็นส่วนประกอบหลักที่เปิดเอกสาร, ใช้กฎการลบข้อความ, และเขียนไฟล์ผลลัพธ์. มันจัดการทรัพยากรภายใน, ดังนั้นคุณต้องปิดมันหลังการประมวลผลเพื่อปล่อยหน่วยความจำ.

### ขั้นตอนที่ 1: นำเข้าคลาสที่จำเป็น
การนำเข้าต่อไปนี้จะให้คุณเข้าถึง API การลบข้อความ:

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;
```

### ขั้นตอนที่ 2: เริ่มต้น redactor และใช้แพทเทิร์น regex
`RegexRedaction` แสดงกฎการลบข้อความที่อิงตามแพทเทิร์น regular‑expression. แพทเทิร์นที่คุณให้จะกำหนดว่าชิ้นส่วนข้อความใดจะถูกแทนที่.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    // Define a regex pattern to find sequences of numbers and apply a replacement color.
    // The pattern: Two digits, optional whitespace, two more digits, non-digit characters,
    // followed by six digits.
    redactor.apply(new RegexRedaction("\\d{2}\\s*\\d{2}[^\\d]*\\d{6}", 
        new ReplacementOptions(java.awt.Color.BLUE)));
```

- **คำอธิบาย Regex**: แพทเทิร์น `\b\d{3}-\d{2}-\d{4}\b` ตรงกับหมายเลข Social Security ของสหรัฐ (สามหลัก, ขีด, สองหลัก, ขีด, สี่หลัก). `ReplacementOptions` ให้คุณเลือกการทับสีดำทึบหรือหน้ากากข้อความที่กำหนดเอง.

### ขั้นตอนที่ 3: กำหนดค่า save options
`SaveOptions` ควบคุมวิธีการเขียนไฟล์ที่ลบข้อความแล้ว. การเพิ่ม suffix ทำให้ชัดเจนว่าไฟล์ใดได้รับการประมวลผล, ในขณะที่การรักษารูปแบบเดิมช่วยหลีกเลี่ยงการแปลงที่ไม่ต้องการ.

```java
    // Configure save options
    SaveOptions saveOptions = new SaveOptions();
    saveOptions.setAddSuffix(true);  // Adds suffix to indicate processing
    saveOptions.setRasterizeToPDF(false);  // Preserves original format

    // Save the redacted document
    redactor.save(saveOptions);
} finally {
    redactor.close();  // Always close resources to prevent memory leaks
}
```

- **ตัวเลือกการบันทึก**: `setAddSuffix(true)` จะเพิ่ม “_redacted” ไปยังชื่อไฟล์ผลลัพธ์โดยอัตโนมัติ, ป้องกันการเขียนทับโดยบังเอิญ.

### ขั้นตอนที่ 4: ปรับแต่งการตั้งค่าการบันทึกเพิ่มเติม
คุณสามารถปรับแต่งผลลัพธ์เพิ่มเติม—เช่นการรักษา metadata หรือการทำให้ annotation แบน—โดยปรับอ็อบเจกต์ `SaveOptions`.

```java
import com.groupdocs.redaction.options.SaveOptions;

SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true);  // Indicates processing by adding a suffix
saveOptions.setRasterizeToPDF(false);  // Keeps original format intact
```

- **การกำหนดค่าหลัก**: การตั้งค่า `setPreserveMetadata(true)` จะรักษาคุณสมบัติเอกสารต้นฉบับ, ซึ่งมักจำเป็นสำหรับการตรวจสอบการปฏิบัติตาม.

## การประยุกต์ใช้งานจริง
สถานการณ์จริงที่ **วิธีลบข้อความ** มีความสำคัญ:
1. **เอกสารทางกฎหมาย** – ซ่อนตัวระบุของลูกค้าก่อนแชร์ร่างให้ที่ปรึกษาภายนอก.  
2. **บันทึกทางการแพทย์** – ปิดบังชื่อผู้ป่วย, รหัส, หรือหมายเลขสุขภาพเพื่อให้สอดคล้องกับ HIPAA.  
3. **รายงานการเงิน** – ลบหมายเลขบัญชีที่เป็นความลับเมื่อแจกจ่ายสรุปไตรมาส.  

## ข้อควรพิจารณาด้านประสิทธิภาพ
- **การจัดการหน่วยความจำ**: เรียก `redactor.close()` เสมอเพื่อปล่อยไฟล์แฮนด์เลและทรัพยากรเนทีฟ.  
- **Regex ที่มีประสิทธิภาพ**: แพทเทิร์นที่เรียบง่ายทำงานเร็วกว่า; หลีกเลี่ยงการ back‑tracking มากเกินไปโดยใช้ atomic groups เมื่อเป็นไปได้.  
- **การประมวลผลเป็นชุด**: สำหรับชุดเอกสารขนาดใหญ่, ประมวลผลไฟล์เป็นชุด 20–50 ไฟล์เพื่อให้การใช้ heap คาดเดาได้.  

## ปัญหาทั่วไปและวิธีแก้
| ปัญหา | วิธีแก้ |
|-------|----------|
| **Regex ตรงกันมากเกินไป** | ทดสอบแพทเทิร์นของคุณด้วยเครื่องมือทดสอบ regex ออนไลน์และจำกัดคลาสอักขระให้แคบลง. |
| **ชื่อไฟล์ผลลัพธ์ซ้ำกัน** | ใช้ `setAddSuffix(true)` หรือระบุเส้นทางออกแบบกำหนดเองผ่าน `saveOptions.setOutputPath()`. |
| **การรั่วของหน่วยความจำใน PDF ขนาดใหญ่** | ประมวลผล PDF ทีละหน้า หรือเพิ่มขนาด heap ของ JVM (`-Xmx2g`). |

## คำถามที่พบบ่อย

**Q: จุดประสงค์ของ `setAddSuffix(true)` ใน SaveOptions คืออะไร?**  
A: มันจะเพิ่ม suffix (เช่น `_redacted`) ไปยังชื่อไฟล์ผลลัพธ์โดยอัตโนมัติ, ทำให้เห็นชัดว่าไฟล์ใดได้รับการประมวลผล.

**Q: ฉันสามารถใช้แพทเทิร์น regex ที่ไม่ใช่ตัวเลขสำหรับการลบข้อความได้หรือไม่?**  
A: แน่นอน. สามารถใช้ regular expression ของ Java ใด ๆ ที่ถูกต้องกับ `RegexRedaction` เพื่อกำหนดเป้าหมายเป็นอีเมล, หมายเลขโทรศัพท์, ID ที่กำหนดเอง ฯลฯ

**Q: ฉันควรจัดการกับข้อผิดพลาดระหว่างการลบข้อความอย่างไร?**  
A: ห่อหุ้มตรรกะการลบข้อความในบล็อก try‑catch, บันทึกข้อยกเว้น, และปิด `Redactor` ในบล็อก finally เสมอเพื่อปล่อยทรัพยากร.

**Q: การลบข้อความใน PDF รองรับหรือไม่?**  
A: รองรับ. GroupDocs.Redaction ทำงานกับ PDF, DOCX, PPTX และรูปแบบอื่น ๆ อีกหลายรูปแบบ.

**Q: แนวทางปฏิบัติที่ดีที่สุดสำหรับโครงการลบข้อความขนาดใหญ่คืออะไร?**  
A: ใช้การประมวลผลเป็นชุด, ทำให้แพทเทิร์น regex เรียบง่าย, และตรวจสอบการใช้หน่วยความจำด้วยเครื่องมือ profiling.

## แหล่งข้อมูลเพิ่มเติม
- **เอกสาร**: [GroupDocs Redaction Documentation](https://docs.groupdocs.com/redaction/java/)  
- **อ้างอิง API**: [GroupDocs API Reference](https://apireference.groupdocs.com/redaction/java)

---

**อัปเดตล่าสุด:** 2026-08-20  
**ทดสอบกับ:** GroupDocs.Redaction 24.9 for Java  
**ผู้เขียน:** GroupDocs

## บทแนะนำที่เกี่ยวข้อง

- [Mask Sensitive Data Java – คู่มือ GroupDocs.Redaction](/redaction/java/getting-started/)
- [Mask Sensitive Data Java – ลบข้อมูลส่วนบุคคลด้วย GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)
- [วิธีลบ PDF ด้วย Aspose OCR และ Java - การใช้แพทเทิร์น Regex ด้วย GroupDocs.Redaction](/redaction/java/ocr-integration/aspose-ocr-java-pdf-redaction/)