---
date: '2026-09-26'
description: เรียนรู้วิธีลบข้อมูลเมตาดาต้าโดยใช้ GroupDocs ใน Java อย่างปลอดภัย เพื่อลบเมตาดาต้าเอกสารที่เป็นความลับโดยไม่ทำให้รูปแบบเดิมเสียหาย
keywords:
- how to redact metadata
- GroupDocs Redaction Java
- secure document processing
- metadata removal Java
lastmod: '2026-09-26'
og_description: วิธีลบข้อมูลเมตาดาต้าโดยใช้ GroupDocs ใน Java – คู่มือขั้นตอนที่แสดงให้คุณเห็นวิธีลบเมตาดาต้าเอกสารที่เป็นความลับอย่างปลอดภัยและรักษารูปแบบเดิมไว้
og_image_alt: Guide showing metadata redaction using GroupDocs in Java
og_title: วิธีลบข้อมูลเมตาดาต้าโดยใช้ GroupDocs ใน Java
schemas:
- author: GroupDocs
  dateModified: '2026-09-26'
  description: Learn how to redact metadata with GroupDocs in Java, securely removing
    confidential document metadata while keeping the original format intact.
  headline: How to redact metadata with GroupDocs in Java
  type: TechArticle
- description: Learn how to redact metadata with GroupDocs in Java, securely removing
    confidential document metadata while keeping the original format intact.
  name: How to redact metadata with GroupDocs in Java
  steps:
  - name: import necessary classes
    text: These imports give you access to the redaction engine, save options, and
      metadata utilities.
  - name: initialize redactor
    text: Instantiate the `Redactor` with the path to your source file.
  - name: configure metadata search and redaction
    text: Create a `MetadataSearchRedaction` that looks for the exact string **"Company
      Ltd."** and replaces it with **"--company--"**. The `setFilter` call limits
      the operation to the *Company* metadata field only.
  - name: apply the redaction
    text: Run the redaction against the opened document.
  - name: save with custom options
    text: '`SaveOptions` allows you to specify output format, file naming, and other
      saving parameters for the redacted document. Configure `SaveOptions` so the
      redacted file gets a “_Redacted” suffix while preserving its original format.'
  - name: release resources
    text: Always close the `Redactor` to free native resources and avoid memory leaks.
  type: HowTo
- questions:
  - answer: It’s a powerful library that enables you to redact text, metadata, and
      images in documents using Java applications.
    question: What is GroupDocs.Redaction for Java?
  - answer: Yes, but with limitations. A free trial or temporary license allows full
      access for testing purposes.
    question: Can I use GroupDocs.Redaction without purchasing a license?
  - answer: Use `SaveOptions` to specify your requirements, such as avoiding rasterization
      when saving to PDF.
    question: How do I ensure document formats are preserved during redaction?
  - answer: It supports a wide range, including Word, Excel, PowerPoint, PDF, and
      many more.
    question: What types of documents can be redacted using GroupDocs.Redaction?
  - answer: Visit the [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33)
      for assistance.
    question: Where can I find support if I run into issues?
  type: FAQPage
tags:
- metadata redaction
- GroupDocs
- Java document security
- redaction tutorial
title: วิธีลบข้อมูลเมตาดาต้าโดยใช้ GroupDocs ใน Java
type: docs
url: /th/java/metadata-redaction/java-metadata-redaction-groupdocs-tutorial/
weight: 1
---

# วิธีลบข้อมูลเมตาโดยใช้ GroupDocs ใน Java

ในบทแนะนำที่ครอบคลุมนี้ คุณจะได้เรียนรู้ **วิธีลบข้อมูลเมตา** จาก Word, PDF และประเภทเอกสารอื่น ๆ มากมายโดยใช้ GroupDocs.Redaction สำหรับ Java. เมื่อจบคู่มือ คุณจะสามารถฝังการลบข้อมูลเมตาเข้าไปในบริการใด ๆ ที่ใช้ Java ได้, เพื่อให้แน่ใจว่าข้อมูลที่เป็นความลับ เช่น ชื่อบริษัท, ผู้เขียน หรือคุณสมบัติกำหนดเอง จะไม่ออกนอกองค์กรของคุณ.

