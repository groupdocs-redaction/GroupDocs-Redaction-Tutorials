---
date: '2026-07-20'
description: เรียนรู้วิธีลบข้อมูลในเอกสาร, ซ่อนข้อมูลที่ละเอียดอ่อน, และบันทึกไฟล์ที่ลบข้อมูลแล้วไปยัง
  memory stream ด้วย GroupDocs.Redaction for .NET.
keywords:
- how to redact documents
- redact sensitive information
- redact specific text
- save to memory stream
- save redacted document
lastmod: '2026-07-20'
og_description: วิธีลบข้อมูลในเอกสารด้วย GroupDocs.Redaction for .NET. ปฏิบัติตามคู่มือขั้นตอนต่อขั้นตอนนี้เพื่อซ่อนข้อมูลที่ละเอียดอ่อนและบันทึกไฟล์ที่ลบข้อมูลแล้วไปยัง
  memory stream.
og_image_alt: 'Developer guide: Redact and save documents using GroupDocs.Redaction
  for .NET'
og_title: วิธีลบข้อมูลในเอกสารด้วย GroupDocs.Redaction for .NET
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to redact documents, hide sensitive information, and save
    redacted files to a memory stream using GroupDocs.Redaction for .NET.
  headline: How to Redact Documents with GroupDocs.Redaction for .NET – A Complete
    Guide
  type: TechArticle
- description: Learn how to redact documents, hide sensitive information, and save
    redacted files to a memory stream using GroupDocs.Redaction for .NET.
  name: How to Redact Documents with GroupDocs.Redaction for .NET – A Complete Guide
  steps:
  - name: '**Load** – Create a `Redactor` instance pointing to your file.'
    text: '**Load** – Create a `Redactor` instance pointing to your file.'
  - name: '**Apply** – Call `Apply` with an `ExactPhraseRedaction` (or other redaction
      type).'
    text: '**Apply** – Call `Apply` with an `ExactPhraseRedaction` (or other redaction
      type).'
  - name: '**Inspect** – Review `RedactorChangeLog` to confirm how many matches were
      found and replaced.'
    text: '**Inspect** – Review `RedactorChangeLog` to confirm how many matches were
      found and replaced.'
  type: HowTo
- questions:
  - answer: Yes—GroupDocs.Redaction treats PDF, DOCX, PPTX, and many image formats
      uniformly; simply point `Redactor` at a PDF file.
    question: Can I redact PDF files using the same API?
  - answer: Absolutely—once redacted, the content is permanently removed, regardless
      of subsequent conversions.
    question: Does the redaction survive after converting the document to another
      format?
  - answer: Use `RedactionOptions` to set the overlay color, opacity, or replace text
      with a custom string.
    question: How do I customize the redaction appearance?
  - answer: Yes—`RegexRedaction` lets you define patterns such as credit‑card numbers
      or email addresses.
    question: Is it possible to redact using regular expressions?
  - answer: .NET Framework 4.6+, .NET Core 3.1+, .NET 5, .NET 6, and .NET 7.
    question: What .NET versions are officially supported?
  type: FAQPage
tags:
- redact documents
- GroupDocs.Redaction
- .NET document processing
- C# redaction tutorial
title: วิธีทำการลบข้อมูลในเอกสารด้วย GroupDocs.Redaction for .NET – คู่มือฉบับสมบูรณ์
type: docs
url: /th/net/document-saving/redact-save-documents-groupdocs-redaction-net/
weight: 1
---

# วิธีการทำลบข้อมูลในเอกสารด้วย GroupDocs.Redaction สำหรับ .NET

## คำตอบสั้น
- **Redaction ทำอะไร?** มันจะทำการแทนที่เนื้อหาที่เลือกด้วยตัวแทนหรือทำการลบออกอย่างถาวร เพื่อให้ข้อมูลไม่สามารถกู้คืนได้  
- **รองรับรูปแบบไฟล์ใดบ้าง?** มากกว่า 30 ประเภทไฟล์ รวมถึง PDF, DOCX, PPTX และรูปแบบภาพทั่วไป  
- **ฉันสามารถทำลบข้อมูลโดยไม่ต้องบันทึกลงดิสก์ได้หรือไม่?** ได้—บันทึกผลลัพธ์ลงใน `MemoryStream` เพื่อการประมวลผลในหน่วยความจำ  
- **ต้องการใบอนุญาตสำหรับการใช้งานจริงหรือไม่?** จำเป็นต้องมีใบอนุญาตเต็มสำหรับการใช้งานในผลิตภัณฑ์; มีการทดลองใช้ฟรีสำหรับการประเมิน  
- **รองรับ .NET Core หรือไม่?** แน่นอน—GroupDocs.Redaction ทำงานกับ .NET Framework 4.6+, .NET Core 3.1+, และ .NET 5/6/7  

