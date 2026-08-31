---
date: '2026-03-22'
description: เรียนรู้วิธีลบข้อมูลในภาพสแกนด้วย Java และ GroupDocs.Redaction คู่มือแบบขั้นตอนต่อขั้นตอนนี้ครอบคลุมการตั้งค่า
  การลบข้อมูลในพื้นที่ของภาพ และการตรวจสอบ.
keywords:
- Java image redaction
- GroupDocs.Redaction for Java
- image area redaction
title: วิธีลบข้อมูลในภาพสแกนด้วย Java โดยใช้ GroupDocs
type: docs
url: /th/java/image-redaction/java-image-redaction-groupdocs-tutorial/
weight: 1
---

# วิธีการลบข้อมูลในภาพสแกนด้วย Java โดยใช้ GroupDocs

ในยุคดิจิทัลปัจจุบัน, **redact scanned image java** มีความสำคัญต่อการปกป้องความเป็นส่วนตัวและการปฏิบัติตามข้อกำหนดด้านการปฏิบัติตามกฎระเบียบ ไม่ว่าคุณจะต้องการซ่อนข้อมูลส่วนบุคคลในสัญญาที่สแกนหรือทำให้รายละเอียดของผู้ป่วยในภาพทางการแพทย์ไม่ชัดเจน บทแนะนำนี้จะแสดงให้คุณเห็น **how to redact image** อย่างรวดเร็วและเชื่อถือได้โดยใช้ **GroupDocs.Redaction for Java** เราจะเดินผ่านทุกขั้นตอนตั้งแต่การตั้งค่าโครงการจนถึงการตรวจสอบว่าการลบข้อมูลสำเร็จหรือไม่ เพื่อให้คุณสามารถผสานโซลูชันนี้เข้ากับแอปพลิเคชัน Java ใดก็ได้ด้วยความมั่นใจ.

## คำตอบอย่างรวดเร็ว
- **ไลบรารีใดที่จัดการการลบข้อมูลภาพใน Java?** GroupDocs.Redaction for Java  
- **ฉันสามารถเลือกสีสำหรับการลบข้อมูลได้หรือไม่?** Yes – any `java.awt.Color` (e.g., `Color.BLUE`)  
- **ต้องการใบอนุญาตสำหรับการใช้งานจริงหรือไม่?** Yes, a valid GroupDocs license is needed  
- **ภาพต้นฉบับจะถูกเขียนทับหรือไม่?** No – you save the result to a new file  
- **เวอร์ชัน Java ที่รองรับคืออะไร?** Java 8+ (compatible with modern JDKs)

## การลบข้อมูลภาพคืออะไรและทำไมต้องลบข้อมูลภาพสแกนด้วย Java?
การลบข้อมูลภาพหมายถึงการทำให้ข้อมูลภาพที่ละเอียดอ่อน—เช่น ชื่อ, ตัวเลข หรือลายเซ็น—หายไปอย่างถาวรเพื่อไม่ให้สามารถกู้คืนได้ เมื่อคุณทำงานกับเอกสารที่สแกน ข้อมูลจะฝังอยู่ในรูปพิกเซล ทำให้เครื่องมือการลบข้อความแบบดั้งเดิมไม่มีประสิทธิภาพ การใช้ GroupDocs.Redaction ช่วยให้คุณกำหนดพื้นที่พิกเซลที่ต้องการและแทนที่ด้วยสีทึบ เพื่อให้ข้อมูลถูกลบอย่างแท้จริง

## ข้อกำหนดเบื้องต้น
- **JDK 8 หรือใหม่กว่า** installed  
- **Maven** (หรือเครื่องมือสร้างอื่น) สำหรับการจัดการ dependencies  
- IDE เช่น **IntelliJ IDEA**, **Eclipse**, หรือ **NetBeans**  
- ความรู้พื้นฐานของ Java และความคุ้นเคยกับการทำงานกับไฟล์ I/O  

## การตั้งค่า GroupDocs.Redaction สำหรับ Java

