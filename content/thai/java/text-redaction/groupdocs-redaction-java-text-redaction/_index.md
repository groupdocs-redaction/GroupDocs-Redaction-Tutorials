---
date: '2026-08-14'
description: วิธีลบข้อมูลในข้อความในเอกสาร Java ด้วย GroupDocs.Redaction – mask ข้อมูลส่วนบุคคลและ
  replace ข้อความที่อ่อนไหวอย่างมีประสิทธิภาพ
keywords:
- how to redact text
- GroupDocs Redaction Java
- text redaction Java
- mask personal information
lastmod: '2026-08-14'
og_description: การลบข้อมูลในข้อความด้วย GroupDocs.Redaction สำหรับ Java ช่วยให้คุณ
  mask ข้อมูลส่วนบุคคลอย่างถาวรและ replace สตริงที่อ่อนไหวใน PDFs, DOCX, และอื่น ๆ
  เพื่อให้สอดคล้องกับ GDPR และ HIPAA
og_image_alt: 'Guide: redact text in Java using GroupDocs.Redaction library'
og_title: วิธีลบข้อมูลในข้อความด้วย GroupDocs.Redaction สำหรับ Java
schemas:
- author: GroupDocs
  dateModified: '2026-08-14'
  description: How to redact text in Java documents using GroupDocs.Redaction – mask
    personal information and replace sensitive text efficiently.
  headline: How to redact text with GroupDocs.Redaction for Java
  type: TechArticle
- description: How to redact text in Java documents using GroupDocs.Redaction – mask
    personal information and replace sensitive text efficiently.
  name: How to redact text with GroupDocs.Redaction for Java
  steps:
  - name: initialize the redactor
    text: '`Redactor` is the core class that loads a document, applies redaction rules,
      and writes the output.'
  - name: apply exact‑phrase redaction
    text: '`ExactPhraseRedaction` searches for an exact string match, while `ReplacementOptions`
      defines how the matched text should be replaced. - **Parameters:** - `"John
      Doe"` – the exact text to be redacted. - `ReplacementOptions("[personal]")`
      – the string that will replace the original content, effective'
  - name: save the redacted document
    text: '`Redactor.save` writes the modified document to a new file or overwrites
      the original, preserving the original format.'
  - name: clean up resources
    text: Always call `Redactor.close()` to release native resources and avoid memory
      leaks.
  type: HowTo
- questions:
  - answer: Yes, the library supports PDF, DOCX, XLSX, PPTX, and many other formats.
    question: Can I redact text from PDFs using GroupDocs.Redaction?
  - answer: No. Redactions permanently remove the original content, so keep a backup
      of the source file.
    question: Is a redaction reversible?
  - answer: Process them in chunks, use batch mode, and monitor memory usage with
      profiling tools.
    question: How do I handle very large documents efficiently?
  - answer: Besides DOCX and PDF, you can redact TXT, RTF, XLSX, PPTX, and more.
    question: What other text formats are supported?
  - answer: Absolutely. The API can be called from web services, background jobs,
      or CI/CD pipelines.
    question: Can I integrate GroupDocs.Redaction into existing workflows?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java document processing
- privacy compliance
- redaction API
title: วิธีลบข้อมูลในข้อความด้วย GroupDocs.Redaction สำหรับ Java
type: docs
url: /th/java/text-redaction/groupdocs-redaction-java-text-redaction/
weight: 1
---

# วิธีทำการลบข้อความด้วย GroupDocs.Redaction สำหรับ Java

