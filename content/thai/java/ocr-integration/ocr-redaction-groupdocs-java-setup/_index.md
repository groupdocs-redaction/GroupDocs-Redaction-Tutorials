---
date: '2026-01-21'
description: เรียนรู้วิธีลบข้อมูลใน PDF ด้วย OCR และลบข้อมูลในเอกสารสแกนโดยใช้ GroupDocs.Redaction
  สำหรับ Java พร้อมการผสานรวม Azure OCR.
keywords:
- OCR-based redactions Java
- GroupDocs Redaction setup
- regex-based text redaction
title: ทำการลบข้อมูลใน PDF ด้วย OCR โดยใช้ GroupDocs และ Azure OCR – คู่มือ Java
type: docs
url: /th/java/ocr-integration/ocr-redaction-groupdocs-java-setup/
weight: 1
---

# ลบข้อมูลใน PDF ด้วย OCR โดยใช้ GroupDocs & Azure OCR – คู่มือ Java

ในบทแนะนำที่ครอบคลุมนี้คุณจะได้ค้นพบวิธี **redact PDF with OCR** ด้วย Java โดยใช้ GroupDocs.Redaction ร่วมกับ Microsoft Azure OCR ไม่ว่าคุณจะทำงานกับ PDF แบบดั้งเดิมหรือภาพสแกน คู่มือนี้จะแสดงให้คุณเห็นวิธีการระบุตำแหน่งและปิดบังข้อมูลที่ละเอียดอ่อนอย่างแม่นยำ เพื่อช่วยให้คุณ **redact scanned documents** ให้สอดคล้องกับกฎระเบียบด้านความเป็นส่วนตัว

## คำตอบด่วน
- **OCR redaction ทำอะไร?** มันจะสกัดข้อความจากรูปภาพ/PDF แล้วใช้กฎการลบข้อมูลโดยอัตโนมัติ  
- **ไลบรารีใดที่ให้เครื่องยนต์การลบข้อมูล?** GroupDocs.Redaction for Java  
- **บริการ OCR ใดที่ใช้?** Microsoft Azure OCR connector  
- **ฉันต้องการไลเซนส์หรือไม่?** ทดลองใช้ฟรีได้สำหรับการทดสอบ; ต้องมีไลเซนส์ถาวรสำหรับการใช้งานจริง  
- **ฉันสามารถลบข้อมูลใน PDF ทั้งแบบดั้งเดิมและแบบสแกนได้หรือไม่?** ใช่ – OCR ทำให้สามารถลบข้อมูลในเอกสารสแกนได้เช่นกัน  

## “Redact PDF with OCR” คืออะไร?
การลบข้อมูลใน PDF ด้วย OCR หมายถึงการใช้การจดจำอักขระด้วยแสง (optical character recognition) เพื่อแปลงข้อความที่มองเห็นเป็นสตริงที่ค้นหาได้ จากนั้นจึงใช้รูปแบบการลบข้อมูล (เช่น regex) เพื่อซ่อนข้อมูลนั้นก่อนที่ไฟล์จะถูกแชร์หรือเก็บไว้

## ทำไมต้องใช้ GroupDocs.Redaction กับ Azure OCR?
- **ความแม่นยำสูง** บนหน้าที่สแกนโดยขอบคุณเครื่อง OCR บนคลาวด์ของ Azure  
- **Simple Java API** ที่รวมเข้ากับกระบวนการทำงานของคุณได้โดยตรง  
- **Flexible redaction rules** – regex, คำสำคัญ, หรือตรรกะที่กำหนดเอง  
- **Compliance‑ready** ผลลัพธ์ที่ลบข้อมูลที่ละเอียดอ่อนอย่างถาวร  

## ข้อกำหนดเบื้องต้น
- Java Development Kit (JDK) 8 หรือใหม่กว่า  
- Maven (หรือทางเลือกในการดาวน์โหลด JAR ด้วยตนเอง)  
- Microsoft Azure account พร้อมข้อมูลประจำตัว OCR  
- ความรู้พื้นฐานของ Java และความคุ้นเคยกับ regular expressions  

## การตั้งค่า GroupDocs.Redaction สำหรับ Java

