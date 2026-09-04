---
date: 2026-08-04
description: เรียนรู้วิธีกรองข้อมูลสเปรดชีต java และทำการลบข้อมูลอย่างปลอดภัยในคอลัมน์หรือเซลล์ของสเปรดชีต
  Excel ด้วย GroupDocs.Redaction สำหรับ Java.
keywords:
- filter spreadsheet data java
- hide sensitive data excel
- GroupDocs.Redaction Java
- spreadsheet redaction
lastmod: 2026-08-04
og_description: เรียนรู้วิธีกรองข้อมูลสเปรดชีต java และทำการลบข้อมูลอย่างปลอดภัยในคอลัมน์หรือเซลล์ของสเปรดชีต
  Excel ด้วย GroupDocs.Redaction สำหรับ Java.
og_image_alt: Guide showing how to filter spreadsheet data in Java using GroupDocs.Redaction
og_title: กรองข้อมูลสเปรดชีต java – คู่มือกับ GroupDocs.Redaction
schemas:
- author: GroupDocs
  dateModified: '2026-08-04'
  description: Learn how to filter spreadsheet data java and securely redact columns
    or cells in Excel spreadsheets using GroupDocs.Redaction for Java.
  headline: Filter spreadsheet data java – guide with GroupDocs.Redaction
  type: TechArticle
- description: Learn how to filter spreadsheet data java and securely redact columns
    or cells in Excel spreadsheets using GroupDocs.Redaction for Java.
  name: Filter spreadsheet data java – guide with GroupDocs.Redaction
  steps:
  - name: instantiate the filter
    text: '`RedactionFilter` is the core class that represents a filtering rule for
      spreadsheet redaction. It accepts column numbers, row numbers, or custom lambda
      expressions to pinpoint data.'
  - name: configure the condition
    text: Use `filter.setColumnIndex(1)` to target column B (zero‑based) and `filter.setRegex("[A‑Z0‑9._%+-]+@[A‑Z0‑9.-]+\\.[A-Z]{2,}")`
      to match email patterns. You can also combine multiple conditions with `filter.and(...)`
      or `filter.or(...)`.
  - name: apply the redaction
    text: '`Redactor` is the main class that executes redaction operations on a workbook.
      Pass the workbook and the configured filter to the `Redactor` object. The API
      streams the workbook, applies the filter, and writes the redacted result to
      a new file, preserving original formatting and formulas.'
  type: HowTo
- questions:
  - answer: Yes, you can add additional column indexes to the same `RedactionFilter`
      instance or chain multiple filters with `filter.or(...)`.
    question: Can I filter multiple columns at once?
  - answer: Provide the password when opening the workbook; the filter operates after
      decryption just like on an unprotected file.
    question: Does the filter work on password‑protected workbooks?
  - answer: The engine is optimized for up to 1 million rows (≈500 MB) without loading
      the entire file into memory.
    question: How many rows can the API handle in a single operation?
  - answer: Yes, call `filter.preview(workbook)` to get a list of cell addresses that
      match the criteria.
    question: Is it possible to preview which cells will be redacted before saving?
  - answer: A full commercial license is required for production deployments; a temporary
      license is sufficient for testing and evaluation.
    question: What licensing model is required for production use?
  type: FAQPage
tags:
- filter spreadsheet data
- GroupDocs.Redaction
- Java spreadsheet redaction
- hide sensitive data excel
- data privacy
title: กรองข้อมูลสเปรดชีต java – คู่มือกับ GroupDocs.Redaction
type: docs
url: /th/java/spreadsheet-redaction/
weight: 12
---

# กรองข้อมูลสเปรดชีตใน Java – คู่มือ GroupDocs.Redaction สำหรับ Java