### การตั้งค่า Maven
เพิ่มรีโพซิทอรีของ GroupDocs และ dependency ลงในไฟล์ `pom.xml` ของคุณ:

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
- **Free Trial:** ลงทะเบียนเพื่อทดลองใช้ API.  
- **Temporary License:** ใช้คีย์ชั่วคราวสำหรับการทดสอบต่อเนื่อง.  
- **Full Purchase:** รับใบอนุญาตการผลิตเพื่อการใช้งานไม่จำกัด.  

## คู่มือการใช้งาน

เราจะแบ่งการใช้งานออกเป็นสองฟีเจอร์หลัก: **Image Area Redaction** (การปิดบังจริง) และ **Redaction Status Check** (การตรวจสอบความสำเร็จ).

### วิธีการลบข้อมูลภาพเอกสารสแกน – ขั้นตอน 1: เริ่มต้น Redactor
แรกสุด สร้างอินสแตนซ์ `Redactor` ที่ชี้ไปยังภาพที่คุณต้องการประมวลผล.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_JPG");
```

### ขั้นตอน 2: กำหนดพารามิเตอร์การลบข้อมูล
ระบุมุมบนซ้าย (`Point`) และขนาด (`Dimension`) ของสี่เหลี่ยมที่ต้องการซ่อน ในตัวอย่างนี้เราใช้สีเติมสีน้ำเงิน.

```java
// Define the position on the image where redaction starts.
Point samplePoint = new Point(385, 485);

