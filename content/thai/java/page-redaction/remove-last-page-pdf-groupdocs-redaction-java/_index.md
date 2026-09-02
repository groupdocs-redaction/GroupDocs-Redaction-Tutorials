---
date: '2026-06-01'
description: เรียนรู้วิธีลบหน้าสุดท้ายของ PDF ด้วย GroupDocs.Redaction สำหรับ Java.
  คู่มือทีละขั้นตอน, ตัวอย่างโค้ด, และแนวปฏิบัติที่ดีที่สุดสำหรับ pdf page count java
  และ remove final pdf page.
keywords:
- delete last pdf page
- pdf page count java
- remove final pdf page
schemas:
- author: GroupDocs
  dateModified: '2026-06-01'
  description: Learn how to delete the last PDF page with GroupDocs.Redaction for
    Java. Step‑by‑step guide, code snippets, and best practices for pdf page count
    java and remove final pdf page.
  headline: How to Delete the Last PDF Page Using GroupDocs.Redaction in Java
  type: TechArticle
- description: Learn how to delete the last PDF page with GroupDocs.Redaction for
    Java. Step‑by‑step guide, code snippets, and best practices for pdf page count
    java and remove final pdf page.
  name: How to Delete the Last PDF Page Using GroupDocs.Redaction in Java
  steps:
  - name: '**Maven Setup**'
    text: '**Maven Setup**'
  - name: '**Direct Download**'
    text: '**Direct Download**'
  - name: '**Maven Configuration**'
    text: '**Maven Configuration**'
  - name: '**Direct Download Setup**'
    text: '**Direct Download Setup**'
  - name: '**Pre‑Publication Editing** – Remove draft or placeholder pages before
      releasing a report.'
    text: '**Pre‑Publication Editing** – Remove draft or placeholder pages before
      releasing a report.'
  - name: '**Archival Optimization** – Trim trailing blank pages to reduce storage
      costs for large document archives.'
    text: '**Archival Optimization** – Trim trailing blank pages to reduce storage
      costs for large document archives.'
  - name: '**Confidentiality** – Strip out a cover page that contains sensitive metadata
      before distribution.'
    text: '**Confidentiality** – Strip out a cover page that contains sensitive metadata
      before distribution.'
  - name: '**Automated Report Generation** – Generate PDFs programmatically and drop
      the automatically added summary page.'
    text: '**Automated Report Generation** – Generate PDFs programmatically and drop
      the automatically added summary page.'
  - name: '**Workflow Integration** – Embed the deletion step into CI/CD pipelines
      that handle document generation.'
    text: '**Workflow Integration** – Embed the deletion step into CI/CD pipelines
      that handle document generation.'
  type: HowTo