หากคุณต้องการ **filter spreadsheet data java** ก่อนทำการลบข้อมูลที่ต้องการซ่อน คุณมาถูกที่แล้ว ในบทแนะนำนี้คุณจะได้เรียนรู้วิธีการแยกแถว, คอลัมน์ หรือเซลล์เดี่ยวที่มีข้อมูลส่วนบุคคลหรือข้อมูลลับออกมา แล้วทำการลบข้อมูลเหล่านั้นอย่างปลอดภัยด้วย GroupDocs.Redaction สำหรับ Java ขั้นตอนต่าง ๆ จะอธิบายด้วยภาษาง่าย ๆ รวมถึงเคล็ดลับการปฏิบัติที่ดีที่สุด และแสดงวิธีทำให้การประมวลผลเร็วแม้กับเวิร์กบุ๊กขนาดใหญ่

## คำตอบอย่างรวดเร็ว
- **ไลบรารีใดที่จัดการการลบข้อมูลสเปรดชีตใน Java?** GroupDocs.Redaction for Java.  
- **ฉันสามารถกรองแถวโดยไม่โหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำได้หรือไม่?** ใช่ – API จะสตรีมข้อมูลและให้คุณใช้ตัวกรองได้ทันที.  
- **รูปแบบไฟล์ใดที่รองรับ?** มีรูปแบบสเปรดชีตกว่า 30 แบบ รวมถึง XLS, XLSX, CSV, และ ODS.  
- **ฉันต้องการไลเซนส์สำหรับการพัฒนาหรือไม่?** ไลเซนส์ชั่วคราวใช้ได้สำหรับการทดสอบ; ไลเซนส์เต็มจำเป็นสำหรับการใช้งานจริง.  
- **มีขีดจำกัดขนาดเวิร์กบุ๊กหรือไม่?** เอนจินสามารถประมวลผลไฟล์ได้สูงสุด 500 MB โดยไม่ใช้หน่วยความจำมากเกินไป.

## filter spreadsheet data java คืออะไร?
**Filter spreadsheet data java** คือกระบวนการเลือกแถว, คอลัมน์ หรือเซลล์เฉพาะในเวิร์กบุ๊กสไตล์ Excel ด้วยโค้ด Java อย่างเป็นโปรแกรม เพื่อให้ตรวจสอบหรือทำการลบข้อมูลเฉพาะที่ต้องการเท่านั้น เทคนิคนี้ช่วยลดเวลาในการทำงาน, จำกัดการเปลี่ยนแปลงที่ไม่จำเป็น, และช่วยให้สอดคล้องกับข้อกำหนดแบบ GDPR

## ทำไมต้องกรองข้อมูลสเปรดชีตใน Java?
GroupDocs.Redaction Java รองรับ **30+ รูปแบบสเปรดชีต** และสามารถประมวลผลเวิร์กบุ๊กที่มีขนาด **สูงสุด 500 MB** (ประมาณ 1 ล้านแถว) พร้อมการใช้หน่วยความจำไม่เกิน **200 MB** การกรองก่อนช่วยให้คุณไม่ต้องสัมผัสข้อมูลที่ไม่เกี่ยวข้อง ซึ่งจะลดเวลาในการประมวลผลโดยเฉลี่ย **40‑60 %** สำหรับสถานการณ์การลบข้อมูลส่วนบุคคลทั่วไป

## ข้อกำหนดเบื้องต้น
- ติดตั้ง Java 17 หรือรุ่นที่ใหม่กว่า  
- ระบบการสร้าง Maven หรือ Gradle  
- GroupDocs.Redaction สำหรับ Java (ดาวน์โหลดได้จากเว็บไซต์ทางการ)  
- คีย์ไลเซนส์ชั่วคราวหรือเต็ม  

## วิธีกรองข้อมูลในสเปรดชีตโดยใช้ GroupDocs.Redaction Java?
โหลดเวิร์กบุ๊ก, กำหนดตัวกรองที่ตรงกับเซลล์ที่ต้องการลบ, แล้วทำการลบข้อมูลตามตัวกรอง API จะทำการกรองแบบสตรีมมิ่ง ดังนั้นคุณไม่จำเป็นต้องเก็บไฟล์ทั้งหมดใน RAM

