---
date: '2026-03-22'
description: เรียนรู้วิธีการอ่านเมตาดาต้าไฟล์ด้วย Java, รับประเภทไฟล์และนับจำนวนหน้าด้วย
  Java โดยใช้ GroupDocs.Redaction สำหรับ Java. คู่มือแบบขั้นตอนพร้อมตัวอย่างโค้ด.
keywords:
- GroupDocs.Redaction Java
- document metadata extraction
- Java stream APIs
title: java อ่านเมตาดาต้าไฟล์ – ประเภทไฟล์ด้วย GroupDocs.Redaction
type: docs
url: /th/java/metadata-redaction/groupdocs-redaction-java-document-metadata-extraction/
weight: 1
---

# java read file metadata – รับประเภทไฟล์ด้วย GroupDocs.Redaction ใน Java

ในแอปพลิเคชัน Java สมัยใหม่ การ **java read file metadata** อย่างรวดเร็ว—โดยเฉพาะประเภทไฟล์ จำนวนหน้า ขนาดไฟล์ และคุณสมบัติเฉพาะอื่น ๆ—เป็นสิ่งสำคัญสำหรับการสร้าง pipeline การจัดการเอกสารหรือการวิเคราะห์ข้อมูลที่เชื่อถือได้ บทเรียนนี้จะพาคุณผ่านการอ่านคุณสมบัติเหล่านั้นด้วย GroupDocs.Redaction อธิบาย **วิธีการ get file type java** และแสดงวิธี **java get page count** และ **read file size java** อย่างสะอาดและเป็นมิตรกับสตรีม

## Quick Answers
- **ฉันจะรับประเภทไฟล์ของเอกสารใน Java ได้อย่างไร?** ใช้ `redactor.getDocumentInfo().getFileType()`  
- **ไลบรารีใดที่จัดการการสกัดเมตาดาต้าและการลบข้อมูลลับพร้อมกัน?** GroupDocs.Redaction สำหรับ Java  
- **ต้องใช้ไลเซนส์สำหรับการพัฒนาหรือไม่?** เวอร์ชันทดลองฟรีใช้ได้สำหรับการประเมิน; ต้องมีไลเซนส์ถาวรสำหรับการใช้งานในโปรดักชัน  
- **ฉันสามารถดึงจำนวนหน้าได้ด้วยหรือไม่?** ได้, เรียก `getPageCount()` บนวัตถุ `IDocumentInfo`  
- **วิธีนี้รองรับ Java 8+ หรือไม่?** รองรับอย่างเต็มที่—GroupDocs.Redaction รองรับ Java 8 และรุ่นใหม่กว่า  

## How to java read file metadata with GroupDocs.Redaction
การเข้าใจขั้นตอน **java read file metadata** ช่วยให้คุณตัดสินใจว่าจะวางตรรกะไว้ที่ไหนในแอปพลิเคชันของคุณ—ไม่ว่าจะเป็นไมโครเซอร์วิสที่ตรวจสอบการอัปโหลดหรือแบชงานที่ทำดัชนีคอลเลกชันเอกสารขนาดใหญ่

### What is “get file type java” and why does it matter?
เมื่อคุณเรียก `getFileType()` บนเอกสาร ไลบรารีจะตรวจสอบส่วนหัวของไฟล์และคืนค่า enum ที่เป็นมิตร (เช่น **DOCX**, **PDF**, **XLSX**) การรู้ประเภทที่แน่นอนช่วยให้คุณส่งไฟล์ไปยัง pipeline การประมวลผลที่เหมาะสม, บังคับใช้นโยบายความปลอดภัย, หรือแสดงข้อมูลที่ถูกต้องให้ผู้ใช้ปลายทาง

### Why use GroupDocs.Redaction for java read document properties?
- **All‑in‑one solution:** การลบข้อมูลลับ, การสกัดเมตาดาต้า, และการแปลงรูปแบบอยู่ภายใต้ API เดียว  
- **Stream‑friendly:** ทำงานโดยตรงกับ `InputStream` ทำให้คุณประมวลผลไฟล์จากดิสก์, เครือข่าย หรือคลาวด์โดยไม่ต้องสร้างไฟล์ชั่วคราว  
- **Performance‑tuned:** ใช้หน่วยความจำน้อยที่สุดและทำความสะอาดทรัพยากรอัตโนมัติเมื่อคุณปิดอินสแตนซ์ `Redactor`  

