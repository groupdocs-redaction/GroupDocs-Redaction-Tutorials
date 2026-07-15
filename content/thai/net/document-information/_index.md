---
date: 2026-06-06
description: เรียนรู้วิธีสกัดข้อมูลเมตาดาต้าเอกสาร, รับจำนวนหน้า, และสร้างตัวอย่างภาพโดยใช้
  GroupDocs.Redaction สำหรับ .NET – การสอน C# ทีละขั้นตอน
keywords:
- extract document metadata
- how to get page count
- metadata extraction c#
- read metadata from stream
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to extract document metadata, get page count, and generate
    previews using GroupDocs.Redaction for .NET – step‑by‑step C# tutorials.
  headline: Extract Document Metadata – GroupDocs.Redaction .NET Tutorials
  type: TechArticle
- description: Learn how to extract document metadata, get page count, and generate
    previews using GroupDocs.Redaction for .NET – step‑by‑step C# tutorials.
  name: Extract Document Metadata – GroupDocs.Redaction .NET Tutorials
  steps:
  - name: Instantiate `RedactionEngine` with the file path or stream.
    text: Instantiate `RedactionEngine` with the file path or stream.
  - name: Call `GetDocumentInfo()`.
    text: Call `GetDocumentInfo()`.
  - name: Access properties like `Author`, `Title`, `CreatedDate`, and `PageCount`.
    text: Access properties like `Author`, `Title`, `CreatedDate`, and `PageCount`.
  type: HowTo
- questions:
  - answer: Yes. Provide the password when constructing `RedactionEngine`; the API
      will decrypt the header and return metadata.
    question: Can I extract metadata from password‑protected PDFs?
  - answer: Absolutely. Loop through your file collection, instantiate `RedactionEngine`
      for each, and call `GetDocumentInfo()`—the engine is lightweight enough for
      thousands of files.
    question: Does the API support batch processing of multiple files?
  - answer: The corresponding properties return `null` or default values; you can
      safely check for `null` before using them.
    question: What happens if a document has no metadata?
  - answer: GroupDocs.Redaction focuses on redaction, not editing metadata. Use GroupDocs.Metadata
      or another library for write‑back scenarios.
    question: Is it possible to modify metadata after extraction?
  - answer: .NET Framework 4.7.2+, .NET Core 3.1+, .NET 5+, and .NET 6+ are fully
      supported.
    question: Which .NET versions are officially supported?
  type: FAQPage
title: สกัดข้อมูลเมตาดาต้าเอกสาร – GroupDocs.Redaction .NET บทเรียน
type: docs
url: /th/net/document-information/
weight: 15
---

# บทแนะนำข้อมูลเอกสารสำหรับ GroupDocs.Redaction .NET

ในศูนย์นี้คุณจะค้นพบวิธีการ **extract document metadata** จากประเภทไฟล์ที่หลากหลาย, กำหนดจำนวนหน้า, และสร้างภาพตัวอย่างก่อนที่คุณจะดำเนินการลบข้อมูล. ด้วยการเข้าถึงข้อมูลนี้โดยโปรแกรม คุณสามารถตัดสินใจว่าไฟล์ใดต้องการการจัดการพิเศษ, บังคับใช้กฎการปฏิบัติตาม, และปรับปรุงประสิทธิภาพการประมวลผลโดยรวม. ตัวอย่างทั้งหมดเขียนด้วย C# และมุ่งเป้าไปที่ .NET 6+, ดังนั้นคุณสามารถนำไปใช้ในโครงการที่มีอยู่ของคุณได้ทันที.

