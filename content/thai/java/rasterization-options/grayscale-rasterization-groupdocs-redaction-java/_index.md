---
date: '2026-02-13'
description: เรียนรู้วิธีสร้าง PDF แบบสีเทาโดยใช้ GroupDocs.Redaction สำหรับ Java,
  แปลง PDF เป็นสีเทาอย่างปลอดภัยพร้อมคงคุณภาพของเอกสาร.
keywords:
- GroupDocs.Redaction
- Java
- Document Processing
title: วิธีสร้าง PDF สีเทาด้วย GroupDocs.Redaction Java – ปกป้องและเพิ่มประสิทธิภาพเอกสารของคุณ
type: docs
url: /th/java/rasterization-options/grayscale-rasterization-groupdocs-redaction-java/
weight: 1
---

# GroupDocs.Redaction Java: คู่มือการทำ Grayscale Rasterization

## Introduction

หากคุณต้องการ **สร้างไฟล์ pdf แบบสีเทา** พร้อมกับรักษาความปลอดภัยและความเป็นมืออาชีพของเอกสารไว้ คุณมาถูกที่แล้ว ในบทเรียนนี้เราจะพาคุณผ่านขั้นตอนที่แน่นอนเพื่อแปลงไฟล์ DOCX, PDF หรือไฟล์ที่รองรับอื่น ๆ ที่มีสีสันให้เป็นเวอร์ชันสีเทาที่แรสเตอร์ไลซ์โดยใช้ GroupDocs.Redaction สำหรับ Java คุณจะได้เรียนรู้ว่าทำไมการแรสเตอร์ไลซ์จึงเพิ่มชั้นความปลอดภัยเพิ่มเติม วิธีการตั้งค่าห้องสมุด และวิธีจัดการทรัพยากรอย่างมีประสิทธิภาพ—all ในสไตล์สนทนาแบบขั้นตอนต่อขั้นตอน

## Quick Answers
- **Grayscale rasterization ทำอะไร?** มันจะแปลงแต่ละหน้าของเอกสารเป็นภาพความละเอียดสูงแล้วใส่ฟิลเตอร์สีเทา เพื่อลบข้อมูลสีทั้งหมดออก  
- **ทำไมต้องใช้ GroupDocs.Redaction สำหรับเรื่องนี้?** มันรวมความปลอดภัยของการลบข้อมูล (redaction) กับตัวเลือกการแรสเตอร์ไลซ์ที่ทรงพลังไว้ใน API เดียว  
- **ฟอร์แมตที่รองรับมีอะไรบ้าง?** DOCX, PDF, XLSX, PPTX, RTF และอื่น ๆ อีกมากมาย  
- **ต้องมีลิขสิทธิ์หรือไม่?** จำเป็นต้องมีลิขสิทธิ์ GroupDocs.Redaction ที่ใช้งานได้สำหรับการผลิต; มีรุ่นทดลองสำหรับการทดสอบ  
- **ต้องใช้ Java เวอร์ชันใด?** JDK 8 หรือสูงกว่า

## What is **create grayscale pdf**?

การสร้าง PDF แบบสีเทาหมายถึงการแปลงทุกองค์ประกอบภาพของเอกสารต้นฉบับให้เป็นเฉดสีเทา ผลลัพธ์คือไฟล์ที่มีขนาดเล็กกว่าและเหมาะสำหรับการพิมพ์ ซึ่งกำจัดการรบกวนจากสีและให้ประโยชน์ด้านความปลอดภัยเล็กน้อยเนื่องจากเนื้อหาเป็นรูปภาพแล้ว

## Why use grayscale rasterization with GroupDocs.Redaction?

- **ความปลอดภัยที่เพิ่มขึ้น** – หน้าแรสเตอร์ไลซ์ไม่สามารถเลือก, คัดลอก หรือแก้ไขเป็นข้อความได้  
- **ลักษณะที่สม่ำเสมอ** – สีถูกลบออก ทำให้ดูเป็นระเบียบและเป็นมืออาชีพ  
- **รองรับฟอร์แมตหลากหลาย** – API เดียวทำงานกับ DOCX, PDF, PPTX และอื่น ๆ  
- **การควบคุมที่ละเอียด** – คุณสามารถปรับ DPI, ฟอร์แมตผลลัพธ์, และตัวเลือกขั้นสูงเช่นการแปลงเป็นสีเทาได้

## Prerequisites

