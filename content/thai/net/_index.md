---
additionalTitle: GroupDocs API References
date: 2026-10-06
description: เรียนรู้วิธีลบข้อมูลในหน้า PDF, ลบคำอธิบายบน PDF, และลบข้อมูลในเซลล์
  Excel ด้วย GroupDocs.Redaction for .NET – API ที่ปลอดภัยและข้ามแพลตฟอร์มสำหรับการลบข้อมูลในเอกสาร
keywords:
- how to redact pdf
- remove pdf annotations
- redact excel cells
- redact pdf pages
- load pdf from stream
lastmod: 2026-10-06
linktitle: บทเรียน GroupDocs.Redaction for .NET
og_description: วิธีลบข้อมูลในหน้า PDF อย่างรวดเร็วด้วย GroupDocs.Redaction for .NET.
  API นี้ลบคำอธิบายบน PDF, ลบข้อมูลในเซลล์ Excel, และปกป้องข้อมูลที่ละเอียดอ่อนในกว่า
  30 รูปแบบ
og_image_alt: Guide to redact PDF pages using GroupDocs.Redaction for .NET
og_title: วิธีลบข้อมูลในหน้า PDF – GroupDocs.Redaction for .NET
schemas:
- author: GroupDocs
  dateModified: '2026-10-06'
  description: Learn how to redact PDF pages, remove PDF annotations, and redact Excel
    cells using GroupDocs.Redaction for .NET – a secure, cross‑platform API for document
    redaction.
  headline: How to redact PDF pages with GroupDocs.Redaction for .NET
  type: TechArticle
- description: Learn how to redact PDF pages, remove PDF annotations, and redact Excel
    cells using GroupDocs.Redaction for .NET – a secure, cross‑platform API for document
    redaction.
  name: How to redact PDF pages with GroupDocs.Redaction for .NET
  steps:
  - name: load the PDF
    text: You can open a file from disk, a memory stream, or a remote source. The
      API accepts both a file path string and a `Stream` object, which is ideal for
      web services that receive uploads.
  - name: define the pages to redact
    text: Pass a list of zero‑based page indexes or a range string such as `"1-3,5"`
      to the `RemovePages` method. The library validates the range and throws a clear
      exception if a page does not exist.
  - name: save the sanitized document
    text: Call `Save` with the desired output format. You can keep the original PDF,
      export to a rasterized PDF, or stream the result directly to the client response.
  type: HowTo
- questions:
  - answer: Yes, the library removes the specified pages while preserving page numbering,
      bookmarks, and cross‑references for the remaining content.
    question: Can I redact PDF pages without affecting the rest of the document’s
      layout?
  - answer: Absolutely. Use `Redactor.RemoveAnnotations()` to strip all annotation
      objects in a single call.
    question: Is it possible to redact PDF annotations only?
  - answer: Load the workbook with `Redactor.LoadExcel(path)`, then call `Redactor.RedactCell(sheetName,
      cellAddress, RedactionMode.Blackout)` and save.
    question: How do I redact Excel cells directly?
  - answer: Yes, you can pass any `System.IO.Stream` to the `Load` method, which is
      ideal for processing files uploaded via ASP.NET Core controllers.
    question: Does GroupDocs.Redaction support loading PDFs from a stream?
  - answer: Metered licensing lets you pay per‑redaction operation, scaling cost‑effectively
      with usage spikes.
    question: What licensing model is recommended for high‑volume production use?
  type: FAQPage
tags:
- pdf redaction
- groupdocs.redaction
- .net document security
- redact pdf pages
title: วิธีลบข้อมูลในหน้า PDF ด้วย GroupDocs.Redaction for .NET
type: docs
url: /th/net/
weight: 10
---

# วิธีทำการลบข้อมูลในหน้า PDF ด้วย GroupDocs.Redaction สำหรับ .NET

