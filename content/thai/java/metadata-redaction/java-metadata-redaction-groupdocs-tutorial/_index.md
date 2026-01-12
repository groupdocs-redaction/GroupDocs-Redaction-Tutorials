---
date: '2026-01-08'
description: เรียนรู้วิธีใช้ MetadataSearchRedaction ใน Java กับ GroupDocs.Redaction
  เพื่อทำการลบข้อมูลเมตาที่ละเอียดอ่อนของเอกสารอย่างปลอดภัย
keywords:
- metadata redaction Java
- GroupDocs Redaction tutorial
- secure document metadata
title: วิธีใช้ MetadataSearchRedaction ใน Java กับ GroupDocs
type: docs
url: /th/java/metadata-redaction/java-metadata-redaction-groupdocs-tutorial/
weight: 1
---

# วิธีใช้ MetadataSearchRedaction ใน Java กับ GroupDocs

ในคู่มือฉบับครอบคลุมนี้คุณจะค้นพบ **วิธีใช้ MetadataSearchRedaction** เพื่อกำจัดเมตาดาต้าลับ—เช่น ชื่อบริษัท—จาก Word, PDF และรูปแบบเอกสารอื่น ๆ ด้วย GroupDocs.Redaction for Java. เมื่อจบบทเรียนคุณจะสามารถรวมการลบเมตาดาต้าเข้ากับเวิร์กโฟลว์ Java ใด ๆ และรักษาข้อมูลที่สำคัญให้ปลอดภัย.

## Quick Answers
- **MetadataSearchRedaction ทำอะไร?** มันค้นหาฟิลด์เมตาดาต้าตามที่ระบุและแทนค่าของพวกมันด้วยข้อความที่กำหนดเอง.  
- **ต้องใช้ไลบรารีใด?** GroupDocs.Redaction for Java (v24.9 หรือใหม่กว่า).  
- **ต้องการไลเซนส์หรือไม่?** การทดลองใช้ฟรีสามารถใช้เพื่อประเมินผล; จำเป็นต้องมีไลเซนส์เต็มสำหรับการใช้งานจริง.  
- **สามารถคงรูปแบบไฟล์เดิมได้หรือไม่?** ได้—ใช้ `SaveOptions` เพื่อรักษารูปแบบเดิม.  
- **วิธีนี้ปลอดภัยต่อการทำงานหลายเธรดหรือไม่?** แต่ละอินสแตนซ์ของ `Redactor` เป็นอิสระ ดังนั้นคุณสามารถประมวลผลเอกสารพร้อมกันได้.

## What is MetadataSearchRedaction?
`MetadataSearchRedaction` เป็นคลาสการลบข้อมูลที่เฉพาะเจาะจงซึ่งให้คุณกำหนดเป้าหมายที่คุณสมบัติเบื้องหลัง (เช่น *Company*, *Author*) และแทนที่เนื้อหาด้วยข้อความแทนที่. เหมาะสำหรับเมื่อคุณต้องการทำให้ข้อมูลบริษัทเป็นนามธรรมก่อนแชร์เอกสารกับพันธมิตรภายนอก.

## Why use MetadataSearchRedaction for metadata redaction?
- **ความแม่นยำ** – ลบเฉพาะฟิลด์ที่คุณระบุ, ปล่อยส่วนที่เหลือของเอกสารไม่เปลี่ยนแปลง.  
- **การปฏิบัติตาม** – ช่วยให้สอดคล้องกับ GDPR, HIPAA, และกฎระเบียบความเป็นส่วนตัวอื่น ๆ โดยการลบตัวระบุที่ซ่อนอยู่.  
- **พร้อมอัตโนมัติ** – เข้ากับ pipeline การประมวลผลแบบแบชหรือไมโครเซอร์วิสได้อย่างราบรื่น.

## Prerequisites
- **GroupDocs.Redaction for Java** ≥ 24.9.  
- Java 8 หรือใหม่กว่า ติดตั้งบนเครื่องของคุณ.  
- IDE เช่น IntelliJ IDEA หรือ Eclipse (ไม่บังคับแต่แนะนำ).  
- ความคุ้นเคยพื้นฐานกับ Maven (หรือความสามารถในการเพิ่ม JAR ด้วยตนเอง).  

