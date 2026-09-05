---
date: '2026-08-20'
description: เรียนรู้วิธีลบข้อความในเอกสาร Java ด้วย GroupDocs.Redaction ครอบคลุม
  exact‑phrase, regex, color replacement, annotation และ metadata redaction เพื่อการปฏิบัติตามที่ปลอดภัย
keywords:
- how to redact text
- replace text with color
- GroupDocs.Redaction Java
- Java document security
- document redaction library
lastmod: '2026-08-20'
og_description: เรียนรู้วิธีลบข้อความในเอกสาร Java ด้วย GroupDocs.Redaction ครอบคลุม
  exact‑phrase, regex, color replacement, annotation และ metadata redaction
og_image_alt: Guide showing Java code redacting text with GroupDocs.Redaction
og_title: วิธีลบข้อความในเอกสาร Java ด้วย GroupDocs.Redaction
schemas:
- author: GroupDocs
  dateModified: '2026-08-20'
  description: Learn how to redact text in Java documents using GroupDocs.Redaction,
    covering exact‑phrase, regex, color replacement, annotation and metadata redaction
    for secure compliance.
  headline: How to redact text in Java documents with GroupDocs.Redaction
  type: TechArticle
- description: Learn how to redact text in Java documents using GroupDocs.Redaction,
    covering exact‑phrase, regex, color replacement, annotation and metadata redaction
    for secure compliance.
  name: How to redact text in Java documents with GroupDocs.Redaction
  steps:
  - name: '**Add the Maven dependency** (or include the JAR).'
    text: '**Add the Maven dependency** (or include the JAR).'
  - name: '**Configure your license** by calling `License.setLicense("path/to/license.lic")`
      early in your application.'
    text: '**Configure your license** by calling `License.setLicense("path/to/license.lic")`
      early in your application.'
  - name: '**Create a `Redactor` instance** pointing at the source document.'
    text: '**Create a `Redactor` instance** pointing at the source document.'
  - name: '**Initialize the Redactor** with the document you want to process:'
    text: '**Initialize the Redactor** with the document you want to process:'
  - name: '**Define the exact‑phrase rule** and apply it:'
    text: '**Define the exact‑phrase rule** and apply it:'
  - name: '**Save the redacted file** to your output folder:'
    text: '**Save the redacted file** to your output folder:'
  - name: 'Load the document:'
    text: 'Load the document:'
  - name: 'Create a regex rule and apply it:'
    text: 'Create a regex rule and apply it:'
  - name: 'Save the result:'
    text: 'Save the result:'
  - name: 'Load the document:'
    text: 'Load the document:'
  type: HowTo
- questions:
  - answer: Yes. Create each redaction object, call `redactor.apply()` for each, then
      save once.
    question: Can I combine multiple redaction rules in a single pass?
  - answer: Absolutely. Pass the password to the `Redactor` constructor that accepts
      a `LoadOptions` object.
    question: Does GroupDocs.Redaction support password‑protected files?
  - answer: You can call `redactor.preview()` to generate a temporary view that highlights
      the areas to be redacted.
    question: Is it possible to preview redactions before saving?
  - answer: DOCX, PDF, PPTX, XLSX, PNG, JPEG, BMP, and many more—over 30 formats in
      total.
    question: What file formats are supported?
  - answer: Use the metadata erasure feature, remove annotations, and apply exact‑phrase
      or regex redactions to all personal data fields.
    question: How do I ensure the redacted document complies with GDPR?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java document security
- regex redaction
- metadata removal
title: วิธีลบข้อความในเอกสาร Java ด้วย GroupDocs.Redaction
type: docs
url: /th/java/text-redaction/java-redaction-guide-groupdocs-document-security/
weight: 1
---

# วิธีการทำลบข้อความในเอกสาร Java ด้วย GroupDocs.Redaction

