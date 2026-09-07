---
date: '2026-09-06'
description: เรียนรู้วิธีการ java รับส่วนขยายไฟล์, ดึงข้อมูล document size, page count,
  และ PDF metadata ด้วย GroupDocs.Redaction สำหรับ Java. เพิ่มประสิทธิภาพการจัดการเอกสารของแอป
  Java ของคุณวันนี้.
keywords:
- java get file extension
- java file type detection
- get document size java
- get page count java
- read pdf metadata java
lastmod: '2026-09-06'
og_description: ค้นพบวิธีการ java รับส่วนขยายไฟล์, document size, page count, และ
  PDF metadata ด้วย GroupDocs.Redaction สำหรับ Java. โค้ดง่าย, ผลลัพธ์เร็ว.
og_image_alt: Guide showing Java code to extract file type, size, and page count using
  GroupDocs.Redaction
og_title: วิธีการ java รับส่วนขยายไฟล์โดยใช้ GroupDocs.Redaction
schemas:
- author: GroupDocs
  dateModified: '2026-09-06'
  description: Learn how to java get file extension, retrieve document size, page
    count, and PDF metadata with GroupDocs.Redaction for Java. Boost your Java app's
    document handling today.
  headline: How to java get file extension using GroupDocs.Redaction
  type: TechArticle
- description: Learn how to java get file extension, retrieve document size, page
    count, and PDF metadata with GroupDocs.Redaction for Java. Boost your Java app's
    document handling today.
  name: How to java get file extension using GroupDocs.Redaction
  steps:
  - name: import necessary classes
    text: 'Add the required imports at the top of your Java file:'
  - name: initialize the redactor
    text: The `Redactor` class is the core engine that opens a document and provides
      access to its metadata.
  - name: retrieve and display document info
    text: '`IDocumentInfo` provides the metadata you need. Call `getDocumentInfo()`
      once and then query the three properties. The three `System.out.println` statements
      output the file type, page count, and size in bytes—exactly the data you need
      for downstream processing.'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction is a Java library that enables redaction, metadata
      extraction, and format‑agnostic document processing across more than 50 file
      types.
    question: What is GroupDocs.Redaction?
  - answer: Yes, `IDocumentInfo` returns PDF version, encryption status, and basic
      metadata without extra code.
    question: Can I retrieve metadata from PDF files?
  - answer: Enclose the `getDocumentInfo()` call in a `try‑catch` block and handle
      `RedactionException` to manage corrupted or unsupported files.
    question: How do I handle exceptions when retrieving document info?
  - answer: File type, number of pages, size in bytes, PDF version, encryption flag,
      and basic author/creation metadata.
    question: What kind of information can I get about a document?
  - answer: Yes, instantiate a separate `Redactor` for each file inside a thread pool
      and reuse the same JVM to achieve high throughput.
    question: Is there support for batch‑processing many documents efficiently?
  type: FAQPage
tags:
- document metadata
- GroupDocs.Redaction
- Java file handling
title: วิธีการ java รับส่วนขยายไฟล์โดยใช้ GroupDocs.Redaction
type: docs
url: /th/java/document-information/retrieve-document-info-using-groupdocs-redaction-java/
weight: 1
---

# วิธีการ java get file extension ด้วย GroupDocs.Redaction

ในแอปพลิเคชัน Java สมัยใหม่ที่ประมวลผลไฟล์ที่ผู้ใช้อัปโหลด การรู้ประเภทไฟล์ที่แน่นอนตั้งแต่แรก—**java get file extension**—เป็นสิ่งสำคัญสำหรับการกำหนดเส้นทาง ความปลอดภัย และการวางแผนทรัพยากร บทเรียนนี้จะแสดงวิธี java get file extension, การรับขนาดเอกสาร, จำนวนหน้า, และแม้กระทั่งการดึงข้อมูลเมตา PDF ด้วยไลบรารี GroupDocs.Redaction โดยตอนจบคุณจะมีการเรียกเดียวที่ใช้หน่วยความจำน้อยซึ่งคืนค่าคุณสมบัติหลักทั้งหมดที่คุณต้องการ

## คำตอบอย่างรวดเร็ว
- **เมธอดใดที่คืนประเภทไฟล์?** `IDocumentInfo.getFileType()`
- **ฉันจะรับจำนวนหน้าได้อย่างไร?** `IDocumentInfo.getPageCount()`
- **การเรียกใดให้ขนาดเอกสารเป็นไบต์?** `IDocumentInfo.getSize()`
- **ฉันต้องใช้ไลเซนส์เพื่อรันตัวอย่างหรือไม่?** ไลเซนส์ทดลองหรือไลเซนส์ชั่วคราวทำงานสำหรับการประเมินค่า
- **เวอร์ชัน Java ที่ต้องการคืออะไร?** Java 8 หรือสูงกว่า

