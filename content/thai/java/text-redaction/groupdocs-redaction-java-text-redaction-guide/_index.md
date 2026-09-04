---
date: '2026-08-09'
description: เรียนรู้วิธีทำการลบข้อมูลในเอกสาร Java ด้วย GroupDocs.Redaction. คู่มือขั้นตอนนี้ครอบคลุมการตั้งค่า
  Maven, การแทนที่ด้วยสี่เหลี่ยมสี, และแนวปฏิบัติที่ดีที่สุดสำหรับการจัดการเอกสารอย่างปลอดภัย.
keywords:
- how to redact java
- GroupDocs.Redaction Java
- java text redaction
lastmod: '2026-08-09'
og_description: เรียนรู้วิธีทำการลบข้อมูลในเอกสาร Java ด้วย GroupDocs.Redaction. ติดตามตัวอย่างเต็มรูปแบบพร้อมการกำหนดค่า
  Maven, การแทนที่ด้วยสี่เหลี่ยมสี, และเคล็ดลับด้านประสิทธิภาพ.
og_image_alt: 'Guide: redact Java documents with GroupDocs.Redaction using colored
  rectangle replacement'
og_title: วิธีทำการลบข้อมูลในเอกสาร Java ด้วย GroupDocs.Redaction
schemas:
- author: GroupDocs
  dateModified: '2026-08-09'
  description: Learn how to redact Java documents using GroupDocs.Redaction. This
    step‑by‑step tutorial covers Maven setup, colored‑rectangle replacement, and best
    practices for secure document handling.
  headline: How to redact Java documents with GroupDocs.Redaction
  type: TechArticle