ในแอปพลิเคชันสมัยใหม่, **วิธีการทำลบข้อความ** ภายใน PDF, ไฟล์ Word หรือรูปภาพเป็นความต้องการที่พบบ่อยเพื่อการปฏิบัติตามกฎระเบียบและความเป็นส่วนตัว. ไม่ว่าคุณจะต้องการซ่อนข้อมูลส่วนบุคคล, ลบคำอธิบายที่เป็นความลับ, หรือกำจัดเมตาดาต้า, GroupDocs.Redaction for Java จะมอบวิธีที่สะอาดและโปรแกรมเมติกเพื่อให้บรรลุ **java document security**. บทแนะนำนี้จะพาคุณผ่านทุกขั้นตอนสำคัญ—ตั้งแต่การตั้งค่าห้องสมุดไปจนถึงการใช้การทำลบแบบ exact‑phrase, regex, color‑based, annotation, และ metadata—เพื่อให้คุณสามารถฝังการทำลบลงในบริการ backend ของคุณได้โดยตรง.

## คำตอบอย่างรวดเร็ว
- **ไลบรารีใดที่จัดการการทำลบเอกสาร Java?** GroupDocs.Redaction for Java.  
- **ฉันสามารถแทนที่ข้อความด้วยสีแทนการลบได้หรือไม่?** ใช่, ใช้ฟีเจอร์ “replace text with color”.  
- **ฉันต้องการไลเซนส์สำหรับการใช้งานในผลิตภัณฑ์หรือไม่?** จำเป็นต้องมีไลเซนส์ชั่วคราวหรือแบบชำระเงินเพื่อใช้งานเต็มรูปแบบ.  
- **เวอร์ชัน Java ที่รองรับคืออะไร?** JDK 8 หรือสูงกว่า.  
- **Maven เป็นวิธีเดียวในการเพิ่มไลบรารีหรือไม่?** แนะนำให้ใช้ Maven, แต่คุณก็สามารถดาวน์โหลด JAR ด้วยตนเองได้.

## “วิธีการทำลบข้อความ” ใน Java คืออะไร?
**Redaction permanently removes or obscures sensitive content so it cannot be recovered.** ใน Java, คุณโหลดไฟล์, กำหนดสิ่งที่ต้องซ่อน, ใช้การทำลบ, และบันทึกเวอร์ชันที่ทำความสะอาดแล้ว. สิ่งนี้ทำให้ผู้รับต่อไปเห็นเฉพาะเอกสารที่ทำความสะอาดแล้ว.

## ทำไมต้องใช้ GroupDocs.Redaction for Java?
โหลดไฟล์ของคุณ, กำหนดกฎ, และ SDK จะจัดการงานที่หนัก. GroupDocs.Redaction รองรับ **30+ รูปแบบ**—รวมถึง DOCX, PDF, PPTX, XLSX, PNG, JPEG, BMP—และประมวลผลเอกสารขนาดใหญ่ผ่านสถาปัตยกรรมแบบ stream. มันมีการทำลบแบบ exact‑phrase, regex, color‑based, annotation, และ metadata, ให้การควบคุมละเอียดเพื่อให้สอดคล้องกับ GDPR, HIPAA, และกฎระเบียบอื่นๆ.

## ข้อกำหนดเบื้องต้น
- **Java Development Kit (JDK) 8+** ติดตั้งบนเครื่องของคุณ.  
- **Maven** สำหรับการจัดการ dependencies (หรือคุณสามารถดาวน์โหลด JAR ด้วยตนเอง).  

### ไลบรารีและ dependencies ที่จำเป็น
เพิ่ม repository ของ GroupDocs และ dependency ของ Redaction ไปยัง `pom.xml` ของคุณ:

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

คุณยังสามารถดาวน์โหลด JAR ล่าสุดจากหน้า release อย่างเป็นทางการ: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### การรับไลเซนส์
สำหรับการใช้งานในผลิตภัณฑ์, ขอรับไลเซนส์ชั่วคราวหรือเต็ม. มีการทดลองใช้ฟรีสำหรับการประเมิน.

## การตั้งค่า GroupDocs.Redaction for Java
1. **เพิ่ม Maven dependency** (หรือรวม JAR).  
2. **กำหนดค่าไลเซนส์ของคุณ** โดยเรียก `License.setLicense("path/to/license.lic")` ตั้งแต่ต้นในแอปพลิเคชันของคุณ. `License` เป็นคลาสที่ใช้โหลดและใช้ไฟล์ไลเซนส์ของ GroupDocs Redaction.  
3. **สร้างอินสแตนซ์ `Redactor`** ที่ชี้ไปที่เอกสารต้นฉบับ.

