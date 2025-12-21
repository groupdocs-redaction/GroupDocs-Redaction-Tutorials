---
date: '2025-12-21'
description: เรียนรู้วิธีแปลงไฟล์ docx เป็นภาพและทำการบังข้อมูลไฟล์ Word ด้วย GroupDocs Redaction สำหรับ Java คู่มือขั้นตอนโดยละเอียดที่ครอบคลุมการเรสเตอร์ไลเซชัน
  การบังข้อมูลในพื้นที่ภาพ และการตั้งค่า Maven.
keywords:
- GroupDocs Redaction Java
- Word document rasterization
- secure redaction
title: วิธีแปลง DOCX เป็นภาพและลบข้อมูลในเอกสาร Word ด้วย GroupDocs Redaction Java
type: docs
url: /th/java/document-saving/groupdocs-redaction-java-rasterize-word-docs/
weight: 1
---

# แปลง DOCX เป็น Image และ Redact Word Documents ด้วย GroupDocs Redaction Java

การปกป้องข้อมูลที่ละเอียดอ่อนในไฟล์ Microsoft Word เป็นความท้าทายประจำวันสำหรับนักพัฒนาที่สร้างแอปพลิเคชันที่เน้นเอกสาร ไม่ว่าคุณจะต้องการซ่อนข้อมูลส่วนบุคคล ปฏิบัติตาม GDPR หรือเตรียมสัญญากฎหมายเพื่อการตรวจสอบจากภายนอก การ **แปลง docx เป็น image** ก่อนทำการลบข้อมูลจะรับประกันว่าเลย์เอาต์เดิมยังคงอยู่ครบถ้วนในขณะที่เนื้อหาถูกปกปิดอย่างปลอดภัย

ในบทเรียนนี้คุณจะได้เรียนรู้วิธี:

- **Convert DOCX to image** โดยทำการ rasterize เอกสาร Word ด้วย GroupDocs Redaction for Java.  
- ใช้ **image area redaction** บน PDF ที่ rasterized เพื่อซ่อนข้อความหรือกราฟิก  
- ตั้งค่า **GroupDocs Maven dependency** และจัดการการให้สิทธิ์ใช้งาน  

มาดำเนินการผ่านกระบวนการทั้งหมด ตั้งแต่การเตรียมสภาพแวดล้อมจนถึงการบันทึกเอกสารขั้นสุดท้าย

## คำตอบอย่างรวดเร็ว
- **What does “convert docx to image” mean?** มันทำการ rasterize แต่ละหน้าของไฟล์ Word เป็น bitmap เพื่อรักษาเลย์เอาต์สำหรับการลบข้อมูลที่เชื่อถือได้.  
- **Which Maven artifact is required?** `com.groupdocs:groupdocs-redaction` (ดูส่วน *groupdocs maven dependency*)  
- **Can I hide text in Java?** ใช่—ใช้ `ImageAreaRedaction` พร้อม `RegionReplacementOptions` เพื่อวางสีทับแบบทึบ.  
- **Do I need a license?** ใบอนุญาตทดลองใช้งานทำงานได้สำหรับการประเมิน; จำเป็นต้องมีใบอนุญาตเชิงพาณิชย์สำหรับการใช้งานจริง.  
- **Is the output a PDF or an image file?** ขั้นตอน rasterization จะสร้าง PDF ที่แต่ละหน้ามีรูปภาพ พร้อมสำหรับการลบข้อมูล.  

## “convert docx to image” คืออะไร?
การ rasterize ไฟล์ DOCX จะเปลี่ยนทุกหน้าให้เป็นภาพ (โดยปกติฝังอยู่ใน PDF) การแปลงนี้ทำให้ข้อความไม่สามารถเลือกได้ ทำให้การลบข้อมูลต่อไปเป็นแบบถาวรและป้องกันการปลอมแปลง

## ทำไมต้องใช้ GroupDocs Redaction for Java?
- **Accurate layout preservation** – การจัดรูปแบบ Word ดั้งเดิมจะคงอยู่อย่างแม่นยำ  
- **Fine‑grained redaction** – คุณสามารถกำหนดเป้าหมายเป็นพื้นที่เฉพาะ ภาพ หรือทั้งหน้าได้  
- **Seamless Maven integration** – *groupdocs maven dependency* มีน้ำหนักเบาและอัปเดตเป็นประจำ  
- **Cross‑platform support** – ทำงานบน OS ใดก็ได้ที่รัน Java 8+

