---
date: '2026-05-17'
description: เรียนรู้วิธีแปลง PDF เป็นระดับสีเทาโดยใช้ GroupDocs.Redaction สำหรับ
  Java, ใช้ฟิลเตอร์ระดับสีเทา, และทำให้เอกสารของคุณปลอดภัยและมีคุณภาพสูง
keywords:
- how to rasterize pdf
- java pdf to image
- apply grayscale filter pdf
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to rasterize PDF to grayscale using GroupDocs.Redaction for
    Java, apply a grayscale filter, and keep your documents secure and high‑quality.
  headline: How to rasterize PDF to grayscale with GroupDocs.Redaction Java – Secure
    and Optimize Your Documents
  type: TechArticle
- questions:
  - answer: In GroupDocs.Redaction, the grayscale option is tied to rasterization,
      which ensures consistent results and adds a security layer.
    question: Can I convert documents to grayscale without rasterization?
  - answer: All major formats supported by GroupDocs.Redaction—including DOCX, PDF,
      XLSX, PPTX, RTF, and more than 100 others—can be rasterized and converted to
      grayscale.
    question: What document formats support grayscale rasterization?
  - answer: Yes. Text‑heavy files may grow, while image‑heavy files might shrink.
      DPI settings have the biggest impact.
    question: Will rasterization affect the file size of my documents?
  - answer: No. Rasterization is one‑way; keep a backup of the original if you need
      to revert.
    question: Is it possible to reverse the grayscale rasterization process?
  - answer: Use a higher DPI (300 + for print quality) and choose PDF as the output
      format for best archival results.
    question: How can I optimize the quality of grayscale rasterized documents?
  type: FAQPage
title: วิธีแปลง PDF เป็นระดับสีเทาด้วย GroupDocs.Redaction Java – ปรับความปลอดภัยและเพิ่มประสิทธิภาพเอกสารของคุณ
type: docs
url: /th/java/rasterization-options/grayscale-rasterization-groupdocs-redaction-java/
weight: 1
---

# วิธีแปลง PDF เป็นระดับสีเทาด้วย GroupDocs.Redaction Java

หากคุณต้องการ **แปลง PDF เป็นภาพราสเตอร์** เป็นระดับสีเทาในขณะที่ทำให้เอกสารของคุณปลอดภัย ดูเป็นมืออาชีพ และง่ายต่อการเก็บรักษา คุณมาถูกที่แล้ว ในบทแนะนำนี้เราจะอธิบายขั้นตอนที่แน่นอนเพื่อแปลงไฟล์ DOCX, PDF หรือไฟล์ที่รองรับอื่น ๆ ที่มีสีสันให้เป็นเวอร์ชันราสเตอร์สีเทาที่สะอาดโดยใช้ GroupDocs.Redaction สำหรับ Java คุณจะเข้าใจว่าทำไมการราสเตอร์จึงเพิ่มชั้นความปลอดภัย วิธีการตั้งค่าห้องสมุด และการจัดการทรัพยากรอย่างมีประสิทธิภาพ—ทั้งหมดนำเสนอในสไตล์เป็นมิตรและเป็นขั้นตอนต่อขั้นตอน

## คำตอบด่วน
- **การราสเตอร์สีเทาทำอะไร?** มันจะแปลงแต่ละหน้เป็นภาพความละเอียดสูงแล้วใช้ฟิลเตอร์สีเทา เพื่อลบข้อมูลสีทั้งหมด  
- **ทำไมต้องใช้ GroupDocs.Redaction สำหรับเรื่องนี้?** มันรวมความปลอดภัยของการลบข้อมูลด้วยการราสเตอร์ใน API เดียวที่ใช้งานง่าย  
- **รูปแบบใดบ้างที่รองรับ?** DOCX, PDF, XLSX, PPTX, RTF และรูปแบบอื่น ๆ มากกว่า 100 รูปแบบ  
- **ฉันต้องการไลเซนส์หรือไม่?** จำเป็นต้องมีไลเซนส์ GroupDocs.Redaction ที่ถูกต้องสำหรับการใช้งานจริง; มีการทดลองใช้ฟรีสำหรับการทดสอบ  
- **ต้องการเวอร์ชัน Java ใด?** JDK 8 หรือสูงกว่า  

## วิธีแปลง PDF เป็นสีเทา?