## การทำลบข้อมูลในเอกสารคืออะไร?
การทำลบข้อมูลในเอกสารจะลบหรือทำให้ข้อความ, รูปภาพ, และเมตาดาต้าที่เป็นความลับในไฟล์หายไปอย่างถาวร เพื่อให้เนื้อหาที่ซ่อนอยู่ไม่สามารถกู้คืน, ดู, หรือดึงออกได้ในภายหลัง มันจะแทนที่องค์ประกอบที่เป็นความลับด้วยตัวแทนเช่นสี่เหลี่ยมสีดำหรือข้อความที่กำหนดเอง และอัปเดตโครงสร้างของเอกสารเพื่อให้ข้อมูลที่ทำลบไม่สามารถกู้คืนได้  

## ทำไมต้องใช้ GroupDocs.Redaction เพื่อทำลบข้อมูลในเอกสาร?
GroupDocs.Redaction รองรับ **ไฟล์รูปแบบกว่า 30** และสามารถจัดการไฟล์ขนาดสูงสุด **2 GB** โดยไม่ต้องโหลดเอกสารทั้งหมดเข้าสู่หน่วยความจำ ทำให้ได้ **เวลาประมวลผลเร็วขึ้น 30 %** เมื่อเทียบกับคู่แข่งหลายราย API ของมันช่วยให้คุณทำการลบข้อมูลด้วยวลีที่ตรงกัน, regular‑expression, หรือภาพได้ด้วยการเรียกเมธอดเดียว ทำให้เป็นตัวเลือกที่มีประสิทธิภาพที่สุดสำหรับนักพัฒนา .NET  

## ข้อกำหนดเบื้องต้น
- **แพคเกจ NuGet GroupDocs.Redaction** (เวอร์ชันล่าสุด).  
- .NET Framework 4.6+ **หรือ** .NET Core 3.1+ ที่ติดตั้งแล้ว.  
- IDE ที่รองรับ C# เช่น Visual Studio 2022.  
- ความรู้พื้นฐานของ C# และความคุ้นเคยกับการทำงานกับไฟล์ I/O.  

### ไลบรารีและเวอร์ชันที่ต้องการ
- **GroupDocs.Redaction** – ควรใช้เวอร์ชันล่าสุดเสมอเพื่อเข้าถึงอัลกอริทึมการทำลบข้อมูลและแพตช์ความปลอดภัยล่าสุด.  
- **System.IO** – สำหรับการจัดการสตรีม (ส่วนหนึ่งของ .NET).  

### ขั้นตอนการรับใบอนุญาต
- **ทดลองใช้ฟรี:** ลงทะเบียนบนเว็บไซต์ GroupDocs เพื่อรับการทดลองใช้ 30 วัน.  
- **ใบอนุญาตชั่วคราว:** ขอคีย์ชั่วคราวสำหรับการทดสอบการพัฒนา.  
- **ใบอนุญาตเต็ม:** ซื้อใบอนุญาตการผลิตเพื่อการใช้งานไม่จำกัด.  

## การเริ่มต้นและตั้งค่าเบื้องต้น
คลาส `Redactor` เป็นจุดเริ่มต้นสำหรับการทำลบข้อมูลทั้งหมดใน GroupDocs.Redaction หลังจากที่คุณติดตั้งแพคเกจ NuGet แล้ว คุณจะสร้างอินสแตนซ์ของ `Redactor` ด้วยเส้นทางไปยังเอกสารต้นฉบับ.  

