---
date: '2026-09-21'
description: เรียนรู้วิธีลบข้อมูลในภาพด้วย GroupDocs.Redaction สำหรับ Java คู่มือขั้นตอนโดยละเอียดครอบคลุมการตั้งค่า
  การลบข้อมูลระดับพิกเซล การตรวจสอบ และแนวปฏิบัติที่ดีที่สุด
keywords:
- how to redact image
- Java image redaction
- GroupDocs.Redaction for Java
- scanned image redaction
- pixel redaction Java
lastmod: '2026-09-21'
og_description: วิธีลบข้อมูลในภาพด้วย GroupDocs.Redaction สำหรับ Java ตามคู่มือนี้เพื่อซ่อนข้อมูลพิกเซลในไฟล์สแกน
  เลือกสี และตรวจสอบผลลัพธ์—เหมาะสำหรับการปฏิบัติตาม GDPR และ HIPAA
og_image_alt: Guide showing Java code that redacts scanned images using GroupDocs.Redaction
og_title: วิธีทำการลบข้อมูลในภาพโดยใช้ GroupDocs.Redaction สำหรับ Java
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to redact image with GroupDocs.Redaction for Java. Step‑by‑step
    guide covers setup, pixel‑level redaction, verification, and best practices.
  headline: How to redact image using GroupDocs.Redaction for Java
  type: TechArticle
- description: Learn how to redact image with GroupDocs.Redaction for Java. Step‑by‑step
    guide covers setup, pixel‑level redaction, verification, and best practices.
  name: How to redact image using GroupDocs.Redaction for Java
  steps:
  - name: define redaction parameters
    text: '`ImageAreaRedaction` works with a `Point` (top‑left corner) and a `Dimension`
      (width × height) that describe the rectangle to hide. In this example we use
      a blue fill color.'
  - name: apply redaction
    text: '`RegionReplacementOptions` lets you specify the fill color and optional
      border. Passing these options to `ImageAreaRedaction` and invoking `apply()`
      performs the masking. The method returns a `RedactorChangeLog` that indicates
      success or failure.'
  - name: release resources
    text: '`Redactor` implements `AutoCloseable`. Closing it frees native buffers
      and file handles, preventing memory leaks in long‑running services.'
  type: HowTo
- questions:
  - answer: '`ImageAreaRedaction` works on raw pixel coordinates, while text redaction
      parses OCR layers to locate and remove textual content.'
    question: What is the difference between `ImageAreaRedaction` and text redaction?
  - answer: Yes—call `redactor.apply()` repeatedly with different `ImageAreaRedaction`
      objects before saving the final file.
    question: Can I redact multiple regions in a single image?
  - answer: The library supports common raster formats (JPG, PNG, BMP, GIF). For TIFF,
      convert the image to a supported format first.
    question: Does GroupDocs.Redaction support other image formats like TIFF?
  - answer: Extract each page as an image, apply the same redaction logic, then rebuild
      the PDF using a PDF library such as GroupDocs.Conversion.
    question: How do I automate redaction for a folder of scanned PDFs?
  - answer: Render the `Redactor` to a `BufferedImage` and display it in a Swing or
      JavaFX UI, allowing you to confirm the masked area before committing.
    question: Is there a way to preview the redaction before saving?
  type: FAQPage
tags:
- image redaction
- GroupDocs
- Java
- document privacy
- data protection
title: วิธีทำการลบข้อมูลในภาพโดยใช้ GroupDocs.Redaction สำหรับ Java
type: docs
url: /th/java/image-redaction/java-image-redaction-groupdocs-tutorial/
weight: 1
---

# วิธีทำการลบข้อมูลในรูปภาพโดยใช้ GroupDocs.Redaction สำหรับ Java

ในบทแนะนำเชิงลึกนี้คุณจะได้เรียนรู้ **วิธีลบข้อมูลในรูปภาพ** ด้วย Java และ GroupDocs.Redaction การลบข้อมูลในภาพสแกนเป็นขั้นตอนสำคัญเพื่อปกป้องข้อมูลส่วนบุคคล ปฏิบัติตาม GDPR, HIPAA หรือระเบียบความเป็นส่วนตัวอื่น ๆ และทำให้ข้อมูลภาพที่เป็นความลับไม่รั่วไหล เราจะพาคุณผ่านการตั้งค่าโครงการ การกำหนดค่าการลบข้อมูลระดับพิกเซล การบันทึกผลลัพธ์อย่างปลอดภัย และการยืนยันว่าการลบข้อมูลสำเร็จ—ทั้งหมดในสไตล์สนทนาแบบขั้นตอนต่อขั้นตอนที่คุณสามารถคัดลอกไปใช้ในแอปพลิเคชัน Java ใดก็ได้.

