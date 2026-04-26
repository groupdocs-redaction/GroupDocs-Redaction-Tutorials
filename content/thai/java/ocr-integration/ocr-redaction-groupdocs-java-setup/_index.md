---
date: '2026-02-08'
description: เรียนรู้วิธีปกปิดข้อมูลที่ละเอียดอ่อนและทำการลบข้อมูลในไฟล์ PDF Java
  ด้วย GroupDocs OCR Redaction พร้อม Microsoft Azure OCR.
keywords:
- OCR-based redactions Java
- GroupDocs Redaction setup
- regex-based text redaction
title: ปกปิดข้อมูลที่ละเอียดอ่อนในไฟล์ PDF ด้วย GroupDocs OCR Redaction
type: docs
url: /th/java/ocr-integration/ocr-redaction-groupdocs-java-setup/
weight: 1
---

# ซ่อนข้อมูลที่ละเอียดอ่อนใน PDF ด้วย GroupDocs OCR Redaction

ในยุคดิจิทัลปัจจุบัน การปกป้องข้อมูลส่วนบุคคลและข้อมูลที่เป็นความลับเป็นสิ่งสำคัญอันดับแรก ในบทแนะนำนี้ **คุณจะได้เรียนรู้วิธีซ่อนข้อมูลที่ละเอียดอ่อน** ในไฟล์ PDF โดยการผสาน GroupDocs Redaction กับ Microsoft Azure OCR วิธีนี้ให้การจดจำข้อความที่เชื่อถือได้บนหน้าที่สแกนและช่วยให้คุณ **ทำการลบข้อมูลใน PDF Java** อย่างแม่นยำ เพื่อให้สอดคล้องกับกฎระเบียบความเป็นส่วนตัว

## คำตอบอย่างรวดเร็ว
- **“mask sensitive data” หมายถึงอะไร?** มันจะแทนที่ข้อความที่เป็นความลับที่ระบุไว้ด้วยตัวแทน (เช่น `[REDACTED]`).  
- **ไลบรารีใดที่จัดการ OCR?** Microsoft Azure OCR connector, ใช้ผ่าน GroupDocs Redaction.  
- **ฉันต้องการไลเซนส์หรือไม่?** การทดลองใช้ฟรีทำงานสำหรับการประเมิน; จำเป็นต้องมีไลเซนส์ถาวรสำหรับการใช้งานจริง.  
- **ฉันสามารถลบข้อมูลใน PDF ที่สแกนได้หรือไม่?** ได้—OCR จะสกัดข้อความที่ซ่อนอยู่ก่อนที่จะใช้การลบด้วย regex.  
- **โซลูชันนี้เป็นเฉพาะ Java หรือไม่?** ตัวอย่างนี้ใช้ Java, แต่ GroupDocs มี API ที่คล้ายกันสำหรับ .NET และแพลตฟอร์มอื่น ๆ.

## OCR‑Based Redaction คืออะไร?
OCR‑based redaction จะทำการรัน Optical Character Recognition บนแต่ละหน้าของเอกสารก่อน, แปลงภาพของข้อความให้เป็นสตริงที่สามารถค้นหาได้ เมื่อข้อความสามารถค้นหาได้แล้ว คุณสามารถใช้กฎ regular‑expression (regex) เพื่อค้นหาข้อมูลที่ละเอียดอ่อน—เช่น หมายเลขประกันสังคม, หมายเลขบัตรเครดิต, หรือข้อมูลระบุตัวตนส่วนบุคคล—และแทนที่ด้วยหน้ากากเช่น **`[REDACTED]`**.

## ทำไมต้องใช้ GroupDocs Redaction กับ Azure OCR?
- **ความแม่นยำสูง** สำหรับ PDF และภาพที่สแกน  
- **การผสานรวม Java อย่างราบรื่น** ผ่าน Maven หรือการดาวน์โหลด JAR โดยตรง  
- **เครื่องมือ regex ที่ยืดหยุ่น** ช่วยให้คุณกำหนดรูปแบบที่กำหนดเองสำหรับข้อมูลประเภทใดก็ได้  
- **สามารถขยายได้** สำหรับชุดเอกสารขนาดใหญ่ พร้อมตัวเลือกการประมวลผลแบบอะซิงโครนัส

## ข้อกำหนดเบื้องต้น
- **Java Development Kit (JDK) 8+** ติดตั้งแล้ว  
- **Maven** (หากคุณต้องการจัดการ dependencies) หรือความสามารถในการดาวน์โหลด JAR ด้วยตนเอง  
- **ข้อมูลรับรอง Microsoft Azure OCR** (endpoint และ subscription key)  
- ความรู้พื้นฐานของ Java และความคุ้นเคยกับ regular expressions

## การตั้งค่า GroupDocs Redaction สำหรับ Java