## Prerequisites
1. **GroupDocs.Redaction for Java** (เวอร์ชัน 24.9 หรือใหม่กว่า)  
2. JDK 8 หรือใหม่กว่า  
3. ความรู้พื้นฐานของ Java และความคุ้นเคยกับสตรีม I/O ของไฟล์  

## Setting Up GroupDocs.Redaction for Java

### Maven Installation
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

### Direct Download
หรือคุณสามารถดาวน์โหลดเวอร์ชันล่าสุดโดยตรงจาก [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/)  

### License Acquisition
- **Free Trial:** เหมาะสำหรับการประเมิน API  
- **Temporary License:** มีให้บนเว็บไซต์อย่างเป็นทางการสำหรับการทดสอบระยะสั้น  
- **Full License:** ซื้อเมื่อพร้อมใช้งานในโปรดักชัน  

## Basic Initialization (Java)

```java
import com.groupdocs.redaction.Redactor;
import java.io.FileInputStream;

FileInputStream stream = new FileInputStream("path/to/your/Sample.docx");
final Redactor redactor = new Redactor(stream);
// Proceed with document operations...
```

## Step‑by‑step guide to retrieve metadata

### Step 1: Open a File Stream
เริ่มต้นด้วยการสร้าง `InputStream` สำหรับเอกสารเป้าหมาย:

```java
FileInputStream stream = new FileInputStream("YOUR_DOCUMENT_DIRECTORY/Sample.docx");
```

### Step 2: Initialize the Redactor
สร้างอินสแตนซ์ `Redactor` ด้วยสตรีมนี้ วัตถุนี้ให้คุณเข้าถึงเมตาดาต้าของเอกสาร

```java
final Redactor redactor = new Redactor(stream);
```

### Step 3: Retrieve Document Information
เรียก `getDocumentInfo()` เพื่อรับวัตถุ `IDocumentInfo` ที่นี่คือจุดที่คุณ **java read file metadata**, **java get document type**, **java get page count**, และแม้กระทั่ง **read file size java**

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

> **Pro tip:** ให้คอมเมนต์บรรทัด `System.out.println` ไว้จนกว่าจะต้องการแสดงผลบนคอนโซล; การคอมเมนต์ไว้ในโปรดักชันจะช่วยลดภาระ I/O  

### Step 4: Close Resources
ปิด `Redactor` และสตรีมในบล็อก `finally` (ตามตัวอย่าง) เสมอเพื่อหลีกเลี่ยงการรั่วไหลของหน่วยความจำ โดยเฉพาะเมื่อประมวลผลเอกสารหลายไฟล์พร้อมกัน  

## Practical Applications (java read document properties)

1. **Document Management Systems:** จัดทำแคตาล็อกไฟล์อัตโนมัติตามประเภท, จำนวนหน้า, และขนาด  
2. **Data‑Analytics Pipelines:** ส่งเมตาดาต้าไปยังแดชบอร์ดสำหรับการรายงาน  
3. **Content‑Creation Platforms:** แสดงรายละเอียดไฟล์ให้ผู้ใช้ก่อนดาวน์โหลดหรือพรีวิว  

## Performance Considerations
- ใช้ **buffered streams** (`BufferedInputStream`) สำหรับไฟล์ขนาดใหญ่เพื่อเพิ่มความเร็ว I/O  
- ปล่อยทรัพยากรโดยเร็ว (`close()` ทั้งบน `Redactor` และสตรีม)  
- เมื่อประมวลผลเป็นแบช ควรพิจารณาใช้ `Redactor` อินสแตนซ์เดียวต่อเธรดเพื่อ ลดค่าใช้จ่ายในการสร้างอ็อบเจ็กต์  