## Setting Up GroupDocs.Redaction for Java
เพิ่ม repository และ dependency ลงใน `pom.xml` ของคุณ ขั้นตอนนี้ทำให้ Maven สามารถดาวน์โหลดไลบรารีโดยอัตโนมัติ.

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

*หรือคุณสามารถดาวน์โหลด JAR โดยตรงจากหน้าปล่อยอย่างเป็นทางการ:*  
[GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/)

### License Acquisition
- **Free Trial** – ดาวน์โหลดไลเซนส์ทดลองเพื่อสำรวจคุณสมบัติทั้งหมด.  
- **Temporary License** – ใช้สำหรับการทดสอบต่อเนื่อง.  
- **Full License** – จำเป็นสำหรับการใช้งานในสภาพแวดล้อมการผลิต.

## Basic Initialization
สร้างอินสแตนซ์ `Redactor` ที่ชี้ไปยังเอกสารที่คุณต้องการประม```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

## Implementation Guide

### Step 1: Import Necessary Classes
การนำเข้าดังกล่าวให้คุณเข้าถึงเอนจินการลบ, ตัวเลือกการบันทึก, และยูทิลิตี้เมตาดาต้า.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.redactions.MetadataFilters;
import com.groupdocs.redaction.redactions.MetadataSearchRedaction;
```

### Step 2: Initialize Redactor
สร้างอินสแตนซ์ของ `Redactor` ด้วยเส้นทางไปยังไฟล์ต้นฉบับของคุณ.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

### Step 3: Configure Metadata Search and Redaction
สร้าง `MetadataSearchRedaction` ที่ค้นหาสตริงที่ตรงกัน **"Company Ltd."** และแทนที่ด้วย **"--company--"**. การเรียก `setFilter` จำกัดการทำงานไว้ที่ฟิลด์เมตาดาต้า *Company* เท่านั้น.

```java
MetadataSearchRedaction redaction = new MetadataSearchRedaction("Company Ltd.", "--company--");
redaction.setFilter(MetadataFilters.Company);
```

### Step 4: Apply the Redaction
เรียกใช้การลบข้อมูลบนเอกสารที่เปิดอยู่.

```java
redactor.apply(redaction);
```

### Step 5: Save with Custom Options
กำหนดค่า `SaveOptions` เพื่อให้ไฟล์ที่ลบข้อมูลมีส่วนต่อท้าย “_Redacted” ในขณะที่ยังคงรูปแบบเดิม.

```java
SaveOptions tmp0 = new SaveOptions();
tmp0.setAddSuffix(true);  // Adds "_Redacted" to file name
	tmp0.setRasterizeToPDF(false);  // Keeps original format

redactor.save(tmp0);
```

### Step 6: Release Resources
ควรปิด `Redactor` เสมอเพื่อปลดปล่อยทรัพยากรเนทีฟและหลีกเลี่ยงการรั่วไหลของหน่วยความจำ.

```java
finally {
    redactor.close();
}
```

## Common Issues and Solutions
- **FileNotFoundException** – ตรวจสอบเส้นทางที่ส่งให้ `Redactor` อีกครั้ง. ใช้เส้นทางแบบเต็มหรือ `Paths.get(...)` เพื่อความน่าเชื่อถือ.  
- **No changes observed** – ตรวจสอบว่าฟิลด์เมตาดาต้าที่คุณกำหนดเป้าหมายมีสตริงที่ค้นหรือไม่; เมตาดาต้าเป็นตัวพิมพ์ใหญ่‑เล็กโดยค่าเริ่มต้น.  
- **Out‑of‑memory errors on large files** – ประมวลผลเอกสารเป็นชุดเล็ก ๆ และเรียก `redactor.close()` ทันทีหลังจากแต่ละไฟล์.

## Practical Applications
1. **Legal Documentation** – ลบชื่อบริษัทของลูกค้าก่อนส่งสัญญาให้กับบุคคลที่สาม.  
2. **Financial Reporting** – ทำให้ตัวระบุภายในในไฟล์การตรวจสอบเป็นนามธรรม.  
3. **Collaborative Projects** – ปกป้องข้อมูลที่เป็นกรรมสิทธิ์เมื่อแชร์ร่างงานกับผู้ขายภายนอก.

