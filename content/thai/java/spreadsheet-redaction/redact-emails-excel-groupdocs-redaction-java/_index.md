---
date: '2026-08-09'
description: เรียนรู้วิธีซ่อนข้อมูลส่วนบุคคลและปกปิดที่อยู่อีเมลในสเปรดชีต Excel ด้วย
  GroupDocs.Redaction Java API
keywords:
- how to hide personal data
- mask email addresses excel
- GroupDocs.Redaction Java
- Excel redaction tutorial
lastmod: '2026-08-09'
og_description: ค้นพบขั้นตอนโดยละเอียดวิธีซ่อนข้อมูลส่วนบุคคลและปกปิดที่อยู่อีเมลในไฟล์
  Excel ด้วย GroupDocs.Redaction Java API – โซลูชันที่รวดเร็วและปลอดภัยสำหรับการปฏิบัติตาม
  GDPR
og_image_alt: Guide showing Java code that redacts email addresses in an Excel spreadsheet
og_title: วิธีซ่อนข้อมูลส่วนบุคคลใน Excel ด้วย GroupDocs Java
schemas:
- author: GroupDocs
  dateModified: '2026-08-09'
  description: Learn how to hide personal data and mask email addresses in Excel spreadsheets
    using the GroupDocs.Redaction Java API.
  headline: How to hide personal data in Excel with GroupDocs Java
  type: TechArticle
- description: Learn how to hide personal data and mask email addresses in Excel spreadsheets
    using the GroupDocs.Redaction Java API.
  name: How to hide personal data in Excel with GroupDocs Java
  steps:
  - name: '**Partner data exchange** – Automatically strip customer emails before
      sending spreadsheets to vendors.'
    text: '**Partner data exchange** – Automatically strip customer emails before
      sending spreadsheets to vendors.'
  - name: '**Internal audit preparation** – Anonymize employee data during compliance
      reviews.'
    text: '**Internal audit preparation** – Anonymize employee data during compliance
      reviews.'
  - name: '**Scheduled reporting** – Embed the redaction step into nightly batch jobs
      that generate distribution‑ready reports.'
    text: '**Scheduled reporting** – Embed the redaction step into nightly batch jobs
      that generate distribution‑ready reports.'
  type: HowTo
- questions:
  - answer: Extend the pattern to include additional allowed characters (e.g., “+”
      or “_”) and test against a larger sample set, then re‑run the redaction.
    question: My regex still misses some corporate email formats. What should I do?
  - answer: Yes. Create a separate `CellFilter` for each column and invoke `redactor.apply`
      for each filter sequentially.
    question: Can I redact more than one column in a single pass?
  - answer: The library processes sheets incrementally, so files up to several gigabytes
      can be redacted as long as you enable streaming and close the `Redactor` after
      each file.
    question: Is GroupDocs.Redaction able to handle Excel files larger than 1 GB?
  - answer: Inspect the `RedactorChangeLog` returned by `apply`; a non‑failed status
      indicates success, while any errors are listed with line numbers and cell references.
    question: How do I capture redaction results or errors?
  - answer: Absolutely. Build the placeholder string dynamically (e.g., `"[redacted:"
      + UUID.randomUUID() + "]"`) and pass it to `ReplacementOptions`.
    question: Can I use a custom placeholder that includes a unique token per row?
  type: FAQPage
tags:
- hide personal data
- GroupDocs.Redaction
- Java Excel processing
- data privacy
title: วิธีซ่อนข้อมูลส่วนบุคคลใน Excel ด้วย GroupDocs Java
url: /th/java/spreadsheet-redaction/redact-emails-excel-groupdocs-redaction-java/
weight: 1
---

# วิธีซ่อนข้อมูลส่วนบุคคลใน Excel ด้วย GroupDocs Java

