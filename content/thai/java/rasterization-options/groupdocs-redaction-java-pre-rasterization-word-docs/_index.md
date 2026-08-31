---
date: '2026-05-22'
description: เรียนรู้วิธีการ pre rasterize เอกสาร Word ด้วย GroupDocs Redaction Java
  เพื่อแปลงภาพ Word เป็น bitmap และทำการ redact อย่างปลอดภัย คู่มือ step‑by‑step พร้อม
  setup, usage, และ troubleshooting.
keywords:
- how to pre rasterize
- convert word images bitmap
- groupdocs redaction java
schemas:
- author: GroupDocs
  dateModified: '2026-05-22'
  description: Learn how to pre rasterize Word docs with GroupDocs Redaction Java
    to convert Word images to bitmap and securely redact them. Step‑by‑step guide
    with setup, usage, and troubleshooting.
  headline: How to pre rasterize Word docs with GroupDocs Redaction Java
  type: TechArticle
- description: Learn how to pre rasterize Word docs with GroupDocs Redaction Java
    to convert Word images to bitmap and securely redact them. Step‑by‑step guide
    with setup, usage, and troubleshooting.
  name: How to pre rasterize Word docs with GroupDocs Redaction Java
  steps:
  - name: '**Sensitive Data Redaction:** Automatically obscure personal photos, signatures,
      or scanned IDs before sharing.'
    text: '**Sensitive Data Redaction:** Automatically obscure personal photos, signatures,
      or scanned IDs before sharing.'
  - name: '**Compliance Management:** Meet industry‑specific regulations by scrubbing
      visual data from contracts or reports.'
    text: '**Compliance Management:** Meet industry‑specific regulations by scrubbing
      visual data from contracts or reports.'
  - name: '**Secure Document Sharing:** Provide partners with redacted versions while
      preserving the original layout.'
    text: '**Secure Document Sharing:** Provide partners with redacted versions while
      preserving the original layout.'
  type: HowTo
- questions:
  - answer: It converts images inside a document to raster format during loading,
      allowing pixel‑level redaction.
    question: What is pre‑rasterization in GroupDocs Redaction for Java?
  - answer: Use the `TextRedaction` class to define text patterns and replacement
      options.
    question: How do I apply text‑based redactions with this library?
  - answer: Yes—wrap the redaction logic in a loop and reuse `LoadOptions` for each
      file.
    question: Can I process multiple documents in a single run?
  - answer: Verify the file path, ensure the file isn’t locked, and confirm that `LoadOptions`
      is correctly configured.
    question: My document isn’t loading—what should I check?
  - answer: Large images may need extra heap memory; increase the JVM `-Xmx` setting
      or process pages individually.
    question: Are there limits to redacting large images?
  type: FAQPage
title: วิธีการ pre rasterize เอกสาร Word ด้วย GroupDocs Redaction Java
type: docs
url: /th/java/rasterization-options/groupdocs-redaction-java-pre-rasterization-word-docs/
weight: 1
---

# วิธีทำการพรีเรสเตอร์ไรซ์เอกสาร Word ด้วย GroupDocs Redaction Java

ในบทแนะนำนี้คุณจะ **เรียนรู้วิธีทำการพรีเรสเตอร์ไรซ์เอกสาร Word** ด้วย GroupDocs Redaction สำหรับ Java ซึ่งทำให้คุณสามารถ **แปลงภาพใน Word เป็นบิตแมพ** แล้วทำการลบข้อมูลด้วยความแม่นยำระดับพิกเซล เราจะเดินผ่านการตั้งค่าเต็มรูปแบบ อธิบายแนวคิดสำคัญของ API และแสดงขั้นตอนที่แน่นอนในการทำการลบข้อมูลในพื้นที่ภาพในสไตล์ที่เป็นกันเองและง่ายต่อการทำตาม

## คำตอบด่วน
- **การพรีเรสเตอร์ไรซ์ทำอะไร?** มันแปลงภาพที่ฝังอยู่ทั้งหมดในไฟล์ Word เป็นบิตแมพเพื่อให้เอนจินการลบข้อมูลสามารถแก้ไขพิกเซลโดยตรง.  
- **ฉันต้องการไลเซนส์หรือไม่?** การทดลองใช้ฟรีเพียงพอสำหรับการพัฒนา; จำเป็นต้องมีไลเซนส์เต็มสำหรับการใช้งานในสภาพแวดล้อมการผลิต.  
- **ต้องการเวอร์ชัน Java ใด?** Java 8 หรือใหม่กว่า (แนะนำ JDK 11+).  
- **ฉันสามารถประมวลผลหลายไฟล์ได้หรือไม่?** ได้—ใส่ตรรกะการลบข้อมูลในลูปเพื่อการประมวลผลเป็นชุด.  
- **หน่วยความจำเป็นปัญหาหรือไม่?** ภาพขนาดใหญ่อาจต้องการ heap ของ JVM ที่ใหญ่ขึ้น (เช่น `-Xmx2g`); ควรตรวจสอบการใช้หน่วยความจำระหว่างการรันแบบชุด.