- Java Development Kit (JDK) 8 หรือใหม่กว่า ตรวจสอบด้วย `java -version`  
- IDE (IntelliJ IDEA, Eclipse หรือ NetBeans) เพื่อความสะดวกในการเขียนโค้ดและดีบัก  
- GroupDocs.Redaction สำหรับ Java ที่เพิ่มผ่าน Maven หรือ Gradle  
- ตัวอย่างเอกสาร (เช่น DOCX หลายหน้า) ที่คุณสามารถทดลองได้อย่างปลอดภัย  
- พื้นที่ดิสก์เพียงพอสำหรับผลลัพธ์ที่แรสเตอร์ไลซ์ (ไฟล์แรสเตอร์อาจใหญ่ก่าไฟล์ต้นฉบับ)

## Import Packages

การตั้งค่าการนำเข้าให้ถูกต้องเหมือนกับการจัดระเบียบกล่องเครื่องมือก่อนเริ่มโครงการ การนำเข้าต่อไปนี้จะให้คุณเข้าถึงคลาส Redactor หลักและตัวเลือกการแรสเตอร์ไลซ์ที่เราต้องใช้

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.options.RasterizationOptions;
import com.groupdocs.redaction.options.AdvancedRasterizationOptions;
```

## Step 1: Initialize the Redactor Object

การสร้างอินสแตนซ์ `Redactor` จะเปิดประตูสู่ความสามารถทั้งหมดในการประมวลผลเอกสาร

```java
final Redactor redactor = new Redactor(Constants.MULTIPAGE_SAMPLE_DOCX);
```

เปลี่ยน `Constants.MULTIPAGE_SAMPLE_DOCX` ให้เป็นพาธของไฟล์ที่คุณต้องการแปลงเป็น PDF สีเทา

## Step 2: Configure Save Options

`SaveOptions` กำหนดวิธีการเขียนไฟล์สุดท้าย การเพิ่ม suffix ช่วยให้คุณเก็บไฟล์ต้นฉบับไว้ไม่เปลี่ยนแปลง

```java
SaveOptions so = new SaveOptions();
so.setRedactedFileSuffix("_scan");
```

ผลลัพธ์จะถูกตั้งชื่อเป็น `yourfile_scan.docx` (หรือฟอร์แมตที่คุณระบุในภายหลัง)

## Step 3: Enable Rasterization

การเปิดใช้งานการแรสเตอร์ไลซ์บอกให้เอนจินเรนเดอร์แต่ละหน้าเป็นภาพก่อนบันทึก

```java
so.getRasterization().setEnabled(true);
```

การแรสเตอร์ไลซ์เป็นพื้นฐานสำหรับการสร้าง PDF สีเทา เพราะมันแปลงเอกสารเป็นรูปแบบภาพ

## Step 4: Apply Grayscale Conversion

ตอนนี้เราจะเพิ่มฟิลเตอร์สีเทาเข้าไปใน pipeline ของการแรสเตอร์ไลซ์

```java
so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Grayscale);
```

ตัวเลือกนี้บังคับให้พิกเซลทุกตัวถูกเรนเดอร์เป็นเฉดสีเทา ทำให้คุณได้ผลลัพธ์ **create grayscale pdf** ที่ต้องการ

## Step 5: Execute the Document Transformation

คำสั่ง `save` จะรันโซ่การประมวลผลทั้งหมด

```java
redactor.save(so);
```

หลังจากบรรทัดนี้ทำงานเสร็จ คุณจะพบไฟล์ใหม่บนดิสก์ที่แรสเตอร์ไลซ์เต็มรูปแบบ, เป็นสีเทา, และบันทึกด้วย suffix `_scan`

## Step 6: Proper Resource Management

การทำความสะอาดทรัพยากรช่วยป้องกันไฟล์ล็อกและการรั่วไหลของหน่วยความจำ

```java
finally { redactor.close(); }
```

สำหรับ Java รุ่นใหม่คุณยังสามารถใช้รูปแบบ try‑with‑resources ที่ปิด `Redactor` โดยอัตโนมัติ:

```java
try (Redactor redactor = new Redactor(Constants.MULTIPAGE_SAMPLE_DOCX)) {
    // Your processing code here
}
// Automatic cleanup happens here
```

ทั้งสองวิธีปลอดภัย; วิธีหลังสั้นกว่า

## Advanced Configuration Options

### Adjust DPI for Quality or Size

DPI ที่สูงกว่าจะให้ภาพคมชัดขึ้น (เหมาะสำหรับการพิมพ์) ส่วน DPI ที่ต่ำจะลดขนาดไฟล์

```java
saveOptions.getRasterization().setDpi(300); // High quality for printing
// or
saveOptions.getRasterization().setDpi(150); // Balanced quality and size
```

### Choose an Output Format

คุณสามารถบังคับผลลัพธ์ที่แรสเตอร์ไลซ์ให้เป็นคอนเทนเนอร์ฟอร์แมตเฉพาะ เช่น PDF

```java
saveOptions.setRasterizationFormat(RasterizationFormat.PDF);
```

## Common Use Cases

- **การเก็บเอกสารทางกฎหมาย** – สร้าง PDF สีเทาแบบไม่เปลี่ยนแปลงที่ไม่สามารถแก้ไขได้  
- **รายงานพร้อมพิมพ์** – รับประกันผลลัพธ์ขาว‑ดำที่สม่ำเสมอสำหรับการพิมพ์จำนวนมาก  
- **กระบวนการปฏิบัติตามกฎ** – ผสานการลบข้อมูลกับการแรสเตอร์ไลซ์สีเทาเพื่อให้สอดคล้องกับระเบียบความเป็นส่วนตัวของข้อมูลที่เข้มงวด

## Common Issues and Solutions

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| ไฟล์ผลลัพธ์ใหญ่กว่าที่คาด | ตั้ง DPI สูงเกินไปหรือปิดการบีบอัดภาพ | ลด DPI (เช่น 150) หรือเปิดการบีบอัดใน `RasterizationOptions` |
| ข้อความดูเบลอ | DPI ไม่เพียงพอสำหรับขนาดฟอนต์ต้นฉบับ | เพิ่ม DPI เป็น 300 หรือสูงกว่า |
| กระบวนการโยน `OutOfMemoryError` กับเอกสารขนาดใหญ่ | โหลดเอกสารทั้งหมดเข้าสู่หน่วยความจำ | ใช้ API สตรีมมิ่งหรือประมวลผลหน้าเป็นชุดถ้ารองรับ |
| ไม่ได้แปลงเป็นสีเทา | ตัวเลือกขั้นสูงไม่ได้เพิ่มอย่างถูกต้อง | ตรวจสอบว่าเรียก `addAdvancedOption(AdvancedRasterizationOptions.Grayscale)` ก่อน `save()` |

## Frequently Asked Questions

**Q: สามารถแปลงเอกสารเป็นสีเทาโดยไม่แรสเตอร์ไลซ์ได้หรือไม่?**  
A: ใน GroupDocs.Redaction ตัวเลือกสีเทาถูกผูกกับการแรสเตอร์ไลซ์ ซึ่งทำให้ผลลัพธ์สม่ำเสมอและเพิ่มความปลอดภัย

**Q: ฟอร์แมตเอกสารใดบ้างที่รองรับการแรสเตอร์ไลซ์สีเทา?**  
A: ฟอร์แมตหลักทั้งหมดที่ GroupDocs.Redaction รองรับรวมถึง DOCX, PDF, XLSX, PPTX, RTF และอื่น ๆ สามารถแรสเตอร์ไลซ์และแปลงเป็นสีเทาได้

**Q: การแรสเตอร์ไลซ์จะส่งผลต่อขนาดไฟล์ของเอกสารหรือไม่?**  
A: ใช่ ไฟล์ที่มีข้อความเป็นส่วนใหญ่อาจเพิ่มขนาดขึ้น ในขณะที่ไฟล์ที่มีรูปภาพเป็นส่วนใหญ่อาจลดลง การตั้งค่า DPI มีผลมากที่สุด

**Q: สามารถย้อนกลับกระบวนการแรสเตอร์ไลซ์สีเทาได้หรือไม่?**  
A: ไม่ได้ การแรสเตอร์ไลซ์เป็นกระบวนการทางเดียว; ควรเก็บสำเนาไฟล์ต้นฉบับไว้หากต้องการกลับสู่สภาพเดิม

**Q: จะปรับคุณภาพของเอกสารที่แรสเตอร์ไลซ์สีเทาอย่างไร?**  
A: ใช้ DPI สูงกว่า (300 + สำหรับคุณภาพการพิมพ์) และเลือกฟอร์แมตผลลัพธ์ที่เหมาะสม (PDF เป็นที่นิยมสำหรับการเก็บรักษา)

## Conclusion

คุณมีสูตรครบถ้วนพร้อมใช้งานในระดับผลิตภัณฑ์เพื่อ **create grayscale pdf** ด้วย GroupDocs.Redaction สำหรับ Java แล้ว ด้วยการเปิดใช้งานการแรสเตอร์ไลซ์, เพิ่มตัวเลือกขั้นสูงสีเทา, และจัดการทรัพยากรอย่างรับผิดชอบ คุณสามารถผลิตเอกสารที่ปลอดภัย, พร้อมพิมพ์, และสอดคล้องกับมาตรฐานการปฏิบัติตามได้

---

**Last Updated:** 2026-02-13  
**Tested With:** GroupDocs.Redaction 23.11 for Java  
**Author:** GroupDocs  

---