`RedactionFilter` class ให้คุณระบุดัชนีคอลัมน์, ช่วงแถว, หรือเงื่อนไขกำหนดเอง ตัวอย่างเช่น คุณสามารถกำหนดเป้าหมายทุกเซลล์ในคอลัมน์ **B** ที่มีรูปแบบอีเมล, หรือจำกัดการลบข้อมูลให้กับแถวที่คอลัมน์ “Status” มีค่าเป็น “Confidential”.

**Direct answer (40‑70 words):**  
สร้างอินสแตนซ์ของ `RedactionFilter`, ตั้งค่าดัชนีคอลัมน์และเงื่อนไข regular‑expression, แล้วส่งตัวกรองให้กับ `Redactor.redact(workbook, filter)`. ตัวกรองบรรทัดเดียวนี้จะแยกเซลล์ที่ตรงกับเกณฑ์ของคุณ, และ Redactor จะลบหรือปกปิดเซลล์เหล่านั้นในขณะที่ปล่อยส่วนอื่นของชีตไว้ไม่เปลี่ยนแปลง การทำงานเสร็จในเวลาเชิงเส้นตามจำนวนแถวที่กรอง

### ขั้นตอนที่ 1: สร้างอินสแตนซ์ของตัวกรอง
`RedactionFilter` คือคลาสหลักที่แสดงกฎการกรองสำหรับการลบข้อมูลสเปรดชีต มันรับหมายเลขคอลัมน์, หมายเลขแถว, หรือ lambda expression กำหนดเองเพื่อระบุตำแหน่งข้อมูล.

### ขั้นตอนที่ 2: กำหนดเงื่อนไข
ใช้ `filter.setColumnIndex(1)` เพื่อกำหนดเป้าหมายที่คอลัมน์ B (เริ่มจากศูนย์) และ `filter.setRegex("[A‑Z0‑9._%+-]+@[A‑Z0‑9.-]+\\.[A-Z]{2,}")` เพื่อจับรูปแบบอีเมล คุณยังสามารถรวมเงื่อนไขหลายอย่างด้วย `filter.and(...)` หรือ `filter.or(...)`.

### ขั้นตอนที่ 3: ทำการลบข้อมูล
`Redactor` คือคลาสหลักที่ดำเนินการลบข้อมูลบนเวิร์กบุ๊ก  
ส่งเวิร์กบุ๊กและตัวกรองที่กำหนดให้กับอ็อบเจ็กต์ `Redactor` API จะสตรีมเวิร์กบุ๊ก, ใช้ตัวกรอง, และเขียนผลลัพธ์ที่ลบข้อมูลแล้วลงไฟล์ใหม่, รักษาการจัดรูปแบบและสูตรเดิมไว้

## ปัญหาทั่วไปและวิธีแก้
- **ตัวกรองไม่ตรงกับเซลล์ใดเลย:** ตรวจสอบดัชนีคอลัมน์ (เริ่มจากศูนย์) และตรวจให้แน่ใจว่าการเขียน regular‑expression ถูกต้องสำหรับ Java.  
- **ข้อผิดพลาด Out‑of‑memory กับไฟล์ขนาดใหญ่:** เพิ่มขนาด heap ของ JVM อย่างพอประมาณ (เช่น `-Xmx1g`) หรือแยกเวิร์กบุ๊กเป็นส่วนย่อยก่อนทำการกรอง.  
- **ผลลัพธ์ที่ลบข้อมูลสูญเสียการจัดรูปแบบ:** `RedactionOptions` ให้คุณปรับแต่งพฤติกรรมการลบข้อมูล เช่น การรักษาการจัดรูปแบบเซลล์ ใช้ `RedactionOptions.setPreserveFormatting(true)` เพื่อคงสไตล์ของเซลล์ไว้.

## ทำไมต้องกรองข้อมูลสเปรดชีต?
การกรองก่อนทำการลบข้อมูลจะคัดแยกเฉพาะส่วนที่เป็นข้อมูลสำคัญของเวิร์กบุ๊กเท่านั้น ซึ่งหมายความว่าคุณจะหลีกเลี่ยงการเปลี่ยนแปลงข้อมูลที่สะอาดโดยไม่จำเป็น วิธีการเลือกนี้ยังลดความเสี่ยงของการสูญเสียข้อมูลโดยบังเอิญและเร่งกระบวนการตรวจสอบความสอดคล้อง เนื่องจากบันทึกการตรวจสอบมีรายการน้อยลงมาก