## การพรีเรสเตอร์ไรซ์ใน GroupDocs Redaction คืออะไร?
`ImageAreaRedaction` มุ่งเป้าไปที่พื้นที่สี่เหลี่ยมเฉพาะของภาพเพื่อทำการลบข้อมูล  
ตัวเลือก **การพรีเรสเตอร์ไรซ์** บังคับให้ไลบรารีเรนเดอร์ภาพทุกภาพในเอกสาร Word เป็นบิตแมพเมื่อไฟล์ถูกโหลด การแปลงครั้งเดียวนี้ทำให้คลาส `ImageAreaRedaction` ทำงานกับพิกัดพิกเซลที่แม่นยำ รับประกันการลบหรือการซ่อนเนื้อหาภาพอย่างแม่นยำ การแปลงนี้ยังทำให้การดำเนินการระดับพิกเซลต่อไปมุ่งเป้าไปที่ข้อมูลภาพที่ถูกต้อง

## ทำไมต้องใช้ GroupDocs Redaction เพื่อลบภาพในเอกสาร Word?
GroupDocs Redaction ให้วิธีที่ปลอดภัยและอัตโนมัติในการลบข้อมูลภาพจากไฟล์ Word ช่วยให้องค์กรปฏิบัติตามกฎระเบียบความเป็นส่วนตัว ผสานการลบข้อมูลเข้ากับกระบวนการเอกสาร และเพิ่มประสิทธิภาพโดยทำการเรสเตอร์ไรซ์ภาพเพียงครั้งเดียวแทนการประมวลผลซ้ำหลายครั้ง รองรับรูปแบบไฟล์หลากหลายและสามารถขยายขนาดเพื่อจัดการกับเอกสารที่มีภาพจำนวนมากโดยยังคงรักษาเค้าโครงไว้
- **การปฏิบัติตามกฎระเบียบ:** ตรงตาม GDPR, HIPAA และข้อกำหนดความเป็นส่วนตัวอื่น ๆ โดยการลบข้อมูลภาพอย่างสมบูรณ์.  
- **พร้อมอัตโนมัติ:** ผสานรวมอย่างไร้รอยต่อกับ CI/CD pipeline, ระบบจัดการเอกสาร หรือไมโครเซอร์วิส.  
- **เพิ่มประสิทธิภาพ:** การเรสเตอร์ไรซ์ครั้งเดียวในขณะโหลดลดภาระการประมวลผลซ้ำโดยเฉพาะไฟล์ที่มีภาพจำนวนมาก.  
- **รองรับรูปแบบหลากหลาย:** GroupDocs Redaction รองรับ **รูปแบบเข้าและออกกว่า 70+** รวมถึง DOCX, PPTX, PDF, และประเภทภาพต่าง ๆ และสามารถประมวลผลเอกสารหลายร้อยหน้าโดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ.

## ข้อกำหนดเบื้องต้น
- **GroupDocs.Redaction 24.9** (หรือใหม่กว่า) – ให้ฟีเจอร์การพรีเรสเตอร์ไรซ์.  
- **Java Development Kit (JDK)** – เวอร์ชัน 8 หรือใหม่กว่า ติดตั้งแล้ว.  
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
หากคุณไม่ต้องการใช้ Maven ให้ดาวน์โหลด JAR ล่าสุดจากหน้าปล่อยอย่างเป็นทางการ: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

#### การรับไลเซนส์
เริ่มต้นด้วยการทดลองใช้ฟรีหรือขอไลเซนส์ชั่วคราวเพื่อประเมินผลิตภัณฑ์ สำหรับฟีเจอร์เต็มในสภาพแวดล้อมการผลิต ให้ซื้อไลเซนส์ถาวร.

## การเริ่มต้นพื้นฐาน

`Redactor` เป็นจุดเริ่มต้นหลักสำหรับการโหลดเอกสารและใช้การกระทำการลบข้อมูล ด้านล่างเป็นโค้ด Java ขั้นต่ำที่คุณต้องการเพื่อสร้างอินสแตนซ์ `Redactor` พร้อมเปิดการพรีเรสเตอร์ไรซ์ เก็บสแนปช็อตนี้ไว้; เราจะต่อยอดในขั้นตอนต่อไป.

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

## คู่มือการใช้งาน

