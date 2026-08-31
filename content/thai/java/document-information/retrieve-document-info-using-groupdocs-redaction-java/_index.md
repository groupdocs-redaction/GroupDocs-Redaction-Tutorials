---
date: '2026-03-20'
description: เรียนรู้วิธีการรับประเภทไฟล์ใน Java, รับขนาดเอกสารใน Java, และดึงข้อมูลเมตาดาต้า
  PDF ใน Java ด้วย GroupDocs.Redaction for Java. เพิ่มประสิทธิภาพการจัดการเอกสารของแอป
  Java ของคุณวันนี้.
keywords:
- get file type java
- get document size java
- retrieve pdf metadata java
- get page count java
- GroupDocs Redaction library setup Java
title: วิธีรับประเภทไฟล์ Java ด้วย GroupDocs.Redaction
type: docs
url: /th/java/document-information/retrieve-document-info-using-groupdocs-redaction-java/
weight: 1
---

# วิธีการรับประเภทไฟล์ java ด้วย GroupDocs.Redaction

การดึงรายละเอียดสำคัญของเอกสาร—เช่น **file type**, จำนวนหน้า, และขนาด—เป็นความต้องการทั่วไปเมื่อสร้างแอปพลิเคชัน Java ที่เน้นเอกสาร ในบทแนะนำนี้คุณจะได้เรียนรู้วิธี **get file type java** และวิธี **get document size java**, **get page count java**, และแม้กระทั่ง **retrieve pdf metadata java** ด้วยไลบรารี GroupDocs.Redaction การรู้ประเภทไฟล์ตั้งแต่ต้นจะช่วยให้คุณตัดสินใจเลือกเส้นทางการประมวลผลได้ ในขณะที่ข้อมูลขนาดและจำนวนหน้าช่วยจัดการทรัพยากรได้อย่างมีประสิทธิภาพ

## คำตอบอย่างรวดเร็ว
- **วิธีใดที่คืนค่าประเภทไฟล์?** `IDocumentInfo.getFileType()`
- **ฉันจะรับจำนวนหน้าได้อย่างไร?** `IDocumentInfo.getPageCount()`
- **การเรียกใดให้ขนาดเอกสารเป็นไบต์?** `IDocumentInfo.getSize()`
- **ฉันต้องมีลิขสิทธิ์เพื่อรันตัวอย่างหรือไม่?** การทดลองหรือใบอนุญาตชั่วคราวทำงานสำหรับการประเมินผล.
- **ต้องใช้เวอร์ชัน Java ใด?** Java 8 หรือสูงกว่า.

## “get file type java” คืออะไร
วลีนี้หมายถึงการสกัดรูปแบบไฟล์ (เช่น DOCX, PDF) จากเอกสารโดยใช้โปรแกรมใน Java. GroupDocs.Redaction เปิดเผยข้อมูลนี้ผ่านอินเทอร์เฟซ `IDocumentInfo` ทำให้เป็นการเรียกหนึ่งบรรทัด.

## ทำไมต้องใช้ GroupDocs.Redaction สำหรับการสกัดเมทาดาต้า?
- **Broad format support:** รองรับ PDF, DOCX, XLSX, PPTX, และอื่น ๆ อีกมาก
- **Simple API:** การเรียกหนึ่งบรรทัดคืนค่าประเภทไฟล์, จำนวนหน้า, และขนาด.
- **Performance‑optimized:** โหลดเฉพาะเมทาดาต้าที่คุณต้องการ ทำให้การใช้หน่วยความจำน้อย.
- **Consistent results:** ทำงานเช่นเดียวกันในทุกนามสกุลไฟล์ที่รองรับ ดังนั้นคุณจึงสามารถพึ่งพาได้สำหรับสถานการณ์ **java get file extension**.

## ข้อกำหนดเบื้องต้น
- Java 8 หรือใหม่กว่า ติดตั้งแล้ว.
- IDE ที่รองรับ Maven (IntelliJ IDEA, Eclipse, ฯลฯ).
- เข้าถึงใบอนุญาต GroupDocs.Redaction (ทดลองฟรีหรือใบอนุญาตชั่วคราว).

## การตั้งค่า GroupDocs.Redaction สำหรับ Java

เพื่อใช้ไลบรารี GroupDocs.Redaction ในโครงการ Java ของคุณ ให้ทำตามขั้นตอนการติดตั้งต่อไปนี้:

**Maven Installation**

เพิ่ม repository และ dependency ต่อไปนี้ในไฟล์ `pom.xml` ของคุณ:

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

**Direct Download**