## คำตอบด่วน
- **ฉันจะดึง metadata อย่างไร?** ใช้ `RedactionEngine.GetDocumentInfo()` เพื่อดึงคุณสมบัติเช่น author, creation date, และ page count.  
- **ฉันสามารถอ่าน metadata จาก stream ได้หรือไม่?** ใช่—ส่ง `MemoryStream` ที่มีไฟล์ไปยังเมธอด API เดียวกัน.  
- **รูปแบบที่รองรับคืออะไร?** มีมากกว่า 100 รูปแบบ, รวมถึง PDF, DOCX, PPTX, และไฟล์รูปภาพ.  
- **การดึงจำนวนหน้ามีความเร็วหรือไม่?** เครื่องยนต์อ่านเฉพาะส่วนหัวของไฟล์, ให้จำนวนหน้าในเวลาน้อยกว่า 50 ms สำหรับเอกสารส่วนใหญ่.  
- **ฉันต้องการใบอนุญาตสำหรับการพัฒนาหรือไม่?** ใบอนุญาตชั่วคราวใช้ได้สำหรับการทดสอบ; จำเป็นต้องมีใบอนุญาตเต็มสำหรับการใช้งานจริง.

## “extract document metadata” คืออะไร?
**Extract document metadata** หมายถึงการดึงคุณสมบัติที่ฝังอยู่โดยโปรแกรม—เช่น author, title, creation date, และ page count—จากไฟล์โดยไม่ต้องเปิดในโปรแกรมดูไฟล์. การดำเนินการที่มีน้ำหนักเบานี้ทำให้แอปพลิเคชันของคุณสามารถตัดสินใจอย่างมีข้อมูลก่อนที่การลบข้อมูลจะเริ่มต้น.

## ทำไมต้องดึงข้อมูลเมตาดาต้าเอกสารด้วย GroupDocs.Redaction?
GroupDocs.Redaction สามารถอ่านเมตาดาต้าจาก **100+** รูปแบบไฟล์พร้อมกับรักษาการใช้หน่วยความจำให้อยู่ต่ำกว่า 10 MB สำหรับเอกสารที่มีจำนวนหน้าสูงสุด 500 หน้า. API จะคืนค่าอ็อบเจ็กต์ `DocumentInfo` ที่มีประเภทเต็ม, ทำให้ไม่ต้องใช้ตัวแยกข้อมูลแบบกำหนดเองและลดเวลาในการพัฒนาถึง 70 %.

## ข้อกำหนดเบื้องต้น
- .NET 6+ (or .NET Core 3.1 / .NET Framework 4.7.2)  
- ติดตั้งแพ็กเกจ NuGet ของ GroupDocs.Redaction for .NET  
- คีย์ใบอนุญาตชั่วคราวหรือเต็ม (พร้อมใช้งานจากพอร์ทัลของ GroupDocs)

## วิธีดึงข้อมูลเมตาดาต้าเอกสารโดยใช้ GroupDocs.Redaction .NET?
`RedactionEngine` คือคอมโพเนนต์หลักที่โหลดเอกสารและให้เมธอดการดึงเมตาดาต้า. `GetDocumentInfo()` คืนค่าอ็อบเจ็กต์ `DocumentInfo` ที่มีเมตาดาต้าเช่น author, title, และ page count. โหลดไฟล์ (หรือ stream) ด้วย `RedactionEngine`, เรียก `GetDocumentInfo()`, และอ่านคุณสมบัติที่คืนค่า. การดำเนินการเสร็จในบรรทัดโค้ดเดียวและไม่ต้องโหลดเอกสารทั้งหมดเข้าสู่หน่วยความจำ.

### วิธีดึงจำนวนหน้าจากเอกสาร?
`DocumentInfo` เป็นอ็อบเจ็กต์ที่มีประเภทซึ่งเก็บเมตาดาต้าเอกสารที่ดึงมา. คุณสมบัติ `DocumentInfo.PageCount` คืนค่าจำนวนหน้าทั้งหมด. ค่านี้คำนวณจากส่วนหัวของไฟล์, ทำให้เครื่องยนต์สามารถกำหนดจำนวนหน้าโดยไม่ต้องโหลดเอกสารทั้งหมด, ดังนั้นแม้ PDF ขนาด 300‑หน้า ก็จะถูกประมวลผลในเวลาเพียงไม่กี่มิลลิวินาที.