### การทำงานของการพรีเรสเตอร์ไรซ์
โหลดเอกสารด้วย `LoadOptions` ตั้งค่าเป็น `true` แล้ว GroupDocs Redaction จะทำการแปลงภาพที่ฝังอยู่แต่ละภาพเป็นบิตแมพโดยอัตโนมัติก่อนที่การกระทำการลบข้อมูลใด ๆ จะถูกนำไปใช้ สิ่งนี้ทำให้การดำเนินการระดับพิกเซลต่อไปมุ่งเป้าไปที่ข้อมูลภาพที่ถูกต้อง ภาพที่เรสเตอร์ไรซ์จะถูกเก็บในหน่วยความจำ ทำให้เข้าถึงคำสั่งการลบข้อมูลได้อย่างรวดเร็วโดยไม่ต้องเรนเดอร์เวกเตอร์ต้นฉบับใหม่.

#### การเปิดใช้งานการพรีเรสเตอร์ไรซ์

#### ภาพรวม
`LoadOptions` กำหนดวิธีการเปิดเอกสาร รวมถึงการเปิดใช้งานการพรีเรสเตอร์ไรซ์หรือไม่ เมื่อ `LoadOptions` ถูกสร้างด้วยค่า `true` GroupDocs Redaction จะทำการเรสเตอร์ไรซ์ภาพทุกภาพในไฟล์ Word ขณะโหลด เพื่อเตรียมพร้อมสำหรับการจัดการระดับพิกเซล.

#### คำแนะนำขั้นตอนต่อขั้นตอน

**3.1 ตั้งค่า Load Options**  
สร้างอ็อบเจ็กต์ `LoadOptions` โดยตั้งค่าสถานะการเรสเตอร์ไรซ์เป็น `true`:

```java
// Set load options with pre-rasterization enabled
LoadOptions loadOptions = new LoadOptions(true);
```

**3.2 การเริ่มต้นอ็อบเจ็กต์ Redactor**  
ส่ง `loadOptions` ไปยังคอนสตรัคเตอร์ของ `Redactor` เพื่อให้เอกสารเปิดพร้อมการเรสเตอร์ไรซ์:

```java
// Initialize the Redactor object using specified file path and load options
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX", loadOptions);
```

**3.3 การใช้ Image Area Redaction**  
กำหนดพื้นที่สี่เหลี่ยม (x, y, ความกว้าง, ความสูง) ที่คุณต้องการซ่อน แล้วแทนที่ด้วยสีทึบ:

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
- **ปัญหาการเรสเตอร์ไรซ์:** ตรวจสอบให้แน่ใจว่าธง `LoadOptions` ตั้งค่าเป็น `true`; หากไม่ภาพจะยังคงเป็นเวกเตอร์และไม่สามารถลบได้.  
- **ข้อจำกัดหน่วยความจำ:** ไฟล์ Word ขนาดใหญ่ที่มีภาพความละเอียดสูงหลายภาพอาจต้องการ heap ของ JVM ที่ใหญ่ขึ้น (`-Xmx2g` หรือสูงกว่า).

## การประยุกต์ใช้งานจริง
1. **การลบข้อมูลที่ละเอียดอ่อน:** ทำให้ภาพส่วนบุคคล, ลายเซ็น, หรือบัตรประจำตัวสแกนถูกซ่อนโดยอัตโนมัติก่อนแชร์.  
2. **การจัดการการปฏิบัติตาม:** ปฏิบัติตามกฎระเบียบเฉพาะอุตสาหกรรมโดยการลบข้อมูลภาพจากสัญญาหรือรายงาน.  
3. **การแชร์เอกสารอย่างปลอดภัย:** ให้คู่ค้าดูเวอร์ชันที่ลบข้อมูลแล้วโดยยังคงรักษาเค้าโครงเดิม.  

การผสาน GroupDocs Redaction เข้ากับเวิร์กโฟลว์ที่มีอยู่ (เช่น CI/CD pipeline, API การจัดการเอกสาร) สามารถทำให้การตรวจสอบการปฏิบัติตามอัตโนมัติมากขึ้น.

## การพิจารณาประสิทธิภาพ
- **การจัดการหน่วยความจำอย่างมีประสิทธิภาพ:** จัดสรร heap เพียงพอและปิดอินสแตนซ์ `Redactor` อย่างรวดเร็ว (บล็อก `try‑with‑resources` ทำเช่นนี้โดยอัตโนมัติ).  
- **การเพิ่มประสิทธิภาพทรัพยากร:** ใช้ `LoadOptions` อย่างชาญฉลาด—เปิดการเรสเตอร์ไรซ์เฉพาะเมื่อจำเป็นต้องแก้ไขพื้นที่ภาพ; หากไม่จำเป็นให้ปิดเพื่อการลบข้อความที่เร็วขึ้น.  

