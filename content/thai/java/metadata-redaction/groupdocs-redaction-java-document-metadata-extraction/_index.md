---
date: '2026-01-06'
description: เรียนรู้วิธีการรับประเภทไฟล์ใน Java, อ่านคุณสมบัติของเอกสาร, และดึงจำนวนหน้าด้วย
  GroupDocs.Redaction สำหรับ Java คู่มือแบบขั้นตอนพร้อมโค้ด
keywords:
- GroupDocs.Redaction Java
- document metadata extraction
- Java stream APIs
title: รับประเภทไฟล์ Java ด้วย GroupDocs.Redaction – การสกัดเมตาดาต้า
type: docs
url: /th/java/metadata-redaction/groupdocs-redaction-java-document-metadata-extraction/
weight: 1
---

# ดึงประเภทไฟล์ java และสกัดเมตาดาต้าเอกสารด้วย GroupDocs.Redaction ใน Java

ในแอปพลิเคชัน Java สมัยใหม่ การสามารถ **get file type java** ได้อย่างรวดเร็ว—พร้อมดึงคุณสมบัติเอกสารที่เป็นประโยชน์อื่น ๆ เช่น จำนวนหน้า, ขนาด, และเมตาดาต้ากำหนดเอง—เป็นสิ่งสำคัญสำหรับการสร้าง pipeline การจัดการเอกสารหรือการวิเคราะห์ข้อมูลที่แข็งแรง คู่มือฉบับนี้จะแสดงให้คุณเห็นอย่างละเอียดว่า จะอ่านคุณสมบัติของเอกสารด้วย GroupDocs.Redaction อย่างไร ทำไมมันถึงเป็นไลบรารีที่เลือกใช้สำหรับงานนี้ และจะผสานโซลูชันเข้ากับโค้ดของคุณอย่างสะอาดตาอย่างไร

## คำตอบอย่างรวดเร็ว
- **ฉันจะดึงประเภทไฟล์ของเอกสารใน Java ได้อย่างไร?** ใช้ `redactor.getDocumentInfo().getFileType()`  
- **ไลบรารีใดที่จัดการการสกัดเมตาดาต้าและการทำลบข้อมูลพร้อมกัน?** GroupDocs.Redaction สำหรับ Java  
- **ต้องมีลิขสิทธิ์สำหรับการพัฒนาหรือไม่?** สามารถใช้รุ่นทดลองฟรีสำหรับการประเมิน; ต้องมีลิขสิทธิ์ถาวรสำหรับการใช้งานจริง  
- **ฉันสามารถดึงจำนวนหน้าได้ด้วยหรือไม่?** ใช่, เรียก `getPageCount()` บนวัตถุ `IDocumentInfo`  
- **วิธีนี้เข้ากันได้กับ Java 8+ หรือไม่?** แน่นอน—GroupDocs.Redaction รองรับ Java 8 และรุ่นใหม่กว่า  

## “get file type java” คืออะไรและทำไมจึงสำคัญ?
เมื่อคุณเรียก `getFileType()` บนเอกสาร ไลบรารีจะตรวจสอบส่วนหัวของไฟล์และคืนค่า enum ที่อ่านง่าย (เช่น **DOCX**, **PDF**, **XLSX**) การรู้ประเภทที่แน่นอนช่วยให้คุณส่งไฟล์ไปยัง pipeline การประมวลผลที่เหมาะสม, บังคับใช้นโยบายความปลอดภัย, หรือแสดงข้อมูลที่ถูกต้องให้ผู้ใช้ปลายทางเห็น  

## ทำไมต้องใช้ GroupDocs.Redaction สำหรับการอ่านคุณสมบัติเอกสารใน java?
- **โซลูชันครบวงจร:** การทำลบข้อมูล, การสกัดเมตาดาต้า, และการแปลงรูปแบบทำงานภายใต้ API เดียว  
- **เป็นมิตรกับสตรีม:** ทำงานโดยตรงกับ `InputStream` ทำให้คุณประมวลผลไฟล์จากดิสก์, เครือข่าย, หรือคลาวด์โดยไม่ต้องสร้างไฟล์ชั่วคราว  
- **ปรับประสิทธิภาพสูง:** ใช้หน่วยความจำน้อยและทำความสะอาดทรัพยากรอัตโนมัติเมื่อปิดอินสแตนซ์ `Redactor`  