โหลดเอกสารต้นฉบับของคุณด้วย `new Redactor("path/to/file")` เปิดใช้งานการราสเตอร์ผ่าน `RasterizationOptions` เพิ่มตัวเลือกขั้นสูงสีเทา แล้วเรียก `save()`—การแปลงทั้งหมดทำในไม่กี่บรรทัดสั้น ๆ วิธีนี้รับประกันว่าทุกหน้าจะกลายเป็น PDF แบบภาพสีขาว‑ดำ ป้องกันการเลือกข้อความและทำให้ลักษณะการพิมพ์เป็นแบบเดียวกัน

## **create grayscale pdf** คืออะไร?

การสร้าง PDF สีเทาหมายถึงการแปลงทุกองค์ประกอบภาพของเอกสารต้นฉบับให้เป็นเฉดสีเทา ผลลัพธ์คือไฟล์ที่มีขนาดเล็กกว่าและเหมาะสำหรับการพิมพ์ ซึ่งกำจัดความรบกวนจากสีและเพิ่มประโยชน์ด้านความปลอดภัยเล็กน้อยเนื่องจากเนื้อหาเป็นภาพแล้ว

## ทำไมต้องใช้การราสเตอร์สีเทากับ GroupDocs.Redaction?

การราสเตอร์จะเปลี่ยนแต่ละหน้าเป็นภาพ ซึ่งหมายความว่าข้อความไม่สามารถคัดลอกหรือแก้ไขได้ และผลลัพธ์ภาพจะคงที่ในเครื่องพิมพ์และโปรแกรมดูไฟล์ต่าง ๆ GroupDocs.Redaction รองรับ **รูปแบบอินพุตและเอาต์พุตมากกว่า 100 รูปแบบ**—รวมถึง DOCX, XLSX, PPTX, HTML และประเภทภาพ—ดังนั้นคุณสามารถใช้กระบวนการเดียวกันกับเอกสารใด ๆ ที่คุณจัดการได้

## ข้อกำหนดเบื้องต้น

- Java Development Kit (JDK) 8 หรือใหม่กว่า ตรวจสอบด้วย `java -version`.  
- IDE (IntelliJ IDEA, Eclipse หรือ NetBeans) เพื่อการเขียนโค้ดและดีบักที่ง่ายขึ้น.  
- GroupDocs.Redaction สำหรับ Java ที่เพิ่มผ่าน Maven หรือ Gradle.  
- ตัวอย่างเอกสาร (เช่น DOCX หลายหน้า) ที่คุณสามารถทดลองได้อย่างปลอดภัย.  
- พื้นที่ดิสก์เพียงพอสำหรับผลลัพธ์ที่ราสเตอร์ (ไฟล์ราสเตอร์อาจใหญ่กแหล่งที่มา).  

## นำเข้าแพ็กเกจ