- description: Learn how to redact Java documents using GroupDocs.Redaction. This
    step‑by‑step tutorial covers Maven setup, colored‑rectangle replacement, and best
    practices for secure document handling.
  name: How to redact Java documents with GroupDocs.Redaction
  steps:
  - name: import required classes
    text: 'First, bring the necessary GroupDocs classes into scope:'
  - name: initialize the redactor
    text: 'Instantiate the `Redactor` with the path to your source document:'
  - name: define the phrase and replacement options
    text: '`ExactPhraseRedaction` represents a redaction rule that searches for an
      exact text phrase and replaces it with the specified style. `ReplacementOptions`
      lets you configure how the redacted area appears, such as color, overlay mode,
      and border width. Tell the engine which exact phrase to hide and wha'
  - name: save the redacted document
    text: 'Write the changes back to disk (or to a stream for further processing):
      > **Warning:** Wrap the above calls in a `try‑catch` block to handle `IOException`
      or `RedactionException` and ensure resources are released.'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction is a Java library that enables you to permanently
      remove or mask sensitive information from documents, images, and PDFs.
    question: What is GroupDocs.Redaction?
  - answer: Use any `java.awt.Color` constant or create a custom RGB color with `new
      Color(r, g, b)` and pass it to `ReplacementOptions`.
    question: How do I choose the color for redaction?
  - answer: Yes, you can chain several `ExactPhraseRedaction` objects or mix different
      redaction types before calling `save`.
    question: Can I apply multiple redactions in one document?
  - answer: GroupDocs.Redaction supports over 30 formats—including PDF, PPTX, XLSX,
      and common image types—so you can redact virtually any file you encounter. See
      the [API Reference](https://reference.groupdocs.com/redaction/java) for the
      full list.
    question: What if my document is not a `.docx` file?
  - answer: Wrap your redaction logic in a `try‑catch` block that catches `IOException`
      and `RedactionException`. Always call `redactor.close()` in a `finally` block
      or use try‑with‑resources to release native resources.
    question: How do I handle errors during redaction?
  type: FAQPage
tags:
- redact Java
- GroupDocs.Redaction
- document security
- Java redaction tutorial
title: วิธีทำการลบข้อมูลในเอกสาร Java ด้วย GroupDocs.Redaction
type: docs
url: /th/java/text-redaction/groupdocs-redaction-java-text-redaction-guide/
weight: 1
---

# วิธีทำการลบข้อมูลในเอกสาร Java ด้วย GroupDocs.Redaction

ในโลกดิจิทัลที่เคลื่อนที่อย่างรวดเร็วในวันนี้, **how to redact Java** เป็นสิ่งสำคัญสำหรับผู้ที่ต้องการซ่อนข้อมูลลับในไฟล์ Office, PDF หรือรูปภาพ ไม่ว่าคุณจะกำลังเตรียมสัญญากฎหมาย, รายงานการเงิน, หรือบันทึก HR การเชี่ยวชาญการลบข้อความด้วยไลบรารีที่เชื่อถือได้จะช่วยประหยัดเวลาและทำให้คุณปฏิบัติตามระเบียบความเป็นส่วนตัวได้ ในคู่มือนี้เราจะอธิบายทุกขั้นตอน—ตั้งแต่การเพิ่ม GroupDocs.Redaction ไปยังโครงการ Maven จนถึงการใช้สี่เหลี่ยมสีเพื่อแทนที่วลีที่เป็นความลับ

## คำตอบสั้น
- **บทเรียนนี้ครอบคลุมอะไร?** ตัวอย่างครบวงจรของการลบข้อความด้วยสี่เหลี่ยมสีโดยใช้ GroupDocs.Redaction สำหรับ Java.  
- **เวอร์ชันของไลบรารีที่ใช้คืออะไร?** GroupDocs.Redaction 24.9 (หรือรุ่นล่าสุดในขณะอ่าน).  
- **ฉันต้องการไลเซนส์หรือไม่?** การทดลองใช้ฟรีหรือไลเซนส์ชั่วคราวเพียงพอสำหรับการพัฒนา; ต้องมีไลเซนส์เชิงพาณิชย์สำหรับการใช้งานจริง.  
- **ฉันสามารถเลือกสีสี่เหลี่ยมใดก็ได้หรือไม่?** ได้—ใช้ค่า `java.awt.Color` ใดก็ได้ใน `ReplacementOptions`.  
- **เหมาะกับเอกสารขนาดใหญ่หรือไม่?** ด้วยการจัดสรรหน่วยความจำและการทำความสะอาดทรัพยากรที่เหมาะสม มันทำงานได้ดีบนไฟล์หลายเมกะไบต์จนถึง 500 MB โดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ.

## การลบข้อความใน Java คืออะไร?
การลบข้อความใน Java คือกระบวนการลบหรือปกปิดข้อความที่เป็นความลับภายในเอกสารอย่างถาวรเพื่อให้ไฟล์สามารถแชร์ได้อย่างปลอดภัย GroupDocs.Redaction จะสแกนเอกสาร, แทนที่ข้อความที่ระบุด้วยรูปทรงสีทึบ, และรักษาเค้าโครงเดิมไว้, ทำให้ไฟล์ PDF หรือ Office สุดท้ายดูเป็นมืออาชีพและข้อมูลที่ซ่อนไม่สามารถกู้คืนได้.

## ทำไมต้องใช้ GroupDocs.Redaction เพื่อลบข้อความใน Java?
GroupDocs.Redaction มี API แบบเรียกครั้งเดียวที่ปกป้องข้อมูลลับขณะรักษาความแม่นยำของภาพ รองรับ **30+ รูปแบบ** เช่น DOCX, PDF, PPTX, XLSX, PNG, JPEG, และ BMP ทำให้ไฟล์ประเภททั่วไปทั้งหมดทำงานได้ เครื่องยนต์สตรีมไฟล์ทำให้สามารถลบข้อมูลในเอกสารขนาดถึง **500 MB** โดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ, ช่วยเพิ่มประสิทธิภาพและลดภาระเซิร์ฟเวอร์.

## ข้อกำหนดเบื้องต้น
- **ไลบรารีที่ต้องการ**: รวม GroupDocs.Redaction สำหรับ Java เวอร์ชัน 24.9 (หรือใหม่กว่า).  
- **สภาพแวดล้อมการพัฒนา**: Java 8 หรือใหม่กว่า, Maven (หรือ IDE ใดก็ได้ที่รองรับ Maven).  
- **ทักษะพื้นฐาน**: ความคุ้นเคยกับการทำ I/O ไฟล์ใน Java และการจัดการข้อยกเว้น.

## การตั้งค่า GroupDocs.Redaction สำหรับ Java
คุณสามารถเพิ่มไลบรารีนี้ลงในโครงการของคุณได้ทั้งผ่าน Maven หรือโดยการดาวน์โหลดไฟล์ JAR โดยตรง.

### การตั้งค่า Maven
เพิ่ม repository และ dependency ลงในไฟล์ `pom.xml` ของคุณ:

```xml
<repositories>
    <repository>
        <id>groupdocs-repo</id>
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

**License acquisition**  
เริ่มต้นด้วยการทดลองใช้ฟรีหรือขอไลเซนส์ชั่วคราวก่อนที่จะอัปเกรดเป็นแผนชำระเงิน.

## การเริ่มต้นและการตั้งค่าพื้นฐาน
`Redactor` เป็นคลาสหลักใน GroupDocs.Redaction ที่โหลดและจัดการเอกสารสำหรับการดำเนินการลบข้อมูล.

สร้างอินสแตนซ์ของ `Redactor` ที่ชี้ไปยังเอกสารที่คุณต้องการปกป้อง:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

> **เคล็ดลับ:** อย่าแก้ไขไฟล์ต้นฉบับ; `Redactor` ทำงานบนสำเนาในหน่วยความจำ, ดังนั้นคุณสามารถย้อนกลับได้ตลอดเมื่อจำเป็น.

## คู่มือการดำเนินการ: ลบข้อความด้วยสี่เหลี่ยมสี
ด้านล่างเป็นขั้นตอนแบบละเอียดที่แสดง **how to redact text Java** โดยการแทนที่วลีเป้าหมายด้วยสี่เหลี่ยมสีทึบ.

### ขั้นตอน 1: นำเข้าคลาสที่จำเป็น
แรกเริ่ม นำเข้าคลาสของ GroupDocs ที่จำเป็นเข้าสู่สโคป:

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;
```

### ขั้นตอน 2: เริ่มต้น Redactor
สร้างอินสแตนซ์ของ `Redactor` ด้วยพาธไปยังเอกสารต้นฉบับของคุณ:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

### ขั้นตอน 3: กำหนดวลีและตัวเลือกการแทนที่
`ExactPhraseRedaction` แสดงกฎการลบข้อมูลที่ค้นหาวลีข้อความที่ตรงกันอย่างแม่นยำและแทนที่ด้วยสไตล์ที่กำหนด  
`ReplacementOptions` ให้คุณกำหนดลักษณะของพื้นที่ที่ลบ เช่น สี, โหมดซ้อน, และความกว้างของขอบ.

บอกเครื่องมือว่าต้องซ่อนวลีใดอย่างแม่นยำและใช้สี่เหลี่ยมสีอะไร:

```java
redactor.apply(new ExactPhraseRedaction(
    "John Doe",
    new ReplacementOptions(java.awt.Color.RED)
));
```

*ที่นี่ `"John Doe"` คือข้อความที่เป็นความลับที่คุณต้องการปกปิด คุณสามารถเปลี่ยนเป็นสตริงใดก็ได้หรือแม้กระทั่ง regular expression.*

### ขั้นตอน 4: บันทึกเอกสารที่ลบข้อมูลแล้ว
เขียนการเปลี่ยนแปลงกลับไปยังดิสก์ (หรือสตรีมสำหรับการประมวลผลต่อไป):

```java
redactor.save("YOUR_DOCUMENT_DIRECTORY/redacted_sample.docx");
```

> **คำเตือน:** ห่อหุ้มการเรียกข้างต้นในบล็อก `try‑catch` เพื่อจัดการ `IOException` หรือ `RedactionException` และรับประกันว่าทรัพยากรถูกปล่อยออก.

## การประยุกต์ใช้งานจริง
- **การเตรียมเอกสารทางกฎหมาย** – ซ่อนชื่อลูกค้าหรือหมายเลขคดีก่อนแชร์ร่าง.  
- **การรายงานทางการเงิน** – ปกปิดหมายเลขบัญชีหรือสูตรลับในรายงานไตรมาส.  
- **เอกสาร HR** – ปกป้องตัวระบุพนักงานเมื่อส่งออกไฟล์บุคลากร.

คุณสามารถรวมเวิร์กโฟลว์นี้เข้ากับระบบจัดการเอกสารขนาดใหญ่, เรียกใช้งานผ่าน REST endpoint, หรือกำหนดเวลาการลบข้อมูลเป็นชุดในตอนกลางคืน.

## พิจารณาด้านประสิทธิภาพ
- **การจัดสรรหน่วยความจำ** – จัดสรรพื้นที่ heap เพียงพอ (`-Xmx2g` หรือมากกว่า) สำหรับไฟล์ DOCX/PDF ขนาดใหญ่.  
- **วงจรชีวิตของอ็อบเจกต์** – เรียก `redactor.close()` (หรือใช้ try‑with‑resources) เพื่อปลดปล่อยทรัพยากรเนทีฟโดยเร็ว.  
- **การประมวลผลเป็นชุด** – ใช้อินสแตนซ์ `Redactor` เดียวสำหรับหลายเอกสารเมื่อเป็นไปได้เพื่อลดภาระ.

## สรุป
ตอนนี้คุณมีบทเรียน **how to redact Java** ที่ครอบคลุมทุกอย่างตั้งแต่การกำหนดค่า Maven จนถึงการใช้มาสก์สี่เหลี่ยมสีบนวลีที่เป็นความลับ โดยทำตามขั้นตอนเหล่านี้คุณสามารถลบข้อความอย่างปลอดภัยในรูปแบบเอกสารที่รองรับทั้งหมด, ปฏิบัติตามระเบียบความเป็นส่วนตัว, และทำให้กระบวนการทำงานของคุณมีประสิทธิภาพ.

**ขั้นตอนต่อไป**  
- ทดลองใช้ประเภทการลบข้อมูลอื่น ๆ เช่น การลบรูปภาพหรือการจับคู่วลีด้วย regex.  
- ผสานการลบข้อมูลกับ GroupDocs.Viewer เพื่อดูตัวอย่างการเปลี่ยนแปลงก่อนบันทึก.  
- สำรวจ API เต็มรูปแบบเพื่อประมวลผลโฟลเดอร์เป็นชุดหรือรวมกับคลาวด์สตอเรจ.

## คำถามที่พบบ่อย

**Q: GroupDocs.Redaction คืออะไร?**  
A: GroupDocs.Redaction เป็นไลบรารี Java ที่ช่วยให้คุณลบหรือปกปิดข้อมูลที่เป็นความลับจากเอกสาร, รูปภาพ, และ PDF อย่างถาวร.

**Q: ฉันจะเลือกสีสำหรับการลบข้อมูลอย่างไร?**  
A: ใช้ค่าคงที่ `java.awt.Color` ใดก็ได้หรือสร้างสี RGB กำหนดเองด้วย `new Color(r, g, b)` แล้วส่งให้ `ReplacementOptions`.

**Q: ฉันสามารถทำการลบข้อมูลหลายรายการในเอกสารเดียวได้หรือไม่?**  
A: ได้, คุณสามารถต่อเนื่องหลายอ็อบเจกต์ `ExactPhraseRedaction` หรือผสมประเภทการลบข้อมูลต่าง ๆ ก่อนเรียก `save`.

**Q: ถ้าเอกสารของฉันไม่ใช่ไฟล์ `.docx`?**  
A: GroupDocs.Redaction รองรับมากกว่า 30 รูปแบบ—รวมถึง PDF, PPTX, XLSX, และรูปแบบภาพทั่วไป—ดังนั้นคุณสามารถลบข้อมูลได้เกือบทุกไฟล์ที่เจอ ดูที่ [API Reference](https://reference.groupdocs.com/redaction/java) สำหรับรายการเต็ม.

**Q: ฉันจะจัดการข้อผิดพลาดระหว่างการลบข้อมูลอย่างไร?**  
A: ห่อรอบตรรกะการลบข้อมูลของคุณในบล็อก `try‑catch` ที่จับ `IOException` และ `RedactionException`. ควรเรียก `redactor.close()` ในบล็อก `finally` หรือใช้ try‑with‑resources เพื่อปลดปล่อยทรัพยากรเนทีฟ.

---

**อัปเดตล่าสุด:** 2026-08-09  
**ทดสอบด้วย:** GroupDocs.Redaction 24.9 for Java  
**ผู้เขียน:** GroupDocs  

**แหล่งข้อมูล**  
- **เอกสาร:** [GroupDocs.Redaction Java Documentation](https://docs.groupdocs.com/redaction/java/)  
- **อ้างอิง API:** [GroupDocs Redaction API Reference](https://reference.groupdocs.com/redaction/java)  
- **ดาวน์โหลดเวอร์ชันล่าสุด:** [GroupDocs Redaction for Java Releases](https://releases.groupdocs.com/redaction/java/)  
- **ที่เก็บ GitHub:** [GroupDocs GitHub Page](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **ฟอรั่มสนับสนุนฟรี:** [GroupDocs Redaction Forum](https://forum.groupdocs.com/c/redaction/33)  
- **การสมัครไลเซนส์ชั่วคราว:** [Get Your Temporary License](https://purchase.groupdocs.com/temporary-license/)

## บทแนะนำที่เกี่ยวข้อง

- [วิธีลบเอกสารด้วย GroupDocs Redaction Java License จากเส้นทางไฟล์ – คู่มือขั้นตอน](/redaction/java/licensing-configuration/implement-groupdocs-redaction-java-license-file-path/)
- [แก้ไขเอกสารที่ป้องกันด้วยรหัสผ่าน Java - ลบเอกสารโดยใช้ GroupDocs.Redaction](/redaction/java/document-loading/groupdocs-redaction-java-password-documents/)
- [ปกปิดข้อมูลที่เป็นความลับ Java – ลบข้อมูลส่วนบุคคลด้วย GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)