ในคู่มือนี้คุณจะได้เรียนรู้ **วิธีซ่อนข้อมูลส่วนบุคคล**—โดยเฉพาะที่อยู่อีเมล—ในไฟล์ Excel โดยใช้ GroupDocs.Redaction Java API ไม่ว่าคุณจะต้องปฏิบัติตาม GDPR, CCPA หรือแนวนโยบายความเป็นส่วนตัวภายใน วิธีการที่แสดงนี้ช่วยให้คุณทำการลบข้อมูลอัตโนมัติอย่างปลอดภัย รักษาไฟล์ต้นฉบับไม่เปลี่ยนแปลง และสร้างเวอร์ชันที่สะอาดพร้อมสำหรับการแจกจ่าย

## คำตอบสั้น
- **ซ่อนข้อมูลส่วนบุคคลหมายถึงอะไร?** หมายถึงการปิดบังหรือการลบข้อมูลที่สามารถระบุตัวบุคคลได้ (PII) จากไฟล์อย่างถาวรเพื่อไม่ให้สามารถอ่านได้อีกต่อไป  
- **ไลบรารีใดทำการลบข้อมูล?** GroupDocs.Redaction for Java  
- **ต้องมีใบอนุญาตเพื่อรันตัวอย่างหรือไม่?** สามารถใช้รุ่นทดลองฟรีสำหรับการทดสอบ; ต้องมีใบอนุญาตระดับผลิตภัณฑ์สำหรับการใช้งานเชิงพาณิชย์  
- **สามารถปรับแต่งข้อความตัวแทนได้หรือไม่?** ได้—คุณสามารถแทนที่อีเมลด้วยสตริงใดก็ได้ เช่น “[redacted email]”  
- **วิธีนี้เหมาะกับสเปรดชีตขนาดใหญ่หรือไม่?** ใช่ เมื่อคุณปฏิบัติตามเคล็ดลับประสิทธิภาพในส่วน “ข้อควรพิจารณาด้านประสิทธิภาพ”

## การซ่อนข้อมูลส่วนบุคคลคืออะไร?
**Hide personal data** หมายถึงการลบหรือปิดบังข้อมูลใด ๆ ที่สามารถระบุตัวบุคคลได้โดยตรงหรือโดยอ้อมอย่างถาวร เช่น ชื่อ, หมายเลขโทรศัพท์ หรือที่อยู่อีเมล กระบวนการนี้ทำให้ไฟล์ที่ได้ไม่สามารถนำไปใช้ระบุตัวบุคคลได้อีก

## ทำไมต้องใช้ GroupDocs.Redaction สำหรับ Java?
GroupDocs.Redaction รองรับ **รูปแบบไฟล์เข้าและออกกว่า 30 แบบ** และสามารถประมวลผลเวิร์กบุ๊กที่มี **สูงสุด 500,000 แถว** โดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ ทำให้ **ลดการใช้หน่วยความจำได้ถึง 80 %** เมื่อเทียบกับวิธีการอ่านไฟล์แบบธรรมดา ประโยชน์เชิงปริมาณเหล่านี้ทำให้เป็นตัวเลือกอันดับต้น ๆ สำหรับสายงานความเป็นส่วนตัวระดับองค์กร

## ข้อกำหนดเบื้องต้น
- Java Development Kit (JDK) 8 หรือใหม่กว่า  
- ความคุ้นเคยพื้นฐานกับไฟล์การสร้างของ Maven  
- การเข้าถึงไลบรารี GroupDocs.Redaction Java (ดาวน์โหลดได้ผ่าน Maven หรือหน้าปล่อยอย่างเป็นทางการ)

## การตั้งค่า GroupDocs.Redaction สำหรับ Java