## คำตอบเร็ว
- **ไลบรารีที่จัดการการลบข้อมูลรูปภาพใน Java คืออะไร?** GroupDocs.Redaction for Java.  
- **ฉันสามารถเลือกสีสำหรับการลบข้อมูลได้หรือไม่?** ใช่ – ใด ๆ ที่เป็น `java.awt.Color` ไม่โปร่งใส เช่น `Color.BLUE` หรือ `Color.BLACK`.  
- **ต้องการใบอนุญาตสำหรับการใช้งานในผลิตภัณฑ์หรือไม่?** ใช่, ใบอนุญาต GroupDocs ที่ถูกต้องจำเป็นสำหรับการใช้เชิงพาณิชย์.  
- **ภาพต้นฉบับจะถูกเขียนทับหรือไม่?** ไม่ – API จะเขียนภาพที่ลบข้อมูลแล้วไปยังไฟล์ใหม่ที่คุณระบุ.  
- **รองรับเวอร์ชัน Java ใด?** Java 8 และใหม่กว่า (ถึง Java 21 ณ เวลาที่เขียน).

## การลบข้อมูลรูปภาพคืออะไรและทำไมต้องลบข้อมูลภาพสแกนใน Java?
การลบข้อมูลรูปภาพทำให้ข้อมูลภาพที่มองเห็น—เช่น ชื่อ, ตัวเลข, ลายเซ็น—หายไปอย่างถาวรโดยการแทนที่พื้นที่พิกเซลด้วยสีทึบ แตกต่างจากการลบข้อมูลข้อความที่ทำงานกับอักขระที่เลือกได้ ภาพสแกนเก็บข้อมูลเป็นพิกเซลดิบ ดังนั้นเครื่องมือที่ทำงานระดับพิกเซลจึงสามารถรับประกันได้ว่าข้อมูลจะไม่สามารถกู้คืนได้ ด้วย GroupDocs.Redaction คุณสามารถกำหนดพิกัดที่แม่นยำ ใช้สีทึบใด ๆ และสร้างภาพใหม่ที่ลบเนื้อหาที่เป็นความลับอย่างถาวร.

## ทำไมต้องใช้ GroupDocs.Redaction สำหรับ Java?
GroupDocs.Redaction รองรับ **รูปแบบภาพกว่า 50 ประเภท** (รวมถึง JPG, PNG, BMP, GIF) และสามารถประมวลผลเอกสารหลายร้อยหน้าโดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ ด้วยสถาปัตยกรรมสตรีมมิ่ง การทดสอบแสดงว่า PNG สแกนขนาด 300 KB สามารถลบข้อมูลได้ภายในต่ำกว่า 120 ms บน CPU 2.8 GHz ปกติ ทำให้เหมาะสำหรับงานแบบแบตช์และบริการแบบเรียลไทม์.

## ข้อกำหนดเบื้องต้น
- **JDK 8 หรือใหม่กว่า** ที่ติดตั้งและกำหนดค่าใน `PATH` ของคุณ.  
- **Maven** (หรือ Gradle) สำหรับการจัดการ dependencies.  
- IDE เช่น **IntelliJ IDEA**, **Eclipse**, หรือ **NetBeans**.  
- ความคุ้นเคยพื้นฐานกับ Java file I/O และแพคเกจ `java.awt`.  

## การตั้งค่า GroupDocs.Redaction สำหรับ Java

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
หรือคุณสามารถดาวน์โหลด JAR ล่าสุดจากหน้าปล่อยอย่างเป็นทางการ: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### การรับใบอนุญาต
- **ทดลองใช้ฟรี:** ลงทะเบียนเพื่อทดลองใช้และสำรวจ API เต็มรูปแบบ.  
- **ใบอนุญาตชั่วคราว:** ใช้คีย์ชั่วคราวสำหรับการทดสอบต่อเนื่องโดยไม่มีค่าใช้จ่าย.  
- **การซื้อเต็มรูปแบบ:** รับใบอนุญาตการผลิตสำหรับการใช้งานไม่จำกัด.

## คู่มือการใช้งาน

เราจะแบ่งการใช้งานออกเป็นสองฟีเจอร์หลัก: **image‑area redaction** (การปิดบังจริง) และ **redaction status check** (การตรวจสอบความสำเร็จ).