หรือดาวน์โหลดเวอร์ชันล่าสุดจาก [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### การรับใบอนุญาต
- **Free Trial:** เริ่มต้นด้วยการทดลองฟรีเพื่อประเมินไลบรารี.  
- **Temporary License:** รับใบอนุญาตชั่วคราวสำหรับการประเมินที่ขยายเวลา.  
- **Purchase:** พิจารณาซื้อหากตรงกับความต้องการของคุณ.

เมื่อติดตั้งแล้ว ให้เริ่มต้นและตั้งค่า GroupDocs.Redaction:

```java
import com.groupdocs.redaction.Redactor;

// Initialize Redactor with the path to your document
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

## ทำไมการรับประเภทไฟล์ java ถึงสำคัญในโครงการจริง
การเข้าใจประเภทของเอกสารตั้งแต่ต้นทำให้คุณสามารถส่งไฟล์ไปยังสายการประมวลผลที่ถูกต้อง—เช่น ส่ง PDF ไปยังกระบวนการลบข้อมูล, ไฟล์ Word ไปยังบริการแปลง, หรือรูปภาพไปยังเครื่อง OCR. นอกจากนี้ยังช่วยบังคับใช้นโยบายความปลอดภัย (บล็อกไฟล์ที่เป็นโปรแกรม) และให้ไอคอน UI ที่แม่นยำในระบบจัดการเอกสาร.

## วิธีการรับประเภทไฟล์ java, รับขนาดเอกสาร java, และรับจำนวนหน้า java

เมื่อไลบรารีพร้อมแล้ว เราจะไปผ่านขั้นตอนที่แน่นอนเพื่อดึงข้อมูลที่คุณต้องการ.

### ขั้นตอนที่ 1: นำเข้าคลาสที่จำเป็น
ตรวจสอบให้แน่ใจว่าคุณได้นำเข้าคลาสที่ต้องการที่ส่วนบนของไฟล์ Java ของคุณ:

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.domain.IDocumentInfo;
```

### ขั้นตอนที่ 2: เริ่มต้น Redactor
สร้างอินสแตนซ์ `Redactor` โดยระบุเส้นทางไปยังเอกสารของคุณ วัตถุนี้ทำให้คุณสามารถโต้ตอบกับไฟล์และดึงเมทาดาต้าได้.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    // Code for retrieving information will go here.
} finally {
    redactor.close();
}
```

### ขั้นตอนที่ 3: ดึงและแสดงข้อมูลเอกสาร
เรียก `getDocumentInfo()` เพื่อรับอ็อบเจ็กต์ `IDocumentInfo` จากอ็อบเจ็กต์นี้คุณสามารถ **get file type java**, **get document size java**, และ **get page count java** ได้ในหนึ่งการเรียก.

```java
// Retrieve document information
IDocumentInfo info = redactor.getDocumentInfo();