## คำตอบอย่างรวดเร็ว
- **MetadataSearchRedaction ทำอะไร?** มันค้นหาฟิลด์เมตาเฉพาะและแทนค่าของพวกมันด้วยข้อความที่กำหนดเอง.  
- **ต้องใช้ไลบรารีใด?** GroupDocs.Redaction for Java (v24.9 หรือใหม่กว่า).  
- **ต้องการไลเซนส์หรือไม่?** การทดลองใช้ฟรีสามารถใช้สำหรับการประเมิน; จำเป็นต้องมีไลเซนส์เต็มสำหรับการใช้งานจริง.  
- **สามารถคงรูปแบบไฟล์ต้นฉบับได้หรือไม่?** ได้—ใช้ `SaveOptions` เพื่อรักษารูปแบบเดิม.  
- **วิธีนี้ปลอดภัยต่อการทำงานหลายเธรดหรือไม่?** แต่ละอินสแตนซ์ของ `Redactor` เป็นอิสระ, ดังนั้นคุณสามารถประมวลผลเอกสารพร้อมกันได้.

## วิธีลบข้อมูลเมตาโดยใช้ GroupDocs?
`Redactor` เป็นคลาสหลักที่โหลดเอกสารและให้การดำเนินการลบข้อมูล.  
โหลดเอกสารต้นฉบับของคุณด้วยอินสแตนซ์ `Redactor`, ตั้งค่า `MetadataSearchRedaction` เพื่อเจาะจุดคีย์เมตาที่ต้องการทำความสะอาด, ใช้การลบข้อมูล, และสุดท้ายบันทึกไฟล์ด้วย `SaveOptions`. กระบวนการทั้งหมดนี้สามารถเขียนได้ในไม่กี่บรรทัดและทำงานกับรูปแบบที่รองรับทั้งหมด, ตั้งแต่ DOCX ถึง PDF และอื่น ๆ.

## การลบข้อมูลเมตาด้วย GroupDocs คืออะไร?
`MetadataSearchRedaction` เป็นคลาสพิเศษที่ให้คุณเจาะจุดคุณสมบัติเบต้าเมตาเฉพาะ (เช่น *Company*, *Author*) และแทนที่เนื้อหาด้วยตัวแทน. เหมาะเมื่อคุณต้องการทำให้ข้อมูลบริษัทเป็นนามธรรมก่อนแชร์เอกสารกับพันธมิตรภายนอก. กระบวนการลบข้อมูลจะไม่เปลี่ยนแปลงส่วนอื่นของเอกสาร, ทำให้การจัดวางและเนื้อหายังคงเหมือนเดิมหลังจากลบเมตา.

## ทำไมต้องใช้การลบข้อมูลเมตาด้วย GroupDocs?
การลบข้อมูลเมตาด้วย GroupDocs ให้วิธีที่เชื่อถือได้ในการลบข้อมูลที่ละเอียดอ่อนจากเอกสารพร้อมคงรูปลักษณ์และโครงสร้างเดิมไว้. ด้วยการมุ่งเน้นที่ฟิลด์เมตา, คุณสามารถปฏิบัติตามมาตรฐานความเป็นส่วนตัวได้อย่างรวดเร็วโดยไม่ต้องแก้ไขเนื้อหาที่มองเห็นหรือเสี่ยงต่อการรั่วไหลของข้อมูลโดยบังเอิญ.