ในบทแนะนำนี้คุณจะได้เรียนรู้ **วิธีทำการลบข้อความ** ในเอกสารที่ใช้ Java ด้วย GroupDocs.Redaction คุณจะเห็นวิธีซ่อนข้อมูลส่วนบุคคล, แทนที่สตริงที่สำคัญด้วยตัวแทนที่ปลอดภัย, และประมวลผลหลายไฟล์ในรูปแบบที่เหมาะกับการทำงานเป็นชุด เมื่อเสร็จคุณจะมีโซลูชันพร้อมใช้งานในระดับการผลิตที่ปกป้องความเป็นส่วนตัว, ตรงตามข้อกำหนด GDPR/HIPAA, และรวมเข้ากับแอปพลิเคชัน Java ที่มีอยู่ได้อย่างราบรื่น.

## คำตอบสั้น
- **ไลบรารีที่ใช้คืออะไร?** GroupDocs.Redaction for Java.  
- **ฉันสามารถซ่อนข้อมูลส่วนบุคคลได้หรือไม่?** ใช่ – ใช้การลบข้อความแบบ exact‑phrase พร้อมตัวเลือกการแทนที่.  
- **รองรับการประมวลผลเป็นชุดหรือไม่?** แน่นอน, คุณสามารถวนลูปผ่านหลายไฟล์ด้วยอินสแตนซ์ Redactor เดียวกัน.  
- **ฉันต้องการไลเซนส์หรือไม่?** การทดลองใช้ฟรีสามารถใช้สำหรับการประเมินได้; จำเป็นต้องมีไลเซนส์เชิงพาณิชย์สำหรับการใช้งานจริง.  
- **ต้องการเวอร์ชัน Java ใด?** JDK 8 หรือใหม่กว่า.

## “how to redact text” คืออะไร?

การลบข้อความ (Redaction) จะลบหรือทำให้ข้อมูลลับจากเอกสารหายไปอย่างถาวร ด้วย GroupDocs.Redaction คุณสามารถค้นหาสตริงเฉพาะ, แทนที่ด้วยตัวแทนที่ปลอดภัย, และบันทึกไฟล์ที่ทำความสะอาดแล้ว—ทั้งหมดโดยไม่ต้องแก้ไขด้วยมือ.

## ทำไมต้องใช้ GroupDocs.Redaction สำหรับ Java?

GroupDocs.Redaction สำหรับ Java รองรับ **รูปแบบอินพุตและเอาต์พุตกว่า 50 ประเภท** (รวมถึง PDF, DOCX, XLSX, PPTX, TXT, RTF) และสามารถประมวลผลไฟล์หลายร้อยหน้าโดยไม่ต้องโหลดเอกสารทั้งหมดเข้าสู่หน่วยความจำ, ให้การทำงานแบบแบตช์ที่มีอัตราผ่านสูงบนฮาร์ดแวร์เซิร์ฟเวอร์มาตรฐาน.

## ข้อกำหนดเบื้องต้น
- **Java Development Kit (JDK):** Version 8 or newer.  
- **IDE:** IntelliJ IDEA, Eclipse, หรือเครื่องมือแก้ไขที่เข้ากันได้กับ Java ใด ๆ.  
- **Maven:** สำหรับการจัดการ dependencies.  
- **Basic Java knowledge:** ความรู้พื้นฐานของ Java: ความคุ้นเคยกับคลาส, เมธอด, และการจัดการข้อยกเว้น.

