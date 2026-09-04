---
date: '2026-07-20'
description: เรียนรู้วิธีแสดงรายการรูปแบบโดยใช้ GroupDocs.Redaction .NET, ผสานคุณลักษณะนี้เข้ากับกระบวนการทำงานเอกสารของคุณ,
  และเพิ่มประสิทธิภาพ
keywords:
- how to list formats
- GroupDocs.Redaction supported formats
- .NET document processing
lastmod: '2026-07-20'
og_description: ค้นพบวิธีแสดงรายการรูปแบบโดยใช้ GroupDocs.Redaction .NET, ดูคำแนะนำแบบขั้นตอนต่อขั้นตอน,
  และรับเคล็ดลับสำหรับประสิทธิภาพสูงสุดในแอปพลิเคชัน .NET ของคุณ
og_image_alt: Guide showing how to list supported file formats with GroupDocs.Redaction
  in a .NET project
og_title: วิธีแสดงรายการรูปแบบด้วย GroupDocs.Redaction .NET
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to list formats using GroupDocs.Redaction .NET, integrate
    the feature into your document workflow, and improve performance.
  headline: How to List Formats with GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to list formats using GroupDocs.Redaction .NET, integrate
    the feature into your document workflow, and improve performance.
  name: How to List Formats with GroupDocs.Redaction .NET
  steps:
  - name: '**Document Management Systems** – Validate uploads against the supported
      list to prevent processing failures.'
    text: '**Document Management Systems** – Validate uploads against the supported
      list to prevent processing failures.'
  - name: '**Content Security** – Apply redaction rules only to file types that the
      engine can safely modify.'
    text: '**Content Security** – Apply redaction rules only to file types that the
      engine can safely modify.'
  - name: '**Batch Processing Pipelines** – Filter large file batches before invoking
      redaction, saving CPU and memory.'
    text: '**Batch Processing Pipelines** – Filter large file batches before invoking
      redaction, saving CPU and memory.'
  - name: '**How do I install GroupDocs.Redaction for .NET?**'
    text: '**How do I install GroupDocs.Redaction for .NET?**'
  - name: '**What are some common issues when retrieving supported formats?**'
    text: '**What are some common issues when retrieving supported formats?**'
  - name: '**Can I use this feature with non‑.NET applications?**'
    text: '**Can I use this feature with non‑.NET applications?**'
  - name: '**How can I optimise performance when using GroupDocs.Redaction?**'
    text: '**How can I optimise performance when using GroupDocs.Redaction?**'
  - name: '**What file types does GroupDocs.Redaction support?**'
    text: '**What file types does GroupDocs.Redaction support?**'
  type: HowTo
- questions:
  - answer: Yes, `FileType.GetSupportedFileFormats()` is static and does not require
      a `Redactor` object.
    question: Can I retrieve the format list without initializing a Redactor instance?
  - answer: The method returns all formats that the library can both read and write;
      each `FileType` includes a `CanRead` and `CanWrite` flag.
    question: Does the list include both input and output formats?
  - answer: GroupDocs releases format updates with each library version; checking
      the list at runtime ensures you always have the latest set.
    question: How often is the supported format list updated?
  - answer: Yes, filter the collection where `format.Extension == ".pdf"` or where
      `format.Name.Contains("PDF")`.
    question: Is there a way to filter only PDF‑compatible formats?
  - answer: The method requires .NET Core 3.1 or later; earlier runtimes are not supported.
    question: Will this approach work on .NET Core 2.1?
  type: FAQPage
tags:
- how to list formats
- GroupDocs.Redaction
- .NET file handling
title: วิธีแสดงรายการรูปแบบด้วย GroupDocs.Redaction .NET
type: docs
url: /th/net/format-handling/groupdocs-redaction-net-supported-formats-listing/
weight: 1
---

# วิธีการแสดงรายการรูปแบบด้วย GroupDocs.Redaction .NET