หากคุณต้องการ **ลบข้อมูลในหน้า PDF** อย่างรวดเร็วและเชื่อถือได้ GroupDocs.Redaction สำหรับ .NET จะมอบ API ครบวงจรแบบข้ามแพลตฟอร์มที่ลบเนื้อหาที่เป็นความลับจากไฟล์กว่า 30 รูปแบบ ไม่ว่าคุณจะสร้างกระบวนการทำงานที่ขับเคลื่อนด้วยการปฏิบัติตามกฎระเบียบ พอร์ทัลการจัดการเอกสาร หรือแอปพลิเคชันที่ให้ความเป็นส่วนตัวเป็นอันดับแรก ไลบรารีนี้ช่วยให้คุณลบข้อมูลลับอย่างถาวรในขณะที่ยังคงรักษาโครงสร้างของเอกสารไว้

**GroupDocs.Redaction for .NET คือไลบรารี .NET ที่ช่วยให้สามารถลบข้อมูลที่เป็นความลับอย่างถาวรจากเอกสารมากกว่า 30 รูปแบบ** รองรับการประมวลผลปริมาณมาก สามารถจัดการไฟล์หลายร้อยหน้าโดยไม่ต้องโหลดเอกสารทั้งหมดเข้าสู่หน่วยความจำ และให้ตัวเลือกการเรสเตอร์ไลซ์ที่แปลงข้อความเป็นภาพเพื่อความปลอดภัยเพิ่มขึ้น

{{% alert color="primary" %}}
GroupDocs.Redaction for .NET มีชุดบทเรียนและตัวอย่างที่ครอบคลุมสำหรับการนำการลบข้อมูลเอกสารอย่างปลอดภัยไปใช้ในแอปพลิเคชัน .NET ของคุณ ตั้งแต่การแทนที่ข้อความพื้นฐานจนถึงการทำความสะอาดเมตาดาต้าขั้นสูง แหล่งข้อมูลเหล่านี้ครอบคลุมเทคนิคสำคัญสำหรับการลบข้อมูลที่เป็นความลับจากเอกสาร เรียนรู้วิธีลบข้อมูลส่วนตัวอย่างถาวรจากรูปแบบเอกสารต่าง ๆ รวมถึง PDF, Word, Excel, PowerPoint และรูปภาพ ด้วยการควบคุมที่แม่นยำและการลบข้อมูลลับอย่างสมบูรณ์ คู่มือขั้นตอนต่อขั้นตอนของเราช่วยให้คุณเชี่ยวชาญทั้งความสามารถการลบข้อมูลมาตรฐานและขั้นสูงเพื่อให้ตรงตามข้อกำหนดการปฏิบัติตามและปกป้องข้อมูลที่สำคัญได้อย่างมีประสิทธิภาพ
{{% /alert %}}

## คำตอบอย่างรวดเร็ว
- **GroupDocs.Redaction สามารถลบข้อมูลในหน้า PDF ทั้งหมดได้หรือไม่?** ใช่, คุณสามารถลบหน้าเดี่ยวหรือช่วงหน้าด้วยการเรียก API เพียงครั้งเดียว.  
- **รองรับการลบคำอธิบายประกอบใน PDF หรือไม่?** แน่นอน – คำอธิบาย, ความคิดเห็น, และการทำเครื่องหมายสามารถลบได้ในขั้นตอนเดียว.  
- **ฉันสามารถลบข้อมูลในเซลล์ Excel ได้โดยไม่ต้องแปลงเป็น PDF หรือไม่?** ใช่, ไลบรารีนี้ทำงานโดยตรงกับแผ่นงาน Excel.  
- **การโหลด PDF จากสตรีมได้รับการสนับสนุนหรือไม่?** API ยอมรับอ็อบเจ็กต์ `Stream` ทำให้สามารถประมวลผลในหน่วยความจำได้.  
- **เวอร์ชัน .NET ใดบ้างที่เข้ากันได้?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## การลบข้อมูลในบริบทของ PDF คืออะไร?
การลบข้อมูลคือการลบหรือบังเนื้อหาที่เป็นความลับจากเอกสารอย่างถาวรเพื่อไม่ให้สามารถกู้คืนหรือดูได้ในภายหลัง ในไฟล์ PDF การลบข้อมูลสามารถทำได้กับข้อความ, รูปภาพ, คำอธิบายประกอบ หรือทั้งหน้า และผลลัพธ์คือไฟล์ที่ผ่านการทำความสะอาดซึ่งยังคงรักษาการจัดวางเดิมไว้