**คลาส `Redactor` เป็นเอนจินหลักที่โหลด, แก้ไข, และบันทึกเอกสารอย่างมีประสิทธิภาพด้านหน่วยความจำ.** เมื่อคุณมีอ็อบเจ็กต์ `Redactor`, คุณสามารถต่อหลายกฎการทำลบก่อนบันทึกผลลัพธ์.

ตอนนี้คุณพร้อมเริ่มทำลบแล้ว.

## คู่มือการใช้งาน

### การทำลบแบบ Exact phrase
แทนที่วลีเฉพาะ (เช่น ชื่อของบุคคล) ด้วยข้อความ placeholder.

#### การทำงานของการทำลบแบบ exact‑phrase คืออย่างไร?
`ExactPhraseRedaction` แสดงถึงกฎที่ลบหรือแทนที่สตริงข้อความที่ตรงกันอย่างเฉพาะเจาะจง. โหลดเอกสาร, สร้างกฎ `ExactPhraseRedaction` ที่มุ่งเป้าไปที่สตริงนั้น, ใช้กฎ, และบันทึกผลลัพธ์. SDK จะลบข้อความที่ตรงกันโดยอัตโนมัติพร้อมคงรูปแบบ.

1. **Initialize the Redactor** กับเอกสารที่คุณต้องการประมวลผล:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. **Define the exact‑phrase rule** และใช้มัน:

```java
ExactPhraseRedaction redaction = new ExactPhraseRedaction(
    "John Doe", 
    new ReplacementOptions("[Client]"));

redactor.apply(redaction);
```

3. **Save the redacted file** ไปยังโฟลเดอร์ผลลัพธ์ของคุณ:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Redaction applied successfully.");
}
```

### การทำลบแบบ Regex พร้อมการแทนที่ข้อความ
ใช้ regular expressions เพื่อค้นหารูปแบบเช่นหมายเลขซีเรียลและแทนที่ด้วยโทเค็นทั่วไป.

#### การทำงานของการทำลบแบบ regex พร้อมการแทนที่คืออย่างไร?
`RegexRedaction` กำหนดกฎโดยอิงจาก regular expression เพื่อค้นหาและแก้ไขข้อความที่ตรงกัน. คุณให้วัตถุ `RegexRedaction` ที่มี pattern และสตริงการแทนที่. เอนจินสแกนเอกสาร, แทนที่ทุกการจับคู่, และคงรูปแบบโดยรอบ.

1. โหลดเอกสาร:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. สร้างกฎ regex และใช้มัน:

```java
RegexRedaction redaction = new RegexRedaction(
    "Redaction",
    new ReplacementOptions("[Product]"));

redactor.apply(redaction);
```

3. บันทึกผลลัพธ์:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Redaction applied successfully.");
}
```

### การทำลบแบบ Regex พร้อมการแทนที่ด้วยสี
แทนที่จะลบข้อความ, คุณสามารถ **replace text with color** เพื่อทำให้มองไม่เห็นโดยยังคงอักขระเดิมอยู่.

#### การทำลบแบบ color‑based แตกต่างจากการลบอย่างไร?
SDK จะทาสีข้อความที่ตรงกับสีที่เลือก, ทำให้มนุษย์อ่านไม่ออกแต่ยังคงอยู่ในสตรีมไฟล์. มีประโยชน์เมื่อคุณต้องการคงโครงสร้างเอกสารสำหรับการประมวลผลต่อไป.

1. โหลดเอกสาร:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. กำหนด pattern regex และตั้งค่าสีแทนที่ (เช่น สีฟ้า):

```java
RegexRedaction redaction = new RegexRedaction(
    "\d{2}\s*\d{2}[^\\d]*\d{6}", 
    new ReplacementOptions(Color.BLUE));

redactor.apply(redaction);
```