การจัดการกับประเภทเอกสารที่หลากหลายเป็นความเป็นจริงในชีวิตประจำวันของนักพัฒนาที่สร้างแอปพลิเคชันที่เน้นเอกสาร ในบทเรียนนี้คุณจะได้เรียนรู้ **วิธีการแสดงรายการรูปแบบ** ที่ GroupDocs.Redaction .NET สามารถจัดการได้ เพื่อให้คุณสามารถตรวจสอบไฟล์ก่อนประมวลผล แสดงตัวเลือกที่แม่นยำให้ผู้ใช้ และทำให้กระบวนการทำงานของคุณมีประสิทธิภาพ

## บทนำ

การจัดการเอกสารอย่างมีประสิทธิภาพเริ่มต้นด้วยการรู้ว่าไลบรารีของคุณรองรับไฟล์ประเภทใดบ้าง GroupDocs.Redaction มีเมธอดในตัวที่ช่วยดึงข้อมูลนี้ออกมา ทำให้คุณสามารถสร้าง UI แบบไดนามิก บังคับใช้กฎการตรวจสอบ และหลีกเลี่ยงข้อผิดพลาดขณะรันได้ ด้านล่างนี้คุณจะพบทุกอย่างที่ต้องการเพื่อเริ่มต้น ตั้งแต่การติดตั้งจนถึงโค้ดตัวอย่างและเคล็ดลับด้านประสิทธิภาพ

### คำตอบอย่างรวดเร็ว
- **“how to list formats” หมายถึงอะไร?** หมายถึงการดึงคอลเลกชันของส่วนขยายไฟล์ที่ GroupDocs.Redaction สามารถประมวลผลได้  
- **ต้องมีใบอนุญาตหรือไม่?** ใช่ ต้องมีใบอนุญาต GroupDocs.Redaction ที่ถูกต้องสำหรับการใช้งานในสภาพแวดล้อมการผลิต  
- **รองรับเวอร์ชัน .NET ใดบ้าง?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7  
- **มีรูปแบบกี่ประเภท?** รองรับรูปแบบการนำเข้าและส่งออกกว่า 30 ประเภทโดยพร้อมใช้งาน  
- **ต้องการการตั้งค่าเพิ่มเติมหรือไม่?** ไม่จำเป็นต้องตั้งค่าเพิ่มเติมนอกจากการเริ่มต้นไลบรารีตามปกติ

## “how to list formats” คืออะไร

มันเกี่ยวข้องกับการเรียก API FileType ของไลบรารีเพื่อรับคอลเลกชันที่แต่ละรายการประกอบด้วยส่วนขยายไฟล์และชื่อที่อ่านเข้าใจได้ นักพัฒนาจึงสามารถวนลูปคอลเลกชันนี้เพื่อสร้างกฎการตรวจสอบ เติมข้อมูลลงใน dropdown ของ UI หรือบันทึกรูปแบบที่รองรับ เพื่อให้แน่ใจว่าเอกสารที่เข้ากันได้เท่านั้นจะถูกประมวลผล

## ทำไมต้องแสดงรายการรูปแบบด้วย GroupDocs.Redaction?

GroupDocs.Redaction รองรับ **30+** ประเภทไฟล์ที่แตกต่างกัน รวมถึง PDF, DOCX, PPTX และรูปแบบภาพต่าง ๆ ทำให้คุณสามารถจัดการเอกสารระดับองค์กรส่วนใหญ่ได้โดยไม่ต้องใช้ตัวแปลงจากบุคคลที่สาม การแสดงรายการรูปแบบเหล่านี้โดยโปรแกรมจะช่วยขจัดการคาดเดา ลดจำนวนตั๋วสนับสนุน และทำให้แน่ใจว่าไฟล์ที่เข้ากันได้เท่านั้นจะเข้าสู่กระบวนการประมวลผลของคุณ

## ข้อกำหนดเบื้องต้น