## ทำไมต้องใช้ GroupDocs.Redaction สำหรับ .NET?
GroupDocs.Redaction สำหรับ .NET ให้โซลูชันที่มีประสิทธิภาพสูงและทนทานต่อเอกสารขนาดใหญ่ พร้อมการลบข้อมูลที่เป็นความลับอย่างสมบูรณ์ มีการเรสเตอร์ไลซ์ในตัว, รองรับรูปแบบไฟล์หลากหลาย, และบันทึกการตรวจสอบอย่างละเอียด ทำให้เหมาะกับแอปพลิเคชันที่ต้องปฏิบัติตามกฎระเบียบและสภาพแวดล้อมระดับองค์กร

- **รองรับรูปแบบกว่า 30 ประเภท** – รวมถึง PDF, DOCX, XLSX, PPTX, HTML, และรูปภาพทั่วไป.  
- **ประสิทธิภาพที่ปรับขนาดได้** – ประมวลผล PDF 500 หน้าในเวลาน้อยกว่า 5 วินาทีบนเซิร์ฟเวอร์ทั่วไป โดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่ RAM.  
- **เรสเตอร์ไลซ์ในตัว** – แปลงหน้าที่ลบเป็นภาพ เพื่อรับประกันว่าไม่มีข้อความที่ซ่อนอยู่.  
- **พร้อมปฏิบัติตามข้อกำหนด** – รองรับ GDPR, HIPAA, และ PCI‑DSS ด้วยการบันทึกเส้นทางการตรวจสอบ.

## ข้อกำหนดเบื้องต้น
- .NET Framework 4.5+ **หรือ** .NET Core 3.1+ ที่ติดตั้งบนเครื่องพัฒนาของคุณ.  
- ใบอนุญาต GroupDocs.Redaction ที่ถูกต้อง (มีรุ่นทดลองให้ประเมิน).  
- การเข้าถึงไฟล์ PDF, Excel หรือ Word ที่คุณต้องการประมวลผล.

## วิธีลบข้อมูลในหน้า PDF ขั้นตอนโดยขั้นตอน

Redactor เป็นคลาสหลักใน GroupDocs.Redaction ที่ใช้โหลด, แก้ไข, และบันทึกเอกสาร `RemovePages` จะลบหน้าที่ระบุออกจากเอกสารที่โหลดแล้ว

โหลด PDF, กำหนดหน้าที่ต้องการลบ, ใช้การลบข้อมูล, แล้วบันทึกผลลัพธ์ ตัวอย่างต่อไปนี้อธิบายรูปแบบหลัก:

โหลด PDF เป้าหมายด้วย `Redactor.Load(streamOrPath)`, เรียก `Redactor.RemovePages(pageNumbers)` เพื่อลบหน้าที่ไม่ต้องการ, และสุดท้ายเรียก `Redactor.Save(outputPath)` – กระบวนการสามขั้นตอนนี้ลบหน้าได้ภายในไม่กี่วินาทีสำหรับเอกสารส่วนใหญ่

### ขั้นตอน 1: โหลด PDF
คุณสามารถเปิดไฟล์จากดิสก์, สตรีมหน่วยความจำ, หรือแหล่งข้อมูลระยะไกล API ยอมรับทั้งสตริงเส้นทางไฟล์และอ็อบเจ็กต์ `Stream` ซึ่งเหมาะกับบริการเว็บที่รับอัปโหลด

### ขั้นตอน 2: กำหนดหน้าที่จะลบ
ส่งรายการดัชนีหน้าที่เริ่มจากศูนย์หรือสตริงช่วงเช่น `"1-3,5"` ไปยังเมธอด `RemovePages` ไลบรารีจะตรวจสอบช่วงและโยนข้อยกเว้นที่ชัดเจนหากหน้าที่ระบุไม่มีอยู่