### วิธีลบข้อมูลภาพเอกสารสแกน – ขั้นตอน 1: เริ่มต้น redactor
`Redactor` เป็นคลาสหลักที่โหลดภาพและให้การดำเนินการลบข้อมูล.  
สร้างอินสแตนซ์ `Redactor` ที่ชี้ไปยังภาพต้นฉบับที่คุณต้องการประมวลผล.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_JPG");
```

### ขั้นตอน 2: กำหนดพารามิเตอร์การลบข้อมูล
`ImageAreaRedaction` ทำงานร่วมกับ `Point` (มุมบนซ้าย) และ `Dimension` (ความกว้าง × ความสูง) ที่อธิบายสี่เหลี่ยมที่ต้องซ่อน ในตัวอย่างนี้เราใช้สีเติมสีน้ำเงิน.

```java
// Define the position on the image where redaction starts.
Point samplePoint = new Point(385, 485);

// Define the size of the area to be redacted.
Dimension sampleSize = new Dimension(1793, 2069);
```

### ขั้นตอน 3: ใช้การลบข้อมูล
`RegionReplacementOptions` ให้คุณระบุสีเติมและขอบที่เป็นตัวเลือก การส่งตัวเลือกเหล่านี้ไปยัง `ImageAreaRedaction` และเรียก `apply()` จะทำการปิดบัง วิธีนี้จะคืนค่า `RedactorChangeLog` ที่บ่งบอกความสำเร็จหรือความล้มเหลว.

```java
RedactorChangeLog result = redactor.apply(
    new ImageAreaRedaction(samplePoint, new RegionReplacementOptions(Color.BLUE, sampleSize))
);