## การตั้งค่า GroupDocs.Redaction สำหรับ Java
เริ่มต้นโดยเพิ่มไลบรารีนี้ลงในโปรเจกต์ Maven ของคุณ.

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
หากคุณต้องการ, ดาวน์โหลด JAR ล่าสุดจาก [เวอร์ชันล่าสุดของ GroupDocs.Redaction สำหรับ Java](https://releases.groupdocs.com/redaction/java/).

### การรับไลเซนส์
คุณสามารถเริ่มต้นด้วย **Free Trial**, ขอ **Temporary License** เพื่อการทดสอบต่อเนื่อง, หรือซื้อ **Commercial License** สำหรับการใช้งานในระดับการผลิต.

## วิธีลบข้อความในเอกสารด้วย GroupDocs.Redaction

ส่วนต่อไปนี้จะพาคุณผ่านขั้นตอนที่จำเป็นเพื่อ **ซ่อนข้อมูลส่วนบุคคล** และ **แทนที่ข้อความที่สำคัญ**.

### ขั้นตอน 1: เริ่มต้น Redactor
`Redactor` คือคลาสหลักที่โหลดเอกสาร, ใช้กฎการลบข้อความ, และเขียนผลลัพธ์ออกมา.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx", new LoadOptions());
```

### ขั้นตอน 2: ใช้การลบข้อความแบบ exact‑phrase
`ExactPhraseRedaction` ค้นหาการจับคู่สตริงที่ตรงกันอย่างสมบูรณ์, ส่วน `ReplacementOptions` กำหนดวิธีการแทนที่ข้อความที่พบ.

```java
redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]"));
```
- **พารามิเตอร์:**  
  - `"John Doe"` – ข้อความที่ต้องการลบอย่างตรงกัน.  
  - `ReplacementOptions("[personal]")` – สตริงที่จะใช้แทนเนื้อหาต้นฉบับ, ทำให้ **ซ่อนข้อมูลส่วนบุคคล** อย่างมีประสิทธิภาพ.

### ขั้นตอน 3: บันทึกเอกสารที่ลบข้อความแล้ว
`Redactor.save` เขียนเอกสารที่แก้ไขแล้วไปยังไฟล์ใหม่หรือเขียนทับไฟล์ต้นฉบับ, รักษารูปแบบเดิมไว้.

```java
redactor.save();
```

### ขั้นตอน 4: ทำความสะอาดทรัพยากร
ควรเรียก `Redactor.close()` เสมอเพื่อปล่อยทรัพยากรเนทีฟและหลีกเลี่ยงการรั่วไหลของหน่วยความจำ.

```java
finally {
    redactor.close();
}
```

## วิธีซ่อนข้อมูลส่วนบุคคลด้วย callback แบบกำหนดเอง
callback แบบกำหนดเองช่วยให้คุณตอบสนองต่อแต่ละเหตุการณ์การลบข้อความ—มีประโยชน์สำหรับการบันทึก, การแทนที่แบบมีเงื่อนไข, หรือการตรวจสอบ.

### สร้างคลาส callback
`IRedactionCallback` กำหนดเมธอดที่ถูกเรียกก่อนและหลังการดำเนินการลบข้อความแต่ละครั้ง.

```java
class RedactionDump implements IRedactionCallback {
    @Override
    public void onRedacted(IRedaction redaction) {
        // Custom processing or logging for each redaction event.
    }
}
```

### ใช้ callback เมื่อสร้างอินสแตนซ์ Redactor
ส่งการทำงานของ callback ของคุณผ่าน `RedactorSettings` เพื่อให้เอนจินทราบและเรียกใช้ในระหว่างการประมวลผล.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx", new LoadOptions(), new RedactorSettings(new RedactionDump()));
```

## การประยุกต์ใช้ในทางปฏิบัติ
- **สัญญากฎหมาย:** ซ่อนชื่อของลูกค้า, หมายเลขประกันสังคม (SSN), หรือข้อกำหนดลับโดยอัตโนมัติก่อนแชร์แบบร่าง.  
- **บันทึกทางการแพทย์:** **ซ่อนข้อมูลส่วนบุคคล** เช่น ตัวระบุผู้ป่วยเมื่อส่งออกบันทึกให้กับพันธมิตรการวิจัย.  
- **การสื่อสารองค์กร:** **แทนที่ข้อความที่สำคัญ** เช่น รหัสโครงการภายใน ก่อนการแจกจ่ายภายนอก เพื่อป้องกันการรั่วไหลโดยบังเอิญ.