// Output document type, page count, and size in bytes
System.out.println("File Type: " + info.getFileType());
System.out.println("Page Count: " + info.getPageCount());
System.out.println("Size (Bytes): " + info.getSize());
```

คำสั่ง `System.out.println` ทั้งสามบรรทัดจะให้ประเภทไฟล์ จำนวนหน้า และขนาดเป็นไบต์—ตรงกับสิ่งที่คุณต้องการสำหรับการประมวลผลต่อไป.

## วิธีการดึงเมทาดาต้า pdf java

หากเอกสารต้นทางเป็น PDF การเรียก `IDocumentInfo` เดียวกันจะคืนค่าเมทาดาต้าเฉพาะ PDF (เช่น เวอร์ชัน PDF, สถานะการเข้ารหัส) ไม่จำเป็นต้องเขียนโค้ดเพิ่มเติม; เพียงใช้เมธอด `getDocumentInfo()` เดียวกัน.

## กรณีการใช้งานทั่วไป
1. **Document Management Systems:** แบ่งประเภทไฟล์อัตโนมัติตามประเภทหรือขนาดก่อนจัดเก็บ.  
2. **Content Processing Pipelines:** เลือกกลยุทธ์การประมวลผลที่แตกต่างตามจำนวนหน้า (เช่น ลบข้อมูลเป็นชุดสำหรับ PDF ขนาดใหญ่ vs. เอกสาร Word ขนาดเล็ก).  
3. **Digital Asset Libraries:** แสดงตัวอย่างคุณสมบัติของเอกสารอย่างรวดเร็วให้ผู้ใช้โดยไม่ต้องเปิดไฟล์.

## ปัญหาทั่วไปและวิธีแก้
- **File not found:** ตรวจสอบเส้นทางแบบ absolute หรือ relative ที่คุณส่งให้ `Redactor`.  
- **Unsupported format:** ตรวจสอบให้แน่ใจว่านามสกุลไฟล์ของคุณได้รับการสนับสนุนโดย GroupDocs.Redaction.  
- **License errors:** ใช้ใบอนุญาตทดลองหรือถาวรที่ถูกต้อง; มิฉะนั้น API จะโยนข้อยกเว้นเรื่องลิขสิทธิ์.

## เคล็ดลับการแก้ปัญหา (read document metadata java)
- ห่อการเรียกเมทาดาต้าในบล็อก `try‑catch` เพื่อจัดการไฟล์ที่เสียหายอย่างราบรื่น.  
- ใช้ `redactor.isEncrypted()` (หากมี) เพื่อตรวจจับ PDF ที่เข้ารหัสก่อนอ่านเมทาดาต้า.  
- เมื่อประมวลผลไฟล์จำนวนมาก ให้ใช้ thread‑pool ซ้ำและปิดแต่ละอินสแตนซ์ `Redactor` อย่างทันท่วงทีเพื่อหลีกเลี่ยงการรั่วของ file‑handle.

## การพิจารณาด้านประสิทธิภาพ
เมื่อจัดการชุดข้อมูลขนาดใหญ่:
- เปิดแต่ละเอกสารในบล็อก `try‑with‑resources` เพื่อรับประกันการปล่อย file handle อย่างทันท่วงที.  
- แคชเฉพาะเมทาดาต้าที่คุณต้องการ; หลีกเลี่ยงการโหลดเนื้อหาเต็มของเอกสารหากไม่จำเป็น.

## สรุป
ตอนนี้คุณรู้วิธี **get file type java**, **get document size java**, **get page count java**, และ **retrieve pdf metadata java** ด้วย GroupDocs.Redaction แล้ว นำส่วนโค้ดเหล่านี้ไปใช้ในแอปพลิเคชัน Java ของคุณเพื่อทำการตัดสินใจที่ฉลาดขึ้นเกี่ยวกับการจัดการเอกสาร, ปรับปรุงประสิทธิภาพ, และมอบประสบการณ์ผู้ใช้ที่ดียิ่งขึ้น.

## ส่วนคำถามที่พบบ่อย
**Q1: GroupDocs.Redaction คืออะไร?**  
A1: เป็นไลบรารีสำหรับการลบข้อมูลและจัดการข้อมูลเอกสารในแอปพลิเคชัน Java.

**Q2: ฉันสามารถดึงเมทาดาต้าจากไฟล์ PDF ได้หรือไม่?**  
A2: ได้, ไลบรารีรองรับรูปแบบไฟล์ต่าง ๆ รวมถึง PDF.

**Q3: ฉันจะจัดการข้อยกเว้นเมื่อดึงข้อมูลเอกสารได้อย่างไร?**  
A3: ใช้บล็อก try‑catch เพื่อจัดการข้อผิดพลาดที่อาจเกิดขึ้นอย่างราบรื่น.

**Q4: ฉันสามารถรับข้อมูลอะไรเกี่ยวกับเอกสารได้บ้าง?**  
A4: ประเภทไฟล์, จำนวนหน้า, และขนาดเป็นไบต์เป็นหนึ่งในรายละเอียดที่คุณสามารถดึงได้.

**Q5: มีการสนับสนุนรูปแบบไฟล์อื่นนอกจากเอกสาร Word หรือไม่?**  
A5: มี, GroupDocs.Redaction รองรับหลายรูปแบบไฟล์รวมถึง PDF, Excel, และอื่น ๆ.

## คำถามที่พบบ่อยเพิ่มเติม
**Q: API คืนค่าเวอร์ชัน PDF (เช่น 1.7) เป็นส่วนหนึ่งของเมทาดาต้าหรือไม่?**  
A: อ็อบเจ็กต์ `IDocumentInfo` มีลักษณะพื้นฐานของ PDF; สำหรับข้อมูลเวอร์ชันโดยละเอียดคุณสามารถสอบถามคุณสมบัติเฉพาะ PDF ผ่าน Redactor API.

**Q: ฉันสามารถดึงเมทาดาต้าโดยไม่โหลดเอกสารทั้งหมดเข้าสู่หน่วยความจำได้หรือไม่?**  
A: ได้, `getDocumentInfo()` อ่านเฉพาะข้อมูลส่วนหัวที่จำเป็นสำหรับเมทาดาต้า ทำให้การใช้หน่วยความจำน้อย.

**Q: สามารถประมวลผลหลายเอกสารเป็นชุดได้อย่างมีประสิทธิภาพหรือไม่?**  
A: ห่อการประมวลผลของแต่ละเอกสารในอินสแตนซ์ `Redactor` ของตนเองและใช้ thread pool ซ้ำเพื่อทำงานแบบขนาน.

## แหล่งข้อมูล
- **เอกสาร:** [GroupDocs Redaction Java Documentation](https://docs.groupdocs.com/redaction/java/)  
- **อ้างอิง API:** [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java)  
- **ดาวน์โหลด:** [GroupDocs.Redaction for Java Downloads](https://releases.groupdocs.com/redaction/java/)  
- **GitHub:** [GroupDocs GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **สนับสนุนฟรี:** [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)  
- **ใบอนุญาตชั่วคราว:** [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license/)  

---

**อัปเดตล่าสุด:** 2026-03-20  
**ทดสอบกับ:** GroupDocs.Redaction 24.9 for Java  
**ผู้เขียน:** GroupDocs