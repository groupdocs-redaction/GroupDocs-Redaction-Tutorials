---
date: '2026-02-24'
description: เรียนรู้วิธีการลบข้อมูลในข้อความด้วย GroupDocs.Redaction สำหรับ Java
  และบันทึกเป็น PDF ที่แปลงเป็นภาพเพื่อเอกสารที่ปลอดภัยและไม่สามารถแก้ไขได้
keywords:
- text redaction Java
- save as rasterized PDF
- GroupDocs.Redaction Java
title: วิธีลบข้อมูลในข้อความและบันทึก PDF ที่แปลงเป็นรูปภาพด้วย GroupDocs.Java
type: docs
url: /th/java/text-redaction/groupdocs-redaction-java-text-redaction-rasterize-pdf/
weight: 1
---

# วิธีทำการลบข้อความและบันทึก PDF ที่แรสเตอร์ไลซ์ด้วย GroupDocs.Redaction Java

การปกป้องข้อมูลที่ละเอียดอ่อนในเอกสารของคุณเป็นสิ่งสำคัญ ไม่ว่าคุณจะต้องการลบชื่อส่วนบุคคลหรือเตรียมเวอร์ชันที่ปลอดภัยของไฟล์ของคุณ GroupDocs.Redaction for Java ทำให้ภารกิจเหล่านี้ง่ายขึ้น **How to redact text** อย่างรวดเร็วและจากนั้น **save as rasterized PDF** เป็นความต้องการทั่วไปสำหรับแอปพลิเคชันที่ขับเคลื่อนด้วยการปฏิบัติตามกฎระเบียบ และคู่มือนี้จะแสดงให้คุณเห็นขั้นตอนอย่างชัดเจน

## คำตอบอย่างรวดเร็ว
- **“redact text” หมายความว่าอะไร?** มันแทนที่หรือเอาสตริงที่ละเอียดอ่อนออกเพื่อไม่ให้สามารถอ่านหรือกู้คืนได้.  
- **ไลบรารีใดที่ทำงานนี้?** GroupDocs.Redaction for Java มีฟีเจอร์การลบข้อความและการแรสเตอร์ไลซ์ในตัว.  
- **ฉันต้องการไลเซนส์หรือไม่?** การทดลองใช้ฟรีสามารถใช้สำหรับการทดสอบได้; จำเป็นต้องมีไลเซนส์ถาวรสำหรับการใช้งานจริง.  
- **ฉันสามารถแปลง DOCX เป็น PDF ที่แรสเตอร์ไลซ์ในขั้นตอนเดียวได้หรือไม่?** ได้ – ทำการลบข้อความก่อน แล้วใช้ `SaveOptions` พร้อมเปิดการแรสเตอร์ไลซ์.  
- **ผลลัพธ์เป็นไฟล์ที่ไม่สามารถแก้ไขได้จริงหรือไม่?** PDF ที่แรสเตอร์ไลซ์จะถูกเรนเดอร์เป็นภาพ ทำให้ไม่สามารถดึงข้อความหรือแก้ไขได้.

## การลบข้อความคืออะไร?
การลบข้อความคือกระบวนการที่ลบหรือบังข้อมูลที่ละเอียดอ่อนอย่างถาวร—เช่น ตัวระบุส่วนบุคคล ข้อมูลการเงิน หรือข้อกำหนดที่เป็นความลับ—ออกจากเอกสาร ไม่เหมือนการค้นหาและแทนที่แบบธรรมดา การลบข้อความจะทำให้เนื้อหาที่ซ่อนอยู่ไม่สามารถกู้คืนได้

## ทำไมต้องใช้ GroupDocs.Redaction สำหรับ Java?
- **ประเภทการลบข้อความในตัว** (exact phrase, regex, image, etc.)  
- **การแรสเตอร์ไลซ์คลิกเดียว** เพื่อสร้าง PDF ที่ปลอดภัย  
- **รองรับหลายรูปแบบ** (DOCX, PPTX, XLSX, PDF, etc.)  
- **API ที่เป็นมิตรต่อผู้พัฒนา** ที่สามารถผสานรวมกับโครงการ Java ที่มีอยู่

## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะเริ่ม โปรดตรวจสอบว่าคุณมี:

1. **Java Development Kit (JDK 11 หรือใหม่กว่า)** และ IDE เช่น IntelliJ IDEA หรือ Eclipse.  
2. **ไลบรารี GroupDocs.Redaction** (เวอร์ชัน 24.9 หรือใหม่กว่า).  
3. **ความรู้พื้นฐานของ Java** — คุณจะเขียนโค้ดสั้น ๆ จำนวนไม่กี่บรรทัด.

## การตั้งค่า GroupDocs.Redaction สำหรับ Java

### การติดตั้งด้วย Maven
เพิ่มรีโพซิทอรีของ GroupDocs และการพึ่งพาในไฟล์ `pom.xml` ของคุณ:

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
หากคุณไม่ใช้ Maven คุณสามารถดาวน์โหลดไฟล์ JAR จากหน้าปล่อยอย่างเป็นทางการ: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

#### การรับไลเซนส์
- **Free Trial** – สำรวจ API ได้โดยไม่มีค่าใช้จ่าย.  
- **Temporary License** – เหมาะสำหรับการทดสอบระยะยาว.  
- **Full License** – จำเป็นสำหรับการใช้งานในสภาพแวดล้อมการผลิต.

### การเริ่มต้นพื้นฐาน
เปิดเอกสารด้วยคลาส `Redactor`:

```java
import com.groupdocs.redaction.Redactor;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

## คู่มือการใช้งาน

### วิธีลบข้อความใน Java
ด้านล่างเราจะอธิบายการลบข้อความแบบ exact‑phrase ซึ่งเหมาะอย่างยิ่งสำหรับการลบตัวระบุที่รู้จัก เช่น ชื่อของบุคคล

#### ขั้นตอนที่ 1: นำเข้าคลาสที่จำเป็น
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;
```

#### ขั้นตอนที่ 2: ใช้ Exact Phrase Redaction
โค้ดต่อไปนี้จะเปลี่ยนทุกการปรากฏของ **“John Doe”** ให้เป็นตัวแทน **[personal]**:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]"));
} finally { 
    redactor.close(); 
}
```

**ทำไมวิธีนี้ถึงได้ผล:**  
- `ExactPhraseRedaction` มุ่งเป้าไปที่สตริงตัวอักษร “John Doe”.  
- `ReplacementOptions` บอกให้เอนจินใส่สิ่งที่ต้องการแทนข้อความเดิม

**เคล็ดลับและข้อผิดพลาดทั่วไป**  
- ตรวจสอบเส้นทางของเอกสารอีกครั้ง; เส้นทางที่ผิดจะทำให้เกิด `FileNotFoundException`.  
- ตรวจสอบให้แน่ใจว่ากระบวนการ Java มีสิทธิ์เขียนในโฟลเดอร์ผลลัพธ์.

### วิธีบันทึกเป็น PDF ที่แรสเตอร์ไลซ์
หลังจากทำการลบข้อความแล้ว คุณอาจต้องการ PDF ที่ไม่สามารถแก้ไขได้ การแรสเตอร์ไลซ์จะเปลี่ยนทุกหน้าเป็นภาพ ทำให้ไม่สามารถเลือกหรือแก้ไขข้อความได้

#### ขั้นตอนที่ 1: นำเข้า `SaveOptions`
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
```

#### ขั้นตอนที่ 2: ตั้งค่าและบันทึก PDF ที่แรสเตอร์ไลซ์
```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    SaveOptions tmp0 = new SaveOptions();
    tmp0.setAddSuffix(false);
    tmp0.setRasterizeToPDF(true);

    redactor.save(tmp0);
} finally { 
    redactor.close(); 
}
```

**คำอธิบาย:**  
- `setAddSuffix(false)` จะรักษาชื่อไฟล์เดิม (คุณสามารถเปิดใช้งานเพื่อเพิ่ม “_redacted” ได้).  
- `setRasterizeToPDF(true)` บอกให้ GroupDocs เรนเดอร์แต่ละหน้าเป็นภาพภายใน PDF ทำให้เอกสารเป็น **non‑editable**.

**การแก้ไขปัญหา**  
- หากการแรสเตอร์ไลซ์ล้มเหลว ให้ตรวจสอบว่า Java runtime มีการพึ่งพาการเรนเดอร์ PDF (รวมอยู่ในไลบรารี).

## การประยุกต์ใช้งานจริง
1. **Legal Document Processing** – ลบชื่อของลูกค้าก่อนแชร์กับฝ่ายตรงข้าม.  
2. **HR Record Management** – ซ่อนหมายเลขพนักงานในรายงานภายใน.  
3. **Financial Reporting** – ปกป้องหมายเลขบัญชีเมื่อแจกจ่ายสรุปการตรวจสอบ.