### ขั้นตอน 3: บันทึกเอกสารที่ทำความสะอาด
เรียก `Save` พร้อมรูปแบบผลลัพธ์ที่ต้องการ คุณสามารถเก็บ PDF ดั้งเดิม, ส่งออกเป็น PDF ที่เรสเตอร์ไลซ์, หรือสตรีมผลลัพธ์โดยตรงไปยังการตอบสนองของไคลเอนต์

## ปัญหาทั่วไปและวิธีแก้
- **ปัญหา:** การลบข้อมูลดูเหมือนทำงานได้แต่ข้อความเดิมยังค้นหาได้.  
  **วิธีแก้:** เปิดใช้งานการเรสเตอร์ไลซ์ (`Redactor.Rasterize = true`) ก่อนบันทึก; วิธีนี้จะแปลงหน้าเป็นภาพและลบเลเยอร์ข้อความที่ซ่อนอยู่.  

- **ปัญหา:** PDF ขนาดใหญ่ทำให้เกิดข้อยกเว้น OutOfMemory.  
  **วิธีแก้:** ใช้ `Redactor.Load(stream, loadOptions => loadOptions.EnableMemoryOptimization = true)` เพื่อประมวลผลไฟล์เป็นชิ้นส่วน.  

- **ปัญหา:** คำอธิบายประกอบไม่ถูกลบ.  
  **วิธีแก้:** เรียก `Redactor.RemoveAnnotations()` หลังจากโหลดเอกสาร; เมธอดนี้จะลบความคิดเห็น, ไฮไลท์, และฟิลด์ฟอร์มทั้งหมด.

## คำถามที่พบบ่อย

**ถาม: ฉันสามารถลบข้อมูลในหน้า PDF ได้โดยไม่กระทบต่อการจัดวางของเอกสารส่วนที่เหลือหรือไม่?**  
ตอบ: ใช่, ไลบรารีจะลบหน้าที่ระบุโดยคงลำดับหน้า, บุ๊กมาร์ก, และการอ้างอิงข้ามสำหรับเนื้อหาที่เหลือไว้

**ถาม: สามารถลบคำอธิบายประกอบใน PDF เท่านั้นได้หรือไม่?**  
ตอบ: แน่นอน. ใช้ `Redactor.RemoveAnnotations()` เพื่อเอาวัตถุคำอธิบายประกอบทั้งหมดออกในหนึ่งการเรียก

**ถาม: วิธีลบเซลล์ Excel โดยตรงคืออะไร?**  
ตอบ: โหลดเวิร์กบุ๊กด้วย `Redactor.LoadExcel(path)`, จากนั้นเรียก `Redactor.RedactCell(sheetName, cellAddress, RedactionMode.Blackout)` แล้วบันทึก

**ถาม: GroupDocs.Redaction รองรับการโหลด PDF จากสตรีมหรือไม่?**  
ตอบ: ใช่, คุณสามารถส่งอ็อบเจ็กต์ `System.IO.Stream` ใด ๆ ไปยังเมธอด `Load` ซึ่งเหมาะกับการประมวลผลไฟล์ที่อัปโหลดผ่านคอนโทรลเลอร์ ASP.NET Core

**ถาม: โมเดลการให้ลิขสิทธิ์ใดที่แนะนำสำหรับการใช้งานในระดับการผลิตที่มีปริมาณสูง?**  
ตอบ: การให้ลิขสิทธิ์แบบ Metered ช่วยให้คุณจ่ายตามการดำเนินการลบข้อมูลแต่ละครั้ง สามารถปรับขนาดค่าใช้จ่ายได้ตามความต้องการใช้งานที่เพิ่มขึ้น

---

**อัปเดตล่าสุด:** 2026-10-06  
**ทดสอบด้วย:** GroupDocs.Redaction 23.10 for .NET  
**ผู้เขียน:** GroupDocs  

---  

