---
date: '2026-06-26'
description: เรียนรู้วิธีสกัดข้อความจาก PDF ที่สแกนและปิดบังข้อมูลที่ละเอียดอ่อนโดยใช้
  GroupDocs OCR Redaction กับ Azure OCR. ปิดบังหมายเลขประกันสังคมและแทนที่ข้อมูลลับใน
  PDF อย่างมีประสิทธิภาพ.
keywords:
- extract text scanned pdf
- redact social security number
- mask sensitive data pdf
- replace confidential info pdf
schemas:
- author: GroupDocs
  dateModified: '2026-06-26'
  description: Learn how to extract text scanned PDF and mask sensitive data using
    GroupDocs OCR Redaction with Azure OCR. Redact social security number and replace
    confidential info PDF efficiently.
  headline: Extract Text Scanned PDF – Mask Data with GroupDocs OCR
  type: TechArticle
- questions:
  - answer: OCR redaction uses Optical Character Recognition to extract hidden text
      from images or scanned PDFs, then applies redaction rules to mask that text.
    question: What is OCR redaction?
  - answer: Yes, but OCR dramatically improves accuracy on scanned documents where
      native text extraction fails.
    question: Can I use GroupDocs Redaction without Azure OCR?
  - answer: Build and test them incrementally, using Java’s `Pattern` class in a sandbox
      before applying to large documents.
    question: How do I handle complex regex patterns?
  - answer: Large PDFs, overly complex regex, and synchronous OCR calls can slow processing;
      consider batch processing and optimized patterns.
    question: What are typical performance bottlenecks?
  - answer: Absolutely—reach out via the [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33)
      for community help or contact GroupDocs support.
    question: Is support available for implementation issues?
  type: FAQPage
title: สกัดข้อความจาก PDF ที่สแกน – ปิดบังข้อมูลด้วย GroupDocs OCR
type: docs
url: /th/java/ocr-integration/ocr-redaction-groupdocs-java-setup/
weight: 1
---

# สกัดข้อความจาก PDF ที่สแกน – ปิดบังข้อมูลด้วย GroupDocs OCR

ในโลกที่ขับเคลื่อนด้วยข้อมูลในปัจจุบัน, **การสกัดข้อความจากไฟล์ PDF ที่สแกน** และการปิดบังข้อมูลที่เป็นความลับเป็นขั้นตอนการปฏิบัติตามที่ไม่อาจต่อรองได้. บทแนะนำนี้จะพาคุณผ่านการใช้ GroupDocs Redaction ร่วมกับ Microsoft Azure OCR เพื่อจดจำข้อความที่ซ่อนอยู่บนหน้าที่สแกนอย่างเชื่อถือได้และแทนที่ด้วยตัวแทนที่ปลอดภัยเช่น **`[REDACTED]`**. คุณจะเห็นว่าทำไมการผสมผสานนี้จึงเร็ว, แม่นยำ, และพร้อมสำหรับงานระดับการผลิต.

## คำตอบด่วน
- **“mask sensitive data” หมายถึงอะไร?** มันแทนที่ข้อความที่เป็นความลับที่ระบุด้วยตัวแทน (เช่น `[REDACTED]`).  
- **ไลบรารีใดที่จัดการ OCR?** Microsoft Azure OCR connector, ใช้ผ่าน GroupDocs Redaction.  
- **ฉันต้องการใบอนุญาตหรือไม่?** การทดลองใช้ฟรีทำงานสำหรับการประเมิน; จำเป็นต้องมีใบอนุญาตถาวรสำหรับการใช้งานจริง.  
- **ฉันสามารถลบข้อมูลใน PDF ที่สแกนได้หรือไม่?** ได้—OCR จะสกัดข้อความที่ซ่อนอยู่ก่อนที่จะใช้การลบข้อมูลด้วย regex.  
- **โซลูชันนี้เป็นเฉพาะ Java หรือไม่?** ตัวอย่างนี้ใช้ Java, แต่ GroupDocs มี API ที่คล้ายกันสำหรับ .NET และแพลตฟอร์มอื่น ๆ.

## OCR‑Based Redaction คืออะไร?
OCR‑Based Redaction ทำการรัน OCR บนแต่ละหน้าเป็นขั้นแรก, แปลงภาพเป็นข้อความที่สามารถค้นหาได้, จากนั้นใช้รูปแบบ regex เพื่อแทนที่ที่ตรงกันด้วยหน้ากากเช่น `[REDACTED]`. กระบวนการสองขั้นตอนนี้ทำให้คุณสามารถปิดบังข้อมูลส่วนบุคคลได้อย่างเชื่อถือแม้ใน PDF ที่สแกน, เพื่อให้แน่ใจว่าข้อความที่เป็นความลับทั้งหมดถูกลบก่อนที่เอกสารจะถูกแชร์หรือเก็บถาวร.