### ฉันจะเพิ่ม GroupDocs.Redaction ไปยังโครงการ Maven อย่างไร?
เพิ่มรีโพซิทอรีของ GroupDocs และการพึ่งพา Redaction ลงในไฟล์ `pom.xml` ของคุณ (ดู [GroupDocs.Redaction releases](https://releases.groupdocs.com/redaction/java/)) จากนั้นรัน `mvn clean install` เพื่อดึง artifacts

```text
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
```

### ฉันจะขอรับใบอนุญาตสำหรับ GroupDocs.Redaction อย่างไร?
GroupDocs มีตัวเลือกใบอนุญาตสามแบบ (ดู [GroupDocs’ website](https://purchase.groupdocs.com/temporary-license/)):

- **Free trial** – การประเมินคุณลักษณะจำกัด, ไม่ต้องใช้บัตรเครดิต  
- **Temporary license** – คีย์ประเมิน 30‑วันที่ได้จากเว็บไซต์ GroupDocs  
- **Full license** – ใบอนุญาตการผลิตแบบถาวรที่ซื้อผ่านพอร์ทัลการขาย  

```text
```java
import com.groupdocs.redaction.Redactor;

public class RedactEmails {
    public static void main(String[] args) {
        // Initialize the redactor with your document path
        try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_XLSX")) {
            // Your redaction logic will go here
        }
    }
}
```
```

## คู่มือการใช้งาน

### ฉันจะสร้างอินสแตนซ์ Redactor สำหรับไฟล์ Excel อย่างไร?
คลาส `Redactor` เป็นจุดเริ่มต้นหลักที่โหลดเอกสารและให้บริการการลบข้อมูล  
สร้างอ็อบเจกต์ `Redactor` ที่ชี้ไปยังเวิร์กบุ๊กต้นฉบับ คลาส `Redactor` เป็นจุดเริ่มต้นสำหรับการดำเนินการลบข้อมูลทั้งหมด; มันโหลดไฟล์เข้าสู่โครงสร้างหน่วยความจำที่จัดการได้ในขณะที่ยังคงไฟล์ต้นฉบับบนดิสก์

```text
```java
import com.groupdocs.redaction.Redactor;

public class RedactEmails {
    public static void main(String[] args) {
        try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_XLSX")) {
            // Proceed to the next steps for redaction
        }
    }
}
```
```

### ฉันจะจำกัดการลบข้อมูลให้กับแผ่นงานและคอลัมน์เดียวได้อย่างไร?
คลาส `CellFilter` ให้คุณระบุว่าแผ่นงานและคอลัมน์ใดบ้างที่จะตรวจสอบสำหรับการลบข้อมูล ใช้ `CellFilter` เพื่อกำหนดชื่อแผ่นงานเป้าหมายและดัชนีคอลัมน์ คลาส `CellFilter` จะกรองเซลล์ก่อนที่เอนจินลบข้อมูลจะประมวลผล เพื่อให้แน่ใจว่าเฉพาะเซลล์ที่ต้องการเท่านั้นที่ถูกประมวลผล

```text
```java
import com.groupdocs.redaction.redactions.CellFilter;

// Create and configure the filter
CellFilter filter = new CellFilter();
filter.setColumnIndex(1); // Targeting the second column (index starts at 0)
filter.setWorkSheetName("Customers"); // Specify the worksheet name
```
```

### ฉันจะกำหนดรูปแบบ regular‑expression ที่จับที่อยู่อีเมลส่วนใหญ่ได้อย่างไร?
คลาส `Pattern` จาก `java.util.regex` แสดงถึง regular‑expression ที่คอมไพล์แล้วใช้ในการจับข้อความ สร้างอ็อบเจกต์ `Pattern` ด้วย regex ที่ครอบคลุมรูปแบบอีเมลทั่วไป รูปแบบด้านล่างจับที่อยู่อีเมลที่สอดคล้องกับ RFC‑5322 ส่วนใหญ่โดยละเว้นสตริงที่ผิดรูป

```text
```java
import java.util.regex.Pattern;

// Define regex pattern for matching emails
Pattern expression = Pattern.compile("^\\w+([-+.']\\w+)*@\\w+([-.]\\w+)*\\.\\w+([-.]\\w+)*$");
```
```

### ฉันจะใช้การลบข้อมูลและแทนที่อีเมลด้วยข้อความแทนที่อย่างไร?
คลาส `ReplacementOptions` กำหนดวิธีที่เนื้อหาที่จับได้จะถูกแทนที่ เช่น ข้อความแทนที่ ผสานฟิลเตอร์, pattern, และอินสแตนซ์ `ReplacementOptions` คลาส `ReplacementOptions` ให้คุณตั้งค่าข้อความแทนที่ที่แน่นอนที่จะปรากฏในแต่ละเซลล์ที่ถูกลบข้อมูล

```text
```java
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.RedactorChangeLog;
import com.groupdocs.redaction.redactions.CellColumnRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

// Apply redaction
RedactorChangeLog result = redactor.apply(new CellColumnRedaction(filter, expression, new ReplacementOptions("[customer email]")));

// Save changes if successful
if (result.getStatus() != RedactionStatus.Failed) {
    SaveOptions saveOptions = new SaveOptions();
    saveOptions.setAddSuffix(true); // Add a suffix to the saved file name
    redactor.save(saveOptions);
}
```
```

## ข้อผิดพลาดทั่วไปและการแก้ไขปัญหา

- **Regex does not catch all cases** – ทดสอบ pattern กับตัวอย่างข้อมูลที่เป็นตัวแทนและปรับคลาสอักขระตามความจำเป็น  
- **Incorrect column index** – จำไว้ว่าการนับคอลัมน์เริ่มที่ 0; คอลัมน์ B มีดัชนี 1  
- **Worksheet name case‑sensitivity** – ใช้ชื่อแผ่นงานที่ตรงกับที่แสดงใน Excel; “Customers” ≠ “customers”  
- **Resource leaks** – ห่อ `Redactor` ด้วยบล็อก try‑with‑resources (ตามที่แสดง) เพื่อให้แน่ใจว่าทรัพยากรเนทีฟถูกปล่อยอย่างทันท่วงที  

## ทำไมต้องซ่อนข้อมูลส่วนบุคคลใน Excel?
การซ่อนข้อมูลส่วนบุคคลใน Excel จะลบข้อมูลที่สามารถระบุตัวบุคคลได้ทั้งหมด ทำให้ไฟล์ไม่สามารถใช้ตามรอยบุคคลได้ สิ่งนี้ช่วยปกป้องความเป็นส่วนตัว, ปฏิบัติตามข้อกำหนดกฎหมาย, และป้องกันการรั่วไหลโดยบังเอิญเมื่อแชร์สเปรดชีตกับบุคคลภายนอกหรือเผยแพร่ข้อมูลสาธารณะ

- **Regulatory compliance** – ปฏิบัติตาม GDPR, CCPA, และข้อบังคับความเป็นส่วนตัวเฉพาะอุตสาหกรรม  
- **Risk mitigation** – ป้องกันการเปิดเผย PII โดยบังเอิญเมื่อแชร์ไฟล์กับพันธมิตรภายนอก  
- **Audit readiness** – รักษาร่องรอยการตรวจสอบที่สะอาดและไม่เปลี่ยนแปลงโดยการลบค่าที่ละเอียดอ่อนอย่างถาวรจากชุดข้อมูลที่เก็บไว้  

## การประยุกต์ใช้งานจริง

1. **Partner data exchange** – ลบอีเมลลูกค้าโดยอัตโนมัติก่อนส่งสเปรดชีตให้ผู้ขาย  
2. **Internal audit preparation** – ทำให้ข้อมูลพนักงานเป็นนามธรรมระหว่างการตรวจสอบความสอดคล้อง  
3. **Scheduled reporting** – ฝังขั้นตอนการลบข้อมูลลงในงานแบตช์รายคืนที่สร้างรายงานพร้อมแจกจ่าย  

## ข้อควรพิจารณาด้านประสิทธิภาพ

- **Batch processing** – ใช้ `Redactor` ตัวเดียวซ้ำหลายไฟล์เพื่อลดภาระ JVM  
- **Memory management** – API ประมวลผลแผ่นงานทีละหนึ่ง; สำหรับเวิร์กบุ๊กที่เกิน 100 MB ให้ประมวลผลแถวเป็นชิ้นเพื่อรักษาการใช้ heap ต่ำ  
- **Large datasets** – เมื่อจัดการไฟล์ที่มี >100 k แถว ให้เปิดใช้โหมดสตรีมมิ่ง (มีในเวอร์ชัน 24.9) เพื่อให้การใช้หน่วยความจำต่ำกว่า 200 MB  

## คำถามที่พบบ่อย

**Q: Regex ของฉันยังพลาดรูปแบบอีเมลของบริษัทบางประเภท ควรทำอย่างไร?**  
A: ขยาย pattern ให้รวมอักขระที่อนุญาตเพิ่มเติม (เช่น “+” หรือ “_”) แล้วทดสอบกับชุดตัวอย่างที่ใหญ่ขึ้น จากนั้นรันการลบข้อมูลใหม่

**Q: สามารถลบข้อมูลหลายคอลัมน์ในครั้งเดียวได้หรือไม่?**  
A: ได้ สร้าง `CellFilter` แยกสำหรับแต่ละคอลัมน์และเรียก `redactor.apply` สำหรับแต่ละฟิลเตอร์ตามลำดับ

**Q: GroupDocs.Redaction สามารถจัดการไฟล์ Excel ที่ใหญ่กว่า 1 GB ได้หรือไม่?**  
A: ไลบรารีประมวลผลแผ่นงานแบบเพิ่มส่วน ทำให้ไฟล์หลายกิกะไบต์สามารถลบข้อมูลได้ตราบใดที่เปิดใช้สตรีมมิ่งและปิด `Redactor` หลังแต่ละไฟล์

**Q: จะจับผลลัพธ์หรือข้อผิดพลาดของการลบข้อมูลอย่างไร?**  
A: ตรวจสอบ `RedactorChangeLog` ที่คืนจาก `apply`; สถานะที่ไม่เป็น Failed แสดงว่าประสบความสำเร็จ ส่วนข้อผิดพลาดจะระบุด้วยหมายเลขบรรทัดและอ้างอิงเซลล์

**Q: สามารถใช้ข้อความแทนที่ที่กำหนดเองและมีโทเค็นเฉพาะแต่ละแถวได้หรือไม่?**  
A: แน่นอน สร้างสตริงแทนที่แบบไดนามิก (เช่น `"[redacted:" + UUID.randomUUID() + "]"`) แล้วส่งให้ `ReplacementOptions`

## แหล่งข้อมูลเพิ่มเติม

- [เอกสาร](https://docs.groupdocs.com/redaction/java/)
- [อ้างอิง API](https://reference.groupdocs.com/redaction/java)
- [ดาวน์โหลด GroupDocs.Redaction](https://releases.groupdocs.com/redaction/java/)
- [ที่เก็บ GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
- [ฟอรั่มสนับสนุนฟรี](https://forum.groupdocs.com/c/redaction/33)
- [ข้อมูลใบอนุญาตชั่วคราว](https://purchase.groupdocs.com/temporary-license/)

---

**อัปเดตล่าสุด:** 2026-08-09  
**ทดสอบด้วย:** GroupDocs.Redaction 24.9 for Java  
**ผู้เขียน:** GroupDocs

## บทเรียนที่เกี่ยวข้อง

- [วิธีกรองข้อมูลในสเปรดชีต – GroupDocs.Redaction Java](/redaction/java/spreadsheet-redaction/)
- [ซ่อนข้อมูลที่ละเอียดอ่อน Java – ลบข้อมูลส่วนบุคคลด้วย GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)
- [ซ่อนข้อมูลที่ละเอียดอ่อน Java – คู่มือ GroupDocs.Redaction](/redaction/java/getting-started/)