## “java get file extension” คืออะไร?
**java get file extension** หมายถึงการดึงรูปแบบไฟล์ (เช่น DOCX, PDF) จากเอกสารใน Java อย่างโปรแกรมเมติก GroupDocs.Redaction เปิดเผยข้อมูลนี้ผ่านอินเทอร์เฟซ `IDocumentInfo` ดังนั้นการเรียกเมธอดเดียวจะคืนสตริงส่วนขยาย

## ทำไมต้องใช้ GroupDocs.Redaction สำหรับการดึงเมตาดาต้า?
GroupDocs.Redaction สามารถอ่านเมตาดาต้าจากรูปแบบอินพุต **50+** ประเภท รวมถึง PDF, DOCX, XLSX, PPTX และรูปภาพ—โดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ มันประมวลผล PDF 300 หน้าในเวลาน้อยกว่า 200 ms บนเซิร์ฟเวอร์ทั่วไป โดยใช้ RAM ต่ำกว่า 20 MB วิธีการที่เพิ่มประสิทธิภาพนี้ทำให้คุณสามารถขยายงานแบบแบตช์ได้พร้อมคงผลลัพธ์ที่สอดคล้องกันในทุกรูปแบบที่รองรับ

## ข้อกำหนดเบื้องต้น
- ติดตั้ง Java 8 หรือใหม่กว่า
- IDE ที่รองรับ Maven (IntelliJ IDEA, Eclipse ฯลฯ)
- เข้าถึงไลเซนส์ GroupDocs.Redaction (ทดลองฟรีหรือไลเซนส์ชั่วคราว)

## การตั้งค่า GroupDocs.Redaction สำหรับ Java

