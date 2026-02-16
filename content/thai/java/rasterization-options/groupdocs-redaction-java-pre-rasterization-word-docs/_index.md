---
date: '2026-02-16'
description: เรียนรู้วิธีใช้ GroupDocs Redaction พร้อมการแรสเตอร์ล่วงหน้าเพื่อทำการลบข้อมูลรูปภาพในเอกสาร
  Word อย่างปลอดภัย รวมถึงการตั้งค่าแบบขั้นตอนต่อขั้นตอน, โค้ด, และการแก้ไขปัญหา
keywords:
- GroupDocs.Redaction Java
- pre-rasterization Word documents
- image area redaction
title: 'วิธีใช้ GroupDocs Redaction สำหรับ Java: การทำพรีเรสเตอร์ไลเซชันในเอกสาร Word'
type: docs
url: /th/java/rasterization-options/groupdocs-redaction-java-pre-rasterization-word-docs/
weight: 1
---

# วิธีใช้ groupdocs redaction สำหรับ Java: Pre‑Rasterization ในเอกสาร Word

ในบทแนะนำนี้คุณจะ **ใช้ groupdocs redaction** เพื่อเปิดใช้งานการทำ pre‑rasterization เมื่อประมวลผลไฟล์ Microsoft Word ทำให้การ **ลบข้อมูลจากรูปภาพในเอกสาร Word** เป็นเรื่องง่าย เราจะเดินผ่านการตั้งค่าเต็มรูปแบบ แสดงวิธีกำหนดค่าไลบรารี และสาธิตการลบข้อมูลในพื้นที่รูปภาพด้วยคำอธิบายที่ชัดเจนและเป็นกันเอง

## คำตอบอย่างรวดเร็ว
- **Pre‑rasterization ทำอะไร?** มันแปลงภาพที่ฝังอยู่เป็นรูปแบบ raster เพื่อให้สามารถแก้ไขหรือทำการลบข้อมูลได้อย่างมีประสิทธิภาพ.  
- **ฉันต้องการไลเซนส์หรือไม่?** การทดลองใช้ฟรีทำงานได้สำหรับการพัฒนา; จำเป็นต้องมีไลเซนส์เต็มสำหรับการใช้งานจริง.  
- **ต้องการเวอร์ชัน Java ใด?** Java 8 หรือใหม่กว่า (แนะนำ JDK 11+).  
- **ฉันสามารถประมวลผลหลายไฟล์ได้หรือไม่?** ได้—ใส่ตรรกะการลบข้อมูลในลูปเพื่อการประมวลผลแบบชุด.  
- **หน่วยความจำเป็นปัญหาหรือไม่?** ภาพขนาดใหญ่อาจต้องเพิ่มขนาด heap; ควรตรวจสอบการใช้หน่วยความจำของ JVM.

## Pre‑rasterization คืออะไรใน groupdocs redaction?
Pre‑rasterization เป็นตัวเลือกการโหลดที่แปลงภาพทั้งหมดในเอกสาร Word ให้เป็นข้อมูลบิตแมพก่อนที่การทำลบข้อมูลใด ๆ จะถูกนำไปใช้ การแปลงนี้ทำให้คลาส `ImageAreaRedaction` สามารถกำหนดเป้าหมายเป็นพิกเซลที่แม่นยำ เพื่อให้การลบหรือปิดบังเนื้อหาภาพทำได้อย่างละเอียด

## ทำไมต้องใช้ groupdocs redaction เพื่อลบรูปภาพในเอกสาร Word?
- **การปฏิบัติตามความปลอดภัย:** สามารถปฏิบัติตาม GDPR, HIPAA หรือกฎระเบียบความเป็นส่วนตัวของข้อมูลอื่น ๆ ได้อย่างง่ายดาย.  
- **พร้อมอัตโนมัติ:** ผสานรวมกับ pipeline ของเอกสาร, ระบบจัดการเนื้อหา, หรือ micro‑services.  
- **เน้นประสิทธิภาพ:** การทำ raster เพียงครั้งเดียวในขณะโหลดจะลดภาระการประมวลผลซ้ำ.  

## ข้อกำหนดเบื้องต้น
- **GroupDocs.Redaction 24.9** (หรือใหม่กว่า) – ไลบรารีที่ให้ฟีเจอร์การทำ raster.  
- **Java Development Kit (JDK)** – เวอร์ชัน 8 หรือใหม่กว่า ติดตั้งบนเครื่องของคุณ.  
- ความคุ้นเคยพื้นฐานกับไวยากรณ์ Java และเครื่องมือสร้าง Maven.  

## การตั้งค่า GroupDocs.Redaction สำหรับ Java