### บทแนะนำ GroupDocs.Redaction สำหรับ .NET – วิธีลบข้อมูลในหน้า PDF

### [บทแนะนำการเริ่มต้น](./getting-started/)

เริ่มต้นที่นี่หากคุณใหม่กับ GroupDocs.Redaction บทแนะนำนี้จะพาคุณผ่านการติดตั้ง, การขอใบอนุญาต, และการสร้างโครงการลบข้อมูลแรกใน .NET คุณจะได้เห็นวิธีเปิดเอกสาร, กำหนดกฎลบข้อมูลอย่างง่าย, และบันทึกไฟล์ที่ทำความสะอาดแล้ว

### [เทคนิคการลบข้อมูลขั้นสูง](./advanced-redaction/)

เจาะลึกด้วยตัวจัดการลบข้อมูลแบบกำหนดเอง, นโยบาย, คอลแบ็ก, และการลบข้อมูลด้วย AI บทนำนี้แสดงวิธีสร้างพายป์ไลน์ที่ยืดหยุ่นเพื่อ **ลบข้อมูลในหน้า PDF**, จัดการโครงสร้างเอกสารที่ซับซ้อน, และรวมโมเดลแมชชีนเลิร์นนิงเพื่อการตรวจจับเนื้อหาที่ฉลาดขึ้น

### [บทแนะนำการลบคำอธิบายประกอบ](./annotation-redaction/)

คำอธิบายประกอบมักมีโน้ตที่เป็นความลับ เรียนรู้วิธีค้นหา, แก้ไข, หรือเอาคำอธิบายประกอบ, ความคิดเห็น, และการทำเครื่องหมายรีวิวออกจาก PDF, ไฟล์ Word, และรูปแบบที่รองรับอื่น ๆ

### [บทแนะนำข้อมูลเอกสาร](./document-information/)

การเข้าใจเมตาดาต้าเอกสารเป็นขั้นตอนแรกสู่การลบข้อมูลอย่างปลอดภัย บทแนะนำนี้อธิบายวิธีดึงคุณสมบัติของเอกสาร, แสดงรูปแบบที่รองรับ, และสร้างภาพตัวอย่างก่อนทำการลบข้อมูลใด ๆ

### [บทแนะนำการโหลดเอกสาร](./document-loading/)

เอกสารอาจอยู่บนดิสก์, ในสตรีม, หรืออยู่หลังชั้นการตรวจสอบสิทธิ์ เรียนรู้แนวปฏิบัติที่ดีที่สุดสำหรับการโหลดไฟล์ท้องถิ่น, สตรีมหน่วยความจำ, และเอกสารที่มีรหัสผ่านอย่างปลอดภัย

### [บทแนะนำการบันทึกเอกสาร](./document-saving/)

หลังการลบข้อมูลคุณต้องบันทึกไฟล์ที่ทำความสะอาด บทนำนี้ครอบคลุมการบันทึกในรูปแบบเดิม, การส่งออกเป็น PDF ที่เรสเตอร์ไลซ์, และการสตรีมผลลัพธ์โดยตรงไปยังแอปพลิเคชันฝั่งไคลเอนต์

### [บทแนะนำการจัดการรูปแบบ](./format-handling/)

GroupDocs.Redaction รองรับรูปแบบไฟล์หลากหลาย สำรวจวิธีทำงานกับประเภทไฟล์ต่าง ๆ, สร้างตัวจัดการรูปแบบแบบกำหนดเอง, และขยายไลบรารีเพื่อรองรับมาตรฐานเอกสารเฉพาะทาง

### [บทแนะนำการลบข้อมูลรูปภาพ](./image-redaction/)

รูปภาพอาจซ่อนข้อมูลที่สำคัญ เรียนรู้วิธีลบพื้นที่รูปภาพเฉพาะ, เอารูปภาพที่ฝังอยู่, และทำความสะอาดเมตาดาต้ารูปภาพเพื่อให้แน่ใจว่าไม่มีข้อมูลที่ซ่อนอยู่เหลืออยู่

### [บทแนะนำการให้ลิขสิทธิ์และการกำหนดค่า](./licensing-configuration/)