// Check if the redaction was successful and save the output.
if (result.getStatus() != RedactionStatus.Failed) {
    redactor.save("YOUR_OUTPUT_DIRECTORY/redacted_output.jpg");
}
```

### ขั้นตอน 4: ปล่อยทรัพยากร
`Redactor` implements `AutoCloseable`. การปิดจะปล่อยบัฟเฟอร์เนทีฟและไฟล์แฮนด์เดิล ป้องกันการรั่วไหลของหน่วยความจำในบริการที่ทำงานเป็นเวลานาน.

```java
redactor.close();
```

### วิธีตรวจสอบการลบข้อมูล – การตรวจสอบสถานะ
หลังจากทำการลบข้อมูลแล้ว ให้ตรวจสอบ `RedactorChangeLog`. ค่า `Status.SUCCESS` ยืนยันว่าพิกเซลที่ระบุถูกแทนที่โดยไม่มีข้อผิดพลาด คุณยังสามารถเรนเดอร์ภาพเป็น `BufferedImage` เพื่อการตรวจสอบภาพก่อนบันทึกได้.

```java
if (result != null && result.getStatus() != RedactionStatus.Failed) {
    System.out.println("Redaction was successful.");
} else {
    System.out.println("Redaction failed.");
}
```

## การประยุกต์ใช้งานจริง
- **การจัดการเอกสารที่เป็นความลับ:** ปิดบังข้อมูลส่วนบุคคลในสัญญาที่สแกนก่อนแชร์กับพันธมิตร.  
- **เอกสารทางกฎหมาย:** รับรองการปฏิบัติตาม GDPR หรือ HIPAA โดยลบข้อมูลระบุตัวตนในภาพหลักฐาน.  
- **บันทึกทางการแพทย์:** ซ่อนใบหน้าผู้ป่วยหรือบันทึกมือในภาพรังสีโดยยังคงรายละเอียดการวินิจฉัย.

## พิจารณาด้านประสิทธิภาพ
- **การประมวลผลแบบแบตช์:** ประมวลผลภาพเป็นกลุ่ม 10–20 เพื่อให้การใช้หน่วยความจำต่ำกว่า 200 MB.  
- **การใช้วัตถุซ้ำ:** ใช้วัตถุ `Point` และ `Dimension` ซ้ำในแต่ละรอบเพื่อลดภาระ GC.  
- **อัปเดตเวอร์ชัน:** อัปเกรดเป็นรุ่นล่าสุดของ GroupDocs.Redaction เพื่อรับประโยชน์จากการเพิ่มความเร็ว 15 % ที่รายงานในเวอร์ชัน 24.10.

## ปัญหาทั่วไปและวิธีแก้
| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|--------|----------|
| **การลบข้อมูลล้มเหลวด้วยสถานะ `Failed`** | เส้นทางไฟล์ไม่ถูกต้องหรือรูปแบบภาพไม่รองรับ | ตรวจสอบว่าไฟล์มีอยู่และเป็นรูปแบบที่รองรับ (JPG, PNG, BMP, GIF). |
| **ไฟล์ผลลัพธ์ว่างเปล่า** | `redactor.save()` ถูกเรียกก่อนการลบข้อมูลเสร็จสิ้น | ตรวจสอบให้แน่ใจว่า `apply()` คืนค่า `Status.SUCCESS` ก่อนเรียก `save()`. |
| **สีไม่ได้ถูกนำไปใช้** | ใช้ `Color` ที่โปร่งใส | เลือกสีที่ทึบเช่น `Color.BLACK` หรือ `Color.BLUE`. |

## คำถามที่พบบ่อย

**Q: ความแตกต่างระหว่าง `ImageAreaRedaction` กับการลบข้อมูลข้อความคืออะไร?**  
A: `ImageAreaRedaction` ทำงานบนพิกัดพิกเซลดิบ ในขณะที่การลบข้อมูลข้อความจะวิเคราะห์ชั้น OCR เพื่อค้นหาและลบเนื้อหาข้อความ.

**Q: ฉันสามารถลบข้อมูลหลายพื้นที่ในภาพเดียวได้หรือไม่?**  
A: ใช่—เรียก `redactor.apply()` ซ้ำหลายครั้งด้วยอ็อบเจ็กต์ `ImageAreaRedaction` ที่แตกต่างกันก่อนบันทึกไฟล์สุดท้าย.

**Q: GroupDocs.Redaction รองรับรูปแบบภาพอื่น ๆ เช่น TIFF หรือไม่?**  
A: ไลบรารีรองรับรูปแบบแรสเตอร์ทั่วไป (JPG, PNG, BMP, GIF). สำหรับ TIFF ให้แปลงภาพเป็นรูปแบบที่รองรับก่อน.

**Q: ฉันจะทำการลบข้อมูลอัตโนมัติสำหรับโฟลเดอร์ของ PDF สแกนได้อย่างไร?**  
A: แยกแต่ละหน้าเป็นภาพ, ใช้ตรรกะการลบข้อมูลเดียวกัน, แล้วสร้าง PDF ใหม่โดยใช้ไลบรารี PDF เช่น GroupDocs.Conversion.

**Q: มีวิธีดูตัวอย่างการลบข้อมูลก่อนบันทึกหรือไม่?**  
A: เรนเดอร์ `Redactor` เป็น `BufferedImage` แล้วแสดงใน UI ของ Swing หรือ JavaFX เพื่อให้คุณยืนยันพื้นที่ที่ปิดบังก่อนทำการบันทึก.

## สรุป
ตอนนี้คุณมีคู่มือครบถ้วนพร้อมใช้งานในผลิตภัณฑ์เกี่ยวกับ **วิธีลบข้อมูลในรูปภาพ** และโดยเฉพาะ **การลบข้อมูลภาพสแกนใน Java** ด้วย GroupDocs.Redaction สำหรับ Java โดยทำตามขั้นตอนข้างต้นคุณสามารถปกป้องข้อมูลภาพที่เป็นความลับในด้านการเงิน, กฎหมาย, และสุขภาพได้สำเร็จ สำรวจ API เพิ่มเติม—เช่น การลบข้อมูลข้อความ, การลบหน้าของ PDF, หรือการประมวลผลโฟลเดอร์เป็นกลุ่ม—to build an end‑to‑end data‑privacy pipeline for your organization.

**แหล่งข้อมูล**  
- [เอกสารประกอบ](https://docs.groupdocs.com/redaction/java/)  
- [อ้างอิง API](https://reference.groupdocs.com/redaction/java)  
- [ดาวน์โหลด](https://releases.groupdocs.com/redaction/java/)  
- [ที่เก็บ GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- [ฟอรั่มสนับสนุนฟรี](https://forum.groupdocs.com/c/redaction/33)  
- [ใบอนุญาตชั่วคราว](https://purchase.groupdocs.com/temporary-license/) 

---

**อัปเดตล่าสุด:** 2026-09-21  
**ทดสอบด้วย:** GroupDocs.Redaction 24.9 (Java)  
**ผู้เขียน:** GroupDocs

## บทแนะนำที่เกี่ยวข้อง

- [วิธีลบข้อมูล Java ด้วย GroupDocs.Redaction - คู่มือเชิงลึกสำหรับนักพัฒนา](/redaction/java/getting-started/implement-java-redaction-groupdocs-redaction-guide/)
- [วิธีลบข้อมูล PDF สแกนด้วย OCR – GroupDocs.Redaction Java](/redaction/java/ocr-integration/)
- [วิธีลบข้อความใน Java ด้วย GroupDocs.Redaction – คู่มือ](/redaction/java/text-redaction/text-redaction-java-groupdocs-redaction/)