### การตั้งค่า Maven
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
หากคุณไม่ต้องการใช้ Maven ให้ดาวน์โหลด JAR ล่าสุดจากหน้า release อย่างเป็นทางการ: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

#### การรับไลเซนส์
เริ่มต้นด้วยการทดลองใช้ฟรีหรือขอไลเซนส์ชั่วคราวเพื่อประเมินผลิตภัณฑ์ สำหรับฟีเจอร์เต็มในการผลิต ให้ซื้อไลเซนส์ถาวร.

## การเริ่มต้นพื้นฐาน

ด้านล่างเป็นโค้ด Java ขั้นต่ำที่คุณต้องใช้เพื่อสร้างอินสแตนซ์ `Redactor` พร้อมเปิดใช้งาน pre‑rasterization เก็บสแนปช็อตนี้ไว้; เราจะต่อยอดในขั้นตอนต่อไป.

```java
// Ensure necessary imports are included
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;

public class DocumentRedaction {
    public static void main(String[] args) {
        // Initialize load options with pre-rasterization enabled
        LoadOptions loadOptions = new LoadOptions(true);

        // Create a Redactor instance to manage the document
        try (final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX", loadOptions)) {
            // Perform operations on the document
        }
    }
}
```

## คู่มือการนำไปใช้

### การเปิดใช้งาน Pre‑Rasterization

#### ภาพรวม
เมื่อสร้าง `LoadOptions` ด้วยค่า `true` GroupDocs.Redaction จะทำ raster ทุกภาพในไฟล์ Word ขณะโหลด เพื่อเตรียมพร้อมสำหรับการจัดการระดับพิกเซล.

#### คำแนะนำขั้นตอนต่อขั้นตอน

**3.1 การตั้งค่า Load Options**  
สร้างอ็อบเจ็กต์ `LoadOptions` โดยตั้งค่าสถานะ rasterization เป็น `true`:

```java
// Set load options with pre-rasterization enabled
LoadOptions loadOptions = new LoadOptions(true);
```

**3.2 การเริ่มต้นอ็อบเจ็กต์ Redactor**  
ส่ง `loadOptions` ไปยังคอนสตรัคเตอร์ของ `Redactor` เพื่อให้เอกสารถูกเปิดด้วยการทำ raster:

```java
// Initialize the Redactor object using specified file path and load options
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX", loadOptions);
```

**3.3 การใช้ Image Area Redaction**  
กำหนดพื้นที่สี่เหลี่ยม (x, y, width, height) ที่คุณต้องการซ่อน จากนั้นแทนที่ด้วยสีทึบ:

```java
import com.groupdocs.redaction.redactions.ImageAreaRedaction;
import com.groupdocs.redaction.redactions.RegionReplacementOptions;

// Define the region to be redacted (x, y, width, height)
ImageAreaRedaction areaRedaction = new ImageAreaRedaction(100, 100, 200, 50);

// Apply a solid color as replacement
RegionReplacementOptions options = new RegionReplacementOptions(java.awt.Color.BLACK);

// Execute the redaction on your document
redactor.apply(areaRedaction);
```

### ข้อผิดพลาดทั่วไปและเคล็ดลับการแก้ปัญหา
- **ข้อผิดพลาดเส้นทางไฟล์:** ตรวจสอบว่าเส้นทางไฟล์ถูกต้องและแอปพลิเคชันมีสิทธิ์อ่าน/เขียน.  
- **ปัญหาการทำ raster:** ตรวจสอบให้แน่ใจว่าธง `LoadOptions` ตั้งเป็น `true`; มิฉะนั้นพื้นที่รูปภาพจะยังเป็นเวกเตอร์และไม่สามารถลบได้.  
- **ข้อจำกัดหน่วยความจำ:** ไฟล์ Word ขนาดใหญ่ที่มีภาพความละเอียดสูงหลายภาพอาจต้องการ heap ของ JVM ที่ใหญ่ขึ้น (`-Xmx2g` หรือสูงกว่า).  

## การประยุกต์ใช้งานจริง

1. **การลบข้อมูลที่ละเอียดอ่อน:** ทำให้รูปถ่ายส่วนบุคคล, ลายเซ็น, หรือบัตรประจำตัวสแกนถูกซ่อนโดยอัตโนมัติก่อนแชร์.  
2. **การจัดการการปฏิบัติตาม:** ปฏิบัติตามกฎระเบียบเฉพาะอุตสาหกรรมโดยลบข้อมูลภาพจากสัญญาหรือรายงาน.  
3. **การแชร์เอกสารอย่างปลอดภัย:** ให้คู่ค้าดูเวอร์ชันที่ลบข้อมูลของเอกสารในขณะที่ยังคงรูปแบบเดิม.  