## ข้อกำหนดเบื้องต้น
- ติดตั้ง JDK 8 หรือใหม่กว่า  
- IDE เช่น IntelliJ IDEA, Eclipse หรือ NetBeans  
- การเชื่อมต่ออินเทอร์เน็ตเพื่อดาวน์โหลด Maven artifacts หรือ JAR โดยตรง  
- ความรู้พื้นฐานของ Java และความคุ้นเคยกับ Maven  

## การตั้งค่า GroupDocs.Redaction สำหรับ Java

### Maven Dependency (groupdocs maven dependency)

เพิ่มรีโพสิตอรีของ GroupDocs อย่างเป็นทางการและไลบรารี Redaction ลงใน `pom.xml` ของคุณ:

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

**Direct Download** – หากคุณไม่ต้องการใช้ Maven ให้ดาวน์โหลด JAR ล่าสุดจากหน้าอย่างเป็นทางการ: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### การรับใบอนุญาต
1. ขอ **free trial license** จากพอร์ทัลของ GroupDocs  
2. สำหรับการใช้งานในสภาพแวดล้อมการผลิต ให้ซื้อ **commercial license** และแทนที่คีย์ทดลองด้วยคีย์ถาวรของคุณ  

## คู่มือขั้นตอนต่อขั้นตอน

### ขั้นตอนที่ 1: นำเข้าคลาสที่จำเป็น (how to rasterize word)

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.RasterizationOptions;
import java.io.ByteArrayInputStream;
import java.io.ByteArrayOutputStream;
import java.nio.file.Files;
import java.nio.file.Paths;
```

### ขั้นตอนที่ 2: โหลดและ rasterize DOCX (convert docx to image)

```java
String inputFilePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
ByteArrayOutputStream stream = new ByteArrayOutputStream();

try (Redactor rasterizer = new Redactor(inputFilePath)) {
    // Enable rasterization options.
    RasterizationOptions options = new RasterizationOptions();
    options.setEnabled(true);
    
    // Save the document as a byte array in rasterized form.
    rasterizer.save(stream, options);
}
```

**Explanation:** `RasterizationOptions` บอก GroupDocs ให้เรนเดอร์แต่ละหน้าเป็นภาพ `ByteArrayOutputStream` เก็บผลลัพธ์ในหน่วยความจำ พร้อมสำหรับขั้นตอนต่อไปโดยไม่ต้องเขียนไฟล์ชั่วคราว

### ขั้นตอนที่ 3: เตรียมผลลัพธ์ที่ rasterized สำหรับการลบข้อมูล

```java
ByteArrayInputStream inputStream = new ByteArrayInputStream(stream.toByteArray());
```

ขณะนี้ PDF ที่ rasterized พร้อมใช้งานเป็น `InputStream` ซึ่งคุณสามารถส่งตรงเข้าไปยังเอนจินการลบข้อมูลได้

### ขั้นตอนที่ 4: ใช้ Image Area Redaction (how to redact word)

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorChangeLog;
import com.groupdocs.redaction.redactions.ImageAreaRedaction;
import com.groupdocs.redaction.redactions.RegionReplacementOptions;
import java.awt.Color;
import java.awt.Dimension;
import java.awt.Point;
import java.io.FileOutputStream;

try (Redactor redactor = new Redactor(inputStream)) {
    // Define the area for redaction.
    Point startPoint = new Point(1160, 2375);
    Dimension size = new Dimension(1050, 720);

    // Set up replacement options with a blue color overlay.
    RegionReplacementOptions replaceWithBlue = new RegionReplacementOptions(Color.BLUE, size);

    // Apply the image area redaction.
    RedactorChangeLog result = redactor.apply(new ImageAreaRedaction(startPoint, replaceWithBlue));

    if (result.getStatus() != Redactor.RedactionStatus.Failed) {
        // Save the final document to an output directory.
        String outputPath = "YOUR_OUTPUT_DIRECTORY/sample_raster.pdf";
        try (FileOutputStream fileStream = new FileOutputStream(outputPath)) {
            RasterizationOptions saveOptions = new RasterizationOptions();
            saveOptions.setEnabled(false);
            redactor.save(fileStream, saveOptions);
        }
    }
}
```