### วิธีอ่านเมตาดาต้าจาก stream?
`RedactionEngine` โหลดเอกสารจากเส้นทางไฟล์หรือ stream และให้ความสามารถในการดึงเมตาดาต้า. ส่งอินสแตนซ์ `Stream` (เช่น `MemoryStream`) ไปยัง `RedactionEngine` แทนเส้นทางไฟล์. เครื่องยนต์อ่านส่วนหัวของ stream, ดึงเมตาดาต้า, แล้วทำการปิด stream โดยอัตโนมัติ, เพื่อให้การใช้หน่วยความจำน้อยที่สุดและการประมวลผลเร็วแม้ไฟล์ขนาดใหญ่.

### วิธีดึงเมตาดาต้าใน C#?
ใช้รูปแบบต่อไปนี้ (ไม่ต้องใช้บล็อกโค้ดสำหรับการปฏิบัติตาม):  
1. สร้างอินสแตนซ์ `RedactionEngine` ด้วยเส้นทางไฟล์หรือ stream.  
2. เรียก `GetDocumentInfo()`.  
3. เข้าถึงคุณสมบัติเช่น `Author`, `Title`, `CreatedDate`, และ `PageCount`.  

ขั้นตอนเหล่านี้จะให้สแนปช็อตเมตาดาต้าที่สมบูรณ์พร้อมใช้ในตรรกะธุรกิจ.

## ปัญหาทั่วไปและวิธีแก้ไข
- **Metadata ปรากฏว่าง** – ตรวจสอบให้แน่ใจว่าไฟล์ต้นทางมีคุณสมบัติที่ฝังอยู่จริง; บางการสแกนอาจลบเมตาดาต้า.  
- **Unsupported format error** – ตรวจสอบให้แน่ใจว่านามสกุลไฟล์อยู่ในตารางรูปแบบที่รองรับของ GroupDocs.Redaction (มีมากกว่า 100 รายการ).  
- **Performance slowdown on large files** – ใช้แฟล็ก `LoadOptions` `ReadOnly = true` เพื่อหลีกเลี่ยงการจัดสรรทรัพยากรที่ไม่จำเป็น.

## คำถามที่พบบ่อย

**Q: ฉันสามารถดึงเมตาดาต้าจาก PDF ที่ป้องกันด้วยรหัสผ่านได้หรือไม่?**  
A: ใช่. ให้รหัสผ่านเมื่อสร้าง `RedactionEngine`; API จะถอดรหัสส่วนหัวและคืนค่าเมตาดาต้า.

**Q: API รองรับการประมวลผลแบบกลุ่มของหลายไฟล์หรือไม่?**  
A: แน่นอน. วนลูปผ่านคอลเลกชันไฟล์ของคุณ, สร้าง `RedactionEngine` สำหรับแต่ละไฟล์, แล้วเรียก `GetDocumentInfo()`—เครื่องยนต์มีน้ำหนักเบาพอสำหรับไฟล์หลายพันไฟล์.

**Q: จะเกิดอะไรขึ้นหากเอกสารไม่มีเมตาดาต้า?**  
A: คุณสมบัติเกี่ยวข้องจะคืนค่า `null` หรือค่าดีฟอลต์; คุณสามารถตรวจสอบ `null` อย่างปลอดภัยก่อนใช้งาน.

**Q: สามารถแก้ไขเมตาดาต้าหลังจากดึงได้หรือไม่?**  
A: GroupDocs.Redaction มุ่งเน้นที่การลบข้อมูล, ไม่ใช่การแก้ไขเมตาดาต้า. ใช้ GroupDocs.Metadata หรือไลบรารีอื่นสำหรับสถานการณ์การเขียนกลับ.