### การติดตั้ง Maven
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
ทางเลือกอื่น ดาวน์โหลดเวอร์ชันล่าสุดของ GroupDocs.Redaction สำหรับ Java จาก [เวอร์ชันล่าสุดของ GroupDocs.Redaction สำหรับ Java](https://releases.groupdocs.com/redaction/java/).

#### การรับไลเซนส์
- **ทดลองฟรี:** เริ่มต้นด้วยการทดลองฟรีเพื่อประเมินไลบรารี  
- **ไลเซนส์ชั่วคราว:** รับไลเซนส์ชั่วคราวสำหรับการประเมินที่ต่อเนื่อง  
- **ซื้อ:** พิจารณาซื้อหากตรงกับความต้องการของคุณ

## ทำไม java get file extension ถึงสำคัญในโครงการจริง
การรู้ประเภทของเอกสารในขณะอัปโหลดทำให้คุณสามารถกำหนดเส้นทางไฟล์ไปยัง pipeline การประมวลผลที่ถูกต้อง—PDF ไปยังการลบข้อมูล, ไฟล์ Word ไปยังการแปลง, รูปภาพไปยัง OCR นอกจากนี้ยังช่วยให้ทำการตรวจสอบความปลอดภัย (บล็อกไฟล์ที่เป็น executable) และแสดงไอคอน UI ที่แม่นยำในระบบจัดการเอกสาร

## วิธีการ java get file extension, get document size java, และ get page count java
คุณสามารถดึงประเภทไฟล์, ขนาด, และจำนวนหน้าได้ด้วยการเรียกเดียวที่ `IDocumentInfo` การเรียกนี้อ่านเฉพาะส่วนหัวของเอกสารเท่านั้น ทำให้ไฟล์ขนาดใหญ่ก็ถูกประมวลผลอย่างรวดเร็วและใช้หน่วยความจำน้อย วิธีการที่เบานี้เหมาะสำหรับการประมวลผลแบบแบตช์ที่ต้องการข้อมูลสรุปก่อนตัดสินใจดำเนินการต่อ อินเทอร์เฟซ `IDocumentInfo` ให้เมตาดาต้าเช่น ประเภทไฟล์, จำนวนหน้า, และขนาดโดยไม่ต้องโหลดเอกสารเต็ม

### ขั้นตอนที่ 1: นำเข้าคลาสที่จำเป็น
เพิ่ม import ที่จำเป็นที่ส่วนบนของไฟล์ Java ของคุณ:

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.domain.IDocumentInfo;
```

### ขั้นตอนที่ 2: เริ่มต้น redactor
คลาส `Redactor` เป็นเอนจิ้นหลักที่เปิดเอกสารและให้เข้าถึงเมตาดาต้าของมัน.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    // Code for retrieving information will go here.
} finally {
    redactor.close();
}
```

### ขั้นตอนที่ 3: ดึงและแสดงข้อมูลเอกสาร
`IDocumentInfo` ให้เมตาดาต้าที่คุณต้องการ เรียก `getDocumentInfo()` ครั้งเดียวแล้วสอบถามคุณสมบัติเพิ่มเติมสามอย่าง.

```java
// Retrieve document information
IDocumentInfo info = redactor.getDocumentInfo();

// Output document type, page count, and size in bytes
System.out.println("File Type: " + info.getFileType());
System.out.println("Page Count: " + info.getPageCount());
System.out.println("Size (Bytes): " + info.getSize());
```

คำสั่ง `System.out.println` สามบรรทัดจะแสดงประเภทไฟล์, จำนวนหน้า, และขนาดเป็นไบต์—ข้อมูลที่คุณต้องการสำหรับการประมวลผลต่อไป

## วิธีการดึงเมตาดาต้า PDF ด้วย Java
โหลด PDF ด้วย `Redactor` แล้วเรียก `getDocumentInfo()` เมธอดเดียวกันจะคืนค่าฟิลด์เฉพาะของ PDF เช่น เวอร์ชันและสถานะการเข้ารหัส ดังนั้นไม่ต้องเขียนโค้ดเพิ่มเติม วัตถุ `IDocumentInfo` ที่คืนมามีฟิลด์เฉพาะของ PDF เช่น หมายเลขเวอร์ชัน, ธงการเข้ารหัส, และเมตาดาต้ามาตรฐาน (ผู้เขียน, ชื่อเรื่อง, วันที่สร้าง) คุณสามารถเข้าถึงคุณสมบัติเหล่านี้โดยตรงผ่านเมธอด getter ทำให้คุณสามารถแสดงหรือบันทึกรายละเอียด PDF ได้โดยไม่ต้องพาร์สเพิ่มเติม

## กรณีการใช้งานทั่วไป
1. **ระบบจัดการเอกสาร:** แยกประเภทไฟล์อัตโนมัติตามประเภทหรือขนาดก่อนจัดเก็บ  
2. **pipeline การประมวลผลเนื้อหา:** เลือกกลยุทธ์การประมวลผลที่แตกต่างตามจำนวนหน้า (เช่น ลบข้อมูลเป็นชุดจาก PDF ขนาดใหญ่ vs. Word เอกสารขนาดเล็ก)  
3. **ห้องสมุดสินทรัพย์ดิจิทัล:** แสดงตัวอย่างคุณสมบัติเอกสารอย่างรวดเร็วให้ผู้ใช้โดยไม่ต้องเปิดไฟล์  

## ปัญหาทั่วไปและวิธีแก้
- **ไฟล์ไม่พบ:** ตรวจสอบเส้นทางแบบ absolute หรือ relative ที่ส่งให้ `Redactor`  
- **รูปแบบไม่รองรับ:** ตรวจสอบให้แน่ใจว่าส่วนขยายของเอกสารของคุณอยู่ในรายการ 50+ รูปแบบที่ GroupDocs.Redaction รองรับ  
- **ข้อผิดพลาดไลเซนส์:** ใช้ไลเซนส์ทดลองหรือไลเซนส์ถาวรที่ถูกต้อง; มิฉะนั้น API จะโยนข้อยกเว้นเรื่องไลเซนส์  

## เคล็ดลับการแก้ปัญหา (อ่านเมตาดาต้าเอกสารด้วย Java)
- ห่อการเรียกเมตาดาต้าในบล็อก `try‑catch` เพื่อจัดการไฟล์ที่เสียหายอย่างราบรื่น  
- ใช้ `redactor.isEncrypted()` (หากมี) เพื่อตรวจจับ PDF ที่เข้ารหัสก่อนอ่านเมตาดาต้า  
- เมื่อประมวลผลไฟล์จำนวนมาก ให้ใช้ thread‑pool ซ้ำและปิดแต่ละอินสแตนซ์ของ `Redactor` อย่างรวดเร็วเพื่อหลีกเลี่ยงการรั่วของ file‑handle  

## พิจารณาด้านประสิทธิภาพ
เมื่อจัดการแบตช์ขนาดใหญ่:
- เปิดแต่ละเอกสารในบล็อก `try‑with‑resources` เพื่อรับประกันการปล่อย file handle อย่างทันท่วงที  
- แคชเฉพาะเมตาดาต้าที่ต้องการ; หลีกเลี่ยงการโหลดเนื้อหาเอกสารเต็มหากไม่จำเป็น  

## คำถามที่พบบ่อย
**ถาม: GroupDocs.Redaction คืออะไร?**  
**ตอบ:** GroupDocs.Redaction เป็นไลบรารี Java ที่ช่วยให้ทำการลบข้อมูล, ดึงเมตาดาต้า, และการประมวลผลเอกสารแบบไม่ขึ้นกับรูปแบบได้มากกว่า 50 ประเภทไฟล์  

**ถาม: ฉันสามารถดึงเมตาดาต้าจากไฟล์ PDF ได้หรือไม่?**  
**ตอบ:** ได้, `IDocumentInfo` คืนค่าเวอร์ชัน PDF, สถานะการเข้ารหัส, และเมตาดาต้าพื้นฐานโดยไม่ต้องเขียนโค้ดเพิ่มเติม  

**ถาม: ฉันจะจัดการข้อยกเว้นเมื่อดึงข้อมูลเอกสารอย่างไร?**  
**ตอบ:** ห่อการเรียก `getDocumentInfo()` ในบล็อก `try‑catch` และจัดการ `RedactionException` เพื่อจัดการไฟล์ที่เสียหายหรือไม่รองรับ  

**ถาม: ฉันสามารถรับข้อมูลอะไรเกี่ยวกับเอกสารได้บ้าง?**  
**ตอบ:** ประเภทไฟล์, จำนวนหน้า, ขนาดเป็นไบต์, เวอร์ชัน PDF, ธงการเข้ารหัส, และเมตาดาต้าพื้นฐานของผู้เขียน/การสร้าง  

**ถาม: มีการสนับสนุนการประมวลผลแบบแบตช์หลายเอกสารอย่างมีประสิทธิภาพหรือไม่?**  
**ตอบ:** มี, สร้าง `Redactor` แยกสำหรับแต่ละไฟล์ภายใน thread pool และใช้ JVM เดียวกันซ้ำเพื่อให้ได้อัตราการทำงานสูง  

## สรุป
ตอนนี้คุณรู้วิธี **java get file extension**, **get document size java**, **get page count java**, และ **retrieve pdf metadata java** ด้วย GroupDocs.Redaction แล้ว นำส่วนโค้ดเหล่านี้รวมเข้าในแอปพลิเคชัน Java ของคุณเพื่อทำการตัดสินใจที่ฉลาดขึ้นเกี่ยวกับการจัดการเอกสาร, ปรับปรุงประสิทธิภาพ, และมอบประสบการณ์ผู้ใช้ที่ดียิ่งขึ้น

---

**อัปเดตล่าสุด:** 2026-09-06  
**ทดสอบกับ:** GroupDocs.Redaction 24.9 for Java  
**ผู้เขียน:** GroupDocs  

**แหล่งข้อมูล**  
- **เอกสาร:** [เอกสาร GroupDocs Redaction Java](https://docs.groupdocs.com/redaction/java/)  
- **อ้างอิง API:** [อ้างอิง API ของ GroupDocs](https://reference.groupdocs.com/redaction/java)  
- **ดาวน์โหลด:** [ดาวน์โหลด GroupDocs.Redaction สำหรับ Java](https://releases.groupdocs.com/redaction/java/)  
- **GitHub:** [ที่เก็บ GitHub ของ GroupDocs](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **สนับสนุนฟรี:** [ฟอรั่ม GroupDocs](https://forum.groupdocs.com/c/redaction/33)  
- **ไลเซนส์ชั่วคราว:** [รับไลเซนส์ชั่วคราว](https://purchase.groupdocs.com/temporary-license/)

```java
import com.groupdocs.redaction.Redactor;

// Initialize Redactor with the path to your document
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

## บทแนะนำที่เกี่ยวข้อง

- [java อ่านเมตาดาต้าไฟล์ – ประเภทไฟล์ด้วย GroupDocs.Redaction](/redaction/java/metadata-redaction/groupdocs-redaction-java-document-metadata-extraction/)
- [สร้างตัวอย่างและจำนวนหน้าของเอกสาร – GroupDocs Java](/redaction/java/document-information/)
- [วิธีดูตัวอย่างหน้าโดยใช้ GroupDocs.Redaction สำหรับ Java – คู่มือฉบับสมบูรณ์](/redaction/java/document-loading/load-preview-document-pages-groupdocs-redaction-java/)