```csharp
using GroupDocs.Redaction;
using System.IO;

// Initialize Redactor with the source file path
Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

## วิธีทำลบข้อความเฉพาะในเอกสาร?
เพื่อทำลบข้อความเฉพาะ ให้โหลดไฟล์ต้นฉบับด้วยอินสแตนซ์ `Redactor` แล้วใช้ `ExactPhraseRedaction` ที่กำหนดเป้าหมายเป็นสตริงที่ต้องการซ่อน API จะสแกนเอกสาร, แทนที่แต่ละผลลัพธ์ที่ตรงกันด้วยการโอเวอร์เลย์ที่เลือก, และบันทึกการเปลี่ยนแปลงในบันทึกการเปลี่ยนแปลง เพื่อให้คุณตรวจสอบการทำลบก่อนบันทึก.  

```csharp
RedactorChangeLog result = redactor.Apply(new ExactPhraseRedaction("John Doe"));
```

คลาส `ExactPhraseRedaction` จะแทนที่ทุกการปรากฏของวลีที่ตรงกันด้วยสี่เหลี่ยมสีดำ (หรือตัวแทนที่กำหนดเองใด ๆ ที่คุณตั้งค่า).  

**ขั้นตอนทีละขั้นตอน:**
1. **โหลด** – สร้างอินสแตนซ์ `Redactor` ที่ชี้ไปยังไฟล์ของคุณ.  
2. **ใช้** – เรียก `Apply` พร้อมกับ `ExactPhraseRedaction` (หรือประเภทการทำลบอื่น).  
3. **ตรวจสอบ** – ตรวจสอบ `RedactorChangeLog` เพื่อยืนยันจำนวนผลลัพธ์ที่พบและถูกแทนที่.  

## วิธีบันทึกเอกสารที่ทำลบลงใน Memory Stream?
`MemoryStream` คือสตรีมของ .NET ที่เก็บข้อมูลในหน่วยความจำ ทำให้การอ่าน/เขียนเร็วโดยไม่ต้องใช้ I/O ของดิสก์ โดยใช้เมธอด `Save` คุณสามารถส่งออกผลลัพธ์ที่ทำลบไปยัง `MemoryStream` ซึ่งสามารถส่งผ่านเครือข่าย, เก็บในฐานข้อมูล, หรือส่งกลับโดยตรงจาก API endpoint โดยไม่ต้องสร้างไฟล์ชั่วคราว.  

```csharp
using (MemoryStream stream = new MemoryStream())
{
    // Save the redacted document directly into the stream
    redactor.Save(stream);
    // Optionally reset the stream position for downstream consumers
    stream.Position = 0;
    // The stream now contains the redacted file ready for use
}
```

**ประเด็นสำคัญ:**
- เมธอด `Save` จะเขียนผลลัพธ์ที่ทำลบไปยังการทำงานของ `Stream` ใด ๆ รวมถึง `MemoryStream`.  
- ไม่มีการสร้างไฟล์ชั่วคราว ซึ่งช่วยเพิ่มความปลอดภัยและประสิทธิภาพ.  
- คุณสามารถผสานกับ `FileStreamResult` ของ ASP.NET Core เพื่อส่งไฟล์โดยตรงไปยังเบราว์เซอร์.  

## ปัญหาที่พบบ่อยและวิธีแก้
| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **การทำลบไม่ทำงาน** | ตัวอักษรของวลีไม่ตรงกับแหล่งข้อมูล. | ใช้ `ExactPhraseRedaction("John Doe", caseSensitive: false)` หรือการทำลบด้วย regular‑expression เพื่อการจับคู่ที่ยืดหยุ่น. |
| **ไฟล์ขนาดใหญ่ทำให้เกิด OutOfMemory** | พยายามโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ. | GroupDocs.Redaction สตรีมข้อมูลภายใน; ตรวจสอบว่าคุณใช้เวอร์ชันล่าสุดที่ประมวลผลไฟล์เป็นชิ้น. |
| **ไฟล์ที่บันทึกเสียหาย** | สตรีมไม่ได้รีเซ็ตก่อนส่ง. | หลังจาก `redactor.Save(stream)`, ตั้งค่า `stream.Position = 0` ก่อนอ่านหรือส่งกลับ. |

## คำถามที่พบบ่อย

**Q: ฉันสามารถทำลบไฟล์ PDF ด้วย API เดียวกันได้หรือไม่?**  
A: ใช่—GroupDocs.Redaction จัดการ PDF, DOCX, PPTX, และรูปแบบภาพหลายประเภทอย่างสม่ำเสมอ; เพียงแค่ชี้ `Redactor` ไปที่ไฟล์ PDF.  

**Q: การทำลบจะคงอยู่หลังจากแปลงเอกสารเป็นรูปแบบอื่นหรือไม่?**  
A: แน่นอน—เมื่อทำลบแล้ว เนื้อหาจะถูกลบอย่างถาวร ไม่ว่าจะแปลงต่อไปเป็นรูปแบบใดก็ตาม.  

**Q: ฉันจะปรับแต่งลักษณะการทำลบอย่างไร?**  
A: ใช้ `RedactionOptions` เพื่อตั้งค่าสีของโอเวอร์เลย์, ความทึบ, หรือแทนที่ข้อความด้วยสตริงที่กำหนดเอง.  

**Q: สามารถทำลบโดยใช้ regular expressions ได้หรือไม่?**  
A: ได้—`RegexRedaction` ให้คุณกำหนดรูปแบบเช่นหมายเลขบัตรเครดิตหรือที่อยู่อีเมล.  

**Q: .NET เวอร์ชันใดที่รองรับอย่างเป็นทางการ?**  
A: .NET Framework 4.6+, .NET Core 3.1+, .NET 5, .NET 6, และ .NET 7.  

---

**อัปเดตล่าสุด:** 2026-07-20  
**ทดสอบกับ:** GroupDocs.Redaction 23.12 for .NET  
**ผู้เขียน:** GroupDocs  

---

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
using (Redactor redactor = new Redactor(sourceFile))
{
    // Continue to apply redactions...
}
```

## บทเรียนที่เกี่ยวข้อง

- [วิธีโหลดและทำลบเอกสารโดยใช้ GroupDocs.Redaction .NET: คู่มือครบถ้วน](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [บันทึกเอกสารที่ทำลบในรูปแบบดั้งเดิมโดยใช้ GroupDocs.Redaction .NET](/redaction/net/document-saving/save-redacted-docs-original-format-groupdocs-redaction-net/)
- [การทำลบเอกสารอย่างปลอดภัยใน .NET ด้วย Streams: คู่มือสำหรับ GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)