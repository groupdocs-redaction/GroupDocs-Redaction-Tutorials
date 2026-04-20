---
date: '2026-04-20'
description: เรียนรู้วิธีทำการลบข้อมูลบนหน้า PDF หน้าสุดท้ายโดยใช้ GroupDocs.Redaction
  สำหรับ Java, แทนที่ข้อความใน PDF ด้วย Java และซ่อนข้อมูลที่เป็นความลับใน PDF อย่างมีประสิทธิภาพ.
keywords:
- redact last page pdf
- replace text pdf java
- hide sensitive data pdf
title: ลบข้อมูลในหน้าสุดท้ายของ PDF ด้วย GroupDocs.Redaction สำหรับ Java
type: docs
url: /th/java/page-redaction/java-pdf-redaction-groupdocs-last-page-focus/
weight: 1
---

# ลบข้อมูลส่วนสุดท้ายของ PDF ด้วย GroupDocs.Redaction สำหรับ Java

## คำตอบอย่างรวดเร็ว
- **เป้าหมายหลักคืออะไร?** เพื่อลบข้อมูลส่วนสุดท้ายของ PDF และพื้นที่เฉพาะภายในนั้น.  
- **ไลบรารีที่ใช้คืออะไร?** GroupDocs.Redaction for Java.  
- **ต้องการไลเซนส์หรือไม่?** ไลเซนส์แบบทดลองหรือชั่วคราวใช้ได้สำหรับการทดสอบ; จำเป็นต้องมีไลเซนส์เต็มสำหรับการใช้งานจริง.  
- **ต้องการเวอร์ชัน Java ใด?** Java 8 หรือสูงกว่า พร้อมการสนับสนุน Maven.  
- **สามารถกำหนดเป้าหมายหน้าอื่นได้หรือไม่?** ได้, สามารถปรับฟิลเตอร์เดียวกันสำหรับช่วงหน้าใดก็ได้.

## การลบข้อมูลใน PDF คืออะไร?
การลบข้อมูลหมายถึงการลบหรือทำให้เนื้อหาใน PDF หายไปอย่างถาวรเพื่อไม่ให้สามารถกู้คืนได้ เมื่อคุณ **redact last page pdf** คุณจะมั่นใจว่าข้อมูลที่เป็นความลับใด ๆ บนหน้าสุดท้ายจะถูกซ่อนอย่างสมบูรณ์.

## ทำไมต้องใช้ GroupDocs.Redaction สำหรับ Java?
GroupDocs.Redaction มีชุดฟิลเตอร์ที่หลากหลาย—ช่วงหน้า, พื้นที่, และข้อความ—ที่ช่วยให้คุณควบคุมการลบได้อย่างแม่นยำ มันมีประโยชน์เป็นพิเศษสำหรับ:
- **Replacing text pdf java** สไตล์โดยไม่เปลี่ยนแปลงส่วนอื่นของเอกสาร.  
- **Hiding sensitive data pdf** เช่น ตัวระบุส่วนบุคคล, ตัวเลขทางการเงิน, หรือข้อกำหนดทางกฎหมาย.  
- การทำงานอัตโนมัติในการตรวจสอบการปฏิบัติตามกฎระเบียบในชุดเอกสารขนาดใหญ่.