- **GroupDocs.Redaction for .NET** – ดาวน์โหลดแพ็กเกจล่าสุดจากเว็บไซต์อย่างเป็นทางการ  
- **.NET Framework or .NET Core** – เข้ากันได้กับสภาพแวดล้อมการพัฒนาของคุณ  
- **Visual Studio** (หรือ IDE ที่รองรับ C# ใด ๆ)  
- ความคุ้นเคยพื้นฐานกับไวยากรณ์ C#

## การตั้งค่า GroupDocs.Redaction สำหรับ .NET

### .NET CLI
`dotnet add package GroupDocs.Redaction`

### Package Manager
`Install-Package GroupDocs.Redaction`

### NuGet Package Manager UI
- ค้นหา **“GroupDocs.Redaction”** และติดตั้งเวอร์ชันล่าสุด

### การรับใบอนุญาต
GroupDocs มีให้ทดลองใช้ฟรี ใบอนุญาตชั่วคราวสำหรับการประเมินผล หรือทางเลือกการซื้อเต็มรูปแบบ เยี่ยมชมเว็บไซต์ของ GroupDocs เพื่อรับไฟล์ใบอนุญาตที่เหมาะสม

### การเริ่มต้นและตั้งค่าเบื้องต้น
หลังจากเพิ่มแพ็กเกจแล้ว ให้อ้างอิงเนมสเปซและสร้างอินสแตนซ์ `Redactor`:

```csharp
using GroupDocs.Redaction;

// Initialize with a license file (replace path as needed)
Redactor redactor = new Redactor("path/to/license/file.lic");
```

## คู่มือการใช้งาน

### วิธีการแสดงรายการรูปแบบด้วย GroupDocs.Redaction .NET?
โหลดไลบรารี เรียกตัวช่วยแบบสแตติก แล้วจัดเรียงผลลัพธ์ — ทำให้คุณได้คอลเลกชันพร้อมใช้ในเพียงสองบรรทัดของโค้ด ใช้ `FileType.GetSupportedFileFormats()` เพื่อดึง `IEnumerable<FileType>` ที่รวมส่วนขยายและชื่อที่แสดงของแต่ละรูปแบบ จากนั้นเรียงตามส่วนขยายเพื่อให้ได้รายการ UI ที่เรียบร้อย

### การดึงรูปแบบไฟล์ที่รองรับ

#### ภาพรวม
เป้าหมายคือการได้รายการประเภทไฟล์ที่ GroupDocs.Redaction สามารถจัดการได้ เพื่อใช้ในตรรกะการตรวจสอบ UI dropdown หรือกลไกการบันทึกบันทึก

#### การดำเนินการตามขั้นตอน

**1. ดึงประเภทไฟล์ที่รองรับ**  
`FileType.GetSupportedFileFormats()` จะคืนค่าทุกรูปแบบที่ไลบรารีรู้จัก เมธอดนี้เป็นส่วนหนึ่งของคลาส `GroupDocs.Redaction.FileType` ซึ่งบรรจุเมตาดาต้าเช่นส่วนขยายไฟล์และชื่อที่เป็นมิตรต่อผู้ใช้

**2. แสดงประเภทไฟล์ที่รองรับ**  
วนลูปคอลเลกชันและพิมพ์แต่ละรูปแบบพร้อมส่วนขยายและคำอธิบาย ตัวอย่างโค้ดแบบอินไลน์:

```csharp
var formats = FileType.GetSupportedFileFormats()
                      .OrderBy(f => f.Extension);

foreach (var format in formats)
{
    Console.WriteLine($"{format.Extension} – {format.Name}");
}
```

สคริปต์นี้จะพิมพ์รายการที่จัดเรียงอย่างเป็นระเบียบ เช่น “.pdf – Portable Document Format” ทำให้เหมาะสำหรับเติมข้อมูลลงใน UI

### เคล็ดลับการแก้ไขปัญหา
- **แพ็กเกจหาย** – ตรวจสอบการอ้างอิงแพ็กเกจ NuGet และทำการ restore หากจำเป็น  
- **เส้นทางใบอนุญาตไม่ถูกต้อง** – ตรวจสอบให้แน่ใจว่าไฟล์ใบอนุญาตถูกคัดลอกไปยังไดเรกทอรี output หรือระบุเส้นทางแบบเต็ม  
- **ส่วนขยายที่ไม่รองรับ** – หากรูปแบบไม่ปรากฏในรายการ ให้ตรวจสอบว่าคุณใช้เวอร์ชันไลบรารีล่าสุด เนื่องจากเวอร์ชันใหม่มักเพิ่มรูปแบบเพิ่มเติม

## การประยุกต์ใช้งานจริง
การเข้าใจรูปแบบไฟล์ที่รองรับเปิดโอกาสให้คุณทำหลายสถานการณ์จริงได้:

1. **ระบบจัดการเอกสาร** – ตรวจสอบการอัปโหลดกับรายการที่รองรับเพื่อป้องกันความล้มเหลวในการประมวลผล  
2. **ความปลอดภัยของเนื้อหา** – ใช้กฎการลบข้อมูลเฉพาะกับประเภทไฟล์ที่เอนจินสามารถแก้ไขได้อย่างปลอดภัย  
3. **สายการประมวลผลแบบแบตช์** – กรองไฟล์จำนวนมากก่อนเรียกใช้การลบข้อมูล เพื่อประหยัด CPU และหน่วยความจำ

## พิจารณาด้านประสิทธิภาพ
- **ขนาดหน่วยความจำ** – การแสดงรายการรูปแบบเป็นการดำเนินการที่ใช้ทรัพยากรน้อย ไม่ได้โหลดเอกสารใด ๆ เข้าไปในหน่วยความจำ  
- **การทำงานแบบแบตช์** – เมื่อประมวลผลหลายร้อยไฟล์ ให้ดึงรายการรูปแบบครั้งเดียวแล้วนำกลับมาใช้ซ้ำ เพื่อลดการเรียกซ้ำ  
- **ความปลอดภัยของเธรด** – `FileType.GetSupportedFileFormats()` ปลอดภัยต่อการเรียกจากหลายเธรดพร้อมกันและไม่ต้องทำการซิงโครไนซ์

## สรุป
คุณมีแนวทางครบถ้วนและพร้อมใช้งานสำหรับ **วิธีการแสดงรายการรูปแบบ** ด้วย GroupDocs.Redaction .NET การผสานคุณลักษณะนี้จะช่วยเพิ่มการตรวจสอบ ปรับปรุงประสบการณ์ผู้ใช้ และทำให้สายการทำงานของคุณแข็งแรงยิ่งขึ้น

### ขั้นตอนต่อไป
- สำรวจ API `Redactor` เพื่อใช้กฎการลบข้อมูลตามประเภทไฟล์  
- ผสานรายการรูปแบบกับ dropdown ฝั่งหน้าเว็บเพื่อการเลือกไฟล์ที่ราบรื่น  
- ตรวจสอบคู่มือด้านประสิทธิภาพเพื่อปรับแต่งงานแบตช์ขนาดใหญ่

## คำถามที่พบบ่อย

**Q: สามารถดึงรายการรูปแบบได้โดยไม่ต้องสร้างอินสแตนซ์ Redactor หรือไม่?**  
A: ใช่ `FileType.GetSupportedFileFormats()` เป็นเมธอดสแตติกและไม่ต้องการอ็อบเจกต์ `Redactor`

**Q: รายการนี้รวมทั้งรูปแบบการนำเข้าและส่งออกหรือไม่?**  
A: เมธอดนี้คืนค่าทุกรูปแบบที่ไลบรารีสามารถอ่านและเขียนได้; แต่ละ `FileType` มีแฟล็ก `CanRead` และ `CanWrite`

**Q: รายการรูปแบบที่รองรับอัปเดตบ่อยแค่ไหน?**  
A: GroupDocs ปล่อยอัปเดตรูปแบบพร้อมกับแต่ละเวอร์ชันของไลบรารี; การตรวจสอบรายการที่ runtime จะทำให้คุณได้ชุดล่าสุดเสมอ

**Q: มีวิธีกรองเฉพาะรูปแบบที่เข้ากันได้กับ PDF หรือไม่?**  
A: มี สามารถกรองคอลเลกชันโดยใช้ `format.Extension == ".pdf"` หรือ `format.Name.Contains("PDF")`

**Q: วิธีนี้ทำงานบน .NET Core 2.1 ได้หรือไม่?**  
A: เมธอดต้องการ .NET Core 3.1 หรือใหม่กว่า; เวอร์ชันที่เก่ากว่าไม่ได้รับการสนับสนุน

## ส่วนคำถามที่พบบ่อย
1. **วิธีติดตั้ง GroupDocs.Redaction สำหรับ .NET?**  
   ใช้คำสั่ง CLI `dotnet add package GroupDocs.Redaction` หรือทำการติดตั้งผ่าน NuGet Package Manager UI  
2. **ปัญหาที่พบบ่อยเมื่อดึงรูปแบบที่รองรับคืออะไร?**  
   ตรวจสอบให้แน่ใจว่าการพึ่งพาทั้งหมดถูก restore และคุณอ้างอิงเนมสเปซ `GroupDocs.Redaction` อย่างถูกต้อง  
3. **สามารถใช้ฟีเจอร์นี้กับแอปพลิเคชันที่ไม่ใช่ .NET ได้หรือไม่?**  
   บทเรียนนี้มุ่งเน้นที่ .NET แต่ GroupDocs มี API ที่คล้ายกันสำหรับ Java, Python และแพลตฟอร์มอื่น ๆ  
4. **จะเพิ่มประสิทธิภาพการใช้ GroupDocs.Redaction อย่างไร?**  
   ใช้รายการรูปแบบซ้ำ, หลีกเลี่ยงการโหลดเอกสารเต็มเมื่อเพียงตรวจสอบความเข้ากันได้, และตรวจสอบการใช้หน่วยความจำระหว่างงานแบตช์  
5. **GroupDocs.Redaction รองรับไฟล์ประเภทใดบ้าง?**  
   ไลบรารีรองรับกว่า 30 รูปแบบ รวมถึง PDF, DOCX, PPTX, XLSX, BMP, PNG, JPEG และอื่น ๆ อีกมาก ใช้ `FileType.GetSupportedFileFormats()` เพื่อดูรายการเต็ม

## แหล่งข้อมูล
- [เอกสาร](https://docs.groupdocs.com/redaction/net/)
- [อ้างอิง API](https://reference.groupdocs.com/redaction/net)
- [ดาวน์โหลด GroupDocs.Redaction](https://releases.groupdocs.com/redaction/net/)
- [ฟอรั่มสนับสนุนฟรี](https://forum.groupdocs.com/c/redaction/33)
- [ใบอนุญาตชั่วคราว](https://purchase.groupdocs.com/temporary-license/)

**อัปเดตล่าสุด:** 2026-07-20  
**ทดสอบกับ:** GroupDocs.Redaction 4.2.0 for .NET  
**ผู้เขียน:** GroupDocs  

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

```csharp
using GroupDocs.Redaction;
// Initialize the Redactor with file path
Redactor redactor = new Redactor("sample.pdf");
```

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using GroupDocs.Redaction;

// Step 1: Use GroupDocs.Redaction API to fetch all supported formats.
IEnumerable<FileType> supportedFileTypes = FileType.GetSupportedFileFormats().OrderBy(f => f.Extension);
```

```csharp
// Step 2: Loop through the list of file types and print details.
foreach (FileType fileType in supportedFileTypes)
{
    Console.WriteLine($"{fileType.Extension} - {fileType.FileFormatName}");
}
```

## บทแนะนำที่เกี่ยวข้อง

- [บทแนะนำการจัดการรูปแบบสำหรับ GroupDocs.Redaction .NET](/redaction/net/format-handling/)
- [บทแนะนำการโหลดเอกสารด้วย GroupDocs.Redaction สำหรับ .NET](/redaction/net/document-loading/)
- [บทแนะนำการบันทึกเอกสารสำหรับ GroupDocs.Redaction .NET](/redaction/net/document-saving/)