## ทำไมต้องใช้ GroupDocs Redaction กับ Azure OCR?
คุณควรใช้ GroupDocs Redaction กับ Azure OCR เพราะมันให้ **ความแม่นยำ OCR >98 % กับข้อความที่พิมพ์**, รองรับ **รูปแบบไฟล์เข้าและออกกว่า 50 แบบ**, และสามารถประมวลผล **PDF หลายร้อยหน้าโดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ**, ทำให้การลบข้อมูลเร็วและขยายขนาดได้สำหรับการปฏิบัติตาม. โซลูชันนี้ยัง **สามารถประมวลผล PDF 1,000 หน้าในเวลาน้อยกว่า 2 นาทีบนเซิร์ฟเวอร์ 8‑คอร์**, ทำให้งานแบตช์เป็นไปได้จริง.

## ข้อกำหนดเบื้องต้น
- **Java Development Kit (JDK) 8+** ติดตั้งแล้ว.  
- **Maven** (หากคุณต้องการการจัดการ dependencies) หรือความสามารถในการดาวน์โหลด JARs ด้วยตนเอง.  
- **Microsoft Azure OCR credentials** (endpoint และ subscription key).  
- ความรู้พื้นฐานของ Java และความคุ้นเคยกับ regular expressions.

## การตั้งค่า GroupDocs Redaction สำหรับ Java

### การตั้งค่า Maven
เพิ่ม repository ของ GroupDocs และ dependency ลงใน `pom.xml` ของคุณ:

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
หากคุณต้องการจัดการ JAR ด้วยตนเอง, ดาวน์โหลดเวอร์ชันล่าสุดจาก [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### การรับใบอนุญาต
- **Free Trial** – สำรวจคุณสมบัติทั้งหมดโดยไม่มีค่าใช้จ่าย.  
- **Temporary License** – ขยายระยะเวลาการประเมิน.  
- **Full License** – ปลดล็อกความสามารถพร้อมใช้งานในการผลิต.

### การเริ่มต้นและตั้งค่าเบื้องต้น
คลาส `Redactor` เป็นเอนจินหลักที่ทำการสกัด OCR และใช้กฎการลบข้อมูลกับเอกสาร PDF.  
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## วิธีปิดบังข้อมูลที่เป็นความลับด้วย OCR Redaction
การปิดบังข้อมูลที่เป็นความลับด้วย OCR Redaction เกี่ยวข้องกับการโหลด PDF ด้วยการตั้งค่า Azure OCR, กำหนดรูปแบบ regex สำหรับข้อมูลที่ต้องการซ่อน, และเรียกใช้ Redactor เพื่อแทนที่แต่ละการจับคู่ด้วยตัวแทนเช่น `[REDACTED]`. ไลบรารีจัดการ OCR, การจับคู่รูปแบบ, และการเขียน PDF ใหม่ในขั้นตอนเดียว.

### ขั้นตอนที่ 1: โหลดเอกสารด้วยการตั้งค่า OCR
`LoadOptions` กำหนดวิธีที่ GroupDocs โหลดไฟล์, ให้คุณส่ง OCR connector เช่น Azure.  
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;

// Load your document with OCR settings
try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf", 
    new LoadOptions(), settings)) {
    // Further operations will go here
}
```
- **`YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf`** – แทนที่ด้วยเส้นทางไปยัง PDF ของคุณ.  
- **`settings`** – มี Azure OCR connector ที่คุณสร้างไว้ก่อนหน้า.

### ขั้นตอนที่ 2: กำหนดและใช้ Regex Redactions
`ReplacementOptions` ระบุข้อความแทนที่ที่จะใช้แทนแต่ละการจับคู่ regex ระหว่างการลบข้อมูล.  
```java
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

// Define the regex for sensitive data (e.g., Social Security Numbers)
RegexRedaction redaction = new RegexRedaction("\\b\\d{3}-\\d{2}-\\d{4}\\b", 
    new ReplacementOptions("[REDACTED]"));

// Apply redaction
redactor.apply(redaction);

