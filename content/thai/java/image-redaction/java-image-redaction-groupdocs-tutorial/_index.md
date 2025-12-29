---
date: '2025-12-29'
description: เรียนรู้วิธีการลบข้อมูลในภาพเอกสารสแกนโดยใช้ GroupDocs.Redaction สำหรับ
  Java คู่มือขั้นตอนโดยละเอียดที่ครอบคลุมการตั้งค่า การลบข้อมูลในพื้นที่ภาพ และการตรวจสอบ
keywords:
- Java image redaction
- GroupDocs.Redaction for Java
- image area redaction
title: วิธีลบข้อมูลส่วนที่ต้องการจากภาพเอกสารสแกนด้วย GroupDocs ใน Java
type: docs
url: /th/java/image-redaction/java-image-redaction-groupdocs-tutorial/
weight: 1
---

# วิธีลบข้อมูลในภาพเอกสารสแกนด้วย GroupDocs ใน Java

ในยุคดิจิทัลปัจจุบัน การ **ลบข้อมูลในภาพเอกสารสแกน** เป็นสิ่งสำคัญสำหรับการปกป้องความเป็นส่วนตัวและการปฏิบัติตามข้อกำหนดด้านการปฏิบัติตามกฎระเบียบ ไม่ว่าคุณจะต้องการซ่อนข้อมูลส่วนบุคคลในสัญญาที่สแกนหรือทำให้รายละเอียดของผู้ป่วยในภาพทางการแพทย์ไม่ชัดเจน บทเรียนนี้จะแสดงให้คุณ **วิธีลบข้อมูลในภาพ** อย่างรวดเร็วและเชื่อถือได้โดยใช้ **GroupDocs.Redaction for Java** เราจะอธิบายทุกขั้นตอนตั้งแต่การตั้งค่าโครงการจนถึงการตรวจสอบว่าการลบข้อมูลสำเร็จหรือไม่ เพื่อให้คุณสามารถผสานโซลูชันนี้เข้ากับแอปพลิเคชัน Java ใดก็ได้ด้วยความมั่นใจ

## คำตอบด่วน
- **ไลบรารีใดที่จัดการการลบข้อมูลภาพใน Java?** GroupDocs.Redaction for Java  
- **ฉันสามารถเลือกสีสำหรับการลบข้อมูลได้หรือไม่?** Yes – any `java.awt.Color` (e.g., `Color.BLUE`)  
- **จำเป็นต้องมีใบอนุญาตสำหรับการใช้งานในสภาพแวดล้อมจริงหรือไม่?** Yes, a valid GroupDocs license is needed  
- **ภาพต้นฉบับจะถูกเขียนทับหรือไม่?** No – you save the result to a new file  
- **เวอร์ชัน Java ที่รองรับคืออะไร?** Java 8+ (compatible with modern JDKs)

## การลบข้อมูลภาพคืออะไรและทำไมต้องลบข้อมูลในภาพเอกสารสแกน?
การลบข้อมูลภาพหมายถึงการทำให้ข้อมูลภาพที่ละเอียดอ่อน—เช่น ชื่อ หมายเลข หรือลายเซ็น—ถูกบังอย่างถาวรเพื่อไม่ให้สามารถกู้คืนได้ เมื่อคุณทำงานกับเอกสารสแกน ข้อมูลจะถูกฝังเป็นพิกเซล ทำให้เครื่องมือการลบข้อมูลข้อความแบบดั้งเดิมไม่มีประสิทธิภาพ การใช้ GroupDocs.Redaction ช่วยให้คุณระบุพื้นที่พิกเซลที่ต้องการและแทนที่ด้วยสีทึบ เพื่อให้แน่ใจว่าข้อมูลถูกลบออกอย่างแท้จริง