การผสาน groupdocs redaction เข้ากับเวิร์กโฟลว์ที่มีอยู่ (เช่น pipeline CI/CD, API การจัดการเอกสาร) สามารถทำให้การตรวจสอบการปฏิบัติตามอัตโนมัติมากยิ่งขึ้น.

## พิจารณาด้านประสิทธิภาพ

- **การจัดการหน่วยความจำอย่างมีประสิทธิภาพ:** จัดสรร heap เพียงพอและปิดอินสแตนซ์ `Redactor` อย่างทันท่วงที (บล็อก `try‑with‑resources` ทำเช่นนี้โดยอัตโนมัติ).  
- **การเพิ่มประสิทธิภาพทรัพยากร:** ใช้ `LoadOptions` อย่างชาญฉลาด—เปิด rasterization เฉพาะเมื่อคุณต้องการแก้ไขพื้นที่รูปภาพ; มิฉะนั้นให้ปิดเพื่อการลบข้อความอย่างรวดเร็ว.  

การปฏิบัติตามแนวทางเหล่านี้ช่วยให้การประมวลผลตอบสนองได้ดีแม้กับไฟล์ Word ขนาดใหญ่ที่มีภาพจำนวนมาก.

## สรุป

คุณได้เรียนรู้วิธี **ใช้ groupdocs redaction** เพื่อเปิดใช้งาน pre‑rasterization สำหรับเอกสาร Word และทำการลบข้อมูลในพื้นที่รูปภาพอย่างแม่นยำ ความสามารถนี้ทำให้คุณสามารถปกป้องเนื้อหาภาพ, ปฏิบัติตามกฎระเบียบ, และทำให้การแจกจ่ายเอกสารที่ปลอดภัยเป็นเรื่องง่าย.

**ขั้นตอนต่อไป:** สำรวจประเภทการลบข้อมูลเพิ่มเติม (ข้อความ, metadata), ทดลองประมวลผลแบบชุด, หรือผสานไลบรารีเข้าสู่บริการ RESTful เพื่อการลบข้อมูลตามความต้องการ.

## คำถามที่พบบ่อย

**Q1: Pre‑rasterization คืออะไรใน groupdocs redaction สำหรับ Java?**  
A: มันแปลงภาพภายในเอกสารเป็นรูปแบบ raster ระหว่างการโหลด, ทำให้สามารถลบข้อมูลระดับพิกเซลได้.

**Q2: ฉันจะทำการลบข้อมูลแบบข้อความด้วยไลบรารีนี้อย่างไร?**  
A: ใช้คลาส `TextRedaction` เพื่อระบุรูปแบบข้อความและตัวเลือกการแทนที่.

**Q3: ฉันสามารถประมวลผลหลายเอกสารในรันเดียวได้หรือไม่?**  
A: ได้—ใส่ตรรกะการลบข้อมูลในลูปและใช้ `LoadOptions` ซ้ำสำหรับแต่ละไฟล์.

**Q4: เอกสารของฉันไม่โหลด—ควรตรวจสอบอะไร?**  
A: ตรวจสอบเส้นทางไฟล์, ให้แน่ใจว่าไฟล์ไม่ได้ถูกล็อก, และยืนยันว่า `LoadOptions` ถูกกำหนดค่าอย่างถูกต้อง.

**Q5: มีขีดจำกัดในการลบข้อมูลภาพขนาดใหญ่หรือไม่?**  
A: ภาพขนาดใหญ่อาจต้องการหน่วยความจำ heap เพิ่ม; พิจารณาเพิ่มการตั้งค่า JVM `-Xmx` หรือประมวลผลหน้าแยกกัน.

**Q6: groupdocs redaction รองรับไฟล์ PDF ด้วยหรือไม่?**  
A: แน่นอน—มีตัวเลือกการทำ raster ที่คล้ายกันสำหรับ PDF ทำให้สามารถลบข้อมูลในพื้นที่รูปภาพได้ในหลายรูปแบบ.

---

**Last Updated:** 2026-02-16  
**Tested With:** GroupDocs.Redaction 24.9 for Java  
**Author:** GroupDocs  

**แหล่งข้อมูล**

- **Documentation:** [เอกสาร GroupDocs.Redaction Java](https://docs.groupdocs.com/redaction/java/)  
- **API Reference:** [อ้างอิง API GroupDocs.Redaction](https://reference.groupdocs.com/redaction/java)  
- **Download:** [ดาวน์โหลด GroupDocs.Redaction](https://releases.groupdocs.com/redaction/java/)  
- **GitHub Repository:** [GroupDocs.Redaction บน GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **Free Support Forum:** [ฟอรั่มสนับสนุน GroupDocs](https://forum.groupdocs.com/c/redaction/33)  
- **Temporary License:** [ขอรับไลเซนส์ชั่วคราว](https://purchase.groupdocs.com/temporary-license/)