คุณสามารถเชื่อมต่อขั้นตอนเหล่านี้เป็นเวิร์กโฟลว์อัตโนมัติ โดยเชื่อม GroupDocs.Redaction กับระบบจัดการเอกสารหรือคลังเก็บข้อมูลบนคลาวด์

## พิจารณาด้านประสิทธิภาพ
- **Batch Processing:** ใช้ `Redactor` ตัวเดียวซ้ำเมื่อจัดการไฟล์หลายไฟล์เพื่อลดภาระ.  
- **Memory Management:** สำหรับเอกสารขนาดใหญ่ ให้เรียก `System.gc()` หลังจาก `redactor.close()` แต่ละครั้ง หรือรันกระบวนการใน JVM แยก.  
- **Keep Dependencies Updated:** รุ่นใหม่มักมีการปรับปรุงประสิทธิภาพสำหรับการแรสเตอร์ไลซ์ PDF.

## ปัญหาทั่วไปและวิธีแก้

| ปัญหา | วิธีแก้ |
|-------|----------|
| *ไม่พบไฟล์* | ตรวจสอบเส้นทางแบบ absolute และยืนยันว่าไฟล์มีอยู่บนเซิร์ฟเวอร์. |
| *การปฏิเสธสิทธิ์* | รัน JVM ด้วยสิทธิ์ของ OS ที่เพียงพอหรือเปลี่ยน ACL ของโฟลเดอร์ผลลัพธ์. |
| *การแรสเตอร์ไลซ์สร้างหน้าว่าง* | ยืนยันว่าเอกสารต้นทางไม่ได้เป็นภาพแรสเตอร์อยู่แล้ว; ใช้เวอร์ชันไลบรารีล่าสุด. |
| *การลบข้อความทิ้งข้อความซ่อนอยู่* | ใช้ `ExactPhraseRedaction` พร้อม `ReplacementOptions`; หลีกเลี่ยงวิธีการค้นหาและแทนที่แบบธรรมดา. |

## คำถามที่พบบ่อย

**ถาม: การลบข้อความแบบ exact phrase คืออะไร?**  
A: มันแทนที่สตริงเฉพาะ (เช่น ชื่อ) ด้วยตัวแทน ทำให้ข้อความเดิมไม่สามารถกู้คืนได้.

**ถาม: การแรสเตอร์ไลซ์ PDF ช่วยเพิ่มความปลอดภัยอย่างไร?**  
A: PDF ที่แรสเตอร์ไลซ์จะเรนเดอร์แต่ละหน้าเป็นภาพ ทำให้ไม่สามารถเลือก, คัดลอก หรือแก้ไขข้อความได้.

**ถาม: ฉันสามารถประมวลผลหลายไฟล์ในรอบเดียวได้หรือไม่?**  
A: ได้ — วนลูปผ่านรายการเส้นทางไฟล์และใช้การตั้งค่า `Redactor` เดียวกันสำหรับแต่ละเอกสาร.

**ถาม: การรวมกับคลาวด์เป็นไปได้หรือไม่?**  
A: แน่นอน คุณสามารถอ่าน/เขียนสตรีมจาก AWS S3, Azure Blob หรือ Google Cloud Storage และส่งตรงไปยัง API.

**ถาม: ข้อผิดพลาดทั่วไปสำหรับผู้เริ่มต้นคืออะไร?**  
A: ลืมปิด `Redactor` (ซึ่งทำให้ไฟล์ล็อก) และใช้ไลบรารีเวอร์ชันเก่าที่ไม่มีการสนับสนุนการแรสเตอร์ไลซ์.

## แหล่งข้อมูล

- **Documentation**: [GroupDocs Redaction Java Documentation](https://docs.groupdocs.com/redaction/java/)  
- **API Reference**: [GroupDocs Redaction API Reference](https://reference.groupdocs.com/redaction/java)  
- **Download**: [Latest Releases](https://releases.groupdocs.com/redaction/java/)  
- **GitHub**: [GroupDocs.Redaction GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **Free Support**: [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)  
- **Temporary License**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license/) 

---

**อัปเดตล่าสุด:** 2026-02-24  
**ทดสอบด้วย:** GroupDocs.Redaction 24.9 for Java  
**ผู้เขียน:** GroupDocs  

---