## ข้อกำหนดเบื้องต้น
- **JDK 8 หรือใหม่กว่า** ติดตั้งแล้ว  
- **Maven** (หรือเครื่องมือสร้างอื่น) สำหรับการจัดการ dependencies  
- IDE เช่น **IntelliJ IDEA**, **Eclipse**, หรือ **NetBeans**  
- ความรู้พื้นฐานของ Java และความคุ้นเคยกับการทำงานกับไฟล์ I/O  

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
- **Free Trial:** ลงทะเบียนเพื่อทดลองใช้ API.  
- **Temporary License:** ใช้คีย์ชั่วคราวสำหรับการทดสอบต่อเนื่อง.  
- **Full Purchase:** รับใบอนุญาตการใช้งานในสภาพแวดล้อมจริงเพื่อการใช้งานไม่จำกัด.  

## คู่มือการใช้งาน

เราจะแบ่งการใช้งานออกเป็นสองฟีเจอร์หลัก: **Image Area Redaction** (การปิดบังจริง) และ **Redaction Status Check** (การตรวจสอบความสำเร็จ).

### วิธีลบข้อมูลภาพเอกสารสแกน – ขั้นตอน 1: เริ่มต้น Redactor
แรกสุด สร้างอินสแตนซ์ `Redactor` ที่ชี้ไปยังภาพที่ต้องการประมวลผล.

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
สร้างอ็อบเจ็กต์ `ImageAreaRedaction` พร้อมกับ `RegionReplacementOptions` แล้วดำเนินการ วิธีนี้จะคืนค่า `RedactorChangeLog` ที่บอกว่าการดำเนินการสำเร็จหรือไม่.

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
ควรปิด `Redactor` เสมอเมื่อทำงานเสร็จเพื่อปล่อยทรัพยากรเนทีฟ.

```java
redactor.close();
```

### วิธีตรวจสอบการลบข้อมูล – การตรวจสอบสถานะ
หลังจากทำการลบข้อมูลแล้ว คุณสามารถตรวจสอบ `RedactorChangeLog` เพื่อยืนยันว่าการดำเนินการไม่ได้ล้มเหลว.

```java
if (result != null && result.getStatus() != RedactionStatus.Failed) {
    System.out.println("Redaction was successful.");
} else {
    System.out.println("Redaction failed.");
}
```

## การใช้งานเชิงปฏิบัติ
- **Confidential Document Handling:** ปิดบังข้อมูลส่วนบุคคลในสัญญาที่สแกนโดยอัตโนมัติก่อนแชร์กับบุคคลภายนอก.  
- **Legal Documentation:** รับรองการปฏิบัติตาม GDPR หรือ HIPAA โดยลบข้อมูลระบุตัวตนในภาพหลักฐาน.  
- **Medical Records:** ปกป้องความเป็นส่วนตัวของผู้ป่วยโดยทำให้ใบหน้าหรือบันทึกมือในภาพรังสีไม่ชัดเจน.  

## การพิจารณาประสิทธิภาพ
- **Batch Processing:** โหลดและลบข้อมูลภาพเป็นชุดเล็ก ๆ เพื่อรักษาการใช้หน่วยความจำให้ต่ำ.  
- **Efficient Data Structures:** ใช้ซ้ำอ็อบเจ็กต์ `Point` และ `Dimension` เมื่อต้องประมวลผลภาพจำนวนมาก.  
- **Stay Updated:** อัปเกรดเป็นเวอร์ชันล่าสุดของ GroupDocs.Redaction อย่างสม่ำเสมอเพื่อปรับปรุงประสิทธิภาพและแก้ไขบั๊ก.  