การให้ลิขสิทธิ์ที่เหมาะสมเป็นสิ่งสำคัญสำหรับการใช้งานในระดับการผลิต บทแนะนำนี้แสดงวิธีใช้ใบอนุญาต, กำหนดค่าการทำงาน, และนำการให้ลิขสิทธิ์แบบ Metered ไปใช้สำหรับการปรับขนาดการใช้งาน

### [บทแนะนำการลบเมตาดาต้า](./metadata-redaction/)

เมตาดาต้ามักทำให้ข้อมูลลับรั่วไหล ตามคู่มือนี้เพื่อเอาคุณสมบัติของเอกสาร, ความคิดเห็นที่ซ่อนอยู่, และเมตาดาต้าอื่น ๆ ออกจากไฟล์ PDF, Word, Excel, และ PowerPoint

### [บทแนะนำการรวม OCR](./ocr-integration/)

เมื่อทำงานกับ PDF หรือรูปภาพที่สแกน OCR เป็นสิ่งจำเป็น เรียนรู้การรวมเครื่องมือ OCR, ดึงข้อความที่ค้นหาได้, แล้ว **ลบข้อมูลในหน้า PDF** ที่มีข้อมูลสำคัญ

### [บทแนะนำการลบหน้า](./page-redaction/)

บางครั้งคุณต้องลบทั้งหน้า บทแนะนำนี้แสดงวิธีลบหน้าเดี่ยว, ช่วงหน้า, และลบหน้าแบบมีเงื่อนไขตามเนื้อหา

### [บทแนะนำการลบข้อมูลเฉพาะ PDF](./pdf-specific-redaction/)

PDF มีคุณลักษณะเฉพาะเช่นเลเยอร์, คำอธิบายประกอบ, และฟิลด์ฟอร์ม เชี่ยวชาญเทคนิคการลบข้อมูลเฉพาะ PDF รวมถึงการกรองเนื้อหาและการรักษาความสมบูรณ์ของเอกสาร

### [บทแนะนำตัวเลือกการเรสเตอร์ไลซ์](./rasterization-options/)

PDF ที่เรสเตอร์ไลซ์จะแปลงเนื้อหาเป็นภาพ ทำให้การสกัดข้อมูลเป็นไปไม่ได้ เรียนรู้การกำหนดค่าเสียงรบกวน, ความเอียง, ระดับสีเทา, และขอบ แล้วค้นพบวิธี **บันทึก PDF ที่เรสเตอร์ไลซ์** เพื่อความปลอดภัยสูงสุด

### [บทแนะนำการลบข้อมูลสเปรดชีต](./spreadsheet-redaction/)

สเปรดชีต Excel มักมีเซลล์ที่เป็นความลับ คู่มือนี้แสดงวิธี **ลบข้อมูลในเซลล์ Excel**, ซ่อนสูตร, และปกป้องแผ่นงานที่สำคัญ

### [บทแนะนำการลบข้อความ](./text-redaction/)

ข้อความเป็นประเภทข้อมูลที่ต้องปกป้องบ่อยที่สุด ทำตามขั้นตอนอย่างละเอียดสำหรับการจับคู่วลีที่ตรงกัน, การลบข้อมูลด้วย regular expression, และการค้นหาแบบแยกตัวพิมพ์ใหญ่‑เล็ก รวมถึงวิธี **ลบข้อความใน Word** อย่างมีประสิทธิภาพ

## บทแนะนำที่เกี่ยวข้อง

- [How to Remove Annotations – Annotation Redaction Tutorials for GroupDocs.Redaction .NET](/redaction/net/annotation-redaction/)
- [How to Remove the Last Page of a PDF Using GroupDocs.Redaction for .NET](/redaction/net/page-redaction/remove-last-page-pdf-groupdocs-redaction-net/)
- [How to Redact PDF and Save as Rasterized PDF with GroupDocs.Redaction for .NET](/redaction/net/document-saving/groupdocs-redaction-net-rasterized-pdfs/)