### การตั้งค่า Maven
เพิ่มรีโพซิทอรีและ dependency ของ GroupDocs ลงใน `pom.xml` ของคุณ:

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
หากคุณไม่ต้องการใช้ Maven ให้ดาวน์โหลด JAR ล่าสุดจากหน้า releases อย่างเป็นทางการ: [รุ่น GroupDocs.Redaction สำหรับ Java](https://releases.groupdocs.com/redaction/java/)

### การรับไลเซนส์
- **Free Trial** – สำรวจคุณสมบัติหลักโดยไม่ต้องผูกมัด  
- **Temporary License** – ขยายระยะทดลองใช้สำหรับโครงการขนาดใหญ่  
- **Full License** – ปลดล็อกการใช้งานไม่จำกัดและรับการสนับสนุนระดับพรีเมียม  

### การเริ่มต้นและตั้งค่าเบื้องต้น
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## วิธีลบข้อมูลใน PDF ด้วย OCR ด้วย Java

### ขั้นตอนที่ 1: โหลดเอกสารพร้อมการตั้งค่า OCR
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;

// Load your document with OCR settings
try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf", 
    new LoadOptions(), settings)) {
    // Subsequent redaction steps will be placed here
}
```
- **Parameters**  
  - `"YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf"` – เส้นทางไปยัง PDF เป้าหมาย  
  - `new LoadOptions()` – การกำหนดค่าการโหลดเริ่มต้น  
  - `settings` – ประกอบด้วย Azure OCR connector  

### ขั้นตอนที่ 2: ใช้การลบข้อมูลด้วย Regex (เช่น หมายเลขประกันสังคม)
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
- **Regex Explanation** – `\b\d{3}-\d{2}-\d{4}\b` จะจับรูปแบบเช่น `123-45-6789`  
- **ReplacementOptions** – แทนที่ข้อความที่ตรวจพบด้วย `[REDACTED]`  

### ข้อผิดพลาดทั่วไปและการแก้ไขปัญหา
- **Azure credentials** – ตรวจสอบคีย์การสมัครและ endpoint อีกครั้ง  
- **File path** – ตรวจให้แน่ใจว่า PDF มีอยู่และแอปพลิเคชันมีสิทธิ์อ่าน/เขียน  
- **Performance** – PDF ขนาดใหญ่อาจต้องเพิ่มขนาด heap หรือใช้การประมวลผลแบบอะซิงโครนัส  

## กรณีการใช้งานจริงสำหรับการลบข้อมูลในเอกสารสแกน
1. **Legal firms** – ซ่อนข้อมูลระบุตัวตนของลูกค้าก่อนแชร์ไฟล์คดี  
2. **Financial institutions** – ปิดบังหมายเลขบัญชีในใบแจ้งยอดสแกน  
3. **Healthcare providers** – ปกป้อง PHI ของผู้ป่วยในบันทึกทางการแพทย์ที่สแกน  
4. **Government agencies** – ลบข้อมูลส่วนบุคคลจาก PDF บันทึกสาธารณะ  
5. **Enterprises** – ทำความสะอาดสัญญาก่อนการตรวจสอบโดยบุคคลภายนอก  

## เคล็ดลับด้านประสิทธิภาพ
- ทำให้รูปแบบ regex มีความเฉพาะเจาะจงมากที่สุดเพื่อลดเวลาในการประมวลผล  
- ปล่อยอินสแตนซ์ `Redactor` อย่างทันท่วงที (ใช้ try‑with‑resources ตามตัวอย่าง)  
- สำหรับการประมวลผลเป็นชุด ให้พิจารณาคิวงานและรันในเธรดแบบขนาน  

## คำถามที่พบบ่อย

**Q: OCR redaction คืออะไร?**  
A: OCR redaction ใช้การจดจำอักขระด้วยแสงเพื่อสกัดข้อความจากรูปภาพหรือ PDF สแกน แล้วใช้กฎการลบข้อมูลเพื่อกำจัดข้อความนั้นอย่างถาวร

**Q: ฉันสามารถใช้ GroupDocs.Redaction โดยไม่ต้องใช้ Azure OCR ได้หรือไม่?**  
A: ใช่, แต่ OCR จะเพิ่มความแม่นยำอย่างมากสำหรับเอกสารสแกน ทำให้คุณ **redact scanned documents** ได้อย่างมีประสิทธิภาพ

**Q: ฉันจะจัดการกับรูปแบบ regex ที่ซับซ้อนได้อย่างไร?**  
A: ทดสอบรูปแบบกับข้อมูลตัวอย่าง, ใช้ขอบคำ (`\b`) เพื่อหลีกเลี่ยงการจับส่วนที่ไม่ครบ, และพิจารณาแบ่งการแสดงผลใหญ่เป็นหลายการลบข้อมูลที่ง่ายกว่า

**Q: จุดคอขวดด้านประสิทธิภาพทั่วไปคืออะไร?**  
A: การเรียก OCR บนไฟล์ขนาดใหญ่, regex ที่กว้างเกินไป, และการจัดสรรหน่วยความจำไม่เพียงพอ ปรับปรุงโดยการปรับ regex และเพิ่มทรัพยากรตามต้องการ

**Q: ฉันจะขอความช่วยเหลือได้จากที่ไหนหากเจอปัญหา?**  
A: ตั้งคำถามในฟอรั่มชุมชนของ GroupDocs: [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33)

## แหล่งข้อมูลเพิ่มเติม
- **เอกสาร**: https://docs.groupdocs.com/redaction/java/  
- **API Reference**: https://reference.groupdocs.com/redaction/java  
- **ดาวน์โหลด**: https://releases.groupdocs.com/redaction/java/  
- **GitHub**: https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java  
- **Free Support**: https://forum.groupdocs.com/c/redaction/33  
- **Temporary License**: https://purchase.groupdocs.com/temporary-license/  

---

**Last Updated:** 2026-01-21  
**Tested With:** GroupDocs.Redaction 24.9 for Java  
**Author:** GroupDocs