## Performance Considerations
- **Memory Management** – ไลบรารีเก็บเอกสารทั้งหมดในหน่วยความจำ; การปิด `Redactor` หลังจากแต่ละไฟล์เป็นสิ่งสำคัญ.  
- **Batch Processing** – สำหรับสถานการณ์ที่มีปริมาณสูง, วนลูปผ่านคอลเลกชันของไฟล์และใช้ `SaveOptions` อินสแตนซ์เดียวซ้ำ.  
- **Stay Updated** – การปล่อยเวอร์ชันใหม่นำมาซึ่งการปรับปรุงประสิทธิภาพและการแก้บั๊ก; ควรใช้เวอร์ชันเสถียรล่าสุดเสมอ.

## Conclusion
คุณตอนนี้รู้ **วิธีใช้ MetadataSearchRedaction** เพื่อกำจัดเมตาดาต้าบริษัทจากเอกสารอย่างปลอดภัยโดยใช้ GroupDocs.Redaction for Java. นำขั้นตอนเหล่านี้ไปใช้ใน pipeline การประมวลผลเอกสารของคุณเพื่อให้สอดคล้องและปกป้องข้อมูลที่สำคัญ.

**Next Steps**
- ทดลองใช้ฟิลด์เมตาดาต้าอื่น ๆ เช่น *Author* หรือ *Creator*.  
- ผสานการลบเมตาดาต้ากับการลบข้อความหรือรูปภาพเพื่อให้ได้โซลูชันครอบคลุมทั้งหมด.  

## FAQ Section
1. **What is GroupDocs.Redaction for Java?**  
   - เป็นไลบรารีที่ทรงพลังที่ช่วยให้คุณลบข้อความ, เมตาดาต้า, และรูปภาพในเอกสารโดยใช้แอปพลิเคชัน Java.  
2. **Can I use GroupDocs.Redaction without purchasing a license?**  
   - ใช่, แต่มีข้อจำกัด. การทดลองใช้ฟรีหรือไลเซนส์ชั่วคราวให้การเข้าถึงเต็มรูปแบบเพื่อการทดสอบ.  
3. **How do I ensure document formats are preserved during redaction?**  
   - ใช้ `SaveOptions` เพื่อระบุความต้องการของคุณ, เช่นหลีกเลี่ยงการแปลงเป็น PDF แบบ rasterization.  
4. **What types of documents can be redacted using GroupDocs.Redaction?**  
   - รองรับหลายประเภท, รวมถึง Word, Excel, PowerPoint, PDF, และอื่น ๆ อีกมาก.  
5. **Where can I find support if I run into issues?**  
   - เยี่ยมชม [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) เพื่อขอความช่วยเหลือ.  

## Frequently Asked Questions
**Q: Does MetadataSearchRedaction work with encrypted documents?**  
A: ใช่. โหลดเอกสารด้วยรหัสผ่านที่เหมาะสมโดยใช้คอนสตรัคเตอร์ของ `Redactor` ที่รับพารามิเตอร์รหัสผ่าน.  

**Q: Can I chain multiple metadata redactions in a single run?**  
A: แน่นอน. สร้างหลาย `MetadataSearchRedaction` ตั้งค่าตัวกรองที่แตกต่างกันและใช้พวกมันตามลำดับก่อนบันทึก.  

**Q: Is it possible to preview redactions before saving?**  
A: คุณสามารถเรียก `redactor.getRedactions()` เพื่อดึงรายการของการลบที่รอดำเนินการและตรวจสอบโดยโปรแกรม.  

## Resources
- **Documentation**: สำรวจคู่มือโดยละเอียดที่ [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/).  
- **API Reference**: ตรวจสอบอ้างอิง API ทั้งหมดที่ [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java).  
- **Download Library**: เข้าถึงเวอร์ชันล่าสุดจาก [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/).  
- **Source Code**: ดูและมีส่วนร่วมบน [GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).  
- **Support**: รับความช่วยเหลือผ่านช่องทางสนับสนุนฟรีที่ [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33).

---

**อัปเดตล่าสุด:** 2026-01-08  
**ทดสอบด้วย:** GroupDocs.Redaction 24.9 for Java  
**ผู้เขียน:** GroupDocs