3. บันทึกไฟล์ที่อัปเดต:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Redaction applied successfully.");
}
```

### การทำลบ Annotation
ลบ annotation ทั้งหมด (คอมเมนต์, ไฮไลท์, ฯลฯ) จากเอกสารเพื่อให้ได้เวอร์ชันสุดท้ายที่สะอาดขึ้น.

#### วิธีลบ annotation ในขั้นตอนเดียว?
`AnnotationRedaction` เป็นกฎที่ลบ annotation เช่น คอมเมนต์, ไฮไลท์, และสแตมป์. สร้างกฎ `AnnotationRedaction` ที่มุ่งเป้าไปที่ทุกประเภทของ annotation, ใช้กฎ, และบันทึกการเปลี่ยนแปลง.

1. โหลดไฟล์ของคุณ:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. ใช้กฎการลบ annotation:

```java
DeleteAnnotationRedaction redaction = new DeleteAnnotationRedaction();

redactor.apply(redaction);
```

3. บันทึกการเปลี่ยนแปลง:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Annotations deleted successfully.");
}
```

### การทำลบ Metadata
ลบ metadata ทุกส่วน (ผู้เขียน, วันที่สร้าง, คุณสมบัติกำหนดเอง) เพื่อปกป้องความเป็นส่วนตัวและสอดคล้องกับมาตรฐานการปฏิบัติตาม.

#### การลบ metadata ทำให้ความเป็นส่วนตัวได้รับการรับประกันอย่างไร?
`MetadataRedaction` ลบฟิลด์ metadata ที่ built‑in และ custom จากเอกสาร. กฎ `MetadataRedaction` ทำความสะอาดฟิลด์ metadata ทั้ง built‑in และ custom, ทำให้ไม่มีตัวระบุที่ซ่อนอยู่ใน property bag ของไฟล์.

1. เปิดเอกสาร:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. ใช้กฎการลบ metadata:

```java
EraseMetadataRedaction redaction = new EraseMetadataRedaction(MetadataFilters.All);

redactor.apply(redaction);
```