- **ความแม่นยำ** – ลบข้อมูลเฉพาะฟิลด์ที่คุณระบุ, ปล่อยส่วนที่เหลือของเอกสารไม่ถูกแก้ไข.  
- **การปฏิบัติตาม** – ช่วยให้สอดคล้องกับ GDPR, HIPAA, และระเบียบความเป็นส่วนตัวอื่น ๆ โดยการลบตัวระบุที่ซ่อนอยู่.  
- **พร้อมอัตโนมัติ** – ผสานเข้ากับไพรไลน์การประมวลผลแบบแบตช์หรือไมโครเซอร์วิสได้อย่างราบรื่น.  
- **รองรับหลายรูปแบบ** – GroupDocs.Redaction รองรับ **รูปแบบเข้าและออกกว่า 50+** (รวมถึง DOCX, PDF, PPTX, XLSX, และประเภทภาพ) และสามารถประมวลผลไฟล์หลายร้อยหน้าโดยไม่ต้องโหลดเอกสารทั้งหมดเข้าสู่หน่วยความจำ.

## ข้อกำหนดเบื้องต้น
- **GroupDocs.Redaction for Java** ≥ 24.9.  
- Java 8 หรือใหม่กว่า ติดตั้งบนเครื่องของคุณ.  
- IDE เช่น IntelliJ IDEA หรือ Eclipse (ไม่บังคับแต่แนะนำ).  
- ความคุ้นเคยพื้นฐานกับ Maven (หรือความสามารถในการเพิ่ม JAR ด้วยตนเอง).

## การตั้งค่า GroupDocs.Redaction สำหรับ Java

เพิ่ม repository และ dependency ลงใน `pom.xml` ของคุณ. ขั้นตอนนี้ทำให้ Maven สามารถดาวน์โหลดไลบรารีโดยอัตโนมัติ.

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