**Explanation:**  
- `ImageAreaRedaction` กำหนดเป้าหมายเป็นพื้นที่สี่เหลี่ยมที่ระบุโดย `startPoint` และ `size`  
- `RegionReplacementOptions` ให้คุณเลือกสีทับ (สีฟ้าในตัวอย่างนี้) และขนาดของสี่เหลี่ยมทดแทน  
- หลังจากทำการลบข้อมูล เอกสารจะถูกบันทึกเป็น PDF ที่ rasterized พร้อมกับพื้นที่ที่สำคัญถูกซ่อนอย่างปลอดภัย  

## การประยุกต์ใช้ (how to redact word)

| Scenario | Why Rasterize & Redact? |
|----------|--------------------------|
| **Legal contracts** | รับประกันความลับของลูกค้าก่อนแชร์ร่าง |
| **Medical records** | ลบ PHI ขณะคงรูปแบบรายงานต้นฉบับ |
| **Financial statements** | ปิดบังหมายเลขบัญชีหรือตัวเลขสำคัญสำหรับการตรวจสอบภายนอก |

## ข้อควรพิจารณาด้านประสิทธิภาพ
- **Memory Management:** ใช้สตรีม (`ByteArrayOutputStream` / `ByteArrayInputStream`) เพื่อหลีกเลี่ยงการโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ  
- **CPU Usage:** การ rasterization ใช้ CPU มาก; พิจารณาเพิ่ม heap ของ JVM (`-Xmx2g`) สำหรับไฟล์ DOCX ขนาดใหญ่  
- **Version Updates:** รักษาไลบรารี GroupDocs ให้เป็นเวอร์ชันล่าสุด (เช่น 24.9) เพื่อรับประโยชน์จากการปรับปรุงประสิทธิภาพและการแก้บั๊ก  

## ปัญหาทั่วไปและวิธีแก้ (hide text java)

| Issue | Solution |
|-------|----------|
| **OutOfMemoryError** when processing large DOCX | ประมวลผลเอกสารเป็นส่วน ๆ หรือเพิ่มขนาด heap ของ JVM |
| **Redaction not applied** | ตรวจสอบว่า `result.getStatus()` ไม่เป็น `Failed` และพิกัดอยู่ในขอบเขตของหน้า |
| **Output PDF blank** | ตรวจสอบว่า `RasterizationOptions.setEnabled(false)` ถูกตั้งค่าเฉพาะหลังการลบข้อมูล; ควรเป็น `true` ในระหว่าง rasterization เริ่มต้น |

## คำถามที่พบบ่อย

**Q: What does “convert docx to image” actually produce?**  
A: กระบวนการสร้าง PDF ที่แต่ละหน้ามี bitmap ฝังอยู่ ทำให้ข้อความไม่สามารถเลือกได้และปลอดภัยสำหรับการลบข้อมูล  

**Q: Can I use GroupDocs Redaction for other file types?**  
A: ใช่, รองรับ PDF, ภาพ, และรูปแบบเอกสารอื่น ๆ มากมาย  

**Q: How does the temporary license work?**  
A: ใบอนุญาตทดลองใช้งานเปิดใช้งานทุกฟีเจอร์เป็นระยะเวลาจำกัด ให้คุณประเมินการ rasterization และการลบข้อมูลโดยไม่มีข้อจำกัด  

**Q: Is there a way to redact multiple regions at once?**  
A: แน่นอน—เรียก `redactor.apply()` หลายครั้งหรือส่งคอลเลกชันของอ็อบเจ็กต์ `ImageAreaRedaction`  

**Q: Do I need to convert the DOCX to PDF first?**  
A: ไม่จำเป็น Redactor สามารถ rasterize DOCX โดยตรงและส่งออกเป็น PDF ในขั้นตอนเดียวตามที่แสดงด้านบน  

---

**อัปเดตล่าสุด:** 2025-12-21  
**ทดสอบด้วย:** GroupDocs.Redaction 24.9 (Java)  
**ผู้เขียน:** GroupDocs