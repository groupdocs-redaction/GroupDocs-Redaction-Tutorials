---
date: '2026-02-18'
description: เรียนรู้วิธีลบหมายเหตุใน PDF ด้วย Java โดยใช้ GroupDocs.Redaction, การกรองด้วย
  regex และบันทึกเอกสารที่ทำการลบข้อมูลด้วยส่วนต่อท้ายชื่อไฟล์.
keywords:
- annotation removal java
- groupdocs redaction setup
- regex annotation cleanup
title: ลบหมายเหตุ PDF ด้วย Java และ GroupDocs.Redaction
type: docs
url: /th/java/annotation-redaction/master-annotation-removal-java-groupdocs-redaction/
weight: 1
---

# ลบการทำเครื่องหมาย PDF ใน Java ด้วย GroupDocs.Redaction

หากคุณต้องการ **remove PDF annotations** อย่างรวดเร็วและเชื่อถือได้—ไม่ว่าจะเป็นความคิดเห็น, ไฮไลท์, หรือโน้ตสติ๊กกี้—GroupDocs.Redaction for Java จะมอบโซลูชันแบบโปรแกรมที่สะอาดตา ในบทแนะนำนี้เราจะอธิบายทุกขั้นตอนตั้งแต่การตั้งค่า Maven ไปจนถึงตัวกรองแบบ regex ที่ลบเฉพาะการทำเครื่องหมายที่คุณต้องการเท่านั้น และเราจะแสดงวิธี **save the redacted document** พร้อมเพิ่มส่วนต่อท้ายชื่อไฟล์เพื่อให้ไฟล์ต้นฉบับไม่ถูกแก้ไข

## คำตอบอย่างรวดเร็ว
- **ไลบรารีใดที่จัดการการลบการทำเครื่องหมาย?** GroupDocs.Redaction for Java.  
- **คีย์เวิร์ดใดที่ทำให้เกิดการลบ?** A regular‑expression pattern you define (e.g., `(?im:(use|show|describe))`).  
- **ฉันต้องการไลเซนส์หรือไม่?** A trial works for evaluation; a commercial license is required for production.  
- **ฉันสามารถบันทึกไฟล์ที่ทำความสะอาดแล้วด้วยชื่อใหม่ได้หรือไม่?** Yes—use `SaveOptions.setAddSuffix(true)`.  
- **Maven เป็นวิธีเดียวในการเพิ่มไลบรารีหรือไม่?** No, you can also download the JAR directly.

## การลบการทำเครื่องหมาย PDF คืออะไร?
การลบการทำเครื่องหมาย PDF หมายถึงการค้นหาและลบวัตถุการทำเครื่องหมาย (ความคิดเห็น, ไฮไลท์, โน้ตสติ๊กกี้) จากเอกสารโดยโปรแกรม ด้วย GroupDocs.Redaction คุณสามารถกำหนดเป้าหมายวัตถุเหล่านี้ตามเนื้อหาข้อความของมัน ทำให้เหมาะอย่างยิ่งสำหรับ **legal document redaction**, โครงการ data‑anonymization, หรือกระบวนการทำงานใด ๆ ที่ต้องการไฟล์ที่สะอาดและพร้อมแชร์

## ทำไมต้องใช้การลบการทำเครื่องหมาย PDF กับ GroupDocs.Redaction?
- **Precision** – Regex ให้คุณระบุได้อย่างแม่นยำว่าความคิดเห็นใดจะลบ.  
- **Speed** – ประมวลผล **multiple documents** เป็นชุดโดยไม่ต้องเปิดแต่ละไฟล์ด้วยตนเอง.  
- **Compliance** – รับประกันว่าความคิดเห็นที่เป็นความลับจะไม่ออกจากองค์กรของคุณ.  
- **Cross‑format support** – ทำงานกับ PDF, DOCX, XLSX และอื่น ๆ ทำให้คุณจัดการไฟล์สำนักงานทั้งหมดในที่เดียว.

## ข้อกำหนดเบื้องต้น
- Java JDK 1.8 หรือใหม่กว่า.  
- IDE เช่น IntelliJ IDEA หรือ Eclipse.  
- ความคุ้นเคยพื้นฐานกับ regular expressions.  

## Maven Dependency GroupDocs

เพิ่มรีโพซิทอรีของ GroupDocs และอาร์ติแฟกต์ Redaction ไปยังไฟล์ `pom.xml` ของคุณ:

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

### ดาวน์โหลดโดยตรง (ทางเลือก)

หากคุณไม่ต้องการใช้ Maven ให้ดาวน์โหลด JAR ล่าสุดจากหน้าอย่างเป็นทางการ: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

#### ขั้นตอนการรับไลเซนส์
1. **Free Trial** – ดาวน์โหลดเวอร์ชันทดลองเพื่อสำรวจคุณสมบัติหลัก.  
2. **Temporary License** – ขอคีย์ชั่วคราวสำหรับการทดสอบฟีเจอร์เต็ม.  
3. **Purchase** – รับไลเซนส์เชิงพาณิชย์สำหรับการใช้งานในผลิตภัณฑ์.  

## การเริ่มต้นและตั้งค่าพื้นฐาน

โค้ดตัวอย่างต่อไปนี้แสดงวิธีสร้างอินสแตนซ์ `Redactor` และกำหนดค่า options การบันทึกพื้นฐาน:

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;

public class InitializeRedaction {
    public static void main(String[] args) throws Exception {
        // Load the document using Redactor
        final Redactor redactor = new Redactor("path/to/your/document");
        
        try {
            // Perform your redaction operations here
            
            // Save options can be customized as needed
            SaveOptions saveOptions = new SaveOptions();
            saveOptions.setAddSuffix(true);  // Example option: Add suffix to filename
            
            // Save the modified document
            redactor.save(saveOptions, "path/to/output/document");
        } finally {
            redactor.close();  // Always close resources to prevent memory leaks
        }
    }
}
```

## คู่มือขั้นตอนการลบการทำเครื่องหมาย PDF

### ขั้นตอน 1: โหลดเอกสารของคุณ

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/ANNOTATED_XLSX");
```