## ข้อกำหนดเบื้องต้น
- **Java Development Kit (JDK) 8+** ติดตั้งแล้ว.  
- **Maven** สำหรับการจัดการ dependencies.  
- เข้าถึงไลเซนส์ **GroupDocs.Redaction** (ทดลอง, ชั่วคราว, หรือซื้อแล้ว).  

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
หากคุณไม่ต้องการใช้ Maven, ดาวน์โหลด JAR เวอร์ชันล่าสุดจากเว็บไซต์อย่างเป็นทางการ: [GroupDocs.Redaction for Java releases](httpshttps://releases.groupdocs.com/redaction/java/).

#### ขั้นตอนการรับไลเซนส์
- **Free Trial:** ทดสอบคุณสมบัติทั้งหมดโดยไม่มีข้อผูกมัด.  
- **Temporary License:** ใช้สำหรับโครงการระยะสั้นหรือการประเมินผล.  
- **Purchase:** ปลดล็อกการใช้งานไม่จำกัดและรับการสนับสนุนระดับพรีเมียม.

## การเริ่มต้นพื้นฐาน
แรกเริ่ม, สร้างอินสแตนซ์ `Redactor` ที่ชี้ไปยังไฟล์ PDF ของคุณ:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_PDF");
```

อินสแตนซ์นี้เป็นจุดเริ่มต้นสำหรับการดำเนินการลบข้อมูลทั้งหมด.

## วิธีลบข้อมูลส่วนสุดท้ายของ PDF – คู่มือขั้นตอนโดยละเอียด

### ฟีเจอร์ 1: การลบข้อมูลในพื้นที่เฉพาะบนหน้าสุดท้าย

#### ขั้นตอนที่ 1: โหลดเอกสาร PDF
```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_PDF");
```

#### ขั้นตอนที่ 2: ดึงข้อมูลหน้า
```java
IDocumentInfo info = redactor.getDocumentInfo();
PageInfo lastPage = info.getPages().get(info.getPageCount() - 1);
```
การรู้ขนาดของหน้าสุดท้ายช่วยให้คุณกำหนดพิกัดได้อย่างแม่นยำ.

#### ขั้นตอนที่ 3: กำหนดตัวเลือกการแทนที่
```java
ReplacementOptions options = new ReplacementOptions("[secret]");
```
ที่นี่เราเลือกข้อความตัวแทนที่จะใช้แทนเนื้อหาที่ถูกลบ.

#### ขั้นตอนที่ 4: ตั้งค่าฟิลเตอร์สำหรับการลบข้อมูลที่กำหนดเป้าหมาย
```java
options.setFilters(new RedactionFilter[] {
    new PageRangeFilter(PageSeekOrigin.End, 0, 1),
    new PageAreaFilter(
        new java.awt.Point(0, lastPage.getHeight() / 2),
        new java.awt.Dimension(lastPage.getWidth(), lastPage.getHeight() / 2)
    )
});
```
- `PageRangeFilter` เลือก **last page**.  
- `PageAreaFilter` จำกัดการทำงานไว้ที่ครึ่งล่างของหน้านั้น.

#### ขั้นตอนที่ 5: ใช้การลบข้อมูล (replace text pdf java)
```java
RedactorChangeLog result = redactor.apply(new ExactPhraseRedaction("bibliography", false, options));
```
วลี “bibliography” จะถูกแทนที่ด้วย “[secret]” เฉพาะในพื้นที่ที่กำหนด.

#### ขั้นตอนที่ 6: ตรวจสอบความสำเร็จและบันทึก
```java
if (result.getStatus() != RedactionStatus.Failed) {
    redactor.save("YOUR_OUTPUT_DIRECTORY/redacted_output.pdf");
}
```
ตรวจสอบสถานะก่อนเขียนไฟล์ผลลัพธ์เสมอ.

#### ขั้นตอนที่ 7: ทำความสะอาดทรัพยากร
```java
redactor.close();
```
การปิด `Redactor` จะปลดปล่อยหน่วยความจำและตัวจัดการไฟล์.

### ฟีเจอร์ 2: การกรองช่วงหน้าสำหรับการลบข้อมูล

#### ขั้นตอนที่ 1: โหลดเอกสาร PDF
```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_PDF");
```

#### ขั้นตอนที่ 2: เข้าถึงข้อมูลเอกสาร
```java
IDocumentInfo info = redactor.getDocumentInfo();
```

#### ขั้นตอนที่ 3: สร้างฟิลเตอร์ช่วงหน้า (hide sensitive data pdf)
```java
PageRangeFilter pageRangeFilter = new PageRangeFilter(PageSeekOrigin.End, 0, 1);
```
ฟิลเตอร์นี้แยกหน้าสุดท้ายออก, ทำให้คุณสามารถใช้ตรรกะการลบข้อมูลใด ๆ ที่ต้องการได้.

### ฟีเจอร์ 3: การลบข้อมูลตามพื้นที่บนหน้า PDF

#### ขั้นตอนที่ 1: โหลดเอกสาร PDF
```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_PDF");
```

#### ขั้นตอนที่ 2: รับรายละเอียดหน้า
```java
IDocumentInfo info = redactor.getDocumentInfo();
PageInfo lastPage = info.getPages().get(info.getPageCount() - 1);
```

#### ขั้นตอนที่ 3: กำหนดฟิลเตอร์พื้นที่ (hide sensitive data pdf)
```java
PageAreaFilter areaFilter = new PageAreaFilter(
    new java.awt.Point(0, lastPage.getHeight() / 2),
    new java.awt.Dimension(lastPage.getWidth(), lastPage.getHeight() / 2)
);
```
ฟิลเตอร์นี้มุ่งเป้าไปที่ครึ่งล่างของหน้าสุดท้าย—เหมาะสำหรับการลบส่วนท้ายหรือลายเซ็น.

#### ขั้นตอนที่ 4: ปล่อยทรัพยากร
```java
redactor.close();
```

## การประยุกต์ใช้งานจริง
- **Legal Documents:** ลบชื่อคลายเอนท์หรือหมายเลขคดีบนหน้าสุดท้ายก่อนแชร์.  
- **Financial Reports:** ซ่อนหมายเลขบัญชีหรือสรุปข้อมูลที่เป็นความลับ.  
- **Healthcare Records:** ลบตัวระบุผู้ป่วยเพื่อให้สอดคล้องกับ HIPAA.  
- **Pre‑Release Drafts:** ปกปิดส่วนที่ยังอยู่ระหว่างการตรวจสอบ.

## เคล็ดลับประสิทธิภาพ
- **Reuse the `Redactor`** เมื่อประมวลผลหลายไฟล์ PDF ในชุด.  
- **Close the object promptly** เพื่อหลีกเลี่ยงการรั่วไหลของหน่วยความจำ, โดยเฉพาะไฟล์ขนาดใหญ่.  
- **Test on a sample** ก่อนรันบนเอกสารจริงเพื่อยืนยันพิกัดฟิลเตอร์.

## คำถามที่พบบ่อย

**Q: Can I redact multiple pages at once?**  
A: ใช่. ปรับพารามิเตอร์ของ `PageRangeFilter` เพื่อรวมช่วงใดก็ได้ (เช่น `new PageRangeFilter(1, 5)` สำหรับหน้า 1‑5).

**Q: Does the library support password‑protected PDFs?**  
A: แน่นอน. ส่งรหัสผ่านไปยังคอนสตรัคเตอร์ของ `Redactor` เพื่อเปิดไฟล์ที่เข้ารหัส.

**Q: How do I change the redaction color or overlay?**  
A: ใช้ `ReplacementOptions` เพื่อระบุภาพ, สี, หรือข้อความโอเวอร์เลย์ที่กำหนดเอง.

**Q: Is the redaction permanent?**  
A: ใช่. เนื้อหาที่ถูกลบจะไม่ถูกเก็บไว้ในไฟล์ PDF ผลลัพธ์, ทำให้ไม่สามารถกู้คืนได้.

**Q: What if I need to redact based on regex patterns?**  
A: GroupDocs.Redaction มี `RegexRedaction` ที่ทำงานคล้ายกับ `ExactPhraseRedaction`.

**Last Updated:** 2026-04-20  
**Tested With:** GroupDocs.Redaction 24.9 for Java  
**Author:** GroupDocs