## Common Issues & Solutions
| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| `FileNotFoundException` | Path ไม่ถูกต้องหรือไฟล์หาย | ตรวจสอบ path แบบ absolute/relative และสิทธิ์การเข้าถึงไฟล์ |
| `LicenseException` | ไม่มีไลเซนส์ที่ถูกต้อง | โหลดไลเซนส์ทดลองหรือไลเซนส์ที่ซื้อก่อนสร้าง `Redactor` |
| `OutOfMemoryError` on large PDFs | สตรีมไม่มีบัฟเฟอร์หรือประมวลผลไฟล์หลายไฟล์พร้อมกัน | เปลี่ยนเป็น `BufferedInputStream` และจำกัดจำนวนเธรดที่ทำงานพร้อมกัน |

## Frequently Asked Questions

**Q: GroupDocs.Redaction ใช้ทำอะไร?**  
A: ส่วนใหญ่ใช้สำหรับการลบข้อมูลลับ, แต่ยังมี API ที่แข็งแรงสำหรับ **java read document properties** เช่น ประเภทไฟล์และจำนวนหน้า  

**Q: สามารถใช้ GroupDocs.Redaction กับเฟรมเวิร์ก Java อื่นได้หรือไม่?**  
A: ใช่, ไลบรารีทำงานร่วมกับ Spring, Jakarta EE, และแม้กระทั่งโครงการ Java SE ธรรมดาได้อย่างราบรื่น  

**Q: จะจัดการกับเอกสารขนาดใหญ่อย่างมีประสิทธิภาพอย่างไร?**  
A: ห่อสตรีมไฟล์ด้วย `BufferedInputStream`, ปิดทรัพยากรโดยเร็ว, และพิจารณาประมวลผลแบบสตรีมแทนการโหลดเอกสารทั้งหมดเข้าสู่หน่วยความจำ  

**Q: ไลบรารีรองรับเอกสารที่ไม่ใช่ภาษาอังกฤษหรือไม่?**  
A: รองรับอย่างเต็มที่—GroupDocs.Redaction จัดการหลายภาษาและชุดอักขระได้โดยอัตโนมัติ  

**Q: จุดบกพร่องทั่วไปเมื่อสกัดเมตาดาต้าคืออะไร?**  
A: ไลเซนส์หาย, path ไฟล์ไม่ถูกต้อง, และลืมปิดสตรีมเป็นปัญหาที่พบบ่อยที่สุด ควรปฏิบัติตามรูปแบบการทำความสะอาดทรัพยากรที่แสดงไว้ข้างต้นเสมอ  

## Conclusion
คุณมีสูตรครบถ้วนและพร้อมใช้งานในระดับโปรดักชันสำหรับ **java read file metadata**, การอ่านคุณสมบัติเอกสารอื่น ๆ, และ **java get page count** ด้วย GroupDocs.Redaction ผสานสคริปต์เหล่านี้เข้ากับบริการที่มีอยู่แล้ว คุณจะได้มองเห็นข้อมูลของทุกเอกสารที่ไหลผ่านระบบของคุณทันที  

**Next Steps**  
- ทดลองใช้ฟิลด์เมตาดาต้าอื่น ๆ ที่เปิดเผยโดย `IDocumentInfo`  
- ผสานการสกัดเมตาดาต้ากับ workflow การลบข้อมูลลับเพื่อความปลอดภัยของเอกสารแบบครบวงจร  
- สำรวจรูปแบบการประมวลผลแบบแบชสำหรับสภาพแวดล้อมที่มีปริมาณสูง  

**Resources**  
- [Documentation](https://docs.groupdocs.com/redaction/java/)  
- [API Reference](https://reference.groupdocs.com/redaction/java)  
- [Download GroupDocs.Redaction for Java](https://releases.groupdocs.com/redaction/java/)  
- [GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- [Free Support Forum](https://forum.groupdocs.com/c/redaction/33)  
- [Temporary License Information](https://purchase.groupdocs.com/temporary-license/)  

---

**Last Updated:** 2026-03-22  
**Tested With:** GroupDocs.Redaction 24.9 for Java  
**Author:** GroupDocs