การนำเข้าต่อไปนี้จะนำคลาสหลัก Redactor และ rasterization ที่จำเป็นสำหรับตัวอย่าง.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.options.RasterizationOptions;
import com.groupdocs.redaction.options.AdvancedRasterizationOptions;
```

## ขั้นตอนที่ 1: เริ่มต้นอ็อบเจกต์ Redactor

คลาส `Redactor` เป็นจุดเริ่มต้นสำหรับการประมวลผลเอกสารทั้งหมดใน GroupDocs.Redaction การสร้างอินสแตนซ์เปิดทางให้โหลด แก้ไข และบันทึกเอกสาร.

```java
final Redactor redactor = new Redactor(Constants.MULTIPAGE_SAMPLE_DOCX);
```

แทนที่ `Constants.MULTIPAGE_SAMPLE_DOCX` ด้วยพาธของไฟล์ที่คุณต้องการแปลงเป็น PDF สีเทา.

## ขั้นตอนที่ 2: กำหนดค่า Save Options

คลาส `SaveOptions` กำหนดวิธีที่เอกสารที่ประมวลผลจะถูกเขียนลงดิสก์ รวมถึงรูปแบบและชื่อไฟล์.

```java
SaveOptions so = new SaveOptions();
so.setRedactedFileSuffix("_scan");
```

ผลลัพธ์จะถูกตั้งชื่อเป็น `yourfile_scan.pdf` (หรือรูปแบบที่คุณระบุภายหลัง).

## ขั้นตอนที่ 3: เปิดใช้งานการราสเตอร์

อ็อบเจกต์ `RasterizationOptions` เปิดใช้งานการเรนเดอร์แบบภาพของแต่ละหน้าก่อนบันทึก.

```java
so.getRasterization().setEnabled(true);
```

## ขั้นตอนที่ 4: ใช้การแปลงเป็นสีเทา

`AdvancedRasterizationOptions.Grayscale` เป็นแฟล็กที่บังคับให้ภาพที่ราสเตอร์ใช้เฉดสีเทาเท่านั้น.

```java
so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Grayscale);
```

## ขั้นตอนที่ 5: ดำเนินการแปลงเอกสาร

การเรียก `save()` จะทำงานผ่านกระบวนการประมวลผลทั้งหมดและเขียนไฟล์ผลลัพธ์.

```java
redactor.save(so);
```

หลังจากบรรทัดนี้ทำงานเสร็จ คุณจะพบไฟล์ใหม่บนดิสก์ที่ราสเตอร์เต็มรูปแบบ สีเทา และบันทึกด้วยส่วนต่อท้าย `_scan`.

## ขั้นตอนที่ 6: การจัดการทรัพยากรอย่างเหมาะสม

เมธอด `close()` จะปล่อยทรัพยากรเนทีฟและลบไฟล์ชั่วคราว.

```java
finally { redactor.close(); }
```

สำหรับ Java รุ่นใหม่คุณสามารถใช้รูปแบบ try‑with‑resources ซึ่งจะปิด `Redactor` โดยอัตโนมัติ:

```java
try (Redactor redactor = new Redactor(Constants.MULTIPAGE_SAMPLE_DOCX)) {
    // Your processing code here
}
// Automatic cleanup happens here
```

ทั้งสองวิธีปลอดภัย; วิธีที่สองสั้นกว่า.

## ตัวเลือกการกำหนดค่าขั้นสูง

### ปรับ DPI เพื่อคุณภาพหรือขนาด

DPI ที่สูงให้ภาพคมชัดขึ้น (เหมาะสำหรับการพิมพ์) ในขณะที่ DPI ที่ต่ำจะลดขนาดไฟล์ การสมดุลที่พบบ่อยคือ 150 DPI สำหรับการดูบนหน้าจอและ 300 DPI สำหรับ PDF ที่พร้อมพิมพ์.

```java
saveOptions.getRasterization().setDpi(300); // High quality for printing
// or
saveOptions.getRasterization().setDpi(150); // Balanced quality and size
```

### เลือกรูปแบบเอาต์พุต

คุณสามารถบังคับผลลัพธ์ที่ราสเตอร์ให้เป็นรูปแบบคอนเทนเนอร์เฉพาะ เช่น PDF, TIFF หรือ PNG. PDF เป็นรูปแบบการเก็บถาวรที่ใช้กันมากที่สุด.

```java
saveOptions.setRasterizationFormat(RasterizationFormat.PDF);
```

## กรณีการใช้งานทั่วไป

- **การเก็บเอกสารทางกฎหมาย** – สร้าง PDF สีเทาที่ไม่สามารถแก้ไขได้  
- **รายงานพร้อมพิมพ์** – รับประกันผลลัพธ์สีขาว‑ดำที่สม่ำเสมอสำหรับการพิมพ์จำนวนมาก.  
- **กระบวนการทำงานตามข้อกำหนด** – ผสานการลบข้อมูลกับการราสเตอร์สีเทาเพื่อให้เป็นไปตามข้อกำหนดความเป็นส่วนตัวของข้อมูลที่เข้มงวด.  

## ปัญหาทั่วไปและวิธีแก้

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|--------|---------|
| ไฟล์ผลลัพธ์ใหญ่กว่าที่คาดหวัง | ตั้งค่า DPI สูงเกินไปหรือปิดการบีบอัดภาพ | ลด DPI (เช่น 150) หรือเปิดการบีบอัดใน `RasterizationOptions`. |
| ข้อความดูเบลอ | DPI ไม่เพียงพอสำหรับขนาดฟอนต์ต้นฉบับ | เพิ่ม DPI เป็น 300 หรือสูงกว่า. |
| กระบวนการโยน `OutOfMemoryError` กับเอกสารขนาดใหญ่ | โหลดเอกสารทั้งหมดเข้าสู่หน่วยความจำ | ใช้ API สตรีมมิ่งหรือประมวลผลหน้าเป็นชุดถ้ารองรับ. |
| ไม่ได้ใช้สีเทา | ตัวเลือกขั้นสูงไม่ได้เพิ่มอย่างถูกต้อง | ตรวจสอบว่า `addAdvancedOption(AdvancedRasterizationOptions.Grayscale)` ถูกเรียกก่อน `save()`. |

## คำถามที่พบบ่อย

**Q: ฉันสามารถแปลงเอกสารเป็นสีเทาโดยไม่ราสเตอร์ได้หรือไม่?**  
A: ใน GroupDocs.Redaction ตัวเลือกสีเทาจะเชื่อมกับการราสเตอร์ ซึ่งทำให้ผลลัพธ์สม่ำเสมอและเพิ่มชั้นความปลอดภัย.

**Q: รูปแบบเอกสารใดบ้างที่รองรับการราสเตอร์สีเทา?**  
A: รูปแบบหลักทั้งหมดที่ GroupDocs.Redaction รองรับ—รวมถึง DOCX, PDF, XLSX, PPTX, RTF และอื่น ๆ มากกว่า 100 รูปแบบ—สามารถราสเตอร์และแปลงเป็นสีเทาได้.

**Q: การราสเตอร์จะส่งผลต่อขนาดไฟล์ของเอกสารหรือไม่?**  
A: ใช่ ไฟล์ที่มีข้อความมากอาจใหญ่ขึ้น ในขณะที่ไฟล์ที่มีภาพมากอาจเล็กลง การตั้งค่า DPI มีผลมากที่สุด.

**Q: สามารถย้อนกลับกระบวนการราสเตอร์สีเทาได้หรือไม่?**  
A: ไม่ได้ การราสเตอร์เป็นกระบวนการทางเดียว; ควรเก็บสำเนาเอกสารต้นฉบับไว้หากต้องการย้อนกลับ.

**Q: ฉันจะปรับปรุงคุณภาพของเอกสารที่ราสเตอร์สีเทาได้อย่างไร?**  
A: ใช้ DPI ที่สูงขึ้น (300 + สำหรับคุณภาพการพิมพ์) และเลือก PDF เป็นรูปแบบเอาต์พุตเพื่อผลลัพธ์การเก็บถาวรที่ดีที่สุด.

## สรุป

ตอนนี้คุณมีสูตรครบถ้วนพร้อมใช้งานในระดับการผลิตเพื่อ **แปลง PDF เป็นสีเทา** ด้วย GroupDocs.Redaction สำหรับ Java การเปิดใช้งานการราสเตอร์ การเพิ่มตัวเลือกขั้นสูงสีเทา และการจัดการทรัพยากรอย่างรับผิดชอบ จะช่วยให้คุณสร้างเอกสารที่ปลอดภัยและเหมาะสำหรับการพิมพ์ซึ่งสอดคล้องกับมาตรฐานการปฏิบัติตามและมีลักษณะเหมือนกันในทุกโปรแกรมดู

---

**อัปเดตล่าสุด:** 2026-05-17  
**ทดสอบด้วย:** GroupDocs.Redaction 23.11 for Java  
**ผู้เขียน:** GroupDocs  

---

## คำหลักเป้าหมาย:

**คีย์เวิร์ดหลัก (ความสำคัญสูงสุด):**  
how to rasterize pdf

**คีย์เวิร์ดรอง (สนับสนุน):**  
java pdf to image, apply grayscale filter pdf

## บทแนะนำที่เกี่ยวข้อง

- [บทแนะนำตัวเลือกการราสเตอร์สำหรับ GroupDocs.Redaction Java](/redaction/java/rasterization-options/)
- [วิธีใช้ groupdocs redaction สำหรับ Java: การราสเตอร์ล่วงหน้าในเอกสาร Word](/redaction/java/rasterization-options/groupdocs-redaction-java-pre-rasterization-word-docs/)
- [การราสเตอร์สัญญาณรบกวนแบบกำหนดเองใน Java: ปกป้องข้อมูลที่ละเอียดอ่อนด้วย GroupDocs.Redaction](/redaction/java/rasterization-options/java-groupdocs-redaction-custom-noise-rasterization/)