## ข้อกำหนดเบื้องต้น
1. **GroupDocs.Redaction สำหรับ Java** (เวอร์ชัน 24.9 หรือใหม่กว่า)  
2. JDK 8 หรือใหม่กว่า  
3. ความรู้พื้นฐานของ Java และความคุ้นเคยกับสตรีม I/O ของไฟล์  

## การตั้งค่า GroupDocs.Redaction สำหรับ Java

### การติดตั้งด้วย Maven
เพิ่ม repository และ dependency ลงในไฟล์ `pom.xml` ของคุณ:

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
หรือคุณสามารถดาวน์โหลดเวอร์ชันล่าสุดได้โดยตรงจาก [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/)  

### การจัดหาลิขสิทธิ์
- **รุ่นทดลองฟรี:** เหมาะสำหรับการประเมิน API  
- **ลิขสิทธิ์ชั่วคราว:** มีให้บนเว็บไซต์อย่างเป็นทางการสำหรับการทดสอบระยะสั้น  
- **ลิขสิทธิ์เต็ม:** ซื้อเมื่อพร้อมใช้งานในสภาพแวดล้อมการผลิต  

## การเริ่มต้นพื้นฐาน (Java)

```java
import com.groupdocs.redaction.Redactor;
import java.io.FileInputStream;

FileInputStream stream = new FileInputStream("path/to/your/Sample.docx");
final Redactor redactor = new Redactor(stream);
// Proceed with document operations...
```

## วิธีดึงประเภทไฟล์ java ด้วย GroupDocs.Redaction

### ขั้นตอน 1: เปิดสตรีมไฟล์
เริ่มต้นด้วยการสร้าง `InputStream` สำหรับเอกสารเป้าหมาย:

```java
FileInputStream stream = new FileInputStream("YOUR_DOCUMENT_DIRECTORY/Sample.docx");
```

### ขั้นตอน 2: เริ่มต้น Redactor
สร้างอินสแตนซ์ `Redactor` โดยใช้สตรีม วัตถุนี้ให้คุณเข้าถึงเมตาดาต้าของเอกสาร

```java
final Redactor redactor = new Redactor(stream);
```

### ขั้นตอน 3: ดึงข้อมูลเอกสาร
เรียก `getDocumentInfo()` เพื่อรับวัตถุ `IDocumentInfo` ที่นี่คุณจะ **get file type java**, อ่านคุณสมบัติอื่น ๆ, และแม้กระทั่ง **retrieve page count java**

```java
try {
    IDocumentInfo info = redactor.getDocumentInfo();
    
    // Display document information (uncomment as needed)
    System.out.println("\
File type: " + info.getFileType() +
           "\
Number of pages: " + info.getPageCount() + 
           "\
Document size: " + info.getSize() + " bytes");
} finally {
    redactor.close();
    stream.close();
}
```

> **เคล็ดลับมืออาชีพ:** ยกเลิกคอมเมนต์บรรทัด `System.out.println` เฉพาะเมื่อคุณต้องการแสดงผลบนคอนโซล; การคอมเมนต์ไว้ในสภาพแวดล้อมการผลิตจะช่วยลดภาระ I/O  

### ขั้นตอน 4: ปิดทรัพยากร
ควรปิด `Redactor` และสตรีมในบล็อก `finally` (ตามตัวอย่าง) เพื่อหลีกเลี่ยงการรั่วไหลของหน่วยความจำ โดยเฉพาะเมื่อประมวลผลเอกสารหลายไฟล์พร้อมกัน  

## การประยุกต์ใช้งานจริง (java read document properties)

1. **ระบบจัดการเอกสาร:** แคตาล็อกไฟล์อัตโนมัติตามประเภท, จำนวนหน้า, และขนาด  
2. **Pipeline การวิเคราะห์ข้อมูล:** ส่งเมตาดาต้าไปยังแดชบอร์ดสำหรับการรายงาน  
3. **แพลตฟอร์มสร้างเนื้อหา:** แสดงรายละเอียดไฟล์ให้ผู้ใช้ก่อนดาวน์โหลดหรือพรีวิว  

## พิจารณาด้านประสิทธิภาพ
- ใช้ **สตรีมบัฟเฟอร์** (`BufferedInputStream`) สำหรับไฟล์ขนาดใหญ่เพื่อเพิ่มความเร็ว I/O  
- ปล่อยทรัพยากรโดยเร็ว (`close()` ทั้งบน `Redactor` และสตรีม)  
- เมื่อประมวลผลเป็นชุด, พิจารณาใช้ `Redactor` อินสแตนซ์เดียวต่อเธรดเพื่อลดค่าใช้จ่ายในการสร้างอ็อบเจกต์  