### การตั้งค่า Maven
เพิ่มรีโพซิทอรีของ GroupDocs และ dependency ลงใน `pom.xml` ของคุณ:

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
หากคุณต้องการจัดการ JAR ด้วยตนเอง ให้ดาวน์โหลดเวอร์ชันล่าสุดจาก [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### การรับไลเซนส์
- **Free Trial** – สำรวจคุณสมบัติทั้งหมดโดยไม่มีค่าใช้จ่าย.  
- **Temporary License** – ขยายระยะเวลาการประเมิน.  
- **Full License** – ปลดล็อกความสามารถพร้อมใช้งานในสภาพแวดล้อมการผลิต.

### การเริ่มต้นและตั้งค่าเบื้องต้น
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## วิธีการซ่อนข้อมูลที่ละเอียดอ่อนด้วย OCR Redaction

### ขั้นตอนที่ 1: โหลดเอกสารพร้อมการตั้งค่า OCR
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
- **`LoadOptions`** – การโหลดค่าเริ่มต้น; คุณสามารถปรับแต่งได้หากต้องการ.  
- **`settings`** – มี Azure OCR connector ที่คุณสร้างไว้ก่อนหน้านี้.

### ขั้นตอนที่ 2: กำหนดและใช้ Regex Redactions
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
- รูปแบบ `\b\d{3}-\d{2}-\d{4}\b` ตรงกับหมายเลข Social Security ของสหรัฐอเมริกา.  
- `ReplacementOptions("[REDACTED]")` จะเปลี่ยนแต่ละการจับคู่เป็นหน้ากาก, ทำให้ **ซ่อนข้อมูลที่ละเอียดอ่อน** อย่างมีประสิทธิภาพ.

## กรณีการใช้งานทั่วไปสำหรับการซ่อนข้อมูลที่ละเอียดอ่อน
1. **Legal Document Management** – ซ่อนตัวระบุของลูกค้าก่อนแชร์ฉบับร่าง.  
2. **Financial Reporting** – ปกป้องหมายเลขบัญชีและรหัสการทำธุรกรรม.  
3. **Healthcare Records** – ปฏิบัติตาม HIPAA โดยลบตัวระบุผู้ป่วย.  
4. **Government Publications** – ลบข้อมูลส่วนบุคคลจากบันทึกสาธารณะ.  
5. **Corporate Contracts** – ปกปิดเงื่อนไขที่เป็นกรรมสิทธิ์ในระหว่างการตรวจสอบจากภายนอก.

## เคล็ดลับการเพิ่มประสิทธิภาพ
- **ปรับแต่ง regex** – หลีกเลี่ยงรูปแบบที่กว้างเกินไปซึ่งทำให้เวลาในการประมวลผลเพิ่มขึ้น.  
- **การจัดการหน่วยความจำ** – ปิดอินสแตนซ์ `Redactor` อย่างทันท่วงที (try‑with‑resources ทำให้โดยอัตโนมัติ).  
- **การดำเนินการแบบอะซิงโครนัส** – สำหรับการประมวลผลเป็นชุด, รันงานลบข้อมูลบนเธรดแยกหรือใช้คิวงาน.

## การแก้ไขปัญหา
- **ข้อผิดพลาดข้อมูลรับรอง Azure** – ตรวจสอบ URL ของ endpoint และ subscription key ใน `MicrosoftAzureOcrConnector` อีกครั้ง.  
- **ไม่สามารถโหลดเอกสาร** – ตรวจสอบเส้นทางไฟล์และให้แน่ใจว่า PDF ไม่ได้ถูกป้องกันด้วยรหัสผ่าน (หรือระบุรหัสผ่านผ่าน `LoadOptions`).  
- **ไม่มีการลบข้อมูลใด ๆ** – ทดสอบ regex ของคุณกับสตริงง่าย ๆ ก่อน; ใช้ `Pattern.compile` ใน unit test เพื่อยืนยันการจับคู่.

## คำถามที่พบบ่อย

**Q: OCR redaction คืออะไร?**  
A: OCR redaction ใช้ Optical Character Recognition เพื่อสกัดข้อความที่ซ่อนอยู่จากภาพหรือ PDF ที่สแกน, จากนั้นใช้กฎการลบข้อมูลเพื่อซ่อนข้อความนั้น.

**Q: ฉันสามารถใช้ GroupDocs Redaction โดยไม่ใช้ Azure OCR ได้หรือไม่?**  
A: ได้, แต่ OCR จะเพิ่มความแม่นยำอย่างมากในเอกสารที่สแกนซึ่งการสกัดข้อความแบบดั้งเดิมล้มเหลว.

**Q: ฉันจะจัดการกับรูปแบบ regex ที่ซับซ้อนได้อย่างไร?**  
A: สร้างและทดสอบอย่างเป็นขั้นเป็นตอน, ใช้คลาส `Pattern` ของ Java ใน sandbox ก่อนนำไปใช้กับเอกสารขนาดใหญ่.

**Q: จุดคอขวดด้านประสิทธิภาพที่พบบ่อยคืออะไร?**  
A: PDF ขนาดใหญ่, regex ที่ซับซ้อนเกินไป, และการเรียก OCR แบบ synchronous สามารถทำให้การประมวลผลช้า; พิจารณาการประมวลผลเป็นชุดและรูปแบบที่ปรับแต่งแล้ว.

**Q: มีการสนับสนุนสำหรับปัญหาการนำไปใช้หรือไม่?**  
A: แน่นอน—ติดต่อผ่าน [ฟอรั่ม GroupDocs](https://forum.groupdocs.com/c/redaction/33) เพื่อขอความช่วยเหลือจากชุมชนหรือสอบถามฝ่ายสนับสนุนของ GroupDocs.

## แหล่งข้อมูลเพิ่มเติม
- **เอกสาร**: https://docs.groupdocs.com/redaction/java/  
- **อ้างอิง API**: https://reference.groupdocs.com/redaction/java  
- **ดาวน์โหลด**: https://releases.groupdocs.com/redaction/java/  
- **GitHub**: https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java  
- **การสนับสนุนฟรี**: https://forum.groupdocs.com/c/redaction/33  
- **Temporary License**: https://purchase.groupdocs.com/temporary-license/

---

**อัปเดตล่าสุด:** 2026-02-08  
**ทดสอบด้วย:** GroupDocs.Redaction 24.9 (Java)  
**ผู้เขียน:** GroupDocs