## ข้อควรพิจารณาด้านประสิทธิภาพ
เมื่อประมวลผลไฟล์ขนาดใหญ่หรือจำนวนมาก, ควรคำนึงถึงเคล็ดลับต่อนี้:
- **การประมวลผลเป็นชุด:** วนลูปผ่านชุดไฟล์เพื่อ ลดภาระการเริ่มต้น.  
- **การจัดการหน่วยความจำ:** ปล่อย `Redactor` หลังจากแต่ละไฟล์; หลีกเลี่ยงการเก็บเอกสารหลายไฟล์ในหน่วยความจำพร้อมกัน.  
- **การทำ Profiling:** ใช้โปรไฟเลอร์ของ Java (เช่น VisualVM) เพื่อหาจุดคอขวดใน I/O หรือตรรกะการลบข้อความ.

## คำถามที่พบบ่อย
**ถาม: ฉันสามารถลบข้อความจาก PDF ด้วย GroupDocs.Redaction ได้หรือไม่?**  
A: ใช่, ไลบรารีนี้รองรับ PDF, DOCX, XLSX, PPTX, และรูปแบบอื่น ๆ อีกมากมาย.

**ถาม: การลบข้อความสามารถย้อนกลับได้หรือไม่?**  
A: ไม่. การลบข้อความจะลบเนื้อหาเดิมอย่างถาวร, ดังนั้นควรเก็บสำเนาสำรองของไฟล์ต้นฉบับ.

**ถาม: ฉันจะจัดการกับเอกสารขนาดใหญ่อย่างมีประสิทธิภาพอย่างไร?**  
A: ประมวลผลเป็นส่วน ๆ, ใช้โหมดแบตช์, และตรวจสอบการใช้หน่วยความจำด้วยเครื่องมือ profiling.

**ถาม: มีรูปแบบข้อความอื่น ๆ ที่รองรับบ้าง?**  
A: นอกจาก DOCX และ PDF, คุณยังสามารถลบข้อความจาก TXT, RTF, XLSX, PPTX, และอื่น ๆ ได้.

**ถาม: ฉันสามารถรวม GroupDocs.Redaction เข้ากับกระบวนการทำงานที่มีอยู่ได้หรือไม่?**  
A: แน่นอน. API สามารถเรียกใช้จากเว็บเซอร์วิส, งานเบื้องหลัง, หรือ pipeline ของ CI/CD.

## แหล่งข้อมูล
- **เอกสาร:** [เอกสาร GroupDocs Redaction Java](https://docs.groupdocs.com/redaction/java/)  
- **อ้างอิง API:** [อ้างอิง API ของ GroupDocs สำหรับ Java](https://reference.groupdocs.com/redaction/java)  
- **ดาวน์โหลด:** [ดาวน์โหลด GroupDocs.Redaction](https://releases.groupdocs.com/redaction/java/)  
- **ที่เก็บ GitHub:** [GitHub ของ GroupDocs Redaction](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **ฟอรั่มสนับสนุนฟรี:** [สนับสนุนฟรีของ GroupDocs](https://forum.groupdocs.com/c/redaction/33)  
- **การสมัครไลเซนส์ชั่วคราว:** [สมัครไลเซนส์ชั่วคราว](https://purchase.groupdocs.com/temporary-license/)

---

**อัปเดตล่าสุด:** 2026-08-14  
**ทดสอบด้วย:** GroupDocs.Redaction 24.9 for Java  
**ผู้เขียน:** GroupDocs

## บทแนะนำที่เกี่ยวข้อง

- [ซ่อนข้อมูลที่สำคัญ Java – คู่มือ GroupDocs.Redaction](/redaction/java/getting-started/)
- [ซ่อนข้อมูลที่สำคัญ Java – ลบข้อมูลส่วนบุคคลด้วย GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)
- [แก้ไขเอกสารที่ป้องกันด้วยรหัสผ่าน Java - ลบข้อความในเอกสารด้วย GroupDocs.Redaction](/redaction/java/document-loading/groupdocs-redaction-java-password-documents/)