## ปัญหาที่พบบ่อยและวิธีแก้ไข
| อาการ | สาเหตุที่เป็นไปได้ | วิธีแก้ |
|-------|-------------------|--------|
| `FileNotFoundException` | เส้นทางไม่ถูกต้องหรือไฟล์หาย | ตรวจสอบเส้นทางแบบ absolute/relative และสิทธิ์การเข้าถึงไฟล์ |
| `LicenseException` | ไม่มีลิขสิทธิ์ที่ถูกต้องโหลด | โหลดลิขสิทธิ์ทดลองหรือที่ซื้อก่อนสร้าง `Redactor` |
| `OutOfMemoryError` บน PDF ขนาดใหญ่ | สตรีมไม่บัฟเฟอร์หรือประมวลผลไฟล์หลายไฟล์พร้อมกัน | เปลี่ยนเป็น `BufferedInputStream` และจำกัดจำนวนเธรดที่ทำงานพร้อมกัน |

## คำถามที่พบบ่อย

**ถาม: GroupDocs.Redaction ใช้ทำอะไร?**  
ตอบ: ส่วนใหญ่ใช้สำหรับการทำลบข้อมูลที่เป็นความลับ, แต่ยังให้ API ที่แข็งแรงสำหรับ **java read document properties** เช่น ประเภทไฟล์และจำนวนหน้า  

**ถาม: สามารถใช้ GroupDocs.Redaction กับเฟรมเวิร์ก Java อื่นได้หรือไม่?**  
ตอบ: ใช่, ไลบรารีทำงานร่วมกับ Spring, Jakarta EE, และแม้กระทั่งโครงการ Java SE ธรรมดาได้อย่างราบรื่น  

**ถาม: จะจัดการเอกสารขนาดใหญ่อย่างมีประสิทธิภาพอย่างไร?**  
ตอบ: ห่อสตรีมไฟล์ด้วย `BufferedInputStream`, ปิดทรัพยากรโดยเร็ว, และพิจารณาประมวลผลแบบสตรีมแทนการโหลดเอกสารทั้งหมดเข้าสู่หน่วยความจำ  

**ถาม: ไลบรารีรองรับเอกสารที่ไม่ใช่ภาษาอังกฤษหรือไม่?**  
ตอบ: แน่นอน—GroupDocs.Redaction รองรับหลายภาษาและชุดอักขระโดยอัตโนมัติ  

**ถาม: จุดบกพร่องทั่วไปเมื่อสกัดเมตาดาต้าคืออะไร?**  
ตอบ: การไม่มีลิขสิทธิ์, เส้นทางไฟล์ไม่ถูกต้อง, และลืมปิดสตรีมเป็นปัญหาที่พบบ่อยที่สุด ควรปฏิบัติตามรูปแบบการทำความสะอาดทรัพยากรที่แสดงไว้ข้างต้นเสมอ  

## สรุป
คุณได้เรียนรู้สูตรครบวงจรสำหรับ **getting file type java**, อ่านคุณสมบัติเอกสารอื่น ๆ, และ **retrieving page count java** ด้วย GroupDocs.Redaction แล้ว นำโค้ดตัวอย่างเหล่านี้ไปผสานในบริการของคุณ จะทำให้คุณเห็นข้อมูลของทุกเอกสารที่ไหลผ่านระบบของคุณได้ทันที  

**ขั้นตอนต่อไป**  
- ทดลองใช้ฟิลด์เมตาดาต้าอื่น ๆ ที่เปิดเผยโดย `IDocumentInfo`  
- ผสานการสกัดเมตาดาต้ากับ workflow การทำลบข้อมูลเพื่อความปลอดภัยของเอกสารแบบครบวงจร  
- สำรวจรูปแบบการประมวลผลแบบ batch สำหรับสภาพแวดล้อมที่มีปริมาณสูง  

---  
**อัปเดตล่าสุด:** 2026-01-06  
**ทดสอบกับ:** GroupDocs.Redaction 24.9 for Java  
**ผู้เขียน:** GroupDocs  

**แหล่งข้อมูล**  
- [Documentation](https://docs.groupdocs.com/redaction/java/)  
- [API Reference](https://reference.groupdocs.com/redaction/java)  
- [Download GroupDocs.Redaction for Java](https://releases.groupdocs.com/redaction/java/)  
- [GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- [Free Support Forum](https://forum.groupdocs.com/c/redaction/33)  
- [Temporary License Information](https://purchase.groupdocs.com/temporary-license/)