การปฏิบัติตามแนวทางเหล่านี้ช่วยให้การประมวลผลตอบสนองได้ดีแม้กับไฟล์ Word ขนาดใหญ่ที่มีภาพจำนวนมาก.

## สรุป
คุณได้เรียนรู้ **วิธีทำการพรีเรสเตอร์ไรซ์เอกสาร Word ด้วย GroupDocs Redaction สำหรับ Java** และทำการลบข้อมูลในพื้นที่ภาพอย่างแม่นยำ ความสามารถนี้ทำให้คุณสามารถปกป้องเนื้อหาภาพ, ปฏิบัติตามกฎระเบียบ, และทำให้การแจกจ่ายเอกสารที่ปลอดภัยเป็นเรื่องง่าย.  

**ขั้นตอนต่อไป:** สำรวจประเภทการลบข้อมูลเพิ่มเติม (ข้อความ, เมทาดาต้า), ทดลองประมวลผลเป็นชุด, หรือห่อหุ้มไลบรารีในบริการ RESTful เพื่อการลบข้อมูลตามความต้องการ.

## คำถามที่พบบ่อย

**Q: การพรีเรสเตอร์ไรซ์ใน GroupDocs Redaction สำหรับ Java คืออะไร?**  
A: มันแปลงภาพภายในเอกสารเป็นรูปแบบเรสเตอร์ในระหว่างการโหลด, ทำให้สามารถลบข้อมูลระดับพิกเซลได้.

**Q: ฉันจะใช้การลบข้อมูลแบบข้อความด้วยไลบรารีนี้อย่างไร?**  
A: ใช้คลาส `TextRedaction` เพื่อกำหนดรูปแบบข้อความและตัวเลือกการแทนที่.

**Q: ฉันสามารถประมวลผลหลายเอกสารในรันเดียวได้หรือไม่?**  
A: ได้—ใส่ตรรกะการลบข้อมูลในลูปและใช้ `LoadOptions` ซ้ำสำหรับแต่ละไฟล์.

**Q: เอกสารของฉันไม่โหลด—ควรตรวจสอบอะไร?**  
A: ตรวจสอบเส้นทางไฟล์, ให้แน่ใจว่าไฟล์ไม่ถูกล็อก, และยืนยันว่า `LoadOptions` ถูกกำหนดค่าอย่างถูกต้อง.

**Q: มีขีดจำกัดในการลบข้อมูลภาพขนาดใหญ่หรือไม่?**  
A: ภาพขนาดใหญ่อาจต้องการหน่วยความจำ heap เพิ่ม; เพิ่มการตั้งค่า JVM `-Xmx` หรือประมวลผลหน้าแยกกัน.

**Q: GroupDocs Redaction รองรับไฟล์ PDF ด้วยหรือไม่?**  
A: แน่นอน—มีตัวเลือกการเรสเตอร์ไรซ์ที่คล้ายกันสำหรับ PDF ทำให้สามารถลบข้อมูลในพื้นที่ภาพได้ในหลายรูปแบบ.

---

**อัปเดตล่าสุด:** 2026-05-22  
**ทดสอบด้วย:** GroupDocs.Redaction 24.9 for Java  
**ผู้เขียน:** GroupDocs  

**แหล่งข้อมูล**
- **เอกสาร:** [GroupDocs.Redaction Java Documentation](https://docs.groupdocs.com/redaction/java/)  
- **อ้างอิง API:** [GroupDocs.Redaction API Reference](https://reference.groupdocs.com/redaction/java)  
- **ดาวน์โหลด:** [GroupDocs.Redaction Downloads](https://releases.groupdocs.com/redaction/java/)  
- **ที่เก็บ GitHub:** [GroupDocs.Redaction on GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **ฟอรั่มสนับสนุนฟรี:** [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33)  
- **ไลเซนส์ชั่วคราว:** [Request a Temporary License](https://purchase.groupdocs.com/temporary-license/)

## บทแนะนำที่เกี่ยวข้อง
- [วิธีแปลง DOCX เป็นภาพและลบข้อมูลเอกสาร Word ด้วย GroupDocs Redaction Java](/redaction/java/document-saving/groupdocs-redaction-java-rasterize-word-docs/)  
- [วิธีลบภาพในเอกสาร Word ด้วย GroupDocs.Redaction for Java – คู่มือฉบับสมบูรณ์](/redaction/java/image-redaction/redact-images-word-docs-groupdocs-redaction-java/)  
- [บทแนะนำตัวเลือกการเรสเตอร์ไรซ์สำหรับ GroupDocs.Redaction Java](/redaction/java/rasterization-options/)