## ปัญหาทั่วไปและวิธีแก้

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|-------|-----|
| **การลบข้อมูลล้มเหลวด้วยสถานะ `Failed`** | เส้นทางไฟล์ไม่ถูกต้องหรือรูปแบบภาพไม่รองรับ | ตรวจสอบว่าภาพมีอยู่และเป็นรูปแบบที่รองรับ (JPG, PNG, BMP). |
| **ไฟล์ผลลัพธ์ว่างเปล่า** | `redactor.save()` ถูกเรียกก่อนการลบข้อมูลเสร็จสมบูรณ์ | ตรวจสอบว่า `apply()` คืนค่าสถานะสำเร็จก่อนทำการบันทึก. |
| **สีไม่ถูกนำไปใช้** | ใช้สีที่โปร่งใส | เลือก `Color` ที่ทึบ (เช่น `Color.BLACK` หรือ `Color.BLUE`). |

## คำถามที่พบบ่อย

**Q: ความแตกต่างระหว่าง `ImageAreaRedaction` กับการลบข้อความคืออะไร?**  
A: `ImageAreaRedaction` ทำงานบนพิกัดพิกเซล ในขณะที่การลบข้อความจะวิเคราะห์ชั้น OCR เพื่อค้นหาและลบเนื้อหาข้อความ.

**Q: ฉันสามารถลบข้อมูลหลายพื้นที่ในภาพเดียวได้หรือไม่?**  
A: ได้—เรียก `redactor.apply()` หลายครั้งโดยใช้ `ImageAreaRedaction` ที่แตกต่างกันก่อนบันทึก.

**Q: GroupDocs.Redaction รองรับรูปแบบภาพอื่นเช่น TIFF หรือไม่?**  
A: ไลบรารีรองรับรูปแบบเรสเตอร์ทั่วไป (JPG, PNG, BMP, GIF) สำหรับ TIFF ให้แปลงเป็นรูปแบบที่รองรับก่อน.

**Q: ฉันจะทำการลบข้อมูลอัตโนมัติสำหรับโฟลเดอร์ของ PDF ที่สแกนได้อย่างไร?**  
A: วนลูปผ่านภาพแต่ละหน้าที่สกัดจาก PDF, ใช้ตรรกะการลบข้อมูลเดียวกัน, แล้วสร้าง PDF ใหม่ด้วยไลบรารี PDF.

**Q: มีวิธีดูตัวอย่างการลบข้อมูลก่อนบันทึกหรือไม่?**  
A: คุณสามารถเรนเดอร์ `Redactor` เป็น `BufferedImage` แล้วแสดงใน UI ของ Swing หรือ JavaFX ก่อนทำการบันทึกการเปลี่ยนแปลง.

## สรุป
คุณได้คู่มือที่ครบถ้วนและพร้อมใช้งานในสภาพแวดล้อมการผลิตเกี่ยวกับ **วิธีลบข้อมูลในภาพ** และโดยเฉพาะ **การลบข้อมูลในภาพเอกสารสแกน** ด้วย GroupDocs.Redaction สำหรับ Java หากทำตามขั้นตอนข้างต้น คุณสามารถปกป้องข้อมูลภาพที่ละเอียดอ่อนในหลากหลายอุตสาหกรรมได้ ค้นหา API เพิ่มเติม—เช่นการลบข้อความหรือการลบหน้าของ PDF—เพื่อสร้างโซลูชันความเป็นส่วนตัวของข้อมูลที่ครอบคลุมสำหรับองค์กรของคุณ.

---

**อัปเดตล่าสุด:** 2025-12-29  
**ทดสอบกับ:** GroupDocs.Redaction 24.9 (Java)  
**ผู้เขียน:** GroupDocs  

**แหล่งข้อมูล**  
- [เอกสาร](https://docs.groupdocs.com/redaction/java/)  
- [อ้างอิง API](https://reference.groupdocs.com/redaction/java)  
- [ดาวน์โหลด](https://releases.groupdocs.com/redaction/java/)  
- [ที่เก็บ GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- [ฟอรั่มสนับสนุนฟรี](https://forum.groupdocs.com/c/redaction/33)  
- [ใบอนุญาตชั่วคราว](https://purchase.groupdocs.com/temporary-license/)