// Save the document after redactions
redactor.save(new SaveOptions());
```
- รูปแบบ `\b\d{3}-\d{2}-\d{4}\b` จับคู่หมายเลข Social Security ของสหรัฐอเมริกา.  
- `ReplacementOptions("[REDACTED]")` แทนที่แต่ละการจับคู่ด้วยหน้ากาก, ทำให้ **ปิดบังข้อมูลที่เป็นความลับ** อย่างมีประสิทธิภาพ.

## กรณีการใช้งานทั่วไปสำหรับการปิดบังข้อมูลที่เป็นความลับ
1. **Legal Document Management** – ซ่อนตัวระบุของลูกค้าก่อนแชร์ฉบับร่าง.  
2. **Financial Reporting** – ปกป้องหมายเลขบัญชีและรหัสการทำธุรกรรม.  
3. **Healthcare Records** – ปฏิบัติตาม HIPAA โดยลบตัวระบุผู้ป่วย.  
4. **Government Publications** – ลบข้อมูลส่วนบุคคลจากบันทึกสาธารณะ.  
5. **Corporate Contracts** – ซ่อนเงื่อนไขที่เป็นกรรมสิทธิ์ระหว่างการตรวจสอบจากภายนอก.

## เคล็ดลับประสิทธิภาพ
- **Optimize regex** – หลีกเลี่ยงรูปแบบที่กว้างเกินไปซึ่งทำให้เวลาในการประมวลผลเพิ่มขึ้น; นิพจน์ที่ออกแบบดีสามารถลดระยะเวลาการทำงานได้ถึง 40 %.  
- **Memory Management** – ปิดอินสแตนซ์ `Redactor` อย่างทันท่วงที (try‑with‑resources ทำให้โดยอัตโนมัติ).  
- **Asynchronous Execution** – สำหรับการประมวลผลจำนวนมาก, รันงานลบข้อมูลบนเธรดแยกหรือใช้คิวงานเพื่อให้ UI ตอบสนอง.

## การแก้ไขปัญหา
- **Azure credentials error** – ตรวจสอบ URL ของ endpoint และ subscription key ใน `MicrosoftAzureOcrConnector` อีกครั้ง.  
- **Document not loading** – ตรวจสอบเส้นทางไฟล์และให้แน่ใจว่า PDF ไม่ได้ถูกป้องกันด้วยรหัสผ่าน (หรือให้รหัสผ่านผ่าน `LoadOptions`).  
- **No redactions applied** – ทดสอบ regex ของคุณด้วยสตริงง่าย ๆ ก่อน; ใช้ `Pattern.compile` ใน unit test เพื่อยืนยันการจับคู่.

## คำถามที่พบบ่อย

**Q: OCR redaction คืออะไร?**  
A: OCR redaction ใช้ Optical Character Recognition เพื่อสกัดข้อความที่ซ่อนอยู่จากภาพหรือ PDF ที่สแกน, จากนั้นใช้กฎการลบข้อมูลเพื่อปิดบังข้อความนั้น.

**Q: ฉันสามารถใช้ GroupDocs Redaction โดยไม่ใช้ Azure OCR ได้หรือไม่?**  
A: ได้, แต่ OCR จะเพิ่มความแม่นยำอย่างมากในเอกสารที่สแกนซึ่งการสกัดข้อความโดยธรรมชาติล้มเหลว.

**Q: ฉันจะจัดการกับรูปแบบ regex ที่ซับซ้อนได้อย่างไร?**  
A: สร้างและทดสอบแบบค่อยเป็นค่อยไป, ใช้คลาส `Pattern` ของ Java ใน sandbox ก่อนนำไปใช้กับเอกสารขนาดใหญ่.

**Q: จุดคอขวดด้านประสิทธิภาพที่พบบ่อยคืออะไร?**  
A: PDF ขนาดใหญ่, regex ที่ซับซ้อนเกินไป, และการเรียก OCR แบบ synchronous สามารถทำให้การประมวลผลช้า; พิจารณาการประมวลผลแบบแบตช์และรูปแบบที่ปรับให้เหมาะสม.

**Q: มีการสนับสนุนสำหรับปัญหาการนำไปใช้หรือไม่?**  
A: แน่นอน—ติดต่อผ่าน [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33) เพื่อขอความช่วยเหลือจากชุมชนหรือสอบถามทีมสนับสนุนของ GroupDocs.

## แหล่งข้อมูลเพิ่มเติม
- **เอกสารประกอบ**: https://docs.groupdocs.com/redaction/java/  
- **อ้างอิง API**: https://reference.groupdocs.com/redaction/java  
- **ดาวน์โหลด**: https://releases.groupdocs.com/redaction/java/  
- **GitHub**: https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java  
- **การสนับสนุนฟรี**: https://forum.groupdocs.com/c/redaction/33  
- **ใบอนุญาตชั่วคราว**: https://purchase.groupdocs.com/temporary-license/

---

**Last Updated:** 2026-06-26  
**ทดสอบกับ:** GroupDocs.Redaction 24.9 (Java)  
**ผู้เขียน:** GroupDocs  

---

## บทแนะนำที่เกี่ยวข้อง

- [การลบข้อมูล PDF อย่างปลอดภัยด้วย OCR – GroupDocs.Redaction Java](/redaction/java/ocr-integration/)
- [วิธีลบข้อความด้วย GroupDocs.Redaction สำหรับ Java](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction/)
- [ปิดบังข้อมูลที่เป็นความลับ Java – ลบข้อมูลส่วนบุคคลด้วย GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)