- questions:
  - answer: It provides a programmatic way to redact, edit, and manipulate sensitive
      content in PDFs and many other document formats without needing Microsoft Office
      installed.
    question: What is the primary use case for GroupDocs.Redaction?
  - answer: Yes—use `RemovePageRedaction` with a range (e.g., `new RemovePageRedaction(5,
      2)`) to delete two pages starting from page 5.
    question: Can I delete multiple pages at once?
  - answer: Absolutely. Pass the password to the `Redactor` constructor or set it
      via `redactor.setPassword("yourPassword")` before performing any operations.
    question: Does the library support password‑protected PDFs?
  - answer: It streams pages, allowing you to process PDFs with hundreds of pages
      while keeping memory usage low; typical processing of a 500‑page file uses under
      200 MB of RAM.
    question: How does GroupDocs.Redaction handle large files?
  - answer: Visit the [GroupDocs website](https://purchase.groupdocs.com/temporary-license/)
      to request a trial license that unlocks all API features for 30 days.
    question: Where can I obtain a temporary license for testing?
  type: FAQPage
title: วิธีลบหน้าสุดท้ายของ PDF ด้วย GroupDocs.Redaction ใน Java
type: docs
url: /th/java/page-redaction/remove-last-page-pdf-groupdocs-redaction-java/
weight: 1
---

# วิธีลบหน้าสุดท้ายของ PDF ด้วย GroupDocs.Redaction ใน Java

การลบ **หน้าสุดท้ายของ PDF** ที่ไม่ต้องการออกจากเอกสารอาจเป็นกระบวนการทำมือที่น่าเบื่อ โดยเฉพาะเมื่อคุณต้องจัดการกับหลายสิบไฟล์ในสายงานอัตโนมัติ ด้วย **GroupDocs.Redaction for Java** คุณสามารถลบหน้าสุดท้ายของ PDF ได้ด้วยเพียงไม่กี่บรรทัดของโค้ด รักษาส่วนที่เหลือของเอกสารให้คงเดิม และคงความสามารถในการแก้ไขเมื่อจำเป็น บทแนะนำนี้จะพาคุณผ่านทุกอย่างที่ต้องรู้—เหตุผลที่การดำเนินการนี้สำคัญ การเรียกใช้ API อย่างแม่นยำ และเคล็ดลับปฏิบัติเพื่อหลีกเลี่ยงข้อผิดพลาดทั่วไป.

## คำตอบอย่างรวดเร็ว
- **ไลบรารีใดที่สามารถลบหน้าสุดท้ายของ PDF ได้?** GroupDocs.Redaction for Java.  
- **ฉันต้องการไลเซนส์หรือไม่?** การทดลองใช้งานทำงานสำหรับการทดสอบพื้นฐาน; จำเป็นต้องมีไลเซนส์เต็มสำหรับการใช้งานในผลิตภัณฑ์.  
- **ฉันสามารถตรวจสอบจำนวนหน้าของ PDF ก่อนการลบได้หรือไม่?** ได้—ใช้ `redactor.getDocumentInfo().getPageCount()`.  
- **PDF ดั้งเดิมยังสามารถแก้ไขได้หลังจากลบหรือไม่?** ตั้งค่า `saveOptions.setRasterizeToPDF(false)` เพื่อคงความสามารถในการแก้ไข.  
- **เวอร์ชัน Java ที่รองรับคืออะไร?** JDK 8 หรือใหม่กว่า.

## “delete last pdf page” คืออะไร?
*การลบหน้าสุดท้ายของ PDF* หมายถึงการลบหน้าสุดท้ายของไฟล์ PDF อย่างโปรแกรมเมติกโดยคงเนื้อหาที่เหลือ, เมตาดาต้า, และความสามารถในการแก้ไขตามต้องการ การดำเนินการนี้มีประโยชน์เมื่อหน้าสุดท้ายมีโน้ตร่าง, ตัวแทนชั่วคราว, หรือข้อมูลที่เป็นความลับที่ไม่ควรอยู่ในเวอร์ชันสุดท้าย การลบโดยโปรแกรมช่วยหลีกเลี่ยงข้อผิดพลาดจากการทำมือ, เร่งความเร็วการประมวลผลแบบแบตช์, และทำให้ขนาดไฟล์เหมาะสมสำหรับการจัดเก็บและการส่งต่อ.

## ทำไมต้องใช้ GroupDocs.Redaction สำหรับงานนี้?
GroupDocs.Redaction รองรับ **รูปแบบอินพุตและเอาต์พุตกว่า 50 ประเภท**, สามารถประมวลผล **PDF หลายร้อยหน้า** โดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ, และมี API `RemovePageRedaction` เฉพาะที่รับประกันการลบหน้าที่แม่นยำพร้อมการตรวจสอบความปลอดภัยในตัว นอกจากนี้ไลบรารียังมีระบบไลเซนส์ที่แข็งแรง, เอกสารประกอบที่ครอบคลุม, และความสามารถในการทำให้ PDF ค้นหาได้และแก้ไขได้หลังการลบข้อมูล, ทำให้เป็นตัวเลือกที่เชื่อถือได้สำหรับสายงานเอกสารระดับองค์กร.

## ข้อกำหนดเบื้องต้น
ก่อนที่คุณจะเริ่ม, ตรวจสอบว่าคุณมีสิ่งต่อไปนี้:

- **Java Development Kit (JDK) 8 หรือใหม่กว่า** ที่ติดตั้งบนเครื่องของคุณ.
- **Maven** (หรือความสามารถในการเพิ่มไฟล์ JAR ด้วยตนเอง) สำหรับการจัดการ dependencies.
- ไลเซนส์ **GroupDocs.Redaction** (การทดลองใช้งานก็พอสำหรับการทดลอง).
- ความคุ้นเคยพื้นฐานกับไวยากรณ์ Java และโครงสร้างโปรเจกต์.

### ไลบรารีและ dependencies ที่จำเป็น
1. **Maven Setup**  
   - ตรวจสอบว่า Maven ได้ติดตั้งบนเครื่องของคุณแล้ว.  
   - เพิ่มการกำหนดค่าต่อไปนี้ในไฟล์ `pom.xml` ของคุณเพื่อรวม GroupDocs.Redaction:

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

สำหรับการใช้งาน API อย่างละเอียดดูที่ [GroupDocs Redaction Java Documentation](https://docs.groupdocs.com/redaction/java/) และ [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java). ตรวจสอบ [Latest Releases](https://releases.groupdocs.com/redaction/java/) เพื่อดูเวอร์ชันใหม่ ๆ.

2. **Direct Download**  
   - หรืออีกทางเลือกหนึ่ง, ดาวน์โหลดเวอร์ชันล่าสุดจาก [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).  
   - คุณยังสามารถดูซอร์สโค้ดได้ที่ [GroupDocs Redaction for Java](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java) และถามคำถามใน [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33).

### ข้อกำหนดการตั้งค่าสภาพแวดล้อม
- ตรวจสอบว่า `JAVA_HOME` ชี้ไปยังการติดตั้ง JDK 8+.
- IDE ของคุณ (IntelliJ, Eclipse, VS Code) ควรตั้งค่าให้ใช้เวอร์ชัน JDK เดียวกัน.

### ความรู้เบื้องต้นที่จำเป็น
- แนวคิดพื้นฐานการเขียนโปรแกรม Java (คลาส, อ็อบเจ็กต์, การจัดการข้อยกเว้น).
- การเข้าใจ `pom.xml` ของ Maven เป็นประโยชน์แต่ไม่จำเป็นหากคุณต้องการใช้วิธีการดาวน์โหลด JAR โดยตรง.

## การตั้งค่า GroupDocs.Redaction สำหรับ Java
การตั้งค่าโปรเจกต์ของคุณเพื่อใช้ GroupDocs.Redaction เกี่ยวข้องกับการเพิ่มไลบรารีและกำหนดค่าไลเซนส์.

### ข้อมูลการติดตั้ง
1. **Maven Configuration**  
   - เพิ่ม repository และ snippet ของ dependency จากส่วนก่อนหน้าไปยังไฟล์ `pom.xml` ของคุณ.

2. **Direct Download Setup**  
   - ดาวน์โหลดไฟล์ JAR จาก [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).  
   - เพิ่มไฟล์ JAR ไปยังเส้นทางการสร้างของโปรเจกต์ของคุณ (เช่น โฟลเดอร์ `libs/`).

### การรับไลเซนส์
- GroupDocs มีการทดลองใช้งานฟรีพร้อมฟังก์ชันจำกัด.  
- รับไลเซนส์ชั่วคราวหรือซื้อไลเซนส์เต็มที่ [GroupDocs website](https://purchase.groupdocs.com/temporary-license/).  
- สำหรับรายละเอียดไลเซนส์ดูที่ [GroupDocs' licensing page](https://purchase.groupdocs.com/temporary-license/) หรือโดยตรงที่ [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license/).

## คู่มือการใช้งาน
เมื่อทุกอย่างพร้อมแล้ว, เรามา Implement ฟีเจอร์ **delete the last PDF page** ด้วย GroupDocs.Redaction.

### ฉันจะลบหน้าสุดท้ายของ PDF ด้วย GroupDocs.Redaction อย่างไร?
โหลด PDF ด้วยอินสแตนซ์ `Redactor`, ตรวจสอบว่าเอกสารมีอย่างน้อยหนึ่งหน้า, ใช้ `RemovePageRedaction` เพื่อลบหน้าสุดท้าย, ตั้งค่า `SaveOptions`, และสุดท้ายบันทึกไฟล์ที่แก้ไขแล้ว กระบวนการทั้งหมดนี้สามารถทำได้ในไม่เกินสิบบรรทัดของโค้ด Java.

#### การดำเนินการแบบขั้นตอน

##### **ขั้นตอน 1: เริ่มต้น Redactor**
`Redactor` คือคลาสหลักที่แทนเอกสาร PDF และให้เมธอดสำหรับการลบข้อมูลและการจัดการหน้า.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/multipage.pdf");
```

บรรทัดนี้เปิด PDF และเตรียมพร้อมสำหรับการดำเนินการต่อ.

##### **ขั้นตอน 2: ตรวจสอบจำนวนหน้าของ PDF**
`DocumentInfo.getPageCount()` คืนค่าจำนวนหน้าทั้งหมด, ช่วยให้คุณตรวจสอบอย่างปลอดภัยว่ามีหน้าสุดท้ายก่อนทำการลบ.

```java
if (redactor.getDocumentInfo().getPageCount() >= 1) {
    // Proceed with removal if true
}
```

หากจำนวนเป็นศูนย์, คุณควรยกเลิกการดำเนินการเพื่อหลีกเลี่ยง `IndexOutOfBoundsException`.

##### **ขั้นตอน 3: ใช้ RemovePageRedaction**
`RemovePageRedaction` คือคลาสที่ลบหน้าตามดัชนีเริ่มจากศูนย์หรืออ้างอิงต้นกำเนิด.

```java
redactor.apply(new RemovePageRedaction(PageSeekOrigin.End, -1));
```

- `PageSeekOrigin.End` ระบุว่าดัชนีหน้าถูกนับจากส่วนท้ายของเอกสาร.  
- ค่าออฟเซ็ต `-1` จะลบหน้าเดียวเท่านั้น—หน้าสุดท้าย.

##### **ขั้นตอน 4: ตั้งค่า SaveOptions**
`SaveOptions` ควบคุมวิธีการเขียน PDF ที่แก้ไขลงดิสก์และให้คุณคงความสามารถในการแก้ไข.

```java
SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true); // Adds a suffix to the filename
saveOptions.setRasterizeToPDF(false); // Retains PDF editability
```

คุณยังสามารถเพิ่ม suffix ให้กับชื่อไฟล์ผลลัพธ์ (เช่น `_trimmed`) เพื่อหลีกเลี่ยงการเขียนทับไฟล์ต้นฉบับ.

##### **ขั้นตอน 5: บันทึกเอกสารที่แก้ไข**
บันทึกการเปลี่ยนแปลงโดยเรียก `redactor.save(outputPath, saveOptions)`. คำสั่งนี้จะสร้าง PDF ใหม่ที่ไม่มีหน้าสุดท้ายแล้ว.

```java
redactor.save(saveOptions);
```

##### **ขั้นตอน 6: ปิดทรัพยากร**
ควรปิดอินสแตนซ์ `Redactor` เสมอเพื่อปลดปล่อยทรัพยากรเนทีฟและหลีกเลี่ยงการรั่วของหน่วยความจำ.

```java
finally {
    redactor.close();
}
```

#### เคล็ดลับการแก้ไขปัญหา
- **เส้นทางไฟล์ไม่ถูกต้อง** – ตรวจสอบให้แน่ใจว่าเส้นทาง PDF อินพุตเป็นแบบ absolute หรือ relative อย่างถูกต้องต่อไดเรกทอรีทำงานของคุณ.  
- **เอกสารศูนย์หน้า** – การตรวจสอบจำนวนหน้าช่วยป้องกันข้อผิดพลาดขณะรัน; หากคืนค่า `0`, ให้บันทึกคำเตือนและข้ามขั้นตอนการลบ.  
- **ข้อผิดพลาดไลเซนส์** – ตรวจสอบว่าไฟล์ไลเซนส์อยู่ใน classpath หรือระบุผ่าน `License.setLicense("path/to/license")`.

## การประยุกต์ใช้งานจริง
การลบหน้าสุดท้ายมีประโยชน์ในหลายสถานการณ์จริง:

1. **Pre‑Publication Editing** – ลบหน้าแบบร่างหรือ placeholder ก่อนเผยแพร่รายงาน.  
2. **Archival Optimization** – ตัดหน้าว่างท้ายเพื่อลดค่าใช้จ่ายการจัดเก็บสำหรับคลังเอกสารขนาดใหญ่.  
3. **Confidentiality** – ลบหน้าปกที่มีเมตาดาต้าซึ่งเป็นข้อมูลลับก่อนการแจกจ่าย.  
4. **Automated Report Generation** – สร้าง PDF ด้วยโปรแกรมและลบหน้าสรุปที่เพิ่มโดยอัตโนมัติ.  
5. **Workflow Integration** – ฝังขั้นตอนการลบหน้าเข้าไปใน CI/CD pipeline ที่จัดการการสร้างเอกสาร.

## ข้อควรพิจารณาด้านประสิทธิภาพ
เมื่อประมวลผล PDF ขนาดใหญ่ด้วย GroupDocs.Redaction, ควรคำนึงถึงเคล็ดลับต่อไปนี้:

- **Memory Management** – ปิด `Redactor` อย่างรวดเร็ว; ไลบรารีสตรีมหน้าต่างแทนการโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ.  
- **Rasterization** – ปิดการแปลงเป็น raster (`setRasterizeToPDF(false)`) หากต้องการให้ผลลัพธ์ยังคงค้นหาและแก้ไขได้.  
- **JVM Heap** – สำหรับ PDF ที่ใหญ่กว่า 200 MB, จัดสรร heap อย่างน้อย **2 GB** (`-Xmx2g`) เพื่อหลีกเลี่ยง `OutOfMemoryError`.  
- **Batch Processing** – ใช้ `Redactor` อินสแตนซ์เดียวสำหรับหลายไฟล์เมื่อเป็นไปได้ เพื่อลดค่าใช้จ่ายการเริ่มต้น.  
- ตรวจสอบ [Latest Releases](https://releases.groupdocs.com/redaction/java/) สำหรับอัปเดตที่เกี่ยวกับประสิทธิภาพ.

## สรุป
คุณมีโซลูชันที่ครบถ้วนและพร้อมใช้งานในผลิตภัณฑ์สำหรับ **deleting the last PDF page** ด้วย GroupDocs.Redaction ใน Java แล้ว โดยทำตามขั้นตอนข้างต้น คุณสามารถรวมความสามารถนี้เข้าไปในบริการแบ็กเอนด์, งานแบตช์, หรือแอปพลิเคชันเดสก์ท็อปใด ๆ เพื่อให้ได้ PDF ที่สะอาดและขนาดเหมาะสมทุกครั้ง.  
ต่อไป, สำรวจฟีเจอร์การลบข้อมูลอื่น ๆ เช่น การลบข้อความ, การลบรูปภาพ, และการทำความสะอาดเมตาดาต้า เพื่อสร้าง pipeline ความเป็นส่วนตัวของเอกสารที่ครบถ้วน.

## คำถามที่พบบ่อย

**Q: การใช้งานหลักของ GroupDocs.Redaction คืออะไร?**  
A: มันให้วิธีการโปรแกรมเมติกในการลบข้อมูล, แก้ไข, และจัดการเนื้อหาที่เป็นความลับใน PDF และรูปแบบเอกสารอื่น ๆ มากมายโดยไม่ต้องติดตั้ง Microsoft Office.

**Q: ฉันสามารถลบหลายหน้าพร้อมกันได้หรือไม่?**  
A: ใช่—ใช้ `RemovePageRedaction` พร้อมช่วง (เช่น `new RemovePageRedaction(5, 2)`) เพื่อลบสองหน้าตั้งแต่หน้า 5.

**Q: ไลบรารีสนับสนุน PDF ที่มีการป้องกันด้วยรหัสผ่านหรือไม่?**  
A: แน่นอน. ส่งรหัสผ่านไปยังคอนสตรัคเตอร์ `Redactor` หรือกำหนดผ่าน `redactor.setPassword("yourPassword")` ก่อนทำการใด ๆ.

**Q: GroupDocs.Redaction จัดการไฟล์ขนาดใหญ่อย่างไร?**  
A: มันสตรีมหน้าต่าง, ทำให้คุณประมวลผล PDF หลายร้อยหน้าโดยใช้หน่วยความจำน้อย; การประมวลผลไฟล์ 500 หน้าโดยทั่วไปใช้ RAM ต่ำกว่า 200 MB.

**Q: ฉันสามารถขอไลเซนส์ชั่วคราวสำหรับการทดสอบได้จากที่ไหน?**  
A: เยี่ยมชม [GroupDocs website](https://purchase.groupdocs.com/temporary-license/) เพื่อขอไลเซนส์ทดลองที่เปิดใช้งานฟีเจอร์ API ทั้งหมดเป็นเวลา 30 วัน.

---
**อัปเดตล่าสุด:** 2026-06-01  
**ทดสอบด้วย:** GroupDocs.Redaction 24.9 for Java  
**ผู้เขียน:** GroupDocs  

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

## บทเรียนที่เกี่ยวข้อง

- [การลบช่วงหน้าของ PDF อย่างมีประสิทธิภาพด้วย GroupDocs.Redaction ใน Java](/redaction/java/page-redaction/java-pdf-page-range-deletion-groupdocs-redaction/)
- [วิธีดูตัวอย่างหน้าโดยใช้ GroupDocs.Redaction Java – คู่มือฉบับสมบูรณ์](/redaction/java/document-loading/load-preview-document-pages-groupdocs-redaction-java/)
- [วิธีลบข้อมูล PDF ด้วย GroupDocs.Redaction สำหรับ Java - คู่มือขั้นตอนต่อขั้นตอน](/redaction/java/advanced-redaction/master-redaction-groupdocs-java-guide/)