3. บันทึกเอกสารที่ทำความสะอาดแล้ว:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Metadata erased successfully.");
}
```

## การประยุกต์ใช้งานจริง (ทำไมจึงสำคัญ)
- **Legal document preparation** – ลบชื่อของลูกค้าก่อนแชร์ร่างให้ฝ่ายตรงข้าม.  
- **Healthcare compliance** – ลบข้อมูลระบุตัวผู้ป่วยเพื่อให้สอดคล้องกับ HIPAA โดยไม่ต้องแก้ไขด้วยมือ.  
- **Corporate data protection** – ซ่อนตัวเลขทางการเงินหรือความลับทางการค้าในรายงานภายในก่อนการแจกจ่าย.  

การทำอัตโนมัติขั้นตอนเหล่านี้ช่วยลดความพยายามด้วยมือ, กำจัดข้อผิดพลาดของมนุษย์, และทำให้การปฏิบัติตามสม่ำเสมอในหลายพันไฟล์.

## พิจารณาด้านประสิทธิภาพ
- **Stream instead of load** – สำหรับไฟล์ขนาดใหญ่, ใช้คอนสตรัคเตอร์ `Redactor` ที่รับ `InputStream` เพื่อหลีกเลี่ยงการโหลดเอกสารทั้งหมดเข้าสู่หน่วยความจำ.  
- **Pre‑compile regex patterns** เมื่อคุณทำการทำลบเดียวกันหลายครั้ง; จะลดภาระ CPU ได้ถึง 30 %.  
- **Monitor JVM heap** – การทำลบอาจใช้หน่วยความจำมาก; พิจารณาเพิ่มขนาด heap (`-Xmx2g`) สำหรับการประมวลผลเป็นชุดของไฟล์หลายกิกะไบต์.

## ปัญหาทั่วไป & การแก้ไข
| อาการ | สาเหตุที่เป็นไปได้ | วิธีแก้ไข |
|---------|--------------|-----|
| ไม่มีการเปลี่ยนแปลงหลังจาก `apply` | เส้นทางไฟล์ผิดหรือไฟล์ถูกล็อก | ตรวจสอบเส้นทางไฟล์และให้แน่ใจว่าเอกสารไม่ได้เปิดที่อื่น |
| Regex ไม่ตรง | ข้อผิดพลาดไวยากรณ์ของ pattern | ทดสอบ regex ด้วยเครื่องมือออนไลน์; หนีบ backslashes อย่างถูกต้อง |
| การแทนที่สีไม่แสดง | รูปแบบเอาต์พุตไม่รองรับสีข้อความ (เช่น plain text) | ใช้รูปแบบเช่น DOCX หรือ PDF ที่คงสไตล์ |
| ข้อผิดพลาดไลเซนส์ขณะรัน | ไฟล์ไลเซนส์หายหรือไม่ถูกต้อง | วางไฟล์ `.lic` ในไดเรกทอรีที่เข้าถึงได้และเรียก `License.setLicense` ก่อนใช้ Redactor ใดๆ |

## คำถามที่พบบ่อย

**Q: ฉันสามารถรวมหลายกฎการทำลบในหนึ่งรอบได้หรือไม่?**  
A: ใช่. สร้างอ็อบเจ็กต์การทำลบแต่ละอัน, เรียก `redactor.apply()` สำหรับแต่ละอัน, แล้วบันทึกครั้งเดียว.

**Q: GroupDocs.Redaction รองรับไฟล์ที่มีรหัสผ่านหรือไม่?**  
A: แน่นอน. ส่งรหัสผ่านไปยังคอนสตรัคเตอร์ `Redactor` ที่รับอ็อบเจ็กต์ `LoadOptions`.

**Q: สามารถดูตัวอย่างการทำลบก่อนบันทึกได้หรือไม่?**  
A: คุณสามารถเรียก `redactor.preview()` เพื่อสร้างมุมมองชั่วคราวที่ไฮไลท์พื้นที่ที่จะทำลบ.

**Q: รองรับรูปแบบไฟล์อะไรบ้าง?**  
A: DOCX, PDF, PPTX, XLSX, PNG, JPEG, BMP, และอื่นๆ อีกมาก—รวมกว่า 30 รูปแบบทั้งหมด.

**Q: ฉันจะทำให้เอกสารที่ทำลบสอดคล้องกับ GDPR อย่างไร?**  
A: ใช้ฟีเจอร์การลบ metadata, ลบ annotation, และใช้การทำลบแบบ exact‑phrase หรือ regex กับฟิลด์ข้อมูลส่วนบุคคลทั้งหมด.

## สรุป
คุณมีคู่มือครบวงจรจากต้นจนจบเกี่ยวกับ **วิธีการทำลบข้อความ** ในเอกสาร Java ด้วย GroupDocs.Redaction. ด้วยการทำตามขั้นตอนสำหรับการทำลบแบบ exact‑phrase, regex, color‑based, annotation, และ metadata, คุณสามารถบรรลุ **java document security** ที่แข็งแกร่งพร้อมกับโค้ดที่สะอาดและดูแลได้ง่าย. ผสานสคริปต์เหล่านี้เข้ากับบริการที่มีอยู่ของคุณ, ทำอัตโนมัติการประมวลผลเป็นชุด, และรักษาการปฏิบัติตามกฎระเบียบความเป็นส่วนตัว.

---

**Last Updated:** 2026-08-20  
**Tested with:** GroupDocs.Redaction 24.9 for Java  
**Author:** GroupDocs

## บทแนะนำที่เกี่ยวข้อง

- [แทนที่ข้อความเมตาดาต้า java – Secure Redaction with GroupDocs](/redaction/java/metadata-redaction/java-redaction-metadata-text-replacement-guide/)
- [วิธีทำลบภาพในเอกสาร Word ด้วย GroupDocs.Redaction for Java – คู่มือครบวงจร](/redaction/java/image-redaction/redact-images-word-docs-groupdocs-redaction-java/)
- [วิธีทำลบเอกสารด้วย GroupDocs Redaction Java License จากเส้นทางไฟล์ – คู่มือขั้นตอนโดยละเอียด](/redaction/java/licensing-configuration/implement-groupdocs-redaction-java-license-file-path/)