## วิธีลบอีเมลในสเปรดชีต Excel ด้วย GroupDocs.Redaction Java API
โหลดไฟล์ Excel ของคุณ, ใช้ตัวกรองที่ค้นหารูปแบบอีเมลทั่วไป, แล้วเรียกใช้ Redactor API จะเปลี่ยนอีเมลที่ตรงกับรูปแบบแต่ละรายการด้วยตัวแทนเช่น “***@***.com” พร้อมคงรูปแบบเซลล์โดยรอบ

## วิธีกรองข้อมูล – บทเรียนที่มีให้
- [วิธีลบอีเมลในสเปรดชีต Excel ด้วย GroupDocs.Redaction Java API](./redact-emails-excel-groupdocs-redaction-java/)

## แหล่งข้อมูลเพิ่มเติม
- [เอกสาร GroupDocs.Redaction สำหรับ Java](https://docs.groupdocs.com/redaction/java/)
- [อ้างอิง API GroupDocs.Redaction สำหรับ Java](https://reference.groupdocs.com/redaction/java/)
- [ดาวน์โหลด GroupDocs.Redaction สำหรับ Java](https://releases.groupdocs.com/redaction/java/)
- [ฟอรั่ม GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)
- [สนับสนุนฟรี](https://forum.groupdocs.com/)
- [ไลเซนส์ชั่วคราว](https://purchase.groupdocs.com/temporary-license/)

---

**อัปเดตล่าสุด:** 2026-08-04  
**ทดสอบด้วย:** GroupDocs.Redaction 23.11 for Java  
**ผู้เขียน:** GroupDocs  

## คำถามที่พบบ่อย
**Q: ฉันสามารถกรองหลายคอลัมน์พร้อมกันได้หรือไม่?**  
A: ใช่, คุณสามารถเพิ่มดัชนีคอลัมน์เพิ่มเติมให้กับอินสแตนซ์ `RedactionFilter` เดียวกันหรือเชื่อมต่อหลายตัวกรองด้วย `filter.or(...)`.

**Q: ตัวกรองทำงานกับเวิร์กบุ๊กที่มีการป้องกันด้วยรหัสผ่านหรือไม่?**  
A: ให้รหัสผ่านเมื่อเปิดเวิร์กบุ๊ก; ตัวกรองทำงานหลังการถอดรหัสเช่นเดียวกับไฟล์ที่ไม่มีการป้องกัน.

**Q: API สามารถจัดการกับแถวได้กี่แถวในหนึ่งการดำเนินการ?**  
A: เอนจินได้รับการปรับให้ทำงานได้สูงสุด 1 ล้านแถว (≈500 MB) โดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ.

**Q: สามารถดูตัวอย่างเซลล์ที่จะถูกลบข้อมูลก่อนบันทึกได้หรือไม่?**  
A: ใช่, เรียก `filter.preview(workbook)` เพื่อรับรายการที่อยู่ของเซลล์ที่ตรงกับเกณฑ์.

**Q: โมเดลไลเซนส์แบบใดที่จำเป็นสำหรับการใช้งานในสภาพแวดล้อมการผลิต?**  
A: จำเป็นต้องมีไลเซนส์เชิงพาณิชย์เต็มรูปแบบสำหรับการใช้งานในสภาพแวดล้อมการผลิต; ไลเซนส์ชั่วคราวเพียงพอสำหรับการทดสอบและประเมินผล.

## บทเรียนที่เกี่ยวข้อง
- [วิธีลบข้อมูลที่ละเอียดอ่อนในสเปรดชีต Excel ด้วย GroupDocs.Redaction Java API](/redaction/java/spreadsheet-redaction/redact-emails-excel-groupdocs-redaction-java/)
- [Mask Sensitive Data Java – คู่มือ GroupDocs.Redaction](/redaction/java/getting-started/)
- [Mask Sensitive Data Java – ลบข้อมูลส่วนบุคคลด้วย GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)