// Define the size of the area to be redacted.
Dimension sampleSize = new Dimension(1793, 2069);
```

### ขั้นตอน 3: ใช้การลบข้อมูล
สร้างอ็อบเจ็กต์ `ImageAreaRedaction` พร้อมกับ `RegionReplacementOptions` แล้วเรียกใช้งาน เมธอดจะคืนค่า `RedactorChangeLog` ที่บอกว่าการดำเนินการสำเร็จหรือไม่.

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
ควรปิด `Redactor` เสมอเมื่อทำงานเสร็จ เพื่อปล่อยทรัพยากรเนทีฟ.

```java
redactor.close();
```

### วิธีการตรวจสอบการลบข้อมูล – การตรวจสอบสถานะ
หลังจากทำการลบข้อมูลแล้ว คุณสามารถตรวจสอบ `RedactorChangeLog` เพื่อยืนยันว่าการดำเนินการไม่ล้มเหลว.

```java
if (result != null && result.getStatus() != RedactionStatus.Failed) {
    System.out.println("Redaction was successful.");
} else {
    System.out.println("Redaction failed.");
}
```

## การประยุกต์ใช้งานจริง
- **Confidential Document Handling:** ทำการซ่อนข้อมูลส่วนบุคคลในสัญญาที่สแกนโดยอัตโนมัติก่อนแชร์กับบุคคลภายนอก.  
- **Legal Documentation:** รับรองการปฏิบัติตาม GDPR หรือ HIPAA โดยการลบข้อมูลระบุตัวตนในภาพหลักฐาน.  
- **Medical Records:** ปกป้องความเป็นส่วนตัวของผู้ป่วยโดยทำให้ใบหน้าหรือบันทึกมือในภาพรังสีไม่ชัดเจน.  

## ข้อควรพิจารณาด้านประสิทธิภาพ
- **Batch Processing:** โหลดและลบข้อมูลภาพเป็นชุดเล็ก ๆ เพื่อรักษาการใช้หน่วยความจำให้ต่ำ.  
- **Efficient Data Structures:** ใช้ซ้ำอ็อบเจ็กต์ `Point` และ `Dimension` เมื่อต้องประมวลผลหลายภาพ.  
- **Stay Updated:** อัปเกรดเป็นเวอร์ชันล่าสุดของ GroupDocs.Redaction อย่างสม่ำเสมอเพื่อปรับปรุงประสิทธิภาพและแก้บั๊ก.  

## ปัญหาที่พบบ่อยและวิธีแก้

| Issue | Cause | Fix |
|-------|-------|-----|
| **การลบข้อมูลล้มเหลวด้วยสถานะ `Failed`** | เส้นทางไฟล์ไม่ถูกต้องหรือรูปแบบภาพไม่รองรับ | ตรวจสอบว่าภาพมีอยู่และเป็นรูปแบบที่รองรับ (JPG, PNG, BMP). |
| **ไฟล์ผลลัพธ์ว่างเปล่า** | `redactor.save()` ถูกเรียกก่อนการลบข้อมูลเสร็จสมบูรณ์ | ตรวจสอบว่า `apply()` คืนค่าสถานะสำเร็จก่อนทำการบันทึก. |
| **สีไม่ถูกนำไปใช้** | ใช้สีที่โปร่งใส | เลือก `Color` ที่ทึบ (เช่น `Color.BLACK` หรือ `Color.BLUE`). |

## คำถามที่พบบ่อย

**Q: ความแตกต่างระหว่าง `ImageAreaRedaction` กับการลบข้อความคืออะไร?**  
A: `ImageAreaRedaction` ทำงานบนพิกัดพิกเซล ในขณะที่การลบข้อความจะทำการวิเคราะห์ชั้น OCR เพื่อค้นหาและลบเนื้อหาข้อความ.

**Q: ฉันสามารถลบหลายพื้นที่ในภาพเดียวได้หรือไม่?**  
A: ได้—เรียก `redactor.apply()` ซ้ำหลายครั้งโดยใช้ `ImageAreaRedaction` ที่แตกต่างกันก่อนบันทึก.

**Q: GroupDocs.Redaction รองรับรูปแบบภาพอื่นเช่น TIFF หรือไม่?**  
A: ไลบรารีรองรับรูปแบบเรสเตอร์ทั่วไป (JPG, PNG, BMP, GIF) สำหรับ TIFF ให้แปลงเป็นรูปแบบที่รองรับก่อน.

**Q: ฉันจะทำการลบข้อมูลอัตโนมัติสำหรับโฟลเดอร์ของ PDF ที่สแกนได้อย่างไร?**  
A: ทำการวนลูปแต่ละภาพหน้าที่สกัดจาก PDF, ใช้ตรรกะการลบข้อมูลเดียวกัน, แล้วสร้าง PDF ใหม่โดยใช้ไลบรารี PDF.

**Q: มีวิธีดูตัวอย่างการลบข้อมูลก่อนบันทึกหรือไม่?**  
A: คุณสามารถเรนเดอร์ `Redactor` เป็น `BufferedImage` แล้วแสดงใน UI ของ Swing หรือ JavaFX ก่อนทำการบันทึกการเปลี่ยนแปลง.

## สรุป
ตอนนี้คุณมีคู่มือครบถ้วนพร้อมใช้งานในระดับการผลิตเกี่ยวกับ **how to redact image** และโดยเฉพาะ **redact scanned image java** ด้วย GroupDocs.Redaction for Java หากทำตามขั้นตอนข้างต้น คุณจะสามารถปกป้องข้อมูลภาพที่ละเอียดอ่อนได้ในหลากหลายอุตสาหกรรม สำรวจ API เพิ่มเติม—เช่น การลบข้อความหรือการลบหน้าของ PDF—เพื่อสร้างโซลูชันความเป็นส่วนตัวของข้อมูลที่ครอบคลุมสำหรับองค์กรของคุณ.

**แหล่งข้อมูล**  
- [Documentation](https://docs.groupdocs.com/redaction/java/)  
- [API Reference](https://reference.groupdocs.com/redaction/java)  
- [Download](https://releases.groupdocs.com/redaction/java/)  
- [GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- [Free Support Forum](https://forum.groupdocs.com/c/redaction/33)  
- [Temporary License](https://purchase.groupdocs.com/temporary-license/) 

---

**อัปเดตล่าสุด:** 2026-03-22  
**ทดสอบด้วย:** GroupDocs.Redaction 24.9 (Java)  
**ผู้เขียน:** GroupDocs