*หรือคุณสามารถดาวน์โหลด JAR โดยตรงจากหน้าการปล่อยอย่างเป็นทางการ:*  
[การปล่อย GroupDocs.Redaction สำหรับ Java](https://releases.groupdocs.com/redaction/java/)

### การรับไลเซนส์
- **ทดลองใช้ฟรี** – ดาวน์โหลดไลเซนส์ทดลองเพื่อสำรวจคุณสมบัติทั้งหมด.  
- **ไลเซนส์ชั่วคราว** – ใช้สำหรับการทดสอบต่อเนื่อง.  
- **ไลเซนส์เต็ม** – จำเป็นสำหรับการใช้งานในสภาพแวดล้อมการผลิต.

## การเริ่มต้นพื้นฐาน
`Redactor` โหลดเอกสารและเปิดเผยเมธอดเพื่อใช้การลบข้อมูลหลายรูปแบบ.  
สร้างอินสแตนซ์ `Redactor` ที่ชี้ไปยังเอกสารที่คุณต้องการประมวลผล.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

## คู่มือการใช้งาน

### ขั้นตอนที่ 1: นำเข้าคลาสที่จำเป็น
การนำเข้าดังกล่าวทำให้คุณเข้าถึงเอนจินการลบข้อมูล, ตัวเลือกการบันทึก, และยูทิลิตี้เมตา.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.redactions.MetadataFilters;
import com.groupdocs.redaction.redactions.MetadataSearchRedaction;
```

### ขั้นตอนที่ 2: เริ่มต้น redactor
สร้างอินสแตนซ์ `Redactor` ด้วยพาธไปยังไฟล์ต้นฉบับของคุณ.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

### ขั้นตอนที่ 3: ตั้งค่าการค้นหาและลบข้อมูลเมตา
สร้าง `MetadataSearchRedaction` ที่ค้นหาสตริงที่ตรงกัน **"Company Ltd."** และแทนที่ด้วย **"--company--"**. การเรียก `setFilter` จะจำกัดการทำงานให้กับฟิลด์เมตา *Company* เท่านั้น.

```java
MetadataSearchRedaction redaction = new MetadataSearchRedaction("Company Ltd.", "--company--");
redaction.setFilter(MetadataFilters.Company);
```

### ขั้นตอนที่ 4: ใช้การลบข้อมูล
ดำเนินการลบข้อมูลบนเอกสารที่เปิดอยู่.

```java
redactor.apply(redaction);
```

### ขั้นตอนที่ 5: บันทึกด้วยตัวเลือกที่กำหนดเอง
`SaveOptions` ช่วยให้คุณระบุรูปแบบเอาต์พุต, การตั้งชื่อไฟล์, และพารามิเตอร์การบันทึกอื่น ๆ สำหรับเอกสารที่ลบข้อมูล.  
ตั้งค่า `SaveOptions` เพื่อให้ไฟล์ที่ลบข้อมูลมีส่วนต่อท้าย “_Redacted” พร้อมคงรูปแบบเดิม.

```java
SaveOptions tmp0 = new SaveOptions();
tmp0.setAddSuffix(true);  // Adds "_Redacted" to file name
tmp0.setRasterizeToPDF(false);  // Keeps original format

redactor.save(tmp0);
```

### ขั้นตอนที่ 6: ปล่อยทรัพยากร
ควรปิด `Redactor` เสมอเพื่อปล่อยทรัพยากรเนทีฟและหลีกเลี่ยงการรั่วไหลของหน่วยความจำ.

```java
finally {
    redactor.close();
}
```

## ปัญหาทั่วไปและวิธีแก้
- **FileNotFoundException** – ตรวจสอบพาธที่ส่งให้ `Redactor` อีกครั้ง. ใช้พาธแบบเต็มหรือ `Paths.get(...)` เพื่อความน่าเชื่อถือ.  
- **ไม่มีการเปลี่ยนแปลง** – ตรวจสอบว่าฟิลด์เมตาที่คุณเจาะจุดมีสตริงที่ค้นหาจริงหรือไม่; เมตาเป็นตัวพิมพ์ใหญ่‑เล็กโดยค่าเริ่มต้น.  
- **ข้อผิดพลาดหน่วยความจำไม่พอบนไฟล์ขนาดใหญ่** – ประมวลผลเอกสารเป็นชุดเล็ก ๆ และเรียก `redactor.close()` ทันทีหลังจากแต่ละไฟล์.

## การประยุกต์ใช้งานจริง
1. **เอกสารทางกฎหมาย** – ลบชื่อบริษัทของลูกค้าก่อนส่งสัญญาให้กับบุคคลที่สาม.  
2. **การรายงานทางการเงิน** – ทำให้ตัวระบุภายในเป็นนามธรรมในไฟล์การตรวจสอบ.  
3. **โครงการร่วมมือ** – ปกป้องข้อมูลที่เป็นกรรมสิทธิ์เมื่อแชร์ร่างงานกับผู้ขายภายนอก.

## ข้อควรพิจารณาด้านประสิทธิภาพ
- **การจัดการหน่วยความจำ** – ไลบรารีเก็บเอกสารทั้งหมดในหน่วยความจำ; การปิด `Redactor` หลังแต่ละไฟล์เป็นสิ่งสำคัญ.  
- **การประมวลผลแบบแบตช์** – สำหรับสถานการณ์ปริมาณสูง, วนลูปผ่านคอลเลกชันไฟล์และใช้ `SaveOptions` อินสแตนซ์เดียวซ้ำ.  
- **อัปเดตอยู่เสมอ** – รุ่นใหม่มาพร้อมการปรับปรุงประสิทธิภาพและแก้บั๊ก; ควรใช้เวอร์ชันเสถียรล่าสุดเสมอ.

## คำถามที่พบบ่อย

**Q: GroupDocs.Redaction for Java คืออะไร?**  
A: เป็นไลบรารีที่ทรงพลังที่ช่วยให้คุณลบข้อความ, เมตา, และรูปภาพในเอกสารโดยใช้แอปพลิเคชัน Java.

**Q: ฉันสามารถใช้ GroupDocs.Redaction ได้โดยไม่ซื้อไลเซนส์หรือไม่?**  
A: ได้, แต่มีข้อจำกัด. การทดลองใช้ฟรีหรือไลเซนส์ชั่วคราวให้การเข้าถึงเต็มรูปแบบเพื่อการทดสอบ.

**Q: ฉันจะทำให้รูปแบบเอกสารคงที่ระหว่างการลบข้อมูลได้อย่างไร?**  
A: ใช้ `SaveOptions` เพื่อระบุความต้องการของคุณ, เช่นหลีกเลี่ยงการแปลงเป็นภาพเมื่อต้องบันทึกเป็น PDF.

**Q: เอกสารประเภทใดบ้างที่สามารถลบข้อมูลด้วย GroupDocs.Redaction?**  
A: รองรับหลายประเภท, รวมถึง Word, Excel, PowerPoint, PDF, และอื่น ๆ อีกมาก.

**Q: ฉันจะหาแหล่งสนับสนุนได้จากที่ไหนหากเจอปัญหา?**  
A: เยี่ยมชม [ฟอรั่มสนับสนุน GroupDocs](https://forum.groupdocs.com/c/redaction/33) เพื่อขอความช่วยเหลือ.

**Q: MetadataSearchRedaction ทำงานกับเอกสารที่เข้ารหัสหรือไม่?**  
A: ใช่. โหลดเอกสารพร้อมรหัสผ่านที่เหมาะสมโดยใช้คอนสตรัคเตอร์ `Redactor` ที่รับพารามิเตอร์รหัสผ่าน.

**Q: ฉันสามารถเชื่อมต่อการลบข้อมูลเมตาหลายรายการในรอบเดียวได้หรือไม่?**  
A: แน่นอน. สร้างหลายอ็อบเจ็กต์ `MetadataSearchRedaction`, ตั้งค่าฟิลเตอร์ต่าง ๆ, และใช้พวกมันตามลำดับก่อนบันทึก.

**Q: สามารถดูตัวอย่างการลบข้อมูลก่อนบันทึกได้หรือไม่?**  
A: คุณสามารถเรียก `redactor.getRedactions()` เพื่อดึงรายการการลบข้อมูลที่ค้างอยู่และตรวจสอบโดยโปรแกรม.

## แหล่งข้อมูลเพิ่มเติม
- **Documentation**: สำรวจคู่มือโดยละเอียดที่ [เอกสาร GroupDocs](https://docs.groupdocs.com/redaction/java/).  
- **API reference**: ตรวจสอบอ้างอิง API ทั้งหมดบน [อ้างอิง API ของ GroupDocs](https://reference.groupdocs.com/redaction/java).  
- **Download library**: เข้าถึงรุ่นล่าสุดจาก [ดาวน์โหลด GroupDocs](https://releases.groupdocs.com/redaction/java/).  
- **Source code**: ดูและมีส่วนร่วมบน [GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).  
- **Support**: รับความช่วยเหลือผ่านช่องทางสนับสนุนฟรีที่ [ฟอรั่มสนับสนุน GroupDocs](https://forum.groupdocs.com/c/redaction/33).

---

**อัปเดตล่าสุด:** 2026-09-26  
**ทดสอบด้วย:** GroupDocs.Redaction 24.9 for Java  
**ผู้เขียน:** GroupDocs

## บทแนะนำที่เกี่ยวข้อง

- [การสกัดข้อมูลเมตาเอกสาร Java ของ Groupdocs Redaction](/redaction/java/metadata-redaction/groupdocs-redaction-java-document-metadata-extraction/)
- [แทนที่ข้อความเมตา java – การลบข้อมูลอย่างปลอดภัยด้วย GroupDocs](/redaction/java/metadata-redaction/java-redaction-metadata-text-replacement-guide/)
- [ดึงข้อมูลเอกสารโดยใช้ Groupdocs Redaction Java](/redaction/java/document-information/retrieve-document-info-using-groupdocs-redaction-java/)