### ขั้นตอน 2: ใช้การลบการทำเครื่องหมายด้วย Regex

```java
redactor.apply(new DeleteAnnotationRedaction("(?im:(use|show|describe))"));
```

- **Explanation** – แพทเทิร์น `(?im:(use|show|describe))` ไม่สนใจตัวพิมพ์ใหญ่‑เล็ก (`i`) และทำงานหลายบรรทัด (`m`). มันจับคู่กับการทำเครื่องหมายใด ๆ ที่มีคำว่า *use*, *show*, หรือ *describe*.

### ขั้นตอน 3: กำหนดค่า Save Options (เพิ่มส่วนต่อท้ายชื่อไฟล์)

```java
SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true);  // Append a suffix to the output filename
saveOptions.setRasterizeToPDF(false);  // Do not convert to PDF format
```

### ขั้นตอน 4: บันทึกและปล่อยทรัพยากร (บันทึกเอกสารที่ทำการลบเครื่องหมายแล้ว)

```java
redactor.save(saveOptions, "YOUR_OUTPUT_DIRECTORY/RedactedDocument");
redactor.close();  // Always close the Redactor instance
```

**เคล็ดลับการแก้ไขปัญหา**  
- ตรวจสอบว่า regex ของคุณตรงกับข้อความการทำเครื่องหมายที่คุณต้องการลบจริงหรือไม่.  
- ตรวจสอบสิทธิ์ของระบบไฟล์อีกครั้งหากการเรียก `save` ทำให้เกิด `IOException`.  

## กรณีการใช้งานทั่วไป

1. **Data Anonymization Java** – ลบความคิดเห็นของผู้ตรวจสอบที่มีข้อมูลส่วนบุคคลออกก่อนแชร์ชุดข้อมูล.  
2. **Legal Document Redaction** – ลบโน้ตภายในโดยอัตโนมัติที่อาจเปิดเผยข้อมูลที่เป็นความลับ.  
3. **Batch Processing Pipelines** – ผสานขั้นตอนข้างต้นเข้าสู่งาน CI/CD ที่ **processes multiple documents** และทำความสะอาดรายงานที่สร้างขึ้นแบบเรียลไทม์.  

## พิจารณาด้านประสิทธิภาพ

- **Optimize regex patterns** – นิพจน์ที่ซับซ้อนอาจเพิ่มเวลา CPU โดยเฉพาะกับ PDF ขนาดใหญ่.  
- **Reuse Redactor instances** ใช้ซ้ำเฉพาะเมื่อประมวลผลหลายไฟล์ประเภทเดียวกัน; มิฉะนั้นให้สร้างอินสแตนซ์ต่อไฟล์เพื่อรักษาการใช้หน่วยความจำให้ต่ำ.  
- **Profile** – ใช้เครื่องมือโปรไฟล์ของ Java (เช่น VisualVM) เพื่อตรวจหาจุดคอขวดในการทำงานแบบกลุ่ม.  

## คำถามที่พบบ่อย

**Q: GroupDocs.Redaction for Java คืออะไร?**  
A: เป็นไลบรารี Java ที่ให้คุณลบข้อความ, เมตาดาต้า, และการทำเครื่องหมายในหลายรูปแบบเอกสาร.

**Q: ฉันจะใช้หลาย regex pattern ในการทำงานครั้งเดียวได้อย่างไร?**  
A: รวมพวกมันด้วยตัวดำเนินการ pipe (`|`) ภายในแพทเทิร์นเดียว หรือเรียงต่อหลายการเรียก `DeleteAnnotationRedaction`.

**Q: ไลบรารีนี้รองรับรูปแบบที่ไม่ใช่ข้อความเช่นรูปภาพหรือไม่?**  
A: ใช่, มันสามารถลบข้อมูลใน PDF ที่เป็นภาพและรูปแบบเรสเตอร์อื่น ๆ ได้ แม้ว่าการลบการทำเครื่องหมายจะใช้ได้เฉพาะกับรูปแบบเวกเตอร์ที่รองรับเท่านั้น.

**Q: ถ้าประเภทเอกสารของฉันไม่อยู่ในรายการที่รองรับจะทำอย่างไร?**  
A: ตรวจสอบ [Documentation](https://docs.groupdocs.com/redaction/java/) ล่าสุดเพื่อดูการอัปเดต หรือแปลงไฟล์เป็นรูปแบบที่รองรับก่อน.

**Q: ฉันควรจัดการกับข้อยกเว้นระหว่างการลบเครื่องหมายอย่างไร?**  
A: ห่อโลจิกการลบเครื่องหมายในบล็อก try‑catch, บันทึกรายละเอียดข้อยกเว้น, และตรวจสอบให้ `redactor.close()` ทำงานในบล็อก finally.

## แหล่งข้อมูลเพิ่มเติม

- [เอกสาร](https://docs.groupdocs.com/redaction/java/)
- [อ้างอิง API](https://reference.groupdocs.com/redaction/java)
- [ดาวน์โหลด GroupDocs.Redaction](https://releases.groupdocs.com/redaction/java/)
- [ที่เก็บ GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
- [ฟอรั่มสนับสนุนฟรี](https://forum.groupdocs.com/c/redaction/33)

---

**อัปเดตล่าสุด:** 2026-02-18  
**ทดสอบด้วย:** GroupDocs.Redaction 24.9 for Java  
**ผู้เขียน:** GroupDocs