**Q: .NET เวอร์ชันใดที่รองรับอย่างเป็นทางการ?**  
A: .NET Framework 4.7.2+, .NET Core 3.1+, .NET 5+, และ .NET 6+ รองรับเต็มรูปแบบ.

## สรุป
ด้วยการเชี่ยวชาญเทคนิค **extract document metadata** คุณจะทำให้แอปพลิเคชันของคุณสามารถตัดสินใจการลบข้อมูลได้อย่างชาญฉลาด, บังคับใช้นโยบายการปฏิบัติตาม, และปรับปรุงความเร็วการประมวลผลโดยรวม. สำรวจบทแนะนำที่เชื่อมโยงด้านล่างเพื่อดูการนำไปใช้จริงสำหรับตัวอย่างหน้าเดียว, การดึงจาก stream, และการดึงเมตาดาต้าเต็มรูปแบบ.

## บทแนะนำที่พร้อมใช้งาน

### [สร้างตัวอย่างเอกสารหน้าเดียวโดยใช้ GroupDocs.Redaction .NET](./create-single-page-preview-groupdocs-redaction-net/)
เรียนรู้วิธีสร้างตัวอย่างเอกสารหน้าเดียวโดยใช้ GroupDocs.Redaction สำหรับ .NET. คู่มือนี้ให้คำแนะนำทีละขั้นตอน, เคล็ดลับการกำหนดค่า, และการใช้งานจริง.

### [วิธีดึงเมตาดาต้าเอกสารจาก Streams โดยใช้ GroupDocs.Redaction .NET](./extract-document-info-streams-groupdocs-redaction-dotnet/)
เรียนรู้วิธีดึงเมตาดาต้าเอกสารอย่างมีประสิทธิภาพโดยใช้ GroupDocs.Redaction สำหรับ .NET. คู่มือนี้ครอบคลุมการตั้งค่า, ตัวอย่างโค้ด, และการใช้งานจริง.

### [เชี่ยวชาญการดึงเมตาดาต้าเอกสารด้วย GroupDocs.Redaction .NET API](./groupdocs-redaction-net-document-metadata-retrieval/)
เรียนรู้วิธีดึงเมตาดาต้าเอกสารอย่างมีประสิทธิภาพโดยใช้ GroupDocs.Redaction .NET. ปรับปรุงการจัดการเอกสารและกระบวนการปฏิบัติตามของคุณ.

## แหล่งข้อมูลเพิ่มเติม

- [เอกสาร GroupDocs.Redaction สำหรับ .NET](https://docs.groupdocs.com/redaction/net/)
- [อ้างอิง API ของ GroupDocs.Redaction สำหรับ .NET](https://reference.groupdocs.com/redaction/net/)
- [ดาวน์โหลด GroupDocs.Redaction สำหรับ .NET](https://releases.groupdocs.com/redaction/net/)
- [ฟอรั่ม GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)
- [การสนับสนุนฟรี](https://forum.groupdocs.com/)
- [ใบอนุญาตชั่วคราว](https://purchase.groupdocs.com/temporary-license/)

---

**อัปเดตล่าสุด:** 2026-06-06  
**ทดสอบด้วย:** GroupDocs.Redaction 4.0 for .NET  
**ผู้เขียน:** GroupDocs

## บทแนะนำที่เกี่ยวข้อง

- [บทแนะนำการโหลดเอกสารด้วย GroupDocs.Redaction สำหรับ .NET](/redaction/net/document-loading/)
- [วิธีลบเมตาดาต้าเอกสารโดยใช้ GroupDocs.Redaction สำหรับ .NET - คู่มือครบถ้วน](/redaction/net/metadata-redaction/redact-metadata-groupdocs-redaction-net/)
- [สร้างตัวอย่างเอกสารหน้าเดียวโดยใช้ GroupDocs.Redaction .NET](/redaction/net/document-information/create-single-page-preview-groupdocs-redaction-net/)